---
published: true
layout: bookpage
weight: 200
outlevel: 2
category: Source Formats
title: Source Formats
---

We keep our font sources in open formats so anyone can have full access to them now and in the long-term future. This also gives us the widest-possible choice of tools, so we can pick the right tool for the right job. Interoperability is a core value of our open font design and production workflow. Being locked into a single proprietary tool supporting only opaque formats is definitely not what we want, especially long-term.

## UFO3 + designspace

Our primary font sources are kept in the [UFO3 format]. It's a clearly documented, platform-neutral open format which allows everyone to access the sources with a range of tools. Using this type of format helps future-proof a font project and makes it more accessible and maintainable by others. It also helps with keeping font sources in revision control - a key to any collaborative development. Many foundries are also now using UFO as their primary source format. It is directly supported by all the main font design tools (Glyphs, Robofont, FontLab, FontForge, etc). *We sometimes store other formats in the repository for archival purposes (typically in source/archive/) but the fonts are produced from the canonical UFO sources.*

We also occasionally store some font-wide data in the UFO3 *lib.plist*.

Our font family structures (styles, masters, instances) are defined in [designspace] files which describe the relationships between individual UFOs.

We use normalization tools from the [pysilfont] collection of font utilities to keep the UFOs in a consistent format even after import/export from various other tools and to synchronize them with one another. These keep the font sources clean, vendor-neutral, and friendly to version control systems.

## Additional font sources (and tools)

There are some types of data that currently have no canonical place in the UFO3 format. We store and maintain these in additional files:

- *Graphite source code* is stored in [GDL (Graphite Description Language)] format in *source/graphite/*
- *Documentation* is typically stored in .md (Markdown) or .odt (OpenDocument Text) format in *documentation/*. ([fontdocs] is used to maintain source documentation and to generate multiple output formats like PDF and HTML)
- *Test data and documents* are stored in a variety of formats ([FTML], [SILE], [TeX], text) in *tests/*
- *Web font demonstration files* (.html, .css) are stored in *web/*
- *Tools*, such as project-specific python scripts, are stored in *tools/*

## Auxiliary data sources

There are also some types of data that __do__ have a place in the UFO3 format but are clumsy or awkward to maintain there. We store and edit these in auxiliary files, and use python scripts (usually in *preflight*) to update the UFOs from them before committing changes to the project repositories:

- *OpenType source code* is stored in the [.fea format] in the UFO (*features.fea)* but may be defined in a separate file using the more efficient and powerful [.feax format]. The .feax is compiled into standard .fea during the build process and should also be used to update the *features.fea* in the UFOs.
- *Individual glyph data* such as production glyph names and glyph orders is stored in a *glyph_data.csv* file for easy maintenance. The glyph names and orders in the fonts are updated from this data in the *preflight* script.

__For an example of how these sources are organized see [Repository Structures].__    

__To learn more about the *preflight* scripts used to update UFOs from auxiliary sources, see [Modifying Font Sources].__

[UFO3 format]: https://unifiedfontobject.org/versions/ufo3/
[designspace]: https://github.com/fonttools/fonttools/tree/main/Doc/source/designspaceLib/index.rst
[pysilfont]: https://github.com/silnrsi/pysilfont
[GDL (Graphite Description Language)]: http://silnrsi.github.io/graphite/graphite_devFont#fontDev
[FTML]: https://github.com/silnrsi/ftml
[SILE]: https://sile-typesetter.org/
[TeX]: https://tug.org/xetex/
[.fea format]: https://github.com/adobe-type-tools/afdko/blob/develop/docs/OpenTypeFeatureFileSpecification.md
[.feax format]: https://github.com/silnrsi/pysilfont/blob/master/docs/feaextensions.md
[Repository Structures]:  Repository_Structures.html
[Modifying Font Sources]: Modifying_Font_Sources.html
[fontdocs]: https://github.com/silnrsi/fontdocs
