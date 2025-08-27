---
layout: blog
name: Is The Zephyr Device Tree Too Complicated?
title: Is The Zephyr Device Tree Too Complicated? | Magpie Embedded
date: 27-08-2025
author: Tim Guite
---

At this year's Open Source Summit Europe in Amsterdam, I [presented a talk](https://osseu2025.sched.com/event/888bfd905c0cf76c659d0408ad498a8e) on the challenges of the Device Tree for specifying hardware in Zephyr.

You can download the presentation here:
<a href="/assets/presentations/IsZephyrDeviceTreeTooComplicated_ZDS2025.pdf">Is the Zephyr Device Tree Too Complicated?

The talk was well attended, and roughly half of the audience raised their hand when I asked if they did think it was too complicated.
It is quite a specialised group of people who travel across countries to attend these conferences and make a choice to find out more about Zephyr.
If half of those people find the Device Tree difficult, there must be many more developers struggling with this without being heard.

In questions following the session, it was highlighted that the Device Tree is used in Linux and many other projects, which also suffer from the same challenges.
That's one of the great things about the work that Kyle Bonnici at Nordic has been doing.
The [DTS LSP](https://github.com/kylebonnici/dts-lsp) is agnostic as to the end project, so it can be used across device tree use cases.

I still believe there is a need for further tooling to simplify the Device Tree experience for application developers who only need to use a limited subset of the device tree capabilities and would appreciate guard rails when doing so.
As Zephyr continues to grow, this will make it a lot easier for developers to join the ecosystem and build useful embedded systems with Zephyr.