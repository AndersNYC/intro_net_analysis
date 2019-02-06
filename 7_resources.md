
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


List taken from [this presentation](https://www.cl.cam.ac.uk/~cm542/teaching/2011/stna-pdfs/stna-lecture11.pdf)


## Resources

- [Stanford Large Network Dataset Collection](https://snap.stanford.edu/data/)
- [re3data - Registry of Research Data Repositories](http://networkrepository.com/)
- [NetworkX documentation](https://networkx.github.io/documentation/stable/index.html)
- [Programming Historian](https://programminghistorian.org/en/lessons/exploring-and-analyzing-network-data-with-python)

[Back to beginning](README.md)
