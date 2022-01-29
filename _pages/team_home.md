---
layout: splash
permalink: /team
read_time: false
header:
  overlay_color: "#5e616c"
  overlay_image: /assets/images/mm-home-page-feature.jpg
excerpt: <h2><FONT color="#ffffff">Team</FONT></h2>

---

We are a community of deep-time climate modelers working in various research labs in France.

{% assign fellow = site.team | where: "type", "fellow" %}
{% assign perm = site.team | where: "type", "perm" %}
{% assign phd = site.team | where: "type", "phd" %}
{% assign alumni = site.team | where_exp: 'member', "member.type == 'alumni'" %}

<div itemscope itemtype="https://schema.org/Person">

  {% if perm != blank %}

    <h2>Permanent Staff</h2>
    <div class='card-list card-group'>

    {% for member in perm %}

    <div class='card'>
      {% assign author = site.data.authors[member.author] | default: member.author %}
      <div style='overflow:hidden' class="card-header team-card-header">
        {% if author.avatar %}
        <div class="author__avatar">
          <a href="{{ member.url | relative_url }}">
            <img src="{{ author.avatar | relative_url }}" alt="{{ author.name }}" itemprop="image">
          </a>
        </div>
        {% endif %}
        <h2>
          <a href="{{ member.url }}">
            {{ author.name }}
          </a>
        </h2>
      </div>
      {% assign bio = author.bio | markdownify | remove: "<p>" | remove: "</p>" %}
      {% if bio.size > 3 %}
      <div class='card-body'>
        <p>{{ bio }}</p>
      </div>
      {% endif %}
    </div>
    {% endfor %}
  </div>
  {% endif %}

  {% if fellow != blank %}

  <h2>Fellows</h2>
  <div class='card-list card-group'>
    {% for member in fellow %}
    <div class='card'>
      {% assign author = site.data.authors[member.author] | default: member.author %}

      <div style='overflow:hidden' class='card-header team-card-header'>
        {% if author.avatar %}
        <div class="author__avatar">
          <a href="{{ member.url | relative_url }}">
            <img src="{{ author.avatar | relative_url }}" alt="{{ author.name }}" itemprop="image">
          </a>
        </div>
        {% endif %}
        <h2>
          <a href="{{ member.url }}">
            {{ author.name }}
          </a>
        </h2>
      </div>
      {% assign bio = author.bio | markdownify | remove: "<p>" | remove: "</p>" %}
      {% if bio.size > 3 %}
      <div class='card-body'>
        <p>{{ bio }}</p>
      </div>
      {% endif %}
    </div>
    {% endfor %}
  </div>
{% endif %}

{% if phd != blank %}

  <h2>PhD Candidates</h2>
  <div class='card-list card-group'>

  {% for member in phd %}
  <div class='card'>
    {% assign author = site.data.authors[member.author] | default: member.author %}

    <div style='overflow:hidden' class='card-header team-card-header'>
      {% if author.avatar %}
      <div class="author__avatar">
        <a href="{{ member.url | relative_url }}">
          <img src="{{ author.avatar | relative_url }}" alt="{{ author.name }}" itemprop="image">
        </a>
      </div>
      {% endif %}
      <h2>
        <a href="{{ member.url }}">
          {{ author.name }}
        </a>
      </h2>
    </div>
    {% assign bio = author.bio | markdownify | remove: "<p>" | remove: "</p>" %}
    {% if bio.size > 3 %}
    <div class='card-body'>
      <p>{{ bio }}</p>
    </div>
    {% endif %}
  </div>
  {% endfor %}
</div>
{% endif %}

{% if alumni != blank %}

  <h2>Alumni</h2>
  <div class='card-list card-group'>

  {% for member in alumni %}
  <div class='card'>
    {% assign author = site.data.authors[member.author] | default: member.author %}

    <div style='overflow:hidden' class='card-header team-card-header'>
      {% if author.avatar %}
      <div class="author__avatar">
        <a href="{{ member.url | relative_url }}">
          <img src="{{ author.avatar | relative_url }}" alt="{{ author.name }}" itemprop="image">
        </a>
      </div>
      {% endif %}
      <h2>
        <a href="{{ member.url }}">
          {{ author.name }}
        </a>
      </h2>
    </div>
    {% assign bio = author.bio | markdownify | remove: "<p>" | remove: "</p>" %}
    {% if bio.size > 3 %}
    <div class='card-body'>
      <p>{{ bio }}</p>
    </div>
    {% endif %}
  </div>
  {% endfor %}
</div>
{% endif %}

</div>
