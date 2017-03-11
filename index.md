---
layout: page
title: Welcome!
tagline: Data Science, and general nerdery
---
{% include JB/setup %}


Welcome to my blog on Data Scicene and generally nerdery!

This is a very early work in progress, so please excuse the mess.

Blog post list:

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>



