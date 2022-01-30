---
layout: splash
permalink: /projects
read_time: false
header:
  overlay_color: "#5e616c"
  overlay_image: /assets/images/mm-home-page-feature.jpg
excerpt: <h2><FONT color="#ffffff">Projects</FONT></h2>

---
{% assign old_projects = site.projects | where: "type", "old" %}
{% assign current_projects = site.projects | where_exp: "proj", "proj.type == 'current'" | sort: 'year_start' | reverse%}


<h2>Current Projects</h2>
<div class='card-list'>
{% for project in current_projects %}
<div class='card'>
  <div class='card-header'>
        
      <a href="{{ project.url }}">
        <center>
        <strong>
          {{ project.acronyme }}
        </strong>
        </center>
      </a>
    
    </div>
    <div class='card-body'>
      
    {% if project.image %}
      <div class="project__image">
         <a href="{{ project.url | relative_url }}">
          <img src="{{ project.image | relative_url }}" alt="{{ project.image }}" itemprop="image">
        </a>
      </div>
    {% endif %}      
      
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
        <center>
        <strong>
          {{ project.title }}
        </strong>
        </center>
      </a>
    </div>
  </div>
{% endfor %}
