---
layout: splash
permalink: /
hidden: true
header:
  overlay_color: "#5e616c"
  overlay_image: /assets/images/mm-home-page-feature.jpg
  # actions:
  #   - label: "<i class='fas fa-download'></i> Install now"
  #     url: "/docs/quick-start-guide/"
excerpt: >
  Home of the CEREGE paleoclimate modelling group<br />
---

{% assign news_items = site.news | sort: "date" | reverse %}

<!-- CSS only -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/css/bootstrap.min.css" rel="stylesheet"  crossorigin="anonymous">

<script src="https://code.jquery.com/jquery-3.2.1.slim.min.js"
  integrity="sha384-KJ3o2DKtIkvYIK3UENzmM7KCkRr/rE9/Qpg6aAZGJwFDMVNA/GpGFF93hXpG5KkN"
  crossorigin="anonymous"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.12.9/umd/popper.min.js"
  integrity="sha384-ApNbgh9B+Y1QKtv3Rn7W3mgPxhU9K/ScQsAP7hUibX39j7fakFPskvXusvfa0b4Q"
  crossorigin="anonymous"></script>
<!-- <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.1/js/bootstrap.min.js"
  integrity="sha384-JZR6Spejh4U02d8jOt6vLEHfe/JQGiRRSQQxSfFWpi1MquVdAyjUar5+76PVCmYl"
  crossorigin="anonymous"></script> -->

  <!-- JavaScript Bundle with Popper -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/js/bootstrap.bundle.min.js"  crossorigin="anonymous"></script>

<div class="d-flex flex-row justify-content-around flex-wrap" style="margin: 1em;">
  <div class='p-2 flex-grow-1 flex-shrink-1 col-md-8 col-sm-12'>
    <div id="carouselExampleIndicators" class="carousel slide" data-ride="carousel">
      <ol class="carousel-indicators">
        {% for entry in news_items limit:5 %}
          {% if forloop.index0 == 0%}
        <li data-target="#carouselExampleIndicators" data-slide-to="0" class="active"></li>
        {% else %}
        <li data-target="#carouselExampleIndicators" data-slide-to="{{forloop.index0}}"></li>
        {% endif %}
        {% endfor %}
      </ol>
      <div class="carousel-inner">
      {% for entry in news_items limit:5 %}
        {% if forloop.index0 == 0%}
        <div class="carousel-item active">
        {% else %}
        <div class="carousel-item">
        {% endif %}
        {% if entry.img == blank %}
          <img class="d-block w-100 news-background" src="https://placeimg.com/1080/500/nature">
        {% else %}
          <img class="d-block w-100 news-background" src="{{entry.img}}">
        {% endif %}
          <div class="carousel-caption d-md-block" style="top:20px">
            <div class="card" style='color:black; opacity:0.7'>
              <div class='card-header'>
                <a href="{{entry.url}}">
                  <div>{{ entry.title }}</div>
                </a>
              </div>
                <div class="card-block p-1">
                  <div class='card-text'>
                    {{ entry.content }}
                    <small class="news-date">
                      {{ entry.date | date: "%-d %B %Y" }}
                    </small>
                  </div>
                </div>
              </div>
          </div>
        </div>
      {% endfor %}
      </div>
      <a class="carousel-control-prev" href="#carouselExampleIndicators" role="button" data-slide="prev">
        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
        <span class="sr-only">Previous</span>
      </a>
      <a class="carousel-control-next" href="#carouselExampleIndicators" role="button" data-slide="next">
        <span class="carousel-control-next-icon" aria-hidden="true"></span>
        <span class="sr-only">Next</span>
      </a>
    </div>
  </div>
  <div class='p-2 flex-grow-1 flex-shrink-1 col-md-4 col-sm-12'>
    <div class='news-aside'>
      <h5>News</h5>
      <ul class="news-list">
      {% for entry in news_items %}
      <li>
          <div class="d-flex flex-row justify-content-between align-items-baseline news-title">
            <a href="{{entry.url}}">
              {{entry.title}}
            </a>
            <small class="news-date">
              {{ entry.date | date: "%-d %B %Y" }}
            </small>
          </div>
          <small class="news-content">{{entry.content}}</small>
          {% if entry.link != blank %}
            <a href="{{entry.link | relative_url}}" class='btn btn-outline-info btn-sm'>
            Read more
            </a>
          {% endif %}
      </li>
      {% endfor %}
    </ul>
    </div>
  </div>
</div>
