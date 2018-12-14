---
layout: page
title: Notes
permalink: /notes/
---

This is where I keep my notes for self, future reference.

<ul class="listing">
{% for note in site.notes %}
    <a href="{{ post.url | prepend: site.baseurl }}" title="{{ note.title }}">{{ note.title }}</a>
  </li>
{% endfor %}
</ul>
