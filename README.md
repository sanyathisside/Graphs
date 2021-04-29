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

<hr/>

## Traversal Techniques:
  1. <a href="https://github.com/sanya2508/Graphs/blob/main/c.%20Breadth-First%20Traversal.cpp">Breadth-First Search (BFS): </a>
      * BFS is traversing the adjacent nodes at first, and after that moving on  to next nodes.
        1. At first we have to take a visited array, and every thing will be marked as zero which means none of the nodes has been visited yet.
        2. Run a for loop so that it calls bfs for every component of the graph.
        3. Now, we take a queue, insert the first node into it, and mark it as visited in the visited array.
        4. Now, iterate till the queue is not empty.
        5. Take the topmost element of the queue, and remove that element from the queue.
        6. Take the adjacent nodes of the node that we popped from the queue, and insert those nodes into the queue (only if not visited). Mark visited for those nodes as well.
        7. Continue this till we get all the adjacent nodes, for all nodes. (The queue is empty).
      * Complexity:
        * Time complexity: O(N+E) -> N is time taken for visiting N nodes, and E is for travelling through adjacent nodes overall.
        * Space complexity: O(N+E) + O(N) + O(N) -> Space for adjacency list, visited array, and queue.
        
    
   2. <a href="https://github.com/sanya2508/Graphs/blob/main/d.%20Depth-First%20Search%20Traversal.cpp">Depth-First Search:</a>
       * DFS is traversing the graph in depthward motion. It is a recursive function.
         1. Create a visited array of size V+1. Mark all the indexes as zero.
         2. Run a for loop so that it calls bfs for every component of the graph.
         3. Take the first node, mark it as visited.
         4. Make a recursive call to its adjacent nodes, and mark those nodes as visited.
         5. Continue this recurvise call till there is no further recursive dfs calls that will be made.
         6. Come back, and make recursive calls for other adjacent nodes.
       * Complexity:
         * Time complexity: O(N+E) -> N is time taken for visiting N nodes, and E is for travelling through adjacent nodes overall.
         * Space complexity: O(N+E) + O(N) + O(N) -> Space for adjacency list, visited array, and auxiliary space.

<hr/>

## Cycle detection in undirected graph:
  * <a href="https://github.com/sanya2508/Graphs/blob/main/e.%20Cycle%20detection%20in%20Undirected%20Graph%20using%20bfs.cpp">Usign BFS: </a>
     * If any of the adjacent node has been visited previously, then we can say that there is a cycle.
     1. Create a visited array of size V+1. Mark all the indexes as zero.
     2. Run a for loop so that it calls bfs for every component of the graph.
     3. In the normal bfs we did just put the node in the queue, but here we will modify it. 
     4. Here we are going to put the node, as well as their previous/parent node in the queue.
     5. Take the previous/parent node for the starting node as -1.
     6. Mark the node as visited after putting it into the queue.
     7. Take every node from the queue and check if it's already been visited (not including the parent node).
     8. If we get any node that's already been visited, then we can return true (cycle is present), else cycle is not present.
     * Complexity:
        * Time complexity: O(N+E) -> N is time taken for visiting N nodes, and E is for travelling through adjacent nodes overall.
        * Space complexity: O(N+E) + O(N) + O(N) -> Space for adjacency list, visited array, and queue.


  * <a href="https://github.com/sanya2508/Graphs/blob/main/f.%20Cycle%20detection%20in%20Undirected%20Graph%20using%20dfs.cpp">Using DFS: </a>
     * While traversing in a depth order fashion, if any of the node has been visited previously, then we can say that there is a cycle.
     1. Create a visited array of size V+1. Mark all the indexes as zero.
     2. Run a for loop so that it calls bfs for every component of the graph.
     3. In the normal dfs we did just take the node and do a recursive dfs call. 
     4. Here we are going to take the node, as well as their previous/parent node for making recursive call.
     5. Take the previous/parent node for the starting node as -1.
     6. Make a recursive call to its adjacent nodes, and mark those nodes as visited.
     7. If we get any adjacent node, that's already been visited (not including the parent node), return true (cycle present), else if there are no further recursion calls, return false (cycle not present).


<hr/>

## Bipartite graphs:
  * A graph that can be coloured using exactly two colors such that no two adjacent nodes have same color.
     * Observation: 
       * Any graph that has an odd length cycle cannot be a bipartite.
       * Any graph that doesn't have an odd length cycle can be a bipartite graph (graph with even length cycle, or graph with no cycle).
     * ### <a href="https://github.com/sanya2508/Graphs/blob/main/g.%20Bipartite%20Graph%20bfs.cpp">Using BFS: </a>
       1. Create a color array of size V+1. Mark all the indexes as -1. Take two colours (0 and 1).
       2. Now, we take a queue, insert the first node into it, and color it with color 1.
       3. Take the adjacent node, put that node in the queue, and color it with exact opposite color (0).
       4. Continue this for further adjacent nodes.
       5. Also keep checking the color of adjacent nodes for each node.
       6. If we come across a situation where two adjacent nodes have same color, we will return false (graph is not bipartite), else return true.
       * Complexity:
         * Time complexity: O(N+E) -> N is time taken for visiting N nodes, and E is for travelling through adjacent nodes overall.
         * Space complexity: O(N+E) + O(N) + O(N) -> Space for adjacency list, visited array, and queue.
     * ### <a href="https://github.com/sanya2508/Graphs/blob/main/h.%20Bipartite%20Graph%20dfs.cpp">Using DFS: </a>
       1. Create a color array of size V+1. Mark all the indexes as -1. Take two colours (0 and 1).
       2. Mark the color for the first node (1) and do a recursive call for the adjacent node.
       3. Mark the adjacent node with exactly opposite color, and continue the recursive call for the next adjacent nodes.
       4. Also keep checking the color of adjacent nodes for each node.
       5. If we come across a situation where two adjacent nodes have same color, we will return false (graph is not bipartite), else return true.
       * Complexity:
         * Time complexity: O(N+E) -> N is time taken for visiting N nodes, and E is for travelling through adjacent nodes overall.
         * Space complexity: O(N+E) + O(N) + O(N) -> Space for adjacency list, visited array, and auxiliary space.

<hr/>


## Cycle detection in directed graph:
   1. <a href="https://github.com/sanya2508/Graphs/blob/main/i.%20Cycle%20Detection%20in%20Directed%20Graph%20using%20DFS.cpp">Using DFS: </a>
     * We will have to use a self dfs along with visited  dfs in case of directed graph.
     1. We need to create two visited arrays.
          1. Visited, and
          2. Dfs visited. (To keep a track if a node was visited in the same dfs call or not).
     2. We take the initial value of node and check if that is unvisited. If that is unvisited we call the cycleCheck for that node.
     3. Whenever cycleCheck of a node is called, we mark the visited and dfs visited array for that node as visited.
     4. Now we call the cycleCheck for the adjacent node. (Also, mark visited in both arrays).
     5. We do recurvise calls on the adjacent and next adjacent nodes.
     6. Once we reach to a point where there is no further adjacent nodes that's not visited, there will be no further recursion calls.
     7. We will try to go back.
     8. Whenever a recursion call for a function or a dfs is over, we will take that value out of dfs visited array. (Because that dfs is over for that node).
     9. If while traversing, we find a node that has been visited in both the arrays, then only we can say that cycle is present in the graph.
     * Complexity:
         * Time complexity: O(N+E) -> N is time taken for visiting N nodes, and E is for travelling through adjacent nodes overall.
         * Space complexity: O(N+E) + O(2N) + O(N) -> Space for adjacency list, visited and dfs visited array, and auxiliary space.
   
   2. <a href="https://github.com/sanya2508/Graphs/blob/main/l.%20Cycle%20Detection%20in%20Directed%20Graph%20using%20BFS.cpp">Using BFS (Kahn's Algorithm): </a>
      * Kahn's algorithm is finding topological sort, and topological sort is only possible for directed acylic graph.
      * So, if a graph has cycle, then topological sort won't be possible.
      * Here we will use the reverse logic of topological sort.
      * We will try to generate topological sort, and if we are unable to generate then we can conclude that it's a cyclic graph.


<hr/>

## Topological Sorting:
  * It is defined as a linear ordering of vertices such that if there is an edge u->v, then u appears before v in that ordering.
  * There can be multiple topological sorting for a given graph.
  * It is possible only for directed acylic graph.
  1. <a href="https://github.com/sanya2508/Graphs/blob/main/j.%20Topological%20Sort%20(DFS).cpp">Using DFS: </a>
      1. We need to run a for loop for all the nodes.
      2. If any node in the for loop is unvisited, then we will call the dfs for that node.
      3. We also need to carry a data strucuture (stack), and a visited array (initially marked 0).
      4. Whenever all the adjacent nodes have been visited for the current node, (that means dfs for that node is over), then we will put that node into the stack.
      5. Once the for loop is over, the stack will be the desired output of topological sort.
      * Complexity:
         * Time complexity: O(N+E) -> N is time taken for visiting N nodes, and E is for travelling through adjacent nodes overall.
         * Space complexity: O(N+E) + O(2N) + O(N) -> Space for adjacency list, visited array and stack, and auxiliary space.
   2. <a href="https://github.com/sanya2508/Graphs/blob/main/k.%20Topological%20Sort%20(BFS).cpp">Using BFS (Kahn's Algorithm) :</a>
      1. BFS algorithm will be requiring two things.
         1. Indegree array, marked 0 at the beginning. (Indegree: Number of incoming edges).
         2. A queue.
      2. Find out indegree for all the nodes.
      3. Traverse through the indegree array, and push the nodes with 0 indegrees in the queue.
      4. Apply bfs for the elements in queue.
      5. For each element in the queue, check out the adjacent nodes.
      6. Print that element.
      7. Go to the adjacent nodes of the element taken in the indegree array, and reduce the indegree for those nodes by 1.
      8. Anytime the indegree of any node becomes 0, we will push that node in the queue.
      9. Continue this till the queue gets empty.
      * Complexity:
         * Time complexity: O(N+E) -> N is time taken for visiting N nodes, and E is for travelling through adjacent nodes overall.
         * Space complexity: O(N+E) + O(N) + O(N) -> Space for adjacency list, indegree array, and queue.

</hr>

    
