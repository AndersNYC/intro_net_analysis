# Things to do

- Make sure to let it clear that most of this presentation was based on programming historian, and the other thing over there. Reference them to the original posts, which are more complete and advance and they should definitively take a look. 
- Make sure they have everything installed. Check libraries and let them know that if they have anaconda installed, they should be good to go.
- Write the description to put on eventbrite. Put the suggested requirements.
- Decide the structure of the course
- Decide a database to work with
- Decide a simple database to create with them
- Create challenges
- Look for pictures to use on the presentation
- Look for interesting conclusions drawed from network analysis
- Prepare speach about the course (I'm no expert in network analysis, I've just started, this is just an intro...) 

# Things will help if they know already

Get useful links for all of those:

- Need anaconda installed, or python + networkx + matplotlib
- Basics of python. Take the intro to python course. https://github.com/DHRI-Curriculum/python
- We will use some types that were not covered on the intro course, so it would be a good idea to read about Tuples and Dictionaries. PROVIDE LINKS
- Tuples (name comes from pair, triple, quadruple, quintuple, sextuple... hence "tuple" as a generic name) Tuples are immutable, which makes them smaller is size (bits wise) and faster in processing.
- Dictionaries
- List comprehension
- csv files
- datetime.date type: https://docs.python.org/3/library/datetime.html
- basic knowledge of networks might be handy.
- Don't let this list scare you off. If you can take a look at them before and have an idea of what they are, great. If they are not making sense, we can talk about them during the workshop.

# Introduction to networks

## Intro

Networks are everywhere: 

- Online (relationships between people)
  - facebook
  - twitter
- Transportation networks (connectivity of locations)
- Github

In sum, network analysis is modeling relationship between entities. Possible insights from it: check important entities, such as influencers in a social network; find out most efficient transport path; find communities ("clustering"). Need examples

Structure:
Nodes and edgers. They form a graph. 

Library: NetworkX 

Goals:
- model and analyze network data
- visualization of networks
- basic concepts
- how to compute important nodes
- how to find communities in a network

`G = nx.Graph()` initializes an empty graph to which we can add nodes and edges

`G.add_node(3)` adds a single node.

`G.add_nodes_from([1, 2, 3])` this method passes a list as argument that adds the integers as nodes to my graph

Note that `G.add_node('spam')` adds the word 'spam' as a node, while `G.add_nodes_from('spam')` will add each character as a node.

`G.nodes()` this method returns a list of nodes

`G.add_edge(1, 2)` adds an edge between nodes 1 and 2.

`G.add_edges_from([(1, 3), (2, 4), (1, 4)])` adds multiple edges at the same time.

If edges are stored in tuples:
`e = (2, 3)`
`g.add_edge(*e)` unpacks edge tuples
`G.add_remove_node()`, `G.remove_nodes_from()`, `G.remove_edge()` and `G.remove_edges_from()` all work in the same way as the adding versions. 

To add weighted edges, `g.add_weighted_edges_from([(1,2,.5), (1,2,.75),
(2,3,.5)])`

`G.clear()` removes all. 

`G.edges()` returns a list of tuples which represents the edges. Each tuple shows the nodes that are present on the edges.

If you try to add an existent node/edge, NetworkX quietly ignores it. Adding an edge of nodes that were not on graph automatically adds the nodes as well. 

`G.number_of_nodes()` and `G.number_of_edges()` will show the number of nodes/edges.

`print(nx.info(G))` Nice summary of your network. Average degree is the average number of connections of each node in your network

`G.neighbors(2)` will show the nodes that are neighbors here. (say, 1 and 3).

Metadata can be stored in the graph as well.

`G.add_node(1, time='5pm')` creates the node with the metadata as a dictionary key.
`G.node[1]['color'] = 'blue'` adds one(another) metadata attribute to an existent node.
`G.node[1]['color]` will return 'blue'.
`G.node[1]` would return the dictionary "{'time': '5pm', 'color': 'blue'}"

Same goes for edges: `G.add_edge(1, 2, weight=4.7)`. 'weight' is a special attribute and it must be numeric.

`G.nodes(data=True)` With the "data=True" argument retreaves the node list with the metadata attached. What this returns is a list of two tuples. The first element of each tuple is the node. The second element is a dictionary. In the dictionary, in which the key value pairs correspond to the metadata.

## basic iterations

To print edges and weights

```python
g.add_edge(1,3,weight=2.5)
g.add_edge(1,2,weight=1.5)
for n1, n2, attr in g.edges(data=True):
    print(n1, n2, attr['weight'])
```

Some useful commands to know about dictionaries: 
`my_dict.keys()` retrieve dictionary keys, while `my_dict.items()` creates a (key,value) tuple that is particularly useful with list comprehensions, as we will see later.

## Other interesting data

The graphs are awesome and look cool, but they can only tell so much. After playing around, you will notice that many graphs look a lot like each other, so we need other measures to help understande the characteristics of our network.

- Density. This measures how many connections exist among all the possible ones. Teoretically, all nodes could be linked to all the other nodes, but in practice, just a smaller number of those connections exist. The function density outputs a number from 0 (no connections whatsoever) to 1 (all possible connections). 

```python
density = nx.desnsity(G)
print(density)
```

- Shortest path measurement: friend of a friend. This calculates the shortest path of edges and nodes between two given nodes. This can take a while to process since python actually checks all the possible connections.

```python
fell_whitehead_path = nx.shortest_path(G, source="Margaret Fell", target="George Whitehead")
```


- Diameter: a derivative of the shortest path measurement, diameter will output what is the longest of all the shortest path measurements. In other words, what are the gives the longest chain of connections. This is a little bit more complicated, because it doesn't run with all the data, we need to make some changes first. Check programming historian

- Triadic closure:


## Plotting

`nx.draw(G)` takes graph g as argument to draw a node-link diagram of the graph. Needs matplotlib.pyplot as plt to show: `plt.show()`. `plt.savefig("image.png")` saves it to a file. `plt.clf()` to clear the contents of a graph.

nx.draw(G) is a simple option to draw without labels or axes. For more options:
`nx.draw_networkx(G) ` Lot's of options [here](https://networkx.github.io/documentation/networkx-1.10/reference/generated/networkx.drawing.nx_pylab.draw_networkx.html#networkx.drawing.nx_pylab.draw_networkx) Arrows and labels are true by defauls. (You can choose to draw only specified nodes and edges, node size, color, shape transparency, colormap scaling, linewidth...). Other options include drawing only edges `draw_network_edges(G)` or only labels `draw_network_labels(G)`. 

### Classic, famous and random graphs

- small famous graphs
`petersen=nx.petersen_graph()`
`tutte=nx.tutte_graph()`
`maze=nx.sedgewick_maze_graph()`
`tet=nx.tetrahedral_graph()`
- classic graphs
`K_5=nx.complete_graph(5)`
`K_3_5=nx.complete_bipartite_graph(3,5)`
`barbell=nx.barbell_graph(10,10)`
`lollipop=nx.lollipop_graph(10,20)`
- random graphs
`er=nx.erdos_renyi_graph(100,0.15)`
`ws=nx.watts_strogatz_graph(30,3,0.1)`
`ba=nx.barabasi_albert_graph(100,5)`
`red=nx.random_lobster(100,0.9,0.9)`

Challenge: create and plot one graph from each category.

List taken from [this presentation](https://www.cl.cam.ac.uk/~cm542/teaching/2011/stna-pdfs/stna-lecture11.pdf)

## Basics of NetworkX API

<!-- NetworkX has been loaded as nx.
The Twitter network has been loaded as 'T'. -->

type(T.nodes())
	<!-- shows that T networks is a list -->
len(T)
	<!-- shows the size of the graph T -->
type(T.edges(data=True)[-1][2])
	<!-- shows the type of the 3rd and last element of the last entry---which is a tuple--- of the T.edges(data=True) -->

## Basic drawing of a network

<!-- A subset of nodes from the graph was pre-loaded as T_sub -->

import matplotlib.pyplot as plt
import networkx as nx

nx.draw(T_sub)
<!-- creates the graph of subsection T_sub -->

plt.show()
<!-- plots created graph on screen -->

## Queries on a graph

`.edges()`  method that return a list of nodes

`.nodes()`
<!-- method that returns a list of tuples, in which each tuple shows the nodes that are present on that edge -->

`data=True`
Passing in the keyword argument retrieves the corresponding metadata associated with the nodes and edges as well.

`[` *output expression* `for` *iterator variable* `in` *iterable* `if` *predicate expression* `]` \
Review of List comprehension

Creating a list of the nodes of interest:

```python
noi = [n for n, d in T.nodes(data=True) if d['occupation'] == 'scientist']
```
Through a list comprehension, we got a list of nodes from the graph T that have 'occupation' label of 'scientist'.

```python
eoi = [(u, v) for u, v, d in T.edges(data=True) if d['date'] < date(2010, 1, 1)]
```

List comprehension to get a list of edges from graph T that were formed before 1 Jan 2010

## Types of graph

1. Undirected graphs\
Example: Facebook social graph. There is no directionality. If we are friends on Facebook, I am your friend, and you are my friend. Two circles are linked by a line without arrows. If we create an undirect graph with `G = nx.Graph()` and ask for the type, we will see an output of "networkx.classes.graph.Graph". That is the standard graph with type "Graph". 
2. Directed network\
Example: Twitter social graph. I may follow Jessica Alba, but she might not follow me back. There is an inherit directionality on it. Circles are linked by arrows. We can create a Directed graph with `D = nx.DiGraph()`. If we query for the type, it will return a "Digraph" object in an output of "networkx.classes.digraph.DiGraph". If you want to convert to undirected graph, there is the method `g.to_undirected()`\
3. Multiple(Di)Graph\
Trip records between bike sharing stations. More than one bike can leave from one station and get to another. Circles are linked by many arrows. To avoid becoming a mess, we can use only one arrow and give the edge a weight metadata indicating  the number of connections. We can create a MultiGraph object with `M = nx.MultiGraph()` and a MultiDiGraph with `MD = nx.MultiDiGraph()`.\
The bike sharing station example also helps us to understand the concept of a "Self-loop", a node that is connected to itself. In this case, we can think of a bike that was taken and returned in the same station. The symbol for it would be a circle with a circled arrow departing and going back to the same node.

## Checking the un/directed status of a graph

`T.edge[1][10]` explores the edge between the nodes 1 and 10. This edge might exist while `T.edge[10][1]` might not. 

To set an attribute of an edge: `network_name.edge[node_a][node_b]['attribute'] = value` In: `T.edge[1][10]['weight'] = 2` We just added another field to the metadata dictionary; 'weight' will indicate the "strenght" of an edge. 

Another way is to iterate. (Couldn't find a practical use for this, but here it goes). To set the weight of every edge involving node 293 to be equal to 1.1: 
```python
for u, v, d in T.edges(data=True):
    if 293 in [u, v]:
	    T.edge[u][v]['weight'] = 1.1
```

# Checking whether there are self-loops in the graph

Ideally, you should check for the existence of self-loops before starting the analysis. Use the method `.number_of_selfloops()` for that. The function below creates a list with self-loops and then checks if they are all there.

```python
# Define find_selfloop_nodes()
def find_selfloop_nodes(G):
    """
    Finds all nodes that have self-loops in the graph G.
    """
    nodes_in_selfloops = []
    
    # Iterate over all the edges of G
    for u, v in G.edges():
    
    # Check if node u and node v are the same
        if u == v:
        
            # Append node u to nodes_in_selfloops
            nodes_in_selfloops.append(u)
            
    return nodes_in_selfloops

# Check whether number of self loops equals the number of nodes in self loops
assert T.number_of_selfloops() == len(find_selfloop_nodes(T))
```

# Network visualization

Regular graphs with too many edges become irrational and look like a hair ball. Other types of visualization can help us to better understand patterns.

1. Matrix plots\
Looks like the New York Times crossword. Go from line to column. If it is non directional, there will be a grey diagonal (since there is no self-loop) and the graph will be symetric (since if a is linked to b, b is linked to a). If the rows are order, the matrix plot can help visualize clusters (like neighbors being close to one another can show a community)
2. Arc plots\
Nodes are ordered on one axis and edges go in a semicircle. If the nodes are ordered with a particular logic (age in social network, geography in a transport network), it will be possible to confront that logic with connectivity. Arc plots are also a good basis for more complex plots we will see later.
3. Circos plot\
Modification of Arc plots. Two ends of arcplots are made into a circle. Aesthetic and compact alternative to Arc plots
4. nxviz API:\
```python
import nxviz as nv
import matplotlib.pyplot as plt

ap = nv.ArcPlot(G)
# instanciate a nv.ArcPlot object and pass the graph G as argument

ap.draw() # to create the plot
plt.show() # to plot it
```
# Visualizing using Matrix plots

When creating a matrix plot with `nv.MatrixPlot(T)` , MatrixPlot uses `nx.to_numpy_matrix(T)` under the hood. In doing so, it loses all the metadata except for 'weight'. To create graph from numpy matrix and vice-versa: `A = nx.to_numpy_matrix(T)` converts a graph to a matrix format, while `T_conv = nx.from_numpy_matrix(A, create_using=nx.DiGraph())` converts it back. Notice that it could be a non-directional graph by calling only "Graph()".

# Visualizing using Arc plots

Arguments `node_order='keyX'` and `node_color='keyX'` specify a key in the node metadata dictionary to color and order the nodes by. Check the example below:

```python
import matplotlib.pyplot as plt
from nxviz import ArcPlot

a2 = ArcPlot(T, node_order='category', node_color='category')

a2.draw()

plt.show()
```

# Reading files and importing data in the Quaker example

We will use the two files that we have available. First, let's create a plaintext file in our directory. Then proceed to import things we need. Depending on how your data comes, the procedure would be different. This is part of knowing how to prepare data for data analysis, which is usually the harderst and more laborious part. 

```python
with open('quakers_nodelist.csv', 'r') as nodecsv: # Open the file                       
    nodereader = csv.reader(nodecsv) # Read the csv  
    # Retrieve the data (using Python list comprhension and list slicing to remove the header row, see footnote 3)
    nodes = [n for n in nodereader][1:]

node_names = [n[0] for n in nodes] # Get a list of only the node names                                       

with open('quakers_edgelist.csv', 'r') as edgecsv: # Open the file
    edgereader = csv.reader(edgecsv) # Read the csv
    edges = [tuple(e) for e in edgereader][1:] # Retrieve the data
```

## Adding nodes from file

`fh = open('tmp.txt', 'w')` fh meaning file handle
`g.add_node(fh)`

## Programming Historian tutorial
 ```python
import csv

node_csv = open('quakers_nodelist.csv', 'r') # opens the file

node_reader = csv.reader(node_csv) # reads the csv
```

The csv readers don't support indexing. The value returned is not a list, it is an iterator over the rows. To make them a list:

```python
nodes = []
for n in node_reader:
    nodes.append(n)
```
`node_csv.close()` It is important to close all files we open to save memory. It is good coding practice.


`print(nodes[0:3])` Problem: first item in the list is not data, it is a header.

```python
node_names = []
for n in nodes:
    node_names.append(n[0])

print(node_names[0:3])
```

`del node_names[0]` to get rid of the header.

Now we want to do the same with the edges list.

```python
edge_csv = open('quakers_edgelist.csv', 'r')
edge_reader = csv.reader(edge_csv)

edges = []
for e in edge_reader:
    edges.append(tuple(e)) # we need to make them as tuples to be in conformity with the standards of NetworkX. If we don't do this, it will produce a list of lists.

print(edges[0:3]) # again, first item is a header. We want to get rid of it.

del edges[0]
print(edges[0:3])
```

As it happens most of the times in programming, there is a better way to write those things above. Better code is usually more concise and clean, which makes them easier to write and to read.

```python
with open('quakers_nodelist.csv', 'r') as nodecsv:
    nodereader = csv.reader(nodecsv)
    nodes = [n for n in nodereader][1:]
```

The with statement makes sure that the file will be open only for what is inside the statement, closing it automatically after it is done. The list comprehension works as a for loop, but it is cleaner.


- Challenge: let's grab one of the files that I brought and prepare them to work
- Challenge 2: if you are feeling particularly adventurous, try it with the more concise writing.

Now, to make them a Graph:

```python
G = nx.Graph()

G.add_nodes_from(node_names)
G.add_edges_from(edges)

print(nx.info(G)) # Average degree is the average number of connections of each node in your network
```

We now want a list of attributes. Remember that we have all of them in the variable `nodes`. We will use the functions: `nx.set_node_attributes()` and `nx.set_edge_attributes()`. Remember, those attributes must be in a dictionary form. We will create a dictionary for each of the values that we have in our list and add them as node attributes with `.set_node_attributes(Networkx_Graph_name, dictionary_name, string_name)`


```python
hist_sig_dict = {}
gender_dict = {}
birth_dict = {}
death_dict = {}
id_dict = {}

for node in nodes:
    hist_sig_dict[node[0]] = node[1]
	gender_dict[node[0]] = node[2]
	birth_dict[node[0]] = node[3]
	death_dict[node[0]] = node[4]
	id_dict[node[0]] = node[5]
	

nx.set_node_attributes(G, hist_sig_dict, 'historical_significance')
nx.set_node_attributes(G, gender_dict, 'gender')
nx.set_node_attributes(G, birth_dict, 'birth_year')
nx.set_node_attributes(G, death_dict, 'death_year')
nx.set_node_attributes(G, id_dict, 'sdfb_id')
```

Now we have a working graph with attributes and we can use visualization tools as before. For example:

```python
for n in G.nodes():
    print(n, G.node[n]['birth_year'])


## Reading edges from source

https://networkx.github.io/documentation/stable/reference/readwrite/generated/networkx.readwrite.edgelist.read_edgelist.html 

## Resources

- [Stanford Large Network Dataset Collection](https://snap.stanford.edu/data/)
- [re3data - Registry of Research Data Repositories](http://networkrepository.com/)
- [NetworkX documentation](https://networkx.github.io/documentation/stable/index.html)
- [Programming Historian](https://programminghistorian.org/en/lessons/exploring-and-analyzing-network-data-with-python)  
