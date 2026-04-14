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
| water (`08`) or calmWater (`09`) adjacent to lava (`0A`) or calmLava (`0B`) | [Header editing] | |
| calmWater (`09`) or calmLava (`0B`) above or next to ID `00` | [Header editing] | |
| calmWater (`09`) at the world border at non-ticking coordinates above or below rock (`01`) | [Header editing] | Recontinued in 0.0.14a_08. |
| calmWater (`09`) at the world border at non-ticking coordinates adjacent to block ID `02` or `04`-`06` | [Header editing] | Recontinued in 0.0.14a_08. |
| calmWater (`09`) at the world border at non-ticking coordinates below dirt (`03`) | [Header editing] | Recontinued in 0.0.14a_08. |
| sand (`0C`) or gravel (`0D`) at Y 1 above block ID `00` | [Header editing] | Also possible in a 256x64x256 world by downgrading sand or gravel to before 0.0.14a_08. |
| sand (`0C`) or gravel (`0D`) above Y 31 above block ID `00` | [Header editing] | Also possible in a 256x64x256 world by downgrading sand or gravel to before 0.0.14a_08. |
| sand (`0C`) or gravel (`0D`) at the world border above block ID `00` | [Header editing] | Also possible in a 256x64x256 world by downgrading sand or gravel to before 0.0.14a_08. |
| sand (`0C`) above block ID `00` below block ID `01`-`06` or `08`-`12` | [Header editing] | Also possible in a 256x64x256 world by downgrading sand to before 0.0.14a_08. |
| sand (`0C`) above block ID `00` next to block ID `04`-`06` or `11` | [Header editing] | Also possible in a 256x64x256 world by downgrading sand to before 0.0.14a_08. |
| sand (`0C`) above block ID `00` next to leaves (`12`) | [Header editing] | Also possible in a 256x64x256 world by downgrading sand to before 0.0.14a_08. Also possible in certain locations on new worlds generated in 0.0.15a-05311904 or later. |
| gravel (`0D`) above and below block ID `00` | [Header editing] | Also possible in certain locations on new worlds generated in 0.0.14a_08. Also possible in a 256x64x256 world by downgrading gravel to before 0.0.14a_08. |
| gravel (`0D`) above block ID `00` below rock (`01`) | [Header editing] | Also possible in a 256x64x256 world by downgrading gravel to before 0.0.14a_08. Also possible in certain locations by downgrading floating gravel below water or calmWater to 0.0.14a_08. |
| gravel (`0D`) above block ID `00` below block ID `02`-`06` or `0A`-`12` | [Header editing] | Also possible in a 256x64x256 world by downgrading gravel to before 0.0.14a_08. |
| gravel (`0D`) above block ID `00` below water (`08`) or calmWater (`09`) | [Header editing] | Also possible in a 256x64x256 world by downgrading gravel to before 0.0.14a_08. Also possible in certain locations on new worlds generated in 0.0.15a-05311904 or later. |
| gravel (`0D`) above block ID `00` next to block ID `04`-`06` or `11`-`12` | [Header editing] | Also possible in a 256x64x256 world by downgrading gravel to before 0.0.14a_08. |
| grass (`02`) somewhere below goldOre(`0E`), ironOre (`0F`) or coalOre (`10`) | [Header editing] | Also possible in a 256x64x256 world by downgrading goldOre, ironOre or coalOre to before 0.0.14a_08. |
| A pocket of water (`08`) or calmWater (`09`) surrounded on the sides and top by goldOre(`0E`), ironOre (`0F`) or coalOre (`10`) below Y 29 | [Header editing] | |
| gravel (`0D`) above and below block ID `00` | 0.0.14a_08 | Worlds generated in 0.0.14a_08 only. Also possible in a 128x64x128 or 256x64x256 world using [header editing] and in a 256x64x256 world by downgrading gravel to before 0.0.14a_08. |
| sand (`0C`) or gravel (`0D`) at Y 1 above block ID `00` | (0.0.14a_08 - ???) -> (0.0.13-launcher - 0.0.13a_03-launcher) | 256x64x256 world only. Also possible using [header editing]. |
| sand (`0C`) or gravel (`0D`) above Y 31 above block ID `00` | (0.0.14a_08 - ???) -> (0.0.13-launcher - 0.0.13a_03-launcher) | 256x64x256 world only. Also possible using [header editing]. |
| sand (`0C`) or gravel (`0D`) at the world border above block ID `00` | (0.0.14a_08 - ???) -> (0.0.13-launcher - 0.0.13a_03-launcher) | 256x64x256 world only. Also possible using [header editing]. |
| sand (`0C`) above block ID `00` below block ID `01`-`06` or `08`-`12` | (0.0.14a_08 - ???) -> (0.0.13-launcher - 0.0.13a_03-launcher) | 256x64x256 world only. Also possible using [header editing]. |
| sand (`0C`) above block ID `00` next to block ID `04`-`06` or `11` | (0.0.14a_08 - ???) -> (0.0.13-launcher - 0.0.13a_03-launcher) | 256x64x256 world only. Also possible using [header editing]. |
| sand (`0C`) above block ID `00` next to leaves (`12`) | (0.0.14a_08 - ???) -> (0.0.13a-launcher - 0.0.13a_03-launcher) | 256x64x256 world only. Also possible using [header editing]. Also possible in certain locations on new worlds generated in 0.0.15a-05311904 or later. |
| gravel (`0D`) above and below block ID `00` | (0.0.14a_08 - ???) -> (0.0.13a-launcher - 0.0.13a_03-launcher) | 256x64x256 world only. Also possible in certain locations next to certain blocks worlds generated in 0.0.14a_08. Also possible using [header editing]. |
| gravel (`0D`) above block ID `00` below rock (`01`) | (0.0.14a_08 - ???) -> (0.0.13a-launcher - 0.0.13a_03-launcher) | 256x64x256 world only. Also possible using [header editing]. Also possible between Y 2 and 27 by downgrading floating gravel below water or calmWater to 0.0.14a_08. |
| gravel (`0D`) above block ID `00` below block ID `02`-`06` or `0A`-`12` | (0.0.14a_08 - ???) -> (0.0.13-launcher - 0.0.13a_03-launcher) | 256x64x256 world only. Also possible using [header editing]. |
| gravel (`0D`) above block ID `00` below water (`08`) or calmWater (`09`) | (0.0.14a_08) -> (0.0.13a-launcher - 0.0.13a_03-launcher) | 256x64x256 world only. Also possible using [header editing]. Recontinued on new worlds generated in 0.0.15a-05311904 or later. |
| gravel (`0D`) above block ID `00` next to block ID `04`-`06` or `11`-`12` | (0.0.14a_08 - ???) -> (0.0.13a-launcher - 0.0.13a_03-launcher) | 256x64x256 world only. Also possible using [header editing]. |
| grass (`02`) somewhere below goldOre(`0E`), ironOre (`0F`) or coalOre (`10`) | (0.0.14a_08 - ???) -> (0.0.13-launcher - 0.0.13a_03-launcher ) | 256x64x256 world only. Also possible using [header editing]. |
| gravel (`0D`) above block ID `00` below rock (`01`) | (0.0.15a-05311904 - ???) -> (0.0.14a_08) | World generated in 0.0.15a-05311904 or later only. Also possible in a 128x64x128 or 256x64x256 world using [header editing] and in a 256x64x256 world by dowgrading gravel to before 0.0.14a_08. |

# Entities
| Discontinued Feature | Version range (path) | Notes |
| --- | --- | --- |
| Zombie with bbHeight other than 1.8 | [Header editing] (0.0.14a_08 - ???) | |
| Zombie with bbWidth other than 0.6 | [Header editing] (0.0.14a_08 - ???) | |
| Zombie with heightOffest, xRot, xRotI, yRot, yRotI, or epsilon other than 0.0 | [Header editing] (0.0.14a_08 - ???) | |
| Zombie with x or z below -4194304.0 or above 4194304.0 | [Header editing] (0.0.14a_08 - ???) | |
| Zombie with horizontal velocity greater than 0.25068867 | [Header editing] (0.0.14a_08 - ???) | |
| Zombie with y above 16777216.0 | [Header editing] (0.0.14a_08 - ???) | |
| Zombie with yd below -3.919994 or above 0.4116 | [Header editing] (0.0.14a_08 - ???) | |
| Zombie with position-velocity mismatch | [Header editing] (0.0.14a_08 - ???) | |
| Zombie with horizontal velocity-rot-rotA mismatch | [Header editing] (0.0.14a_08 - ???) | |
| Zombie with rot below -1.3421773E8 or above 2.1474836E9 | [Header editing] (0.0.14a_08 - ???) | |
| Zombie with rotA below -7.9999685 or above 99.99962 | [Header editing] (0.0.14a_08 - ???) | |
| Zombie with speed other than 1.0 | [Header editing] (0.0.14a_08 - ???) | |
| Zombie with timeOffs below 0.0 or above 1239813.0 | [Header editing] (0.0.14a_08 - ???) | |
| Zombie with timeOffs not a multiple of 1.376469E-10 | [Header editing] (0.0.14a_08 - ???) | |
| Zombie with sufficiently incorrectly sized hitbox | [Header editing] (0.0.14a_08 - ???) | |
| Zombie with a new Level object inside the level field | [Header editing] (0.0.14a_08 - ???) | Crashes the game if the zombie is inside the new level when rendering. |
| More than 256 zombies in a world | [Header editing] (0.0.14a_08 - ???) | |
| Multiple instances of a Zombie in the entities list | [Header editing] (0.0.14a_08 - ???) | |
| Multiple Zombies sharing the same hitbox | [Header editing] (0.0.14a_08 - ???) | |
| Entity entity | [Header editing] (0.0.14a_08 - ???) | |
| Particle entity (0.0.14a_08) | [Header editing] (0.0.14a_08) | Temporary. Can't be updated to 0.0.15a-05311904 or later due to a change in the serialVersionUID. |
| NetworkPlayer entity | [Header editing] (0.0.15a-05311904 - ???) | |
| Particle entity (0.0.15a-05311904 - ???) | [Header editing] (0.0.15a-05311904 - ???) | Temporary. |

# World data
| Discontinued Feature | Version range (path) | Notes |
| --- | --- | --- |
| "--" name | (rd-132211-launcher - 0.0.12a_03-200018) -> (0.0.13a-launcher - ???) | |
| "unknown" creator | (rd-132211-launcher - 0.0.12a_03-200018) -> (0.0.13a-launcher) | Recontinued on newly generated worlds in 0.0.13a_03. |
| World dimensions of 32x64x512 | 0.0.13-launcher | New worlds only, partially recontinued using [header editing] (can't be fully recreated for most create time values, see page for more details). All combinations can be recreated using [header editing] in the [0.0.14a_08+ save format](save-formats/serialized-level.md). |
| World dimensions other than 256x64x256 | [Header editing] (0.0.13a-launcher - ???) | Restrictions on what the world dimensions can be are detailed on the [header editing] page. A 32x64x512 world is also possible in 0.0.13a-launcher. A 128x64x128 world is recontinued on new worlds in 0.0.14a_08. |
| name other than "--" or "A Nice World" | [Header editing] (0.0.13a-launcher - ???) | Between 0.0.13a-launcher and 0.0.13a_03 strings are limited to a maximum of 65,535 bytes. |
| creator other than "noname" | [Header editing] (0.0.13a-launcher - ???) | Many variants recontinued on newly generated worlds in 0.0.13a_03. Between 0.0.13a-launcher and 0.0.13a_03 strings are limited to a maximum of 65,535 bytes. |
| creator containing null, horizontal tab, line feed, form feed, carriage return, or surrogates | [Header editing] (0.0.13a-launcher - ???) | Between 0.0.13a-launcher and 0.0.13a_03 strings are limited to a maximum of 65,535 bytes. |
| creator starting or ending with space or a C0 control character | [Header editing] (0.0.13a-launcher - ???) | Between 0.0.13a-launcher and 0.0.13a_03 strings are limited to a maximum of 65,535 bytes. |
| rotSpawn above 9.0071993E15 | [Header editing] (0.0.14a_08 - ???) | |
| rotSpawn not a multiple of 2^-25 | [Header editing] (0.0.14a_08 - ???) | |
| unprocessed other than 0 if the volume of the world is a multiple of 200 | [Header editing] (0.0.14a_08 - ???) | |
| unprocessed not a multiple of 100/50/40/25/20/10/8/5/4/2 if the greatest common diviser of the volume of the world and 200 is 100/50/40/25/20/10/8/5/4/2 | [Header editing] (0.0.14a_08 - ???) | |
| unprocessed-tickCount mismatch if the volume of the world modulo 200 is not a multiple of 8 | [Header editing] (0.0.14a_08 - ???) | |
| ySpawn below -67,108,864 | [Header editing] (0.0.14a_08 - ???) | |
| ySpawn not representable as a float | [Header editing] (0.0.14a_08 - ???) | |
| ySpawn -16,777,215 ir -33,554,432 | [Header editing] (0.0.14a_08 - ???) | |
| ySpawn above 16,777,216 | [Header editing] (0.0.14a_08 - ???) | |
| null name or creator | [Header editing] (0.0.14a_08 - ???) | |
| entities ArrayList capacity other than 10,15,22,33,49,73,109,163,244, or 366 | [Header editing] (0.0.14a_08 - ???) | |

[Header editing]: complex-methods/header-editing.md