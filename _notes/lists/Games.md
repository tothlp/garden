---
title: Games
format: list
description: Egy nem teljes lista azokról a játékokról, amiket kitoltam az évek során.
permalink: /games
---

{% assign games_by_year = site.data.games | reverse | group_by:"year" %}
{% for year in games_by_year %}
  <h3> {{ year.name }} </h3>

  <div class="grid-container">
{% for game in year.items %}
  <div class="grid-item" style="background-image: url('{{'/assets/img/covers/' | append: game.cover | relative_url }}');">
    <!-- <img src="{{'/assets/img/covers/' | append: game.cover | relative_url }}" alt="{{game.cover}}"> -->
      <div class="overlay">
          <p class="item-title">{{ game.title }} </p>
          <p class="item-icon">
              {% if game.platform == "PS" %}
                <i class="fa-brands fa-playstation"></i>
              {% elsif game.platform == "PC" %}
                <i class="fa-solid fa-desktop" alt="PC"></i>
              {% elsif game.platform == "XBOX" %}
                <i class="fa-brands fa-xbox"></i>
              {% endif %}
          </p>
      </div>
  </div>    
{% endfor %}
  </div>

{% endfor %}