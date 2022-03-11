---
layout: splash
permalink: /opportunities
read_time: false
header:
  overlay_color: "#5e616c"
  overlay_image: /assets/images/mm-home-page-feature.jpg
excerpt: <h2><FONT color="#ffffff">Opportunities</FONT></h2>

---

Interested in the Earth system evolution across the Earth’s history with a comfortable background in maths, physics, and computing. Our group works on many fascinating subjects, from the first continental glaciations in the Phanerozoic to the link between Life and Climate with a little hitch on the processes controlling the atmospheric CO2 concentration at all time scales. Contact us for both post-doctoral and graduate student opportunities. Apply also for Master internship.

{% assign fellow = site.opportunities | where: "type", "fellow" %}
{% assign perm = site.opportunities | where: "type", "perm" %}
{% assign phd = site.opportunities | where: "type", "phd" %}
{% assign master2 = site.opportunities | where: "type", "master2" %}

{% if perm != blank %}
<h2>Permanent Positions</h2>
<div class='card-list'>
  {% for position in perm %}
   <div class='card'>
      <div class='card-header'>
        <a href="{{ position.url }}">
          {{ position.title }}
        </a>
      </div>
      {% if position.image %}
        <div class='card-body'>
          <div class="position__image">
             <a href="{{ position.url | relative_url }}">
             <img src="{{ position.image | relative_url }}" alt="{{ position.image }}" itemprop="image">
             </a>
          </div>   
        </div>      
      {% endif %}
   </div>     
  {% endfor %}
  </div>
{% endif %}

{% if fellow != blank %}
<h2>Fellow Positions</h2>
<div class='card-list'>
  {% for position in fellow %}
   <div class='card'>
      <div class='card-header'>
        <a href="{{ position.url }}">
          {{ position.title }}
        </a>
      </div>
      {% if position.image %}
        <div class='card-body'>
          <div class="position__image">
             <a href="{{ position.url | relative_url }}">
             <img src="{{ position.image | relative_url }}" alt="{{ position.image }}" itemprop="image">
             </a>
          </div>   
        </div>      
      {% endif %}
   </div>     
  {% endfor %}
  </div>
{% endif %}

{% if phd != blank %}
<h2>PhD Positions</h2>
<div class='card-list'>
  {% for position in phd %}
   <div class='card'>
      <div class='card-header'>
        <a href="{{ position.url }}">
          {{ position.title }}
        </a>
      </div>
      {% if position.image %}
        <div class='card-body'>
          <div class="position__image">
             <a href="{{ position.url | relative_url }}">
             <img src="{{ position.image | relative_url }}" alt="{{ position.image }}" itemprop="image">
             </a>
          </div>   
        </div>      
      {% endif %}
   </div>     
  {% endfor %}
  </div>
{% endif %}

{% if master2 != blank %}
<h2>Master 2 Positions</h2>
<div class='card-list'>
  {% for position in master2 %}
   <div class='card'>
      <div class='card-header'>
        <a href="{{ position.url }}">
          {{ position.title }}
        </a>
      </div>
      {% if position.image %}
        <div class='card-body'>
          <div class="position__image">
             <a href="{{ position.url | relative_url }}">
             <img src="{{ position.image | relative_url }}" alt="{{ position.image }}" itemprop="image">
             </a>
          </div>
        </div>
      {% endif %}
   </div>
  {% endfor %}
  </div>
{% endif %}

