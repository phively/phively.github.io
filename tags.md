---
layout: navpage-top
title: Tags
description: "An archive of posts sorted by tag"
---

<!-- Adapted from https://github.com/LanyonM/lanyonm.github.io/blob/master/tags.html -->

{% capture site_tags %}{% for tag in site.tags %}{{ tag | first }}{% unless forloop.last %},{% endunless %}{% endfor %}{% endcapture %}
<!-- site_tags: {{ site_tags }} -->
{% assign tag_words = site_tags | split:',' | sort %}
<!-- tag_words: {{ tag_words }} -->

<div id="tags">
  {% for tag in tag_words) %}
    <a href="#{{ tag | cgi_escape }}">{{ tag }}<sup>{{ site.tags[tag] | size }}</sup></a>
  {% endfor %}


  {% for item in (0..site.tags.size) %}{% unless forloop.last %}
    {% capture this_word %}{{ tag_words[item] | strip_newlines }}{% endcapture %}
  <h2 id="{{ this_word | cgi_escape }}">{{ this_word }}</h2>
  <ul class="posts">
    {% for post in site.tags[this_word] %}{% if post.title != null %}
    <li itemscope><a href="{{ post.url }}##">{{ post.title }}</a> &ndash; <span class="entry-date"><time datetime="{{ post.date | date_to_xmlschema }}" itemprop="datePublished">{{ post.date | date: "%F" }}</time></span></li>
    {% endif %}{% endfor %}
  </ul>
  {% endunless %}{% endfor %}
</div>