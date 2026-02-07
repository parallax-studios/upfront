# UPFRONT — Release Plan

**Author**: SHIP (Release Manager)
**Version**: 1.0
**Date**: 2026-02-07
**Status**: Production Release Checklist — Ready for Execution

---

> "First impressions are permanent. Launch day defines a game's trajectory. There are no second chances for a botched release."

I have read the pitch, the design doc, and the technical architecture. I know what this game is: a narrative-driven management sim where the player manages an advertising agency, navigates the Approval Gauntlet, and chases the Super Bowl. It is PC-first on Steam, with potential Switch and iPad ports post-launch.

This document is the master checklist. Every step from code complete to live on Steam. Every contingency. Every rollback plan. Every hour of launch day. If it is not on the checklist, it does not happen.

Launch day will be boring. That means I did my job.

---

## 1. MASTER LAUNCH CHECKLIST

### 1.1 Overview

The checklist is organized into seven phases:

1. **PRE-PRODUCTION SETUP** (Months 1-3) — Repository, tools, pipelines
2. **BUILD PIPELINE** (Months 4-12) — Continuous integration, automated builds
3. **PLATFORM CONFIGURATION** (Months 9-12) — Steam setup, achievements, DRM
4. **PRE-LAUNCH PREP** (Months 10-12) — Store page, press, marketing
5. **GOLD MASTER** (Week of launch) — Final build, submission, approval
6. **LAUNCH DAY** (Day 0) — Go-live, monitoring, hotfix readiness
7. **POST-LAUNCH** (Weeks 1-4) — Patch pipeline, analytics, player support

Each phase has a checklist. Each checklist item has an owner, a deadline, and a definition of done.

---

### 1.2 Phase 1: Pre-Production Setup (Months 1-3)

**Goal**: Establish the foundation for repeatable, reliable builds.

| Task | Owner | Deadline | Status | Definition of Done |
|------|-------|----------|--------|-------------------|
| Initialize Git repository with LFS | BYTE | Week 1 | [ ] | Repo cloned, .gitignore configured, LFS tracking binary assets |
| Set up Unity project (2023.2 LTS) | BYTE | Week 1 | [ ] | Project opens without errors, version control integration working |
| Create build pipeline (Unity Cloud Build or Jenkins) | BYTE | Week 4 | [ ] | Automated Windows build triggered on commit to `develop` branch |
| Establish branch strategy (main/develop/feature) | BYTE | Week 2 | [ ] | Branching policy documented in repo README |
| Set up Steam partner account | SHIP | Week 6 | [ ] | Account created, app ID registered (placeholder name OK) |
| Generate Steamworks SDK credentials | SHIP | Week 6 | [ ] | API keys stored securely, not committed to repo |
| Create internal playtest distribution method | SHIP | Week 8 | [ ] | Itch.io private page OR Dropbox folder for build sharing |
| Document build process in repo wiki | BYTE | Week 12 | [ ] | Any team member can build locally by following wiki steps |

**Critical Path**: Build pipeline must be operational by Month 3. If we cannot build automatically, every subsequent phase breaks.

---

### 1.3 Phase 2: Build Pipeline (Months 4-12)

**Goal**: Maintain continuous integration. Always have a working build.

| Task | Owner | Deadline | Status | Definition of Done |
|------|-------|----------|--------|-------------------|
| Add macOS build target to pipeline | BYTE | Month 4 | [ ] | macOS builds auto-generated alongside Windows |
| Add Linux build target to pipeline | BYTE | Month 5 | [ ] | Linux builds auto-generated (for Steam Deck compatibility) |
| Implement build versioning (semantic versioning) | BYTE | Month 5 | [ ] | Builds tagged with version (e.g., v0.5.2-alpha), visible in main menu |
| Set up automated unit tests (if any) | BYTE | Month 6 | [ ] | Tests run on commit, build fails if tests fail |
| Configure release build pipeline (optimized) | BYTE | Month 9 | [ ] | Separate pipeline for release builds with code stripping, obfuscation |
| Generate build artifacts for QA | BYTE | Month 10 | [ ] | Builds uploaded to shared location, QA team has access |
| Establish nightly build schedule | BYTE | Month 7 | [ ] | Nightly builds auto-triggered at 2 AM, logs sent to team Slack/Discord |
| Document rollback procedure for broken builds | BYTE | Month 8 | [ ] | Wiki page: "How to revert to last known good build" |

**Critical Path**: By Month 7 (Alpha), nightly builds must be rock-solid. QA cannot test unstable builds.

---

### 1.4 Phase 3: Platform Configuration (Months 9-12)

**Goal**: Configure Steam integration, achievements, cloud saves, and store page.

#### 3.1 Steamworks Configuration

| Task | Owner | Deadline | Status | Definition of Done |
|------|-------|----------|--------|-------------------|
| Set up Steamworks app ID (production) | SHIP | Month 9 | [ ] | App ID active, set to "coming soon" state |
| Configure Steam depot structure (Windows/Mac/Linux) | SHIP | Month 9 | [ ] | Depots created for each platform, manifest files configured |
| Integrate Steamworks.NET SDK into Unity project | BYTE | Month 9 | [ ] | SDK imported, test build detects Steam client, logs user Steam ID |
| Implement Steam Cloud Save integration | BYTE | Month 10 | [ ] | Save files sync to Steam Cloud on exit, restore on launch |
| Configure Steam Cloud quota (5MB recommended) | SHIP | Month 10 | [ ] | Quota set in Steamworks admin, tested with max-size save file |
| Implement Steam Rich Presence | BYTE | Month 11 | [ ] | Player status shows "In Gauntlet" / "Year 3, Q2" on friends list |
| Test Steamworks integration on clean machine | CRASH | Month 11 | [ ] | Game launches via Steam, achievements fire, cloud saves sync |

#### 3.2 Achievements

| Task | Owner | Deadline | Status | Definition of Done |
|------|-------|----------|--------|-------------------|
| Design achievement list (30-40 achievements) | HYPE + REED | Month 9 | [ ] | List includes milestone achievements, hidden achievements, joke achievements |
| Create achievement icons (64x64 px) | PIXEL | Month 10 | [ ] | Icons uploaded to Steamworks, visible in achievement admin |
| Implement achievement unlock triggers in code | BYTE | Month 10 | [ ] | Achievements fire on correct events (e.g., "Win first Clio", "Fire client in Gauntlet") |
| Test all achievements on dev build | CRASH | Month 11 | [ ] | Every achievement confirmed unlockable in normal gameplay |
| Configure achievement rarity percentages (estimate) | SHIP | Month 11 | [ ] | Steamworks admin has rarity estimates (updated post-launch with real data) |

**Achievement Design Notes**:
- Include "story milestone" achievements (first campaign, first Super Bowl, year 5 complete)
- Include "skill-based" achievements (Win Cannes Grand Prix, Legendary audience score)
- Include "discovery" achievements (Walk away from client, Meltdown team produces hit ad)
- Include "easter egg" achievements (hidden, not revealed on Steam until unlocked)

#### 3.3 DRM & Anti-Piracy

| Task | Owner | Deadline | Status | Definition of Done |
|------|-------|----------|--------|-------------------|
| Decide on DRM approach (Steam DRM vs. none) | SHIP + BYTE | Month 9 | [ ] | Decision documented. Recommendation: Steam DRM only (lightweight, non-intrusive) |
| Enable Steam DRM wrapper in Steamworks | SHIP | Month 10 | [ ] | Executable wrapped, cannot launch without Steam client |
| Test DRM-wrapped build on clean machine | CRASH | Month 11 | [ ] | Game launches via Steam, fails if Steam offline |

**DRM Philosophy**: Use Steam DRM only. Do not use additional third-party DRM (Denuvo, etc.). Reason: Management sim audience skews older, values convenience over anti-piracy theater. Steam DRM is sufficient to prevent casual piracy. Aggressive DRM alienates legitimate customers.

#### 3.4 Controller Support

| Task | Owner | Deadline | Status | Definition of Done |
|------|-------|----------|--------|-------------------|
| Implement controller input mapping | BYTE | Month 10 | [ ] | Xbox / PS5 / Switch Pro controller detected, buttons mapped |
| Add on-screen button prompts (auto-switch) | BYTE | Month 11 | [ ] | Prompts change from keyboard to controller based on last input |
| Test on Steam Deck | CRASH | Month 11 | [ ] | Game playable at 30+ FPS on Deck, text readable at native resolution |
| Mark as "Steam Deck Verified" (if passes) | SHIP | Month 12 | [ ] | Submitted to Valve for Deck verification, badge approved |

**Steam Deck Notes**: This game is ideal for Deck (UI-heavy, no twitch gameplay). Ensure text size is readable at 800p. Target 40-60 FPS. If performance is an issue, add a "Low Quality" graphics preset that reduces UI effects.

---

### 1.5 Phase 4: Pre-Launch Prep (Months 10-12)

**Goal**: Build marketing assets, finalize store page, distribute press keys.

#### 4.1 Steam Store Page

| Task | Owner | Deadline | Status | Definition of Done |
|------|-------|----------|--------|-------------------|
| Write store page description (short & long) | HYPE + NOVA | Month 10 | [ ] | Description captures hook ("Mad Men meets Game Dev Tycoon"), features list, min specs |
| Generate 5 store screenshots (1920x1080) | PIXEL | Month 10 | [ ] | Screenshots show Gauntlet, concept selection, Super Bowl, agency office, broadcast reaction |
| Record gameplay trailer (1-2 minutes) | HYPE + PIXEL | Month 11 | [ ] | Trailer uploaded to YouTube unlisted, embedded on Steam page |
| Record announce trailer (30-60 seconds) | HYPE + PIXEL | Month 10 | [ ] | Short teaser for social media, shows Super Bowl moment, ends with logo |
| Write system requirements (min/recommended) | BYTE | Month 10 | [ ] | Specs tested on real hardware, not guessed |
| Generate capsule art (header, library, grid) | PIXEL | Month 11 | [ ] | All Steam image sizes generated, uploaded to Steamworks |
| Set "Coming Soon" date on Steam | SHIP | Month 10 | [ ] | Store page visible but not purchasable, wishlist enabled |
| Set release date on Steam (final) | SHIP | Month 12 Week 1 | [ ] | Release date locked 2 weeks before launch |
| Proofread store page (copy editing pass) | NOVA | Month 11 | [ ] | Zero typos, grammar errors, formatting issues |

**Store Page Copy Philosophy**: The description should answer three questions in 30 seconds:
1. What is the core loop? (Manage ad agency, create campaigns, navigate client approval)
2. What makes it unique? (Approval Gauntlet mechanic, Super Bowl climax)
3. Who is this for? (Game Dev Tycoon fans, Mad Men fans, creative industry professionals)

#### 4.2 Press & Marketing

| Task | Owner | Deadline | Status | Definition of Done |
|------|-------|----------|--------|-------------------|
| Compile press list (30 outlets + YouTubers) | HYPE | Month 10 | [ ] | Spreadsheet with contact emails, outlet focus, audience size |
| Write press release (launch announcement) | HYPE | Month 11 | [ ] | 1-page PDF, includes hook, release date, trailer link, key art |
| Generate press kit (screenshots, logos, fact sheet) | HYPE + PIXEL | Month 11 | [ ] | Hosted on public URL (presskit.upfrontgame.com or itch.io page) |
| Send press keys 2 weeks before launch | HYPE | Month 12 Week 2 | [ ] | Keys sent via Keymailer or email, embargo date specified (launch day) |
| Set up social media accounts (Twitter, Discord) | HYPE | Month 10 | [ ] | Twitter handle claimed, Discord server live, bio links to Steam page |
| Post announcement trailer on social media | HYPE | Month 11 | [ ] | Trailer posted with launch date, pinned on Twitter, shared in relevant subreddits |
| Reach out to streamers (optional) | HYPE | Month 11 | [ ] | 5-10 streamers contacted with keys, no obligation to stream |
| Schedule Reddit AMA (optional) | HYPE | Month 12 Week 3 | [ ] | AMA scheduled on r/gamedev or r/Games, 3 days before launch |

**Press Outreach Philosophy**: Target outlets that cover management sims (PC Gamer, Rock Paper Shotgun, Polygon indie coverage) and advertising industry media (AdAge, Campaign, The Drum). The latter is untapped — no other game has pitched to advertising press. This is free earned media.

#### 4.3 Age Ratings

| Task | Owner | Deadline | Status | Definition of Done |
|------|-------|----------|--------|-------------------|
| Decide if age rating is required for launch | SHIP | Month 9 | [ ] | Decision made based on target markets (ESRB optional for digital-only PC launch) |
| Submit to IARC (if pursuing console ports) | SHIP | Month 10 | [ ] | IARC questionnaire completed, rating certificate received |
| Display rating on store page (if applicable) | SHIP | Month 11 | [ ] | Rating icon visible on Steam page |

**Age Rating Notes**: UPFRONT has no violence, sexual content, or explicit language. Expected rating: E (Everyone) or PEGI 3. For PC-only Steam launch, ESRB rating is optional. Required for console ports (Switch, Xbox, PlayStation). IARC is free and covers most regions.

**Content Warnings**: Mild themes (workplace stress, client conflict, alcohol references in 2000s office setting). No content likely to trigger rating escalation.

---

### 1.6 Phase 5: Gold Master (Week of Launch)

**Goal**: Lock the final build. No more code changes except critical hotfixes.

| Task | Owner | Deadline | Status | Definition of Done |
|------|-------|----------|--------|-------------------|
| Code freeze (feature complete) | BYTE | Launch - 10 days | [ ] | No new features, only critical bug fixes allowed |
| Build Release Candidate 1 (RC1) | BYTE | Launch - 9 days | [ ] | Build tagged in git as `v1.0.0-rc1`, uploaded to staging depot |
| Full QA pass on RC1 (all platforms) | CRASH | Launch - 7 days | [ ] | QA report: critical bugs listed, minor bugs deferred |
| Fix critical bugs from RC1 | BYTE | Launch - 6 days | [ ] | Crash bugs, save corruption, soft locks fixed |
| Build Release Candidate 2 (RC2) | BYTE | Launch - 5 days | [ ] | Build tagged as `v1.0.0-rc2`, uploaded to staging |
| Full QA pass on RC2 | CRASH | Launch - 4 days | [ ] | Zero critical bugs, minor bugs documented for post-launch patch |
| Declare Gold Master (GM) | SHIP + CRASH | Launch - 3 days | [ ] | RC2 promoted to GM, tagged as `v1.0.0` in git |
| Upload GM to Steam default depot | SHIP | Launch - 3 days | [ ] | Build live on Steam "default" branch (not public yet) |
| Test GM on clean machines (Win/Mac/Linux) | CRASH | Launch - 2 days | [ ] | Install from Steam, play 30 minutes, verify achievements, cloud saves |
| Prepare Day 1 patch (if needed) | BYTE | Launch - 1 day | [ ] | If minor bugs found, build 1.0.1 ready to deploy post-launch |
| Write launch day runbook | SHIP | Launch - 2 days | [ ] | Hour-by-hour checklist for launch day (see section 6) |

**Gold Master Philosophy**: The GM build must be shippable. If a critical bug is found after GM, we have two options:
1. Delay launch (only if bug is game-breaking: crashes on startup, save corruption)
2. Ship GM, deploy Day 1 patch within 24 hours

Option 2 is preferable unless the bug prevents players from launching the game.

---

### 1.7 Phase 6: Launch Day (Day 0)

**Goal**: Monitor launch, respond to issues, communicate with players.

See section 6 for hour-by-hour timeline.

---

### 1.8 Phase 7: Post-Launch (Weeks 1-4)

**Goal**: Stabilize the game, patch critical bugs, support players.

| Task | Owner | Deadline | Status | Definition of Done |
|------|-------|----------|--------|-------------------|
| Monitor crash reports (Unity Cloud Diagnostics) | BYTE | Daily, Week 1 | [ ] | Check crash dashboard every 6 hours, triage critical crashes |
| Monitor Steam reviews | HYPE + SHIP | Daily, Week 1 | [ ] | Read all reviews, flag bug reports, respond to negative reviews if actionable |
| Monitor Discord / Reddit for bug reports | HYPE + CRASH | Daily, Week 1 | [ ] | Compile bug list in shared doc, prioritize by severity |
| Deploy Patch 1.0.1 (critical bugs only) | BYTE | Week 1 | [ ] | Patch deployed within 48 hours of launch if critical bugs found |
| Deploy Patch 1.0.2 (minor bugs + balance) | BYTE | Week 2-3 | [ ] | Address most-reported minor bugs, tweak economy balance if needed |
| Publish post-launch roadmap (optional) | HYPE | Week 2 | [ ] | Blog post on Steam: upcoming features, patch schedule, thank you to players |
| Analyze launch metrics (sales, CCU, reviews) | SHIP + HYPE | Week 1 | [ ] | Metrics compiled in shared doc, inform post-launch decisions |

**Post-Launch Support Philosophy**: The first week is critical. Players expect rapid response to bugs. A game that crashes on launch and is not patched within 24 hours will be review-bombed. We must be ready to hotfix.

---

## 2. BUILD PIPELINE DOCUMENTATION

### 2.1 Build Pipeline Overview

**Primary Tool**: Unity Cloud Build (Months 1-6) → Jenkins (Months 7-12)

**Why the transition?** Unity Cloud Build is easy to set up but slow (15+ minute builds). Jenkins on a dedicated build machine is faster (5-10 minute builds) and gives us full control over build scripts. The transition happens at Alpha (Month 7) when build frequency increases.

---

### 2.2 Build Types

| Build Type | Trigger | Optimization | Platforms | Upload Destination | Frequency |
|------------|---------|--------------|-----------|-------------------|-----------|
| **Dev Build** | Manual (local) | None | Windows only | Local disk | On-demand |
| **Playtest Build** | Auto (commit to `develop`) | Debug symbols | Win/Mac/Linux | Itch.io private page | Nightly |
| **Steam Beta Build** | Manual (git tag) | Medium | Win/Mac/Linux | Steam beta depot | Weekly during beta |
| **Release Build (GM)** | Manual (git tag) | Full | Win/Mac/Linux | Steam default depot | Once (launch) |

---

### 2.3 Build Script Example (Jenkins)

This is the master build script. It builds all platforms, tags the build, and uploads to Steam.

```bash
#!/bin/bash
# UPFRONT Build Script v1.0
# Runs on Jenkins build server

set -e  # Exit on error

# Configuration
PROJECT_PATH="/Users/buildmachine/upfront-project"
UNITY_PATH="/Applications/Unity/Hub/Editor/2023.2.10f1/Unity.app/Contents/MacOS/Unity"
BUILD_OUTPUT="/Users/buildmachine/builds"
STEAM_USER="${STEAM_BUILD_USER}"  # From Jenkins credentials
STEAM_PASS="${STEAM_BUILD_PASS}"  # From Jenkins credentials
STEAMCMD_PATH="/usr/local/bin/steamcmd"

# Get version from git tag
VERSION=$(git describe --tags --abbrev=0)
echo "Building version: $VERSION"

# Clean previous builds
rm -rf $BUILD_OUTPUT/*

# Build Windows
echo "Building Windows..."
$UNITY_PATH -quit -batchmode -projectPath $PROJECT_PATH \
  -buildWindows64Player "$BUILD_OUTPUT/UPFRONT_${VERSION}_Win64/UPFRONT.exe" \
  -logFile "$BUILD_OUTPUT/build_win.log"

# Build macOS
echo "Building macOS..."
$UNITY_PATH -quit -batchmode -projectPath $PROJECT_PATH \
  -buildOSXUniversalPlayer "$BUILD_OUTPUT/UPFRONT_${VERSION}_macOS.app" \
  -logFile "$BUILD_OUTPUT/build_mac.log"

# Build Linux
echo "Building Linux..."
$UNITY_PATH -quit -batchmode -projectPath $PROJECT_PATH \
  -buildLinuxUniversalPlayer "$BUILD_OUTPUT/UPFRONT_${VERSION}_Linux/UPFRONT.x86_64" \
  -logFile "$BUILD_OUTPUT/build_linux.log"

# Check for build errors
if grep -q "Error" $BUILD_OUTPUT/*.log; then
  echo "Build failed! Check logs."
  exit 1
fi

echo "All builds completed successfully."

# Upload to Steam (if release build)
if [[ $VERSION == *"rc"* ]] || [[ $VERSION == "v1.0.0" ]]; then
  echo "Uploading to Steam..."
  $STEAMCMD_PATH +login $STEAM_USER $STEAM_PASS \
    +run_app_build ../steam/app_build_upfront.vdf \
    +quit
  echo "Steam upload complete."
fi

echo "Build pipeline finished."
```

**What this script does**:
1. Reads version from git tag (e.g., `v1.0.0-rc1`)
2. Builds Windows, macOS, Linux in sequence
3. Checks build logs for errors
4. If this is a release candidate or gold master, uploads to Steam via SteamCMD
5. Exits with error code if any step fails

**Build time**: Approximately 8-10 minutes on a modern Mac Mini M2 (8-core, 16GB RAM, SSD).

---

### 2.4 Testing the Build Pipeline

Before launch, test the full pipeline end-to-end:

| Test Case | Expected Result | Status |
|-----------|----------------|--------|
| Trigger build on commit to `develop` | Nightly build generated, uploaded to itch.io | [ ] |
| Trigger build on git tag `v0.9.0-beta` | Beta build generated, uploaded to Steam beta depot | [ ] |
| Trigger build on git tag `v1.0.0` | GM build generated, uploaded to Steam default depot | [ ] |
| Build fails due to compilation error | Build marked as failed, team notified via Slack/Discord webhook | [ ] |
| Build succeeds but crashes on launch | QA catches this before GM, build rejected | [ ] |

**Definition of Done**: All test cases pass. Any team member can trigger a build by pushing a git tag. No manual steps required.

---

### 2.5 Clean Machine Testing

Before declaring Gold Master, test the build on clean machines (no dev tools, no Unity installed).

**Test Machines**:
- Windows 10 laptop (minimum spec: i5-4460, 4GB RAM, integrated graphics)
- macOS Ventura (Intel Mac OR M1/M2 Mac)
- Linux (Ubuntu 22.04 LTS, Steam client installed)
- Steam Deck (optional, but highly recommended)

**Test Procedure**:
1. Install Steam client
2. Download UPFRONT from Steam (staging depot)
3. Launch game via Steam
4. Play for 30 minutes: complete 1 full campaign, test save/load, unlock 1 achievement
5. Exit game, verify cloud save syncs
6. Launch again, verify save restores

**Pass Criteria**:
- Game launches without errors
- No crashes during 30-minute session
- Achievements unlock
- Cloud saves sync
- Text is readable at native resolution
- Performance is 60 FPS (PC) or 30 FPS (Deck)

**If any test fails**: Build is not Gold Master. Fix the issue, build RC3, re-test.

---

## 3. PLATFORM CONFIGURATION CHECKLIST

### 3.1 Steamworks Configuration

**App ID**: (Register during Month 9, record here: __________)

**Depots**:
| Depot ID | Platform | Size (approx) | Notes |
|----------|----------|---------------|-------|
| 100001 | Windows | 1.2 GB | Executable + assets |
| 100002 | macOS | 1.3 GB | Universal binary (Intel + Apple Silicon) |
| 100003 | Linux | 1.2 GB | Tested on Ubuntu 22.04 |
| 100004 | Shared assets | 800 MB | Common files (UI textures, audio, JSON configs) |

**Launch Options**: None required. Game auto-detects resolution and graphics settings.

**Steam Cloud**:
- Quota: 5 MB
- File patterns: `saves/*.json`, `settings.json`
- Auto-sync: Enabled on game exit and launch

**Steam Input**:
- Controller configuration: Use default "Gamepad with Mouse Joystick" template
- Custom bindings: Not required (game has native controller support)

**DLC** (future):
- Plan for 1-2 content expansions post-launch (Agency Crisis system, new client archetypes)
- DLC app IDs: Register when ready, not at launch

---

### 3.2 Achievement Design & Implementation

**Total Achievements**: 35 (30 visible, 5 hidden)

**Achievement Categories**:
1. **Story Milestones** (10 achievements) — First campaign, first year, first Super Bowl, year 5, etc.
2. **Mastery** (8 achievements) — Win Cannes Grand Prix, Legendary audience score, 5-star client trust, etc.
3. **Discovery** (7 achievements) — Walk away from client, Meltdown team produces hit, Fire a high-Ego creative, etc.
4. **Funny/Easter Egg** (5 achievements, hidden) — Create 10 ads with chimps, Name agency "Mad Men", etc.
5. **Progression** (5 achievements) — Unlock Tier 5 clients, Hire 16 creatives, Complete 100 campaigns, etc.

**Achievement Rarity Targets**:
- 10 achievements should be earned by 80%+ of players (easy story milestones)
- 15 achievements should be earned by 30-50% of players (moderate skill)
- 10 achievements should be earned by 5-15% of players (hard mastery or rare discovery)

**Implementation Checklist**:
| Achievement ID | Name | Trigger Event | Tested | Status |
|----------------|------|---------------|--------|--------|
| ACH_FIRST_CAMPAIGN | "Getting My Feet Wet" | Complete first campaign | [ ] | [ ] |
| ACH_FIRST_SUPERBOWL | "The Big Game" | Air first Super Bowl ad | [ ] | [ ] |
| ACH_WALK_AWAY | "Artistic Integrity" | Walk away from Gauntlet | [ ] | [ ] |
| ACH_LEGENDARY | "Legendary" | Audience Score 91-100 | [ ] | [ ] |
| ACH_CANNES_GRANDPRIX | "Best in Show" | Win Cannes Grand Prix | [ ] | [ ] |
| (30 more...) | | | [ ] | [ ] |

**Testing Protocol**:
- CRASH tests all achievements in dev build
- Each achievement must be unlockable in normal gameplay (no debug commands required)
- Achievements fire immediately when condition is met (no delayed triggers)

---

### 3.3 Trading Cards (Optional Post-Launch)

**Status**: Not prioritized for launch. Can be added post-launch once player base is established.

**If pursued**:
- Design 8 card designs (agency office scenes, creatives, clients, Super Bowl moments)
- Submit to Steam for approval (2-4 week review)
- Requires game to have sufficient playtime data (avg 2+ hours per player)

---

## 4. ROLLBACK & HOTFIX PROCEDURES

### 4.1 Rollback Plan

**Scenario**: A critical bug is discovered after launch (e.g., save corruption, crash on Year 2 transition).

**Rollback Procedure**:

1. **Assess Severity** (Owner: SHIP + BYTE, Time: 15 minutes)
   - Is the bug game-breaking? (crashes, prevents progress, deletes saves)
   - How many players are affected? (check crash reports, Steam reviews, Discord)
   - Can we fix it quickly (within 2 hours)?

2. **Decision Point**:
   - If fixable in 2 hours: Deploy hotfix (see section 4.2)
   - If not fixable quickly: Rollback to previous stable build

3. **Rollback Execution** (Owner: SHIP, Time: 30 minutes):
   - Log into Steamworks admin
   - Navigate to Builds > Set Build Live
   - Select previous stable build (e.g., `v0.9.9-beta` if `v1.0.0` is broken)
   - Set as live on "default" branch
   - Update "News" on Steam store: "We have rolled back to a stable build while we fix a critical issue. Expect a patch within 24 hours."
   - Post update on Discord, Twitter

4. **Fix & Re-Deploy** (Owner: BYTE, Time: 2-24 hours):
   - Fix the bug in a branch
   - Build new release (e.g., `v1.0.1`)
   - Test on clean machine (fast QA pass, 1 hour)
   - Upload to Steam
   - Set as live
   - Update "News" on Steam: "Patch 1.0.1 is now live. This fixes [describe bug]. Thank you for your patience."

**Rollback Checklist**:
| Step | Owner | Time | Status |
|------|-------|------|--------|
| Assess bug severity | SHIP + BYTE | 15 min | [ ] |
| Decide: hotfix or rollback | SHIP | 5 min | [ ] |
| Execute rollback on Steam | SHIP | 10 min | [ ] |
| Post communication to players | HYPE | 10 min | [ ] |
| Fix bug and build v1.0.1 | BYTE | 2-24 hours | [ ] |
| QA pass on v1.0.1 | CRASH | 1 hour | [ ] |
| Deploy v1.0.1 to Steam | SHIP | 10 min | [ ] |
| Post patch notes | HYPE | 10 min | [ ] |

**Worst-Case Timeline**: Rollback within 30 minutes of decision. Patch deployed within 24 hours.

---

### 4.2 Hotfix Procedure

**Scenario**: A non-critical bug is found post-launch (e.g., UI typo, minor balance issue, broken achievement).

**Hotfix Procedure**:

1. **Triage** (Owner: SHIP, Time: 15 minutes)
   - Is this a hotfix (can wait 48 hours) or an emergency (needs immediate fix)?
   - If emergency: Follow rollback procedure

2. **Schedule Hotfix Window** (Owner: SHIP)
   - Hotfixes deploy during low-traffic hours: 2-6 AM PST
   - Announce in Discord/Steam: "Patch 1.0.1 will deploy at 3 AM PST. Expect brief downtime."

3. **Develop Fix** (Owner: BYTE, Time: 1-4 hours)
   - Fix bug in `hotfix/v1.0.1` branch
   - Build and test locally
   - Merge to `main` via pull request (code review required)

4. **Build Hotfix** (Owner: BYTE, Time: 15 minutes)
   - Tag commit as `v1.0.1`
   - Trigger build pipeline
   - Upload to Steam staging depot

5. **Fast QA Pass** (Owner: CRASH, Time: 30 minutes)
   - Test the specific bug fix
   - Smoke test: launch game, load save, play 5 minutes, exit
   - If QA passes: approve for deploy

6. **Deploy to Live** (Owner: SHIP, Time: 10 minutes)
   - Set build live on Steam "default" branch
   - Post patch notes on Steam News, Discord, Twitter

**Hotfix Checklist**:
| Step | Owner | Time | Status |
|------|-------|------|--------|
| Triage bug severity | SHIP | 15 min | [ ] |
| Schedule hotfix window | SHIP | 5 min | [ ] |
| Develop fix | BYTE | 1-4 hours | [ ] |
| Build hotfix | BYTE | 15 min | [ ] |
| QA pass | CRASH | 30 min | [ ] |
| Deploy to Steam | SHIP | 10 min | [ ] |
| Post patch notes | HYPE | 10 min | [ ] |

**Target Timeline**: Hotfix deployed within 48 hours of discovery for non-critical bugs, within 2 hours for critical bugs.

---

### 4.3 Emergency Contacts

**Launch Day On-Call Roster**:

| Role | Name | Contact | Backup |
|------|------|---------|--------|
| Release Manager | SHIP | (phone) | BYTE |
| Lead Programmer | BYTE | (phone) | (backup dev) |
| QA Lead | CRASH | (phone) | (backup QA) |
| Marketing | HYPE | (phone) | (backup PR) |

**Escalation Path**:
1. Bug discovered (by player, QA, or monitoring tool)
2. SHIP triages within 15 minutes
3. If critical: SHIP calls BYTE immediately
4. BYTE assesses fix time
5. If rollback needed: SHIP executes rollback, HYPE posts communication
6. If hotfix possible: BYTE develops fix, CRASH tests, SHIP deploys

**Communication Templates** (pre-written):

**Rollback Announcement**:
> "We have identified a critical issue in the launch build and are rolling back to a stable version while we fix it. Your saves are safe. We will deploy a patch within 24 hours. Thank you for your patience."

**Hotfix Announcement**:
> "Patch 1.0.1 is now live. This fixes [bug description]. If you encounter any issues, please report them in our Discord or Steam forums. Thank you!"

---

## 5. LAUNCH DAY TIMELINE

### 5.1 Overview

Launch day is the most critical 24 hours of the project. The timeline below is hour-by-hour from T-12 hours (midnight before launch) to T+12 hours (noon after launch).

**Launch Time**: 10 AM PST (chosen to align with US West Coast working hours, when Steam traffic is high)

---

### 5.2 Launch Day Checklist

#### T-12 Hours (10 PM PST, Day -1)

| Task | Owner | Status |
|------|-------|--------|
| Verify Gold Master is live on Steam default depot | SHIP | [ ] |
| Set release date/time in Steamworks (10 AM PST) | SHIP | [ ] |
| Pre-write launch day tweets, Discord posts | HYPE | [ ] |
| Confirm press embargo lifts at 10 AM PST | HYPE | [ ] |
| Verify Discord server is ready (welcome message, rules, channels) | HYPE | [ ] |
| Test purchase flow on Steam (buy game, refund, rebuy) | SHIP | [ ] |
| Set up monitoring dashboard (Steam analytics, Unity crash reports) | BYTE | [ ] |
| Confirm team is on-call for next 24 hours | SHIP | [ ] |

#### T-2 Hours (8 AM PST, Launch Day)

| Task | Owner | Status |
|------|-------|--------|
| Final check: GM build is live, price is correct, store page is public | SHIP | [ ] |
| Pre-launch tweet: "Going live in 2 hours!" | HYPE | [ ] |
| Open monitoring dashboard in war room (shared screen) | BYTE | [ ] |
| Prepare Day 1 patch (if any minor bugs need fixing) | BYTE | [ ] |

#### T-0 (10 AM PST, Launch Day)

| Task | Owner | Status |
|------|-------|--------|
| GAME GOES LIVE ON STEAM | SHIP | [ ] |
| Post launch tweet: "UPFRONT is now live on Steam!" + trailer link | HYPE | [ ] |
| Post launch announcement on Discord | HYPE | [ ] |
| Post on relevant subreddits (r/gamedev, r/IndieGaming, r/tycoon) | HYPE | [ ] |
| Monitor Steam reviews (check every 30 minutes for first 4 hours) | HYPE | [ ] |
| Monitor crash reports (check every 15 minutes for first 2 hours) | BYTE | [ ] |
| Monitor Discord for bug reports | CRASH | [ ] |

#### T+1 Hour (11 AM PST)

| Task | Owner | Status |
|------|-------|--------|
| Check Steam analytics: how many purchases, how many refunds | SHIP | [ ] |
| Check concurrent players (CCU) | SHIP | [ ] |
| Triage any critical bugs reported in first hour | SHIP + BYTE | [ ] |
| Respond to first wave of Steam reviews (thank positive, acknowledge negative) | HYPE | [ ] |

#### T+2 Hours (12 PM PST)

| Task | Owner | Status |
|------|-------|--------|
| Lunch break (in shifts, someone always monitoring) | ALL | [ ] |
| Check crash report trends: any patterns? | BYTE | [ ] |
| If critical bug found: Begin hotfix procedure (see section 4.2) | BYTE | [ ] |

#### T+4 Hours (2 PM PST)

| Task | Owner | Status |
|------|-------|--------|
| Post "4 hours in" update on Discord: CCU, review sentiment, thank you | HYPE | [ ] |
| Compile bug list from Discord, Steam forums, Reddit | CRASH | [ ] |
| Prioritize bugs for Day 1 patch (if not deploying emergency hotfix) | SHIP + BYTE | [ ] |

#### T+8 Hours (6 PM PST)

| Task | Owner | Status |
|------|-------|--------|
| End of core work day, but monitoring continues | ALL | [ ] |
| Check analytics: total sales, CCU peak, review score | SHIP | [ ] |
| Post end-of-day update on Discord: "Thank you for playing!" | HYPE | [ ] |
| If Day 1 patch is needed, schedule for T+24 hours (next morning) | SHIP | [ ] |

#### T+12 Hours (10 PM PST)

| Task | Owner | Status |
|------|-------|--------|
| Final check of crash reports before sleep | BYTE | [ ] |
| Set up overnight monitoring alerts (crash spike, review bomb) | SHIP | [ ] |
| Go to sleep (except one person on-call for emergencies) | ALL | [ ] |

#### T+24 Hours (10 AM PST, Day +1)

| Task | Owner | Status |
|------|-------|--------|
| Morning debrief: What went well? What went wrong? | ALL | [ ] |
| Deploy Day 1 patch if ready (see section 4.2) | BYTE + SHIP | [ ] |
| Post 24-hour update on Steam News: sales milestone, thank you, patch notes | HYPE | [ ] |
| Respond to all Steam reviews from launch day | HYPE | [ ] |

---

### 5.3 Launch Day "War Room" Setup

**Physical Setup** (if team is co-located):
- One room with large monitor showing:
  - Steam analytics dashboard (sales, CCU, refunds)
  - Unity Cloud Diagnostics (crash reports)
  - Discord server (bug reports channel)
  - Steam reviews (live feed)
- Whiteboard for tracking critical bugs
- Coffee. Lots of coffee.

**Remote Setup** (if team is distributed):
- Shared Zoom/Discord call for 12 hours (10 AM - 10 PM PST)
- Shared Google Doc for bug triage
- Slack/Discord bot posting alerts for:
  - New crash reports
  - Negative Steam reviews
  - Sales milestones (100, 500, 1000 copies)

---

### 5.4 Launch Day Metrics to Watch

| Metric | Tool | Check Frequency | Red Flag Threshold |
|--------|------|-----------------|-------------------|
| **Crash Rate** | Unity Cloud Diagnostics | Every 15 min (first 2 hours) | > 5% of sessions |
| **Concurrent Players (CCU)** | Steam analytics | Every 30 min | N/A (track for baseline) |
| **Refund Rate** | Steam partner dashboard | Every 1 hour | > 10% of purchases |
| **Review Score** | Steam store page | Every 30 min | < 70% positive |
| **Critical Bug Reports** | Discord + Steam forums | Every 15 min | > 5 reports of same bug |

**Red Flag Protocol**:
- If crash rate > 5%: Emergency hotfix within 2 hours
- If refund rate > 10%: Investigate cause (broken feature? misleading marketing?)
- If review score < 70%: Read negative reviews, identify common complaints
- If critical bug is widespread: Rollback or emergency hotfix

---

### 5.5 Launch Day Success Criteria

**Minimum Success** (we can call this a successful launch):
- Game is purchasable and playable on Steam
- Crash rate < 5%
- Refund rate < 10%
- Review score > 70% positive
- No game-breaking bugs found in first 24 hours
- CCU peak > 50 players (for a small indie launch)

**Ideal Success**:
- Review score > 85% positive
- CCU peak > 200 players
- Front page of Steam "New & Trending"
- At least 3 positive reviews from press/YouTubers
- Discord server has 100+ members by end of day

**If we hit Ideal Success**: Celebrate. Then get back to work on Day 1 patch.

---

## 6. POST-LAUNCH MONITORING & SUPPORT

### 6.1 Week 1 Post-Launch Checklist

| Task | Owner | Frequency | Status |
|------|-------|-----------|--------|
| Monitor crash reports | BYTE | Every 6 hours | [ ] |
| Monitor Steam reviews | HYPE | Daily | [ ] |
| Monitor Discord for bug reports | CRASH | Every 4 hours | [ ] |
| Compile bug list in shared doc | CRASH | Daily | [ ] |
| Triage bugs by severity (critical/high/medium/low) | SHIP | Daily | [ ] |
| Deploy Patch 1.0.1 (if critical bugs found) | BYTE + SHIP | Within 48 hours | [ ] |
| Respond to negative Steam reviews (if actionable) | HYPE | Daily | [ ] |
| Post daily update on Discord (thank players, share metrics) | HYPE | Daily | [ ] |

---

### 6.2 Patch Pipeline

**Patch Cadence**:
- **Week 1**: Patch 1.0.1 (critical bugs only), deployed within 48 hours of launch
- **Week 2-3**: Patch 1.0.2 (minor bugs + balance tweaks), deployed 10-14 days post-launch
- **Month 2**: Patch 1.1.0 (QoL improvements, based on player feedback), deployed 6-8 weeks post-launch

**Patch Deployment Process**:
1. CRASH compiles bug list from all sources (Discord, Steam forums, reviews, crash reports)
2. SHIP triages bugs by severity
3. BYTE fixes critical bugs first, then high-priority, then medium
4. BYTE builds patch, tags as `v1.0.X`
5. CRASH does QA pass (smoke test + regression test on reported bugs)
6. SHIP deploys to Steam
7. HYPE posts patch notes on Steam News, Discord, Twitter

**Patch Notes Template**:

```
UPFRONT — Patch 1.0.1

FIXES:
- Fixed crash when loading save from Year 3+
- Fixed achievement "Artistic Integrity" not unlocking when walking away from client
- Fixed UI scaling issue on ultrawide monitors (21:9)

BALANCE:
- Reduced salary costs for junior creatives by 10%
- Increased Client Trust gain from accepting notes (+5 -> +7)

KNOWN ISSUES:
- Minor visual glitch in Super Bowl broadcast (cosmetic, will fix in 1.0.2)

Thank you for playing and reporting bugs!
```

---

### 6.3 Analytics & Metrics

**What to Track** (post-launch):

| Metric | Tool | Purpose |
|--------|------|---------|
| **Total Sales** | Steam partner dashboard | Revenue, success measurement |
| **Daily Active Users (DAU)** | Steam analytics | Player retention |
| **Average Session Length** | Unity Analytics (if integrated) | Engagement, pacing validation |
| **Completion Rate** (Year 1, Year 5) | Unity Analytics | How many players finish the game |
| **Achievement Unlock Rates** | Steam analytics | Difficulty tuning, content discovery |
| **Crash Rate** | Unity Cloud Diagnostics | Stability |
| **Refund Rate** | Steam partner dashboard | Quality/marketing alignment |
| **Review Score** | Steam store page | Player sentiment |

**Monthly Analytics Review** (Owner: SHIP + HYPE):
- Compile metrics into report
- Identify trends (e.g., "players are refunding after 90 minutes — is there a difficulty spike?")
- Inform roadmap decisions (e.g., "only 20% of players reach Year 5 — do we need better onboarding?")

---

### 6.4 Player Support

**Support Channels**:
1. **Steam Forums** — Official support, CRASH monitors daily
2. **Discord Server** — Community-driven support, HYPE moderates
3. **Email** — support@upfrontgame.com (if registered), HYPE responds within 48 hours

**Common Support Issues** (prepare canned responses):

| Issue | Canned Response |
|-------|----------------|
| "Game won't launch" | "Please verify game files via Steam (right-click > Properties > Local Files > Verify Integrity). If issue persists, post your log file." |
| "Save file corrupted" | "We are sorry to hear this. Please send us your save file (location: [path]). We will investigate and may be able to recover it." |
| "Achievement didn't unlock" | "Achievements sometimes delay. Exit and re-launch the game. If still not unlocking, please report in Discord with steps to reproduce." |
| "How do I win the Super Bowl?" | "The Super Bowl unlocks at Reputation 46+. Focus on building client trust and winning awards to increase your reputation." |

---

## 7. AGE RATINGS & REGIONAL COMPLIANCE

### 7.1 Age Rating Strategy

**UPFRONT Content Summary**:
- No violence, sexual content, explicit language, drug use, or gambling
- Themes: Workplace dynamics, creative conflict, client negotiation, advertising industry satire
- Alcohol references: Implied (2000s office culture, "drinks after work" dialogue), not depicted
- Expected rating: **E (Everyone)** or **PEGI 3**

**Rating Submission Strategy**:
- **PC Launch (Steam)**: ESRB rating optional. Not required for digital distribution in US/EU.
- **Switch Port**: ESRB/PEGI required. Use IARC (International Age Rating Coalition) for fast, free rating.
- **Retail Release (if pursued)**: ESRB/PEGI required.

---

### 7.2 IARC Submission Process

**What is IARC?**
- International Age Rating Coalition
- One questionnaire generates ratings for ESRB (US), PEGI (EU), USK (Germany), ClassInd (Brazil), etc.
- Free, results in 24-48 hours

**Submission Checklist**:
| Step | Owner | Deadline | Status |
|------|-------|----------|--------|
| Create IARC account | SHIP | Month 10 | [ ] |
| Complete IARC questionnaire | SHIP | Month 10 | [ ] |
| Upload gameplay video (5-10 minutes) | SHIP | Month 10 | [ ] |
| Submit for review | SHIP | Month 10 | [ ] |
| Receive rating certificate | SHIP | Month 10 (24-48h after submission) | [ ] |
| Display rating on Steam page (if console port) | SHIP | Month 11 | [ ] |

**IARC Questionnaire Key Answers** (draft):
- Violence: None
- Sexual content: None
- Language: Mild (workplace banter, no profanity)
- Controlled substances: References only (alcohol mentioned, not depicted)
- Gambling: None
- Online interactions: None (single-player only)

Expected IARC Result: **E (Everyone) / PEGI 3**

---

### 7.3 Regional Compliance Notes

**European Union (GDPR)**:
- UPFRONT does not collect personal data (no account system, no telemetry beyond Steam analytics)
- No GDPR compliance required beyond standard Steam privacy policy

**China**:
- Not targeting Chinese market at launch (requires government approval, localization, content审查)
- Consider for post-launch expansion if PC sales exceed 50K units

**Australia**:
- No additional rating required (Steam handles regional restrictions)
- IARC rating sufficient

**Germany (USK)**:
- IARC generates USK rating automatically
- No additional submission required

---

## 8. LAUNCH DAY COMMUNICATION PLAN

### 8.1 Pre-Written Communication Templates

#### Launch Announcement (Twitter/Discord)

```
UPFRONT is now live on Steam!

Run a 2000s ad agency. Manage creative egos. Chase the Super Bowl. Discover that the best ad you ever made is the one the client killed.

"Game Dev Tycoon meets Mad Men"

🎮 Play now: [Steam link]
🎬 Trailer: [YouTube link]

#indiegame #gamedev #managementsim
```

#### Press Release (Email to Press List)

```
Subject: UPFRONT — Ad Agency Management Sim — Now Available on Steam

FOR IMMEDIATE RELEASE

[Date]

UPFRONT, a management simulation game about running a 2000s advertising agency, launched today on Steam for PC, Mac, and Linux.

Players manage an ad agency, assembling creative teams, navigating client approval processes, and chasing the ultimate prize: a Super Bowl ad slot. The game features the "Approval Gauntlet" — a negotiation system where players defend creative work against risk-averse clients.

Key Features:
- Manage creative teams with distinct personalities, stats, and egos
- Navigate the Approval Gauntlet: present concepts, push back on client notes, compromise or walk away
- Chase the Super Bowl: the annual climax event where your ad airs for 100 million simulated viewers
- Build your agency's reputation through awards, client relationships, and bold creative choices

"UPFRONT is the game the advertising industry has been waiting to play about itself," said [Your Name/Studio Name]. "It captures the tension between art and commerce that every creative person has felt."

Availability:
- Platform: PC (Windows, Mac, Linux) via Steam
- Price: $[X]
- Launch discount: [X]% off for first week

Media Contact: [Email]
Press Kit: [Link to presskit()]

[Studio Bio]
```

#### Day 1 Patch Announcement (Steam News)

```
UPFRONT — Patch 1.0.1 Now Live

Thank you to everyone who played UPFRONT on launch day! Your feedback has been invaluable.

Patch 1.0.1 is now live with the following fixes:

FIXES:
- [List critical bugs fixed]

BALANCE:
- [List balance tweaks]

KNOWN ISSUES:
- [List known minor bugs, to be fixed in 1.0.2]

If you encounter any issues, please report them in our Discord server or Steam forums. We are monitoring both closely.

Thank you for your patience and support!

— The UPFRONT Team
```

---

### 8.2 Social Media Schedule (Launch Week)

| Day | Time | Platform | Content |
|-----|------|----------|---------|
| **Launch Day** | 10 AM PST | Twitter, Discord, Reddit | Launch announcement + trailer |
| Launch Day | 2 PM PST | Twitter | "4 hours in" update: CCU, thank you to players |
| Launch Day | 8 PM PST | Discord | End-of-day update: sales milestone, top bug reports |
| **Day +1** | 10 AM PST | Twitter, Discord | 24-hour update: patch notes (if deployed), sales milestone |
| Day +2 | 12 PM PST | Twitter | Player testimonial (quote from positive review) |
| Day +3 | 12 PM PST | Twitter | Gameplay GIF (Gauntlet or Super Bowl moment) |
| Day +4 | 12 PM PST | Twitter | Community highlight (funny agency name, creative team composition) |
| Day +5 | 10 AM PST | Discord | Weekly wrap-up: sales, review score, upcoming patch roadmap |

---

### 8.3 Press Outreach Timeline

| Week | Action | Owner | Status |
|------|--------|-------|--------|
| **Launch - 4 weeks** | Compile press list (30 outlets + YouTubers) | HYPE | [ ] |
| Launch - 3 weeks | Send email pitch to press list | HYPE | [ ] |
| Launch - 2 weeks | Send press keys via Keymailer | HYPE | [ ] |
| Launch - 1 week | Follow-up email to press who requested keys | HYPE | [ ] |
| **Launch Day** | Monitor press coverage (set up Google Alerts for "UPFRONT game") | HYPE | [ ] |
| Launch + 1 week | Send thank-you email to press who covered the game | HYPE | [ ] |

**Press List Categories**:
1. **Gaming Press** (20 outlets): PC Gamer, Rock Paper Shotgun, Polygon, IGN, Eurogamer, etc.
2. **YouTubers/Streamers** (10 creators): Splattercat, Wanderbots, Retromation, Northernlion, etc.
3. **Advertising Industry Media** (5 outlets): AdAge, Campaign, The Drum, Adweek, Creative Review
4. **Reddit AMAs** (optional): r/Games, r/gamedev, r/tycoon

---

## 9. RISK REGISTER & CONTINGENCY PLANS

### 9.1 Critical Risks

| Risk | Likelihood | Impact | Mitigation | Contingency |
|------|-----------|--------|------------|-------------|
| **Critical bug in GM build** | Medium | CRITICAL | QA pass on RC1 and RC2, clean machine testing | Rollback to previous build, deploy hotfix within 24 hours |
| **Steam payment processing fails at launch** | Low | CRITICAL | Test purchase flow 24 hours before launch | Contact Steam support emergency line, delay launch if not resolved |
| **Press embargo broken early** | Low | Medium | Clearly communicate embargo date in press email | No real harm; press coverage is press coverage |
| **Review bomb (negative coordinated reviews)** | Low | High | Monitor reviews hourly, respond professionally | Do not engage with trolls; post statement acknowledging issues |
| **Competitor launches similar game same day** | Very Low | Medium | Cannot mitigate | Double down on unique selling points (Gauntlet, Super Bowl) in marketing |
| **Key team member unavailable on launch day** | Low | High | Establish backup on-call roster | Backup executes launch day checklist |

---

### 9.2 Contingency: Delay Launch

**Scenario**: A critical bug is found 48 hours before launch that cannot be fixed in time.

**Decision Criteria**:
- Is the bug game-breaking? (prevents launch, corrupts saves, crashes on startup)
- Can we fix it in 48 hours?
- Can we ship with a Day 1 patch?

**If delay is necessary**:

| Step | Owner | Timeline |
|------|-------|----------|
| Decide to delay (team vote) | SHIP + ALL | T-48h |
| Update Steam release date (+7 days minimum) | SHIP | T-48h |
| Post delay announcement on Steam News, Discord, Twitter | HYPE | T-48h |
| Email press list with updated embargo date | HYPE | T-48h |
| Fix bug, build new RC, full QA pass | BYTE + CRASH | 48-72h |
| Set new launch date | SHIP | T-24h |
| Launch (new date) | ALL | T-0 |

**Delay Announcement Template**:

```
UPFRONT Launch Delayed to [New Date]

We have discovered a critical bug that affects gameplay and we want to ensure you have the best experience possible at launch.

We are delaying the launch by one week to [New Date] to fix this issue and perform additional QA.

We apologize for the delay and appreciate your patience. The extra time will make the game better.

Thank you for your support.
```

---

### 9.3 Contingency: Catastrophic Failure

**Scenario**: The game launches, but within 2 hours, crash rate exceeds 20%, refund rate exceeds 30%, and review score drops below 50%.

**This is a catastrophic failure. Here is the emergency protocol.**

| Step | Owner | Timeline |
|------|-------|----------|
| Emergency team call (all hands) | SHIP | T+2h |
| Assess: Can we fix this, or do we pull the game? | SHIP + BYTE | T+2h 15min |
| If fixable: Deploy emergency hotfix | BYTE | T+4h |
| If not fixable: Set Steam store to "Coming Soon" (de-list) | SHIP | T+2h 30min |
| Post statement on Steam News: "We are aware of critical issues and are working on a fix. We have temporarily de-listed the game. All purchases will be refunded." | HYPE | T+3h |
| Refund all purchases manually if needed | SHIP | T+24h |
| Fix issues over next 7-14 days | BYTE + CRASH | 1-2 weeks |
| Re-launch when stable | SHIP | TBD |

**This is the nuclear option. Use only if the game is fundamentally broken and unplayable.**

In 20 years of shipping games, I have never seen this scenario happen to a team that followed a proper QA process. But if it does happen, we have a plan.

---

## 10. POST-LAUNCH ROADMAP (MONTHS 1-6)

### 10.1 Patch Roadmap

| Patch | Target Date | Focus | Status |
|-------|-------------|-------|--------|
| **1.0.1** | Launch + 48h | Critical bugs only | [ ] |
| **1.0.2** | Launch + 14 days | Minor bugs, balance tweaks | [ ] |
| **1.1.0** | Launch + 6 weeks | QoL improvements, new content (5 briefs, 3 creatives) | [ ] |
| **1.2.0** | Launch + 3 months | Major content update (Award Season system, if cut from launch) | [ ] |

---

### 10.2 Content Roadmap (If PC Launch Succeeds)

**Success Threshold**: 5,000 copies sold in first month, 80%+ positive reviews

**Post-Launch Content**:
1. **Month 2-3**: Free content update — 10 new briefs, 5 new creatives, 2 new client archetypes
2. **Month 4-6**: Switch port development begins (if sales support it)
3. **Month 6-9**: Paid DLC — "Agency Crisis" system (new campaign type: PR disasters, client boycotts, recovery campaigns)
4. **Month 9-12**: iPad port (if Switch port succeeds)

---

## 11. FINAL PRE-LAUNCH CHECKLIST (T-7 DAYS)

This is the master checklist. Print it. Hang it on the wall. Check every box before launch.

| Category | Task | Owner | Status |
|----------|------|-------|--------|
| **Build** | Gold Master tagged in git as `v1.0.0` | BYTE | [ ] |
| **Build** | GM uploaded to Steam default depot | SHIP | [ ] |
| **Build** | GM tested on clean Windows machine | CRASH | [ ] |
| **Build** | GM tested on clean macOS machine | CRASH | [ ] |
| **Build** | GM tested on clean Linux machine | CRASH | [ ] |
| **Build** | GM tested on Steam Deck (if targeting) | CRASH | [ ] |
| **Build** | Day 1 patch ready (if minor bugs exist) | BYTE | [ ] |
| **Steam** | Store page public, wishlist enabled | SHIP | [ ] |
| **Steam** | Release date set (locked) | SHIP | [ ] |
| **Steam** | Price set, launch discount configured | SHIP | [ ] |
| **Steam** | All screenshots and trailer uploaded | PIXEL | [ ] |
| **Steam** | System requirements tested and accurate | BYTE | [ ] |
| **Steam** | Achievements tested and working | CRASH | [ ] |
| **Steam** | Cloud saves tested | CRASH | [ ] |
| **Steam** | Controller support tested | CRASH | [ ] |
| **Marketing** | Launch trailer posted on YouTube | HYPE | [ ] |
| **Marketing** | Press keys sent to 30 outlets | HYPE | [ ] |
| **Marketing** | Press release written and scheduled | HYPE | [ ] |
| **Marketing** | Social media accounts active | HYPE | [ ] |
| **Marketing** | Discord server ready (channels, roles, welcome message) | HYPE | [ ] |
| **Support** | Steam forums set up | SHIP | [ ] |
| **Support** | Discord support channel created | HYPE | [ ] |
| **Support** | Canned support responses prepared | HYPE | [ ] |
| **Team** | Launch day on-call roster confirmed | SHIP | [ ] |
| **Team** | Launch day war room set up (physical or virtual) | SHIP | [ ] |
| **Team** | Emergency contact list distributed | SHIP | [ ] |
| **Rollback** | Rollback procedure documented and tested | SHIP | [ ] |
| **Rollback** | Hotfix procedure documented | SHIP | [ ] |
| **Rollback** | Communication templates pre-written | HYPE | [ ] |

**If any box is unchecked at T-48 hours, we delay.**

---

## 12. CLOSING NOTES

### 12.1 What Keeps Me Up At Night

I have launched 12 games. Here is what worries me about this launch:

1. **The Gauntlet is the core mechanic. If it is buggy on launch, the game is dead.** We must QA the hell out of the Gauntlet. Every client archetype. Every note. Every pushback scenario. If one client crashes the game, players will refund.

2. **Save corruption.** This is a multi-hour game. If a save corrupts at Year 3, the player loses hours of progress. They will refund and leave a negative review. Save/load must be bulletproof. Test it on 50+ save files. Test it across Unity versions (if we update Unity during dev). Test it with corrupted JSON (what happens if a player edits their save file?).

3. **The first 2 hours are critical.** Steam's refund window is 2 hours. If the player does not "get" the game in 2 hours, they refund. The tutorial must be tight. The first campaign must hook them. The first Gauntlet must make them feel the tension. If we lose them in the first campaign, we lose the sale.

4. **Review bombing.** If the game has a controversial element (the 2000s office culture, the advertising industry satire), a small group of players may review-bomb. We cannot prevent this. But we can respond professionally and ensure the game delivers what the store page promises.

---

### 12.2 What Could Go Right

If the Gauntlet works — if players feel the tension of defending their creative vision against a client who controls the budget — this game will resonate.

The target audience is clear: Game Dev Tycoon fans, Mad Men fans, creative industry professionals. All three groups are hungry for this game. If we execute, word-of-mouth will carry us.

The setting is untapped. There has never been a management sim about advertising. The Super Bowl is a cultural touchstone. Everyone knows what it is. Everyone has opinions about Super Bowl ads. The cultural timing is perfect.

The launch plan is solid. Every step is documented. Every contingency is planned. The team knows what to do. If we follow this checklist, launch day will be boring.

Boring is the goal.

---

### 12.3 Final Checklist (SHIP's Personal Pre-Launch Ritual)

**T-24 Hours**:
- [ ] Print this document
- [ ] Highlight critical path items
- [ ] Set phone alarm for launch time (9:50 AM PST)
- [ ] Set up monitoring dashboard on laptop
- [ ] Charge laptop, phone, backup battery
- [ ] Brew coffee
- [ ] Deep breath

**T-0 (Launch)**:
- [ ] Click "Set Build Live" on Steam
- [ ] Post launch tweet
- [ ] Stare at monitoring dashboard
- [ ] Wait

**T+24 Hours**:
- [ ] Evaluate: Did we hit success criteria?
- [ ] Deploy Day 1 patch if needed
- [ ] Debrief with team
- [ ] Sleep

---

**END OF RELEASE PLAN**

Is it on the checklist?

If yes, do it.

If no, do not do it.

Launch day will be boring.

That means I did my job.

-- SHIP
