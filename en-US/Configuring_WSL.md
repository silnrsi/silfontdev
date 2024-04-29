---
published: true
layout: bookpage
weight: 600
outlevel: 6
category: Configuring WSL 
title: Configuring WSL 
---

*This section is only for Windows users. If you are using macOS or Ubuntu you can skip this entire section and go back to [Setting up Tools - Step D: Installing anvil](Setting_Up_Tools.html#step-d-installing-anvil)* (or go directly to [Building Font Projects](Building_Font_Projects.html) if anvil is already installed). 

Now that WSL is fully installed, we can configure various aspects like the shared project folder and the settings of the git GUI.  

Because of current performance issues with native Docker on Windows filesystem, we need to store the font project sources inside the WSL VM. We will create a shared folder repository inside the VM and point our toolchain to it. 


## Adjusting the resources allocated to WSL in Windows

By default Windows automatically allocates resources to the WSL VM, but you can adjust these settings by dropping this [.wslconfig configuration file](https://github.com/silnrsi/anvil/blob/main/.wslconfig) into *%USERPROFILE%* (or *C:\Users\username\.wslconfig* where *username* is your Windows username).
You can adjust the defaults settings to the specific resources available on your computer. 

## Setting up a fonts project folder

We recommend that you set up a dedicated font projects folder - *~/repos/wstechfonts/* - and that each font project has its own folder within the dedicated folder, such as *~/repos/wstechfonts/font-project-name*. This makes it easy to use a single container configuration for multiple projects. You do not need to run a separate container for each project. __Further steps and examples in this guide will assume that you have set up this folder.__

To get into the WSL VM, launch your Terminal app (cmd) and type:

`wsl` 

Then inside the VM, type:

`mkdir -p ~/repos/wstechfonts`

Don't check out any repositories into the new folder yet. There are some further configuration steps that need to be completed first.

## Mapping the WSL virtual disk to a Windows drive letter

The contents of the WSL VM are visible in the Explorer tree structure but we are going to map it to a Windows network drive. This is needed because most Windows apps don't know how to browse to the special folders inside the WSL VM, but when they are mapped to a drive, they can find them and use them.

- In the Navigation Pane of Windows File Explorer, scroll down to the Linux section and right-click on the Ubuntu-24.04 entry
- Select "Map Network Drive" then select W:  (W for WSTech or WSL) check that it’s set to “Reconnect at sign-in” and then press Finish
- Select that drive (Ubuntu-24.04 or W:) in the Navigation Pane, right-click and choose "Pin to Quick Access". Alternatively you can type: `\\wsl$`  (or `\\wsl.localhost` ) in the address bar to access it directly.


### Setting Sourcetree options and git configuration

Because the git index is handled differently between Windows and Ubuntu you should only use the GUI version of git and not the command-line version inside your VM or your container. Many Windows users like [Sourcetree] as a friendly no-cost git GUI for Windows. 

We need to adjust Sourcetree's configuration so that git does not get confused by the shared filesystem in WSL and also ignores the executable flags set for certain scripts (as the Windows filesystem cannot currently represent that). *It’s important to do this before checking out any repositories!* If Sourcetree is constantly asking for your credentials, you should make sure you have the [Git Credentials Manager] installed and that in *Tools -> Options*, in the Git tab, the option "Allow Sourcetree to manage my credentials via the Git Credentials Manager" is ticked. 

In Sourcetree, make sure the following settings are set in *Tools -> Options*, in the Git tab
tick "Use git bash as default terminal".

Under Git Version check that "Embedded" is chosen (the button should look light gray and pressed down).

We need to further adjust certain git configuration items because the git font projects sources are stored inside the VM filesystem. Open a Terminal window from inside Sourcetree by going to *Action -> Open in Terminal* then type:

`git config --global --add safe.directory "*"`

`git config --global core.autocrlf false`

`git config --global core.filemode false`

Double-check the current configuration by typing:

`git config --list --show-origin`

The *~/.gitconfig* file inside your Windows user profile directory (accessible directly via *%USERPROFILE%* and not the Ubuntu VM inside WSL should have the following lines. Type this to open that file and verify its contents:

`wsl`

`cd ~`

`editor /mnt/c/Users/username/.gitconfig`

or

`editor C:\Users\username\.gitconfig`

(*username* is your Windows username and *editor* is your preferred editor, like VScode for example)

It should contain the following lines:

```[core]
autocrlf = false
filemode = false 
[safe]
directory = *```

Then close that terminal/command prompt window.


### Clone/checkout and adjust individual projects in Sourcetree

If you have existing project repositories on your local machine, it is important to reclone your projects with Sourcetree rather than manually copying them over. 

Clone the project with Sourcetree and set the Destination path to W:

```\home\username\repos\wstechfonts\font-andika-mtihani```

(change *username* to correspond to the username chosen when WSL first set up Ubuntu)

IMPORTANT: because of Sourcetree limitations related to Windows and the WSL filesystem, you need to run the *fix-git-execute-bits-scripts* after you clone a repository to restore the executable bit on certain files, so you can run the various preflight and preglyphs scripts, and any other scripts you may have in tools/. The *fix-git-execute-bits-scripts* script is already part of the Docker image. For example, type: 

`anvil up`

`anvil ssh`

`cd ~/repos/wstechfonts/font-andika-mtihani`

`fix-git-execute-bits-scripts`

IMPORTANT: when copying new scripts into your own project, like *makedocs* from the [fontdocs] project, make sure you keep the execute bit or re-apply it afterwards by typing:

`git update-index --chmod=+x makedocs`

and then committing the change.

Now that the Windows/WSL-specific set up is done, you can go back to the main documentation and follow the common steps there:
[Setting up Tools - Step D: Installing anvil](Setting_Up_Tools.html#step-d-installing-anvil).

[Sourcetree]: https://sourcetreeapp.com/
[Git Credentials Manager]: https://github.com/git-ecosystem/git-credential-manager
[fontdocs]: https://github.com/silnrsi/fontdocs
