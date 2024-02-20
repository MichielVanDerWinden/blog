---
title: "Software setup for cloud engineering & development"
slug: "software-setup-for-cloud-engineering-and-development"
date: 2024-02-06T09:34:22+01:00
draft: false
categories: ["aws", "iac", "life", "tools", "work"]
---

As preparation for my move from inQdo to Devoteam, I started wondering about the operating systems, software and tools I used to use for my day to day work. I've been spoiled as inQdo provided everyone with a top of the line Macbook Pro (M1 Pro, 32 GB RAM in my case) that ran everything I could throw at it, but it never felt exactly in line with my work needs. Making the move to Devoteam gave me the option to *byod*, and being Dutch, this meant I didn't want to spend too much money. Cost and performance optimization for work needs became the name of the game! 

<!--more-->

## TLDR (Spoilers!)
Manjaro, Gnome, Firefox, Gnome Terminal with Oh-My-Zsh, Docker, minikube, Terraform, cdk, Logseq, VS Code, Ferdium (for Whatsapp & Google Chat) and GFeeds (RSS reader). Also: Gnome extensions Battery Time & gTile.

## Too long, still reading!
If you've read my bio, you'll know that I love containerizing everything. Docker doeesn't do well with MacOS though; minor performance issues, annoyances with sharing storage between the host and its containers, and more tiny issues that in and of itself don't mind me too much. Eventually, I started work on a client project where I ran into each of these issues at the same time. Annoyances occurred and workarounds had to be made, resulting in a project that was passibly workable.

Another issue I had with MacOS and (especially) the Apple M*-processors was the insane lack of flexibility when it came to running different operating systems or adding stuff like eGPUs. There are multiple projects trying to run either Windows or Linux on newer Apple devices, but it's not fully compatible yet and you're leaving behind all Apple guarantees of "it just works".

As posted previously, I'm currently using a [Framework 13 AMD laptop with 32 GB of RAM and a 2 TB SSD](/posts/living-with-framework-laptop). It suits my needs when it comes to performance and affordability whilst also giving me a wealth of flexibility when it comes to operating systems, tools, software and even hardware expansions. It's a proper solution for years to come. But what OS am I running, and which applications are most useful for my work? Let's go through them all.

## OS woes
As mentioned in the introduction, I'm a big fan of containerization. I love using Docker, and I am getting quite fond with running Kubernetes for most (professional) workloads. During my day-to-day work, I'm mostly working in the command line and will be running Terraform deployments, synthesizing CDK projects and deploying Helm charts. Thus, choosing which type of operating system to run was quite easy; general CLI tools, Docker and Kubernetes are most at home on Linux meaning the best integration could be had there.
But, as many Linux users know, [there are way too many distros to choose from.](https://upload.wikimedia.org/wikipedia/commons/1/1b/Linux_Distribution_Timeline.svg) Apart from this, everyone and their dog have differing opinions about which distro is best for which use case, eventually resulting in either "it depends" or "every distro can do whatever you want".

Luckily, Framework offers a solution. They've officially only tested two different distributions; [Fedora 39 and Ubuntu 22.04 LTS at the time of writing](https://frame.work/nl/en/linux) and thus officially only support these two options. I've tried both, and in proper IT-person fashion I didn't like either of them! I found Fedora to be too _bleeding edge_ whilst not giving me any reassurances whatsoever that the newest available updates to packages had been tested properly, whilst Ubuntu 22.04 is quite old (at least in the IT sense) and thus provides you with only a couple of recently updated packages. Also, it's pre-packaged with Snap (a containerization tool for GUI applications) which I hate with a passion due to its closed sourcedness and Canonical's need of providing more and more default packages as _snap only_.

As the Framework 13 AMD version uses a relatively new CPU/SOC, it isn't supported by each available OS out of the box yet. For proper functionality and at least a modicum of power efficiency you'll need your Linux Kernel to be at or above version 6.6 (or a specifically built LTS kernel when using Debian-based distributions) and thus a relatively _bleeding edge_ distribution best suits the platform. I've hopped all over the place, falling in love with the simplicity of Linux Mint, having fun with good ol' Debian and struggling with EndeavourOS (Arch based distro from the Netherlands 🥳), eventually landing on Manjaro for its ease of use, relatively modern kernel and proper testing of packages before releasing them to their audience.

## Manjaro & Gnome
Manjaro provides three official desktop environments; KDE, XFCE and Gnome. As I've been using MacOS quite heavily over the past few years and have a serious dislike of the amount of options you'll get with KDE, I went with Gnome. It provides me with loads of usable space, quite a big set of possible (third party) extensions and loads of built-in integrations (entire Google toolset, Microsoft Exchange, Nextcloud etc.) that I'll probably never use. I've made some minor adjustments but it's mostly the out of the box experience and I've been liking it so far.

To improve my workflow, I've added some Gnome extensions, though. On my Macbook, I frequently used Magnet for window "snapping" and making sure all my applications are set to their correct corner of the screen. Also, by default Gnome doesn't provide you with a battery time indicator, thus having to rely solely on an icon with a percentage next to it. These issues have been covered by using [gTile](https://extensions.gnome.org/extension/28/gtile/) and [Battery Time](https://extensions.gnome.org/extension/5425/battery-time/) respectively. For the former, I've set up a solution similar to Magnet's corner snapping by using CTRL+SUPER+[u, i, j, k] for the four corners of the screen. Any other location on the screen is handled by the built-in Gnome window snapping functionality of SUPER+[arrow keys].

## Daily tools & software
Apart from previously using MacOS, I'd also been using several tools that were MacOS-only and thus had to be replaced by something similar; preferrably tools that are managed through my package manager. For each of these tools, having a separate version for MacOS or Windows as well would be the cherry on top. This is the list of tools & applications I'm currently using in my day-to-day work:

 * Firefox - The best browser that isn't built by Google
 * Gnome Terminal - Built-in terminal for Gnome that suits my needs just fine
    * Oh-my-zsh - Extension that adds useful information to my prompt, e.g. git status, kubernetes context & namespace, AWS region etc.
 * Docker - Containerizing everything since 2013
 * minikube - Running an entire single-instance Kubernetes cluster locally can be vital for quickly checking functionality. Also, when testing something locally I'm eventually left with a reusable config file for running the same software on an actual Kubernetes cluster.
 * [Terraform](https://www.terraform.io/) - Simply the best IaC tool that's currently available
 * [CDK](https://aws.amazon.com/cdk/) - One of the IaC tools ever, second best IaC tool available on the market if you like restricting yourself to most AWS services (and nothing else) or love Cloudformation templates.
 * [Logseq](https://logseq.com/) - In my opinion the best solution for [documenting your work and life.](/posts/documenting-work-and-life-with-logseq) Can be extremely addicting as you're trying to expand your graph to link to more and more stuff, eventually resulting in your own, local version of Wikipedia.
 * VS Code - I love coding, I love extensibility, I love VS Code.
    * Extensions:
        * JavaScript and TypeScript Nightly
        * YAML
        * Rainbow CSV
        * Dev Containers
        * Docker
        * Even Better TOML
        * Go
        * indent-rainbow
        * Kubernetes
        * Python
 * Ferdium - Free, open source version of Franz. Used to combine all my messaging tools into one application (Whatsapp, Google Chat, Slack)
 * [Feeds](https://gfeeds.gabmus.org/) - Simple, easy to use RSS reader with the option to show the entire page in-application whilst others only show a title and summary with a link to said post.
 * [Special mention: WineGUI](https://github.com/winegui/WineGUI) - As I've ran into some problems with runnning Windows-only applications (or some older games that aren't on Steam), I've looked into an easier way of handling Wine setups. WineGUI is a really simple but insanely powerful GUI for Wine.

As you can see, this list is short and simple. I don't need much to do my work - 50% of it is browser based anyways. Of course this will change over time, as needs arise or I find other applications, tools or extensions that are to my liking. Still, I find that I can work quite comfortably with nearly the same efficiency as I had on my Macbook Pro whilst keeping the costs down and making it easily possible to reinstall the system without much downtime.

## Also... Gaming
Oh yeah, I do some gaming from time to time as well. I've created a dual boot with Windows 11 and have booted into that once or twice in the last couple of months to play a game that couldn't run on Linux. It's a bare bones installation without any modifications from my side. I've installed my drivers, downloaded Steam and started playing. Hopefully that's all I'll ever have to do with Windows in the coming years.