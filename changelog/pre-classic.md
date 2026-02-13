# rd-132211-launcher
## Additions
### Blocks
**rock and grass**
- Both blocks share the ID `01` with the type being determined by the Y level. All blocks on Y 42 are grass, all other blocks are rock instead.

**"air"**
- Any ID other than `01` signifies the absence of a block, though only ID `00` is obtainable through regular gameplay in this version.
- Downgrading calmWater or calmLava from 0.0.12a_03-200018 into this version can be used to create invalid block configurations as breaking or placing blocks nearby does not cause block updates. The invalid configurations include:
  - calmWater or calmLava next to or above ID `00`.⬟
  - calmWater at the world edge at non-ticking coordinates above or below rock.⬟

### World generation
- The world is finite and its dimensions are 256x64x256.
- World generation consists of 42 layers of `rock` and 1 layer of `grass`.
- When loading a world, if the level.dat is too short the missing blocks are filled with natural generation.

### Gameplay
- Left-clicking places blocks. Right-clicking destroys blocks (sets the ID to `00`).
  - The player's reach is 3 blocks. This is not measured by Euclidian distance, instead the player can reach any block whose perpendicular distance to the player's hitbox is less than 3.
- Horizontal movement is controlled by both `W`, `A`, `S`, `D` and the arrow keys.
- Jumping is controlled by `SPACE`, `LMETA` and `LWIN`.
- The movement physics run at a rate of 60 ticks per second.
  - A maximum of 60 ticks can happen in a frame.
- When loading into the world or after pressing `R` the player is spawned at Y 74 at a random point above the world.
  - Pressing `R` does not reset the player's velocity, making it possible to build up falling speed up to the terminal velocity by continually pressing `R`.
  - For 1 tick, the player's eye level is 0.9 blocks above the feet instead of 1.62 blocks, which means the player is effectively spawned at Y 74.72 instead.
    - This mismatch also results in the camera rising by 0.715 blocks after the first tick, though is barely noticable.
- Pressing `RETURN` saves the world.
  - The world is saved in a single file called "[level.dat](../save-formats/block-byte-array.md)".
    - Loading worlds with this save format in 0.0.13a-launcher or later will result in discontinued world name and creator values.⬟
    - Downgrading worlds from 0.0.13a-launcher or later will cause the extra data stored by the newer save format to be interpreted as block IDs. Editing them by placing and breaking blocks gives rise to many possibilities and is known as [header editing](../complex-methods/header-editing.md).⬟
- Pressing `ESC` closes the game.
  - Closing the game automatically saves the world.

### General
- The game is windowed with a resolution of 1024x768
- Block textures are stored in a single image called `terrain.png`, which consists of 16x16 cells for 16x16 pixel textures. 2 are used for the rock and grass textures, while the rest contain a pink placeholder texture.
- Once a second, the fps and number of chunk updates get sent to the game log.
  - Every chunk update is counted twice.

### Issues
- The way `HitResult` is calculated is inefficient and may cause immense lag depending on the graphics drivers.
  - This is caused by the `GL11.glDrawArrays` method being called 6 times for every block within the player's reach.
- When the player is spawned (or respawned) the player's old position, which is used for camera interpolation, isn't properly set. This results in the camera quickly moving from the old position to the new for a tick instead of it being instant.
  - In the case of first loading into the world, the camera moves from 0,0,0 to the spawn position
  - This is barely noticable due to the high tps.
- Due to how the timer is implemented, the game crashes when `System.nanoTime()` overflows after 2^63 nanoseconds (roughly 292 years).

# rd-132328-launcher
## Additions
### Mobs
**Zombie**
- 100 are randomly spawned at Y 74 on world load.
  - They're effectively spawned at Y 74.72 for the same reason as the player.
  - Their initial position is set to 128,0,128 before their spawn position is determined, which results in a graphical bug.
    - Before the first tick, their position is interpolated between 0,0,0 and 128,0,128.
    - Before the second tick, their position is interpolated between 128,0,128 and their random spawn position.
    - This is barely noticable due to the hight tps.
- Moves around randomly with the same physics as the player.
  - Has a 1% chance of jumping every frame.
- Zombies above Y 100 respawn.
  - This can't happen in practice.
- They aren't saved in the `level.dat`.
- Their texture is stored in a new `char.png` file.

### General
- `resourceName` + " -> " + `id` now gets sent to the game log when a new texture is loaded.

# rd-160052-launcher
## Additions
### Blocks
**dirt**
- Has an ID of `03`.
- Can be selected by pressing `2`.

**stoneBrick**
- Has an ID of `04`
- Can be selected by pressing `3`.
- Uses a slightly modified version of the previous rock texture.
- Downgrading calmWater into this version makes it possible to obtain calmWater at the world edge at non-ticking coordinates adjacent to a stoneBrick, which is normally unobtainable.⬟
  - This is very difficult to obtain, as rendering the chunk with the calmWater crashes the game.

**wood**
- Has an ID of `05`
- Can be selected by pressing `4`.
- Downgrading calmWater into this version makes it possible to obtain calmWater at the world edge at non-ticking coordinates adjacent to wood, which is normally unobtainable.⬟
  - This is very difficult to obtain, as rendering the chunk with the calmWater crashes the game.

**empty**
- Isn't assigned an ID, and instead it's an unused constant with a value of `null`.

### Non-mob entities
**Particle**
- Breaking a block creates 64 particle entitites.
- They're 0.2 blocks wide.
- Every tick a Particle has a 10% of being removed.
- They have different movement physics compared to the player and zombie.
  - They are affected by gravity less.
  - They lose their horizontall velocity midair slower.
- Particles are rendered as a flat texture using billboarding.
  - The texture only tilts horizontally, not vertically.
- They have the same rendering issue as the player camera and Zombies. Before they're first ticked, their position is interpolated between 0,0,0 and their actual position.
- They aren't saved in the `level.dat`.

### World generation
- The world is now randomly generated using Perlin noise.
- The terrain consists of rock, grass and dirt.
- Attempting to load a level.dat that is too short now crashes the game instead of filling missing blocks with natural generation.

### Gameplay
**Controls**
- Pressing `1`, `2`, `3` or `4` now sets the block type of placed blocks to rock, dirt, stoneBrick or wood respectively.
  - The currently selected block type is shown in the top right corner of the screen.
- Pressing `G` now spawns a zombie at the player's position.
  - This does not have the same interpolation issue as other entities because the zombie is ticked before it has a chance to render.

**Random ticks**
- Every tick a number of blocks in the world are randomly selected to be ticked.
  - The number of blocks is `width * height * depth / 400`, which is 10,485.76 in this version.
    - Fractional block ticks carry over to the next game tick.
    - A given block will therefore be ticked every 20 seconds on average.
- The only block affected by random ticks is grass.
  - If the grass is not lit, it turns into dirt.
  - Else 4 random blocks get picked in a 3x5x3 box around the grass. If a picked block is dirt and is lit, it turns into grass.
- If a block with ID between `06` and `FF` is ticked, the game crashes.

### General
- Added a crosshair.

### Issues
-  Blocks with ID between `06` and `7F` crash the game when a chunk containing them is rebuilt or when moving into them.
  - Since only 8 chunks can be rebuilt per frame, this can be temporarily prevented by dirtying nearby chunks.
  - This makes it much more difficult to obtain invalid block configurations from downgrading calmWater or calmLava, but still technically possible. The further the block is from a chunk boundary the higher the difficulty.
- Blocks with ID between `80` and `FF` crash the game when random ticked, when an adjacent solid block is rendered, when in reach of the player or when exposed to skylight.
  - Currently all blocks are considered solid.
  - Blocks on Y 0 don't crash the game when exposed to skylight.
  - If the block is exposed to skylight on world load, it will regenerate the world instead of crashing.

## Changes
### Blocks
**rock**
- Can be selected by pressing `1`.
- Texture changed.

**grass**
- Changed ID to `02`. Grass blocks from previous versions convert to rock.
  - grass cannot be obtained in worlds generated in older version through normal means.
- Texture changed, now has a 3 different textures for the top, side and bottom faces.

### Mobs
**Zombie**
- Reduced the number of initially spawned Zombies from 100 to 10.
- Now get removed when below Y -100 instead of respawning when above Y 100.
- Increased the chance of a zombie jumping every tick from 1% to 8%.
- Modified how a zombie's angular acceleration randomly changes.

### Gameplay
- Lowered the tick rate to 20 ticks per second.
  - Modified movement physics to account for this.
    - Increased walking speed from 4.41176 m/s to 5.50964 m/s.
    - Increased jump height from 1.06750 blocks to 1.23350 blocks.
    - Increased terminal falling velocity from 14.99998 m/s to 79.99988 m/s.
    - Increased friction while grounded.
  - Lowered the maximum number of ticks in a frame to 20.

### General
- The game is now in fullscreen mode.
- Changed chunk rendering.
  - Only 8 chunks can be rebuilt per frame.
    - Dirty chunks are sorted based on whether the chunk is within the player's field of view, when the chunk was last dirtied and their distance to the player.
- Changed fog rendering.
- Made the block selection flashing less harsh.
- Updated `terrain.png` to include new block textures and texture changes.

# rd-161348-launcher
## Additions
### Blocks
**bush**
- Has an ID of `06`.
- Can be selected by pressing `6`.
- Decays into ID `00` when random ticked unless it is lit and the block below is either grass or dirt.
  - The bush has no placement restrictions, it can be placed regardless of if it ends up decaying or not.
- Unlike all other blocks it isn't solid.
  - It doesn't impede movement, block light, or cause neighboring faces to be culled.
- Its model is 2 perpendicular flat textures on a 45° angle.
- Downgrading calmWater into this version makes it possible to obtain calmWater at the world edge at non-ticking coordinates adjacent to a bush, which is normally unobtainable.⬟
  - This is very difficult to obtain, as rendering the chunk with the calmWater crashes the game.
### General
- Added an applet class.
- Added the `META-INF` folder, which includes the `MANIFEST.MF`, `MOJANGCS.RSA` and `MOJANGCS.SF` files.

## Changes
### Blocks
**wood**
- Texture changed.

### Non-mob entities
**Particle**
- Reduced intial particle velocity. Particles are now given a slight upward boost.
- Particles now fall slower.
- Particles no longer have a flat 10% chance of getting removed every tick, instead when they have a random lifetime between 4 and 40 ticks.
  - Shorter durations are likelier.
  - A lifetime of 40 ticks is extremely unlikely, as it requires `Math.random()` to return exactly 0.0.
- Particles now have a random size between 0.1 and 0.2 blocks.
  - This is purely visual, their hitbox is still a 0.2 blocks wide cube.
- Particles now billboard vertically as well, instead of just horizontally.

### General
- Slightly optimized block selection code.
  - Blocks not within the player's field of view are no longer checked.
- The game is once again windowed with a resolution of 1024x768 like before.
- Made the crosshair thicker and larger.
- Made the selected block GUI slightly larger.
- Updated the `terrain.png`.
  - The file is anachronistic, it dates to 2009-05-21 and is identical to 0.0.13a's version.
  - Added the bush texture. Changed the wood texture.
  - Added unused unbreakable, opaque and semi-transparent water, lava and duplicate top grass textures.
- Changed the package name from `com.mojang.rubydung` to `com.mojang.minecraft`.