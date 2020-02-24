---
layout: page
title: 自己紹介
permalink: /about-ja/
weight: 5
---

# **About Me**

Hi I am **{{ site.author.name }}**,<br>
A person who likes all kinds of interesting things and wants anything to be better.

<div class="row">
{% include about/skills.html title="Major skills" source=site.data.major-skills %}
{% include about/skills.html title="Minor skills" source=site.data.minor-skills %}
</div>

## Educational experience

<div class="row">
{% include about/timeline-education.html %}
</div>

## Work experience and internships

<div class="row">
{% include about/timeline-work.html %}
</div>

## Research and software works

<div class="row">
{% include about/timeline-research.html %}
</div>
