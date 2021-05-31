---
layout: splash
permalink: /projects
read_time: false
header:
  overlay_color: "#5e616c"
  overlay_image: /assets/images/mm-home-page-feature.jpg
title: Projects
excerpt: >
  This is where you can find all the cool stuff we are working on, have worked on and will hopefully be working on!   
---
{% assign old_projects = site.projects | where: "type", "old" %}
{% assign current_projects = site.projects | where_exp: "proj", "proj.type == 'current'" | sort: 'year_start' | reverse%}


<h2>Current Projects</h2>
<div class='card-list'>
{% for project in current_projects %}
<div class='card'>
  <div class='card-header'>
      <a href="{{ project.url }}">
        {{ project.acronyme }}
      </a>
    </div>
    <div class='card-body'>
    <p>
      <b>Start year: </b>{{ project.year_start }}
    </p>
    <p>
      <b>Title: </b>{{ project.title }}
    </p>
    </div>
  </div>
  
{% endfor %}
</div>

<h2>Archived Projects</h2>
<div class='card-list'>
{% for project in old_projects %}
  <div class='card'>
    <div class='card-header'>
      <a href="{{ project.url }}">
        {{ project.title }}
      </a>
    </div>
  </div>
{% endfor %}