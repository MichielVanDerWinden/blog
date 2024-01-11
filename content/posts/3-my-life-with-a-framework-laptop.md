---
title: "My life with a framework laptop"
slug: "living-with-framework-laptop-2-months-in"
date: 2024-01-11T07:14:31+02:00
draft: false
categories: ["gear", "life", "work"]
---

I've started working at Devoteam in December 2023. This transition meant giving up my Macbook Pro 16" with M1 Pro and 32 GB of memory. I loved that machine for how fast and silent it was whilst maintaining great battery life. Nevertheless, running an ARM chip meant I couldn't do everything I wanted with it - being a bit of a gamer means I'd love to run more than the handful of Steam games currently available for MacOS on an ARM machine, and thus I've always had a separate machine for gaming.
Transitioning to Devoteam gave me the option of brining my own device (BYOD) for work, thus giving me the possibility of buying whatever I wanted. Going for a sweet gaming laptop, a handheld that I plug into a dock or a simple work laptop that'll do whatever I need it to do (mostly browsing, text-based work like programming and scripting, and some IM-stuff)? Nope, I went for a [Framework](https://frame.work) laptop instead.

<!--more--> 

## Building a Framework laptop
Framework laptops are great machines. They're built to have replaceable parts, can be upgraded in the future (want a new mainboard? [Framework has got you covered!](https://frame.work/marketplace/mainboards)) and don't look all that different from other machines either.
I've ordered mine as a DIY kit (I love building my own PCs, so why not build a laptop as well?) and it arrived quite quickly. As most default options for the SSD and memory were a bit pricy for my tastes, I've opted for buying my own kits instead. Building the machine was quite straight forward (Framework provide all the necessary steps in [an iFixit-style guide](https://guides.frame.work/Guide/Framework+Laptop+13+(AMD+Ryzen%E2%84%A2+7040+Series)+DIY+Edition+Quick+Start+Guide/211)) and I got it up and running within approximately an hour.

## My machine
I've gone for the lowest spec AMD 13" as I didn't feel the need to spend more for a couple of extra CPU and GPU cores. In my opinion CPU power and GPU power have gone way past the point of requirements for a workable computing experience (especially if you're **not** using Windows) and thus I didn't find the upgrade warranted. Still, as Framework provides drop-in replacements for mainboards, I could technically upgrade to a higher spec whenever I feel like it.

My machine is currently specced as follows:
 - **CPU**: AMD Ryzen 5 7640u (6 cores, 12 threads)
 - **GPU**: AMD Radeon 760M
 - **Memory**: Kingston Impact 32 GB DDR5 @ 5600 MT/s
 - **SSD**: Crucial P5 Plus 2TB
 - **Screen**: Matte 2256x1504 (3:2)
 - **Ports**: 4x USB-C (2 in use), 1x DP 2.0, 1x HDMI 2.1 (1 in use), 2x USB-A (1 in use)

This suits my needs really well as the Ryzen 5 is part of the Zen 4 platform and thus very fast, quite power efficient and contains a proper iGPU for some light gaming or encoding/decoding. The OS I've chosen to use is [Manjaro](https://manjaro.org/) - I wanted to use Linux for its flexibility, but also found that other distributions often came with older kernels that didn't yet properly support this AMD CPU and chipset, or they were running properly but testing was done so poorly that each single update broke my system in one way or another (*looking at you here, Fedora*).

## Complaints
Although I've not yet had enough time to fully use everything the machine has to offer me, I've found some issues and complaints already. The keyboard isn't as crispy and doesn't feel as nice as my Macbook's keyboard did. The trackpad is fine, but it's not nearly as precise or nice to use as my Macbook's trackpad was. I really miss the ambient light sensor for dimming the screen **and** the keyboard backlighting when in a darker room. The screen is really nice but maybe just a tad too high in resolution for the 13,5" panel.

Minor gripes though, and as I found myself comparing a 1000 dollar machine to a 3500 dollar machine, I found that I could live with these issues really well. They don't bother me much and every day I'm using the machine I find that I'm focussing on them less, whilst enjoying my time more and more. This laptop is really growing on me :)

## Adding more horsepower
Having mentioned that I'm a bit of a gamer, I've come from a desktop PC with an i5, 16 GB of DDR4 and an RTX 3070 GPU. This setup gave me hours of fun (although since I became a parent it's been sitting there, turned off, for most of the time) but has been cumbersome as I didn't like switching my screen and peripherals between my laptop and PC as this always came with weird side effects (USB microphone not reconnecting, speakers not changing over etc.).
One of the reasons I've chosen for the AMD machine is that it comes with Zen 4 cores, which are really fast and can handle games just fine from a CPU standpoint. The iGPU is only passable when it comes to gaming though, but I knew that since the introduction of USB-4, it would only take a couple of months before eGPU solutions started working as well.

So that's what I did. I took my RTX 3070, put it in a [Razer Core X](https://www.razer.com/gaming-egpus/razer-core-x) eGPU enclosure, connected said enclosure to the top-right port of my laptop and the OS immediately recognized a new GPU. Although it's not fully stable in Manjaro yet (Nvidia and Linux never match that well anyways), I've been able to boot into Windows and start gaming as soon as the display shows the desktop. Some might call it a clunky solution (and that I'm leaving performance on the table due to USB-4/TB3's PCI-E3.0x4 bandwidth maximum) but for me it's been a dream solution as I finally don't have to switch between machines for work and fun anymore.

## What do I think of the Framework AMD 13"?
Up to now I've had a blast using the system as is. I've had a couple of complaints, most of which stem from coming from a Macbook Pro that costs way more, but also provides a more "full fledged" experience out of the box. Still - the flexibility I've gained from using an x86 machine with Linux has been invaluable over the past two months already. Here's hoping to getting many years out of this machine! Whenever I'm adding something new to the machine, or if I'll upgrade the entire thing with a new mainboard, I'll put out an update with my findings and feelings at that time.