The [save format](../save-formats/early-classic.md) used between 0.0.13a-launcher and 0.0.13a_03-launcher includes additional data about the world at the beginning of the file. Loading those worlds between rd-132211-launcher and 0.0.12a_03-200018 causes the extra data to be interpreted as blocks, which can subsequently be modified by block breaking or placing.

While this can be done in versions up to 0.0.12a_03-200018, opening such a world in rd-160052-launcher the game will crash shortly after loading when a chunk with invalid block IDs is rendered. Nevertheless it is still possible to place and break blocks in that short window (especially on lower framerates, since there is a limit to the number of chunks that can be rebuilt in a frame). This page will for the most part assume all editing is done by setting bytes to either `00` or `01`, with more unconventional methods being mentioned in their own section.

# Basic techniques
## Invalidating the header
The simplest edit possible is invalidating the header, that is editing it in such a way that newer versions don't recognize it. This is possible by either editing the magic number (bytes 0x00 through 0x03) in any way, or by editing the version number (byte 0x04) to be higher than 1. Editing the version number requires using rd-160052-launcher or later and as such is much more difficult.

Invalidating the header converts all header bytes to blocks, potentially creating otherwise unobtainable block IDs, and in the process shifting all blocks of the world to make room, potentially creating otherwise unobtainable block configurations or positions.

## Editing field contents
Performing any edits other than invalidating the header requires additional care, as loading the world in any version before 0.0.13a-launcher discards all but the first 4,194,304 bytes. The world can't be loaded in rd-160052-launcher or later if there aren't enough bytes for all the blocks in the world, as such if the header isn't invalidated the world dimensions have to be small enough such that the volume of the world is sufficiently below 4,194,304 to fit the header. The world either has to be the 32x64x512 world generated in 0.0.13a-launcher or the world dimensions themselves have to be edited as well.

Any of the bytes in the world and creator names, the time created as well as any of the world dimensions can be edited. Editing either the width or height will shift blocks around to fit the new dimensions.

## Editing the length of strings
A more advanced and more powerful technique involves changing the length of the world name or creator fields. Doing so makes the data that comes after it be read from a different part of the header, allowing for many possibilities. Most notably increasing the length of the string allows for the create time and world dimensions to be read from the blocks array, providing much control to their values.

# Advanced techniques
## Header stacking
By invalidating a header and updating back to 0.0.13a-launcher or later a new header will be generated with the old header being at the start of the block array. Doing this before increasing the length of strings allows for the data being read from the old header, providing more options just valid block IDs give.

## Null byte conversion
The world name and creator fields are encoded using java's MUTF-8. A quirk of MUTF-8 is that the null character (U+0000) is encoded with the overlong encoding `C0 80` instead of `00` as UTF-8 dictates. When a world with `00` in one of these fields is loaded, instead of the game crashing the `00` is converted to `C0 80`. Notably this increases the string's length, since it's measured as the number of bytes, not characters. By repeatedly updating and downgrading while setting bytes in one of these fields to `00` it's possible to arbitrarily increase the length of the string up to 65,535 (`FF FF`). This can be used to get a byte with an arbitrary value.

By performing null byte conversion on both the world name and creator fields at once it is possible to create sequence of arbitrary bytes with values between `01` and `7F` up to tens of thousands of bytes long. Below is a step by step process.

| Step # | Name length | Name | Creator length | Creator | Notes |
| :---: | :---: | --- | :---: | --- | --- |
| 1 | `01 01` | 256 bytes, `01` | `01 xx` | ... | Get the name and creator fields in this state via null byte conversion. |
| 2 | `01 00` | 256 bytes | `01 01` | `xx` ... | Decrease the length of the name field by 1. |

This process can be repeated as long as there is room in the creator string. The steps above allow the creation of sequences up to about 250 bytes long. By replacing the `01` at the end of the world name with `80` (obtained from `00` converting to `C0 80`, it is possible to create sequences up to 32 thousand bytes long. Using the `C0` byte by decreasing the world name length by 2 increases the limit to about 49 thousand bytes.

Since the creator field also gets shortened in the second step, the world dimensions will be read from the end of the creator field. In order to not lose a large portion of the world's block, the relevant bytes can be set to `C0 80 C0 80 C0 80` with the `C0` bytes being manually changed to `00` during the second step. This will set the world's dimensions to 128x128x128, which will preserve 2,097,152 blocks.

# Uses
## Blocks
Below is a table of blocks and how they can be created from the header without having to use create time or null byte conversion.

| Block ID | Block Type | Obtainability | Recontinued version | Notes |
| :---: | --- | --- | --- | --- |
| `00` | N/A | Can be created in all header editing versions. | N/A | Not discontinued. |
| `01` | rock | Can be placed in all header editing versions. | N/A | Not discontinued. |
| `02` | grass | Length of "--" world name. Height of the 32x64x512 world. | N/A | Antidiscontinued on worlds created before rd-160052-launcher. |
| `03` | dirt | Can be placed in rd-160052-launcher or later. | N/A | Not discontinued. |
| `04` | stoneBrick | Can be placed in rd-160052-launcher or later. | N/A | Not discontinued. |
| `05` | wood | Can be placed in rd-160052-launcher or later. | N/A | Not discontinued. |
| `06` | bush | Lenght of "noname" creator name. Can be placed in rd-161348-launcher or later. | N/A | Not discontinued. |
| `07` | unbreakable | Length of "unknown" creator name. | ??? | |
| `08` | water | | 0.0.13a_03 | Briefly discontinued in 0.0.13a-launcher. Discontinued at Y 32 or above (Can be obtained from naturally generated water by shifting the world). Antidiscontinued on worlds created before 0.0.12a_03-200018. |
| `09` | calmWater | 0.0.13a_03 | Briefly discontinued in 0.0.13a-launcher. Discontinued at Y 32 or above and in unnatural non-ticking locations (Can be obtained from naturally generated calmWater by shifting the world). Antidiscontinued on worlds created before 0.0.12a_03-200018. |
| `0A` | lava | | N/A | Discontinued at Y 32 or above and briefly discontinued at Y 22 or above in 0.0.13a-launcher (Can be obtained from naturally generated lava by shifting the world). Antidiscontinued on worlds created before 0.0.12a_03-200018. |
| `0B` | calmLava | | N/A | Discontinued at Y 32 or above and in unnatural non-ticking locations, and briefly discontinued at Y 22 or above in 0.0.13a-launcher (Can be obtained from naturally generated lava by shifting the world). Antidiscontinued on worlds created before 0.0.12a_03-200018. |
| `0C` | N/A | World name length in worlds generated in 0.0.13a-launcher or later. | ??? | |
| `0D`-`1A` | N/A | | ??? | |
| `1B` | N/A | Part of the magic number. | ??? | |
| `1C`-`1F` | N/A | | ??? | |
| `20` | N/A | Part of the "A Nice World" world name. Width of the 32x64x512 world. | ??? | |
| `21`-`26` | N/A | | ??? | |
| `27` | N/A | Part of the magic number. | ??? | |
| `28`-`2C` | N/A | | ??? | |
| `2D` | N/A | Part of the "--" world name. | ??? | |
| `2E`-`3F` | N/A | | ??? | |
| `40` | N/A | World depth. | ??? | |
| `41` | N/A | Part of the "A Nice World" world name. | ??? | |
| `42`-`4D` | N/A | | ??? | |
| `4E` | N/A | Part of the "A Nice World" world name. | ??? | |
| `4F`-`56` | N/A | | ??? | |
| `57` | N/A | Part of the "A Nice World" world name. | ??? | |
| `58`-`60` | N/A | | ??? | |
| `61` | N/A | Part of the "noname" creator name. | ??? | |
| `62` | N/A | | ??? | |
| `63` | N/A | Part of the "A Nice World" world name. | ??? | |
| `6C` | N/A | Part of the "A Nice World" world name. | ??? | |
| `65` | N/A | Part of the "noname" creator name and the "A Nice World" world name. | ??? | |
| `66`-`68` | N/A | | ??? | |
| `69` | N/A | Part of the "A Nice World" world name. | ??? | |
| `6A` | N/A | | ??? | |
| `6B` | N/A | Part of the "unknown" creator name. | ??? | |
| `6C` | N/A | Part of the "A Nice World" world name. | ??? | |
| `6D` | N/A | Part of the "noname" creator name. | ??? | 
| `6E` | N/A | Part of the "unknown" and "noname" creator names. | ??? | |
| `6F` | N/A | Part of the "unknown" and "noname" creator names, and the "A Nice World" world name. | ??? | |
| `70`-`71` | N/A | | ??? | |
| `72` | N/A | Part of the "A Nice World" world name. | ??? | |
| `73`-`74` | N/A | | ??? | |
| `75` | N/A | Part of the "unknown" creator name. | ??? | |
| `76` | N/A | | ??? | |
| `77` | N/A | Part of the "unknown" creator name. | ??? | |
| `78`-`87` | N/A | | ??? | |
| `88` | N/A | Part of the magic number. | ??? | |
| `89`-`B6` | N/A | | ??? | |
| `B7` | N/A | Part of the magic number. | ??? | |
| `B8`-`FF` | N/A | | ??? | |

## Block configurations
Block IDs being created from the header and shifting blocks (either via invalidating the header or changing the world dimensions) both allow invalid block configurations. Those include :
- water or calmWater adjacent to lava or calmLava.
- calmWater or calmLava above or next to ID `00`.
- calmWater at the world border at non-ticking coordinates above or below rock.
- calmWater at the world border at non-ticking coordinates adjacent to grass, stoneBrick, wood or bush.
- calmWater at the world border at non-ticking coordinates below dirt.

## World data
The width, height and depth of the world can be edited to many different combinations of values from a range of -32,768 to 32,767. For the world to not immediately crash on load none of the dimensions can be negative, and their product has to be sufficiently below 4,194,304 for there to be enough bytes in the level.dat for each block to have an associated ID.

The world and creator names can be edited to many otherwise impossible values. The game will crash on loading if either of the names includes malformed UTF-8 or a 4 byte character. If either of the strings contain `00` bytes and converting them to `C0 80` brings the length of the string over 65,535 bytes, the world is able to be loaded, but can't be saved. 

The create time can be edited to be any value between -292275055-5-17 16:47:04.192 and 292278994-08-17 07:12:55.807. Most of these values are impossible to obtain otherwise, though the exact range depends on the operating system.