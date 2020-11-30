---
layout: splash
permalink: /team
read_time: false
header:
  overlay_color: "#5e616c"
  overlay_image: /assets/images/mm-home-page-feature.jpg
  # actions:
  #   - label: "<i class='fas fa-download'></i> Install now"
  #     url: "/docs/quick-start-guide/"
excerpt: >
  Team   
---

{% for member in site.team %}
  <h2>
    <a href="{{ member.url }}">
      {{ member.name }} - {{ member.position }}
    </a>
  </h2>
  <p>{{ member.content | markdownify }}</p>
{% endfor %}