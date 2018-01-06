---
layout: portfolio
title: Portfolio
---

{% assign allRepos = site.github.public_repositories | where: 'fork', 'false' %}
{% assign groupedByStars = allRepos | sort: 'stargazers_count', 'last' | reverse | group_by: 'stargazers_count' %}
<!-- sort these by my preference -->
<ul id="portfolio-list">
{% for group in groupedByStars %}
  {% assign reposSortedByForks = group.items | sort: 'forks_count', 'last' | reverse %}
  {% for repository in reposSortedByForks %}
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
            {% octicon star %} {{ repository.stargazers_count }} Stars &nbsp;&nbsp;&nbsp;{% octicon repo-forked %} {{ repository.forks_count }} Forks
          </p>
          <p style="opacity: 0.54">
            {{ repository.description }}
          </p>
        </div>
        <!-- <div class="portfolio-item-action-bar">
          <button class="portfolio-item-button">VIEW</button>
        </div> -->
      </div>
    </li>
  {% endfor %}
{% endfor %}
</ul>

<!-- http://codepen.io/ettrics/pen/Jdjdzp -->
<!-- http://codepen.io/mistkaes/pen/EjQzxy -->
<!-- https://github.com/Shopify/liquid/wiki/Liquid-for-Designers -->
<!-- Consider adding "star repo url" with button see docs for "starred_url" at https://developer.github.com/v3/repos/#list-organization-repositories -->
<!-- Consider adding an indicator if it is owned by someone else and it was a forked project for external contribution -->
