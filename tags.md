---
layout: page
title: Tags
permalink: /tags/
---
<script language="javascript">
function toggle(id) {
    var ele = document.getElementById(id);
    var tag = document.getElementById(id + '-tag');
    if(ele.style.display == "block") {
          ele.style.display = "none";
          tag.style.filter = "invert(0%)";
    } else {
      ele.style.display = "block";
      tag.style.filter = "invert(100%)";
      window.location.hash = id;
    }
}
</script>
<ul class="tag-cloud">
{% assign tags_list = site.tags %}
{% if tags_list.first[0] == null %}
    {% for tag in tags_list %}
    <li id="{{ tag }}-tag" style="font-size: {{ tag | last | size | times: 100 | divided_by: tags_list.size | plus: 70 }}%">
        <a href="javascript:toggle('{{ tag }}');">
          {{ tag }}
        </a>
    </li>
    {% endfor %}
{% else %}
    {% for tag in tags_list %}
    <li id="{{ tag[0] }}-tag" style="font-size: {{ tag | last | size | times: 100 | divided_by: tags_list.size | plus: 70 }}%">
        <a href="javascript:toggle('{{ tag[0] }}');">
          {{ tag[0] }}
        </a>
    </li>
    {% endfor %}
{% endif %}
{% assign tags_list = nil %}
</ul>
{% for tag in site.tags %}
<div id="{{ tag[0] }}" style="display: none">
    <h2 class='tag-header' id="{{ tag[0] }}">{{ tag[0] }}</h2>
    <ul>
      {% assign pages_list = tag[1] %}
      {% for node in pages_list %}
        {% if node.title != null %}
          {% if group == null or group == node.group %}
            {% if page.url == node.url %}
            <li class="active">
              <a href="{{ site.baseurl }}{{ node.url }}" class="active">{{ node.title }}</a>
            </li>
            {% else %}
            <li>
              {% if node.category == 'link' %}
              <a href="{{ node.external-url }}" class="external-link">{{ node.title }}</a>
              {% elsif node.category == 'project' and site.github_user %}
              <a href="https://github.com/{{ site.github_user }}/{{ node.title }}" class="github-project-link">{{ node.title }}</a>
              {% else %}
              <a href="{{ site.baseurl }}{{ node.url }}">{{ node.title }}</a>
              {% endif %}
            </li>
            {% endif %}
          {% endif %}
        {% endif %}
      {% endfor %}
      {% assign pages_list = nil %}
      {% assign group = nil %}
    </ul>
</div>
{% endfor %}
