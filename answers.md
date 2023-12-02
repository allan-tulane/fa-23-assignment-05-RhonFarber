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


- **2b.**


- **2c.**

- **2d.**

- **2e.**



- **3a.**


- **3b.**


- **3c.**
