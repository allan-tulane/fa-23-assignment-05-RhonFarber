# CMPS 2200 Assignment 5
## Answers

**Name:** Rhon Farber






- **1a.**
The maximum depth of a d-ary heap is O(log_d n). This is because max depth of a binary heap is O(log_2 n), so replacing log_2 with log_d is the max depth for d-ary heap.

- **1b.**
The work done by delete-min in a d-ary heap is O(d log_d n), where n is the height of the heap. This is because delete-min for a binary heap has a work of O(log n) for the depth of the binary heap aka the number of swaps and each recursive call is doing d work for comparing all children and then swapping if necessary. 

The work done by insert in a d-ary heap is O(log_d n), where n is the height of the heap. Each recursive call is doing constant work for swapping and number of swaps is the height of the heap.

- **1c.**
The work for using a d-ary heap for Dijkstra's algorithm would be the work of delete-min + the work of insert. The work of delete-min is O(d log_d n). The work of insert is |E| calls each doing O(log_d n) work, so O(|E|log_d n) total work. Therefore, the total work for the entire algorithm is dominated by O(d log_d |E|).

- **1d.**
To achieve a runtime of O(|E|), d must be equal to |E| aka the amount of edges because then O(d log_d |E|) becomes O(|E| log_|E| |E|) which simplifies to O(|E|) since the identity property of logarithms states that the logarithm of a base to that same base is always 1, i.e., log_|E| |E| = 1. 

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
For a graph with n vertices, there are v possible values for i, v possible values for j, and e possible values for k, since k ranges from 0 to n-1 where n is the number of vertices in the graph. Therefore, the number of distinct subproblems that we might need to compute is: v * v * e = v^2 * e. Therefore, the resulting work of this dynamic programming algorithm is O(|V|^2 |E|) where each distinct subproblem, APSP(i, j, k), would be computed exactly once. This work can be even further reduced through memoization because APSP(i,j,k) is the same as APSP(j,i,k) as long as the graph is undirected. Therefore, the work of our algorithm is O(|V| |E|)

- **2e.**
The work of Johnson's algorithm is O(|V| * |E| log |E|). In comparison to the algorithm we have been working on with work of O(|V| |E|), what matters is the amount of edges. Both algorithms have |V|, so what matters is whether |E| < |E| log |E| because when this is true then our algorithm is more efficient. What this means is that our algorithm is more efficient when the amount of edges is greater than the base of the log. Assuming log base 10, then our algorithm is more efficient if |E| is greater than 10, otherwise Johnson's algorithm is more efficient.

- **3a.**
Yes, a solution to MST is guaranteed to be a solution to MMET. This is because the process of minimizing the total weight of the tree also minimizes the weight of the heaviest edge included in that tree (greedy criteria is valid). You can also prove this by contradiction. If an MST did not satisfy the MMET criterion (minimizing the weight of the heaviest edge in the spanning tree), it would imply that there exists a spanning tree with a lower maximum edge weight than the MST. However, this would contradict the principle of MST, where every edge is chosen to ensure the lowest total and individual edge weights.

- **3b.**
def findNextBestMST(graph):
    # Step 1: Find the optimal MST using Prim's algorithm
    optimalMST = primsAlgorithm(graph)

    # Initialize a min heap to store the weights and trees
    minHeap = new MinHeap()

    # Step 2: Iterate through each edge of the optimal MST
    for each edge in optimalMST.edges:
        # Remove the edge from the optimal MST
        tempMST = optimalMST.removeEdge(edge)

        # Step 3: Try adding each other edge in the graph
        for each otherEdge in graph.edges:
            if otherEdge not in optimalMST:
                # Add the edge to the temporary MST
                newMST = tempMST.addEdge(otherEdge)

                # Check if the new MST is a valid tree
                if isValidTree(newMST, graph.nodes):
                    # Calculate the weight of the new MST
                    weight = calculateWeight(newMST)

                    # Add the new MST and its weight to the min heap
                    minHeap.add((weight, newMST))

    # Step 4: The top of the heap now contains the next best MST
    # (after removing the optimal MST, which is the first element)
    minHeap.pop() # Remove the optimal MST
    nextBestMST = minHeap.pop() # Get the next best MST

    return nextBestMST

- **3c.**
This algorithm would be asymptotically dominated by Prim's algorithm which has work of O(|E| log |E|). This is because the swaps would be done in constant time.
