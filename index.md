---
layout: default
title: "Home"
---
<table style="b3ackground-color: #f7b7f0ff; height:100%;width:100%;">
<tr>
<td style="width:60%; vertical-align:top;background-color: #f7b7f0ff;"><img src="/assets/images/Cover.png" alt="Cover" width="100%"></td>
<td style="width:50%; vertical-align:top;background-color: #f7b7f0ff;">
  <div style="padding-left:40px;padding-right:40px;padding-top:50px;display: flex;justify-content: center;align-items: center;">
  <p style="font-size:32px; font-style:oblique;font-family:cursive;">Explore delicious vegetarian recipes, modern twists, and quick meals</p>
  </div>
  <div style="padding-left:40px;padding-right:40px;padding-bottm:50px;display: flex;justify-content: center;align-items: center;margin-top:-30px;">
  <p style="font-size:20px;">Join me in my love of food & cooking!</p>
  </div>
  <div  style="padding-left:40px;padding-right:40px;padding-bottm:50px;display: flex;justify-content: center;align-items: center;"><a class="swad-rajsi-read-now" href="{{ '/recipes/' | relative_url }}">READ NOW</a></div>
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
