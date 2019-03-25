---
published: true
layout: bookpage
weight: 300
outlevel: 3
category: Repository Structures
title: Repository Structures
---

To make it easier to know where various source files are located, or can be found when generated, we use the following conventions, or recommended best practices, for repository structures.

We talk about repositories because we assume that a local folder structure and all the files it contains will be tracked with [git](https://git-scm.com/).

We recommend that you have a project folder that contains all the font sources, so that it's self-contained. (Using git submodules for some scenarios where you are sharing common data and sources across fonts might work but it does add an extra layer of complexity that not everybody wants to deal with). 

A good convention is __font-nameoffontfamily/__ for the name of that project folder. 


### Repository Structures ###

If we take [Andika Mtihani](https://github.com/silnrsi/font-andika-mtihani)'s public git repository structure, we can see: 

> __font-andika-mtihani/__
>
>├── FONTLOG.txt    (the font design and engineering-oriented changelog)
>
>├── OFL-FAQ.txt   (the Frequently Asked Question file for the Open Font License)
>
>├── OFL.txt   (the Open Font License file with the copyright statement in its header)
>
>├── org.sil.font-andika-mtihani.metainfo.xml   (a Appstream metadata template, optional) 
>
>├── Pipfile  (an example Pipfile to capture the build requirements, optional)
>
>├── Pipfile.lock  (the lock file for the file above, optional)
>
>├── preflight  (the normalization script to be run before testing/committing a change)
>
>├── preflightg   (the Glyphs-specific normalization script)
>
>├── preglyphs  (the Glyphs-specific script to generate a current but temporary .glyphs file) 
>
>├── README.md   (a Markdown file with minimal information)
>
>├── README.txt   (a more complete README file describing the font project)
>
>├── source/  (the source subfolder contains UFOs, designspaces, smart code sources, etc)
> 
>├──    ├──  AndikaMtihani-BoldItalic.ufo
>
>├──    ├── AndikaMtihani-Bold.ufo
>
>├──    ├── AndikaMtihani-Italic.ufo
>
>├──    └── AndikaMtihani-Regular.ufo
>
>├──    └── composites.txt  (the definition for the composite characters)
>
>├──    └──  AndikaMtihaniItalic.designspace  (the designspace definition for Italic)
>
>├──    └──  AndikaMtihaniRoman.designspace (the designspace definition for Roman)
>
>├──    └── glyph_data.csv  (the file indicating the desired glyph ordering, used by prefligt) 
>
>├──    └──  ...
>
>├── source/archive  (a folder to hold legacy formats if needed for archival needs) 
>
>├──     └──  ...
>
>├──  source/backups  (a temporary folder to hold backups of UFOs as they go through the process of normalization via preflight)
>
>├──     └──  ...
>
>├──  source/logs  (a folder holding logs files)
>
>├──     └──  ...
>
>├──  tests/  (a folder holding the various test data files and test documents) 
>
>├──     └──  ...
>
>├── web  (example files for self-hosting webfonts)
>
> │   ├── Andika-Mtihani-webfont-example.css
>
> │   └── Andika-Mtihani-example.html
>
>├── wscript (the smith configuration used for building, testing and releasing)
>




### Ignored files: temporary files, generated files ###

By default the generated results of builds will appear in a separate folder, the __results/__ folder. By default, temporary files and generated artifacts like fonts, test results, specimens, etc are not stored in the repository and should be set to be ignored by git via a __.gitignore__ configuration file. There is some flexibility though, as certain source files are generated or modified by scripts at various times in the lifecycle of a project. 



