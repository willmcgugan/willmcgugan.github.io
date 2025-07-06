---
layout: post
title: Bridging the JS and Python divide
categories: [tech]
---

The JS world has `npx` to install tools, and Python has `uvx`.
Both of which give you quick access to CLI apps that might not be published on the package managers favored by your OS.

I like them because you can give out a single command to install on all platforms.

My only reservation is that unless you have used both ecosystems you are likely to prefer one over the other purely out of familiarity.

I asked on [Xitter](https://x.com/willmcgugan/status/1941818072521715778) if there was a way to bridge these two ecosystems, so JS devs could install Python tools in a way that was familiar (and vice versa).

Turns out [Trevor Manz](https://x.com/trevmanz) had that very though a while back&mdash;and it is already possible!

JS devs, try the following to run a Python tool:


```
npx @manzt/uv tool run textual-demo
```

Python devs, you can do this:

```
uvx textual-demo
```

