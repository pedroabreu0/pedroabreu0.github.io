---
layout: post
title: "Work Loging with the Google API"
description: "In this post I will describe how I put together Google Calendar,
Google Spreadsheet and the Google script API in order to log my PhD work"
categories: ["Google", "Calendar", "Programming", "Javascript", "Google Script",
"en"]
location: "Purdue - West Lafayette"
---

{% assign rsp = '{:class="img-responsive"}' %}
{% assign ctb = '{:class="center-block"}'   %}
{% capture blk %}{:target="_blank"}{% endcapture %}

Since this semester I finally became an RA (Hoorray!), I felt that I have way
too much freedom of when and how to work. So even though I have a lot of open
windows to work, I have to make sure I am actually sitting down working at least
40hrs/week, otherwise it will be a wasted week.

Since my last internship I became quite used to loging exactly how I have been
working each day, so I decided that doing this would be a great first step
towards it. 

![My Calendar][calendar]{{rsp}}

[You can see it all
here](https://calendar.google.com/calendar?cid=Z2g2NWkxbjYzYjU0aG11N2huOWw0cXZlYjBAZ3JvdXAuY2FsZW5kYXIuZ29vZ2xlLmNvbQ)

The problem with calendar is that it does not give me any details on how I have
been spending my time. If I want to know how many hours I worked in the week I
have to do the math myself, and things get even worse if you want to know how
many hours you worked in a particular project.

So I decided I needed to program a spreadsheet to do that for me. That's when I
discovered the Google API, which is pretty nice and seems to provide with
everything a dev might need to conquer the world.

My first decision was to do it using python, but after failing to install the
library in a couple of hours I decided to use the google script language, which
is made on top of javascript. [Here's the script page](https://script.google.com/d/1Bvrxj87qBKZ_PAofz30PWjV13A16Wva-JllwWGmPq2aD1d1exwrMQ5xr/edit?usp=sharing).

Here's a screenshot with the resulting spreadsheet:

![My Spreadsheet][spreadsheet]{{rsp}}


I won't go into the step by step details of how the script works, but please
feel free to shoot me if you have any questions.

Now I feel that I finally got to the point where my calendar is organized
enough.

![Complete Calendar][completecalendar]{{rsp}}

The green (main) calendar is with all the events where I _must_ do something,
such as classes, meetings or phone calls. The purple one is routinely things,
purely a plan on how my day/week should look like in order to achieve a reasonable
amount of work done. And the red one is the work log, where I update every day
with the work that I have performed.

Now I feel that I will have an objective answer to the questions: "How many
hours of work does it take to get a PhD?"


[//]: # Referências

[calendar]: {% link assets/posts/googleapi/calendar.png %}
[spreadsheet]: {% link assets/posts/googleapi/spreadsheet.png %}
[completecalendar]: {% link assets/posts/googleapi/completecalendar.png %}
