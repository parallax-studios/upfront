# UPFRONT -- Game Design Document

**Author**: REED (Game Designer)
**Version**: 1.0
**Date**: 2026-02-07
**Status**: Complete First Pass -- Ready for Playtest Planning

---

> "A game is its loop. If the 30-second experience isn't compelling, no amount of content saves it."

I have read the pitch. I know what this game wants to be. Now let me tell you what it *is* -- mechanically, systemically, down to the numbers. Every section here answers the same question I ask of every design: **what's the loop, where's the depth, and does this hold up at hour 20?**

This document covers the full mechanical skeleton of UPFRONT. No placeholders. No "TBD." If something is in here, it is implementable. If something is not in here, it is a conscious cut.

Let's find the fun.

---

## 1. PLAYER FANTASY STATEMENT

**"I am the person who stands between a brilliant idea and the coward who is paying for it -- and the version of that idea that reaches the world is my responsibility."**

That is the fantasy. Not "I run a business." Not "I make ads." The fantasy is *creative authority under pressure*. The player wants to feel what every creative director, showrunner, and lead designer has felt: the weight of defending work you believe in to someone who controls the budget. The thrill when the bold version ships. The hollow ache when the safe version wins.

Every system in this game must serve that fantasy. If a mechanic does not create, heighten, or resolve the tension between creative ambition and commercial survival, it does not belong. That is the filter. That is the north star.

---

## 2. CORE LOOP

### 2.1 The 30-Second Loop: Read, Staff, Choose

The player looks at a brief. They assign a team. The team generates concepts. The player picks one. Every cycle takes about 20-30 seconds of active decision-making.

The verb is **CURATE**. The player does not design ads. They select, refine, and champion concepts that their team produces. This distinction is critical -- it models the actual creative director experience and prevents the game from becoming an ad-design tool.

### 2.2 The 5-Minute Loop: Brief to Broadcast

A single campaign from brief intake to ad broadcast plays out over 5-8 minutes of real time. The arc:

1. **Brief Intake** (30 sec) -- Read the client brief, identify hidden priorities
2. **Team Assignment** (30 sec) -- Staff the project from your roster
3. **Concept Selection** (60 sec) -- Review 2-3 generated concepts, pick one, optionally revise
4. **Approval Gauntlet** (90-120 sec) -- Present to the client, negotiate notes, defend or concede
5. **Production Allocation** (60 sec) -- Distribute budget across production categories
6. **Broadcast & Reaction** (30-60 sec) -- Watch the ad air and the metrics shift

This is the heartbeat. Every campaign is a self-contained dramatic arc with a beginning (the brief), a middle (the gauntlet), and an end (the broadcast). If this loop is not satisfying on its own, the game fails. No amount of meta-progression saves a broken 5-minute loop. I learned that the hard way.

### 2.3 The Meta Loop: The Calendar Year

A full calendar year is one session (45-90 minutes). The year structures long-term decision-making:

- **Q1 (January-March)**: New client pitches arrive. Take on 2-3 accounts. Safe bread-and-butter work to build cash reserves and Client Trust.
- **Q2 (April-June)**: Mid-year campaigns. Award submissions for last year's work. Results from Cannes/Clios affect reputation and talent recruitment.
- **Q3 (July-September)**: Super Bowl media buy auction opens. Ambitious clients begin pitching big Q4 campaigns. The player must decide how aggressively to pursue a Super Bowl slot.
- **Q4 (October-December)**: Crunch. Super Bowl production. Holiday campaign deadlines. Team fatigue peaks. The tension between "finish the safe work" and "swing for the fences on the big game" is at maximum.
- **Super Bowl Sunday**: The climax. One ad. One hundred million simulated viewers. Monday Morning report. Year resets.

### 2.4 Core Loop Diagram

```
                    +-----------+
                    |  CLIENT   |
                    |  BRIEF    |
                    +-----+-----+
                          |
                          v
                    +-----+-----+
                    |   TEAM    |
                    | ASSIGNMENT|
                    +-----+-----+
                          |
                          v
                    +-----+-----+
                    |  CONCEPT  |
                    |   FORGE   |-------> [Concept A] [Concept B] [Concept C]
                    +-----+-----+                        |
                          |                              |
                          v                              |
                    +-----+-----+                        |
                    |  PLAYER   |<-----------------------+
                    |  SELECTS  |
                    +-----+-----+
                          |
                          v
              +-----------+-----------+
              |    APPROVAL GAUNTLET  |
              |  (Negotiate / Defend) |
              +-----------+-----------+
                          |
                +---------+---------+
                |                   |
                v                   v
          [Approved]          [Killed/Walked]
                |                   |
                v                   v
          +-----+-----+      +-----+-----+
          | PRODUCTION |      | REPUTATION |
          | PIPELINE   |      | SHIFT      |
          +-----+-----+      +-----------+
                |
                v
          +-----+-----+
          | BROADCAST  |
          | & REACTION |
          +-----+-----+
                |
                v
          +-----+-----+
          |  METRICS   |----> Agency Rep / Client Trust / Awards / Revenue
          |  UPDATE    |
          +-----+-----+
                |
                v
          +-----+-----+
          | NEXT BRIEF |
          +-----------+
```

The loop feeds itself: better metrics attract better clients with bigger budgets and harder briefs. The player spirals upward in complexity, not just difficulty. That is the difference between a treadmill and a growth curve.

---

## 3. CORE MECHANICS

### 3.1 The Brief System

**Player Verb**: READ and INTERPRET

**System Description**: Each brief is procedurally generated from a matrix of parameters:

| Parameter | Range | Example |
|---|---|---|
| Brand Archetype | 8 types (see below) | "Legacy Challenger" |
| Campaign Goal | 5 types: Awareness, Perception, Launch, Retention, Crisis | "Brand Perception Repair" |
| Budget Ceiling | $50K - $5M (scales with client tier) | $800K |
| Target Demo | 6 segments: Youth 18-24, Young Adult 25-34, Family 35-49, Affluent 35-54, Mass Market, Niche | "Young Adult 25-34" |
| Non-Negotiables | 0-3 constraints from a pool of 20 | "Must include mascot", "No humor" |
| Hidden Priority | 1 of 5 internal motivations | "CMO needs a win before board review" |
| Risk Tolerance | 1-10 scale | 3 (conservative) |
| Cultural Moment Sensitivity | Low / Medium / High | Medium |

**Brand Archetypes** (8 total):
1. **Corporate Titan** -- Fortune 500, massive budget, risk-averse, values Brand Clarity above all
2. **Desperate Startup** -- Small budget, high risk tolerance, needs Originality to stand out
3. **Legacy in Decline** -- Medium budget, terrified of irrelevance, says they want bold but flinches at bold
4. **Trend Chaser** -- Medium-high budget, wants whatever is culturally hot right now, fickle
5. **Prestige House** -- High budget, values Emotion and Production Value, slow approval process
6. **Local Hero** -- Low budget, loyal, values authenticity, easy to please but low-reward
7. **Category Disruptor** -- High budget, genuinely wants risk, but their board does not
8. **Scandal Recovery** -- Medium budget, needs Brand Clarity and Emotion, zero tolerance for humor

**Feedback**: The brief appears as a printed document on the player's desk. Key parameters are highlighted. Hidden priorities are never stated directly -- they are implied through client dialogue during the Approval Gauntlet. A "CMO needs a win" hidden priority means the client pushes harder for safe work but folds quickly if you show confidence. A "Board wants innovation" hidden priority means the client will tolerate risk but needs data to justify it.

**Depth**: Over dozens of campaigns, the player learns to read hidden priorities from context clues in the brief text. A brief that mentions "recent leadership changes" signals a new CMO. A brief that mentions "category disruption from competitors" signals desperation. The system rewards attention and pattern recognition -- the same skills a real creative director develops.

---

### 3.2 Team Chemistry Engine

**Player Verb**: ASSEMBLE and MANAGE

**System Description**: Each creative has six stats rated 1-10:

| Stat | Effect on Output | Effect on Process |
|---|---|---|
| **Vision** | Increases Originality of concepts | Higher-Vision creatives clash more with low-Vision teammates |
| **Craft** | Increases Production Value and Emotion | High-Craft creatives are slower but produce polished work |
| **Speed** | Reduces production time by (Speed * 5)% | Speed above 7 introduces "sloppy" risk: 10% chance of a production error per point above 7 |
| **Ego** | Increases Originality ceiling but also increases concept variance | Ego > 7 means the creative may ignore client notes. Ego > 9 means they may ignore YOUR notes |
| **Taste** | Biases concept generation toward specific Tones | Creatives with matching Taste produce cohesive work. Mismatched Taste creates tonal chaos OR brilliant surprise |
| **Ambition** | Increases Production Ambition of concepts | Ambition > 7 means the creative pushes budget overruns. Ambition > 9 means they may pitch unauthorized concepts to the client directly |

**Chemistry Formula**:

```
Team Cohesion = Base(50) + (Taste Alignment * 3) + (Avg Craft * 2) - (Ego Variance * 4) - (Ambition Gap * 2)
```

Where:
- Taste Alignment = number of team members sharing at least one Taste tag (0-3, scaled to 0-10)
- Ego Variance = standard deviation of Ego stats across the 4-person team
- Ambition Gap = difference between highest and lowest Ambition on the team

**Team Cohesion thresholds**:
- **70-100 (Synergy)**: Concepts generated are +15% quality. Production is 10% faster. Low variance.
- **40-69 (Functional)**: Standard output. No bonuses or penalties. Moderate variance.
- **20-39 (Friction)**: Concepts are +20% Originality OR -20% quality (coin flip per concept). Production is 15% slower. High variance. This is the "brilliant friction" zone -- experienced players deliberately engineer it.
- **0-19 (Meltdown)**: One team member threatens to quit per week. Concepts are wildly inconsistent. Production halts until the player intervenes with a Morale action.

**Feedback**: Team chemistry is visualized as a "bullpen temperature" gauge -- cool blue for Synergy, warm amber for Functional, hot orange for Friction, red alarm for Meltdown. Individual creatives display thought bubbles during concept generation showing their reactions: "This is beneath me" (high Ego, low-risk concept), "Now we're talking" (high Vision, bold concept), "We're going to miss the deadline" (high Speed watching a slow team).

**Depth**: The mastery curve is in learning to engineer Friction deliberately. A Synergy team produces reliable, good work. A Friction team produces unpredictable work that occasionally spikes to brilliance. The expert player learns which briefs need reliability (Corporate Titan, Scandal Recovery) and which need volatility (Desperate Startup, Category Disruptor). At hour 20, team composition is not a staffing problem -- it is a creative strategy.

---

### 3.3 The Concept Forge

**Player Verb**: CURATE and REFINE

**System Description**: When a team is assigned to a brief, the Concept Forge generates 2-3 concepts. Each concept has five stats on a 1-100 scale:

| Stat | What It Measures | Primary Drivers |
|---|---|---|
| **Production Value** | Visual polish, cinematic quality, production ambition | Team Craft + Budget Allocation |
| **Humor** | Comedy effectiveness, quotability | Team Vision + Tone tags + Cultural Risk |
| **Emotion** | Emotional resonance, sincerity, heart | Team Craft + Team Taste alignment + Tone tags |
| **Originality** | Novelty, surprise factor, cultural disruption | Team Vision + Team Ego + Cultural Risk |
| **Brand Clarity** | How clearly the ad communicates the brand message | Inverse relationship with Originality (base modifier of -0.3 per Originality point above 60). Boosted by brief compliance |

Concept generation algorithm:

```
For each stat S:
  Base = (Relevant Team Stats Average) * 5
  Brief Bonus = +10 if concept aligns with brief's stated goals
  Chemistry Modifier = Team Cohesion bonus/penalty (see 3.2)
  Randomness = random(-15, +15)
  Cultural Risk Multiplier = 1.0 + (Risk Level * 0.05) for Originality/Humor
                             1.0 - (Risk Level * 0.03) for Brand Clarity
  S = clamp(Base + Brief Bonus + Chemistry Modifier + Randomness) * Cultural Risk Multiplier, 1, 100)
```

Each concept also has:
- **Tone** (1 of 8): Funny, Emotional, Provocative, Surreal, Earnest, Ironic, Nostalgic, Aspirational
- **Hook Type** (1 of 8): Celebrity Cameo, Narrative Mini-Film, Visual Gag, Musical Number, Shock Value, Slice-of-Life, Anthem, Mockumentary
- **Production Ambition** (1-5 scale): 1=lo-fi scrappy, 2=solid broadcast, 3=cinematic, 4=blockbuster, 5=unprecedented
- **Cultural Risk Score** (1-10): 1=invisible safe, 5=conversation starter, 8=polarizing, 10=career-defining or career-ending

**Player Refinement**: After selecting a concept, the player can spend one "Revision Token" (limited resource, 3 per quarter, replenished by team Morale) to nudge one stat by +10/-10 or swap the Tone. This models the creative director's editorial hand -- you are shaping, not creating.

**Feedback**: Concepts are presented as mood boards -- collaged visual panels with tone descriptors, a one-sentence logline, and stat bars. The player sees the concept as the team would present it: evocative, slightly messy, full of potential.

**Depth**: The expert player reads the Concept Forge's outputs probabilistically. They know that a high-Vision, high-Ego team on a Desperate Startup brief with Cultural Risk 7+ will produce at least one concept with Originality above 80 roughly 60% of the time. They learn the generation patterns and staff teams to produce the *distribution* of concepts they want, not just the single best concept. That is a deep optimization layer.

---

### 3.4 The Approval Gauntlet

**Player Verb**: PRESENT, DEFEND, CONCEDE, WALK AWAY

This is the heart of the game. This is where the player fantasy lives or dies. Let me be precise about how it works.

**Structure**: The Gauntlet is a 3-5 round negotiation played in a presentation room interface. Each round:

1. The player presents the current state of the concept (round 1 is the initial pitch)
2. The AI client reacts based on their parameters
3. The client issues 0-2 **Notes** (revision requests)
4. The player chooses a response for each Note:
   - **ACCEPT** the note: Concept stat shifts per the note's effect. Client Trust +5. Creative Integrity -3.
   - **PUSH BACK** on the note: Spend 1 Pushback Point. Persuasion check against client Risk Tolerance. Success: note withdrawn, Client Trust -2, Creative Integrity +5. Failure: Client Trust -8, note remains, client adds a harder note next round.
   - **COMPROMISE**: Offer a middle-ground counter-proposal. Concept stat shifts by half the note's effect. Client Trust +2. Creative Integrity -1. Available once per Gauntlet.
   - **WALK AWAY**: End the Gauntlet. Campaign is killed. Client Trust -20. Creative Integrity +15. The brief returns to the pool (a different client may pick it up). Reputation shifts toward "uncompromising." This is the nuclear option and it should feel like one.

**Pushback Points**: The player starts each Gauntlet with Pushback Points equal to:

```
Pushback Points = floor(Agency Reputation / 20) + floor(Client Trust with this client / 25) + 1
```

A new agency with 30 reputation and 50 Client Trust gets floor(30/20) + floor(50/25) + 1 = 1 + 2 + 1 = **4 Pushback Points**. A legendary agency with 90 reputation and 80 Client Trust gets 4 + 3 + 1 = **8 Pushback Points**. Pushback is a resource you earn through track record. New agencies must compromise. Legendary agencies can fight.

**Persuasion Check**:

```
Persuasion Roll = random(1, 100)
Success Threshold = Client Risk Tolerance * 8 + (Agency Reputation / 5) + (Creative Integrity / 10)
```

Example: Client Risk Tolerance 5, Agency Reputation 60, Creative Integrity 40. Threshold = 40 + 12 + 4 = **56**. The player succeeds 56% of the time. Against a risk-averse client (Tolerance 2) with a new agency (Rep 20, CI 20): threshold = 16 + 4 + 2 = **22%**. You *feel* powerless against conservative clients early on. That is intentional. That is the fantasy.

**Client Note Types** (20 total, drawn from pools based on client archetype):

| Note Category | Example Note | Stat Effect if Accepted |
|---|---|---|
| **De-Risk** | "Can we tone down the humor?" | Humor -15, Brand Clarity +5 |
| **De-Risk** | "Lose the controversial element" | Originality -20, Brand Clarity +10 |
| **Brand Police** | "The logo needs to be bigger" | Brand Clarity +10, Production Value -5, Originality -5 |
| **Brand Police** | "Can we add the tagline at the end?" | Brand Clarity +8, Emotion -5 |
| **Scope Creep** | "What if we added a celebrity?" | Production Value +10, Budget +30%, Originality -5 |
| **Scope Creep** | "Can we make it a 60-second spot?" | All stats +5, Budget +80% |
| **Taste Override** | "My wife didn't get the joke" | Humor -20, forced Tone shift to Earnest |
| **Taste Override** | "I want it to feel more premium" | Emotion +5, Production Value +10, Humor -15 |
| **Data Demand** | "Do we have research supporting this approach?" | If you have a relevant Market Research report: no stat change, Client Trust +5. If not: -10 to most ambitious stat |
| **Panic Note** | "Our competitor just launched something similar" | Forces complete Tone or Hook Type change. All stats reroll with -10 penalty |

**Feedback**: The presentation room is visualized with the client across a conference table. Their facial expressions shift with each round -- nodding, frowning, checking their phone (very bad), leaning forward (very good). When a Pushback succeeds, there is a visible shift: the client uncrosses their arms, pauses, says something like "Okay, I trust you on this one." When it fails, the temperature drops. The player *feels* the negotiation in the room's body language.

**Depth**: At hour 1, the Gauntlet is a menu of choices. At hour 20, it is poker. The expert player reads the client archetype, estimates their Risk Tolerance, calculates their Pushback Points, and plans a negotiation strategy before the first round. They know to accept early low-impact notes to build Client Trust for the critical Pushback on round 3 when the client tries to kill the Hook. They learn that walking away from a Prestige House client in year 1 is suicide, but walking away from a Corporate Titan in year 5 -- when your reputation is high enough -- sends a signal that attracts Category Disruptors. Every Gauntlet is a story. Every Gauntlet teaches.

---

### 3.5 Production Pipeline

**Player Verb**: ALLOCATE

**System Description**: After the concept survives the Gauntlet, the player distributes the approved budget across five production categories:

| Category | What It Affects | Minimum Spend | Diminishing Returns Threshold |
|---|---|---|---|
| **Casting** | Emotion +2 per 5% allocated, Humor +1 per 5% if Tone is Funny | 5% of budget | Above 35% |
| **Location & Set** | Production Value +2 per 5% allocated | 5% of budget | Above 30% |
| **VFX & Post** | Production Value +3 per 5% allocated, Originality +1 per 5% | 10% of budget | Above 40% |
| **Sound & Music** | Emotion +2 per 5% allocated, Production Value +1 per 5% | 5% of budget | Above 25% |
| **Edit & Polish** | Brand Clarity +2 per 5% allocated, all other stats +0.5 per 5% | 10% of budget | Above 30% |

Budget is a zero-sum allocation puzzle. Every dollar in VFX is a dollar not in Casting. The player must read their concept's strengths and double down or shore up weaknesses.

**Production Ambition Tax**: If the concept's Production Ambition exceeds what the budget can support, a penalty applies:

```
Ambition Gap = Production Ambition - floor(Budget / $200K)
If Ambition Gap > 0: All stats suffer -(Ambition Gap * 8) penalty
```

A $400K budget supports Ambition 2 (solid broadcast). A concept with Ambition 4 (blockbuster) on that budget suffers a -16 to all stats. The player learns not to greenlight ambition they cannot fund. Or they learn to fight the client for more budget in the Gauntlet -- a legitimate advanced strategy.

**Feedback**: The production phase is visualized as a timeline with milestone markers. Budget allocation is a drag-and-drop bar chart (Excel 2003 aesthetic). When the player over-allocates one category, others visually shrink. When the Ambition Gap penalty triggers, the timeline flashes red and a warning reads: "Production team says the budget doesn't match the vision."

**Depth**: The production pipeline is deliberately the shallowest mechanic. It is a 60-second allocation puzzle, not a management sim within a management sim. The depth is in how production choices *interact* with Gauntlet compromises: if the client forced you to add a celebrity (Scope Creep note), your Casting budget must increase, which starves VFX, which lowers Production Value, which means the ambitious visual concept your team pitched now looks cheap. Every Gauntlet concession has a production cost. The systems talk to each other.

---

### 3.6 Broadcast & Reaction System

**Player Verb**: WATCH and RESPOND

**System Description**: When the ad airs, the game calculates audience response using the ad's final stats against the current cultural climate and target demographic preferences.

**Audience Response Formula**:

```
Cultural Fit = (Ad Tone alignment with Current Year Trend) * 15
Demo Match = (Ad Target Demo match with Campaign Brief Demo) * 10
Raw Impact = (Production Value * 0.2) + (Humor * 0.25) + (Emotion * 0.25) + (Originality * 0.2) + (Brand Clarity * 0.1)
Audience Score = Raw Impact + Cultural Fit + Demo Match + random(-10, +10)
```

**Audience Score thresholds**:

| Score | Result | Effect |
|---|---|---|
| 0-25 | **Forgotten** | No brand metric change. Client Trust -5. No awards eligibility. |
| 26-45 | **Adequate** | Brand Awareness +5%. Client Trust +3. Revenue covers costs. |
| 46-65 | **Effective** | Brand Awareness +15%, Brand Trust +5%. Client Trust +8. Profit margin 20%. |
| 66-80 | **Hit** | Brand Awareness +30%, Brand Trust +10%. Client Trust +15. Profit margin 40%. Award nomination likely. |
| 81-90 | **Cultural Moment** | Brand Awareness +50%, internet discourse triggers, Brand Trust +15% or -5% (polarization roll). Award nomination guaranteed. New client inquiries. |
| 91-100 | **Legendary** | Brand Awareness +80%, Brand Trust +20%, agency Reputation +15. Award win likely. Defines the player's career. Triggers a "legacy moment" in the agency history timeline. |

**Super Bowl Modifier**: Ads airing during the Super Bowl get a flat +15 to Audience Score and all brand metric effects are doubled. The stakes are real. The Super Bowl is not a reskin -- it is a mechanical amplifier.

**Polarization**: Ads with Originality above 70 or Cultural Risk above 7 trigger a **Polarization Roll**:

```
Polarization = random(1, 100)
If Polarization > 60: Brand Trust shifts become split (+X% among favorable demo, -Y% among unfavorable demo)
If Polarization > 85: "Controversy Event" triggers -- media coverage, client panic call, forced crisis response
```

Controversy is not failure. A controversial Super Bowl ad that splits the country generates more long-term brand awareness than a safe one that everyone forgets by halftime. But the client will not see it that way on Monday morning. The player must weigh short-term client relationship damage against long-term reputation gains. That is the game.

**Feedback**: The broadcast sequence is the spectacle moment. Split screen: storyboard animatic on the left, "America Reacts" sentiment panel on the right. Faces light up, frown, laugh, look at their phones. A scrolling discourse bar shows simulated social media reactions -- one-liners, memes, hot takes. The Audience Score ticks up in real time. The player watches their work land (or crash). This is the payoff for every Gauntlet battle.

---

### 3.7 Agency Reputation & Economy

**Player Verb**: GROW and CHOOSE IDENTITY

**Economy Table -- Revenue Sources**:

| Source | Revenue Range | Frequency |
|---|---|---|
| **Client Retainer** (ongoing account) | $10K-$50K/month based on client tier | Monthly, per active client |
| **Campaign Completion Bonus** | 15% of campaign budget on delivery | Per campaign |
| **Performance Bonus** | 5-20% of campaign budget if Audience Score > 65 | Per successful campaign |
| **Award Prize Money** | $25K (nomination), $75K (win), $150K (Grand Prix) | Annual, per submission |
| **New Client Signing Bonus** | $20K-$100K based on client tier | On signing |

**Economy Table -- Expenses**:

| Expense | Cost Range | Frequency |
|---|---|---|
| **Salaries** | $3K-$15K/month per creative (scaled by seniority) | Monthly |
| **Office Overhead** | $20K/month base, +$5K per team member above 8 | Monthly |
| **Production Costs** | Equal to campaign budget allocation | Per campaign |
| **Recruitment** | $10K-$40K per hire (headhunter fee) | Per hire |
| **Morale Events** | $5K-$20K (team dinners, retreats, bonuses) | Discretionary |
| **Award Submission Fees** | $5K per entry | Annual |
| **Super Bowl Media Buy** | $500K-$2.5M (auction, scales with year) | Annual |

**Target Economy Balance**: The player should operate at 5-15% profit margin in years 1-2, scaling to 15-30% in years 3-5 as reputation unlocks premium clients. Cash crunches should occur 2-3 times per career, forcing difficult choices (drop a client, cut staff, take a compromising brief). The player should never feel comfortable. Comfort is the enemy of interesting decisions.

**Reputation System**:

Agency Reputation is a 0-100 score composed of three sub-scores:

| Sub-Score | Driven By | Affects |
|---|---|---|
| **Creative Prestige** (0-100) | Award wins, high-Originality campaigns, Creative Integrity score | Talent recruitment quality, award jury favorability |
| **Commercial Reliability** (0-100) | Campaign completion rate, Client Trust averages, revenue growth | Client tier access, retainer size, brief quality |
| **Cultural Relevance** (0-100) | Audience Scores, Super Bowl performance, Polarization events | Trend Chaser and Category Disruptor client attraction, media coverage |

```
Agency Reputation = (Creative Prestige * 0.35) + (Commercial Reliability * 0.35) + (Cultural Relevance * 0.30)
```

The weighting is intentional: Creative Prestige and Commercial Reliability are equally important, with Cultural Relevance as the volatile multiplier. A player who wins awards but loses clients stalls. A player who keeps clients but never takes risks plateaus. A player who manages all three ascends.

**Reputation unlocks client tiers**:

| Reputation | Client Tier Access | Super Bowl Eligibility |
|---|---|---|
| 0-25 | Tier 1: Local Heroes, Desperate Startups | No |
| 26-45 | Tier 2: + Trend Chasers, Scandal Recovery | No |
| 46-65 | Tier 3: + Legacy in Decline, Category Disruptors | Eligible (expensive) |
| 66-80 | Tier 4: + Prestige Houses | Eligible (competitive) |
| 81-100 | Tier 5: + Corporate Titans with flagship briefs | Eligible (favored) |

---

## 4. SYSTEMS INTERACTIONS

This is where the game transcends its individual parts. Let me map the feedback loops.

### 4.1 Positive Feedback Loops (Snowball Effects)

**The Prestige Spiral**: Win an award -> Creative Prestige rises -> Better talent wants to join your agency -> Better talent produces higher-Originality concepts -> Higher-Originality concepts win more awards. This is deliberate. It models how real agencies build creative reputations. But it has a cost -- see negative loops below.

**The Trust Cascade**: Deliver a successful campaign -> Client Trust rises -> Client gives more budget on next brief -> More budget enables higher Production Value -> Higher Production Value improves Audience Score -> Client Trust rises further. Reliable agencies get richer clients. This is the commercial stability path.

**The Super Bowl Flywheel**: Reach the Super Bowl -> Cultural Relevance spikes -> Premium clients come calling -> Premium clients fund next year's Super Bowl bid -> Repeat. The Super Bowl is self-reinforcing. Getting there once makes getting there again easier. But the first time is the hardest -- you have to earn it through years of building reputation.

### 4.2 Negative Feedback Loops (Balance Mechanisms)

**The Ego Tax**: Hiring high-stat talent increases salaries and increases Team Chemistry volatility. A roster full of 8+ Ego creatives produces brilliant concepts but melts down frequently, requiring Morale spending that eats into profits. The best talent is the most expensive and the most difficult. The player cannot simply hoard stars.

**The Compromise Erosion**: Every Gauntlet concession lowers Creative Integrity. Low Creative Integrity lowers Creative Prestige. Low Creative Prestige makes it harder to recruit top talent AND reduces Pushback success rates (talented people do not want to work at an agency known for caving, and clients respect pushovers less). Compromising too often is self-defeating -- the game mechanically punishes perpetual compliance. This is critical to the player fantasy: the system *agrees* with you that fighting for the work matters.

**The Overreach Penalty**: Taking on too many simultaneous campaigns (more than 3 in year 1, more than 5 by year 5) triggers team Fatigue. Fatigued creatives have all stats reduced by 2. Fatigued teams have Cohesion reduced by 15. The player who tries to scale too fast produces worse work, which lowers Audience Scores, which lowers Reputation. Growth must be paced.

**Client Concentration Risk**: If more than 50% of revenue comes from a single client and that client leaves (failed campaign, walked away in Gauntlet, budget cuts), the agency enters a **Cash Crisis** -- 3-month period with 50% reduced operating budget. Diversification is survival.

### 4.3 Emergent Possibilities

These are the moments the systems create that no designer explicitly scripted:

- **The Sacrifice Play**: A player deliberately walks away from a Corporate Titan client in the Gauntlet, tanking their Commercial Reliability but spiking Creative Prestige. Two months later, a Category Disruptor with double the budget signs because they heard the agency "has integrity." The player did not plan this -- the reputation system created the opportunity.

- **The Friction Masterpiece**: A player assembles a team with Ego variance of 8 (Meltdown risk). The team nearly implodes but generates a concept with Originality 95. The player spends every Pushback Point in the Gauntlet defending it. The ad airs at the Super Bowl and scores Legendary. The team member with the highest Ego demands a raise and threatens to leave for a rival. The player's best ad and biggest personnel crisis are the same event.

- **The Long Con**: A player takes every note from a Prestige House client for three straight campaigns, building Client Trust to 90+. On the fourth campaign -- the Super Bowl brief -- the player has 8 Pushback Points. They reject every note. The client, trusting the player's track record, approves the bold version. The player weaponized compliance as a long-term strategy.

- **The Award Trap**: A player wins the Cannes Grand Prix for a provocative ad. Creative Prestige skyrockets. But the ad was for a Local Hero client who got unexpected backlash. The client leaves. Two new Trend Chaser clients sign, but they expect the same level of boldness on every brief, and their budgets cannot support it. Success creates expectations the player cannot sustainably meet.

These emerge from the system. I did not script them. The systems create them. That is how you know the design works.

---

## 5. PROGRESSION DESIGN

### 5.1 Player Growth Vectors

The player grows along three axes simultaneously:

**Skill Growth** (player knowledge, not character stats):
- Reading hidden priorities in briefs (pattern recognition)
- Engineering team chemistry for specific outcomes (system mastery)
- Gauntlet negotiation strategy (resource management + psychology)
- Calendar optimization (when to take safe work vs. swing big)
- Cultural trend reading (meta-awareness)

**Agency Growth** (mechanical progression):
- Reputation score climbing through tiers
- Roster expanding from 4 creatives (1 team) to 16 creatives (4 teams)
- Budget ceiling rising from $200K campaigns to $3M Super Bowl spots
- Office upgrades providing passive bonuses
- Client tier access opening new brief complexity

**Narrative Growth** (emergent story):
- Creative relationships deepening (loyalty, friction, mentorship)
- Client relationships developing (trust, history, betrayal)
- Agency identity crystallizing (bold vs. reliable vs. culturally sharp)
- Legacy moments accumulating (the campaign that defined you)

### 5.2 Difficulty Curve

The difficulty curve is **stepped**, not linear. Each step introduces a new systemic pressure:

| Year | New Pressure | Max Simultaneous Campaigns | Roster Size | Available Client Tiers |
|---|---|---|---|---|
| **Year 1** | Learn the loop. One team, simple briefs, forgiving clients. | 2 | 4-6 | Tier 1 |
| **Year 2** | Multi-campaign juggling. Team Fatigue introduced. Award season begins. | 3 | 6-8 | Tier 1-2 |
| **Year 3** | Super Bowl eligibility. Media Buy Auction introduced. Rival agencies appear (if stretch goal). Cultural Trends shift. | 3-4 | 8-10 | Tier 1-3 |
| **Year 4** | Client careers shift (contacts move companies). Complex briefs with 3 non-negotiables. Talent poaching begins (rivals steal your creatives). | 4 | 10-12 | Tier 1-4 |
| **Year 5+** | Full complexity. Legacy events trigger. Creative burnout system activates (long-tenure creatives lose Ambition). The player manages decline alongside growth. | 4-5 | 12-16 | Tier 1-5 |

Each step gives the player one "safe quarter" to absorb the new pressure before the next one arrives. Year 1 Q1 is the tutorial. Year 1 Q2-Q4 is unrestricted play with training wheels. Year 2 Q1 introduces Fatigue with a forgiving brief to practice. The player is never overwhelmed because each system is introduced in isolation before it interacts with the others.

### 5.3 Pacing

The pacing alternates between **EXPAND** phases (new mechanics, new possibilities) and **TEST** phases (increased difficulty on existing mechanics):

```
Year 1: EXPAND (learn loop) -> TEST (first full year)
Year 2: EXPAND (fatigue, awards) -> TEST (balance creative vs commercial)
Year 3: EXPAND (Super Bowl, trends) -> TEST (first Super Bowl pressure)
Year 4: EXPAND (client careers, poaching) -> TEST (manage a complex ecosystem)
Year 5: EXPAND (burnout, legacy) -> TEST (sustain or rebuild)
```

Every EXPAND phase gives the player a new toy. Every TEST phase asks "can you handle all your toys at once?" The rhythm prevents both boredom (nothing new) and overwhelm (everything new).

### 5.4 Session Pacing (Within a Single Year)

A single year session (45-90 minutes) has its own internal rhythm:

```
Q1 [15 min]: Setup. New clients. Team hiring. Low stakes. Player plans.
Q2 [15 min]: Execution. Campaigns in production. First Gauntlets. Rising action.
Q3 [20 min]: Pivot. Super Bowl prep begins. Hard choices about resource allocation. Tension builds.
Q4 [20 min]: Crunch. Multiple deadlines converge. Super Bowl production. Maximum pressure.
Super Bowl [10 min]: Climax. One ad. One reaction. One result.
Year End [5 min]: Denouement. Awards. Metrics. Reflection. Reset.
```

The quarter structure ensures the player never goes more than 15-20 minutes without a major decision point or a narrative payoff. Dead time is the enemy of session engagement.

---

## 6. RISK ASSESSMENT

I have shipped a game with a broken core loop. I know what kills fun. Here is everything that could go wrong with UPFRONT and what we do about it.

### 6.1 Risk: The Approval Gauntlet Feels Like a Menu, Not a Conversation

**Severity**: CRITICAL. If the Gauntlet feels mechanical -- click Accept, click Pushback, watch numbers change -- the entire game collapses. The Gauntlet IS the game. It must feel like a tense human interaction.

**Mitigation**: Client dialogue must be procedurally varied and specific. The client does not say "reduce humor." They say "My CEO's wife watched this and she didn't laugh. She's on the board." The player is not clicking a button -- they are responding to a person. Each client archetype needs 50+ unique dialogue lines per note type. The writing investment here is non-negotiable.

**Playtest Priority**: #1. Build the Gauntlet as a standalone prototype. Four rounds. One concept. One client. If playtesters say "I wanted to fight for my ad," we have the game. If they say "I just clicked the best number," we do not.

### 6.2 Risk: Concept Forge Repetition

**Severity**: HIGH. If the player sees the same concept archetypes repeating after 15 campaigns, the creative fantasy evaporates. "Another surreal mini-film with a celebrity cameo" becomes eye-rolling.

**Mitigation**: The combinatorial space must be large enough. 8 Tones x 8 Hook Types x 5 Ambition levels x 10 Risk levels = 3,200 unique concept templates before stat variation. Each template needs a unique logline generated from a modular sentence structure: [Hook] + [Tone Modifier] + [Brand Integration] + [Twist]. With 10 variants per slot, that is 3,200 x 10,000 = 32 million logline combinations. The math works. The implementation must follow through.

**Playtest Priority**: #3. Run 30 campaigns in sequence. Track concept repetition. If a playtester recognizes a repeated structure within a single career, the pool needs expansion.

### 6.3 Risk: The Production Pipeline Is Tedious

**Severity**: MEDIUM. Budget allocation is important but not exciting. If the player is spending 90 seconds on a slider screen every campaign, the pacing dies.

**Mitigation**: Keep it fast. Five sliders. Drag and drop. Auto-fill suggestion based on concept stats (one click for "recommended allocation"). The expert player overrides the suggestion; the casual player accepts it. Total interaction time target: 30-45 seconds, not 60+.

**Playtest Priority**: #5. Time how long players spend on production. If average exceeds 60 seconds, simplify. If players consistently use auto-fill, consider making it the default with manual override.

### 6.4 Risk: Agency Economy Is Either Too Tight or Too Loose

**Severity**: HIGH. If the player is always broke, every decision becomes "what can I afford" instead of "what do I believe in." If the player is always flush, budget allocation loses all tension.

**Mitigation**: Target 2-3 genuine cash crises per career, always triggered by narrative events (lost client, expensive hire, Super Bowl bid), not by baseline math. The player should feel prosperous-but-stretched, not desperate. Baseline revenue should cover salaries + overhead with 10% buffer. Campaign bonuses fund ambition. Super Bowl bids are the luxury the player stretches for.

**Playtest Priority**: #4. Run three full 5-year careers with different playstyles (cautious, balanced, aggressive). Track cash flow curves. If any playstyle hits zero cash more than 3 times, the economy needs loosening. If any playstyle never dips below 50% reserves, it needs tightening.

### 6.5 Risk: Team Management Becomes Spreadsheet Optimization

**Severity**: MEDIUM. If players reduce creatives to stat blocks and optimize team composition purely by numbers, the character fantasy dies. These are supposed to be *people*, not resources.

**Mitigation**: Creatives must have narrative weight. Periodic "life events" (a copywriter's partner is ill, an art director gets a job offer from a rival, a creative director has a crisis of confidence after a killed campaign) force the player to respond with empathy, not optimization. The events affect stats temporarily but the player's response affects loyalty permanently. A creative whose crisis you ignored works at 80% and leaves within 2 years. A creative whose crisis you supported works at 110% and stays through your worst year.

**Playtest Priority**: #6. Ask playtesters to name their favorite creative. If they can, the character system works. If they describe creatives by stats ("my 8-Vision guy"), it needs more personality.

### 6.6 Risk: The Super Bowl Is Anticlimactic

**Severity**: HIGH. The Super Bowl is the entire session's payoff. If it feels like "another ad broadcast but with bigger numbers," the climax fails.

**Mitigation**: The Super Bowl sequence must be mechanically distinct. Longer broadcast animation. Expanded reaction panel with regional breakdowns. Post-game press coverage. Monday Morning meeting with the client. A week of in-game aftermath (memes, discourse, competitor responses). The Super Bowl is not a broadcast -- it is an *event* that occupies the last 10 minutes of the session with escalating reveals. The player should hold their breath.

**Playtest Priority**: #2. Build the Super Bowl as a vertical slice. One ad. Full reaction sequence. Full Monday Morning. If playtesters want to play again immediately to try a different approach, the climax works.

### 6.7 Risk: Late-Game Stagnation

**Severity**: MEDIUM. By year 5, the player may have "solved" the systems. Optimal team compositions, reliable Gauntlet strategies, and predictable client behaviors could make the game feel automated.

**Mitigation**: Year 5+ introduces **Creative Burnout** (long-tenure creatives lose Ambition and need sabbaticals or new challenges), **Industry Disruption** events (a major cultural shift that invalidates current trend assumptions), and **Legacy Dilemmas** (choices that force the player to sacrifice one sub-reputation for another). The late game is not about growing -- it is about *sustaining* in the face of entropy. The agency that was perfect in year 4 is rotting by year 6 unless the player actively reinvents.

**Playtest Priority**: #7. Accelerated late-game test. Start playtesters at year 4 with an established agency. Does the game still present interesting choices? If not, the late-game pressures need sharpening.

---

## 7. BALANCE FRAMEWORK SUMMARY

### Core Tension Ratios

These are the design targets for systemic balance:

| Tension | Target Ratio | Meaning |
|---|---|---|
| Bold vs. Safe campaigns | 40/60 in year 1, 60/40 by year 3 | Early play rewards safety. Mid-game rewards risk. |
| Client Trust vs. Creative Integrity | The player should be able to max one but not both | Forces identity choice |
| Revenue from retainers vs. bonuses | 60/40 | Stability from retainers, upside from performance |
| Team Synergy vs. Friction teams | Player should use both, roughly 50/50 | Each has distinct advantages |
| Gauntlet Accept vs. Pushback | 60/40 Accept-heavy in year 1, 50/50 by year 3, player-determined by year 5 | Mirrors real power dynamics |
| Super Bowl participation | Every 2-3 years for average player, every year for expert | The Super Bowl should feel earned, not routine |

### Stat Scaling Reference

All player-visible stats (Concept stats, Agency Reputation, Client Trust, Creative Integrity) use a 0-100 scale with the following general interpretation:

| Range | Quality | Frequency Target |
|---|---|---|
| 0-20 | Terrible | 5% of outcomes |
| 21-40 | Below Average | 15% of outcomes |
| 41-60 | Average | 40% of outcomes |
| 61-80 | Good | 25% of outcomes |
| 81-90 | Excellent | 10% of outcomes |
| 91-100 | Legendary | 5% of outcomes |

The distribution is intentionally bell-curved around Average. Legendary outcomes are rare. The player must *engineer* excellence through deliberate team composition, Gauntlet strategy, and production allocation. Excellence is not random -- it is systemic mastery with a randomness floor. The best team in the best conditions with perfect Gauntlet play should produce Good-or-better results 80% of the time and Excellent-or-better 40% of the time. Legendary requires everything to align -- skill, system mastery, and a little luck. That is how it should feel.

---

## 8. OPEN QUESTIONS FOR PLAYTESTING

These are the questions that only playtesting can answer. I have opinions. Playtesters have data. Data wins.

1. **Gauntlet Round Count**: Is 3-5 rounds the right range? Three rounds may feel too fast for complex negotiations. Five rounds may feel like a slog for simple briefs. Should the round count scale with client tier? Test with fixed 3, fixed 4, and dynamic 3-5.

2. **Pushback Point Economy**: Is the current formula generous enough for the early game? A new player with 4 Pushback Points against a conservative client may feel they can never fight. Should year 1 have a +2 "beginner bonus" to Pushback Points that phases out by year 2?

3. **Campaign Duration Feel**: Does a 5-8 minute campaign feel like a satisfying short story, or does it need to be 10-12 minutes with more beats? The Gauntlet may need to breathe more. The production phase may need to breathe less.

4. **Number of Simultaneous Campaigns**: The pitch suggested 3-5. Is 3 the sweet spot for mental load, or can players handle 4 without losing track of individual campaigns? This depends on how distinct the campaigns feel, which depends on how well the Concept Forge differentiates them.

5. **Creative Personality Depth**: How much narrative event content do creatives need before players form emotional attachments? Is 3 events per creative per year enough? 5? Do events need to be unique per creative, or can they be archetypal with name/stat swaps?

6. **Concept Selection Engagement**: Does choosing from 2-3 generated concepts feel like creative direction, or does it feel like a multiple-choice test? Should the player have more input -- e.g., selecting a Tone *before* generation to constrain the output? Test both approaches.

7. **Cultural Trend Readability**: Can players actually learn to read and predict cultural trends from the in-game media feed, or does it feel random? If players cannot anticipate trends, the system rewards luck, not skill. The trend telegraph window (how far in advance trends are signaled) needs calibration.

8. **Walk Away Frequency**: How often do players use the Walk Away option in the Gauntlet? If never, the stakes are too low or the penalty is too high. If constantly, the penalty is too low or the frustration is too high. Target: 5-10% of Gauntlets end in Walk Away.

9. **Year Length Satisfaction**: Is 45-90 minutes the right session length for a calendar year? If players disengage at 60 minutes, the year needs compression. If players want more, the year needs more events. Measure where attention drops.

10. **Super Bowl as Motivation**: Does the Super Bowl create sufficient pull to sustain 45+ minutes of play? Or does the player need mid-year climax events (Cannes results, major client pitch wins) to maintain momentum through the middle quarters? My instinct says the Super Bowl alone is enough. But instinct is not data.

---

## CLOSING NOTE

This document is a first pass. Design is iteration, and iteration requires playtesting. But every system here is connected. The Brief feeds the Team feeds the Forge feeds the Gauntlet feeds the Production feeds the Broadcast feeds the Reputation feeds the next Brief. The loop is closed. The systems talk. The depth is real.

The question this game asks -- **what are you willing to sacrifice to protect the work?** -- is embedded in every mechanic. The Gauntlet makes you feel it. The economy makes you pay for it. The reputation system makes you live with it. That is not a theme pasted onto a spreadsheet. That is a theme expressed through systems.

Find the Gauntlet. Find the fun. Build from there.

-- REED
