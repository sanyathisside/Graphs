# Graphs

## Introduction: 

* Graph is a data structure which has two components:
   1. Node/Vertex
   2. Edge (which connects two nodes)
* Types of graph:
   1. Directed Graph
   2. Undirected Graph
* Degree in a graph:
   * The number of edges that are incoming or outgoing in a graph.
   * In an undirected graph there are degerees.
       * Total degree of all the nodes = 2*edges. 
   * In a directed graph there are:
       1. Indegree (Incoming edge)
       2. Outdegree (Outgoing edge)
 * Path:
   * Path is a sequence of nodes or vertex such that none of the nodes are repeating or visited more than once.
 * Cyclic graph:
    * If there is a cycle in an undirected graph we can call that as an undirected cyclic graph.
      * Undirected acylic graph: Tree/no cycle.  
    * If there is a cycle in a directed graph we can call that as a directed cyclic graph.
      * Directed acyclic graph: No cycle.
 * Weighted graph:
    * Weighted directed graph.
    * Weighted undirected graph. 

<hr/>

## Graph representation in C++:
 1. <a href="https://github.com/sanya2508/Graphs/blob/main/a.%20Adjacency%20matrix%20representation.cpp">Adjacency matrix: </a>
    1. Find out the number of nodes.
    2. Check if it is one based indexing or zero based indexing.
       * If it is one based indexing we create 6*6 2D array.
    3. Fill the 2D array with zeroes.
    4. Iterate over all the edges and mark 1 whenever there is an edge present for that node. (adj[u][v] =1)
       * If the graph is undirected, mark the reverse edge 1 as well. (adj[u][v] =1) and (adj[v][u] =1) 
    * Disadvantages of using this method:
      1. We can only use adjacency matrix for smaller values of n.
    * Space complexity: O(n*n)
  
  2. <a href="https://github.com/sanya2508/Graphs/blob/main/b.%20Adjacency%20List%20Representation.cpp">Adjacency List: </a>
    1. If it's an undirected or directed graph, we are going to have vector<int> of an adjaceny array of size (n+1).
       * For directed:
          ```
          adj[u].push_back(v);
          ```
          
       * For undirected: 
          ```
          adj[u].push_back(v);
          adj[v].push_back(u);
          ```
          
   2. Then we can store adjacent nodes at each index for all the index in their respective vector. 
    * Space complexity: 
      * Undirected: O(N+2E)
      * Directed: O(N+E)
    * If there is an edge weight as well, then we can convert the vector into pair <int, int> instead of int.


<hr/>

## Connected components in a graph:
 * A graph can either be a connected graph, or disconnected graph.
 * In general, whatever code we write, we have to write for multiple components.
