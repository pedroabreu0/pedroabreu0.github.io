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
and share a little about my internship experience at [Galois
Inc.](https://galois.com/) located in Portland - OR.

Let's begin!

![Paulette Smashing the Gong][paulette]{{rsp}}
<p style="text-align: center;">
<a href="https://twitter.com/koronkebitch">@koronkebitch</a> smashes the gong
</p>

As you can probably deduce from this awesome gong in the office, Galois
is an amazing place with amazing people.
They do some pretty cool stuff with [Haskell](https://www.haskell.org/), Formal
Methods and Cryptography. And to the best of my knowledge Galois is the first
company in the world to use Haskell to solve real world problems, and they
are kind of famous in the PL community for it. In fact, I knew about Galois much
before moving to the US, and I confess that interning there was kind of a dream
for the young me -- So hooray to dreams coming true!

<!-- I have heard about -->
<!-- them, and one of the big reasons I decided to do a PhD in the US was for this -->
<!-- open possibility of maybe landing in an internship using PL in the industry, -->
<!-- impacting the world very directly. -->

Galois is a contractor company that basically functions by applying to grants --
just like any researcher would, but on a bigger scale. Big part of their projects
revolve around two very important of their tools:
[Cryptol](https://cryptol.net/) and [SAW](https://saw.galois.com/). 

Cryptol is a
[DSL](https://en.wikipedia.org/wiki/Domain-specific_language) aimed for
developing cryptographic algorithms. And SAW is a tool/language used for
reasoning about llvm code. The way SAW works is by translating the program
execution path to the logical formulas of Z3 and checking if this translation
meets a specification written in Cryptol. This is what we call [symbolic
execution](https://en.wikipedia.org/wiki/Symbolic_execution), and the cool thing
about it is that even if you don't provide a specification, just by the fact
that a symbolic execution didn't crash it already means that the program is
memory safe! The symbolic execution tool they use is
[Crucible](https://github.com/GaloisInc/crucible), and its one of the most
advanced Haskell code in the wild, with tons of language extensions.

If you want to know more about their projects check [their
github](https://github.com/GaloisInc/), its all open source!!

During my summer I worked maintaining the SAW proofs of the amazon [S2N](https://github.com/awslabs/s2n)
TTLS/SSL protocols. Honestly it was a somewhat dull work to make all of that C
code to compile and run in my machine, then I had to tweak the code by adding
the proper annotations and make sure I could make the CI run SAW on it to provide
the proper guarantee that the code was memory safe. That code was written in C
with a very interesting macro system to make the programming more
object-oriented and reusable, it changed my perspective on the power of macros.

Every week I would meet the project leader to discuss my progress, and
after a few weeks he noticed that I was not the most passionate person to work with
automatic provers, he helped me to find another project where I would be
happier. Then my second project was specifying the interface of
[ElectionGuard](https://freeandfair.us/electionguard/) in Coq, unfortunately I
could not finish things by the end of my internship.

Turns out that it is quite competitive to get an internship there. According to
the hiring team they get thousands of applications every year and will only hire
a handful of them. My cohort was around 20 interns, and apparently this was the
summer they had the most number of interns so far.

The reason why it is so competitive is that the number of people that applies
with a 0 fit is quite high. Out of those that are actually a good fit they will
only hire if they can find a specific and self-contained project, that the
intern would be able to complete during his stay. 
The shorter they will hire for an internship is 3 months, but it can be longer,
and also extended.

Galois loves interns, that's because their hiring process for full time
employees is quite conservative. They want to be sure that the person fits
the company culture, and since they are looking for long term employees, they
want versatile people that would be able to work on different projects.
Since PL and formal methods are so new to the industry, a good fit for galois is
often (but not necessarily) a person with a PhD, which means that it is very
hard for them to find a good candidate.

This means that hiring interns is a good way for amazing people to learn about
their work culture from the inside, and maybe consider applying as full time in
the future. On the company side, they will also be able to
make a more informed decision if that person is a good fit for a full time
position or not. They hire people from multiple backgrounds and degree levels.
The best fit are usually grad students with background in functional
programming, PL and/or Security. But in my cohort there were interns from
engineering, biology and machine learning too.

Here's a picture of part of my cohort. From left to right we have Yerim Lee,
Haneef Mubarak,
Eric Bond, Paulette Koronkevich, Nikki Carroll, Parker Southwick, Nes Cohen, Me and Chris Phifer 
![Interns Farewell][interns]{{rsp}}


It is very hard for a small company like Galois to compete in terms of salary
and benefits with the big companies like Google, Facebook, Amazon and Microsoft.
So their approach to finding -- and keeping -- talents is by 
providing this absolutely amazing work-life balance.

![Reuben Chillin'][reuben]{{rsp}}

This picture was taken at a place that we named the Intern Island, 
because everyone there were intern... and Reuben, this handsome
dude on the picture. One day he simply decided that we had to make our workspace
more personal and off we go to Target to buy some decoration. I think this shows
well how relaxed and friendly the environment is.
For example, in my first day as an intern pretty much every employee came to
introduce themselves to me
and show that they could be reached if I ever needed anything.

The office has a pool table, pinball machines, espresso machine, ice cream, soft
drinks, tea,
VR games, Steam games, Chess board, and a dangerously rich snack bar.

![Snooker and Pinball][snooker]{{rsp}}

Every Thursday someone would organize to go out and grab some beers. It was a
very chilled environment where everyone would just go to a happy hour and relax.

One Friday of the month someone organize a game night at their house, where
people can play board games and poker. One of these night was in an
unforgettable farm full of llamas and alpacas. Have a fabulous gif of me
petting an alpaca.

![Me petting an Alpaca][alpaca]{{rsp}}

For me, socializing is the most important part of any internship. It is
when you get to _actually_ know people around you and grow your network. But not
only that, I've always tried to learn as much as possible from the experience of
those around me. I will often try to lean the conversation towards people's
opinions and visions on my field, and try to learn from their extensive
experience. Thanks to that I'm able to write this detailed blog post, for
example. Most of the information here I learned directly from the
HR people during these social events!

The last thing I would like to mention in this post is Portland. What a city!
What an experience! Everyone there is a hipster. Every bar is a brewery. Weed is
legal. Every year there are naked bike races. The rose festival was super fun.
The food carts has a special place in my heart and I will miss them for the rest
of my life.

The summer of 2019 was a remarkable summer in my life, thanks to this
internship. Our cohort would go out literally every weekend and explore the city. I had an
amazing roommate. Since we lived so close to the office, the interns would
hangout at our apartment often. If I could go back and change anything about
that summer I wouldn't change a single thing, it was spectacular.

If you are thinking of applying to work at Galois, either as an intern or a
full-time, rest assured that the place is amazing and you will be lucky to
receive an offer from them.

I hope this text could give you glimpse of how amazing working at Galois was
for me. Drop a comment bellow if you have any
questions, remarks or fix to any imprecision. If I cannot answer your questions
I might be able to contact someone who will!

Until next time.

![Mannequin][galois]{{rsp}}

[//]: # Referências

[galois]: {% link assets/posts/galoisreport/galois.jpg %}
[paulette]: {% link assets/posts/galoisreport/paulette_hits_gong.gif %}
[alpaca]: {% link assets/posts/galoisreport/alpaca.gif %}
[reuben]: {% link assets/posts/galoisreport/reuben.jpg %}
[interns]: {% link assets/posts/galoisreport/interns.jpg %}
[snooker]: {% link assets/posts/galoisreport/snooker.JPG %}
