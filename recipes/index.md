---
layout: default
title: "All Recipes"
permalink: /recipes/
---

# All Recipes

<ul>
{% for recipe in site.recipes %}
  <li>
    <a href="{{ recipe.url }}">{{ recipe.title }}</a>
  </li>
{% endfor %}
</ul>
