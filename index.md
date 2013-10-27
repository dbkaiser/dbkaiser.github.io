---
layout: page
title: Hello World!
tagline: Supporting tagline
---
{% include JB/setup %}

{% for post in site.posts limit:2 %}
<div class="post">
  <div class="top">
     <time datetime="{{ post.date | xmlschema }}">{{ post.date | date: "%d %b" }}</time>
	 <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
  </div>
  <div class="content">
      {{ post.content}}
  </div>
  <div class="bottom">
      <span>{{post.date | date: "%A %D"}}</span>
  </div>
</div>
{% endfor %}

