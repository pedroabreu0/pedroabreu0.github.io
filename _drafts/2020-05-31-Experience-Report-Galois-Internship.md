---
layout: post
title: "Experience Report - Galois Internship"
description: "In this post I share a little about my experience as an intern at Galois"
categories: ["Galois", "Formal Methods", "Cryptol", "PL", "en"]
location: "Purdue - West Lafayette"
---

{% assign rsp = '{:class="img-responsive"}' %}
{% assign ctb = '{:class="center-block"}'   %}
{% capture blk %}{:target="_blank"}{% endcapture %}

After a whole year putting this off, I finally decided to put in some time
and share a little about my internship experience at [Galois Inc.](https://galois.com/)

Let's begin!

![Paulette Smashing the Gong][paulette]{{rsp}}
<p style="text-align: center;">
<a href="https://twitter.com/koronkebitch">@koronkebitch</a> smashes the gong
</p>

Yep, that's right! Galois has this massive gong in their office.
From this you can already probably guess how cool this company is, right?

Ok, but let's start from the beginning. Galois is this pretty cool company
that does some cool stuff with [Haskell](https://www.haskell.org/), Programming
Languages, Formal Methods and Criptography. Since I was in Brazil I heard about
them, and one of the big reasons I decided to do a PhD in the US was for this
open possibility of maybe landing in an internship using PL in the industry,
impacting the world very directly.

<!-- Write how is the structure of the company -->

I would say that their most important projects currently are
[Cryptol](https://cryptol.net/) 
and [SAW](https://saw.galois.com/). Cryptol is a [DSL](https://en.wikipedia.org/wiki/Domain-specific_language) 
for aimed for developing cryptographic algorithms. And SAW is a tool/language
used for reasoning about llvm code. The way it works is by translating the program execution
path to the logical formulas of Z3 and checking if this translation meets a
specification written in Cryptol. This is what we call [symbolic
execution](https://en.wikipedia.org/wiki/Symbolic_execution), and the cool thing
about it is that even if you don't provide a specification, just by the fact
that a symbolic execution didn't crash it already means that the program is
memory safe! The symbolic execution tool they use is
[Crucible](https://github.com/GaloisInc/crucible), and its one of the most
advanced Haskell code in the wild.

If you want to know more about their project check [their
github](https://github.com/GaloisInc/), its all open source!!

Turns out that it is quite competitive to get an internship there, according to
the hiring team they get thousands of applications every year and will only hire
a handful of them. My cohort was around 20 interns, and apparently this was the
summer they had the most number of interns.

The reason why it is so competitive is that the number of people that applies
with a 0 fit is quite high. Out of those that are actually good fit they will
only hire if they can find a specific and self-contained project, in which the
applicant would excel in the amount of time he will be there. The shorter they will hire for
an internship is 3 months, and it can be extended.

Galois loves interns, and the reason for that is that they are very conservative
in hiring for the full time positions. In the sense that they will hire full
times looking into his whole fit with the culture of the company, and if they
show value by being capable of participating in different projects.
This means that hiring interns is a very good way to keep their door open for amazing
people to get to know their work culture from the inside, and maybe consider
to apply as full time in the future. Now since the company also knows that
person, they will also be able to have a more informed decision if that person
is a good fit or not.

It is very hard for a small company like Galois to compete in terms of salary
and benefits with the big companies like Google, Facebook, Amazon and Microsoft.
So their approach to finding, and keeping talents, is by 
providing this absolutely amazing work-life balance.

![Reuben Chillin'][reuben]{{rsp}}

This picture was taken at a place that we named the Intern Island, 
because everyone there were intern... and Reuben, this handsome
dude on the picture. One day he simply decided that we had to make our workspace
more personal and off we go to Target to buy some decoration.

I think this shows well how relaxed and friendly the environment is. In my first
day as an intern pretty much everyone came to introduce themselves and show that
they could be reached if I ever needed anything.

![Interns Farewell][interns]{{rsp}}

![Me petting an Alpaca][alpaca]{{rsp}}

[//]: # Referências

[paulette]: {% link assets/posts/galoisreport/paulette_hits_gong.gif %}
[alpaca]: {% link assets/posts/galoisreport/alpaca.gif %}
[reuben]: {% link assets/posts/galoisreport/reuben.jpg %}
[interns]: {% link assets/posts/galoisreport/interns.jpg %}
