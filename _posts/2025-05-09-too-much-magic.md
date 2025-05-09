---
layout: post
title: Too much magic
categories: [tech]
---

A common criticisms of frameworks like [Textual](https://github.com/textualize/textual) is that they have "too much magic".

This always makes me think of the Goldilocks and the Three Bears fable, where Goldilocks is a Gen Z software developer declaring "there is too much magic in this API!"[^1] (presumably there is an API where the dev finds the amount of magic in the API "just right").

This tends to occur when an API moves from a procedural design to something more declarative.
In other words, you tell the API *what* you want without telling it *how* you want it done.
The difference is generally only apparent at a micro scale.
When you zoom in or out, you see that going procedural -> declarative is fractal in nature, where something declarative is procedural the next level up.

For instance, this might look maximally procedural:

```
a + b
```

But it is essence a declarative way of implementing this:

```
add(a, b)
```

And that is merely a declarative alternative to pushing and popping data on a call stack.
Keep zooming out and you get to frameworks, ORMs, browsers, and LLMs.
But the magic goes all the way down. 

The transition from one level to another occurs when the API doesn't scale.
When it becomes too verbose or complex to express your intent clearly, a phase shift from procedural to declarative has to occur.

Now "too much magic" is not quite the same thing as "bad magic".
Although they are often conflated, bad magic is when the implementation details leak out from the level below.
This can manifest itself as cryptic errors that reference the magic's implementation.
It can also take the form of poor optimization.
Like an ORM where the user has clearly expressed intent but the generated query is massively inefficient.
You could legitimately levy the criticism of "bad magic" there.
But that still isn't too much magic--the amount of magic wouldn't change if the ORM produced super efficient queries.

So please avoid the phrase "too much magic" unless you are watching card tricks.
But by all means, point out where the magic could work better.


[^1]: Don't OK Boomer me, I'm Gen X.