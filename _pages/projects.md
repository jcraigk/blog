---
title: Projects
layout: collection
permalink: /projects/
collection: projects
entries_layout: grid
classes: wide
---

{% for project in site.projects %}
  <h2>
    <a href="{{ project.url }}">
      {{ project.title }}
    </a>
  </h2>
{% endfor %}
