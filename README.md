# GB Studio 3.0.3 Background Sprites Tutorial
![Alt text](/help/BackgroundSprites-2.4.gif "Example")

Interactive GB Studio 3.0.3 tutorial for rendering background tiles in front of sprites


### Lessons:
1. How to setup a sprite to render behind background tiles
2. How transparency is handled
3. Use of triggers to toggle player sprite in front of and behind background tiles
4. Simulating additional layers
5. Animating background tiles to hide the transition between sprites in front of and behind background tiles

### Concepts:
1. Animation States
2. Related Sprite Editor features
3. Builds off https://github.com/phinioxGlade/gbstudio-3-animated-tile-tutorial 

Enjoy :)

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

## Currently the rest of the lesson is only available within the source code
