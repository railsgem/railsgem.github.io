---
layout: post
title:  "Prolog Notes"
date:   2016-03-20 17:15:09 +1100
categories: Prolog
---
* 目录
{:toc}


####1.	Sometimes the order of the terms makes a difference. Try these two queries:####

{% highlight prolog %}
?- parent(pat, X), parent(pat, Y), X \= Y.

?- X \= Y, parent(pat, X), parent(pat, Y).
	
{% endhighlight %}

One of them succeeds but not the other. There are too many possible values of X and Y for which X is not equal to Y. Earlier versions of Prolog would get stuck in an infinite loop testing all the options. The current version of SWI-Prolog avoids the infinite loop, but in doing so it refuses to process the query and therefore fails to find any answer.

####2.	Recursive definition####
If we want to find all the descendants of a particular person, we could first find all the immediate descendants using the parent relation. We could then repeatedly find all the descendants of the descendants and so on. In Prolog this is done using recursion.

We will now add a recursive definition for the rule descendant(Person, Descendant) which succeeds when Descendant is a direct or indirect descendant of Person. First the base case:

{% highlight prolog %}
    descendant(Person, Descendant) :-
        parent(Person, Descendant).
{% endhighlight %}
How would you phrase this rule in English?
Here is the recursive case:

{% highlight prolog %}
    descendant(Person, Descendant) :-
        parent(Person, Child),
        descendant(Child, Descendant).
{% endhighlight %}
Add the descendant predicate (both the base case and the recursive case) to the family.pl program and re-consult.
{% highlight prolog %}
% parent(Parent, Child)
%
parent(albert, jim).
parent(albert, peter).
parent(jim, brian).
parent(john, darren).
parent(peter, lee).
parent(peter, sandra).
parent(peter, james).
parent(peter, kate).
parent(peter, kyle).
parent(brian, jenny).
parent(irene, jim).
parent(irene, peter).
parent(pat, brian).
parent(pat, darren).
parent(amanda, jenny).



[trace]  ?- descendant(irene, D).
   Call: (6) descendant(irene, _G387) ? creep
   Call: (7) parent(irene, _G457) ? creep
   Exit: (7) parent(irene, jim) ? creep
   Call: (7) descendant(jim, _G387) ? creep
   Call: (8) parent(jim, _G457) ? creep
   Exit: (8) parent(jim, brian) ? creep
   Call: (8) descendant(brian, _G387) ? creep
   Call: (9) parent(brian, _G457) ? creep
   Exit: (9) parent(brian, jenny) ? creep
   Call: (9) descendant(jenny, _G387) ? creep
   Call: (10) parent(jenny, _G457) ? creep
   Fail: (10) parent(jenny, _G457) ? creep
   Redo: (9) descendant(jenny, _G387) ? creep
   Call: (10) parent(jenny, _G387) ? creep
   Fail: (10) parent(jenny, _G387) ? creep
   Fail: (9) descendant(jenny, _G387) ? creep
   Redo: (8) descendant(brian, _G387) ? creep
   Call: (9) parent(brian, _G387) ? creep
   Exit: (9) parent(brian, jenny) ? creep
   Exit: (8) descendant(brian, jenny) ? creep
   Exit: (7) descendant(jim, jenny) ? creep
   Exit: (6) descendant(irene, jenny) ? creep
D = jenny ;
   Redo: (7) descendant(jim, _G387) ? creep
   Call: (8) parent(jim, _G387) ? creep
   Exit: (8) parent(jim, brian) ? creep
   Exit: (7) descendant(jim, brian) ? creep
   Exit: (6) descendant(irene, brian) ? creep
D = brian ;
{% endhighlight %}
>	REFRENCES: UNSW COMP9414 

>	http://webapps.cse.unsw.edu.au/webcms2/course/index.php?cid=2443&color=lavendar
