---
layout: default
title: Events
permalink: /events/
---

# Events

{% assign events = site.data.events.events %}
{% assign sorted_events = events | sort: "date" %}
{% assign now_ts = "now" | date: "%s" | plus: 0 %}

<p>Define events in <code>_data/events.json</code> (<code>date</code> plus optional <code>end_date</code> for multi-day events).</p>

<h2>Upcoming events</h2>
{% assign has_upcoming = false %}
<ul class="events-list">
  {% for event in sorted_events %}
    {% assign event_end_ts = event.end_date | default: event.date | date: "%s" | plus: 0 %}
    {% if event_end_ts >= now_ts %}
      {% assign has_upcoming = true %}
      <li class="event-item">
        <h3 class="event-title">{{ event.title | default: "Untitled event" }}</h3>
        {% if event.date %}
          <p class="event-meta">
            <strong>Date:</strong>
            {% if event.end_date and event.end_date != event.date %}
              {{ event.date }} - {{ event.end_date }}
            {% else %}
              {{ event.date }}
            {% endif %}
          </p>
        {% endif %}
        {% if event.location %}<p class="event-meta"><strong>Location:</strong> {{ event.location }}</p>{% endif %}
        {% if event.description %}<p class="event-description">{{ event.description }}</p>{% endif %}
        {% if event.url %}
          <p class="event-link"><a href="{{ event.url }}" target="_blank" rel="noopener noreferrer">{{ event.url }}</a></p>
        {% endif %}
      </li>
    {% endif %}
  {% endfor %}
  {% unless has_upcoming %}
    <li>No upcoming events defined yet.</li>
  {% endunless %}
</ul>

<h2>Past events</h2>
{% assign has_past = false %}
<ul class="events-list">
  {% for event in sorted_events reversed %}
    {% assign event_end_ts = event.end_date | default: event.date | date: "%s" | plus: 0 %}
    {% if event_end_ts < now_ts %}
      {% assign has_past = true %}
      <li class="event-item">
        <h3 class="event-title">{{ event.title | default: "Untitled event" }}</h3>
        {% if event.date %}
          <p class="event-meta">
            <strong>Date:</strong>
            {% if event.end_date and event.end_date != event.date %}
              {{ event.date }} - {{ event.end_date }}
            {% else %}
              {{ event.date }}
            {% endif %}
          </p>
        {% endif %}
        {% if event.location %}<p class="event-meta"><strong>Location:</strong> {{ event.location }}</p>{% endif %}
        {% if event.description %}<p class="event-description">{{ event.description }}</p>{% endif %}
        {% if event.url %}
          <p class="event-link"><a href="{{ event.url }}" target="_blank" rel="noopener noreferrer">{{ event.url }}</a></p>
        {% endif %}
      </li>
    {% endif %}
  {% endfor %}
  {% unless has_past %}
    <li>No past events defined yet.</li>
  {% endunless %}
</ul>
