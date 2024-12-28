<td><a href="https://m.youtube.com/watch?v=L1u6AkSpR98&t=2s" title="Youtube" rel="noopener"><img src="https://i.imgur.com/eEX1qmB.png"></a></td>

Welcome to openpilot 0.7.1_OC_WATER💧 Comma 3X Mercedes Benz SLK 200 r170 year 1997 and later customization project
======

💵 💴 FINANCIAL BUDGET 💶 DUE DILLIGENCE 💷 💳
======
I do hope to cover all possible functions with Comma 3X. At first we will try to focus on financial budget and time schedule estimates, because we assume this side as project is also relevant and many owners will consider return of investments. Obviously many will consider if investing ammount of money which attacks price of the vehicle is worth it with current market prices, if it is better to wait for price drop and development, or if get newer car with no or very little customization needed is better option.

| Product part				|	Estimated price	|
|---------------------------------------|-----------------------|
| Comma 3X				|	1150 USD	|
| Comma 3X Harness			|	  99 USD	|
| Electric power steering unit (EPS)	|	 500 USD	|
| Steering angle sensor			|	   ? USD	|
| Electronic brake booster aka ibooster	|	 500 USD	|
| Throttle control			|	   ? USD	|
| Radar sensor				|	   ? USD	|
| Custom welding			|	 300 USD	|
| Custom wiring				|	 300 USD	|
|---------------------------------------|-----------------------|
|Total					|			|


🕐🕢⌚ PLANNING 🕰️ AND ⏲️ TIME SCHEDULE ⏰⏳⌛📅📆🗓️ 
======
If we have reached this section, we have the budget agreement and now we are curious about how long this construction party can last. How fast we can get all parts together, how long time take the manual work itself, what kinds of expertise we are going to need and how long we are going to check the result.

🕺 INTRODUCTION 🕺
======

[openpilot](http://github.com/commaai/openpilot) is an open source driving agent. Currently, it performs the functions of Adaptive Cruise Control (ACC) and Lane Keeping Assist System (LKAS).  It's about on par with Tesla Autopilot.
This OLD_CAR Branch brings openpilot to almost every car. Follow this readme to get an overview how it works.

Big thank you goes to @wocsor. He developed the whole thing and modified the code.

⚙️ CODE CHANGES ⚙️
======================

💧WATER💧 = COMMA + OLD_CAR

CHANGES FOR OLD_CAR:

1. 💧OLD_CAR is in selfdrive/car/toyota (use /Toyota/interface.py for tuning)
2. 💧CanValid was set to True to avoid can / communication error messages.
3. 💧It uses the SteeringRatio which is set in interface.py.
     Vehicle_model.py does not change it anymore.
4. 💧CAMERA offset is set to 0.00.
     (Set it to where ever your EON is mounted in lane_planner.py)
6. 💧Steering Angle sensor is flipped because it is mounted upside down in my van. 
     (Delete "-" in Toyota/carstate.py line 166 to flip it back) 
7. 💧It is forced to send GAS_PEDAL command on canID 0x200


🚌 OVERVIEW 🚌
======================

I think retrofitting and #old_car is the hidden future of openpilot.
Eon and openpilot, like it is expected to be used, is limited to a few makes and type of cars which are build in 2018-2021.
In a few years cars will have better selfdriving on stock, than comma can ever deliver - due to better hardware an software.
All older cars will not be plug and play.
That's where #old_cars comes in.
Plus, there is no limitation due to brands or types.
There are billions of cars which can be upgraded.
Right now we are using the same actuators in completely different types of cars.
(Celica 2003, VW Vanagon 1988, Ford E350 1994).
We upgrade cars from zero assistant to level 2 self driving.
We make driving safe and chill. That's really impressive!
Let's see where our journey will end. I can think of like a dev-kit with some actuators and interceptors for easy DIY projects.
Thank you <@Wocsor> for spending so much effort.
He is doing fundamental research and hacking!

🛠 HOW TO START 🛠
======================

To make openpilot work in an old car, we need to retrofit actuators from supported cars like toyota corolla 2018. Some small ECU needs to be build DIY.

Brain:
* [EON and Panda](#eon-and-panda)


Steering:
* [EPS - electric power steering](#eps)
* [VSS - vehicle speed sensor](#vss)
* [Buttons](#buttons)
* [Cruise_ECU](#cruise_ecu)
* [Steering angle sensor](#steering-angle-sensor)

Throttle:
* [Cruise Control Actuator](#cruise-control-actuator)
* [Potentiometer](#potentiometer)
* [Throttle_ECU](#throttle_ecu)

Radar: 
* [Radar sensor](#radar)

Brake (not finished yet):
* [ABS PUMP / OSCC Module](#POLYSYNC-OSCC-Brake-module-and-Prius-Actuator)

Community
 * [Community](#commutity)

# BRAIN

## EON and Panda

![enter image description here](https://i.imgur.com/RBqQvoZ.jpg)

First, we need a brain to control everything. 
This is EON. An extremely powerful piece of hardware which runs openpilot. 
We also need Panda, which connects EON to the OBD2 port of the car. So that EON can talk to the car via CAN-Bus. 
Oh wait! - we do not have a CAN-Bus network in our car. Don't worry we will build it DIY.
For more informations to EON or PANDA visit [comma.ai.](https://comma.ai)

I have used a cheap [OBD2 wire connector](https://www.amazon.com/iKKEGOL-Connector-Diagnostic-Extension-Pigtail/dp/B07F16HC12/ref=sr_1_15?__mk_de_DE=%C3%85M%C3%85%C5%BD%C3%95%C3%91&keywords=obd2%20cable&qid=1560506720&s=gateway&sr=8-15) to pinout the panda. 


# STEERING


## Eps

I have used an EPS (electronic power steering) out of a Toyota corolla 2018.
This is already supported by Openpilot so we do not have to port it from sketch.

![electric steering column out of a corolla](https://i.imgur.com/PUOQNph.png)

It is  important, that it provides LKAS (lane keep assistent). The steering column and motor might be the same like in older corollas. But the ECU is different. So make sure to buy the ECU with LKAS ( "KV" on the sticker).
![EPS ECU COROLLA 2018 WITH LKAS](https://i.imgur.com/Bl3FpBX.png)

This is how to wire the steering ECU:

![enter image description here](https://i.imgur.com/w6tnlDq.png)

z11 and z7 connectors will be connected to the EPS Motor.

Now it's time to retrofit the steering column. Since every car is slightly different, you need to be a little creative. 
Im my case, I have cut my stock column in half and welded both ends to the corolla steering column.
If you already have a hydraulic power steering, you might want to disable that. Otherwise you would have a power steering on top of a power steering, and your steering wheel will never return to center by itself.

This is how my conversion looks like: 

![enter image description here](https://i.imgur.com/TTxdILC.jpg)

![enter image description here](https://i.imgur.com/349kMvt.png)

Now we have a working power steering in our car! 
Unfortunately it goes into failsafe, which means that it will disable LKAS. 
Cruise_ECU will take care of this issue.

----
## Vss

Eon needs to know how fast we are driving. Therefore we need to add a sensor which measure the "speed" of the car. Most cars already provide such a signal already. For example for the radio. If you have such a signal, you can grab that. In my case I have added a hall sensor to the rotary disc of the speedometer. This counts 4000 signal each km. MAIN.ino reads that signal and calculate the speed in km/h with some math to send that value to the can bus.

NOTE: you need to adjust the "counts per km" of your specific sensor in MAIN.ino code. (https://github.com/Lukilink/ECU/blob/master/MAIN.ino)


----
## Buttons

Since we do not have original toyota buttons, - guess what - we need to build it ourself.
Be creative, it is simple task. Pull-down buttons, which will be connected to MAIN.ino ECU.
MAIN.ino ECU will read the Button State, and send messages to the Can-Bus for: (enable/disable) (set speed up/ set speed down).

![enter image description here](https://i.imgur.com/V3gqlWY.png)

![enter image description here](https://i.imgur.com/LdcZqPN.jpg)

----
## MAIN ECU

MAIN ECU Hardware is an [Arduino Uno](https://www.amazon.com/Elegoo-EL-CB-001-ATmega328P-ATMEGA16U2-Arduino/dp/B01EWOE0UU/ref=sr_1_2?__mk_de_DE=%C3%85M%C3%85%C5%BD%C3%95%C3%91&keywords=arduino%20uno&qid=1560514638&s=gateway&sr=8-2) with a [CAN bus shield]  (MCP2515 EF02037)

![CRUISE_ECU](https://i.imgur.com/CnysIXP.png)


It handles the following functions: 

 1. Cruise_ECU sends some CAN messages on the bus, which needs to be send to enable Openpilot.
 
 2. Cruise_ECU calculates the current speed by reading the VSS (Vehicle speed sensor). It sends km/h to 0xaa message on the CAN-Bus. EON / Openpilot can read and use this messages.
 
 3. Cruise_ECU digitalReads the buttons and sends the associated CAN messages to the bus. It let's us enable and disable
 Openpilot. We can also increase or decrease the set speed.
 
 5. It provides some safety function. It will disable immediately, if it looses CAN safety checksum.
 
 This is how you wire Cruise_ECU (Update: that may have changed please take a look in the code) : 
![CRUISE_ECU_PINOUT](https://i.imgur.com/9Mnr5qg.jpg)

[Download Cruise ECU Code.](https://github.com/Lukilink/ECU/blob/master/MAIN.ino)


----
## Steering Angle Sensor

I am using the stock steering angle sensor out of a toyota corolla / rav4.
I highly recommend buying it with the hair spring attached. Also we do not need the hair spring, it takes care of the sensor while shipping.
Fortunatley the sensor provides it's own ECU. Therefor it is like plug and play. 

![enter image description here](https://i.imgur.com/8hsyrax.png)


![enter image description here](https://i.imgur.com/CwXuUUv.jpg)
	
Note: I have mounted the sensor upsidedown. I have compensate that in the openpilot code. 

---

# THROTTLE / GAS

## Cruise Control Actuator

Add an electric cruise control actuator to your throttle.
Choose what ever brand you like. They are all very similar and it is easy to get one cheap out of a 90th car on ebay. 
It needs to have an electric motor, and something similar to a clutch.
The "clutch" is basically a solenoid, which disconnects everything mechanically. Pretty nice safety feature :) 
If you already have stock cruise control in your car, take that one!


## Potentiometer

To measure the position of the throttle we use the stock potentiometer. Almost every throttle has a potentiometer attached.
We read that amount in GAS.ino (https://github.com/Lukilink/ECU/blob/master/GAS.ino). 

Note: GAS.ino sketch must be adjusted for your specific potentiometer. Therefore you need to "measure" the min and max value of your potentiometer with analog_read_to_serial. If you have your min and max values you can set those in Throttle_ECU sketch.

## GAS_ECU

Throttle ECU hardware is an [Arduino Uno](https://www.amazon.com/Elegoo-EL-CB-001-ATmega328P-ATMEGA16U2-Arduino/dp/B01EWOE0UU/ref=sr_1_3?__mk_de_DE=%C3%85M%C3%85%C5%BD%C3%95%C3%91&keywords=arduino%20uno&qid=1560516407&s=gateway&sr=8-3) with a [CAN-bus shield] MCP2515 EF02037 and a [Motor Controler](https://www.robotshop.com/de/de/cytron-10a-dc-motor-treiber-arduino-shield.html?gclid=CjwKCAiAz--OBhBIEiwAG1rIOtq9lzE9XKenDgZFCtUJ_VIgl4X1wVGqAu6yuw4j7MSbVEsXjBfUaRoCnGAQAvD_BwE) attached.

![OLD PICTURE](https://i.imgur.com/EClutor.png)
Note: This is a picture of an old prototype. Not the hardware that ist listet above.

It handles the following functions: 

- reads gas message 0x200 on can bus (send by Openpilot / Panda)
- reads potentiometer on Throttel
- Closes the solenoir and drives the motor (cruise control aktuator) which is attached to throttle.
- cancels openpilot when human input on gas pedal is detected. 

Download [gas.ino](https://github.com/Lukilink/ECU/blob/master/GAS.ino).


---
# RADAR

## Radar

Part Number:  88210-07010

![enter image description here](https://i.imgur.com/0dD9zPy.png)

Similar to the steering angle sensor, the radar out of a corolla / rav4 provides its own ECU. 
Therefore it is pretty easy to install. 

![enter image description here](https://i.imgur.com/soMhXAJ.png)

![enter image description here](https://i.imgur.com/qrvZv66.jpg)

Note: It has two can bus. One bus is on the same like all other ECU. The other one has a seperate pin on panda.


---

# BRAKE

We use the same method like on throttle / gas.
I have attached a cruise control actualtor to the bake pedal. 
The motor is strong enough to handle a good deceleration but can not do emmergency brake.
I have attached a brake sensor to measure the pressure of the system as a reference. (simmilar like the poti on throttle)
ST749 Bremsdrucksensor, 3/8-UNF 100 bar

Hardware is exactly the same like Throttle ECU hardware: 

Brake ECU hardware is an [Arduino Uno](https://www.amazon.com/Elegoo-EL-CB-001-ATmega328P-ATMEGA16U2-Arduino/dp/B01EWOE0UU/ref=sr_1_3?__mk_de_DE=%C3%85M%C3%85%C5%BD%C3%95%C3%91&keywords=arduino%20uno&qid=1560516407&s=gateway&sr=8-3) with a [CAN-bus shield] MCP2515 EF02037 and a [Motor Controler](https://www.robotshop.com/de/de/cytron-10a-dc-motor-treiber-arduino-shield.html?gclid=CjwKCAiAz--OBhBIEiwAG1rIOtq9lzE9XKenDgZFCtUJ_VIgl4X1wVGqAu6yuw4j7MSbVEsXjBfUaRoCnGAQAvD_BwE) attached.

It handles the following functions: 

- reads brake message on can bus (send by Openpilot / Panda)
- reads pressure sensor
- Closes the solenoir and drives the motor (cruise control aktuator) which is attached to brake pedal.
- operates brake light (via relai)
- cancels openpilot when human input on brake pedal is detected. 

Download [brake.ino](https://github.com/Lukilink/ECU/blob/master/BRAKE.ino).




##

# 🥇🥈🥉 COMMUNITY AND CREDITS🏅🎖️🏆
======

Community is the most important thing on this project.

The [legendary Arne Fork] does support old_cars now.
Big thanks to Arne182 for his awesome work. 


Comma [Twitter you should follow](https://twitter.com/comma_ai).

Also, we have a several thousand people community on [Discord](https://discord.comma.ai).



Licensing
------

openpilot is released under the MIT license. Some parts of the software are released under other licenses as specified.

Any user of this software shall indemnify and hold harmless Comma.ai, Inc. and its directors, officers, employees, agents, stockholders, affiliates, subcontractors and customers from and against all allegations, claims, actions, suits, demands, damages, liabilities, obligations, losses, settlements, judgments, costs and expenses (including without limitation attorneys’ fees and costs) which arise out of, relate to or result from any use of this software by user.

**THIS IS ALPHA QUALITY SOFTWARE FOR RESEARCH PURPOSES ONLY. THIS IS NOT A PRODUCT.
YOU ARE RESPONSIBLE FOR COMPLYING WITH LOCAL LAWS AND REGULATIONS.
NO WARRANTY EXPRESSED OR IMPLIED.**

---

<img src="https://d1qb2nb5cznatu.cloudfront.net/startups/i/1061157-bc7e9bf3b246ece7322e6ffe653f6af8-medium_jpg.jpg?buster=1458363130" width="75"></img> <img src="https://cdn-images-1.medium.com/max/1600/1*C87EjxGeMPrkTuVRVWVg4w.png" width="225"></img>
