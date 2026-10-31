At some point between 0.0.15a-05311904 and 0.0.16a_02-081047 protocol version numbers (abbreviated PVN) were added, the server refuses connections from clients with the incorrect protocol version. The protocol is otherwise very similar to the [one](/early-multiplayer-test.md) used in the first multiplayer test.

| Protocol version number | Client | Server |
| :---: | --- | --- |
| 3 | 0.0.16a_02-081047 | 1.2 |

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

Receiving a packet with an invalid ID causes and exception and disconnects the player from the server. Position and rotation of entites are not sent as floats, instead coordinates are measured in 32nds of a block and rotation is measured in 256ths of a full rotation.

| ID | Data types | Clientbound | Serverbound |
| :---: | --- | --- | --- |
| `00` | Byte, String, String | Sent after the server receives a packet with a valid PVN from an unbanned player. Contains the PVN, the server name, and the motd. Creates a loading screen with the server name as the title and the motd as the status. | First packet sent when connecting to a server. Contains the PVN, the player's username as well as the string "--". If the protocol version number is incorrect, or the player is banned the server refuses connection, otherwise a gzipped buffer containing the number of blocks and block IDs is prepared for the player by a separate thread. |
| `01` | - | Sent to every player every 0.5 seconds, does nothing | unused |
| `02` | - | Sent before the player receives level data. Initializes a buffer for loading the level. | unused |
| `03` | Short, byte[], Byte | The short indicates the number of bytes from the byte array to copy to the level loading buffer. The byte indicates the level loading percetage used for the loading screen progress bar. | unused |
| `04` | Short, Short, Short | Sent after all the level data. The data in the level loading buffer is unzipped, the first 4 bytes indicate the number of blocks in the world with the rest being block IDs. The level is initialized with these blocks and the 3 shorts as its dimensions. | unused |
| `05` | Short, Short, Short, Byte, Byte | unused | Sent when the player breaks/places a blocks. Contains the block's coordinates, the edit mode, and the selected block ID. Based on the edit mode the block at those coordinates is set to ID `00` or the selected block ID (the latter only if it would replace a liquid or block ID `00`). |
| `06` | Short, Short, Short, Byte | Sent whenever a block changes (with the exception of water/lava turning to calmWater/calmLava and vice versa). Changes the block at the given coordinates to the given block ID. Sends block updates. | unused |
| `07` | Byte, String, Short, Short, Short, Byte, Byte | Contains an id, a username, coordinates, yRot and xRot. If the id isn't negative a new NetworkPlayer entity is created, otherwise the player's position and rotation is changed. Sent to the client when they join the server with an id of -1, to all online players whenever a new player joins the server, and once for every currently online player to the client when they join the server. | unused |
| `08` | Byte, Short, Short, Short, Byte, Byte | Contains an id, coordinates, yRot and xRot. If the id is not negative, the position and rotation of the NetworkPlayer of the given id is updated. Sometimes sent by the server after it receives a `08` packet from another client. | Is sent every tick with the id set to -1 and the player's current position and rotation. Can cause packet `08`,`09`,`0A`, or `0B` to be sent to other clients by the server. |
| `09` | Byte, Byte, Byte, Byte, Byte, Byte | Contains an id, change of position, and yRot and xRot. If the id is not negative, movement of the NetworkPlayer is queued. Sometimes sent by the server after it receives a `08` packet from another client. | unused |
| `0A` | Byte, Byte, Byte, Byte | Contains an id and change of position. If the id is not negative, movement of the NetworkPlayer is queued. Sometimes sent by the server after it receives a `08` packet from another client. | unused |
| `0B` | Byte, Byte, Byte | Contains an id, yRot and xRot. If the is not negative, movement of the NetworkPlayer is queued. Sometimes sent by the server after it receives a `08` packet from another client. | unused |
| `0C` | Byte | Contains an id, if it's not negative the NetworkPlayer with the given id is removed. Sent when a player disconnects. | unused. |
| `0D` | Byte, String | Contains an id and a chat message. The message is added to the chat log. If the id is negative the message is prepended with the formatting code "&e". Sent to every player when a player sends a chat message. Sent to every player with an id of -1 when a player is kicked, banned, or ip banned, or as a result of the "/broadcast" or "/say" commands. Sent to a single player with an id of -1 when a non-admin attempts to use a command, or when an admin attempts to use an unknown command. | Sent with an id of -1 when a player finishes a chat message. If the message starts with "/", it's interpreted as a command, otherwise it's sent to every player alongside the username of the player who said it. |
| `0E` | String | Creates an error screen with the title "Connection lost" and the string as the message. Sent whenever a client attempts to join when they are ip banned, attempts to join a full server, or when they are kicked. | unused |

## Movement packets
These versions have 4 separate movement packets, being packet IDs `08` to `0B`. The client only ever sends packet `08`, but the server may send the others at times.

Server-side, every client has an associated tick count that is incremented whenever the server receives a position packet from the client. If the tick count is even and if the player's position or rotation changed in the last 2 packets, the server will send a movement packet to other players.
- The `08` packet is sent if the player's position changed by more that 4 blocks in any cardinal direction, or if the tick count is at most 1 modulo 20.
  - With constant player movement and a vanilla client this packet is sent once per second.
  - If the tick count overflows this packet is sent every time until the tick count reaches 0 again.
- The `09` packet is sent whenever only the player's rotation changes, unless the `08` packet is sent instead.
- The `0A` packet is sent whenever only the player's position changes, unless the `08` packet is sent instead.
- The `0B` packet is sent whenever both the player's position and rotation changes, unless the `08` packet is sent.

# Interactions with other client protocols
## [0.0.15a-05311904](/early_multiplayer_test.md)
The 0.0.15a-05311904 client sends a `00` packet as soon as it connects, afterwords it starts sending `08` packets every tick, and `05` packet whenever the client attempts to break/place a block (after the client either generates a new world or loads a world). The behavior of the server depends on how many packets the client sent to the server before it handles the `00` packet.

The length of the `00` packet was increased from 65 bytes to 130 bytes between the protocols. If the client does not send enough additional packets to fill the remaining 65 bytes, the server *should* do nothing until it receives those remaining bytes. Due to a bug the length of strings is not counted in this check, as a result the packet is read before the enough bytes are receives, which causes a BufferUnderflowException, kicking the client.

If the server receives more than 130 bytes worth of packets the `00` packet is read with a PVN of 103, which kicks the client due to wrong protocol version. Even though the client is kicked, the server attempts to handle up to 99 additional packets from it this tick. The packet ID of the 2nd packet can, and typically is, read from a byte that is in the middle of a packet as sent by the client, which can result in wild behavior.

If the packet ID is ever an invalid ID, the server stops trying to read additional packets from the client. Most valid packets don't do anything of note, but in classic server 1.2 the `05` packet can be used to place any valid block ID (see [protocol mismatch](../complex-methods/protocol-mismatch.md) for more details).