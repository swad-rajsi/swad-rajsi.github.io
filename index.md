---
layout: default
title: "Home"
---

# Welcome to My Cooking Blog 👩‍🍳🍲

Explore delicious vegetarian recipes, modern twists, and quick meals.

👉 Browse all **[Recipes](/recipes/)**  
👉 Learn more **[About Me](/about/)**  
👉 Get in touch **[Contact](/contact/)**

---
## Latest Recipes

<ul>
  {% for recipe in site.recipes %}
    <li>
      <a href="{{ recipe.url }}">{{ recipe.title }}</a>
    </li>
  {% endfor %}
</ul>
