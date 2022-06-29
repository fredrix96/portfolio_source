---
title: "Large Game Project - Hell Loop"
date: 2021-01-17
type: post
draft: false
---
<div style="background-color: rgba(10, 10, 10, 0.8); width:100%; height:100%; padding-top:10px;">

<div id="container">
  <iframe id="video" width="1280" height="720" src="https://www.youtube.com/embed/EPoPFmjj784?autoplay=1&mute=1" title="Preview" frameborder="0" allowfullscreen></iframe>
</div>

## Introduction
I made this game together with 10 other students for the course "Large Game Project" at Blekinge Institute of Technology.
The project went on from August 2020 until January 2021. 
We all worked from home through the program "Discord" thanks to the Covid pandemic. 
We followed the Agile Scrum methodology where we had meetings every morning and sprints to follow.
Our sprints lasted for two weeks each.

## About the game
The game was made with C++ with our own built DirectX 12 engine.
The game is a "Roguelike" where you have to surive as many rounds on the arena as possible.
After each round, you travel to a shop where you can upgrade your abilities.
The rounds get more and more difficult the further you progress.

## My contribution
The technical parts that I created and worked on are the engine's "text and font system" and its "grid system".
Simply put, the engine's graphical user interface (GUI) system for 2D elements. 
I have also worked with the game's screen size and resolution via DirectX 12s
swapchain, created some textures for the GUI system, implemented the aim and crosshair, designed the
different rooms in the game, edited the background music plus ambient sounds, and added the ability to
change the brightness of the game via the game's settings.

### The GUI system
The GUI system was the biggest technique that I contributed with. 
The GUI system processes 2D elements, such as quads (see Figure 1), and texts (see Figure 2). 
These are then drawn directly on the screen via "normalized device coordinates" NDC and therefore does not use any world coordinates.
Both the texts and the boxes can be updated dynamically by changing its colors, sizes, positions and transparency. 
The texts can have different fonts and can also be changed to new texts at runtime, 
while the boxes can be selected, have their own textures and can send various calls leading to certain events in the game.
These calls are made via the engine's event system and via function calls.

<br />

<div align="center" >
  <img class="figure" src="../resources/quads.jpg" width="480" title="Figure 1">
  <div class="figText" style="width:480px">
    Figur 1: A quad on the screen. It consists of two triangles which can be seen on the left side of the figure. The quads can have a color and a texture, seen on the right side.
  </div>
</div>

<br />

<div align="center" >
  <img class="figure" src="../resources/text.jpg" width="480" title="Figure 2">
  <div class="figText" style="width:480px">
    Figur 2: Texts consist of one quad per character. The quads can be seen in the upper part of the figure, while the text (result) can be seen in the lower part.
  </div>
</div>

<br />

The GUI system is visible throughout the whole game.
The system is needed so that the user can navigate menus and get the information about what is going on in the game, such as how many enemies the user has defeated, how much life the user has left, how much time has passed in certain rounds and get information about what the various upgrades in the store do.

#### Textures in the GUI system
Since I have some experience in the program "Photoshop", I took on the task of creating many of the textures in the game via that tool,
such as the player's health, crosshair, particles when the player and enemies shoot, the menu background, the number of dead enemies, the money icon and the wooden backgrounds for the store and the menu for purchased upgrades.

### Windowed fullscreen VS true fullscreen
You could already change the screen size in the engine before I sat down on this task. 
But the plan was to expand the system so that the user could change the screen sizes in the game settings if he/she wanted to play the game in a smaller window with lower resolution, windowed fullscreen, with different resolutions or in true fullscreen. 
It took a lot of work to finish that system, however, even though all of the problems with true fullscreen were solved, such as being able to press the button combinations "alt-tab" and "alt-enter" without having the game crash, the true fullscreen was sadly not included in the finished product.
This was because the game's gamma seemed to change as soon as someone tried to change the game's screen mode to true fullscreen while the game was running. 

<br />

I asked DirectX's official Discord channel why the gamma did not work as it should in true fullscreen mode.
One from the Microsoft team responded and was surprised that the problem still persisted when she thought it had disappeared in DirectX 12. 
She said that she would consult with the people working in that field, but she unfortunately never returned with an answer.
But since windowed fullscreen mode is enough to get a similar gaming experience, it was not considered necessary to
spend too much time continuing to ask her questions or spend more time fixing the problem myself. 
So with that we skipped true fullscreen mode. 
Note that Microsoft changed how true fullscreen mode works between DirectX 11 and DirectX 12.

### Room creation
In this task I got the chance to get more familiar with the tool modelling tool "Blender". 
I found free 3D models online, mostly via the website "SketchFab".
The free models usually have licenses which allows you to freely share and use the models as long as you mention the creators in your project, so-called
"Creative Common Attribution" licenses. 
I then opened these models in Blender where I added their material properties and textures, corrected / added / removed vertices and ensured that the UV mapping was correctly adjusted and if the UVs needed to repeat so that the textures would not look stretched in the game.
Then I exported them as OBJ files and gave them the correct positions in the game through text files with the file extensions ".map".
A map file has all of the room's different 3D objects and their properties. 
To have an entire room declared in one text-file made it easier for our procedural generation to load randomly selected rooms and place them side by side through
randomly selected positions (see Figure 3).

<br />

<div align="center" >
  <img class="figure" src="../resources/rum.jpg" width="480" title="Figure 3">
  <div class="figText" style="width:480px">
    Figur 3: This figure shows two different procedural generated levels. Every hexagon in the levels is a room. A room is loaded through a .map-file which contains all of the associated objects and their properties.
  </div>
</div>

<br />

### Crosshair
Some adjustments had to be made to get the projectiles to go where the player is aiming, due to the fact that the player's projectile starts in front of the game character and that the game is in a third-person perspective, which means that the crosshair is in the middle of the screen. 
This was done by first sending a ray from the center of the screen towards the game world with a search distance of the length of the projectile's "time to live", which is the time the projectile has before getting removed.
If the ray hits something within the search distance, the projectile's firing direction changes towards that point. 
Otherwise it goes in the direction of the point where the ray ended (see Figure 4). 
This makes it possible to hit enemies' heads even though they are very close to the player character.
This can sometimes, however, cause problems when bodies still remain on the ground, because they will thereby be covering the aim when the player is trying to aim for the enemies behind these bodies.

<br />

<div align="center" >
  <img class="figure" src="../resources/sikte.jpg" width="480" title="Figure 4">
  <div class="figText" style="width:480px">
    Figur 4: The solid line represents the ray from the crosshair while the other line represents the projectile's direction. In the top case, the ray of the crosshair does not hit anything. The projectile will then go towards the end point of that ray. In the lowest case, the ray of the crosshair hits an enemy. The projectile will then move towards that point where the ray collided with the enemy.
  </div>
</div>

<br />

### Background music and ambient sounds
These two sounds were found on the page "Freesound" where the sounds are free to use as long as you mention the page somewhere in the project. 
Ambient sounds, are sounds that removes the silence and gives the player a greater feeling of being in a certain place. 
Both the background music and the ambient sounds needed to be restarted once they run out. 
To fix this, the music tool "FL Studio" was used, which I am pretty used to.
I have been using FL Studio for my music projects which can be found on my Soundcloud page.
The tool called "Audacity" was then used to shorten the background music and the ambient sounds and finish them in a way that makes the looping of the sounds more natural.
The game's sound engine takes care of the looping.
The sound engine is a part of our DirectX 12 engine.

### Game brightness
We noticed that the brightness of the game varied a lot depending on which computer or screen the user played on.
So I added a variable that the player can change in the game settings. 
This variable is sent to the engine's "Forward Pixel Shader", which controls the majority of the colors in the game, and is then multiplied with its output value.
This simple trick gave a surpisingly effective result (see Figure 5).

<br />

<div align="center" >
  <img class="figure" src="../resources/ljusstyrka.jpg" width="480" title="Figure 5">
  <div class="figText" style="width:480px">
    Figur 5: The figure shows three different levels of brightness. The left one is when playing with the preset "1". The middle one is the preset "2" and the one on the far right is preset "5", which is also the game's highest brightness. The lowest preset the game can have is "0". The result varies depending on the player's computer components and the screen the player uses.
  </div>
</div>

<br />

## My GUI system: Down the rabbit hole
The text and font system itself is built from the tutorial "Drawing text in DirectX 12" from the website "Braynzar Soft".
This page went through all the parts, tools and knowledge necessary to get a working text and font system.
The grid system is then mostly a simpler extension of the same system, but with a few extra options such as textures, "clickability" and the ability to select
the boxes with the mouse pointer.

### The structure of the system
I started by going through the tutorial on Braynzar Soft to get an idea of ​​what was needed to be done and how to proceed to get a working text and font system. 
Then I also downloaded the "Hiero tool" (see Figure 6), so that we had the opportunity to implement all the different kinds of fonts that we wanted to use in our project. 
Hiero turned out to be a good tool when we noticed that we needed fonts that contain Swedish letters such as the letters "å", "ä" and "ö", and special characters such as "é" to our list of participants, thus our credits. 
This could easily be done in the Hiero tool. 
Then I investigated our engine to get an better idea of ​​how the system could be implemented in our engine.
After that I started to implement the classes and shaders that were needed and then started filling them with necessary variables and functions. 
These classes were a font class, text class, text manager class and a text task class. 
The shaders that were created were a vertex shader and a pixel shader. 
Necessary comments were added where the code was a little harder to understand. 
In addition to this, some comments were also added to a tutorial file so that everyone in the team had the opportunity to use the Hiero tool to bring their own fonts into the system.

<br />

<div align="center" >
  <img class="figure" src="../resources/hiero.jpg" width="480" title="Figure 6">
  <div class="figText" style="width:480px">
    Figur 6: Hiero is a free tool that allows the user to create their own ".fnt" files and font images. Either through selecting existing fonts, or by uploading his/her own. This gives the user the ability to add the letters and characters needed in his/her font files.
  </div>
</div>

<br />

A little later in the project, I also added the grid system. 
This is built in a similar way to the text and font system, but is much simpler as a quad only consists of four vertices while a text consists of
one quad per letter / character, which means that it is more difficult to determine the sizes of the texts and their positioning. 
However, the grid system needed to have some other options, such as adding textures, textures which shows when a quad is selected and the ability to click with the mouse on a quad so that an event gets activated.
The grid system consists of a quad manager class, quad task class, vertex shader and a pixel shader.
Both the quad manager class and the text manager class are then linked via a GUI2DComponent class that can be given to an entity, which allows the developer to provide entities with both quads and texts via this component class.

<br />

The testing was done via a sandbox located in the project. 
Here I was able to stress test the system by changing all the different values ​​that the system recieves per iteration during the program's execution.
This was a good thing to do, because by doing so, we noticed that the system was not really optimal when the system variables had to be updated too
quickly.
This led to a lot of optimization in the system.
However, it was noticed that the result in the sandbox did not always reflect the reality, because outside of the sandbox, the system had to work together with the other team members' implementations. 
This was not only unique to the GUI system, but was noticed for many parts of the project.
This made it extra important to also run some tests in the actual game part of the engine to make sure that the new system worked well with the other parts of the engine.

<br />

The optimization was about what worked best when it comes to managing data between the CPU and the GPU. 
The first attempt was to always delete and create a new quad or text every time a value needed to be changed. 
Obviously, this was not a good solution as the GPU needed finish its work with that data that was uploaded and then waiting for the data to be deleted and then for new data to be created and resubmitted.
This was mostly done due to incomplete understanding of how the engine was built and how DirectX 12 takes care of that data. 
Thus, "constant buffers" were implemented, which made sure to send up those values that needed to be changed to the GPU. 
In addition, it was ensured that the objects created on the CPU side were not equally constant, which gave them the opportunity to be more easily modified in the vertex shader. 
The system ran much better after this optimization and made it easier for the user to handle it more smoothly.

<br />

### Advantages and disadvantages of the implementation
The advantages of the implementation are that it is easy to access all properties of the system via the entity's GUI2D component. 
This makes it possible to easily call on all its functions and have the opportunity to change its properties while the game is running, ie in a dynamic way. This means that you can put texts and quads wherever you want on the screen, change the content of the texts, colors, sizes, transparency and positioning whenever you want while the game is running, while you can also change the similar properties of the quads whenever you want during the same run. 
This simply leads to a lot of creative freedom. 
Another advantage is that the system is built in a similar way to the rest of the entity and component system in the engine, ie that you as a developer can create an entity and give it a text and a quad in the same way as you would give it any other component in the engine.

<br />

The disadvantages are that an entity is always given both a quad and a text, regardless of whether it will just use one of them. 
This does not mean that an entity must display a quad and a text at the same time, but means that both classes are created when assigning this GUI component. You also have to make long argument calls to be able to reach exactly the properties that you are looking for. 
Another disadvantage is that an entity can only have one quad.
The text system itself is built so that an entity can have many texts, but the grid system can only create one mesh, which in this case is a square. 
However, this feels more like a personal problem as it has been talked about that it might have been best for an entity to be just a quad or a text. 
How good or bad this is, is probably mostly due to how the entity and component system is built in different engines. 
Another disadvantage is that the text and font system has an array of constant buffers. 
This is because of the fact that the current implementation takes care of one letter at a time in the vertex shader and that the properties of the specific letter depend entirely on their neighbors' properties such as positioning, neighbor distance, size and of course what character it is. 
For the sake of simplicity and also for performance optimization, it would probably have been best to have only one common
constant buffer for all letters. 
A final disadvantage is that the system has no effective way of positioning boxes and texts. 
Because of the fact that quads and texts use the coordinates (0,0) to (1,1) for positioning (see Figure 7), the user can calculate where the quad ends up and how far it extends.
This, however, does not work as good for the texts as they will vary in length depending on the number of characters included in the texts. 
It would have been better to have an anchor system so that the user can specify a position for a quad or a text and then be able to expect the correct placement. 
Another way would have been to let the user be able to reposition all GUI elements by dragging them around with the mouse for better precision. 
This problem meant that the users of the system had to spend quite a lot of time positioning the elements so that they
ended up nicely.

<br />

<div align="center" >
  <img class="figure" src="../resources/koordinater.png" width="480" title="Figure 7">
  <div class="figText" style="width:480px">
    Figur 7: This square represents the coordinates of the screen. The coordinates start at the point (0,0) which is located at the top left corner of the screen and ends at the point (1,1) at the bottom right corner of the screen.
  </div>
</div>

</div>

<script>
  /* Storing user's device details in a variable*/
  let details = navigator.userAgent;

  /* Creating a regular expression
  containing some mobile devices keywords
  to search it in details string*/
  let regexp = /android|iphone|kindle|ipad/i;

  /* Using test() method to search regexp in details
  it returns boolean value*/
  let isMobileDevice = regexp.test(details);

  var figures = document.getElementsByClassName('figure');
  var figTexts = document.getElementsByClassName('figText');

  if (isMobileDevice) {
      document.getElementById('video').width = "300";
      document.getElementById('video').height = "168";

      for (var i = 0; i < figures.length; i++)
      {
        figures[i].style.width = "300px";
        figures[i].style.height = "168px";
      }

      for (var i = 0; i < figTexts.length; i++)
      {
        figTexts[i].style.width = "300px";
      }
  }
</script>