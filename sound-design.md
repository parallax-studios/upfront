# UPFRONT — Sound Design Document

**Sound Designer**: ECHO
**Version**: 1.0
**Date**: 2026-02-07
**Status**: Production-Ready

---

> "Audio IS game feel. The player doesn't notice good sound — they FEEL it in their chest when the client rejects their pitch, in their breath when the Super Bowl ad airs, in the hollow ache when they choose the safe version. Every moment in UPFRONT has a frequency. Every frequency has an emotion. Listen to the space between."

---

## 1. SONIC IDENTITY STATEMENT

UPFRONT sounds like ambition under fluorescent lights.

This is not the bombast of war or the fantasy of magic. This is the human-scale tension of creative work: the confidence of a great pitch, the deflation of a killed concept, the adrenaline of a deadline, the collective held breath when your 30-second masterpiece plays for a hundred million simulated people.

The sonic identity is built on contrast:

**INTIMATE** vs. **SPECTACLE**
The agency sounds close, diegetic, tactile — keyboards, paper, coffee cups, hushed conversations through glass. The Super Bowl sounds massive, symphonic, broadcast-scale. The player lives in the intimate and reaches for the spectacle.

**ANALOG** vs. **DIGITAL**
The early 2000s sonic texture: the whir of rear-projection screens, the click of BlackBerry keyboards, the hum of CRT monitors in edit suites. But beneath it, the digital pulse of simulated audience sentiment, algorithmic cultural trends, the heartbeat of metrics shifting in real time.

**CONFIDENCE** vs. **DOUBT**
Music and SFX should oscillate between two emotional poles: the swaggering jazz of a successful pitch and the minor-key dread of a client frown. Every sound either builds the player up or asks "are you sure?"

The sonic palette is **warm, specific, and human**. No sci-fi bleeps. No fantasy swells. The closest reference is *the sound of ambition happening in a room* — Mad Men's mid-century cool meets The Social Network's laptop-driven urgency, filtered through the 2003 office aesthetic.

Every sound in this game answers one question: *Does this make the player feel the weight of creative authority under pressure?*

If it does, it belongs. If it does not, silence is better.

---

## 2. SONIC PALETTE & REFERENCES

### 2.1 Core Palette Description

**Texture**: Warm analog with digital punctuation. The base layer is **felt and physical** — wood furniture, paper sliding on desks, leather chair creaks, glass conference room doors, fabric rustling, human breath. The detail layer is **precise and modern** — UI clicks, notification chimes, keyboard taps, the electric hum of screens.

**Frequency Range**: The world lives in the **mid-range** — human voices, footsteps, office ambience. Low-end is reserved for moments of gravitas (client tension, Super Bowl broadcast). High-end sparkles are used sparingly for UI feedback, award notifications, and cultural moment triggers.

**Tonal Center**: The sonic world is tuned to **warm, slightly melancholic major** — confident but aware of its fragility. Think D major as home, with frequent visits to B minor when stakes rise. The game never sounds cynical or ironic. It sounds sincere about the cost of making things for other people.

**Dynamic Range**: Wide. Quiet moments (reading a brief at your desk, 30-40 dB ambient) contrast sharply with loud moments (Super Bowl broadcast climax, 80-90 dB orchestral swell). The player should feel the shift in stakes through volume and density alone.

### 2.2 Reference Tracks

#### Music References

1. **Vince Guaraldi Trio — "Linus and Lucy"**
   - *Why*: The confident, walking-bassline jazz that scores creative momentum. This is what a good pitch sounds like — swinging, tight, assured without being slick.
   - *Use case*: Presentation room underscore when the player enters a Gauntlet with high reputation and solid Pushback Points. The player is in control and the music knows it.

2. **Trent Reznor & Atticus Ross — "In Motion" (The Social Network OST)**
   - *Why*: The digital-analog hybrid texture, the hypnotic pulse, the feeling of work happening at night under deadline. Focused, obsessive, brilliant.
   - *Use case*: Edit suite ambience, production pipeline sequences, late-Q4 crunch periods when multiple campaigns converge.

3. **Brian Eno — "Music for Airports"**
   - *Why*: Spacious, contemplative, unobtrusive. The sound of waiting, of reflection, of looking at your agency and seeing what you built.
   - *Use case*: Year-end wrap screen, award ceremony sequences, moments of pause between campaigns.

4. **David Holmes — "I Heard Wonders" (Ocean's Eleven OST)**
   - *Why*: Heist-film cool. Confident, stylish, the feeling of pulling off a plan. This is the sound of a bold concept surviving the Gauntlet intact.
   - *Use case*: Post-Gauntlet victory cue when the player successfully defends a high-risk concept with multiple Pushback wins.

5. **Jon Brion — "Knock Yourself Out" (I Heart Huckabees OST)**
   - *Why*: Quirky, warm, slightly melancholic Americana with a dry wit. Sounds human and handmade.
   - *Use case*: Q1 client intake sequences, new team member introductions, lighter narrative moments.

6. **Thomas Newman — "Any Other Name" (American Beauty OST)**
   - *Why*: The ache of suburban yearning, the beauty of something ordinary becoming transcendent. The sound of caring too much about something that the world might not notice.
   - *Use case*: The moment when the player looks at a brilliant concept the client just killed. The music validates the loss.

#### SFX / Ambience References

1. **Mad Men (TV series) — Office ambience**
   - *Why*: The period-accurate texture of mid-century office life: typewriters, rotary phones, ice in glass, paper shuffling. UPFRONT is 40 years later but the *feeling* is the same.
   - *Use case*: General office ambience palette — update the tech (keyboards not typewriters, LCD hum not typewriter dings) but preserve the human-scale intimacy.

2. **Halt and Catch Fire (TV series) — Edit room ambience**
   - *Why*: The hum of machines, the focus of people working late, the feeling of building something fragile and important.
   - *Use case*: Edit suite, production pipeline, late-night work sessions.

3. **The West Wing (TV series) — Walk-and-talk hallway scenes**
   - *Why*: The rhythm of urgent conversation over footsteps, doors opening, the building itself as a sonic character.
   - *Use case*: Agency office navigation, inter-department movement, the feeling of momentum and busy-ness.

4. **Super Bowl Broadcast (actual NFL footage)**
   - *Why*: The real thing. Crowd roar, commentator cadence, ad break transitions, the massive spectacle of broadcast TV.
   - *Use case*: Super Bowl Sunday sequence — sample and process real broadcast ambience for authenticity.

### 2.3 Anti-References (What This Game Does NOT Sound Like)

- **Not**: Bombastic orchestral fantasy (Skyrim, God of War). This is not epic in scale — it is epic in stakes.
- **Not**: Hyper-polished corporate minimalism (Apple keynote sound design). This world has texture, dust, coffee stains.
- **Not**: Retro-synthwave pastiche (Hotline Miami, Drive). The 2000s were not the 80s. No neon nostalgia.
- **Not**: Quirky indie-game whimsy (Untitled Goose Game, Katamari). The tone is sincere, not ironic.
- **Not**: Silence-as-default (Inside, Limbo). This world is *alive* with human presence. Silence is a choice, not a baseline.

---

## 3. SFX DESIGN — ORGANIZED BY CATEGORY

All SFX are described with:
- **Name** — What to call it in implementation
- **Description** — What it sounds like
- **Trigger** — When it plays
- **Emotional Purpose** — Why it exists
- **Mix Priority** — Where it sits in the hierarchy (Critical / Feedback / Ambient)

---

### 3.1 UI / MENU LAYER

These are the sounds of interface interaction. They must be immediate, responsive, and satisfying without being intrusive. The aesthetic is **tactile and diegetic** — clicks feel like physical buttons, opens feel like folders or papers.

#### UI_Click_Primary
- **Description**: Soft mechanical click, like a luxury pen retracting. Warm mid-range (500-800 Hz fundamental), short decay (50ms).
- **Trigger**: Primary button press (approve concept, enter room, confirm allocation).
- **Emotional Purpose**: Confidence. Every decision feels considered.
- **Mix Priority**: Feedback

#### UI_Click_Secondary
- **Description**: Quieter tap, like a pencil on paper. Higher fundamental (1.2 kHz), even shorter decay (30ms).
- **Trigger**: Secondary actions (navigate tabs, cycle through options, dismiss notifications).
- **Emotional Purpose**: Non-intrusive responsiveness.
- **Mix Priority**: Feedback

#### UI_Click_Negative
- **Description**: Dull thud with slight distortion, like a button refusing to press. Low-mid (300 Hz), with a subtle dissonant overtone.
- **Trigger**: Invalid action, insufficient funds, locked option.
- **Emotional Purpose**: Gentle frustration. The game is saying "not yet."
- **Mix Priority**: Feedback

#### UI_Open_Document
- **Description**: Paper slide and settle. Realistic foley — the sound of pulling a printed brief from a folder and placing it on a desk.
- **Trigger**: Opening a brief, a concept pitch, a report.
- **Emotional Purpose**: Physicality. This is not data — it is a *thing* you hold.
- **Mix Priority**: Feedback

#### UI_Close_Document
- **Description**: Paper shuffle and soft slap. Slightly lower in pitch than Open, with more finality.
- **Trigger**: Closing a document, dismissing a screen.
- **Emotional Purpose**: Completion. You are done with this for now.
- **Mix Priority**: Feedback

#### UI_Tab_Slide
- **Description**: Smooth whoosh with a subtle card-flip texture. Low-end filtered out (high-pass at 300 Hz) to avoid muddiness.
- **Trigger**: Switching between UI tabs (Brief, Concept, Production, etc.).
- **Emotional Purpose**: Fluidity. The interface is responsive and elegant.
- **Mix Priority**: Feedback

#### UI_Notification_Neutral
- **Description**: Single marimba note (C5) with soft attack, medium sustain. Warm and non-alarming.
- **Trigger**: General notifications (new brief available, team member ready, quarter change).
- **Emotional Purpose**: Information without urgency.
- **Mix Priority**: Feedback

#### UI_Notification_Urgent
- **Description**: Two-note descending chime (G4 to D4) with slight dissonance between them. Faster attack than Neutral.
- **Trigger**: Deadline warnings, client calls, cash flow alerts.
- **Emotional Purpose**: Attention required. Not panic, but "handle this soon."
- **Mix Priority**: Feedback

#### UI_Notification_Success
- **Description**: Ascending three-note arpeggio (C4-E4-G4) on electric piano. Bright, warm, satisfying.
- **Trigger**: Campaign approved, award nomination, reputation milestone reached.
- **Emotional Purpose**: Reward. The game validates your success.
- **Mix Priority**: Feedback

#### UI_Notification_Failure
- **Description**: Single low piano note (A2) with long reverb tail. Mournful but not dramatic.
- **Trigger**: Campaign killed, client lost, Gauntlet walked away from.
- **Emotional Purpose**: Acknowledgment of loss. The game sits with you in the moment.
- **Mix Priority**: Feedback

#### UI_Slider_Drag
- **Description**: Subtle granular texture, like dragging a stylus over fine sandpaper. Pitch shifts slightly with slider position (lower at 0%, higher at 100%).
- **Trigger**: Dragging budget allocation sliders in Production Pipeline.
- **Emotional Purpose**: Tactile feedback. The player feels the budget moving.
- **Mix Priority**: Feedback

#### UI_Slider_Release
- **Description**: Soft "snap" like a slider locking into place. Very short (20ms), mid-range click.
- **Trigger**: Releasing a slider after allocation.
- **Emotional Purpose**: Finality. The decision is locked in.
- **Mix Priority**: Feedback

#### UI_Reputation_Shift
- **Description**: Slow upward/downward pitch sweep (portamento) over 2 seconds, mixed with a subtle shimmer. Upward for positive rep change (A3 to A4), downward for negative (A4 to A3).
- **Trigger**: Post-campaign reputation update.
- **Emotional Purpose**: The player feels their agency's identity shifting over time.
- **Mix Priority**: Feedback

---

### 3.2 OFFICE AMBIENCE

The agency is a living space. Ambience provides **presence and place**. The player should always know where they are by sound alone.

#### AMB_Office_General
- **Description**: Low-level office hum. Distant conversations (unintelligible), keyboard clacks at varying distances, occasional phone ring (muted, 2-3 per minute), fluorescent light buzz (60 Hz hum, subtle), HVAC white noise. 8-10 layered elements in randomized timing. Total level: 35-40 dB.
- **Trigger**: Always active when viewing the main office screen.
- **Emotional Purpose**: The agency is alive. People are working.
- **Mix Priority**: Ambient

#### AMB_Office_Late_Night
- **Description**: Stripped-down version of General. Only 2-3 keyboards, one distant voice, heavier HVAC presence. Crickets or street ambience faintly audible through windows. Occasional desk lamp buzz. Total level: 30-35 dB.
- **Trigger**: Active when viewing office screen during Q4 crunch or late-hour work sessions.
- **Emotional Purpose**: Loneliness and focus. The player is one of the last people here.
- **Mix Priority**: Ambient

#### AMB_Presentation_Room
- **Description**: Dead acoustic space. Very low ambient noise — slight AC hum, the hum of a rear-projection screen (120 Hz + harmonics). No keyboards, no distant voices. The room is **waiting**.
- **Trigger**: Active during Approval Gauntlet sequences.
- **Emotional Purpose**: Tension through absence. The silence between words matters here.
- **Mix Priority**: Ambient

#### AMB_Edit_Suite
- **Description**: Machine hum. Multiple monitors running (various CRT whines at 15.7 kHz harmonics, audible but filtered to avoid harshness), hard drive spin-up/spin-down cycles, cooling fan white noise. Occasional mouse click. One chair creak every 15-20 seconds.
- **Trigger**: Active during Production Pipeline screen.
- **Emotional Purpose**: Focus and craft. This is where the work gets made.
- **Mix Priority**: Ambient

#### AMB_Bullpen_Stressed
- **Description**: Higher density version of Office_General. Overlapping voices (slightly louder), more frequent phone rings, footsteps, door slams. Occasional sigh or frustrated "damn it." Total level: 45-50 dB.
- **Trigger**: Active when Team Cohesion is in Friction or Meltdown state, or during Q4 deadline convergence.
- **Emotional Purpose**: Pressure. Everyone is feeling it.
- **Mix Priority**: Ambient

#### AMB_Client_Office_Lobby
- **Description**: Upscale corporate ambience. Elevator ding in distance, muted classical music (muzak-style, barely audible), receptionist keyboard, the subtle hum of expensive HVAC. Everything is polished and cold.
- **Trigger**: Active during client pitch sequences (stretch goal / narrative moments).
- **Emotional Purpose**: You are in their world now. It is not comfortable.
- **Mix Priority**: Ambient

---

### 3.3 TEAM / CREATIVE LAYER

Sounds associated with individual creatives and team interactions. These humanize the roster.

#### TEAM_Keyboard_Standard
- **Description**: Mechanical keyboard typing burst, 3-5 seconds, irregular rhythm. Medium-loud. The sound of someone working.
- **Trigger**: Background element in office ambience, more prominent when viewing team assignments.
- **Emotional Purpose**: Presence. Your team is doing the work.
- **Mix Priority**: Ambient

#### TEAM_Keyboard_Frustrated
- **Description**: Harder, faster typing burst followed by a sharp DELETE key mash (heavier mechanical thunk). Ends with a pause.
- **Trigger**: Plays occasionally when a high-Ego creative is on a low-risk brief or when Team Cohesion is in Meltdown.
- **Emotional Purpose**: Characterization. This person is not happy.
- **Mix Priority**: Feedback

#### TEAM_Chair_Lean_Back
- **Description**: Aeron chair creak, slow squeak as someone leans back. The sound of satisfaction or exhaustion.
- **Trigger**: Post-concept generation, post-Gauntlet approval.
- **Emotional Purpose**: Human body language through sound.
- **Mix Priority**: Ambient

#### TEAM_Chair_Spin
- **Description**: Office chair rotation with slight wheel rattle. Playful, quick.
- **Trigger**: Rare. Plays during positive morale events or when team chemistry is Synergy and they complete work ahead of schedule.
- **Emotional Purpose**: Joy. This team is vibing.
- **Mix Priority**: Ambient

#### TEAM_Sigh_Relief
- **Description**: Human exhale, subtle, not exaggerated. The sound of tension releasing.
- **Trigger**: When a concept is approved after a tense Gauntlet, or when a campaign completes successfully.
- **Emotional Purpose**: Shared relief. The player and the team both feel it.
- **Mix Priority**: Feedback

#### TEAM_Sigh_Disappointment
- **Description**: Shorter, sharper exhale with a slight descending vocal tone (almost a grunt).
- **Trigger**: When a concept is killed in the Gauntlet or when the player accepts a De-Risk note that guts Originality.
- **Emotional Purpose**: Loss. Someone on the team cared about what was just cut.
- **Mix Priority**: Feedback

#### TEAM_Applause_Small
- **Description**: 3-4 people clapping briefly (2-3 seconds), natural room reverb, not polished. The sound of a small victory in an office.
- **Trigger**: Award win notification, major client signing, reputation milestone.
- **Emotional Purpose**: Celebration that feels earned and intimate, not bombastic.
- **Mix Priority**: Feedback

#### TEAM_Murmur_Positive
- **Description**: Overlapping approving hums, a quiet "yeah," a whispered "nice." 4-5 voices, indistinct.
- **Trigger**: When the player selects a high-Originality or high-Emotion concept that aligns with team Taste.
- **Emotional Purpose**: The team believes in this one.
- **Mix Priority**: Feedback

#### TEAM_Murmur_Skeptical
- **Description**: Uncertain "hmm," a throat clear, a pause that lasts too long. 3-4 voices, hesitant.
- **Trigger**: When the player selects a concept with low stats or heavy client compromise.
- **Emotional Purpose**: Doubt. The team is unsure about this choice.
- **Mix Priority**: Feedback

---

### 3.4 CLIENT / GAUNTLET LAYER

The most critical SFX in the game. These are the sounds of negotiation, power, and compromise.

#### CLIENT_Enter_Room
- **Description**: Conference room door open (glass, heavy, with pneumatic hiss), footsteps (dress shoes on hard floor, 4-5 steps), briefcase or bag set down (leather thud).
- **Trigger**: Beginning of Approval Gauntlet sequence.
- **Emotional Purpose**: The client is here. The stakes are active.
- **Mix Priority**: Feedback

#### CLIENT_Sit_Down
- **Description**: Chair pull (wood or metal scrape), body settle (fabric rustle, chair slight creak).
- **Trigger**: Immediately after Enter_Room, before dialogue begins.
- **Emotional Purpose**: Ritual. Every Gauntlet starts the same way.
- **Mix Priority**: Feedback

#### CLIENT_Paper_Shuffle
- **Description**: Papers being moved, the sound of someone pretending to review while thinking.
- **Trigger**: Between Gauntlet rounds, during client "consideration" pauses.
- **Emotional Purpose**: Real-time body language. The client is processing.
- **Mix Priority**: Feedback

#### CLIENT_Pen_Tap
- **Description**: Ballpoint pen tapping on a desk or notepad, rhythmic, 3-5 taps.
- **Trigger**: When client Risk Tolerance is low and they are resisting a Pushback.
- **Emotional Purpose**: Impatience. The client is not convinced.
- **Mix Priority**: Feedback

#### CLIENT_Hmm_Positive
- **Description**: Approving hum, rising intonation (A3 to C4), 0.5 seconds.
- **Trigger**: When the player accepts a client note or presents a concept aligned with client priorities.
- **Emotional Purpose**: You are giving them what they want. They relax.
- **Mix Priority**: Feedback

#### CLIENT_Hmm_Negative
- **Description**: Disapproving hum, descending intonation (A3 to F3), slightly longer (0.7 seconds), with a subtle vocal fry.
- **Trigger**: When the player attempts a Pushback that fails the Persuasion Check.
- **Emotional Purpose**: Resistance. The client is not moved.
- **Mix Priority**: Feedback

#### CLIENT_Laugh_Relieved
- **Description**: Single chuckle, genuine, slightly nervous. 1 second.
- **Trigger**: When the player successfully Compromises after a tense round, or when a Pushback succeeds with high margin.
- **Emotional Purpose**: The tension breaks. Both parties found common ground.
- **Mix Priority**: Feedback

#### CLIENT_Phone_Check
- **Description**: Subtle buzz (phone vibrate on table), followed by the faint click of the phone being picked up and set back down.
- **Trigger**: When a Gauntlet round is taking too long or when Client Trust is below 40.
- **Emotional Purpose**: Disinterest. The client is losing patience.
- **Mix Priority**: Feedback

#### CLIENT_Lean_Forward
- **Description**: Chair creak with fabric rustle, hands placed on table (soft thud x2).
- **Trigger**: When the player presents a high-stat concept or when a Pushback succeeds decisively.
- **Emotional Purpose**: Engagement. The client is interested.
- **Mix Priority**: Feedback

#### CLIENT_Stand_Up_Abrupt
- **Description**: Chair scrape (fast, harsh), footsteps (2-3 quick steps).
- **Trigger**: When the player selects Walk Away in the Gauntlet.
- **Emotional Purpose**: Shock and anger. The negotiation has collapsed.
- **Mix Priority**: Critical

#### CLIENT_Door_Slam
- **Description**: Heavy glass door close with force, slight rattle of frame.
- **Trigger**: End of Walk Away sequence.
- **Emotional Purpose**: Finality. This relationship is damaged.
- **Mix Priority**: Critical

#### CLIENT_Handshake
- **Description**: Two palms clasping, brief. Confident, mutual.
- **Trigger**: End of successful Gauntlet when concept is approved.
- **Emotional Purpose**: Partnership. You did it together.
- **Mix Priority**: Feedback

---

### 3.5 PRODUCTION / CAMPAIGN LAYER

Sounds that represent the abstract process of making an ad. These are more conceptual, less literal.

#### PROD_Budget_Allocate
- **Description**: Mechanical "chunk" sound, like a token dropping into a slot. Pitched based on category (Casting = higher pitch, VFX = mid, Edit = lower). 100-150ms.
- **Trigger**: Each time the player allocates budget to a production category.
- **Emotional Purpose**: Spending money feels tangible.
- **Mix Priority**: Feedback

#### PROD_Timeline_Advance
- **Description**: Soft mechanical tick, like a film reel advancing one frame. 30ms, mid-range.
- **Trigger**: Visual timeline progress during Production Pipeline.
- **Emotional Purpose**: Time is moving. The work is happening.
- **Mix Priority**: Ambient

#### PROD_Render_Complete
- **Description**: Satisfying "lock-in" sound, like a vault closing. Low-mid thunk + high metallic shimmer tail.
- **Trigger**: When production is finalized and the ad is ready to air.
- **Emotional Purpose**: Completion. The work is done.
- **Mix Priority**: Feedback

#### PROD_Ambition_Warning
- **Description**: Subtle dissonant tone cluster (C-C#-D played together), quiet, with slow fade-in. Uncomfortable but not loud.
- **Trigger**: When Ambition Gap penalty is active (budget cannot support concept ambition).
- **Emotional Purpose**: Unease. Something is wrong here.
- **Mix Priority**: Feedback

#### PROD_Overbudget_Alert
- **Description**: Sharp two-tone alarm (440 Hz + 554 Hz, classic alarm interval), short burst (0.5 sec), not piercing but clear.
- **Trigger**: When the player attempts to allocate more than 100% of available budget.
- **Emotional Purpose**: Stop. This is not allowed.
- **Mix Priority**: Critical

---

### 3.6 BROADCAST / REACTION LAYER

The sounds of ads airing and the world responding. This is where intimate becomes spectacle.

#### BROADCAST_TV_Static
- **Description**: Brief analog TV static burst (200ms), band-limited to avoid harshness (high-pass 800 Hz, low-pass 8 kHz).
- **Trigger**: Transition into ad broadcast sequence.
- **Emotional Purpose**: Medium shift. You are now on television.
- **Mix Priority**: Feedback

#### BROADCAST_Ad_Play_Start
- **Description**: The sound of broadcast silence — a very specific 0.2 seconds of absolute quiet before content begins. Then a subtle low-end "bloom" (40 Hz sine fade-in over 1 sec).
- **Trigger**: The moment the ad begins playing in the broadcast screen.
- **Emotional Purpose**: Breath held. The world is watching.
- **Mix Priority**: Critical

#### BROADCAST_Audience_Laugh
- **Description**: Crowd laughter, 20-30 people, natural and varied. Starts quiet, peaks at 2 sec, fades over 4 sec total. Warm, genuine.
- **Trigger**: Plays during broadcast if ad Humor stat is above 65.
- **Emotional Purpose**: It is working. They get it.
- **Mix Priority**: Feedback

#### BROADCAST_Audience_Aww
- **Description**: Collective empathetic sigh, 15-20 people, soft and sincere. 2-3 seconds.
- **Trigger**: Plays during broadcast if ad Emotion stat is above 70.
- **Emotional Purpose**: You made them feel something.
- **Mix Priority**: Feedback

#### BROADCAST_Audience_Confused
- **Description**: Murmurs, uncertain "huh?" sounds, 10-15 people. Overlapping, indistinct. 2 seconds.
- **Trigger**: Plays during broadcast if ad Originality is above 75 but Brand Clarity is below 40.
- **Emotional Purpose**: Ambiguity. They do not know what they just saw.
- **Mix Priority**: Feedback

#### BROADCAST_Audience_Silence
- **Description**: Not literal silence — a tense room tone. Breath, subtle movement, but no reaction.
- **Trigger**: Plays during broadcast if Audience Score is below 35.
- **Emotional Purpose**: Failure. The ad landed flat.
- **Mix Priority**: Feedback

#### BROADCAST_Social_Buzz
- **Description**: Layered notification chimes (5-10 overlapping, various pitches, chaotic but not harsh), mixed with typing burst SFX, subtle human voice textures (laughing, gasping). 4-6 seconds.
- **Trigger**: Plays post-broadcast if Audience Score is above 75 or if Polarization event triggers.
- **Emotional Purpose**: Virality. The internet is talking about this.
- **Mix Priority**: Feedback

#### BROADCAST_Phone_Ring_Client
- **Description**: Landline phone ring (classic bell, not digital), 2-3 rings, slightly distorted/urgent.
- **Trigger**: Monday Morning sequence when client is calling to respond to campaign results.
- **Emotional Purpose**: Reckoning. Here comes the verdict.
- **Mix Priority**: Critical

---

### 3.7 SUPER BOWL LAYER

The Super Bowl is mechanically and sonically distinct. These sounds exist nowhere else in the game.

#### SB_Countdown_Tick
- **Description**: CRT monitor tick (the sound of an old TV warming up + a metronome at 60 BPM), clean and precise.
- **Trigger**: During pre-Super-Bowl countdown screen.
- **Emotional Purpose**: Ritual and anticipation. This moment is different.
- **Mix Priority**: Feedback

#### SB_Crowd_Roar_Stadium
- **Description**: Massive crowd ambience, 60,000+ people, low-end rich (spectral emphasis 150-400 Hz), chaotic and alive. 10+ seconds loopable.
- **Trigger**: Background ambience during Super Bowl broadcast sequence.
- **Emotional Purpose**: Scale. This is the biggest stage.
- **Mix Priority**: Ambient

#### SB_Commentator_Murmur
- **Description**: Two male voices, indistinct, professional cadence, the rhythm of sports commentary without intelligible words. Occasional "and we're back" type phrases barely audible.
- **Trigger**: During Super Bowl pre-ad and post-ad commentary transitions.
- **Emotional Purpose**: Authenticity. This feels like the real broadcast.
- **Mix Priority**: Ambient

#### SB_Ad_Slot_Transition
- **Description**: Broadcast "whoosh" — the sound of a network transition, part digital beep (1 kHz, 100ms) + part sub-bass drop (60 Hz, 300ms fade).
- **Trigger**: Moment when "your" ad begins during Super Bowl.
- **Emotional Purpose**: Threshold crossing. This is it.
- **Mix Priority**: Critical

#### SB_Audience_Reaction_Huge
- **Description**: Explosive crowd response — laughter, cheers, gasps, all layered. 80+ people, massive stereo width, 8-10 seconds with natural decay.
- **Trigger**: Plays during Super Bowl ad if Audience Score is above 85.
- **Emotional Purpose**: Triumph. You made something that moved a hundred million people.
- **Mix Priority**: Critical

#### SB_Monday_Morning_Theme
- **Description**: A specific musical cue (see Music section 4.3), but also: coffee maker gurgling, office door opening, footsteps approaching. Diegetic scene-setting.
- **Trigger**: Transition into Monday Morning report sequence.
- **Emotional Purpose**: Return to reality. The spectacle is over. Now comes the reckoning.
- **Mix Priority**: Feedback

---

### 3.8 AWARD / MILESTONE LAYER

Sounds that mark achievement and legacy.

#### AWARD_Nomination_Announced
- **Description**: Envelope open (paper tear), pause (1 sec), single piano note (E4) with long reverb tail.
- **Trigger**: Award nomination notification screen.
- **Emotional Purpose**: Recognition. Your work mattered enough to be seen.
- **Mix Priority**: Feedback

#### AWARD_Win_Announced
- **Description**: Rising orchestral swell (strings, 2 seconds, C major to G major resolution) + applause (50+ people, auditorium reverb, 6 seconds).
- **Trigger**: Award win notification screen.
- **Emotional Purpose**: Validation. You won.
- **Mix Priority**: Feedback

#### AWARD_Trophy_Place
- **Description**: Heavy object (metal + wood base) set down on shelf. Solid, final thud.
- **Trigger**: When award trophy is added to office display (visual + audio sync).
- **Emotional Purpose**: Permanence. This is part of your history now.
- **Mix Priority**: Feedback

#### MILESTONE_Reputation_Tier
- **Description**: Ascending harp glissando (2 octaves, 1.5 seconds) + soft orchestral hit (no percussion, just sustained strings).
- **Trigger**: When agency Reputation crosses a tier threshold (25, 45, 65, 80).
- **Emotional Purpose**: Ascension. You have reached a new level.
- **Mix Priority**: Feedback

#### MILESTONE_Legacy_Moment
- **Description**: Solo piano playing a simple, bittersweet melody (4-bar phrase, D major with borrowed minor chords), with room reverb. No accompaniment.
- **Trigger**: When a campaign creates a "legacy moment" (Legendary Audience Score, career-defining event).
- **Emotional Purpose**: Reflection. This is the moment you will remember.
- **Mix Priority**: Feedback

---

### 3.9 YEAR / CALENDAR LAYER

Sounds that mark the passage of time and the rhythm of the annual cycle.

#### YEAR_Quarter_Change
- **Description**: Page turn (calendar page), soft and deliberate, followed by a quiet bell tone (G4, 1 second sustain).
- **Trigger**: Transition from Q1 to Q2, Q2 to Q3, etc.
- **Emotional Purpose**: Time moves forward. A new chapter begins.
- **Mix Priority**: Feedback

#### YEAR_Clock_Tick
- **Description**: Wall clock second hand, steady and neutral. Not loud. Background texture.
- **Trigger**: Active during time-sensitive sequences (deadline warnings, countdown timers).
- **Emotional Purpose**: Pressure. Time is finite.
- **Mix Priority**: Ambient

#### YEAR_New_Year_Bell
- **Description**: Single deep bell toll (C2, 4-second natural decay, warm and resonant).
- **Trigger**: Transition from Year End screen to Year 1 / Year 2 / etc. start.
- **Emotional Purpose**: Renewal. The cycle begins again.
- **Mix Priority**: Feedback

#### YEAR_End_Ambience
- **Description**: Quiet office at night. One distant keyboard. Distant traffic outside. The hum of the building settling. 20-30 dB, very sparse.
- **Trigger**: Year End wrap screen, post-awards, pre-new year.
- **Emotional Purpose**: Solitude and reflection. You are alone with what you built.
- **Mix Priority**: Ambient

---

### 3.10 CRISIS / TENSION LAYER

Sounds for moments when things go wrong.

#### CRISIS_Cash_Flow_Warning
- **Description**: Low drone (G2, sawtooth wave, slow LFO wobble at 0.3 Hz), unsettling but not piercing.
- **Trigger**: When cash reserves drop below 20% of monthly expenses.
- **Emotional Purpose**: Dread. Money is running out.
- **Mix Priority**: Feedback

#### CRISIS_Client_Lost
- **Description**: Phone hang-up (dial tone, then dead air), followed by a descending minor third on piano (E4 to C#4).
- **Trigger**: When a client relationship ends (fired, walked away, budget cut).
- **Emotional Purpose**: Loss. A relationship is over.
- **Mix Priority**: Critical

#### CRISIS_Team_Quit
- **Description**: Door close (not slam — quiet, final), footsteps receding, fade to silence.
- **Trigger**: When a team member leaves the agency.
- **Emotional Purpose**: Departure. Someone you worked with is gone.
- **Mix Priority**: Critical

#### CRISIS_Deadline_Missed
- **Description**: Alarm clock buzz (analog, harsh, 440 Hz square wave), 2 seconds, abruptly cut.
- **Trigger**: When a campaign misses its deadline.
- **Emotional Purpose**: Failure. Time ran out.
- **Mix Priority**: Critical

#### CRISIS_Controversy_Event
- **Description**: Overlapping news broadcast fragments (voices, not intelligible), mixed with phone rings (3-4 overlapping), mixed with notification chimes (chaotic). 5-6 seconds, high density, then sudden cut to silence.
- **Trigger**: When a Polarization roll triggers a Controversy Event.
- **Emotional Purpose**: Chaos. The world is reacting and you are at the center.
- **Mix Priority**: Critical

---

## 4. MUSIC BRIEF

### 4.1 Musical Identity & Style

UPFRONT's music is **mid-century modern jazz meets contemporary minimalism**. Think Vince Guaraldi's warm piano trio work crossed with the restrained electronic textures of Trent Reznor's *The Social Network* score, filtered through Jon Brion's quirky humanity.

The instrumentation is:
- **Core**: Acoustic piano (grand, not upright), upright bass (walking basslines, pizzicato), drum kit (brushes primarily, sticks only for high-tension moments)
- **Accent**: Muted trumpet (for cool confidence), vibraphone (for warmth and nostalgia), Rhodes electric piano (for late-night work sessions)
- **Texture**: Analog synth pads (Moog-style, warm and thick, never harsh), subtle electronic pulses (for UI and data layers), tape hiss and vinyl crackle (barely audible, textural glue)

The harmonic language is:
- **Tonal center**: D major / B minor axis (warm but ambivalent)
- **Progressions**: Classic jazz ii-V-I and tritone substitutions for sophistication; occasional modal ambiguity (Dorian, Mixolydian) for modern edge
- **Avoid**: Schmaltz, bombast, irony. Every note is sincere.

The tempo range:
- **Chill / Reflective**: 70-85 BPM (office work, reading briefs, year-end screens)
- **Momentum / Working**: 95-115 BPM (concept generation, production, mid-game flow)
- **Tension / Climax**: 120-140 BPM (Gauntlet stress, deadline crunch, Super Bowl lead-up)

The dynamic range:
- Music should sit *behind* the player's focus most of the time (conversational level, -18 to -24 LUFS)
- Swell forward during key moments (Gauntlet victories, Super Bowl broadcast, award wins) to -12 to -15 LUFS
- Fade to near-silence during critical decision moments (Pushback choice, Walk Away consideration) — let the player think

### 4.2 Adaptive Music System Design

UPFRONT's music is **layered and reactive**, not linear. The system uses:

**Horizontal Resequencing** (different cues for different contexts):
- Office Work Theme
- Presentation Room Theme (Gauntlet music)
- Edit Suite Theme
- Super Bowl Theme
- Reflective / Year End Theme

**Vertical Remixing** (layers added/removed based on game state):
Each theme has 3-4 stems that crossfade in/out based on parameters:
- **Base Layer** (always playing): Piano + bass + light ambience
- **Momentum Layer** (added when player is actively working, campaigns in progress): Drums (brushes)
- **Tension Layer** (added when stakes rise — low Client Trust, Gauntlet intensity, deadline pressure): Muted trumpet or Rhodes, dissonant pad
- **Triumph Layer** (added when player succeeds — Pushback win, campaign success, award): Vibraphone, ascending melodic motif

**Parameter Mapping**:
| Game State | Music Response |
|---|---|
| Client Trust > 70 | Add Triumph Layer, increase tempo +5%, major key center |
| Client Trust < 40 | Add Tension Layer, decrease tempo -5%, shift to minor/modal |
| Team Cohesion = Synergy | Clean mix, clear piano melody, steady pulse |
| Team Cohesion = Friction | Slightly detuned elements, offbeat accents, harmonic tension |
| Team Cohesion = Meltdown | Tension Layer forced on, dissonant cluster chords, irregular rhythm |
| Deadline < 1 week | Add Tension Layer, increase tempo, ticking hi-hat added |
| Campaign in Production | Add Momentum Layer |
| Idle / Reading | Base Layer only, tempo slowest |
| Gauntlet Round 1-2 | Base + light Momentum |
| Gauntlet Round 3+ | Base + Momentum + Tension, volume increases +3 dB |
| Gauntlet Pushback Success | Brief Triumph Layer swell (4 bars), then return |
| Gauntlet Pushback Fail | Dissonant piano cluster, Tension Layer intensifies |
| Walk Away Selected | All layers cut except solo piano (unresolved phrase, hangs on 7th chord) |
| Super Bowl Countdown | Tempo locked to 60 BPM, minimalist pulse, building tension |
| Super Bowl Ad Airs | Full orchestral swell (NOT jazz — this is the spectacle moment, temporary genre shift) |

### 4.3 Individual Music Cues

#### MUS_Office_Work_Theme "The Bullpen"
- **Description**: Mid-tempo jazz trio (piano, bass, brushed drums). Walking bassline in D major, piano comps simple II-V-I progressions, melody is sparse and conversational. Vibraphone occasionally doubles the melody. Warm, focused, unobtrusive.
- **Length**: 2:30 loopable
- **Stems**: Piano/Bass (base), Drums (momentum), Vibes (triumph)
- **Emotional Purpose**: This is the sound of your agency working. Calm, human, alive.
- **Reference**: Vince Guaraldi — "Skating," but slightly slower and more introspective.

#### MUS_Presentation_Room_Theme "The Pitch"
- **Description**: Cool jazz with muted trumpet lead. Piano and bass lay down a steady groove (Bb major, medium swing), trumpet plays a confident melodic line. No drums initially (Base Layer), brushed hi-hat and snare added in Momentum Layer, Rhodes harmonic pad added in Tension Layer.
- **Length**: 3:00 loopable
- **Stems**: Piano/Bass (base), Trumpet (momentum), Rhodes Pad (tension), Vibes (triumph)
- **Emotional Purpose**: Confidence and persuasion. This is your arena.
- **Reference**: Miles Davis — "So What" energy, but warmer and less icy.

#### MUS_Edit_Suite_Theme "Late Shift"
- **Description**: Minimalist electronic-acoustic hybrid. Rhodes electric piano plays a repeating four-chord progression (Dm7 - Gm7 - Am7 - Fmaj7, slow arpeggios). Analog synth pad drones underneath (D fundamental). Subtle electronic pulse (dotted eighth note, filtered white noise) in Momentum Layer. Upright bass plays whole notes in Tension Layer.
- **Length**: 4:00 loopable
- **Stems**: Rhodes/Pad (base), Pulse (momentum), Bass (tension)
- **Emotional Purpose**: Focus and craft. Hypnotic, slightly melancholic, the sound of work at midnight.
- **Reference**: Trent Reznor & Atticus Ross — "In Motion," but with more organic warmth.

#### MUS_Gauntlet_Tension_Rise "The Ask"
- **Description**: Stinger cue (not loopable). Solo piano plays a rising chromatic line over 8 bars, harmonized in thirds, building from ppp to mf. Ends on an unresolved dominant 7th chord (A7, leading to D major that never comes).
- **Length**: 20 seconds
- **Trigger**: Plays when player selects Pushback and the Persuasion Check begins.
- **Emotional Purpose**: Suspense. The outcome is unknown.
- **Reference**: Thomas Newman's string suspensions, but on piano.

#### MUS_Gauntlet_Victory "Small Win"
- **Description**: Stinger cue. Four-bar phrase: piano and vibes in unison play an ascending major arpeggio (D-F#-A-D) resolving to a I-IV-I cadence. Brushes play a quick fill on the resolution. Warm, satisfying, not bombastic.
- **Length**: 8 seconds
- **Trigger**: Plays when a Pushback succeeds or when a Gauntlet ends with concept approved.
- **Emotional Purpose**: Relief and validation. You won the argument.
- **Reference**: Pixar "discovery" motifs — simple, clear, earned.

#### MUS_Gauntlet_Defeat "Concession"
- **Description**: Stinger cue. Solo piano plays a descending minor phrase (Bm to F#m, 4 bars, slow). No resolution. Fades into silence.
- **Length**: 10 seconds
- **Trigger**: Plays when the player accepts a harsh client note or when a Pushback fails badly.
- **Emotional Purpose**: Disappointment. Something was lost here.
- **Reference**: Thomas Newman — "Any Other Name" melancholy.

#### MUS_Super_Bowl_Countdown "48 Hours"
- **Description**: Minimalist pulse. Single piano note (D, octaves, metronomic at 60 BPM). Analog synth drone slowly fades in underneath (D fundamental, building over 90 seconds). At 60 seconds remaining, light percussion added (brushes on snare rim, matching pulse). At 30 seconds, bass enters (whole notes, D-C-Bb-A descending over 4 bars, looping).
- **Length**: 3:00 non-looping (builds continuously)
- **Trigger**: Pre-Super Bowl countdown screen.
- **Emotional Purpose**: Anticipation building to unbearable. This is the threshold.
- **Reference**: Jóhann Jóhannsson — "Arrival to Earth" minimalism.

#### MUS_Super_Bowl_Broadcast "The Big Game"
- **Description**: Full orchestral piece (strings, brass, timpani, piano). NOT jazz — this is the one moment the genre shifts to match the spectacle. Begins with a massive orchestral hit (fff, C major chord, all sections), then a triumphant ascending brass melody over driving string ostinato. Builds to a peak at 1:30, sustains, then cuts to total silence at 2:00 (when the ad "airs").
- **Length**: 2:00 non-looping
- **Trigger**: Super Bowl ad slot transition, leading up to player's ad airing.
- **Emotional Purpose**: THIS IS THE SUPER BOWL. Maximum spectacle. The player's heart should be pounding.
- **Reference**: John Williams — Olympic fanfares, but modern and less militaristic.

#### MUS_Super_Bowl_Reaction "Monday Morning"
- **Description**: Return to jazz. Solo piano (no accompaniment) plays a simple, reflective melody in D major. Slow, deliberate, each note given space. At 0:45, bass enters quietly (walking line, cautious). At 1:15, brushes enter (light, almost apologetic). The melody never resolves — it just... continues.
- **Length**: 2:00 loopable
- **Trigger**: Monday Morning post-Super Bowl report screen.
- **Emotional Purpose**: The spectacle is over. Now comes the reckoning. Regardless of outcome, there is a bittersweet return to reality.
- **Reference**: Bill Evans — "Peace Piece" contemplative simplicity.

#### MUS_Award_Ceremony "Recognition"
- **Description**: String quartet (2 violins, viola, cello) playing a gentle, ascending melody in G major. Classical form, warm and elegant, not showy. At the resolution (award win), a solo trumpet plays a 4-note fanfare (G-B-D-G), then the strings swell into a major cadence.
- **Length**: 1:30 non-looping
- **Trigger**: Award ceremony screen (nomination version cuts off before trumpet; win version plays full).
- **Emotional Purpose**: Prestige and validation. This is art being recognized by peers.
- **Reference**: Aaron Copland — "Appalachian Spring" Americana warmth, scaled down.

#### MUS_Year_End_Theme "What We Built"
- **Description**: Solo piano and distant strings. Piano plays a simple, bittersweet melody in D major/B minor (shifts between both). Melody is introspective, nostalgic, unresolved. Strings enter at 1:00 (long, sustained pads, no melody). The piece never climaxes — it just exists, like a memory.
- **Length**: 2:30 loopable
- **Trigger**: Year End wrap screen.
- **Emotional Purpose**: Reflection. The player looks at what they built this year — the wins, the compromises, the losses. The music does not judge. It just sits with them.
- **Reference**: Max Richter — "On the Nature of Daylight" emotional restraint.

#### MUS_Crisis_Theme "Freefall"
- **Description**: Dissonant ambient piece. Low drone (A, detuned slightly with beating at 4 Hz), atonal piano fragments (no melody, just clusters and single notes in no particular rhythm), distant processed breath sounds, irregular heartbeat pulse (sub-bass, 40 Hz, slow). Deeply unsettling but not loud.
- **Length**: 2:00 loopable
- **Trigger**: Cash crisis, major client loss, team mass exodus — catastrophic events.
- **Emotional Purpose**: Dread. The agency is in danger.
- **Reference**: Hildur Guðnadóttir — "Joker" score textures.

---

## 5. ADAPTIVE AUDIO SYSTEM DESIGN

### 5.1 Music Implementation Structure

UPFRONT uses a **stem-based adaptive music system** with real-time mixing. Each music theme consists of 3-4 stems (Base, Momentum, Tension, Triumph) that are:

- Recorded and mixed separately
- Sample-rate and bar-length synced (all stems are identical length, tempo-locked)
- Crossfaded in/out via volume automation (fade time: 2-4 bars, depending on tempo, to avoid jarring transitions)
- Controlled by game state parameters (Client Trust, Team Cohesion, deadline proximity, Gauntlet state, etc.)

**Middleware**: Recommend FMOD or Wwise.

**Implementation Notes**:
- All music stems should be 24-bit 48kHz WAV files, mixed at -6dB headroom for dynamic layering
- Loops must be sample-accurate (zero-crossing edits) to avoid clicks
- Parameter smoothing: All game state → music parameter mappings should use smoothed interpolation (0.5-1 second ramp) to avoid abrupt jumps
- Music should duck (reduce by -6 to -9 dB) during critical dialogue moments (client speech in Gauntlet, major notifications) and return smoothly

### 5.2 SFX Implementation Structure

**Categories & Priority Levels**:

UPFRONT's mix has three priority tiers:

1. **Critical** (always heard, never masked): Client reactions in Gauntlet, crisis events, Super Bowl key moments. Max 2-3 critical SFX playing simultaneously. If a new critical SFX triggers, it ducks all other audio by -12dB.

2. **Feedback** (important but can be masked if density is high): UI interactions, team reactions, notifications, most gameplay feedback. Max 8-10 feedback SFX simultaneously. If limit exceeded, oldest SFX is faded out early.

3. **Ambient** (foundational, always present but low in mix): Office ambience, background keyboards, distant voices, HVAC hum. These are continuous layers, not one-shots.

**Mixing Targets** (pre-master):
- Ambient layer: -30 to -24 LUFS
- Feedback layer: -18 to -12 LUFS
- Critical layer: -12 to -6 LUFS
- Music: -18 to -15 LUFS (dynamic, swells to -12 LUFS at peaks)

**Master Output**: -14 LUFS integrated, -1dB true peak (industry standard for game audio, comfortable for long sessions)

### 5.3 Spatial Audio Design

UPFRONT is a 2D-interface game, but spatial audio adds depth:

**Stereo Positioning**:
- UI sounds: Center-weighted (90% center, 10% stereo width for "air")
- Office ambience: Full stereo width — different elements panned across field (keyboard left-30°, phone ring right-45°, distant conversation center-left, etc.)
- Gauntlet room: Narrow stereo (player is "in the room," not observing it) — client voice slightly right of center (implies they are across the table), player's own sounds (paper, breathing) slightly left
- Super Bowl broadcast: Exaggerated stereo width for crowd, center-focused for commentators and ad playback

**Reverb Strategy**:
- Office ambience: Short plate reverb (0.6s decay, pre-delay 15ms) — the sound of a mid-sized open-plan office with acoustic tile ceiling
- Presentation room: Minimal reverb (0.3s decay, heavily damped high frequencies) — dead corporate conference room with carpet and fabric panels
- Edit suite: Tight room reverb (0.4s, neutral) — enclosed space with equipment
- Super Bowl stadium: Large hall reverb (2.5s decay, pre-delay 50ms) — massive, enveloping
- Award ceremony: Concert hall reverb (1.8s decay, warm) — prestigious and spacious

**Distance Cues**:
- Near (0-2 meters): Full frequency range, minimal reverb. Example: UI clicks, paper on your desk, keyboard you are using.
- Medium (2-10 meters): High-pass filter at 150 Hz, increased reverb send +3dB. Example: teammate conversations across the bullpen, distant phone ring.
- Far (10+ meters): High-pass at 300 Hz, low-pass at 8 kHz, reverb send +6dB, volume reduced. Example: street traffic outside windows, voices in adjacent rooms.

### 5.4 Dynamic Mixing — Contextual Ducking

Music and ambience should dynamically duck (reduce volume) when critical audio needs focus:

| Event | Music Response | Ambience Response |
|---|---|---|
| Client speaks in Gauntlet | Duck to -9dB over 0.5s | Duck to -12dB over 0.5s |
| Player selects Pushback | Music swells +3dB for 2 seconds, then returns | Ambience unchanged |
| Urgent notification | Music unchanged | Ambience duck -6dB for duration of notification SFX |
| Super Bowl ad airs | Music cuts to silence (hard cut) | Ambience replaced by stadium crowd |
| Award win announced | Music swells to foreground (+6dB) | Ambience duck to -18dB |
| Player idle for 30+ seconds | Music Base Layer only, volume reduced to -21 LUFS | Ambience unchanged (maintains presence) |

### 5.5 Procedural Audio Elements

Certain systems benefit from procedural variation to avoid repetition fatigue:

**TEAM_Keyboard typing**:
- Pool of 20 individual keypress samples (mechanical, varying force)
- Procedurally sequenced at random intervals (50-150ms between presses) for 2-4 second bursts
- Velocity randomized ±15% per press
- Result: Every typing burst sounds organic and unique

**AMB_Office_General**:
- 8-10 looping ambience layers (keyboards, phones, voices, HVAC, footsteps) each with independent timers
- Each element triggers at semi-random intervals (e.g., phone ring every 20-40 seconds, randomized)
- Spatial position of each element randomly assigned on trigger within stereo field constraints
- Result: Office never sounds "looped" — it sounds alive and unpredictable

**BROADCAST_Social_Buzz**:
- Pool of 15 notification chime samples + 10 typing burst samples + 5 vocal reaction samples
- When triggered, 8-12 samples randomly selected and layered with random timing offsets (0-800ms spread)
- Pitch variation ±10% per sample
- Result: Every virality moment sounds chaotic and unique

---

## 6. MIX HIERARCHY

The mix hierarchy defines what the player hears at any given moment when multiple sounds compete. This is the most critical document for implementation.

### 6.1 Priority Pyramid (Top to Bottom)

```
                     [CRITICAL EVENTS]
                Client voice in Gauntlet
              Super Bowl broadcast moments
                  Crisis notifications
                   Walk Away door slam

                  [FEEDBACK LAYER]
           UI interactions (clicks, opens)
          Team reactions (sighs, murmurs)
       Notifications (success, failure, urgent)
            Production SFX (allocate, render)

                  [MUSIC LAYER]
          Adaptive music (stem-based mix)
        Occasional stingers (victory, defeat)

               [AMBIENCE LAYER]
          Office/Room ambient loops
      Background team keyboards/voices
           HVAC, environmental hum

               [SILENCE / ROOM TONE]
```

**Rule**: Higher layers mask lower layers. Critical events can silence everything else. Feedback can mask ambience but not critical. Music sits beneath critical and feedback but above ambience.

### 6.2 Frequency Allocation (Preventing Masking)

To ensure clarity, different layers occupy different frequency ranges:

| Layer | Primary Frequency Band | Secondary Band | EQ Strategy |
|---|---|---|---|
| **Critical (dialogue, key SFX)** | 1-4 kHz (speech intelligibility) | 200-800 Hz (body/warmth) | Boost at 2.5 kHz (+2dB), cut at 300 Hz (-1dB) if muddy |
| **Feedback (UI, reactions)** | 800 Hz - 2 kHz | 4-8 kHz (air/presence) | High-pass at 200 Hz, slight boost at 5 kHz (+1dB) for clarity |
| **Music** | 200 Hz - 1 kHz (foundational) | 80-200 Hz (bass), 2-6 kHz (melody) | Notch at 2.5 kHz (-2dB) to leave space for critical dialogue |
| **Ambience** | 100-500 Hz, 6-12 kHz | Full spectrum but quiet | Gentle low-pass at 10 kHz, high-pass at 80 Hz, overall volume low |

**Result**: Even when all layers play simultaneously, each occupies its own spectral niche. Dialogue is always intelligible. UI feedback is always heard. Music provides foundation without masking. Ambience fills space without cluttering.

### 6.3 Moment-by-Moment Mix Examples

**Scenario 1: Player reading a brief at their desk**
- Ambience: Office_General at -30 LUFS (keyboards, distant voices, HVAC)
- Music: Office_Work_Theme, Base Layer only, at -21 LUFS
- Feedback: UI_Open_Document at -15 LUFS (brief opens), then silence
- Result: Calm, focused, the player can think

**Scenario 2: Gauntlet Round 3, high tension, client about to give harsh note**
- Ambience: Presentation_Room (minimal, just AC hum) at -36 LUFS
- Music: Presentation_Room_Theme, Base + Momentum + Tension Layers, at -15 LUFS
- Critical: CLIENT_Pen_Tap at -12 LUFS, then CLIENT_Hmm_Negative at -10 LUFS
- Music ducks to -21 LUFS when client speaks
- Result: The player hears every nuance of the client's reaction. Tension is palpable.

**Scenario 3: Super Bowl ad airing**
- Ambience: SB_Crowd_Roar_Stadium at -18 LUFS (massive, enveloping)
- Music: Super_Bowl_Broadcast theme at -12 LUFS, then HARD CUT to silence when ad plays
- Critical: BROADCAST_Ad_Play_Start (silence bloom) at -6 LUFS, then ad "content" (represented by abstract sound design, TBD), then BROADCAST_Audience_Reaction_Huge at -9 LUFS
- Result: The player experiences the transition from spectacle to silence to reaction as a visceral emotional arc

**Scenario 4: Crisis — client calls after controversial ad**
- Ambience: Office_General, but Team_Murmur_Anxious layered in at -24 LUFS
- Music: Crisis_Theme at -18 LUFS (dissonant, unsettling)
- Critical: BROADCAST_Phone_Ring_Client at -9 LUFS, repeating until player interacts
- All other SFX suppressed during phone ring
- Result: The phone ring dominates. The player cannot ignore it. The music reinforces dread.

### 6.4 Silence Map (Where and Why)

Silence is a sound design choice. In UPFRONT, deliberate silence is used sparingly for maximum impact.

**Moment 1: The Walk Away Decision**
- When the player hovers over the "Walk Away" button in the Gauntlet, all music fades out over 2 seconds. Ambience remains but very quiet. Only the player's breath (if we add subtle player-avatar breath SFX — optional) and the hum of the AC.
- *Why*: This is the most consequential decision in the game. The silence forces the player to sit with it. No music is telling them how to feel.

**Moment 2: Between Super Bowl Ad Airing and Audience Reaction**
- After the player's ad finishes "playing" (storyboard animatic completes), there is 1.5 seconds of total silence. No music. No ambience. No crowd. Just... nothing.
- Then the reaction hits (laughter, applause, confusion, or silence from the crowd).
- *Why*: That pause is the held breath of a hundred million people. It is the longest 1.5 seconds of the player's year. The silence makes the reaction hit harder.

**Moment 3: A Concept is Killed in the Gauntlet**
- When the client definitively kills a concept (not just requests revisions, but kills it entirely), the music stops mid-phrase (does not resolve). There is 2-3 seconds of silence as the "Campaign Killed" UI appears. Then MUS_Gauntlet_Defeat plays.
- *Why*: The abrupt loss deserves a pause. The music cutting mid-phrase mirrors the concept being cut mid-development. The player feels the interruption.

**Moment 4: Year End Screen, Before Awards Announced**
- After the year's campaigns are tallied and before awards are revealed, the Year_End_Theme fades out completely. 4-5 seconds of silence (only very quiet room tone, sub-30 dB). Then AWARD_Nomination_Announced or "No Nominations" message.
- *Why*: Anticipation. The player does not know if their work mattered to the juries. The silence is the question hanging in the air.

**Moment 5: Player Idle (Intentional Quiet)**
- If the player is idle for 45+ seconds (reading, planning, thinking), music fades to Base Layer at -24 LUFS, ambience continues unchanged.
- *Why*: The game respects the player's thought process. It does not force stimulus. When the player acts, the music responds.

---

## 7. IMPLEMENTATION PLAN & TECHNICAL REQUIREMENTS

### 7.1 Production Pipeline

**Phase 1: Pre-Production (Weeks 1-3)**
- Finalize SFX list and music cue list with development team (confirm triggers, integration points)
- Create temp sound design using library assets and MIDI mockups for music (for vertical slice / prototype)
- Integrate temp audio into Gauntlet prototype and Super Bowl vertical slice (playtest priority #1 and #2 per GDD)
- Gather playtest feedback on: Gauntlet audio clarity, music emotional impact, UI feedback responsiveness

**Phase 2: Asset Production (Weeks 4-12)**
- **SFX Recording** (Weeks 4-6):
  - Foley session for office sounds (paper, keyboards, chairs, doors, footsteps) — 2 days, professional foley stage
  - Vocal session for human reactions (sighs, murmurs, laughter, breath) — 1 day, 4-6 voice actors, varied ages/genders
  - Field recording for ambience (office building HVAC, street traffic, distant crowds) — 1 day, location recording
- **SFX Design** (Weeks 6-8):
  - Synthesis for UI sounds (clicks, transitions, notifications) using analog hardware (Moog, modular synth) and soft synths
  - Processing and layering for broadcast/reaction sounds (crowd reactions, social media buzz, phone rings)
  - Procedural system design (typing, ambience randomization) — scripting and sample pool creation
- **Music Composition & Recording** (Weeks 7-12):
  - Compose and produce 10 music cues (Office, Presentation, Edit Suite, Gauntlet stingers, Super Bowl, Crisis, Award, Year End)
  - Record live instruments: piano (studio grand), upright bass, drum kit (brushes + sticks), muted trumpet, vibraphone
  - Record stems separately (Base, Momentum, Tension, Triumph) for adaptive tracks (6 cues x 3-4 stems = 20-24 stem files)
  - Mix and master all stems at -6dB headroom, 24-bit 48kHz

**Phase 3: Implementation (Weeks 13-16)**
- Import all assets into FMOD or Wwise
- Set up adaptive music system (parameter mapping: Client Trust, Team Cohesion, Gauntlet state, deadline proximity, etc.)
- Implement SFX triggers tied to game events (UI callbacks, Gauntlet state changes, broadcast sequence, etc.)
- Build procedural audio systems (typing, ambience randomization, social buzz layering)
- Implement dynamic mixing (ducking, priority system, contextual volume automation)
- Set up spatial audio (stereo positioning, reverb sends, distance attenuation)

**Phase 4: Integration & Polish (Weeks 17-20)**
- Full playthrough testing (audio QA: missing triggers, popping/clicking, mix balance issues, music transition smoothness)
- Iterate on mix balance based on full-game context (adjust LUFS targets, EQ tweaks, compression settings)
- Implement accessibility features: volume sliders (Master, Music, SFX, Ambience), visual indicators for critical audio cues (subtitles for client dialogue, notification icons)
- Final master limiting and export (ensure -14 LUFS integrated, -1dB true peak across all platforms)

**Phase 5: Platform-Specific Optimization (Weeks 21-22)**
- PC/Steam: 24-bit 48kHz for music, 16-bit 44.1kHz for SFX (balance quality vs. file size)
- Switch (if applicable): Compress to Opus codec, test on hardware for CPU overhead
- Implement adaptive quality settings (high/med/low SFX density for performance scaling)

### 7.2 Team & Resources

**Core Audio Team**:
- **Sound Designer (1 full-time, 22 weeks)**: Me. SFX design, recording supervision, implementation, mix.
- **Composer (1 contract, 6 weeks)**: Live instrument recording and music production. If budget allows, hire a jazz pianist/composer (or I handle this if skillset overlaps).
- **Foley Artist (1 contract, 2 days)**: Professional foley stage session for office recordings.
- **Voice Actors (4-6 people, 1 day)**: Human reaction recordings (sighs, murmurs, breath, laughter). Diverse casting for vocal texture variety.
- **Audio Programmer (0.5 full-time, shared with dev team, weeks 13-20)**: FMOD/Wwise integration, parameter mapping, procedural system scripting.

**External Resources**:
- Foley stage rental: 2 days
- Recording studio (for music): 4-5 days (live instrument tracking + mixing)
- Sound library subscriptions (for temp audio and supplemental assets): Boom Library, Sonniss, Pro Sound Effects

### 7.3 Technical Specifications

**Middleware**: FMOD Studio or Wwise (recommend FMOD for indie-scale adaptive music and easier Unity/Unreal integration)

**File Formats**:
- Music: WAV, 24-bit, 48kHz (stems), Ogg Vorbis or Opus for runtime (compressed, quality 8-9)
- SFX: WAV, 16-bit, 44.1kHz (one-shots), 24-bit 48kHz (ambience loops), runtime compression as needed
- All files mono unless stereo is essential (ambience, music) — saves memory

**Sample Counts**:
- UI SFX: ~40 one-shots
- Team/Office SFX: ~30 one-shots + 10 ambience loops
- Client/Gauntlet SFX: ~25 one-shots
- Production/Broadcast SFX: ~20 one-shots
- Super Bowl SFX: ~15 one-shots + 2 ambience loops
- Award/Milestone SFX: ~10 one-shots
- Crisis SFX: ~8 one-shots
- **Total SFX**: ~150 one-shots + ~15 loops

**Music Cue Count**:
- Loopable themes: 7 (Office, Presentation, Edit Suite, Super Bowl Countdown, Monday Morning, Year End, Crisis)
- Stingers (non-looping): 5 (Gauntlet Tension Rise, Gauntlet Victory, Gauntlet Defeat, Super Bowl Broadcast, Award Ceremony)
- **Total music cues**: 12
- **Total stem files** (loopable themes with 3-4 stems each): ~25 files

**Memory Budget Estimate**:
- Music (compressed, all stems loaded): ~120-150 MB
- SFX (uncompressed in memory): ~30-40 MB
- Ambience loops (streaming): ~10 MB
- **Total audio memory**: ~160-200 MB (reasonable for PC/modern consoles, may need streaming/compression strategy for Switch)

**Parameter Mapping (FMOD/Wwise)**:
- `Client_Trust` (0-100) → Music Tension Layer volume, tempo shift
- `Team_Cohesion` (0-100) → Music harmonic content (detuning, dissonance), ambience density
- `Deadline_Days` (0-90) → Music tempo increase, percussion layer addition
- `Gauntlet_Round` (1-5) → Music layer addition (Tension, Triumph), SFX density
- `Super_Bowl_Active` (bool) → Genre shift to orchestral, ambience swap to stadium
- `Audience_Score` (0-100) → Post-broadcast reaction SFX selection, music cue selection

### 7.4 Accessibility Considerations

UPFRONT's audio must be accessible to players with hearing impairments or audio sensitivities.

**Features**:
1. **Volume Sliders** (independent control):
   - Master Volume
   - Music Volume
   - SFX Volume
   - Ambience Volume
   - Voice/Dialogue Volume (if client dialogue is voiced — TBD)

2. **Visual Indicators for Critical Audio**:
   - Client reactions in Gauntlet: Text subtitles + emotion icon (positive/negative/neutral)
   - Notifications: Always accompanied by on-screen text + icon
   - Super Bowl audience reaction: On-screen sentiment bar (visual representation of laughter/applause/confusion)
   - Crisis events: Red UI flash + text alert

3. **Audio Description Mode** (stretch goal):
   - Option to enable brief text descriptions of non-verbal audio cues (e.g., "Client leans forward, interested" when CLIENT_Lean_Forward plays)

4. **Flashing/Strobing Content Warning**:
   - Ensure no audio-reactive visual effects (screen flashes synced to sound) exceed safe frequency thresholds (no more than 3 flashes per second)

5. **Mono Audio Option**:
   - Downmix all stereo content to mono for players with single-sided hearing loss

---

## 8. SILENCE MAP (EXPANDED)

Silence is the most powerful sound in UPFRONT's arsenal. Where music and SFX are withheld, the player's focus sharpens and emotional weight increases.

### 8.1 Structural Silence (Designed Quiet Zones)

These are moments where silence (or near-silence, <30 dB room tone) is an intentional design choice:

**1. The Walk Away Decision (Gauntlet)**
- **When**: Player hovers over "Walk Away" button for 2+ seconds
- **What Remains**: Presentation Room ambience (AC hum, very faint) at -36 LUFS. Optional: slow, deliberate breath SFX (player avatar implied presence).
- **What Cuts**: All music. All other SFX.
- **Duration**: As long as the player hesitates. When they click, sound returns (CLIENT_Stand_Up_Abrupt or CLIENT_Handshake depending on choice).
- **Why**: This is the nuclear option. The silence mirrors the weight of the decision. No music is allowed to editorialize. The player must choose in the void.

**2. Post-Super-Bowl Ad, Pre-Reaction (Broadcast)**
- **When**: Player's ad finishes playing (storyboard animatic ends), before audience reaction begins
- **What Remains**: Nothing. Absolute silence. Not even room tone.
- **What Cuts**: Stadium crowd ambience, all music, all SFX.
- **Duration**: 1.5 seconds (feels like 10).
- **Why**: This is the held breath of America. The silence is the gap between "did we do it?" and "here's the answer." The reaction hits infinitely harder after this pause.

**3. Concept Killed (Gauntlet Failure)**
- **When**: Client definitively kills the concept (not revision, but full rejection)
- **What Remains**: Presentation Room ambience at -40 LUFS (barely audible).
- **What Cuts**: Music cuts mid-phrase (does not resolve). All feedback SFX muted.
- **Duration**: 2-3 seconds while "Campaign Killed" UI appears. Then MUS_Gauntlet_Defeat plays.
- **Why**: The abrupt music cut mirrors the concept being cut. The silence is loss. The player earned this moment of mourning.

**4. Pre-Award Announcement (Year End)**
- **When**: After year metrics are tallied, before award nominations are revealed
- **What Remains**: Room tone (very quiet office at night, distant traffic) at -33 LUFS.
- **What Cuts**: Year_End_Theme fades out completely over 3 seconds.
- **Duration**: 4-5 seconds of near-silence.
- **Why**: Anticipation. The player does not know if their work was seen. The silence is the question. The answer (nomination or none) breaks the silence.

**5. Player Deep Focus (Idle State)**
- **When**: Player is idle for 45+ seconds (reading brief, planning, staring at concept stats)
- **What Remains**: Ambience continues at normal level. Music fades to Base Layer only, volume drops to -24 LUFS.
- **What Cuts**: Momentum, Tension, Triumph music layers. All non-essential SFX.
- **Duration**: Until player acts (click, navigate, make decision).
- **Why**: Respect the player's thought process. The game does not demand attention. It waits. When the player acts, the music responds ("oh, you're back — let's go").

### 8.2 Emotional Silence (Absence as Punctuation)

These are micro-silences — gaps in sound that create rhythm and emphasis:

**1. Pre-Pushback Silence**
- **When**: Player selects "Push Back" option in Gauntlet. Before Persuasion Check resolves.
- **Duration**: 0.5 seconds of near-silence (music ducks to -30 LUFS, ambience muted, no SFX).
- **Then**: MUS_Gauntlet_Tension_Rise plays (rising chromatic piano line).
- **Why**: The pause before the gamble. The player committed. Now they wait.

**2. Post-Notification Silence**
- **When**: After a major notification (award win, client lost, reputation milestone)
- **Duration**: 1 second of UI silence before next action is allowed.
- **Why**: Give the notification weight. The player must absorb the information before moving forward. No instant dismiss.

**3. Between Gauntlet Rounds**
- **When**: After player responds to a client note, before next round begins
- **Duration**: 0.8-1.2 seconds of reduced ambience (music continues but SFX layer muted).
- **Why**: Breath. The negotiation is not constant — it has pauses. Real conversations have silence.

**4. Pre-Broadcast Silence**
- **When**: After player finalizes production, before ad broadcast sequence begins
- **Duration**: 1.5 seconds. Music fades out. Ambience shifts (office → broadcast transition).
- **Why**: Threshold crossing. The work phase is over. The reception phase begins.

### 8.3 Systemic Silence (Dynamic Audio Absence)

These are silence states triggered by game systems, not scripted moments:

**1. Cash Crisis Ambience Thinning**
- **When**: Cash reserves drop below 10% of monthly expenses
- **What Changes**: Office ambience density reduced by 60%. Fewer keyboards, fewer voices, more empty space.
- **Why**: The agency is barely alive. Silence = absence of people = layoffs implied. The soundscape mirrors the financial reality.

**2. Team Meltdown Silence**
- **When**: Team Cohesion reaches 0-10 (Meltdown state)
- **What Changes**: Team-related SFX (keyboards, murmurs, chair movement) cut by 80%. Only occasional frustrated typing or sigh remains.
- **Why**: The team is not working. They are stewing. Silence = passive resistance.

**3. Post-Walk-Away Office Return**
- **When**: Player returns to office screen after walking away from a Gauntlet
- **What Changes**: Office ambience is quieter (−6dB) for 60 seconds. Fewer voices. Music Tension Layer lingers.
- **Why**: The mood is somber. The agency feels the loss. Sound reflects narrative consequence.

**4. Late Night Crunch Isolation**
- **When**: Q4, multiple deadlines active, after 10 PM in-game time (if time-of-day is tracked — stretch goal)
- **What Changes**: Office ambience shifts to Late_Night variant (see SFX section 3.2). Music shifts to Edit_Suite_Theme regardless of screen. More silence between sounds.
- **Why**: Everyone went home except the player (implied). The soundscape = loneliness + focus.

---

## 9. CLOSING NOTE — THE FREQUENCY OF AMBITION

Audio is not the last thing you add to a game. Audio IS game feel.

Every sound in UPFRONT exists to answer one question: *What does it feel like to defend creative work to someone who controls the money?*

That question has a frequency. It sounds like:
- The confidence of a walking bassline when you enter the Gauntlet with high reputation
- The hollow thud of a client hanging up after you walked away
- The collective held breath of a hundred million people in 1.5 seconds of silence before your Super Bowl ad is judged
- The quiet ache of a solo piano when you look at your agency at year's end and see every compromise and every victory reflected back

The sounds in this document are not decoration. They are the invisible architecture of the player fantasy. The Gauntlet is tense because the music builds and the client's pen taps and the silence before a Pushback decision makes the player's heart rate rise. The Super Bowl is climactic because the orchestral swell is massive and the cut to silence is abrupt and the crowd reaction is deafening. The year-end reflection is bittersweet because the piano melody never resolves and the office is quiet and the player is alone with what they built.

Audio does not tell the player what to feel. Audio makes them feel it in their chest, in their breath, in the space between sounds.

This document is production-ready. Every sound is specified. Every system is designed. Every silence is mapped. The work is to make it real.

Listen to the space between.

— ECHO

---

**FINAL SPECIFICATIONS SUMMARY**

- **Total SFX Assets**: ~150 one-shots, ~15 ambience loops
- **Total Music Cues**: 12 cues, ~25 stem files
- **Estimated Audio Memory**: 160-200 MB
- **Middleware**: FMOD Studio or Wwise
- **Production Timeline**: 22 weeks (pre-production through platform optimization)
- **Core Team**: Sound Designer (full-time), Composer (contract, 6 weeks), Foley Artist (2 days), Voice Actors (4-6, 1 day), Audio Programmer (shared, 8 weeks)
- **Mix Target**: -14 LUFS integrated, -1dB true peak
- **Accessibility**: Volume sliders (4 independent), visual indicators for critical audio, mono downmix option

**File Deliverables**:
- SFX asset library (WAV files, organized by category)
- Music stems (WAV, 24-bit 48kHz)
- FMOD/Wwise project file (adaptive system, parameter mapping, mix automation)
- Implementation documentation (trigger list, parameter table, mix notes)

**This is the sound of UPFRONT. Make it heard.**
