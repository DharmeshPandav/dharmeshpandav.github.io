---
layout: page
title: Archive
---

## Blog Posts

{% for post in site.posts %}

  {% assign post_month_year = post.date | date: "%B %Y" %}
  {% assign newer_post_month_year = post.next.date | date: "%B %Y" %}
  {% if post_month_year != newer_post_month_year % or newer_post_month_year == null}
    <h3 class="section-header-archive">
      {{ post_month_year }}
      {{ newer_post_month_year }}
    </h3>
  {% endif %}
  
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})
{% endfor %}