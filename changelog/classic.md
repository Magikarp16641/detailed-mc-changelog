# 0.0.11a-launcher
## Additions
### World generation
**Caves**
- Added caves
- `width * height * depth / 256 / 64` attempts are made to generate caves. This results in 256 attempts in this version.
- Caves can be anywhere between 0 and 150 blocks long.
- Caves start at 2 blocks wide and increase in width up to 7 blocks.
  - They are half as tall as they are wide.
- Caves carve only through rock and can't carve through blocks that are at edge, top or bottom of the world.

### General
**GUI**
- Added a version number to the top left of the screen that currently reads "0.0.11a".

**Font**
- Added support for text rendering.
- The font is contained in a new `default.gif` file.
- Only codepoints between U+0000 and U+00FF can be rendered. Attempting to render any other character results in a crash.
- Added text formatting, `&` changes the color of the rest of the string based on the character after it.
  - The character `&` can never render because of this.
  - The game crashes if `&` is the last character of a string.

| Formatting code | Base color | Shadow color |
| :---: | :---: | :---: |
| `&0` | `#000000` | `#000000` |
| `&1` | `#0000BF` | `#00002F` |
| `&2` | `#00BF00` | `#002F00` |
| `&3` | `#00BFBF` | `#002F2F` |
| `&4` | `#BF0000` | `#2F0000` |
| `&5` | `#BF00BF` | `#2F002F` |
| `&6` | `#BFBF00` | `#2F2F00` |
| `&7` | `#BFBFBF` | `#2F2F2F` |
| `&8` | `#404040` | `#101010` |
| `&9` | `#4040FF` | `#10103F` |
| `&a` | `#40FF40` | `#103F10` |
| `&b` | `#40FFFF` | `#103F3F` |
| `&c` | `#FF4040` | `#3F1010` |
| `&d` | `#FF40FF` | `#3F103F` |
| `&e` | `#FFFF40` | `#3F3F10` |
| any other code | `#FFFFFF` | `#3F3F3F` |

- The font has the appearance of the Code page 437 character set.
- Characters `00`, `20` and `FF` are spaces with widths 1, 4 and 0 respectively.
- Characters `07`, `09`, `0C`, `12`, `13`, `16`, `18`, `19`, `7B` and `7C` (`•`, `○`, `♀`, `↕`, `‼`, `▬`, `↑`, `↓`, `{` and `¦`) have their width incorrectly set to 1.
- Characters `80` through `FF` have their width incorrectly set to 0.
- Neither the text formatting or any of the incorrect width or crash issues are observable in-game.

**Controls**
- Pressing `Y` now inverts the mouse Y axis.

**Applet support**
- The game can now be run from an applet. Doing so sets the game's resolution to 640x480.

**Multiplayer**
- Added unused multiplayer code.

## Changes
### Blocks
**bush**
- Texture changed.

### General
- Right-clicking now changes between destroying and placing modes.
- Left-clicking now destroys and places blocks based on the current edit mode.
- Solid blocks can no longer be placed inside the player or zombies.
- Pressing `ESC` no longer closes the game and instead ungrabs the mouse.
- The framerate and number of chunk updates now display below the version number instead of being sent to the game log.
- The game's resolution is now 854x480 instead of 1024x768. This is not the correct aspect ratio and as such the actual gameplay has a resolution of 640x480 with a 214 pixel wide light blue section to its right.
- Updated the `terrain.png`.
  - Removed the unused unbreakable, opaque and semi-transparent water, and lava textures.
  - Updated the bush texture.
- Changed fog density.
- The game window now has "Minecraft 0.0.11a" as its title.
- Changed all references of "RubyDung" to "Minecraft" in the code.
- Class files are now compiled with Java 5 instead of Java 6.
- Encountering a GL error now prints an error message into the log.
- Slightly optimized the particle engine and tesselator to not do useless calculations.

## Removals
### General
- Removed the `META-INF` folder and the `MANIFEST.MF`, `MOJANGCS.RSA`, and `MOJANGCS.SF` files.

# 0.0.12a_03-200018
## Additions
### Blocks
**unbreakable**
- Has an ID of `07`.
- Cannot be obtained.
- Despite its name it can be broken.

**water, lava**
- Have IDs of `08` and `0A`.
- They affect the physics of the player.
  - Zombies and particles are not affected.
  - The player can swim in both water and lava. Swimming in lava is slower.
  - Moving and falling is slowed when in water, even slower in lava.
  - If the player is inside water and lava at the same time, they're only affected by the water.
  - The check for whether the player is inside a liquid is imperfect in the positive X, Y and Z directions. This makes it possible to swim up when up against a +X +Z corner if there's liquid behind it.
    - It's also possible to be supported by just a ceiling corner, though getting to the correct Y level requires swimming up first.
- Can't be selected.
- Aren't solid, but do block light.
- Water has a spread speed of 8. Lava has a spread speed of 2.
- When ticked it attempts to spread with a depth of 0.
- The spreading algorithm is the following:
  - Attempts to spread downwards.
    - Replaces an ID `00` below with the liquid.
    - Water spreads until it reaches a different block type.
    - Lava can only spread 1 block downwards, if it does it immediately stops the spreading algorithm.
  - Attempts to spread horizontally from the ticked block or, if the water spread downwards, from the bottommost placed water.
    - If the depth is equal to the spread speed, stop.
    - Replaces horizontally adjacent ID `00`s to the last with the liquid and restarts the spreading algorithm from them with a depth 1 higher.
  - If it couldn't spread at all, it turns into the corresponding calm liquid block.
- When water is updated by lava it turns to rock and when lava is updated by water it turns to rock.
- Their model is shifted 0.1 blocks downwards.
  - This causes z-fighting in certain scenarios.
- They are semi-transparent.
  - Doesn't trigger occlusion culling (unless the adjacent block is of the same liquid type).
  - They aren't back-face culled.
- The top face doesn't render if the block above is solid, resulting in an x-ray like effect.
- When the player is submerged in a liquid a fog effect renders. The fog is dark blue when in water and orange when in lava. The lava fog is denser.
- Can only be obtained via spreading from preexisting calmWater or calmLava, which can't be obtained outside of terrain generation. Cannot be obtained above Y 31.
  - Water will briefly become unobtainable in 0.0.13a-launcher.★
  - Lava above Y 21 will briefly become unobtainable in 0.0.13a-launcher.★

**calmWater, calmLava**
- Have IDs of `09` and `0B`.
- Have the same properties and render the same as their non-calm counterparts.
- Does nothing when ticked.
- When updated, if any of the horizontally adjacent blocks or the block below have ID `00`, it turns into its non-calm counterpart.
  - If it's at the edge or bottom of the world, it will always turns into its non-calm counterpart.
  - calmWater and calmLava can be downgraded to an earlier version to break or place an adjacent block without causing a block update.⬠
    - Doing this in any version other that rd-132211-launcher or rd-132328-launcher is extremely difficult, as rendering the liquid block crashes the game.
    - This can be used to create calmWater or calmLava next to or on top of ID `00`, which is normally impossible.⬟
    - This can be used to create calmWater at the world edge at non-ticking coordinates next to an unnatural block, which is normally not possible at certain coordinates.⬟
      - Unnatural blocks include:
        - Rock above or below the calmWater.
	   - calmWater can never generate atop or below rock at the world edge due to caves not carving through edge blocks.
	 - Grass in rd-160052-launcher or later.
	   - Grass next to or below the calmWater is considerably easier that other newer blocks, as it doesn't require any player interaction if dirt generated naturally in the correct spot.
	   - Grass can't generate adjacent to water due to it always generating above Y 31, the highest water level.
	 - Dirt above the calmWater in rd-160052-launcher or later.
	   - Dirt can't generate above calmWater at the world edge due to caves not carving through edge blocks.
	 - stoneBrick and wood in rd-160052-launcher or later.
	 - Bush in rd-161348-launcher or later.
      - calmWater can never generate on top of or below rock at the world edge due to caves not carving through edge blocks.
      - calmWater at the world edge always turns to water upon receiving a block update, but if it's one of the about 17% of blocks which are never random ticked it can never turn back into calmWater.
- When calmWater is updated by lava, it turns to rock. When calmLava is is updated by water, it turns to rock.
- Can initially only be obtained via terrain generation. Cannot be obtained above Y 31.
  - calmWater will briefly become unobtainable in 0.0.13a-launcher.★
  - calmLava above Y 21 will briefly become unobtainable in 0.0.13a-launcher.★

### Gameplay
**Block updates**
- Placing or breaking a block, a bush decaying, grass dying or spreading, and liquid spreading now triggers a block update for all adjacent blocks.
  - A liquid turning into its calm state and vice versa, and a liquid turning to rock do *not* trigger a block update.
- The only blocks currently affected by block updates are liquids.
  - calmWater and calmLava turn to water and lava respectively when updated if they are bordered at the side or bottom by a block with ID `00` or the world boundary.
  - Water and calmWater turn to rock when updated by lava.
  - Lava and calmLava turn to rock when updated by water.

**World boundary**
- Added a boundary to the bottom and sides of the world, which prevents the player and entities from going outside the world.
  - Respawning within 0.3 blocks of the world boundary causes the player to spawn standing inside it, where they'll stand at Y 73 until they move or respawn again. This has a 0.46820% chance of occuring.
  - Respawning withing 0.3 blocks of the world corner and walking deeper into the boundary makes it possible to get stuck with no way out aside from respawning again. Spawning close enough to the corner has a 0.00054% chance of occuring.
  - The 10 zombies that spawn on world load also have a chance of spawning clipped outside the world.
- Below the world and on its sides up to Y 30 the boundary has the appearance of the new `rock.png` texture tiled every block.
  - Because `rock.png` is identical to the unbreakable block texture, this makes it appear as if the world was encased with unbreakable blocks placed up to Y 29.
- Outside the world there is a plane of the `rock.png` texture at Y 30 up to 640 blocks outside the world.
  - This makes it appear as if there was a plane of unbreakable blocks on Y 29.
- Outside the world there is a plane of the `water.png` texture at Y 31.9 up to 640 blocks outside the world.
  - This is supposed to mimic a layer of water (or calmWater) at Y 30 and 31, but the water is missing its side texture.
- Faces on the outside of the world no longer render.
  - This is noticable on the top faces of blocks at Y 63.
  - As a direct result, the selected block type is no longer shown in the top right corner of the screen as it's being rendered at 0,-2,0. The bush is not affected.
- Zombies can no longer be removed by being below Y -100 in practice.

**Controls**
- Pressing `N` regenerates the world, respawns the player and deletes all zombies.
  - With the addition of the world boundary, this is the only way to be in a world with less than 10 zombies.
- Pressing `F` cycles through render distances.
  - By default the entire world renders.
  - Other render distances include 128 blocks, 64 blocks and 32 blocks.
  - A chunk renders if the euclidian distance from its center to the player is less than the render distance.
  - Only blocks are affected by render distance. The world boundary, zombies, and particles render at any distance.

### General
**Loading screen**
- When loading or generating a level a dirt background (using the new `dirt.png` texture) is shown with 2 lines of text.
- When loading an existing level the lines read "Loading level" and "Reading.."
- When generating a new level the top line reads "Generating level" with the bottom cycling through "Raising..", "Carving..", "Watering.." and "Melting.." as the level is being generated.

**Miscellaneous**
- Added the "IT HAPPENED!" and "hoooly fuck" error messages into the `floodFillLiquids` method. They can never appear in normal gameplay.
- Readded the `META-INF` folder, which includes a `MANIFEST.MF` file.
- Added an unused `grass.png` texture.
- Added an unused `null` file.

## Changes
### Blocks
**grass**
- Now only has a 25% chance to spread or decay when ticked.

### World generation
- Majorly changed terrain generation.
  - Grass can no longer generate below Y 32.
    - This can result in patches of dirt generating.
  - The terrain now resembles as island. Terrain tends to be lower closer to the world edge.
  - Ground level is lower on average.
  - It's less varied when below Y 31.
  - calmWater now floods the world from the edges during terrain generation.
  - calmLava now generates inside lava pools.
    - 400 attempts are made to find ID `00` in the bottom half of the world, from which calmLava is flooded.
    - If calmWater floods a cave that tilts up, it is possible for calmLava to generate on top of calmWater. Which is not normally possible.★
      - If either of the liquids is given space to spread it can turn into the non-calm state, allowing for any combination of lava or calmLava on top of water or calmWater.
      - This block combination can currently be only be destroyed by the water (or calmWater) being turned to rock from the side or bottom, the lava (or calmLava) being turned to rock from the side or top, or from the player placing a block inside one of the liquids.
- When the terrain is generated 2 strings are sent into the game log.
  - "LavaCount: " + number of succesful lava attempts
  - "Flood filled " + total number of calmWater and calmLava tiles placed + " tiles in " + time it took to flood fill *just calmWater* in milliseconds + " ms"
- Noise maps now use the same random instance as the rest of the level generator.

### Gameplay
**Movement physics**
- Changed the movement physics of the player. Zombies retain their old physics.
- Increased friction, reducing walking speed from 5.50964 m/s to 4.40529 m/s.
  - Jump walking is now slightly faster than walking at 4.43141 m/s.
- Changed the order of gravity and drag, which resulted in the jump height increasing from 1.23350 blocks to 1.68546 blocks.

**Random ticks**
- Doubled the number of random ticks in a game tick to 20,971.52
  - A given block ticks on average every 10 seconds.
- The coordinates of a randomly selected block are now determined by a single random number instead of 3.
- Blocks are not picked uniformly, instead each block has one of 10 possible probabilities to be picked.
  - Most notably about 17% of blocks are never random ticked.
    - That means that in those positions bushes never decay, grass never spreads from or dies, and liquids never spread from or turn into calm liquid.
    - calmWater and calmLava are only obtainable in these positions if they naturally generated there.

| Probability out of 2<sup>32</sup> | Average time between ticks | # of blocks |
| ---: | --- | :---: |
| 0 | N/A | 715264 |
| 256 | 40 s | 448512 |
| 512 | 20 s | 398592 |
| 768 | 13.33333 s | 395264 |
| 1024 | 10 s | 354816 |
| 1280 | 8 s | 383232 |
| 1536 | 6.66667 s | 373504 |
| 1792 | 5.71429 s | 432128 |
| 2048 | 5 s | 492544 |
| 2304 | 4.44444 s | 200448 |

### General
- The version number in the top left of the screen now reads "0.0.12a_03".
- Changed the game window title to "Minecraft 0.0.12a_03".
- Light depths now track the Y level of the last transparent block instead of the first light blocker.
  - The only noticable difference this makes is making zombies appear darker when clipped inside a block.
    - In this version, zombies can get inside a block by standing inside a liquid when it turns to rock.
    - Zombies couldn't get inside blocks in 0.0.11a-launcher, but in rd-161348-launcher and before a block could simply be placed where they're standing.
- Halved the maximum number of chunks that can be rebuilt per frame to 4.
- When a chunk was last dirtied no longer affects rebuild order. The order is now based only on whether the chunk is within the player's field of view and the chunk's distance to the player.
- Chunk updates no longer contribute towards the number of chunk updates twice.
- Changed fog color from white to light blue.
- Optimized block selection code. Faces are only checked when they wouldn't be back-face culled.
- The code is now obfuscated.
- Updated the `terrain.png` to textures for unbreakable, water and lava.
  - Added an opaque water texture.

## Removals
### General
- The game can no longer be run outside an applet. As such the game's resolution is now always 640x480.
- `resourceName` + " -> " + `id` no longer gets sent to the game log when a new texture is laoded.
- Removed unused server code.
- Removed the unused stoneBrick, wood and bush constants from the code, the blocks themselves aren't removed.
- Removed the unused empty block constant.

# 0.0.13a-launcher
## Additions
### Gameplay
**Pause screen**
- Pressing `ESC` or tabbing out now opens a pause screen instead of just releasing the mouse.
- The pause screen includes 4 buttons:
  - "Generate new level"
    - Generates a new level with the dimensions of 32x64x512 and removes all zombies.
      - The world is small enough to be safely downgraded to prior versions without losing data, making it possible to create calmLava next to or on top of ID `00` by downgrading to before 0.0.12a_03-200018.⬟
        - In rd-160052-launcher and later the game will crash not only when rendering the lava, but also when rendering what used to be the header.
  - "Save level.."
    - Does nothing.
  - "Load level.."
    - Does nothing.
  - "Back to game"
    - Closes the pause screen.
- The text color does not correspond to any formatting code.
  - The color is `#E0E0E0` with its shadow being `#383838`.
  - When the button is hovered over the color changes to `#FFFFA0` with its shadow being `#3F3F28`.

### General
- The game can once again be ran outside an applet. It has a resolution of 864x480.
- Added game arguments. Launching the game with the `-fullscreen` argument opens the game in fullscreen mode.
- Added a thin black block selection outline.
- Added uncompiled `_LevelGen.java_` and `_NoiseMap.java_` files.
  - Include a slightly modified version of last version's terrain generator without water and lava generation.
  - `_LevelGen.java_` includes commented out lines of code which would make water (not calmWater) generate at the edge of the world without flooding.
- Added an unused improved Perlin noise implementation.
- Readded unused server code.
- Readded the unused empty, stoneBrick, wood and bush constants to the code.

## Changes
### Blocks
**bush**
- Texture changed.
- The orientation of the rendered textures is now opposite of what it used to be.

**water, calmWater**
- Water now turns to rock when updated by calmLava.
  - This never happens as calmLava never sends out block updates.
- Made the water collision check stricter. The player is no longer considered as in water if only the bottom or top 0.4 blocks of the hitbox collide with water.
  - Being supported by water through a positive ceiling corner due to collision check imperfection is no longer possible.
- The player now does a 0.69085 block jump when coming ashore.
  - With the new water collision check changes, it would otherwise be impossible to get ashore from water.
- Water, calmWater and the water texture past the world border no longer render behing the block placing preview.
- The underwater fog now renders based on 0.12 blocks above the player's eye level.
- The underwater fog is bluer than before.

**lava, calmLava**
- Lava now turns to rock when updated by calmWater.
  - This never happens as calmWater never sends out block updates.
- The player now does a 0.69085 block jump when coming ashore.
- Lava is no longer semi-transparent.
- Slightly changed texture.
- The underlava fog now renders based on 0.12 blocks above the player's eye level.
- The underlava fog is now denser and red instead of orange.

### World generation
- Greatly simplified terrain generation.
- Added an "Eroding.." step between "Raising.." and "Carving.."
- The terrain now consists of 22 layers of rock, 10 layers of dirt and 1 layer of grass.
- Caves still generate.
  - 64 caves generate in the new world size.
- Due to Y 31 always generating filled with dirt, no calmWater can get flooded from the edges.
- Added water pools. `width * height / 5000` attempts are made to find an ID `00` at Y 31 to flood fill calmWater from.
  - The number of attempts is 13 for the default world size and 3 for the new thin world size.
  - Water pools can never generate for the same reason as above.
- The "Flood filled " + count + " tiles in " + time + " ms" message is now shown first and only calmWater is counted towards the number of tiles.
- The number of attempts to generate lava pools is now dependand on world dimensions and is equal to `width * height * depth / 10000`. This results in a slight increase for the default world size from 400 to 419. The number of attempts on the new thin world size is 104.
- calmLava generating on top of calmWater now turns the water into rock.☆
- Because Y 31 always generates filled with dirt, calmWater can't generate. Discontinuing water and calmWater.☆
- Because all layers between Y 22 and Y 31 always generates filled with dirt, calmLava can't generate above Y 21. Discontinueding lava and calmLava above Y 21.☆

### Gameplay
**Random ticks**
- The number and distribution of random ticks depends on the world size.
  - The number of random ticks per game tick is still `width * height * depth / 200`
  - Unless all dimensions are a power of 2, large sections of the world never get random ticked.
    - If all dimensions are 1 more than a power of 2 only 8 blocks ever get random ticked (less if one ore more of the dimensions is exactly 1).
- The newly possible 32x64x512 world has 5,242.88 random ticks per game tick and notably does not have any blocks that never tick.

| Probability out of 2<sup>32</sup> | Average time between ticks | # of blocks |
| ---: | --- | :---: |
| 3328 | 12.30769 s | 4608 |
| 3456 | 11.85185 s | 24576 |
| 3584 | 11.42857 s | 58368 |
| 3712 | 11.03448 s | 82944 |
| 3840 | 10.66667 s | 103936 |
| 3968 | 10.32258 s | 157696 |
| 4096 | 10 s | 178688 |
| 4224 | 9.69697 s | 131072 |
| 4352 | 9.41176 s | 125952 |
| 4480 | 9.14286 s | 117760 |
| 4608 | 8.88889 s | 54272 |
| 4736 | 8.64865 s | 7168 |
| 4864 | 8.42105 s | 1536 |

**Controls**
- Modified the player's movement physics.
  - Reverted jump height from 1.68546 blocks to 1.23350 blocks.
  - Increased swimming and sinking speed in water from 1.33333 m/s to 2.00000 m/s.
  - Decresed the speed of swimming up in water from 2.66667 m/s to 2.00000 m/s.
- Holding down the `SPACE`, `LMETA` or `LWIN` now makes the player jump only once.
- Holding down `R` now makes the player respawn only once.
- Reduced player reach from 3 blocks to 2.5 blocks.

### General
**World boundary**
- The player and zombies can no longer spawn within a block of the world boundary to prevent spawning inside it.
  - If either the height or depth of the world is 1, it's possible to spawn anywhere between 0 and 1, which results in a 60% chance to spawn clipped inside the world border (84% if both dimensions are 1).
    - If both dimensions are 1 there is a 36% chance of spawning clipped inside the corner of the world.
  - If either the height or depth of the world is 0, it's possible to spawn anywhere between -1 and 1, which results in a 30% chance to spawn clipped 2 blocks inside the world border (51% if both dimensions are 0).
    - If both dimensions are 0 there is a 9% chance of spawning clipped inside a corner 2 blocks inside the world border.
- How far the `rock.png` and `water.png` textures stretch past the world border now depends on the height and width of the world. They render for 640 blocks, 5 times the height or 5 times the width of the world, whichever is smallest.
  - The textures are rendered in chunks with a width of 128 blocks, the world's height, or the world's width.
  - If the chunk width does not divide one of the world dimensions, texture misalighnments occur in the corresponding positive direction.
    - The floor at the bottom of the world extends past the world edge.
    - The water and ground levels start further from the world.
    - The textures extend further from the world than in the negative direction.
- Faces on the outside of the world once again render.
  - Does not apply to liquids.
  - This fixes the bug that made selected block types not render in the top right of the screen.

**Save format**
- Changed the [save format](../save-formats/early-classic.md).
  - Worlds from previous versions are automatically converted upon loading.
    - Specifically worlds are assumed to use the [older save format](../save-formats/block-byte-array.md) if either the magic number is incorrect or the version number is greater than 1.
- World name and creator name are now saved. They are encoded using MUTF-8.
  - Newly generated world have the world name set to "A Nice World" and the creator set to "noname".
  - Worlds converted from previous versions have the world name set to "--" and the creator set to "unknown".⬠⬟
  - Attempting to load a string with invalid UTF-8 or a 4 byte character will crash the game.
  - Loading a string with an overlong encoding will convert it to its regular encoding.
  - Loading a string containing `00` will convert it to `C0 80`.
- The create time of the world is now saved.
  - Worlds converted from previous versions have the create time set to 1970-01-01 00:00:00.000.
- Added support for different world sizes.
  - Worlds generated when no level.dat is found have their world size set to 256x64x256 (width, depth, height).
  - Worlds generated by the "Generate new level" button have their world size set to 32x64x512.
  - Worlds converted from previous versions have their world size set to 256x64x256.
  - Attempting to load a world with a negative world dimension crashes the game.
- The level.dat of a 256x64x256 world is now too long to be able to be safely downgraded and updated back. Making creating invalid liquid block configurations via downgrading no longer possible in those worlds.⬠
- Downgrading worlds with this save format into earlier versions makes the header be interpreted as block IDs, which can subsequently be modified. This gives rise to many possibilities and is known as [header editing](../complex-methods/header-editing.md).⬠⬟

**Miscellaneous**
- The version number in the top left of the screen now reads "0.0.13a".
- Changed the game window title to "Minecraft 0.0.13a".
- Increased the maximum render distance from 1000 blocks to 1024 blocks.
- Changed the lighting of the selected block type shown in the top right corner.
- Running the game in an applet no longer forces the game to have a resoltion of 640x480. It will instead have resolution equal to the dimensions of the applet.
- The code is no longer obfuscated.

## Removals
### Gameplay
- Pressing `N` no longer generates a new world.

### General
- Removed the `META-INF` folder and the `MANIFEST.MF` file.
- Removed the unused `null` file.