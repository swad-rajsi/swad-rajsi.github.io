---
layout: default
title: "All Recipes"
permalink: /recipes/
---

<div class="swad-rajsi-centre-display" style="margin-top:-30px;margin-bottom:10px;color: #d25fd2ff;font-size:20px;font-family:Georgia;justify-content:left !important;" >
All Recipes
</div>

<ul>
{% for recipe in site.recipes %}
  <li>
    <a href="{{ recipe.url }}"  class="swad-rajsi-recipe-link">{{ recipe.title }}</a>
  </li>
{% endfor %}
</ul>
