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

<h2>Upcoming workshops</h2>
<div class='card-list'>
{% for workshop in upcoming_workshops %}
<div class='card'>
  <div class='card-header'>
      <a href="{{ workshop.url }}">
        {{ workshop.title }}
      </a>
    </div>
    <div class='card-body'>
    <p>
      <b>Start year: </b>{{ workshop.year_start }}
    </p>
    <p>
      <b>Title: </b>{{ workshop.title }}
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
