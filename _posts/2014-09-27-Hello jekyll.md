---
layout: post
title : Hello Jekyll , Poole-lanyon and GitHub Pages
tags:
- mytag
permalink: hello-jekyll21
excerpt: this is my Third post using Jekyll , poole on Github pages
---

<div class="message">
  Hello world !! <Br>
   Say hello to my first blog using Awesome Parsing Engine - <strong>jekyll</strong>
   ,minimal blogging framework with no bloat code <strong>lanyon-Poole</strong> ,
   Robust-Free-Opensource Repository - <strong>Github</strong> And Free Hosting Service <strong>GitHub Pages</strong> 
</div>

{% highlight sql %}
    select t.* from mytable where  t.name = "my" AND t.id = 1
    
    Insert into mytable (A,B,C) VALUES  ( 1, 2,3)
{% endhighlight %}


{% highlight java linenos %}

Public Class myclass implements runnable {
    Public static void main(args[]){
        system.out.println("Hello World");
    }
}
   
{% endhighlight %}


<div> this is the gist from Github to list all the Tags used in the Static site ..this will be usefull in created Tag cloud and easy navigation </div>

{% gist DharmeshPandav/6302910d68176935fed4 %}

<div> one more try at GIST </div>

{% gist DharmeshPandav/TagList %}


{% highlight ruby %}
{% for tag in site.tags %}
    <div class="tag-list">
        <a class="firm" href="/tags/{{ tag[0] }}">{{ tag[0] }}</a>
        <span class="tag-icon-prefix"></span>
    </div>
    {% endfor %}
{% endhighlight  %}