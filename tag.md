---
layout: page
permalink: /tag
title: Posts Grouped by Tag
---

<section id="tag-archives">
{% for tag in site.tags %}
  {% capture tag_name %}{{ tag | first }}{% endcapture %}
  {% capture tag_count %}{{ site.tags[tag_name] | size }}{% endcapture %}
  <a id="{{ tag_name | downcase | replace: ' ', '-' }}"></a>
  <h2 class="tagcloud-title">{{ tag_name }} <span class='tag-count'>({{ tag_count }})</span></h2>
  <ul>
  {% for post in site.tags[tag_name] %}
    <li>
      <a href="{{ site.baseurl }}{{ post.url }}">{{post.title}}</a>
    </li>
  {% endfor %}
  </ul>
{% endfor %}
</section>
