---
layout: default
title: "Home"
---

<h3 style="font-size:90px;font-weight:100; color:#eba0eb;font-family:'Damion', serif;text-align:center;font-style:italic"> Taste Shahi </h3>
<table style="b3ackground-color: #f7b7f0ff">
<tr>
<td style="width:60%; vertical-align:top;"><img src="/assets/images/Cover.png" alt="Cover" width="100%"></td>
<td style="width:50%; vertical-align:top;background-color: #f7b7f0ff;">Explore delicious vegetarian recipes, modern twists, and quick meals.
</td>
</tr>
</table>

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
