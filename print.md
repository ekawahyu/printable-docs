---
title: Printable View
layout: default
nav_order: 999
print: true
---

{% assign top_pages = site.pages | where_exp: "p", "p.title and p.parent == nil and p.path != page.path" | sort: "nav_order" %}

<h1>Table of Contents</h1>
<div class="toc">
  <ul>
  {% for chapter in top_pages %}
    <li class="toc-label">
      <a href="#{{ chapter.title }}">
        <span class="toc-text">{{ chapter.title }}</span>
        <span class="toc-page" data-target="#{{ chapter.title }}"></span>
      </a>
    </li>
    {% assign sections = site.pages | where: "parent", chapter.title | sort: "nav_order" %}
    {% for section in sections %}
      <li class="toc-label">
        <a href="#{{ section.title }}">
          <span class="toc-text">{{ section.title }}</span>
          <span class="toc-page" data-target="#{{ section.title }}"></span>
        </a>
      </li>
      {% assign subsections = site.pages | where: "parent", section.title | sort: "nav_order" %}
      {% for subsection in subsections %}
        <li class="toc-label">
          <a href="#{{ subsection.title }}">
            <span class="toc-text">{{ subsection.title }}</span>
            <span class="toc-page" data-target="#{{ subsection.title }}"></span>
          </a>
        </li>
      {% endfor %}
    {% endfor %}
  {% endfor %}
  </ul>
</div>

{% for chapter in top_pages %}
  <div id="{{ chapter.title }}" class="chapter" data-running-title="{{ chapter.title }}">
    <h1>{{ chapter.title }}</h1>
    {{ chapter.content | markdownify }}

    {% assign sections = site.pages | where: "parent", chapter.title | sort: "nav_order" %}
    {% for section in sections %}
      <div id="{{ section.title }}" class="section">
        <h2>{{ section.title }}</h2>
        {{ section.content | markdownify }}

        {% assign subsections = site.pages | where: "parent", section.title | sort: "nav_order" %}
        {% for subsection in subsections %}
          <div id="{{ subsection.title }}" class="subsection">
            <h3>{{ subsection.title }}</h3>
            {{ subsection.content | markdownify }}
          </div>
        {% endfor %}
      </div>
    {% endfor %}
  </div>
{% endfor %}
