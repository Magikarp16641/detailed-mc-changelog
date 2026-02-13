Between 0.0.13a-launcher and 0.0.13a_03-launcher the world is stored in a gzipped file called "level.dat". The save format is identical to the [previous](block-byte-array.md) with a header with additional information prepended.

The file consists of the following:

| Data | Length (bytes) | Description |
| --- | --- | --- |
| magic number | 4 | A number used to identify the save format. Always `27 1B B7 88`. |
| version | 1 | A number used to identify the save format. Always `01`. |
| name length | 2 | The length of the world name in bytes. |
| name | variable | The name of the world encoded in MUTF-8. |
| creator length | 2 | The length of the creator name in bytes. |
| creator | variable | The creator name encoded in MUTF-8. |
| create time | 8 | The creation time of the world, measured in milliseconds since midnight 1970-01-01 UTC. |
| width | 2 | The width of the world along the X axis. |
| height | 2 | The height of the world along the Z axis. |
| depth | 2 | The depth of the world along the Y axis. |
| block | variable | Block IDs listed in the same XZY order as the [previous](block-byte-array.md) format. |

Table of block IDs and their corresponding blocks:

| ID | Block | Version added |
| :---: | --- | --- |
| `01` | rock | rd-160052-launcher |
| `02` | grass | rd-160052-launcher |
| `03` | dirt | rd-160052-launcher |
| `04` | stoneBrick | rd-160052-launcher |
| `05` | wood | rd-160052-launcher |
| `06` | bush | rd-161348-launcher |
| `07` | unbreakable | 0.0.12a_03-200018 |
| `08` | water | 0.0.12a_03-200018 |
| `09` | calmWater | 0.0.12a_03-200018 |
| `0A` | lava | 0.0.12a_03-200018 |
| `0B` | calmLava | 0.0.12a_03-200018 |