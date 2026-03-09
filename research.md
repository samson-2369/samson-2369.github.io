
---
title: Research
permalink: /research/
---

# Research Archive

{% assign papers = site.research | sort: "date" | reverse %}

{% for paper in papers %}

### [{{ paper.title }}]({{ paper.url }})

{{ paper.description }}

{% endfor %}
