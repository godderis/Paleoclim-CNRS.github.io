
---
layout: splash
permalink: /resources/presentations
read_time: false
header:
  overlay_color: "#5e616c"
  overlay_image: /assets/images/mm-home-page-feature.jpg
excerpt: <h2><FONT color="#ffffff">Presentations</FONT></h2>
---

{% assign defenses = site.presentations | where: "type", "defense" %}
{% assign seminaires = site.presentations | where: "type", "seminaire" %}

<h2>Seminaires</h2>
<div class='card-list'>
{% for presentations in seminaires %}
<div class='card'>
  <div class='card-header'>
        
      <a href="{{ presentation.url }}">
        <center>
        <strong>
          {{ presentation.title }}
        </strong>
        </center>
      </a>
    
    </div>
    <div class='card-body'>
      
    {% if presentation.image %}
      <div class="presentation__image">
         <a href="{{ presentation.url | relative_url }}">
          <img src="{{ presentation.image | relative_url }}" alt="{{ presentation.image }}" itemprop="image">
        </a>
      </div>
    {% endif %}      
    </div>
  </div>

<h2>Defenses</h2>
<div class='card-list'>
{% for presentations in defenses %}
<div class='card'>
  <div class='card-header'>
        
      <a href="{{ presentation.url }}">
        <center>
        <strong>
          {{ presentation.title }}
        </strong>
        </center>
      </a>
    
    </div>
    <div class='card-body'>
      
    {% if presentation.image %}
      <div class="presentation__image">
         <a href="{{ presentation.url | relative_url }}">
          <img src="{{ presentation.image | relative_url }}" alt="{{ presentation.image }}" itemprop="image">
        </a>
      </div>
    {% endif %}      
    </div>
  </div>