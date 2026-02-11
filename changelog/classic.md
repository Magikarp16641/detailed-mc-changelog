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

<style>table,th,td{border:1px solid black;border-collapse:collapse;text-align:center;padding-left:4px;padding-right:4px;}</style>
<table>
  <tr>
    <th>Formatting code</th>
    <th>Base color</th>
    <th>Shadow color</th>
  </tr>
  <tr>
    <td><code>&0</code></td>
    <td style="background-color:#000000;color:white">#000000</td>
    <td style="background-color:#000000;color:white">#000000</td>
  </tr>
  <tr>
    <td><code>&1</code></td>
    <td style="background-color:#0000BF">#0000BF</td>
    <td style="background-color:#00002F;color:white">#00002F</td>
  </tr>
  <tr>
    <td><code>&2</code></td>
    <td style="background-color:#00BF00">#00BF00</td>
    <td style="background-color:#002F00;color:white">#002F00</td>
  </tr>
  <tr>
    <td><code>&3</code></td>
    <td style="background-color:#00BFBF">#00BFBF</td>
    <td style="background-color:#002F2F;color:white">#002F2F</td>
  </tr>
  <tr>
    <td><code>&4</code></td>
    <td style="background-color:#BF0000">#BF0000</td>
    <td style="background-color:#2F0000;color:white">#2F0000</td>
  </tr>
  <tr>
    <td><code>&5</code></td>
    <td style="background-color:#BF00BF">#BF00BF</td>
    <td style="background-color:#2F002F;color:white">#2F002F</td>
  </tr>
  <tr>
    <td><code>&6</code></td>
    <td style="background-color:#BFBF00">#BFBF00</td>
    <td style="background-color:#2F2F00;color:white">#2F2F00</td>
  </tr>
  <tr>
    <td><code>&7</code></td>
    <td style="background-color:#BFBFBF">#BFBFBF</td>
    <td style="background-color:#2F2F2F;color:white">#2F2F2F</td>
  </tr>
  <tr>
    <td><code>&8</code></td>
    <td style="background-color:#404040;color:white">#404040</td>
    <td style="background-color:#101010;color:white">#101010</td>
  </tr>
  <tr>
    <td><code>&9</code></td>
    <td style="background-color:#4040FF">#4040FF</td>
    <td style="background-color:#10103F;color:white">#10103F</td>
  </tr>
  <tr>
    <td><code>&a</code></td>
    <td style="background-color:#40FF40">#40FF40</td>
    <td style="background-color:#103F10;color:white">#103F10</td>
  </tr>
  <tr>
    <td><code>&b</code></td>
    <td style="background-color:#40FFFF">#40FFFF</td>
    <td style="background-color:#103F3F;color:white">#103F3F</td>
  </tr>
  <tr>
    <td><code>&c</code></td>
    <td style="background-color:#FF4040">#FF4040</td>
    <td style="background-color:#3F1010;color:white">#3F1010</td>
  </tr>
  <tr>
    <td><code>&d</code></td>
    <td style="background-color:#FF40FF">#FF40FF</td>
    <td style="background-color:#3F103F;color:white">#3F103F</td>
  </tr>
  <tr>
    <td><code>&e</code></td>
    <td style="background-color:#FFFF40">#FFFF40</td>
    <td style="background-color:#3F3F10;color:white">#3F3F10</td>
  </tr>
  <tr>
    <td>any other code</td>
    <td style="background-color:#FFFFFF">#FFFFFF</td>
    <td style="background-color:#3F3F3F;color:white">#3F3F3F</td>
  </tr>
</table>

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
- When water is updated by lava it turns to rock. When lava is updated by water it turns to rock.
- Their model is shifted 0.1 blocks downwards.
  - This causes z-fighting in certain scenarios.
- They are semi-transparent.
  - Doesn't trigger occlusion culling (unless the adjacent block is of the same liquid type).
  - They aren't back-face culled.
- The top face doesn't render if the block above is solid, resulting in an x-ray like effect.
- When the player is submerged in a liquid a fog effect renders. The fog is dark blue when in water and orange when in lava. The lava fog is denser.
- Can only be obtained via spreading from preexisting calmWater or calmLava, which can't be obtained outside of terrain generation. Cannot be obtained above Y 31.

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
  - As a direct result, the selected block is no longer shown in the top right corner of the screen as it's being rendered at 0,-2,0. The bush is not affected.
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
- Readded the `META-INF` fodler, which includes a `MANIFEST.MF` file.
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

<table>
  <tr>
    <th>Probability out of 2^32</th>
    <th>Average time between ticks</th>
    <th>Number of blocks</th>
  </tr>
  <tr>
    <td>0</td>
    <td>N/A</td>
    <td>715264</td>
  </tr>
  <tr>
    <td>256</td>
    <td>40 s</td>
    <td>448512</td>
  </tr>
  <tr>
    <td>512</td>
    <td>20 s</td>
    <td>398592<td>
  </tr>
  <tr>
    <td>768</td>
    <td>13.33333 s</td>
    <td>395264</td>
  </tr>
  <tr>
    <td>1024</td>
    <td>10 s</td>
    <td>354816</td>
  </tr>
  <tr>
    <td>1280</td>
    <td>8 s</td>
    <td>383232</td>
  </tr>
  <tr>
    <td>1536</td>
    <td>6.66667 s</td>
    <td>373504</td>
  </tr>
  <tr>
    <td>1792</td>
    <td>5.71429 s</td>
    <td>432128</td>
  </tr>
  <tr>
    <td>2048</td>
    <td>5 s</td>
    <td>492544</td>
  </tr>
  <tr>
    <td>2304</td>
    <td>4.44444 s</td>
    <td>200448</td>
  </tr>
</table>

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
### Blocks
- Removed the unused stoneBrick, wood and bush constants from the code, the blocks themselves aren't removed.
- Removed the unused empty block constant.

### General
- The game can no longer be run outside an applet. As such the game's resolution is now always 640x480.
- `resourceName` + " -> " + `id` no longer gets sent to the game log when a new texture is laoded.
- Removed unused server code.