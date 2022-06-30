---
title: "Small Game Project - Daedalus' Maze"
author: "Fredrik Lind"
date: 2019-03-22
type: post
draft: false
---
<div style="background-color: rgba(10, 10, 10, 0.8); width:100%; height:100%; padding-top:10px;">

<div id="container">
  <iframe id="video" width="1280" height="720" src="https://www.youtube.com/embed/rK4MIVfmG8w?autoplay=1&mute=1" title="Preview" frameborder="0" allowfullscreen></iframe>
</div>

## Introduction
This is the first game that I ever made and I worked together with four other students for the course "Small Game Project" at Blekinge Institute of Technology. 
The project went on from January 2019 until late March 2019. 
We all worked together in a room where we had ours desks placed together as a group.
We followed the Agile Scrum methodology where we had meetings every morning and sprints to follow.
Our sprints lasted for two weeks each.

## About the game
The game was made with C++ with our own built OpenGL engine.
The game is a horror where you are placed in a randomly generated labyrinth and have to find three buttons to press before you can escape.
But you need to be careful, because there is a Minotaur walking along the halls.
You start with some coins which you can throw to lure him in another direction.

## My contribution
I programmed the particles for the torch, tessellation on the walls, the collisions between coins and walls so that the coins would bounce whenever they hit the walls, and the randomized placement of props.

## Fun fact
A south korean Youtuber which seems to play smaller indie games found and played our game.
The game has therefore been seen by more than 100k people. 
* Here is the link to his Youtube channel: [김왼팔](https://youtu.be/G0b1Zi4N9lg)

## <em>[Click here to download the game](https://gamejolt.com/games/daedalusmaze/404262)</em>

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