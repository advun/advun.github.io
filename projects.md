---
layout: page
title: Projects
wide: true
---

{% assign sorted_projects = site.projects | sort: "date" | reverse %}

<div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(220px, 1fr)); gap: 1.5rem;">
  {% for project in sorted_projects %}
    <a href="{{ project.url }}" style="text-decoration: none; color: inherit;">
      <img src="{{ project.photo | relative_url }}" alt="{{ project.title }}" loading="lazy" style="width: 100%; border-radius: 6px; margin-bottom: 0.5rem;">
      <h3 style="margin: 0;">{{ project.title }}</h3>
      {% if project.excerpt %}
        <p style="margin: 0.25rem 0 0; color: #666;">{{ project.excerpt }}</p>
      {% endif %}
    </a>
  {% endfor %}
</div>