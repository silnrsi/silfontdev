---
published: true
layout: bookpage
weight: 100
outlevel: 1
category: Introduction
title: Introduction
---


This site has been set up as a step-by-step guide to building, modifying, and contributing to [SIL International font projects](http://software.sil.org/products/#fonts). It's definitely a work-in-progress. Our first priority is to document what is needed to get the basic workflow going, this rest of the content will be fleshed out later on.

The font we will use as our practical example throughout this guide is [Andika-Mtihani](https://github.com/silnrsi/font-andika-mtihani). This font project is specifically designed to be an ongoing testbed for current open workflow best practices.
 
In this guide we assume:
- we have access to a computer running either macOS, Windows or Ubuntu where we already have or can install the following software: Virtualbox, Vagrant, Bash and Git.
- we are familiar with the basics of using the terminal (or command-line). There is no graphical interface available for using the various tools *(simple cut and paste instructions will be available though, don't worry)*. 
- we'll use a Virtual Machine (VM) to install the various software components needed on the computer. Using a VM allows for easier installation, update and management of the various tools we need, we can spin up a new separate environment in a guest VM, snapshot it, remove it and start from scratch without any risk to the host computer or the files we are working on. [Ubuntu](https://www.ubuntu.com/) is very well-suited to this task. We are currently using Ubuntu 16.04 LTS (xenial). *(There is ongoing work happening on a newer version targetting Ubuntu 18.04 LTS (bionic) and moving to python3 but it's not fully ready yet. Stay tuned).*
- we approach font design and engineering like a libre/open source software project, with a set of recommended best practices to enable collaborative work with others on the publicly accessible font sources. Andika Mtihani, along with all the fonts designed and produced by SIL, is released under the [SIL Open Font License](https://scripts.sil.org/OFL) (we strongly recommend browsing through the current [FAQ](https://scripts.sil.org/ofl-faq_web) for more practical information). The font sources are set up to use [smith](https://github.com/silnrsi/smith), our open font development toolchain. We can, of course, use this for other font projects - either restricted or open - but this guide will focus on working in the open with the Andika Mtihani font as our example. 

Please bear in mind that __the toolchain is fairly large (over 500 software components for both base OS and toolchain: a total of about 2 Gb)__, so it will require us to have a __comfortable unmetered network connection__ to download both the base image and the various components on top of that. Even on recent hardware and with a decent network connection it's likely to take __more than 20 minutes__ to download and install everything. But it sure beats having to install everything manually. 

A mention of this guide with a link in a CONTRIBUTING.md (or equivalent file) in a project repository is probably worthwhile. 

*&mdash; The SIL International Writing Systems Technology Team [Contributors]*

[on GitHub]: {{site.repourl}}
[Contributors]:../AUTHORS.txt
