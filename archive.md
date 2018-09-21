---
layout: page
title: Archive
permalink: /archive/
---

<div class="archives" itemscope itemtype="http://schema.org/Blog">
{% for post in site.posts reversed %}
{% if post.layout == 'post' %}
	{% capture date %}{{ post.date }}{% endcapture %}
  {% capture this_year %}{{ date | date: "%Y" }}{% endcapture %}
  {% unless year == this_year %}
	  {% assign year = this_year %}
	  {% unless forloop.first %}
		  </ul>
	  {% endunless %}
	  <h2 class="year">{{ date | date: "%Y" }}</h2>
	  <ul>
  {% endunless %}
	<li>
        {% if post.category == 'link' %}
        <a href="{{ post.external-url }}" class="external-link">{{post.title}}</a>
        {% elsif post.category == 'project' and site.github_user %}
        <a href="https://github.com/{{ site.github_user }}/{{ post.title }}" class="github-project-link">{{post.title}}</a>
        {% else %}
        <a href="{{ site.baseurl }}{{ post.url }}">{{post.title}}</a>
        {% endif %}
	</li>
{% endif %}
{% endfor %}
  </ul>
</div>
