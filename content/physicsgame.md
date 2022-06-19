---
title: "Unity 2D: Game Physics - Projectiles, Explosions and Shockwaves"
date: 2018-11-22
type: post
draft: false
---

## Introduction
This small game project was done together with another student for the course "Game Physics" during my time at Blekinge Institute of Technology.
It is built with C# in Unity 2D.

## About the project
All of Unity's physics are turned off.
That means that all of the physics that are seen in this project have been made by us.
The physics are based on real-life formulas of objects traveling through air with air resistance, the impacts and sizes of explosions and the speed and movement of their shockwaves.
Just for fun, we have added the possibility to change the gravitational force to see how the projectiles get affected if you were to shoot on another planet.
After every time the tank shoots, you can see how long time the projectile was in the air and its distance before collision with the ground. 
The mach represents the speed of the projectile, and therefore the tank's shooting power.
The number "2.89" mach was based on information we found on a real tank.
The tank takes damage depending on the power of the shockwave, that is, how close the tank is to the center of the explosion.
The power and direction of the wind is randomized each time you reset the game.

## Controls
You can zoom in and out with your mouse's scroll-wheel.
The tank drives with the A and D buttons.
The W and S buttons change the tank's power and the Q and E buttons change the angle of the turret.
The gravity and speed of time for the projectiles can be changed at the button of the screen. 
A "SlowMo Speed" of 1.00 represents a normal time for the projectile, lower than that is slow motion and higher is a speed up.
You shoot with Space button.

## Project
{{<physicsgame>}}