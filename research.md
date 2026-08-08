---
layout: page
title: Research
eyebrow: Working papers & policy notes
permalink: /research/
---

Longer-form research, working papers, and policy notes. This list is generated automatically from whatever PDFs are in the `papers/` folder — no editing this page required.

**To publish a new paper:** just add a PDF to the `papers` folder, named like `2026-03-your-paper-title.pdf` (four-digit year, two-digit month, then a title with words separated by dashes). It will appear below automatically, newest first, next time the site rebuilds.

{% assign pdf_ext = ".pdf" %}
{% assign papers_folder = "/papers/" %}
{% assign papers = site.static_files | where_exp: "f", "f.extname == pdf_ext" %}
{% assign papers = papers | where_exp: "f", "f.path contains papers_folder" %}
{% assign papers = papers | sort: "name" | reverse %}

<ul class="pub-list">
{% for file in papers %}
  {% assign name_no_ext = file.name | remove: '.pdf' %}
  {% assign parts = name_no_ext | split: '-' %}
  {% assign part_count = parts | size %}

  {% if part_count >= 3 %}
    {% assign paper_year = parts[0] %}
    {% assign paper_month = parts[1] %}
    {% assign paper_title = "" %}
    {% assign word_count = 0 %}
    {% for word in parts %}
      {% if forloop.index0 >= 2 %}
        {% assign cap_word = word | capitalize %}
        {% if word_count == 0 %}
          {% assign paper_title = cap_word %}
        {% else %}
          {% assign paper_title = paper_title | append: " " | append: cap_word %}
        {% endif %}
        {% assign word_count = word_count | plus: 1 %}
      {% endif %}
    {% endfor %}
    {% assign date_str = paper_year | append: "-" | append: paper_month | append: "-01" %}
    {% assign display_date = date_str | date: "%B %Y" %}
  {% else %}
    {% assign paper_title = name_no_ext | replace: '-', ' ' | replace: '_', ' ' | capitalize %}
    {% assign display_date = file.modified_time | date: "%B %Y" %}
  {% endif %}

  <li class="pub-item">
    <div class="meta">{{ display_date }}</div>
    <div class="pub-title">{{ paper_title }}</div>
    <div class="pub-venue"><a href="{{ file.path | relative_url }}">PDF</a></div>
  </li>
{% endfor %}
</ul>

{% if papers.size == 0 %}
<p class="meta">No papers uploaded yet. Drop a PDF into the <code>papers/</code> folder to see it appear here.</p>
{% endif %}
