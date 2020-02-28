---
layout: page
title: About me
permalink: /about-en/
weight: 3
---

# **About me**

Hi I am **{{ site.author.name }}**,<br>
A person who likes all kinds of interesting things and wants anything to be better.

## Educational experience

<div class="row">
{% include about/en/timeline-education.html %}
</div>

## Research and software works

<div class="row">
{% include about/en/timeline-research.html %}
</div>

## Work experience and internships

<div class="row">
{% include about/en/timeline-work.html %}
</div>

<div class="row">
{% include about/skills.html title="Major skills" source=site.data.major-skills %}
{% include about/skills.html title="Minor skills" source=site.data.minor-skills %}
</div>
