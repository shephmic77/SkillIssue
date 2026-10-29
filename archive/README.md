# Archive

Files that are no longer used, kept instead of deleted.

## `starter-templates/`

Leftovers from the project generators the apps were created with. Nothing in the code references them.

| Folder | What's there | Came from |
| --- | --- | --- |
| `companion/assets/images/` | React logo, Expo badges, `tutorial-web.png`, the `tabIcons/` set | Expo's default app template |
| `companion/scripts/reset-project.js` | Expo's "reset project" script. When run, it **moves the app's code out into an example folder and replaces it with a blank starter**, so it was taken out of `apps/companion` and its `npm run reset-project` entry removed | Expo's default app template |
| `landing/public/` | `next.svg`, `vercel.svg`, `file.svg`, `globe.svg`, `window.svg` | `create-next-app` |

Brian's early game prototype is **not** here: it lives in [`apps/game/prototypes`](../apps/game/prototypes/README.md), because Godot can only load files inside the game folder and one of the maps still uses it.
