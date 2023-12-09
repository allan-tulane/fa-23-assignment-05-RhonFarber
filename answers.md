# CMPS 2200 Assignment 5
## Answers

**Name:** Rhon Farber






- **1a.**
The maximum depth of a d-ary heap is O(log_d n). This is because max depth of a binary heap is O(log_2 n), so replacing log_2 with log_d is the max depth for d-ary heap.

- **1b.**
The work done by delete-min in a d-ary heap is O(log_d n), where n is the height of the heap. This is because delete-min for a binary heap has a work of O(log n) for the depth of the binary heap aka the number of swaps and each recursive call is doing constant work for swapping.

The work done by insert in a d-ary heap is also O(log_d n), where n is the height of the heap. Each recursive call is doing constant work for swapping and number of swaps is the height of the heap.

- **1c.**
The work for using a d-ary heap for Dijkstra's algorithm would be the work of delete-min + the work of insert. The work of delete-min is |V| calls each doing O(log_d |V|) work, so O(∣V∣log_d ∣V∣) total work. The work of insert is |E| calls each doing O(log_d ∣V∣) work, so O(∣E∣log_d ∣V∣) total work. Therefore, the total work for the entire algorithm is O(∣V∣log_d ∣V∣) + O(∣E∣log_d ∣V∣).

- **1d.**


- **2a.**
k = 0:
APSP(0,0,0) = 0.0
APSP(0,1,0) = -2.0
APSP(0,2,0) = 2.0
APSP(1,0,0) = -2.0
APSP(1,1,0) = 0.0
APSP(1,2,0) = 1.0
APSP(2,0,0) = 2.0
APSP(2,1,0) = 1.0
APSP(2,2,0) = 0.0
k = 1:
APSP(0,0,1) = 0.0
APSP(0,1,1) = -2.0
APSP(0,2,1) = -1.0
APSP(1,0,1) = -2.0
APSP(1,1,1) = 0.0
APSP(1,2,1) = 1.0
APSP(2,0,1) = -1.0
APSP(2,1,1) = 1.0
APSP(2,2,1) = 0.0
k = 2:
APSP(0,0,2) = 0.0
APSP(0,1,2) = -2.0
APSP(0,2,2) = -1.0
APSP(1,0,2) = -2.0
APSP(1,1,2) = 0.0
APSP(1,2,2) = 1.0
APSP(2,0,2) = -1.0
APSP(2,1,2) = 1.0
APSP(2,2,2) = 0.0

- **2b.**
Yes, I do see a relationship between APSP(i,j,1) and APSP(i,j,2). In terms of the graph given, the solutions are identical. This occurs because the graph is small, and the inclusion of the third vertex (vertex 2) does not provide any new shorter paths that were not already accounted for by vertices 0 and 1. In general however, the relationship is demonstrated below.

APS(i,j,2) in terms of APS(i,j,0) and APS(i,j,1) can be represented as:
APSP(i,j,2) = min(APSP(i,j,1), APSP(i,2,1) + APSP(2,j,1))

The first term considers the existing path with at most one intermediate vertex and the second term explores the possibility of using vertex 2 as an intermediate point. The formula then takes the minimum of these two options to ensure the shortest path is found.

- **2c.**
An optimal substructure property for APSP(i,j,k) i.e., the shortest path from i to j with k intermediaries is the best solution to each of its subproblems defined as the shortest path from i to j with k-1 intermediaries. This property can be defined as: APSP(i,j,k) = min(APSP(i,j,k−1), APSP(i,k,k−1) + APSP(k,j,k−1)). The first term being the shortest route from i to j that doesn't include stopping at point k, and the second term being going from i to k and then from k to j, using the shortest routes that don't include k for both parts.

- **2d.**
For a graph with n vertices, there are n possible values for i, n possible values for j, and n possible values for k, since k ranges from 0 to n-1 where n is the number of vertices in the graph. Therefore, the number of distinct subproblems that we might need to compute is: n * n * n = n^3. Therefore, the resulting work of this dynamic programming algorithm is O(n^3) where each distinct subproblem, APSP(i, j, k), would be computed exactly once. 

- **2e.**
The work of Johnson's algorithm is O(|V|^2 * log |V| + |V| * |E|). This is derived from first running the Bellman-Ford algorithm to reweight the edges to eliminate negative weights. Then Johnson's algorithm runs Dijkstra's algorithm once from each vertex, each being O(E + V * log V). In comparison to the algorithm we have been working on with work of O(V^3), what matters is the proportion of edges to vertices. If the number of edges is close to the number of vertices squared then the DP algorithm is preferable. If the number of edges is less than the number of vertices squared then Johnson's algorithm is better because V * E will asymptotically dominate V^3 making Johnson's algorithm more efficient.

- **3a.**


- **3b.**


- **3c.**
