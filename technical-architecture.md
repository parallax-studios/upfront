# UPFRONT — Technical Architecture Document

**Author**: BYTE (Lead Programmer)
**Version**: 1.0
**Date**: 2026-02-07
**Status**: Production-Ready Technical Blueprint

---

> "The best architecture is invisible. You never see it — you just feel the game respond."

I've read the pitch and the design doc. I know what this game is: a management sim where the core verb is *negotiate*, not *build*. The technical challenge is making a turn-based negotiation system feel like a conversation, a procedural content generator feel hand-crafted, and a year-long session feel like a story.

This is not an unsolved problem. The solutions are known. The risks are known. What follows is how we build it, what it costs, and where it breaks.

Ship it, then improve it. Let's go.

---

## 1. ENGINE RECOMMENDATION

### 1.1 Chosen Engine: **Unity 2023.2 LTS**

**Rationale**:

- **UI-heavy game, not performance-critical**: UPFRONT is 90% UI interactions. No physics. No real-time combat. No massive open world. The bottleneck is UI rendering and data flow, not GPU compute.
- **UI Toolkit maturity**: Unity's UI Toolkit (runtime + editor) is production-ready as of 2023.2 LTS. We need nested menus, animated transitions, data binding, and complex layouts. UI Toolkit delivers.
- **Rapid iteration on data-driven systems**: The Concept Forge, Brief System, and Gauntlet all depend on JSON-driven config. Unity handles JSON deserialization natively and has robust tooling for content iteration.
- **Cross-platform out of the box**: Primary is PC (Steam). Switch port is stretch. Unity handles both with minimal platform-specific code.
- **Team familiarity**: Unity is the known quantity. A solo or small team (2-4 devs) can be productive in Unity within a week. Custom engines are how projects die.

**Alternatives considered and rejected**:

| Engine | Why Not |
|--------|---------|
| **Godot 4.x** | UI Toolkit is less mature than Unity's. Export pipeline for Switch is unproven. Stronger for 2D games; this is a UI sim. |
| **Unreal Engine 5** | Massive overkill. UMG (Unreal's UI system) is powerful but heavyweight. Blueprint spaghetti risk is high for data-heavy systems. Build times would kill iteration speed. |
| **Custom Engine** | I will not make that mistake again. 18 months of engine dev and the game never shipped. Unity ships. |
| **Web (React/Electron)** | Seriously considered. Web gives instant cross-platform and UI tooling is best-in-class. Rejected because Steam integration (achievements, cloud saves, controller support) is clunky via Steamworks4JS. Also: performance on lower-end PCs is worse than native. |

**Verdict**: Unity 2023.2 LTS. It is boring. It works. Ship the game on a boring stack.

---

### 1.2 Tech Stack

| Layer | Technology | Rationale |
|-------|-----------|-----------|
| **Engine** | Unity 2023.2 LTS | (see above) |
| **UI Framework** | UI Toolkit (runtime) | Modern, performant, UXML + USS is closer to web dev than IMGUI/UGUI. Easier to iterate. |
| **Data Serialization** | JSON via Newtonsoft.Json | Human-readable, designer-friendly, diff-able in git. |
| **State Management** | Custom FSM + Event Bus | State machines for campaign flow, Gauntlet rounds. Event bus for decoupled system communication. |
| **Save System** | JSON + delta compression | (see section 6) |
| **AI/Simulation** | Rule-based systems, no ML | Client behavior in Gauntlet is deterministic given inputs. Procedural generation uses weighted tables + seeded RNG. |
| **Audio** | FMOD Studio | Better middleware than Unity's built-in. Dynamic music layers for Gauntlet tension. Event-driven sound. |
| **Version Control** | Git + LFS | Lock binary assets (audio, UI mockups). Code and JSON are diffable. |
| **Build Pipeline** | Unity Cloud Build or local Jenkins | Automated builds on commit. Target: sub-10-minute iteration time. |
| **Localization** | Unity Localization package | Stretch goal for EU launch. Architected from day 1, implemented post-launch. |

---

## 2. CORE SYSTEMS ARCHITECTURE

### 2.1 System Overview

The game is structured around **five core systems** that communicate via an event bus. Each system owns its domain and exposes a public API.

```
┌─────────────────────────────────────────────────────────────┐
│                      GAME DIRECTOR                          │
│  (Session manager, calendar, year progression)              │
└────────────┬────────────────────────────────────────────────┘
             │
             │ Events: NewBrief, CampaignComplete, QuarterEnd
             │
       ┌─────▼──────┐
       │ EVENT BUS  │───────────────────────┐
       └─────┬──────┘                       │
             │                              │
    ┌────────┴────────────────────┬─────────┴────────┬─────────────┐
    │                             │                  │             │
┌───▼────────┐          ┌─────────▼────────┐   ┌────▼─────┐  ┌───▼──────┐
│   BRIEF    │          │   TEAM MANAGER   │   │ CONCEPT  │  │ APPROVAL │
│   SYSTEM   │          │   (Chemistry)    │   │  FORGE   │  │ GAUNTLET │
└────────────┘          └──────────────────┘   └──────────┘  └──────────┘
     │                           │                   │              │
     │                           │                   │              │
     └───────────────────────────┴───────────────────┴──────────────┘
                                 │
                        ┌────────▼─────────┐
                        │ PRODUCTION       │
                        │ PIPELINE         │
                        └────────┬─────────┘
                                 │
                        ┌────────▼─────────┐
                        │ BROADCAST &      │
                        │ REACTION ENGINE  │
                        └────────┬─────────┘
                                 │
                        ┌────────▼─────────┐
                        │ REPUTATION &     │
                        │ ECONOMY SYSTEM   │
                        └──────────────────┘
```

**Data Flow Example** (one campaign cycle):

1. `GameDirector` fires `NewBriefAvailable` event → `BriefSystem` generates brief → stores in `BriefLibrary`
2. Player clicks "Staff Project" → `TeamManager` validates roster → assigns team → fires `TeamAssigned` event
3. `ConceptForge` receives `TeamAssigned` → generates 2-3 concepts → fires `ConceptsReady` event
4. Player selects concept → `ApprovalGauntlet` initializes with selected concept + client data → Gauntlet FSM starts
5. Gauntlet completes (approved or walked) → fires `CampaignApproved` or `CampaignKilled` event
6. If approved: `ProductionPipeline` receives event → player allocates budget → fires `ProductionComplete`
7. `BroadcastEngine` receives `ProductionComplete` → calculates audience score → fires `AdAired` event
8. `ReputationSystem` receives `AdAired` → updates metrics → fires `MetricsUpdated` → UI refreshes

The event bus decouples systems. The Brief System does not know the Gauntlet exists. The Gauntlet does not know the Broadcast Engine exists. Each system is testable in isolation. This is critical: we can prototype the Gauntlet as a standalone scene with mock data and no dependency on the Brief System.

---

### 2.2 Component Diagram

Each system is implemented as a **manager singleton** (I know, singletons are controversial — but for a UI-heavy sim with one active game state, they work). Alternatively, use a **service locator pattern** if the team prefers testability over convenience.

**Key classes**:

```csharp
// Core game loop
public class GameDirector : MonoBehaviour
{
    public CalendarData CurrentCalendar { get; private set; }
    public void AdvanceToNextQuarter();
    public void TriggerSuperBowl();
}

// Brief generation
public class BriefSystem
{
    public Brief GenerateBrief(int agencyReputation, int currentYear);
    public List<Brief> GetAvailableBriefs();
}

// Team and chemistry
public class TeamManager
{
    public List<Creative> Roster { get; private set; }
    public TeamChemistry CalculateChemistry(Creative[] team);
    public void AssignTeamToBrief(Brief brief, Creative[] team);
}

// Concept generation
public class ConceptForge
{
    public List<Concept> GenerateConcepts(Brief brief, Creative[] team, TeamChemistry chemistry);
    public Concept RefineConceptWithRevision(Concept original, StatAdjustment adjustment);
}

// Approval negotiation
public class ApprovalGauntlet
{
    public void StartGauntlet(Concept concept, ClientData client);
    public GauntletResult ResolvePlayerChoice(PlayerResponse response);
    public bool IsGauntletComplete { get; }
}

// Production budget allocation
public class ProductionPipeline
{
    public void AllocateBudget(Concept concept, BudgetAllocation allocation);
    public Concept ApplyProductionModifiers(Concept concept, BudgetAllocation allocation);
}

// Audience simulation
public class BroadcastEngine
{
    public AudienceReaction SimulateBroadcast(Concept finalConcept, CulturalContext context);
    public void DisplayReactionUI(AudienceReaction reaction);
}

// Meta progression
public class ReputationSystem
{
    public AgencyReputation CurrentReputation { get; private set; }
    public void UpdateReputation(CampaignResult result);
    public List<ClientTier> GetUnlockedTiers();
}

public class EconomySystem
{
    public float CurrentCash { get; private set; }
    public void ProcessMonthlyExpenses();
    public void AddRevenue(float amount, RevenueSource source);
}
```

**Data structures**:

```csharp
[Serializable]
public class Brief
{
    public string BriefID;
    public BrandArchetype Archetype;
    public CampaignGoal Goal;
    public int BudgetCeiling;
    public TargetDemo TargetDemo;
    public List<string> NonNegotiables;
    public HiddenPriority HiddenPriority; // not shown to player
    public int RiskTolerance; // 1-10
}

[Serializable]
public class Creative
{
    public string Name;
    public int Vision;        // 1-10
    public int Craft;         // 1-10
    public int Speed;         // 1-10
    public int Ego;           // 1-10
    public List<TasteTag> TasteTags; // e.g. Funny, Emotional
    public int Ambition;      // 1-10
    public int CurrentMorale; // affects performance
}

[Serializable]
public class Concept
{
    public string ConceptID;
    public int ProductionValue; // 1-100
    public int Humor;           // 1-100
    public int Emotion;         // 1-100
    public int Originality;     // 1-100
    public int BrandClarity;    // 1-100
    public ToneType Tone;
    public HookType Hook;
    public int ProductionAmbition; // 1-5
    public int CulturalRisk;      // 1-10
    public string Logline; // generated from template
}

[Serializable]
public class ClientData
{
    public string ClientID;
    public BrandArchetype Archetype;
    public int RiskTolerance;
    public int ClientTrust; // builds over multiple campaigns
    public List<ClientNote> AvailableNotes; // weighted by archetype
}

[Serializable]
public class GauntletState
{
    public int CurrentRound;
    public int RemainingPushbackPoints;
    public Concept CurrentConcept; // mutable during Gauntlet
    public List<ClientNote> ActiveNotes; // notes issued this round
    public float ClientTrustDelta; // cumulative change this Gauntlet
    public float CreativeIntegrityDelta;
}
```

---

### 2.3 State Machine: Campaign Flow

Each campaign is a state machine. This makes the flow explicit and debuggable.

```
START
  │
  ├──> BRIEFING (player reads brief)
  │
  ├──> STAFFING (player assigns team)
  │
  ├──> CONCEPT_GENERATION (Forge generates concepts)
  │
  ├──> CONCEPT_SELECTION (player picks one)
  │
  ├──> APPROVAL_GAUNTLET (negotiation rounds)
  │       │
  │       ├──> APPROVED ──────┐
  │       │                   │
  │       └──> WALKED_AWAY ───┼──> CAMPAIGN_ENDED
  │                            │
  ├──> PRODUCTION (budget allocation) <─┘
  │
  ├──> BROADCAST (ad airs, reaction simulated)
  │
  └──> RESULTS (metrics update, campaign complete)
       │
       └──> CAMPAIGN_ENDED
```

Implementation:

```csharp
public enum CampaignState
{
    Briefing,
    Staffing,
    ConceptGeneration,
    ConceptSelection,
    ApprovalGauntlet,
    Production,
    Broadcast,
    Results,
    Ended
}

public class Campaign
{
    public CampaignState CurrentState { get; private set; }
    public Brief Brief;
    public Creative[] AssignedTeam;
    public Concept SelectedConcept;
    public GauntletResult GauntletOutcome;

    public void TransitionTo(CampaignState newState)
    {
        // State exit logic
        OnExitState(CurrentState);

        CurrentState = newState;

        // State entry logic
        OnEnterState(CurrentState);
    }

    private void OnEnterState(CampaignState state)
    {
        switch(state)
        {
            case CampaignState.ConceptGeneration:
                var concepts = ConceptForge.Instance.GenerateConcepts(Brief, AssignedTeam, chemistry);
                EventBus.Publish(new ConceptsReadyEvent(concepts));
                break;
            case CampaignState.ApprovalGauntlet:
                ApprovalGauntlet.Instance.StartGauntlet(SelectedConcept, Brief.ClientData);
                break;
            // etc.
        }
    }
}
```

**Why a state machine**: The campaign flow is linear with conditional branches. A state machine makes the flow self-documenting. Debugging is trivial: "The campaign is stuck in ConceptSelection state — why didn't it transition to ApprovalGauntlet?" The log shows the event that failed to fire. FSMs are boring. Boring is good.

---

### 2.4 Event Bus Architecture

The event bus is a lightweight pub/sub system. Systems subscribe to events they care about. Systems publish events when their state changes. No system directly references another system.

```csharp
public static class EventBus
{
    private static Dictionary<Type, List<Delegate>> eventSubscribers = new();

    public static void Subscribe<T>(Action<T> handler) where T : IEvent
    {
        var eventType = typeof(T);
        if (!eventSubscribers.ContainsKey(eventType))
            eventSubscribers[eventType] = new List<Delegate>();

        eventSubscribers[eventType].Add(handler);
    }

    public static void Unsubscribe<T>(Action<T> handler) where T : IEvent
    {
        var eventType = typeof(T);
        if (eventSubscribers.ContainsKey(eventType))
            eventSubscribers[eventType].Remove(handler);
    }

    public static void Publish<T>(T eventData) where T : IEvent
    {
        var eventType = typeof(T);
        if (!eventSubscribers.ContainsKey(eventType))
            return;

        foreach (var handler in eventSubscribers[eventType])
        {
            (handler as Action<T>)?.Invoke(eventData);
        }
    }
}

// Example events
public interface IEvent { }

public struct ConceptsReadyEvent : IEvent
{
    public List<Concept> Concepts;
}

public struct GauntletCompleteEvent : IEvent
{
    public GauntletResult Result;
    public Concept FinalConcept;
}

public struct AdAiredEvent : IEvent
{
    public AudienceReaction Reaction;
    public CampaignResult Result;
}
```

**Why an event bus**: Decoupling. The Gauntlet does not need to know what happens after it completes — it just publishes `GauntletCompleteEvent`. The Production Pipeline subscribes to that event and starts its work. Add a new system later (e.g., a News Feed that reacts to controversial ads)? Subscribe to `AdAiredEvent`. No refactoring.

**Performance**: For a UI sim with ~20 events per campaign and max 5 simultaneous campaigns, event bus overhead is negligible. Profile if you see >1ms spent in EventBus.Publish per frame.

---

## 3. KEY GAMEPLAY SYSTEMS: TECHNICAL DESIGN

### 3.1 The Brief System

**Design Goal**: Generate procedurally varied briefs from a finite content library. Target: 100+ unique briefs from 50 content chunks.

**Implementation**:

Briefs are assembled from **JSON templates** with **weighted random selection**:

```json
{
  "brandArchetypes": [
    {
      "id": "corporate_titan",
      "name": "MegaCorp Industries",
      "riskToleranceRange": [1, 4],
      "budgetRange": [800000, 3000000],
      "preferredGoals": ["brand_awareness", "brand_clarity"],
      "commonNotes": ["de_risk_01", "brand_police_02", "scope_creep_03"],
      "flavorTextTemplates": [
        "We're launching a new product line targeting {demo}. The board wants safe but memorable.",
        "After last quarter's results, we need a win. Think bold, but not too bold."
      ]
    }
  ],
  "campaignGoals": [
    {"id": "brand_awareness", "name": "Brand Awareness", "statPriority": "Originality"},
    {"id": "perception_repair", "name": "Brand Perception Repair", "statPriority": "Emotion"}
  ],
  "nonNegotiables": [
    {"id": "must_include_mascot", "text": "Must prominently feature the brand mascot"},
    {"id": "no_humor", "text": "Humor is off-brand for us"}
  ]
}
```

**Generation algorithm**:

```csharp
public Brief GenerateBrief(int agencyReputation, int currentYear)
{
    // 1. Select archetype weighted by agency reputation
    //    Higher rep unlocks higher tiers
    var availableTiers = GetUnlockedTiers(agencyReputation);
    var archetype = WeightedRandom.Select(availableTiers);

    // 2. Select goal based on archetype preferences
    var goal = WeightedRandom.Select(archetype.PreferredGoals);

    // 3. Determine budget (higher rep = higher budgets)
    var budgetMultiplier = 1.0f + (agencyReputation / 100f);
    var budget = Random.Range(archetype.BudgetRange.Min, archetype.BudgetRange.Max) * budgetMultiplier;

    // 4. Add 0-3 non-negotiables based on archetype conservatism
    var nonNegotiables = new List<string>();
    var nonNegCount = archetype.RiskTolerance < 4 ? Random.Range(2, 4) : Random.Range(0, 2);
    for (int i = 0; i < nonNegCount; i++)
    {
        nonNegotiables.Add(WeightedRandom.Select(contentLibrary.NonNegotiables).ID);
    }

    // 5. Assign hidden priority based on current year events
    var hiddenPriority = DetermineHiddenPriority(currentYear, archetype);

    // 6. Generate flavor text from template
    var template = Random.Select(archetype.FlavorTextTemplates);
    var flavorText = PopulateTemplate(template, goal, targetDemo);

    return new Brief
    {
        BriefID = GenerateID(),
        Archetype = archetype,
        Goal = goal,
        BudgetCeiling = budget,
        TargetDemo = SelectTargetDemo(archetype),
        NonNegotiables = nonNegotiables,
        HiddenPriority = hiddenPriority,
        RiskTolerance = Random.Range(archetype.RiskToleranceRange.Min, archetype.RiskToleranceRange.Max),
        FlavorText = flavorText
    };
}
```

**Content authoring workflow**:

1. Designer edits `briefs_config.json` to add archetypes, goals, non-negotiables.
2. Designer runs an in-editor "Brief Generator Test" tool that generates 50 briefs and displays them in a list.
3. Designer verifies variety (no repeated patterns) and tweaks weights.
4. No code changes required.

**Estimated content volume**:

- 8 archetypes x 10 flavor text templates each = 80 base templates
- 5 goals x 6 target demos = 30 combinations
- 20 non-negotiables (0-3 per brief) = ~8,000 possible constraint sets
- **Result**: Effectively infinite variety for a 20-hour game. The player will not see a "repeated brief" within a career.

---

### 3.2 Team Chemistry Engine

**Design Goal**: Team composition should produce measurably different outputs. The player should *feel* the difference between a Synergy team and a Friction team.

**Implementation**:

Chemistry is calculated when a team is assigned to a brief. The result is a `TeamChemistry` object that modifies concept generation.

```csharp
public class TeamChemistry
{
    public float Cohesion; // 0-100
    public float SpeedModifier; // 0.5 - 1.5x
    public float QualityVariance; // 0 - 30 (higher = more random)
    public List<string> SpecialTraits; // e.g., "Brilliant Friction", "Groupthink"
}

public TeamChemistry CalculateChemistry(Creative[] team)
{
    // Base cohesion starts at 50
    float cohesion = 50f;

    // Taste alignment bonus
    var tasteTags = team.SelectMany(c => c.TasteTags).ToList();
    var sharedTags = tasteTags.GroupBy(t => t).Where(g => g.Count() > 1).Count();
    cohesion += sharedTags * 3f;

    // Average Craft bonus (polished teams work smoothly)
    var avgCraft = team.Average(c => c.Craft);
    cohesion += avgCraft * 2f;

    // Ego variance penalty
    var egoVariance = CalculateVariance(team.Select(c => c.Ego));
    cohesion -= egoVariance * 4f;

    // Ambition gap penalty
    var ambitionGap = team.Max(c => c.Ambition) - team.Min(c => c.Ambition);
    cohesion -= ambitionGap * 2f;

    // Clamp to 0-100
    cohesion = Mathf.Clamp(cohesion, 0f, 100f);

    // Derive modifiers from cohesion
    var chemistry = new TeamChemistry
    {
        Cohesion = cohesion
    };

    if (cohesion >= 70)
    {
        chemistry.SpeedModifier = 1.1f;
        chemistry.QualityVariance = 5f;
        chemistry.SpecialTraits.Add("Synergy");
    }
    else if (cohesion >= 40)
    {
        chemistry.SpeedModifier = 1.0f;
        chemistry.QualityVariance = 15f;
        chemistry.SpecialTraits.Add("Functional");
    }
    else if (cohesion >= 20)
    {
        chemistry.SpeedModifier = 0.85f;
        chemistry.QualityVariance = 30f;
        // 50% chance of "Brilliant Friction" trait
        if (Random.value > 0.5f)
            chemistry.SpecialTraits.Add("Brilliant Friction");
        else
            chemistry.SpecialTraits.Add("Friction");
    }
    else
    {
        chemistry.SpeedModifier = 0.5f;
        chemistry.QualityVariance = 40f;
        chemistry.SpecialTraits.Add("Meltdown");
    }

    return chemistry;
}
```

**Special traits**:

- **Synergy**: +15% to all concept stats. Low variance. Reliable.
- **Functional**: No bonuses. Moderate variance. Workmanlike.
- **Brilliant Friction**: +20% Originality OR -20% to one random stat (coin flip per concept). High risk/reward.
- **Meltdown**: One team member threatens to quit per week. Production halts until player takes a Morale action (costs time/money).

**UI Feedback**:

When the player is assigning a team, a real-time chemistry gauge updates as they drag creatives into slots. The gauge shows:

- Cohesion score (color-coded: blue = Synergy, amber = Functional, orange = Friction, red = Meltdown)
- Predicted trait
- Speed modifier

This gives the player immediate feedback. They can experiment with team composition and see the chemistry shift. The expert player learns to deliberately engineer Friction for high-Originality campaigns.

---

### 3.3 The Concept Forge

**Design Goal**: Generate concepts that feel unique and authored, not generic and templated. The player should read a concept and think "my team made this," not "the RNG made this."

**Implementation**:

Concepts are generated using a **template system** + **weighted stat generation** + **chemistry modifiers**.

**Concept generation steps**:

1. **Select Tone and Hook**: Weighted by team Taste tags and brief goals.
2. **Generate base stats**: Each stat (Production Value, Humor, Emotion, Originality, Brand Clarity) is calculated from team stats + chemistry.
3. **Apply brief alignment bonuses**: If concept aligns with brief goal, boost relevant stat.
4. **Apply randomness**: +/- 15 variance to simulate creative unpredictability.
5. **Generate logline**: Assemble from modular sentence templates.

**Stat generation formula** (per stat):

```csharp
float GenerateConceptStat(StatType stat, Creative[] team, TeamChemistry chemistry, Brief brief)
{
    // 1. Base from team stats
    float teamAvg = team.Average(c => GetRelevantStat(c, stat)) * 5f; // scale 1-10 to 5-50

    // 2. Chemistry modifier
    float chemistryBonus = 0f;
    if (chemistry.SpecialTraits.Contains("Synergy"))
        chemistryBonus = 15f;
    else if (chemistry.SpecialTraits.Contains("Brilliant Friction") && stat == StatType.Originality)
        chemistryBonus = 20f;

    // 3. Brief alignment bonus
    float briefBonus = 0f;
    if (IsStatAlignedWithBrief(stat, brief))
        briefBonus = 10f;

    // 4. Randomness
    float randomness = Random.Range(-15f, 15f);

    // 5. Cultural risk multiplier (affects Originality and Humor positively, Brand Clarity negatively)
    float riskMultiplier = 1.0f;
    float culturalRisk = Random.Range(1f, 10f); // TODO: make this emergent from team stats
    if (stat == StatType.Originality || stat == StatType.Humor)
        riskMultiplier = 1.0f + (culturalRisk * 0.05f);
    else if (stat == StatType.BrandClarity)
        riskMultiplier = 1.0f - (culturalRisk * 0.03f);

    float finalValue = (teamAvg + chemistryBonus + briefBonus + randomness) * riskMultiplier;

    // 6. Apply variance from chemistry
    if (chemistry.QualityVariance > 0)
        finalValue += Random.Range(-chemistry.QualityVariance, chemistry.QualityVariance);

    return Mathf.Clamp(finalValue, 1f, 100f);
}
```

**Logline generation**:

Loglines are assembled from templates with variable slots:

```json
{
  "loglineTemplates": [
    "{hook} featuring {talent}, set in {location}, with a {tone_modifier} twist.",
    "A {tone_modifier} {hook} that shows {brand_integration}, ending with {payoff}.",
    "{talent} {action_verb} through {location} while {brand_integration}, culminating in {payoff}."
  ],
  "hooks": {
    "celebrity_cameo": ["a surprise celebrity appearance", "a star-studded lineup", "a beloved icon"],
    "narrative_mini_film": ["a cinematic short film", "a heartfelt story", "an epic journey"],
    "visual_gag": ["a rapid-fire series of sight gags", "a single unbroken visual joke", "a surreal visual metaphor"]
  },
  "toneModifiers": {
    "funny": ["hilarious", "absurd", "laugh-out-loud"],
    "emotional": ["heartwarming", "tearjerking", "deeply sincere"],
    "provocative": ["edgy", "controversial", "boundary-pushing"]
  }
}
```

Example generated logline:

> "A cinematic short film featuring a retired NFL quarterback, set in the American desert, with a surreal twist."

The logline reads like a human wrote it because the templates are authored by a human. The variables inject variety.

**Concept variety**:

- 8 Tones x 8 Hooks = 64 base combinations
- 30+ logline templates
- 10+ variants per template slot
- Stats vary based on team composition (infinite permutations)

**Result**: The player will rarely see the exact same concept twice. Even if they do see "a narrative mini-film with a surreal twist," the *stats* will differ based on the team that generated it.

---

### 3.4 The Approval Gauntlet

This is the heart of the game. This is where we succeed or fail.

**Design Goal**: Make a turn-based menu system feel like a tense human negotiation. The player should feel the client's hesitation, the weight of their own pushback, and the relief when a note is withdrawn.

**Implementation**: Multi-round FSM with dynamic client AI and animated UI feedback.

**Gauntlet FSM**:

```
INIT (load client, calculate pushback points)
  │
  ├──> PRESENTATION (player presents current concept)
  │
  ├──> CLIENT_REACTION (client evaluates concept, generates notes)
  │
  ├──> PLAYER_CHOICE (player selects response: Accept, Pushback, Compromise, Walk)
  │       │
  │       ├──> [Accept] ─────> Apply stat changes ───> Next round
  │       ├──> [Pushback] ───> Persuasion check ─────> Success: note withdrawn | Failure: trust drop
  │       ├──> [Compromise] ─> Apply half stat changes > Next round
  │       └──> [Walk Away] ──> GAUNTLET_ENDED (killed)
  │
  ├──> CHECK_TERMINATION
  │       │
  │       ├──> Client satisfied (no more notes) ──> GAUNTLET_ENDED (approved)
  │       ├──> Round limit reached (3-5 rounds) ─> GAUNTLET_ENDED (approved if concept viable)
  │       └──> Pushback failed + client angry ───> GAUNTLET_ENDED (killed)
  │
  └──> Loop to PRESENTATION
```

**Client note generation**:

Each round, the client evaluates the current concept against their archetype preferences and generates 0-2 notes.

```csharp
public List<ClientNote> GenerateNotes(Concept currentConcept, ClientData client)
{
    var notes = new List<ClientNote>();

    // 1. Brand Clarity check: if below client's tolerance, issue a Brand Police note
    if (currentConcept.BrandClarity < client.MinBrandClarity)
    {
        notes.Add(SelectRandomNote(client.AvailableNotes, "brand_police"));
    }

    // 2. Cultural Risk check: if too risky for client, issue a De-Risk note
    if (currentConcept.CulturalRisk > client.RiskTolerance)
    {
        notes.Add(SelectRandomNote(client.AvailableNotes, "de_risk"));
    }

    // 3. Random "taste override" note (10% chance per round)
    if (Random.value < 0.1f)
    {
        notes.Add(SelectRandomNote(client.AvailableNotes, "taste_override"));
    }

    // 4. Cap at 2 notes per round
    if (notes.Count > 2)
        notes = notes.Take(2).ToList();

    return notes;
}
```

**Persuasion check** (when player pushes back):

```csharp
public bool AttemptPersuasion(ClientData client, AgencyReputation reputation, float creativeIntegrity)
{
    float roll = Random.Range(0f, 100f);
    float threshold = (client.RiskTolerance * 8f) + (reputation.Score / 5f) + (creativeIntegrity / 10f);

    bool success = roll <= threshold;

    // Log for debugging
    Debug.Log($"Persuasion: Roll={roll}, Threshold={threshold}, Success={success}");

    return success;
}
```

**UI/UX Critical Details**:

The Gauntlet succeeds or fails based on *presentation*. Here is what makes it feel like a conversation, not a menu:

1. **Client avatar with facial expressions**: The client is a 2D portrait with 5 expressions (neutral, pleased, concerned, frustrated, angry). Expression updates based on:
   - Concept stats alignment with preferences → pleased
   - Player accepts note → neutral/pleased
   - Player pushes back (before check) → concerned
   - Pushback succeeds → neutral
   - Pushback fails → frustrated/angry

2. **Dialogue variations**: Each note has 5+ dialogue variations. The client never says the exact same line twice. Example for "de_risk_humor":
   - "I'm not sure the humor lands with our core demo."
   - "My CEO's wife didn't laugh. She's on the board."
   - "Can we dial back the comedy? It feels off-brand."
   - "Our focus groups respond better to sincerity than jokes."
   - "The humor is clever, but I worry it distracts from the message."

3. **Pushback counter-dialogue**: When the player pushes back, the client responds with a counter-argument (if check fails) or a concession (if check succeeds). Success example:
   - "Okay. I trust you on this one. Let's keep it."

   Failure example:
   - "I hear you, but I really need you to reconsider. The board won't go for this."

4. **Animated stat changes**: When a note is accepted, the affected stat bar visually shrinks (or grows if positive). The player *sees* the compromise erode their concept.

5. **Tension escalation**: Background music intensity increases with each round. By round 4, the tension is palpable. If the player walks away, the music cuts to silence — and then a single low note. The decision should feel heavy.

**Estimated dev time for Gauntlet polish**: 3-4 weeks for core FSM + UI. 2-3 weeks for dialogue content and animation. This is the most expensive system in the game. It is also the most important. Do not cut corners here.

---

### 3.5 Production Pipeline

**Design Goal**: Fast budget allocation puzzle that respects player time. Target interaction time: 30-45 seconds.

**Implementation**:

The production phase is a single screen with five sliders representing budget categories. The player drags sliders to allocate percentage of the approved budget.

```csharp
public class BudgetAllocation
{
    public float CastingPercent;
    public float LocationPercent;
    public float VFXPercent;
    public float SoundPercent;
    public float EditPercent;

    public float Total => CastingPercent + LocationPercent + VFXPercent + SoundPercent + EditPercent;

    public bool IsValid => Mathf.Approximately(Total, 100f);
}

public Concept ApplyProductionModifiers(Concept concept, BudgetAllocation allocation, int totalBudget)
{
    var modified = concept.Clone();

    // Apply per-category bonuses
    modified.Emotion += (int)(allocation.CastingPercent / 5f) * 2;
    modified.ProductionValue += (int)(allocation.LocationPercent / 5f) * 2;
    modified.ProductionValue += (int)(allocation.VFXPercent / 5f) * 3;
    modified.Originality += (int)(allocation.VFXPercent / 5f);
    modified.Emotion += (int)(allocation.SoundPercent / 5f) * 2;
    modified.ProductionValue += (int)(allocation.SoundPercent / 5f);
    modified.BrandClarity += (int)(allocation.EditPercent / 5f) * 2;

    // Apply diminishing returns (above thresholds, bonuses halve)
    if (allocation.CastingPercent > 35f)
        modified.Emotion -= (int)((allocation.CastingPercent - 35f) / 10f);
    // ... (repeat for other categories)

    // Apply Ambition Gap penalty
    int supportedAmbition = totalBudget / 200000; // $200K per Ambition point
    int ambitionGap = concept.ProductionAmbition - supportedAmbition;
    if (ambitionGap > 0)
    {
        int penalty = ambitionGap * 8;
        modified.ProductionValue -= penalty;
        modified.Emotion -= penalty;
        modified.Humor -= penalty;
        modified.Originality -= penalty;
        modified.BrandClarity -= penalty;
    }

    // Clamp all stats to 1-100
    modified.Clamp();

    return modified;
}
```

**UI Features**:

- **Auto-suggest button**: Calculates an "optimal" allocation based on concept's stat strengths. One-click accept.
- **Real-time stat preview**: As the player drags sliders, the concept stat bars update in real-time. The player sees the impact immediately.
- **Ambition warning**: If the budget is insufficient for the concept's Ambition, a red warning appears: "Budget too low for this concept's ambition. Consider scaling down or expect penalties."

**Polish**: The production phase is intentionally shallow. It is a 30-second interstitial between the Gauntlet (high tension) and the Broadcast (high spectacle). It serves as a breather. Do not over-design it.

---

### 3.6 Broadcast & Reaction System

**Design Goal**: The spectacle moment. The player watches their work land in the simulated world. This needs to *feel* like a Super Bowl ad airing.

**Implementation**:

**Broadcast sequence** (for regular campaigns):

1. **Storyboard animatic** (left side of split-screen): A 10-15 second sequence of 4-6 still frames representing the ad. Each frame is generated from the concept's Hook and Tone.
   - Example: Narrative Mini-Film + Emotional = [Hero running] → [Hero exhausted] → [Hero drinking product] → [Hero triumphant] → [Product logo]
   - Frames are pre-authored assets tagged by Hook/Tone. Concept's stats determine which frames are selected.

2. **America Reacts panel** (right side): Simulated viewer faces (8-12 portraits) with animated reactions:
   - Laughter (if Humor > 60)
   - Confusion (if Brand Clarity < 40)
   - Tears (if Emotion > 70)
   - Boredom (if all stats < 50)
   - Anger (if Cultural Risk > 8 and polarization triggered)

3. **Discourse ticker** (bottom): Scrolling simulated social media posts:
   - Generated from templates: "What was that even for?", "I'm crying", "Best ad of the year", "This is offensive"
   - Posts are weighted by Audience Score and Polarization result

4. **Audience Score reveal**: After 15 seconds, the Audience Score ticks up from 0 to final value over 3 seconds. Suspense.

**Super Bowl sequence** (amplified version):

- All of the above, but:
  - Storyboard is 20-25 seconds (longer ad).
  - America Reacts panel has 20 faces instead of 8.
  - Discourse ticker is faster and denser.
  - After Audience Score reveal, a "viral spread" animation shows the ad spreading across a map of the US.
  - Post-game: Monday Morning meeting cutscene with client. Client's dialogue is dynamically generated based on results.

**Audience Score calculation**:

(See section 3.6 in design doc for formula. Implemented as written.)

**Polarization system**:

```csharp
public void CheckPolarization(Concept concept, out bool isPolarizing, out PolarizationResult result)
{
    isPolarizing = concept.Originality > 70 || concept.CulturalRisk > 7;

    if (!isPolarizing)
    {
        result = PolarizationResult.None;
        return;
    }

    float roll = Random.Range(0f, 100f);

    if (roll > 85f)
        result = PolarizationResult.ControversyEvent; // Media coverage, client panic
    else if (roll > 60f)
        result = PolarizationResult.SplitOpinion; // Brand Trust splits by demo
    else
        result = PolarizationResult.None; // Risky but not controversial
}
```

**Asset requirements**:

- 64 storyboard frames (8 Hooks x 8 Tones = 64 combinations). Each frame is a single illustrated still.
- 20 viewer portrait variations (different ages, genders, expressions).
- 100+ discourse templates (positive, negative, confused, memetic).
- Background music: 3 intensity layers (low/med/high) that cross-fade based on Audience Score.

**Estimated production time**: 4 weeks for system + UI. 2-3 weeks for asset creation (if art is contracted out).

---

## 4. AI / SIMULATION SYSTEMS

### 4.1 Client AI (The Approval Gauntlet)

UPFRONT does not use machine learning. The "AI" is rule-based and deterministic given inputs. This is correct. ML would be overkill and unpredictable.

**Client behavior model**:

Each client archetype has:
- **Risk Tolerance** (1-10): Affects note generation frequency and persuasion thresholds.
- **Stat Preferences**: Which concept stats the client values most.
- **Note Pool**: Weighted list of available notes the client can issue.
- **Trust Decay Rate**: How quickly Client Trust erodes on pushback failure.

**Client evaluation each round**:

```csharp
public ClientReaction EvaluateConcept(Concept concept, ClientData client, int round)
{
    var reaction = new ClientReaction();

    // 1. Calculate overall satisfaction
    float satisfaction = 0f;
    satisfaction += concept.BrandClarity * client.BrandClarityWeight;
    satisfaction += concept.ProductionValue * client.ProductionValueWeight;
    // ... (weighted sum of stats based on archetype)

    reaction.SatisfactionScore = satisfaction;

    // 2. Determine if termination conditions met
    if (satisfaction > 70f && round >= 2)
    {
        reaction.IsTerminal = true;
        reaction.Outcome = GauntletOutcome.Approved;
        return reaction;
    }

    // 3. Generate notes if dissatisfied
    if (satisfaction < 60f || concept.CulturalRisk > client.RiskTolerance)
    {
        reaction.Notes = GenerateNotes(concept, client);
    }

    // 4. Check for walk-out (if trust too low and pushback failed last round)
    if (client.ClientTrust < 20f && round > 2)
    {
        reaction.IsTerminal = true;
        reaction.Outcome = GauntletOutcome.ClientWalkout;
    }

    return reaction;
}
```

**Why rule-based is better than ML**:

- Predictable: Playtesting can validate that client archetypes behave as designed.
- Debuggable: If a client is too harsh, tweak their RiskTolerance value.
- Transparent to player: The expert player learns client patterns. "Corporate Titans always push for Brand Clarity above 60." That skill development is impossible with a black-box ML model.
- No training data required: We do not have 10,000 real client-creative negotiations to train on.

---

### 4.2 Audience Simulation

**Design Goal**: Simulate how the American public reacts to an ad without modeling individual agents (computationally expensive and unnecessary).

**Implementation**: Aggregate formula with demographic breakdown.

Audience is segmented into 6 demos (see design doc section 3.1). Each demo has stat preferences:

| Demo | Preferred Stats |
|------|-----------------|
| Youth 18-24 | Humor, Originality |
| Young Adult 25-34 | Originality, Production Value |
| Family 35-49 | Emotion, Brand Clarity |
| Affluent 35-54 | Production Value, Emotion |
| Mass Market | Brand Clarity, Humor |
| Niche | Originality, Emotion |

Audience Score is calculated per demo, then weighted by demo size:

```csharp
public AudienceReaction SimulateAudience(Concept concept, TargetDemo targetDemo, CulturalContext context)
{
    var reaction = new AudienceReaction();

    // Calculate score per demo
    var demoScores = new Dictionary<TargetDemo, float>();
    foreach (var demo in DemoLibrary.AllDemos)
    {
        float score = CalculateDemoScore(concept, demo, context);
        demoScores[demo] = score;
    }

    // Weighted average based on demo sizes
    float overallScore = 0f;
    foreach (var kvp in demoScores)
    {
        overallScore += kvp.Value * kvp.Key.PopulationWeight;
    }

    // Bonus if target demo matches
    if (demoScores.ContainsKey(targetDemo) && demoScores[targetDemo] > 60f)
        overallScore += 10f;

    reaction.OverallScore = Mathf.Clamp(overallScore, 0f, 100f);
    reaction.DemoBreakdown = demoScores;

    // Check polarization
    CheckPolarization(concept, out reaction.IsPolarizing, out reaction.PolarizationResult);

    return reaction;
}

private float CalculateDemoScore(Concept concept, DemoData demo, CulturalContext context)
{
    float score = 0f;

    // Weighted stat matching
    score += concept.GetStat(demo.PreferredStat1) * 0.3f;
    score += concept.GetStat(demo.PreferredStat2) * 0.3f;
    score += concept.ProductionValue * 0.2f; // everyone appreciates polish
    score += concept.BrandClarity * 0.1f;
    score += concept.Originality * 0.1f;

    // Cultural fit modifier
    if (concept.Tone == context.TrendingTone)
        score += 15f;

    // Randomness
    score += Random.Range(-10f, 10f);

    return Mathf.Clamp(score, 0f, 100f);
}
```

**Cultural Context System** (Stretch Goal):

Tracks the zeitgeist year-to-year. Implementation:

```csharp
public class CulturalContext
{
    public int Year;
    public ToneType TrendingTone; // what's "hot" this year
    public float IronyIndex; // 0-100, how much ironic detachment is acceptable
    public List<CulturalEvent> RecentEvents; // e.g., 9/11 shifts tone
}

public void UpdateCulturalContext(int year)
{
    // Scripted shifts for narrative years
    if (year == 2001)
    {
        context.TrendingTone = ToneType.Earnest; // post-9/11 shift
        context.IronyIndex = 30f; // irony drops
    }
    else if (year >= 2003)
    {
        context.TrendingTone = ToneType.Ironic;
        context.IronyIndex = Mathf.Min(context.IronyIndex + 5f, 80f); // irony rises
    }

    // Random micro-shifts each year (±10%)
    context.IronyIndex += Random.Range(-5f, 5f);
}
```

If stretch goal is cut: Cultural Context is static (year 2003 defaults). Game still works without it.

---

### 4.3 Rival Agencies (Stretch Goal)

**Design Goal**: AI competitors that pursue Super Bowl slots, win awards, and poach your talent.

**Implementation**: Each rival is a simplified version of the player agency.

```csharp
public class RivalAgency
{
    public string Name;
    public AgencyArchetype Archetype; // Safe Corporate, Reckless Creative, Boutique Trendy
    public float Reputation;
    public List<ClientData> Clients;

    // Rivals do not simulate full campaigns — outcomes are abstracted
    public void SimulateYear(int year)
    {
        // Each rival completes 3-5 campaigns per year
        int campaignCount = Random.Range(3, 6);
        for (int i = 0; i < campaignCount; i++)
        {
            var result = SimulateCampaign(year);
            if (result.IsSuccessful)
                Reputation += Random.Range(2f, 5f);
            else
                Reputation -= Random.Range(1f, 3f);
        }

        // Rivals bid on Super Bowl slots
        if (Reputation > 50f)
            AttemptSuperBowlBid(year);
    }

    private CampaignResult SimulateCampaign(int year)
    {
        // Roll dice weighted by archetype
        // Safe Corporate: 70% success rate, low Originality
        // Reckless Creative: 50% success rate, high Originality
        // Boutique Trendy: 60% success rate, matches cultural trends

        float successChance = Archetype.BaseSuccessRate;
        bool success = Random.value < successChance;

        return new CampaignResult { IsSuccessful = success };
    }
}
```

**Player-facing impact**:

- Rivals appear in the "Industry News" feed: "BoldCraft Agency wins Cannes Grand Prix."
- Rivals compete in Super Bowl media auction (raises price).
- Rivals poach your creatives (if your morale is low and rival reputation is high).

**Cut if time is tight**: Rivals add flavor but are not essential to core loop. Focus on player agency first.

---

## 5. SAVE SYSTEM DESIGN

### 5.1 Save Format

**Approach**: JSON serialization with delta compression for autosaves.

**Why JSON**:

- Human-readable (easier debugging).
- Diff-able in git (designer can inspect save file changes).
- Cross-platform compatible.
- Unity's JsonUtility handles serialization automatically for [Serializable] classes.

**What gets saved**:

```csharp
[Serializable]
public class SaveData
{
    public int SaveVersion; // for forward compatibility
    public string AgencyName;
    public int CurrentYear;
    public int CurrentQuarter;
    public float CurrentCash;
    public AgencyReputation Reputation;
    public List<Creative> Roster;
    public List<ClientData> ActiveClients;
    public List<CampaignSaveData> ActiveCampaigns;
    public List<HistoricalEvent> AgencyHistory; // past campaigns, awards, key moments
    public Dictionary<string, float> RelationshipScores; // client trust, creative loyalty
    public CulturalContext CurrentContext;
    public PlayerStats Stats; // total campaigns, Super Bowl wins, awards, etc.
}

[Serializable]
public class CampaignSaveData
{
    public string CampaignID;
    public Brief Brief;
    public CampaignState CurrentState;
    public Creative[] AssignedTeam;
    public Concept SelectedConcept;
    public GauntletState GauntletState; // if currently in Gauntlet
}
```

---

### 5.2 Save Strategy

**Autosave triggers**:

- End of each quarter (4 times per year).
- After each campaign completes (broadcast results finalized).
- After Super Bowl Sunday.

**Autosave slots**: 3 rotating slots. Each save includes timestamp and year/quarter label.

**Manual save**: Player can save at any time from the pause menu. Unlimited manual save slots (stored as separate files).

**Cloud save** (via Steam Cloud):

- Enabled by default.
- Syncs save files to Steam Cloud on game exit.
- Max save size: ~5MB per save (JSON text compresses well).

---

### 5.3 Delta Compression (Optional Optimization)

If save file size becomes an issue (unlikely for a UI sim), implement delta saves:

- Full save written on year start.
- Each quarter, save only *changed* data (e.g., campaign states, cash).
- On load, apply deltas sequentially to reconstruct state.

Estimated save file size without compression: ~500KB per save. With text compression (gzip): ~150KB. Not worth optimizing unless save/load times exceed 2 seconds (profile before optimizing).

---

### 5.4 Save Compatibility

**Problem**: Game updates may change save format (new fields, removed systems).

**Solution**: Save versioning + migration system.

```csharp
public SaveData LoadSave(string filePath)
{
    string json = File.ReadAllText(filePath);
    var rawData = JsonUtility.FromJson<SaveData>(json);

    // Check version
    if (rawData.SaveVersion < CURRENT_SAVE_VERSION)
    {
        rawData = MigrateSave(rawData, rawData.SaveVersion, CURRENT_SAVE_VERSION);
    }

    return rawData;
}

private SaveData MigrateSave(SaveData oldData, int fromVersion, int toVersion)
{
    // Apply incremental migrations
    if (fromVersion < 2)
    {
        // Migration 1 -> 2: Added CulturalContext field
        oldData.CurrentContext = new CulturalContext { Year = oldData.CurrentYear };
    }

    if (fromVersion < 3)
    {
        // Migration 2 -> 3: Added PlayerStats tracking
        oldData.Stats = GenerateStatsFromHistory(oldData.AgencyHistory);
    }

    oldData.SaveVersion = toVersion;
    return oldData;
}
```

**Versioning policy**:

- Minor updates (bug fixes, balance tweaks): No version increment. Saves are forward-compatible.
- Major updates (new systems, changed data structures): Increment version, write migration.
- Breaking changes (removed systems): Increment version, write migration or warn player save is incompatible.

---

## 6. PERFORMANCE BUDGET & OPTIMIZATION STRATEGY

### 6.1 Performance Targets

| Platform | Target Framerate | Target Load Time | Target Memory |
|----------|-----------------|------------------|---------------|
| **PC (Steam)** | 60 FPS (1080p), 120 FPS (high-end) | < 5 sec to main menu, < 3 sec to load save | < 2GB RAM |
| **Nintendo Switch** | 30 FPS (docked), 30 FPS (handheld) | < 8 sec to main menu, < 5 sec to load save | < 1GB RAM |

**Why these targets**:

- This is a UI sim, not a real-time action game. 60 FPS on PC is table stakes. 30 FPS on Switch is acceptable (players do not expect high framerate for management sims).
- Load times under 5 seconds keep the session flow smooth. A player starting a new year should not wait more than 3 seconds.
- Memory budget is generous. Most assets are UI textures and JSON data. No massive 3D assets.

---

### 6.2 Performance Bottlenecks (Anticipated)

**1. UI rendering (most likely bottleneck)**:

- Problem: Complex nested UI (presentation room, storyboard animatics, reaction panels) can tank framerate if poorly optimized.
- Solution: Use UI Toolkit's GPU-based rendering. Batch draw calls. Avoid rebuilding UI every frame — update only when data changes (event-driven UI updates, not Update() polling).
- Profile target: UI rendering should take < 5ms per frame at 1080p.

**2. Concept generation (potential spike during team assignment)**:

- Problem: Generating 2-3 concepts involves hundreds of calculations (stat generation, chemistry, logline assembly). If done synchronously, causes a frame hitch.
- Solution: Run concept generation on a background thread or coroutine. Display a "Concepts brewing..." animation (1 second) while generation completes.
- Profile target: Concept generation < 100ms per concept.

**3. Save/load (potential long load times)**:

- Problem: Deserializing large JSON files can block the main thread.
- Solution: Load save data asynchronously. Display a loading screen with progress bar. Target: < 500ms to deserialize a 500KB save file.

**4. Storyboard animatics (potential GPU overhead)**:

- Problem: Displaying 4-6 animated frames with transitions could cause overdraw if frames are full-screen textures.
- Solution: Use sprite atlases. Render frames at native resolution (1920x1080 max). Avoid alpha blending where possible.

---

### 6.3 Optimization Strategy

**Phase 1 (Prototype, Months 1-3): No optimization. Build systems. Profile nothing.**

- Premature optimization is the root of all evil. Get the game working first. Make it fun. Measure nothing.

**Phase 2 (Vertical Slice, Months 4-6): Profile hot paths. Identify bottlenecks.**

- Use Unity Profiler to capture a full campaign cycle (brief to broadcast).
- Identify any frame where CPU time > 16ms (60 FPS budget) or GPU time > 16ms.
- Fix obvious bottlenecks (e.g., UI rebuilding every frame, unnecessary allocations in tight loops).

**Phase 3 (Alpha, Months 7-9): Optimize critical paths. Hit performance targets.**

- Focus on Gauntlet UI (the system players spend the most time in). Ensure it never drops below 60 FPS on target PC spec.
- Optimize save/load to hit < 3 second target.
- Run memory profiler. Identify leaks (common in Unity: event subscribers not unsubscribed, abandoned UI objects not destroyed).

**Phase 4 (Beta, Months 10-11): Platform-specific optimization (if Switch port is active).**

- Switch has 4GB RAM total, ~2GB available to game. Profile memory usage on Switch dev kit.
- Reduce texture resolution for UI elements if needed.
- Lower audio quality (compress to OGG Vorbis at 128kbps instead of 256kbps).

**Phase 5 (Release Candidate, Month 12): Final polish. Stress test.**

- Run 10+ full careers (50+ hours of play). Monitor for frame drops, memory leaks, crashes.
- Fix all crash bugs. Tolerate minor frame drops in non-critical moments (e.g., year-end recap screen can drop to 50 FPS if it only lasts 5 seconds).

---

### 6.4 Profiling Targets (What to Measure)

| Metric | Tool | Acceptable Range |
|--------|------|------------------|
| **Frame Time (CPU)** | Unity Profiler | < 16ms (60 FPS) on target PC |
| **Frame Time (GPU)** | Unity Profiler | < 16ms (60 FPS) on target PC |
| **Memory Usage** | Unity Profiler (Memory module) | < 1.5GB on PC, < 900MB on Switch |
| **GC Allocations** | Unity Profiler | < 10KB per frame (avoid GC spikes) |
| **Load Time** | Manual stopwatch + Debug.Log | < 5 sec cold start, < 3 sec save load |
| **Save File Size** | File system | < 1MB per save (uncompressed) |

**Red flags**:

- Frame time spikes above 33ms (visible stutter).
- GC collections during Gauntlet rounds (causes hitching during critical moment).
- Memory usage climbing over time (leak).
- Save/load taking > 5 seconds (player frustration).

Profile once per milestone. Do not profile daily — it is a waste of time during active development.

---

## 7. PLATFORM CONSIDERATIONS

### 7.1 Primary Platform: PC (Steam)

**Target Specs**:

- **Minimum**: Intel i5-4460 / Ryzen 3 1200, 4GB RAM, integrated graphics (Intel HD 4000 or equivalent), 2GB disk space
- **Recommended**: Intel i7-8700 / Ryzen 5 3600, 8GB RAM, GTX 1060 / RX 580, 3GB disk space

**Why these specs**: This is a UI-heavy game with minimal graphical demands. The minimum spec should run on a 2015-era office laptop. The recommended spec ensures 120 FPS for high-refresh-rate monitors.

**Input**: Mouse + keyboard primary. Controller support secondary (many Steam Deck players expect controller support for management sims).

**Steam integration**:

- Achievements: 30-40 achievements (e.g., "Win your first Clio", "Fire a client in the Gauntlet", "Create a Legendary Super Bowl ad").
- Cloud saves: Enabled via Steamworks API.
- Trading cards: Optional, low priority.
- Workshop: Not applicable (no user-generated content in v1).

**Localization** (Stretch):

- Launch in English.
- Post-launch: Add German, French, Spanish (EU market). All text is in JSON, so localization is straightforward.

---

### 7.2 Secondary Platform: Nintendo Switch (Post-Launch Port)

**Target**: 6-12 months post-PC launch.

**Technical considerations**:

- **Performance**: Switch is underpowered compared to PC. Target 30 FPS. Reduce UI texture resolution to 720p. Simplify particle effects (e.g., confetti in award ceremony).
- **Input**: Joy-Con + touch screen. Rebuild UI for controller navigation (cursor snapping, button prompts). Touch support for handheld mode (drag-and-drop is natural on touch).
- **Memory**: Switch has ~3GB RAM available to games. Profile memory usage and reduce texture memory if needed. Use Unity's addressables system to load assets on-demand.
- **Storage**: Switch games must fit on a 4GB cartridge (digital-only launch is cheaper). Compress audio assets. Estimated final build size: 1.5GB.

**Switch-specific features**:

- HD Rumble: Subtle rumble when pushback succeeds/fails in Gauntlet. Low priority.
- Touchscreen: Use touch for budget sliders in production phase. Natural fit.

**Nintendo approval process**: Plan for 3-6 months of certification. Nintendo is strict about performance (no crashes, consistent framerate, proper button prompts). Budget time for this.

---

### 7.3 Tertiary Platform: iPad (Premium Mobile)

**Status**: Stretch goal. Only pursue if PC launch succeeds.

**Target**: iPad Pro, iPad Air (2020+). Do not target iPhone (screen too small for dense UI).

**Technical considerations**:

- **UI scaling**: Redesign for 4:3 aspect ratio. Simplify multi-pane layouts.
- **Input**: Touch-only. Drag-and-drop for team assignment and budget allocation. Tap for menu navigation.
- **Performance**: iPads are powerful (A14 chip rivals Switch). Target 60 FPS at native resolution (2388x1668).
- **Monetization**: Premium ($14.99 upfront, no IAP). Apple Arcade is a possible distribution channel (but requires exclusive for 6 months).

---

## 8. BUILD PIPELINE & TOOLS

### 8.1 Build Pipeline

**Goal**: Fast iteration. A designer should be able to change a JSON file, rebuild, and test within 5 minutes.

**Pipeline stages**:

1. **Dev Build** (local, on-demand):
   - Triggered by developer hitting "Build" in Unity.
   - No optimization. Debug symbols enabled. Development console enabled.
   - Build time: ~2 minutes on modern PC (SSD, 8-core CPU).

2. **Playtest Build** (automated, nightly):
   - Triggered by git commit to `develop` branch.
   - Run unit tests (if any).
   - Build for Windows + macOS.
   - Upload to internal playtest server (Dropbox, Google Drive, or itch.io private page).
   - Build time: ~10 minutes (parallelized Win/Mac builds on build server).

3. **Steam Beta Build** (manual, weekly during beta):
   - Triggered by git tag (e.g., `v0.8.1-beta`).
   - Build for Windows, macOS, Linux.
   - Upload to Steam via SteamPipe.
   - Notify beta testers via Steam announcement.
   - Build time: ~20 minutes.

4. **Release Build** (manual, for launch):
   - Full optimization. Code stripping. Obfuscation (optional, low priority).
   - Build for all platforms (PC, Switch if ready).
   - QA pass on final build (full playthrough, no crashes).
   - Upload to Steam, submit to Nintendo for certification.
   - Build time: ~30 minutes.

---

### 8.2 Build Automation

**Tool**: Unity Cloud Build (easiest) or local Jenkins server (more control).

**Unity Cloud Build**:

- Pros: Zero setup. Integrated with Unity. Supports multi-platform builds.
- Cons: Slow (15+ minute builds). Limited control over build scripts.

**Jenkins**:

- Pros: Fast (if run on dedicated build machine). Full control via build scripts.
- Cons: Setup overhead (1-2 days). Requires maintenance.

**Recommendation**: Start with Unity Cloud Build for first 6 months. If build times become a bottleneck, migrate to Jenkins + dedicated build machine.

**Build script** (example for Jenkins):

```bash
#!/bin/bash
# Build script for UPFRONT

UNITY_PATH="/Applications/Unity/Hub/Editor/2023.2.10f1/Unity.app/Contents/MacOS/Unity"
PROJECT_PATH="/path/to/upfront-project"
BUILD_PATH="/path/to/builds"

# Build Windows
$UNITY_PATH -quit -batchmode -projectPath $PROJECT_PATH -buildWindows64Player $BUILD_PATH/UPFRONT_Win64.exe

# Build macOS
$UNITY_PATH -quit -batchmode -projectPath $PROJECT_PATH -buildOSXUniversalPlayer $BUILD_PATH/UPFRONT_macOS.app

# Upload to Steam (via SteamCMD)
steamcmd +login $STEAM_USER $STEAM_PASS +run_app_build ../scripts/app_build_upfront.vdf +quit
```

---

### 8.3 Content Tools

**Designer-facing tools** (in-editor):

1. **Brief Generator Test**:
   - Window in Unity Editor.
   - Designer clicks "Generate 50 Briefs" → displays list of generated briefs with all parameters visible.
   - Useful for tuning weights and verifying variety.

2. **Concept Forge Tester**:
   - Designer selects a brief + team from dropdowns → clicks "Generate Concepts" → sees 3 generated concepts with stats and loglines.
   - Iterate on logline templates and stat formulas without launching the full game.

3. **Gauntlet Simulator**:
   - Designer selects a client archetype + concept → runs a full Gauntlet simulation (no UI, just logs).
   - Outputs: number of rounds, notes issued, pushback success rate, final concept stats.
   - Useful for balancing client archetypes.

4. **Economy Simulator**:
   - Designer inputs agency parameters (reputation, roster size, active clients) → runs a full year simulation.
   - Outputs: cash flow per quarter, profit margin, cash crises triggered.
   - Useful for tuning economy balance.

**Implementation**: Each tool is a Unity Editor Window (UnityEditor namespace). 1-2 days dev time per tool. High ROI for design iteration.

---

### 8.4 Version Control

**Tool**: Git + Git LFS (Large File Storage for binary assets).

**Repo structure**:

```
upfront-project/
├── Assets/
│   ├── Scripts/
│   ├── Data/          # JSON config files
│   ├── UI/            # UXML + USS files
│   ├── Art/           # Textures, sprites (tracked by LFS)
│   ├── Audio/         # Music, SFX (tracked by LFS)
│   └── Prefabs/
├── Packages/          # Unity packages
├── ProjectSettings/   # Unity project settings (track in git)
└── .gitignore         # Ignore Library/, Temp/, Logs/
```

**Git LFS setup**:

```bash
git lfs track "*.png"
git lfs track "*.jpg"
git lfs track "*.wav"
git lfs track "*.ogg"
git lfs track "*.mp3"
```

**Branch strategy**:

- `main`: Always stable. Represents the last shipped build.
- `develop`: Active development. Features merge here.
- `feature/[name]`: Short-lived branches for individual features (e.g., `feature/gauntlet-ui`).

**Merge policy**: Feature branches merge to `develop` via pull request. Code review required (if team size > 1). `develop` merges to `main` at milestones (alpha, beta, release).

---

## 9. TECHNICAL RISK ASSESSMENT

I have shipped games. I know where projects die. Here is what could go wrong and what we do about it.

---

### 9.1 CRITICAL RISK: Gauntlet UI feels like a menu, not a conversation

**Severity**: CRITICAL. If this fails, the game fails.

**Likelihood**: MEDIUM. Nailing a dynamic UI conversation is hard.

**Mitigation**:

- **Prototype early**: Build a standalone Gauntlet scene in Month 1. Test with 5+ playtesters. If they say "I wanted to fight for my ad," we have it. If they say "it felt like clicking buttons," we iterate.
- **Invest in dialogue content**: Each client note needs 5+ dialogue variations. Budget 2-3 weeks for a writer to flesh out client personalities.
- **Animate everything**: Client facial expressions. Stat bars shrinking. Music intensity rising. The Gauntlet must *feel* tense, not look tense.

**Contingency**: If the Gauntlet does not work after 3 iterations, pivot to a simpler "client preference matrix" system where the player adjusts sliders to match client desires. Less thematic, but functional. This is the nuclear option — avoid if possible.

---

### 9.2 HIGH RISK: Concept Forge produces repetitive concepts

**Severity**: HIGH. Repetition kills the creative fantasy.

**Likelihood**: MEDIUM. Procedural content is hard to get right.

**Mitigation**:

- **Large content library**: 30+ logline templates, 10+ variants per slot. Math works out to millions of permutations.
- **Playtest with extended sessions**: Run 20-30 campaigns in a single session. Track how often concepts feel similar. If repetition is noticeable within 10 campaigns, expand the content library.
- **Designer tools**: The Concept Forge Tester (see section 8.3) lets designers verify variety without playing the full game.

**Contingency**: If procedural generation fails, hand-author 100 unique concepts and assign them to specific brief archetypes. This loses the emergent feel but guarantees variety. Requires ~1 week of design work.

---

### 9.3 HIGH RISK: Economy is too tight or too loose

**Severity**: HIGH. Economy balance affects player stress and pacing.

**Likelihood**: MEDIUM. Economy tuning is always iterative.

**Mitigation**:

- **Economy Simulator tool**: Designer can simulate full years with different parameters and see cash flow curves.
- **Playtest with different playstyles**: Test cautious, balanced, and aggressive strategies. Track how often each playstyle hits zero cash.
- **Tuning knobs**: All revenue/expense values are in JSON. Designer can tweak without code changes.

**Contingency**: If economy is too tight and players are always broke, increase baseline retainer revenue by 20%. If too loose, increase salary costs or add a new expense category (e.g., "office rent increases per team member").

---

### 9.4 MEDIUM RISK: Super Bowl sequence is anticlimactic

**Severity**: MEDIUM. The Super Bowl is the session payoff. If it feels flat, the session arc fails.

**Likelihood**: LOW. Spectacle is easier to deliver than nuanced systems like the Gauntlet.

**Mitigation**:

- **Prototype Super Bowl as a vertical slice** (Month 2-3). Build the full sequence (animatic, reaction panel, discourse ticker, Monday Morning meeting) standalone. If it feels climactic in isolation, it will work in the full game.
- **Add layers of reveal**: Score reveal, then brand metric shifts, then client call, then news coverage, then rival reactions. Each reveal is a 5-10 second beat. Total sequence is 10 minutes. The player should be on the edge of their seat.

**Contingency**: If the sequence feels flat, add more interactivity. Example: After the ad airs, the player receives three phone calls (client, reporter, rival) and chooses how to respond. Adds drama and player agency.

---

### 9.5 MEDIUM RISK: Performance on low-end PCs / Switch

**Severity**: MEDIUM. Framerate drops damage the experience but do not break the game.

**Likelihood**: LOW. This is a UI sim, not a real-time game. Performance should not be a problem.

**Mitigation**:

- **Profile early**: Run the game on minimum-spec PC (integrated graphics) in Month 6. If framerate is below 60 FPS, identify bottlenecks and optimize.
- **Scalable UI**: If needed, add a "Low Quality" graphics option that reduces UI texture resolution and disables particle effects.
- **Switch-specific testing**: If pursuing Switch port, test on dev kit in Month 9. If framerate is below 30 FPS, reduce texture resolution and simplify animations.

**Contingency**: If Switch performance is poor and cannot be fixed, delay Switch port to post-launch. Focus on PC launch first. Better to ship a great PC game than a mediocre multi-platform game.

---

### 9.6 MEDIUM RISK: Save system bugs (corruption, version incompatibility)

**Severity**: MEDIUM. Save bugs are frustrating but fixable post-launch.

**Likelihood**: LOW. JSON serialization is robust.

**Mitigation**:

- **Test save/load frequently**: Every milestone, run a full career and save/load at multiple points.
- **Save versioning**: Implement migration system (see section 5.4) from day 1. All future updates will change save format — plan for it.
- **Backup saves**: Autosave system writes to 3 rotating slots. If one save corrupts, player can load an earlier save.

**Contingency**: If save corruption becomes a widespread issue post-launch, hotfix within 48 hours. Priority 1 bug. In the meantime, provide a manual "export save to clipboard" feature so players can back up their saves externally.

---

### 9.7 LOW RISK: Scope creep (stretch goals consume core dev time)

**Severity**: HIGH (if it happens). Scope creep is how games die in development.

**Likelihood**: MEDIUM. Designers love features. Programmers love systems. Both are dangerous.

**Mitigation**:

- **Strict feature lock at Alpha milestone** (Month 7). After Alpha, no new features. Only polish and bug fixes.
- **Stretch goals are clearly marked**: Rival agencies, cultural trends, award season, office customization are ALL stretch. If any threaten the core loop, cut them.
- **Monthly scope review**: Every month, the team reviews remaining work and estimates time to completion. If estimate exceeds deadline, cut the lowest-priority stretch goal.

**Contingency**: If timeline slips, cut in this order: (1) Office customization, (2) Award season, (3) Cultural trends, (4) Rival agencies. The core loop (Brief → Team → Forge → Gauntlet → Production → Broadcast → Reputation) is non-negotiable. Everything else is negotiable.

---

## 10. DEVELOPMENT MILESTONES (TECH PERSPECTIVE)

### 10.1 Timeline Overview

**Total Development Time**: 12 months (solo or 2-4 person team).

**Breakdown**:

- Months 1-3: Prototyping (vertical slice of core loop)
- Months 4-6: Production (full systems, content creation)
- Months 7-9: Alpha (feature complete, balancing)
- Months 10-11: Beta (bug fixing, polish)
- Month 12: Release Candidate (QA, certification, launch prep)

---

### 10.2 Month 1-3: Prototyping

**Goal**: Prove the core loop is fun. Build a vertical slice that shows one complete campaign from brief to broadcast.

**Deliverables**:

- **Week 1-2**: Project setup. Unity 2023.2 LTS installed. Git repo initialized. Core folder structure. Event bus implemented. Basic game loop (calendar, quarters).
- **Week 3-4**: Brief System. JSON config for 8 archetypes. Brief generation algorithm. UI mockup for brief display.
- **Week 5-6**: Team Manager. Creative class with 6 stats. Chemistry calculation. UI for team assignment (drag-and-drop).
- **Week 7-8**: Concept Forge. Stat generation algorithm. Logline templates (10 templates). UI for concept display (mood board mockup).
- **Week 9-10**: Approval Gauntlet (core mechanic). FSM for Gauntlet rounds. Client note generation. Persuasion check. Placeholder UI (no animations yet).
- **Week 11**: Production Pipeline. Budget allocation UI. Stat modifiers from allocation.
- **Week 12**: Broadcast & Reaction. Audience score calculation. Placeholder animatic (4 static frames). Reaction panel (8 faces). Metrics update.

**Milestone**: By end of Month 3, the player can complete one full campaign in ~8 minutes. Playtest with 5 people. Get feedback on Gauntlet feel. Iterate.

**Tech Debt Tolerance**: HIGH. Prototype code is messy. No unit tests. Hardcoded values. This is fine. The goal is to find the fun, not ship the game.

---

### 10.3 Month 4-6: Production

**Goal**: Build out the full game systems. Content creation begins. Replace placeholders with real assets.

**Deliverables**:

- **Month 4**:
  - Expand Brief System to 50+ briefs (JSON authoring).
  - Expand Concept Forge to 30+ logline templates.
  - Implement Team Chemistry edge cases (Meltdown, Brilliant Friction).
  - Build Gauntlet UI with animations (client expressions, stat bar shrinking, music intensity).
  - Implement Reputation System (3 sub-scores, client tier unlocks).
  - Implement Economy System (revenue, expenses, cash flow).

- **Month 5**:
  - Build Super Bowl sequence (extended animatic, expanded reaction panel, Monday Morning meeting).
  - Implement Save/Load system (JSON serialization, autosave triggers).
  - Build Calendar UI (year overview, quarter progression, event markers).
  - Implement Morale system (creative events, loyalty, quit threats).
  - Build Roster management UI (hire, fire, salary negotiation).

- **Month 6**:
  - Build Awards system (submission, jury evaluation, ceremony).
  - Implement Cultural Trends (if stretch goal is active).
  - Build Rival Agencies (if stretch goal is active).
  - Content creation: Storyboard frames (64 frames for Hook/Tone combinations). Viewer portraits (20 variations). Audio (3 music tracks, UI SFX).
  - Polish Gauntlet UI (dialogue variations, more animations).

**Milestone**: By end of Month 6, the game is feature-complete (minus stretch goals). The player can play a full year (4 quarters, multiple campaigns, Super Bowl). Playtest with 10 people for full sessions (60-90 minutes).

**Tech Debt Tolerance**: MEDIUM. Code should be modular and testable. Event bus should be solid. No major refactors after this point.

---

### 10.4 Month 7-9: Alpha

**Goal**: Feature lock. Focus on balance, tuning, and polish. Bug fixing begins.

**Deliverables**:

- **Month 7**:
  - Feature lock: No new systems. Only bug fixes and balance tweaks.
  - Economy balancing: Run Economy Simulator for 100+ simulated years. Tune revenue/expense values.
  - Concept Forge balancing: Test for repetition over 30+ campaigns. Expand content library if needed.
  - Gauntlet balancing: Tune client archetypes for appropriate difficulty. Ensure pushback success rates match design targets.

- **Month 8**:
  - UI polish pass 1: Add transitions, hover states, tooltips, button feedback.
  - Audio implementation: FMOD integration. Dynamic music layers. Event-driven SFX.
  - Accessibility pass: Add colorblind mode, adjustable text size, key rebinding.
  - Performance profiling: Run Unity Profiler on full campaign. Identify and fix bottlenecks.

- **Month 9**:
  - Content expansion: Add 20 more briefs, 10 more logline templates.
  - Playtest marathon: 3-5 playtesters play full careers (5+ years). Track issues (bugs, balance, pacing).
  - Bug fixing: Prioritize critical bugs (crashes, soft locks, save corruption). Defer minor bugs (typos, minor UI glitches).

**Milestone**: By end of Month 9, the game is Alpha-complete. No crashes. All core systems work. Playtester feedback is positive ("I want to play more"). Begin closed beta.

**Tech Debt Tolerance**: LOW. Any major refactors needed (e.g., rearchitecting a system) should be done now. Post-beta, only bug fixes and minor tweaks.

---

### 10.5 Month 10-11: Beta

**Goal**: Closed beta with 50-100 players. Collect feedback. Fix bugs. Polish everything.

**Deliverables**:

- **Month 10**:
  - Closed beta launch on Steam (private branch). Invite 50 players via mailing list / Discord.
  - Set up feedback channels: Discord server, Google Form for bug reports.
  - Monitor crash reports (Unity Cloud Diagnostics or Sentry).
  - Daily bug triage: Prioritize critical bugs (crashes, save corruption). Fix within 24 hours. Defer minor bugs.

- **Month 11**:
  - UI polish pass 2: Final animations, transitions, particle effects.
  - Audio polish: Mix and master music tracks. Normalize SFX volumes.
  - Content polish: Proofread all text (briefs, dialogue, loglines). Fix typos.
  - Performance optimization: Profile on min-spec PC. Ensure 60 FPS.
  - Achievements implementation: 30-40 Steam achievements. Hook into game events.

**Milestone**: By end of Month 11, the game is Beta-complete. Crash rate < 1%. Positive player sentiment (Steam reviews if public beta). Ready for final QA pass.

**Tech Debt Tolerance**: ZERO. Code freeze after Month 11. Only critical bug fixes allowed.

---

### 10.6 Month 12: Release Candidate

**Goal**: Final QA. Build submission to Steam (and Nintendo if Switch is active). Marketing ramp-up. Launch.

**Deliverables**:

- **Week 1-2**:
  - Final QA pass: Full playthrough on Windows, macOS, Linux. Test all input methods (mouse/keyboard, controller). Verify all achievements trigger.
  - Build Release Candidate 1 (RC1). Upload to Steam for final testing.
  - Fix any critical bugs found in RC1. Build RC2.

- **Week 3**:
  - Steam store page finalization: Screenshots, trailer, description, tags.
  - Press outreach: Send keys to 20-30 gaming press outlets and YouTubers.
  - Marketing: Announce launch date on social media, mailing list, Discord.

- **Week 4**:
  - Launch day: Release on Steam. Monitor crash reports and reviews. Be ready to hotfix critical bugs within 24 hours.
  - Post-launch support: Monitor Discord and Steam forums. Respond to player feedback. Patch bugs as needed.

**Milestone**: By end of Month 12, the game is LIVE on Steam. First patch (1.0.1) within 1 week to fix any launch-day issues.

---

### 10.7 Post-Launch Roadmap

**Months 13-15** (optional, if PC launch succeeds):

- Patch support: 1-2 patches per month for bug fixes and balance tweaks.
- Content updates: Add 2-3 new client archetypes, 10 new briefs, 5 new logline templates. Free update.
- Switch port: Begin Switch port (3-6 months dev time). Submit to Nintendo certification.

**Months 16-18** (stretch):

- Major content expansion: Add "Agency Crisis" system (public scandals, client boycotts, PR recovery campaigns). $5 DLC or free update depending on PC sales.
- iPad port: If resources allow.

---

## 11. CLOSING NOTES

### 11.1 What Could Go Wrong

I have been honest about risks. Here is what keeps me up at night:

**The Gauntlet does not feel tense.** If negotiation feels like a menu, the game is dead. This is the highest-risk system. Prototype it first. Iterate ruthlessly. Do not ship until it sings.

**Scope creep.** Every designer wants more features. Every programmer wants more systems. The game already has 10+ interlocking systems. Adding more is how projects die. Feature lock at Month 7. Cut stretch goals if timeline slips.

**Playtester feedback is ignored.** If 5 playtesters say "the Gauntlet is confusing," they are right. Do not rationalize. Do not explain. Fix it. Playtesters are the ground truth.

---

### 11.2 What Could Go Right

If the Gauntlet works — if players feel the tension of defending their work against a client who controls the money — this game is special. No other management sim has this. The fantasy is real. The systems support it. The setting is perfect.

The technical architecture is solid. Unity is boring. Event bus is boring. JSON configs are boring. Boring is good. Boring means the tech is invisible and the game is visible.

The scope is achievable. 12 months for a 2-4 person team is realistic. I have built larger games in less time. This one is UI-heavy, not content-heavy. That is a controllable scope.

The market is there. Game Dev Tycoon sold 2.5 million copies. Two Point Hospital sold 4 million. Management sim players are hungry for new settings and new verbs. UPFRONT delivers both.

---

### 11.3 Final Verdict

This game is shippable. The architecture is sound. The risks are known. The mitigation strategies are in place. The timeline is realistic.

Build the Gauntlet first. If that works, everything else follows.

Ship it.

-- BYTE

---

## APPENDIX A: KEY FILE PATHS

For reference during development:

| File | Purpose | Path |
|------|---------|------|
| **Core Systems** | | |
| GameDirector.cs | Main game loop | `/Assets/Scripts/Core/GameDirector.cs` |
| EventBus.cs | Event pub/sub system | `/Assets/Scripts/Core/EventBus.cs` |
| SaveSystem.cs | Save/load manager | `/Assets/Scripts/Core/SaveSystem.cs` |
| **Gameplay Systems** | | |
| BriefSystem.cs | Brief generation | `/Assets/Scripts/Systems/BriefSystem.cs` |
| TeamManager.cs | Team chemistry | `/Assets/Scripts/Systems/TeamManager.cs` |
| ConceptForge.cs | Concept generation | `/Assets/Scripts/Systems/ConceptForge.cs` |
| ApprovalGauntlet.cs | Gauntlet FSM | `/Assets/Scripts/Systems/ApprovalGauntlet.cs` |
| ProductionPipeline.cs | Budget allocation | `/Assets/Scripts/Systems/ProductionPipeline.cs` |
| BroadcastEngine.cs | Audience simulation | `/Assets/Scripts/Systems/BroadcastEngine.cs` |
| ReputationSystem.cs | Agency reputation | `/Assets/Scripts/Systems/ReputationSystem.cs` |
| EconomySystem.cs | Cash flow | `/Assets/Scripts/Systems/EconomySystem.cs` |
| **Data Configs** | | |
| briefs_config.json | Brief archetypes, goals | `/Assets/Data/Configs/briefs_config.json` |
| creatives_config.json | Creative templates | `/Assets/Data/Configs/creatives_config.json` |
| clients_config.json | Client archetypes, notes | `/Assets/Data/Configs/clients_config.json` |
| concepts_config.json | Logline templates | `/Assets/Data/Configs/concepts_config.json` |
| economy_config.json | Revenue/expense values | `/Assets/Data/Configs/economy_config.json` |
| **UI** | | |
| MainMenu.uxml | Main menu layout | `/Assets/UI/MainMenu.uxml` |
| GauntletUI.uxml | Gauntlet screen | `/Assets/UI/GauntletUI.uxml` |
| BroadcastUI.uxml | Broadcast sequence | `/Assets/UI/BroadcastUI.uxml` |
| Styles.uss | Global UI styles | `/Assets/UI/Styles.uss` |

---

## APPENDIX B: TECH STACK SUMMARY

| Layer | Technology |
|-------|-----------|
| Engine | Unity 2023.2 LTS |
| Language | C# 9.0 |
| UI Framework | UI Toolkit (UXML + USS) |
| Data Format | JSON (Newtonsoft.Json) |
| Audio Middleware | FMOD Studio 2.x |
| Version Control | Git + Git LFS |
| Build Automation | Unity Cloud Build → Jenkins (post-alpha) |
| CI/CD | GitHub Actions (optional) |
| Profiling | Unity Profiler, Memory Profiler |
| Platform SDKs | Steamworks.NET, Nintendo SDK (if Switch port) |
| Save System | JSON serialization + delta compression |
| State Management | Custom FSM + Event Bus |

---

## APPENDIX C: ESTIMATED LOC (LINES OF CODE)

Based on similar projects:

| System | Estimated LOC |
|--------|---------------|
| Core (GameDirector, EventBus, SaveSystem) | ~1,500 |
| Brief System | ~500 |
| Team Manager | ~600 |
| Concept Forge | ~800 |
| Approval Gauntlet | ~1,200 |
| Production Pipeline | ~400 |
| Broadcast Engine | ~700 |
| Reputation & Economy | ~900 |
| UI Controllers | ~2,000 |
| Data Models | ~1,000 |
| Utilities | ~500 |
| **Total** | ~10,000 LOC |

For a 12-month project with a 2-person team, ~10K LOC is reasonable. Most complexity is in data (JSON configs) and content (UI, audio), not code.

---

**END OF TECHNICAL ARCHITECTURE DOCUMENT**

*This document is a living blueprint. As prototyping reveals unknowns, update this doc. But the core architecture — event-driven systems, JSON configs, state machines — should remain stable. Build on solid ground.*

*Ship it.*