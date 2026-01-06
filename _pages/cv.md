---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

<a href="/files/cjmack_resume.pdf" class="btn btn--primary" download>📄 Download Resume (PDF)</a>

---

## Education

**Ph.D. in Oceanography** (In Progress)  
Scripps Institution of Oceanography, UC San Diego  
*Focus: Climate change mitigation and marine carbon dioxide removal*

---

## Research Experience

**Graduate Researcher** | Scripps Institution of Oceanography  
*2022 – Present*  
- Leading research on scalability of ocean alkalinity enhancement
- Analyzing governance frameworks for marine carbon removal
- Developing coastal monitoring methods using LiDAR technology

---

## Skills

**Programming & Data Analysis**
- Python (NumPy, Pandas, Matplotlib, Xarray)
- R for statistical analysis
- Data visualization and scientific computing

**Geospatial & Remote Sensing**
- LiDAR data processing
- GIS applications
- Coastal monitoring techniques

**Research & Communication**
- Scientific writing and peer review
- Policy analysis and stakeholder engagement
- Conference presentations

---

## Publications

<ul>{% for post in site.publications reversed %}
  {% include archive-single-cv.html %}
{% endfor %}</ul>

---

## Presentations

<ul>{% for post in site.talks reversed %}
  {% include archive-single-talk-cv.html %}
{% endfor %}</ul>
