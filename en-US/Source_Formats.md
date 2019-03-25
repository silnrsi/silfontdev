---
published: true
layout: bookpage
weight: 200
outlevel: 2
category: Source Formats
title: Source Formats
---

We want to keep our font sources in open formats so we (or anyone else) can have our pick of the right tool for the right job.
Interoperability is a core value of the open font design and production workflow. Being locked-in a particular tool is definitely not we we want. 

We require that font sources are kept in the [UFO3 format](http://unifiedfontobject.org/versions/ufo3/), it's a documented non-opaque XML platform-neutral open format which does not keep font sources tied up to a particular piece of software (as good as it might be) but allows everyone to use them across a range of tools. Using this format helps future-proof a font project and makes it accessible and maintainable by others. It also helps with keeping font sources in revision control. We might sometimes store other formats in the repository as archival material but we do the actual work with the UFOs as the canonical source. Many foundries are also now using UFOs as their primary source format. 

We use normalization tools (from the [pysilfont](https://github.com/silnrsi/pysilfont) collection of font utilities) to make sure that the font sources remain clean and vendor-neutral and, while there are useful provisions to hold tool-specific data in the UFO3 spec, we want to prevent one particular tool making the font sources harder to use overall or parts of the sources inaccessible to other tools who do conform to the specification. 

Example source format include the following: 
- Opentype source code is stored in the .fea (or .feax the fea extended format).
- Graphite source code is stored in .gdl format. 
- Documentation is stored in OpenDocument .odt format. 
- Test data is stored in .ftml format  (and the corresponding .xsl to generate corresponding output) 
- Test documents are stored in .tex XeTeX format, in .sil SILE format, in .idml IDML format, or in plain text.
- Data available as csv. 
- The rest are human-readable text files. 
- ...
