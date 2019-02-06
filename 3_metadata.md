# Metadata

Metadata can be stored in the graph as well.

`G.add_node(1, time='5pm')` creates the node with the metadata as a dictionary key.
`G.node[1]['color'] = 'blue'` adds one(another) metadata attribute to an existent node.
`G.node[1]['color]` will return 'blue'.
`G.node[1]` would return the dictionary "{'time': '5pm', 'color': 'blue'}"


`G.nodes(data=True)` With the "data=True" argument retreaves the node list with the metadata attached. What this returns is a list of two tuples. The first element of each tuple is the node. The second element is a dictionary. In the dictionary, in which the key value pairs correspond to the metadata.


# Weights

Same goes for edges: `G.add_edge(1, 2, weight=4.7)`. 'weight' is a special attribute and it must be numeric.

Finally, to add weighted edges, `g.add_weighted_edges_from([(1,2,2), (3,4,5),
(2,3,17)])`

`G.size()` count edges, since it comes with weight=None. If weight='weight', it will output the sum of all connections. 


## Creating nodes of interest and edges of interest


What if we want to check only nodes that match some specific requirements?

```python
noi = []
for n, d in G.nodes(data=True):
    if d['sex'] == 'Male':
        noi.append({n:d['age']}) # just n if we want only to know
```		

The same could be done for edges. We could imagine a network T that has the dates of each connection as metadata. If we wanted to get the data for a specific time, (say, only connections after january first 2010) we could do something like:

```python
eoi = []
for u, v, d in T.edges(data=True):
    if d['date'] > date(2010, 1, 1):
	    eoi.append((u,v))
```

Notice that the date would have to be on Python [datetime type](https://docs.python.org/3/library/datetime.html) to work. 


## Challenge:

Let's create a network for real so we can play around with it. First, open a file in you favorite text editor and name it "my\_network.py" .

We will create a thanksgiving network, where the nodes are the relatives, and the edges represent who is in speaking terms with whom. Try to add at least 5 family members and create some connections between them. Since it is a small network, let's use names to represent the nodes. Create at least 10 connections.



[Next](4_plotting.md)
