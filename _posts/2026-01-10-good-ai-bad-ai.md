---
layout: post
title: Good AI, Bad AI - the experiment
categories: [tech, AI]
---

If you are in tech, or possibly even if you aren't, your social feeds are likely awash with AI.
Most developers seem to be either all-in or passionately opposed to AI (with a leaning towards the all-in camp).
Personally I think the needle is hovering somewhere between bad and good.

## Good AI

AI for writing code is a skill *multiplier*.

We haven't reached the point where a normie can say "Photoshop, but easier to use".
Will we ever?
But for now it seems those who are already skilled in what they are asking the AI to do, are getting the best results.

I've seen accomplished developers on X using AI to realize their projects in a fraction of the time.
These are developers who absolutely *could* write every line that the LLM produces.
They choose not to, because time is their most precious commodity.

Why is this *good* AI?
It means that skills acquired in the age before AI [^1] are still valuable.
We have a little time before mindless automatons force senior developers into new careers as museum exhibits, tapping on their mechanical keyboards in front of gawping school kids, next to the other fossils,

## Bad AI

The skill multiplier effect may not be enough to boost inexperienced (or mediocre) developers to a level they would like.
But AI use does seem to apply a greater boost to the Dunning-Kruger effect.

If you maintain an Open Source project you may be familiar with AI generated Pull Requests. Easily identifiable by long bullet lists in the description, these PRs are often from developers who copied an issue from a project into their prompt, prefixed with the words "please fix".

These drive-by AI PRs generate work for the FOSS developer.
They can look superficially correct, but it takes time to figure out if the changes really do satisfy the requirements.
The maintainer can't use the usual signals to cut through the noise when reviewing AI generated PRs.
Copious amounts of (passing) tests and thorough documentation are no longer a signal that the PR won't miss the point, either subtly or spectacularly.

This is bad AI (more accurately a bad *outcome*), because it typically takes more time for the maintainer to review such PRs than the creator took to type in the prompt.
And those that contribute such PRs rarely respond to requests for changes.

In the past you could get around this with a blanket ban on AI generated code.
Now, I think developers would be foolish to do that.
Good code is good code, whether authored by a fleshy mammalian brain or a mechanical process.
And it is undeniable that AI code can be *good* code.

## The Experiment

This makes me wonder if the job of maintainer could be replaced with AI.

I want to propose an experiment...

Let's create a repository with some initial AI generated code: "Photoshop, but easier to use" is as a starting point as good as any.
An AI agent will review issues, respond via comments, and may tag the issue with "todo" or close it if it doesn't reach a bar for relevance and quality.

PRs are accepted for "todo" issues and will be reviewed, discussed, and ultimately merged or closed by the AI.
These PRs may be human or AI generated—the AI doesn't care (as if it could).

Note that PRs could modify any of the prompts used by the AI, and those edits will be reviewed by the AI in the same way as any other file.

Would the end result be quality software or a heinous abomination, succeeding only in creating a honeypot for prompt-injection attacks?

I have no intention of making this happen.
But if somebody does, tell me how it goes.

[^1]: Feels like a long time, but there has only been a single Fast and Furious movie made since the advent of the AI age.