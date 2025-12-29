---
layout: default
title: "All Recipes"
permalink: /recipes/
---
<!-- <div class="swad-rajsi-centre-display" style="margin-top:-30px;margin-bottom:10px;color: #d25fd2ff;font-size:20px;font-family:Georgia;justify-content:left !important;" >
All Recipes
</div> -->
{% include recipe-gallery.html %}

<div class="recipe-search" style="padding-top:10px;">
  <div class="all-recipes-filter-row" style="margin-left:1em;padding-bottom:0.5em;">
    {% assign flavours = site.recipes | map: "flavour" | uniq | sort %}
    <select id="flavourFilter" class="recipe-search-select">
        <option value="">ALL FLAVOURS</option>
        {% for f in flavours %}
          {% assign flavour_items = f | split: ',' %}
          {% for item in flavour_items %}
            {% assign flavour = item | strip %}
            <option value="{{ flavour | downcase }}">{{ flavour }}</option>
            {% endfor %}
          {% endfor %}
    </select>

    <div class="desktop-only">
    {% assign food_types = site.recipes | map: "food_type" | uniq | sort %}
    <select id="foodTypeFilter" class="recipe-search-select">
        <option value="">ALL TYPES</option>
        {% for f in food_types %}
          {% assign food_types_items = f | split: ',' %}
          {% for item in food_types_items %}
            {% assign food_type = item | strip %}
            <option value="{{ food_type | downcase }}">{{ food_type }}</option>
            {% endfor %}
          {% endfor %}
    </select>
    </div>

    {% assign courses = site.recipes | map: "course" | uniq | sort %}
    <select id="courseFilter" class="recipe-search-select">
        <option value="">ALL COURSES</option>
        {% for f in courses %}
          {% assign courses_items = f | split: ',' %}
          {% for item in courses_items %}
            {% assign course = item | strip %}
            <option value="{{ course | downcase }}">{{ course }}</option>
            {% endfor %}
          {% endfor %}
    </select>

    <select id="durationFilter" class="recipe-search-select">
      <option value="144000">TOTAL TIME IN</option>
      <option value="15">15 minutes</option>
      <option value="30">30 minutes</option>
      <option value="45">45 minutes</option>
      <option value="60">1 hour</option>
      <option value="90">1.5 hours</option>
      <option value="120">2 hours</option>
      <option value="480">8 hours</option>
      <option value="1440">24 hours</option>
    </select>

    {% assign dietary_patterns = site.recipes | map: "dietary_pattern" | uniq | sort %}
    <select id="dietaryPatternFilter" class="recipe-search-select">
        <option value="">ALL DIETS</option>
        {% for f in dietary_patterns %}
          {% assign dietary_patterns_items = f | split: ',' %}
          {% for item in dietary_patterns_items %}
            {% assign dietary_pattern = item | strip %}
            <option value="{{ dietary_pattern | downcase }}">{{ dietary_pattern }}</option>
            {% endfor %}
          {% endfor %}
    </select>

    <a href="#" id="clearFilters" class="clear-filters">Clear Filters</a>
    </div>
    <div id="recipeList" class="multi-column-list" style="margin-top:1em;"></div>

</div>

<script>
  const recipes = [
    {% for recipe in site.recipes %}
      {
          "title": "{{ recipe.title | escape }}",
          "url": "{{ recipe.url | relative_url }}",
          "flavour": "{{ recipe.flavour | escape }}",
          "food_type": "{{ recipe.food_type | escape }}",
          "dietary_pattern": "{{ recipe.dietary_pattern | escape }}",
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
    const dietary_pattern = dietaryPatternFilter.value.toLowerCase();
    const course = courseFilter.value.toLowerCase();
    const duration = Number(durationFilter.value);
    const filtered = recipes.filter(r => {
        const matchesFlavour = flavour === "" || r.flavour.toLowerCase().includes(flavour);
        const matchesFoodType = food_type === "" || r.food_type.toLowerCase().includes(food_type);
         const matchesFoodType = dietary_pattern === "" || r.dietary_pattern.toLowerCase().includes(dietary_pattern);
        const matchesCourse = course === "" || r.course.toLowerCase().includes(course);
        const matchesDuration = duration === 144000 || r.total_time <= duration;
        return matchesFlavour && matchesFoodType && matchesCourse && matchesDuration;
    });

    renderRecipes(filtered);
  }

  flavourFilter.addEventListener("change", filterRecipes);
  foodTypeFilter.addEventListener("change", filterRecipes);
  dietaryPatternFilter.addEventListener("change", filterRecipes);
  courseFilter.addEventListener("change", filterRecipes);
  durationFilter.addEventListener("change", filterRecipes);

  clearFilters.addEventListener("click", function(e) {
  e.preventDefault(); // Prevent default anchor behavior
  flavourFilter.value = "";
  foodTypeFilter.value = "";
  dietaryPatternFilter.value = "";
  courseFilter.value = "";
  durationFilter.value = 144000;
  renderRecipes(recipes); // Show all recipes
});

</script>