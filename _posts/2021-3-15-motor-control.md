---
layout: post
title: PID based Feedback Control of DC Motor
image: img/motor/step.gif
tags: [C, DC Motor, SPI, UART, Mechatronics, Feedback Control]
author: dk
---

One of the fundamental aspects of robotics is motor control. This project uses the PIC32MX250F128B microcontroller mounted on board the NU32 board and MATLAB based GUI for desired angle for the motor. 

# HARDWARE
- Brushed DC motor 
- Motor encoder
- NU32 microcontroller board
- Quadrature encoder counter
- MAX9918 current-sense amplifier
- DRV8835 H-bridge
- 6V battery pack
- Resistors and capacitors



# SOFTWARE

The controller uses two feedback loops: 
- inner high-frequency 5kHz current controller that controls the PWM output to the motor 
- outer low-frequency 200Hz position controller that controls the motor

<div class="post-flex-display">
    <img src="/img/motor/diagram.png" alt="diagram">
</div>


## CURRENT CONTROL

The output torque of the motor is drectly proportional to the current. Therefore we change the amount of current into the motor and control the torque and speed ofthe motor. This process can be done by seeing the duty cycle of a PWM signal corresponds to the desired torque. The MAX9918 current-sense amplifier is used to read the current at any given moment - specifically, it reads the current at 5kHz for the control loop, and a PI controller is implemented to set the right duty cycle.

<div class="post-flex-display">
    <img src="/img/motor/diagram.png" alt="diagram">
</div>
(*Performance of the current control*)


## POSITION CONTROL

A PID controller is used for position control. It uses encoder information to determine how far the motor is from its desired postion and calculates the required current needed to bring the motor to that position.



<div class="post-flex-display">
    <img src="/img/motor/step.gif" alt="stepf">
</div>
(*Step Trajectory*)


<div class="post-flex-display">
    <img src="/img/motor/step.png" alt="step">
</div>
(*Performance of the position control for a step trajectory*)



<div class="post-flex-display">
    <img src="/img/motor/cubic.gif" alt="cubicf">
</div>
(*Cubic Trajectory*)


<div class="post-flex-display">
    <img src="/img/motor/cubic.png" alt="cubic">
</div>
(*Performance of the position control for a cubic trajectory*)



<div class="post-flex-display">
    <img src="/img/motor/comeback.gif" alt="cb">
</div>
(*Feedback Control Bring the Motor Back to the Desired Position*)