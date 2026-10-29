# Prototypes

Brian Podolskiy's first playable prototype from Saturday afternoon at HackPSU, before the team settled on the shared Duo character. It is kept as a record of how the game started. Nothing here is deleted.

| Saturday 16:30: first blockout | Saturday 18:19: the arena |
| --- | --- |
| <img src="../../../docs/hackathon-journal/images/map-sat-1630-first-blockout.png" alt="First blockout test level"> | <img src="../../../docs/hackathon-journal/images/map-sat-1819-arena-box.png" alt="The first arena"> |
| `prototype_test_level.tscn` | Became `maps/arena_base.tscn`, still used by Arena v2 |

| File | What it was |
| --- | --- |
| `prototype_test_level.tscn` | The first test level: a floor, a ramp and a few cover boxes, with the prototype player. Open it and press **F6** to try it |
| `player_movement.gd` | First-person movement with mouse look (`class_name PlayerMovement`) |
| `player_health_armor.gd` | Health and armor for the prototype player |
| `weapon_system.gd` | Weapon slots and ammo counts |
| `armor_pickup.gd` | An empty starter script for an armor pickup |
| `box_collision_shape.tres` | A box collision shape that nothing references |

## Is any of this still used?

Yes, partly. `maps/arena_base.tscn` (Brian's arena) still contains nodes that use `player_movement.gd`, `player_health_armor.gd` and `weapon_system.gd`, so these scripts must stay in the project. The real match uses the Duo's components instead (`components/`, `entities/duo/`). The team chose `WeaponComponent` over `weapon_system.gd` as the weapon system.

If you move or rename a file here, do it inside the Godot editor (or update the `res://prototypes/...` paths in `maps/arena_base.tscn` by hand), then run the smoke tests.
