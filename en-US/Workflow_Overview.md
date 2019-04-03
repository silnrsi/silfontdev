---
published: true
layout: bookpage
weight: 400
outlevel: 4
category: Workflow Overview
title: Workflow Overview
---

This is the high-level overview of the workflow and the various steps involved:

- installing the needed software to run Virtual Machines (VMs) (Virtualbox, Vagrant) if not already available
- checking out the desired upstream git repository to have a local working copy on the host computer
- spinning up a new VM with the whole [smith](https://github.com/silnrsi/smith/) toolchain inside (or launching the existing VM)
- updating that VM if necessary with desired new features or bugfixes
- opening the project folder on the host computer shared with the VM 
- from the command-line, logging into the VM to run smith targets (from inside the VM) on the font sources on the host computer
	- cleaning the working directory of previous builds and temporary files if any
	- configuring the project and checking if we have all the needed components
	- running the build
	- running the tests
	- generating a development zip and tarball
	- generating a release zip and tarball 
- going through the generated files (in the __results/__ folder) 
	- installing the freshly built fonts to allow for local testing
	- examining the test results and reports to track changes
	- examining any relevant log files for warnings and errors
- making a new change to the font sources (using tools like preglyphs to prepare a temporary file to load into the font editor)
- running preflight or preflightg (which includes various checks, can apply fixes and do normalization)
- launching another build with newly introduced changes
- browsing the results of that new build (in the __results/__ folder) 
- committing the change when satisfied 
- if the project is set up on a Continuous Integration (CI) service somewhere, comparing the results there as well






