---
layout: page
title: Notícias
permalink: /noticias/
---





## Últimas Notícias

{% assign noticias = site.posts | where: "categories", "noticias" %}
{% for post in noticias %}
  {% include post-card.html post=post %}
{% endfor %}