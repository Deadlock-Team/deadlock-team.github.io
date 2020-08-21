---
layout: page
title: Wtf
description: "What The actual F*ck is ... ?"
permalink: /wtf/
---
<div class="home">
    {% for post in site.categories["WTF"] %}
      {% capture current_year %}{{ post.date | date: "%Y" }}{% endcapture %}
        {% if current_year != previous_year %}
          {% unless forloop.first %}
            </ul>
          {% endunless %}
          <h2>{{ current_year }}</h2>
          <ul class="post-list">
          {% assign previous_year = current_year %}
        {% endif %}
        <li>
            {% if post.event != "" %}
                <span class="post-meta"><a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.event }} - {{ post.title }}</a></span>
            {% else %}
                <span class="post-meta"><a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></span>
            {% endif %}
        </li>
        {% if forloop.last %}
          </ul>
        {% endif %}
    {% endfor %}
</div>