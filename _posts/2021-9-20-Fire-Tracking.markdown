---
layout: post
title: Fire & Thermal Object 3D Tracking
image: img/adroit/fire_tracking.gif
tags: [Python, Depth Sensing, Thermal Imaging, Rat, Point Cloud]
featured: true
hidden: true
author: dk
---

This is extended project from [Autonomous Fire Figihgting Robot Arm](https://dokkev.github.io/firefigther-robot/) to improve fire sensing. The previous project limited fire sensing to 2D imaging, but this project extends to localizing the fire in 3D location relative to the robot and the world frame.

You can check out the source code from the [Github Repository](https://github.com/dokkev/Fire_3D_Tracking)

### DEMO VIDEO

[![1](http://img.youtube.com/vi/ELHQRg86zm0/0.jpg)](https://www.youtube.com/watch?v=ELHQRg86zm0)


# PROJECT BACKGROUND

[Autonomous Fire Figihgting Robot Arm Project](https://dokkev.github.io/firefigther-robot/)'s thermal image processing was able to sense the heatsource and align it with robot arm, but it did not have any information where the heatsoruce is relative to the robot. Since Adroit plans its movement using Moveit, localizing the fire is crucial to the performance of an autonomous fire fighting robot. I added Depth sensing camera and combined a depth image and a thermal image to get depth from the heatsource and eventually localize its location using transformation.

# HARDWARE

FLIR Lepton 2.5 - Thermal Imaging Module
<div class="post-flex-display">
    <img src="/img/adroit/lepton.jpg" alt="lepton">
</div>


PureThermal 2 - FLIR Lepton Smart I/O Board
<div class="post-flex-display">
    <img src="/img/adroit/purethermal.jpg" alt="purethermal">
</div>

Intel RealSense Depth Camera D435 
<div class="post-flex-display">
    <img src="/img/adroit/realsense.jpg" alt="realsense">
</div>


3D Printed Cameras Mount
<div class="post-flex-display">
    <img src="/img/adroit/cammount.jpg" alt="cammount">
</div>




# Contour Detection From Thermal Image

The previous method of detecting the heat source was getting the pixel of highest value from the radiometric image. This method was rather unstable due to often bounce of target pixel. Therefore, I calculated the contour from the radiometic image and its centroid to get a target pixel of the heat source.

<div class="post-flex-display">
    <img src="/img/adroit/contour.png" alt="contour">
</div>
(*contour of a electric heater*)

<div class="post-flex-display">
    <img src="/img/adroit/fcontour.png" alt="fcontour">
</div>
(*contour of fire*)



# Combined Vision Processing

<div class="post-flex-display">
    <img src="/img/adroit/process.png" alt="process">
</div>

Getting the pixel coordinate (u,v) from the centroid of thermal image's contour, it's fed into the realsense depth camera to get depth data at (u,v).

<div class="post-flex-display">
    <img src="/img/adroit/ruler_color_image.png" alt="ruler">
</div>

<div class="post-flex-display">
    <img src="/img/adroit/combined.png" alt="combined">
</div>

The evaluate depth sensing, the result was compared to measurement with a ruler. The error range was about +-100 mm at maximum when measuring distance from 1.2 m to 0.3 m. The error got greater as the depth camera was more far away from the target object.


When it comes to combining two cameras, thermal image and depth image are deviated from each other. Therefore it's important align two cameras properly. `ropstopic` `combined_image2` provides combined images of color image and thermal image to provide how well two cameras are aligned while `combined_image` provides combined images of aligned color to depth image and thermal image. Thermal camera and realsense camera should be calibrated to avoid error due to cameras deviation.



# Testing

## Testing with Electric Heater
<div class="post-flex-display">
    <img src="/img/adroit/eh1.png" alt="heater">
</div>

<div class="post-flex-display">
    <img src="/img/adroit/eh2.png" alt="heater2">
</div>


<div class="post-flex-display">
    <img src="/img/adroit/aeh.png" alt="aheater1">
</div>

(*This moudle can be mounted on Adroit robot arm*)

<div class="post-flex-display">
    <img src="/img/adroit/aeh2.png" alt="aheater2">
</div>


## Testing with Fire

<div class="post-flex-display">
    <img src="/img/adroit/fire1.png" alt="fire1">
</div>


<div class="post-flex-display">
    <img src="/img/adroit/fire2.png" alt="fire2">
</div>


<div class="post-flex-display">
    <img src="/img/adroit/fire3.png" alt="fire3">
</div>


<div class="post-flex-display">
    <img src="/img/adroit/fire4.png" alt="fire4">
</div>


<div class="post-flex-display">
    <img src="/img/adroit/fire_color.png" alt="firecolor">
</div>


<div class="post-flex-display">
    <img src="/img/adroit/fire_comc.png" alt="firecolorc">
</div>
(*Thermal Image + Color Image*)


<div class="post-flex-display">
    <img src="/img/adroit/fire_comd.png" alt="firecolord">
</div>
(*Thermal Image + Aligned Color to Depth Image*)


## Testing with Human

Another application of this project is that we can use it keep track human too.

<div class="post-flex-display">
    <img src="/img/adroit/human.png" alt="human">
</div>


<div class="post-flex-display">
    <img src="/img/adroit/human_track.gif" alt="human2">
</div>
