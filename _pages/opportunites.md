---
layout: splash
permalink: /opportunities
read_time: false
header:
  overlay_color: "#5e616c"
  overlay_image: /assets/images/mm-home-page-feature.jpg
title: "Current Opportunities"
excerpt:  "<div style='text-align: justify'> Interested in the Earth system evolution across the Earth’s history with a comfortable background in maths, physics, and computing. Our group works on many fascinating subjects, from the first continental glaciations in the Phanerozoic to the link between Life and Climate with a little hitch on the processes controlling the atmospheric CO2 concentration at all time scales. Contact us for both post-doctoral and graduate student opportunities. Apply also for Master internship. </div>"

---

{% assign fellow = site.opportunities | where: "type", "fellow" %}
{% assign perm = site.opportunities | where: "type", "perm" %}
{% assign phd = site.opportunities | where: "type", "phd" %}

{% if perm != blank %}
<h2>Permenant Positions</h2>

{% for position in perm %}
  <h3>
    <a href="{{ position.url }}">
      {{ position.title }}
    </a>
  </h3>
{% endfor %}
{% endif %}

{% if fellow != blank %}
<h2>Fellow Positions</h2>

{% for position in fellow %}
  <h3>
    <a href="{{ position.url }}">
      {{ position.title }}
    </a>
  </h3>
{% endfor %}
{% endif %}

{% if phd != blank %}
<h2>PhD Positions</h2>

{% for position in phd %}
  <h3>
    <a href="{{ position.url }}">
      {{ position.title }}
    </a>
  </h3>
{% endfor %}
{% endif %}