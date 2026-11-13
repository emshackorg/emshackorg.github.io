---
layout: default
title: Hackerspaces
permalink: /hackerspaces/
---

# Hackerspaces

{% assign spaces = site.data.hackerspaces.hackerspaces %}
{% if spaces and spaces.size > 0 %}
<ul class="hackerspaces-list">
  {% for space in spaces %}
    <li class="hackerspace-item">
      <h2 class="hackerspace-name">{{ space.name | default: "Unnamed hackerspace" }}</h2>
      {% if space.city %}
        <p class="hackerspace-city">{{ space.city }}</p>
      {% endif %}
      {% if space.note %}
        <p class="hackerspace-note">{{ space.note }}</p>
      {% endif %}
      {% if space.url %}
        <p class="hackerspace-link">
          <a href="{{ space.url }}" target="_blank" rel="noopener noreferrer">{{ space.url }}</a>
        </p>
      {% endif %}
    </li>
  {% endfor %}
</ul>
{% else %}
<ul class="hackerspaces-list">
  <li>No hackerspaces defined yet.</li>
</ul>
{% endif %}
