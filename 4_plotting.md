# Plotting

`nx.draw(G)` takes graph g as argument to draw a node-link diagram of the graph. Needs matplotlib.pyplot as plt to show: `plt.show()`. `plt.savefig("image.png")` saves it to a file. `plt.clf()` to clear the contents of a graph.

nx.draw(G) is a simple option to draw without labels or axes. For more options:
`nx.draw_networkx(G) ` Lot's of options [here](https://networkx.github.io/documentation/networkx-1.10/reference/generated/networkx.drawing.nx_pylab.draw_networkx.html#networkx.drawing.nx_pylab.draw_networkx) Arrows and labels are true by defauls. (You can choose to draw only specified nodes and edges, node size, color, shape transparency, colormap scaling, linewidth...). Other options include drawing only edges `draw_network_edges(G)` or only labels `draw_network_labels(G)`.

USE SOME OF THOSE OPTIONS

One example is nx.draw_circular(G)


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

# Plotting weighted network graphs

Plotting weighted graphs is a bit more complicated and we won't be able to cover in this workshop. If you want to know more about it, here are a couple links:

https://qxf2.com/blog/drawing-weighted-graphs-with-networkx/

https://networkx.github.io/documentation/stable/auto_examples/drawing/plot_weighted_graph.html

# Another option: using other softwares

Python can do whatever you want to do in terms of plotting things. There is a learning curve though. Maybe you don't want to invest on it right now, and that is fair. One way around is to do all the analysis on python, and then save your graph on a gexf file so you can plot using softwares that are more intuitive and straightforward, such as [Gephi](https://gephi.org/), a multiplatform open-source option. To write a file in gexf format, you can use `nx.write_gexf(G, 'my_network.gexf')`. 

[Next](5_other_tools.md)
