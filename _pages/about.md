---
permalink: /
title: "Richard Brutti's personal page"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

<p class="page__kicker">PhD, Computational Linguistics · Director of Research</p>

Hello! I recently completed my PhD in Computer Science (Computational Linguistics) at Brandeis University, advised by Professor James Pustejovsky. My dissertation, *["Uh, Actually: Grunt Acts as Grounding Contributions in Multimodal Dialogue"](https://richardbrutti.github.io/files/Brutti_Dissertation.pdf)*, focuses on formal semantic and computational models for non-verbal communication, such as gesture and grunts, using naturalistic multimodal data. 

Learning what my last name means sent me down the linguistics path. I received my BA in Linguistics & Italian Studies from Boston College and MA in Computational Linguistics from Brandeis. 

I also serve as Director of Research at a large SaaS company, managing Machine Learning and Annotation teams focused on speech, audio, and NLP. Beyond my dissertation work, I have published on emotion recognition in speech, technology in education, and food and language.

{% include base_path %}

<h2 class="section-label">Recent publications</h2>
{% assign pubs = site.publications | sort: "date" | reverse %}
{% assign prev_year = "" %}
<div class="pub-list pub-list--compact">
{% for post in pubs limit: 3 %}
  {% assign year = post.date | date: "%Y" %}
  {% if year != prev_year %}{% assign show_year = true %}{% else %}{% assign show_year = false %}{% endif %}
  {% include archive-single-pub.html %}
  {% assign prev_year = year %}
{% endfor %}
</div>
<p class="more-link"><a href="{{ base_path }}/publications/">All publications &rarr;</a></p>

<h2 class="section-label">Talks</h2>
<ul class="talk-list">
{% assign talks = site.talks | sort: "date" | reverse %}
{% for talk in talks %}
  <li>
    <span class="talk-list__date">{{ talk.date | date: "%b %Y" }}</span>
    <span class="talk-list__body"><a href="{{ base_path }}{{ talk.url }}">{{ talk.title }}</a><br><span class="talk-list__venue">{{ talk.venue }}{% if talk.location %} · {{ talk.location }}{% endif %}</span></span>
  </li>
{% endfor %}
</ul>

<figure class="grunt">
  <img src="/images/blue_striped_grunt_cropped.jpg" alt="Blue striped grunt">
  <figcaption>The blue striped grunt (<em>Haemulon sciurus</em>), from Ripley's Aquarium of Canada, Toronto.</figcaption>
</figure>
