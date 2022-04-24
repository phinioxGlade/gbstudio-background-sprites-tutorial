# GB Studio Tutorial - Background Sprites 
![](/help/BackgroundSprites-2.4.gif "Example")

Interactive GB Studio tutorial for rendering background tiles in front of sprites. The source code was built using with GBS 3.0.3. Enjoy :)

### GB Studio Tutorials:

- [1.0 - Animated Tiles](https://github.com/phinioxGlade/gbstudio-3-animated-tile-tutorial)
- [2.0 - Background Sprites](https://github.com/phinioxGlade/gbstudio-background-sprites-tutorial) &lt; This Tutorial

### Lessons:

- [2.0 - How to setup a sprite to render behind background tiles](#lesson-20---how-to-setup-a-sprite-to-render-behind-background-tiles)
- [2.1 - How transparency is handled](#lesson-21---how-transparency-is-handled)
- [2.2 - Use of triggers to toggle player sprite in front of and behind background tiles](#lesson-22---use-of-triggers-to-toggle-player-sprite-in-front-of-and-behind-background-tiles)
- [2.3 - Simulating additional layers](#lesson-23---simulating-additional-layers)
- [2.4 - Animating background tiles to hide the transition between sprites in front of and behind background tiles](#24---animating-background-tiles-to-hide-the-transition-between-sprites-in-front-of-and-behind-background-tiles)

### Concepts:

- Animation States and Frames 
- How an actor is contructed
- Related Sprite Editor features
- Builds off concepts from my previous [GB Studio 3.0.3 - Tutorial 1.0 - Animated Tiles](https://github.com/phinioxGlade/gbstudio-3-animated-tile-tutorial)

### Useful Resources:

- [GBVM source file](https://github.com/untoxa/gbvm/blob/master/include/vm.i)
- [GBVM Command Reference](https://gist.github.com/pau-tomas/92b0ad77506088d184a654af226f5b7d)
- [GB Studio Central - Understanding GBVM](https://github.com/untoxa/gbvm/blob/master/include/vm.i)
- [GB Studio Plug-In Database](https://docs.google.com/spreadsheets/d/1d2F5hSEMt6nkacw-qVnYlT3IPHqmCCaLFhRboC5xxc0/edit#gid=0)

### Lesson 2.0 - How to setup a sprite to render behind background tiles

We will begin by discussing the basic steps to render am actor/player sprite behind the background layer.

In GBS3, actors can be made up of multiple component sprites and frames of animations. 
We will refer to smaller component sprites as sub-sprites.
Each sub-sprite within animation frame can be independently set to render behind the background layer.
GBS3 provides the Sprite Editor for configuring sprite sheets.

#### How-to edit a Sprite

From the Game World section:
1. Expand the "Game World" drop down list in the top left under the File Edit menu
2. Then select "Sprites" to open the Sprite Editor
3. Find the sprite you want to edit, this part of tutorial we will focus on the *player_platform* sprite

#### Animation States and Sub-States

Each sprite is made up of animation states. These states are made up of sub-states based on the "Animation Type". 
*player_platform* is of type "Platformer Player", which consists of:

1. Idle Left/Right: Animation played when not moving
2. Moving Left/Right: Animation played when while moving
3. Jump Left/Right: Animation played while jumping
4. Climbing: Animation played while climbing a ladder

GBS studio allows you to mirror Left/Right animations and this is checked by default.

#### Creating a new Animation State

To create a new animation state, click the "+" button next to the ANIMATIONS heading.
New states default to the "Fixed Direction" animation type, with only the Idle sub-state.
To get the additional sub-stats, change the type to "Platformer Player".
Its recommended that you also rename state so its easier reference, in this tutorial it was renamed to "behind"

#### Recreating the Animations

Currently GBS lacks a clone animation state/sub-status feature, so you will need to manually recreate all the animation frames.
This is done my dragging tiles from the sprite sheet into the animation frame and repeating for all frame you want to recreate.

#### Set sprites to display behind background layer

Once the animation has been recreated, the final step is setting which parts of the actor will be "Display behind background layer".
As mentioned previous each sub-sprite can be independently set to render behind the background layer, in this tutorial we made the entire frame to behind:

1. Select all the tiles in the frame
2. Check the "Display behind background layer" in the Sprite Tiles panel on the right
3. Repeat for each frame of animation and all the sub-states

#### Using the "behind" Animation State

Now the sprite is built. We just need to set the Animation State.
Add the event "Set Actor Animation State", in this example to the Scene "On Init", and set Player's state to "behind".
You can do this for any actor, no just the Player.
Use the same event to swap back to "Default" animation state, we will discuss this further in next part of the lesson.

### Lesson 2.1 - How transparency is handled

<img src="/help/lesson-2-1-0.gif" style="width: 320px;" />

When your designing your artwork for sprites behind the background layer, there is the transparent shade.

This is assigned to the lightest/white shade.

So light green, dark green and black all render in front of the sprite.

You need to keep this in mind when creating backgrounds to avoid unwanted overlap.

You can change the which shade is transparent, but requires [NalaFala (Yousurname)'s plug-in](https://github.com/Y0UR-U5ERNAME/gbs-plugin-collection/tree/main/plugins/setPaletteColorsPlugin/events) or GBVM scripting (presumed GBVM has this feature). This will be covered in a future tutorial.

### Lesson 2.2 - Use of triggers to toggle player sprite in front of and behind background tiles

<img src="/help/lesson-2-2-0.png" style="width: 320px;" />

In this basic example we will toggle the player's animation state between sprites in-front of background tiles and spirtes behind background tiles.

In this instance we have added a trigger which overs the brick pilar.

Trigger's "On Enter" has the event "Set Actor Animation State", which sets the player's the state to "behind".

<img src="/help/lesson-2-2-1.png" style="width: 320px;" />

Trigger's "On Leave" does the reverse. Its swaps the state back to "Default".

<img src="/help/lesson-2-2-2.png" style="width: 320px;" />

This is done so the player is only behind while obscured by the pilar.

<img src="/help/lesson-2-2-3.gif" style="width: 320px;" />

To avoid noticable pop when the states are swapped we have empty tiles either side of the pilar. This needs to be size of your player sprite, hence two transparent tiles left and right. 

### Lesson 2.3 - Simulating additional layers

<img src="/help/lesson-2-3-scene.png" style="width: 320px;" />

The Gameboy is limited to just two layers:

1. The background tiles
2. The sprites

But what if you wanted three layers?

Well, you can achieve this affect by carefully mixing sprites rendered in front of and behind the background layer.

We have already shown that triggers can be used to toggle player sprite behind but you can also do this for any sprite.

#### Background Layer

<img src="/help/lesson-2-3-1.gif" style="width: 320px;" />

Lets add a spaceship.

Which we want to be on the furtherest layer back. Set its state to *behind*.

![](/help/lesson-2-3-spaceship-background-animation-state.png "Spaceship-Background Animation State Event")

#### Middle Ground Layer

<img src="/help/lesson-2-3-2.gif" style="width: 320px;" />

Next lets make a middle ground layer.

Add another spaceship.

Add logic to the actor's *On Update* so that if the actor is between X 15 and X 19, set the state to behind.

<img src="/help/lesson-2-3-4.png" style="width: 640px;" />

*The example in the tutorial is incomplete and doesn't always work as intended. The spaceship movement script would need to be adjusted to better incorporate the layer change*

#### Foreground Layer

<img src="/help/lesson-2-3-5.gif" style="width: 320px;" />

You could add a forth layer with sprites in front of the foreground pilar.

#### Concussion

Now we have 3 psuedo layers:
1. Spaceship always behind
2. Spaceship that toggles state using logic
3. Pilar in front of all sprites

The amount of simulated layers is upto your creativity, coding skills and choice artwork.

## 2.4 - Animating background tiles to hide the transition between sprites in front of and behind background tiles

![](/help/BackgroundSprites-2.4.gif "Example")

For the final part of the lesson, we will be using animated tiles to mask the transition between sprite states to create hidden path.

The code for animating tiles was covered in my [Animated Tiles Tutorial](https://github.com/phinioxGlade/gbstudio-3-animated-tile-tutorial) available on Github. We will not be explaining the GBVM scripting required.

![](/help/lesson-2-4-frames.png "Tile Animation Frames")

Above is 8 frames of the animations. We will reuse the first 4 frames for both the dark and very dark end tiles.

This is the basic concept:

1. Initialize the hidden path by setting actors behind and swapping background tiles to their foreground version (GBVM scripting)
2. Add a trigger within the foreground wall which sets the actor sprite states to "behind" and begin the animated transition (GBVM scripting)
3. The animation is handled using the "On Update" of the orb actor, a Timer event might be a better choice
4. When the animation reaches the frame 5, set the states to "Default"
5. When the animation reaches the frame 8, stop animation
6. Add a second trigger with the reverse logic to hide the path

## Currently the rest of the lesson is only available within the source code
