---
layout: page
title: Archive
---

## Blog Posts

{% for post in site.posts %}

  {% assign post_month_year = post.date | date: "%B %Y" %}
  {% assign newer_post_month_year = post.next.date | date: "%B %Y" %}
  {% if post_month_year != newer_post_month_year %}
    
    <strong>  {{ post_month_year }} </strong>
    
  {% endif %}
  
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})
{% endfor %}