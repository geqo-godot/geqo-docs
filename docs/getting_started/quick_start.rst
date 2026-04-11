:allow_comments: True

.. _doc_getting_started_quick_start:
Quickstart
==========

GEQO was designed to be simple to pick up and start designing with. Here are the steps to get it running in your project.

Installation
------------
1. Grab the latest `release <https://github.com/geqo-godot/geqo/releases>`_ compatible with your Godot version.
2. Unpack the addons/geqo folder into your /addons folder in your Godot project.
3. Enable the addon within the Godot settings: Project > Project Settings > Plugins


Key concepts
------------
**Context** - This is a reference point to any Generator or Test, which can be a single Node, or entire groups of nodes. For example, Generators will generate points around each node in the context. Contexts can be Nodes or just positions.

**Generator** - They produce potential locations (called Items) that will then be evaluated by the tests for testing.

**Test** - These are used to decide which of the generated Items is the best, multiple tests can be used for more control over the final result. For example, one can test whether a Context is in line of sight of each Item, or how far that Context is.


How a query is built
--------------------

Create your first query
-----------------------

Testing and debugging the query
-------------------------------
