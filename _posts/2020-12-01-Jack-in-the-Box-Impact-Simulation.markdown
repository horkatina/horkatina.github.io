---
layout: post
title:  Impact Simulation
image:  img/impact/jackgif.gif
tags:   [Impact, Simulation, Python]
author: dk
---

This project simulates a "jack" which is made of a 4 point masses inside the square box in a 2D plane. The box is subjected to external forces which will allow jack to experience impacts. This project was done in Jupyter notebook and source codes can be found in my [github repository](https://github.com/rubberdk/jack-in-the-box)

# Results

<div class="post-flex-display">
    <img src="/img/impact/jackgif.gif" alt="jackbox">
</div>

<div class="post-flex-display">
    <img src="/img/impact/plot.png" alt="plot">
</div>

# Simulation Setup

## Transformation
<div class="post-flex-display">
    <img src="/img/impact/draw.png" alt="tf">
</div>

Vertexes of the bot were represented as {A}, {B}, {C}, and {D} while the edges of it were done as {1}, {2}, {3}, and {4}. Four point masses of jack were shown as {a}, {b}, {c}, and {d} while the World frame is shown as {W}.

## Configuration
<div class="post-flex-display">
    <img src="/img/impact/config.png" alt="config">
</div>
Both the box and jack are free to translate and rotate in a xy-plane

## LAGRANGIAN

<div class="post-flex-display">
    <img src="/img/impact/v1v2.png" alt="v1v2">
</div>

<div class="post-flex-display">
    <img src="/img/impact/velocity.png" alt="velocity">
</div>

<div class="post-flex-display">
    <img src="/img/impact/pe.png" alt="pe">
</div>

<div class="post-flex-display">
    <img src="/img/impact/ke.png" alt="ke">
</div>

<div class="post-flex-display">
    <img src="/img/impact/L.png" alt="L">
</div>

## External Force

<div class="post-flex-display">
    <img src="/img/impact/F.png" alt="F">
</div>

<div class="post-flex-display">
    <img src="/img/impact/Fext.png" alt="Fext">
</div>

External force was applied assuming someone is shaking the box.

To ensure that jack hit all four edges of the box, the external force was applied in x-direction since gravitational force will take y-direction to make sure jack hit the all four edges of the box.

## Constraint
<div class="post-flex-display">
    <img src="/img/impact/qlist.png" alt="qlist">
</div>

<div class="post-flex-display">
    <img src="/img/impact/qfor.png" alt="qfor">
</div>

The jack has the constraint that it has to stay within the boundaries of the box.

Phi defines when the point masses of the jack make contacts with the boundaries of the box which are {1}, {2}, {3}, and {4}. There are multiple phi called phi_list in this system, and they are called in a for-loop so that it eliminates the necessity of making multiple impact update functions.

Phi can be expressed with g matrix while g_ij [3] represents x-component and g_ij [7] does y-component.

## Euler-Lagrangian
<div class="post-flex-display">
    <img src="/img/impact/EL.png" alt="EL">
</div>

## Impact Update Law
<div class="post-flex-display">
    <img src="/img/impact/qpm.png" alt="qpm">
</div>

<div class="post-flex-display">
    <img src="/img/impact/ham.png" alt="ham">
</div>

<div class="post-flex-display">
    <img src="/img/impact/eq.png" alt="eq">
</div>

Function ‘impact_condition’ takes phi_list and initial conditions which includes initial positions and velocities, lambdifies phi values, and tolerance to decide the impact condition.

Function ‘impact_update takes initial conditions and impact equations to numerically update impacts