In 0.0.15a-05311904 support for multiplayer was added. Clients and the server communicate with each other using packets, which consist of a single byte packet ID and the payload. Each packet type has an associated list of data types of which determines the length of the payload and the manner in how the byte stream is interpreted.

The first protocol in unique in that it lacks a protocol version. 0.0.15a-05311904 is the only archived client version with this protocol. No server version for this protocol was ever publically released, at the time it was only possible to play multiplayer by joining the server hosted by Notch.

# Data types

| Data type | Length | Notes |
| :---: | :---: | --- |
| Byte | 1 | |
| Short | 2 | |
| Integer | 4 | unused |
| Long | 8 | unused |
| Float | 4 | unused |
| Double | 8 | unused |
| String | 64 | encoded in UTF-8 and truncated or padded with 0x20 to 64 bytes. If a multi-byte character is partially cut off, it will be replaced with � when decoded. The string is trimmed when read. |
| byte[] | 1024 | truncated or padded with 0 to 1024 bytes. |

# Packets

Receiving a packet with an ID above `08` causes and exception and disconnects the player from the server. Position and rotation of entites are not sent as floats, instead coordinates are shorts measuring 32nds of a block and rotation is a byte measuring 256ths of a full rotation.

| ID | Data types | Clientbound | Serverbound |
| :---: | --- | --- | --- |
| `00` | String | Creates a loading screen with the title "Connecting to the server.." and prints the string to the log. | First packet sent when connecting to the server. Should contain the player's username, but instead always contains the string "guest". |
| `01` | - | does nothing | unused |
| `02` | - | Sets the status on the loading screen to "Loading level.." and initializes a buffer for loading the level. | unused |
| `03` | Short, byte[], Byte | The short indicates the number of bytes from the byte array to copy to the level loading buffer. The byte indicates the level loading percetage used for the loading screen progress bar. | unused |
| `04` | Short, Short, Short | The data in the level loading buffer is unzipped, the first 4 bytes indicate the number of blocks in the world with the rest being block IDs. The level is initialized with these blocks and the 3 shorts as its dimensions. | unused |
| `05` | Short, Short, Short, Byte, Byte | unused | Sent when the player breaks/places a blocks. Contains the block's coordinates, the edit mode, and the selected block ID. |
| `06` | Short, Short, Short, Byte | Changes the block at the given coordinates to the given block ID. Sends block updates. | unused |
| `07` | Byte, String, Short, Short, Short, Byte, Byte | Contains an id, a username, coordinates, yRot and xRot. If the id isn't negative a new NetworkPlayer entity is created (the xRot and yRot are erroneously swapped), otherwise the player's position and rotation is changed. | unused |
| `08` | Byte, Short, Short, Short, Byte, Byte | Contains an id, coordinates, yRot and xRot. If the id is negative does nothing, otherwise the position and rotation of the NetworkPlayer of the given id is updated. | Is sent every tick with the id set to -1 and the player's current position and rotation. |
| `09` | Byte | Contains an id, if it's not negative the NetworkPlayer with the given id is removed. | unused. |