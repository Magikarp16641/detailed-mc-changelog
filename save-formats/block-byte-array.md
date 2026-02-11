Between rd-132211-launcher and 0.0.12a_03-200018 the world is stored in a gzipped file called "level.dat".

The file is a list of block IDs, each one being a byte. Blocks are stored starting at 0,0,0 going in the x, z and y directions (starting at the front-left-bottom corner going left-to-right, front-to-back and bottom-to-top based on the spawning angle).

In rd-132211-launcher and rd-132328-launcher an ID `01` indicated the existance of a block and any other ID is interpreted as the lack of a block.

In rd-160052-launcher and later the type of block is determined by the block ID.

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