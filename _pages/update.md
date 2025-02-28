---
layout: page
title: Update
permalink: /update/
nav: true
nav_order: 6
---

<div class="news">
  {%- if site.data.news.items -%}
    <div class="table-responsive">
      <table class="table table-sm table-borderless">
        {% for item in site.data.news.items %}
          <tr>
            <td>
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
            </td>
          </tr>
        {%- endfor %}
      </table>
    </div>
  {%- else -%}
    <p>No news so far...</p>
  {%- endif %}
</div>