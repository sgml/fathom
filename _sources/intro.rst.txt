============
Introduction
============

Fathom is a JavaScript framework for extracting meaning from web pages, identifying parts like Previous/Next buttons, address forms, and the main textual content—or classifying a page as a whole. Essentially, it scores DOM nodes and extracts them based on conditions you specify. A Prolog-inspired system of types and annotations expresses dependencies between scoring steps and keeps state under control. It also provides the freedom to extend existing sets of scoring rules without editing them directly, so multiple third-party refinements can be mixed together.

Why?
====

A study of existing projects like Readability and Distiller suggests that purely imperative approaches to semantic extraction get bogged down in the mechanics of DOM traversal and state accumulation, obscuring the operative parts of the extractors and making new ones long and tedious to write. They are also brittle due to the promiscuous profusion of state. Fathom is an exploration of whether we can make extractors simpler and more extensible by providing a declarative framework around these weak points. In short, Fathom handles tree-walking, execution order, and annotation bookkeeping so you don't have to.

Specific Areas We Address
=========================

* Browser-native DOM nodes are mostly immutable, and ``HTMLElement.dataset`` is string-typed, so storing arbitrary intermediate data on nodes is clumsy. Fathom addresses this by providing the Fathom node (or :term:`fnode`, pronounced fuh-NODE), a proxy around each DOM node which we can scribble on.
* With imperative extractors, any experiments or site-specific customizations must be hard-coded in. On the other hand, Fathom's :term:`rulesets<ruleset>` (the programs you write in Fathom) are unordered and thereby decoupled, stitched together only by the :term:`types<type>` they consume and emit. External rules can thus be plugged into existing rulesets, making it easy to experiment without maintaining a fork—or to provide dedicated rules for particularly intractable web sites.
* Types provide an easy way to categorize DOM nodes. They are also Fathom's black-box units of abstraction, as functions are in other programming languages. Complex extractors can begin by attaching broad types to nodes and then narrowing to more specific ones as they are examined more closely. (Each type implicitly provides a hook point to interpose additional rules.) Relationships between type-taggings can also be harnessed through logical operators like :func:`and`, and, in the future, ``or``, ``not``, and ``contains``, building higher levels of abstraction.
* The type system also makes explicit the division between a ruleset's public and private APIs: the types are public, and the imperative activity that goes on inside callback functions is private. Third-party rules can use the types as hook points to interpose themselves.
* Persistent state is cordoned off in typed :term:`notes<note>` on fnodes. Thus, when a rule declares that it takes such-and-such a type as input, it can rightly assume (if rules are written consistently) there will be a note of that type on the fnodes that are passed in.

Bonus Features
--------------

* Efficient execution, driven by a query planner that understands inter-rule dependencies
* Lazy execution, so you can have arbitrarily large rulesets with impunity
* Caching to keep from re-deriving intermediate results between queries
* Clustering based on a notion of DOM node distance influenced by structural similarity
* Many handy utils from which to compose scoring callbacks


Support
=======

You can find us on...

* #fathom on irc.mozilla.org
* `GitHub <https://github.com/mozilla/fathom>`_
* `The mailing list <https://mail.mozilla.org/listinfo/fathom>`_
