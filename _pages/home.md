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
feature_row:
  - image_path: /assets/images/mm-customizable-feature.png
    alt: "Resources"
    title: "Resources"
    excerpt: "Take a look at publications and presentations from the team as well as some documentation"
    url: "/resources"
    btn_class: "btn--primary"
    btn_label: "Learn more"
  - image_path: /assets/images/mm-responsive-feature.png
    alt: "Team"
    title: "Meet the Team"
    excerpt: "Come meet our team of Researchers, PhD Students and Post Docs"
    url: "/team"
    btn_class: "btn--primary"
    btn_label: "Learn more"
  - image_path: /assets/images/mm-free-feature.png
    alt: "Projects"
    title: "Projects"
    excerpt: "Check out the projects we are working on and the ones in the pipeline"
    url: "/projects"
    btn_class: "btn--primary"
    btn_label: "Learn more"     
---

<!-- {% include vtkElevationReader.html %} -->
<div style="text-align: center;display: flex;flex-wrap: wrap;justify-content: space-evenly;margin-bottom: 2em;">
  <iframe src='https://kitware.github.io/paraview-glance/app/?name=202-t.glance&url=https://raw.githubusercontent.com/CEREGE-CL/CEREGE-CL.github.io/main/assets/data/homepage.glance' style="height: 400px; width: 40%; flex: 1 1 300px; margin: 1em"></iframe>
  <div style="position: relative; height:400px; flex: 1 1 300px; margin: 1em">
    <iframe src='https://earth.nullschool.net/' style="width: 100%;height: 100%;position: relative;"> </iframe>
    <p style="position: absolute;bottom: -1em;right: 0.1em;background: gray;font-size: 10px;">
      Source = https://earth.nullschool.net
    </p>
  </div>
</div>

{% include feature_row %}
