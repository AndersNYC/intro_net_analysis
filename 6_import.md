
# Reading files and importing data

Reading files can be very different depending on the format that you find them. We will practice here one that is already made for you. This part is about learning to to prepare data for analysis, which is usually the hardest and more laborious part. 


```python
with open('quakers_nodelist.csv', 'r') as nodecsv: # Open the file                       
    nodereader = csv.reader(nodecsv) # Read the csv  
    # Retrieve the data (using Python list comprehension and list slicing to remove the header row, see footnote 3)
    nodes = [n for n in nodereader][1:]

node_names = [n[0] for n in nodes] # Get a list of only the node names                                       

with open('quakers_edgelist.csv', 'r') as edgecsv: # Open the file
    edgereader = csv.reader(edgecsv) # Read the csv
    edges = [tuple(e) for e in edgereader][1:] # Retrieve the data
```


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

Quick review of List comprehension: 
`[` *output expression* `for` *iterator variable* `in` *iterable* `if` *predicate expression* `]` 



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
```

## Reading edges from source

https://networkx.github.io/documentation/stable/reference/readwrite/generated/networkx.readwrite.edgelist.read_edgelist.html 

## Adding nodes from file

`fh = open('tmp.txt', 'w')` fh meaning file handle
`g.add_node(fh)`


## If you have only an edge list:

`G = nx.read_edgelist('my_file.txt')`. You create the graph like this. 


If you need to make it a different kind of Graph, such as a DiGraph, you can pass an argument: `G = nx.read_edgelist('test.txt', create_using=nx.DiGraph())`.
If the third number is the weight, we can use `G = nx.read_edgelist('test.txt', data=(('weight',float),), create_using=nx.DiGraph())`. Don't ask me about the comma after the parenthesys in "...float),)". I can't see any sense, but that's how it is in the official documentation.

[Next](7_resources.md)
