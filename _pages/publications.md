---
layout: page
permalink: /publications/
title: Publications
description: List of my publications and preprints
nav: false
nav_order: 1
---
<!-- _pages/publications.md -->
<div class="publications">

  <h2>Journal and Preprints</h2>
  {% bibliography -f papers -q @article %}
  <h2>Conference</h2>
  {% bibliography -f papers -q @InProceedings %}
  <h2>Thesis</h2>
  {% bibliography -f papers -q @MastersThesis %}
  <h2>Misc</h2>
  {% bibliography -f papers -q @unpublished %}
  
</div>