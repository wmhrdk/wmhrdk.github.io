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

The problem arises from the fact that in order to produce greater shooting power, the
actuator needs a greater energy which in this mechanism is stored within a *Capacitor Bank*.
This *Capacitor Bank* is often times made of smaller capacitor put together in series in
order for it to store greater energy in form of electric potential difference (Voltage).
Usually these *Capacitor Bank* needs to store around 400V to produce enough power for
shooting the ball, but most of the robots equipped only with 12-24V batteries.

So the problem is quite clear, how do we get 400V stored in a *Capacitor Bank* from 12-24V
batteries in a short time window. In order to tackle the problem, I've designed a prototype that could potentially resolve
the issue. 

### Overall Design
This design consists of three main parts which are a **DC to DC Step Up
Converter**, a **Trigger Circuit** and a **Discharge Circuit**. The discharge circuit is
included so that when the battery power goes out, the *Capacitor Bank* could be safely
discharged through the circuit.

![block-diagram](/assets/solenoid_kicker/diag_solenoid_kicker.drawio.png "Diagram")
_Overall System Diagram_

There are quite a lot to cover from this design so I'm not going into great details about
the design choices I made but instead focus mainly on the idea behind every parts of the
design.

### Solenoid Design
We start with the solenoid. The solenoids that are available on the market are usually
small and not suitable for the kind of stroking power that we need. So I designed a
custom solenoid that will fit in most robots but still has big stroking power to shoot
a ball with 400 grams of weight.

![solenoid-design](/assets/solenoid_kicker/solenoid_design.png "Solenoid Design")
_Solenoid Design_

The wire used in this design needs to be able to withstand a huge amount of electric current 
so copper wire with bigger diameter is required. Other design consideration is quite 
complicated for this solenoid so for me to go into details would make this post too long 
—although I might feature this in a future post. So to make things simple, below is the 
specification of the solenoid.

| Specifications  | Value     |
|-----------------|-----------|
| Wire size       | 18 AWG    |
| Wire length     | 345.2 m   |
| Turns           | 2680      |
| Inner diameter  | 22 mm     |
| Wire resistance | 7.516 Ω   |
| Inductance      | 95.698 mH |

### Step Up DC Voltage Converter
There are many ways one can convert DC voltage. But for this application, I choose to use 
a Mazzilli's Flyback Driver because of it's efficiency and ability to deliver huge amount 
of power.

![flyback-driver](/assets/solenoid_kicker/flyback_driver.png "Mazzilli's Flyback Driver")
_Mazzilli's Flyback Driver_

The two MOSFETs I used in this circuit are IRFP250. I chose this type of MOSFET because of
it's high *Drain-Source* current rating. Meanwhile, the transformator in this circuit is
made of *E* ferrite core with winding ratio of 7+7:224.

### Trigger Circuit
The trigger circuit is kind of a no brainer. All I need is just an output interface that 
can withstand a huge amount of current in a fraction of a second. I've seen some design 
use an SCR for this purpose but I decided to go with a IGBT for simplicity.

![trigger-circuit](/assets/solenoid_kicker/trigger_circuit.png "Trigger Circuit")
_Trigger Circuit_

### Discharge Circuit
When designing electronics, safety should be one of the most important considerations 
especially when we are dealing with high voltages. One of the potential risks in this 
design is unexpected human errors. When testing the actuator, often times human tester
forget to safely discharge the *Capacitor Bank* —Which even if they do remember they do it
in a very risky way. The voltage that remains in the capacitor might cause some serious 
harm in the future for the people who is unaware of the potential damage.

For that, I embedded a safety discharge circuit that would turn on when the battery power
goes out. It just need some simple electronics magic with transistors.

![discharge-circuit](/assets/solenoid_kicker/discharge_circuit.png "Discharge Circuit")
_Discharge Circuit_

### Final PCB Design
All the schematic capture and the board layout design for the electronic parts of this 
project is done using KiCAD. And finally, after a few weeks of designing, I came up with 
the following result.

![board-view](/assets/solenoid_kicker/solenoid_kicker_board.png "Board 3D View")
_Board 3D View_

