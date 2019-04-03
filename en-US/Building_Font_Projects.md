---
published: true
layout: bookpage
weight: 600
outlevel: 6
category: Building Font Projects
title: Building Font Projects
---

Once the VM is configured, provisioned, and working, you're ready to start building fonts!
*This assumes that you have completed all four steps in [Setting Up Tools].*

Here is a walkthrough of how to download one of SIL's font projects and build it locally. The main tool used to run the process is [Smith], a Python-based tool for building, testing, and maintaining fonts and other writing system implementation components. It orchestrates and integrates various tools and utilities to make a standards-based open font production workflow easier to manage. 

## Check out a font project repository

On your local machine (not in the VM) navigate to your font projects folder (typically *Documents/work/fonts*) and check out the font repository, as in this example using[Andika Mtihani]:

> `git clone https://github.com/silnrsi/font-andika-mtihani`

This will checkout a local working copy of the git repository into a *font-andika-mtihani* folder within your font projects folder. You can also use a GUI client for git to do this if you prefer that method.

## Start the VM and navigate to the project folder

Start up the VM and connect to it via ssh

> `vagrant up`  
> `vagrant ssh`

Navigate to the newly checked out repository:

> `cd /smith`  
> `cd font-andika-mtihani`

## Build using Smith

Configure Smith if this is the first build for this project in your VM. This checks to see if all needed tools are installed:

> `smith configure`

Build the fonts:

> `smith build`

Run the whole test suite:

> `smith alltests`

There are times, especially if you've changed the project *wscript*, when you need to wipe the results clean of any temporary artifacts. If at any time you want to start with a fresh build, run:

> `smith distclean`  
> `smith configure`  
> `smith build`

## Review build results

By default the build results will be in a *results/* folder inside the project folder (*font-andika-mtihani/results/*). You can simply browse through these files on your host computer.

## Build release packages

Smith also supports building both development and release versions of release archives in .zip and .tar.xz formats. These contain the fonts and key user documentation.

The following commands will produce development versions of the current work. "zip" is the Windows-targeted artifact with Windows line-endings and "tar.xz" is the macOS/Linux-targeted artifact with Unix line-endings. The current git hash and a -dev suffix will be added to the name of the artifacts to help distinguish development vs. released versions: 

> smith zip 

> smith tarball

To produce release versions of the current work without the git hash and -dev suffix, both in "zip" and "tar.xz" formats, type: 

> smith release

## Video walkthrough

Watch this  full screen for more legibility. 

<video src="../assets/videos/building-font-projects-steps.webm" width="90%" height="90%" controls preload></video>

## Understanding Smith

*For those of you wanting to know more about [Smith]:*

Building a font involves numerous steps and various programs, which, if done by hand, would be prohibitively slow. Even working out what those steps are can take a lot of work. Smith uses a dedicated file, based on python syntax, at the root of the project - the *wscript* file - to allow the user to describe how to build the font. By chaining the different build steps intelligently, Smith reduces build times to seconds rather than minutes or hours, and makes build, test, fix, repeat cycles very manageable.

By making these processes repeatable, including for a number of fonts at the same time, projects can be shared with others simply, or - better yet - they can be included in a CI (Continuous Integration) system. This enables fonts to be developed using libre/open source software tools and open, collaborative methodologies.

The toolchain components (Smith itself and all the various components) are all open and do not place any undue restricted licensing requirements on the user or developer. You can run it on any system via a VM, and you can run it on a Continuous Integration (CI) server as well. You are welcome to copy the whole VM to other computers or share it with colleagues and friends without restrictions. 

[Setting Up Tools]: Setting_Up_Tools.md
[Smith]: https://github.com/silnrsi/smith
[Andika Mtihani]: https://github.com/silnrsi/font-andika-mtihani
