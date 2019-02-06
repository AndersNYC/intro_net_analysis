# Plotting

`nx.draw(G)` takes graph g as argument to draw a node-link diagram of the graph. Needs matplotlib.pyplot as plt to show: `plt.show()`. `plt.savefig("image.png")` saves it to a file. `plt.clf()` to clear the contents of a graph.

`nx.draw(G)` is a simple option to draw without labels or axes. Let's try it.

For more options, we can use `nx.draw_networkx(G)`. There are a lot of options, you can check it [here](https://networkx.github.io/documentation/networkx-1.10/reference/generated/networkx.drawing.nx_pylab.draw_networkx.html#networkx.drawing.nx_pylab.draw_networkx) Whe using this option, arrows and labels are true by default.


# Network visualization

# Plotting weighted network graphs

Plotting weighted graphs is a bit more complicated and we won't be able to cover in this workshop. If you want to know more about it, here are a couple links:

https://qxf2.com/blog/drawing-weighted-graphs-with-networkx/

https://networkx.github.io/documentation/stable/auto_examples/drawing/plot_weighted_graph.html

# Another option: using other softwares

Python can do whatever you want to do in terms of plotting things. There is a learning curve though. Maybe you don't want to invest on it right now, and that is fair. One way around is to do all the analysis on python, and then save your graph on a gexf file so you can plot using softwares that are more intuitive and straightforward, such as [Gephi](https://gephi.org/), a multiplatform open-source option. To write a file in gexf format, you can use `nx.write_gexf(G, 'my_network.gexf')`. 

# CHALLENGE

Check this [link](https://networkx.github.io/documentation/networkx-1.10/reference/generated/networkx.drawing.nx_pylab.draw_networkx.html#networkx.drawing.nx_pylab.draw_networkx) and make two changes in your plot. If you are out of ideas, you can change the color and size of the nodes. Remember: plotting in Python has a very steep learning curve, so if you try something too bold, it might take you some time to figure out how to make it work.

[Next](5_other_tools.md)

