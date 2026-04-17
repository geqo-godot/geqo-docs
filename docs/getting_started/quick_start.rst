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

**Generator** - They produce potential locations (called Items) that will then be evaluated by the tests.

**Test** - These are used to decide which of the generated Items is the best, multiple tests can be used for more control over the final result. For example, one can test whether a Context is in line of sight of each Item, or how far that Context is.


How a query is built
--------------------
1. The root of a query is always EnvironmentQuery3D or EnvironmentQuery2D.
2. After that, several QueryContexts can be placed under EnvironmentQuery.
3. EnvironmentQuery needs one QueryGenerator node as a child to work.
4. The generator has QueryTests as children.

How to request queries
----------------------
Queries are requested with ``request_query()``, and extracted via signal or cached result.

.. tabs::
 .. code-tab:: gdscript
    # First, the signal is connected
    func _ready():
        $EnvironmentQuery3D.query_finished.connect(_on_query_finished)

    # Then, whenever a position is needed, you need to request it
    $EnvironmentQuery3D.request_query()
    
    func _on_query_finished(result: QueryResult3D):
        # You can get just the position
        var best_position: Vector3 = result.get_highest_score_position()
        # You can also get the node the Generator picked
        var best_node: Node = result.get_highest_score_node()
        # From here you can do your navigation logic
        navigate_to(best_position)
        # Or perform an action with the node
        consume(best_node)

You can also use ``await`` to get the results.
.. tabs::
 .. code-tab:: gdscript
    $EnvironmentQuery3D.request_query()
    await $EnvironmentQuery3D.query_finished
    var query_result: QueryResult3D = $EnvironmentQuery3D.get_result()
    var best_position: Vector3 = query_result.get_highest_score_position()

Testing and debugging the query
-------------------------------
EnvironmentQuery3D/2D have the ``use_debug_shapes``, which enable you to see the final score of each item, from green to red, and blue if they are filtered.
In the ``Monitors`` tab in the debugger, you can see min/max query time, average query time and latest query time.
Some tests have their own visual debugging, such as TestPathFindTo3D that you need to turn on independently of ``use_debug_shapes``
