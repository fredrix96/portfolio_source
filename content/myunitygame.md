---
title: "My Unity 2D Game - In Progress"
author: "Fredrik Lind"
//date: 2022-08-18
type: post
draft: false
---
<div style="background-color: rgba(10, 10, 10, 0.8); width:100%; height:100%; padding-top:10px;">

## Introduction
This is a 2D game that I am working on in Unity. 
I started this project because I wanted to be able to showcase a bigger project that I have done outside of school, on my own. 
But also because I love programming, especially programming for games.
The game was made entirely programmatically with C#.
This means that all the game objects are created on start and are not saved in the Unity Engine, which means that everything is created completely from code.
I did this as a challenge so that I could learn C# better, but also so that I could get a better understanding of the content inside the Unity engine, such as the game object system, the component system, the physics, etc. Everthing is made by me, from sprites to music.

<br />

Note that the game is in progress, so this page will be updated continously.

## About the game
The game's objective is to keep your character alive, while building your own base and gathering an army to defeat the never ending horde of enemies.
The player will build its base on the left side of the game field (see Figure 1) while the enemies will spawn on the right side (see Figure 2).
The character with a crown in the middle of Figure 1 is the player's character, called the "king".
The king can only be spawned when there exists a castle (located above the king).
When the king dies, the player has to wait until it respawns again.
However, the player will loose if the king dies without a castle.

<br />

<div align="center" >
  <img class="figure" src="../resources/gameImages/leftside.jpg" width="1080" title="Figure 1">
  <div class="figText" style="width:1080px">
    Figur 1: The player will build and manage its base on the left side of the battlefield.
  </div>
</div>

<br />

<div align="center" >
  <img class="figure" src="../resources/gameImages/rightside.jpg" width="1080" title="Figure 2">
  <div class="figText" style="width:1080px">
    Figur 2: The enemies will spawn on the right side of the battlefield.
  </div>
</div>

<br />

The player will be able to buy new building through the shop seen to the left of Figure 3 and the player's soldiers will automatically walk towards the enemies after being spawned and fight with them, also seen in Figure 3. Every killed enemy will yield coins which are used to upgrade and manage the base.

<br />

<div align="center" >
  <img class="figure" src="../resources/gameImages/shopandfighting.jpg" width="1080" title="Figure 3">
  <div class="figText" style="width:1080px">
    Figur 3: The shop can be seen to the right. The player can open it with the "E" button. The soldiers will automatically attack enemies when they are in range.
  </div>
</div>

<br />

## Code

To save some performance, the soldiers' and enemies' movements are multithreaded (see Figure 4 - 6). 
This is done by using Unity's "Job system" shown in Figure 6.
The difficult part with multithreading in Unity is that Unity's game objects can not be multithreading due to "thread-safety".
This means that the movement first has to be calculated seperately, and then being applied to the game object's position at the main thread.

<div align="center" >
  <img class="figure" src="../resources/gameImages/multithread1.jpg" width="1080" title="Figure 4">
  <div class="figText" style="width:1080px">
    Figur 4: Here we look if the program is multithreaded. If it is, then we decide on which frame the characters should search for a new path to follow (in this case every 60th frame). This is done to maximize performance and is barely noticable in game.
  </div>
</div>

<br />

<div align="center" >
  <img class="figure" src="../resources/gameImages/multithread2.jpg" width="720" title="Figure 5">
  <div class="figText" style="width:720px">
    Figur 5: Here we split all the characters in different groups (chunks). This means that not every character's movement is updated on the same frame. This makes the character movements more fluid but also less performance heavy. The "job.Schedule(...)" function calls the job system.
  </div>
</div>

<br />

<div align="center" >
  <img class="figure" src="../resources/gameImages/multithread3.jpg" width="720" title="Figure 6">
  <div class="figText" style="width:720px">
    Figur 6: This is the layout of Unity's job system. Each execution is made per thread.
  </div>
</div>

<br />

The [BurstCompile] command seen at the top of figure 6 is yet an additonal way to optimize the code. 
It is a seperate compiler which will run execute the code even faster by further optimizing the code.
However, I have not yet succeeded in implementing it because it is even more strict to use than the job system.
The burst compiler can not work with classes or Unity objects unless they are singletons.
So for me to implement it would mean that I have to rethink bigger parts of my code structure, and I am not sure if it is worth it.
I would definitely have planned for it if I knew that it existed while I started this project.

<br />

I have made general classes to make sure that I do not have too many copies of the same code.
One example is my UI manager class.
Its usecase can be seen in figure 7.
Without these type of classes, I would have to copy chunks of code like the two chunks in figure 8.

<br />

<div align="center" >
  <img class="figure" src="../resources/gameImages/UImanagerusecase.jpg" width="1080" title="Figure 7">
  <div class="figText" style="width:1080px">
    Figur 7: The UI manager makes it possible to create a UI element with just one call. These elements can be images, texts, sliders, buttons, etc.
  </div>
</div>

<br />

<div align="center" >
  <img class="figure" src="../resources/gameImages/codechunks.jpg" width="1080" title="Figure 8">
  <div class="figText" style="width:1080px">
    Figur 8: Each UI element needs a canvas which is created at the initialization of the UI manager (Init()). Then we need to create a game object and its component for each UI element (CreateImage(...)).
  </div>
</div>

<br />

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