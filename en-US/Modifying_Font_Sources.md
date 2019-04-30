---
published: true
layout: bookpage
weight: 700
outlevel: 7
category: Modifying Font Sources
title: Modifying Font Sources
---

If you want to make modifications to our font projects you are very welcome to do so under the terms of the [SIL Open Font License]. Here is the workflow we use to develop and modify our fonts, with some tips for those of you wanting to redistribute modified versions (derivatives).

## Get the latest version and confirm that it builds for you

Before you begin making any changes, please be sure you have the most recent version of the source files. If you've just checked out (cloned) the project you will have the latest, however if it's been a few days (or months) be sure to update your local copy. In git terminology, be sure you 
"pull" changes.

## Change the font names

You will want to pick a new name for your modified font so it won't be confused with the original font. Almost all SIL fonts have [Reserved Font Names (RFNs)], so if you modify and redistribute the fonts you will need to pick a name that does not contain the RFNs. In the case of Andika Mtihani you can't use a name that includes "Andika" or "SIL". But you can pick something creative. IOW you can't modify Andika Mtihani and redistribute the modified version as "Andika Mtihani" or any name containing "Andika".

There are a few places where names appear in the source files and may need to be changed:

- OFL.txt — *copyright statement*
- FONTLOG.txt — *add information on your new derivative*
- UFO fontinfo.plist — *in many places!*
- Designspace files — *both sources and instances*
- Filenames

## Make changes

There are many ways to change the fonts:

- __Manually edit the files with a text editor.__ This is especially useful for metadata changes, such as those in the UFO fontinfo.plist and designspaces.
- __Use scripts to make changes__, such as those provided in [pysilfont]. This is useful for making changes that affect many files or glyphs.
- __Open the UFOs in GUI design apps__, such as [Robofont], [Glyphs], or [FontForge]. These require extra effort, as these apps tend to make massive changes to the fonts that have to be controlled and managed. In some cases, import/export can cause data loss, so be careful! See the section on *Using GUI design tools*, below.

__If you modify the fonts or related files you likely need to normalize the fonts before committing the changes to your repository - see next section.__

## Normalize and commit

The UFO3 source format is a bit unusual (and frustrating) in that it does not always specify how some bits of data are formatted (for example, integers or floats) or organized (for example, the sorting of keys in fontinfo.plist). Because of this, tools are free to interpret *and write out* the UFOs in inconsistent ways, making change tracking and version management difficult.

The solution is *normalization* - a process that formats and organizes UFOs in a consistent manner. Normalization can be done with a [pysilfont] command: [psfnormalize]. Our projects, however, have a very simple way to normalize all the UFOs in a project, synchronize the metadata between family members, and update the UFOs from auxiliary data — *preflight*.

Whenever you change anything in the project, start up your VM, `vagrant ssh` to connect with it, then navigate to the project folder and run:

> `./preflight`

This will get the UFOs back into a consistent format and isolate only the specific changes you've made. Then you can use a git client to review the changes and commit those you wish to keep.

*If you want to eventually contribute any changes back to the original projects your UFOs much be fully normalized and synchronized.*

## Using GUI font design tools

Many font design changes are best done with dedicated font design tools, such as [Glyphs]. All the major font design tools now support the UFO3 font format, however the level of their support differs greatly and each has some rough edges. The subsections below give specific guidance on using each tool successfully. *In some cases we don't yet have a well-tested and established workflow. We'll add details for each tool as we complete testing.*

There are some general principles to keep in mind when using font design apps with our projects:

- Consider app-specific file formats (.glyphs, .sfd, .vfb, etc.) as only temporary working files. It can be helpful to temporarily save into these formats, but always write out your changes to the UFOs.
- Don't commit app-specific files to the repositories. An exception to this is for archive sources stored in *source/archive/*. 
- Don't expect to be able to generate fonts from within the app and end up with fonts that work just like the originals. You will need to run our build process (using the VM and Smith) to rebuild the fonts.
- OpenType code can't be edited in these apps, as most of our projects maintain the OpenType code in .fea or .feax files outside the UFOs. Instead, edit the .fea/.feax files directly, run the build, and check the tests. That's not ideal but it is the only way to work around the pecularities of individual apps.
- Import/export with apps can cause data loss. The workflows described below attempt to minimize this, but be aware that it can occur.
- When committing changes to projects be selective about what you commit. You may need to ignore/discard changes that relate to specific app use. Selective commits can be a good workaround for app data loss!

### Glyphs

We currently use the [Glyphs] font editor to take care of the design side of font creation. It is a closed-source, macOS-only tool, but thankfully there is a open cross-platform python library called [glyphsLib](https://github.com/googlei18n/glyphsLib) with read and write support for the native source format of Glyphs, the *.glyphs* file.

To load the current font sources into Glyphs we do not open the UFOs directly in Glyphs. Instead, we use the following process using project-specific scripts (run from within the vagrant VM):

- Run `./preglyphs` from the individual project folder using the terminal. This synthesizes a temporary *.glyphs* file from the existing UFO sources and corresponding designspaces.
- Open the *.glyphs* file in Glyphs, make changes, and save.
- Run `./preflightg` from the individual project folder. This reads the *.glyphs* file and exports UFOs, and then runs all the steps in the normal *preflight* script to normalize and sync the UFOs.
- Review the changes in your git client and commit the changes you wish to keep.

This is the best tested and recommended method for modifying fonts with a dedicated font design tool. *Most, but not all, of our projects include these scripts.*

### Robofont

[Robofont] version 3 uses UFO3 as its native format, and does not require a special script prior to using it. Please use the latest release! The workflow is simple:

- Open individual UFOs in Robofont, make changes, save.
- Run `./preflight` to normalize and sync — *this is important!*
- Review the changes in your git client and commit the changes you want to keep.

You'll notice that Robofont may add a few things to the UFOs that remain even after normalization. You can feel free to add these if you want, but please don't later contribute them to our projects. An example:

- a lib.plist key: *com.typemytype.robofont.segmentType*

There may also be some other additions depending on the project or Robofont 3 version.

### FontForge

The most recently released version of [FontForge] (2019-04-13) has vastly improved UFO3 support. It's important to use that release or later, and also be sure that your VM has recently been provisioned, as we have recently added built-in support for handling FontForge-produced UFOs to our *pysilfont* tools. The workflow is:

- Open individual UFOs in FontForge, make changes *(but do not save!)*
- Choose File / Generate Fonts... and specify the output format as *Unified Font Object (UFO3)*, replacing the original UFO. *You can now quit FontForge - there is no need to save the file.*
- Run `./preflightff` to normalize and sync. Note that this is a special FontForge-specific version of *preflight*.
- Review the changes in your git client and commit the changes you want to keep.

Note: Most of our projects do not have the special *preflightff* script yet. If the project doesn't yet have it you can run the normal `./preflight`, but be aware that if there are background glyphs FontForge will copy anchors and Unicode values between layers. You can avoid this by creating your own *preflightff* script based on the example in [Andika Mtihani]. We'll be adding *preflightff* files to our projects as soon as we can.

This FontForge workflow works well, but there are two issues that you may encounter:

- If the UFO contains a features.fea file, FontForge will likely change it considerably. You will want to use your git client to discard any changes to that file prior to commit.
- FontForge will remove any `note` elements it finds in glif files.

It is also possible to use FontForge on another OS (and macOS in particular) to modify the UFOs in a folder shared with the VM, then switch to the VM and run *preflightff* there.  

### FontLab VI

Recent versions of [FontLab VI] have improved UFO3 support, however there are still significant issues. We hope to provide a workflow for FontLab at some point, however it is not a high priority for us as we no longer use FontLab ourselves.

### TruFont

[TruFont] uses UFO3 as its native font format. While it holds great promise, the app is still very limited, so we haven't put effort into testing it with our projects. We would like to provide a workflow, but would first need to see the app become more broadly useful.

[SIL Open Font License]: https://scripts.sil.org/OFL
[Reserved Font Names (RFNs)]: https://scripts.sil.org/OFL
[pysilfont]: https://github.com/silnrsi/pysilfont/blob/master/docs/scripts.md
[psfnormalize]: https://github.com/silnrsi/pysilfont/blob/master/docs/scripts.md#psfnormalize
[RoboFont]: https://robofont.com/
[FontForge]: http://www.fontforge.org/
[TruFont]: http://trufont.github.io/
[Glyphs]: https://glyphsapp.com/
[glyphsLib]: https://github.com/googlei18n/glyphsLib
[FontLab VI]: https://www.fontlab.com/font-editor/fontlab-vi/
[Andika Mtihani]: https://github.com/silnrsi/font-andika-mtihani/blob/master/preflightff
