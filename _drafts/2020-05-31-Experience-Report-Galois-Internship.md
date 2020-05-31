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


![Me petting an Alpaca][alpaca]{{rsp}}

[//]: # Referências

[paulette]: {% link assets/posts/galoisreport/paulette_hits_gong.gif %}
[alpaca]: {% link assets/posts/galoisreport/alpaca.gif %}
