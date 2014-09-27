---
layout: default
title: Archive
---


{% for post in site.posts %}
<div><strong>
  {% assign post_month_year = post.date | date: "%B %Y" %}
  {% assign newer_post_month_year = post.next.date | date: "%B %Y" %}
  {% if post_month_year != newer_post_month_year %}
    {{ post_month_year }}      
    
  {% endif %}
</strong></div>
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})
{% endfor %}
