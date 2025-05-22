---
layout: page
title: Updates
permalink: /updates/
nav: true
nav_order: 3
---

<div class="news">
{%- if site.data.news.items -%}
  {% assign spacing = site.news_item_spacing | default: "10px" %}
  <div class="news-list">
    {% for item in site.data.news.items %}
    <div class="news-item" style="margin-bottom: {{ spacing }};">
[<strong>{% assign formatted_date = item.date | date: "%b, %d, %Y" %}{{ formatted_date }}</strong>]
{% comment %}
  First, split the content by "{" to isolate bold sections.
{% endcomment %}
{% assign curly_parts = item.content | split: '{' %}
{% assign text = curly_parts[0] %}
{% assign quote_parts = text | split: '"' %}
{% for part in quote_parts %}
  {% assign modq = forloop.index0 | modulo: 2 %}
  {% if modq == 0 %}
    {{ part }}
  {% else %}
    <i>{{ part }}</i>
  {% endif %}
{% endfor %}
{% for block in curly_parts offset:1 %}
  {% comment %}
    Split the block on '}' so that the part before '}' is the bold text.
  {% endcomment %}
  {% assign subparts = block | split: '}' %}
  <strong>{{ subparts[0] }}</strong>
  {% if subparts.size > 1 %}
    {% assign remainder = subparts[1] %}
    {% assign quote_parts = remainder | split: '"' %}
    {% for part in quote_parts %}
      {% assign modq = forloop.index0 | modulo: 2 %}
      {% if modq == 0 %}
        {{ part }}
      {% else %}
        <i>{{ part }}</i>
      {% endif %}
    {% endfor %}
  {% endif %}
{% endfor %}
    </div>
    {% endfor %}
  </div>
{%- else -%}
  <p>No news so far...</p>
{%- endif %}
</div>

