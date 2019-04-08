---
published: true
layout: bookpage
weight: 100
outlevel: 1
category: Introduction
title: Introduction
---


This site has been set up as a step-by-step guide to building, modifying, and contributing to [SIL International font projects]. It's definitely a work-in-progress. Our first priority is to document what is needed to get the basic workflow going, this rest of the content will be fleshed out later on.

The font we will use as our practical example throughout this guide is [Andika Mtihani]. This font project is specifically designed to be an ongoing testbed for current open workflow development.

In this guide we assume that you:

- have access to a computer running macOS, Windows, or Ubuntu where you already have or can install the following software: Virtualbox, Vagrant, Bash and Git. We are currently using a VM (Virtual Machine) based on Ubuntu 16.04 LTS (Xenial) - see [Setting Up Tools].
- are familiar with the basics of using the terminal (or command line). There is no graphical interface available for using the various tools. *Don't worry, simple cut and paste instructions will be available.*
- have some basic understanding of how to use distributed version control systems - [Git] and [GitHub] in particular. *If all you want to do is build fonts locally we'll provide the minimal info you need.*

We approach font design and engineering like a libre/open source software project, with publicly accessible font sources, build systems that use libre/open tools, and a consistent set of recommended best practices to enable collaborative work with others. The [Andika Mtihani] family, along with all fonts designed and produced by SIL International, are released under the [SIL Open Font License] (see the current [FAQ]).

We're in the process of adjusting all our active projects to use the workflow described in this guide, and encourage you to use it for your projects. You can then mention this guide in your documentation, such as a link in a CONTRIBUTING.md (or equivalent file) in a project repository. 

__To learn more about how our project sources are organized see [Source Formats].__  
<!--__To read a summary of our font development workflow see [Workflow Overview].__  -->
__To jump right into configuring your machine see [Setting Up Tools].__

*&mdash; [The SIL International Writing Systems Technology Team]*

[SIL International font projects]: http://software.sil.org/products/#fonts
[Andika Mtihani]: https://github.com/silnrsi/font-andika-mtihani
[Setting Up Tools]: Setting_Up_Tools.html
[Git]: https://git-scm.com/
[GitHub]: https://help.github.com/en#dotcom
[SIL Open Font License]: https://scripts.sil.org/OFL
[FAQ]: https://scripts.sil.org/ofl-faq_web
[Source Formats]: Source_Formats.html
[Workflow Overview]: Workflow_Overview.html
[The SIL International Writing Systems Technology Team]: ../AUTHORS.txt
