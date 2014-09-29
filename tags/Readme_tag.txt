how to use Tag in the website...

 when ever user Tags post with the "new" tag. ( *other than the existing tags)
he must follow below mentioned step to include tag navigation.
until we host this website on over private server where executing third-party plugins is allowed.

(as soon as new Tag will be added with the front matter layout: page ..it will be added in tag list tags->index.html)

1. create a folder with the same name as Tags name ( case sensitive)  ...recommended to use lower case tag name without space
2. create an index.html file inside that folder.
3. include this Front matter in the file
---
layout: tags
title: {{ Exact name of the tag }}
---

4. below that paste the following code


    {% assign flag = false %}

    <ul class="related-posts">

        {% for post in site.posts %}

		{% assign flag = false %}
		{% for tag in post.tags %}
			{% if tag == page.title %}
				{% assign flag = true %}
			{% endif %}
		{% endfor %}

        {% if flag %}
        {% assign post_month_year = post.date | date: "%B %Y" %}
        {% assign newer_post_month_year = post.next.date | date: "%B %Y" %}

        {% if post_month_year != newer_post_month_year %}
        <div class="archive-title"><strong>
            {{ post_month_year }}
        </strong></div>
        {% endif %}

        <li>
            {{ post.date | date_to_string }} &raquo;
            <a href="{{ post.url }}">
                {{ post.title }}
            </a>
        </li>
        {% endif %}
        {% endfor %}
    </ul>

 <div class="inline-title">Other Tags</div>

{% for tag in site.tags %}
<div class="tag-list">
    <a class="firm" href="/tags/{{ tag[0] }}">{{ tag[0] }}</a>
    <span class="tag-icon-prefix"></span>
</div>
{% endfor %}

5. and you are good to go..now your website will be compiled with the tag based indexing