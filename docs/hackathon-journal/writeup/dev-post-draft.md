---
tags: [writeup, dev, mlhacks, skill-issue]
publish_by: 2026-10-31
devto_tags: [mlhacks, devchallenge, hackathon, godot, gamedev]
---
# DEV Post Draft: MLH × DEV Writing Challenge

> [!NOTE]
> **Checklist**
> - [ ] Sign in to DEV with the **MLH account linked to my HackPSU registration**
> - [ ] Official template: What I Built · Demo · Partner Technologies · Hackathon Experience
> - [ ] Tags: `#mlhacks` `#devchallenge` `#hackathon`
> - [ ] Publish by **Oct 31** (Eastern)
> - [ ] Demo GIF/video (**still needed**: a real 4-phone match) + repo + skillissue.vodka
> - [ ] Share it (popularity is a judging criterion)
> - [ ] Everything claimed is **confirmed** in these notes; nothing about results until they're known

**Working title:** *Two Raccoons, One Trench Coat: Building a Phone-Motion 2v2 Shooter at HackPSU*

![noir play](../images/noir-play.png)

## What I Built
- **Hook:** one character, two players, two phones. The Runner tilts to walk; the Gunner turns the phone to aim. Neither can win alone.
- The Mystery Stack draw (phone motion, rivalry, 4+) and how the split body hits all three ([01 Event & Challenge](../notes/01-event-and-challenge.md)).
- My part: the **Duo** character and its systems, the maps, and the noir look ([04 Team & Roles](../notes/04-team-and-roles.md)).

## Demo
*(GIF of both halves of the TV and four people on phones; repo link; site link.)*

## How it works *(technical substance)*
- **Input decoupling:** `DuoInput` + `DuoController` let phones, keyboard or bots drive the same body. That's why the game could be tested at a desk ([05 Architecture](../notes/05-architecture.md)).
- **Readable split body:** legs and top face separately; an enemy-visible gun; hit flash; the hat flies off on headshots; the two raccoons tumble out on death ([08 Duo Character](../notes/08-duo-character.md)).
- **Spread as a teamwork lever:** a scoped sniper is only perfect when the Runner stands still ([09 Weapons & Combat](../notes/09-weapons-and-combat.md)).
- **The Pit:** a three-level Quake-style map with sightline-tested spawn rooms, then a noir city block built from one shader ([10 Maps](../notes/10-maps.md)).
- **Networking (team):** a relay that owns codes and slots, a control plane on Vercel, Godot owning gameplay.
- **Render-layer trick** for split-screen first person.

## Partner Technologies
- **Google Gemini:** match MVP judge + raccoon badge (live).
- **Tiger Data:** leaderboard/accounts API (*describe accurately: wired, deployment status TBD*).
- **Auth0:** only if `claude/mlh-tracks` merges.
- Godot 4.7, Expo / React Native, Next.js on Vercel, Node WebSocket relay.

## Hackathon Experience *(be honest about decisions)*
- Catching early that touch joysticks would fail the motion card
- Adding my work as new folders so PR #1 changed **zero** teammate files, and still merged cleanly while four other commits landed
- Adapting to a teammate's `GameEvents` instead of overwriting it
- The accidental 157° map rotation, and why I now read every `.tscn` diff
- Function first: crude boxes → raccoons once the game worked
- Playtesting The Pit and spawning while staring at a gray wall → grid shader, spawns facing doorways
- Noir: references beat adjectives
- *(Fill in after the demo: what players did, what broke, what got laughs.)*

## Team
Aditya Pratap Singh · Brian Podolskiy · Kenneth Tran · Michael Shepherd · Ryan Smith. One line each from [04 Team & Roles](../notes/04-team-and-roles.md).
