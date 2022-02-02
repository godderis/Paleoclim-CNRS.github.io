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

{% if seminaires != blank %}
<h2>Seminaires</h2>
<div class='card-list'>
{% for presentation in seminaires %}
<div class='card'>
  <div class='card-header'>
        
      <a href="{{ presentation.url }}">
        <center>
          {{ presentation.title }}
        </center>
      </a>
    
    </div>

    {% if presentation.summary %}
      <div class='card-body'>
      
        {% if presentation.image %}
          <div class="presentation__image">
            <a href="{{ presentation.url | relative_url }}">
               <img src="{{ presentation.image | relative_url }}" alt="{{ presentation.image }}" itemprop="image">
            </a>
          </div>
        {% endif %}      

    
        {% assign sum = presentation.summary | markdownify | remove: "<p>" | remove: "</p>" %}
        {% if sum.size > 3 %}
          <p>{{ sum }}</p>
        {% endif %}
      
      </div>
    {% endif %}  

  </div>
{% endfor %}
</div>
{% endif %}

{% if defenses != blank %}
<h2>Defenses</h2>
<div class='card-list'>
{% for presentation in defenses %}
<div class='card'>
  <div class='card-header'>
        
      <a href="{{ presentation.url }}">
        <center>
          {{ presentation.title }}
        </center>
      </a>
    
    </div>

    {% if presentation.summary %}
      <div class='card-body'>
      
        {% if presentation.image %}
          <div class="presentation__image">
            <a href="{{ presentation.url | relative_url }}">
               <img src="{{ presentation.image | relative_url }}" alt="{{ presentation.image }}" itemprop="image">
            </a>
          </div>
        {% endif %}      

    
        {% assign sum = presentation.summary | markdownify | remove: "<p>" | remove: "</p>" %}
        {% if sum.size > 3 %}
          <p>{{ sum }}</p>
        {% endif %}
      
      </div>
    {% endif %}  

  </div>
{% endfor %}
</div>
{% endif %}
