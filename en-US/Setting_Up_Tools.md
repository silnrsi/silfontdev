---
published: true
layout: bookpage
weight: 500
outlevel: 5
category: Setting Up Tools
title: Setting Up Tools
---

Our projects use a consistent set of free tools for building and modifying fonts. To build our fonts you will need to use the same toolchain and workflow we use.
To allow for easier installation, use, and management of the various software tools which form part of the toolchain, we use a Virtual Machine (VM). This VM is currently based on [Ubuntu] 16.04 LTS (Xenial). *There is ongoing work happening on a newer version based on Ubuntu 18.04 LTS (Bionic) and python3 but it's not fully ready yet. Stay tuned. It is also possible to separately install required packages directly on a linux-based OS, but that is not covered in this guide.*

The process of setting up the toolchain involves:

- Installing Virtualbox and Vagrant
- Setting up a font projects folder
- Configuring Vagrant
- Running Vagrant for the first time - to download and install required tools

Please bear in mind that __the toolchain is fairly large (over 500 software components for both base OS and toolchain: a total of about 2 Gb)__, so it will require a __comfortable unmetered network connection__ to download both the base image and the various components on top of that. Even on recent hardware and with a decent network connection it's likely to take __more than 20 minutes__ to download and install everything. But it sure beats having to install everything manually.

## Step 1: Install Virtualbox and Vagrant

Virtualbox enables us to spin up a new, separate, linux-based environment in a guest VM without any risk to the host computer or the files we are working on. To install Virtualbox:

- Download the [Virtualbox installer] for the preferred host OS. __Please stay with version series 5.2 for now__.
- Run the installer. You may also need to reboot.
- Install the corresponding Extension Pack.

We use Vagrant to automatically drive Virtualbox and make handling of our VM much simpler, less manual and less error-prone. To install Vagrant:

- Download the [64-bit Vagrant installer] for the preferred host OS. 
- Run the installer. You may also need to reboot.

## Step 2: Set up a font projects folder

We recommend that you set up a dedicated font projects folder (such as *Documents/work/fonts/*). This makes it easy to use a single VM configuration for multiple projects. __Further steps and examples in this guide will assume that you have set up this folder.__

## Step 3: Configure Vagrant

Our particular Vagrant VM configuration is defined by two files available from our Smith project github repository. Download these two files and put them into your font projects folder (*Documents/work/fonts/*). The easiest way to do that is to right click on the following links, and choose "Save Link As..." or "Download Linked File As...":

- [Vagrantfile] (be sure to save the file as "Vagrantfile" not "Vagrantfile.txt")
- [provision.sh]

## Step 4: Run Vagrant

The first time you run Vagrant it will automatically:

- Download all the required software components
- Install them in a fresh VM
- Set up shared folders to provide access to everything in your font projects folder
- Enable you to control the VM through a local ssh connection

To run Vagrant use the terminal to navigate to your font projects folder (*/Documents/work/fonts/*) and type:

> `vagrant up`

*Note that this first-time run will take a while - typically 20 minutes or more - while it "provisions" (configures) the VM. Time to grab a cup of tea or coffee...*

While it's installing everything you'll notice hundreds of lines of commands and messages. There may even be warnings among the messages. As long as the final message isn't a bright red warning, and you see the message "smith is now ready to use" you're probably fine.

After the provisioning is complete, briefly test the VM by connecting with it through ssh:

> `vagrant ssh`

The command prompt should change. Then navigate to your font projects folder, which in the VM is mapped to */smith*:

> `cd /smith`

Then leave the VM:

> `exit`

Shut down the VM:

> `vagrant halt`

If at any point in this something doesn't work, then the Vagrant provision may have failed at some point. In that case, be sure to `exit` the VM then run the following to try the provisioning step again:

> `vagrant provision`

### Video walkthrough

Here is a video that shows some of the installation process but skips some of the longer steps. Watch it full screen for more legibility. 

<video src="../assets/videos/setting-up-tools.webm" width="90%" height="90%" controls preload></video>

## Using the VM

After the VM is configured and working, the normal process of using it is to:

- Navigate to your font projects in the terminal
- `vagrant up`
- `vagrant ssh`
- Wait until the prompt changes
- `cd /smith`
- (do whatever you're wanting to do - see next section on [Building Font Projects])
- When done, `exit`
- Wait until the prompt changes back
- `vagrant halt`

## Maintaining the VM and tools

Normally the VM only needs to be updated if there is a particular feature or bug fix in a newer version of the tools that you want to use. Running `vagrant provision` will automatically get the latest versions of everything already installed. *However be aware that newer versions may potentially cause problems, so tread carefully!*

If you want to configure a new VM, or get the latest set of tools (for example, if we've added new tools needed for some project), then you'll need to go back to Step 3 above. BTW - `vagrant destroy` will delete the VM but not any of the work files shared on the host computer.

## Technical notes on Vagrant

*These are only for those that want to customize or tweak their setup and can safely be ignored by others!*

The vagrant profile will automatically set up shared folders, so the VM will see the files inside the folder from which you've run Vagrant (typically your font projects folder - *Documents/work/fonts/*. You can adjust this by editing the Vagrantfile to your liking.

Vagrant stores certain files in a *.vagrant/* subfolder on the host computer. _Remember that if we rename or move that subfolder or the whole parent folder in the course of working on the project, vagrant won't be able to find the path to the VM again and we may have to spin up a new VM._ The actual Virtual Machine configuration and disk images are stored in *~/.Virtualbox/*.

Watch the command-line output as it automatically downloads, sets up the base VM (also called a box in Vagrant jargon) then runs the provision.sh script which contains instructions on what to install and from where. You can open the provision.sh script in your preferred text editor to see what it does. 

It is also possible to update the VM components separate from running `vagrant provision`. From the command prompt inside the VM run:

> sudo apt-get update -y -q
>
> sudo apt-get upgrade -y -q -o Dpkg::Options::="--force-confdef" -o Dpkg::Options::="--force-confold" -o Dpkg::Options::="--force-overwrite" -u -V --with-new-pkgs

[Ubuntu]: https://www.ubuntu.com/
[Virtualbox installer]: https://www.virtualbox.org/wiki/Downloads
[64-bit Vagrant installer]:  https://www.vagrantup.com/downloads.html
[Vagrantfile]: https://github.com/silnrsi/smith/raw/master/vm-install/Vagrantfile
[provision.sh]: https://github.com/silnrsi/smith/raw/master/vm-install/provision.sh
[Building Font Projects]: Building_Font_Projects.md
