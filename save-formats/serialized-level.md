Starting in 0.0.14a_08, the world is saved using [Java's Serializable interface](https://docs.oracle.com/javase/6/docs/platform/serialization/spec/protocol.html).

The world save is a gzipped file called "level.dat" that contains the following:

| Data | Length (bytes) | Description |
| --- | :---: | --- |
| save magic number | 4 | A number used to identify the save format. Always `27 1B B7 88`. |
| save version | 1 | A number used to identify the save format. Always `02`. |
| stream magic number | 2 | Always `AC ED`. |
| stream version number | 2 | Always `00 05`. |
| Serialized level object | variable | A level object serialized using the Serializable interface. |

# 0.0.14a_08 - 0.0.23a_01
## com.mojang.minecraft.level.Level
The level object has the following fields:

| Field | Type | Description |
| --- | :---: | --- |
| createTime | long | The time when the world was created, measured in milliseconds since the Unix epoch. |
| depth | int | The depth of the world along the Y axis. |
| height | int | The height of the world along the Z axis. |
| rotSpawn | float | The yaw of the spawn point. |
| tickCount | int | Total number of ticks processed. |
| unprocessed | int | Used for fractional random ticks. Always below 200. |
| width | int | The width of the world along the X axis. |
| xSpawn | int | The X coordinate of the spawn point. |
| ySpawn | int | The Y coordinate of the spawn point. |
| zSpawn | int | The Z coordinate of the spawn point. |
| blocks | byte[] | The blocks inside the world. Block IDs are listed in the same XZY order as before. |
| creator | java.util.String | The creator name. |
| entities | java.util.ArrayList | List of the entities in the world. Can theoretically contain any entity, but practically always only contains zombies. |
| name | java.util.String | The world name. |

## com.mojang.minecraft.Entity
The Entity class is extended by the NetworkPlayer, Particle, Player, and Zombie classes. Levels typically only include zombies.

The Entity class has the following fields:

| Field | Type | Description |
| --- | :---: | --- |
| bbHeight | float | Hitbox height, only used during initialization. |
| bbWidth | float | Hitbox width, only used during initialization. |
| heightOffset | float | Vertical offset between the feet and the saved Y coordinate. Always 0.0. |
| horizontalCollision | boolean | If the entity collided with a wall last tick. |
| onGround | boolean | If the entity was grounded last tick.|
| removed | boolean | If the entity is supposed to be removed next tick. Cannot be saved as `true` |
| x | float | X position. |
| xRot | float | Pitch, only used for players. |
| xRotI | float | Unused, was supposed to be used for turn interpolation. Always 0.0. |
| xd | float | X velocity. |
| xo | float | X position in the previous tick. |
| y | float | Y position. |
| yRot | float | Yaw, only used for players. |
| yRotI | float | Unused, was supposed to be used for turn interpolation. Always 0.0. |
| yd | float | Y velocity. |
| yo | float | Y position in the previous tick. |
| z | float | Z position. |
| zd | float | Z velocity. |
| zo | float | Z position in the previous tick. |
| bb | com.mojang.minecraft.phys.AABB | The entity hitbox. |
| level | com.mojang.minecraft.level.Level | Always a reference to the original Level object (`71 00 7E 00 04`) |


### com.mojang.minecraft.character.Zombie
The Zombie class has the following fields:

| Field | Type | Description |
| --- | :---: | --- |
| rot | float | Yaw. Used instead of yRot. |
| rotA | float | Angular velocity. |
| speed | float | Animation speed. Always 1.0. |
| timeOffs | float | The offset of the animation. |

### com.mojang.minecraft.particle.Particle
The Particle class has the following fields. xd, yd, and zd share the same name as fields from the Entity class. The super classes fields are unused.

| Field | Type | Description |
| --- | :---: | --- |
| age | int | Age of the particle, the particle is removed if age is greater than lifetime. |
| lifetime | int | Lifetime of the particle. |
| size | float | Visual size of the particle. |
| tex | int | Id of the texture used in the `terrain.png`. |
| uo | float | Random texture offset. |
| vo | float | Random texture offset. |
| xd | float | X velocity. |
| yd | float | Y velocity. |
| zd | float | Z velocity. |

### com.mojang.minecraft.player.Player
The Player class contains an input field, whose class cannot be serialized. As such the player can only be saved if the value of this field is null. When the entity is ticked this causes a NullPointerException, and since the game can only be ran from an applet, the player cannot be saved to file at all.

| Field | Type | Description |
| --- | :---: | --- |
| input | com.mojang.minecraft.player.a | Cannot be serialized. |

### com.mojang.minecraft.net.NetworkPlayer
The NetworkPlayer class has the following fields:

| Field | Type | Description |
| --- | :---: | --- |
| ticks | int | Number of times the network player has been ticked, used for the animation. |

## com.mojang.minecraft.phys.AABB
| Field | Type | Description |
| --- | :---: | --- |
| epsilon | float | Effectively increases the size of the hitbox. Always 0.0. |
| x0 | float | Negative X side coordinate. |
| x1 | float | Positive X side coordinate. |
| y0 | float | Negative Y side coordinate. |
| y1 | float | Positive Y side coordinate. |
| z0 | float | Negative Z side coordinate. |
| z1 | float | Positive Z side coordinate. |

# Block IDs
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
| `0C` | sand | 0.0.14a_08 |
| `0D` | gravel | 0.0.14a_08 |
| `0E` | goldOre | 0.0.14a_08 |
| `0F` | ironOre | 0.0.14a_08 |
| `10` | coalOre | 0.0.14a_08 |
| `11` | treeTrunk | 0.0.14a_08 |
| `12` | leaves | 0.0.14a_08 |

# Java serialization format
## Default serialized object format (simplified)
The Serializable interface can serialize many kinds of objects, most of which are not relevant to a Minecraft save file and as such many irrelevant bits of information are ommited. Classes can define a custom serialization format, such classes will be mentioend when relevant. Strings are written as their length as an unsigned short followed by an MUTF-8 representation of the string. The basic structure of the default format is as follows:

* TC_OBJECT constant (`73`)
* Class description
* Field values

### Class description
* TC_CLASSDESC constant (`72`)
* full class name
* serialVersionUID (8 bytes)
* flags (1 byte)
  * SC_WRITE_METHOD (`01`) - the class defines a custom write method
  * SC_SERIALIZABLE (`02`) - the class is serializable
  * SC_EXTERNALIZABLE (`04`) - the class is externalizable, not relevant for Minecraft
  * SC_BLOCK_DATA (`08`) - indicated externalizable data written in Block Data mode, not relevant for Minecraft
  * SC_ENUM (`10`) - indicates an enum, not relevant for Minecarft.
* number of fields (2 bytes)
* field descriptions
  * type (1 byte)
    * boolean - Z (`5A`)
	* byte - B (`42`)
	* short - S (`53`)
	* int - I (`49`)
	* float - F (`46`)
	* long - J (`4A`)
	* double - D (`44`)
	* array - [ (`5B`)
	* object - L (`4C`)
  * field name
  * type signature (array or object only)
* TC_ENDBLOCKDATA constant (`78`)
* super class
  * TC_NULL of there is no super class (`70`)
  * class description of the super class otherwise

### Field values
Packed data of the field values, in the same order as in the class description. Field values of super classes are listed first.

| Type | Length (bytes) | Notes |
| --- | :---: | --- |
| boolean | 1 | |
| byte | 1 | |
| short | 2 | |
| int | 4 | |
| float | 4 | |
| long | 8 | |
| double | 8 | |
| array | variable | Uses its own serialized array format |
| object | variable | Uses the serialized object format |
| object (string) | variable | Uses a custom format |

#### Array serialization
* TC_ARRAY constant (`75`)
* class description
* length of the array (4 bytes)
* packed contents of the array

#### String serialization
If the string is at most 65,535 bytes:
* TC_STRING constant (`74`)
* length of the string (2 bytes)
* MUTF-8 encoding of the string

If the string is at least 65,536 bytes:
* TC_LONGSTRING constant (`7C`)
* length of the string (8 bytes)

### References
If a class description or type signature was already written earlier in the data stream, or when the value of a field is an object serialized earlier in the stream. Any future instances of it can be replaced by a reference.

* TC_REFERENCE constant (`71`)
* `00 7E 00 00` + handle number

Handle numbers start at `00 00` and are incremented every new class description, type signature, object, array object or string object. Object and array handles are generated between the class description and the field values.

## Classes with a custom write method
## java.util.ArrayList
ArrayList has 1 int field named "size", whose value is equal to the number of elements it contains. After the field values the following is written:

* TC_BLOCKDATA constant (`77`)
* length of the blockdata header (`04`)
* capacity of the ArrayList
* packed serialized data of the objects the ArrayList contains
* TC_ENDBLOCKDATA constant (`78`)

## Table of serialVersionUIDs

| Class | Decimal | Hexadecimal | Versions |
| --- | :---: | :---: | :---: |
| com.mojang.minecraft.Entity | 0 | `00 00 00 00 00 00 00 00` | 0.0.14a_08 - ??? |
| com.mojang.minecraft.character.Zombie | 77479605454997290 | `01 13 43 4A 68 7B 87 2A` | 0.0.14a_08 - ??? |
| com.mojang.minecraft.level.Level | 0 | `00 00 00 00 00 00 00 00` | 0.0.14a_08 - ??? |
| com.mojang.minecraft.net.NetworkPlayer | 77479605454997290 | `01 13 43 4A 68 7B 87 2A` | 0.0.15a-05311904 - ??? |
| com.mojang.minecraft.particle.Particle | -635797757596879942 | `F7 2D 31 4E DD 72 B3 BA` | 0.0.14a_08 |
| com.mojang.minecraft.particle.Particle | -4069360689737339054 | `C7 86 BA 03 59 44 6F 52` | 0.0.15a-05311904 - ??? |
| com.mojang.minecraft.phys.AABB | 0 | `00 00 00 00 00 00 00 00` | 0.0.14a_08 - ??? |
| com.mojang.minecraft.player.Player | 9206737118623327547 | `7F C4 E6 A1 47 F2 65 3B` | 0.0.14a_08 - ??? |
| byte[] | -5984413125824719648 | `AC F3 17 F8 06 08 54 E0` | N/A |
| java.util.ArrayList | 8683452581122892189 | `78 81 D2 1D 99 C7 61 9D` | N/A |