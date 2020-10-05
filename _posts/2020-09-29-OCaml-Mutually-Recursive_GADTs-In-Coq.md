---
layout: post
title: "(Not) Implementing OCaml's Mutually Recursive GADTs in Coq"
description: "I argue "
categories: ["OCaml", "Formal Methods", "PL", "en"]
location: "Purdue - West Lafayette"
---

{% assign rsp = '{:class="img-responsive"}' %}
{% assign ctb = '{:class="center-block"}'   %}
{% capture blk %}{:target="_blank"}{% endcapture %}

In the [last post]({% post_url 2020-08-05-OCaml-GADTs-In-Coq %}) I showed the
approached we devised to translate OCaml's GADTs in
[coq-of-ocaml](https://github.com/clarus/coq-of-ocaml).
In this blog post I will give a brief idea of why implementing mutually
recursive GADTs following the same idea can be tricky.

The root of all of our problems is the lack of inductive-inductive types in Coq,
I refer the reader to [this stack overflow
question](https://stackoverflow.com/questions/48191057/would-it-be-inconsistent-to-relax-coqs-strict-positivity-checker-to-not-look-at)
to a discussion of the topic and how to get away with it.
The key idea is to have a non-indexed pre-type, and then have a mutually
recursive function to talk about the indexes, then finally binding it all
together with a sigma type.

Here is a problem for us to try to encode with this idea.

{% highlight ocaml linenos %}
type _ foo =
  | Foo_int : int -> int foo
  | Foo_Bar_string : string bar -> (string bar) foo
and _ bar =
  | Bar_string : string -> string bar
  | Bar_bool : bool -> bool bar
{% endhighlight %}

Let's try to encode this datatype naively using the tagged representation of the
[last post]({% post_url 2020-08-05-OCaml-GADTs-In-Coq %}).

{% highlight coq linenos %}
Inductive foo : vtag -> Type :=
  | Foo_int : int -> foo int_tag
  | Foo_Bar_string : bar string_tag ->
                     foo (constr_tag "bar_string" (bar string_tag))

with bar : vtag -> Type :=
  | Bar_string : string -> bar string_tag
  | Bar_bool : bool -> bar bool_tag.
{% endhighlight %}

And we have the same error as the SO question

`Error: Non strictly positive occurrence of "bar" in "bar string_tag -> foo
(constr_tag "bar_string" (bar string_tag))".`


Let's try to follow the same steps to model this datatype.
We start with the same idea of getting rid of the indexes

{% highlight coq linenos %}
Inductive pre_foo : Type :=
  | Foo_int : int -> pre_foo 
  | Foo_Bar_string : pre_bar -> pre_foo

with pre_bar : Type :=
  | Bar_string : string -> pre_bar 
  | Bar_bool : bool -> pre_bar.
{% endhighlight %}

Now we need a mutually recursive function to talk about the indexes
We need the mutualy recursive functions `foo_wf` and `bar_wf` with the following signature

{% highlight coq linenos %}
Fixpoint foo_wf (t : pre_foo) (tag: vtag) : Type := ...
with bar_wf (t : pre_bar) (tag: vtag) : Type := ...
{% endhighlight %}

And after that we tie the knot with the sigma types

{% highlight coq linenos %}
Definition foo t := sigT (fun f => foo_wf f t).
Definition bar t := sigT (fun b => bar_wf b t).
{% endhighlight %}

Now notice that `Foo_Bar_string` will have the index `bar string_tag`, being a
sigma type. Unfortunately this will mean that we cannot prove termination for
`foo_wf`.

{% highlight coq linenos %}
Fixpoint foo_wf (t : pre_foo) (tag: vtag) : Type :=
  match t with
  | Foo_int x => tag = int_tag
  | Foo_Bar_string b => (tag = constr_tag "bar_string" (sigT (fun f => bar_wf f string_tag)))
           * (bar_wf b string_tag)
  end

with bar_wf (t : pre_bar) (tag: vtag) : Type :=
match t with
| Bar_string s => tag = string_tag
| Bar_bool b => tag = bool_tag
end.
{% endhighlight %}

This will fail with `Error: Cannot guess decreasing argument of fix.` And I cannot
see how to get away of this problem, because no matter what encoding of the tags
we define we will always need a way to recover from the tag to a type. 

You could argue that we may be able to fix this problem by changing how tags
are encoded but I don't think that is the case.
The key problem is that the type of the tag can actually be defined much after the
definition of the tags, which indicates that we need a way to inject an
arbitrary type into the definition of the tag. In the end of the day, this will
lead us to something isomophic to `constr_tag`.




[//]: # References

