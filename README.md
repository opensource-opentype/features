OpenType feature reference material
===================================

This repository holds references material pertaining to the syntax,
meaning, and interaction of the various OpenType features adressed by
the Open Source OpenType project.

Where necessary, it will include additional reference information
about the various OpenType internals (like GPOS and GSUB tables) and
language/script information, but in all cases we will try to point to
external resources.

What it will not contain, though, is code.  For that, you'll want to
look in the other repositories.



Overview
========

This project addresses best practices for applications to implement
access to advanced font features, primarily those defined in the
OpenType specification, but also those defined elsewhere, like
Graphite and Apple Advanced Typography (AAT).

The features of interest break into a few broad categories.  Some
define script-shaping behavior that is mandatory to making text look
correct in a given language / writing-system combination.  Some others
are intended to be active all the time, making adjustments to glyph
selection or placement without user intervention.  Still others are
entirely optional---there to be activated by the user on an as-desired
basis.

Features in the first category should be handled by the glyph shaping
engine (e.g., HarfBuzz), and do not require special attention from the
application developer.  Features in the second category should, for
the most part, also be handled automatically by the text-rendering
stack, rather than by application code.

For features in the last category, applications that merely need to
display typographically feature-rich text should again require no new
work, but it may be important to understand the features and how they
can affect layout, bounding boxes, and other such details.  For
applications that provide text-editing capabilities, this last class
of feature will likely require new preferences and user-interface
considerations.


Registered features
===================

The bulk of modern fonts use the OpenType format, which has [a lengthy
list of pre-defined features](otf-features.md).  This list comes from
the OpenType specification.

Other fonts may use the AAT or Graphite formats, which have their own
sets of feature definitions.  

* [AAT](aat-features.md)
* [Graphite](graphite-features.md)

Many of these features map conceptually to corresponding features also
defined in OpenType.  HarfBuzz, the free-software OpenType shaping
library, comes with a [mapping](harfbuzz-feature-map.md).



Feature classes
===============

Unfortunately, despite the clean-sounding "three categories" described
above, it is not always obvious whether any particular feature belongs
in a particular category---especially when it comes to deciding
between the "invisible and active all the time" and "entirely
optional" categories.

Our attempt to break down the set of well-known features into easily
understood categories can be found on the [feature
breakdown](feature-breakdown.md) page.
