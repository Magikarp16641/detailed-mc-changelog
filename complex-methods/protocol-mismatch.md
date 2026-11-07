When a client connects to a server which has an incompatible client-server protocol the server may misinterpret the packets sent by the client, which can theoretically result in things otherwise only possible using a hacked client. In practice most client-server combinations have sufficient protections against this exact thing however.

# 1.2 (classic server) + 0.0.15a-05311904
Classic server 1.2 has no protections against player action packets (`05`) containing blocks not normally placeable by the client (blocks can still only *place* inside block ID `00` or a liquid). In particular grass, unbreakable, water, calmWater, lava, calmLava, goldOre, ironOre and coalOre can only be placed using a hacked client. Additionally the server will always attempt to read 100 packets from a client in a tick, provided that enough data is sent by the client, only stopping if it encounters an invalid packet. The server does *still* attempts to read the remaining packets even if the client was already kicked this tick.

When a 0.0.15a-05311904 connects to a server it sends the following packets:

| Packet ID | Data Types | Length | Contents |
| :---: | --- | :---: | --- |
| `00` | String | 65 | Send as the first packet immediately after joining a server. The string is always "guest". |
| `05` | Short, Short, Short, Byte, Byte | 9 | Sent whenever the client attempts to break or place a block. Contains the block's coordinates, the edit mode (0 for breaking, 1 for placing) and the selected block ID. |
| `08` | Byte, Short, Short, Short, Byte, Byte | 10 | Sent every tick. Contains -1, the client's coordinates in 1/32 fixed point and the client's yRot and xRot in 1/256th of a full rotation. |

If no level has been loaded the coordinates and rotation in the `08` packet are set to 0. Sending any other `08` packet or sending the `05` packet requires the client to generate a new world or load a world.

In classic server 1.2 the length of the `00` packet was increased to 130. Since the `00` packet sent by the 0.0.15a-05311904 is not long enough, the remaining bytes are read from the following packets. The `00` packet sent by the client always "contains" a PVN of 107, which causes the client to be kicked. Provided that the client sent enough data, the server continues to read at most 99 additional packets, but because the length of the `00` packet changed, the packet ID of the 2nd packet isn't necessarily read from what the client intended to be a packet ID. It could be said that the "packet boundaries" desync between the client and the server.

| Packet ID | Length |
| :---: | :---: |
| `00` | 130 |
| `01` | 1 |
| `02` | 1 |
| `03` | 1028 |
| `04` | 7 |
| `05` | 9 |
| `06` | 8 |
| `07` | 74 |
| `08` | 10 |
| `09` | 7 |
| `0A` | 5 |
| `0B` | 4 |
| `0C` | 2 |
| `0D` | 66 |
| `0E` | 65 |

Unless the client loads or generates a world within a few ticks of connecting to the server, the packets that are sent by the client and how they will be interpreted by the server are as follows:

<table><tr><th>0.0.15a-05311904 packet</th><td colspan="4">preLogin packet (<code>00</code>)</td><td colspan="3">6 position packets (<code>08</code>)</td><td colspan="10">position packet (<code>08</code>)</td></tr>
<tr><th>Bytes</th><td><code>00</code></td><td><code>67</code></td><td>... (62 bytes)</td><td><code>20</code></td><td><code>08</code></td><td>... (58 bytes)</td><td><code>00</code></td><td><code>08</code></td><td><code>FF</code></td><td><code>00</code></td><td><code>00</code></td><td><code>00</code></td><td><code>00</code></td><td><code>00</code></td><td><code>00</code></td><td><code>00</code></td><td><code>00</code></td></tr>
<tr><th>Classic server 1.2 packet</th><td colspan="12">preLogin packet (<code>00</code>)</td><td colspan="5">...</td></tr></table>

The packet ID of the 2nd packet is read from the lower byte of the Y position in the `08` packet, which is `00` because the player's position hasn't been initialized due to no world being loaded. Because the length of the `08` packet as sent by the client is a divisor of the length of the packet `00` as read by the server, unless the client eventually loads or generates a world all packets read by the server will be `00` packets.

<table><tr><th>0.0.15a-05311904 packet</th><td colspan="5">...</td><td colspan="3">12 position packets (<code>08</code>)</td><td colspan="10">position packet (<code>08</code>)</td></tr>
<tr><th>Bytes</th><td><code>00</code></td><td><code>00</code></td><td><code>00</code></td><td><code>00</code></td><td><code>00</code></td><td><code>08</code></td><td>... (118 bytes)</td><td><code>00</code></td><td><code>08</code></td><td><code>FF</code></td><td><code>00</code></td><td><code>00</code></td><td><code>00</code></td><td><code>00</code></td><td><code>00</code></td><td><code>00</code></td><td><code>00</code></td><td><code>00</code></td></tr>
<tr><th>Classic server 1.2 packet</th><td colspan="13">preLogin packet (<code>00</code>)</td><td colspan="5">...</td></tr></table>

When the client loads or generates a world their position is initialized, which causes the server to read a packet other than `00`. Assuming that the player spawns on flat ground there are no Y positions which can be achieved without inputs that would result in the packet ID to be valid. A possible way to get a valid packet ID y position from flat ground is by spawning at a Y level that is 6 mod 8 and jumping quickly. After 2 or 9 ticks the lower byte of Y position will be `01`, or after 2 or 9 ticks the lower byte of Y position will be `0B`. The jump has to have tick perfect alighnment in relation to where in the 13 tick cycle that makes up a `00` packet. The `01` packet causes the next packet ID to be read from the higher byte of the Z position and the `0B` packet causes the nexxt packet to be read from the xRot, the latter being easier to control.

<table><tr><th>0.0.15a-05311904 packet</th><td colspan="5">...</td></tr>
<tr><th>Bytes</th><td><code>0B</code></td><td>ZZ</td><td>zz</td><td>yR</td><td>xR</td></tr>
<tr><th>Classic server 1.2 packet</th><td colspan="4">rotation change packet (<code>0B</code>)</td><td>...</td></tr></table>

By default the xRot is `00` which once again creates a 13 tick loop, this time being controlled by an easier to control variable. The player may be moved to a better position during this time. Getting outside this loop can be done by changing the xRot, in particular changing it to `08` swaps the 13 tick loop with a 1 tick loop, removing the need for inputs to be tick perfect in relation to this invisible cycle. When ready the xRot can be changed to a value that eventually results in a `05` packet at the desired offset. Since the server only handles a maxium of 100 packets, using `00` loops gives a time limit of about a minute for putting the client in a desired position, with the time limit decreasing if an `08` loop is used. By using the `03` packet, which doesn't loop, it's possible to increase the time limit to over an hour at the cost of requiring tick perfect inputs.

## Possible player action packets
None of the available packets provide a long enough sequence of manipulable bytes to create an arbitrary player action packet. Below is a summary of what player action packets are theoretically possible based on what byte the packet ID is read from and based on whether the client sends only a stream of `08` packets, or if it sends an `05` packet as well.

<table><tr><th colspan="10">position packet (<code>08</code>)</th><th colspan="10">position packet (<code>08</code>)</th></tr>
<tr><td><code>08</code></td><td><code>FF</code></td><td>XX</td><td>xx</td><td>YY</td><td>yy</td><td>ZZ</td><td>zz</td><td>yR</td><td>xR</td><td><code>08</code></td><td><code>FF</code></td><td>XX</td><td>xx</td><td>YY</td><td>yy</td><td>ZZ</td><td>zz</td><td>yR</td><td>xR</td></tr></table>

| Packet ID byte | Effect |
| :---: | --- |
| `08` | Can't be `05`. |
| `FF` | Can't be `05`. |
| XX | Can only place water (`08`). |
| xx | Can only try to place block ID `FF`, which fails. |
| YY | Can only place blocks at coordinates $`z \equiv 8 \pmod{256}`$. |
| yy | Can only place blocks at coordinates $`z = 2303`$. |
| ZZ | Can only try to place blocks at negative Z coordinates, which fails. |
| zz | Can only place blocks at coordinates $`y = 2303`$. |
| yR | Can only try to place blocks at negative Y coordinates, which fails. |
| xR | Can only place blocks at coordinates $`x = 2303`$. |

<table><tr><th colspan="10">position packet (<code>08</code>)</th><th colspan="9">block placement packet (<code>09</code>)</th><th colspan="10">position packet (<code>08</code>)</th></tr>
<tr><td><code>08</code></td><td><code>FF</code></td><td>XX</td><td>xx</td><td>YY</td><td>yy</td><td>ZZ</td><td>zz</td><td>yR</td><td>xR</td><td><code>05</code></td><td>XX</td><td>xx</td><td>YY</td><td>yy</td><td>ZZ</td><td>zz</td><td>em</td><td>id</td><td><code>08</code></td><td><code>FF</code></td><td>XX</td><td>xx</td><td>YY</td><td>yy</td><td>ZZ</td><td>zz</td><td>yR</td><td>xR</td></tr></table>

| Packet ID byte | Effect |
| :---: | --- |
| `08` | Can't be `05`. |
| `FF` | Can't be `05`. |
| XX | Can only place wood (`05`). |
| xx | Requires the client loading a world with a width of more than 256 times the id of the placed block. |
| YY | Can only place blocks at coordinates $`z \equiv 5 \pmod{256}`$. Requires the client loading a world with a width of more than 256. |
| yy | Can only place blocks at coordinates $`1280 \leq z \leq 1535`$. Requires the client loading a world with a depth of more than 256 times the id of the placed block. |
| ZZ | Can only place blocks at coordinates $`y \equiv 5 \pmod{256}`$. Requires the client loading a world with a depth of more than 256. |
| zz | Can only place blocks at coordinates $`1280 \leq y \leq 1535`$. Requires the client loading a world with a height of more than 256 times the id of the placed block. |
| yR | Can only place blocks at coordinates $`x \equiv 5 \pmod{256}`$. Requires the client loading a world with a height of more than 256. |
| xR | Can only place blocks at coordinates $`1280 \leq x \leq 1535`$. Can only place rock (`01`). |
| `05` | Regular player action packet. |
| XX | Can only place blocks at coordinates $`z \equiv 0 \pmod{256}`$ or $`z \equiv 1 \pmod{256}`$. Can only place water (`08`). Requires the client loading a world with a width of more than 1280. | 
| xx | Can only try to place block ID `FF`, which fails. |
| YY | Can only place blocks at coordinates $`y \equiv 0 \pmod{256}`$ or $`y \equiv 1 \pmod{256}`$ and $`z \in \{264,776,1032,1288,1544,3080,3336,4360,4616\}`$. Requires the client loading a world with a depth of more than 1280. |
| yy | Can only place blocks at coordinates $`y \in \{1,3,4,5,6,12,13,17,18,257,259,260,261,262,268,269,273,274\}`$ and $`z = 2303`$. |
| ZZ | Can only try to place blocks at negative Z coordinates, which fails. |
| zz | Can only place blocks at coordinates $`x \in \{1,3,4,5,6,12,13,17,18,257,259,260,261,262,268,269,273,274\}`$ and $`y = 2303`$. |
| em | Can't be `05`. |
| id | Can only place blocks at coordinates $`x = 2303`$. |