# 2D Platformer Tutorial for Unity 2017

TODO intro. 
[Demo of the game](https://hardlydifficult.com/Kong/index.html)

Target audience: we try to assume little without boring those with experience.  You don't need to know how to code and it's okay if this is your first time with Unity.  You can follow step-by-step and copy/paste scripts, but we aim to teach the process along the way as well.  New concepts are introduced as they come to help beginners and intermediate developers understand.  

This is very much a WIP.  I'm trying to make a tutorial helpful to a range of experience levels.  Please let me know if you have any suggestions - I'm creating this live at [twitch.tv/HardlyDifficult](https://twitch.tv/HardlyDifficult) or email nick@HardlyDifficult.com


<br><br>

**FYI**: The sequence and 'How' sections should be solid for chapter 1-5.  Questions as well as general 'what did that do' type content will be revisited.  If you try this, please take notes of any questions which come to mind and send those my way.  We'll be working on those after the process and how-to sections are complete.

<br><br>

# 1) A game with enemies spawning

In chapter 1, we create a 2D game in Unity with spiked balls spawning at random intervals from an evil cloud.  They roll across platforms and fall from level to level.

TODO tutorial video link

<img src="http://i.imgur.com/V5qEyiQ.gif" width=300 />

TODO demo of level 1

## 1.1) Start a 2D project

Get Unity and start a 2D project. 

<details><summary>How</summary>

 - [Download Visual Studio Community edition](https://www.visualstudio.com/), if you don't already have it.
 - [Download Unity](https://unity3d.com/), the free Personal edition has everything you need. 
   - You may be prompted to register / sign in.
 - Select '2D' when creating a new project.
 - Enter a name/directory - the other options can be left at defaults.

<img src="http://i.imgur.com/q5NVa7p.png" width=300 />

<hr></details>


<br>


<details><summary>Whats the difference between 2D and 3D?</summary>

Presenting the 2D vs 3D option when you create a new project suggests this is a significant choice.  It's not really... 2D just changes default settings on things like your camera.   Unity is a 3D engine, when creating 2D games your actually creating a 3D world where everything is very flat but the camera looks straight ahead and the only rotation in the world is around the z axis.  

[More on 2D vs 3D from Unity](https://docs.unity3d.com/Manual/2Dor3D.html).

<hr></details>




## 1.2) Import assets

Create directories and import assets.  TODO link

<details><summary>How</summary>

 - Right click in the 'Project' window's Assets directory -> Create Folder named "Art".
   - You can rename folders by selecting and pressing F2.
 - Drag/drop all the assets (images and sounds) into the folder you just created.
   - If you have a zip file, you may need to unzip to a temp directory before drag/drop will work.

<img src="http://i.imgur.com/7JleUl7.png" width=300px />

 - Create additional directories which we will be using to organize our game:
   - Assets/**Art**
   - Assets/**Code**
     - Assets/Code/**Components**
     - Assets/Code/**Editor**
     - Assets/Code/**Utils**
   - Assets/**Prefabs**

TODO create directory struture

<hr></details><br>
<details><summary>TODO</summary>

We are using:
 - [Kenney.nl's Platformer Pack Redux](http://kenney.nl/assets/platformer-pack-redux) **spritesheets/spritesheet_ground.png**.

<hr></details>


<details><summary>Can I name folders differently?</summary>

aoeu

<hr></details>
<details><summary>What's a sprite / sprite sheet?</summary>

A sprite is an image, used in 2D games and for UI.  They may represent an object, part of an object, or a frame of an entity's animation, etc.  

A sprite sheet is a single image file that contains multiple individual sprites.  The sheet may use these sprites to represent different frames for an animation or to hold a collection of various object types (as is the case here).

<hr></details>
<details><summary>Can I use my own art?</summary>

Of course, this tutorial only assumes that you are using sprites.  You can build your own sprite sheet or use individual sprites, but this tutorial is geared towards a 2D game and some things may not work out well if you try using 3D models instead.

<hr></details>

</details>


## 1.3) Slice sprite sheets

Slice each of the sprite sheets in order to access the individual sprites within.


<details><summary>How</summary>

- Select a sprite sheet in the 'Project' (such as Assets/Art/**spritesheet_ground**).
- In the 'Inspector', set 'Sprite Mode' to 'Multiple'.

<img src="http://i.imgur.com/duYuVMy.png" width=300px />

- Click 'Sprite Editor' and apply changes when prompted.
- Click the 'Slice' menu item (see below for the type to use per sprite).
  - If all the sprites in the sheet are the same size, use Grid By Cell Count and enter the number of sprites in the sheet horizontally (columns) and vertically (rows).
  - If the sprites in the sheet are various sizes, use Automatic.

<img src="http://i.imgur.com/3wLWBZG.png" width=300px />

<img src="http://i.imgur.com/d3XzhRU.png" width=300px />

- Click 'Slice' button.
- Click 'Apply' and close the Sprite Editor.
- Repeat for each sprite sheet.

We are using:
 - **spritesheet_ground**: Cell Count (8 x 16)
 - **adventurer_tilesheet**: Cell Count (9 x 3)
 - **spritesheet_jumper**: Automatic
 - **spritesheet_tiles**: Cell Count (8 x 16)

<hr></details><br>

<details><summary>Why not always use Automatic?</summary>

TODO

<img src="http://i.imgur.com/lKfaiMj.png" width=300px />

<hr></details>
<details><summary>What does slicing achieve?</summary>

Slicing is the process of defining each individual sprite in a sprite sheet.  Once sliced, you can access each sprite as if it were a unique asset.

After you have sliced, white lines appear in the 'Sprite Editor'.  These lines show you how the sprite sheet is cut, boxing in each individual sprite.  Any whitespace as shown in this example is ignored (i.e. it does not generate blank sprites as well).

<img src="http://i.imgur.com/NawupLS.png" width=50% />

After closing the 'Sprite Editor' and applying changes you can expand the sprite sheet in Assets to see each sprite it created.

<img src="http://i.imgur.com/Qq0nn2B.png" width=50% />

<hr></details>

## 1.4) Set the filter mode

Update each sprite's and sprite sheet's import settings to use filter mode point.

<details><summary>How</summary>

 - Select all of the sprites and sprite sheets.
   - Use Ctrl click or shift click as you would while selecting in Windows Explorer.
 - In the 'Inspector', set 'Filter Mode' to 'Point (no filter)' and apply.

<img src="http://i.imgur.com/B0nqf75.png" width=300px />

<hr></details><br>
<details><summary>Why use Point and not the default of Bilinear?</summary>

Filter mode of Bilinear or Trilinear blurs the image a bit in attempt to make smooth lines.  Often for a 2D game, we want control down to the pixel and this effect is not desirerable.  Here's an example with the character sprite we will be using:

<img src="http://i.imgur.com/AYyx3Ma.png" width=150px />

<img src="http://i.imgur.com/8wMlM1S.png"  width=150px />

For sprite sheets, often each object is touching the one next to it.  Filter Mode Point prevents blending happening between one sprite and it's neighbor.  The blending that occurs with other modes besides Point may lead to random lines showing up on screen.  For example:

<img src="http://i.imgur.com/ZKqg5JP.png" width=50% />

<hr></details>



## 1.5) Set the mesh type

Update each sprite's and sprite sheet's import settings to use mesh type full rect.

<details><summary>How</summary>

 - Select all the sprite sheets.
   - For some reason, Unity won't allow this option to be changed for both sprites and sprite sheets at the same time.
 - In the Inspector, set 'Mesh Type: Full Rect'.
 - Then select each sprite and do the same.

<img src="http://i.imgur.com/Dhe3Nzt.png" width=300px />

<hr></details><br>

<details><summary>Why use Full Rect and not the default of Tight?</summary>

When using tiling on a sprite, Unity recommends updating the sprite sheet to use 'Full Rect'.  I don't have an example of issues that may arrise from using 'Tight' instead, but here is the warning from Unity recommending 'Full Rect':

<img src="http://i.imgur.com/e9jE83B.png" width=50% />

TODO .  Plus performance.  Rect uses 2 trigs while tight creates a complex polygon.  Rect batches better.

<hr></details>



## 1.6) Disable Anti-Aliasing

Update the project settings, disabling Anti-Aliasing for each quality level.

<details><summary>How</summary>

 - Menu 'Edit' -> 'Project Settings' -> 'Quality'.
 - In the Inspector change 'Anti Aliasing' to 'Disabled'.

<img src="http://i.imgur.com/auHPjbi.png" width=300px />

 - Repeat this for each quality 'Level'.
   - Click on the row to modify (e.g. 'Very High').
   - Update Anti Aliasing if needed.

<img src="http://i.imgur.com/KYym6V0.png" width=300px />

 - Click 'Ultra' to resume testing with the best settings.

<hr></details><br>

<details><summary>Why do we need to change this setting multiple times?</summary>

The highlighted Level is what you are testing with ATM.  It will default to Ultra.  The green checkboxes represent the default quality level for different build types.  In this example I'm testing with Ultra, using Ultra by default for PC builds, and High by default for WebGL builds.  To avoid artifacts, I disable Anti Aliasing in every level and then switch back to Ultra.

<hr></details>
<details><summary>What is Anti Aliasing and why disable it?</summary>

Anti Aliasing is a technique used to smooth jagged edges as shown here:

<img src="https://qph.ec.quoracdn.net/main-qimg-10856ecbea4f439fb9fb751d41ff704a" width=50% />

Like changing the filter mode to Point, we do this when working with sprites because we often want control over images down to the pixel.

Anti-aliasing may lead to unexpected gaps or distortions when sprites are side by side.  Here is an example that appears when using tiling and Anti Aliasing is enabled:

<img src="http://i.imgur.com/vY5YmVj.png" width=50% />

<hr></details>



## 1.7) Select an aspect ratio

Change the aspect ratio to 5:4 in the Game window and build settings.

<details><summary>How</summary>

 - In the 'Game' window, near the top, change 'Free Aspect' to '5:4'.

<img src="http://i.imgur.com/MTnZtu4.png" width=300px />

You'll also want to update the supported resolutions for the different platforms you may cut a build for:

 - Menu File -> 'Build Settings'.
 - Select the desired platform and click 'Player Settings'.

<img src="http://i.imgur.com/R1B43yZ.png" width=300px />

 - In the Inspector, set the supported resolution or aspect ratio (this will be different for different platform types), for example:

<img src="http://i.imgur.com/to0M9sA.png" width=300px />

<img src="http://i.imgur.com/NhCWDTp.png" width=300px />

<hr></details><br>

<details><summary>TODO</summary>

The white box here represents the area that players will see:

<img src="http://i.imgur.com/eIq2LD2.png" width=300px />

<hr></details>

<details><summary>Why use a fixed aspect ratio?</summary>

We are building a game with a fixed display.  The camera is not going to follow the character which will simplify the game and level design for this tutorial.  With a fixed aspect ratio we can design a scene without any camera movement and be sure everyone has the same experience.

Different resolutions will scale the display larger or smaller but everyone will see the same amount of the world.

5:4 was an arbitrary choice, use anything you'd like.

<hr></details>


## 1.8) Set the camera size

Update the camera size to about 10.

<details><summary>How</summary>

 - In the 'Hierarchy' window, select the 'Main Camera'.
 - In the Inspector, change 'Size' to '10'.

<img src="http://i.imgur.com/PmeoqG7.png" width=300px />


<hr></details><br>

<details><summary>What does this do?</summary>

In the Game window, the platform should look smaller now.  In the Scene, the white box representing the viewable area has grown.

<hr></details>
<details><summary>Why change 'Size' and not camera position?</summary>

2D games by default use 'Projection: Orthographic'.  This means that the camera does not consider perspective, the ability to see more of the world the further it is from your eye. The amount of the world visible with a perspective camera is driven by it's position.  

For an Orthographic camera, the amout of the world visible is driven by a special 'Size' property. 'Size' defines how much of the world is visible vertically.  Then the aspect ratio is used to determine how much to display horizontally.  

<hr></details>

## 1.9) Select a background color 

Change the background color to black.

<details><summary>How</summary>

 - In the 'Hierarchy' window, select the 'Main Camera'.
 - In the Inspector, change 'Background' color and select black.

<img src="http://i.imgur.com/QKGcl9o.png" width=300px />


<hr></details><br>

<details><summary>TODO</summary>

TODO

<hr></details>

## 1.10) Save the scene

Save the current scene as "Level1".

<details><summary>How</summary>

 - File -> 'Save Scenes'.
 - Save it as Assets/Scenes/**Level1**.

<hr></details><br>
<details><summary>What's a scene?</summary>

The Scene represents a collection of GameObjects and components (defined below) configured for a game level or menu screen.  For this tutorial we are starting by creating part of Level 1.  Level 2, the menu, and other UI screens will be saved as separate scenes.  You can switch scenes via the SceneManager, and will cover this later in the tutorial. 

<hr></details>


## 1.11) Add an auto save script 

Create an editor script which automatically saves everytime you hit play.

<details><summary>How</summary>

 - In the Project Assets/Code/Editor directory:
   - Right click
   - Select 'Create' -> 'C# Script'
   - Name it **AutoSave**
 - Double click to open the file in Visual Studio.
 - Paste in the the following source code:
 
```csharp
using UnityEditor;
using UnityEditor.SceneManagement;

[InitializeOnLoad]
public class AutoSave
{
  static AutoSave()
  {
    EditorApplication.playmodeStateChanged
      += OnPlaymodeStateChanged;
  }

  static void OnPlaymodeStateChanged()
  {
    if(EditorApplication.isPlaying)
    { 
      return;
    }

    EditorSceneManager.SaveOpenScenes();
  }
}
```


<hr></details><br>

<details><summary>What happened and how do I know it worked?</summary>

You can confirm the save is working by noting the * in Unity's title.  This * indicates unsaved changes and should now go away everytime you click play.

<hr></details>
<details><summary>What about performance?</summary>

As an editor script, this logic is not included in the game you release.  Saving is incremental so there is very little time wasted when there is nothing new to save.  Unless you're one of the lucky ones who never sees Unity crash, this script is absolutely worth the time tradeoff.


<hr></details>
<details><summary>Why is the folder name important?</summary>

Unity uses special folder names to drive certain capabilities.  Any script under a folder named "Editor" will only run while testing in the Unity editor (vs in your built game).

[Read more](
https://docs.unity3d.com/Manual/SpecialFolders.html) from Unity.

<hr>

</details>

<details><summary>What's InitializeOnLoad</summary>

InitializeOnLoad is an attribute which enables the script.  The static constructor of any class with this attribute is executed before anything else in the game.

InitializeOnLoad is an editor only script and found under the UnityEditor namespace.

</details>


<details><summary>What's a C# attribute?</summary>

Attributes in C# are metadata added to classes, fields, or methods that may be queried by other classes.  In the AutoSave script, InitializeOnLoad, a Unity specific attribute, is used to ensure the static constructor on our AutoSave class is called when the game begins.

There are many [standard C# attributes](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/attributes/index) and [Unity specific attributes](http://www.tallior.com/unity-attributes/) that may be used.  Here are a few random examples:

```csharp
using UnityEngine;
using UnityEngine.Networking;

// Tells unity that this component only works
// if the GameObject also has a SpriteRenderer
[RequireComponent(typeof(SpriteRenderer))]
public class MyClassName : MonoBehaviour
{
  // Tells unity this field can be modified
  // in the inspector
  [SerializeField]
  // Limits the values you can enter 
  // in the inspector
  [Range(1, 10)]
  int count;

  // Used for multiplayer games to sync 
  // method calls
  [ClientRpc]
  void MyMethod() { }
}
```


<hr></details>
<details><summary>What's a C# static constructor?</summary>

Every object in C# may include a static constructor, this applies to static and non-static classes.  A static constructor is guaranteed to be called once (and only once).  The constructor will run before the first object is instantiated, a field is accessed, or a method is called (i.e. it happens before you touch the class).  You never call the static constructor directly.

A static constructor is a private static method named the same as the class, with no parameters and no return type.

```csharp
public class MyClassName 
{
  static MyClassName() 
  {
    // This is executed once automatically, before we do 
    // anything else with MyClassName.
  }
}
```
<hr></details>
<details><summary>What's a C# delegate?</summary>

A delegate in C# is an object representing method(s) to call at a later time. You may encounter delegates under the following names: Events, Action, Func, and delegate. Under the hood these are all implemented with a 'multicast delegate'.  

When a method is added to a delegate to be called later, this is referred to as 'subscribing'.  Multicast delegate means that any number of methods may subscribe to the same delegate.  We use += when subscribing so not to overwrite any other subscribers.

```csharp
EditorApplication.playmodeStateChanged += OnPlaymodeStateChanged;
```

If the owner of the delegate (in the example above that's EditorApplication) may outlive the subscriber, the subscriber should unsubcribe when it's destroyed.  Also, any time you are no longer interested in future updates, unsubscribe.  We do this with -= to remove our method and leave any remaining methods subscribed.

```csharp
EditorApplication.playmodeStateChanged -= OnPlaymodeStateChanged;
```

Events are a common use case for delegates.  For example, you may have a GameManager with a field for Points include an event "onPointsChange".  Other components/systems in the game, such as Achievements and the UI, may subscribe to the onPointsChange event.  When a player earns points, a method in Achievements is then called which can consider awarding a high score achievement and a method in the UI is called to refresh what the player sees on-screen.  This way those components only need to refresh when something has changed as opposed to checking the current state each frame.

```csharp
using System;
using UnityEngine;

public static class GameManager
{
  public static event Action onPointsChange;
  static int _points;
  public static int points
  {
    get
    {
      return _points;
    }
    set
    {
      _points = value;
      if(onPointsChange != null)
      {
        onPointsChange();
      }
    }
  }
}

public class MyCustomComponent : MonoBehaviour
{
  protected void Awake()
  {
    GameManager.onPointsChange 
      += GameManager_onPointsChange; 
  }

  protected void OnDestroy()
  {
    GameManager.onPointsChange
      -= GameManager_onPointsChange;
  }

  void GameManager_onPointsChange()
  {
    // React to points changing
  }
}
```

<hr></details>



## 1.12) Add a platform to the scene

Add a sprite to the scene representing the middle segment of a platform.  

<details><summary>How</summary>

 - Click the arrow on the sprite sheet in your Assets/Art directory (this displays each individual sliced image).  We are using **spritesheet_ground**.
 - Click and drag the platform sprite you want to use into the 'Hierarchy' window.  We are using **spritesheet_ground_72**. 
 
<img src="http://i.imgur.com/kZC4i6d.png" width=300px />


<hr></details><br>
<details><summary>TODO</summary>

This creates a GameObject with a SpriteRenderer component for that sprite.

<hr></details>
<details><summary>What's a GameObject, Transform, and Component?</summary>

Everything you see and interact with in a game is driven by GameObjects.  Typically a GameObject represents a single logical object in the world (e.g. a character).  It may be composed of child GameObjects, each responsible for part of the display and/or behaviour. It may also hold various components.  

A component is a set of logic (i.e. code) which may be added to a GameObject, or child GameObject, and is exposed in the 'Inspector' window for the GameObject you have selected in the 'Hierarchy'.  A GameObject may have any number of components and those components may by configured to customize the behaviour for that specific object.  

Unity has a number of components available out of the box, we will be using several Unity components in this tutorial and will be making many custom components as well.

A Transform component manages the GameObject's position, rotation and scale.  Every GameObject, including child GameObjects, have a Transform. Occasionally you will encounter a GameObject that has nothing rendered on screen.  In these cases the Transform is often completely ignored but may not be removed.

<hr></details>
<details><summary>What's a SpriteRenderer?</summary>

SpriteRenderer is a Unity component which renders a sprite on screen.  Select the GameObject in the 'Hierarchy' to view the SpriteRenderer component for this object in the 'Inspector'.  Here several options are available for modifying how the sprite is rendered.  For example:

 - Sprite: This is the sprite image to render.  It was populated automatically when you created the GameObject with drag/drop.
 - Color: White is the default, displaying the sprite as it was created by the artist.  Changing this color modifies the sprite's appearance.  You can also use the alpha value here to make a sprite transparent.

<img src="http://i.imgur.com/4w3P1nx.png" width=50% />

<hr></details>



## 1.13) Tile the platform's width

Change the SpriteRenderer draw mode to tiled and increase the width.

<details><summary>How</summary>

 - In the Hierarchy, select the 'spritesheet_ground_72' GameObject.
 - In the Inspector, under the SpriteRenderer component:
   - Change 'Draw Mode' to 'Tiled'
   - An option for 'Width' appears, increase this to about 10 (but don't change height).

<img src="http://i.imgur.com/MIgzjdO.png" width=300px />


<hr></details><br>

<details><summary>TODO</summary>

You should see the platform sprite get wider, repeating it's pattern.

<hr></details>
<details><summary>Why not use Transform scale?</summary>

Using transform scale to change the width cause the sprite displayed to stretch.  We are using tiling so the sprite repeats instead:

<img src="http://i.imgur.com/ejbs3RK.png" width=50% />

<hr></details>



## 1.14) Create platform GameObject

Create a new parent GameObject for the platform sprite.


<details><summary>How</summary>

 - In the Hierarchy, right click and 'Create Empty'.
 - Rename to "Platform".
 - Ensure the Transform is at defaults (position 0, rotation 0, scale 1) for both the 'Platform' and the sprite's GameObject 'spritesheet_ground_72'.

<img src="http://i.imgur.com/FAkZf1H.png" width=300px />

 - Drag and drop the sprite (spritesheet_ground_72) onto the Platform GameObject.  
 
It should appear indented under Platform in the Hierarchy:

<img src="http://i.imgur.com/XOve0Ap.png" width=300px />

<hr></details><br>
<details><summary>Why create a parent GameObject?</summary>

Most of the platforms we will be creating require multiple different sprites to display correctly.  We tackle this in the next section.  Even for platforms which are represented with a single sprite, it's nice to be consistent across all of our platforms.

The implications of using a parent GameObject or not will be more clear when we start to add game mechanics later in the tutorial.

<hr></details>
<details><summary>How is the sprite position calulated when it's a child?</summary>

When a GameObject is a child of another GameObject, it's position, rotation, and scale are the combination of the child's Transform and the parent's Transform (via matrix multiplication).  

Typically all Transform updates during the game and in level design are done to the parent GameObject.  Child Transforms are often static offsets from the center of the parent GameObject.  e.g. we'll be adding rounded edges to the platform, which will require an x offset so they are positioned next to the middle segment.

<hr></details>



## 1.15) Add rounded corners to platforms

Add sprites with rounded edges to the left and right of the platform.  

<details><summary>How</summary>

 - Click and drag one of the edge sprites onto the 'Platform' GameObject. We're using **spritesheet_ground_65** and **spritesheet_ground_79**.
   - The edge sprite should be a child GameObject, like the middle sprite.  If it does not appear indented, drag drop in the Hierarchy window to rearrange.
   - Confirm that each of the child sprites are still at 0 position, 0 rotation, and 1 scale.  The edge sprites may have an X position when we are done.
 - Move the edge sprite away from the main platform:   
   - Select the edge sprite (one of the child GameObjects).
   - Use the move tool to position it away from the other sprites.

<img src="http://i.imgur.com/bYsJhjs.png" width=150px />

 - Use Vertex Snap to position the edge next to the main platform:
   - Hold V to enable Vertex Snap mode.
   - A box appears for each anchor point (e.g. the corners of the sprite).  Hover over the top right corner.
   - Click and drag the box.  The sprite will snap perfectly with other anchor points in the world.

<img src="http://i.imgur.com/L82mkXu.gif" width=300px />

 - Repeat for both edges, creating smooth corners on both sides of the platform.

<hr></details><br>
<details><summary>TODO</summary>

TODO faq move, scale tools

TODO copy paste vs duplicate

<hr></details>


## 1.16) Create a connected platform

Our level design calls for the bottom platform to rotate half way through.  Create two Platform GameObjects and position and rotate their parents' GameObjects so that they appear connected.

<details><summary>How</summary>

 - Use two copies of the Platform GameObject.
   - Select and copy / paste or right click and 'Duplicate'.
 - Move their parent GameObjects so that the sprites appear near the bottom of the screen, side by side. 
 - Raise the right Platform a little above the left.
 - Delete the rounded edges from both Platforms.
 - Increase the 'Width' of middle sprite of each platform to about 15 so that the platforms combined cover more than the width of the screen.
 - Use Vertex Snap (by holding V) to reposition the edges.
 - Select the parent GameObject for the Platform on the right and use the rotate tool to modify the Transform's rotation Z value to about 4.

<img src="http://i.imgur.com/3s1bSBb.png" width=150px>

The scene should look something like this:

<img src="http://i.imgur.com/kL3NvA7.png" width=500px>


 - Select the middle sprite's GameObject for the platform on the right.
 - Drag and drop that child GameObject out of the Platform so it stands alone. (it will still appear at the same position/rotation). 
 - With Vertex Snap, use the box in the bottom left corner to drag the platform and connect perfectly with the other.
 - Copy paste the Transform position from the child you just placed to its original parent GameObject.
 - Drag and drop the sprite back into the original parent GameObject.
   - Confirm the child GameObject's Transform position and rotation are at 0.

<img src="http://i.imgur.com/iJ4fdYQ.gif" width=700px />

<hr></details><br>
<details><summary>Why not use a single GameObject for this bottom platform?</summary>

Up next we will be adding colliders to these platforms.  There are several ways this could be handled, as is always the case with GameDev. We will be placing BoxCollider2Ds on our Platforms' parent GameObjects.  This works great when the parent is a middle sprite segment along with a rounded corner sprite - but does not work as well when the platform changes it's rotation half way through.

<hr></details>
<details><summary>Why extend the platform beyond the edge of the screen?</summary>

The width of the world players are going to see is fixed so you could argue that extending over the edge is not necessary.  I recommend this to ensure there are no unexpected gaps at the edge and to leave some flexibility for future mechanics, including:

 - Allow some enemies to continue off screen and use the platform we can't see before returning to the game.
 - Screen shake.  This works by moving the camera up/down/left/right a bit.  Having the platforms extend beyond the edge of the screen allows us to do that without exposing gaps.

<hr></details>


## 1.17) Complete level 1 platform layout

At this point we have covered everything you need to match the level 1 platform layout.  You can match the layout we used or come up with your own.

<details><summary>How</summary>

The basic steps are:

 - Copy a parent Platform to start from.
 - Modify the tile 'Width' for the middle segment as needed.  Platforms should extend off the screen a bit.
 - Use Vertex Snap to position the edge sprites.
 - Move and rotate the sprite by modifying the parent GameObject, leaving the children at position and rotation 0, with the exception of the corner sprites which have an X position.
 - You can delete the rounded edges which are completely off screen.

Optionally, you can rename the platform GameObjects and organize your platforms by placing them in a parent GameObject.  e.g.:

 - Click and drag to re-arrange the platform GameObjects so they appear in the same order in the hierarchy as they do in game.
 - Rename each to represent it's position - e.g. "Level2".
 - Create an Empty GameObject, name it "Platforms".  Ensure that it is a position 0.
 - Select all of your existing platforms (the parent GameObjects) and click and drag them onto "Platforms".

The project should looks something like this, but don't worry about trying to match it perfectly:

<img src="http://i.imgur.com/utVCg6G.png" width=500px />

<hr></details><br>

<details><summary>TODO</summary>

Refer to the Game window to confirm your layout as they player will see it.

How to zoom and navigate the scene

<hr></details>



## 1.18) Add colliders to platforms

Add a BoxCollider2D to each of the Platforms.  Add an edge radius and edit colliders to match the sprites.

<details><summary>How</summary>

 - Select a platform's parent GameObject.
 - Click the 'Add Component' button, type "BoxCollider2D" and select it from the list.
 - Under Box Collider 2D in the Inspector, set 'Edge Radius' to '.1'

<img src="http://i.imgur.com/yM4DRr6.png" width=300px>

 - Click 'Edit Collider' and click/drag the box which appears so that the outer green line encapsulates the platform.
    - Click and then hold Alt while adjusting the sides to pull both sides in evenly.

<img src="http://i.imgur.com/Q4T1KfJ.gif" width=300px />

 - Repeat for each of the platforms.
   - For the bottom platforms which are two connected parent platform GameObjects - allow the colliders to overlap a little.

<img src="http://i.imgur.com/D5gBSiW.gif" width=300px />

</details><br>

<details><summary>TODO</summary>

some for a smooth experience when entities are walking from one to the next

<hr></details>
<details><summary>What is a Collider?</summary>

[Colliders](https://docs.unity3d.com/Manual/CollidersOverview.html) are components placed on GameObjects to define their shape for the purposes of physical collisions.  The collider shape may or may not align with the visuals on screen.

Typically colliders match the shape of the art on screen.  For example, they are used to keep the character from falling through the floor or walking through walls, and to cause the character to die when they hit an enemy.

Colliders may also be used as 'triggers' to detect something happening near an object without causing a physical reaction.  For example, an entity could have a second collider twice as large as the entity itself and use that to know when danger is approaching - causing the entity to run the other way.

</details>
<details><summary>Why not place colliders on the child GameObjects instead?</summary>

Well, you could!  With GameDev, you'll find there are almost always various ways you could achieve a goal and pros/cons to each.  

Since we are using BoxCollider2D and an Edge radius, getting our sprites to connect with a smooth surface for entities to walk over would be more challenging when the colliders are on the child sprite GameObjects instead of the parent Platform.  

<img src="http://i.imgur.com/QTjSEt7.png" width=50% />

Additionally, fewer colliders may improve your game's performance - however the difference here will not be noticeable.

</details>




## 1.19) Create a spike ball

Add a GameObject for the spike ball. 

<details><summary>How</summary>

 - Drag the sprite into the Hierarchy to create a GameObject for the sprite. We are using **spritesheet_jumper_59**.
 - Create a parent GameObject:
   - Right click -> 'Create Empty' GameObject named "Spike Ball".
   - Drag and drop the sprite into Spike Ball.
 
</details><br>
<details><summary>TODO</summary>

Why use a parent here?

<hr></details>



## 1.20) Set the ball's order in layer

Update the Spike Ball's Order in Layer to -1.

<details><summary>How</summary>

 - Select the Spike Ball's sprite.
 - Change the Sprite Renderer's 'Order in Layer' to '-1'.

<img src="http://i.imgur.com/TSqk7hb.png" width=300px />

</details><br>
<details><summary>What does Order in Layer do?</summary>

When multiple sprites are overlapping, Order in Layer is used to determine which one is on top of the other.  So if the spike ball sprite has Order in Layer '-1' and everything else uses the default Order in Layer '0', the spike ball will always appear behind of other sprites in the world.

Order in Layer may be any int value, positive or negative. Here's an example showing the character sprite we will be using with Order in Layer '-1' and with '2'... sitting on a platform which still has the default Order in Layer '0'.

<img src="http://i.imgur.com/QCHPLDf.png" width=50% />

</details>

## 1.21) Add a rigidbody to the ball

Add a Rigidbody2D to the spike ball.

<details><summary>How</summary>

 - Select the Spike Ball's parent GameObject.
 - Click Add Component and select 'Rigidbody2D'.

</details><br>

<details><summary>TODO</summary>

Hit play and watch the spike ball fall through the platforms and out of view:

<img src="http://i.imgur.com/PuWWL3z.gif" width=50px />

<hr></details>
<details><summary>What's a Rigidbody2D?</summary>

A rigidbody is a core component for the Unity physics engine, Rigidbody2D is the 2D version of this component (vs 3D).  It's added to GameObjects which may be manipulated by physics during the game.

TODO elaborate

Physics refers to the logic in a game engine which moves objects based on forces such as gravity. We'll be using rigidbodys on all moving objects in this game. 

</details>


## 1.22) Add a collider to the ball

Add a CircleCollider2D to the spike ball.  Adjust the radius as needed.

<details><summary>How</summary>

 - Add a 'CircleCollider2D' component to the spike ball.
 - Modify the radius so the collider is around the main body and not the spikes.

<img src="http://i.imgur.com/crXdz35.gif" width=300px />

</details><br>
<details><summary>TODO</summary>

Test, by placing the ball at the top of each platform.  If it gets stuck because some platforms are too close, update the platform position or rotation.

Hit play to watch the spike ball fall onto a platform and roll.

<img src="http://i.imgur.com/x4a848N.gif" width=300px />

<hr></details>
<details><summary>Why shrink the collider?</summary>

It's optional, use what you think creates the best experience.

When we added the CircleCollider2D, it defaulted to surround the entire sprite.  This may be the right experience, it's up to how you want the game to play.  I'm suggesting that we pull the collider in a bit, this will cause the spike ball to roll on its body with the spikes digging into platforms instead of rolling on the tips of each spike as shown here:

<img src="http://i.imgur.com/ov1F5Fo.gif" width=200px />

<img src="http://i.imgur.com/WRLQITb.gif" width=200px />

On a related note, seting the 'Order in Layer' to '-1' ensures that the spikes are behind the platform.  Without this the spikes would be ontop:

<img src="http://i.imgur.com/8cgB7jZ.gif" width=200px />


</details>



## 1.23) Add invisible bumpers

Add additional BoxCollider2Ds offscreen to redirect balls back on screen.

<details><summary>How</summary>

 - Create an Empty GameObject named "Bumper".
 - Add a 'BoxCollider2D' component.
 - Increase the collider Size X to about 20.

<img src="http://i.imgur.com/3ca7cy3.png" width=150px>


 - Move the GameObject off screen, near one of the platforms, like this:

<img src="http://i.imgur.com/VrjqmfY.png" width=300px />

 - Use the Rotate tool and adjust until the Z rotation to about 30.
 - Use the Move tool to reposition it so the edge of our bumper overlaps the platform.

<img src="http://i.imgur.com/5mUaPov.png" width=300px />



 - Copy paste the bumper and modify it's position and rotation so that each platform that may send a spike ball offscreen has a bumper.
   - We do not want a bumper for the bottom left as balls should not return after that point.

 Your screen with bumpers should look something like this:

<img src="http://i.imgur.com/NTMCw37.png" width=300px />

 - Optionally organize your bumpers by placing them in a parent GameObject named "Bumpers", like we had done for the Platforms.

</details><br>

<details><summary>TODO</summary>

Hit play, the spike ball should hit the bumper and quickly reverse and then accelerate the other direction: 

<img src="http://i.imgur.com/vMjWoia.gif" width=150px />
to cause the spike balls to quickly turn around and roll back on-screen

<hr></details>

## 1.24) Add a script to get the ball moving

Add a script to the spike ball which sets an initial velocity and angular velocity.

<details><summary>How</summary>

 - In the Assets/Code/Compenents/Movement directory, Create a C# Script and name it **InitializeRigidbody**.
 - Double click the script to open it and paste the following:

 ```csharp
using UnityEngine;

[RequireComponent(typeof(Rigidbody2D))]
public class InitializeRigidbody : MonoBehaviour
{
  [SerializeField]
  Vector2 startingVelocity = new Vector2(3, 0);

  [SerializeField]
  float startingAngularVelocity = -500;

  protected void Start()
  {
    Rigidbody2D myBody = GetComponent<Rigidbody2D>();

    myBody.velocity = startingVelocity;
    myBody.angularVelocity = startingAngularVelocity;
  }
}
```

 - Add the 'InitializeRigidbody' component to the spike ball.
 - Confirm the values in the Inspector are at the defaults written in code:
   - Initial Velocity of (3, 0) 
   - Angular Velocity of -500

<img src="http://i.imgur.com/34kpVEP.png" width=300px />


</details><br>
<details><summary>TODO</summary>
For the game, we  want the ball spawning in the top left.  But that's a flat surface so the ball does not roll down platforms.  

TODO

TODO faq on GetComponent, GetChildComponents...


TODO - Debugging tip / talk about the defaults in code vs inspector.  Check your values.  Maybe we should be more explicit in the steps.

TODO - FAQ.  Scripts don't work if the class is named different from the file.  Not normally true for C#. And no error presented.  It just won't be selectable as a component.


<hr></details>


<details><summary>Why not use a "SpikeBall" component instead?</summary>

You could, but...  

Unity encourages component based solutions, where you aim to offer a single mechanic per component.  Here's a good [wikipedia article on component based](https://en.wikipedia.org/wiki/Component-based_software_engineering) design.  Briefly, the advantages to this approach are:

 - Each script or component focuses on a single feature or mechanic, simplifying and making it easier to debug.
 - Components may be reused between different object types.  If we had one master SpikeBall component and then created a similar enemy with a few different mechanics, reusing logic would be more challanging and we might copy paste parts to our new enemy compoment instead. 

</details>
<details><summary>What's velocity and angularVelocity?</summary>

A GameObject with a rigidbody may be moved with forces.  The Unity Physics engine uses these forces as inputs in order to calculate the object's position and rotation, considering other things in the world such as a wall blocking your path.  

Unity follows the [Newton's Laws of Motion](https://en.wikipedia.org/wiki/Newton%27s_laws_of_motion) - e.g. an object either remains at rest or continues to move at a constant velocity, unless acted upon by a force.

There are various APIs for manipulating forces on a rigidbody.  This script will be setting initial values for:

 - Velocity: the desired movement direction and speed.  Abstent any additional forces, 'Drag' decreases the velocity every frame until it reaches 0.
 - Angular velocity: degrees per second to rotate the object.  Abstent any additional forces, 'Angular drag' will decrease this until it reaches 0.

</details>
<details><summary>What's SerializeField and why not use public instead?</summary>

[SerializeField] exposes the object's field (data) in the 'Inspector' window.  The default value seen in the C# script becomes the default in the Inspector - however when the script runs, the value is whatever you set for that object in the Inspector. This allows you to change values per-object or have different values for a component which is used on various different object types.  You can also change values in the Inspector at runtime, which can be helpful while debugging.

Read [more about Serialization in Unity](https://docs.unity3d.com/Manual/script-Serialization.html).

Any public field is a SerializeField by default.  If you do not want a public field to be exposed in the inspector, you can add the [NonSerialized] attribute (from the System namespace).  

So why not just public instead of [SerializeField]?

The fields in question are often only leveraged inside the component itself.  Other components may not interact with these fields directly.  In those scenarios, I prefer to follow the Object-Oriented programming best practice of [data encapsulation](https://en.wikipedia.org/wiki/Encapsulation_(computer_programming)) - meaning we only expose public fields when we want other classes to interact with them.

</details>

<details><summary>What's RequireComponent do?</summary>

[RequireComponent] is an Unity attribute used to let the editor know that this component requires another component on the same GameObject.

```csharp
[RequireComponent(typeof(ComponentThatMustBeOnThisGameObject))]
public class MyComponent ...
```

When you add a component in the inspector which requires another, and the required component is not already on that GameObject, Unity will automatically add it for you.

</details>
<details><summary>What is MonoBehaviour / how is Start() called?</summary>

Most of the scripts that you create in Unity will derive from MonoBehaviour.  [MonoBehaviour](https://docs.unity3d.com/ScriptReference/MonoBehaviour.html) is the base class for a GameObject component (scripts on objects in your world).  It allows you to execute logic every Update (each frame) and respond collision events, etc.

There are a lot of events available to MonoBehaviours.  In this example we are using Start which is called once per-object, when that object is first spawned in the world.

Note that when implementing MonoBehaviour events, you do not use 'override' nor subscribe to the event.  Unity uses reflection based on the method signature instead to improve performance.  This creates an unintuative pattern for C# delevelopes but allows Unity to eliminate unncessary calls.  This optimization normally in development would be considered overkill but for a game engine this kind of thing adds up, particularly since there are typically hundreds of MonoBehaviours in the world.

TODO flow of events https://docs.unity3d.com/uploads/Main/monobehaviour_flowchart.svg

</details>
<details><summary>Why use protected on the Unity event?</summary>

Protected is an access modifier in C# which ensures that the only way to call that method, or field, is from the same class or from a class that derives from it.  Unity will find events such as Update() based on the signature, ignoring the access modifier - allowing you to use anything you'd like.

Why protected and not private?

When you are using inheritence and both the child and parent classes need to include an event such as Update(), Unity will only call the child's implementation.  This can make it easy to miss that some events in the parent class have been overwritten (vs complemented by) the child.

I recommend using protected on every Unity event so that the compiler can help avoid this mistake.  In the event the parent and child classes both have protected Update(), you will get a compile warning about the conflict.  

If you want both child and parent called, update the methods as follows:

```csharp
using UnityEngine;

public class Test : MonoBehaviour
{
  protected virtual void Update()
  {
    // Parent update logic
  }
}

public class AChildOfTest : Test
{
  protected override void Update()
  {
    base.Update();
    // Child update logic to run after the parent's Update
  }
}
```

If you want the child to replace the parent's update method (so that the parent's Update is never called), update the method like so:

```csharp
using UnityEngine;

public class Test : MonoBehaviour
{
  protected void Update()
  {
    // Parent update logic
  }
}

public class AChildOfTest : Test
{
  protected new void Update()
  {
    // Child update logic to be run instead of the parent's Update
  }
}
```

What if it's not a parent class?

I recommend always using protected on Unity events.  A class may not be a parent at the moment but code constantly changes and matures.  This is a best practice to help avoid potential issues in the future.  If the class never becomes a parent, the method is effectively treated as private.  There is no performence or other runtime impact from using protected.

Why not always make the methods virtual?

Performance.  There is a runtime cost to marking a method as virtual, even if there are no overrides.

Why not public instead?

Encapsulation.  If we were to make these methods public, it suggests that other components may call the events directly.  I've yet to encounter a use case where it's appropriate to do that - you should rely only on Unity to call these events to keep your code clean.

</details>

## 1.25) Add a script to destroy balls that roll off

Add a script to the spike ball which destroy's the GameObject after it rolls off the bottom platform.

<details><summary>How</summary>

 - Create a script **SuicideOutOfBounds** under Assets/Code/Compenents/Death and paste the following:

```csharp
using UnityEngine;

public class SuicideOutOfBounds : MonoBehaviour
{
  const float outOfBoundsYPosition = -12;

  protected void Update()
  {
    if(transform.position.y < outOfBoundsYPosition) 
    { 
      Destroy(gameObject);
    }
  }
}
```

 - Add 'SuicideOutOfBounds' to the spike ball.

</details><br>
<details><summary>What did that do?</summary>

SuicideOutOfBounds will destroy the GameObject for anything that goes below -12, which is a bit lower than the lowest the camera can see. 

Play and the ball should now destroy itself when it falls off screen:

<img src="http://i.imgur.com/xcqUO8I.gif" width=300px />

This script would work the same without a fixed aspect ratio (since different aspect ratios only impact how much of the world we see horizontally).  If we supported a moving camera, we may need to calculate the kill height differently.

<hr></details>
<details><summary>Why bother, the GameObject is already off screen?</summary>

When a GameObject is off screen, there is no attempt to render it so your GPU is not wasting time but Unity is still processing Physics and logic for any components on the GameObject.  In this case, once the GameObject has fallen off the bottom it will never return to the game.  

We destroy it to save performance while the game is running.  Without this script, the endless stream of balls spawning and then falling off would be a 'memory leak'.  This means that you are wasting resources and over time the performance of your game will get worse.

</details>
<details><summary>What is Destroy and why not Destroy(this)?</summary>

Destroy is a Unity method to remove something from the scene.  You can:

 - Destroy a component, causing the component to be removed from that GameObject (and stopping future event calls such as Update).  
 - Destroy a GameObject, causing that entire GameObject to be removed from the scene.

For example:

```csharp
using UnityEngine;

public class MyComponent : MonoBehaviour
{
  public bool shouldThisComponentStop;
  public bool shouldThisGameObjectBeRemoved;

  protected void Update()
  {
    if(shouldThisComponentStop)
    {
      // Remove MyComponent from this GameObject
      Destroy(this); 
    }
    if(shouldThisGameObjectBeRemoved)
    {
      // Destroy this entire GameObject from the scene
      Destroy(gameObject);
    }
  }
}
```

</details>
<details><summary>What about an object pool?</summary>

An object pool is an optimization technique which may be appropriate to use but we are not implementing it here for simplicity.  Additionally the performance gain for a game like this would be negligible.

What is an object pool?

Instantiate (creating a new GameObject) is one of the most expensive calls you can make.  An object pool is the programming term for reusing objects instead of destroying and creating new ones.  

For this example, instead of destroying a spike ball that falls off screen we would instead have it respawn at the top and go through the entire level again.

When should an object pool be used?

Objects which destroy and spawn again several times may warrent an object pool. There is overhead associated with having and using an object pool so it is not recommended for absolutely everything.  For example, a boss which is going to surface once in a game may not be a good choice to include in an object pool.

How is an object pool implemented?

Basically anytime we spawn a GameObject, we ask the object pool if there is one already available for us to reuse.  And when we would have destroyed a GameObject, we would instead do gameObject.SetActive(false) and add it to the object pool's list of available objects.  

For more, see [Catlike Coding's Object Pool tutorial](http://catlikecoding.com/unity/tutorials/object-pools/).

</details>

## 1.26) Create a ball prefab

Create a prefab for the spike ball, and remove the GameObject from the scene.

<details><summary>How</summary>

 - Select the Spike Ball and click/drag it to the Assets/Prefabs folder.
 - Delete the GameObject from the Hierarchy, removing it from the scene but leaving our prefab in-tact.

<img src="http://i.imgur.com/roE0SWK.gif" width=300px />

<hr></details><br>
<details><summary>TODO</summary>

TODO

<hr></details>

## 1.27) Create an evil cloud

Add a GameObject for the evil cloud.  Size and position it in the top left.

<details><summary>How</summary>

 - Drag in the sprite, we are using **spritesheet_jumper_57**.
 - Add it to an empty parent GameObject named "Evil Cloud".
 - Move it to the top left of the screen.
 - Use the Scale tool evenly on all dimensions till it fits nicely.

<img src="http://i.imgur.com/MZWguje.png" width=150px />
<br>
<img src="http://i.imgur.com/kK9dKcD.gif" width=300px />

</details><br>
<details><summary>What does changing scale Z do?</summary>

Nothing (for 2D games).  When we are scaling, in order to not distort the art we only need to ensure X and Y scales match.  Z could be left at the default of 1, but I prefer to keep it in sync with X and Y as well as Unity's scale tool will do this by default.

</details>



## 1.28) Add a script to spawn balls

Add a script to the evil cloud which periodically spawns balls.

<details><summary>How</summary>

 - Create a script **Spawner** under Assets/Code/Compenents/Life and paste the following:

```csharp
using System.Collections;
using UnityEngine;

public class Spawner : MonoBehaviour
{
  [SerializeField]
  GameObject thingToSpawn;

  [SerializeField]
  float initialWaitTime = 2;

  [SerializeField]
  float minTimeBetweenSpawns = .5f;

  [SerializeField]
  float maxTimeBetweenSpawns = 10;

  protected void Start()
  {
    StartCoroutine(SpawnEnemies());
  }

  IEnumerator SpawnEnemies()
  {
    yield return new WaitForSeconds(initialWaitTime);

    while(true)
    {
      Instantiate(
        thingToSpawn, 
        transform.position, 
        Quaternion.identity);

      float sleepTime = UnityEngine.Random.Range(
        minTimeBetweenSpawns, 
        maxTimeBetweenSpawns);
      yield return new WaitForSeconds(sleepTime);
    }
  }
}
```

 - Add 'Spawner' to the evil cloud.
 - Confirm the values for the component match the defaults in code.
 - Click/drag the Spike Ball prefab onto the 'Thing To Spawn' field.
 
<img src="http://i.imgur.com/scu8YUR.gif" width=300px />

</details><br>
<details><summary>TODO</summary>

Click play to see the spawner in action:

<img src="http://i.imgur.com/ZJSulAj.gif" width=300px /> 

<hr></details>

<details><summary>What's a prefab?</summary>

A prefab is a file representing a configured GameObject.  This includes any child GameObjects as well as Components and their settings from the Inspector. 

This allows things like our spawner to instantiate a GameObject with the appropriate components and configurations, without knowing any details about the specific object type it is spawning.  More [on prefabs from Unity](https://docs.unity3d.com/Manual/Prefabs.html).

</details>
<details><summary>What is a Coroutine / WaitForSeconds?</summary>

A Coroutine allows you to define a sequence which takes more than a single frame to execute.  It's implemented with a C# enumerator which Unity will then execute over time.  For example:

```csharp
using System.Collections;
using UnityEngine;

public class MyComponent : MonoBehaviour
{
  protected void Start()
  {
    StartCoroutine(ExampleCoroutine());
  }

  IEnumerator ExampleCoroutine()
  {
    print("Launch in T minus 3 seconds");
    yield return new WaitForSeconds(1);
    print("Launch in T minus 2 seconds");
    yield return new WaitForSeconds(1);
    print("Launch in T minus 1 seconds");
    yield return new WaitForSeconds(.75f);
    print("Almost there!");
    yield return new WaitForSeconds(.25f);
    print("Go go go");
  }
}
```

When Start is called, the first line is printed ("Launch in T minus 3 seconds") immediatally.  Then we 'yield return' how long until the next line should be excuted.

'yield' before the return is a special C# keyword used with enumerators.  It is marking your location in the method, allowing another class (in this example, Unity's internal logic), to resume the method from where it left off.

WaitForSeconds is a Unity class used to define how long before the enumerator should be resumed.  There are similar classes available: WaitForSecondsRealtime, WaitForEndOfFrame, WaitForFixedUpdate, WaitUntil, and WaitWhile to give you more control over when the Coroutine is resumed.

Coroutines may be canceled before it's complete by calling StopCoroutine or StopAllCoroutines.  When a GameObject is destroyed, any Coroutines it had started are stopped.

</details>
<details><summary>What does Instantiate do?</summary>

Instantiate clones a GameObject or prefab, creating a new GameObject in the scene.  There are a few variations of the call you could use.

To clone using the original's Transform (position, rotation, scale):
```csharp
Instantiate(thingToSpawn);
```

To clone and set a position and rotation:
```csharp
Instantiate(thingToSpawn, Vector3.zero, Quaternion.identity);
```

To clone and set a parent for this GameObject:

```csharp
Instantiate(thingToSpawn, gameObject);
```

</details>
<details><summary>How do you choose a random number?</summary>

Unity provides a convientent static class for getting random data.  For example:

```csharp
float randomNumber0To1 = UnityEngine.Random.value;
float randomNumberNeg10p5ToPos5 = UnityEngine.Random.Range(-10.5f, 5f);
Quaternion randomRotation = UnityEngine.Random.rotation;
```

How is [UnityEngine.Random](https://docs.unity3d.com/ScriptReference/Random.html) different from System.Random?

In addition to providing APIs which are convenient for games (such as .rotation), the UnityEngine.Random is accessed statically while the System.Random requires you to create an object first.

Since the Unity random class has the same name as the System random class, I try to consistently use the fully qualified name like this:

```csharp
UnityEngine.Random.Range(-1f, 1f);
```

The reason for this is if you have 'using System' in the file, the compile may throw an error.  For example:

```csharp
using System;
using UnityEngine;

public class ExampleClass : MonoBehaviour
{
  protected void Start()
  {
    // This line is a compile error
    float randomNumber = Random.Range(-1f, 1f); 

    // This line works correctly
    float randomNumber = UnityEngine.Random.Range(-1f, 1f);
  }
}
```

</details>
<details><summary>What does Debug.Assert do?</summary>

Debug.Assert is a used to confirm an assumption your code is making.  If the assumption does not hold (i.e. if the contents of the Debug.Assert evaluate to false), then the assert fails and an error is presented in the Unity console for you to investigate.

```csharp
Debug.Assert(confirmThisIsTrue);
```

You can optionally include a message to be displayed when the assert fails.  e.g.:

```csharp
Debug.Assert(confirmThisIsTrue, "confirmThisIsTrue must be true");
```

Debug.Assert is there to help identify problems sooner.  If the assert fails it does not prevent other code from being executed - however you can select 'Error Pause' in the 'Console' to better see what is happening at that moment.

Debug.Assert does not execute in release / the built version of your game.  In other words there is no performance impact to your final game by including these checks.

TODO pre conditions and post conditions

</details>

## 1.29) Assign an enemy layer

Create a layer for Enemy and assign it to the Spike Ball prefab.

<details><summary>How</summary>

 - Menu Edit -> Project Settings -> Tags and Layers.
 - Under 'Layers' add "Enemy" to one of the empty 'User Layer' slots.

<img src="http://i.imgur.com/spZG3NZ.png" width=300px />

 - Select the 'Spike Ball' prefab under Assets/Prefabs.
 - In the Inspector, click the dropdown next to 'Layer' in the top right and select 'Enemy'.
   - Select 'No, this object only' when prompted.

<img src="http://i.imgur.com/KPvq22a.png" width=300px />

<hr></details><br>
<details><summary>TODO</summary>

TODO
why this object only - best practice as sometimes children are different.

<hr></details>


## 1.30) Disable collisions between enemies

Update the collision matrix, disabling enemy to enemy collisions.

<details><summary>How</summary>

 - Edit -> Project Settings -> Physics 2D.
 - Under the 'Layer Collision Matrix', uncheck the box where 'Enemy' meets 'Enemy'.

<img src="http://i.imgur.com/JkjXpZN.png" width=300px />

</details><br>
<details><summary>TODO</summary>

TODO
 to allow enemies to travel through other enemies in the world.

<hr></details>
<details><summary>What's a Layer and how's it different from a Tag?</summary>

A layer is a number representing a category or type of object in your game which may be compared to a LayerMask.  The Unity editor allows you to associate a string with this value as well for convienence.  Layers can be used to effeciently include or exclude objects based off of their type.  For this reason, the physics matrix in Unity works with layers.

To determine if a layer is included with in a LayerMask, you can do it like the following example.  Comparing to a LayerMask uses 'bit shifting' and a 'bitwise and' which are not intuitive.  Later in the tutorial we'll create an extension method so we don't have to look at this ever again.

```csharp
using UnityEngine;

public class MyComponent : MonoBehaviour
{
  protected void Start()
  {
    LayerMask mask = LayerMask.GetMask(new[] { "Water", "UI" });
    if((mask.value & 1 << gameObject.layer) > 0)
    {
      // This gameObject is included in the LayerMask
    } 
    else
    {
      // This gameObject is NOT in the LayerMask
    }
  } 
}
```

A tag is also a way of categorizing objects, but by string.  It's useful for more targeted use cases, such as identifying the MainCamera and the Player.  

To check the tag, use CompareTag as shown here:

```csharp
using UnityEngine;

public class MyComponent : MonoBehaviour
{
  protected void Start()
  {
    if(gameObject.CompareTag("Player"))
    {
      // This gameObject is a Player
    }
    else
    {
      // This gameObject is NOT a Player
    }
  }
}
```

Every GameObject has both one layer and one tag.

</details>
<details><summary>What does the collision matrix impact?</summary>

The collision matrix defines which GameObjects may collide with what other GameObjects, based off of the GameObjects' layers.

A checked box indicates that collisions are supported.  Uncheck to disable collisions between those layers.  When unchecked, collisions between GameObjects with those layers are completely disabled - allowing objects to pass through each other as if the other didn't exist.  

Every possible combination of layers is exposed as a checkbox in settings, including a layer coming in contact with itself.  Remember that layers are defining a category or object type, so by disabling the 'Enemy' layer from coming in contact with itself - we are preventing one ball from colliding with another in the world while still allowing them to roll over platforms.

</details>


## 1.31) Test!

That's it for chapter 1!  Your game should now look a lot like the gif at the top.  You can compare to our  [demo build](https://hardlydifficult.com/PlatformerTutorialPart1/index.html) and review the [Unity Project / Source Code for Chapter 1](https://github.com/hardlydifficult/Unity2DPlatformerTutorial/tree/Part1). 


<details><summary>To review...</summary>

To review, you may want to:
 - Try adjusting the variables in Spawner to get a reasonable flow of enemies.
 - Try adjusting the initial velocity values for the spike ball.
   - Consider adding randomness to these values as well.
 - Try adjusting the bumper position angles so balls return to the screen promptly / smoothly. 
 - Try adjusting the size of colliders, ensure that objects appear to be touching the ground reasonably.
 - Cut a test build and try it outside of the Unity editor environment.

<hr></details><br>
<details><summary>Testing / Debugging tips</summary>

TODO add something about changing values in run mode vs save.

TODO testing - increase the time scale while in play mode.

<hr></details>

# Next chapter

[Chapter 2](https://github.com/hardlydifficult/Platformer/blob/master/Chapter2.md).