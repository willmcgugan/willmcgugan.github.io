---
layout: post
title: Why I ban users from my repositories
categories: [tech]
---

I've been maintaining various Open Source projects for more than a decade now.
In that time I have had countless interactions with users reporting issues and submitting pull requests.
The *vast* majority of these interactions are positive, polite, and constructive.
In fact, it is these interactions which make me continue to do the work.

A few haven't been so pleasant, and I have banned a subset of the users involved.
If we exclude spam, I think the number of users I have banned over the years may still be a single figure.

There are three broad categories of banned users, listed below.

## Spammers

I'm sure there is a place for links to sites that sell male enhancement pills, but my repositories are not it.
Spam earns you an instant ban.
This doesn't happen all that often as GitHub is quite proactive about dealing with spam.
Often I'll get a notification, but by the time I open it the spammer's account will have been deleted.

As well as the usual spam nonsense, I've had some other weird stuff posted on my repositories.
I recall one user that posted lengthy conspiracy theories, with something about terminals intertwined.
I'm pretty sure this user wasn't a spammer in the traditional sense, and was suffering from psychological issues.
I had no choice but to ban them, but I genuinely hope they found treatment for their condition.

## Venting

A venting post almost always starts with "I spent X hours / days on this".
Such users want me to know how much I have inconvenienced them and they are rarely genuine in asking for help.

I try to be generous, but that tends to put me on the defensive.
I'm not going to treat that issue as a priority, and when I do respond it will be a tad more snarky that usual.

Venting posts are almost always a skill issue in behalf of the user.
The user has either misread the docs or not read them at all, and they have consequently made some invalid assumptions about how the API should work.
They couldn't get their code to work, because it was never intended to work in they way they were using it.
Rather than stepping back to reconsider their approach, or read the docs again, they want to shift the blame to me.

Venting is not an instant ban, because I know how frustrating programming can be.
But virtually 100% of these issues are resolved with a link to the docs, and none of reply with a "my bad" even if I suppress my snark.

So not an instant ban, but if venting crosses the line to personal abuse, then I'm going to be reaching for that ban button.

Almost everyone recognizes that an posting an issue is essentially asking a favor.
If you want somebody to help you move house, you wouldn't start by criticizing their driving.
Same deal with issues.

## Time wasting

This last category is trickier to define, as its not a single transgression like the others.
It's more of a pattern of behavior that sucks time that could be better spent helping other users or writing code.

So what constitutes time wasting?

It will often start with well meaning issues that are overly long.
Pages and pages of text that don't clearly describe the problem the user is tackling.
In the end, the issue typically boils down to a perfectly legitimate "it crashes when I do this".
But it can take a lot of fruitless back and forth to get there.

One time I can overlook.
But if it keeps happening, I can feel like I am essentially working for this user at the expense of other users.

Related, is the user who doesn't listen or choses not to respond to my requests.
Simple things like asking for the version of their OS or software they are using.
Details that I need to properly investigate their issue.
Sometimes it takes the form of ignoring a recommendation.
I'll let them know there is a canonical solution to that issue, and give them a short code snippet that resolves the issue with less work, but they won't use it or even acknowledge it.

However the most common "not listening" issue is when I ask the user *why* they are attempting the thing they need help with.
This can be vital in avoiding the [XY Problem](https://en.wikipedia.org/wiki/XY_problem).
If there is a better way of solving their problem then I can point them in the right direction.
But only if they tell me.
A few users have just refused to and repeatedly assert the odd thing they are trying to do is the only acceptable fix.

Other examples of time wasting include asking for LLM hallucinated code to work, posting lists of questions that can be answered with a skim over the docs, and posting the same questions in multiple support locations even after they have been answered (as though they will keep posting until they get a response they like)?

This is a tricky category, because the user can be well meaning.
So its a very high threshold to be banned for this.
I only consider it if the user is a clear net negative for the project.

## Unbanning

I so rarely ban users, and when I do it's for the good of the project.
But I don't hold grudges.
Other than spammers, if anyone I have banned wants to contribute I am happy to un-ban if they reach out.
No apology required, but I will require they avoid the ban categories above.

## Open Source is awesome

I hope this post doesn't sound too much like whinging.

I'd like to end by stressing that the community is what makes Open Source awesome.
Everyone benefits by contributing in their own way.
