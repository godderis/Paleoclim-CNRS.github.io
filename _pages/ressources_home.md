---
layout: splash
permalink: /resources
read_time: false
header:
  overlay_color: "#5e616c"
  overlay_image: /assets/images/mm-home-page-feature.jpg
  # actions:
  #   - label: "<i class='fas fa-download'></i> Install now"
  #     url: "/docs/quick-start-guide/"
excerpt: <h2><FONT color="#ffffff">Resources</FONT></h2>

feature_rowl1:
  - image_path: /assets/images/man-woman-reading.jpg
    alt: "Publications"
    title: "Publications"
    excerpt: 'Want to see the latest articles from the group come and check them out here'
    url: "/resources/publications"
    btn_label: "Read More"
    btn_class: "btn--primary"
feature_rowr1:
  - image_path: /assets/images/pointing-at-postit.jpg
    alt: "Presentations"
    title: "Presentations"
    excerpt: 'Or maybe you would prefer to look at some of our presentations to see what we have been up to'
    url: "/resources/presentations"
    btn_label: "Read More"
    btn_class: "btn--primary"
---

{% include feature_row id="feature_rowl1" type="left" %}

{% include feature_row id="feature_rowr1" type="right" %}
