---
layout: portfolio
title: Portfolio
---
<!-- Play Store -->
<h3 class="portfolio-header">Projects</h3>
<ul id="portfolio-list">
  <li>
    <div class="project-item">
      <div class="project-item-image" style="background-color: rgba(88,183,154,1)"></div>
      <h3 class="project-item-header"><a href="https://play.google.com/store/apps/details?id=com.paywithextend.extend">Extend</a></h3>
      <div class="project-item-footer">
        <p style="opacity: 0.54">
          The most convenient and secure way to send and request access to a credit card
        </p>
      </div>
      <div class="project-item-play-store-badge">
        <a href='https://play.google.com/store/apps/details?id=com.paywithextend.extend'>
          <img alt='Get it on Google Play' src='https://play.google.com/intl/en_us/badges/images/generic/en_badge_web_generic.png'/>
        </a>
      </div>
    </div>
  </li>
  <li>
    <div class="project-item">
      <div class="project-item-image" style="background-color: rgba(117,21,38,1)"></div>
      <h3 class="project-item-header"><a href="https://play.google.com/store/apps/details?id=com.ncfbins.android">NC Farm Bureau Insurance</a></h3>
      <div class="project-item-footer">
        <p style="opacity: 0.54">
          Make payments, report a claim, view your insurance cards, or contact your agent
        </p>
      </div>
      <div class="project-item-play-store-badge">
        <a href='https://play.google.com/store/apps/details?id=com.ncfbins.android'>
          <img alt='Get it on Google Play' src='https://play.google.com/intl/en_us/badges/images/generic/en_badge_web_generic.png'/>
        </a>
      </div>
    </div>
  </li>
  <li>
    <div class="project-item">
      <div class="project-item-image" style="background-color: rgba(85,159,196,1)"></div>
      <h3 class="project-item-header"><a href="https://play.google.com/store/apps/details?id=com.smashingboxes.crnt">CRNT</a></h3>
      <div class="project-item-footer">
        <p style="opacity: 0.54">
          Real-time conditions at the top surf spots. Air & water temperature, wave height, period, & direction, wind speed & direction.
        </p>
      </div>
      <div class="project-item-play-store-badge">
        <a href='https://play.google.com/store/apps/details?id=com.smashingboxes.crnt'>
          <img alt='Get it on Google Play' src='https://play.google.com/intl/en_us/badges/images/generic/en_badge_web_generic.png'/>
        </a>
      </div>
    </div>
  </li>
  <li>
    <div class="project-item">
      <div class="project-item-image" style="background-color: rgba(83,114,144,1)"></div>
      <h3 class="project-item-header"><a href="https://play.google.com/store/apps/details?id=com.smashingboxes.dudesolutions.schooldude">SchoolDude Work Center</a></h3>
      <div class="project-item-footer">
        <p style="opacity: 0.54">
          Project tracking for maintenance and operations management
        </p>
      </div>
      <div class="project-item-play-store-badge">
        <a href='https://play.google.com/store/apps/details?id=com.smashingboxes.dudesolutions.schooldude'>
          <img alt='Get it on Google Play' src='https://play.google.com/intl/en_us/badges/images/generic/en_badge_web_generic.png'/>
        </a>
      </div>
    </div>
  </li>
</ul>

<!-- Open Source -->
<h3 class="portfolio-header">Open Source</h3>
{% assign allRepos = site.github.public_repositories | where: 'fork', 'false' %}
{% assign groupedByStars = allRepos | sort: 'stargazers_count', 'last' | reverse | group_by: 'stargazers_count' %}
<ul id="github-list">
{% for group in groupedByStars %}
  {% assign reposSortedByForks = group.items | sort: 'forks_count', 'last' | reverse %}
  {% for repository in reposSortedByForks %}
    <li>
      <div class="project-item">
        <div class="project-item-image"></div>
        {% if repository.fork == false %}
      	    <h3 class="project-item-header"><a href="{{ repository.html_url }}">{{ repository.name }}</a></h3>
        {% else %}
      	    <h3 class="project-item-header"><a href="{{ repository.html_url }}">{{ repository.name }}</a></h3>
        {% endif %}
        <div class="project-item-footer">
          <p style="opacity: 0.87"> <!-- Clean this up -->
            {% octicon star %} {{ repository.stargazers_count }} Stars &nbsp;&nbsp;&nbsp;{% octicon repo-forked %} {{ repository.forks_count }} Forks
          </p>
          <p style="opacity: 0.54">
            {{ repository.description }}
          </p>
        </div>
        <!-- <div class="project-item-action-bar">
          <button class="project-item-button">VIEW</button>
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
