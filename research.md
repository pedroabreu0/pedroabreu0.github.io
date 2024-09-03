---
layout: page
permalink: /research/
title: Publications
pubs:
---
<!--
    - title:   "Paper title in 3-7 words that sound like Clingon"
      author:  "M. McFly, D. Kirk, L. Skywalker, H.J. Potter, I. Jones, H. Houdini"
      journal: "Transactions on Black Magic"
      note:    "(presented at Oz)"
      year:    "2012"
      url:     "http://publish-more-stuff.org"
      doi:     "http://dx.doi.org"
      image:   "https://images.duckduckgo.com/iu/?u=http%3A%2F%2Fimages.moviepostershop.com%2Fthe-matrix-movie-poster-1999-1020518087.jpg&f=1"
      media:
        - name: "IMDB"
          url:  "http://www.imdb.com/title/tt0133093/"
-->

[A Type-Based Approach to Divide-and-Conquer Recursion in Coq](https://dl.acm.org/doi/abs/10.1145/3571196), *Abreu, Pedro and Delaware, Benjamin and Hubers, Alex and Jenkins, Christa and Morris, J. Garrett and Stump, Aaron*, POPL'23

[MSc Thesis: _A Translation of OCaml GADTs into Coq_](https://github.com/pedroabreu0/pedroabreu0.github.io/raw/master/docs/thesis.pdf), Purdue University

## Presentations

[POPL'20 Poster - How Small Can We Make A Useful Type Theory?](https://github.com/pedroabreu0/pedroabreu0.github.io/raw/master/docs/POPL20-poster.pdf)

[Datatypes Presentation for week 2 at Nomadic Labs](https://github.com/pedroabreu0/pedroabreu0.github.io/raw/master/docs/datatypes.pdf)


{% assign thumbnail="left" %}

{% for pub in page.pubs %}
{% if pub.image %}
{% include image.html url=pub.image caption="" height="100px" align=thumbnail %}
{% endif %}
[**{{pub.title}}**]({% if pub.internal %}{{pub.url | prepend: site.baseurl}}{% else %}{{pub.url}}{% endif %})<br />
{{pub.author}}<br />
*{{pub.journal}}*
{% if pub.note %} *({{pub.note}})*
{% endif %} *{{pub.year}}* {% if pub.doi %}[[doi]({{pub.doi}})]{% endif %}
{% if pub.media %}<br />Media: {% for article in pub.media %}[[{{article.name}}]({{article.url}})]{% endfor %}{% endif %}

{% endfor %}
