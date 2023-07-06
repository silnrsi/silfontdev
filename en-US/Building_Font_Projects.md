---
published: true
layout: bookpage
weight: 700
outlevel: 7
category: Building Font Projects
title: Building Font Projects
---

Once the container is up and running, you can log into it and see your shared font project files as shared from the host into the guest. This means you're ready to start building fonts!
*This assumes that you have completed all the steps in [Setting Up Tools].*

Building a font involves numerous steps using various programs, which, if done by hand, would be prohibitively slow. Even working out what those steps are can take a lot of work. By making these processes repeatable, including for a number of fonts at the same time, projects can be shared with others simply, or - better yet - they can be included in a CI (Continuous Integration)   system. This enables fonts to be developed using libre/open source software tools and open, collaborative methodologies.

The main tool used to run the process is [Smith], a Python-based tool for building, testing, and maintaining fonts. It orchestrates and integrates various tools and utilities (many written in Python) to make a standards-based open font production workflow easier to manage. Smith uses a dedicated file, based on Python syntax, at the root of the project - the *wscript* file - to describe how to build the font. By chaining the different build steps intelligently, Smith reduces build times to minutes rather than hours, and makes build, test, fix, repeat cycles very manageable.

The toolchain components (Smith itself and all the various components) are all open and do not place any undue restricted licensing requirements on the user or developer. 
 
Here is a walkthrough of how to download one of SIL's font projects and build it locally. 

*Note that this build process is not only for SIL font projects. It will work with any projects that use similar source formats, repository structure and the smith toolchain needed to set up the build according to the wscript file.*

## Checking out a font project repository

MacOS and Ubuntu users can navigate to the font projects folder (*~/repos/wstechfonts* by default) and check out a new font project repository, for example [Andika Mtihani]:

To get into the project font folder, type:

`cd ~/repos/wstechfonts`

`git clone https://github.com/silnrsi/font-andika-mtihani`

This will checkout a local working copy of the git repository into a *font-andika-mtihani* folder within your font projects folder which then will be available from inside the container. 

You can use a GUI git client if you'd like on macOS and Ubuntu to do this checking out.  But if you are using Windows, you must use a git GUI client (like [Sourcetree] for example) to do this and only that client. Using git on the command-line either in the VM or the container on the same project will change the index back and forth which will confuse either git client and result in making it extremely slow. 

## Starting the container and navigating to the font project folder

To start up the container, type:

`anvil up`  

to log into the container, type:

`anvil ssh`

To navigate to the newly checked out repository (by default the container opens a prompt in the */smith* folder which is where all your font projects should be shared from the host computer), type:

`cd font-andika-mtihani`

## Building and running test using Smith

Running the various smith targets assumes that your prompt shows that you are at the root of the font project like */smith/font-andika-mtihani*

To configure the project, this checks if all necessary tools are properly available, type:

`smith configure`

To build the fonts, type:

`smith build`

To run the whole test suite, type

`smith alltests`

To run the FontBakery checks (via the pysilfont profile), type:

`smith ttfchecks`

There are times, especially if you've changed the project *wscript*, when you need to wipe the results clean of any temporary artifacts, cache or config files. If at any time you want to start with a fresh build, type:

`smith distclean` 

Then to reconfigure and redo a fresh build, type:  

`smith configure`  

`smith build`

## Reviewing build results

By default the build artifacts will be stored in a *results/* folder inside the project folder (*font-andika-mtihani/results/*). You can simply browse through these files on your host computer with your preferred file manager.

## Building release packages

Smith also supports building release archives in .zip and .tar.xz formats, and in both development and release versions. These contain the fonts, author and licensing information as well as key documentation.

"zip" is the Windows-targeted artifact with Windows line-endings and "tarball" is the macOS/Ubuntu-targeted artifact with Unix line-endings and a .tar.xz extension. The current git hash (the current revision) and a *-dev* suffix will be added to the internal versions and the filenames of the artifacts to help distinguish between development vs. released versions. To produce development versions artifacts, type:

`smith zip`

`smith tarball`

To produce release versions, without the git hash and *-dev* suffix indicating a development version, both in zip and tar.xz formats, type:

`smith release`

## Debugging smith targets

If a smith step generates an error, and the existing logs don't help, you can increase the verbosity of that particular build step by typing, for example: (the more v added the more verbosity)

`smith build -vv` 

`smith pdf -vvv` 


[Setting Up Tools]: Setting_Up_Tools.html
[Smith]: https://github.com/silnrsi/smith
[Andika Mtihani]: https://github.com/silnrsi/font-andika-mtihani
[Sourcetree]: https://www.sourcetreeapp.com
