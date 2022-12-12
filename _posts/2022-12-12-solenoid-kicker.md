---
title: Magnetic Based Kicker Design for Indonesian Robotics Contest
date: 2022-12-12 12:27:00 +0800
categories: [Electronics]
tags: [electronics, hardware, actuator]
---

The magnetic based kicking mechanism in the **Indonesian Robotics Contest** (**KRI**) has 
been around for years. It provides greater shooting power, less weight, and less space
requirement for implementation than any other mechanism. But this mechanism is not without
disadvantage. To mention one of them, is the time that is required for the actuator to get
ready to shoot.

The problem arises fromm the fact that in order to produce greater shooting power, the
actuator needs a greater energy which in this mechanism is stored within a *Capacitor Bank*.
This *Capacitor Bank* is often times made of smaller capacitor put together in series in
order for it to store greater energy in form of electric potential difference (Voltage).
Usually these *Capacitor Bank* needs to store around 400V to produce enough power for
shooting the ball, but most of the robots equipped only with 12-24V batteries. So the
problem is quite clear, how do we get 400V stored in a *Capacitor Bank* from 12-24V
batteries in a short time window.

In order to tackle the problem, I've designed a prototype that potentially could resolved
the issue. This design consists of three main parts which are a **DC to DC Step Up
Converter**, a **Trigger Circuit** and a **Discharge Circuit**. The discharge circuit is
included so that when the battery power goes out, the *Capacitor Bank* could be safely
discharged through the circuit.

![Block Diagram](https://imgbox.com/rQwF3ToI)

