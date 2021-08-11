---
layout: post
title: Digital Rat Exploration with Active Vibrissal Sensing
image: img/rat_nav.gif
tags: [C++, BulletPhysics, Whikser, Rat, Simulation]
featured: true
hidden: true
author: dk
---

This is my Final Project for Master of Science in Robotics program at Northwestern University.
This is still on-going project which will be finihsed in December 2021. This post includes the progress up to June 2021.
You can check my [github repository](https://github.com/rubberdk/whisker_project) for codes


# Introduction
Rats use whiskers to navigate thorugh holes and find open space, As they scan, their whiskers make unexpected contact with an object, and the rat then explores the object to extract the details of its shape. The use of whisker inputs to detect, localize, and extract the spatial properties of objects. With these unique traits, whiksers allow rats to operate in complete darkness<sup>1</sup>. This project aims simulating digital rat's whisking over different shapes of objects, understanding the dynamtic data whiskers sense, and finally implementing a digital rat's whisker-based expoloration algorithm in a simulated world with obstacles.

This project untilized [WHISKiT Physics Simulator](https://github.com/SeNSE-lab/whiskitphysics) is a 3D dynamical model of the full rat vibrissal array using the open-source physics engine Bullet Physics and OpenGL. It allows to simulate the sensory input of the vibrissal system, i.e. the mechanical signals (moment and force) generated at the base of each whisker in the array. Based on WHISKiT Physics Simulator, I modified the source codes to integrate three following features:

1) customizable transformation of objects in the simulation world
2) parallel simulation using Northwestern's high performance computing cluster [Quest](https://www.it.northwestern.edu/research/user-services/quest/)
3) user-controllable digital rat in the simulation

# Virbrissal Sensing over Objects
Objects in the simulation take Buttelt Physics' transformation data as their parameters. This simulation take different 'OBJECT' parameters.

<div class="post-flex-display">
    <img src="/img/rat/object3.png" alt="object3">
</div>

Setting the 'OBJECT' parameter to 3 creates the object in the origin of the simulation.

<div class="post-flex-display">
    <img src="/img/rat/object4.png" alt="object4">
</div>

Setting the 'OBJECT' parameter to 4 creates the object in the user-specified using cartesian coordinates and 4D quaternion (x,y,z,w)

<div class="post-flex-display">
    <img src="/img/rat/object5.png" alt="object5">
</div>

Setting the 'OBJECT' parameter to 5 creates the object in the user-specified using cartesian coordinates and 3D quaternion (yaw,pitch,roll)

<div class="post-flex-display">
    <img src="/img/rat/shell.png" alt="shell">
</div>

While this simulation operates in C++, changing an object or its parameters such as size, position, and orientation in the codes would have required re-compiling. However, using shell scripts to define those parameters eliminates the hassle of re-compiling. Example shell script is shown above with brief explanaiton. You can see more detail about the parameters in the [main_opengl.cpp](https://github.com/rubberdk/whisker_project/blob/master/code/src/main_opengl.cpp).

<div class="post-flex-display">
    <img src="/img/rat/xyz.png" alt="xyz">
</div>
*object in the simulation*

<div class="post-flex-display">
    <img src="/img/rat/whisk.gif" alt="whisk">
</div>
*Active whisking over a pinecone*


# Parallel Simulation Over 97 different Objects
Simulating over multiple sets of objects with active vibrissial sensing is time consuming. Therefore, I utilized Northwestern University's [Quest](https://www.it.northwestern.edu/research/user-services/quest/) for the parallel simulation over 97 objects. The 97 objects include scans of natural objects such as rocks, tree branches, leaves, and fruits. Each object was simulated 10 times with smalll variation of their position and orientation. `TIME_STOP` parameter was set to 1.0 with `TIME_STOP` as 0.001. As a result, force and moment data of right side whiskers were obtained.

Due to the lack of `sudo` access in Quest server, this part of the project is separated from the `master` branch to eliminate unecessary libraries for obtaining the simulation result. You can find the codes for parallel simulation in [questsim](https://github.com/rubberdk/whisker_project/tree/questsim) branch

# User-Controllable Digital Rat Interface
To control the digital rat's position and orientation with user input during the simulation, communication between the simulation codes and control codes were setup using `msgpack`. The control codes allow user to control the digital rat using keyboard and visually represent real-time the data that the rat obtains with vibrassial sensing.

<div class="post-flex-display">
    <img src="/img/rat/graph.gif" alt="graph">
</div>
*real-time force and moment data*


# Future Plans
The final goal of this project is to allow a digital rat to autobomoulsy explore and navigate a simulation world filled with obstacles. Based on the data that whiskers obtain, I can implement force control for the digital rat. The current problem is that activating all whiskers slow down the simulation. With activation of all whiskers, whisking over an object for 4 seconds in simulation time take about 20 minutes in real time. I am considering using Unity Engine or Unreal Engine to finish the autonomous exploration part.



## References
[1] Hartmann MJ. A night in the life of a rat: vibrissal mechanics and tactile exploration. Ann N Y Acad Sci. 2011 Apr;1225:110-8. doi: 10.1111/j.1749-6632.2011.06007.x. PMID: 21534998.