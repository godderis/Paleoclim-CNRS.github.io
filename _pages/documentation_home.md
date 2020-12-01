---
layout: single
permalink: /resources/documentation
author_profile: false
---

{% assign doc = site.resources | where: "type", "doc" %}

{% for d in doc %}
  <h3>
    <a href="{{ d.url }}">
      {{ d.title }}
    </a>
  </h3>
  <p>{{ d.description }}</p>
{% endfor %}