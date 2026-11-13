---
layout: default
---

<p class="home-intro">EMSHACK_ is a collaboration of hackerspaces across Emsland in Lower Saxony, Germany.</p>

<div class="map-wrapper">
  <img
    id="emsland-map"
    src="{{ site.emsland_svg }}"
    alt="Emsland region map"
  >
  <div id="map-markers" class="map-markers" aria-label="Hackerspace locations">
    {% assign north = site.emsland_geo_bounds.north | plus: 0.0 %}
    {% assign south = site.emsland_geo_bounds.south | plus: 0.0 %}
    {% assign west = site.emsland_geo_bounds.west | plus: 0.0 %}
    {% assign east = site.emsland_geo_bounds.east | plus: 0.0 %}
    {% assign lat_range = north | minus: south %}
    {% assign lon_range = east | minus: west %}
    {% for space in site.data.hackerspaces.hackerspaces %}
      {% assign x = nil %}
      {% assign y = nil %}
      {% if space.lat and space.lon and lat_range > 0 and lon_range > 0 %}
        {% assign lon_offset = space.lon | minus: west %}
        {% assign lat_offset = north | minus: space.lat %}
        {% assign x = lon_offset | divided_by: lon_range | times: 100.0 %}
        {% assign y = lat_offset | divided_by: lat_range | times: 100.0 %}
      {% elsif space.x_pct and space.y_pct %}
        {% assign x = space.x_pct %}
        {% assign y = space.y_pct %}
      {% endif %}
      {% if x != nil and y != nil %}
        <div class="map-marker" style="left: {{ x | at_least: 0 | at_most: 100 }}%; top: {{ y | at_least: 0 | at_most: 100 }}%;" aria-label="{{ space.name | default: 'Hackerspace' }}" tabindex="0">
          <span class="map-marker-dot"></span>
          <div class="map-tooltip">
            <strong class="map-tooltip-name">{{ space.name | default: "Hackerspace" }}</strong>
            {% if space.city %}<div>City: {{ space.city }}</div>{% endif %}
            {% if space.note %}<div>{{ space.note }}</div>{% endif %}
            {% if space.url %}
              <a href="{{ space.url }}" target="_blank" rel="noopener noreferrer">Homepage</a>
            {% endif %}
          </div>
        </div>
      {% endif %}
    {% endfor %}
  </div>
</div>

<h2 class="home-cta-title">Add your hackerspace</h2>
<p class="home-cta-text">If your hackerspace should be listed here, fork the repository, update <code>_data/hackerspaces.yml</code>, and open a pull request.</p>
