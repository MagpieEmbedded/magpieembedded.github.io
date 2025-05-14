---
layout: blog
name: Ocean Business 2025
title: Ocean Business 2025 | Magpie Embedded
date: 14-05-2025
author: Tim Guite
banner_image: /assets/ocean_business_2025.jpg
banner_caption: Tim and various robots at Ocean Business 2025
---

Last month, companies and experts working on ocean science and technology gathered in Southampton for [Ocean Business 2025](https://www.oceanbusiness.com/).
It takes place once every two years and is one of the largest conferences focussing on the ocean worldwide.
I was very excited to attend and learn more about this exciting industry.
In this post, I'm going to provide my key takeaways from the conference, highlight the tech stack and give an overview of the companies I met.

# Key Takeaways

**There are a lot more robots in the sea than you might think!**

Approximately half of the stands at the conference were hosting an autonomous or semi-autonomous vehicle of some sort.
Some of these vehicles travel on the surface, and some of them are down on the seafloor.
There was also a great range in size of the vehicles being given autonomy.
The smallest were a bit bigger than a microwave, while the largest were large ships capable of carrying crew and equipment.

**Innovation is allowing smaller companies into the market**

The ocean is a harsh environment, and building equipment that can handle that is difficult.
Traditionally, this has meant high capital costs to manufacture large, robust equipment.
However, demand for more autonomy and new manufacturing methods have allowed smaller companies and startups to gain an edge.
Open source technologies can be leveraged to provide more intelligence at a lower cost.
3d printing can be used to rapidly iterate on prototypes or even build the final vessel.
The larger companies in this space have been taking notice and applying this modern approach to their own products.

**Funding is hard**

A lot of companies at the conference rely heavily on funding from governmental sources, such as defence and research organisations.
As governments restrict budgets, particularly in the US, this funding becomes more scarce and may not be fully replaced by private capital.
Even if it does, research organisations may find it harder to make their findings public and collaborate on models of the ocean.
Companies working on more directly industrial use cases such as energy transfer and mining may find themselves on surer footing.

# Tech Stack

A couple of key terms to find your way in the ocean technology space:

- ROV - Remotely Operated Vehicle. This is usually an unmanned vehicle connected by cables (umbilical) to an operator.
- AUV - Autonomous Underwater Vehicle. Not to be confused with UAV (for flying in the sky), AUVs are similar to ROVs but without the cable. Typically they will be programmed with a route and series of operations to follow. Keeping track of location is an essential and difficult task for these vehicles.
- IMU - Inertial Measurement Unit. Combines accelerometers and gyroscopes to track an objects movements. Used for dead reckoning location tracking.
- AHRS - Attitude and Heading Reference System. Similar to IMU function with additional magnetic sensors and onboard processing to calculate heading.
- Observation Class - This refers to vehicles which carry cameras and other sensors only.
- Work Class - Vehicles which carry equipment such as drills, manipulators, trenchers, for carrying out work.
- CTD - Conductivity, Temperature, Depth sensor. The primary tool for measuring sea water.

Looking at the software, a lot of companies use [ROS](https://www.ros.org/) as part of their tech stack.
It can be a good way to abstract the hardware from the autonomous operations and data collection required at the operations level.

Sensor choice is important in this industry and there were companies there just to demonstrate their specific sensor modules.
Accurately collecting data is the main requirement for surveying companies so this has a lot of value.
Ensuring the sensors work for long periods of time in a difficult environment is hard and there are often self-check systems built in.

Various levels of computing were used on the vessels themselves.
Often there are microcontrollers for real time operations such as handling the motors, with larger compute modules for higher level logic and control.
Many vessels communicate with an operator which can add a significant delay to the control loop.

# Companies

This is a quick overview of companies that I met, thinking about their tech stack, their market and any interesting facts!

## Sofar Ocean

Sofar make and sell a module which floats on the sea surface and transmits measurement data back to customers.
It is powered by solar panels and connects to sensor modules which float at some depth under the water.
They have a fleet of devices which helps them to generate an ocean currents / weather model as a demonstration.
They have been developing on the open standard [Bristlemouth Connector](https://www.bristlemouth.org/) to provide a plug and play interface for sensor companies to build against.
When their modules end up on shore, they can simply be handed to the nearest fisherman, boat, or ship and let back out to sea!

## FET Subsea

FET build a range of ROVs from their base in Yorkshire.
Apparently a lot of subsea companies are derived from aerospace companies as there is a lot of crossover in the types of engineers who build them - or at least there used to be.
This means not all subsea companies are located near the sea!
I had an interesting chat with them about a software solution they have for observation which carefully tracks timestamps on measurements from cameras and other sensors to ensure accurate playback.

## SMD

Unfortunatly a lot of SMDs products are too big to fit in the conference!
They build trenchers, which dig trenches on the sea floor for pipelines, power cables and data lines.
These trenchers are almost as big as a house in some cases.
More recently they have moved into the ROV space as well as remote operation from a Star Trek like command chair (not the only ones doing this).

## Kraken Robotics

Canadian company which produces a variety of subsea surveying equipment.
Often working on defence applications, they have several Synthetic Aperture Sonar (SAS) measurement vehicles for mapping the seafloor.
Some of these can power themselves while others are towed behind a boat.
Additionally, make a subsea battery which can power devices for months while they sit on the seafloor.

## Exail

Part of a massive company which resulted from two large French engineering companies merging, Exail have quite a range of products available and are well vertically integrated in this space.
They can produce a custom ROV or AUV from scratch, sell you all the parts you need to make your own or sell you one of their existing models which you can modify.

## Framework Robotics

Taking an interesting approach to subsea vehicle design, Framework have a 3d printed open cube which can be easily attached to more cubes in a Lego-like fashion, to build an outer skeleton.
Other sensor and compute modules can then be built into the skeleton.
While this may create some new control dynamics challenges, it has allowed them to move from concept to reality very quickly.
Furthermore, it also opens up designs such as donut-shaped vessels which would be harder to create without this modular approach.

## Develogic

Develogic make equipment for seafloor applications, such as communication modules and landers.
These devices are designed to sit on the seafloor over long periods.

## Tethys Robotics

Tethys is a spin-out of a university research project in Switzerland, which has created a relatively small observation class drone that is suited to high current applications.
It can stay in place while monitoring the target even in very rough conditions thanks to its configuration of propellers.

## Boxfish Robotics

AUV manufacturer with a specialisation in cinematography!
So if 4k cameras and advanced lighting setups at depth are your thing, this is the company for you!

## Blue Abyss

Currently selling a vision, Blue Abyss want to create an enormous, deep test tank somewhere in south-west England which can be used not only by the subsea industry but also by the space industry.
There are very few facilities like this available worldwide.
Large water tanks are an effective training tool for astronauts due to the weightless-like effect of neutral buoyancy.
They are still looking for a site so this is a few years away at least, but an interesting idea!

## Ocean Infinity

Working on creating unmanned ships which can be operated fully remotely.
Also had a Star Trek inspired command setup!
Looking to improve efficiency by operating 24 hours a day.

## Sea-bird Scientific

With a tag-line of "For scientists, by scientists", Sea-bird make sensor modules such as CDT sensors for use in scientific surveying.
As a result, a large part of their customer base are academic or research based organisations who are seeing their funding diminish at the moment.

## XSens

Create sensor modules such as IMUs for subsea applications.
These can be bought as a very small PCB or as waterproofed modules that can be bolted onto the outside of a vessel.

## Foreshore Technology

A little different than the other companies here as their product is mostly above the water.
Foreshore have developed a sensor system which attaches to dredgers that can be combined with subsea mapping data.
This allows the operator to keep much better track of what they are removing below the waterline, even in muddy water.
It reminded me of [knee surgery systems](https://www.precisionjointreplacement.co.uk/mako-robotic-arm-assisted-technology-for-total-knee-replacement-orthopaedic-surgeon-birmingham-west-midlands.php) which use 3d models of bones combined with live sensors to aid surgeons.

# Wrap Up

I had a great time at Ocean Business 2025!
The sun was shining and there were a lot of cool robots on show - can't ask for a much better conference day than that!
This is clearly an industry undergoing a lot of change, with increased use of software at various layers of the stack.
What an exciting area to work in!