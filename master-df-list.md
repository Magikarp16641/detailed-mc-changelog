This serves as a list of all discontinued features mentioned in this changelog.

# Blocks
## Individual blocks
| Discontinued Feature | Version range (path) | Notes |
| --- | --- | --- |
| Block ID `00` at the world edge between Y 30 and Y 31 | rd-132211-launcher - 0.0.13a_03-launcher | |
| water (`08`), calmWater (`09`) | 0.0.12a_03-200018 | New worlds only, recontinued using [header editing] and in 0.0.13a_03. |
| lava (`0A`), calmLava (`0B`) between Y 22 and Y 27 | 0.0.12a_03-200018 | New worlds only, recontinued using [header editing] and in 0.0.13a_03. |
| lava (`0A`), calmLava (`0B`) between Y 28 and Y 31 | 0.0.12a_03-200018 | New worlds only, recontinued using [header editing]. |
| water (`08`), calmWater (`09`) | [Header editing] | Also possible on new worlds generated in 0.0.13a_03, or 0.0.13a_03-launcher. Recontinued on all worlds in 0.0.14a_08. |
| water (`08`) or calmWater (`09`) between Y 32 and Y 63 | [Header editing] | |
| calmWater (`09`) in unnatural non-ticking locations | [Header editing] | Recontinued in 0.0.14a_08. |
| lava (`0A`) or calmLava (`0B`) between Y 22 and Y 27 | [Header editing] | Also possible in new worlds generated in 0.0.13a_03 or later. |
| lava (`0A`) or calmLava (`0B`) between Y 28 and Y 63 | [Header editing] | |
| calmLava (`0B`) in unnatural non-ticking locations | [Header editing] | Recontinued in 0.0.14a_08. |
| sand (`0C`), gravel (`0D`) | [Header editing] | Recontinued in 0.0.14a_08. |
| goldOre (`0E`), ironOre (`0F`), coalOre (`10`) | [Header editing] | Recontinued on new worlds generated in 0.0.14a_08 or later. |
| goldOre (`0E`), ironOre (`0F`) or coalOre (`10`) at world edge, Y 0 or Y 63 | [Header editing] | |
| goldOre (`0E`), ironOre (`0F`) or coalOre (`10`) in unnatural quantities | [Header editing] | |
| treeTrunk (`11`), leaves (`12`) | [Header editing] | Recontinued in 0.0.14a_08. |
| Block ID `13`-`FF` | [Header editing] | |

## Block configurations
| Discontinued Feature | Version range (path) | Notes |
| --- | --- | --- |
| water (`08`) or calmWater (`09`) below lava (`0A`) or calmLava (`0B`) | 0.0.12a_03-200018 | New worlds only. Recontinued using [header editing]. |
| calmWater (`09`) or calmLava (`0B`) above or next to ID `00` | (0.0.12a_03-200018) -> (rd-132211-launcher - 0.0.11a-launcher) | Worlds generated in 0.0.12a_03-200018 only. Recontinued using [header editing]. |
| calmWater (`09`) at the world border at non-ticking coordinates above or below rock (`01`) | (0.0.12a_03-200018) -> (rd-132211-launcher - 0.0.11a-launcher) | Worlds generated in 0.0.12a_03-200018 only. Recontinued using [header editing] and in 0.0.14a_08. |
| calmWater (`09`) at the world border at non-ticking coordinates next to grass (`02`) | (0.0.12a_03-200018) -> (rd-160052-launcher - 0.0.11a-launcher) | Worlds generated in 0.0.12a_03-200018 only. Recontinued using [header editing], on newly generated worlds in 0.0.13a_03, and on all worlds in 0.0.14a_08. |
| calmWater (`09`) at the world border at non-ticking coordinates above or below grass (`02`) | (0.0.12a_03-200018) -> (rd-160052-launcher - 0.0.11a-launcher) | Worlds generated in 0.0.12a_03-200018 only. Recontinued using [header editing] and in 0.0.14a_08. |
| calmWater (`09`) at the world border at non-ticking coordinates adjacent to stoneBrick (`04`) or wood (`05`) | (0.0.12a_03-200018) -> (rd-160052-launcher - 0.0.11a-launcher) | Worlds generated in 0.0.12a_03-200018 only. Recontinued using [header editing] and in 0.0.14a_08. |
| calmWater (`09`) at the world border at non-ticking coordinates below dirt (`03`) | (0.0.12a_03-200018) -> (rd-160052-launcher - 0.0.11a-launcher) | Worlds generated in 0.0.12a_03-200018 only. Recontinued using [header editing] and in 0.0.14a_08. |
| calmWater (`09`) at the world border at non-ticking coordinates adjacent to bush (`06`) | (0.0.12a_03-200018) -> (rd-161348-launcher - 0.0.11a-launcher) | Worlds generated in 0.0.12a_03-200018 only. Recontinued using [header editing] and in 0.0.14a_08. |
| calmLava (`0B`) above or next to ID `00` in a 32x64x512 world | (0.0.13a-launcher) -> (rd-132211-launcher - 0.0.11a-launcher) | Worlds generated in 0.0.13a-launcher only, recontinued using [header editing]. |
| water (`08`) or calmWater (`09`) adjacent to lava (`0A`) or calmLava (`0B`) | [Header editing] | |
| calmWater (`09`) or calmLava (`0B`) above or next to ID `00` | [Header editing] | |
| calmWater (`09`) at the world border at non-ticking coordinates above or below rock (`01`) | [Header editing] | Recontinued in 0.0.14a_08. |
| calmWater (`09`) at the world border at non-ticking coordinates adjacent to grass (`02`), stoneBrick (`04`), wood (`05`) or bush (`06`) | [Header editing] | Recontinued in 0.0.14a_08. |
| calmWater (`09`) at the world border at non-ticking coordinates below dirt (`03`) | [Header editing] | Recontinued in 0.0.14a_08. |
| sand (`0C`) or gravel (`0D`) above block ID `00` | [Header editing] | Also possible in a 256x64x256 world by downgrading sand or gravel to before 0.0.14a_08. |
| grass (`02`) somewhere below goldOre(`0E`), ironOre (`0F`) or coalOre (`10`) | [Header editing] | Also possible in a 256x64x256 world by downgrading goldOre, ironOre or coalOre to before 0.0.14a_08. |
| A pocket of water (`08`) or calmWater (`09`) surrounded on the sides and top by goldOre(`0E`), ironOre (`0F`) or coalOre (`10`) below Y 29 | [Header editing] | |
| sand (`0C`) or gravel (`0D`) above block ID `00` | (0.0.14a_08 - ???) -> (0.0.13-launcher - 0.0.13a_03-launcher ) | 256x64x256 world only. Also possible using [header editing]. |
| grass (`02`) somewhere below goldOre(`0E`), ironOre (`0F`) or coalOre (`10`) | (0.0.14a_08 - ???) -> (0.0.13-launcher - 0.0.13a_03-launcher ) | 256x64x256 world only. Also possible using [header editing]. |

# Entities
| Discontinued Feature | Version range (path) | Notes |
| --- | --- | --- |
| Zombie with bbHeight other than 1.8 | [Header editing] | |
| Zombie with bbWidth other than 0.6 | [Header editing] | |
| Zombie with heightOffest, xRot, xRotI, yRot, yRotI, or epsilon other than 0.0 | [Header editing] | |
| Zombie with x or z below -4194304.0 or above 4194304.0 | [Header editing] | |
| Zombie with horizontal velocity greater than 0.25068867 | [Header editing] | |
| Zombie with y above 16777216.0 | [Header editing] | |
| Zombie with yd below -3.919994 or above 0.4116 | [Header editing] | |
| Zombie with position-velocity mismatch | [Header editing] | |
| Zombie with horizontal velocity-rot-rotA mismatch | [Header editing] | |
| Zombie with rot below -1.3421773E8 or above 2.1474836E9 | [Header editing] | |
| Zombie with rotA below -7.9999685 or above 99.99962 | [Header editing] | |
| Zombie with speed other than 1.0 | [Header editing] | |
| Zombie with timeOffs below 0.0 or above 1239813.0 | [Header editing] | |
| Zombie with timeOffs not a multiple of 1.376469E-10 | [Header editing] | |
| Zombie with sufficiently incorrectly sized hitbox | [Header editing] | |
| Zombie with a new Level object inside the level field | [Header editing] | Crashes the game if the zombie is inside the new level when rendering. |
| More than 256 zombies in a world | [Header editing] | |
| Multiple instances of a Zombie in the entities list | [Header editing] | |
| Multiple Zombies sharing the same hitbox | [Header editing] | |
| Entity entity | [Header editing] | |
| Particle entity | [Header editing] | Temporary. |

# World data
| Discontinued Feature | Version range (path) | Notes |
| --- | --- | --- |
| "--" name | (rd-132211-launcher - 0.0.12a_03-200018) -> (0.0.13a-launcher - ???) | |
| "unknown" creator | (rd-132211-launcher - 0.0.12a_03-200018) -> (0.0.13a-launcher) | Recontinued on newly generated worlds in 0.0.13a_03. |
| World dimensions of 32x64x512 | 0.0.13-launcher | New worlds only, partially recontinued using [header editing] (can't be fully recreated for most create time values, see page for more details). All combinations can be recreated using [header editing] in the [0.0.14a_08+ save format](save-formats/serialized-level.md). |
| World dimensions other than 256x64x256 | [Header editing] | The volume of the world must be sufficiently less than 4,194,304. The area of the world must be less than 2,147,483,646. A 32x64x512 world is also possible in 0.0.13a-launcher. A 128x64x128 world is recontinued on new worlds in 0.0.14a_08. |
| name other than "--" or "A Nice World" | [Header editing] | |
| creator other than "noname" | [Header editing] | Many variants recontinued on newly generated worlds in 0.0.13a_03. |
| creator containing null, horizontal tab, line feed, form feed, carriage return, or surrogates | [Header editing] | |
| creator starting or ending with space or a C0 control character | [Header editing] | |
| rotSpawn above 9.0071993E15 | [Header editing] | |
| rotSpawn not a multiple of 2^-25 | [Header editing] | |
| unprocessed other than 0 if the volume of the world is a multiple of 200 | [Header editing] | |
| unprocessed not a multiple of 100/50/40/25/20/10/8/5/4/2 if the greatest common diviser of the volume of the world and 200 is 100/50/40/25/20/10/8/5/4/2 | [Header editing] | |
| unprocessed-tickCount mismatch if the volume of the world modulo 200 is not a multiple of 8 | [Header editing] | |
| xSpawn or zSpawn above 4,194,304 | [Header editing] | Cannot be loaded without softlocking if the position is outside the world. |
| ySpawn below -67,108,864 | [Header editing] | |
| ySpawn not representable as a float | [Header editing] | |
| ySpawn -16,777,215 ir -33,554,432 | [Header editing] | |
| ySpawn above 16,777,216 | [Header editing] | |
| null name or creator | [Header editing] | |
| entities ArrayList capacity other than 10,15,22,33,49,73,109,163,244, or 366 | [Header editing] | |

[Header editing]: complex-methods/header-editing.md