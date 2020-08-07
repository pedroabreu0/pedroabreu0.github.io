---
layout: post
title: "Implementing OCaml's GADTs in Coq"
description: ""
categories: ["OCaml", "Formal Methods", "Cryptol", "PL", "en"]
location: "Purdue - West Lafayette"
---

{% assign rsp = '{:class="img-responsive"}' %}
{% assign ctb = '{:class="center-block"}'   %}
{% capture blk %}{:target="_blank"}{% endcapture %}

Consider the following OCaml variant and program:

{% highlight ruby linenos %}
type _ unit_or_double_unit =
| Unit : unit unit_or_double_unit
| Double_unit : (unit * unit) unit_or_double_unit

let unit_twelve (x : unit unit_or_double_unit) =
  match x with
  | Unit -> 12
  | Double_unit ->.
{% endhighlight %}

Line 6 is what OCaml calls an "impossible branch". It means that there is no way to build a term
of type `int unit_or_double_unit`, and therefore this branch of the pattern matching will never
be reached.

Let's try to translate this to Coq. 
{% highlight coq linenos %}
Inductive unit_or_double_unit : Type -> Type :=
    | Unit : unit_or_double_unit unit
    | Double_unit : unit_or_double_unit (unit * unit).
{% endhighlight %}

Now, the key idea to translate `twelve` is that we should be able to
prove `False` in branch for `Double_unit`, and from `False`, anything follows.

Let's try to do it by refinement. We will need dependent pattern matching for this.

{% highlight coq linenos %}
Definition twelve_unit (x : unit_or_double_unit unit) : nat. 
    refine (match x in unit_or_double_unit T return T = nat -> nat with
    | Unit => fun eq_unit_nat => 12
    | Double_unit => fun eq_double_unit_nat => _
    end eq_refl).
    (* Insert proof of False here *)
Admitted.
{% endhighlight %}

Don't freak out if you've never seen a dependent pattern matching in the wild.
Basically what line 2 above is doing is making it explicit that on the first branch 
`unit = unit` and the second branch `unit * unit = unit`, and naming these
hypothesis `eq_unit_nat` and `eq_double_unit_nat`, respectively.

From this we should be able to prove `False`, right? Wrong!
In Coq, the only way to prove that two types are not equal is by a cardinality
argument, i.e. We have to show that the two types have a different number of
members.

This means that we cannot prove that `unit * unit <> unit` without
extra axioms, because `unit * unit` has exactly one member, namely `(tt, tt)`. And
`unit` also has only one member `tt`.

Does it mean that everything is lost? Not really. Here we propose a solution for
dealing with this, and it is by taging our type constructors so that we gain the
freedom to choose what are the types that we will consider equal or not.

For this we introduce the language of _variant_ tags.

{% highlight coq linenos %}
Inductive vtag : Type :=
| constr_tag : string -> Type -> vtag
| arrow_tag : vtag -> vtag -> vtag
| tuple_tag : vtag -> vtag -> vtag
| var_tag : forall (t : Type), vtag.

Open Scope string_scope.
Notation unit_tag := (constr_tag "unit" unit).
Notation double_unit_tag := (tuple_tag unit_tag unit_tag).
Notation int_tag := (constr_tag "nat" nat).
Notation bool_tag := (constr_tag "bool" bool).

Fixpoint decode_vtag (tag : vtag) {struct tag} : Type :=
  match tag with
  | @constr_tag s t => t
  | arrow_tag t1 t2 => decode_vtag t1 -> decode_vtag t2
  | tuple_tag t1 t2 => decode_vtag t1 * decode_vtag t2
  | var_tag t => t
  end.
{% endhighlight %}

Don't mind this decode function for now, we'll explain it later.
The important is that we can now define `unit_or_double_unit` as follows

{% highlight coq linenos %}
Inductive unit_or_double_unit' : vtag -> Type :=
    | Unit : unit_or_double_unit unit_tag
    | Double_unit : unit_or_double_unit double_unit_tag.

Definition twelve (x : unit_or_double_unit' unit_tag) : nat.
  refine (match x in unit_or_double_unit' T return T = unit_tag -> nat with
    | Unit' => fun _ => 12
    | Double_unit' => fun eq_double_unit_nat => _
          end eq_refl).
  inversion eq_double_unit_nat.
Defined.
{% endhighlight %}

As you can see, a simple inversion was enough to prove that `unit_tag <>
double_unit_tag`.
That's because we have provided `constr_tag` with different strings
representations, making this inequality trival.

Ok, seems like it works, but between you and me we have to agree that this isn't
the most realistic GADT out there. Let's take a look into something more
reasonable.

{% highlight ocaml linenos %}
type _ expr =
| Int : int -> int expr
| Bool: bool -> bool expr
| Sum : int expr * int expr -> int expr
| Or : bool expr * bool expr -> bool expr

let rec eval : type a. a expr -> a =
function
| Int n -> n
| Bool b -> b
| Sum (n, m) -> eval n + eval m
| Or (x, y) -> eval x || eval y
{% endhighlight %}

We start by translating the datatype, nothing surprising here.

{% highlight coq linenos %}
Inductive expr : vtag -> Set :=
| Int : nat -> expr int_tag
| Bool : bool -> expr bool_tag
| Sum : expr int_tag -> expr int_tag -> expr int_tag
| Or : expr bool_tag -> expr bool_tag -> expr bool_tag.
{% endhighlight %}

But now, to translate eval we need to return the actual type of the tag. And
this is where `decode_vtag` comes in:

{% highlight coq linenos %}
Fixpoint eval {a} (e : expr a) : decode_vtag a :=
  match e with
  | Int n => n
  | Bool b => b
  | Sum n1 n2 => (eval n1) + (eval n2)
  | Or x y => orb (eval x) (eval y)
  end.
{% endhighlight %}

And here is another example of a function with impossible branches:

{% highlight ocaml linenos %}
let get_int (e : int expr) : int =
  match e with
  | Int x -> x
  | Sum _ -> eval e
{% endhighlight %}

Would be translated ot

{% highlight coq linenos %}
Definition get_int (e : expr int_tag) : nat :=
  match e in expr T return T = int_tag -> nat with
  | Int n => fun _ => n
  | Sum n1 n2 => fun _ => (eval n1) + (eval n2)
  | _ => fun _ => ltac:(discriminate)
  end eq_refl.
{% endhighlight %}

For now this is it, next time I will talk about Mutually Recursive Datatypes.


[//]: # Referências

[snooker]: {% link assets/posts/galoisreport/snooker.JPG %}
