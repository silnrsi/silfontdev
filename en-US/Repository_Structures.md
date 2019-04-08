---
published: true
layout: bookpage
weight: 300
outlevel: 3
category: Repository Structures
title: Repository Structures
---

Our projects use a consistent directory structure for both our source repositories and release packages. So if you know your way around one of our projects you can easily understand all of them. We'd be very happy to see others adopt this overall structure, too, so please consider it for your projects.

We talk about repositories because our project directory structures and all the files they contain are tracked with [git]. We make our repositories available on [GitHub], but there's nothing about our structures or processes that depends on that service.

Each of our projects (which usually contain only a single font family) use a single dedicated project folder that contains all the font sources, so that it's self-contained. We avoid using more complicated dependency structures such as [git] submodules - they often bring more frustration and confusion than benefits.

Our convention is to name the project folder __font-*nameoffontfamily*__ as in *font-shimenkan* or *font-andika-mtihani*.

## Example structure

Here is an annotated example of our project repository structure based on [Andika Mtihani]'s public git repository. Files that we normally have in all projects are in __bold__. All others are optional and may differ from project to project. Files and folders not in the [Andika Mtihani] project are in ( parentheses ) and are provided as a guide to other projects.

- __.gitattributes__ — *git attributes configuration hidden file tailored for font projects*
- __.gitignore__ — *git ignore configuration hidden file tailored for font projects*
- .gitlab-ci.yml — *gitlab configuration hidden file*
- .travis.yml — *travis configuration hidden file*
- __FONTLOG.txt__ — *font design and engineering-oriented changelog*
- __OFL-FAQ.txt__ — *Frequently Asked Questions file for the SIL Open Font License*
- __OFL.txt__ — *SIL Open Font License file with the copyright statement in its header*
- org.sil.font-andika-mtihani.metainfo.xml — *Appstream metadata template*
- Pipfile — *example Pipfile to capture the build requirements*
- Pipfile.lock — *lock file for the file above*
- __preflight__ — *normalization script to be run before testing/committing a change*
- __preflightg__ — *script to produce and normalize UFOs from a Glyphs file*
- __preglyphs__ — *script to produce temporary Glyphs files from UFOs+designspace*
- __README.md__ — *markdown file with minimal information*
- __README.txt__ — *more complete README file describing the font project*
- wscript — *Smith configuration used for building, testing and releasing*
- ( documentation/ — *folder for user documentation* )
- __source/__ — *folder for containing UFOs, designspaces, smart code sources, etc*
  - ( AndikaMtihani.feax — OpenType feature code including SIL extensions to .fea )
  - AndikaMtihani-Bold.ufo
  - AndikaMtihani-BoldItalic.ufo
  - AndikaMtihani-Italic.ufo
  - __AndikaMtihani-Regular.ufo__
  - AndikaMtihaniItalic.designspace — *designspace definition for Italic & Bold Italic*
  - __AndikaMtihaniRoman.designspace__ — *designspace definition for Regular & Bold*
  - composites.txt — *composite character definitions*
  - __glyph_data.csv__ — *glyph-specific data such as production glyph names and glyph orders*
  - archive/ — *folder for legacy formats if needed for archival purposes*
  - ( graphite/ — *folder for Graphite source code* )
  - logs/ — *folder for log files, only needed as a placeholder to make tools happy*
  - ( masters/ — *folder for master UFOs for projects involving interpolated instances* )
- __tests/__ — *folder for various test documents and data files*
- ( tools/ — *folder for project-specific scripts and utilities* )
- ( web/ — *example files for self-hosted webfonts* )

## Ignored files: temporary files, generated files ###

By default, the generated results of builds (including the generated fonts) will appear in a separate *results/* folder not stored in the repository. Temporary files and generated artifacts like backups, logs, test results, specimens, etc. are not stored in the repository and are set to be ignored by git via the *.gitignore* configuration file. There is some flexibility though, as certain source files are generated or modified by scripts at various times in the lifecycle of a project.

[git]: https://git-scm.com/
[GitHub]: https://github.com/
[Andika Mtihani]: https://github.com/silnrsi/font-andika-mtihani
