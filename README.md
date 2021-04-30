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

<hr/>


## <a href="https://github.com/sanya2508/Graphs/blob/main/m.%20Shortest%20Path%20in%20Undirected%20Graph%20with%20Unit%20Weights%20(BFS).cpp">Shortest Path in Undirected Graph with Unit Weights: </a>
   * We need to find the shortest distance to every node, from the given source.
   * We can solve this using bfs and doing some modifications to it.
   1. We will take a distance array of size similar to the number of nodes, and mark each as infinity.
   2. Now we will take a queue that is always going to store the nodes.
   3. Put the source node into the queue, and mark its distance as zero.
   4. Take the source node out, and check its adjacent nodes.
   5. Take the adjacent nodes of the node and mark their distace as 1.
   6. Put those adjacent nodes into the queue.
   7. Take the nodes from queue one by one.
   8. For each node check their adjacent nodes.
   9. For each adjacent node, to get the distance of that adjacent node add a distance of 1 to the distance of the node from source node, and also compare it to the already assigned distance. Take the minimum of both.
   10. Conitinue this till the queue gets empty.
   * Complexity:
       * Time complexity: O(N+E) -> N is time taken for visiting N nodes, and E is for travelling through adjacent nodes overall.
       * Space complexity: O(N+E) + O(N) + O(N) -> Space for adjacency list, distance array, and queue.


<hr/>

## <a href="https://github.com/sanya2508/Graphs/blob/main/n.%20Shortest%20Path%20in%20weighted%20Directed%20Acyclic%20Graph%20(DAG).cpp">Shortest Path in weighted Directed Acyclic Graph:</a>
  * Given a source, we need to find the shortest distance for every other node from source.
  * We will find the topological sort and then it will be a simple comparison algorithm on bfs.
  1. Since it's a weighted graph, we need to store the node in pairs (node and weight).
  2. We will need a stack, a visited array, and a distance array.
  3. Mark every node as unvisited in visited array.
  4. Mark every node as infinity in distance array.
  5. Take the source node, mark it as visited.
  6. Do a recursion call to its adjacent nodes one by one for all the adjacent nodes. There will be no calls made for the node that's already been visited.
  7. Keep marking the nodes as visited whenver a call is being made to that node. 
  8. When we reach to a point where there is no further recursion calls, take the end node(the node from which we are returning back, similar thing we did in dfs topological sort) and put it into the stack.
  9. We will get the topological sort in the stack.
  10. Make the distance of source element as zero in the distance array.
  11. Take the first element out of the stack.
  12. Check the distance of first element (it should not be infinity).
  13. Take the adjacent nodes one by one for that element and add the distance of that adjacent node to the distance of the element, and also compare it to the already assigned distance.
  14. Take the minimum of both.
  15. Continue this for all the nodes (in the stack) till the stack gets empty.
  * Complexity:
       * Time complexity: O(2(N+E)) -> N is time taken for visiting N nodes, and E is for travelling through adjacent nodes overall. We are traversing twice.
       * Space complexity: O(N+E) + O(N) + O(N) + O(N/0) -> Space for stack, distance array, and (auxiliary space, depends if we are using dfs or bfs for topological sort).

<hr/>

## <a href="https://github.com/sanya2508/Graphs/blob/main/o.%20Shortest%20Path%20in%20Undirected%20Graphs%20(Dijkstra's%20Algorithm).cpp">Shortest Path in Undirected Graphs (Dijkstra's Algorithm):</a>
   1. We will have a priority queue (that will store distance, node).
   2. Priority queue should be a min heap, so that the element with the lower distance should always be on top of priority queue.
   3. We will also be having a distance array of the size of nodes+1, initially marked as infinity.
   4. Take the first node out of queue and mark its distance as zero.
   5. Insert the distance of that node, and the node in the priority queue. 
   6. Now start iterating the graph similar to bfs.
   7. Take the adjacent nodes of that element one by one, and add the distance of that adjacent node to the distance of the element, and also compare it to the already assigned distance.
   8. Put the node and distance in the priority queue.
   9. Take the first element from the priority queue. (It will be storing the element with lower distant on top).
   10. Take the adjacent nodes, and repeat the above process. (7,8,9)
   11. Continue this till the priority queue becomes empty.
   * Complexity:
      * Time complexity: O((N+E)logN) -> N is time taken for visiting N nodes, and E is for travelling through adjacent nodes overall. Log N is for priority queue.
      * Space complexity: O(N+E) + O(N) + O(N)  

<hr/>

## Minimum spanning tree: 
   * Whenever we can draw a tree from a given graph such that the tree has all the N nodes, and the number of edges is N-1 such that every node can be reachable from every other node, that's when we call it a minimum spanning tree.
   * The minimum refers to the spanning tree with the minimum weight amongst all the other spanning trees that can be formed from a graph.
   * This can be find using two different algorithms:
      1. Prim's Algorithm
      2. Kruskal's Algorithm 
   * ### Prim's Algorithm for Minimum Spanning Tree:
      * Intuition: 
        1. Start with the first node, and find the minimum weighted edge attached to this node.
        2. Take that edge, and the node connected to that edge.
        3. Check out all the adjacent edges among both the nodes which one is the minimal.
        4. Take the minimal edge along with the node.
        5. Now continue the same for all the three nodes. Find the adjacent node with the minimal edge weight.
        6. Do this until all the nodes are covered.
        7. The tree that we will get would be the MST.
      * #### <a href="https://github.com/sanya2508/Graphs/blob/main/p.1.%20Prim's%20Algorithm%20(Brute%20Force).cpp">Implementation (Brute Force): </a>
        1. We will be requiring three different arrays.
           1. Key array of size N (everything initialized to infinity in the beginning apart from the zero index).
           2. MST array (everything initialized to false in the beginning).
           3. Parent array (everythin initialized to -1 in the beginning).
        2. Find out the node with the minimum possible key value that is not the part of the mst and take that node.
        3. Mark the node as true in mst array.
        4. Check out all the adjacent nodes of that node.
        5. For each adjacent node of that node, mark the edge weight for that adjacent node as the weight in the key array, and also mark its parent in the parent array.
        6. Take the next node from the key array with minimum value and not part of mst.
        7. Mark that node as true in the mst array.
        8. Again check for all the adjacent nodes (5,6,7), but don't consider the nodes that are marked true in mst array.
        9. If at any instance the weight of any adjacent node is already having a lesser weight, then don't change the weight for that node.
        10. Continue this till all the nodes in mst becomes true.
        11. Iterate the parent array and form the tree.
        12. The tree that we will get would be the MST.
         * Complexity:
            * Time complexity: O(>N^2)
            * Space complexity: O(N+E) + O(3N)
      * #### <a href="https://github.com/sanya2508/Graphs/blob/main/p.2.%20Prim's%20Algorithm%20(Efficient).cpp">Implementation (Efficient approach): </a>
        1. We can use priority queue that will give us the minimal value from the key array.
        2. Do the modifications accordingly.
         * Complexity:
           * Time complexity: O(N+E+NlogN)
           * Space complexity: O(N+E) + O(4N)
   * ### <a href="https://github.com/sanya2508/Graphs/blob/main/q.%20Kruskal's%20Algorithm.cpp">Kruskal's Algorithm (Using Disjoint Set): </a>
     1. We are not going to store the graph in adjacency list. We will store it in a simple linear data strucutre.
     2. Sort all the edges according to weight.
     3. Greedily pick up the shortest edge.
     4. Check if both the nodes of that edge belong to same component or not (using disjoint set).
     5. If not take that edge.
     6. Next, again greedily pick up the next shortest edge. Then 4,5.
     7. If there comes a case where two nodes of an edge belongs to the same component we will not take that edge.
     8. Do this for all the edges.
     9. Once all the edges are covered, the resulting tree will be our minimum spanning tree.
     * Complexity: (for M edges)
       * Time complexity: O(MlogM) + O(M*4α) ≈ O(MlogM) -> Sort the edges, iterating over the edges and checking if they belong to same component or not.
       * Space complexity: O(3M) + O(N) + O(N) -> For storing edges, parent and rank array for implementation of disjoint set.

<hr/>


## Disjoint Set | Union By Rank and Path Compression:
   * ### Disjoint Set data strucuture:
      * This data structure is going to provide us with two different operations:
        1. findParent()
        2. Union() 
      1. Assume there are 7 nodes and each node belongs to different component.
      2. Every one is its parent itself.
      3. Now, if we need to find the parent of any node then we will get the same node only.
      4. Now, Union(1,2)-> which means combine them in a single component.
      5. After combining, let's assume one node as the parent for both.
      6. Now, do Union(2,3)-> hence 3 nodes in a single component.
      7. Again, let's assume 1 as the parent of all three.
      8. Now, Union(4,5) -> Parent:4.
      9. Now, Union(6,7) -> Parent:6.
      10. Now, Union(5,6) -> Parent:4.
      11. If two nodes has same parent, then they belong to one component.
      12. Now, Union(3,7) -> Parent:1.
      * So, the efficient implementation of disjoint set is done by union by rank, and path compression.
        * So, we make sure that there is a parent array, and every node has itself as the parent when we start.
        * We also maintain another array (rank array), which is going to store the rank of all these nodes.
        * Make initial rank of all the nodes as zero.
        * Start doing the union operation.
        * For the first two nodes, make any of them as the parent (since rank for both the nodes are zero).
        * Whenever we are attaching two similar rank nodes, we need to make sure that the node to whom we are attaching, we need to increase it's rank by 1.
        * Take the next union, compare ranks, and the one with higher rank will be the parent for that node.
        * Do path compression whenever required.
      * Complexity:
        * Time complexity: O(4α) ≈ O(4) -> If there are m operations we are doing m time as every union operation is done in constant time (4α is mathematically proved).
        * Space complexity: O(2N) -> Rank array, and parent array.
