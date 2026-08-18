---
layout: page
title: Research
eyebrow: Working papers & policy notes
permalink: /research/
---

Longer-form research, working papers, and policy notes. Each list below is generated automatically from PDFs in the corresponding folder — no editing this page required.

To publish a new paper: add a PDF to `papers/academic/` (for peer-reviewed or academic-style working papers) or `papers/applied/` (for practitioner-facing policy briefs and applied notes). Name it like `2026-03-your-paper-title.pdf` for an automatic date and title, or name it anything if you don't need that.

{% assign pdf_ext = ".pdf" %}

## Academic Research

{% assign academic_folder = "/papers/academic/" %}
{% assign academic_papers = site.static_files | where_exp: "f", "f.extname == pdf_ext" %}
{% assign academic_papers = academic_papers | where_exp: "f", "f.path contains academic_folder" %}
{% assign academic_papers = academic_papers | sort: "name" | reverse %}

<div class="paper-list" id="academic-list" data-per-page="5">
{% for file in academic_papers %}
  {% assign name_no_ext = file.name | remove: '.pdf' %}
  {% assign normalized_name = name_no_ext | replace: '_', '-' | replace: ' ', '-' %}
  {% assign parts = normalized_name | split: '-' %}
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

  <div class="paper-item">
    <span class="paper-date">{{ display_date }}</span>
    <span class="paper-title">{{ paper_title }}</span>
    <a class="paper-link" href="{{ file.path | relative_url }}">PDF</a>
  </div>
{% endfor %}
</div>

<div class="paper-pagination" id="academic-list-pagination"></div>

{% if academic_papers.size == 0 %}
<p class="paper-empty">No academic papers uploaded yet. Drop a PDF into <code>papers/academic/</code> to see it appear here.</p>
{% endif %}

## Applied Research &amp; Policy Notes

{% assign applied_folder = "/papers/applied/" %}
{% assign applied_papers = site.static_files | where_exp: "f", "f.extname == pdf_ext" %}
{% assign applied_papers = applied_papers | where_exp: "f", "f.path contains applied_folder" %}
{% assign applied_papers = applied_papers | sort: "name" | reverse %}

<div class="paper-list" id="applied-list" data-per-page="5">
{% for file in applied_papers %}
  {% assign name_no_ext = file.name | remove: '.pdf' %}
  {% assign normalized_name = name_no_ext | replace: '_', '-' | replace: ' ', '-' %}
  {% assign parts = normalized_name | split: '-' %}
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

  <div class="paper-item">
    <span class="paper-date">{{ display_date }}</span>
    <span class="paper-title">{{ paper_title }}</span>
    <a class="paper-link" href="{{ file.path | relative_url }}">PDF</a>
  </div>
{% endfor %}
</div>

<div class="paper-pagination" id="applied-list-pagination"></div>

{% if applied_papers.size == 0 %}
<p class="paper-empty">No applied papers uploaded yet. Drop a PDF into <code>papers/applied/</code> to see it appear here.</p>
{% endif %}

<style>
.paper-item {
  display: flex;
  align-items: baseline;
  gap: 0.75em;
  padding: 0.5em 0;
  border-bottom: 1px solid #e5e5e5;
}
.paper-date {
  min-width: 8em;
  color: #666;
  font-size: 0.9em;
}
.paper-title {
  flex: 1;
}
.paper-link {
  white-space: nowrap;
}
.paper-pagination {
  display: flex;
  gap: 0.4em;
  margin: 1em 0 2em 0;
  align-items: center;
}
.paper-pagination button {
  padding: 0.3em 0.7em;
  border: 1px solid #ccc;
  background: #fff;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.9em;
}
.paper-pagination button.active {
  background: #222;
  color: #fff;
  border-color: #222;
}
.paper-pagination button:disabled {
  opacity: 0.4;
  cursor: default;
}
</style>

<script>
(function () {
  function paginateList(listId, paginationId) {
    var list = document.getElementById(listId);
    var pagination = document.getElementById(paginationId);
    if (!list || !pagination) return;

    var items = Array.prototype.slice.call(list.getElementsByClassName('paper-item'));
    var perPage = parseInt(list.getAttribute('data-per-page'), 10) || 5;
    var pageCount = Math.ceil(items.length / perPage);

    if (pageCount <= 1) return; // nothing to paginate

    function showPage(page) {
      items.forEach(function (item, i) {
        item.style.display = (i >= (page - 1) * perPage && i < page * perPage) ? '' : 'none';
      });
      var buttons = pagination.getElementsByTagName('button');
      Array.prototype.forEach.call(buttons, function (btn) {
        btn.classList.toggle('active', parseInt(btn.getAttribute('data-page'), 10) === page);
      });
    }

    for (var p = 1; p <= pageCount; p++) {
      var btn = document.createElement('button');
      btn.textContent = p;
      btn.setAttribute('data-page', p);
      btn.addEventListener('click', function () {
        showPage(parseInt(this.getAttribute('data-page'), 10));
      });
      pagination.appendChild(btn);
    }

    showPage(1);
  }

  paginateList('academic-list', 'academic-list-pagination');
  paginateList('applied-list', 'applied-list-pagination');
})();
</script>

