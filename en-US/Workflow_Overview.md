---
published: true
layout: bookpage
weight: 400
outlevel: 4
category: Workflow Overview
title: Workflow Overview
---

This is a general overview of the workflow.

## Initial setup (one-time)

- Install and configure Docker and anvil 
- Set up a font projects folder and clone projects of interest

These steps are covered in [Setting Up Tools]. 

## Daily routines

- Start up Docker and the container (`anvil up`)
- Navigate to the project folder
- Pull any changes others have made to the project 
- Change things! Some ways to do that:
    - Manually edit files using a text editor
    - Run scripts to make changes
    - Run the *preglyphs* script to create a Glyphs file that can be edited
    - Open the UFOs directly in other apps (Robofont, FontForge, FontLab)
- Save and normalize your changes
    - Run *preflight* scripts (including *preflightg*, *preflightff*, *preflightfl*)
- Use *Smith* commands to:
    - Clean and configure the build folder
    - Build the fonts
    - Prepare test files
- Review the results (in `/results`)
- Commit your changes locally then push them to the main project
    - You may need to issue a pull request if it's not your project
- Exit the container and shut it down (`exit` and `anvil down`)

See [Modifying Font Sources] and [Building Font Projects] for details.

## Preparing a font release

- Modify the project metadata to reflect the release, including font version number
    - In the UFOs (fontinfo.plist)
    - In the FONTLOG.txt
- Adjust any other documentation
- Tag the last commit to reflect the release version
- Build the fonts using `smith zip`, `smith tarball`, or `smith release`
- Make a release on Github, uploading the release package from `results/releases/`

## Contributing back to the project

- Contact the project maintainer to indicate your interest in contributing back to the project
    - You may need to agree to a CLA (Contributor License Agreement)
- Issue a pull request containing your changes
- Adjust your submission as needed until it is accepted!

Read [Contributing Changes] for more information.

[Setting Up Tools]: Setting_Up_Tools.html
[Modifying Font Sources]: Modifying_Font_Sources.html
[Building Font Projects]: Building_Font_Projects.html
[Contributing Changes]: Contributing_Changes.html
