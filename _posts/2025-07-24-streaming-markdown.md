---
layout: post
title: Efficient streaming of Markdown in the terminal
categories: [tech,markdown,toad]
---


While working on [Toad](../announcing-toad/), it occurred to me there was a missing feature I would need.
Namely *streaming markdown*.
 
When talking to an LLM via an API, the Markdown doesn't arrive all at once.
Rather you get fragments of markdown (known as tokens) which should be appended to an existing document.
Until recently the only way to render this in Textual was to remove the Markdown widget and add it again with the updated markdown.
This worked, but it would get slower to append content as the document grew.
It wasn't a scalable solution.

Fortunately there are a number of optimizations which made markdown streaming scalable to massive documents.
I would expect these *tricks* to be equally applicable in the browser.

Here's Textual's new Markdown streaming in action:

<iframe width="100%" style="aspect-ratio: 1512 / 982;"  src="https://www.youtube.com/embed/PzkOAkvtF40" title="" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

In a Textual Markdown widget, every part of the output it also a widget.
In other words, every paragraph, code fence, and table is a independent widget in its own right, with its own event loop.
Since the bottleneck was adding and removing these widgets, any solution would have to avoid or dramatically reduce the number of times that needed to occur.

### Optimization 1.

The Python library I use for Markdown parsing, [markdown-it-py](https://markdown-it-py.readthedocs.io/en/latest/), doesn't support any kind of streaming, but it turned out that it is possible to build streaming on top of it (and possibly any library).
Markdown documents can be neatly divided in to top-level blocks, like a header, paragraph, code fence, table etc.
When you add to the document, only the very last block can change.
You can consider the blocks prior to the last to be finalized.

This observation lead me to working on an optimization to avoid removing and re-creating these finalized blocks.
But there was a sticking point.
It turns out that the very last block can change its type when you add new content.
Consider a table where the first tokens add the headers to the table.
The parser considers that text to be a simple paragraph block up until the entire row has arrived, and then all-of-a-sudden the paragraph becomes a table.
Once I took that into account, it worked.
It was a massive win and streaming became more practical.

### Optimization 2.

The next step was to avoid replacing even last widget on new content.
This is unavoidable if the last block changes type, but if it didn't, I could add new content without replacing the widget (a far simpler operation in Textual).
The paragraph block, for instance, was trivial to update.
As was the code fence.
The table was more complicated, but still doable.
Replacing even a single widget per token could be expensive when new tokens arrive 100 times a second or higher.
So this update was a decent win.

### Optimization 3.

I could possibly have left it there, but there was one more outstanding optimization.
Markdown-it-py is an excellent library and really quite fast, but a very large document could take a few milliseconds to parse.
Multiply that by 100 tokens a second and it becomes significant.

I could reduce that parsing cost dramatically by only considering the last block in the document.
All it took was to store the line number where that last block began, and feed the parser the data from there to the end of the document.
This update meant that no matter how large the document is, parsing was always sub 1ms.

### Optimization 4.

This final optimization occurs not within the Markdown widget itself, but at a level above.

No matter how optimized appending to the markdown widget is, tokens could arrive faster than they can be displayed.
A naive solution would queue up these updates, so you see all the intermediate steps.
The problem with that is that your UI can be dutifully scrolling through content for many seconds after it has arrived.
I say if you have the output, let the user see it without delay.
They probably paid for the tokens, after all.

I fixed this with a buffer between the producer (the LLM) and the consumer (the Markdown widget).
When new tokens arrive before the previous update has finished, they are concatenated and stored until the widget is ready for them.
The end result is that the display is only ever a few milliseconds behind the data itself.

### Get the code

This work will shortly land in the [Textual repository](https://github.com/textualize/textual).
I would expect this to be a common occurrence working on Toad.
If it belongs in the core library it goes in the core library, so expect some Toad features being available in Textual prior to the release of Toad itself.



