---
layout: page
title: Thoughts and Code 
tagline: (in no particular order)
---
{% include JB/setup %}

{% for post in site.posts offset: 0 limit: 50 %}
<div class="row-fluid">
      <div class="span12">
		<h4><strong><a href="{{ post.url }}">{{ post.title }}</a></strong></h4>
        <p>
          {{ post.summary }}
        </p>
        <p><span>{{ post.date | date_to_long_string }}</span> — <a href="{{ post.url }}">Read more</a></p>
      </div>
</div>
{% endfor %}	


