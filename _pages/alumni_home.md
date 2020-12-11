---
layout: splash
permalink: /alumni
read_time: false
header:
  overlay_color: "#5e616c"
  overlay_image: /assets/images/mm-home-page-feature.jpg
title: "Meet the Team"
excerpt: >
  Please feel free to checkout our team of motivated Researchers, Post Doc's, PhD Student's and Engineers
---
{% assign alumni = site.team | where_exp: 'member', "member.type == 'alumni'" %}

<div itemscope itemtype="https://schema.org/Person">
{% for member in alumni %}
  {% assign author = site.data.authors[member.author] | default: member.author %}
  <div style='overflow:auto'>
  {% if author.avatar %}
    <div class="author__avatar" style="float:left;margin-right: 15px;">
        <a href="{{ member.url | relative_url }}">
          <img src="{{ author.avatar | relative_url }}" alt="{{ author.name }}" itemprop="image">
        </a>
    </div>
  {% endif %}
  <h2 style="float: left;">
    <a href="{{ member.url }}">
      {{ author.name }} - {{ member.position }}
    </a>
  </h2>
  </div>
  <p>{{ author.bio | markdownify }}</p>
{% endfor %}
</div>