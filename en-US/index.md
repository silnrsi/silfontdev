---
published: true
layout: homepage
weight: 0
title: SIL Font Development Guide
---

Welcome to the SIL font development guide.

This website has been set up as a step-by-step guide to building, modifying and contributing to the various [open font projects](http://software.sil.org/fonts) designed and developed by [SIL International](https://www.sil.org). Let us know if you have any comments or suggestions to add to this guide. Enjoy!


<ol class="rectangle-list">
  {% assign pageList = site.pages | sort: 'weight' %}
  {% for p in pageList %}
    {% if p.path contains 'en-US' and p.title != page.title %}
      <li>
        <span class="outlevel">
          {{ p.outlevel }}
        </span>
        <a {% if p.url == page.url %}class="active"{% endif %} href="{{site.baseurl}}{{ p.url }}">
          {{ p.title }}
        </a>
      </li>
    {% endif %}
  {% endfor %}
</ol>
