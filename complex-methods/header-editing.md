The [save](../save-formats/early-classic.md) [formats](../save-formats/serialized-level.md) used between 0.0.13a-launcher and 0.0.13a_03-launcher and between 0.0.14a_08 and ??? include additional data about the world apart from the blocks. Loading those worlds between rd-132211-launcher and 0.0.12a_03-200018 causes the extra data to be interpreted as blocks, which can subsequently be modified by block breaking or placing.

While this can be done in versions up to 0.0.12a_03-200018, opening such a world in rd-160052-launcher the game will crash shortly after loading when a chunk with invalid block IDs is rendered. Nevertheless it is still possible to place and break blocks in that short window (especially on lower framerates, since there is a limit to the number of chunks that can be rebuilt in a frame). This page will for the most part assume all editing is done by setting bytes to either `00` or `01`, with more unconventional methods being mentioned in their own section.

# Manipulation techniques
## Invalidating the header
The simplest edit possible is invalidating the header, that is editing it in such a way that newer versions don't recognize it. This is possible by either editing the magic number (bytes 0x00 through 0x03) in any way, or by editing the version number (byte 0x04) to be higher than 1. Editing the version number requires using rd-160052-launcher or later and as such is much more difficult.

Invalidating the header converts all header bytes to blocks, potentially creating otherwise unobtainable block IDs, and in the process shifting all blocks of the world to make room, potentially creating otherwise unobtainable block configurations or positions.

## Editing field contents
Performing any edits other than invalidating the header requires additional care, as loading the world in any version before 0.0.13a-launcher discards all but the first 4,194,304 bytes. The world can't be loaded in rd-160052-launcher or later if there aren't enough bytes for all the blocks in the world, as such if the header isn't invalidated the world dimensions have to be small enough such that the volume of the world is sufficiently below 4,194,304 to fit the header. The world either has to be the 32x64x512 world generated in 0.0.13a-launcher or the world dimensions themselves have to be edited as well.

## Editing the length of strings
A more advanced and more powerful technique involves changing the length of the world name or creator fields. Doing so makes the data that comes after it be read from a different part of the header, allowing for many possibilities. Most notably increasing the length of the string allows for the create time and world dimensions to be read from the blocks array, providing much control to their values.

Creating a world in 0.0.13a_03 or later makes it possible to set the creator field to almost any UTF-8 string up to 65,535 bytes long. The string cannot start or end with a character with the codepoint of U+0020 or below and the string cannot contain any of the following character codepoints: U+0000, U+0009-U+000A, U+000C-U+000D, U+D800-U+DFFF, U+10000-U+10FFFF.

## Header stacking
By invalidating a header and updating back to 0.0.13a-launcher or later a new header will be generated with the old header being at the start of the block array. Doing this before increasing the length of strings allows for the data being read from the old header, providing more options just valid block IDs give.

## Manual downgrading
Changing the version number in [serialized level format](../save-formats/serialized-level) world (byte at position 4) to `00` or `01` makes it be interpreted as an [early classic](../save-formats/early-classic.md) world. This can be used to to set the createTime, the world dimensions and partially the world name and creator name using serialized level fields which, depending on the field, might be simple to set to an almost arbitrary value.

## Null byte conversion
The world name and creator fields are encoded using java's MUTF-8. A quirk of MUTF-8 is that the null character (U+0000) is encoded with the overlong encoding `C0 80` instead of `00` as UTF-8 dictates. When a world with `00` in one of these fields is loaded, instead of the game crashing the `00` is converted to `C0 80`. Notably this increases the string's length, since it's measured as the number of bytes, not characters. By repeatedly updating and downgrading while setting bytes in one of these fields to `00` it's possible to arbitrarily increase the length of the string up to 65,535 (`FF FF`). This can be used to get a byte with an arbitrary value.

By performing null byte conversion on both the world name and creator fields at once it is possible to create sequence of arbitrary bytes with values between `01` and `7F` up to tens of thousands of bytes long. Below is a step by step process.

| Step # | Name length | Name | Creator length | Creator | Notes |
| :---: | :---: | --- | :---: | --- | --- |
| 1 | `01 01` | 256 bytes, `01` | `01 xx` | ... | Get the name and creator fields in this state via null byte conversion. |
| 2 | `01 00` | 256 bytes | `01 01` | `xx` ... | Decrease the length of the name field by 1. |

This process can be repeated as long as there is room in the creator string. The steps above allow the creation of sequences up to about 250 bytes long. By replacing the `01` at the end of the world name with `80` (obtained from `00` converting to `C0 80`, it is possible to create sequences up to 32 thousand bytes long. Using the `C0` byte by decreasing the world name length by 2 increases the limit to about 49 thousand bytes.

Since the creator field also gets shortened in the second step, the world dimensions will be read from the end of the creator field. In order to not lose a large portion of the world's block, the relevant bytes can be set to `C0 80 C0 80 C0 80` with the `C0` bytes being manually changed to `00` during the second step. This will set the world's dimensions to 128x128x128, which will preserve 2,097,152 blocks.

## Field description corruption
By changing the name of a field in the field description, the field will effectively be reset to its default value. For primitive data types this isn't useful, as the value can be set to 0 directly instead. For non-primitive data types this will set their value to `null`.

## Custom field description creation
Via creative usage of null byte conversion and other manipulation techniques, it's possible to write custom field descriptions.
- If new fields are added it's possible to delete sequences of bytes, as they won't be serialized again after being loaded.
- If existing fields are written in a different order it's possible to reorder sequences of bytes, as fields are always serialized in the same order.
  - Primitive data types are always serialized first, otherwise fields are sorted alphabetically.

# Uses
## Blocks
Below is a table of blocks and how they can be created from the header without having to use create time or null byte conversion.

| Block ID | Block Type | Recontinued version | Notes |
| :---: | --- | --- | --- |
| `00` | N/A | rd-132211-launcher | Not discontinued. |
| `01` | rock | rd-132211-launcher | Not discontinued. |
| `02` | grass | rd-160052-launcher | Not discontinued. |
| `03` | dirt | rd-160052-launcher | Not discontinued. |
| `04` | stoneBrick | rd-160052-launcher | Not discontinued. |
| `05` | wood | rd-160052-launcher | Not discontinued. |
| `06` | bush | rd-161348-launcher | Not discontinued. |
| `07` | unbreakable | N/A | Also possinble using a hacked client or [protocol mismatch](/protocol-mismatch.md) in 1.2 (classic server). |
| `08` | water | 0.0.12a_03-200018 | Briefly discontinued in 0.0.13a-launcher. Discontinued at Y 32 or above. |
| `09` | calmWater | 0.0.12a_03-200018 | Briefly discontinued in 0.0.13a-launcher. Discontinued at Y 32 or above and in unnatural non-ticking locations (before 0.0.14a_08). |
| `0A` | lava | 0.0.12a_03-200018 | Discontinued at Y 32 or above and briefly discontinued at Y 22 or above in 0.0.13a-launcher. |
| `0B` | calmLava | 0.0.12a_03-200018 | Discontinued at Y 32 or above and in unnatural non-ticking locations, and briefly discontinued at Y 22 or above in 0.0.13a-launcher. |
| `0C` | sand | 0.0.14a_08 | |
| `0D` | gravel | 0.0.14a_08 | |
| `0E` | goldOre | 0.0.14a_08 | |
| `0F` | ironOre | 0.0.14a_08 | |
| `10` | coalOre | 0.0.14a_08 | |
| `11` | treeTrunk | 0.0.14a_08 | |
| `12` | leaves | 0.0.14a_08 | |
| `13`-`FF` | N/A | N/A | |

## Block configurations
Block IDs being created from the header and shifting blocks (either via invalidating the header or changing the world dimensions) both allow invalid block configurations. Block configurations that are discontinued at some point include:
- water or calmWater adjacent to lava or calmLava.
- calmWater or calmLava above or next to block ID `00`.
- calmWater at the world border at non-ticking coordinates above or below rock.
- calmWater at the world border at non-ticking coordinates adjacent to grass, stoneBrick, wood or bush.
- calmWater at the world border at non-ticking coordinates below dirt.
- sand at world edge, Y 1, or between Y 32 and Y 63 above block ID `00`.
- sand above block ID `00` below block ID `01`-`06` or `08`-`12`.
- sand or gravel above block ID `00` next to block ID `04`-`06` or `11`-`12`.
- gravel at world edge, Y 1, or between Y 31 and Y 63 above block ID `00`.
- gravel above block ID `00` below block ID `00`-`06` or `08`-`12`.
- grass somewhere below goldOre, ironOre, coalOre, or sand or gravel above block ID `00`.
- grass below Y 5 at least 3 blocks below a ring of goldOre, ironOre, coalOre, or sand or gravel above block ID `00`.
- a pocket of water or calmWater below Y 29 surrounded on all sides and top by goldOre, ironOre, coalOre, or block ID `00` below sand or gravel.
- global block configurations which don't appear on any world seed.

## World data
### 0.0.13a-launcher - 0.0.13a_03-launcher
The width, height and depth of the world can be edited to many different combinations of values from a range of -32,768 to 32,767. For the world to not immediately crash on load none of the dimensions can be negative, and their product has to be sufficiently below 4,194,304 for there to be enough bytes in the level.dat for each block to have an associated ID. In 0.0.13a_03 or later the game crashes if either the width or height is 0.

The world and creator names can be edited to many otherwise impossible values. The only otherwise obtainable world names are "--" through updating older worlds to 0.0.13a-launcher or later, and "A Nice World" from generating a new world in 0.0.13a-launcher or later. "unknown" creator is also obtainable from updating older worlds to 0.0.13a-launcher, and "noname" creator is not discontinued and obtainable from generating a new world in 0.0.13a-launcher or later. Creator names that don't include U+0000, U+0009, U+000A, U+000C, U+000D, or a surrogate, and don't start or end with U+0020 or less are also possible by generating a new world in 0.0.13a_03 or later. The game will crash on loading if either of the names includes malformed UTF-8 or a 4 byte character. If either of the strings contain `00` bytes and converting them to `C0 80` brings the length of the string over 65,535 bytes, the world is able to be loaded, but can't be saved.

#### 0.0.13a-launcher world
The dimensions, world name and creator of the 32x64x256 world that can be generated in 0.0.13a-launcher can be fully recreated using header editing, however only certain values of create time can be created.

Using null conversion the create time can consist of the following:
 - ASCII character (`00`-`7F`)
 - Null (`C0 80`)
 - 2 byte utf-8 character (`C2`-`DF` followed by `80`-`BF`)
 - The last byte can be the start of a 2 byte character sequence (`C0` or `C2`-`DF`)

Additionally any byte of a multi-byte character can be replaced with the following:
 - `00`-`01`, `08` or `0A`
 - `02`-`06`
   - If the byte being replaced is the starting byte, all bytes that come before it in the create time have to be ASCII.
   - If the byte being replaced is the continuation byte, all bytes that come after it in the create time have to be ASCII.
 - `09` or `0B`
   - The byte being replaced cannot be the 3rd or 8th most significant byte in the create time.

If the world is generated in 0.0.13a_03 or 0.0.13a_03-launcher with the username being set correctly non-surrogate 3-byte characters can be used as well:
  - `E0` followed by `90`-`BF` followed by `80`-`BF`
  - `E1`-`EC` followed by 2 `80`-`BF` bytes
  - `ED` followed by `80`-`9F` followed by `80`-`BF`
  - `EE`-`EF` followed by 2 `80`-`BF` bytes
  - The last 2 bytes of the create time can be the first 2 bytes of a 3-byte character
  - Any of the bytes in 3-byte characters can be replaced following the same rules as 2-byte characters
  - If the create time consists of 2 3-byte characters separated by an ASCII character, the character can't be `09`, `0C` or `0D`.

### 0.0.14a_08 - ???
The width, height and depth of the world can be edited to many different combinations of values from a range of -2147483648 to 2147483647. The combinations that can be loaded without crashing depend on the version.

In client versions the width and height have to be positive and the depth has to be non-negative. The volume of the world has to be sufficiently below 4194304 for there to be enough bytes in the level.dat for each block to have an associated ID. The height or width cannot be 0 and the height or width can only be 1 if the spawn point is already set (Worlds with such height or width cannot be updated from between 0.0.13a-launcher and 0.0.13a_03-launcher). The area of the world has to be less than 2147483646 (only relevant due to the other limitations if the depth is 0).

Servers can load worlds as long as they meet the following criteria:
- $`width * height`$ is between 0 and 2147483645 when cast to an int.
- At least one of the following is true:
  - $`width`$ or $`height`$ is at most 0.
  - $`width * height`$ is at most 2147483645 and $`depth`$ is at most 1.
  - $`width * height * depth`$ is sufficiently below 419304.
  - $`width * height`$ is at most 4194304 and $`width * height * depth`$ and $`width * height * (depth - 1)`$ are both non-negative and sufficently below 4194304 when cast to an int.
    - This also assumes that blocks on the "topmost" layer of the world are all solid. If any of them isn't the requirements become more constrained.
- Unless $`width`$ or $`height`$ are both at least 2, worlds can be loaded only if the spawn point isn't set to 0,0,0
Additionally extreme world sizes may experience issues due to random ticks, though technically this does not prevent the world from being loaded, since the world is first saved before any in-game ticks occur.
- If either $`width`$ or $`height`$ are at least 1073741825, the game gets stuck in an infinite loop.
- If $`width * height * depth`$ is more than the length of the blocks array, or if $`width`$, $`height`$, or $`depth`$ are less than 1, the world may crash from random ticks unless the product is at most 0 when cast to an int.
  - Some such combinations of world dimensions don't crash, though the exact set depends on the length of the blocks array.

All 0.0.13a-launcher worlds can be recreated in this save format.

Besides custom world dimensions the following field values are not otherwise possible:
- rotSpawn above 9.0071993E15
- rotSpawn not a multiple of 2^-25
- rotSpawn of Infinity, -Infinity, or NaN
- unprocessed other than 0 if the volume of the world is a multiple of 200
- unprocessed not a multiple of 100/50/40/25/20/10/8/5/4/2 if the greatest common diviser of the volume of the world and 200 is 100/50/40/25/20/10/8/5/4/2
- unprocessed tickCount mismatch if the volume of the world modulo 200 is not a multiple of 8
- xSpawn or zSpawn outside the world
  - Causes a softlock on load
- ySpawn below -67,108,864
- ySpawn not representable as a float
- ySpawn -16,777,215 or -33,554,432
- ySpawn above 16,777,216
- creator or name set to null
- creator containing null, horizontal tab, line feed, form feed, carriage return, or surrogates
- creator starting or ending with space or a C0 control character
- entities ArrayList capacity other than 10,15,22,33,49,73,109,163,244 or 366
- name other than "A Nice World"

## Entities
- Zombie with bbHeight other than 1.8
- Zombie with bbWidth other than 0.6
- Zombie with heightOffset, xRot, xRotI, yRot, yRotI or epsilon other than 0.0
- Zombie with x or z below -4194304.0 or above 4194304.0
- Zombie with horizontal velocity greater than 0.25068867
- Zombie with y above 16777216.0
- Zombie with yd below -3.919994 or above 0.4116
- Zombie with position-velocity mismatch
- Zombie with horizontal velocity-rot-rotA mismatch
- Zombie with rot below -1.3421773E8 or above 2.1474836E9
- Zombie with rotA below -7.9999685 or above 99.99962
- Zombie with speed other than 1.0
- Zombie with timeOffs below 0.0 or above 1239813.0
- Zombie with timeOffs not a multiple of 1.376469E-10
- Zombie with a sufficiently incorrectly sized hitbox
- Zombie with level as a new Level object
  - Crashes the game if the zombie is ever inside the bounds of the new level
- More than 256 zombies in the world
- Multiple instances of a Zombie in the entities list
- Multiple Zombies sharing a hitbox
- Entity entity
- Particle entity
  - Has a different serialVersionUID in 0.0.14a_08 and in 0.0.15a-05311904 and later
- Player entity
  - Crashes the game on the first game tick and therefore cannot be saved while playing on an applet
- NetworkPlayer entity
  - 0.0.15a-05311904 or later only

## Arbitrary Code Excecution
WIP