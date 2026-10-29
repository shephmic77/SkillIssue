---
tags: [retrospective, todo, postmortem, skill-issue]
---
# Open Items & Retrospective

## Open items
### Game
- [ ] **Real 4-phone match** at full player count, with results recorded (phone models, lag, Wi-Fi)
- [ ] Decide on `powerups` (Kenneth): bounty, mystery power-ups, swap on death, music, SFX
- [ ] Re-add the **HAT helmet** rule? (built and tested by me, not on `main`)
- [ ] Sound: no audio on `main` yet; ElevenLabs voice lines were a whiteboard idea
- [ ] Unapplied tuning suggestions ([16 Tuning](16-tuning.md)): longer time-to-kill so duos have time to talk
- [ ] Whiteboard ideas not built: shotgun-jump pushback, shared stamina, anti-camping reveal, grenades, melee, taunt, debuffs, >4 players

### Phone app
- [ ] iPhone path: EAS/TestFlight (Apple Developer account) or a dev build from a Mac
- [ ] Confirm the noir screens on a real device

### Website
- [ ] Accessibility for the PNG hero: hotspot names, keyboard focus, HTML equivalents of baked-in text
- [ ] 375 px check, image weight
- [ ] Delete the `site-before-preview` tag once final
- [ ] Decide whether the unused Next.js noir redesign is worth keeping

### Repo
- [ ] Delete merged branches (`andmotion`, `claude/reworked-movement`) once their owners agree
- [ ] Decide on `claude/mlh-tracks`

### Records still missing (fill in, don't guess)
| Topic | What to collect |
|---|---|
| Submission | Devpost/HackPSU submission link, track entered |
| Judging | Feedback, placement, any awards |
| Demo | Video or GIF of a real match with four phones |
| Venue test | Which phones worked, what broke |
| Art rights | Which art is original, AI-generated or licensed |

## Retrospective
### What went well
- **The concept carried the constraints.** Splitting one body between two phones answered all three Mystery Stack cards with one idea, and the trench coat gag explained the controls before anyone read a rule.
- **Folder ownership worked.** Five people in one Godot project with very few conflicts. My PR #1 merged cleanly while four teammate commits landed alongside it.
- **Decoupled input paid off.** `DuoInput` + controllers meant the whole game could be tested on a keyboard. That's how I could build maps, weapons and UI without four phones.
- **Data-driven tuning.** Hitboxes, spread and trails live in `.tres` files, so retuning for a new model was numbers, not code.
- **Small, reversible changes.** The homepage swap was one rewrite plus one file, with a tag to go back.

### What was hard
- **Godot scene files in git:** an accidental editor rotation slipped into a commit and was only caught later.
- **Moving `main`:** several of my zips had to be rebuilt with 3-way merges.
- **Phones:** HTTPS for web sensors, iOS vs Android sign differences, Android permission quirks, Expo Go SDK limits on iPhone.
- **Art direction through words:** the noir look took several rounds; references fixed what adjectives couldn't.
- **Features overlapping between people:** my regen vs Brian's medkits; my no-ammo call vs Aditya's magazines; the hat helmet that didn't survive later edits.

### What I'd do differently
1. Agree on a **feature owner list** early for overlapping systems (health, ammo), so work doesn't get built twice.
2. Run a **real-phone test every few hours**, not just at the end.
3. Put **reference images** in the brief before the first art pass.
4. Read `git diff -- "*.tscn"` before **every** commit (it's now in my loop).
5. After each merge, **audit what's on `main`** against what I think I shipped (like [17 Testing Log](17-testing-log.md) §18).

### Postmortem outline (for the DEV post)
1. Original concept: phone-motion rivalry with split control
2. Prototype: standalone Godot + relay + web controller in 30 minutes
3. First playable: two inputs driving one Duo (keyboard, then phones via `InputRouter`)
4. Multiplayer: both teams fighting on the split screen
5. Polish: raccoon model, The Pit, noir theme, MVP, website
6. Demo and judging: **fill in**
7. Lessons: above
