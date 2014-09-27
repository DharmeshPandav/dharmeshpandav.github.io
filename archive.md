---
layout: page
title: Archive
---

<ul class="related-posts">

{% for post in site.posts %}

  {% assign post_month_year = post.date | date: "%B %Y" %}
  {% assign newer_post_month_year = post.next.date | date: "%B %Y" %}
  {% if post_month_year != newer_post_month_year %}
<p><strong>
    {{ post_month_year }}
</strong></p>
  {% endif %}
  
  <li>
    {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})
    <a href="{{ post.url }}">
       {{ post.title }}
    </a>
  </li>   
{% endfor %}

</ul>