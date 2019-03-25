---
published: true
layout: bookpage
weight: 400
outlevel: 5
category: Setting Up Tools
title: Setting Up Tools
---

To allow for easier installing, using and updating of the various software tools which form part of the toolchain, we use a Virtual Machine (VM). This VM is based on [Ubuntu](https://www.ubuntu.com/). 

### Installing Virtualbox and Vagrant ###

We need to install Virtualbox from [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)
- Download the installer for the preferred host OS. (Please stay with version series 5.2 at this stage).
- Run the installer (we might have to reboot).
- Also install the corresponding Extension Pack.

We use Vagrant to automatically drive Virtualbox and make handling of our VM much simpler, less manual and error-prone.

We need to install Vagrant from [https://www.vagrantup.com/downloads.html](https://www.vagrantup.com/downloads.html)
- Download the 64 bits installer for the preferred host OS. 
- Run the installer (we might have to reboot).

### Understanding what Smith is and what it does ###

[Smith](https://github.com/silnrsi/smith) is a Python-based framework for building, testing and maintaining WSI (Writing Systems Implementation) components such as fonts. It is based on waf. Smith orchestrates and integrates various tools and utilities to make a standards-based open font design and production workflow easier to manage.

Building a font involves numerous steps and various programs, which, if done by hand, would be prohibitively slow. Even working out what those steps are can take a lot of work. Smith uses a dedicated file at the root of the project (the file is python-based) to allow the user to describe how to build the font. By chaining the different build steps intelligently, smith reduces build times to seconds rather than minutes or hours, and makes build, test, fix, repeat cycles very manageable. By making these processes repeatable, including for a number of fonts at the same time, projects can be shared with others simply, or - better yet - they can be included in a CI (Continuous Integration) system. This allows for fonts (and their various source formats) to truly be libre/open source software and developed with open and collaborative methodologies.

Smith is _Copyright (c) 2011-2018 SIL International (www.sil.org)_   
and is released under _the BSD license_.

Smith is developed and maintained by [SIL International's WSTech team](https://software.sil.org/wstech/).

The toolchain components (smith itself and the various components) are all open and do not place any undue restricted licensing requirements on the user or developer. We can run it on any system via a VM, and we can run it on a Continuous Integration (CI) as well if desired. We can copy the whole VM to other computers or share it with colleagues and friends without restrictions. 

#### Downloading the current smith vagrant profile ####

Download the current Vagrant profile from the smith github repository. The profile is just two files:
-  [Vagrantfile](https://github.com/silnrsi/smith/raw/master/vm-install/Vagrantfile)
-  [provision.sh](https://github.com/silnrsi/smith/raw/master/vm-install/provision.sh)

Download these two files and put them into the same parent folder of the font project folder: __Documents/work/fonts/__. (We do it this way so we can use the same VM for multiple font projects). 

Then check out the out Andika Mtihani git repository by typing:

> cd __~/Documents/work/fonts/__
>
> git clone https://github.com/silnrsi/font-andika-mtihani 

This will checkout a local working copy of the git repository in __~/Documents/work/fonts/font-andika-mtihani/__. (We can use a GUI client for git to do if needed).

#### Spinning up the profile and testing that it runs ####

Open this parent folder __Documents/work/fonts/__ in the terminal and type:

> vagrant up 

This will start spinning up the whole toolchain. 
Now is probably at good time to go grab a cup of tea or coffee...

Vagrant has a few subcommand which are pretty self-explanatory and useful to remember:
- __vagrant up__ spins up the profile by reading the configuration in Vagrantfile, then provisions the VM by running the provision.sh script
- __vagrant provision__ can be typed separately once the VM is running to have it re-run the installation steps and to get updates for example. 
- __vagrant ssh__ allows us to log into the VM so that we can run the various commands (see next section). 
- __vagrant halt__ stops the VM
- __vagrant destroy__ deletes the VM but not any of the work files shared on the host computer 

The vagrant profile will automatically set up shared folders, so the VM will see the files under the __Documents/work/fonts/__ folder on the host computer. We can adjust this in the Vagrantfile to our liking (and then type __vagrant reload__) but by default it shares the folder where it was launched it, in our case __Documents/work/fonts/__ on the host computer with __/smith/__ inside the VM. 

(Vagrant stores certain files in a __.vagrant/__ subfolder on the host computer. _Remember that if we rename or move that subfolder or the whole parent folder in the course of work on the project, vagrant won't be able to find the path to the VM again and we may have to spin up a new VM._
The actual Virtual Machine configuration and disk images are stored in __~/.Virtualbox/__.)

Watch the command-line output as it automatically downloads, sets up the base VM (also called a box in Vagrant jargon) then runs the provision.sh script which contains instructions on what to install and from where. We can open the provision.sh script in our preferred text editor to see what it does. 

Once the whole vagrant up process has finished (and "smith is now ready to use"), we can type __vagrant ssh__ to log into the VM. 

### Keeping the VM updated ###

Over the course of working with the VM, there will be updates to various components of the toolchain. These updates are not applied automatically. We can choose to apply them by typing inside the VM: 
> sudo apt-get update -y -q
>
> sudo apt-get upgrade -y -q -o Dpkg::Options::="--force-confdef" -o Dpkg::Options::="--force-confold" -o Dpkg::Options::="--force-overwrite" -u -V --with-new-pkgs

or by what telling Vagrant to reprovision (re-run the provision.sh script) by typing in the terminal on the host computer:
> vagrant provision


### Video preview of the steps ###

(The video skips some of the longer parts of the installation process).

Watch it fullscreen for more legibility. 

<video src="../assets/videos/setting-up-tools.webm" width="90%" height="90%" controls preload></video>




