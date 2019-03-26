---
published: true
layout: bookpage
weight: 500
outlevel: 6
category: Building Font Projects
title: Building Font Projects
---

Now that we have the whole toolchain installed, or in other words, that we have successfully done the first __vagrant up__, and we also checked that were able to log into that freshly created VM without issues, we can move on to building fonts. 

### Going through the build steps ###

- In the terminal, go the folder where Vagrant is set up, in our example in __Document/work/fonts__, which is a parent of  __font-andika-mtihani/__. 

to log into the VM and access the smith commands which will run on the source files in the shared folder, type: 

> vagrant ssh 

*(Logging into the VM is handled via a local network connection, the vagrant user and a private key . But it should all work automatically, there is nothing to set up or no passwords to type in)*

To change directories to get to our project folder, simply type: 

> cd /smith

> cd font-andika-mtihani 

to make sure no build artifacts or temporary files are left from previous builds, type:

> smith distclean

to configure the project, which also includes checking if we have all the necessary components, type:

> smith configure

to run the build itself, type:

> smith build

to run the whole test suite, type:

> smith alltests

to provide development versions of the current work ("zip" is the Windows-targeted artifact with Windows line-endings and "tar.xz" is the macOS/Linux-based artifact with Unix line-endings, the current git hash and a -dev suffix will be added to the name of the artifacts to help distinguish ongoing work vs. released font), type: 

> smith zip 

> smith tarball

to provide release versions of the current work (both in zip and "tar.xz" formats which the corresponding line-endings), type: 

> smith release 

### finding the generated files ###

We will see the results of the  various smith subcommands (or targets) in the form of generated files and log files in the __results/__ folder. We can simply browse through these files on the host computer. 

### Video preview of the steps ###

Watch it full screen for more legibility. 

<video src="../assets/videos/building-font-projects-steps.webm" width="90%" height="90%" controls preload></video>





