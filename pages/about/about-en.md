---
layout: page
title: About me
permalink: /about-en/
weight: 3
---

# **About me**

I am **{{ site.author.name }}**, now living in Yokohama. Thank you for coming to my blog.


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
