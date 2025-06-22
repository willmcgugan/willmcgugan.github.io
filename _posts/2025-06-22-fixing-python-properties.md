---
layout: post
title: Fixing Python Properties
categories: [tech, python]
date: 2025-06-22 15:30:00 +0100
---

Python properties work well with type checkers such MyPy and friends.
This is to be expected, given how conventional the properties are in Python code.
However there is one area where properties do not play so well with type checkers.

The type of your property is taken from the getter only.
Even if your setter accepts different types, the type checker will complain on assignment.
This could be an oversight and perhaps should be flagged, but there are some legitimate uses for a setter that accepts different types.

Let's look at a practical example (and the actual use case that lead to me discovering this).
I want to be able to specify *padding* for a component in UI, which can be specified in the same way as CSS in the browser.
A single value may be given for equal space around the component, or two values for the horizontal and vertical edges, or four values (one for each side).

Here's how you might capture that with a traditional property:

```python
from __future__ import annotations

type PaddingDimensions = int | tuple[int] | tuple[int, int] | tuple[int, int, int, int]


def unpack_padding(pad: PaddingDimensions) -> tuple[int, int, int, int]:
    """Unpack padding specified in CSS style."""
    if isinstance(pad, int):
        return (pad, pad, pad, pad)
    if len(pad) == 1:
        _pad = pad[0]
        return (_pad, _pad, _pad, _pad)
    if len(pad) == 2:
        pad_top, pad_right = pad
        return (pad_top, pad_right, pad_top, pad_right)
    if len(pad) == 4:
        top, right, bottom, left = pad
        return (top, right, bottom, left)
    raise ValueError(f"1, 2 or 4 integers required for padding; {len(pad)} given")


class WithPadding:
    def __init__(self, padding: PaddingDimensions):
        self._padding = unpack_padding(padding)

    @property
    def padding(self) -> tuple[int, int, int, int]:
        return self._padding

    @padding.setter
    def padding(self, padding: PaddingDimensions) -> None:
        self._padding = unpack_padding(padding)


with_padding = WithPadding(0)
with_padding.padding = (1, 2)  # Typing error!
```

This allows the developer to set `padding=1`, or `padding=(1, 2)`, or `padding=(1, 2, 3, 4)`.
It works just fine, but the type checker will complain about setting anything other than a tuple of 4 ints.

We could just require that the dev always uses a tuple of four integers, but that places a burden on the caller.
I also like to avoid punishing the dev if they want to write something in a more natural / expressive way.

Fortunately, we can create a property which does allow for this kind of flexibility.
The trick is to implement the property with a Python *descriptor*.

The code is only a fraction more verbose:

```python
from __future__ import annotations

type PaddingDimensions = int | tuple[int] | tuple[int, int] | tuple[int, int, int, int]


def unpack_padding(pad: PaddingDimensions) -> tuple[int, int, int, int]:
    """Unpack padding specified in CSS style."""
    if isinstance(pad, int):
        return (pad, pad, pad, pad)
    if len(pad) == 1:
        _pad = pad[0]
        return (_pad, _pad, _pad, _pad)
    if len(pad) == 2:
        pad_top, pad_right = pad
        return (pad_top, pad_right, pad_top, pad_right)
    if len(pad) == 4:
        top, right, bottom, left = pad
        return (top, right, bottom, left)
    raise ValueError(f"1, 2 or 4 integers required for padding; {len(pad)} given")


class PaddingProperty:
    """Descriptor to get and set padding."""

    def __get__(self, obj: WithPadding, _) -> tuple[int, int, int, int]:
        return obj._padding

    def __set__(self, obj: WithPadding, padding: PaddingDimensions) -> None:
        obj._padding = unpack_padding(padding)


class WithPadding:

    def __init__(self, padding: PaddingDimensions):
        self._padding = unpack_padding(padding)

    padding = PaddingProperty()


with_padding = WithPadding(0)
with_padding.padding = (1, 2)  # This works!
```

The `@property` has been replaced with a descriptor called `PaddingProperty`.
Descriptors allow different types for the `__get__` and `__set__` operations, and MyPy is now happy with that last assignment, and the other variations.
From the caller's point of view, the API hasn't change at all, but now the typing works.

Personally I think that if the property setter has to accept the same type as the getter, then the type checker should complain about the setter, and not the assignment.
If anyone knows why that isn't the case, let me know!
But if you want this flexibility, descriptors are a solid way of doing that.

For a great introduction to descriptors, see [Rodrigo Serrão's 2023 talk](https://www.youtube.com/watch?v=eXkBfRqJ2f8&ab_channel=PythonIreland) on the subject.

Ping me on the socials, if you want more content like this.