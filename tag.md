---
layout: page
permalink: /tag
title: Posts Grouped by Tag
---

<section id="tag-archives">
{% for tag in site.tags %}
  {% capture tag_name %}{{ tag | first }}{% endcapture %}
  <a id="{{ tag_name | downcase | replace: ' ', '-' }}"></a>
  <h4>#{{ tag_name }}</h4>
  <ul>
  {% for post in site.tags[tag_name] %}
    <li>
      <a href="{{ site.baseurl }}{{ post.url }}">{{post.title}}</a>
    </li>
  {% endfor %}
  </ul>
{% endfor %}
</section>
