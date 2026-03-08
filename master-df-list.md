This serves as a list of all discontinued features mentioned in this changelog.

# Blocks
## Individual blocks

| Discontinued Feature | Version range (path) | Notes |
| --- | --- | --- |
| water (`08`), calmWater (`09`) | 0.0.12a_03-200018 | New worlds only, recontinued using [Header editing] and in 0.0.13a_03. |
| lava (`0A`), calmLava (`0B`) between Y 22 and Y 27 | 0.0.12a_03-200018 | New worlds only, recontinued using [Header editing] and in 0.0.13a_03. |
| lava (`0A`), calmLava (`0B`) between Y 28 and Y 31 | 0.0.12a_03-200018 | New worlds only, recontinued using [Header editing]. |
| water (`08`), calmWater (`09`) | [Header editing] | |
| water (`08`) or calmWater (`09`) between Y 32 and Y 63 | [Header editing] | |
| calmWater (`09`) in unnatural non-ticking locations | [Header editing] | |
| lava (`0A`) or calmLava (`0B`) between Y 22 and Y 31 | [Header editing] | |
| lava (`0A`) or calmLava (`0B`) between Y 32 and Y 63 | [Header editing] | |
| calmLava (`0B`) in unnatural non-ticking locations | [Header editing] | |
| block ID `0C`-`FF` | [Header editing] | |

## Block configurations

| Discontinued Feature | Version range (path) | Notes |
| --- | --- | --- |
| water (`08`) or calmWater (`09`) below lava (`0A`) or calmLava (`0B`) | 0.0.12a_03-200018 | New worlds only, recontinued using [Header editing] |
| calmWater (`09`) or calmLava (`0B`) above or next to ID `00` | (0.0.12a_03-200018) -> (rd-132211-launcher - 0.0.11a-launcher) | Worlds generated in 0.0.12a_03-200018 only, recontinued using [Header editing] |
| calmWater (`09`) at the world border at non-ticking coordinates above or below rock (`01`) | (0.0.12a_03-200018) -> (rd-132211-launcher - 0.0.11a-launcher) | Worlds generated in 0.0.12a_03-200018 only, recontinued using [Header editing] |
| calmWater (`09`) at the world border at non-ticking coordinates next to grass (`02`) | (0.0.12a_03-200018) -> (rd-160052-launcher - 0.0.11a-launcher) | Worlds generated in 0.0.12a_03-200018 only, recontinued using [Header editing] and on newly generated worlds in 0.0.13a_03. |
| calmWater (`09`) at the world border at non-ticking coordinates above or below grass (`02`) | (0.0.12a_03-200018) -> (rd-160052-launcher - 0.0.11a-launcher) | Worlds generated in 0.0.12a_03-200018 only, recontinued using [Header editing]. |
| calmWater (`09`) at the world border at non-ticking coordinates adjacent to stoneBrick (`04`) or wood (`05`) | (0.0.12a_03-200018) -> (rd-160052-launcher - 0.0.11a-launcher) | Worlds generated in 0.0.12a_03-200018 only, recontinued using [Header editing]. |
| calmWater (`09`) at the world border at non-ticking coordinates below dirt (`03`) | (0.0.12a_03-200018) -> (rd-160052-launcher - 0.0.11a-launcher) | Worlds generated in 0.0.12a_03-200018 only, recontinued using [Header editing]. |
| calmWater (`09`) at the world border at non-ticking coordinates adjacent to bush (`06`) | (0.0.12a_03-200018) -> (rd-161348-launcher - 0.0.11a-launcher) | Worlds generated in 0.0.12a_03-200018 only, recontinued using [Header editing]. |
| calmLava (`0B`) above or next to ID `00` in a 32x64x512 world | (0.0.13a-launcher) -> (rd-132211-launcher - 0.0.11a-launcher) | Worlds generated in 0.0.13a-launcher only, recontinued using [Header editing]. |
| water (`08`) or calmWater (`09`) adjacent to lava (`0A`) or calmLava (`0B`) | [Header editing] | |
| calmWater (`09`) or calmLava (`0B`) above or next to ID `00` | [Header editing] | |
| calmWater (`09`) at the world border at non-ticking coordinates above or below rock (`01`) | [Header editing] | |
| calmWater (`09`) at the world border at non-ticking coordinates adjacent to grass (`02`), stoneBrick (`04`), wood (`05`) or bush (`06`) | [Header editing] | |
| calmWater (`09`) at the world border at non-ticking coordinates below dirt (`03`) | [Header editing] | |

# World data

| Discontinued Feature | Version range (path) | Notes |
| --- | --- | --- |
| "--" world name | (rd-132211-launcher - 0.0.12a_03-200018) -> (0.0.13a-launcher - ???) | |
| "unknown" creator | (rd-132211-launcher - 0.0.12a_03-200018) -> (0.0.13a-launcher) | Recontinued on newly generated worlds in 0.0.13a_03. |
| World dimensions of 32x64x256 | 0.0.13-launcher | New worlds only, partially recontinued using [Header editing] (can't be fully recreated for most create time values, see page for more details). |
| World dimensions other than 256x64x256 | [Header editing] | |
| World name other than "--" or "A New World" | [Header editing] | |
| Creator other than "noname" | [Header editing] | Many variants recontinued on newly generated worlds in 0.0.13a_03. |
| Creator containing null, horizontal tab, line feed, form feed, carriage return or surrogates | [Header editing] | |
| Creator starting or ending with space or a C0 control character | [Header editing] | |

[Header editing]: complex-methods/header-editing.md