# Basic network operations

## Nodes

There are different ways of adding nodes. From now on, we will work only with our basic undirected graph, "G". With `G.add_node(3)` we can add a single node, in this case, the number three. If you don't get any errors, that means it worked.

To add more than one node, we can use .add\_nodes\_from(). It passes a list as argument that adds the items as nodes:

`G.add_nodes_from([1, 2, 3])`

Notice that trying to add a node that already exists does not raises an error, NetworkX quietly ignores the repeated node.

Nodes can also be other types, such as strings or floats. In the case of strings, `G.add_node('spam')` adds the word 'spam' as a node, while `G.add_nodes_from('spam')` will add each character as a node. It is more convenient than `G.add_nodes_from(['s', 'p', 'a', 'm'])`, right?

By now we should have a bunch of nodes. Try `G.number_of_nodes()` to see how many we've got. Now let's check them using `G.nodes()` which will output a list of nodes. 

The output should be a bit of a mess, with integers, string characters and a string word. Let's clean this leaving only the nodes that are numbers (integers in Python language). To remove nodes one by one, we can use `G.remove_node()`. 

To remove multiple nodes at the same time, `G.remove_nodes_from()` works in the same way as its adding version. Try it with all the other strings.

Question: if I run `G.remove_nodes_from(['spam'])` what nodes will remain in my graph?

Try it and see.

Just like its adding version, it considered each of the characters as a node to be removed. Notice that the order of the nodes does not matter. `G.remove_nodes_from('abcde')` will work in the same way as `G.remove_nodes_from('edcba')`. 


Final note here: trying to remove nodes that are not in your graph with `G.remove_node()` will raise an error, but not with `G.remove_nodes_from()`, so you can use the last one to remove undesirable values from your graph even if you are not sure they are there.

## Edges

To add edges, we can use `G.add_edge(1, 2)`, which will add an edge between nodes 1 and 2. 

If you don't know about tuples, you can google it, or read [this question on stackoverflow about the difference between them and lists](https://stackoverflow.com/questions/626759/whats-the-difference-between-lists-and-tuples), but for now you can think of them as immutable lists.

To add multiple edges at the same time, we can use the .add\_edges\_from() method, passing a list of tuples representing the edges: `G.add_edges_from([(1, 3), (2, 4), (1, 4)])`. Try it.

If the list of edges is already on a variable, you can just call the variable:

```python
my_edges = [(2,3), (1,5)]
G.add_edges_from(my_edges)
```

Going back to the example above, when we added a list of tuples, notice that even though we did not have number 4 as a node, we were able to pass this list of edges without raising any error. That's because when you add an edge of nodes that were not on graph, NetworkX automatically adds the nodes as well. You can use the '.nodes()' method and check if 4 is there now. You can create a whole network graph just by adding the edges if you want. Many networks datasets you will find online are just lists of edges.

`G.remove_edge()` and `G.remove_edges_from()` work in the same way as the adding methods. Finally, `G.clear()` removes everything from the Graph.

Again, let's check the number of edges with `G.number_of_edges()`, and we can see the list of edges with `G.edges()`. This will return a list of tuples which represents the edges.

## CHECKING DATA IN OUR GRAPH

There are other things we can check in our graph.

`(nx.info(G))` outputs a nice summary of your network. Average degree is the average number of connections of each node in your network.

## Challenge:

Let's create a thinksgiving network. The relatives are nodes and the edges represent who is in speaking terms with whom. Add at least 5 family members. You could call them by numbers, but since it is going to be a small network, let's do it by some sort of nickname. I will go with "thanksgiving" as my network name and add "Me","maga_uncle", "stoned_cousing", "vegan_sister", "yoga_aunt", "dont_bother_me_father", "gun_lover_mother_in_law" and "nice_heart_mommy" as nodes. Feel free to do it however you want. Then, make sure to add some edges of who is in speaking terms to whom. Now create some edges, at least 10 of them.


[Next](3_metadata.md)
