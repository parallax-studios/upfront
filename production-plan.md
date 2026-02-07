# UPFRONT — Production Plan

**Producer**: CLOCK
**Version**: 1.0
**Date**: 2026-02-07
**Status**: Production-Ready

---

> "A shipped game beats a perfect concept. Scope is the lever you pull when time and resources are fixed."

I've read the pitch, the GDD, the narrative bible, the art direction, the sound design, and the technical architecture. I know what this game is: an advertising agency management sim where the player negotiates creative vision against client demands, culminating in a Super Bowl broadcast. The core verb is not "build" — it is "defend." That is the pitch. That is the hook. That is also the risk.

This document is the production roadmap. Milestones. Dependencies. Critical path. Risk register. What ships, what doesn't, and what we cut when (not if) the timeline compresses. Every decision here serves one goal: ship a game that delivers on the player fantasy in 12 months with a 2-4 person team.

Cut scope, not corners. Let's go.

---

## 1. PROJECT OVERVIEW

### 1.1 Game Identity

**Title**: UPFRONT
**Genre**: Management Sim / Business Sim
**Platform**: PC (Steam) primary, Switch (post-launch), iPad (stretch)
**Target Players**: Management sim fans (Game Dev Tycoon, Two Point Hospital), creative industry professionals, prestige drama fans (Mad Men, Halt and Catch Fire)
**Core Fantasy**: You are the creative director who stands between a brilliant idea and the client who is paying for it. What survives is your responsibility.

**Unique Selling Proposition**: The only management sim where defending your creative work against client feedback is the core mechanic. The Approval Gauntlet is a negotiation system that no other tycoon game has.

---

### 1.2 Team Structure

**Minimum Viable Team**: 2-4 people

| Role | Responsibility | FTE | Critical Skills |
|------|---------------|-----|----------------|
| **Lead Programmer (BYTE)** | Core systems, Unity implementation, performance | 1.0 | C#, Unity, state machines, JSON |
| **Game Designer (REED)** | System design, balance, content tools | 0.5 | Excel, playtesting, balance tuning |
| **Narrative Designer (NOVA)** | Client dialogue, creative character arcs, loglines | 0.5 | Writing, character voice, procedural narrative |
| **Art Director (PIXEL)** | UI design, storyboard frames, office isometric art | 0.75 | Figma, illustration, UI/UX |
| **Sound Designer (ECHO)** | SFX, music integration (FMOD), dynamic audio | 0.5 | FMOD, music composition, foley |
| **Producer (CLOCK)** | Milestone tracking, scope management, risk mitigation | 0.25 | Project management, Excel, communication |

**Total**: ~3.5 FTE (realistic for a 2-4 person indie team with overlapping roles)

**Alternative Configuration** (solo/duo):
- **Option A (Solo)**: Programmer wears all hats. Contracts out art and audio. Timeline extends to 18 months.
- **Option B (Duo)**: Programmer + designer/artist. Contracts out audio. Timeline extends to 15 months.

**Contractors**:
- Foley artist (2 days)
- Voice actors (4-6 people, 1 day)
- Composer (6 weeks, part-time) — if ECHO does not handle music

---

### 1.3 Timeline Summary

**Total Development Time**: 12 months
**Ship Date**: Month 12, Week 4 (launch day)
**Buffer**: 2 weeks built into beta phase (can absorb slippage from alpha)

| Phase | Duration | End Date | Key Deliverable |
|-------|----------|----------|----------------|
| **Prototype** | Months 1-3 | Week 12 | Vertical slice: One campaign playable |
| **Production** | Months 4-6 | Week 24 | Feature-complete: Full year playable |
| **Alpha** | Months 7-9 | Week 36 | Alpha-complete: No crashes, balance tuned |
| **Beta** | Months 10-11 | Week 48 | Beta-complete: Closed beta with 50+ players |
| **Release Candidate** | Month 12 | Week 52 | RC1 submitted to Steam, launch prep |

**Post-Launch** (optional):
- Patch support: Months 13-15 (bug fixes, balance updates)
- Switch port: Months 16-21 (6 months dev + certification)

---

### 1.4 Budget Estimate (Indie Scale)

**Assumption**: Small team, minimal burn rate, revenue-share for contractors.

| Category | Estimated Cost | Notes |
|----------|---------------|-------|
| **Salaries** (3.5 FTE x 12 months) | $0 - $250K | Equity/revenue-share model OR bootstrapped team |
| **Contractors** (art, audio, voice) | $10K - $30K | Foley, voice actors, composer, additional art assets |
| **Software Licenses** (Unity Pro, FMOD, tools) | $2K - $5K | Unity Pro not required until revenue > $100K/year |
| **Hardware** (dev PCs, Switch dev kit if port) | $3K - $8K | PC upgrades, Switch dev kit ($450) |
| **Marketing** (trailer, key art, press outreach) | $2K - $10K | Primarily organic marketing via Steam |
| **Legal/Admin** (business formation, contracts) | $1K - $3K | LLC formation, contractor agreements |
| **Contingency** (20%) | $3.6K - $61.2K | Overruns, unexpected expenses |
| **Total** | $21.6K - $367.2K | Low-end: bootstrapped indie. High-end: funded small studio |

**Funding Model Options**:
1. **Bootstrapped**: Team works part-time, no salaries until revenue. Minimal external costs ($20K-$30K).
2. **Self-funded**: Founder invests savings. Covers living expenses + contractors ($100K-$200K).
3. **Grants/Publisher**: Apply for indie game grants (Epic MegaGrant, regional arts grants). Or sign with indie publisher (revenue-share, advances cover costs).

**Revenue Target** (to recoup + sustain):
- Launch price: $14.99
- Units to break even (at $30K burn): 2,857 copies (post-platform cut)
- Target: 10,000+ copies in Year 1 (realistic for well-reviewed management sim on Steam)

---

## 2. MILESTONE DEFINITIONS

Each milestone has:
- **Entry Criteria**: What must be done before this phase starts
- **Exit Criteria**: What must be done before this phase ends
- **Key Deliverables**: Specific outputs
- **Risk Register**: What could go wrong in this phase

---

### 2.1 Prototype Phase (Months 1-3)

**Goal**: Validate the core loop. Build a vertical slice that proves the Approval Gauntlet works.

**Entry Criteria**:
- Unity 2023.2 LTS installed and configured
- Git repo initialized with folder structure
- Team roles assigned
- Weekly sprint planning cadence established

**Key Deliverables**:

| Week | Owner | Task | Output |
|------|-------|------|--------|
| 1-2 | BYTE | Project setup, event bus, game director skeleton | Core architecture functional |
| 3-4 | BYTE + REED | Brief System (JSON config, generation algorithm, UI mockup) | 8 archetypes, 20 generated briefs visible |
| 5-6 | BYTE + REED | Team Manager (creative stats, chemistry calculation, assignment UI) | 6 creatives assignable to briefs |
| 7-8 | BYTE + REED | Concept Forge (stat generation, 10 logline templates, mood board UI) | 3 concepts generated per brief |
| 9-10 | BYTE + REED + NOVA | Approval Gauntlet (FSM, client notes, persuasion check, placeholder UI) | 3-round negotiation playable |
| 11 | BYTE + REED | Production Pipeline (5 sliders, budget allocation, stat modifiers) | Budget allocation functional |
| 12 | BYTE + REED | Broadcast & Reaction (audience score calc, placeholder animatic, reaction panel) | Campaign completion visible |

**Sprint Plan**:
- 2-week sprints
- Sprint 1: Core architecture + Brief System
- Sprint 2: Team Manager + Concept Forge
- Sprint 3: Approval Gauntlet (core FSM)
- Sprint 4: Approval Gauntlet (UI) + Production Pipeline
- Sprint 5: Broadcast + Reaction
- Sprint 6: Playtest + iteration

**Exit Criteria**:
- One campaign playable end-to-end in ~8 minutes
- 5 external playtesters complete the vertical slice
- Playtest feedback is positive ("I wanted to fight for my ad" > 50% of testers)
- No critical bugs (crashes, soft-locks)
- Team agrees the Gauntlet "feels like negotiation, not a menu"

**Risk Register**:

| Risk | Severity | Likelihood | Mitigation | Owner |
|------|----------|-----------|-----------|-------|
| Gauntlet feels like a menu, not a conversation | CRITICAL | MEDIUM | Prototype Gauntlet in Week 9 as standalone. Iterate based on feel. Add client expressions, dialogue variations. | REED + NOVA |
| Concept Forge produces repetitive concepts | HIGH | MEDIUM | Test with 20+ generated concepts. Verify variety. Expand logline templates if repetition detected. | REED |
| Team velocity slower than estimated | MEDIUM | HIGH | Accept slippage. Extend prototype phase to Week 14 if needed. Buffer exists in production phase. | CLOCK |
| Unity version issues (LTS bugs) | LOW | LOW | Use stable 2023.2 LTS. Monitor Unity forums. Downgrade if critical bug found. | BYTE |

**Contingency**:
- If Gauntlet does not work by Week 10, pivot to simpler "client preference matrix" system (player adjusts concept stats to match client desires). Less thematic, but functional.
- If timeline slips by 2+ weeks, cut Broadcast polish (use static reaction panel instead of animated).

**Dependencies**:
- Week 9-10 (Gauntlet) depends on Week 7-8 (Concept Forge) completing. Cannot test negotiation without concepts to negotiate over.

---

### 2.2 Production Phase (Months 4-6)

**Goal**: Build out the full game. Expand systems. Create content. Replace placeholders with production assets.

**Entry Criteria**:
- Prototype playtest complete with positive feedback
- Gauntlet core mechanic validated ("it feels tense")
- Team confident in technical architecture (event bus, FSM, JSON configs)

**Key Deliverables**:

**Month 4** (Weeks 13-16):
- Expand Brief System to 50+ briefs (REED: JSON authoring)
- Expand Concept Forge to 30+ logline templates (NOVA: writing)
- Implement Team Chemistry edge cases: Meltdown, Brilliant Friction (BYTE + REED)
- Build Gauntlet UI with animations: client facial expressions, stat bar transitions, music layers (BYTE + PIXEL)
- Implement Reputation System: 3 sub-scores, client tier unlocks (BYTE + REED)
- Implement Economy System: revenue sources, expenses, cash flow tracking (BYTE + REED)
- Begin storyboard frame production: 16 frames (4 Hooks x 4 Tones, subset) (PIXEL contracts out or produces)

**Month 5** (Weeks 17-20):
- Build Super Bowl sequence: extended animatic, expanded reaction panel, Monday Morning meeting (BYTE + PIXEL + NOVA)
- Implement Save/Load system: JSON serialization, autosave triggers, versioning (BYTE)
- Build Calendar UI: year overview, quarter progression, deadline markers (PIXEL + BYTE)
- Implement Morale system: creative life events, loyalty tracking, quit threats (BYTE + NOVA)
- Build Roster Management UI: hire, fire, salary negotiation (PIXEL + BYTE)
- Expand storyboard frames to 32 total (PIXEL)
- Create viewer portraits: 20 variations (PIXEL contracts out or produces)

**Month 6** (Weeks 21-24):
- Build Awards system: submission, jury evaluation, ceremony sequence (BYTE + REED)
- Implement Cultural Trends system (STRETCH — cut if timeline slips) (BYTE + REED)
- Implement Rival Agencies (STRETCH — cut if timeline slips) (BYTE + REED)
- Complete storyboard frames: 64 total (8 Hooks x 8 Tones) (PIXEL + contractors)
- Audio asset production begins: 3 music tracks (Office, Gauntlet, Super Bowl), 50 SFX (ECHO + composer contractor)
- Polish Gauntlet UI: 5+ dialogue variations per client note, more animations (NOVA + PIXEL)
- Playtest full year (4 quarters, 6-8 campaigns, Super Bowl) with 10 testers

**Sprint Plan** (2-week sprints):
- Sprint 7: Reputation + Economy systems
- Sprint 8: Super Bowl sequence
- Sprint 9: Save/Load + Calendar + Morale
- Sprint 10: Awards + stretch goals (Trends, Rivals) OR content production if stretch cut
- Sprint 11: Audio integration + final Gauntlet polish
- Sprint 12: Full-year playtest + iteration

**Exit Criteria**:
- Full year (Q1-Q4 + Super Bowl) playable
- 10 playtesters complete a full year session (60-90 minutes) without critical bugs
- Economy balanced (playtesters finish year with positive cash flow, 2-3 close calls acceptable)
- Super Bowl sequence feels climactic (playtest feedback: "that was the payoff")
- All placeholder art replaced with production assets (storyboards, portraits, UI mockups)
- Audio assets integrated (music dynamic layers functional in FMOD, SFX triggering correctly)

**Risk Register**:

| Risk | Severity | Likelihood | Mitigation | Owner |
|------|----------|-----------|-----------|-------|
| Super Bowl sequence is anticlimactic | MEDIUM | LOW | Prototype Super Bowl as standalone in Week 17-18. Test with 5 people. If flat, add interactivity (player responds to post-game calls). | BYTE + REED |
| Asset production bottleneck (64 storyboard frames) | MEDIUM | MEDIUM | Contract out 50% of frames to external illustrator. PIXEL art directs, contractor executes. Budget $3K-$5K. | PIXEL |
| Audio integration issues (FMOD complexity) | MEDIUM | LOW | ECHO begins FMOD setup in Week 21. Test dynamic music layers early. If FMOD is problematic, fallback to Unity Audio Mixer (less flexible but faster). | ECHO + BYTE |
| Stretch goals consume time (Trends, Rivals) | MEDIUM | HIGH | Cut stretch goals in Week 22 if sprint velocity drops below target. Trends and Rivals are NOT essential. | CLOCK |
| Economy too tight/too loose | MEDIUM | MEDIUM | Use Economy Simulator tool (BYTE builds in Week 15) to run 100+ simulated years. Tune revenue/expense values before Month 6 playtest. | REED |

**Contingency**:
- If timeline slips by 2+ weeks, cut Cultural Trends system entirely. Game works without it.
- If timeline slips by 4+ weeks, also cut Rival Agencies. Focus on player agency, not AI competitors.
- If storyboard frame production is behind, reduce from 64 to 32 frames (4 Hooks x 4 Tones, generic combinations). Quality over quantity.

**Dependencies**:
- Super Bowl sequence (Week 17-20) depends on Broadcast system (Week 12) and storyboard frames (PIXEL, ongoing).
- Save/Load (Week 17-18) must complete before full-year playtests (Week 24). Cannot test sessions without saving progress.
- Audio integration (Week 21-24) depends on FMOD setup (ECHO, Week 21) and asset delivery (composer, Week 20-22).

---

### 2.3 Alpha Phase (Months 7-9)

**Goal**: Feature lock. Balance, tune, polish. Bug fixing begins.

**Entry Criteria**:
- Feature-complete: All core systems implemented
- Full year playable without placeholders
- Playtest feedback from Month 6 is positive (>70% would recommend to a friend)
- No show-stopper bugs (crashes, data loss)

**Key Deliverables**:

**Month 7** (Weeks 25-28):
- **Feature Lock**: No new systems after Week 25. Only bug fixes, balance tweaks, and polish.
- Economy balancing: Run Economy Simulator for 100+ simulated years. Adjust revenue/expense values until cash flow matches design targets (2-3 crises per career, not constant). (REED)
- Concept Forge balancing: Test for repetition over 30+ campaigns in sequence. If concepts feel similar within 10 campaigns, expand content library (add 10 logline templates, 5 Hook variants). (REED + NOVA)
- Gauntlet balancing: Tune client archetypes (risk tolerance, note frequency, persuasion thresholds). Ensure pushback success rates match design targets (40% success for new agency, 70% for established). (REED)
- Performance profiling: Unity Profiler on full campaign cycle. Identify bottlenecks (UI rendering, concept generation, save/load). Fix if frame time >16ms on target PC spec. (BYTE)

**Month 8** (Weeks 29-32):
- UI polish pass 1: Add transitions (page slides, fades), hover states, tooltips, button feedback animations. (PIXEL + BYTE)
- Audio implementation: FMOD dynamic music layers fully integrated. All SFX triggering correctly via event bus. Mix balance verified (music -18 LUFS, SFX feedback layer -12 to -18 LUFS, critical layer -6 to -12 LUFS). (ECHO + BYTE)
- Accessibility features: Colorblind mode (3 filters), adjustable UI scale (80%-150%), high-contrast mode, dyslexia font option. (BYTE)
- Performance profiling pass 2: Test on minimum-spec PC (Intel HD 4000 integrated graphics, 4GB RAM). Ensure 60 FPS at 1080p. If not, reduce UI texture resolution or add Low Quality mode. (BYTE)

**Month 9** (Weeks 33-36):
- Content expansion: Add 20 more briefs (total: 70), 10 more logline templates (total: 40). (REED + NOVA)
- Playtest marathon: 3-5 dedicated playtesters play full 5-year careers (4-6 hours each). Track all issues in bug database. (CLOCK manages tester coordination)
- Bug fixing: Triage all reported bugs. Prioritize Critical (crashes, save corruption, soft-locks) and High (broken mechanics, balance issues). Fix Critical within 24 hours. Defer Low priority (typos, minor UI glitches) to beta. (BYTE + team)
- QA checklist: Test all edge cases (zero cash, all creatives quit, client walkout, Super Bowl loss, award win, etc.). (CLOCK + REED)

**Sprint Plan** (2-week sprints):
- Sprint 13: Balance tuning (Economy, Gauntlet, Concept Forge)
- Sprint 14: UI polish + audio integration
- Sprint 15: Accessibility features + performance profiling
- Sprint 16: Content expansion + playtest marathon
- Sprint 17: Bug fixing sprint (all hands)
- Sprint 18: Final alpha QA + alpha milestone review

**Exit Criteria**:
- Alpha-complete: All features implemented and balanced
- Crash rate < 5% (5 crashes per 100 hours of playtesting)
- Playtest feedback: "I want to play more" >80%
- Performance: 60 FPS on target PC spec, no frame drops during critical moments (Gauntlet, Super Bowl)
- Economy: Playtesters finish 5-year careers with positive cash in 70%+ of runs
- Gauntlet: Pushback success rates match design targets
- All Critical and High bugs fixed
- Content library: 70 briefs, 40 logline templates, 64 storyboard frames, 20 portraits, 150 SFX, 12 music cues

**Risk Register**:

| Risk | Severity | Likelihood | Mitigation | Owner |
|------|----------|-----------|-----------|-------|
| Balance is off (economy too tight, Gauntlet too hard) | HIGH | MEDIUM | Use simulation tools to test balance before human playtesting. Iterate based on playtest data. Be willing to make large balance changes (50% revenue increase if needed). | REED |
| Performance issues on low-end PCs | MEDIUM | LOW | Profile early (Week 25). If framerate <60 FPS, identify bottleneck (likely UI rendering). Optimize or add Low Quality mode. | BYTE |
| Playtest reveals unfun systems (e.g., Morale is annoying) | HIGH | LOW | If 3+ playtesters cite the same system as frustrating, discuss with team. Be willing to simplify or cut. Player enjoyment > design vision. | CLOCK + REED |
| Bug backlog overwhelms team | MEDIUM | HIGH | Triage ruthlessly. Fix Critical immediately. High bugs by end of alpha. Medium/Low bugs deferred to beta or post-launch. Use bug tracker (Trello, Jira, or GitHub Issues). | CLOCK + BYTE |

**Contingency**:
- If alpha slips by 2 weeks, cut content expansion (stay at 50 briefs, 30 templates). Content volume is less important than polish.
- If performance cannot hit 60 FPS on min-spec, target 45 FPS and be transparent in Steam system requirements.
- If a core system is unfun (e.g., Morale is tedious), simplify ruthlessly. Example: Remove Morale life events, make morale a passive stat affected only by campaign outcomes.

**Dependencies**:
- Bug fixing (Week 33-36) depends on playtest marathon completing (Week 33-34). Cannot fix bugs we don't know about.
- Audio polish (Week 29-32) depends on all SFX and music assets delivered by ECHO + composer (end of Week 28).

---

### 2.4 Beta Phase (Months 10-11)

**Goal**: Closed beta with 50-100 players. Collect feedback. Fix bugs. Polish everything. Prepare for launch.

**Entry Criteria**:
- Alpha-complete: No show-stopper bugs
- Game is fun: Playtest feedback is consistently positive
- Performance targets met: 60 FPS on target PC spec
- Content complete: No placeholders

**Key Deliverables**:

**Month 10** (Weeks 37-40):
- Closed beta launch: Set up Steam private branch. Invite 50 players via mailing list, Discord, r/tycoon, r/BaseBuildingGames. (CLOCK manages outreach)
- Feedback infrastructure: Discord server for beta testers. Google Form for bug reports. Unity Cloud Diagnostics for crash reporting (or Sentry). (CLOCK + BYTE)
- Daily bug triage: Review crash reports and bug submissions every morning. Prioritize Critical bugs (fix within 24 hours). High bugs (fix within 1 week). Medium/Low (defer to post-launch patch). (CLOCK + BYTE)
- Balance iteration: Monitor beta player behavior via telemetry (if implemented) or Discord discussions. Are players going broke? Is the Gauntlet too easy/hard? Adjust economy and difficulty values via JSON hotfixes. (REED)
- UI polish pass 2: Fix all reported UI bugs (clipping, alignment, missing hover states). Add final animations (confetti on award win, screen shake on walk away, etc.). (PIXEL + BYTE)

**Month 11** (Weeks 41-44):
- Audio polish: Final mix and master. Normalize SFX volumes. Ensure music layers transition smoothly. Test on headphones, speakers, TV audio. (ECHO)
- Content polish: Proofread all text (briefs, dialogue, loglines, UI labels). Fix typos and grammar. Ensure consistent tone across all client dialogue. (NOVA + CLOCK)
- Performance optimization: Run Unity Profiler on min-spec PC one final time. Ensure <16ms frame time during all gameplay (Gauntlet, Super Bowl, Office navigation). If any spikes remain, optimize. (BYTE)
- Steam achievements: Implement 30-40 achievements. Hook into game events (first Clio win, fire client, Legendary Super Bowl ad, etc.). Test all achievements trigger. (BYTE)
- Beta wrap-up: Final bug fixing sprint. Close all Critical and High bugs. Review Medium bugs — fix if time allows, defer if not. Thank beta testers. Announce launch date. (CLOCK + team)

**Sprint Plan** (2-week sprints):
- Sprint 19: Beta launch + initial bug triage
- Sprint 20: Balance iteration + UI polish
- Sprint 21: Audio polish + content proofread
- Sprint 22: Achievements + final optimization
- Sprint 23: Beta wrap-up + launch prep
- Sprint 24: Code freeze + RC build

**Exit Criteria**:
- Beta-complete: Crash rate <1% (1 crash per 100 hours)
- Positive player sentiment: If public beta reviews exist, target Mixed or better on Steam. Aim for Positive.
- All Critical bugs fixed
- All High bugs fixed or have documented workarounds
- Medium/Low bugs documented for post-launch patch
- Performance: 60 FPS on target PC, 30+ FPS on min-spec
- Audio: All tracks mixed and mastered, no volume spikes or dead silence
- Text: No typos in player-facing content (briefs, UI, dialogue)
- Achievements: All 30-40 achievements implemented and tested
- Steam store page: Complete (screenshots, trailer, description, tags)
- Press list: 20-30 outlets/YouTubers identified and contacted

**Risk Register**:

| Risk | Severity | Likelihood | Mitigation | Owner |
|------|----------|-----------|-----------|-------|
| Crash rate too high (>5% in beta) | CRITICAL | LOW | If crashes are frequent, extend beta by 1 week. Cancel non-critical features (e.g., final animation polish) to focus on stability. | BYTE |
| Negative beta feedback (game is not fun) | CRITICAL | VERY LOW | If 30%+ of beta testers say game is boring/frustrating, delay launch by 4 weeks. Identify core issue via Discord discussions. Iterate on problem system. | CLOCK + REED |
| Timeline slips (beta extends into Month 12) | MEDIUM | MEDIUM | If beta extends past Week 44, compress RC phase. Launch in Week 52 regardless (with Day 1 patch planned). | CLOCK |
| Achievements not triggering | LOW | LOW | Test all achievements manually during Sprint 22. If time is tight, defer 10 "stretch" achievements to post-launch patch. | BYTE |

**Contingency**:
- If crash rate is >5%, delay launch by 2 weeks. Stability is non-negotiable.
- If beta feedback reveals a fundamental flaw (e.g., "the Gauntlet is still not fun"), delay launch by 4-6 weeks. Fix the core issue. A delayed game that is good is better than a shipped game that is mediocre.
- If timeline slips, cut all non-essential features: animations, achievements, Steam Trading Cards. Focus on stability and core loop.

**Dependencies**:
- Launch prep (Week 41-44) depends on beta completing (Week 40). Cannot finalize Steam page until beta validates the game is ready.
- Achievements (Week 41-42) depend on game events being stable. If core systems are still changing, defer achievements.

---

### 2.5 Release Candidate Phase (Month 12)

**Goal**: Final QA. Build submission to Steam. Marketing ramp-up. Launch.

**Entry Criteria**:
- Beta-complete: Crash rate <1%, positive player sentiment
- All Critical and High bugs fixed
- Steam store page complete (screenshots, trailer, description)
- Press list finalized (20-30 contacts)

**Key Deliverables**:

**Week 45-46 (RC1 Build)**:
- Final QA pass: Full playthrough on Windows, macOS, Linux. Test all input methods (mouse/keyboard, controller). Verify all achievements trigger. Test edge cases (zero cash, all creatives quit, etc.). (CLOCK + REED + external QA if budget allows)
- Build Release Candidate 1 (RC1): Full optimization, code stripping, obfuscation (optional). Build for Windows (primary), macOS, Linux. (BYTE)
- Upload RC1 to Steam: Set up Steam build via SteamPipe. Test download and installation on fresh PC. (BYTE)
- Internal RC1 playtest: Team plays RC1 for 4-6 hours each. Log any critical issues. (All hands)

**Week 47 (RC2 Build if needed)**:
- If critical bugs found in RC1, fix and build RC2. If no critical bugs, RC1 becomes final build.
- Steam store page finalization: Upload 10 screenshots (office view, Gauntlet, concept forge, Super Bowl, awards). Upload trailer (2 minutes: hook, gameplay, Super Bowl climax). Write description (500 words: pitch, features, USP). Add tags (management sim, tycoon, singleplayer, 2D, strategy, indie). (CLOCK + PIXEL for trailer)
- Press outreach: Send Steam keys to 20-30 gaming press outlets (PC Gamer, Rock Paper Shotgun, Polygon) and YouTubers (Wanderbots, Retromation, management sim specialists). Include press kit (game description, key art, screenshots, developer quote). (CLOCK)

**Week 48 (Marketing Ramp-Up)**:
- Announce launch date: Post on Steam, social media (Twitter, Reddit r/gamedev, r/tycoon, r/IndieGaming), mailing list, Discord. Target launch window: 1-2 weeks from announcement (urgency creates buzz). (CLOCK)
- Create launch trailer: 30-second version for social media. GIF showing Super Bowl split-screen moment (PIXEL creates GIF from trailer footage). (PIXEL)
- Prepare Day 1 patch: If any non-critical bugs remain, prepare patch 1.0.1 for launch +1 week. (BYTE)

**Week 49 (Launch Week)**:
- Launch day: Release on Steam (Monday preferred — most Steam traffic early in week). Set price: $14.99. Monitor Steam forums, Discord, Twitter for player feedback. (CLOCK + all hands on standby)
- Community management: Respond to player questions on Steam forums and Discord within 4 hours. Address complaints. Thank players for positive reviews. (CLOCK + NOVA for writing responses)
- Monitor crash reports: Unity Cloud Diagnostics or Sentry. If crash rate >1%, identify cause and prepare hotfix within 24 hours. (BYTE)
- Press coverage: Monitor for reviews. If review outlets publish, share on social media. (CLOCK)
- Sales tracking: Monitor Steam revenue via Steamworks dashboard. Track reviews (target: Positive or better after 100 reviews). (CLOCK)

**Week 50+ (Post-Launch Support)**:
- Patch 1.0.1: Release within 1 week of launch. Fix any launch-day bugs (typos, balance tweaks, crash fixes). (BYTE + team)
- Community engagement: Continue responding to forums and Discord. Post weekly dev updates on Steam community hub. (CLOCK)
- Monitor reviews: If reviews drop below Mixed, identify common complaints. Plan patch to address top 3 issues. (CLOCK + REED)

**Sprint Plan** (1-week sprints for RC phase):
- Sprint 25: RC1 build + QA
- Sprint 26: RC2 build (if needed) + press outreach
- Sprint 27: Marketing ramp-up
- Sprint 28: Launch week + community management

**Exit Criteria**:
- Game launched on Steam
- No critical bugs in launch build (crash rate <1%)
- Steam store page live with complete assets (screenshots, trailer, description)
- Press keys sent to 20+ outlets/YouTubers
- Day 1 patch ready (if needed)
- Community channels active (Steam forums, Discord)
- Sales tracking dashboard set up (monitor daily revenue, review score, wishlist conversions)

**Risk Register**:

| Risk | Severity | Likelihood | Mitigation | Owner |
|------|----------|-----------|-----------|-------|
| Critical bug found in RC1 | HIGH | LOW | If critical bug found, delay launch by 1 week. Build RC2. Re-test. Do not ship broken game. | BYTE + CLOCK |
| Press does not cover game | MEDIUM | MEDIUM | If no press coverage by Week 48, pivot to community-driven marketing (Reddit AMAs, streamer outreach, organic Discord growth). | CLOCK |
| Launch day crash spike (>5% crash rate) | CRITICAL | LOW | If crash rate spikes, take game offline (set to "Coming Soon" on Steam if possible). Fix and relaunch within 48 hours. Apologize publicly. | BYTE + CLOCK |
| Negative reviews at launch (Mixed or worse) | HIGH | LOW | If reviews are negative, read reviews. Identify top 3 complaints. Respond publicly with patch plan. Release patch 1.0.1 within 1 week addressing complaints. | CLOCK + REED |
| Sales below expectations (<1K units in Week 1) | MEDIUM | MEDIUM | If sales are low, run Steam sale (10% off) in Week 3. Increase marketing (Reddit ads, YouTuber sponsorships). Pivot to long-tail strategy (update game regularly, build community). | CLOCK |

**Contingency**:
- If critical bug found in RC1, delay launch by 1-2 weeks. Better to delay than launch broken.
- If press coverage is zero, rely on organic Steam discovery (tags, recommendations, featured lists). Management sims have strong word-of-mouth.
- If reviews are negative, do not panic. Respond with roadmap. Players respect developers who listen and iterate.
- If sales are low, do not abandon game. Patch regularly. Build community. Management sims are slow burns (Game Dev Tycoon launched quietly, grew over months).

**Dependencies**:
- Launch (Week 49) depends on RC1 passing QA (Week 45-46). If RC1 has critical bugs, launch slips.
- Press outreach (Week 47) depends on Steam page being complete (Week 47). Cannot send press kit without trailer and screenshots.

---

## 3. SPRINT PLAN (HIGH-LEVEL)

**Sprint Structure**: 2-week sprints (except RC phase: 1-week sprints)
**Sprint Cadence**: Sprint starts Monday, ends Friday 2 weeks later. Weekend is buffer for overflow.
**Sprint Planning**: Monday Week 1 (2 hours: review last sprint, plan next sprint, assign tasks)
**Sprint Review**: Friday Week 2 (1 hour: demo completed work, discuss blockers)
**Daily Standups**: 15 minutes, async via Discord or Slack (small team, no synchronous meetings needed unless blocked)

**Sprint Breakdown** (26 total sprints over 52 weeks):

| Sprint | Weeks | Phase | Focus | Key Deliverable |
|--------|-------|-------|-------|-----------------|
| 1 | 1-2 | Prototype | Core setup + Brief System | Brief generation functional |
| 2 | 3-4 | Prototype | Team Manager + Concept Forge | Concepts generated from teams |
| 3 | 5-6 | Prototype | Approval Gauntlet FSM | Negotiation playable (no UI) |
| 4 | 7-8 | Prototype | Gauntlet UI + Production | Gauntlet has UI, budget allocation works |
| 5 | 9-10 | Prototype | Broadcast + Reaction | Campaign completes end-to-end |
| 6 | 11-12 | Prototype | Playtest + iteration | Vertical slice validated |
| 7 | 13-14 | Production | Reputation + Economy systems | Meta-progression functional |
| 8 | 15-16 | Production | Super Bowl sequence | Climax moment built |
| 9 | 17-18 | Production | Save/Load + Calendar + Morale | Session structure complete |
| 10 | 19-20 | Production | Awards + stretch goals (or content) | Awards ceremony functional |
| 11 | 21-22 | Production | Audio integration + Gauntlet polish | FMOD integrated, Gauntlet has personality |
| 12 | 23-24 | Production | Full-year playtest + iteration | Year loop validated |
| 13 | 25-26 | Alpha | Balance tuning (Economy, Gauntlet, Forge) | Systems balanced |
| 14 | 27-28 | Alpha | UI polish + audio integration | UI feels polished, audio reactive |
| 15 | 29-30 | Alpha | Accessibility + performance profiling | Game runs well on min-spec |
| 16 | 31-32 | Alpha | Content expansion + playtest marathon | Content volume sufficient |
| 17 | 33-34 | Alpha | Bug fixing sprint | Critical/High bugs fixed |
| 18 | 35-36 | Alpha | Final alpha QA | Alpha-complete milestone |
| 19 | 37-38 | Beta | Beta launch + initial triage | 50 beta testers playing |
| 20 | 39-40 | Beta | Balance iteration + UI polish pass 2 | Beta feedback addressed |
| 21 | 41-42 | Beta | Audio polish + content proofread | Audio final, text clean |
| 22 | 43-44 | Beta | Achievements + final optimization | Beta-complete milestone |
| 23 | 45-46 | Beta | Code freeze + beta wrap-up | Ready for RC |
| 24 | 47-48 | RC | RC1 build + press outreach | RC1 on Steam, press keys sent |
| 25 | 49-50 | RC | Marketing ramp-up + Steam page finalization | Launch announced |
| 26 | 51-52 | RC | Launch week + community management | Game live on Steam |

**Sprint Velocity Target**: ~40 story points per sprint (calibrated after Sprint 1-2)
**Buffer**: 2 weeks built into beta phase (Sprints 23-24 can absorb slippage from alpha)

---

## 4. RISK REGISTER (COMPREHENSIVE)

**Risk Scoring**:
- Severity: CRITICAL (game fails) | HIGH (major setback) | MEDIUM (manageable delay) | LOW (minor issue)
- Likelihood: VERY HIGH (>75%) | HIGH (50-75%) | MEDIUM (25-50%) | LOW (<25%)

| Risk | Severity | Likelihood | Impact | Mitigation | Owner | Phase |
|------|----------|-----------|--------|-----------|-------|-------|
| **Gauntlet feels like menu, not conversation** | CRITICAL | MEDIUM | Game fails core fantasy | Prototype early, iterate ruthlessly, add dialogue variations + animations | REED + NOVA | Prototype |
| **Concept Forge produces repetitive concepts** | HIGH | MEDIUM | Creative fantasy breaks | Expand content library (40+ logline templates), test with 30-campaign sequence | REED + NOVA | Production |
| **Super Bowl sequence is anticlimactic** | MEDIUM | LOW | Session payoff fails | Prototype as standalone vertical slice, add interactivity if flat | BYTE + REED | Production |
| **Economy too tight or too loose** | HIGH | MEDIUM | Player stress misaligned | Use Economy Simulator tool, playtest with varied strategies, tune via JSON | REED | Alpha |
| **Scope creep (stretch goals consume time)** | HIGH | MEDIUM | Timeline slips, core suffers | Feature lock at Alpha (Week 25), cut stretch goals if velocity drops | CLOCK | Production/Alpha |
| **Performance on low-end PCs / Switch** | MEDIUM | LOW | Framerate <60 FPS | Profile early (Week 25), optimize UI rendering, add Low Quality mode if needed | BYTE | Alpha |
| **Save system bugs (corruption, incompatibility)** | MEDIUM | LOW | Player frustration, lost progress | Implement save versioning from day 1, test frequently, 3 autosave slots | BYTE | Production/Beta |
| **Team velocity slower than estimated** | MEDIUM | HIGH | Timeline slips 2-4 weeks | Accept early slippage, cut content (not systems), use buffer in beta phase | CLOCK | All phases |
| **Asset production bottleneck (64 storyboard frames)** | MEDIUM | MEDIUM | Art assets delay integration | Contract out 50% of frames to external illustrator ($3K-$5K budget) | PIXEL | Production |
| **Audio integration issues (FMOD complexity)** | MEDIUM | LOW | Dynamic audio fails, falls back to static | ECHO begins FMOD setup early (Week 21), test layers, fallback to Unity Audio Mixer if needed | ECHO + BYTE | Production |
| **Critical bug found in RC1** | HIGH | LOW | Launch delayed 1-2 weeks | Thorough QA in Weeks 45-46, external QA if budget allows, build RC2 if needed | BYTE + CLOCK | RC |
| **Negative beta feedback (game not fun)** | CRITICAL | VERY LOW | Delay launch 4-6 weeks to fix | If 30%+ of beta testers cite same issue, delay and iterate. Player enjoyment > deadline. | CLOCK + REED | Beta |
| **Launch day crash spike (>5%)** | CRITICAL | LOW | Take game offline, fix within 48 hours | Monitor crash reports via Unity Cloud Diagnostics, hotfix immediately | BYTE + CLOCK | RC |
| **Negative reviews at launch (Mixed or worse)** | HIGH | LOW | Sales suffer, reputation damaged | Read reviews, identify top complaints, patch within 1 week, communicate roadmap | CLOCK + REED | Post-launch |
| **Press does not cover game** | MEDIUM | MEDIUM | Low launch visibility | Pivot to community-driven marketing (Reddit AMAs, streamer outreach, organic growth) | CLOCK | RC |
| **Sales below expectations (<1K Week 1)** | MEDIUM | MEDIUM | Revenue insufficient for post-launch | Run Steam sale (10% off) Week 3, increase marketing, build community, long-tail strategy | CLOCK | Post-launch |

**Risk Response Strategy**:
- **Critical risks**: Monitor daily during relevant phase. Escalate to team immediately if triggered. Be willing to delay launch to fix.
- **High risks**: Monitor weekly. Mitigate proactively (e.g., cut stretch goals before velocity drops, not after).
- **Medium/Low risks**: Monitor at milestone reviews. Accept some low risks (not all risks are worth mitigating).

---

## 5. CRITICAL PATH ANALYSIS

**Critical Path**: The sequence of dependent tasks that determines the minimum project duration. If any task on the critical path is delayed, the entire project is delayed.

**Critical Path for UPFRONT** (tasks that cannot slip):

```
[Start] → Brief System → Team Manager → Concept Forge → Approval Gauntlet →
Prototype Playtest → Super Bowl Sequence → Full Year Playtest → Balance Tuning →
Beta Launch → Beta Complete → RC1 Build → Launch
```

**Breakdown**:

1. **Brief System (Weeks 3-4)**: Blocks Team Manager (cannot assign teams without briefs)
2. **Team Manager (Weeks 5-6)**: Blocks Concept Forge (cannot generate concepts without teams)
3. **Concept Forge (Weeks 7-8)**: Blocks Approval Gauntlet (cannot negotiate without concepts)
4. **Approval Gauntlet (Weeks 9-10)**: Blocks Prototype Playtest (Gauntlet is core mechanic — must be validated)
5. **Prototype Playtest (Weeks 11-12)**: Blocks Production phase (cannot expand systems until core loop is validated)
6. **Super Bowl Sequence (Weeks 17-20)**: Blocks Full Year Playtest (year must include Super Bowl)
7. **Full Year Playtest (Week 24)**: Blocks Alpha phase (cannot balance until full loop is playable)
8. **Balance Tuning (Weeks 25-28)**: Blocks Beta Launch (cannot ship beta with broken balance)
9. **Beta Launch (Week 37)**: Blocks Beta Complete (beta must run for 4+ weeks to collect feedback)
10. **Beta Complete (Week 44)**: Blocks RC1 Build (cannot build RC until beta validates stability)
11. **RC1 Build (Weeks 45-46)**: Blocks Launch (cannot launch without final build)
12. **Launch (Week 49)**: End of critical path

**Parallel Paths** (can happen simultaneously, NOT on critical path):

- **Content Production** (briefs, loglines, storyboard frames, portraits, SFX, music): Happens in parallel to system development. Can slip by 1-2 weeks without blocking critical path (as long as assets are ready by Full Year Playtest).
- **Stretch Goals** (Cultural Trends, Rival Agencies, Office Customization): NOT on critical path. Can be cut without impacting launch.
- **UI Polish** (animations, transitions, hover states): Happens in parallel to balance tuning in Alpha. Important for feel, but not blocking (can ship with 80% polish if needed).
- **Achievements**: Happens in parallel to Beta. Can be deferred to post-launch patch if needed.

**Critical Path Buffer**:
- 2 weeks buffer in Beta phase (Weeks 43-44 can absorb slippage from Alpha)
- 1 week buffer in RC phase (Week 48 is flex week for RC2 if RC1 has critical bugs)

**What This Means**:
- **Do not delay Gauntlet prototype** (Weeks 9-10). This is the highest-risk task on critical path. If Gauntlet slips by 2 weeks, entire project slips by 2 weeks.
- **Do not delay Full Year Playtest** (Week 24). This validates the year loop. Slipping this delays Alpha, which delays Beta, which delays Launch.
- **You CAN delay content production** by 1-2 weeks (e.g., storyboard frames not done by Week 24) as long as placeholder assets allow playtest to proceed. Polish later.
- **You CAN cut stretch goals** (Trends, Rivals) with zero impact to critical path. Cut ruthlessly if needed.

---

## 6. SCOPE MANAGEMENT

### 6.1 Feature Pillars (Non-Negotiable)

These are the core systems that define UPFRONT. They ship, or the game does not ship.

1. **Brief System & Concept Forge**: Procedural brief generation + concept generation from team chemistry. (BYTE + REED + NOVA)
2. **The Approval Gauntlet**: Client negotiation with pushback, compromise, walk away. (BYTE + REED + NOVA)
3. **Team Chemistry Engine**: Creatives with distinct personalities, chemistry affects output. (BYTE + REED)
4. **Super Bowl Sunday**: Annual climax with ad airing, audience reaction, Monday Morning report. (BYTE + REED + NOVA + PIXEL)
5. **Agency Reputation & Economy**: Persistent reputation system (3 sub-scores), cash flow tracking, client tier unlocks. (BYTE + REED)

**Total**: 5 feature pillars. All must be functional and polished by Beta Complete (Week 44).

---

### 6.2 Stretch Goals (Cut if Timeline Slips)

These systems are desirable but not essential. Cut in this order:

1. **Office Customization** (unlockable furniture, decor, passive stat bonuses): NICE TO HAVE. Does not affect core loop. Cut first if timeline slips. (Savings: 2 weeks, PIXEL + BYTE)
2. **Award Season** (Clio/Cannes simulation, submission, ceremony): NICE TO HAVE. Adds prestige but not essential to year loop. Cut second. (Savings: 2 weeks, BYTE + REED)
3. **Cultural Trend System** (zeitgeist shifts year-to-year, tone preferences change): ADDS DEPTH. Enriches replayability but game works without it. Cut third. (Savings: 1 week, BYTE + REED)
4. **Rival Agencies** (AI competitors, bid on Super Bowl, poach talent): ADDS FLAVOR. Fun but not core to player experience. Cut fourth. (Savings: 2 weeks, BYTE + REED)

**Cutting Strategy**:
- If timeline slips by 2 weeks (Sprint 10 or earlier): Cut Office Customization.
- If timeline slips by 4 weeks (Sprint 12 or earlier): Also cut Award Season.
- If timeline slips by 6 weeks (Sprint 14 or earlier): Also cut Cultural Trends.
- If timeline slips by 8+ weeks (Sprint 16 or earlier): Also cut Rival Agencies. At this point, reassess project viability with team.

**What We Do NOT Cut**:
- **Gauntlet dialogue variations** (5+ per client note): Essential to making Gauntlet feel human. This is not negotiable. If this slips, delay launch.
- **Super Bowl sequence polish** (expanded reaction panel, Monday Morning meeting): This is the session payoff. Must feel climactic. Not negotiable.
- **Economy balance** (cash flow tuning, crisis frequency): If economy is broken, game is unplayable. Not negotiable.

---

### 6.3 Content Volume Targets

**Minimum Viable Content** (ships at launch):

| Content Type | Target | Minimum (if slip) | Owner |
|--------------|--------|-------------------|-------|
| **Briefs** | 70 | 50 | REED |
| **Logline Templates** | 40 | 30 | NOVA |
| **Storyboard Frames** | 64 (8x8) | 32 (4x4 generic) | PIXEL |
| **Viewer Portraits** | 20 | 12 | PIXEL |
| **Client Dialogue Variations** | 5+ per note type | 3 per note type | NOVA |
| **Music Tracks** | 12 cues | 6 (Office, Gauntlet, Super Bowl x2, Award, Crisis) | ECHO |
| **SFX** | 150 one-shots | 100 (cut ambient variety) | ECHO |

**Content Expansion Post-Launch** (if PC launch succeeds):
- Add 30 briefs, 10 logline templates, 16 storyboard frames (patch 1.1, free)
- Add 2-3 new client archetypes with unique note pools (patch 1.2, free or $3 DLC)

---

## 7. KEY DEPENDENCIES (WHAT BLOCKS WHAT)

**System Dependencies** (cannot start Y until X is complete):

| Task X (Prerequisite) | Task Y (Dependent) | Blocker Reason |
|-----------------------|-------------------|----------------|
| Brief System (W3-4) | Team Manager (W5-6) | Cannot assign teams without briefs to assign to |
| Team Manager (W5-6) | Concept Forge (W7-8) | Cannot generate concepts without teams to generate them |
| Concept Forge (W7-8) | Approval Gauntlet (W9-10) | Cannot negotiate without concepts to negotiate over |
| Gauntlet FSM (W9-10) | Gauntlet UI (W13-16) | Cannot build UI until FSM logic is functional |
| Broadcast System (W12) | Super Bowl Sequence (W17-20) | Super Bowl is extended version of broadcast — cannot build until base broadcast works |
| Save/Load System (W17-18) | Full Year Playtest (W24) | Cannot playtest full year without saving progress between sessions |
| FMOD Setup (W21) | Audio Integration (W21-24) | Cannot integrate dynamic music until FMOD project is configured |
| Storyboard Frames (ongoing, PIXEL) | Super Bowl Sequence (W17-20) | Cannot display ad animatics without storyboard frames |
| Full Year Playtest (W24) | Alpha Balance Tuning (W25-28) | Cannot balance economy/Gauntlet without full year data |
| Alpha Complete (W36) | Beta Launch (W37) | Cannot launch beta with unstable build |
| Beta Complete (W44) | RC1 Build (W45-46) | Cannot build RC until beta validates stability |
| RC1 QA Pass (W45-46) | Launch (W49) | Cannot launch without QA-validated build |

**Resource Dependencies** (shared resources create bottlenecks):

| Resource (Person) | Shared Across | Bottleneck Risk | Mitigation |
|-------------------|---------------|-----------------|------------|
| **BYTE (Programmer)** | All systems | HIGH — BYTE is on critical path for 20+ weeks | Prioritize critical path tasks. Defer polish (animations, achievements) to beta. |
| **REED (Designer)** | Brief content, balance tuning, playtesting | MEDIUM — REED splits time between content creation and balance | Front-load brief authoring (complete 50 briefs by Week 16). Balance tuning happens in Alpha (dedicated time). |
| **NOVA (Writer)** | Loglines, dialogue, character arcs | MEDIUM — NOVA must deliver dialogue variations by Week 16 (Gauntlet polish) | Write client archetypes + note dialogue in Weeks 13-16. Loglines are iterative (can expand in Alpha). |
| **PIXEL (Artist)** | UI mockups, storyboard frames, portraits | HIGH — 64 storyboard frames is heavy lift | Contract out 50% of frames ($3K-$5K). PIXEL art directs, contractor executes. |
| **ECHO (Audio)** | SFX recording, music composition, FMOD integration | MEDIUM — Audio integration happens late (W21-24), risk of crunch | Begin FMOD setup early (W21). Contract out music composition if ECHO bandwidth is tight. |

**External Dependencies** (outside team's control):

| Dependency | Risk | Impact | Mitigation |
|------------|------|--------|-----------|
| **Contractor availability** (illustrator, composer) | MEDIUM | Storyboard frames or music delayed | Contract early (by Week 12). Have backup contractors identified. Pay 50% upfront to secure commitment. |
| **Unity LTS stability** (engine bugs) | LOW | Development blocked by Unity bug | Use stable 2023.2 LTS. Monitor Unity forums for known issues. Downgrade if critical bug found. |
| **Steam platform stability** (SteamPipe, workshop) | LOW | Cannot upload builds | Test Steam build upload in Week 24 (early). If SteamPipe is broken, delay launch until Steam fixes it (out of our control). |
| **Beta tester recruitment** (50+ players) | MEDIUM | Beta has <20 players, insufficient feedback | Begin recruiting in Week 30 (7 weeks before beta launch). Post on Reddit, Discord, mailing list. Offer free copy of game to early testers. |

---

## 8. TEAM HEALTH & MORALE MANAGEMENT

**The Team is the Asset**: A burned-out team ships a broken game. Protect the team.

### 8.1 Crunch Policy

**Policy**: No crunch. Crunch is a management failure, not a badge of honor.

**Definition of Crunch**: Working >45 hours/week for >2 consecutive weeks.

**If Crunch is Detected**:
1. **Identify cause**: Is it unrealistic sprint goals? Is it scope creep? Is it a blocker (bug, missing dependency)?
2. **Cut scope**: If sprint goals are too ambitious, cut features. If timeline is too tight, delay launch.
3. **Do not push through**: Crunch produces low-quality work. A tired team makes bad decisions. It is never worth it.

**Acceptable Overtime** (not crunch):
- 1-2 extra hours on launch week (Week 49) to monitor crash reports and respond to community. This is acceptable because it is time-boxed (1 week) and voluntary.
- 1-2 extra hours before major milestones (prototype playtest, alpha complete, beta launch) to finish polish. This is acceptable if it is <2 weeks and team agrees.

**Burnout Warning Signs**:
- Team member misses standups or sprint planning
- Quality of work drops (more bugs, less attention to detail)
- Team member expresses frustration or disengagement
- Sprint velocity drops by 30%+ for 2 consecutive sprints

**Burnout Response**:
- **Talk to team member**: 1-on-1 conversation. What is wrong? Are sprint goals too ambitious? Is there a personal issue?
- **Reduce workload**: Reassign tasks to other team members. Extend sprint by 1 week. Cut stretch goals.
- **Take time off**: Encourage team member to take 3-5 days off. A rested team is more productive than a burned-out team pushing through.

---

### 8.2 Morale Management

**Morale Boosters** (things that make the team feel good):

1. **Celebrate milestones**: When prototype playtests well, celebrate. When alpha is complete, celebrate. When game launches, celebrate. Recognition matters.
2. **Public progress**: Post sprint progress on Discord or internal blog. Team sees the game coming together. Momentum builds morale.
3. **Playtest wins**: When a playtester says "I love this," share it with the team. External validation is powerful.
4. **Autonomy**: Let team members own their systems. BYTE owns Gauntlet FSM. PIXEL owns UI. ECHO owns audio. Trust the team.

**Morale Killers** (things that demoralize):

1. **Unclear goals**: If team does not know what success looks like, they feel lost. Define exit criteria for every milestone.
2. **Scope creep**: Adding features mid-sprint makes team feel like they are never done. Feature lock at Alpha.
3. **No feedback**: If team works for weeks without playtesting, they do not know if work is good. Playtest often.
4. **Ignoring concerns**: If team member says "this system is not fun," listen. Do not dismiss. Discuss and iterate.

**Weekly Check-In** (15 minutes, async or sync):
- **What went well this week?**
- **What is blocking you?**
- **What are you working on next week?**
- **How are you feeling (1-10 scale)?**

If anyone reports <6 on morale scale for 2 consecutive weeks, escalate (1-on-1 conversation, reduce workload, cut scope).

---

## 9. SUCCESS METRICS (HOW WE KNOW WE WON)

### 9.1 Development Milestones (Internal)

| Milestone | Success Criteria | Measurement |
|-----------|-----------------|-------------|
| **Prototype Complete (W12)** | 5 external playtesters complete vertical slice, >50% say "I wanted to fight for my ad" | Playtest survey |
| **Production Complete (W24)** | 10 playtesters complete full year, >70% say "I want to play more" | Playtest survey |
| **Alpha Complete (W36)** | Crash rate <5%, playtesters finish 5-year careers, economy balanced | Bug tracker + playtest data |
| **Beta Complete (W44)** | Crash rate <1%, positive player sentiment (Mixed or better if public reviews) | Unity Cloud Diagnostics + Steam reviews |
| **Launch (W49)** | Game live on Steam, crash rate <1%, no critical bugs | Unity Cloud Diagnostics |

---

### 9.2 Launch Success Metrics (External)

**Week 1 Post-Launch**:

| Metric | Target | Stretch Goal | Measurement |
|--------|--------|--------------|-------------|
| **Units Sold** | 1,000 | 3,000 | Steamworks dashboard |
| **Steam Review Score** | Positive (70-79%) | Very Positive (80%+) | Steam store page |
| **Crash Rate** | <1% | <0.5% | Unity Cloud Diagnostics |
| **Refund Rate** | <10% | <5% | Steamworks dashboard |
| **Press Coverage** | 5+ articles/videos | 10+ articles/videos | Manual tracking |

**Month 1 Post-Launch**:

| Metric | Target | Stretch Goal | Measurement |
|--------|--------|--------------|-------------|
| **Units Sold** | 5,000 | 10,000 | Steamworks dashboard |
| **Steam Review Score** | Positive (70-79%) | Very Positive (80%+) | Steam store page (cumulative) |
| **Wishlist Conversions** | 20% of wishlists convert to sales | 30% | Steamworks dashboard |
| **Community Engagement** | 500+ Discord members, 100+ active | 1,000+ Discord, 200+ active | Discord analytics |

**Year 1 Post-Launch**:

| Metric | Target | Stretch Goal | Measurement |
|--------|--------|--------------|-------------|
| **Units Sold** | 10,000 | 25,000 | Steamworks dashboard |
| **Revenue** (post-platform cut) | $100K | $250K | Steamworks dashboard (70% of $14.99 per unit) |
| **Break-Even** | Revenue > total burn ($21K-$367K) | Profitable enough to fund Switch port | Financial tracking |
| **Post-Launch Patches** | 3-5 patches addressing top player requests | 5+ patches + 1 content DLC | Patch notes |

---

### 9.3 What "Success" Means

**Minimum Viable Success**: 10,000 units sold in Year 1, Positive Steam reviews, break-even on budget.

**This funds**:
- Post-launch support (patches, bug fixes)
- Next project (if team wants to continue)
- Switch port (if demand exists)

**Stretch Success**: 25,000 units sold in Year 1, Very Positive Steam reviews, profitable enough to fund Switch port + DLC.

**This funds**:
- Switch port (6 months dev time)
- Content expansion DLC ($5, adds 30 briefs + new systems)
- Team salaries for next project

**What Failure Looks Like**: <1,000 units sold in Month 1, Negative/Mixed reviews, high refund rate (>15%).

**If This Happens**:
- Post-mortem: What went wrong? Was it marketing? Was the game not fun? Was pricing wrong?
- Patch aggressively: Address top player complaints within 2 weeks. Show players we are listening.
- Pivot marketing: Try different channels (Reddit ads, YouTuber sponsorships, bundles).
- Accept failure: Not every game succeeds. Learn, move on, make the next one better.

---

## 10. CLOSING NOTES

### 10.1 What Could Go Wrong

I manage teams through crunch. I have watched projects collapse under scope creep. I know how games die. Here is what keeps me awake:

**The Gauntlet does not feel tense.** This is the core mechanic. If it feels like a menu, the game fails. We prototype it first (Week 9-10). We iterate ruthlessly. We do not ship until it sings. If it does not work by Week 12, we pivot or delay. No exceptions.

**Scope creep.** Every designer wants more features. Every artist wants more polish. The game already has 10+ interlocking systems. Adding more is how indie teams burn out and projects die. Feature lock at Week 25 (Alpha). Cut stretch goals before they consume core dev time. CLOCK enforces this. Not negotiable.

**Team burnout.** A tired team makes bad decisions. If sprint velocity drops, we cut scope, not push through. If a team member is burned out, they take time off. A delayed game that ships is better than a rushed game that dies in development.

**Launch day disasters.** Crash spikes. Negative reviews. No press coverage. We mitigate by testing early and often. We have contingency plans (hotfixes, patch roadmaps, community-driven marketing). We do not panic. We respond.

---

### 10.2 What Could Go Right

If we ship on time, if the Gauntlet works, if the Super Bowl feels climactic, this game is special. No other management sim makes defending creative work the core verb. The market is there (Game Dev Tycoon: 2.5M units, Two Point Hospital: 4M units). The setting is untapped (no one has made an ad agency sim). The fantasy is real (every creative person has felt the tension of defending work to someone with authority).

The architecture is solid. Unity is boring (boring is good). The event bus decouples systems. JSON configs let designers iterate without code changes. The critical path is clear. The risks are identified. The mitigation strategies are in place. The team is small enough to move fast, large enough to cover all disciplines.

We ship in 12 months. We cut scope, not corners. We protect the team. We launch with a stable, fun, polished game that delivers on the player fantasy.

**Ship the game. Learn. Make the next one better. That is the only way forward.**

---

### 10.3 Producer's Commitment

As producer, I commit to:

1. **Protect the team**: No crunch. No scope creep. No unrealistic deadlines.
2. **Track dependencies**: Update critical path weekly. Escalate blockers immediately.
3. **Cut ruthlessly**: When timeline slips, cut stretch goals before core systems suffer.
4. **Communicate clearly**: Sprint goals are concrete. Exit criteria are non-negotiable. Team always knows what success looks like.
5. **Celebrate wins**: Milestones matter. Playtest feedback matters. Team morale matters.
6. **Ship the game**: A shipped game beats a perfect concept. We ship in 12 months, or we delay and ship when it is ready. We do not ship broken.

This production plan is a living document. As prototyping reveals unknowns, we update this plan. But the core structure — milestones, critical path, risk register, scope management — remains stable.

**Cut scope, not corners. Protect the team. Ship the game.**

--- CLOCK

---

## APPENDIX A: MILESTONE CHECKLIST

**Prototype Complete (Week 12)**:
- [ ] One campaign playable end-to-end (~8 minutes)
- [ ] Brief generation functional (8 archetypes, 20+ briefs)
- [ ] Team assignment functional (6 creatives, chemistry calculation)
- [ ] Concept Forge generates 3 concepts per brief
- [ ] Approval Gauntlet FSM complete (3-5 rounds, negotiation works)
- [ ] Gauntlet UI has placeholder animations
- [ ] Production Pipeline functional (5 sliders, budget allocation)
- [ ] Broadcast & Reaction displays audience score
- [ ] 5 playtesters complete vertical slice
- [ ] Playtest feedback: >50% say "I wanted to fight for my ad"
- [ ] Zero critical bugs (no crashes, no soft-locks)

**Production Complete (Week 24)**:
- [ ] Full year (Q1-Q4 + Super Bowl) playable
- [ ] 50+ briefs, 30+ logline templates
- [ ] Team Chemistry edge cases functional (Meltdown, Brilliant Friction)
- [ ] Gauntlet UI polished (5+ dialogue variations per note, client expressions)
- [ ] Reputation System functional (3 sub-scores, tier unlocks)
- [ ] Economy System functional (revenue, expenses, cash flow)
- [ ] Super Bowl sequence complete (extended animatic, reaction panel, Monday Morning)
- [ ] Save/Load system functional (JSON, autosave, versioning)
- [ ] Calendar UI functional (year overview, quarter tracking)
- [ ] Morale system functional (life events, loyalty, quit threats)
- [ ] Awards system functional (submission, ceremony)
- [ ] Storyboard frames: 32+ completed (target: 64)
- [ ] Viewer portraits: 12+ completed (target: 20)
- [ ] Audio assets: 3 music tracks, 50+ SFX integrated
- [ ] 10 playtesters complete full year without critical bugs
- [ ] Playtest feedback: >70% say "I want to play more"

**Alpha Complete (Week 36)**:
- [ ] Feature lock enforced (no new systems after Week 25)
- [ ] Economy balanced (2-3 cash crises per career, not constant)
- [ ] Gauntlet balanced (pushback success rates match targets)
- [ ] Concept Forge balanced (no repetition within 30 campaigns)
- [ ] Performance: 60 FPS on target PC spec
- [ ] UI polish pass 1 complete (transitions, hover states, tooltips)
- [ ] Audio polish complete (FMOD integrated, mix balanced)
- [ ] Accessibility features implemented (colorblind modes, UI scale, high-contrast)
- [ ] Content expansion: 70 briefs, 40 logline templates
- [ ] Playtest marathon complete (3-5 testers, 5-year careers)
- [ ] Bug backlog: All Critical and High bugs fixed
- [ ] Crash rate <5%

**Beta Complete (Week 44)**:
- [ ] Closed beta launched (50+ players)
- [ ] Crash rate <1%
- [ ] All Critical bugs fixed
- [ ] All High bugs fixed or documented with workarounds
- [ ] Medium/Low bugs documented for post-launch
- [ ] Performance: 60 FPS on target PC, 30+ FPS on min-spec
- [ ] Audio polish: All tracks mixed and mastered
- [ ] Content polish: No typos in player-facing text
- [ ] Achievements: 30-40 implemented and tested
- [ ] Steam store page complete (screenshots, trailer, description)
- [ ] Press list: 20-30 contacts identified

**Launch (Week 49)**:
- [ ] RC1 build QA-passed (Windows, macOS, Linux)
- [ ] Steam build uploaded via SteamPipe
- [ ] Store page live (screenshots, trailer, tags, description)
- [ ] Press keys sent to 20+ outlets/YouTubers
- [ ] Launch announced (social media, Reddit, Discord, mailing list)
- [ ] Community channels active (Steam forums, Discord)
- [ ] Day 1 patch ready (if needed)
- [ ] Crash rate <1% on launch day
- [ ] Sales tracking dashboard set up

---

## APPENDIX B: CONTACT SHEET

| Role | Name | Responsibilities | Email/Discord |
|------|------|-----------------|---------------|
| **Producer** | CLOCK | Milestone tracking, risk management, scope enforcement | [contact] |
| **Lead Programmer** | BYTE | Core systems, Unity implementation, performance | [contact] |
| **Game Designer** | REED | System design, balance, playtesting | [contact] |
| **Narrative Designer** | NOVA | Dialogue, character arcs, loglines | [contact] |
| **Art Director** | PIXEL | UI design, storyboards, isometric art | [contact] |
| **Sound Designer** | ECHO | SFX, music, FMOD integration | [contact] |
| **Contractors** | | | |
| Illustrator | [TBD] | Storyboard frames (32+ frames) | [contact] |
| Composer | [TBD] | Music composition (6 weeks) | [contact] |
| Foley Artist | [TBD] | Office SFX recording (2 days) | [contact] |
| Voice Actors | [TBD] | Human reaction sounds (4-6 people, 1 day) | [contact] |

---

## APPENDIX C: SPRINT RETROSPECTIVE TEMPLATE

**Sprint [#]** (Weeks X-Y)
**Date**: [Date]
**Attendees**: [Team members]

**What Went Well**:
- [Accomplishment 1]
- [Accomplishment 2]
- [Accomplishment 3]

**What Could Be Improved**:
- [Issue 1]
- [Issue 2]
- [Issue 3]

**Blockers**:
- [Blocker 1: Description | Owner | Status]
- [Blocker 2: Description | Owner | Status]

**Sprint Velocity**:
- **Planned**: [X story points]
- **Completed**: [Y story points]
- **Velocity**: [Y/X = Z%]

**Next Sprint Focus**:
- [Priority 1]
- [Priority 2]
- [Priority 3]

**Action Items**:
- [ ] [Action 1 | Owner | Due Date]
- [ ] [Action 2 | Owner | Due Date]

---

**END OF PRODUCTION PLAN**

*This plan is the contract between the team and the deadline. We ship in 12 months. We cut scope when needed. We protect the team. We ship a game that delivers on the player fantasy. Anything that does not serve that goal gets cut. No exceptions.*

*What's the critical path? Build the Gauntlet first. If that works, everything else follows.*

*Ship it.*

— CLOCK
