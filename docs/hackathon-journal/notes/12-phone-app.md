---
tags: [phone, expo, react-native, companion, skill-issue]
---
# Phone App (companion)

## What it is
- **Expo SDK 58 / React Native 0.88**, in `apps/companion`. It uses `expo-sensors` (gyroscope + accelerometer).
- **Native only.** Its web build shows a "use the native app" message, because browsers block motion sensors without HTTPS.
- Screens: **Main menu → Join a Lobby (enter code) → Team + Role select → Ready → in-match controller (Runner or Gunner) → Game over**, plus **Practice Controls** and a `/debug` stream.
- Finds the relay through `skillissue.vodka/api/connection`; `skillissue://join?code=<CODE>` deep links fill in the code.

## Running it (from the README)
```sh
# Node.js 24, from the repo root
npm install
npm run companion:lan      # or companion:start (Expo tunnel when needed)
```
On Windows PowerShell, `npm.cmd` gets around the script execution policy.

### The iPhone / Expo Go problem (Sun morning)
- The App Store **Expo Go** only supports **SDK 54**, and the app is on **SDK 58**, so scanning the QR code on an iPhone fails.
- Options:
  1. `eas go` + **TestFlight**: needs an Apple Developer account.
  2. **Android**: install the matching Expo Go from expo.dev/go.
  3. A **Mac** with Xcode: `npx expo run:ios --device`.
- "Sync npm lockfile for EAS builds" (Ryan, Sun 11:24) points to the team moving toward EAS builds.

**Errors I hit setting it up on my PC, and the fixes:**
| Error | Fix |
|---|---|
| `EBADENGINE`, Node 21 | Install **Node 24 LTS** |
| `npm` not recognized | Open a new PowerShell window (or refresh PATH) |
| `npm.ps1 cannot be loaded` (execution policy) | Use `npm.cmd` |
| Pasted a whole chat transcript into PowerShell | Paste only the commands |

## Look: before → after
**Before (Sat–Sun early):** navy/blue Expo screens; Ryan added an animated menu background and full-screen backgrounds (Sun 05:34–06:16).

**After, noir (me, PR #9, Sun 10:00).** Brief: *"make a similar style page for the phone/mobile/app of joining the lobby and all."*

![app noir preview](../images/app-noir-preview.png)
*Mock-up of the noir screens: main menu, enter code, team/role select, game over.*

| File | Change |
|---|---|
| `theme.ts` | Noir palette and fonts, including `script: "TeXGyreChorus-MediumItalic"` |
| `kit.tsx` | `Title` gains a `depth` extrusion (same trick as the game's `title_3d`); new `Script` component; `SlantButton` is now flat (name kept so callers don't change), dark text on light fills |
| `split-background.tsx` | `SplitBackground` is now a brick wall, flickering spotlight, team glow at the bottom and vignette. **Respects reduce-motion.** |
| Screens | `main-menu.tsx`, `enter-code.tsx`, `team-select.tsx`, `game-over.tsx`, `match-bar.tsx` restyled |
| Fonts | `assets/fonts/TeXGyreChorus-MediumItalic.otf` + license |

Ryan then extended it to the **in-match screens and Practice** ("Noir theme for the in-match phone screens and Practice", Sun 10:57) and removed the **Settings / server URL** field from the phone menu (Sun 11:03), since the relay is found automatically.

## Practice Controls (repo preview)
<img src="../../screenshots/companion-practice.png" alt="repo companion practice" width="520">

## Join reliability fixes (Ryan, Sun 05:28–06:01)
- Join by code through the **relay only**.
- "Say why a join is stuck" instead of "Joining your lobby…" forever; show what the server sent.
- **Phones never sent the join**: the cause was React Native's `bufferedAmount`. Fixed.
- A 10 s join deadline with a retry; a wrong code is reported immediately.
