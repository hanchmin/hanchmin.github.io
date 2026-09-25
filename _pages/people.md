---
layout: page
title: People
permalink: /people/
description: Members of the research group
nav: false
---

<!-- pages/people.md -->
<div class="people">

  <p>
    We are part of the <a href="https://ins.sjtu.edu.cn/">Institute of Natural Sciences</a>
    and the <a href="https://math.sjtu.edu.cn">School of Mathematics</a> at
    <a href="https://www.sjtu.edu.cn/">Shanghai Jiao Tong University</a>. Our research
    centers on the interplay between machine learning and dynamical systems.
  </p>

  <h2 class="category">PhD Students</h2>

  <div class="people-grid">
    {%- for p in site.data.people.phds -%}
      <div class="people-card">
        <img
          src="{% if p.image %}../assets/img/{{ p.image }}{% else %}../assets/img/people/placeholder.png{% endif %}"
          alt="{{ p.name }}"
          class="people-photo"
        />
        <div class="people-card-body">
          <div class="people-name">
            {%- if p.homepage -%}
              <a href="{{ p.homepage }}">{{ p.name }}</a>
            {%- else -%}
              {{ p.name }}
            {%- endif -%}
          </div>
          <div class="people-meta">{{ p.role }}{% if p.year %}, {{ p.year }}{% endif %}</div>
          {%- if p.blurb -%}
            <p class="people-blurb">{{ p.blurb | strip }}</p>
          {%- endif -%}
          {%- if p.interests -%}
            <p class="people-interests"><b>Interests:</b> {{ p.interests }}</p>
          {%- endif -%}
        </div>
      </div>
    {%- endfor -%}
  </div>

  <h2 class="category">Master's &amp; Undergraduate Students</h2>

  <ul class="people-list">
    {%- for p in site.data.people.masters -%}
      <li><b>{{ p.name }}</b> — {{ p.info }}</li>
    {%- endfor -%}
    {%- for p in site.data.people.undergrads -%}
      <li><b>{{ p.name }}</b> — {{ p.info }}</li>
    {%- endfor -%}
  </ul>

  <h2 class="category">Alumni</h2>

  <ul class="people-list">
    {%- for p in site.data.people.alumni -%}
      <li>
        <b>{{ p.name }}</b>{% if p.role %} ({{ p.role }}){% endif %}{% if p.year %}, {{ p.year }}{% endif %}
        {% if p.next %} — {{ p.next }}{% endif %}
      </li>
    {%- endfor -%}
  </ul>

</div>
