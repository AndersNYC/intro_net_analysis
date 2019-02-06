

# Introduction to networks

Networks are everywhere: 

- Online (relationships between people)
  - facebook
  - twitter
- Transportation networks (connectivity of locations)
  - Uber
  - Citybike
- Academic (who's citing whom)

Network analysis deals with the relationships between entities.
Possible insights from it:

- Check important entities, such as influencers in a social network;
- Find out most efficient transport paths;
- Find communities ("clustering").

# Structure of a network:

Network Graphs are data structures that consist of nodes and edges (the word "graph" comes from [graph theory](https://en.wikipedia.org/wiki/Graph_theory)). The nodes represent the entities (people, cars, etc) while the edges represent the connections. Graphs are good ways to represent networks, showing patterns that are otherwise not noticed.

PUT IMG1 HERE!


# Types of graphs

## Undirected graphs

Example: Facebook social graph. There is no directionality. If we are friends on Facebook, I am your friend, and you are my friend. Two circles are linked by a line without arrows

## Directed graphs

Example: Twitter social graph. I may follow Jessica Alba, but she might not follow me back. There is an inherit directionality on it. Circles are linked by arrows. 

## Multiple(Di)Graph

Trip records between bike sharing stations. More than one bike can leave from one station and get to another. Circles could be linked by many arrows or, more commonly, one arrow with the number of connections (weight). 

The bike sharing station example also helps us to understand the concept of a "Self-loop", a node that is connected to itself. In this case, we can think of a bike that was taken and returned in the same station. The symbol for it would be a circle with a circled arrow departing and going back to the same node.


# Creating graphs:

To work with networks, we will mainly use the NetworkX library. I will play around in the Python Interactive Shell for now, but you feel free to use any environment that suits you.

The first thing we need to do is to import the library. If you have Anaconda, NetworkX should be installed by defauld. We start our file by importing the library. By convention, we import it as 'nx'.

`import networkx as nx`

Now, we use the .Graph() method to initialize an empty network graph to which we will add nodes and edges later.

`G = nx.Graph()`

If we create an undirect graph with `G = nx.Graph()` and ask for the type, we will see an output of "networkx.classes.graph.Graph". That is the standard graph with type "Graph". 

For an undirected Graph, we would use `D = nx.DiGraph()`.

We can create a MultiGraph object with `M = nx.MultiGraph()` and a MultiDiGraph with `MD = nx.MultiDiGraph()`.

Note that "G", "D", "M" and "MD" are the variable names we chose for the graphs, but you could call them any way you want.

# CHALLENGE

If you haven't done it, create one graph for each of the options above, and check their type. Try to print the graph and see what happens. Why this result?


[Next](2_basics.md)
