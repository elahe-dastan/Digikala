# Digikala
## Similarity Search, Hierarchical Navigable Small World (approximate search of nearest neighbors)

Construct efficient multy-layered graphs to boost speed in massice volumes of data

The main idea of HNSW is to construct such a graph where a path between any pair of vertices could be traversed in a small number of steps.

All people are six or fewer social connections away from each other (six handshakes rule)

### Skip lists
Skip list is a probabilistic data structure that allows inserting and searching elements within a sorted list for O(logn) on average.

It's constructed by several layers of linked lists. The lowesr layer has all the elements. When moving to higher levels, the number of skipped elements increases (decreasing the number of connections)

![images/skip-list.jpg](images/skip_list.jpg)

Search for the value starts from the highest level and compares it with its next element:

If the value is less or equal to the next elemnt, proceeds to its next element otherwise, descend to the lower layer and repeat the same. At the end the algorithm finds the desired node.

If an element appears in layer i, then the probability that it will appear in layer i + 1 is equal to p (usually set to 0.5 or 0.25). 

This process is much faster than the normal linear search in the linked list. In fact, HNSW inherits the same idea but instead of linked lists, it uses graphs.

### Navigable Small World
Navigable small world is a graph with polylogarithmic T = O(log^k(n)) search complexity which uses greedy routing. Routing refers to the process of starting from low-degree vertices and ending with high-degree vertices. Since low-degree vertices have very few connections, the algorithm can rapidly move between them to efficiently navigate to the region where the nearest neighbor is likely to be located. Then it gradually zooms in and switches to high-degree vertices.

#### Search
![images/photo_2024-10-28_15-35-07.jpg](images/photo_2024-10-28_15-35-07.jpg)

Node A is used as an entry point. Node D is closer to the query than B. Then node E is the closest neighbour to the query, so we move to E. Finally the search process will lead to node L. Since all neighbours of L are located further from the query than itself, we stop the algorithm and return L as the answer to the query.

Early stopping is one of the problems of the algorithm. It occurs especially at the beginning of the search procedure when there are no better neighbour nodes than the current one. This might happen when the starting region has too many low-degree vertices.

![images/photo_2024-10-28_15-55-52.jpg](images/photo_2024-10-28_15-55-52.jpg)

the accuracy can be improved by using several entry points
