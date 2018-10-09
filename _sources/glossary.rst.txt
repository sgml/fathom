========
Glossary
========

.. glossary::

   fnode
       A data structure parallel to a DOM node, holding :term:`scores<score>`, :term:`notes<note>`, and :term:`types<type>` pertaining to it. See :doc:`fnodes`.

   note
       An arbitrary, opaque-to-Fathom piece of data attached to a given :term:`type` on a :term:`fnode`. Notes can be consulted by scoring callbacks and are a good place to park expensive-to-recompute information. They are the main way of passing data between rules.

   ruleset
       The unordered collection of rules that forms a Fathom program. See :doc:`using` for more on the relationships between top-level constructs.

   score
       The fuzzy-edged part of :term:`fnode` state. A floating-point number attached to a certain :term:`type` on a :term:`fnode`. They often represent the degree to which a node belongs to a type.

   type
       A string-typed category assigned to a :term:`fnode`. Types are the boolean, hard-edged, enumerated parts of fnode state. They also largely determine inter-rule dependencies and thus which rules get run in response to a query.
