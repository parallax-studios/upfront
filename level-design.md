# UPFRONT — Level Design Document

**Author**: GRID (Level Designer)
**Version**: 1.0
**Date**: 2026-02-07
**Status**: Spatial Architecture Complete — Ready for Layout Prototyping

---

> "A level is not geometry. It is a sequence of decisions shaped by where the player looks and where they can walk. In UPFRONT, the player never leaves the agency office. So the office must be a dozen levels compressed into one space — each room a distinct emotional beat, each sightline a breadcrumb, each locked door a progression gate. Where does the player LOOK? At their team. At the client. At the campaign on the wall. The level design is the camera operator for a game that never cuts."

---

## 1. LEVEL DESIGN PHILOSOPHY FOR UPFRONT

### The Core Spatial Challenge

UPFRONT is a management sim without spatial exploration in the traditional sense. The player does not traverse dungeons or navigate combat arenas. They inhabit a single location — the agency office — across dozens of hours of play. This presents a unique level design problem:

**How do you make one space feel like fifty levels?**

The answer is FUNCTIONAL ZONING + TEMPORAL LAYERING + VISUAL NARRATIVE PROGRESSION.

- **Functional Zoning**: Each room is a distinct gameplay beat with its own camera framing, UI density, and interaction rules. The Presentation Room is a negotiation arena. The Bullpen is a personnel management screen. The Edit Suite is a production pipeline. The player "travels" between gameplay modes by moving between rooms, and the spatial transition reinforces the tonal shift.

- **Temporal Layering**: The office changes over time. A year-one agency with six people and empty walls feels spatially and emotionally different from a year-five agency with sixteen people and a lobby full of awards. The same space becomes a different level as the player's history accumulates.

- **Visual Narrative Progression**: Every surface tells a story. The whiteboard. The desks. The walls. The player reads their own choices reflected in the environment. Level design IS environmental storytelling when the player never leaves the level.

### Player Movement Goals

The player's movement through the office should feel like:

1. **Purpose** — Every room transition is a decision. "I need to check on the team" means going to the Bullpen. "I need to see the client" means going to the Presentation Room. Movement is intentional, not exploratory.

2. **Rhythm** — The spatial flow should create natural pacing beats. Leaving the intensity of the Gauntlet to return to the calm of the Corner Office is a moment to breathe. Walking past the Lobby wall of campaigns is a moment to reflect.

3. **Orientation** — The player should always know where they are in the agency and what each space is for. No confusion. No getting lost. This is not a maze. This is a workplace you inhabit.

4. **Ownership** — By year three, the player should know this office like they know their own home. Which desk is Jordan's. Which window Marcus stares out of when he is thinking. Where the coffee stain on the floor appeared after that disastrous pitch. Spatial familiarity breeds emotional investment.

### The Super Bowl Sunday Exception

Once per year, the normal spatial rules suspend for ten minutes. The entire agency crowds into one room to watch the Super Bowl broadcast. The office feels different — smaller, more intimate, electric with shared anticipation. This spatial compression is the climax. The level design must prepare for it by making every other day feel spacious and structured, so the convergence feels special.

---

## 2. THE AGENCY — MASTER LAYOUT

### 2.1 Spatial Overview

The agency occupies a single open-plan floor in a Manhattan mid-rise. Approximately 6,000 square feet. The layout is organized around a central Bullpen with specialized rooms radiating outward. Floor-to-ceiling windows on the west wall provide natural light and a view of the city skyline. The east wall is interior-facing with access to elevators and building services.

### 2.2 Top-Down Map (ASCII)

```
    NORTH

WEST ←  [Agency Floor Plan — Year One Configuration]  → EAST

╔════════════════════════════════════════════════════════════════════╗
║                                                                    ║
║  [Elevator]  [Lobby]──────[Reception Desk]──────[Lobby Wall]     ║
║     │           │                                    │             ║
║     └───────────┴────────────[Hallway]──────────────┴────────┐   ║
║                                  │                             │   ║
║        [Kitchen]────[Hallway]────┼────[Corner Office (Player)] │   ║
║            │                     │              │               │   ║
║            │                     │              │               │   ║
║        [Whiteboard]          [BULLPEN]      [Glass Wall]        │   ║
║                                  │                               │   ║
║                    ┌─────────────┼──────────────┐               │   ║
║                    │             │              │               │   ║
║            [Edit Suite]   [Presentation Room]  [Media Buy]      │   ║
║                    │             │              │               │   ║
║                    │        [Client Chair]      │               │   ║
║                    │        [Player Chair]      │               │   ║
║                    │        [Projection Screen] │               │   ║
║                    │                            │               │   ║
║  [WINDOWS]═════════════════════════════════════════════════════════
║   (West-facing, city skyline view, golden hour light)            ║
╚════════════════════════════════════════════════════════════════════╝

    SOUTH
```

### 2.3 Spatial Flow Diagram

```
        ENTRY                         RITUAL
          ↓                             ↓
       [Lobby] ─────────────────→ [Corner Office]
          │                             ↓
          │                       [Bullpen (Hub)]
          │                             │
          ├─────────────┬───────────────┼──────────────┬──────────────┐
          │             │               │              │              │
      [Kitchen]   [Presentation]  [Edit Suite]   [Media Buy]   [Recruit]
     (Reflect)      (Combat)      (Production)    (Strategy)   (Growth)
          │             │               │              │              │
          └─────────────┴───────────────┴──────────────┴──────────────┘
                                        │
                                    [Lobby Wall]
                                   (Legacy View)
```

The player enters through the Lobby every session. They naturally move to the Corner Office (their desk, their starting point). From there, all paths lead to the Bullpen — the hub. From the Bullpen, the player branches to specialized rooms based on which game system they are engaging. The flow is radial, not linear. No room is more than two clicks from any other room. Fast travel is spatial coherence, not a menu.

---

## 3. ROOM-BY-ROOM BREAKDOWN

### 3.1 The Lobby

**Purpose**: ORIENTATION + FIRST IMPRESSION + LEGACY DISPLAY

**Emotional Beat**: "This is the agency's face. This is what the world sees."

**Dimensions**: 20' x 30'. Elevator doors on east wall. Reception desk in center. West wall is the Lobby Wall — 15 feet of framed campaign posters, award plaques, and press clippings.

**Sightlines**: The player sees the Lobby Wall immediately upon entering. It is the anchor visual. The first time the player enters (year one, day one), the wall is empty except for the agency logo. Every successful campaign adds a frame. By year five, the wall is full. The player watches their history accumulate. This is the game's most powerful environmental storytelling element.

**Lighting**: Bright and professional. Warm overhead spots highlight the Lobby Wall. Cool fluorescent in the hallway beyond. The contrast creates a "public face / private reality" divide.

**Interaction Points**:
- **Lobby Wall** — Click any framed campaign to review its stats, client feedback, and cultural impact. This is the player's trophy room and their memoir in poster form.
- **Cultural Feed Screen** — A flat-panel display near Reception shows scrolling news headlines, trend signals, and industry gossip. This is where the player reads the cultural moment.
- **Reception Desk** — Gatekeeper for client meetings. When a client arrives for an Approval Gauntlet, they appear here first. The player sees them through the glass before entering the Presentation Room. This two-second preview is critical — the player can read the client's mood (body language, facial expression, the speed at which they check their phone) before the negotiation begins.

**Pacing Function**: The Lobby is a PAUSE room. The player enters here at the start of each session. It is not a high-intensity space. It is a breath before the work begins. But it is also a REWARD space — the Lobby Wall is a constant feedback loop showing the player what they have built.

**Breadcrumbing**: A notification icon appears above the Reception Desk when a new client brief arrives or when a scheduled Gauntlet is about to begin. The player knows where to go.

**Progression Gating**: In year one, the Lobby Wall is mostly empty, making the space feel sparse and aspirational. As the agency grows, the wall fills, making the same space feel established and prestigious. The room does not change. The player's perception of it does.

---

### 3.2 The Corner Office (Player's Domain)

**Purpose**: PLANNING + REFLECTION + DECISION-MAKING HUB

**Emotional Beat**: "This is mine. I built this."

**Dimensions**: 12' x 15'. Glass walls on two sides (facing Bullpen and Lobby hallway). Solid wall with window facing west skyline. Desk in center, facing the Bullpen so the player can see their team.

**Sightlines**: From the desk, the player has a clear view into the Bullpen. They can see their team working — who is at their desk, who is collaborating, who is staring at the ceiling in frustration. This voyeuristic sightline is intentional. The player SEES the people they manage, not just stat blocks in a menu. The west window provides a skyline view — a reminder that the agency exists in a larger city, a larger industry.

**Lighting**: Warm and focused. A desk lamp provides task lighting. Natural light from the west window creates dynamic time-of-day shifts. Morning light is cool and blue. Evening light is amber and long. Late-night work happens under the desk lamp alone, the Bullpen dark beyond the glass except for a few dedicated creatives still grinding.

**Interaction Points**:
- **The Desk** — The game's main menu. Clicking the desk opens the campaign overview, active briefs, financial dashboard, and calendar. This is the "mission select" screen, spatially grounded.
- **The Shelf** — Behind the desk. Displays awards won (physical Clio trophies, framed certificates). Empty in year one. Slowly fills. A visual reputation meter.
- **The Whiteboard** — Small personal board on the wall. The player can pin mood images, notes, and reminders. This is cosmetic but personal — a space for the player to express taste.
- **The Window** — Click to trigger a "reflection moment" — a brief text vignette where the player character thinks about the agency's trajectory. These moments are opt-in narrative beats. Most players will never click the window. The ones who do are the ones seeking story.

**Pacing Function**: This is the BREATH room. The player returns here between campaigns, between meetings, between crises. It is the only space that is exclusively theirs. When the player needs to think, they come here.

**Camera Framing**: The camera is positioned behind the player's desk, looking out through the glass wall into the Bullpen. The player is the observer, the director, the architect. The framing reinforces the power dynamic — but also the isolation. Leadership is watching through glass.

---

### 3.3 The Bullpen

**Purpose**: TEAM MANAGEMENT + PERSONNEL INTERACTION + CREATIVE ENERGY

**Emotional Beat**: "These are my people. This is where the work happens."

**Dimensions**: 30' x 40'. Open-plan workspace. Ten to sixteen desks depending on roster size, arranged in clusters of four (one per team). Desks face each other to encourage collaboration. Wide aisles between clusters for movement.

**Sightlines**: From the entrance (either from Corner Office or Lobby hallway), the player sees the entire Bullpen at once. No blind corners. No hidden desks. The player can read the room's energy instantly. Are people working? Talking? Stressed? Celebrating? The spatial read is the emotional read.

**Lighting**: Overhead fluorescent with individual desk lamps. Harsh and functional but softened by personal touches — desk lamps with colored shades, string lights on cubicle edges, a paper lantern someone brought from home. The light is utilitarian but the people humanize it.

**Interaction Points**:
- **Individual Desks** — Click any creative's desk to open their personnel file, assign them to a project, or trigger a one-on-one conversation. Each desk has environmental storytelling: framed photos, stacks of concept sketches, coffee mugs, stress balls, personal totems. A thriving creative has a cluttered, lively desk. A burnt-out creative has a bare one.
- **Mood Board Wall** — A large cork wall where the active project's concept images, reference photos, and inspirational scraps are pinned. This updates dynamically based on which campaign is in development. It is the Bullpen's largest visual element and the player's window into what the team is thinking.
- **Team Chemistry Indicator** — A subtle environmental tell. When a team has high Cohesion, the four-desk cluster is tidy and organized. When Friction is high, the desks are chaotic — papers everywhere, Post-its peeling, a coffee cup knocked over two days ago. When Meltdown is imminent, one desk is empty — someone is avoiding the office.

**Pacing Function**: This is the ENERGY room. The Bullpen hums with activity. It is never silent unless something is very wrong. The player spends more time here than anywhere else because team management is a continuous loop, not a discrete task.

**Spatial Flow**: The Bullpen is the hub. Every specialized room connects to it. The player always passes through the Bullpen when moving between rooms. This creates natural "check-in" moments — the player sees their team even when they are not actively managing them. Passive observation builds attachment.

**Encounter Breakdown**: The Bullpen hosts micro-encounters — brief conversations, check-ins, morale moments. A creative might approach the player as they walk through: "Got a second? I want to run something by you." These are 15-30 second narrative beats that add texture without disrupting flow.

---

### 3.4 The Presentation Room

**Purpose**: THE APPROVAL GAUNTLET — NEGOTIATION ARENA

**Emotional Beat**: "This is where work lives or dies. The client sits across from me. I must defend what we made."

**Dimensions**: 15' x 25'. Long conference table down the center. Projection screen at the far end. Client side of the table faces the screen. Player side faces the door (so the client's back is to the entrance — a subtle power dynamic; the player sees anyone approaching, the client does not).

**Sightlines**: The camera is positioned from the player's seat, looking across the table at the client. The projection screen is visible behind/above the client, showing the concept being pitched. The door is visible to the player's right — they see people pass in the hallway, a reminder that the agency continues outside this room, but inside, it is just two people negotiating.

**Lighting**: Controlled and slightly dim. The screen provides most of the light. This focuses attention on the client's face and the concept on screen. No windows. No distractions. The room has the specific tension of a space designed for judgment.

**Interaction Points**:
- **The Table** — The negotiation interface. Concept stats displayed as a "pitch deck" spread across the table. Client reaction indicators (facial expression, body language, phone-checking frequency) update in real time based on their archetype and current satisfaction.
- **The Projection Screen** — Displays the ad concept as a storyboard animatic, mood board, or key frames. The player and client both look at this. Shared focus.
- **Pushback Gauge** — A subtle UI element near the player's seat showing remaining Pushback Points and estimated Persuasion success rate for the current note. This is not diegetic (the player character does not see a gauge) but the player needs this information to make strategic decisions.
- **The Door** — During intense Gauntlet moments, a team member may enter — Marcus checking on progress, Diane arriving to reinforce the pitch, Victor delivering a production update that changes the budget constraints. These scripted interruptions are spatial storytelling: the agency is a living system, and the Presentation Room is not isolated from it.

**Pacing Function**: This is the COMBAT room. The Approval Gauntlet is the highest-tension beat in the game. The player's heart rate should elevate when they enter this space. The room's design reinforces this: enclosed, focused, pressurized.

**Camera Framing**: Fixed perspective from the player's chair. No ability to move the camera. This lack of control mirrors the negotiation itself — the player cannot escape, cannot look away, cannot leave until the Gauntlet resolves. Spatial constraint creates emotional constraint.

**Encounter Design**:

Each Gauntlet is a 3-5 round encounter:

**Round 1 (Introduction)**:
- Client enters. Brief pleasantries. Camera focuses on client face as they react to initial pitch.
- Player presents concept. Screen displays storyboard. Client's micro-expressions provide feedback before dialogue begins.
- First Note issued (if any). Player selects response.

**Round 2-4 (Escalation)**:
- Player implements accepted changes or defends with Pushback.
- Client's mood shifts based on player choices. Visual tells: leaning forward (engaged), leaning back (skeptical), checking phone (losing patience), nodding (close to approval).
- Each round, the concept on screen updates to reflect accepted changes. The player SEES the work being compromised or defended in real time.

**Round 5 (Resolution)**:
- Client approves, walks away, or demands one final change.
- If approved: client stands, shakes hand, leaves. The room empties. The player sits alone for three seconds, looking at the final concept on screen. Beat of reflection.
- If walked: client stands, says something curt, exits. The screen goes dark. The room feels cold.
- Transition back to Bullpen. The spatial return to the team after the isolation of the Gauntlet is a relief.

**Difficulty Variants**:
- **Conservative Client (Low Risk Tolerance)**: More Notes per round. Faster patience decay. The player must concede more often or burn Pushback Points aggressively.
- **Desperate Client (High Risk Tolerance)**: Fewer Notes but higher emotional volatility. A failed Pushback might trigger immediate walkout instead of just lowering trust.
- **Prestige Client (Slow Approval)**: Gauntlet extends to 5+ rounds. Each Note is small but cumulative. Death by a thousand cuts. Tests patience and resource management.

---

### 3.5 The Edit Suite

**Purpose**: PRODUCTION PIPELINE — BUDGET ALLOCATION + CRAFT FOCUS

**Emotional Beat**: "This is where concept becomes reality. Where vision meets constraint."

**Dimensions**: 10' x 20'. Long, narrow room. Editing workstation at far end with multiple monitors. Mixing board and sound equipment. Dark walls and ceiling (to minimize screen glare). Blue-glow ambiance from monitors.

**Sightlines**: The camera enters over the player's shoulder as they stand behind Victor (or whichever producer is working). The focus is the screens — storyboard previews, timeline, budget tracker. The room is a cave, intentionally cut off from the rest of the agency. This is where the work goes to become REAL.

**Lighting**: Cool and dark. Monitor glow is the primary light source. Occasional desk lamp. No natural light. This is a 2 AM space even at 2 PM. The lighting reinforces focus and craft.

**Interaction Points**:
- **Budget Allocation Sliders** — The production pipeline interface. Five categories (Casting, Location, VFX, Sound, Edit). Drag to allocate. Visual feedback shows concept stats shifting as budget is distributed. Diminishing returns thresholds highlighted.
- **Preview Screen** — Shows a rough animatic of the ad with current production values applied. Low-budget looks rough and kinetic. High-budget looks polished and cinematic. The player SEES the production choices, not just numbers.
- **Victor (or Producer)** — Present in the room, offering commentary. "That VFX budget is going to hurt us," or "If we move $50K from Casting to Location, we can get the warehouse." These are diegetic tooltips — expert advice from the character.

**Pacing Function**: This is a 60-90 second ALLOCATION PUZZLE between the high-tension Gauntlet and the high-stakes Broadcast. It is a tactical break, not a strategic deep dive. The player makes quick, informed decisions and moves forward.

**Spatial Flow**: The player enters from the Bullpen after a concept is approved. They spend 60-90 seconds here, then exit back to the Bullpen to wait for the Broadcast moment. The Edit Suite is a PASS-THROUGH space, not a destination.

**Progression Over Time**: In year one, the Edit Suite is bare-bones — a single workstation, outdated monitors, jury-rigged equipment. As the agency grows and invests in office upgrades, the Edit Suite improves — better monitors, professional mixing board, a second workstation for simultaneous projects. The space visually reflects the agency's increasing production capacity.

---

### 3.6 The Kitchen

**Purpose**: MORALE HUB + COMMUNITY SPACE + NARRATIVE DELIVERY

**Emotional Beat**: "This is where we are human. Where hierarchy dissolves for five minutes."

**Dimensions**: 12' x 18'. Kitchenette along one wall (sink, coffee maker, mini fridge, microwave). Small table with four chairs. Whiteboard on the opposite wall.

**Sightlines**: Open doorway to the Bullpen. The player sees people coming and going. The Kitchen is permeable — not a closed room but an open gathering space. The Whiteboard is the visual anchor, covered in messages, countdowns, and the collective voice of the agency.

**Lighting**: Overhead fluorescent. Harsh but familiar. The coffee maker glows orange when brewing. The whiteboard reflects light, making it readable from the doorway.

**Interaction Points**:
- **The Whiteboard** — The game's meta-narrative delivery system. Updated weekly with messages from unnamed agency members. Countdowns to Super Bowl Sunday. Birthday announcements. Passive-aggressive notes ("Whoever keeps stealing my yogurt, I KNOW who you are"). Occasional moments of genuine creative inspiration or emotional vulnerability ("We're going to be okay"). The player can read but not write — this is the team's voice, not the player's.
- **The Coffee Maker** — Click to trigger a "coffee break" — a 10-second idle animation where the player character makes coffee and the camera lingers on the Whiteboard, encouraging the player to read the latest updates. This is a voluntary pause button embedded in the space.
- **Random Encounters** — Team members occasionally appear here. Jordan eating lunch alone, reading a book. Diane and Marcus having a tense conversation that stops when the player enters. Victor microwaving something that smells aggressively like fish. These are 5-10 second vignettes that add life.

**Pacing Function**: This is the INTIMACY room. The player comes here to check morale, to read the Whiteboard, to witness the human side of the agency. It is the counterbalance to the Presentation Room's pressure.

**Narrative Progression**: The Whiteboard content evolves across the year:
- **Q1**: Optimistic and energized. "New year, new campaigns." "Who's ready for this?" Countdown begins if Super Bowl slot secured.
- **Q2**: Mid-year fatigue. Deadlines loom. "46 days until the pitch. Who's nervous? Everyone? Cool." Birthday for a team member. Someone leaves a supportive note.
- **Q3**: High tension. "Super Bowl countdown: 89 days." "We're going to be fine." "We're going to be great." "We're going to be fired." Dark humor increases.
- **Q4**: Crunch. Countdown accelerates. Messages get shorter, more frantic. The Whiteboard is a barometer of collective stress.
- **Post-Super Bowl**: Relief or devastation depending on outcome. Someone writes "We did it" or "Next year" or just "...well."

---

### 3.7 The Media Buy Desk

**Purpose**: STRATEGIC PLANNING — SUPER BOWL BIDDING + AD PLACEMENT

**Emotional Beat**: "This is where ambition meets budget. Where I decide how big to bet."

**Dimensions**: 8' x 10'. A single desk against the wall, surrounded by printed media rate sheets, market analysis reports, and a year-long placement calendar pinned to a cork board.

**Sightlines**: The desk faces the Bullpen through an open doorway. The player can glance out and see their team working, a reminder that every bidding decision affects the people beyond this room.

**Lighting**: Functional fluorescent. A desk lamp throws harsh light on the spreadsheets. This is not a beautiful space. It is a tactical one.

**Interaction Points**:
- **The Super Bowl Auction Interface** — Opens in Q3 once the player's Reputation threshold is met. Displays available Super Bowl ad slots (first quarter, halftime, third quarter, fourth quarter, post-game), current bid prices, and competitor bids (if Rival Agencies stretch goal is active). The player commits budget and watches the auction resolve.
- **Placement Calendar** — Shows the year's ad schedule. Which campaigns air when. Regular-season placements are low-stakes background events. The Super Bowl is the red-circled date everyone sees from across the room.
- **Financial Projections** — A spreadsheet showing revenue, expenses, and projected cash flow. The player can see whether a Super Bowl bid is financially sustainable or reckless. Diane occasionally appears here to provide analysis: "If we bid this, we cannot afford to lose the MegaBev account."

**Pacing Function**: This is a HIGH-STAKES DECISION room but LOW-FREQUENCY. The player visits once or twice per quarter. The decisions made here ripple through the entire year, but the room itself is not a hub.

**Spatial Flow**: Tucked in a corner, adjacent to the Bullpen but not central. The player must deliberately choose to go here. It is not on the critical path for standard campaigns — only for Super Bowl bids and strategic planning.

---

### 3.8 Super Bowl Sunday — Spatial Exception

**Purpose**: ANNUAL CLIMAX — SHARED EXPERIENCE + VULNERABILITY + CATHARSIS

**Emotional Beat**: "We are all watching. Together. Everything we built comes down to this."

**Spatial Configuration**: The entire agency crowds into one room — the Kitchen or the Bullpen, depending on team size. A large TV (a retro CRT in 2003) is wheeled in. Folding chairs, couches from the lobby, people standing. The normal spatial boundaries dissolve. Everyone is pressed together. The Corner Office is empty. The Presentation Room is dark. The Edit Suite is silent. The whole agency is HERE, in THIS moment.

**Sightlines**: The camera pulls back to show the crowd. Faces in the blue glow of the TV. The player character is seated in the center or standing at the back — positioned to see both the screen and the team's reactions. Split-screen interface: TV broadcast on the left, team reactions on the right.

**Lighting**: Dark except for the TV. Faces glow blue. Someone brought chips. Someone else is holding their breath. Marcus is motionless. Diane is gripping the arm of her chair. Jordan is biting their nails. Victor is watching with the analytical detachment of someone who knows exactly how much this cost to make.

**Pacing**:
1. **Pre-Game (2 minutes)**: The team gathers. Small talk. Nervous energy. Someone tries to make a joke. It does not quite land.
2. **Countdown (30 seconds)**: The pregame show on TV. "Coming up next, the ads everyone's been waiting for." The room goes quiet.
3. **Broadcast (30 seconds)**: The ad airs. No one breathes. The storyboard animatic plays in the game. The TV audience sees the finished product. The player sees both.
4. **Immediate Reaction (15 seconds)**: The team reacts first. Cheers or groans or stunned silence. Then the America Reacts panel lights up — simulated viewer sentiment flooding in.
5. **Post-Game (1 minute)**: The room does not disperse immediately. People linger. Someone refreshes the internet discourse feed. Someone hugs someone else. Or someone leaves quietly, and their absence is loud.
6. **Monday Morning (3 minutes)**: The spatial return to normal. The Corner Office. The Bullpen. But everything feels different. The metrics are in. The client calls. The agency must reckon with the result.

**Encounter Design**: The Super Bowl is not a decision point. The player has NO CONTROL during the broadcast. They are a spectator to their own work's reception. This powerlessness is the climax's emotional engine. The player spent 11 months making decisions. Now they watch the world decide.

---

## 4. PROGRESSION & SPATIAL UNLOCKS

### Year One — The Startup Space

**Spatial Feel**: Sparse. Aspirational. Empty.

- The Lobby Wall has one framed piece: the agency logo.
- The Bullpen has six desks for the initial team. Four to eight more desks sit empty, waiting.
- The Corner Office shelf is bare.
- The Kitchen Whiteboard has a hand-drawn logo and a message: "Day One. Let's go."
- The Edit Suite has minimal equipment.

**Player Emotion**: "We are small. We are new. We have potential."

**Unlocks**: None. All rooms accessible from day one. The agency is fully navigable, but much of it feels underutilized.

---

### Year Two — Growing Pains

**Spatial Changes**:
- The Lobby Wall now has 3-5 framed campaigns.
- The Bullpen has 8-10 desks filled. The empty desks are fewer.
- The Corner Office shelf has one or two awards (if earned).
- The Kitchen Whiteboard has more layers — old messages not fully erased, new ones written over them, creating a palimpsest of the agency's year.
- The Edit Suite gets an equipment upgrade (visible new monitors, better lighting).

**Player Emotion**: "We are growing. We are legitimate. We are still fragile."

**Unlocks**:
- **Media Buy Desk** becomes relevant (if Reputation threshold met). Previously accessible but inactive. Now it matters.
- **Rival Agency Alerts** (if stretch goal active) — occasionally, the Lobby screen shows a rival's campaign launch. The player sees what they are up against.

---

### Year Three to Four — Established Agency

**Spatial Changes**:
- The Lobby Wall is 60-80% full. The agency's history is visible at a glance.
- The Bullpen is full or nearly full. 12-16 desks occupied. The space hums with energy.
- The Corner Office shelf is crowded with awards. The player may need a second shelf.
- The Kitchen Whiteboard is dense with overlapping text, years of messages creating texture.
- The Edit Suite is professional-grade. A second workstation appears if the player invests in office upgrades.

**Player Emotion**: "We are a force. We have a reputation. We are respected."

**Unlocks**:
- **Private Offices for Senior Staff** — If the player invests in office expansion, Marcus and Diane get small private offices adjacent to the Bullpen. These become new interaction points. The player can have private conversations here that the team cannot overhear. The spatial hierarchy reflects the organizational hierarchy.

---

### Year Five Plus — Legacy or Decline

**Spatial Divergence**: The agency's physical space now reflects the player's choices across years.

**Path A: Creative Prestige Agency**
- Lobby Wall is full of awards and bold campaign posters.
- Bullpen desks are cluttered, energetic, collaborative. Post-its everywhere. Mood boards chaotic.
- Corner Office shelf overflows with Clios and Grand Prix trophies.
- Kitchen Whiteboard has inspirational quotes, weird inside jokes, evidence of a tight-knit team.
- **Feel**: "We made something that mattered."

**Path B: Commercial Reliability Agency**
- Lobby Wall is full of safe, polished campaigns and client testimonials.
- Bullpen desks are organized, professional, tidy. Less chaotic energy, more corporate discipline.
- Corner Office shelf has fewer awards but more framed thank-you letters from clients and revenue milestone plaques.
- Kitchen Whiteboard is more procedural — schedules, deadlines, compliance reminders.
- **Feel**: "We built something that lasts."

**Path C: Stagnant or Declining Agency**
- Lobby Wall has gaps where frames were removed (lost clients, campaigns the player wants to forget).
- Bullpen has empty desks. People left and were not replaced.
- Corner Office shelf has old awards gathering dust. No new ones in years.
- Kitchen Whiteboard has fewer messages. The collective voice is quieter.
- **Feel**: "We survived. But at what cost?"

The spatial environment is the reputation score made visible. The player reads their choices in the furniture.

---

## 5. CAMERA & NAVIGATION DESIGN

### Camera Perspectives by Room

| Room | Camera Type | Justification |
|------|-------------|---------------|
| **Lobby** | Third-person isometric, elevated | Player sees the whole space and the Lobby Wall. Survey view for reflection. |
| **Corner Office** | Over-the-shoulder from desk, facing Bullpen | Player sees their team through glass. Voyeuristic, paternal. |
| **Bullpen** | Free isometric with slight rotation | Player can orbit to see all desks. Management perspective. |
| **Presentation Room** | Fixed first-person from player's chair | Cannot move. Must face client. Claustrophobic. Focused. |
| **Edit Suite** | Over-the-shoulder behind producer | Player watches the screens, not the producer. Craft focus. |
| **Kitchen** | Third-person isometric, low angle | Player is at eye level with the team. Democratic space. |
| **Media Buy Desk** | Top-down over desk | Spreadsheets and calendars fill the frame. Tactical perspective. |

### Navigation Method: POINT-AND-CLICK WITH SPATIAL GROUNDING

The player clicks to move between rooms. No WASD exploration. This is not a walking simulator. The value is not in traversal — it is in decision-making.

**Interaction Flow**:
1. Player is in Room A.
2. Player clicks doorway/exit to Room B.
3. Brief transition (1-2 seconds) — camera tracks through the hallway or Bullpen, showing the agency in motion. This is not a loading screen. It is spatial continuity.
4. Camera arrives in Room B, positioned for that room's interaction.

**Fast Travel Exception**: A radial menu (right-click or hotkey) allows instant jump to any room. Expert players will use this. New players will click doorways, learning the spatial layout organically. Both methods are valid.

**Spatial Audio Cues**: Each room has distinct ambient sound that fades in as the player approaches.
- Lobby: Distant elevator ding, muffled street noise, professional quiet.
- Corner Office: Muted Bullpen sounds through glass, occasional phone ring.
- Bullpen: Keyboard clatter, low conversations, chair squeaks, creative energy.
- Presentation Room: Silence. Projector hum. Uncomfortable stillness.
- Edit Suite: Monitor buzz, mouse clicks, soft music from headphones.
- Kitchen: Coffee maker gurgle, fridge hum, whiteboard marker squeak.

The player navigates by sound as much as by sight. You HEAR the Bullpen from the hallway before you see it.

---

## 6. BREADCRUMBING & WAYFINDING

### How the Player Knows Where to Go

UPFRONT has no quest markers, no glowing arrows, no minimap. The player learns the space and the systems teach navigation.

**Notification System**:
- **Active Brief Icon** appears above the Corner Office desk when a new campaign is ready to start.
- **Client Arrival Icon** appears above the Reception Desk when a Gauntlet is scheduled.
- **Team Alert Icon** appears above the Bullpen when a team member requests attention (morale issue, concept ready for review, personnel crisis).
- **Whiteboard Icon** appears above the Kitchen when new messages are posted (optional, for players who care about narrative texture).

These icons are diegetic — they appear as glowing Post-it notes, message notifications, or desk lamps turning on. No HUD pollution.

**Spatial Memory**:
By hour five, the player knows the layout instinctively. "I need to check the team" means Bullpen. "I need to see the client" means Presentation Room. "I need to think" means Corner Office. The space becomes muscle memory.

**Environmental Cues**:
- The Lobby Wall is visible from multiple rooms. It orients the player: "If I can see the Lobby Wall, the exit is behind me."
- The windows are always on the west side. The player learns cardinal directions.
- The Bullpen is always central. No matter where you are, the Bullpen is two clicks away.

**Narrative Guidance**:
Diane and Marcus occasionally send messages: "Can you meet me in the Presentation Room?" or "I'm in the Kitchen if you want to talk." These are diegetic navigation prompts for key story beats.

---

## 7. PACING CURVES ACROSS ROOM TYPES

### 7.1 The Campaign Arc (5-8 Minutes)

**Pacing Graph**:

```
Tension
   │
10 │                           ██ Gauntlet
   │                         ██  ██
 8 │                       ██      ██
   │                     ██          ██ Broadcast
 6 │                   ██              ██
   │                 ██                  ██
 4 │               ██  Production          ██
   │             ██                          ██
 2 │  ██ Brief ██  Selection                  ██ Aftermath
   │██                                          ██
 0 └──────────────────────────────────────────────────────→
   0   1    2    3    4    5    6    7    8    (minutes)

   Lobby → Office → Bullpen → Office → Presentation → Edit → Bullpen → Lobby
  (Enter) (Read)  (Assign)  (Choose)   (COMBAT)    (Allocate) (Watch) (Reflect)
```

**Spatial Rhythm**:
- Low tension rooms: Lobby, Corner Office, Kitchen (breathing spaces)
- Medium tension rooms: Bullpen, Edit Suite, Media Buy (tactical decisions)
- High tension rooms: Presentation Room (the spike)
- Catharsis rooms: Bullpen (team reaction), Lobby (see the campaign added to the wall)

Every campaign flows through this curve. The player learns the rhythm. The spatial progression mirrors the emotional progression.

---

### 7.2 The Super Bowl Arc (10 Minutes)

**Pacing Graph**:

```
Tension
   │
10 │                                          ██ Broadcast
   │                                        ██  ██
   │                                      ██      ██
 8 │                                    ██          ██ Monday
   │                              ████                ██
 6 │                          ████                      ██
   │                    ██████ Pre-Game                  ██
 4 │              ██████                                   ██
   │        ██████ Build-Up                                 ██
 2 │  ████████                                                ██
   │██ Anticipation                                             ██
 0 └────────────────────────────────────────────────────────────────→
   0    1    2    3    4    5    6    7    8    9    10   (minutes)

   Office → Media Buy → Bullpen → Kitchen → [CONVERGENCE] → Office
  (Decision) (Confirm)  (Team Prep) (Gather)   (WATCH)    (Aftermath)
```

The Super Bowl arc is longer, slower-building, and peaks higher than any standard campaign. The spatial convergence (everyone in one room) reinforces the climax.

---

### 7.3 The Calendar Year (45-90 Minutes)

**Pacing Graph**:

```
Tension
   │
10 │                                                       ██ Super Bowl
   │                                                     ██  ██
 8 │                                     ████          ██      ██
   │                           ████    ██    ██      ██          ██
 6 │         ████      ████  ██    ████        ████              ██
   │   ████      ████      ██                                      ██
 4 │ ██                  ██   Awards                                 ██
   │                  ██        Crunch                                 ██
 2 │              ████                                                   ██
   │          ████   Build                                                ██
 0 └──────────────────────────────────────────────────────────────────────────→
   Q1          Q2          Q3          Q4          Super Bowl  Reset
  (Setup)   (Growth)  (Push)      (Crunch)        (Climax)   (Reflect)

  Multiple campaigns, overlapping tension curves, building to singular peak.
```

The year is not flat. It has waves. The player feels the rhythm of the industry — the slow Q1, the building Q2, the intense Q3 media buy decision, the relentless Q4 crunch, and the singular Super Bowl peak.

Spatial flow mirrors this: Early year, the player spends more time in the Corner Office and Bullpen (planning, building). Late year, the player spends more time in the Presentation Room and Edit Suite (execution, crisis management). Super Bowl Sunday is spatial convergence. Post-Super Bowl is spatial dispersal and reflection.

---

## 8. DIFFICULTY CONSIDERATIONS

### 8.1 Spatial Complexity Scaling

The office does not get MORE complex. It gets MORE DENSE.

**Year One**: Few people. Quiet rooms. Empty desks. The player learns navigation without distraction.

**Year Five**: Full roster. Overlapping conversations. Desks cluttered with ongoing projects. The same space is harder to READ because there is more information layered into it. The level design challenge shifts from "learn the layout" to "parse the density."

This is intentional. A veteran agency SHOULD feel busier. The spatial overwhelm mirrors the management overwhelm.

---

### 8.2 Gauntlet Difficulty by Spatial Tell

The Presentation Room encounter difficulty is signaled spatially BEFORE the Gauntlet begins:

**Easy Gauntlet**:
- Client arrives calm. Sits immediately. Leans forward. Makes eye contact.
- Projection screen boots quickly. No technical issues.
- Door remains closed. No interruptions.

**Medium Gauntlet**:
- Client arrives distracted. Checks phone before sitting. Sits back in chair.
- Projection screen takes a moment to load (minor production anxiety).
- Door may open once (Diane checking in, Victor delivering an update).

**Hard Gauntlet**:
- Client arrives tense. Does not sit immediately. Stands by window, looking out, before turning to the table. Bad sign.
- Projection screen glitches (the concept itself is on shaky ground).
- Door opens multiple times (external pressures intrude — Marcus wants to make changes, Diane warns the client is one bad note away from walking, a phone call interrupts).

The player learns to read the room before the first word is spoken. Spatial literacy IS difficulty literacy.

---

### 8.3 Late-Game Spatial Entropy

By year five, IF the player has mismanaged, the office shows decay:

- Empty desks in the Bullpen (people left, were not replaced).
- Lobby Wall has gaps (campaigns removed, clients lost).
- Corner Office shelf has trophies but they are dusty, unlit.
- Kitchen Whiteboard has fewer messages, longer gaps between updates.
- Edit Suite equipment is outdated (no upgrades invested).

The space reflects decline. This is not a fail state. This is a STORY state. The player can rebuild from here — but the spatial environment tells the truth before the numbers do.

---

## 9. PLAYTESTING METRICS

### What to Measure in Level Design Playtests

**Spatial Navigation**:
- Time to first successful room transition (target: <30 seconds from start).
- Number of times player opens fast-travel menu in first hour (high number = layout is confusing).
- Percentage of players who read the Lobby Wall at least once per session (target: >70%).

**Emotional Beats**:
- Does the player pause in the Corner Office to look at their team through the glass? (Observational data: if yes, voyeuristic framing is working.)
- Does the player voluntarily visit the Kitchen to read the Whiteboard? (If no, the Whiteboard is not compelling or well-signaled.)
- Post-Gauntlet: does the player linger in the Presentation Room, or do they exit immediately? (Linger = emotional weight. Immediate exit = tension relief sought. Both are valid but the data reveals player processing style.)

**Pacing Validation**:
- Average time spent per room type. If players spend 10+ minutes in the Edit Suite, the production pipeline is too deep (contradicts design intent). If players spend <30 seconds, it may be too shallow (no meaningful choice).
- Campaign completion time (target: 5-8 minutes from brief to broadcast). If consistently under 5, pacing is rushed. If consistently over 8, pacing drags.

**Progression Reads**:
- Can players articulate the agency's growth when looking at the Lobby Wall? ("We started with nothing. Now look.") If yes, visual progression is legible.
- Do players notice when a creative's desk goes from cluttered to empty (burnout signal)? If no, the environmental storytelling is too subtle.

**Super Bowl Climax**:
- Player heart rate during Super Bowl broadcast (if biometric data available). Target: measurable spike. If flat, the spatial convergence and broadcast pacing need intensification.
- Post-Super Bowl: do players immediately start a new campaign, or do they sit in the aftermath? (Immediate action = climax did not land emotionally. Sitting = catharsis achieved.)

---

## 10. OPEN QUESTIONS FOR ITERATION

These are the spatial design questions that need playtesting to answer:

**1. How much spatial exploration vs. menu efficiency do players want?**

Do players enjoy the spatial grounding (clicking through rooms, seeing the office), or do they quickly default to fast-travel menus? If 80% of navigation is fast-travel by hour 10, the spatial layer may be narrative flavor, not core engagement. That is fine — but we need to know.

**Test**: Track navigation method usage over time. Interview players: "Do you feel like moving through the office adds to the experience, or would you prefer a menu?"

**2. Does the Presentation Room's fixed camera enhance tension or frustrate players?**

The locked perspective is intentional — it creates claustrophobia and focus. But some players may find it restrictive. If playtesters consistently ask "can I move the camera?" we need to evaluate whether the constraint serves the design or hinders it.

**Test**: A/B test. Half of playtesters get fixed camera. Half get limited camera rotation (45 degrees left/right). Measure tension self-reports and Gauntlet engagement.

**3. Is the Lobby Wall reward sufficient for the player's effort?**

The Lobby Wall is the primary environmental storytelling device. But if players do not engage with it — if they walk past without looking — it is wasted design. Does it need more explicit signaling? A notification when a new frame is added? A character comment ("Check out the wall, we just hung the BrightBurst poster")?

**Test**: Eye-tracking or observational data. Do players look at the Lobby Wall? How often? For how long? If engagement is low, test explicit prompts.

**4. Does the Kitchen Whiteboard feel like a living document or a static prop?**

The Whiteboard is designed to update weekly and reflect the agency's collective voice. But does it feel dynamic enough? Do players check it regularly, or do they read it once in year one and never again?

**Test**: Track Kitchen visits. Count Whiteboard interactions. If <20% of players engage past the first visit, the content needs more variability, more narrative hooks, or better integration with gameplay systems (e.g., "A team member left you a note on the Whiteboard").

**5. What is the right frequency for environmental changes?**

How often should the office visibly change? Weekly? Quarterly? Annually? Too frequent and the changes blur together. Too infrequent and the progression feels static.

**Test**: Three variants. Group A gets monthly updates (new desk clutter, Whiteboard changes, Lobby additions). Group B gets quarterly updates. Group C gets annual updates. Measure which group reports the strongest sense of progression.

**6. Should the office be 2D isometric or 3D explorable?**

The design assumes isometric point-and-click (Game Dev Tycoon, Two Point Hospital style). But could the game benefit from full 3D traversal? Does walking through the office in first-person or third-person create stronger spatial attachment?

**Test**: Build a 3D prototype of the Bullpen. Let playtesters walk through it. Measure emotional attachment ("Do you feel like this is YOUR agency?") compared to isometric control group. Balance against development cost.

---

## 11. VARIANT LEVEL CONCEPTS (STRETCH GOALS)

If development resources allow, these are additional spatial layers that deepen the experience:

### 11.1 Multiple Office Tiers

Instead of a single office that upgrades cosmetically, the player can MOVE to a larger office as the agency grows. Three tiers:

**Tier 1: Startup Office (Year 1-2)**
- 3,000 sq ft. Six desks. Minimal rooms. Shared kitchen is a corner with a coffee maker. No Presentation Room — pitches happen in the Bullpen. Scrappy. Intimate. Underdog energy.

**Tier 2: Mid-Rise Office (Year 3-4)**
- 6,000 sq ft (current design). Dedicated rooms for each function. Proper Presentation Room. Professional but not luxurious. The "we made it" space.

**Tier 3: Prestige Office (Year 5+)**
- 10,000 sq ft. Multiple team clusters. Private offices for senior staff. Client lounge. Rooftop terrace for team events. Glass and steel. The player can SEE the success in the architecture.

**Design Impact**: Moving offices is a HUGE narrative beat. The player leaves the space where they started. Nostalgia and ambition collide. The old office was where they made their first great campaign. The new office is where they will make their legacy. Environmental storytelling through absence.

**Risk**: Development cost triples if three full office layouts are required. Mitigation: Tier 1 and Tier 2 share a base layout with scaling (Tier 1 is the Tier 2 space but half-empty). Tier 3 is a new layout, unlocked only if the player reaches 80+ Reputation.

---

### 11.2 Rival Agency Glimpses

If the Rival Agencies stretch goal is active, the player occasionally visits a rival's office for industry events (award ceremonies, pitch competitions). These are NON-INTERACTIVE spaces — the player does not navigate them, but they SEE them.

**Purpose**: Environmental storytelling about the rival's philosophy.

**Example**:
- **Safe Corporate Agency (Sterling & Hayes)**: Sterile. Glass. Chrome. Identical desks in perfect rows. No clutter. No personality. A Lobby Wall of blue-chip brands and Fortune 500 logos. The player feels the difference immediately: "This is not us."

- **Reckless Award-Hungry Agency (Voltage Creative)**: Chaos. Exposed brick. Graffiti on the walls. A skateboard ramp in the Bullpen. Lobby Wall covered in Cannes Lions and Grand Prix trophies but also eviction notices and unpaid invoices pinned with ironic pride. The player feels the difference: "This is what we could become if we chase awards and nothing else."

**Design Impact**: Contrast illuminates identity. The player sees other agencies and understands their own choices more clearly.

---

### 11.3 The Client's Office (Gauntlet Variant)

Occasionally, instead of the client coming to the agency, the player goes to the CLIENT'S office for the Gauntlet. This is a power-dynamic shift.

**Spatial Design**:
- CLIENT's Presentation Room is more intimidating. Larger. Colder. The player sits on the opposite side of the table. The client's trophies, their brand history, their power is on display.
- The player is in the client's territory. Pushback success rates decrease by 10%. The space itself applies pressure.

**When This Happens**:
- Corporate Titan clients (high-tier, high-power-imbalance).
- Crisis pitches (the agency is on thin ice, the client demands the meeting on their turf).
- Final approval for Super Bowl spots (the stakes are so high the client wants home-field advantage).

**Design Impact**: Spatial location becomes a difficulty modifier. The player FEELS the power imbalance through the environment before the negotiation begins.

---

## 12. CLOSING STATEMENT

UPFRONT is a game about people in rooms making decisions. The rooms must be more than backdrops. They must be emotional instruments.

Every room has a PURPOSE. Every sightline has a MEANING. Every spatial transition has a RHYTHM.

The Lobby is the mirror. The Corner Office is the throne. The Bullpen is the heartbeat. The Presentation Room is the arena. The Kitchen is the confession booth. The Edit Suite is the workshop. The Super Bowl convergence is the cathedral.

The player walks these rooms for 50 hours. By the end, they know which floorboard creaks. They know which window catches the golden hour light. They know the shape of the space the same way they know the shape of their own apartment. The office becomes HOME — and that is the level design's ultimate goal.

When the player looks at the Lobby Wall, full of campaigns, and thinks "I built this," the level design has succeeded. Because the WALL is the level. The CAMPAIGNS are the level. The PEOPLE at the DESKS are the level. The office is not a container for the game. The office IS the game.

Where does the player LOOK? At their work. At their people. At the years they spent in these rooms.

Where does the player WALK? Through their own history, one campaign at a time.

That is the level. That is the design.

Now build it. Test it. Watch someone play it. Then come back and tell me where they got lost, where they paused, and where they felt HOME.

— GRID
