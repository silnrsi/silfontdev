---
published: true
layout: bookpage
weight: 600
outlevel: 7
category: Modifying Font Sources
title: Modifying Font Sources
---



### Design and GUI-driven changes ###

Currently, we recommend the [Glyphs](https://glyphsapp.com/) font editor to take care of the design side of font creation. 
It is a closed-source macOS-only tool but thankfully there is a open cross-platform python library called [glyphsLib](https://github.com/googlei18n/glyphsLib) with read and write support for the native source format of Glyphs, the .glyphs file. 

To load the current font sources into Glyphs we need to use a script that will synthesize a temporary .glyphs file from the existing UFO sources and the corresponding designspace. That script is called __preglyphs__. 

To run it, we open the terminal in the folder of the font project's local working copy and type: 

> ./preglyphs 

Then we open the .glyphs file that was generated in Glyphs in the __source/__ folder. 

After having made any desired changes, we save this .glyphs file, then we can run another script also located at the root of the font project by typing: 

> ./preflightg

This will propagate the changes back into the UFOs, normalize the UFOs, and sync/propagates metadata. This is why it's called preflight, typically being run this before more manual testing locally and before committing and pushing a public change (the final g stands for Glyphs). We can set the preflightg script to _check mode_ to flag well-known errors, we can also set it to _fix mode_ where it will apply fixes to well-known errors. 

If we don't have Glyphs available we can still run a similar script: 
> ./preflight 

These scripts are fairly simple bash scripts specific to each project to run tools to provide normalization or similar data manipulation of the font sources, we can open them in our favorite text editor to see what they actually do, which utility is being called with which parameter. Both preglyphs and preflight will generate output messages and logs files that we probably want to pay attention to. 

Then we can then go back to building the font to see our changes and to test them. 

_Other font editors who provide good support for the UFO3 format directly are [RoboFont](https://robofont.com/), [FontForge](http://www.fontforge.org/), or [TruFont](http://trufont.github.io/)._

(more details later on using other font editors to do a similar roundtripping from UFO3).


### Text editor-based font engineering changes ###

We can just make changes directly with our favorite text editor. 

Then we can then go back to building the font to see our changes and to test them. 

(more details on this later).

### Development name and font derivative renaming ### 

Please remember that we probably need to pick a name for q derivative so as not to collide with the existing namespace of the font we are deriving from. This name cannot be a reserved font name that is already declared in the font that we're modifying, in the case of Andika-Mtihani we can't use Andika or SIL. But we can pick something creative. We can just choose a development name that is not the name that we intend to have end-users recognize and see in their font menu.





