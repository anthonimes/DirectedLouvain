# Directed Louvain algorithm

The algorithm used in this package is based on the Louvain algorithm developed by V. Blondel, J.-L. Guillaume, R. Lambiotte, E. Lefebvre and was downloaded on the [Louvain algorithm webpage] (https://sites.google.com/site/findcommunities/) (**[2]**).
The algorithm was then adjusted to handle directed graphs and to optimize the directed modularity of Leich and Newman instead of the classic modularity.
These modifications were mostly made by [Anthony perez] (https://www.univ-orleans.fr/lifo/membres/Anthony.Perez) and by [Nicolas Dugué] (https://lium.univ-lemans.fr/team/nicolas-dugue/).

The directed modularity is proved to be more efficient in the case of directed graphs as shown in [Directed Louvain : maximizing modularity in directed networks] (https://hal.archives-ouvertes.fr/hal-01231784) (**[3]**) and was also succesfully used in [A community role approach to assess social capitalists visibility in the Twitter network] (https://hal.archives-ouvertes.fr/hal-01163741) with Vincent Labatut and Anthony Perez (**[1]**).

**The README below is adapted from the Louvain algorithm: our package works in a similar way.**

-----------------------------------------------------------------------------
## How to use

Computes communities and displays hierarchical tree:

    ./bin/community graph/graph.txt -l -1 -v > graph.tree

The graph **must** be in edgelist format, that is one edge per line as follows (the `weight` being optional):  

    src dest [weight]

Moreover, it is **mandatory** that vertices of the input graph are numbered from `0` to `n-1`. 
To ensure a proper computation of the communities, the default computation encompasses a renumbering of the input graph. 
The option `-n` indicates that the graph is already numbered from `0` to `n-1` and hence avoids renumbering. 
**Important**: communities are written using the **original label nodes**.

Another possibility is to pass a binary file containing all information regarding the graph. 
This file **must** be generated using the `-r` option, see below. In this case, the 
only mandatory option is `-w` to indicate whether the graph is weighted. 

Several options are available, among which:
+ `-w` to indicate that the input graph is weighted
+ `-n` to indicate that the input graph is correctly numbered (from `0` to `n-1`)
+ `-r` for reproducibility purposes: the renumbered and binary graphs are stored on 
files and can be reused. 

More options and information are provided using `./bin/community`

## Examples 
Using `graph/graph.txt` one obtains: 

    ./bin/community graph/graph.txt -l -1 -v -w -r > graph/graph.tree

to compute hierarchical community structure (using **original** label nodes) 
by first renumbering the graph, and 
then writing files for reproducibility. The next runs would thus be: 

    ./bin/community graph/graph.bin -w -l -1 > graph/graph.tree

Finally, using an already renumbered graph one gets: 

    ./bin/community graph/graph_renum.txt -l -1 -v -w -n > graph/graph.tree

The program can also start with any given partition using -p option

    ./community graph.bin -p graph.part -v

### Improvements

To ensure a faster computation (with a loss of quality), one can use
the -q option to specify that the program must stop if the increase of
modularity is below epsilon for a given iteration or pass:

    ./bin/community graph/graph.bin -w -l -1 -q 0.0001 > graph/graph.tree

-----------------------------------------------------------------------------
**Display communities information**

Displays information on the tree structure (number of hierarchical
levels and nodes per level):

    ./hierarchy graph.tree

Displays the belonging of nodes to communities for a given level of
the tree:

    ./hierarchy graph.tree -l 2 > graph_node2comm_level2

-----------------------------------------------------------------------------
## References
* **[1]** Nicolas Dugué, Vincent Labatut, Anthony Perez. A community role approach to assess social capitalists visibility in the Twitter network. Social Network Analysis and Mining, Springer, 2015, 5, pp.26.
* **[2]** BLONDEL, Vincent D., GUILLAUME, Jean-Loup, LAMBIOTTE, Renaud, et al. Fast unfolding of communities in large networks. Journal of Statistical Mechanics: Theory and Experiment, 2008, vol. 2008, no 10, p. P10008.
* **[3]** Nicolas Dugué, Anthony Perez. Directed Louvain : maximizing modularity in directed networks. [Research Report] Université d'Orléans. 2015.
