---
title: "Large Game Project - Hell Loop"
date: 2021-01-17
type: post
draft: false
---

## Preview
{{<hellloop>}}

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
The technical parts that I have been involved in and worked on are the engine's "text and font system" and its "grid system".
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
  <img src="../resources/quads.jpg" width="480" title="Figure 1">
  <div style="width:480px">
    Figur 1: A quad on the screen. It consists of two triangles which can be seen on the left side of the figure. The quads can have a color and a texture, seen on the right side.
  </div>
</div>

<br />

<div align="center" >
  <img src="../resources/text.jpg" width="480" title="Figure 2">
  <div style="width:480px">
    Figur 2: Texts consist of one quad per character. The quads can be seen in the upper part of the figure, while the text (result) can be seen in the lower part.
  </div>
</div>

<br />

The GUI system is visible throughout the whole game.
The system is needed so that the user can navigate menus and get the information about what is going on in the game, such as how many enemies the user has defeated,
how much life the user has left, how much time has passed in certain rounds and get information about what the various upgrades in the store do.
