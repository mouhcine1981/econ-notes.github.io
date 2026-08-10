---
layout: page
title: Research
eyebrow: Working papers & policy notes
permalink: /research/
---

Longer-form research, working papers, and policy notes. Each list below is generated automatically from PDFs in the corresponding folder — no editing this page required.

**To publish a new paper:** add a PDF to `papers/academic/` (for peer-reviewed or academic-style working papers) or `papers/applied/` (for practitioner-facing policy briefs and applied notes). Name it like `2026-03-your-paper-title.pdf` for an automatic date and title, or name it anything if you don't need that.

{% assign pdf_ext = ".pdf" %}

## Academic Research

{% assign academic_folder = "/papers/academic/" %}
{% assign academic_papers = site.static_files | where_exp: "f", "f.extname == pdf_ext" %}
{% assign academic_papers = academic_papers | where_exp: "f", "f.path contains academic_folder" %}
{% assign academic_papers = academic_papers | sort: "name" | reverse %}

<ul class="pub-list">
{% for file in academic_papers %}
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

{% if academic_papers.size == 0 %}
<p class="meta">No academic papers uploaded yet. Drop a PDF into <code>papers/academic/</code> to see it appear here.</p>
{% endif %}

## Applied Research & Policy Notes

{% assign applied_folder = "/papers/applied/" %}
{% assign applied_papers = site.static_files | where_exp: "f", "f.extname == pdf_ext" %}
{% assign applied_papers = applied_papers | where_exp: "f", "f.path contains applied_folder" %}
{% assign applied_papers = applied_papers | sort: "name" | reverse %}

<ul class="pub-list">
{% for file in applied_papers %}
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

{% if applied_papers.size == 0 %}
<p class="meta">No applied papers uploaded yet. Drop a PDF into <code>papers/applied/</code> to see it appear here.</p>
{% endif %}
