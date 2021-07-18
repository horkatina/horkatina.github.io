---
layout: post
title:  Lava Java
image:  img/lj/demo.gif
tags:   [Arduino, Thermal Sensing, Prototyping]
author: dk
---

Lava Java is an Arduino based project that sought out a way to display the temperature of a hot beverage to a user through the color of a RGB LED. The goal is for the user to have the general knowledge of the temperature of their beverage, so they can make decisions on when to drink. Fading of the temperature ranges strives to give the user even more knowledge of what temperature their coffee is at.

# Prototype Demo

[![Watch the video](https://img.youtube.com/vi/5qaFL9PA8Cg/0.jpg)](https://youtu.be/5qaFL9PA8Cg)

This is a time lapse video can be found of Lava Java working. In the video Lava Java goes from the red temperature range and fades to green and fades through to blue. Starbucks was closing or else we would have waited until the coffee got below 99 degrees which would have turned the LED off.

# Codes

<div class="post-flex-display">
    <img src="/img/lj/code.png" alt="code">
</div>
<div class="post-flex-display">
    <img src="/img/lj/code2.png" alt="code2">
</div>

The Adafruit_MLX90614 temperature sensor came with a code that displayed the temperature. We integrated this into our code so that our if functions displayed a certain color for a set temperature range. Within the if functions the map functions are used so that the RGB LED fades from bright to dim within the given temperature ranges. A switch was integrated as usual to stop the device from functioning when flipped.

# Circuits

<div class="post-flex-display">
    <img src="/img/lj/circuit.png" alt="circuit">
</div>
<div class="post-flex-display">
    <img src="/img/lj/circuit2.png" alt="circuit2">
</div>

# 3D Modeling

<div class="post-flex-display">
    <img src="/img/lj/m1.png" alt="m1">
</div>
<div class="post-flex-display">
    <img src="/img/lj/m2.png" alt="m2">
</div>

The CAD model is essentially a recreation of the plastic casing we originally used for the prototype presented. However the case was lengthened by 3/10 ths of an inch in order to improve some internal spacing issues of the components. Further, aluminum was used instead of plastic in order to increase strength of the case since the object is something intended to be carried around in a bag where it will be banging into other items. Another improvement made was that instead of having a hinge that sticks out, a pin-and-hole system was added in its place to lock the top and bottom together, allowing for smooth walls on all sides. The dimensions were: length 5 inches, width 3.3 inches, height 2 inches, and thickness 1/10th of an inch.

# Thermal Analysis

<div class="post-flex-display">
    <img src="/img/lj/thermal.png" alt="thermal">
</div>

For the thermal analysis, a heat source of around 130 degrees Fahrenheit was applied to the surface where the coffee would sit. 130 was chosen because that was what we determined was the “ideal” temperature for coffee and therefore the temperature at which the coffee would sit at the longest if possible. The heat sink was then added on the opposite side since that's the only other surface that would be contacting the case at a lower temperature. Heat loss due to air convection were purposefully excluded from this analysis, however would be included should further analysis be conducted. As can be seen from the results though, while the surface near the source is very hot, the heat flux through the case is marginal and quickly dissipates to room temperature by the time it is half way down the sides of the case.