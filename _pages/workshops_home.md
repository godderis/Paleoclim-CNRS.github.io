---
layout: splash
permalink: /workshops
read_time: false
header:
  overlay_color: "#5e616c"
  overlay_image: /assets/images/mm-home-page-feature.jpg
excerpt: <h2><FONT color="#ffffff">Workshops</FONT></h2>

---
{% assign old_workshops = site.workshops | where: "type", "old" %}
{% assign upcoming_workshops = site.workshops | where_exp: "work", "work.type == 'upcoming'" | sort: 'year_start' | reverse%}

<h2>Upcoming Workshops</h2>
<div class='card-list'>
{% for workshop in upcoming_workshops %}
<div class='card'>
  <div class='card-header'>
    
      <a href="{{ workshop.url }}">
        <center>
        <strong>
            {{ workshop.title }}
        </strong>
        </center>  
      </a>
    
       {% if workshop.image %}
        <div class="workshop__image">
          <a href="{{ workshop.url | relative_url }}">
            <img src="{{ workshop.image | relative_url }}" alt="{{ workshop.image }}" itemprop="image">
          </a>
        </div>
       {% endif %}
  
    </div>
    <div class='card-body'>
    <p>
      <b>When: </b>{{ workshop.days}}
    </p>
    <p>
      <b>Where: </b>{{ workshop.location }}
    </p>
    </div>
  </div>
  
{% endfor %}
</div>


<h2>Archived Workshops</h2>
<div class='card-list'>
{% for workshop in old_workshops %}
  <div class='card'>
    <div class='card-header'>
      <a href="{{ workshop.url }}">
        {{ workshop.title }}
      </a>
    </div>
  </div>
{% endfor %}
