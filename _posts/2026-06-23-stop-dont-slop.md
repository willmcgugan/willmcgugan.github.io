---
layout: post
title: Stop, don't Slop
categories: [tech, AI]
---

So you find a bug in an Open Source project and wish to spend your tokens solving that issue for the good of humanity. Your fingers hover over the keyboard, trembling in anticipation of the glorious prompt that will unblock your fellow developers. Before you type "FIx issue X make no mistaks" Stop!

AI is a modern marvel, but a Thanos level click of the fingers it is not. To prompt the best fix *you* need context. You need to diagnose the issue while considering the broader implications of your changes. I'm a maintainer of several open source packages, and let me tell you that well over half of issue reports incorrectly attribute the source of the bug and they often have grave misunderstandings about what the correct behavior is. No matter how good your AI is, if you give it a bum steer it may produce garbage.

I'm faced with a few options for AI PRs, which I will list in order:

1. Review them.
2. Merge them without a full review.
3. Reject them.

Option 1 takes work, especially given AI's tendency for loquacious bloviation. To figure out if the mechanical megabrain has solved the issue correctly requires that I solve it myself. The time taken to do this dwarfs the time taken to type the prompt.

Option 2 would work for a while. Users would be happy&mdash;for a while. But each change that strays from the big picture design or introduces an edge case or compromises an invariant, degrades the code. It's like taking a photocopy of a photocopy. Fuck, that dates me. It's like taking a JPEG of a JPEG.

Option 3 makes me look like the jerk. I'm not the jerk. You are not the jerk. There is no jerk here, both have good motivations. Unless the PR was submitted by your OpenFlaw, sorry, OpenClaw. Then you are the jerk. You are spending silly money to inconvenience Open Source maintainers, and I have no time for you.

Realistically, option 3 is the only practical solution for now.

I'd like to clarify that I'm not an AI doomer. We developers will all have to come to terms with a new way of working. But for libraries used by millions you need to be precious about every line, and that can only be done by a knowledgeable human or an AI under supervision of such a human. If you want to use AI to contribute to any of my projects I ask that you know enough that you *could* have written every line, even if AI did the grunt work for you.

Before I go, let me point out that every project described as being created by AI ships with the majority of code in dependencies created by mammalian brains; imperfect, squishy, sometimes cranky, brains consisting of water, lipids, and protein. I don't know for how much longer that will be the case, but while it is: Stop, don't slop.