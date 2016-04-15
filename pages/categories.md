---
title: 分类目录
permalink: /categories/
layout: default
nav: true
---

<div class="article">
    <h3 class="title">标签列表</h3>
    <hr>
    <ul class="categories" style=" list-style: none; ">
    {% assign categories_list = site.categories %}
    {% for category in categories_list %}
        <li class="categories-item" style="display:inline-block;font-size:14px;color:#555;background:#FFEFD5;border:1px solid #aaa;border-radius:2px;padding:1px 6px;margin:0 7px 7px 0;cursor:pointe; "><a href="{{ BASE_PATH }}{{ site.JB.categories_path }}#{{ category[0] }}-ref">
            {{ category[0] | join: "/" }}
        </a></li>
    {% endfor %}
    </ul>

<div class="article">
  <h3 class="title">归档</h3>
  <hr>
{% for category in site.categories %} 
  <h2 style="display:inline-block;font-size:14px;color:#555;background:#FFEFD5;border:1px solid #aaa;border-radius:2px;padding:1px 6px;margin:0 7px 7px 0;cursor:pointe;" class="article-year" id="{{ category[0] }}-ref" data-year="&diams;">{{ category[0] | join: "/" }}</h2>
  <ul style="list-style: none">
    {% assign pages_list = category[1] %}  
    {% for node in pages_list %}
      {% if node.title != null %}
        {% if group == null or group == node.group %}
            <li><a href="{{ BASE_PATH }}{{node.url}}">{{node.title}}</a></li>
        {% endif %}
      {% endif %}
    {% endfor %}
   
  </ul>
{% endfor %}
</div>
</div>