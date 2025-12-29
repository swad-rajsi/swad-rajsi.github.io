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
    {% assign all_flavours = "" | split: "" %}
    {% for recipe in site.recipes %}
      {% if recipe.flavour %}
        {% assign items = recipe.flavour | split: "," %}
        {% for item in items %}
          {% assign flavour = item | strip %}
          {% assign all_flavours = all_flavours | push: flavour %}
        {% endfor %}
      {% endif %}
    {% endfor %}
    {% assign flavours = all_flavours | uniq | sort %}
    <select id="flavourFilter" class="recipe-search-select">
        <option value="">ALL FLAVOURS</option>
        {% for flavour in flavours %}
          <option value="{{ flavour | downcase }}">{{ flavour }}</option>
        {% endfor %}
    </select>

    <div class="desktop-only">
    {% assign all_food_types = "" | split: "" %}
    {% for recipe in site.recipes %}
      {% if recipe.food_type %}
        {% assign items = recipe.food_type | split: "," %}
        {% for item in items %}
          {% assign food_type = item | strip %}
          {% assign all_food_types = all_food_types | push: food_type %}
        {% endfor %}
      {% endif %}
    {% endfor %}
    {% assign food_types = all_food_types | uniq | sort %}
    <select id="foodTypeFilter" class="recipe-search-select">
        <option value="">ALL TYPES</option>
        {% for food_type in food_types %}
          <option value="{{ food_type | downcase }}">{{ food_type }}</option>
        {% endfor %}
    </select>
    </div>

    {% assign all_courses = "" | split: "" %}
    {% for recipe in site.recipes %}
      {% if recipe.course %}
        {% assign items = recipe.course | split: "," %}
        {% for item in items %}
          {% assign course = item | strip %}
          {% assign all_courses = all_courses | push: course %}
        {% endfor %}
      {% endif %}
    {% endfor %}
    {% assign courses = all_courses | uniq | sort %}
    <select id="courseFilter" class="recipe-search-select">
        <option value="">ALL COURSES</option>
        {% for course in courses %}
          <option value="{{ course | downcase }}">{{ course }}</option>
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

    {% assign all_dietary_patterns = "" | split: "" %}
    {% for recipe in site.recipes %}
      {% if recipe.dietary_pattern %}
        {% assign items = recipe.dietary_pattern | split: "," %}
        {% for item in items %}
          {% assign dietary_pattern = item | strip %}
          {% assign all_dietary_patterns = all_dietary_patterns | push: dietary_pattern %}
        {% endfor %}
      {% endif %}
    {% endfor %}
    {% assign dietary_patterns = all_dietary_patterns | uniq | sort %}
    <select id="dietaryPatternFilter" class="recipe-search-select">
        <option value="">ALL DIETS</option>
        {% for dietary_pattern in dietary_patterns %}
          <option value="{{ dietary_pattern | downcase }}">{{ dietary_pattern }}</option>
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
  const dietaryPatternFilter = document.getElementById("dietaryPatternFilter");
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
        const matchesDietaryPattern = dietary_pattern === "" || r.dietary_pattern.toLowerCase().includes(dietary_pattern);
        const matchesCourse = course === "" || r.course.toLowerCase().includes(course);
        const matchesDuration = duration === 144000 || r.total_time <= duration;
        return matchesFlavour && matchesFoodType && matchesDietaryPattern && matchesCourse && matchesDuration;
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