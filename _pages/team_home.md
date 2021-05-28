---
layout: splash
permalink: /team
read_time: false
header:
  overlay_color: "#5e616c"
  overlay_image: /assets/images/mm-home-page-feature.jpg
title: "Meet the Team"
excerpt: >
  Please feel free to checkout our team of motivated Researchers, Post Doc's, PhD Student's and Engineers
---

{% assign fellow = site.team | where: "type", "fellow" %}
{% assign perm = site.team | where: "type", "perm" %}
{% assign phd = site.team | where: "type", "phd" %}
{% assign alumni = site.team | where_exp: 'member', "member.type == 'alumni'" %}

<h2>Maybe add an about statement here like global goals and such???</h2>

<div itemscope itemtype="https://schema.org/Person">

{% if perm != blank %}
<h2>Permenant Staff</h2>

{% for member in perm %}
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
{% endif %}

{% if fellow != blank %}
<h2>Fellows</h2>

{% for member in fellow %}
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
{% endif %}

{% if phd != blank %}
<h2>PhD Candidates</h2>

{% for member in phd %}
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
{% endif %}

{% if alumni != blank %}
<h2>Alumni</h2>

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
{% endif %}


</div>