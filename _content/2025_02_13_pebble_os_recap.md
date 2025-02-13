---
layout: blog
name: Lessons from Pebble OS
title: Lessons from Pebble OS | Magpie Embedded
date: 13-02-2025
author: Tim Guite
---

At the start of 2025, [Google made the firmware for Pebble watches open source](https://opensource.googleblog.com/2025/01/see-code-that-powered-pebble-smartwatches.html).
You can find the code [*here*](https://github.com/google/pebble).
This is quite an unusual step for Google to take and there is an interesting history - and perhaps [future](https://repebble.com/) - behind the Pebble watches and technology.
One of the legacies of Pebble is [Memfault](https://memfault.com/), who host an excellent blog called [*Interrupt*](https://interrupt.memfault.com/blog/).
It was started by engineers who had worked on the telemetry for Pebble and saw an opportunity to use it across more systems.
Therefore, they were well placed to host a talk with several people who had worked at Pebble to discuss the decisions they made and what can be learned from the project.
The full video is available [*here*](https://www.youtube.com/watch?v=dk5wsNN8abo).
I thought this was an excellent discussion and collected my notes below.

## The People

*François Baldassari* - CEO and Co-Founder of Memfault. He worked at Pebble for 3 years, moving to Oculus for 3 more years before founding Memfault in 2019.
Strong embedded systems background.

*Chris Coleman* - CTO and Co-Founder of Memfault. He worked at Pebble for almost 3 years, then at Fitbit for 2 years after they acquired Pebble before founding Memfault in 2019.
Strong embedded software background.

*Brad Murray* - Head of Engineering at Beeper. Worked at Pebble for 4 years from the initial kickstarted campaign.
Started as a firmware engineer and gained more responsibility as the company grew.
After Fitbit he seems to have moved into more managerial positions away from embedded systems.
Since 2021 he has been working on [Beeper](https://www.beeper.com/), with Pebble founder Eric Migicovsky.
Beeper was recently acquired by [Automattic](https://automattic.com/), which owns Wordpress.

## The Short Story

Pebble was initially funded by a historically successful Kickstarter campaign.
After several years it was [bought by Fitbit in 2016](https://www.theverge.com/2016/12/7/13867158/fitbit-buys-pebble-smartwatch-acquisition-deal) for around $40M.
Fitbit absorbed a lot of the Pebble staff but shut down the Pebble brand and devices.
Fitbit itself was then [acquired by Google in 2019 for $2.1B](https://www.forbes.com/sites/davidphelan/2019/11/01/google-buys-fitbit-for-21-billion-heres-what-it-means/).
Unclear how much of that value was from Pebble IP!
Fitbit has been plodding along since then although the Pebble community was still working on their devices and software.
Last year, [Eric simply asked Alphabet if they could release the source code for the operating system](https://www.theverge.com/2025/1/27/24352968/pebble-smartwatch-open-source-google-comeback), which they did!
He is now leading an effort to create new Pebble devices called [*RePebble*](https://ericmigi.com/blog/why-were-bringing-pebble-back).
It is important to note that Alphabet removed some key pieces from the code they released to avoid licensing conflicts, so the codebase is not actually ready to go at the moment.

## Notes From The Talk

All three agreed that this is quite a rare example of a commercial firmware codebase becoming open source.
There are some RTOS examples such as [ThreadX](https://threadx.io/), but very few that were developed to be used solely by one company.
The point was made that the git history was not released, as this would have given a very interesting look into the development of the codebase and the way the company changed over time.

Initially, a lot of people working at Pebble did not have significant firmware experience.
This resulted in a very software-oriented approach.
Brad stated, **"We did a lot of things very simply until that didn't work anymore"**.
An example of this desire for simplicity is that the codebase had to build for all hardware platforms, including development boards and the QEMU emulator.
The [QEMU](https://www.qemu.org/) target allowed significant regression testing which would have been very difficult to achieve otherwise - and is still not common in the embedded systems world.
Francois also mentioned that he has had success using [Renode](https://renode.io/) at Memfault, and that it can be useful for this kind of emulation if it already supports your target hardware.

PebbleOS was treated as a platform rather than a single device firmware.
It needed to support apps across all Pebble devices.
To start with (doing it the simple way first), apps were statically linked against the firmware using tools provided by the Pebble team.
This was sufficient to support early adopters.
Later, changes to the hardware, such as colour screens on some models, required backwards compatibility to be built into the OS.
Chris was inspired by [*The Old New Thing*](https://devblogs.microsoft.com/oldnewthing/) which details some of Microsoft's challenges in maintaining a stable API for decades.

Additionally, the software team were able to advocate for hardware that was easier to build on and debug.
Often, electrical engineers are given complete responsibility for component selection including the MCU.
However, it sounds like the Pebble team collaborated effectively and gave a lot of weighting to the software challenges.
This includes the creation of a "big board" prototype that had multiple current sensors to support power analysis.
Particular credit was given to electrical engineer Nick Ford, as well as the [INA226](https://www.ti.com/lit/ds/symlink/ina226.pdf) power measurement chip.

Early Pebble devices were built using [ContikiOS](https://github.com/contiki-ng/contiki-ng).
The decision was made to move away from it because of difficulties with how it handled large numbers of files in the file system and how it detected the beginning and ending of files in NOR flash.
When this proved too big of an issue, Chris wrote a custom [NOR flash driver](https://github.com/google/pebble/tree/main/src/fw/drivers/flash).
The system ended up being build around [FreeRTOS](https://www.freertos.org/).

There was discussion about the [hard fault handler](https://github.com/google/pebble/blob/main/src/fw/hardfault_handler.c) which provided a simple way for applications to crash safely.
Sometimes this would trigger a system restart.
Crucially, this would log a [`RebootReason`](https://github.com/google/pebble/blob/main/src/fw/system/reboot_reason.h) which could be later analysed.
I am speculating, but there is a clear thread between this work and what is now provided my Memfault.
Francois mentioned that one of the challenges they had at Fitbit was interpreting these structs across multiple versions of firmware and the server.
Memfault has tooling in place to avoid this kind of issue.

The MPU was used extensively by Pebble.
This was an essential tool as it was supporting arbitrary application loading by users.
One of Brad's favourite bugs came from a slight misconfiguration of this system.
A user found a series of bytes in the Pebble binary (possibly font files) which could be executed by the application API as ARM instructions to return control to the application in a privileged mode, giving it full control of the system.
No one was clear on how someone would find a series of bytes like this but there you go!
The fix was using the MPU to register the binary as read only and not executable.
There may be other interesting use cases of the MPU within the codebase.

Finally, mutex deadlocks were called out as being a constant source of headaches!
Asynchronous programming is hard!

## Key Lessons

- Do things the simple way first
- Take software seriously in your embedded systems
- You never know how far a small idea can go