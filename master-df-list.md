This serves as a list of all discontinued features mentioned in this changelog.

# Blocks
## Individual blocks
| Discontinued Feature | Version range (path) | Notes |
| --- | --- | --- |
| Block ID `00` at the world edge between Y 30 and Y 31 | rd-132211-launcher - 0.0.13a_03-launcher | |
| water (`08`) or calmWater (`09`) | 0.0.12a_03-200018 | Recontinued in 0.0.13a_03 or using [header editing]. |
| lava (`0A`) or calmLava (`0B`) between Y 22 and Y 31 | 0.0.12a_03-200018 | Recontinued between Y 22 and Y 27 in 0.0.13a_03. Recontinued using [header editing] or using a hacked client or [protocol mismatch] in 1.2 (classic server). |
| unbreakable (`07`) | [Header editing] | Also possible using a hacked client or [protocol mismatch] in 1.2 (classic server). |
| water (`08`) or calmWater (`09`) | [Header editing] | Recontinued in 0.0.13a_03. |
| water (`08`) or calmWater (`09`) between Y 32 and Y 63 | [Header editing] | Also possible using a hacked client or [protocol mismatch] in 1.2 (classic server). |
| calmWater (`09`) in unnatural non-ticking locations | [Header editing] | Recontinued in 0.0.14a_08. |
| lava (`0A`) or calmLava (`0B`) between Y 22 and Y 63 | [Header editing] | Recontinued between Y 22 and Y 27 in 0.0.13a_03. Also possible using a hacked client or [protocol mismatch] in 1.2 (classic server). |
| calmLava (`0B`) in unnatural non-ticking locations | [Header editing] | Recontinued in 0.0.14a_08. |
| sand (`0C`) or gravel (`0D`) | [Header editing] | Recontinued in 0.0.14a_08. |
| goldOre (`0E`), ironOre (`0F`) or coalOre (`10`) | [Header editing] | Recontinued in 0.0.14a_08. |
| goldOre (`0E`), ironOre (`0F`) or coalOre (`10`) at world edge, Y 0 or Y 63 | [Header editing] | Also possible using a hacked client or [protocol mismatch] in 1.2 (classic server). |
| treeTrunk (`11`) or leaves (`12`) | [Header editing] | Recontinued in 0.0.14a_08. |
| Block ID `13`-`FF` | [Header editing] | |
| unbreakable (`07`) | 1.2 (classic server + hacked client) | Also possible using a 0.0.15a-05311904 client or using [header editing]. |
| water (`08`) or calmWater (`09`) between Y 32 and Y 63 | 1.2 (classic server + hacked client) | Also possible using a 0.0.15a-05311904 client or using [header editing]. |
| lava (`0A`) or calmLava (`0B`) between Y 28 and Y 63 | 1.2 (classic server + hacked client) | Also possible using a 0.0.15a-05311904 client or using [header editing]. |
| goldOre (`0E`), ironOre (`0F`) or coalOre (`10`) at world edge, Y 0 or Y 63 | 1.2 (classic server + hacked client) | Also possible using a 0.0.15a-05311904 client or using [header editing]. |
| unbreakable (`07`) | 1.2 (classic server + 0.0.15a-05311904) | Using [protocol mismatch]. Also possible using a hacked client or using [header editing]. |
| water (`08`) or calmWater (`09`) between Y 32 and Y 63 | 1.2 (classic server + 0.0.15a-05311904) | Using [protocol mismatch]. Also possible using a hacked client or using [header editing]. |
| lava (`0A`) or calmLava (`0B`) between Y 28 and Y 63 | 1.2 (classic server + 0.0.15a-05311904) | Using [protocol mismatch]. Also possible using a hacked client or using [header editing]. |
| goldOre (`0E`), ironOre (`0F`) or coalOre (`10`) at world edge, Y 0 or Y 63 | 1.2 (classic server + 0.0.15a-05311904) | Using [protocol mismatch]. Also possible using a hacked client or using [header editing]. |

## Block configurations
| Discontinued Feature | Version range (path) | Notes |
| --- | --- | --- |
| water (`08`) or calmWater (`09`) below lava (`0A`) or calmLava (`0B`) | 0.0.12a_03-200018 | Recontinued using [header editing]. |
| calmWater (`09`) above or next to block ID `00` | {0.0.12a_03-200018} -> {rd-132211-launcher - 0.0.11a-launcher} | Recontinued by downgrading calmWater from 0.0.13a_03 or later, using [header editing], or using a hacked client or [protocol mismatch] in 1.2 (classic server). |
| calmWater (`09`) at the world border at non-ticking coordinates above or below rock (`01`) | {0.0.12a_03-200018} -> {rd-132211-launcher - 0.0.11a-launcher} | Recontinued in 0.0.14a_08 or using [header editing]. |
| calmWater (`09`) at the world border at non-ticking coordinates adjacent to grass (`02`), stoneBrick (`04`) or wood (`05`) | {0.0.12a_03-200018} -> {rd-160052-launcher - 0.0.11a-launcher} | Variant horizontally adjacent to grass recontinued in 0.0.13a_03. Recontinued in 0.0.14a_08 or using [header editing]. |
| calmWater (`09`) at the world border at non-ticking coordinates below dirt (`03`) | {0.0.12a_03-200018} -> {rd-160052-launcher - 0.0.11a-launcher} | Recontinued in 0.0.14a_08 or using [header editing]. |
| calmWater (`09`) at the world border at non-ticking coordinates adjacent to bush (`06`) | {0.0.12a_03-200018} -> {rd-161348-launcher - 0.0.11a-launcher} | Recontinued in 0.0.14a_08 or using [header editing]. |
| calmLava (`0B`) between Y 22 and Y 31 above or next to block ID `00` | {0.0.12a_03-200018} -> {rd-132211-launcher - 0.0.11a-launcher} | Variant between Y 22 and Y 27 also possible by downgrading calmLava from 0.0.13a_03 or later. Recontinued using [header editing], or using a hacked client or [protocol mismatch] in 1.2 (classic server). |
| calmLava (`0B`) between Y 0 and Y 21 above or next to block ID `00` | {0.0.12a_03-200018 - ???} -> {rd-132211-launcher - 0.0.11a-launcher} | Also possible using [header editing], or using a hacked client or [protocol mismatch] in 1.2 (classic server). |
| water (`08`) or calmWater (`09`) adjacent to lava (`0A`) or calmLava (`0B`) | [Header editing] | |
| calmWater (`09`) or calmLava (`0B`) above or next to block ID `00` | [Header editing] | Also possible using a hacked client or [protocol mismatch] in 1.2 (classic server). |
| calmWater (`09`) at the world border at non-ticking coordinates above or below rock (`01`) | [Header editing] | Recontinued in 0.0.14a_08. |
| calmWater (`09`) at the world border at non-ticking coordinates adjacent to block ID `02` or `04`-`06` | [Header editing] | Recontinued in 0.0.14a_08. |
| calmWater (`09`) at the world border at non-ticking coordinates below dirt (`03`) | [Header editing] | Recontinued in 0.0.14a_08. |
| sand (`0C`) at world edge, Y 1 or between Y 32 and 63 above block ID `00` | [Header editing] | Also possible in a 256x64x256 world by downgrading sand to before 0.0.14a_08. Also possible in 0.0.16a_02 - ???. |
| sand (`0C`) above block ID `00` below block ID `01`-`06` or `08`-`12` | [Header editing] | Also possible in a 256x64x256 world by downgrading sand to before 0.0.14a_08. Also possible in 0.0.16a_02 - ???. |
| sand (`0C`) or gravel (`0D`) above block ID `00` next to block ID `04`-`06` or `11`-`12` | [Header editing] | Also possible in a 256x64x256 world by downgrading sand or gravel to before 0.0.14a_08. Variant of sand next to leaves also possible in certain locations and block configurations in 0.0.15a-05311904 or later. Also possible in 0.0.16a_02 - ???. |
| gravel (`0D`) at world edge, Y 1 or between Y 31 and 63 above block ID `00` | [Header editing] | Also possible in a 256x64x256 world by downgrading gravel to before 0.0.14a_08. Variant at Y 31 also possible in certain locations and block configurations in 0.0.14a_08. Also possible in 0.0.16a_02 - ???. |
| gravel (`0D`) above block ID `00` below block ID `00`-`06` or `08`-`12` | [Header editing] | Also possible in a 256x64x256 world by downgrading gravel to before 0.0.14a_08. Variant below block ID `00` also possible in certain locations and block configurations in 0.0.14a_08. Variant below rock also possible by downgrading floating gravel below water or calmWater to 0.0.14a_08. Variant below water or calmWater also possible in certain locations and block configurations in 0.0.15a-05311904 or later. Also possible in 0.0.16a_02 - ???. |
| grass (`02`) somewhere below goldOre(`0E`), ironOre (`0F`), coalOre (`10`), or sand (`0C`) or gravel (`0D`) above block ID `00` | [Header editing] | Also possible in a 256x64x256 world by downgrading sand, gravel, goldOre, ironOre or coalOre to before 0.0.14a_08. Also possible using a hacked client or [protocol mismatch] in 1.2 (classic server). Variant below floating sand or gravel also possible in 0.0.16a_02 - ???. |
| grass (`02`) below Y 5 at least 3 blocks below a ring of goldOre (`0E`), ironOre (`0F`), coalOre (`10`), or sand (`0C`) or gravel (`0D`) above block ID `00` | [Header editing] | Also possible in a 256x64x256 world by downgrading sand, gravel, goldOre, ironOre or coalOre. Variant with goldOre, ironOre or coalOre also possible using a hacked client or [protocol mismatch] in 1.2 (classic server). Variant with floating sand or gravel also possible in 0.0.16a_02 - ???. |
| A pocket of water (`08`) or calmWater (`09`) below Y 29 surrounded on the sides and top by goldOre (`0E`), ironOre (`0F`), coalOre (`10`), or block ID `00` below sand (`0C`) or gravel (`0D`) | [Header editing] | Also possible using a hacked client or [protocol mismatch] in 1.2 (classic server). Variant below sand or gravel also possible in 0.0.16a_02 - ???. |
| Unnatural configuration of grass (`02`), goldOre (`0E`), ironOre (`0F`), coalOre (`10`), or sand (`0C`) or gravel (`0D`) above block ID `00` | [Header editing] | Variant without floating sand or gravel also possible using a hacked client or a [protocol mismatch] in 1.2 (classic server). Variant without goldOre, ironOre and coalOre also possible in 0.0.16a_02 - ???. |
| calmWater (`09`) at the world border at non-ticking coordinates above or below rock (`01`) | {0.0.13a_03 - 0.0.13a_03-launcher} -> {rd-132211-launcher - 0.0.11a-launcher} | Recontinued in 0.0.14a_08 or using [header editing]. |
| calmWater (`09`) at the world border at non-ticking coordinates above or below grass (`02`) | {0.0.13a_03 - 0.0.13a_03-launcher} -> {rd-160052-launcher - 0.0.11a-launcher} | Recontinued in 0.0.14a_08 or using [header editing]. |
| calmWater (`09`) at the world border at non-ticking coordinates adjacent to stoneBrick (`04`) or wood (`05`) | {0.0.13a_03 - 0.0.13a_03-launcher} -> {rd-160052-launcher - 0.0.11a-launcher} | Recontinued in 0.0.14a_08 or using [header editing]. |
| calmWater (`09`) at the world border at non-ticking coordinates below dirt (`03`) | {0.0.13a_03 - 0.0.13a_03-launcher} -> {rd-160052-launcher - 0.0.11a-launcher} | Recontinued in 0.0.14a_08 or using [header editing]. |
| calmWater (`09`) at the world border at non-ticking coordinates adjacent to bush (`06`) | {0.0.13a_03 - 0.0.13a_03-launcher} -> {rd-161348-launcher - 0.0.11a-launcher} | Recontinued in 0.0.14a_08 or using [header editing]. |
| calmWater (`09`) above or next to block ID `00` | {0.0.13a_03 - ???} -> {rd-132211-launcher - 0.0.11a-launcher} | Also possible using [header editing], or using a hacked client or [protocol mismatch] in 1.2 (classic server). |
| calmLava (`0B`) between Y 22 and Y 27 above or next to block ID `00` | {0.0.13a_03 - ???} -> {rd-132211-launcher - 0.0.11a-launcher} | Also possible using [header editing], or using a hacked client or [protocol mismatch] in 1.2 (classic server). |
| gravel (`0D`) above and below block ID `00` | 0.0.14a_08 | Also possible in a 256x64x256 world by downgrading gravel to before 0.0.14a_08 and in a 128x64x128 or 256x64x256 world using [header editing]. Recontinued in 0.0.16a_02. |
| sand (`0C`) or gravel (`0D`) at world edge, Y 1 or between Y 32 and Y 63 above block ID `00` | {0.0.14a_08 - ???} -> {rd-132211-launcher - 0.0.13a_03-launcher} | 256x64x256 world only. Also possible using [header editing] or in 0.0.16a_02 - ???. |
| sand (`0C`) above block ID `00` below block ID `01`-`06` or `08`-`12` | {0.0.14a_08 - ???} -> {rd-132211-launcher - 0.0.13a_03-launcher} | 256x64x256 world only. Also possible using [header editing] or in 0.0.16a_02 - ???. |
| sand (`0C`) or gravel (`0D`) above block ID `00` next to block ID `04`-`06` or `11`-`12` | {0.0.14a_08 - ???} -> {rd-132211-launcher - 0.0.13a_03-launcher} | 256x64x256 world only. Variant of sand next to leaves also possible in certain locations and block configurations in 0.0.15a-05311904 or later. Also possible using [header editing] or in 0.0.16a_02 - ???. |
| gravel (`0D`) above block ID `00` below block ID `00`-`06`, `08`-`09`, or `0A`-`12` | {0.0.14a_08 - ???} -> {rd-132211-launcher - 0.0.13a_03-launcher} | 256x64x256 world only. Variant below block ID `00` is also possible in certain locations and block configurations in 0.0.14a_08. Variant below rock (`01`) is also possible in certain locations and block configurations by downgrading floating gravel below water or calmWater to 0.0.14a_08. Variant below water (`08`) or calmWater (`09`) is also possible in certain locations and block configurationson in 0.0.15a-05311904 or later. Also possible using [header editing] or in 0.0.16a_02 - ???. |
| grass (`02`) somewhere below goldOre (`0E`), ironOre (`0F`), coalOre (`10`), or sand (`0C`) or gravel (`0D`) above block ID `00` | {0.0.14a_08 - ???} -> {rd-160052-launcher - 0.0.13a_03-launcher} | 256x64x256 world only. Variant below floating sand or gravel also possible in 0.0.16a_02 - ???. Variant below goldOre, ironOre or coalOre also possible using a hacked client or [protocol mismatch] in 1.2 (classic server). Also possible using [header editing]. |
| grass (`02`) below Y 5 at least 3 blocks below a ring of goldOre (`0E`), ironOre (`0F`), coalOre (`10`), or sand (`0C`) or gravel (`0D`) above block ID `00` | {0.0.14a_08 - ???} -> {rd-160052-launcher - 0.0.13a_03-launcher} | 256x64x256 world only. Variant below floating sand or gravel also possible in 0.0.16a_02 - ???. Variant below goldOre, ironOre or coalOre also possible using a hacked client or [protocol mismatch] in 1.2 (classic server). Also possible using [header editing]. |
| gravel (`0D`) above block ID `00` below rock (`01`) | {0.0.15a-05311904 - ???} -> {0.0.14a_08} | Also possible in a 128x64x128 or 256x64x256 world using [header editing]. Also possible in 0.0.16a_02 - ???. |
| calmWater (`09`) or calmLava (`0B`) above or next to block ID `00` | 1.2 (classic server + hacked client) | Also possible using [protocol mismatch] or using [header editing]. |
| grass (`02`) somewhere below goldOre(`0E`), ironOre (`0F`) or coalOre (`10`) | 1.2 (classic server + hacked client) | Also possible using [protocol mismatch] or using [header editing]. |
| grass (`02`) below Y 5 at least 3 blocks below a ring of goldOre (`0E`), ironOre (`0F`), coalOre (`10`), or naturally generated sand (`0C`) or gravel (`0D`) above block ID `00` | 1.2 (classic server + hacked client) | Also possible using [protocol mismatch] or using [header editing]. |
| A pocket of water (`08`) or calmWater (`09`) below Y 29 surrounded on the sides and top by goldOre (`0E`), ironOre (`0F`) or coalOre (`10`) | 1.2 (classic server + hacked client) | Also possible using [protocol mismatch] or using [header editing]. |
| Unnatural configuration of grass (`02`), goldOre (`0E`), ironOre (`0F`), coalOre (`10`), or sand (`0C`) or gravel (`0D`) above block ID `00` | 1.2 (classic server + hacked client) | sand and gravel have to be naturally generated. Also possible using [protocol mismatch] or using [header editing]. |
| calmWater (`09`) or calmLava (`0B`) above or next to block ID `00` | 1.2 (classic server + 0.0.15a-05311904) | Using [protocol mismatch]. | Also possible using a hacked client or using [header editing]. |
| grass (`02`) somewhere below goldOre(`0E`), ironOre (`0F`) or coalOre (`10`) | 1.2 (classic server + 0.0.15a-05311904) | Using [protocol mismatch]. Also possible using a hacked client or using [header editing]. |
| grass (`02`) below Y 5 at least 3 blocks below a ring of goldOre (`0E`), ironOre (`0F`), coalOre (`10`), or naturally generated sand (`0C`) or gravel (`0D`) above block ID `00` | 1.2 (classic server + 0.0.15a-05311904) | Using [protocol mismatch]. Also possible using a hacked client or using [header editing]. |
| A pocket of water (`08`) or calmWater (`09`) below Y 29 surrounded on the sides and top by goldOre (`0E`), ironOre (`0F`) or coalOre (`10`) | 1.2 (classic server + 0.0.15a-05311904) | Using [protocol mismatch]. Also possible using a hacked client or using [header editing]. |
| Unnatural configuration of grass (`02`), goldOre (`0E`), ironOre (`0F`), coalOre (`10`), or sand (`0C`) or gravel (`0D`) above block ID `00` | 1.2 (classic server + 0.0.15a-05311904) | Using [protocol mismatch]. sand and gravel have to be naturally generated. Also possible using a hacked client or using [header editing]. |
| sand (`0C`) at world edge, Y 1 or between Y 32 and Y 63 above block ID `00` | 0.0.16a_02 - ??? (client + server) | Also possible using [header editing]. |
| sand (`0C`) above block ID `00` below block ID `01`-`06` or `08`-`12` | 0.0.16a_02 - ??? (client + server) | Also possible using [header editing]. |
| sand (`0C`) above block ID `00` next to block ID `04`-`06` or `11` | 0.0.16a_02 - ??? (client + server) | Also possible using [header editing]. |
| sand (`0C`) above block ID `00` below Y 7 next to leaves (`12`) | 0.0.16a_02 - ??? (client + server) | Also possible using [header editing]. |
| sand (`0C`) above block ID `00` to leaves (`12`) on a side at most 4 blocks from the world edge | 0.0.16a_02 - ??? (client + server) | Also possible using [header editing]. |
| gravel (`0D`) at world edge, Y 1 or between Y 31 and Y 63 above block ID `00` | 0.0.16a_02 - ??? (client + server) | Also possible using [header editing]. |
| gravel (`0D`) above block ID `00` below block ID `00`-`06` or `0A`-`12` | 0.0.16a_02 - ??? (client + server) | Also possible using [header editing]. |
| gravel (`0D`) above block ID `00` next to block ID `04`-`06` or `11`-`12` | 0.0.16a_02 - ??? (client + server) | Also possible using [header editing]. |
| grass (`02`) somewhere below sand (`0C`) or gravel (`0D`) above block ID `00` | 0.0.16a_02 - ??? (client + server) | Also possible using [header editing]. |
| grass (`02`) below Y 5 at least 3 blocks below a ring of sand (`0C`) or gravel (`0D`) above block ID `00`, or naturally generated goldOre (`0E`), ironOre (`0F`) or coalOre (`10`) | 0.0.16a_02 - ??? (client + server) | Also possible using [header editing]. |
| Unnatural configuration of grass (`02`), goldOre (`0E`), ironOre (`0F`), coalOre (`10`), or sand (`0C`) or gravel (`0D`) above block ID `00` | 0.0.16a_02 - ??? (client + server) | goldOre, ironOre and coalOre have to be naturally generated. Also possible using [header editing]. |
| Unnatural configuration of grass (`02`), goldOre (`0E`), ironOre (`0F`), coalOre (`10`), or sand (`0C`) or gravel (`0D`) above block ID `00` | {1.2 (classic server + hacked client)} <-> {0.0.16a_02 - ??? (client + server)} | Also possible using [header editing]. |
| Unnatural configuration of grass (`02`), goldOre (`0E`), ironOre (`0F`), coalOre (`10`), or sand (`0C`) or gravel (`0D`) above block ID `00` | {1.2 (classic server + 0.0.15a-05311904)} <-> {0.0.16a_02 - ??? (client + server)} | Using [protocol mismatch]. Also possible using [header editing]. |

# Entities
| Discontinued Feature | Version range (path) | Notes |
| --- | --- | --- |
| Zombie with a field with the value of NaN | [Header editing] (0.0.14a_08 - ???) | Cannot be loaded on a server. |
| Zombie with bbHeight other than 1.8 | [Header editing] (0.0.14a_08 - ???) | Cannot be loaded on a server. |
| Zombie with bbWidth other than 0.6 | [Header editing] (0.0.14a_08 - ???) | Cannot be loaded on a server. |
| Zombie with heightOffset, xRot, xRotI, yRot, yRotI, or epsilon other than 0.0 | [Header editing] (0.0.14a_08 - ???) | Cannot be loaded on a server. |
| Zombie with x or z above 4194304.0 or below -4194304.0 | [Header editing] (0.0.14a_08 - ???) | Cannot be loaded on a server. |
| Zombie with horizontal velocity greater than 0.25068867 | [Header editing] (0.0.14a_08 - ???) | Cannot be loaded on a server. |
| Zombie with y above 16777216.0 | [Header editing] (0.0.14a_08 - ???) | Cannot be loaded on a server. |
| Zombie with yd above 0.4116 or below -3.919994| [Header editing] (0.0.14a_08 - ???) | Cannot be loaded on a server. |
| Zombie with position-velocity mismatch | [Header editing] (0.0.14a_08 - ???) | Cannot be loaded on a server. |
| Zombie with horizontal velocity-rot-rotA mismatch | [Header editing] (0.0.14a_08 - ???) | Cannot be loaded on a server. |
| Zombie with rot above 2.1474836E9 or below -1.3421773E8 | [Header editing] (0.0.14a_08 - ???) | Cannot be loaded on a server. |
| Zombie with rotA above 99.99962 or below -7.9999685 | [Header editing] (0.0.14a_08 - ???) | Cannot be loaded on a server. |
| Zombie with speed other than 1.0 | [Header editing] (0.0.14a_08 - ???) | Cannot be loaded on a server. |
| Zombie with timeOffs above 1239813.0 or below 0.0 | [Header editing] (0.0.14a_08 - ???) | Cannot be loaded on a server. |
| Zombie with timeOffs not a multiple of 1.376469E-10 | [Header editing] (0.0.14a_08 - ???) | Cannot be loaded on a server. |
| Zombie with sufficiently incorrectly sized hitbox | [Header editing] (0.0.14a_08 - ???) | Cannot be loaded on a server. |
| Zombie with a new Level object inside the level field | [Header editing] (0.0.14a_08 - ???) | Crashes the game if the zombie is inside the new level when rendering. Cannot be loaded on a server. |
| More than 256 zombies in a world | [Header editing] (0.0.14a_08 - ???) | Cannot be loaded on a server. |
| Multiple instances of a Zombie in the entities list | [Header editing] (0.0.14a_08 - ???) | Cannot be loaded on a server. |
| Multiple Zombies sharing the same hitbox | [Header editing] (0.0.14a_08 - ???) | Cannot be loaded on a server. |
| Entity entity | [Header editing] (0.0.14a_08 - ???) | |
| Particle entity (0.0.14a_08) | [Header editing] (0.0.14a_08) | Temporary. Can't be updated to 0.0.15a-05311904 or later due to a change in the serialVersionUID. |
| NetworkPlayer entity | [Header editing] (0.0.15a-05311904 - ???) | Crashes the game during rendering in 0.0.16a_02-081047 or later. Cannot be loaded on a server. |
| Particle entity (0.0.15a-05311904 - ???) | [Header editing] (0.0.15a-05311904 - ???) | Temporary. Cannot be loaded on a server. |

# World data
| Discontinued Feature | Version range (path) | Notes |
| --- | --- | --- |
| "--" name | {rd-132211-launcher - 0.0.12a_03-200018} -> {0.0.13a-launcher - ???} | |
| "unknown" creator | {rd-132211-launcher - 0.0.12a_03-200018} -> {0.0.13a-launcher} | Recontinued on newly generated worlds in 0.0.13a_03. |
| World dimensions of 32x64x512 | 0.0.13-launcher | New worlds only, partially recontinued using [header editing] (can't be fully recreated for most create time values, see page for more details). All combinations can be recreated using [header editing] in the [0.0.14a_08+ save format](save-formats/serialized-level.md). |
| World dimensions other than 256x64x256 | [Header editing] (0.0.13a-launcher - ???) | The set of wolrd dimensions that can be loaded depend on the version (see [header editing]). A 32x64x512 world is also possible in 0.0.13a-launcher. A 128x64x128 world is recontinued on new worlds in 0.0.14a_08. |
| name other than "--" or "A Nice World" | [Header editing] (0.0.13a-launcher - ???) | Between 0.0.13a-launcher and 0.0.13a_03 strings are limited to a maximum of 65,535 bytes. |
| creator other than "noname" | [Header editing] (0.0.13a-launcher - ???) | Many variants recontinued on newly generated worlds in 0.0.13a_03. Between 0.0.13a-launcher and 0.0.13a_03 strings are limited to a maximum of 65,535 bytes. |
| creator containing null, horizontal tab, line feed, form feed, carriage return, or surrogates | [Header editing] (0.0.13a-launcher - ???) | Between 0.0.13a-launcher and 0.0.13a_03 strings are limited to a maximum of 65,535 bytes. |
| creator starting or ending with space or a C0 control character | [Header editing] (0.0.13a-launcher - ???) | Between 0.0.13a-launcher and 0.0.13a_03 strings are limited to a maximum of 65,535 bytes. |
| creator other than "--" | 0.0.13a_03 - ??? (client only) | |
| World dimensions of 128x64x128 | 0.0.14a_08 - ??? (client only) | Also possible using [header editing]. |
| World dimensions of 512x64x512 | 0.0.14a_08 - ??? (client only) | |
| rotSpawn above 9.0071993E15 or below -9.0071993E15 | [Header editing] (0.0.14a_08 - ???) | |
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
[Protocol mismatch]: complex-methods/protocol-mismatch.md