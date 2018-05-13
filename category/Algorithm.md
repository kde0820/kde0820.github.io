---
layout: default
---

<ul>
	{% for post in site.categories.Algorithm %}
	<li><a href="{{ post.url }}">{{ post.title }}</a></li>
	{% endfor %}
</ul>