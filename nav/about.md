---
layout: page
title: About
---

<a href="{{ site.baseurl}}/about">
<i class="fa fa-group fa-fw"></i> About Us</a>

<a href="{{ site.baseurl}}/docs">
<i class="fa fa-question-circle fa-fw"></i> Course Development Help</a>

{% if site.github.repo == 'https://github.com/ryanpeek/semester-biology' %}
Contact Us
: <a href="{{ site.github.repo }}">
  <i class="fa fa-github fa-fw"></i> On GitHub</a>
: <a href="mailto:{{ site.email }}">
  <i class="fa fa-envelope fa-fw"></i> Via Email</a>
{% else %}
Contact Us
: About Course Materials: <a href="{{ site.github.repo }}">
  <i class="fa fa-github fa-fw"></i> On GitHub</a> |
  <a href="mailto:{{ site.email }}">
  <i class="fa fa-envelope fa-fw"></i> Via Email</a>
: About Course Website: <a href="https://github.com/gge-ucd/wRangling-Ecology">
  <i class="fa fa-github fa-fw"></i> On GitHub</a> |
  <a href="mailto:rapeek@ucdavis.edu">
  <i class="fa fa-envelope fa-fw"></i> Via Email</a>
{% endif %}
