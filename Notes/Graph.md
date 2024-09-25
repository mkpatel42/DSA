# Table of Contents

1. [What is Graph?](#what-is-graph)
2. [Types of Graphs](#types-of-graphs)
    - [Undirected Graph](#undirected-graph)
    - [Directed Graph (Digraph)](#directed-graph-digraph)
    - [Cyclic and Acyclic Graphs](#cyclic-and-acyclic-graphs)
3. [Graph Representation](#graph-representation)
    - [1. Adjacency Matrix](#1-adjacency-matrix)
    - [2. Adjacency List](#2-adjacency-list)
4. [Graph Traversal](#graph-traversal)
    - [BFS](#bfs)
    - [DFS](#dfs)
5. [Cycle Detection in Undirected Graph](#cycle-detection-in-undirected-graph)
    - [Using BFS](#cycle-detection-in-undirected-graph-using-bfs)
    - [Using DFS](#cycle-detection-in-undirected-graph-using-dfs)
6. [Bipartite Graph](#bipartite-graph)
    - [Using BFS](#bipartite-graph-bfs)
    - [Using DFS](#bipartite-graph-dfs)
7. [Cycle Detection in Directed Graph Using DFS](#cycle-detection-in-directed-graph-using-dfs)
8. [Topological Sort Using DFS](#topological-sort-using-dfs)


## What is Graph?
![img_3.png](Assets/img_3.png)

A graph is a group of points (called vertices or nodes) that are connected by lines (called edges).

### Vertices (Nodes)
These are the individual points in the graph. They represent things like cities, people, or any entities.

### Edges
Edges are the lines that connect the vertices. They can be one-way (directed) or two-way (undirected).

## Types of Graphs

![img_1.png](Assets/img_1.png)

### Undirected Graph
- In this type of graph, the edges allow travel in both directions.
- For example, if there is a connection between nodes (u, v), it’s the same as the connection (v, u).

### Directed Graph (Digraph)
- Here, the edges have a direction, meaning you can only travel one way between nodes.
- For instance, the connection (u, v) is different from (v, u). We can consider that as one way road, there is a way to go from city u to city v. But you can't go back.

### Cyclic and Acyclic Graphs
![img_2.png](Assets/img_2.png)
- A **cyclic graph** contains loops or cycles, meaning you can return to a starting point.
- A **Directed Acyclic Graph (DAG)** is a directed graph that has no cycles.

## Structure of Graphs
- A graph may or may not contain cycles.
- Some graphs are open (like a line) while others are closed (like a circle).

## Path in a Graph
A path is a way to connect different nodes through edges, where each node can only appear once in that path.

## Degree of a Node

### Undirected Graphs
- The degree of a node is the number of edges connected to it.
- The total degree of the graph is twice the number of edges since each edge connects two nodes.

### Directed Graphs
- **Indegree**: The number of edges coming into a node.
- **Outdegree**: The number of edges going out from a node.

## Edge Weight
- Some edges have weights, which can represent costs or distances between nodes.
- If no weight is given, it is assumed to be 1 by default.

# Graph Representation

Graphs can be represented in various ways in Java. The two most common representations are:

## 1. Adjacency Matrix

An adjacency matrix is a 2D array used to represent a graph. The rows and columns represent the vertices, and the values in the matrix indicate whether there is an edge between the vertices.

### Example

```java
class Graph {
    private int[][] adjacencyMatrix;

    public Graph(int numberOfVertices) {
        adjacencyMatrix = new int[numberOfVertices][numberOfVertices];
    }

    public void addEdge(int source, int destination) {
        adjacencyMatrix[source][destination] = 1; // For directed graph
        // Uncomment the line below for undirected graph
        // adjacencyMatrix[destination][source] = 1; 
    }

    public void display() {
        for (int i = 0; i < adjacencyMatrix.length; i++) {
            for (int j = 0; j < adjacencyMatrix[i].length; j++) {
                System.out.print(adjacencyMatrix[i][j] + " ");
            }
            System.out.println();
        }
    }
}
```

### Key Points:
- Space Complexity: O(V^2)
- Adding an Edge: O(1)
- Removing an Edge: O(1)
- Checking if an Edge Exists: O(1)
- Iterating over All Edges: O(V^2)
- Efficient for dense graphs but uses more space

## 2. Adjacency List

An adjacency list uses a list to represent a graph. Each vertex has a list of adjacent vertices. This representation is more space-efficient for sparse graphs.

```Java
class Graph {
    private List<List<Integer>> adjacencyList;

    public Graph(int numberOfVertices) {
        adjacencyList = new ArrayList<>(numberOfVertices);
        for (int i = 0; i < numberOfVertices; i++) {
            adjacencyList.add(new ArrayList<>());
        }
    }

    public void addEdge(int source, int destination) {
        adjacencyList.get(source).add(destination); // For directed graph
        // Uncomment the line below for undirected graph
        // adjacencyList.get(destination).add(source);
    }

    public void display() {
        for (int i = 0; i < adjacencyList.size(); i++) {
            System.out.print("Vertex " + i + ": ");
            for (int neighbor : adjacencyList.get(i)) {
                System.out.print(neighbor + " ");
            }
            System.out.println();
        }
    }
}
```

### Key Points:
- Space Complexity: O(V + E)
- Adding an Edge: O(1)
- Removing an Edge: O(V)
- Checking if an Edge Exists: O(V)
- Iterating over All Edges: O(E)
- More space-efficient for sparse graphs

# Graph Traversal

## BFS
Breadth-First Search (BFS) is an algorithm for traversing or searching tree or graph data structures. It explores all the neighbor nodes at the present depth before moving on to nodes at the next depth level. BFS is commonly used to find the shortest path in unweighted graphs.

## Steps of BFS
1. **Initialize**:
    - Create a queue to keep track of the nodes to be explored.
    - Create a list or set to track visited nodes.

2. **Enqueue the Starting Node**:
    - Add the starting node (source) to the queue and mark it as visited.

3. **Dequeue a Node**:
    - Remove the node from the front of the queue.

4. **Process the Node**:
    - Perform the desired operation (e.g., print the node).

5. **Enqueue All Adjacent Nodes**:
    - For each unvisited adjacent node, mark it as visited and enqueue it.

6. **Repeat**:
    - Repeat steps 3-5 until the queue is empty.
    
```java
class Solution {
    public ArrayList<Integer> bfsOfGraph(int V,
                                         ArrayList<ArrayList<Integer>> adj) {

        ArrayList < Integer > bfs = new ArrayList < > ();
        boolean vis[] = new boolean[V];
        Queue < Integer > q = new LinkedList < > ();

        q.add(0);
        vis[0] = true;

        while (!q.isEmpty()) {
            Integer node = q.poll();
            bfs.add(node);

            // Get all adjacent vertices of the dequeued vertex s
            // If a adjacent has not been visited, then mark it
            // visited and enqueue it
            for (Integer it: adj.get(node)) {
                if (vis[it] == false) {
                    vis[it] = true;
                    q.add(it);
                }
            }
        }

        return bfs;
    }

    public static void main(String args[]) {

        ArrayList < ArrayList < Integer >> adj = new ArrayList < > ();
        for (int i = 0; i < 5; i++) {
            adj.add(new ArrayList < > ());
        }
        
        adj.get(4).add(0);
        adj.get(1).add(2);
        adj.get(2).add(1);
        adj.get(1).add(3);
        adj.get(3).add(1);
        adj.get(0).add(1);
        adj.get(1).add(0);
        adj.get(0).add(4);
      

        Solution sl = new Solution();
        ArrayList < Integer > ans = sl.bfsOfGraph(5, adj);
        int n = ans.size();
        for(int i = 0;i<n;i++) {
            System.out.print(ans.get(i)+" ");
        }
    }
}
```

### Key Points:
- Uses a queue for traversal
- Explores nodes level by level
- Time Complexity: O(V + E)
- Space Complexity: O(V)
- Useful for finding shortest path in unweighted graphs
- If we have more than one components in graph then we need to iterate all the vertices and if !visited then need to call *bfsFromVertex()*.

![img.png](Assets/img.png)

```
 for (int i = 0; i < V; i++) {
        if (!vis[i]) {  // Check if the node is unvisited
            bfsFromVertex(i, vis, adj, bfs); // Start BFS for each unvisited node
        }
}
```

## DFS

Depth-First Search (DFS) is an algorithm used to traverse or search through the nodes of a graph. Unlike BFS, which explores neighbors level by level, DFS explores as far down a branch as possible before backtracking. It is useful for exploring all possible paths in a graph and is often used in applications like maze solving, topological sorting, and cycle detection.

## Steps of DFS
1. **Initialize**:
    - Create a stack (or use recursion) to keep track of nodes to visit.
    - Create a list or array to track visited nodes.

2. **Start from a Node**:
    - Push the starting node onto the stack and mark it as visited.

3. **Explore the Graph**:
    - While there are nodes in the stack:
        - Pop a node from the stack.
        - Process the node (e.g., print it or check its edges).
        - Push all unvisited adjacent nodes onto the stack and mark them as visited.

4. **Backtrack**:
    - If there are no unvisited adjacent nodes, backtrack to the previous node by popping from the stack.

5. **Repeat**:
    - Continue until all nodes in the connected component are visited.

### Key Points:
- Uses recursion or a stack for traversal
- Explores as far as possible along each branch before backtracking
- Time Complexity: O(V + E)
- Space Complexity: O(V)
- Useful for topological sorting and cycle detection

```java
import java.util.ArrayList;
import java.util.Stack;

class Solution {
    public ArrayList<Integer> dfsOfGraph(int V, ArrayList<ArrayList<Integer>> adj) {
        ArrayList<Integer> dfs = new ArrayList<>();
        boolean[] vis = new boolean[V];

        for (int i = 0; i < V; i++) {
            if (!vis[i]) {  // Check if the node is unvisited
                dfsFromVertex(i, vis, adj, dfs); // Start DFS for each unvisited node
            }
        }

        return dfs;
    }

    private void dfsFromVertex(int node, boolean[] vis, ArrayList<ArrayList<Integer>> adj, ArrayList<Integer> dfs) {
        vis[node] = true; // Mark the node as visited
        dfs.add(node); // Process the node

        // Explore all adjacent vertices
        for (Integer neighbor : adj.get(node)) {
            if (!vis[neighbor]) { // If the neighbor has not been visited
                dfsFromVertex(neighbor, vis, adj, dfs); // Recursively call DFS for the neighbor
            }
        }
    }

    public static void main(String args[]) {
        ArrayList<ArrayList<Integer>> adj = new ArrayList<>();
        for (int i = 0; i < 5; i++) {
            adj.add(new ArrayList<>());
        }

        // Constructing the graph
        adj.get(0).add(1);
        adj.get(1).add(0);
        adj.get(1).add(2);
        adj.get(2).add(1);
        adj.get(1).add(3);
        adj.get(3).add(1);
        adj.get(4).add(0);

        Solution sl = new Solution();
        ArrayList<Integer> ans = sl.dfsOfGraph(5, adj);
        for (int node : ans) {
            System.out.print(node + " ");
        }
    }
}
```

## Cycle Detection in Undirected Graph using BFS
**Hint:** Do BFS, If from a node 'u', you visited node 'v' & if 'v' is already visited and also if 'v' is not parent of 'u' then we can say cycle is there.

![img_4.png](Assets/img_4.png)

```Java
class Solution {
    boolean checkForCycle(ArrayList<ArrayList<Integer>> adj, int s,
                          boolean vis[]) {
        Queue<Node> q = new LinkedList<>(); //BFS
        q.add(new Node(s, -1));
        vis[s] = true;

        // until the queue is empty
        while (!q.isEmpty()) {
            // source node and its parent node
            int node = q.peek().first;
            int par = q.peek().second;
            q.remove();

            // go to all the adjacent nodes
            for (Integer it : adj.get(node)) {
                if (vis[it] == false) {
                    q.add(new Node(it, node));
                    vis[it] = true;
                }

                // if adjacent node is visited and is not its own parent node
                else if (par != it) return true;
            }
        }

        return false;
    }
}
```
### Key Points:
- Checks if a visited node is not the parent of the current node
- Time Complexity: O(V + E)
- Space Complexity: O(V)

## Cycle Detection in Undirected Graph using DFS

**Hint:** If adjacent node (next node) is already visited then cycle is present

In DFS call we will pass parent and we will check one more condition 

**else if (par != it) return true;**

```Java
class Solution {
    public boolean checkForCycle(int node, int parent, boolean vis[], ArrayList<ArrayList
            <Integer>> adj) {
        vis[node] = true;
        for (Integer it : adj.get(node)) {
            if (vis[it] == false) {
                if (checkForCycle(it, node, vis, adj) == true)
                    return true;
            } else if (it != parent)
                return true;
        }

        return false;
    }

    // 0-based index
    public boolean isCycle(int V, ArrayList < ArrayList < Integer >> adj) {
        boolean vis[] = new boolean[V];
        for (int i = 0; i < V; i++) {
            if (vis[i] == false) {
                if (checkForCycle(i, -1, vis, adj))
                    return true;
            }
        }
        return false;
    }
}
```
### Key Points:
- Checks if a visited node is not the parent of the current node
- Time Complexity: O(V + E)
- Space Complexity: O(V)

## Bipartite Graph (BFS) | Graph Coloring:

A Graph that can be colored using 2 colors such that no two adjacent nodes have same color is called as Bipartite Graph

- Use BFS to traverse the graph, coloring nodes alternately with two colors.
- For each node, color all its uncolored neighbors with the opposite color.
- If you encounter an already-colored neighbor with the same color as the current node, the graph is not bipartite.

```Java
class Solution {
    public boolean isBipartite(int[][] graph) {
        int[] visited = new int[graph.length];
        for(int i=0; i< graph.length;i++){
            if(visited[i]==0 && !helper(graph,i,1,visited)){
                return false;
            }
        }
        return true;
    }

    public boolean helper(int[][] graph, int n, int color, int[] visited) {

        Queue<Integer> queue = new LinkedList<>();

        queue.add(n);
        visited[n] = color;
        while(!queue.isEmpty()){
            int size = queue.size();
            System.out.println(size);
            while(size>0){
                int node = queue.remove();
                int nearestColor = visited[node];
                for(int i=0; i< graph[node].length;i++){
                    int nextNode = graph[node][i];
                    if(visited[nextNode] == 0){
                        visited[nextNode] = -nearestColor;
                        queue.add(nextNode);
                    }else{
                        if(visited[nextNode]== nearestColor){
                            return false;
                        }
                    }
                }
                size--;
            }
        }

        return true;
    }
}
```

## Bipartite Graph (DFS)

- Use BFS to traverse the graph, coloring nodes alternately with two colors.
- For each node, color all its uncolored neighbors with the opposite color.
- If you encounter an already-colored neighbor with the same color as the current node, the graph is not bipartite.

```Java
class Solution {
    public boolean isBipartite(int[][] graph) {
        int[] visited = new int[graph.length];
        for(int i=0; i< graph.length;i++){
            if(visited[i]==0 && !helper(graph,i,1,visited)){
                return false;
            }
        }
        return true;
    }

    public boolean helper(int[][] graph, int i, int color, int[] visited) {
        if(visited[i]!= 0){
            if(visited[i]!= color){
                return false;
            }
            return true;
        }

        visited[i] = color;
        for(int node: graph[i]){
            if(!helper(graph, node, -color, visited)){
                    return false;
            }
        }
        return true;
    }
}
```

## Cycle Detection in Directed Graph Using DFS
```
3 ---> 4    3 -------4
|      |    |        |
|      |    |        |
V      V    |        |
6 ---> 5    6--------5
No Cycle      Cycle
```

So, we can't use idea of cycle detection of undirected graph

**Hint:**
- **Initialize Structures:** Create two sets—one for tracking visited nodes and another for nodes currently in the path (recursion stack).

- **DFS Traversal:** Start a DFS traversal from each unvisited node. For each node you visit, add it to the current path set.

- **Cycle Detection:** While exploring a node’s neighbors, if you encounter a node that is already in the current path set, a cycle is detected.

- **Backtracking:** After exploring all neighbors of a node, remove it from the current path set before backtracking to the previous node.

```Java
class solution{
    private static boolean checkCycle(int node,  ArrayList<ArrayList<Integer>> adj, int vis[], int dfsVis[]) {
        vis[node] = 1;
        dfsVis[node] = 1;

        for(Integer neighbor: adj.get(node)) {
            if(vis[neighbor] == 0) {
                if(checkCycle(neighbor, adj, vis, dfsVis) == true) {
                    return true;
                }
            } else if(dfsVis[neighbor] == 1) {
                return true;
            }
        }
        dfsVis[node] = 0;
        return false;
    }
}
```

### Key Points:
- Uses two arrays: one for visited nodes and one for nodes in the current path
- remove current path in backtracking
- Time Complexity: O(V + E)
- Space Complexity: O(V)

## Topological sort using DFS
Topological sorting is linear ordering of vertices such that if there is an edge u -> v then u appears before v in that ordering


## Example
Imagine you are managing a software development project with several tasks that need to be completed in a specific order. Some tasks depend on the completion of others before they can start.

### Tasks:
- **Task A**: Requirements Gathering
- **Task B**: Design
- **Task C**: Implementation
- **Task D**: Testing
- **Task E**: Deployment

### Dependencies:
- Task A must be completed before Task B can start.
- Task A must be completed before Task C can start.
- Task B must be completed before Task D can start.
- Task C must be completed before Task D can start.
- Task D must be completed before Task E can start.

![Description](Assets/graphviz.svg)

For above image, One of the possible topological sort: 5, 4, 2, 3, 1, 0 (edge will be left to right)

**Topological Sort is possible for only DAG**

**Hint:**
- Maintain visited array & a satck to store the topological sort
- If adjacent of the node are done then push the node into stack (means we already have adjacent nodes into stack)

```Java
class Solution{
    static void findTopoSort(int node, int vis[], ArrayList<ArrayList<Integer>> adj, Stack<Integer> st) {
        vis[node] = 1;
        for(Integer it: adj.get(node)) {
            if(vis[it] == 0) {
                findTopoSort(it, vis, adj, st);
            }
        }
        st.push(node);
    }
    static int[] topoSort(int N, ArrayList<ArrayList<Integer>> adj) {
        Stack<Integer> st = new Stack<Integer>();
        int vis[] = new int[N];

        for(int i = 0;i<N;i++) {
            if(vis[i] == 0) {
                findTopoSort(i, vis, adj, st);
            }
        }

        int topo[] = new int[N];
        int ind = 0;
        while(!st.isEmpty()) {
            topo[ind++] = st.pop();
        }
        // for(int i = 0;i<N;i++) System.out.println(topo[i] + " "); 
        return topo;
    }
}
```
### Key Points:
- Works only on Directed Acyclic Graphs (DAGs)
- Uses a stack to store nodes after exploring all neighbors
- Time Complexity: O(V + E)
- Space Complexity: O(V)

## Topological sort using BFS | Kahn's Algo
***Hint:**
- Node will lesser indegree will come before greater indegree

### Steps:

1. Calculate in-degree (number of incoming edges) for each vertex and store it in an array.

2. Create a queue and add all vertices with in-degree 0 to it.

3. Initialize an empty list to store the topological order.

4. While the queue is not empty:
    - Remove a vertex from the queue (dequeue)
    - Add it to the topological order list
    - Reduce in-degree by 1 for all its neighboring vertices
    - If in-degree of a neighboring vertex becomes 0, add it to the queue

5. If the topological order list contains all vertices, return it. Otherwise, the graph has at least one cycle.

```Java
class Solution {
    // Function to return list containing vertices in Topological order.
    static int[] topoSort(int V, ArrayList<ArrayList<Integer>> adj) {
        int indegree[] = new int[V];
        for (int i = 0; i < V; i++) {
            for (int it : adj.get(i)) {
                indegree[it]++;
            }
        }

        Queue<Integer> q = new LinkedList<Integer>();
        ;
        for (int i = 0; i < V; i++) {
            if (indegree[i] == 0) {
                q.add(i);
            }
        }

        int topo[] = new int[V];
        int i = 0;
        while (!q.isEmpty()) {
            int node = q.peek();
            q.remove();
            topo[i++] = node;
            // node is in your topo sort
            // so please remove it from the indegree

            for (int it : adj.get(node)) {
                indegree[it]--;
                if (indegree[it] == 0) {
                    q.add(it);
                }
            }
        }

        return topo;
    }
}

```
### Key Points:
- Works only for Directed Acyclic Graphs (DAGs)
- Detects cycles in the graph
- Time Complexity: O(V + E), where V is the number of vertices and E is the number of edges
- Space Complexity: O(V)

## Shortest Path in weighted DAG
**Given a source node, find shortest path length from src to every other node**
