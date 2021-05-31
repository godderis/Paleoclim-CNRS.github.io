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

  <div class='card-list'>
    <h2>Permenant Staff</h2>

    {% for member in perm %}

    <div class='card'>
      {% assign author = site.data.authors[member.author] | default: member.author %}
      <div style='overflow:auto' class="card-header">
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
      <div class='card-body'>
        <p>{{ author.bio | markdownify }}</p>
      </div>
    </div>
    {% endfor %}
  </div>
  {% endif %}

  {% if fellow != blank %}

  <h2>Fellows</h2>
  <div class='card-list'>
    {% for member in fellow %}
    <div class='card'>
      {% assign author = site.data.authors[member.author] | default: member.author %}

      <div style='overflow:auto' class='card-header'>
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
      <div class='card-body'>
        <p>{{ author.bio | markdownify }}</p>
      </div>
    </div>
    {% endfor %}
  </div>
{% endif %}

{% if phd != blank %}

<div class='card-list'>
  <h2>PhD Candidates</h2>

  {% for member in phd %}
  <div class='card'>
    {% assign author = site.data.authors[member.author] | default: member.author %}

    <div style='overflow:auto' class='card-header'>
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
    <div class='card-body'>
      <p>{{ author.bio | markdownify }}</p>
    </div>
  </div>
  {% endfor %}
</div>
{% endif %}

{% if alumni != blank %}

<div class='card-list'>
  <h2>Alumni</h2>

  {% for member in alumni %}
  <div class='card'>
    {% assign author = site.data.authors[member.author] | default: member.author %}

    <div style='overflow:auto' class='card-header'>
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
    <div class='card-body'>
      <p>{{ author.bio | markdownify }}</p>
    </div>
  </div>
  {% endfor %}
</div>
{% endif %}

</div>