---
layout:     default
permalink:  "/posts/"
author:   HaloSern
menutitle: Post
title:     Post
---

<div id="content" class="content">
    <ul class="category recent-posts">       
        {% for post in site.posts %}
        {% unless post.draft %}
        
        {% if post.menutitle %}
        {% assign title = post.menutitle %}
        {% else %}
        {% assign title = post.title %}
        {% endif %}
        {% capture year %}{{ post.date | date: '%Y %b' }}{% endcapture %}
        {% capture nyear %}{{ post.next.date | date: '%Y %b' }}{% endcapture %}
        {% if year != nyear %}
            <br>
            <h3>{{ post.date | date: '%Y %b' }}</h3>
            <br>
          {% endif %} 
        <li>
            <div class="article">
                <article class="article" itemscope itemtype="http://schema.org/BlogPosting">
                    <header class="post-header">
                        <span class="title"><a itemprop="name" href="{{ post.url | prepend: site.github.url | prepend: site.baseurl}}" title="{{ title }}">{{ title }}</a></span>
                        <time class="date" itemprop="datePublished" datetime="{{post.date | date: "%Y-%m-%d"}}">{{post.date | date: "%B %e, %Y"}}</time>
                    </header>
                </article>

            </div>
        </li>
        {% endunless %}
        {% endfor %}
    </ul>
</div>