---
layout: page
title: "Coding Posts"
permalink: coding/
---

<ul class="post-list">
	{% for post in site.posts %}
		{% if post.categories contains 'coding' %}
			{% capture currentyear %}{{ post.date | date: "%Y" }}{% endcapture %}

			{% if currentyear != year %}
				<li><h2>&mdash;&nbsp;&nbsp; {{ currentyear }}</h2></li>
				{% capture year %}{{currentyear}}{% endcapture %}
			{% endif %}

			<li>
				<a class="post-link" href="{{ post.url | prepend: site.url }}" title="{{ post.title }}">
					<h2><span class="post-meta">{{ post.date | date: "%Y-%m-%d" }}</span> – {{ post.title }}</h2>
				</a>
				<small>CATEGORY: {{ post.categories | join: ', ' | upcase }}</small>
			</li>
		{% endif %}
	{% endfor %}
</ul>
