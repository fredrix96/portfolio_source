---
title: "Metaballs"
date: 2020-05-25
type: post
draft: false
---

<div style="background-color: rgba(10, 10, 10, 0.8); width:100%; height:100%; padding-top:10px;">

## Introduction
I made this project for the course "Game Techniques for the Web" during my time at Blekinge Institute of Technology.
It is built with javascript, css and html. 

## Metaballs
Metaballs are n-dimensional (in this case three-dimensional) isosurfaces, which are surface respresentations of points, that meld together at a chosen distance.
Metaballs can be rendered in many different ways, but I have used ray-marching, which is a technique where rays are stepping through the space, one ray per each pixel on the screen, until they register collisions and returns a color.

## How the project works
Simply put, the metaballs are generated at the start of the program in the javascript.
Here they get a position and a radius.
The metaballs are confined inside a box and bounce between its walls.
This is done to make them collide with each other and not just move away from the area indefinitely.
The metaballs information is then sent to the vertex and the fragment shaders.
The ray-marching is then done per pixel inside this fragment shader.
Here, a treshold is chosen and it tells the metaballs how close to each other they should be before melding.
If a ray steps through the radius or the treshold between two metaballs, then it registers a hit and returns the color of the metaball based on the light in the scene.
The light is stuck to the camera. 
The metaballs are basically just points that moves around on the screen. 
The ray-marching does the rest.
The colors are randomized each time you refresh this page.

## Project
{{<metaballs>}}

</div>