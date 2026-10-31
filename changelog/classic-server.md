# 1.2
This server version is based on 0.0.16a_02. It uses the [classic server protocol](../server-protocols/classic.md).

## Additions
### General
**Server properties**
- A `server.properties` file is generated when the jar is run.
- The file contains a comment that says "Minecraft server properties" as well as the current date and time.
- The file contains several properties which can be changed to configure the server.

| Property | Default value | Notes |
| --- | --- | --- |
| `server-name` | Minecraft Server | gets shown to players when they join |
| `motd` | Welcome to my Minecraft Server! | gets shown to players when they join |
| `port` | 25565 | |
| `max-players` | 16 | Maximum number of players that can be on the server at once. Gets clamped between 1 and 32. |
| `public` | true | |

**Admins**
- An empty `admins.txt` file is generated when the jar is run.
- Usernames added to the file become admins, which have the ability to use commands.
- Any chat message starting with "/" is considered a command.
- A non-admin player attempting to use a command will be told "You're not a server admin!" in the chat.
- Attempting to use a non-existant command will be told "Unknown command!" in the chat.
- Commands are followed by arguments separated by spaces. Adding more arguments than necessary has no effect. Adding fewer results in the user being kicked due to an exception.
- All commands that take a player's username as an argument are case insensitive.
  - If multiple player have the same username if case is ignored, all are going to be affected.

| Command | # of arguments | Description |
| --- | :---: | --- |
| /ban | 1 | Kicks the player with the specified username with the message "You were banned" and adds their username to `banned.txt`. Other players will see username + " got banned!" in the chat. |
| /kick | 1 | Kicks the player with the specified username with the message "You were kicked". Other players will se username + " got kicked from the server" in the chat. |
| /banip | 1 | Kicks the player with the specified username with the message "You were banned" and adds their ip to `banned-ip.txt`. Other players will see username + " got banned!" in the chat. |
| /unban | 1 | Removes the specified username from `banned.txt`. |
| /op | 1 | Adds the specified username to `admins.txt` and sends the player the message "You're now op!" |
| /deop | 1 | Removes the specified username from `admins.txt` and sends the player the message "You're no longer op!" |
| /broadcast | N/A | Sends the entire message sans "/broadcast " to the chat of every player as a system message. |
| /say | N/A | Sends the entire message sans "/say " to the chat of every player as a system message. |

**Heartbeat**
- Is sent to http://www.minecraft.net/heartbeat.jsp every 600 ticks.
- Contains the string `name=` + server name + `&users=` + number of online players + `&max=` + max player slots + `&public=` + public boolean + `&port=` + server port.

## Changes
### Gameplay
- All newly created worlds have the dimensions of 256x64x256 and "--" as the creator.
  - This discontinues 128x64x128 and 512x64x512 worlds as well as worlds with creator other that "--".☆
- Worlds are no longer saved online. Instead worlds are saved in a "server_level.dat" file.
  - The world is saved immeditely after loading, 1 tick after it is loaded, and subsequently every 1200 ticks.
- There are currently no protections against hacked packets. If a hacked client is used it's possible to place any valid block ID.★
  - This can be used to obtain unbreakable; water, calmWater, lava, calmLava, goldOre, ironOre or coal ore in an unnatural position; grass somewhere below goldOre, ironOre, coalOre, or floating sand or gravel, or below Y 5 at least 3 blocks below a ring of goldOre, ironOre, coalOre, or floating sand or gravel; a pocket of water below Y 29 surrounded on the sides and top by goldOre, ironOre, coalOre, or block ID `00` below sand or gravel; or a configuration of grass, goldOre, ironOre, coalOre, or floating sand or gravel that doesn't naturally generate on any world seed.★
    - Floating sand or gravel cannot be created using this method, instead existing floating sand or gravel blocks (created for example by natural generation) have to be used.
  - This cannot be used to place block ID `00` at the world edge between the ground and water levels.
  - The hacked client can be substituted for a vanilla client using [protocol mismatch](../complex-methods/protocol-mismatch.md).★
- Due to various server changes, more extreme world sizes can be loaded without issue.
  - Worlds can be loaded as long as they meet the following criteria (this assumes the length of the blocks array being the theoretical maximum of 2147483645, shorter arrays constrict world sizes more):
    - $`width * height`$ is between 0 and 2147483645 when cast to an int.
    - at least one of the following is true:
      - $`width`$ or $`height`$ is at most 0.
      - $`width * height`$ is at most 2147483645 and $`depth`$ is at most 1.
      - $`width * height * depth`$ is at most 2147483645.
      - $`width * height`$ is at most 2147483645 and $`width * height * depth`$ and $`width * height * (depth - 1)`$ are both between 0 and 2147483645 when cast to an int.
        - This also assumes that blocks on the "topmost" layer of the world are all solid. If any of them isn't the requirements become more constrained.
    - Unless $`width`$ or $`height`$ are both at least 2, worlds can be loaded only if the spawn point isn't set to 0,0,0
  - Additionally extreme world sizes may experience issues due to random ticks, though technically this does not prevent the world from being loaded, since the world is first saved before any in-game ticks occur.
    - If either $`width`$ or $`height`$ are at least 1073741825, the game gets stuck in an infinite loop.
    - If $`width * height * depth`$ is more than the length of the blocks array, or if $`width`$, $`height`$, or $`depth`$ are less than 1, the world may crash from random ticks unless the product is at most 0 when cast to an int.
      - Some such combinations of world dimensions don't crash, though the exact set depends on the length of the blocks array.

### General
- The game no longer runs as an applet.
- Class files are now compiled using Java 6 instead of Java 5.

**Logging**
- Added proper logging
- Entries consists of a 3 character string indicating its level, the time, and the message itself separated by "  ".
  - Severe entries begin with "***".
  - Warning entries begin with "  !".
  - All other entries begin with "   ".

| Level | Message |
| :---: | --- |
| FINE | "Reading.." |
| FINE | "Raising.." |
| FINE | "Eroding.." |
| FINE | "Soiling.." |
| FINE | "Carving.." |
| FINE | "Watering.." |
| FINE | "Melting.." |
| FINE | "Growing.." |
| FINE | "Planting.." |
| INFO | "Setting up" |
| INFO | "Loading level" |
| INFO | "Generating level" |
| INFO | "Now accepting input on " + port |
| INFO | "Saving level" |
| INFO | "Load: " + player count + "/" + max players |
| INFO | "Sending heartbeat" |
| INFO | ip + " tried to connect, but is banned" |
| INFO | ip + " tried to connect, but failed because the server was full." |
| INFO | player + " connected" |
| INFO | ip + " logged in as " + username |
| INFO | player + " says: " + message |
| INFO | "Kicking " + player + ": " + message |
| INFO | player + " lost connection suddenly. (" + exception ")" |
| INFO | player + " disconnected" |
| WARNING | 'Failed to load player list "' + name + '". (' + exception + ')' |
| WARNING | 'Failed to save player list "' + name + '". (' + exception + ')' |
| WARNING | "Failed to load server.properties" |
| WARNING | "server.properties is broken! Delete it or fix it!" |
| WARNING | "Failed to save server.properties" |
| WARNING | "Failed to load level. Generating a new level" |
| WARNING | "Failed to send heartbeat: " + exception |
| WARNING | player + ":" + exception |
| WARNING | "Exception handling " + player " + "!" |
| SEVERE | "Failed to start server!" |
| SEVERE | "Failed to save level! " + exception |
| SEVERE | "Failed to assemble heartbeat: " + exception |
| SEVERE | "Error in main loop, server shutting down!" |

## Removals
- Removed the NetworkPlayer, Particle, Player and Zombie entities.
- Removed rendering code.
- Removed all textures.
- Removed online level saving.
- Removed player controls.
- Removed code for converting worlds from the [pre-classic save format](../save-formats/block-byte-array.md)
  - Attempting to load such a world, will result in a new world being generated instead.
- Removed the `MOJANG_C.DSA` and `MOJANG_C.SF` files.
- Removed all the signatures from the `MANIFEST.MF` file.