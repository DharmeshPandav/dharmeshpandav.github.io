---
layout: page
title: Archive
---
<div class="card card-background-none">
    <ul class="related-posts ">

        {% for post in site.posts %}

          {% assign post_month_year = post.date | date: "%B %Y" %}
          {% assign newer_post_month_year = post.next.date | date: "%B %Y" %}
          {% if post_month_year != newer_post_month_year %}
            <div class="archive-title"><strong>
                {{ post_month_year }}
            </strong></div>
          {% endif %}

          <li>
            {% comment %}
                {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})
            {% endcomment %}

            {{ post.date | date_to_string }} &raquo;
            <a href="{{ post.url }}">
               {{ post.title }}
            </a>
          </li>
        {% endfor %}

    </ul>

</div>
