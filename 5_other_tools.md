# Other interesting tools

The graphs are awesome and look cool, but they can only tell so much. After playing around, you will notice that many graphs look a lot like each other, and that is even more so in the case of graphs with lots of nodes. Therefore, we need other measures to help understand the characteristics of our network.

## Degrees

Let's say we are working with friends, and we want to see how many friends each person has.

`print(G.degree())` brings a dictionary with the nodes and how many connections each has. We could do a for loop to print them:

```python

for person, connections in G.degree():
    print(f"{person} has {connections} friends")
    
```

But that only works well for a small number of nodes. Another way to go would be to create a graph of the degrees:

```python

people = []
friends = []

for person, connections in G.degree():
    people.append(person)
    friends.append(connections)

plt.plot(people, friends, 'yo') # 'yo' means put dots on our Y values. Try 'yo-' to see what happens.
plt.xlabel('Person')
plt.ylabel('Friends')
plt.show()
```

If we want this graph sorted by weight, there are some extra steps, because dictionaries are unsorted by definition. If you want to try this as a challenge, take a look at [this](https://stackoverflow.com/questions/11089655/sorting-dictionary-python-3).

Note: Networkx 2.x versions have changed the way degrees work. If you try to follow a tutorial and it isn't working, that might be the reason. 


## Density

This measures how many connections exist among all the possible ones. Teoretically, all nodes could be linked to all the other nodes, but in practice, just a smaller number of those connections exist. The function density outputs a number from 0 (no connections whatsoever) to 1 (all possible connections). 

Try `nx.density(G)`. 


## Triadic closure and transitivity

The concept of triadic closure comes from the assumption that if A knows C and B knows C, it is likely that A and B also know each other, completing a triangle (A-B-C-A). The existence of such triangles in a network are a sign of communities. One way to measure it is by calculating *transitivity*. It is the ratio of the existent triangles in a community by all the possible triangles. `nx.transitivity(G)`. Just like density, transitiviy goes from 0 (none of the possible triangles exists) to 1 (all of the possible triangles exist).


## Path measurements

Think of it as the friend of a friend in a facebook network. We can calculate the distance between two entities in a network. 

If we want to check if there is a path between two nodes, we can check with `nx.has_path(G, source, target)`.

To show the shortest path of edges and nodes between two given nodes, `nx.shortest_path(G, source, target)`. Depending on the size of your graph, this operation can take a while to process since python actually checks all the possible connections. The output is the path that from source to target. If we want to know the length of that path, we can use `nx.shortest_path_length(G, source, target)`. Try it.

Another good indicatior of how close the communities in our network are, is to see the average shortest path. For that, we can use `nx.average_shortest_path_length(G)`


## Diameter

Diameter is a derivative of the shortest path measurement, diameter will output what is the longest of all the shortest path measurements. In other words, it gives the longest chain of connections. Or, better said, it gives the length of the nodes that are further apart. 

To check the diameter of a network graph, do `nx.diameter(G)`. The problem with this method is that it outputs an error if there are nodes that have no path to all others. In that case, what we could do is to find the largest component of the network, make it a subgraph and check its diameter. We won't do it here, but this is how to:

```python
components = nx.connected_components(G)
largest_component = max(components, key=len)

subgraph = G.subgraph(largest_component)
diameter = nx.diameter(subgraph)
```

[Next](6_import.ipynb)
