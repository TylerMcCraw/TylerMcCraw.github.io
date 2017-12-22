---
layout: portfolio
title: Portfolio
---

<!-- sort these by my preference -->
<ul id="portfolio-list">
{% for repository in site.github.public_repositories %}
  <li>
    <div class="portfolio-item">
      <div class="portfolio-item-image" style="background-color: #424242"></div>
      {% if repository.fork == false %}
    	    <h3 class="portfolio-item-header"><a href="{{ repository.html_url }}">{{ repository.name }}</a></h3>
      {% else %}
    	    <h3 class="portfolio-item-header"><a href="{{ repository.html_url }}">{{ repository.name }}</a></h3>
      {% endif %}
      <div class="portfolio-item-text">
        <p style="opacity: 0.87"> <!-- Clean this up -->
          <i class="material-icons md-18">&#xE838;</i> {{ repository.stargazers_count }} Stars <i class="material-icons md-18">&#xE0B6;</i> {{ repository.forks_count }} Forks
        </p>
        <p style="opacity: 0.54">
          {{ repository.description }}
        </p>
      </div>
      <div class="portfolio-item-action-bar">
        <button class="portfolio-item-button">VIEW</button>
      </div>
    </div>
  </li>
{% endfor %}
</ul>

<!-- http://codepen.io/ettrics/pen/Jdjdzp -->
<!-- http://codepen.io/mistkaes/pen/EjQzxy -->
<!-- https://github.com/Shopify/liquid/wiki/Liquid-for-Designers -->
<!-- Consider adding "star repo url" with button see docs for "starred_url" at https://developer.github.com/v3/repos/#list-organization-repositories -->
<!-- Consider adding an indicator if it is owned by someone else and it was a forked project for external contribution -->
