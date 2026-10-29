---
tags: [art, design, noir, lessons, skill-issue]
---
# Art Direction

## Where it landed
**Black-and-white film noir with red and blue as the only saturated colors.** It shows up as a gray rainy city (map), brick walls and film-title lettering (game UI and phone app), and near-black pages with off-white type (website).

**Why it works:** the whiteboard asked for *"clean, distinct sides by color/object, monotone environment"* ([03 Whiteboard Brainstorm](03-whiteboard-brainstorm.md) Board 6). Noir is exactly that, and it fits the detective trench coat gag.

## The path there
| Phase | What we tried | Result |
|---|---|---|
| A. Function first (Sat) | Crude boxes; gray test maps | Readable, not pretty ([08 Duo Character](08-duo-character.md)) |
| B. Concept (Sat 19:15) | Low-poly raccoons in a red/blue trench coat, light mafia/burglar feel | **Kept**: became the in-game model |
| C. Map (Sun 03:46) | Plain gray Pit; an orange Quake sky | Orange sky **rejected** (too much); gray kept as the base for theming |
| D. Noir map (Sun ~08:00) | First version too dark and **amber** | **Changed** to neutral gray/white plus red/blue neon, from Michael's flat-noir references. *"Map is really good."* |
| E. Noir UI | Gray UI → darker **B&W film** title cards | **Kept**; the doorway + silhouette in the menu were **removed** on request |
| F. Poster | Rubber-hose cartoon raccoons | **Rejected** firmly; style dropped completely |
| G. Website hero | Flat silhouettes → a flat teal two-raccoon poster → an ink style | Code-drawn art couldn't match a hand-inked reference; I said so and gave an image-generator prompt instead. Michael chose his own PNG art for the site ([13 Website](13-website.md)) |
| H. Phone app | Same B&W kit as the game | **Kept** (PR #9) |

## Rules that came out of it
> [!IMPORTANT]
> **Anatomy rule**
> **Top raccoon = Gunner, holds the gun. Bottom raccoon = Runner, NO gun and no gun-holding pose.** One continuous coat, one pair of legs. The top raccoon rides on the bottom one's shoulders **inside** the coat; the bottom one peeks out where the coat parts. Generated art kept getting this wrong (an armed bottom raccoon, or two separate raccoons), so check every new image against it.
>
> *Known violation to fix:* my flat teal poster (phase G) has the bottom raccoon holding the pistol. Don't reuse it as-is.

- **Team color goes on the coat and hat, plus neon in the world.** Never on large surfaces of the map.
- **Script font only for flourishes** ("presents", "vs.", "and the winner is…"); the display font for everything else.
- **Motion effects** (flicker, grain, rain) must respect reduced-motion settings.
- **Function first:** every new look must keep the model's readability (separate legs/top, visible gun, hit flash).

## Honest lessons
- **References beat adjectives.** "Noir" alone produced amber; Michael's flat gray reference images got it right on the next pass.
- **Know the medium's limit.** Code-drawn vector art can match flat graphic shapes but not hand-inked illustration. Saying so early saved time.
- **Some things should be thrown out, not iterated.** When a style is rejected that strongly, the right move is to remove it everywhere and not come back to it.

## Open
- The rejected poster artboard is still on the Design canvas; Michael hasn't decided whether to delete it.
- Art rights: record which art is original, which is AI-generated (the Gemini MVP badges, any website art) and which is licensed (TeX Gyre Chorus under the GUST Font License, Barlow under OFL).
