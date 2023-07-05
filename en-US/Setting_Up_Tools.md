---
published: true
layout: bookpage
weight: 500
outlevel: 5
category: Setting Up Tools
title: Setting Up Tools
---

Our projects use a consistent set of libre/open tools for modifying, building and testing fonts. We call this software collection our toolchain. To rebuild our fonts yourself, the easiest will be to use the same toolchain and workflow we use. But since we use open formats, you should be able to use the various source files with other tools as well, although you will have to rely on your own experience and on documentation available outside of this guide for the practical details.

To allow for easier installation, use and update of the various software tools which form part of the [smith] toolchain, we use a container (a container is a lightweight version of a virtual machine). This container is currently based on [Ubuntu](https://www.ubuntu.com/){:target="_blank"} 22.04 LTS (Jammy) and uses the [Docker] technology. This enables us to spin up a new, separate, Ubuntu-based environment in a container without any risk to the host computer. For the toolchain to be accessible and be allowed to run on the shared font folder files, Docker will need to run as a background service. 

The process of setting up the smith toolchain on your own computer involves:

A. Installing Docker

B. Installing WSL for Windows users 

C. Installing anvil 

D. Setting up a font projects folder

E. Configuring anvil 

F. Using and managing the container with anvil 


Please bear in mind that __the container is fairly large (over 500 software components for both base OS and toolchain: a total of about 1.6 GB uncompressed)__, so it will require a __comfortable unmetered network connection__ to download everything the first time as well as subsequent updates. The image is compressed so should usually take under 3 minutes to download. It's not immediate, but it sure beats having to install and upgrade every single component manually!

## Step A: Installing Docker 

To install Docker, go to [Docker.com](https://www.docker.com){:target="_blank"}

- Download the 64-bit Docker installer for your target host OS (and type of CPU).  
- Run the installer. You may also need to reboot and authorize the background service.

## Step B: Installing WSL for Windows users

*(If you are using macOS or Ubuntu, you can skip this step and go directly to [Step C: Setting up a font projects folder](#step-c-setting-up-a-font-projects-folder))*

Unlike macOS and Ubuntu, Windows does not come with some of the basic command-line tools installed by default but, thanks to the recent introduction of [WSL (Windows Subsystem for Linux)](https://learn.microsoft.com/en-us/windows/wsl/), this has improved a lot. Windows users should install WSL to use a command-line environment. The native Windows shell (cmd) and the native Windows filesystem are currently too slow for Docker so we use WSL instead. 

Launch the Windows command prompt (or type: `cmd`)

Type the following to install WSL:
`wsl --install -d Ubuntu-20.04`

After granting permissions and rebooting, your computer will prepare the WSL VM (Virtual Machine) and ask you to pick a username and password. Make a note of both, especially the password which you will need to use again. 

In the Docker settings available from the system tray menu (look for the icon of a whale carrying containers on its back) or by clicking on the gears icon in the Docker dashboard, you will need to make sure that this newly created VM is selected as the one integrated by default. Under Resources -> WSL Integration, make sure that "Enable integration with my default WSL distro" is ticked and that the sliding button next to Ubuntu-20.04 is set to on (blue rather than gray). Now press the "Apply and Restart" button. 

Windows users need to go through the extra steps described in [Configuring WSL].

## Step C: Setting up a font projects folder

We recommend that you set up a dedicated font projects folder: *~/repos/wstechfonts/*. And that however many projects you work on they are checked out as subfolders in that main folder. This makes it easy to use a single container configuration for multiple projects. You do not need to run a container for each project at the same time. __Further steps and examples in this guide will assume that you have set up this folder.__  Type:

`mkdir -p ~/repos/wstechfonts`


## Step D: Installing anvil 

The easiest way to interact with this Docker container is via a separate utility called [anvil](https://github.com/silnrsi/anvil). _It's named after the solid tool the smiths use to repeatedly hammer on when working in their forge_. Anvil is a frontend to Docker compose and reads a configuration file available from its own github project repository. This makes it simpler to run the container with dedicated targets. It saves you from having to remember all the many underlying details of Docker and Docker compose. It basically acts as a simple Vagrant replacement. 

### Checking out the anvil repository 

Open your Terminal app (Windows users need to type `wsl` as an added step to get into the VM) and type:

`cd ~/repos` 

`git clone https://github.com/silnrsi/anvil` 

### Installing anvil in the path 

In your Terminal app type: 

`mkdir -p ~/bin`

`cp ~/repos/anvil/anvil ~/bin/anvil`

`chmod +x ~/bin/anvil`

You can also install the bash completion script to more easily tab through the various anvil subcommands (_on Windows/WSL, it will ask you for the password you set at the creation of the VM earlier_):
`sudo cp ~/repos/anvil/bash_completion_anvil /etc/bash_completion.d/anvil` 

Exit the terminal by typing: 

`exit` 

or just close the Terminal app. 


## Step E: Configuring anvil  

When you add anvil to your path, it will look for the configuration file in *~/repos/anvil/docker-compose.yml* by default. This file contains all the necessary configuration fields including where to find the image, the shared folder path, memory allocation, etc. You can adjust the default values if your specific needs are different but they should work as is. 


## Step F: Using and managing the container with anvil 

To spin up a container, simply type in your Terminal:

`anvil up`

If a more recent Docker image has been produced on the remote server, it will also fetch that new image and use it to spin up a new container. If the base image is current then it will use that to spin up a new container. 

To remove/destroy a container, but without touching any of the work files shared on the host computer, type:

`anvil down`


### Using the container

After the container is configured and working, the day-to-day usage goes like that:

To get into the container and access the toolchain inside simply type:

- `anvil ssh`

The command prompt should change to show you the minimal information needed: a whale as the Docker symbol, the current absolute path and a timestamp.

```🐳  /smith  
(Mon June 26 08:01:38) ❯```

- Make any changes you want - see next section on [Building Font Projects](Building_Font_Projects.html)
- When done, type: `exit`
- Wait until the prompt changes back to your usual Terminal on the host computer  

### Maintaining the container and keeping it up-to-date 

The container is made of various components which are being improved and worked on regularly. You don't need to be running the bleeding edge constantly, but it's good to stay somewhat current with new bugfixes and extra features. Since you are not building any of the components locally on your own computer but you are getting a pre-built image, it is now much faster. Running `anvil up` will automatically get the latest version of everything already compiled and properly installed. Currently, new images are rebuilt on the server every week on Monday morning (at 00:00 UTC time). 

Since spinning up a new container is fairly quick, usually under a minute, it's OK to do `anvil up` and `anvil down` fairly regularly. It's up to you (and the CPU and memory resources of your computer) if you want to leave the container running and just find it when you get back to your computer again or if you'd rather spin it down to free up those resources.  

If you want a persistent container to make local changes to the toolchain (like adding a new library or utility) and find everything again the next time you get into the container, then use `anvil up` then `anvil ssh-dev` ("dev" stands for development). 

`anvil clean` removes the existing containers, images and entire build cache. Only use this if you need a clean slate with the whole toolchain.   

`anvil when` tells you how old your container is

`anvil status` gives you status information

`anvil --help` or `anvil` gives you a usage summary of all the targets





[Docker]: https://www.docker.com 
[smith]: https://github.com/silnrsi/smith 
[Configuring WSL]: Configuring-WSL.html
[Building Font Projects]: Building_Font_Projects.html
