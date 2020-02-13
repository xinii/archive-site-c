---
layout: page
title: About
permalink: /about-en/
weight: 3
---

# **About Me**

Hi I am **{{ site.author.name }}**,<br>
A person who likes all kinds of interesting things and wants anything to be better.

<div class="row">
{% include about/skills.html title="Programming Skills" source=site.data.programming-skills %}
{% include about/skills.html title="Other Skills" source=site.data.other-skills %}
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
