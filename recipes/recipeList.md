---
layout: default
title: "All Recipes"
permalink: /recipes/
---

<div class="swad-rajsi-centre-display" style="margin-top:-30px;margin-bottom:10px;color: #d25fd2ff;font-size:20px;font-family:Georgia;justify-content:left !important;" >
All Recipes
</div>

<!-- <h3>DEBUG: Total recipes = {{ site.recipes | size }}</h3> -->
{% include recipe-gallery.html %}

<div class="recipe-search" style="padding-top:10px;">
  <div style="margin-left:30px;padding-bottom:10px;">
    {% assign flavours = site.recipes | map: "flavour" | uniq | sort %}
    <select id="flavourFilter" class="recipe-search-select">
        <option value="">All Flavours</option>
        {% for f in flavours %}
        <option value="{{ f | downcase }}">{{ f }}</option>
        {% endfor %}
    </select>

    {% assign food_types = site.recipes | map: "food_type" | uniq | sort %}
    <select id="foodTypeFilter" class="recipe-search-select">
        <option value="">All Types</option>
        {% for t in food_types %}
        <option value="{{ t | downcase }}">{{ t }}</option>
        {% endfor %}
    </select>

    {% assign course = site.recipes | map: "course" | uniq | sort %}
    <select id="courseFilter" class="recipe-search-select">
        <option value="">All Courses</option>
        {% for c in course %}
        <option value="{{ c | downcase }}">{{ c }}</option>
        {% endfor %}
    </select>

    <select id="durationFilter" class="recipe-search-select">
      <option value="144000">Cook under:(Time)</option>
      <option value="15">15 minutes</option>
      <option value="30">30 minutes</option>
      <option value="45">45 minutes</option>
      <option value="60">1 Hour</option>
      <option value="90">1.5 Hours</option>
      <option value="120">2 Hours</option>
      <option value="480">8 Hours</option>
      <option value="1440">24 Hours</option>
    </select>


    <a href="#" id="clearFilters" class="clear-filters">Clear Filters</a>
    </div>
    <div id="recipeList"></div>

</div>


<script>
  const recipes = [
    {% for recipe in site.recipes %}
      {
          "title": "{{ recipe.title | escape }}",
          "url": "{{ recipe.url | relative_url }}",
          "flavour": "{{ recipe.flavour | escape }}",
          "food_type": "{{ recipe.food_type | escape }}",
          "course": "{{ recipe.course | escape }}",
          "total_time":{{ recipe.total_time }}
      } {% if forloop.last == false %}, {% endif %}
    {% endfor %}
  ];

  const searchInput = document.getElementById("searchInput");
  const flavourFilter = document.getElementById("flavourFilter");
  const foodTypeFilter = document.getElementById("foodTypeFilter");
  const courseFilter = document.getElementById("courseFilter");
  const durationFilter = document.getElementById("durationFilter");
  const recipeList = document.getElementById("recipeList");
  const clearFilters = document.getElementById("clearFilters");

  function renderRecipes(list) {
      recipeList.innerHTML = `
        <ul>
          ${list.map(r => `
            <li>
              <a href="${r.url}" class="swad-rajsi-recipe-link">${r.title}</a>
            </li>
          `).join('')}
        </ul>
      `;
  }

  // Initial render
  renderRecipes(recipes);

  function filterRecipes() {
    const flavour = flavourFilter.value.toLowerCase();
    const food_type = foodTypeFilter.value.toLowerCase();
    const course = courseFilter.value.toLowerCase();
    const duration = Number(durationFilter.value);
    const filtered = recipes.filter(r => {
        const matchesFlavour = flavour === "" || r.flavour.toLowerCase().includes(flavour);
        const matchesFoodType = food_type === "" || r.food_type.toLowerCase().includes(food_type);
        const matchesCourse = course === "" || r.course.toLowerCase().includes(course);
        const matchesDuration = duration === 144000 || r.total_time <= duration;
        return matchesFlavour && matchesFoodType && matchesCourse && matchesDuration;
    });

    renderRecipes(filtered);
  }

  flavourFilter.addEventListener("change", filterRecipes);
  foodTypeFilter.addEventListener("change", filterRecipes);
  courseFilter.addEventListener("change", filterRecipes);
  durationFilter.addEventListener("change", filterRecipes);

  clearFilters.addEventListener("click", function(e) {
  e.preventDefault(); // Prevent default anchor behavior
  flavourFilter.value = "";
  foodTypeFilter.value = "";
  courseFilter.value = "";
  durationFilter.value = 144000;
  renderRecipes(recipes); // Show all recipes
});

</script>
<!-- <ul>
{% for recipe in site.recipes %}
  <li>
    <a href="{{ recipe.url }}"  class="swad-rajsi-recipe-link">{{ recipe.title }}</a>
  </li>
{% endfor %}
</ul> -->