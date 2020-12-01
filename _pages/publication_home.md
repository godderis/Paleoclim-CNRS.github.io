---
layout: single
permalink: /resources/publications
author_profile: false
---

{% assign publications = site.resources | where: "type", "publication" %}

{% for pub in publications %}
  {% assign author = site.data.authors[pub.author] %}
  <h3>
    <a href="{{ pub.url }}">
      {{ pub.title }} - {{ author.name }}
    </a>
  </h3>
  <p>{{ pub.description }}</p>
{% endfor %}