# UPFRONT — QA Plan

**Author**: CRASH (QA Lead)
**Version**: 1.0
**Date**: 2026-02-07
**Status**: Pre-Production QA Strategy

---

> "A bug isn't fixed until it's verified. Then regression test everything it touched."

I've read the pitch, the design doc, the narrative bible, and the tech doc. I know what this game promises: a management sim where the core loop is negotiation, not optimization. Where the Approval Gauntlet makes you *feel* the tension of defending creative work. Where the Super Bowl is a climactic spectacle.

Here's the problem: Everything connects to everything. The Brief System feeds the Team Manager feeds the Concept Forge feeds the Gauntlet feeds Production feeds Broadcast feeds Reputation feeds the next Brief. One broken link breaks the entire chain. One stat miscalculation in the Concept Forge cascades into broken Gauntlet negotiations and meaningless Broadcast results.

This is not a game you can test in pieces and ship. This is a game where the systems talk to each other, and the QA plan must reflect that.

What follows is how we test it, what could break, and what we do when it does.

Define "works."

---

## 1. QA PHILOSOPHY & APPROACH

### 1.1 Core Principles

**Test the loop, not the features.** The core loop is the game. If the 5-minute campaign cycle from Brief to Broadcast is broken, nothing else matters. We test that loop first, last, and always.

**Systems testing before content testing.** Mechanics must work before we worry about whether the 50th brief feels repetitive. A perfect content library on a broken Concept Forge is worthless.

**Find breaking points, not happy paths.** The player who follows the tutorial and plays normally is not the problem. The problem is the player who walks away from every Gauntlet, fires their entire roster mid-campaign, or hits the Super Bowl with zero budget. Edge cases are someone's entire experience.

**Document everything.** A bug report without repro steps is a rumor. A repro without expected-vs-actual is incomplete. A bug without severity is impossible to prioritize.

---

### 1.2 Testing Phases

**Phase 1: Systems Verification (Months 1-3, Prototype)**
- Test each system in isolation with mock data.
- Verify math: stat calculations, chemistry formulas, persuasion checks.
- No UI required. Test via debug logs and automated tests where possible.
- **Goal**: Prove the math works before building the game on top of it.

**Phase 2: Integration Testing (Months 4-6, Production)**
- Test system-to-system handoffs: Brief → Team → Forge → Gauntlet → Production → Broadcast.
- Verify event bus communication: Does GauntletCompleteEvent trigger ProductionPipeline correctly?
- Test with real UI but limited content (10 briefs, 5 creatives, 3 clients).
- **Goal**: Prove the systems talk to each other correctly.

**Phase 3: Content & Balance Testing (Months 7-9, Alpha)**
- Test with full content library: 50+ briefs, 30+ loglines, 20+ creatives.
- Look for repetition, outliers, exploits.
- Test economy balance across 5+ full career playthroughs.
- **Goal**: Prove the game is playable, balanced, and not repetitive.

**Phase 4: Stress & Compatibility Testing (Months 10-11, Beta)**
- Extended session testing: 10-hour sessions, multiple careers, edge cases.
- Platform testing: Windows, macOS, Linux, min-spec PCs, various screen resolutions.
- Save/load testing: Corrupt saves, version migrations, autosave failures.
- **Goal**: Prove the game won't crash, corrupt, or break under player abuse.

**Phase 5: Final Verification & Regression (Month 12, Release Candidate)**
- Full regression pass: Re-test all critical paths after final bug fixes.
- Zero-tolerance for crash bugs, save corruption, or soft locks.
- Playtest final build on fresh installs (no dev environment).
- **Goal**: Ship a stable product. No excuses.

---

## 2. TEST PLAN BY FEATURE AREA

### 2.1 BRIEF SYSTEM

**What it does**: Generates procedurally varied client briefs from JSON templates.

#### Happy Path Test Cases

| Test ID | Preconditions | Steps | Expected Result |
|---------|--------------|-------|-----------------|
| **BS-001** | New game started | Player views first available brief | Brief displays with brand archetype, budget, target demo, non-negotiables, flavor text |
| **BS-002** | Agency Reputation = 30 | Generate 10 briefs | All briefs are Tier 1-2 clients (Local Heroes, Desperate Startups, Trend Chasers) |
| **BS-003** | Agency Reputation = 70 | Generate 10 briefs | Briefs include Tier 4 clients (Prestige Houses, Corporate Titans) |
| **BS-004** | 50 briefs generated in sequence | Check for logline/flavor text repetition | No exact duplicate text. Similar structure OK, identical phrasing = fail |

#### Sad Path Test Cases

| Test ID | Preconditions | Steps | Expected Result |
|---------|--------------|-------|-----------------|
| **BS-101** | Brief with 3 non-negotiables | Attempt to generate concept that violates all 3 | Gauntlet should heavily penalize or auto-fail |
| **BS-102** | Budget = $50K (minimum) | Assign high-ambition team (Ambition 8+) | Concept should generate but with Ambition Gap penalty warning |
| **BS-103** | Invalid JSON in briefs_config.json | Launch game | Game should log error and fall back to default briefs or fail gracefully with error screen |

#### Evil Path Test Cases

| Test ID | Preconditions | Steps | Expected Result |
|---------|--------------|-------|-----------------|
| **BS-201** | Multiple briefs available | Accept all briefs simultaneously (5+) | System should either cap at max campaigns or trigger Overreach Penalty / team Fatigue |
| **BS-202** | Brief with RiskTolerance = 1 (extremely conservative) | Generate high-CulturalRisk concept (Risk 9+) | Client should issue multiple De-Risk notes and potentially walk out if player pushes back |
| **BS-203** | Save/load during brief selection | Save game with brief open, reload | Brief state should persist exactly (same brief, same stats, same text) |

---

### 2.2 TEAM CHEMISTRY ENGINE

**What it does**: Calculates team cohesion from creative stats, applies modifiers to concept generation.

#### Happy Path Test Cases

| Test ID | Preconditions | Steps | Expected Result |
|---------|--------------|-------|-----------------|
| **TC-001** | Assign 4 creatives with matching Taste tags (all prefer "Funny") | Calculate chemistry | Cohesion = 70+ (Synergy), concepts biased toward Humor stat |
| **TC-002** | Assign 4 creatives with avg Craft = 8+ | Calculate chemistry | Cohesion bonus from Craft, concepts have high Production Value |
| **TC-003** | Assign team with Ego variance = 1 (all similar Ego) | Calculate chemistry | No Ego penalty, stable concept generation |

#### Sad Path Test Cases

| Test ID | Preconditions | Steps | Expected Result |
|---------|--------------|-------|-----------------|
| **TC-101** | Assign 4 creatives with Ego = [9, 9, 3, 3] (high variance) | Calculate chemistry | Cohesion -16 (from Ego Variance * 4), Friction or Meltdown risk |
| **TC-102** | Team with Cohesion = 15 (Meltdown range) | Run campaign for 1 week in-game time | At least 1 creative threatens to quit, production halts until Morale action taken |
| **TC-103** | Ambition gap = [9, 2] (difference of 7) | Calculate chemistry | Cohesion -14 (from Ambition Gap * 2) |

#### Evil Path Test Cases

| Test ID | Preconditions | Steps | Expected Result |
|---------|--------------|-------|-----------------|
| **TC-201** | Deliberately engineer Meltdown (Cohesion < 20) | Run 3 campaigns with same Meltdown team without Morale actions | Team should either quit, refuse to work, or produce extremely low-quality concepts |
| **TC-202** | Assign team mid-campaign, then fire one member before Concept Generation completes | Trigger Concept Forge | System should either use original team or gracefully handle missing creative (error or auto-replace) |
| **TC-203** | Creative with Speed = 10, Ego = 10, Ambition = 10 (max volatility) | Assign to team | Concepts should be unpredictable, may trigger budget overruns or ignore player notes |

---

### 2.3 CONCEPT FORGE

**What it does**: Generates 2-3 ad concepts with stats, tone, hook, logline based on team/brief.

#### Happy Path Test Cases

| Test ID | Preconditions | Steps | Expected Result |
|---------|--------------|-------|-----------------|
| **CF-001** | Team with Vision = 8+, brief with goal = "Brand Awareness" | Generate concepts | At least 1 concept has Originality > 60 |
| **CF-002** | Team with Craft = 8+, Synergy chemistry | Generate concepts | All concepts have Production Value > 60 |
| **CF-003** | Brief with "must include mascot" non-negotiable | Generate concepts | At least 1 concept mentions mascot in logline or tags |
| **CF-004** | Generate 30 concepts in sequence | Check for logline repetition | No exact duplicate loglines. Less than 10% "very similar" loglines (same hook/tone/structure) |

#### Sad Path Test Cases

| Test ID | Preconditions | Steps | Expected Result |
|---------|--------------|-------|-----------------|
| **CF-101** | Team with Friction chemistry (Cohesion = 25) | Generate 5 concepts | Stat variance should be high (some stats 80+, some 30-), unpredictable |
| **CF-102** | Team with all stats = 3 (low-quality team) | Generate concepts | All concepts should have stats in 20-40 range (low quality) |
| **CF-103** | Cultural Risk = 10, client RiskTolerance = 2 | Generate concepts | Concepts should have high Originality but low Brand Clarity, mismatch should be obvious |

#### Evil Path Test Cases

| Test ID | Preconditions | Steps | Expected Result |
|---------|--------------|-------|-----------------|
| **CF-201** | Spam "Generate Concepts" button 100 times | Measure memory usage | No memory leak. Concepts should continue generating or system should cap generation attempts |
| **CF-202** | Generate concept, save game, reload, regenerate with same team/brief | Compare concepts | Concepts should differ (RNG seed should not be deterministic across saves) OR should be identical if RNG seed is intentionally saved |
| **CF-203** | Brief with all non-negotiables violated by generated concept | Proceed to Gauntlet | Client should reject immediately or issue 3+ notes demanding total rework |

---

### 2.4 APPROVAL GAUNTLET

**This is the game. This is where we succeed or fail.**

**What it does**: Multi-round negotiation FSM where player defends concept against client notes.

#### Happy Path Test Cases

| Test ID | Preconditions | Steps | Expected Result |
|---------|--------------|-------|-----------------|
| **AG-001** | Concept with BrandClarity = 65, client MinBrandClarity = 60 | Start Gauntlet | Client satisfaction = high, 0-1 notes issued, approved in 2-3 rounds |
| **AG-002** | Client RiskTolerance = 7, concept CulturalRisk = 5 | Start Gauntlet | Client comfortable with risk, minimal De-Risk notes |
| **AG-003** | Player has 5 Pushback Points, client issues 2 notes, player pushes back on 1 | Spend 1 Pushback Point, pass persuasion check | Note withdrawn, ClientTrust -2, CreativeIntegrity +5 |
| **AG-004** | Player accepts all client notes (3 notes over 3 rounds) | Complete Gauntlet | ClientTrust +15 total, CreativeIntegrity -9, concept stats shifted per note effects |

#### Sad Path Test Cases

| Test ID | Preconditions | Steps | Expected Result |
|---------|--------------|-------|-----------------|
| **AG-101** | Pushback fails (persuasion roll below threshold) | Lose 1 Pushback Point | ClientTrust -8, note remains, client adds harder note next round |
| **AG-102** | ClientTrust drops below 20 after failed pushback | Continue Gauntlet | Client walks out (GauntletOutcome = ClientWalkout), campaign killed, ClientTrust -20 |
| **AG-103** | Player uses Compromise option | Stat shifts apply at 50% of note's effect | ClientTrust +2, CreativeIntegrity -1, stats change by half |
| **AG-104** | Round limit reached (5 rounds), client still issuing notes | Gauntlet terminates | If concept viable (satisfaction > 50), approve. Otherwise, kill campaign |

#### Evil Path Test Cases

| Test ID | Preconditions | Steps | Expected Result |
|---------|--------------|-------|-----------------|
| **AG-201** | Player chooses "Walk Away" on round 1 | End Gauntlet immediately | Campaign killed, ClientTrust -20, CreativeIntegrity +15, brief returns to pool or client blacklisted |
| **AG-202** | Spend all Pushback Points, fail all checks, ClientTrust < 20 | Force worst-case scenario | Client walks out, agency reputation takes hit, relationship damaged permanently |
| **AG-203** | Client issues "Panic Note" (forces complete Tone change) | Accept note | All concept stats reroll with -10 penalty, logline regenerates, essentially new concept |
| **AG-204** | Save/load mid-Gauntlet (between rounds) | Reload save | Gauntlet state should restore exactly (current round, remaining Pushback Points, active notes, concept stat changes) |
| **AG-205** | Client issues Scope Creep note ("add celebrity"), player accepts | Budget increases by 30% | If player does not have cash reserves, production phase should show red warning or auto-fail due to insufficient funds |
| **AG-206** | Mash "Pushback" button rapidly (input spam) | System should queue or ignore rapid inputs | UI should not break, Pushback should execute once per round, no duplicate Pushback spends |

---

### 2.5 PRODUCTION PIPELINE

**What it does**: Budget allocation across 5 categories, applies stat modifiers, enforces Ambition Gap penalty.

#### Happy Path Test Cases

| Test ID | Preconditions | Steps | Expected Result |
|---------|--------------|-------|-----------------|
| **PP-001** | Budget = $500K, allocate 20% per category | Allocate evenly | All stats receive minor bonuses, no warnings |
| **PP-002** | Concept has Ambition = 3, budget = $600K | Allocate budget | No Ambition Gap penalty (budget supports Ambition 3 = $600K / $200K) |
| **PP-003** | Use Auto-Suggest button | System calculates optimal allocation | Allocation suggested, player can accept or adjust, one-click workflow |

#### Sad Path Test Cases

| Test ID | Preconditions | Steps | Expected Result |
|---------|--------------|-------|-----------------|
| **PP-101** | Concept has Ambition = 5, budget = $400K | Attempt production | Ambition Gap = 3 (5 - 2), all stats suffer -24 penalty, red warning displayed |
| **PP-102** | Allocate 60% to VFX (above diminishing returns threshold of 40%) | Complete allocation | VFX bonuses apply but with diminishing returns (half effectiveness above 40%) |
| **PP-103** | Total allocation = 95% (incomplete) | Attempt to proceed | System should prevent progression or auto-allocate remaining 5% to default category |

#### Evil Path Test Cases

| Test ID | Preconditions | Steps | Expected Result |
|---------|--------------|-------|-----------------|
| **PP-201** | Allocate 100% to one category, 0% to all others | Proceed to broadcast | One stat heavily boosted, others suffer. Minimum spend requirements (5-10% per category) should trigger warnings or block progression |
| **PP-202** | Budget insufficient after Gauntlet Scope Creep note | Proceed to production | If cash reserves < increased budget, production should fail or force player to take emergency loan / drop campaign |
| **PP-203** | Save/load during budget allocation | Reload save | Allocation sliders should restore to saved positions exactly |

---

### 2.6 BROADCAST & REACTION SYSTEM

**What it does**: Simulates ad airing, calculates Audience Score, displays reactions, updates metrics.

#### Happy Path Test Cases

| Test ID | Preconditions | Steps | Expected Result |
|---------|--------------|-------|-----------------|
| **BR-001** | Concept with Humor = 75, Emotion = 65, BrandClarity = 60 | Broadcast ad | Audience Score = 60-75 (Hit range), reactions show laughter and positive sentiment |
| **BR-002** | Super Bowl ad (amplifier active) | Broadcast during Super Bowl | Audience Score +15 flat bonus, all brand metrics doubled |
| **BR-003** | Ad with Originality = 85, Cultural Risk = 8 | Broadcast ad | Polarization check triggers, 60% chance of split opinion or controversy |

#### Sad Path Test Cases

| Test ID | Preconditions | Steps | Expected Result |
|---------|--------------|-------|-----------------|
| **BR-101** | Concept with all stats < 40 (poor quality) | Broadcast ad | Audience Score = 0-25 (Forgotten), no brand metric change, ClientTrust -5, no awards eligibility |
| **BR-102** | Polarization Roll > 85 (Controversy Event) | Complete broadcast | Media coverage triggered, client panic call, forced crisis response, brand trust splits |
| **BR-103** | Cultural Fit negative (ad tone mismatches current trend) | Broadcast ad | Audience Score penalty, lower engagement in reaction panel |

#### Evil Path Test Cases

| Test ID | Preconditions | Steps | Expected Result |
|---------|--------------|-------|-----------------|
| **BR-201** | Ad with Cultural Risk = 10, client RiskTolerance = 2, Audience Score = 85 | Broadcast ad | Controversy triggered, client enraged despite high score, ClientTrust plummets, relationship damaged |
| **BR-202** | Broadcast 5 ads simultaneously (multiple campaigns completing same quarter) | Render all broadcast sequences | No framerate drop below 30 FPS, no memory leak, all sequences play correctly in sequence or parallel |
| **BR-203** | Storyboard animatic assets missing (deleted from build) | Attempt broadcast | System should fall back to placeholder images or log error gracefully, not crash |

---

### 2.7 REPUTATION & ECONOMY SYSTEM

**What it does**: Tracks agency reputation across 3 sub-scores, manages cash flow, unlocks client tiers.

#### Happy Path Test Cases

| Test ID | Preconditions | Steps | Expected Result |
|---------|--------------|-------|-----------------|
| **RE-001** | Complete campaign with Audience Score = 75 | Update reputation | Creative Prestige +3-5, Cultural Relevance +2-4 depending on Originality/Risk |
| **RE-002** | Reputation crosses 46 threshold | Check client tier access | Tier 3 clients (Category Disruptors) become available, Super Bowl eligibility unlocked |
| **RE-003** | Monthly expenses = $50K, revenue = $60K | Process month-end | Cash increases by $10K, no warnings |

#### Sad Path Test Cases

| Test ID | Preconditions | Steps | Expected Result |
|---------|--------------|-------|-----------------|
| **RE-101** | Cash = $20K, upcoming monthly expenses = $50K | Process month-end | Cash goes negative, Cash Crisis triggered, 3-month 50% budget reduction, player forced to cut costs or fire staff |
| **RE-102** | 60% revenue from single client, client leaves (fired or walked away) | Lose client | Client Concentration Risk triggered, Cash Crisis, revenue drops 60%, emergency measures required |
| **RE-103** | Reputation = 65, player walks away from 3 clients in a row (CreativeIntegrity +45) | Update reputation | Creative Prestige spikes but Commercial Reliability plummets, reputation may stay flat or drop depending on weighting |

#### Evil Path Test Cases

| Test ID | Preconditions | Steps | Expected Result |
|---------|--------------|-------|-----------------|
| **RE-201** | Hire entire roster to max (16 creatives), max salaries | Run for 3 months with no campaigns | Cash bleeds out rapidly, forced bankruptcy or roster cuts, game should warn or intervene |
| **RE-202** | Exploit: Take multiple high-budget briefs, walk away from Gauntlet to bank retainer fees without completing work | Repeat 10 times | System should track completion rate, lower Commercial Reliability, clients stop offering work if pattern detected |
| **RE-203** | Reputation = 95, deliberately fail 5 campaigns in a row | Tank reputation | Reputation should drop below 70, lose client tier access, talent leaves, downward spiral possible |

---

### 2.8 SAVE/LOAD SYSTEM

**What it does**: Serializes game state to JSON, restores on load, handles autosaves and version migration.

#### Happy Path Test Cases

| Test ID | Preconditions | Steps | Expected Result |
|---------|--------------|-------|-----------------|
| **SL-001** | Mid-campaign (Gauntlet round 2) | Save game manually | Save file created, all state serialized (campaign state, Gauntlet round, Pushback Points, concept stats) |
| **SL-002** | Load save from SL-001 | Restore game | Gauntlet resumes at round 2 with exact state (same notes, same Pushback Points, same concept) |
| **SL-003** | Autosave triggers at quarter-end | Play through Q1 | Autosave file created, labeled with timestamp and "Year 1 Q1" |
| **SL-004** | 3 rotating autosave slots | Play through 4 quarters | Oldest autosave (Q1) overwritten by Q4 autosave, only 3 most recent exist |

#### Sad Path Test Cases

| Test ID | Preconditions | Steps | Expected Result |
|---------|--------------|-------|-----------------|
| **SL-101** | Save file JSON manually corrupted (invalid syntax) | Attempt to load save | Game detects corruption, displays error message, does not crash, offers option to load backup or start new game |
| **SL-102** | Save file from older version (SaveVersion = 1, current = 2) | Load old save | Migration system applies, new fields added with defaults, save loads successfully |
| **SL-103** | Disk full during autosave | Trigger autosave | Save fails gracefully, logs error, does not crash, player warned on next manual save attempt |

#### Evil Path Test Cases

| Test ID | Preconditions | Steps | Expected Result |
|---------|--------------|-------|-----------------|
| **SL-201** | Spam save button 50 times rapidly | Rapid-fire saves | System should queue saves or ignore duplicate requests, no crash, no file corruption |
| **SL-202** | Save file size = 10MB (extremely bloated due to 10+ year career) | Load save | Load time should remain < 5 seconds (if longer, investigate compression or delta saves) |
| **SL-203** | Delete save file while game is running, attempt to load deleted save | Load attempt | System detects missing file, error message, does not crash |
| **SL-204** | Cloud save sync conflict (Steam Cloud has different version than local) | Launch game with conflicting saves | Game should prompt player to choose local or cloud version, not silently overwrite |

---

## 3. EDGE CASE MATRIX

These are the "what happens if the player does THIS" scenarios. Edge cases are not bugs unless the system breaks. They are opportunities to discover design holes.

### The Gauntlet Edge Cases

| Scenario | Expected Behavior | Failure Mode |
|----------|------------------|--------------|
| Player pushes back on every note with 0 Pushback Points | Pushback button disabled or greyed out when points = 0 | Crash or negative Pushback Points |
| Client issues note, player accepts, client issues same note again next round | Client should not repeat notes OR should acknowledge "you already addressed this" | Infinite note loop |
| Player walks away after investing 4 Pushback Points | Points lost, campaign killed, no refund | Player expects refund or feels cheated (design decision, not bug, but test sentiment) |
| Concept's BrandClarity = 0 after client notes | Client should be satisfied OR recognize impossibility and walk out | Client continues issuing notes despite stat bottoming out |
| Gauntlet lasts 10+ rounds due to player rejecting compromise | Round cap should trigger termination at 5 rounds | Infinite Gauntlet loop |

### The Economy Edge Cases

| Scenario | Expected Behavior | Failure Mode |
|----------|------------------|--------------|
| Cash goes negative | Cash Crisis triggered, player forced to take emergency measures | Game allows negative cash indefinitely (exploit) |
| Fire entire roster mid-year | Active campaigns fail, clients leave, reputation tanks | Crash or soft lock (no staff to run campaigns) |
| Take 10 briefs, complete 0 campaigns | Clients leave, Commercial Reliability drops to 0, no new briefs offered | Game continues offering briefs despite 100% failure rate |
| Super Bowl bid = $2.5M, player has $100K cash | Bid rejected or player forced to take loan | Game allows bid, player goes bankrupt |
| Revenue = $0 for 12 months (player takes no briefs) | Agency should collapse or game should warn/intervene | Game allows indefinite idling |

### The Progression Edge Cases

| Scenario | Expected Behavior | Failure Mode |
|----------|------------------|--------------|
| Reach year 10 with Reputation = 10 (lowest tier) | Only Tier 1 clients available, no Super Bowl access, limited growth | Game continues offering high-tier clients despite low rep |
| Win 5 Cannes Grand Prix in a row | Creative Prestige maxed, top talent recruitment, rival agencies envy | No recognition of exceptional achievement |
| Creative with 10 years tenure, never given meaningful work | Loyalty = 0, threatens to quit or leaves | Creative stays indefinitely despite neglect |
| Player deliberately engineers Meltdown team every campaign | Team quits, replacement costs spike, morale actions required every week | Game allows indefinite Meltdown abuse |

---

## 4. SYSTEMS INTEGRATION TESTING

These tests verify that the event bus and state machine handoffs work correctly. A failure here means two systems are not communicating properly.

### Integration Test Suite

| Test ID | Systems Involved | Test Case | Pass Condition |
|---------|-----------------|-----------|---------------|
| **INT-001** | Brief → Team → Forge | Assign team to brief, trigger Concept Forge | ConceptsReadyEvent fires with 2-3 valid concepts |
| **INT-002** | Forge → Gauntlet | Select concept, start Gauntlet | GauntletStartEvent fires, client data loaded correctly |
| **INT-003** | Gauntlet → Production | Approve concept in Gauntlet | GauntletCompleteEvent fires, Production Pipeline starts |
| **INT-004** | Production → Broadcast | Complete budget allocation | ProductionCompleteEvent fires, Broadcast Engine calculates Audience Score |
| **INT-005** | Broadcast → Reputation | Ad airs with Audience Score = 75 | AdAiredEvent fires, Reputation System updates Creative Prestige and Cultural Relevance |
| **INT-006** | Reputation → Brief | Reputation crosses tier threshold (46 → 47) | Next brief generation includes Tier 3 clients |
| **INT-007** | Economy → Roster | Cash < monthly expenses | Cash Crisis triggered, Morale events fire, creatives react to budget cuts |
| **INT-008** | Gauntlet (Walk Away) → Economy | Walk away from client in Gauntlet | ClientTrust drops, campaign revenue lost, brief returns to pool |
| **INT-009** | Multiple campaigns running simultaneously | 3 campaigns in different states (Gauntlet, Production, Broadcast) | All campaigns progress independently, no state collision |
| **INT-010** | Save/Load across all systems | Save mid-campaign (Gauntlet), load | All systems restore state correctly (Brief, Team, Concept, Gauntlet, Economy, Reputation) |

---

## 5. SUPER BOWL TESTING

**The Super Bowl is the climax. If this breaks, the entire session arc fails.**

### Super Bowl Test Matrix

| Test ID | Scenario | Expected Outcome | Failure Mode |
|---------|----------|------------------|--------------|
| **SB-001** | Reach Super Bowl in Year 2 with Reputation = 55 | Media buy auction opens, player bids $1.5M, wins slot | Auction does not appear or player blocked despite meeting requirements |
| **SB-002** | Super Bowl ad with Audience Score = 90 (Legendary) | +15 bonus applied, metrics doubled, Monday Morning meeting with ecstatic client, award nomination guaranteed | Audience Score not amplified or metrics not doubled |
| **SB-003** | Super Bowl ad with Audience Score = 30 (Forgotten) | Disaster outcome, client rage, reputation drop, rival agencies mock | No negative consequences or same outcome as regular campaign |
| **SB-004** | Polarization triggered during Super Bowl (Cultural Risk = 10) | Controversy Event, media firestorm, brand trust splits dramatically, client panic | Polarization mechanics identical to regular campaign (should be amplified) |
| **SB-005** | Rival agency also bids on Super Bowl slot | Auction price increases, player may lose bid if outbid | Rival bids ignored or auction non-competitive |
| **SB-006** | Player wins Super Bowl slot but cannot afford production budget (Ambition 5, insufficient funds) | Production phase shows red warning, player forced to scale down or cancel | Game allows production without funds, economy breaks |
| **SB-007** | Save/load during Super Bowl sequence (mid-broadcast) | Reload save, sequence resumes from start of broadcast with same results | Sequence replays with different RNG results or crashes |

---

## 6. PERFORMANCE & STRESS TESTING

### Performance Benchmarks

| System | Metric | Target | Test Method |
|--------|--------|--------|-------------|
| **Frame Rate** | FPS during Gauntlet UI | 60 FPS @ 1080p (PC) | Unity Profiler, 5-minute Gauntlet session |
| **Frame Rate** | FPS during Broadcast sequence | 60 FPS @ 1080p (PC) | Profiler, measure full Super Bowl broadcast |
| **Memory Usage** | RAM consumption during gameplay | < 1.5GB (PC), < 900MB (Switch) | Profiler, 2-hour session |
| **Load Time** | Cold start to main menu | < 5 seconds | Stopwatch, average of 10 launches |
| **Load Time** | Load save file (Year 5 career) | < 3 seconds | Stopwatch, save file with 50+ campaigns in history |
| **Save Time** | Write save to disk | < 1 second | Stopwatch, measure autosave during gameplay |
| **Concept Generation** | Time to generate 3 concepts | < 100ms | Debug.Log timer in ConceptForge |
| **Gauntlet Performance** | Frame time during client reaction | < 16ms CPU, < 16ms GPU | Profiler, measure per-frame during note issuance |

### Stress Tests

| Test ID | Scenario | Duration | Pass Condition |
|---------|----------|----------|---------------|
| **STRESS-001** | Continuous play session | 10 hours | No crash, no memory leak (RAM stable), no save corruption |
| **STRESS-002** | Rapid campaign cycling | Complete 50 campaigns back-to-back | No performance degradation, frame rate stable |
| **STRESS-003** | Maximum roster size (16 creatives) | Play full year with 5 simultaneous campaigns | Memory usage < target, no slowdown |
| **STRESS-004** | Spam UI interactions | Click all buttons rapidly for 5 minutes | No crash, no duplicate actions, UI responsive |
| **STRESS-005** | Save/load loop | Save and load 100 times in succession | No corruption, load time remains < 3 seconds |
| **STRESS-006** | Extended career (10+ years) | Play through 10 years, 120+ campaigns | Save file size < 2MB, load time < 5 seconds |

### Platform-Specific Tests (If Switch Port Active)

| Test ID | Platform | Test Case | Pass Condition |
|---------|----------|-----------|---------------|
| **PLAT-001** | Switch Docked | Full campaign cycle | 30 FPS stable, no drops below 25 FPS |
| **PLAT-002** | Switch Handheld | UI readability at 720p | Text readable, buttons tap-friendly |
| **PLAT-003** | Switch Touch | Budget allocation via touch | Sliders respond to touch, no input lag |
| **PLAT-004** | Switch Sleep Mode | Put console to sleep mid-campaign, resume | Game resumes exactly where it left off, no state loss |
| **PLAT-005** | Min-Spec PC (Intel HD 4000, 4GB RAM) | Full campaign cycle | 30 FPS minimum, playable experience |

---

## 7. REGRESSION CHECKLIST

**Use this checklist after every major bug fix or system change. If you change one system, test everything it touches.**

### Post-Fix Regression Tests

When a bug is fixed in:

**Brief System**:
- [ ] Re-test brief generation variety (BS-004)
- [ ] Re-test Concept Forge integration (INT-001)
- [ ] Re-test client tier unlocks (RE-002)

**Team Chemistry**:
- [ ] Re-test chemistry calculations with edge cases (TC-101, TC-102, TC-103)
- [ ] Re-test Concept Forge stat generation (CF-001, CF-002)
- [ ] Re-test Meltdown behavior (TC-201)

**Concept Forge**:
- [ ] Re-test logline variety (CF-004)
- [ ] Re-test Gauntlet integration (INT-002)
- [ ] Re-test stat calculation accuracy (CF-001, CF-002)

**Approval Gauntlet** (CRITICAL — test everything):
- [ ] Re-test all happy path cases (AG-001 through AG-004)
- [ ] Re-test pushback mechanics (AG-003, AG-101, AG-202)
- [ ] Re-test walk away (AG-201)
- [ ] Re-test save/load mid-Gauntlet (AG-204)
- [ ] Re-test production integration (INT-003)
- [ ] Re-test all evil paths (AG-201 through AG-206)

**Production Pipeline**:
- [ ] Re-test Ambition Gap penalty (PP-101)
- [ ] Re-test budget allocation edge cases (PP-201, PP-202)
- [ ] Re-test broadcast integration (INT-004)

**Broadcast & Reaction**:
- [ ] Re-test Audience Score calculation (BR-001, BR-002)
- [ ] Re-test polarization mechanics (BR-003, BR-102)
- [ ] Re-test reputation integration (INT-005)
- [ ] Re-test Super Bowl amplifier (SB-002)

**Reputation & Economy**:
- [ ] Re-test cash flow (RE-003, RE-101)
- [ ] Re-test client tier unlocks (RE-002)
- [ ] Re-test Cash Crisis (RE-101, RE-102)
- [ ] Re-test brief generation integration (INT-006)

**Save/Load**:
- [ ] Re-test save at every campaign state (Briefing, Staffing, Gauntlet, Production, Broadcast)
- [ ] Re-test autosave triggers (SL-003)
- [ ] Re-test version migration (SL-102)
- [ ] Re-test corruption handling (SL-101)

---

## 8. RISK ASSESSMENT

**What systems are most likely to break? Where should QA focus?**

### CRITICAL RISK — The Approval Gauntlet

**Why**: This is the game. If negotiation feels broken, mechanical, or unfair, the entire fantasy collapses.

**Failure Modes**:
- Persuasion check feels random instead of skill-based.
- Client notes repeat or feel generic.
- Pushback economy is too stingy (player never has points) or too generous (player always succeeds).
- Walk Away option is never used (stakes too high) or always used (penalty too low).
- Save/load mid-Gauntlet causes state corruption.

**Mitigation**:
- Test Gauntlet extensively in isolation before integrating with full game.
- Playtest with 20+ players, track pushback usage rates (target: 5-10% of Gauntlets end in Walk Away, 30-50% of rounds involve at least one pushback attempt).
- Test all edge cases (zero Pushback Points, failed persuasion chains, client walkout).
- Automated test: Run 1000 simulated Gauntlets with varying parameters, log outcomes, verify distribution matches design targets.

---

### HIGH RISK — Concept Forge Repetition

**Why**: If the player sees the same concepts repeatedly, the creative fantasy dies.

**Failure Modes**:
- Loglines repeat exact phrasing within 10 campaigns.
- Stat distributions produce "samey" concepts (all concepts cluster around 50-60 in all stats).
- Hook/Tone combinations feel limited (player sees "surreal mini-film" 5 times in a row).

**Mitigation**:
- Content volume test: Generate 100 concepts, manually review for repetition. Flag any exact duplicates or near-duplicates.
- Stat distribution test: Generate 100 concepts, plot stat distributions. Verify variance matches design intent (bell curve around 40-60, outliers at 80+ and 20-).
- Playtest extended sessions (30+ campaigns) and survey players: "Did concepts feel repetitive?" If yes, expand content library.

---

### HIGH RISK — Economy Balance

**Why**: If the player is always broke, every decision becomes "what can I afford" instead of "what do I believe in." If the player is always flush, budget tension evaporates.

**Failure Modes**:
- Cash Crises happen too often (5+ per career) or never (0 per career).
- Super Bowl bids are either trivially affordable or impossibly expensive.
- Player discovers exploit (e.g., taking retainers and walking away from campaigns to bank fees without completing work).

**Mitigation**:
- Automated economy simulation: Run 100 simulated careers with different playstyles (cautious, balanced, aggressive). Track cash flow, count Cash Crises, verify 2-3 per career on average.
- Playtest with economy focus: Track cash reserves every quarter for 5 playthroughs. If any playstyle hits zero cash more than 3 times, economy too tight. If any playstyle never dips below 50% reserves, economy too loose.
- Exploit testing: Deliberately attempt to game the economy. If exploit found, patch immediately.

---

### MEDIUM RISK — Save/Load Corruption

**Why**: Save bugs are frustrating and can destroy 10+ hours of player progress.

**Failure Modes**:
- Save file corrupts during autosave (partial write due to crash or disk full).
- Version migration fails (old save loads but critical data missing).
- Save/load mid-campaign causes state desync (Gauntlet resumes with wrong concept, wrong round, or missing Pushback Points).

**Mitigation**:
- Test save/load at every campaign state (10+ states per campaign).
- Corruption test: Manually corrupt save files (delete random JSON fields, introduce syntax errors), verify graceful error handling.
- Version migration test: Create save files for every version, verify migration path from v1 → v2 → v3 works.
- Backup system: Autosave system writes to 3 rotating slots. If one corrupts, player loses at most 1 quarter of progress, not entire career.

---

### MEDIUM RISK — Performance on Low-End PCs / Switch

**Why**: Framerate drops damage the experience, especially during the Gauntlet (high tension) and Broadcast (high spectacle).

**Failure Modes**:
- Gauntlet UI tanks to 30 FPS on min-spec PC due to excessive UI redraws.
- Broadcast sequence drops frames during animatic transitions.
- Memory leak causes performance degradation after 2+ hours.

**Mitigation**:
- Profile early and often: Run Unity Profiler every milestone. Identify bottlenecks before they become systemic.
- Test on min-spec hardware: Borrow or buy a 2015-era laptop with integrated graphics. If it can't hit 30 FPS, optimize.
- Memory leak test: 10-hour session with memory profiler running. RAM usage should plateau, not climb indefinitely.

---

## 9. QUALITY GATES

**What must pass before we ship? These are non-negotiable.**

### Pre-Alpha Quality Gate (Month 7)

**Criteria for passing Alpha milestone:**

- [ ] **Zero crash bugs** in core loop (Brief → Team → Forge → Gauntlet → Production → Broadcast → Reputation).
- [ ] **Gauntlet feels tense** in playtest feedback (5+ playtesters report "I wanted to fight for my ad").
- [ ] **Concept Forge produces variety** (100 generated concepts, < 5% exact duplicates).
- [ ] **Economy balance passes simulation** (100 careers, 2-3 Cash Crises per career on average).
- [ ] **Save/load works** at all campaign states with zero corruption in 50+ test cycles.
- [ ] **Performance hits targets** (60 FPS on target PC, 30 FPS on min-spec).

**If any of these fail, do not proceed to Beta. Fix first.**

---

### Pre-Beta Quality Gate (Month 10)

**Criteria for closed beta launch:**

- [ ] **All Alpha criteria still pass** (regression test confirms no broken systems).
- [ ] **All critical bugs fixed** (crash, soft lock, save corruption).
- [ ] **UI polish complete** (animations, transitions, tooltips, no placeholder art).
- [ ] **Audio implemented** (music, SFX, no silent moments unless intentional).
- [ ] **Full content library** (50+ briefs, 30+ loglines, 20+ creatives, 8 client archetypes).
- [ ] **Playtest satisfaction > 70%** (survey beta testers: "Would you recommend this game?").

**If satisfaction < 70%, identify pain points and iterate before expanding beta.**

---

### Pre-Launch Quality Gate (Month 12)

**Criteria for Release Candidate:**

- [ ] **Crash rate < 0.1%** (fewer than 1 crash per 1000 play sessions).
- [ ] **Zero save corruption reports** from beta testers.
- [ ] **Performance stable** (no frame drops below target FPS, no memory leaks).
- [ ] **Steam achievements work** (all 30-40 achievements trigger correctly).
- [ ] **Localization complete** (if applicable) and verified by native speakers.
- [ ] **Full regression pass complete** (all critical tests re-run and passing).
- [ ] **Press build stable** (no embarrassing bugs in review copies).

**If crash rate > 0.1% or any critical bug remains, delay launch. Better to ship late than ship broken.**

---

## 10. BUG SEVERITY CLASSIFICATION

**How do we prioritize bugs? Use this rubric.**

### CRITICAL (P0) — Ship Blocker

**Definition**: Prevents core gameplay. Causes crash, data loss, or soft lock.

**Examples**:
- Game crashes during Gauntlet.
- Save file corrupts, player loses entire career.
- Soft lock: Player cannot progress past Production phase (button non-functional).
- Economy allows negative infinite cash (exploit breaks progression).

**SLA**: Fix within 24 hours. Drop everything else.

---

### HIGH (P1) — Major Gameplay Issue

**Definition**: Breaks a system but does not prevent play. Significantly damages experience.

**Examples**:
- Concept Forge generates identical loglines 50% of the time.
- Persuasion check in Gauntlet always fails regardless of stats (feels unfair).
- Super Bowl sequence does not apply +15 Audience Score bonus.
- Client walks out despite high ClientTrust (logic error).

**SLA**: Fix within 1 week. Block release if unfixed.

---

### MEDIUM (P2) — Noticeable but Workaround Exists

**Definition**: Affects experience but does not break gameplay. Player can work around it.

**Examples**:
- UI tooltip displays incorrect stat value (displays 65, actual value is 68).
- Autosave does not trigger at quarter-end (player can manual save).
- Music does not fade correctly during Gauntlet tension escalation.
- Client dialogue repeats exact phrasing twice in one Gauntlet (variety issue, not logic error).

**SLA**: Fix before launch. Can be deferred to patch if time-constrained.

---

### LOW (P3) — Polish Issue

**Definition**: Minor visual, audio, or text issue. Does not affect gameplay.

**Examples**:
- Typo in brief flavor text.
- UI button hover state slightly misaligned.
- SFX volume too loud on one button.
- Award ceremony screen has placeholder art.

**SLA**: Fix if time allows. Can be patched post-launch.

---

### NOT A BUG (CLOSED)

**Definition**: Reported behavior is intended design.

**Examples**:
- "Pushback always fails against conservative clients." — Working as intended (RiskTolerance = 2 means low success threshold).
- "I went bankrupt after firing my entire roster." — Working as intended (no staff = no campaigns = no revenue).
- "Client issued the same note twice." — If client issues note, player accepts, then violates same constraint again, client can re-issue. Check logic. If truly duplicate without cause, escalate to P1.

**Response**: Close ticket, explain design intent, document in FAQ if commonly reported.

---

## 11. PLAYTESTING PROTOCOL

### Internal Playtesting (Dev Team)

**Frequency**: Weekly during Prototype (Months 1-3), bi-weekly during Production (Months 4-6).

**Duration**: 30-60 minute sessions.

**Focus**: Systems verification. Does the loop work? Are the numbers correct?

**Deliverable**: Bug reports in tracker (Jira, Trello, GitHub Issues), severity assigned.

---

### External Playtesting (Closed Alpha, Month 7-9)

**Participants**: 10-20 selected playtesters (recruited via mailing list, Discord, industry contacts).

**Duration**: Full session (60-90 minutes per tester).

**Focus**: Balance, pacing, feel. Does the Gauntlet feel tense? Do concepts feel varied? Is the economy too tight?

**Deliverable**: Survey responses (Google Form), recorded sessions (if testers consent), bug reports.

**Survey Questions**:
- On a scale of 1-10, how tense did the Approval Gauntlet feel?
- Did you ever feel like you wanted to push back on a client note?
- Did you ever Walk Away from a client? Why or why not?
- Did concepts feel repetitive? After how many campaigns?
- Did you ever run out of cash? Was it frustrating or motivating?
- Would you play this game again? Would you recommend it to a friend?

---

### External Playtesting (Closed Beta, Month 10-11)

**Participants**: 50-100 beta testers (Steam beta branch, private invite).

**Duration**: Extended play (5-10 hours per tester, full career).

**Focus**: Stability, polish, content depth. Are there crash bugs? Does the late game stay interesting?

**Deliverable**: Crash reports (Unity Cloud Diagnostics), Steam forum feedback, bug reports via Discord.

**Metrics to Track**:
- Crash rate per session.
- Average session length.
- Progression: What percentage of players reach Year 3? Year 5? Super Bowl?
- Drop-off points: Where do players stop playing?

---

## 12. POST-LAUNCH SUPPORT PLAN

### Week 1 Post-Launch

**Priority**: Critical bug fixes. Monitor crash reports and Steam forums hourly.

**SLA**: Hotfix critical bugs (crash, save corruption) within 24 hours. Patch 1.0.1 within 7 days.

**Monitoring**:
- Unity Cloud Diagnostics: Track crash rate.
- Steam forums: Triage bug reports, escalate critical issues.
- Discord: Active dev presence, respond to player issues in real-time.

---

### Month 1 Post-Launch

**Priority**: Balance tweaks, medium bugs, QoL improvements.

**Patch cadence**: 1-2 patches per month.

**Content**: Based on player feedback:
- If economy too tight: Increase retainer revenue by 10-20%.
- If Gauntlet too harsh: Adjust RiskTolerance values for conservative clients.
- If Concept Forge repetitive: Add 10 more logline templates.

---

### Months 2-6 Post-Launch

**Priority**: Content updates, stretch goals (if PC launch successful).

**Roadmap**:
- **Month 2**: Add 2-3 new client archetypes (free update).
- **Month 3**: Add Award Season system (if cut from v1).
- **Month 4**: Add Rival Agencies (if cut from v1).
- **Month 5**: Begin Switch port (if sales support it).
- **Month 6**: Major content expansion or DLC.

---

## 13. TOOLS & INFRASTRUCTURE

### Bug Tracking

**Tool**: GitHub Issues (if open-source) or Jira (if internal).

**Workflow**:
1. Bug reported (tester, player, dev).
2. QA triages: Assign severity (P0-P3), assign to developer.
3. Dev fixes bug, marks "Ready for QA."
4. QA verifies fix, runs regression tests, closes ticket.

**Required Fields**:
- **Title**: Short, descriptive (e.g., "Gauntlet crashes on round 3 when client issues Panic Note").
- **Severity**: P0, P1, P2, P3.
- **Repro Steps**: Exact steps to reproduce (numbered list).
- **Expected Result**: What should happen.
- **Actual Result**: What actually happens.
- **Environment**: PC/Mac/Linux/Switch, OS version, game build number.
- **Attachments**: Screenshots, save files, log files.

---

### Test Environments

**Dev Build** (unstable, latest code):
- Updated daily from `develop` branch.
- Used for internal playtesting.
- Crashes expected.

**QA Build** (semi-stable, weekly):
- Built from `develop` branch every Monday.
- Used for regression testing.
- Should be playable start-to-finish.

**Beta Build** (stable, weekly during beta):
- Built from `develop` branch, uploaded to Steam beta branch.
- Public-facing, must be stable.

**Release Candidate** (final, pre-launch):
- Built from `main` branch.
- Zero known critical bugs.
- Final QA pass before launch.

---

### Automation

**Automated Tests** (if time allows):
- Unit tests for critical formulas (chemistry calculation, Audience Score calculation, persuasion check).
- Integration tests for event bus (verify events fire correctly).
- Performance tests (measure frame time during Gauntlet, Broadcast).

**CI/CD** (if team uses Jenkins/GitHub Actions):
- Automated build on every commit.
- Run unit tests, fail build if tests fail.
- Upload successful builds to internal server.

**Benefit**: Catch regressions early. If a code change breaks chemistry calculation, unit test fails immediately, dev notified before QA even sees the build.

---

## 14. FINAL NOTES

### What This Game Cannot Survive

**A broken Gauntlet.** If negotiation feels like a menu instead of a conversation, the game fails. This is the hill we live or die on. Test it relentlessly. Iterate until it sings. Do not ship until playtesters say "I felt the tension."

**Save corruption.** A player who loses 10 hours of progress to a corrupt save will never trust us again. The save system must be bulletproof. Test it at every campaign state. Test version migration. Test corruption recovery. Zero tolerance.

**Repetitive content.** If the player sees the same concept logline five times in one career, the creative fantasy dies. Test for variety early and often. Expand the content library if repetition is detected within 30 campaigns.

---

### What This Game Can Survive

**Minor balance issues.** If the economy is slightly too tight in v1.0, we can patch it in v1.1. If a client archetype is too harsh, we can tweak RiskTolerance values post-launch. Balance is iterative.

**Polish bugs.** Typos, misaligned UI, placeholder art — these are embarrassing but not fatal. Fix them if time allows, patch them if not.

**Performance hiccups.** If the game drops to 55 FPS during the Super Bowl sequence on min-spec hardware, that is acceptable. If it drops to 15 FPS, that is not. Know the difference.

---

### The Testing Priorities

**Priority 1: Core Loop** (Brief → Team → Forge → Gauntlet → Production → Broadcast → Reputation).
If this loop is broken, nothing else matters. Test it first, test it most, test it always.

**Priority 2: The Gauntlet.**
This is the game. If this does not work, the game does not work. Test every edge case. Playtest with 50+ people if necessary. Do not ship until it is right.

**Priority 3: Save/Load.**
The player's career is their investment. Protect it. Zero tolerance for corruption.

**Priority 4: Economy & Progression.**
The player should feel challenged but not punished. Test balance extensively. Simulate 100 careers if necessary.

**Priority 5: Content Variety.**
The player should never see the exact same brief, concept, or logline twice in a single career. Test for repetition.

**Priority 6: Performance.**
The game should run at 60 FPS on target hardware, 30 FPS on min-spec. Profile early, optimize late.

**Priority 7: Polish.**
Everything else. Important, but not existential.

---

A bug isn't fixed until it's verified. Then regression test everything it touched.

Ship it when it's ready. Not before.

-- CRASH

---

**END OF QA PLAN**
