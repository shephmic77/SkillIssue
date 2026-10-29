# Music

The `Music` autoload (`scripts/music.gd`) plays these files and crossfades between them:

| File | Plays on |
|---|---|
| `menu_dusty_memories.ogg` | main menu and lobby |
| `match_crushing_it.ogg` | during a match |
| `results_schmoovin.ogg` | results screen (optional: without it the menu track plays) |
| `extra_batteries_not_included.ogg` | not used yet |

To change a track, drop the file in this folder and point the matching entry in `TRACKS`
in `scripts/music.gd` at it. `.ogg` is best, since it's small and loops cleanly. Music loops
automatically, whatever the import settings say.

Volume: the Music bus (Audio tab at the bottom of the editor), and the Music Volume slider
in Settings.

**Credit the artist.** Most free tracks are CC BY and need credit. List each one in
[`../CREDITS.md`](../CREDITS.md): title, artist, link, license.
