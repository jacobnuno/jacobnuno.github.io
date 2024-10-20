---
layout: default
title: "Archive"
permalink: /archive/
---

<h1>The Archives</h1>
<ul class="posts">
    {% for post in site.posts %}
        <li>
            <span class="post-meta">{{ post.date | date_to_string }} - </span>
            <a href="{{ post.url | relative_url }}">
                {{ post.title | escape }}
            </a>
        </li>
    {% endfor %}
</ul>
