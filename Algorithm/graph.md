Graph representation:

- Adjacency Matrix
  - good for dense graph

- Adjacency List
  - good for sparse graph

adjacency list 可以用HashMap<Node, Set<Node>>



## 图里常用的search算法

### 1. Breadth-first-search

**Data structure:** Maintain a FIFO queue, put all traversed nodes that haven't been expand

专业术语： **expend** parent node, and **generate** children nodes

如何描述graph算法

1. initial state
2. expand a node and  generate its neighbor nodes
3. termination condition

**how to deduplicate**

碰到graph的问题思考五个方面

datastructure, initial state, expand & generate rule, termination condition, deduplicate



### BFS 经典例题

1. level order traverse (分层打印）

2. Bipirate 

   use two state to represents 2 different state

   use bfs to traverse the graph and check whether there is  a conflict or not.

3. determinate whether a binary tree is a complete binary tree

   一旦遇到气泡，就不能遇见其他非气泡

   when we expand a node and generate the first null, after that, if any node in the queue can generate any not null children node, then return false





### 2. Best First Search (BFS-2)

经典算法 Dijkstra's Algorithm

Usage: find the shortest path cost from a single node to any other nodes in the graph

BFS1 use priority queue instead of queue is BFS2

Properties of dijsktra's algorithm

1. One node can be expand once and only once

2. One node can be generated more than once (cost can be reduced over time)
3. all the cost of the nodes that are expanded are non-decreasing
4. Time: O(E * log(V))
5. when node is popped out for expansion, its value is equal to the shortest distance from the start node.