### 1. Algorithms & Data Structures (C++): Minimum Spanning Cost

To find the minimum spanning tree (MST) of a graph, you can use algorithms like Prim's or Kruskal's. Here's an example implementation of Kruskal's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

struct Edge {
    int src, dest, weight;
};

class Graph {
    int V;
    vector<Edge> edges;

public:
    Graph(int V) : V(V) {}

    void addEdge(int src, int dest, int weight) {
        edges.push_back({src, dest, weight});
    }

    // Find function of Union-Find
    int find(vector<int>& parent, int i) {
        if (parent[i] == -1)
            return i;
        return find(parent, parent[i]);
    }

    // Union function of Union-Find
    void Union(vector<int>& parent, int x, int y) {
        int xset = find(parent, x);
        int yset = find(parent, y);
        parent[xset] = yset;
    }

    // Kruskal's algorithm to find MST
    void KruskalMST() {
        vector<Edge> result;
        int e = 0, i = 0;
        sort(edges.begin(), edges.end(), [](Edge a, Edge b) {
            return a.weight < b.weight;
        });
        vector<int> parent(V, -1);

        while (e < V - 1 && i < edges.size()) {
            Edge next_edge = edges[i++];
            int x = find(parent, next_edge.src);
            int y = find(parent, next_edge.dest);

            if (x != y) {
                result.push_back(next_edge);
                Union(parent, x, y);
                e++;
            }
        }

        cout << "Edges in the MST:" << endl;
        for (i = 0; i < result.size(); i++)
            cout << result[i].src << " - " << result[i].dest << " : " << result[i].weight << endl;
    }
};

int main() {
    int V = 4;  // Number of vertices
    Graph g(V);

    // Adding edges to the graph
    g.addEdge(0, 1, 10);
    g.addEdge(0, 2, 6);
    g.addEdge(0, 3, 5);
    g.addEdge(1, 3, 15);
    g.addEdge(2, 3, 4);

    // Find MST using Kruskal's algorithm
    g.KruskalMST();

    return 0;
}
```

This code demonstrates how to find the Minimum Spanning Tree of a graph using Kruskal's algorithm. You can modify the `main()` function to use your own graph or input method.

### 1. Algorithms & Data Structures (C++): Breadth First Search: PreOrder, InOrder, PostOrder

It seems like you might be mixing up terminologies from tree traversal and graph traversal. Breadth-First Search (BFS) is typically used for graph traversal, while PreOrder, InOrder, and PostOrder are used for tree traversal. However, if you're interested in performing BFS on a tree structure, it can be done as well.

Here's a brief explanation of each:

1. **Breadth-First Search (BFS)**: BFS is an algorithm used for traversing or searching tree or graph data structures. It starts at a chosen node (often called the 'source' node), explores all of its neighboring nodes at the present depth, and then moves to the nodes at the next depth level. It uses a queue data structure to keep track of nodes to visit.

2. **PreOrder Traversal**: In pre-order traversal, the nodes are recursively visited in this order: root, left, right. It's often used to create a copy of the tree.

3. **InOrder Traversal**: In in-order traversal, the nodes are recursively visited in this order: left, root, right. In binary search trees, an in-order traversal returns nodes in sorted order.

4. **PostOrder Traversal**: In post-order traversal, the nodes are recursively visited in this order: left, right, root. It's often used to delete the tree.

Would you like code examples for any of these algorithms in C++?

### 1. Algorithms & Data Structures (C++): Breadth First Search: Spanning Tree

In the realm of algorithms and data structures, breadth-first search (BFS) is a fundamental graph traversal algorithm used to explore a graph layer by layer. One of the applications of BFS is finding the spanning tree of a graph.

A spanning tree of a graph is a subgraph that is a tree which includes all the vertices of the original graph with the minimum possible number of edges. In other words, it's a connected, acyclic subgraph of the original graph that spans all the vertices.

Here's how you can implement BFS to find the spanning tree of a graph in C++:

```cpp
#include <iostream>
#include <queue>
#include <vector>
#include <unordered_set>

using namespace std;

class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V) {
        adj.resize(V);
    }

    void addEdge(int v, int w) {
        adj[v].push_back(w);
        adj[w].push_back(v); // For undirected graph
    }

    void BFS(int start) {
        vector<bool> visited(V, false);
        queue<int> q;

        visited[start] = true;
        q.push(start);

        while (!q.empty()) {
            int v = q.front();
            q.pop();
            cout << v << " ";

            for (int i : adj[v]) {
                if (!visited[i]) {
                    visited[i] = true;
                    q.push(i);
                }
            }
        }
    }
};

int main() {
    Graph g(6);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(2, 4);
    g.addEdge(2, 5);

    cout << "BFS Traversal starting from vertex 0: ";
    g.BFS(0);
    cout << endl;

    return 0;
}
```

In this code:

- We define a `Graph` class representing an undirected graph using an adjacency list.
- The `addEdge` function adds an edge between two vertices.
- The `BFS` function performs BFS traversal starting from a given vertex, printing out the vertices in the order they are visited.
- In the `main` function, we create a graph and add some edges to it. Then, we perform BFS starting from vertex 0.

This BFS traversal effectively constructs a spanning tree rooted at the chosen starting vertex.

### 1. Algorithms & Data Structures (C++): Graph - Add Vertex

Adding a vertex to a graph involves adding a new node to the graph structure and updating the adjacency list or matrix accordingly. Here's how you can do it in C++ using an adjacency list representation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    // Constructor
    Graph(int vertices) : V(vertices) {
        adj.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w);
        adj[w].push_back(v); // If the graph is undirected
    }

    // Function to add a vertex to the graph
    void addVertex() {
        V++;
        adj.resize(V);
    }

    // Function to print the adjacency list representation of the graph
    void printGraph() {
        for (int v = 0; v < V; ++v) {
            cout << "Adjacency list of vertex " << v << ":\n";
            cout << "head";
            for (auto x : adj[v])
                cout << " -> " << x;
            cout << endl;
        }
    }
};

int main() {
    Graph g(4); // Create a graph with 4 vertices

    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(1, 3);

    cout << "Original Graph:\n";
    g.printGraph();

    g.addVertex(); // Add a vertex

    cout << "\nGraph after adding a vertex:\n";
    g.printGraph();

    return 0;
}
```

In this code:

- The `Graph` class represents the graph using an adjacency list.
- The `addVertex()` method increases the number of vertices and resizes the adjacency list to accommodate the new vertex.
- `addEdge()` adds an edge between two vertices (for an undirected graph, it adds edges in both directions).
- `printGraph()` prints the adjacency list representation of the graph.

You can modify the `addEdge()` method if you're dealing with directed graphs or if you have a weighted graph.

### 1. Algorithms & Data Structures (C++): Graph + Tree Traversals

Sure, I'd be happy to give you an overview of graph and tree traversals in C++.

Let's start with trees:

### Tree Traversals

In trees, there are mainly three types of traversals:

1. **Inorder Traversal**: In an inorder traversal, the nodes are recursively visited in this order: left, root, right.

2. **Preorder Traversal**: In a preorder traversal, the nodes are recursively visited in this order: root, left, right.

3. **Postorder Traversal**: In a postorder traversal, the nodes are recursively visited in this order: left, right, root.

Here's a simple implementation of these traversals:

```cpp
#include <iostream>

using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;

    Node(int val) : data(val), left(nullptr), right(nullptr) {}
};

void inorderTraversal(Node* root) {
    if (root) {
        inorderTraversal(root->left);
        cout << root->data << " ";
        inorderTraversal(root->right);
    }
}

void preorderTraversal(Node* root) {
    if (root) {
        cout << root->data << " ";
        preorderTraversal(root->left);
        preorderTraversal(root->right);
    }
}

void postorderTraversal(Node* root) {
    if (root) {
        postorderTraversal(root->left);
        postorderTraversal(root->right);
        cout << root->data << " ";
    }
}

int main() {
    // Create a sample binary tree
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);

    cout << "Inorder Traversal: ";
    inorderTraversal(root);
    cout << endl;

    cout << "Preorder Traversal: ";
    preorderTraversal(root);
    cout << endl;

    cout << "Postorder Traversal: ";
    postorderTraversal(root);
    cout << endl;

    return 0;
}
```

### Graph Traversals

In graphs, traversal can be more complex depending on the type of graph and the algorithm used. The two most common traversal algorithms are:

1. **Depth-First Search (DFS)**: In DFS, you start from a source node and traverse as far as possible along each branch before backtracking. This traversal can be implemented recursively or using a stack.

2. **Breadth-First Search (BFS)**: In BFS, you explore all the neighboring nodes at the present depth before moving on to the nodes at the next level of depth. This traversal can be implemented using a queue.

Here's a basic example of both DFS and BFS traversal for an adjacency list representation of a graph:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <stack>

using namespace std;

class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list representation

public:
    Graph(int V) : V(V) {
        adj.resize(V);
    }

    void addEdge(int u, int v) {
        adj[u].push_back(v);
    }

    void DFS(int start) {
        vector<bool> visited(V, false);
        stack<int> stk;
        stk.push(start);
        visited[start] = true;

        cout << "DFS Traversal: ";
        while (!stk.empty()) {
            int curr = stk.top();
            stk.pop();
            cout << curr << " ";
            for (int neighbor : adj[curr]) {
                if (!visited[neighbor]) {
                    stk.push(neighbor);
                    visited[neighbor] = true;
                }
            }
        }
        cout << endl;
    }

    void BFS(int start) {
        vector<bool> visited(V, false);
        queue<int> que;
        que.push(start);
        visited[start] = true;

        cout << "BFS Traversal: ";
        while (!que.empty()) {
            int curr = que.front();
            que.pop();
            cout << curr << " ";
            for (int neighbor : adj[curr]) {
                if (!visited[neighbor]) {
                    que.push(neighbor);
                    visited[neighbor] = true;
                }
            }
        }
        cout << endl;
    }
};

int main() {
    Graph g(5); // Create a graph with 5 vertices

    // Add edges
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 4);

    g.DFS(0); // Start DFS from node 0
    g.BFS(0); // Start BFS from node 0

    return 0;
}
```

These are the basic implementations of tree and graph traversals in C++. You can expand and modify them according to your specific requirements or use more sophisticated data structures and algorithms for more complex scenarios.

### 1. Algorithms & Data Structures (C++): Backedge Detection

Backedge detection is a concept primarily associated with graph algorithms, particularly in the context of depth-first search (DFS) or breadth-first search (BFS). When traversing a graph, especially in DFS, it's crucial to identify backedges to detect cycles efficiently.

In DFS, a backedge is an edge that connects a vertex to one of its ancestors in the DFS tree. It signifies the presence of a cycle in the graph. Detecting these backedges is fundamental in many graph algorithms, such as cycle detection, topological sorting, and finding strongly connected components in directed graphs.

Here's how you can detect backedges in a graph using DFS in C++:

```cpp
#include <iostream>
#include <vector>
#include <stack>
using namespace std;

enum class State { UNDISCOVERED, DISCOVERED, PROCESSED };

void dfs(int node, const vector<vector<int>>& graph, vector<State>& state, vector<int>& parent, vector<int>& discoveryTime, vector<int>& finishTime, int& time, stack<int>& backEdges) {
    state[node] = State::DISCOVERED;
    discoveryTime[node] = ++time;

    for (int neighbor : graph[node]) {
        if (state[neighbor] == State::UNDISCOVERED) {
            parent[neighbor] = node;
            dfs(neighbor, graph, state, parent, discoveryTime, finishTime, time, backEdges);
        } else if (state[neighbor] == State::DISCOVERED && parent[node] != neighbor) {
            // Backedge detected
            backEdges.push(node);
            backEdges.push(neighbor);
        }
    }

    state[node] = State::PROCESSED;
    finishTime[node] = ++time;
}

stack<int> findBackEdges(const vector<vector<int>>& graph) {
    int n = graph.size();
    vector<State> state(n, State::UNDISCOVERED);
    vector<int> parent(n, -1);
    vector<int> discoveryTime(n);
    vector<int> finishTime(n);
    stack<int> backEdges;
    int time = 0;

    for (int i = 0; i < n; ++i) {
        if (state[i] == State::UNDISCOVERED) {
            dfs(i, graph, state, parent, discoveryTime, finishTime, time, backEdges);
        }
    }

    return backEdges;
}

int main() {
    // Example graph represented as an adjacency list
    vector<vector<int>> graph = {
        {1, 2},
        {3},
        {4},
        {1},
        {2}
    };

    stack<int> backEdges = findBackEdges(graph);

    if (backEdges.empty()) {
        cout << "No backedges found.\n";
    } else {
        cout << "Backedges found:\n";
        while (!backEdges.empty()) {
            int u = backEdges.top();
            backEdges.pop();
            int v = backEdges.top();
            backEdges.pop();
            cout << u << " -> " << v << "\n";
        }
    }

    return 0;
}
```

In this code:

- `dfs()` performs depth-first search on the graph and identifies backedges while traversing.
- `findBackEdges()` initializes the required data structures and calls `dfs()` on each undiscovered node.
- The `main()` function provides an example of how to use `findBackEdges()` with an adjacency list representation of the graph.

This code snippet should help you understand and implement backedge detection in C++.

### 1. Algorithms & Data Structures (C++): Minimum Spanning Tree

In C++, implementing a Minimum Spanning Tree (MST) typically involves using algorithms like Kruskal's algorithm or Prim's algorithm. Here's a basic overview of how you can implement both:

### Kruskal's Algorithm

1. **Sort Edges**: Sort all the edges in non-decreasing order of their weight.
2. **Pick Smallest Edge**: Start picking edges one by one from the sorted list and check if it forms a cycle with the spanning tree formed so far. If it doesn't form a cycle, include it in the MST.
3. **Union-Find**: To check whether adding an edge will form a cycle, use the Union-Find algorithm.

### Prim's Algorithm

1. **Choose a Starting Vertex**: Start from an arbitrary vertex.
2. **Grow the Tree**: At each step, grow the spanning tree by adding the cheapest edge that connects the tree to a vertex not in the tree.
3. **Priority Queue**: Use a priority queue to efficiently select the next vertex to add to the MST.

Here's a simple example of how you can implement Kruskal's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

struct Edge {
    int src, dest, weight;
};

class Graph {
public:
    int V, E; // Number of vertices and edges
    vector<Edge> edges;

    Graph(int V, int E) {
        this->V = V;
        this->E = E;
    }

    void addEdge(int src, int dest, int weight) {
        Edge edge = {src, dest, weight};
        edges.push_back(edge);
    }

    // Find set of an element i
    int find(int parent[], int i) {
        if (parent[i] == -1)
            return i;
        return find(parent, parent[i]);
    }

    // Union of two sets of x and y
    void Union(int parent[], int x, int y) {
        parent[x] = y;
    }

    // Function to construct MST using Kruskal's algorithm
    void KruskalMST() {
        Edge result[V]; // Array to store the MST
        int e = 0; // Index variable for result[]
        int i = 0; // Index variable for sorted edges
        sort(edges.begin(), edges.end(), [](Edge a, Edge b) {
            return a.weight < b.weight;
        });

        // Allocate memory for creating V subsets
        int *parent = new int[V];
        fill(parent, parent + V, -1);

        // Number of edges to be taken is equal to V-1
        while (e < V - 1 && i < E) {
            Edge next_edge = edges[i++];

            int x = find(parent, next_edge.src);
            int y = find(parent, next_edge.dest);

            // If including this edge does't cause cycle, include it
            if (x != y) {
                result[e++] = next_edge;
                Union(parent, x, y);
            }
        }

        cout << "Edges in the constructed MST:\n";
        for (i = 0; i < e; ++i)
            cout << result[i].src << " -- " << result[i].dest << " == " << result[i].weight << endl;

        delete[] parent;
    }
};

int main() {
    int V = 4; // Number of vertices
    int E = 5; // Number of edges
    Graph graph(V, E);
    // Example edges: (src, dest, weight)
    graph.addEdge(0, 1, 10);
    graph.addEdge(0, 2, 6);
    graph.addEdge(0, 3, 5);
    graph.addEdge(1, 3, 15);
    graph.addEdge(2, 3, 4);

    graph.KruskalMST();

    return 0;
}
```

This is a basic implementation to get you started. For larger graphs or more efficiency, you might want to optimize further, perhaps by using a disjoint set data structure for Union-Find operations.

### 1. Algorithms & Data Structures (C++): Minimum Spanning Tree (Disjoint Set)

To implement a Minimum Spanning Tree (MST) using Disjoint Set (Union-Find) data structure in C++, you typically follow these steps:

1. Define a structure for representing edges.
2. Implement a function to sort the edges based on their weights.
3. Implement the Disjoint Set data structure, including functions for finding the parent and for union.
4. Implement the function to find the Minimum Spanning Tree using Kruskal's algorithm, which involves iterating through the sorted edges and adding them to the MST if they don't form a cycle.

Here's a sample implementation:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Structure to represent an edge in the graph
struct Edge {
    int src, dest, weight;
};

// Structure to represent a subset for union-find
struct Subset {
    int parent;
    int rank;
};

class Graph {
    int V; // Number of vertices
    vector<Edge> edges;

public:
    Graph(int V) : V(V) {}

    // Add an edge to the graph
    void addEdge(int src, int dest, int weight) {
        edges.push_back({src, dest, weight});
    }

    // Find the parent of a node
    int find(vector

<Edge>& edges, Subset subsets[], int i) {
        if (subsets[i].parent != i)
            subsets[i].parent = find(edges, subsets, subsets[i].parent);
        return subsets[i].parent;
    }

    // Union two subsets
    void Union(Subset subsets[], int x, int y) {
        int xroot = find(edges, subsets, x);
        int yroot = find(edges, subsets, y);

        // Attach smaller rank tree under root of high rank tree
        if (subsets[xroot].rank < subsets[yroot].rank)
            subsets[xroot].parent = yroot;
        else if (subsets[xroot].rank > subsets[yroot].rank)
            subsets[yroot].parent = xroot;
        else {
            // If ranks are the same, make one as the root and increment its rank
            subsets[yroot].parent = xroot;
            subsets[xroot].rank++;
        }
    }

public:
    // Function to find the MST using Kruskal's algorithm
    void KruskalMST() {
        // Sort all the edges in non-decreasing order of their weight
        sort(edges.begin(), edges.end(), [](const Edge& a, const Edge& b) {
            return a.weight < b.weight;
        });

        vector<Edge> result; // Stores the MST edges

        // Allocate memory for creating V subsets
        Subset *subsets = new Subset[V];

        // Initialize V subsets with single elements
        for (int v = 0; v < V; v++) {
            subsets[v].parent = v;
            subsets[v].rank = 0;
        }

        int e = 0; // An index variable, used for result[]
        int i = 0; // An index variable, used for sorted edges

        // Number of edges to be taken is equal to V-1
        while (e < V - 1 && i < edges.size()) {
            // Pick the smallest edge
            Edge next_edge = edges[i++];

            int x = find(edges, subsets, next_edge.src);
            int y = find(edges, subsets, next_edge.dest);

            // If including this edge doesn't cause cycle, include it in the result and increment the index
            if (x != y) {
                result.push_back(next_edge);
                Union(subsets, x, y);
                e++;
            }
        }

        // Print the MST
        cout << "Minimum Spanning Tree (MST):\n";
        for (Edge edge : result) {
            cout << edge.src << " -- " << edge.dest << "  Weight: " << edge.weight << endl;
        }

        delete[] subsets;
    }
};

int main() {
    int V = 4; // Number of vertices in the graph
    Graph g(V);

    // Add edges to the graph
    g.addEdge(0, 1, 10);
    g.addEdge(0, 2, 6);
    g.addEdge(0, 3, 5);
    g.addEdge(1, 3, 15);
    g.addEdge(2, 3, 4);

    // Find the Minimum Spanning Tree
    g.KruskalMST();

    return 0;
}
```

This implementation should give you a basic idea of how to implement Kruskal's algorithm for finding the Minimum Spanning Tree using the Disjoint Set (Union-Find) data structure in C++.

### 1. Algorithms & Data Structures (C++): Minimum Spanning Tree of a Graph

To find the Minimum Spanning Tree (MST) of a graph, you can use algorithms like Kruskal's algorithm or Prim's algorithm. Here's an outline of how you can implement both algorithms in C++:

1. **Kruskal's Algorithm**:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

struct Edge {
    int src, dest, weight;
};

class Graph {
    int V;
    vector<Edge> edges;

public:
    Graph(int V) : V(V) {}

    void addEdge(int src, int dest, int weight) {
        edges.push_back({src, dest, weight});
    }

    int findParent(vector<int>& parent, int i) {
        if (parent[i] == -1)
            return i;
        return findParent(parent, parent[i]);
    }

    void unionSets(vector<int>& parent, int x, int y) {
        int xset = findParent(parent, x);
        int yset = findParent(parent, y);
        parent[xset] = yset;
    }

    void kruskalMST() {
        vector<Edge> result;
        sort(edges.begin(), edges.end(), [](const Edge& a, const Edge& b) {
            return a.weight < b.weight;
        });

        vector<int> parent(V, -1);

        int i = 0, e = 0;
        while (e < V - 1 && i < edges.size()) {
            Edge next_edge = edges[i++];
            int x = findParent(parent, next_edge.src);
            int y = findParent(parent, next_edge.dest);

            if (x != y) {
                result.push_back(next_edge);
                unionSets(parent, x, y);
                e++;
            }
        }

        for (auto edge : result)
            cout << edge.src << " - " << edge.dest << " : " << edge.weight << endl;
    }
};

int main() {
    int V = 4;
    Graph graph(V);
    graph.addEdge(0, 1, 10);
    graph.addEdge(0, 2, 6);
    graph.addEdge(0, 3, 5);
    graph.addEdge(1, 3, 15);
    graph.addEdge(2, 3, 4);

    graph.kruskalMST();

    return 0;
}
```

1. **Prim's Algorithm**:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <climits>

using namespace std;

#define INF INT_MAX

class Graph {
    int V;
    vector<vector<pair<int, int>>> adj;

public:
    Graph(int V) : V(V) {
        adj.resize(V);
    }

    void addEdge(int u, int v, int weight) {
        adj[u].push_back({v, weight});
        adj[v].push_back({u, weight});
    }

    void primMST() {
        vector<int> key(V, INF);
        vector<int> parent(V, -1);
        vector<bool> inMST(V, false);

        priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;

        int src = 0; // Start from vertex 0

        pq.push({0, src});
        key[src] = 0;

        while (!pq.empty()) {
            int u = pq.top().second;
            pq.pop();

            inMST[u] = true;

            for (auto& neighbor : adj[u]) {
                int v = neighbor.first;
                int weight = neighbor.second;

                if (!inMST[v] && key[v] > weight) {
                    key[v] = weight;
                    pq.push({key[v], v});
                    parent[v] = u;
                }
            }
        }

        for (int i = 1; i < V; i++)
            cout << parent[i] << " - " << i << " : " << key[i] << endl;
    }
};

int main() {
    int V = 4;
    Graph g(V);
    g.addEdge(0, 1, 10);
    g.addEdge(0, 2, 6);
    g.addEdge(0, 3, 5);
    g.addEdge(1, 3, 15);
    g.addEdge(2, 3, 4);

    g.primMST();

    return 0;
}
```

Both algorithms will output the edges of the Minimum Spanning Tree along with their weights. You can adjust the graph representation and input to fit your needs.

### 1. Algorithms & Data Structures (C++): Minimum Spanning Tree: Kruskal's Algorithm

Kruskal's algorithm is a popular algorithm used to find the Minimum Spanning Tree (MST) of a connected, undirected graph. The MST of a graph is a subset of the edges that forms a tree that includes all the vertices, with the minimum possible total edge weight. Kruskal's algorithm is greedy in nature and works by adding edges to the MST in increasing order of their weights while ensuring that no cycles are formed.

Here's a general outline of how Kruskal's algorithm works:

1. **Sort Edges:** Sort all the edges in the graph in non-decreasing order of their weight.
2. **Initialize MST:** Create an empty set to hold the edges of the MST.
3. **Iterate Through Edges:** Iterate through all the sorted edges.
4. **Check for Cycle:** For each edge, if adding it to the MST does not create a cycle, add it to the MST.
5. **Repeat:** Repeat steps 3 and 4 until the MST contains \( n-1 \) edges (where \( n \) is the number of vertices in the graph) or until all edges have been processed.

Here's a C++ implementation of Kruskal's algorithm:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Structure to represent an edge
struct Edge {
    int src, dest, weight;
};

// Structure to represent a subset for union-find
struct Subset {
    int parent, rank;
};

class Graph {
    int V; // Number of vertices
    vector<Edge> edges;

public:
    Graph(int V) : V(V) {}

    // Function to add an edge to the graph
    void addEdge(int src, int dest, int weight) {
        edges.push_back({src, dest, weight});
    }

    // Find set of an element (uses path compression technique)
    int find(vector



```cpp
    Subset subsets[], int i) {
        // find root and make root as parent of i (path compression)
        if (subsets[i].parent != i)
            subsets[i].parent = find(subsets, subsets[i].parent);

        return subsets[i].parent;
    }

    // Union of two sets (uses union by rank)
    void Union(Subset subsets[], int x, int y) {
        int xroot = find(subsets, x);
        int yroot = find(subsets, y);

        // Attach smaller rank tree under root of high rank tree
        // (Union by Rank)
        if (subsets[xroot].rank < subsets[yroot].rank)
            subsets[xroot].parent = yroot;
        else if (subsets[xroot].rank > subsets[yroot].rank)
            subsets[yroot].parent = xroot;
        else {
            // If ranks are the same, then make one as root and increment
            // its rank by one
            subsets[yroot].parent = xroot;
            subsets[xroot].rank++;
        }
    }

    // Function to apply Kruskal's algorithm
    void KruskalMST() {
        vector<Edge> result; // This will store the resultant MST

        // Step 1: Sort all the edges in non-decreasing order of their weight
        sort(edges.begin(), edges.end(), [](const Edge& a, const Edge& b) {
            return a.weight < b.weight;
        });

        Subset* subsets = new Subset[V];

        // Create V subsets with single elements
        for (int v = 0; v < V; v++) {
            subsets[v].parent = v;
            subsets[v].rank = 0;
        }

        // Index used to pick the next edge
        int e = 0;

        // Number of edges to be taken is equal to V-1
        while (result.size() < V - 1 && e < edges.size()) {
            // Step 2: Pick the smallest edge. Check if it forms a cycle
            Edge next_edge = edges[e++];
            int x = find(subsets, next_edge.src);
            int y = find(subsets, next_edge.dest);

            // If including this edge does not cause a cycle, include it
            if (x != y) {
                result.push_back(next_edge);
                Union(subsets, x, y);
            }
        }

        // Print the edges of MST
        cout << "Edges of MST:" << endl;
        int minimumCost = 0;
        for (auto& edge : result) {
            cout << edge.src << " - " << edge.dest << " : " << edge.weight << endl;
            minimumCost += edge.weight;
        }
        cout << "Minimum Cost Spanning Tree: " << minimumCost << endl;

        delete[] subsets;
    }
};

int main() {
    // Create a graph
    int V = 4; // Number of vertices
    Graph graph(V);

    // Add edges
    graph.addEdge(0, 1, 10);
    graph.addEdge(0, 2, 6);
    graph.addEdge(0, 3, 5);
    graph.addEdge(1, 3, 15);
    graph.addEdge(2, 3, 4);

    // Find MST using Kruskal's algorithm
    graph.KruskalMST();

    return 0;
}
```

This code demonstrates how to use Kruskal's algorithm to find the Minimum Spanning Tree of a graph in C++. The example graph used in this code has 4 vertices and 5 edges. You can modify the graph by adding or removing edges as needed. When you run this code, it will output the edges of the Minimum Spanning Tree along with their weights and the total weight of the MST.

### 1. Algorithms & Data Structures (C++): Minimum Spanning Tree: Prim's Algorithm

Prim's algorithm is a popular method used to find the Minimum Spanning Tree (MST) of a connected, undirected graph. Here's a basic explanation of how Prim's algorithm works:

1. **Initialization**: Start with an arbitrary vertex as the initial vertex and mark it as visited.

2. **Selecting Edges**: Find the minimum-weight edge that connects a visited vertex to an unvisited vertex. Add this edge to the MST and mark the newly visited vertex as visited.

3. **Repeat**: Repeat step 2 until all vertices are visited.

4. **Termination**: Once all vertices are visited, the algorithm terminates, and the resulting tree is the MST of the graph.

Here's a simple implementation of Prim's algorithm in C++ using adjacency matrix representation:

```cpp
#include <iostream>
#include <climits>
using namespace std;

#define V 5 // Number of vertices

int minKey(int key[], bool mstSet[]) {
    int min = INT_MAX, min_index;
    for (int v = 0; v < V; v++)
        if (mstSet[v] == false && key[v] < min)
            min = key[v], min_index = v;
    return min_index;
}

void printMST(int parent[], int graph[V][V]) {
    cout << "Edge \tWeight\n";
    for (int i = 1; i < V; i++)
        cout << parent[i] << " - " << i << " \t" << graph[i][parent[i]] << " \n";
}

void primMST(int graph[V][V]) {
    int parent[V]; // Array to store constructed MST
    int key[V]; // Key values used to pick minimum weight edge in cut
    bool mstSet[V]; // To represent set of vertices not yet included in MST

    // Initialize all keys as INFINITE
    for (int i = 0; i < V; i++)
        key[i] = INT_MAX, mstSet[i] = false;

    // Always include first 0th vertex in MST.
    key[0] = 0;
    parent[0] = -1; // First node is always root of MST

    // The MST will have V vertices
    for (int count = 0; count < V - 1; count++) {
        // Pick the minimum key vertex not yet included in MST
        int u = minKey(key, mstSet);
        // Add the picked vertex to the MST Set
        mstSet[u] = true;
        // Update key value and parent index of the adjacent vertices of the picked vertex.
        // Consider only those vertices which are not yet included in MST
        for (int v = 0; v < V; v++)
            // graph[u][v] is non zero only for adjacent vertices of m
            // mstSet[v] is false for vertices not yet included in MST
            // Update the key only if graph[u][v] is smaller than key[v]
            if (graph[u][v] && mstSet[v] == false && graph[u][v] < key[v])
                parent[v] = u, key[v] = graph[u][v];
    }

    // print the constructed MST
    printMST(parent, graph);
}

int main() {
    // Sample graph
    int graph[V][V] = {
        {0, 2, 0, 6, 0},
        {2, 0, 3, 8, 5},
        {0, 3, 0, 0, 7},
        {6, 8, 0, 0, 9},
        {0, 5, 7, 9, 0}
    };

    // Print the solution
    primMST(graph);

    return 0;
}
```

This implementation finds the MST of a sample graph and prints the edges along with their weights. You can modify the `graph` array to represent your own graph.

### 1. Algorithms & Data Structures (C++): Breadth First Search & Depth First Search

Breadth First Search (BFS) and Depth First Search (DFS) are fundamental algorithms used for traversing or searching tree or graph data structures. In C++, you can implement both algorithms using various data structures like arrays, linked lists, or queues (for BFS) and stacks (for DFS). Here's a brief overview and implementation for both:

#### Breadth First Search (BFS)

BFS explores all the vertices on the current level before moving to the vertices on the next level. It visits the vertices in a level-by-level manner.

```cpp
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

void BFS(vector<vector<int>>& graph, int start) {
    int numVertices = graph.size();
    vector<bool> visited(numVertices, false);
    queue<int> q;

    visited[start] = true;
    q.push(start);

    while (!q.empty()) {
        int current = q.front();
        q.pop();
        cout << current << " ";

        for (int neighbor : graph[current]) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                q.push(neighbor);
            }
        }
    }
}

int main() {
    int numVertices = 5;
    vector<vector<int>> graph(numVertices);

    // Example graph
    graph[0] = {1, 2};
    graph[1] = {0, 2, 3};
    graph[2] = {0, 1, 4};
    graph[3] = {1};
    graph[4] = {2};

    cout << "BFS Traversal: ";
    BFS(graph, 0); // Start BFS from vertex 0

    return 0;
}
```

### Depth First Search (DFS)

DFS explores as far as possible along each branch before backtracking. It goes as deep as possible along each branch before backtracking to explore other branches.

#### Implementation

```cpp
#include <iostream>
#include <vector>

using namespace std;

void DFS(vector<vector<int>>& graph, vector<bool>& visited, int current) {
    visited[current] = true;
    cout << current << " ";

    for (int neighbor : graph[current]) {
        if (!visited[neighbor]) {
            DFS(graph, visited, neighbor);
        }
    }
}

int main() {
    int numVertices = 5;
    vector<vector<int>> graph(numVertices);

    // Example graph
    graph[0] = {1, 2};
    graph[1] = {0, 2, 3};
    graph[2] = {0, 1, 4};
    graph[3] = {1};
    graph[4] = {2};

    vector<bool> visited(numVertices, false);

    cout << "DFS Traversal: ";
    for (int i = 0; i < numVertices; ++i) {
        if (!visited[i]) {
            DFS(graph, visited, i); // Start DFS from each unvisited vertex
        }
    }

    return 0;
}
```

These implementations assume an adjacency list representation of the graph. Adjustments might be needed depending on how your graph is represented.

### 1. Algorithms & Data Structures (C++): Breadth First Search Concept

Breadth First Search (BFS) is a fundamental graph traversal algorithm used to explore nodes and edges of a graph in a breadthward motion. It starts at a designated source node and explores all of its neighboring nodes at the present depth before moving on to the nodes at the next depth level. This algorithm is particularly useful for finding the shortest path between two nodes in an unweighted graph.

Here's a basic outline of the BFS algorithm:

1. **Start with a source node**: Choose a starting node and mark it as visited.

2. **Explore neighbors**: Visit all the adjacent nodes of the current node that have not been visited yet.

3. **Queue**: As you visit each node, enqueue it into a queue to keep track of which nodes to visit next. This ensures that nodes are visited in the order they were discovered.

4. **Dequeue and Repeat**: Dequeue a node from the queue and repeat steps 2-3 for each of its unvisited neighbors.

5. **Termination**: Continue this process until the queue is empty. At this point, you have visited all the reachable nodes from the source node.

Here's a simple C++ implementation of BFS using an adjacency list representation of the graph:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

// Graph class representing an undirected graph using adjacency list
class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V) {
        adj.resize(V);
    }

    // Function to add an edge between vertices u and v
    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u); // Assuming undirected graph
    }

    // Breadth First Search from a given source vertex
    void BFS(int source) {
        vector<bool> visited(V, false); // Keep track of visited nodes
        queue<int> q; // Queue for BFS traversal

        visited[source] = true; // Mark source as visited
        q.push(source); // Enqueue source

        while (!q.empty()) {
            int current = q.front();
            cout << current << " ";
            q.pop();

            // Visit all adjacent vertices of current vertex
            for (int neighbor : adj[current]) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true; // Mark neighbor as visited
                    q.push(neighbor); // Enqueue neighbor
                }
            }
        }
    }
};

int main() {
    Graph g(6); // Create a graph with 6 vertices

    // Add edges
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 4);
    g.addEdge(3, 4);
    g.addEdge(3, 5);
    g.addEdge(4, 5);

    cout << "Breadth First Traversal starting from vertex 0: ";
    g.BFS(0);

    return 0;
}
```

This code creates a graph with 6 vertices and adds edges between them. Then, it performs BFS starting from vertex 0 and prints the traversal sequence.

### 1. Algorithms & Data Structures (C++): Breadth First Search for Disconnected Graph

Sure, implementing Breadth First Search (BFS) for a disconnected graph in C++ involves visiting all the vertices of the graph, even those that are not connected to the starting vertex. Here's how you can do it:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

// Class representing a graph
class Graph {
    int V; // Number of vertices

    // Pointer to an array containing adjacency lists
    vector<int> *adj;

public:
    Graph(int V); // Constructor
    void addEdge(int v, int w); // Function to add an edge to the graph
    void BFS(); // Breadth First Search function
    void BFSUtil(int v, vector<bool> &visited); // Utility function for BFS
};

Graph::Graph(int V) {
    this->V = V;
    adj = new vector<int>[V];
}

void Graph::addEdge(int v, int w) {
    adj[v].push_back(w); // Add w to v’s list.
}

void Graph::BFSUtil(int v, vector<bool> &visited) {
    // Create a queue for BFS
    queue<int> queue;

    // Mark the current node as visited and enqueue it
    visited[v] = true;
    queue.push(v);

    // 'i' will be used to get all adjacent vertices of a vertex
    vector<int>::iterator i;

    while (!queue.empty()) {
        // Dequeue a vertex from queue and print it
        v = queue.front();
        cout << v << " ";
        queue.pop();

        // Get all adjacent vertices of the dequeued vertex v
        // If an adjacent has not been visited, then mark it
        // visited and enqueue it
        for (i = adj[v].begin(); i != adj[v].end(); ++i) {
            if (!visited[*i]) {
                visited[*i] = true;
                queue.push(*i);
            }
        }
    }
}

void Graph::BFS() {
    // Mark all the vertices as not visited
    vector<bool> visited(V, false);

    // Call the recursive helper function to print DFS traversal
    // starting from all vertices one by one
    for (int i = 0; i < V; i++) {
        if (!visited[i]) {
            BFSUtil(i, visited);
        }
    }
}

int main() {
    // Create a graph given in the above diagram
    Graph g(6);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(3, 4);
    g.addEdge(4, 5);

    cout << "Breadth First Traversal of disconnected graph: \n";
    g.BFS();

    return 0;
}
```

In this code:

- We create a `Graph` class to represent the graph.
- The `addEdge` function is used to add an edge between two vertices.
- The `BFS` function is the main function to perform BFS. It calls `BFSUtil` for all vertices one by one.
- The `BFSUtil` function performs the actual BFS traversal. It takes a starting vertex and a boolean vector to keep track of visited vertices.

This implementation ensures that all the vertices of the graph are visited, even if the graph is disconnected.

### 1. Algorithms & Data Structures (C++): Breadth First Search for SSSPP

Sure, let's delve into implementing Breadth First Search (BFS) for Single Source Shortest Path (SSSP) in C++.

Here's a simple implementation of BFS for SSSP:

```cpp
#include <iostream>
#include <queue>
#include <vector>
#include <climits>

using namespace std;

// Graph class representing an undirected graph using adjacency list representation
class Graph {
    int V; // Number of vertices

    // Adjacency list representation of the graph
    vector<vector<int>> adj;

public:
    Graph(int V) {
        this->V = V;
        adj.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u); // Assuming undirected graph
    }

    // Function to perform Breadth First Search for SSSP
    vector<int> BFS_SSSP(int source) {
        vector<int> dist(V, INT_MAX); // Initialize distances with infinity
        queue<int> q;

        // Distance from source to itself is 0
        dist[source] = 0;
        q.push(source);

        while (!q.empty()) {
            int u = q.front();
            q.pop();

            // Traverse all adjacent vertices of u
            for (int v : adj[u]) {
                // If v is not visited yet
                if (dist[v] == INT_MAX) {
                    // Update distance of v from source
                    dist[v] = dist[u] + 1;
                    q.push(v);
                }
            }
        }

        return dist;
    }
};

int main() {
    int V = 6; // Number of vertices
    Graph g(V);

    // Adding edges to the graph
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(2, 4);
    g.addEdge(2, 5);

    int source = 0; // Source vertex for SSSP

    // Perform BFS for SSSP from the given source
    vector<int> shortestDistances = g.BFS_SSSP(source);

    // Print shortest distances from the source to all vertices
    cout << "Shortest distances from source vertex " << source << ":\n";
    for (int i = 0; i < V; ++i) {
        cout << "Distance to vertex " << i << " is " << shortestDistances[i] << endl;
    }

    return 0;
}
```

In this implementation:

- We have a `Graph` class that represents an undirected graph using an adjacency list.
- The `addEdge` function adds edges to the graph.
- The `BFS_SSSP` function performs Breadth First Search for Single Source Shortest Path from a given source vertex.
- The `main` function demonstrates the usage of the `Graph` class and performs BFS for SSSP from a chosen source vertex.

You can modify the `main` function and add more edges to the graph to test the BFS algorithm further.

### 1. Algorithms & Data Structures (C++): Graph Abstract Data Type (ADT)

In C++, you can implement a Graph Abstract Data Type (ADT) using various data structures like adjacency matrix, adjacency list, or an edge list. Here, I'll provide a basic implementation of a graph using an adjacency list representation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) {
        this->V = V;
        adj.resize(V);
    }

    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u); // For undirected graph
    }

    void printGraph() {
        for (int i = 0; i < V; ++i) {
            cout << "Vertex " << i << " is connected to: ";
            for (int j : adj[i]) {
                cout << j << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph graph(5);

    // Add some edges
    graph.addEdge(0, 1);
    graph.addEdge(0, 4);
    graph.addEdge(1, 2);
    graph.addEdge(1, 3);
    graph.addEdge(1, 4);
    graph.addEdge(2, 3);
    graph.addEdge(3, 4);

    // Print the graph
    graph.printGraph();

    return 0;
}
```

This implementation creates a simple undirected graph with an adjacency list representation. You can modify or extend this implementation to suit your specific needs, such as adding methods to perform operations like depth-first search (DFS) or breadth-first search (BFS), checking for connectivity, finding shortest paths, etc.

### 1. Algorithms & Data Structures (C++): Graph Adjacency List

Graphs are fundamental data structures used to model connections between entities. One common way to represent a graph is using an adjacency list. In C++, you can implement a graph using an adjacency list using various data structures like vectors, lists, or maps. Here's a basic implementation of a graph using an adjacency list:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int vertices) : V(vertices) {
        adj.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int src, int dest) {
        adj[src].push_back(dest);
        // For undirected graph, add this line:
        // adj[dest].push_back(src);
    }

    // Function to print the adjacency list representation of the graph
    void printGraph() {
        for (int i = 0; i < V; ++i) {
            cout << "Adjacency list of vertex " << i << ": ";
            for (int j : adj[i]) {
                cout << j << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph graph(5);
    
    // Add edges
    graph.addEdge(0, 1);
    graph.addEdge(0, 4);
    graph.addEdge(1, 2);
    graph.addEdge(1, 3);
    graph.addEdge(1, 4);
    graph.addEdge(2, 3);
    graph.addEdge(3, 4);
    
    // Print the adjacency list
    graph.printGraph();

    return 0;
}
```

In this code:

- The `Graph` class represents the graph using an adjacency list.
- `V` represents the number of vertices in the graph.
- `adj` is a vector of vectors where each vector represents the adjacency list for a vertex.
- The `addEdge` function adds an edge between two vertices.
- The `printGraph` function prints the adjacency list representation of the graph.

You can create a graph object, add edges to it, and print its adjacency list using this implementation.

### 1. Algorithms & Data Structures (C++): Graph Adjacency Matrix

In C++, you can represent a graph using an adjacency matrix. An adjacency matrix is a 2D array where the entry at row i and column j represents whether there is an edge from vertex i to vertex j. Here's a basic implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
private:
    int numVertices;
    vector<vector<int>> adjMatrix;

public:
    Graph(int n) : numVertices(n), adjMatrix(n, vector<int>(n, 0)) {}

    void addEdge(int src, int dest) {
        // Assuming the graph is undirected
        adjMatrix[src][dest] = 1;
        adjMatrix[dest][src] = 1;
    }

    void printAdjMatrix() {
        for (int i = 0; i < numVertices; ++i) {
            for (int j = 0; j < numVertices; ++j) {
                cout << adjMatrix[i][j] << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph graph(5);

    // Add some edges
    graph.addEdge(0, 1);
    graph.addEdge(0, 4);
    graph.addEdge(1, 2);
    graph.addEdge(1, 3);
    graph.addEdge(1, 4);
    graph.addEdge(2, 3);
    graph.addEdge(3, 4);

    // Print the adjacency matrix
    cout << "Adjacency Matrix:" << endl;
    graph.printAdjMatrix();

    return 0;
}
```

In this code:

- The `Graph` class represents an undirected graph using an adjacency matrix.
- The `addEdge` function adds an edge between two vertices by setting the corresponding entries in the adjacency matrix to 1.
- The `printAdjMatrix` function prints the adjacency matrix to the console.

You can modify this code according to your requirements, such as adding functions to remove edges, check if an edge exists, or perform other graph-related operations.

### 1. Algorithms & Data Structures (C++): Graph ADT Class

Creating a Graph ADT (Abstract Data Type) class in C++ involves defining the data structure and operations to manipulate graphs. Here's a basic implementation using adjacency lists:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>

using namespace std;

class Graph {
private:
    unordered_map<int, vector<int>> adjList;
    int numVertices;

public:
    Graph(int vertices) : numVertices(vertices) {}

    // Function to add an edge between two vertices
    void addEdge(int src, int dest) {
        // Assuming the graph is undirected
        adjList[src].push_back(dest);
        adjList[dest].push_back(src);
    }

    // Function to print the adjacency list representation of the graph
    void printGraph() {
        for (const auto& pair : adjList) {
            cout << pair.first << " -> ";
            for (int v : pair.second) {
                cout << v << " ";
            }
            cout << endl;
        }
    }

    // Function to get the number of vertices in the graph
    int getNumVertices() {
        return numVertices;
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph graph(5);

    // Add some edges
    graph.addEdge(0, 1);
    graph.addEdge(0, 4);
    graph.addEdge(1, 2);
    graph.addEdge(1, 3);
    graph.addEdge(1, 4);
    graph.addEdge(2, 3);
    graph.addEdge(3, 4);

    // Print the adjacency list representation
    cout << "Graph:" << endl;
    graph.printGraph();

    return 0;
}
```

This code defines a `Graph` class with an adjacency list representation. It supports adding edges between vertices and printing the graph. You can extend it by adding more functionalities like removing edges, checking if an edge exists, etc., based on your requirements.

### 1. Algorithms & Data Structures (C++): Graph Algorithms

Graph algorithms are fascinating and foundational in computer science. They deal with structures that represent relationships between pairs of objects. Here's an overview of some essential graph algorithms in C++:

1. **Breadth-First Search (BFS)**:
   - BFS explores all the vertices at the present depth before moving on to the vertices at the next depth level.
   - It can be used to find the shortest path in an unweighted graph.
   - Implementation:

     ```cpp
     void BFS(vector<vector<int>>& graph, int start) {
         vector<bool> visited(graph.size(), false);
         queue<int> q;
         q.push(start);
         visited[start] = true;
         while (!q.empty()) {
             int curr = q.front();
             q.pop();
             cout << curr << " ";
             for (int neighbor : graph[curr]) {
                 if (!visited[neighbor]) {
                     q.push(neighbor);
                     visited[neighbor] = true;
                 }
             }
         }
     }
     ```

2. **Depth-First Search (DFS)**:
   - DFS explores as far as possible along each branch before backtracking.
   - It's used to detect cycles in a graph, topological sorting, and more.
   - Implementation:

     ```cpp
     void DFS(vector<vector<int>>& graph, int start, vector<bool>& visited) {
         visited[start] = true;
         cout << start << " ";
         for (int neighbor : graph[start]) {
             if (!visited[neighbor]) {
                 DFS(graph, neighbor, visited);
             }
         }
     }
     ```

3. **Dijkstra's Algorithm**:
   - Dijkstra's algorithm finds the shortest path from a source node to all other nodes in a weighted graph (non-negative weights).
   - It's greedy and guarantees the shortest path.
   - Implementation using priority queue:

     ```cpp
     void Dijkstra(vector<vector<pair<int, int>>>& graph, int start) {
         priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
         vector<int> dist(graph.size(), INT_MAX);
         dist[start] = 0;
         pq.push({0, start});
         while (!pq.empty()) {
             int u = pq.top().second;
             pq.pop();
             for (auto& edge : graph[u]) {
                 int v = edge.first;
                 int weight = edge.second;
                 if (dist[v] > dist[u] + weight) {
                     dist[v] = dist[u] + weight;
                     pq.push({dist[v], v});
                 }
             }
         }
     }
     ```

4. **Bellman-Ford Algorithm**:
   - Bellman-Ford algorithm finds the shortest path from a source node to all other nodes in a weighted graph (can handle negative weights).
   - It detects negative weight cycles.
   - Implementation:

     ```cpp
     void BellmanFord(vector<vector<pair<int, int>>>& graph, int start) {
         vector<int> dist(graph.size(), INT_MAX);
         dist[start] = 0;
         for (int i = 0; i < graph.size() - 1; ++i) {
             for (int u = 0; u < graph.size(); ++u) {
                 for (auto& edge : graph[u]) {
                     int v = edge.first;
                     int weight = edge.second;
                     if (dist[u] != INT_MAX && dist[v] > dist[u] + weight) {
                         dist[v] = dist[u] + weight;
                     }
                 }
             }
         }
     }
     ```

These are just a few fundamental graph algorithms in C++. Depending on your needs, you might explore more advanced algorithms like Floyd-Warshall, Kruskal's Algorithm, Prim's Algorithm, etc.

### 1. Algorithms & Data Structures (C++): Graph Algorithms - Dijsktra's Algorithm

Dijkstra's algorithm is a fundamental algorithm for finding the shortest paths between nodes in a graph, which may represent, for example, road networks. It was conceived by Dutch computer scientist Edsger W. Dijkstra in 1956. Here's a basic outline of how the algorithm works:

1. **Initialization**: Start by assigning a tentative distance value to every node. Set the source node's distance to 0 and all other nodes' distances to infinity. Keep a set of unvisited nodes.

2. **Selecting the Node**: Choose the unvisited node with the smallest tentative distance. If there's no such node left, stop.

3. **Exploring Neighbors**: For the current node, consider all of its unvisited neighbors and calculate their tentative distances through the current node. Compare the newly calculated tentative distance to the current assigned value and assign the smaller one. For example, if the current node A is marked with a distance of 6, and the edge connecting it with a neighbor B has length 2, then the distance to B through A will be 6 + 2 = 8. If 8 is less than the current distance assigned to B, then update it.

4. **Marking as Visited**: Once we've considered all the neighbors of the current node, mark the current node as visited and remove it from the unvisited set. A visited node will not be checked again.

5. **Termination**: Repeat steps 2 through 4 until the destination node has been visited, or if the smallest tentative distance among the nodes in the unvisited set is infinity, indicating that no path exists.

After the algorithm completes, the shortest distance to every node from the source node is known, and the paths themselves can be reconstructed if required.

Here's a simple pseudocode representation:

```plaintext
function Dijkstra(Graph, source):
    create vertex set Q
    for each vertex v in Graph:           
        dist[v] ← INFINITY                
        prev[v] ← UNDEFINED               
        add v to Q                      
    dist[source] ← 0                      
    while Q is not empty:
        u ← vertex in Q with min dist[u]  
        remove u from Q
        for each neighbor v of u:          
            alt ← dist[u] + length(u, v)
            if alt < dist[v]:             
                dist[v] ← alt
                prev[v] ← u
    return dist[], prev[]
```

This algorithm's time complexity depends on the implementation. With a naive implementation using arrays or lists, it can be O(V^2), where V is the number of vertices. With more efficient data structures like a priority queue (e.g., binary heap or Fibonacci heap), it can be reduced to O((V + E) * log V), where E is the number of edges.

### 1. Algorithms & Data Structures (C++): Graph Algorithms - Floyd Warshall Algorithm

The Floyd-Warshall algorithm is a dynamic programming algorithm used to find the shortest paths between all pairs of vertices in a weighted graph with positive or negative edge weights (but with no negative cycles). It's particularly useful for finding shortest paths in dense graphs, where other algorithms like Dijkstra's or Bellman-Ford might be inefficient.

Here's a brief overview of how the algorithm works:

1. **Initialization**: Initialize a 2D array `dist[][]` where `dist[i][j]` will represent the shortest distance between vertex `i` and vertex `j`. If there's no edge between `i` and `j`, set `dist[i][j]` to infinity, and set `dist[i][i]` to 0. Also, initialize `dist[][]` with the weights of the edges.

2. **Main Loop**: Iterate over all vertices `k` from 1 to `V` (where `V` is the number of vertices in the graph). For each pair of vertices `i` and `j`, check if going through vertex `k` shortens the path from `i` to `j`. If it does, update the value of `dist[i][j]` to the new shorter path.

3. **Optimization**: The time complexity of the Floyd-Warshall algorithm is O(V^3), where `V` is the number of vertices in the graph. It's quite efficient for dense graphs but can be slower than other algorithms like Dijkstra's or Bellman-Ford for sparse graphs.

Here's a simple implementation of the Floyd-Warshall algorithm in C++:

```cpp
#include <iostream>
#include <vector>
using namespace std;

#define INF 999999

void floydWarshall(vector<vector<int>>& graph, int V) {
    vector<vector<int>> dist = graph;

    // Main loop
    for (int k = 0; k < V; k++) {
        for (int i = 0; i < V; i++) {
            for (int j = 0; j < V; j++) {
                if (dist[i][k] != INF && dist[k][j] != INF && dist[i][k] + dist[k][j] < dist[i][j])
                    dist[i][j] = dist[i][k] + dist[k][j];
            }
        }
    }

    // Printing the shortest distances
    cout << "Shortest distances between every pair of vertices:\n";
    for (int i = 0; i < V; i++) {
        for (int j = 0; j < V; j++) {
            if (dist[i][j] == INF)
                cout << "INF\t";
            else
                cout << dist[i][j] << "\t";
        }
        cout << endl;
    }
}

int main() {
    int V, E;
    cout << "Enter the number of vertices and edges: ";
    cin >> V >> E;

    // Initialize the graph with INF as initial distances
    vector<vector<int>> graph(V, vector<int>(V, INF));

    cout << "Enter the edges (source, destination, weight):\n";
    for (int i = 0; i < E; i++) {
        int u, v, w;
        cin >> u >> v >> w;
        graph[u][v] = w;
    }

    // Calling the Floyd-Warshall function
    floydWarshall(graph, V);

    return 0;
}
```

This implementation takes input for the number of vertices and edges, and then for each edge, it takes the source vertex, destination vertex, and the weight of the edge. It then applies the Floyd-Warshall algorithm to find the shortest distances between all pairs of vertices and prints the result.

### 1. Algorithms & Data Structures (C++): Graph Algorithms - Kruskal and Prim's Algorithms

Kruskal's and Prim's algorithms are both classic algorithms used for finding minimum spanning trees (MSTs) in a graph. These algorithms are essential in network design, circuit layout, and various optimization problems.

#### Kruskal's Algorithm

Kruskal's algorithm is a greedy algorithm that finds a minimum spanning tree for a connected weighted graph. It repeatedly adds the next lightest edge to the spanning tree if adding it will not form a cycle. Here's a general outline:

1. **Sort Edges:** Sort all the edges in non-decreasing order of their weight.
2. **Initialize MST:** Create an empty set to hold the minimum spanning tree (MST).
3. **Iterate:** Iterate through the sorted edges, and for each edge:
   - If adding the edge to the MST doesn't form a cycle, add it to the MST.
4. **Output MST:** The MST is formed when \( V - 1 \) edges are added, where \( V \) is the number of vertices in the graph.

Here's a simplified implementation in C++:

```cpp
// Assuming the graph is represented as a vector of edges {u, v, weight}
// Also assuming Union-Find data structure implementation for cycle detection

vector<int> parent, rank;

int find(int u) {
    if (parent[u] != u)
        parent[u] = find(parent[u]);
    return parent[u];
}

void union_sets(int u, int v) {
    u = find(u);
    v = find(v);
    if (u != v) {
        if (rank[u] < rank[v])
            swap(u, v);
        parent[v] = u;
        if (rank[u] == rank[v])
            rank[u]++;
    }
}

int kruskalMST(vector<vector<int>>& edges, int n) {
    parent.resize(n);
    rank.resize(n);
    for (int i = 0; i < n; i++) {
        parent[i] = i;
        rank[i] = 0;
    }
    sort(edges.begin(), edges.end(), [](const vector<int>& a, const vector<int>& b) {
        return a[2] < b[2];
    });
    int cost = 0;
    vector<vector<int>> mst;
    for (auto edge : edges) {
        int u = edge[0], v = edge[1], w = edge[2];
        if (find(u) != find(v)) {
            cost += w;
            mst.push_back(edge);
            union_sets(u, v);
        }
    }
    // return cost; // If you only need the cost
    // return mst; // If you need the edges of the MST
    return cost;
}
```

### Prim's Algorithm

Prim's algorithm is another greedy algorithm that finds a minimum spanning tree for a connected weighted graph. It starts with an arbitrary node and repeatedly grows the spanning tree by adding the cheapest edge that connects the tree to a vertex not yet in the tree. Here's how it works:

1. **Initialize:** Choose an arbitrary node as the starting point.
2. **Grow Tree:** Grow the tree by adding the cheapest edge that connects the tree to a vertex not yet in the tree.
3. **Repeat:** Repeat step 2 until all vertices are included in the tree.

Here's a simplified implementation in C++:

```cpp
// Assuming the graph is represented as an adjacency list of {node, weight} pairs

int primMST(vector<vector<pair<int, int>>>& graph, int n) {
    vector<bool> inMST(n, false);
    vector<int> key(n, INT_MAX);
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    int cost = 0;

    pq.push({0, 0}); // Start from vertex 0
    key[0] = 0;

    while (!pq.empty()) {
        int u = pq.top().second;
        pq.pop();
        if (inMST[u])
            continue;
        inMST[u] = true;
        cost += key[u];
        for (auto& [v, weight] : graph[u]) {
            if (!inMST[v] && weight < key[v]) {
                key[v] = weight;
                pq.push({key[v], v});
            }
        }
    }
    return cost;
}
```

These implementations are basic and might need modifications based on specific requirements or the exact representation of the graph. Additionally, for larger graphs, you might want to consider more optimized data structures and algorithms.

### 1. Algorithms & Data Structures (C++): Graph Algorithms: Adjacency matrix and adjacency list

In the realm of graph algorithms, the choice between adjacency matrix and adjacency list representation often depends on the specific problem you're trying to solve and the characteristics of the graph you're working with. Let's break down each representation:

### Adjacency Matrix

- **Definition**: An adjacency matrix is a 2D array of size V x V where V is the number of vertices in the graph.
- **Space Complexity**: O(V^2), where V is the number of vertices.
- **Pros**:
  - Simple implementation, especially for dense graphs (where most vertices are connected to most other vertices).
  - Easy to check if there is an edge between two vertices (O(1) time complexity).
- **Cons**:
  - Space-inefficient for sparse graphs (where few vertices are connected to few other vertices).
  - Adding or removing vertices is expensive (O(V^2) time complexity).

### Adjacency List

- **Definition**: An adjacency list is an array of lists, where each element of the array represents a vertex and its corresponding list contains all the adjacent vertices.
- **Space Complexity**: O(V + E), where V is the number of vertices and E is the number of edges.
- **Pros**:
  - Space-efficient for sparse graphs.
  - Adding or removing vertices/edges is relatively inexpensive (O(1) or O(V) time complexity).
- **Cons**:
  - Less straightforward for checking if there is an edge between two vertices (time complexity depends on the implementation, typically O(V) or O(E)).
  - Slightly more complex implementation compared to adjacency matrix.

Here's a simple implementation of both adjacency matrix and adjacency list in C++:

#### Adjacency Matrix

```cpp
#include <iostream>
#include <vector>

using namespace std;

const int MAX_VERTICES = 100;

int adjMatrix[MAX_VERTICES][MAX_VERTICES];

void addEdge(int u, int v) {
    adjMatrix[u][v] = 1;
    adjMatrix[v][u] = 1; // Assuming an undirected graph
}

int main() {
    // Initialize adjacency matrix with zeros
    memset(adjMatrix, 0, sizeof(adjMatrix));
    
    // Adding edges
    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 2);
    addEdge(2, 3);

    // Displaying adjacency matrix
    for (int i = 0; i < 4; ++i) {
        for (int j = 0; j < 4; ++j) {
            cout << adjMatrix[i][j] << " ";
        }
        cout << endl;
    }
    
    return 0;
}
```

#### Adjacency List

```cpp
#include <iostream>
#include <vector>

using namespace std;

vector<int> adjList[MAX_VERTICES];

void addEdge(int u, int v) {
    adjList[u].push_back(v);
    adjList[v].push_back(u); // Assuming an undirected graph
}

int main() {
    // Adding edges
    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 2);
    addEdge(2, 3);

    // Displaying adjacency list
    for (int i = 0; i < 4; ++i) {
        cout << "Adjacency list of vertex " << i << ": ";
        for (int j = 0; j < adjList[i].size(); ++j) {
            cout << adjList[i][j] << " ";
        }
        cout << endl;
    }
    
    return 0;
}
```

Both representations have their own strengths and weaknesses, so choosing the appropriate one depends on the specific requirements and characteristics of your graph-based problem.

### 1. Algorithms & Data Structures (C++): Graph Algorithms: Applications of graphs

Graphs are incredibly versatile data structures with numerous applications across various domains. Some common applications of graphs include:

1. **Social Networks**: Social media platforms like Facebook, Twitter, and LinkedIn utilize graphs to represent connections between users. Nodes represent individuals, and edges represent relationships or interactions between them.

2. **Network Routing**: Graphs are used to model networks of interconnected devices, such as the internet or transportation systems. Routing algorithms like Dijkstra's or Bellman-Ford algorithm are applied to find the shortest path between nodes.

3. **Recommendation Systems**: Graphs can be employed to model user-item interactions in recommendation systems. Nodes represent users and items, and edges represent user-item interactions. Algorithms like collaborative filtering or personalized PageRank can then be applied to make recommendations.

4. **Geographical Information Systems (GIS)**: Graphs are used to model geographical data, such as maps and road networks. Routing algorithms are applied to find the shortest or fastest path between locations.

5. **Computer Networks**: Graphs are used to model computer networks, where nodes represent devices like computers or routers, and edges represent connections between them. Graph algorithms are applied for tasks such as network topology analysis, routing, and network flow optimization.

6. **Circuit Design**: Graphs are used to model electrical circuits, where components like resistors, capacitors, and transistors are represented as nodes, and connections between them as edges. Graph algorithms are applied to analyze circuit properties and optimize designs.

7. **E-commerce**: Graphs can be used to model relationships between products, customers, and transactions in e-commerce platforms. Algorithms are applied for tasks like product recommendation, fraud detection, and customer segmentation.

8. **Bioinformatics**: Graphs are used to model biological data, such as protein-protein interactions, genetic pathways, and evolutionary relationships. Graph algorithms are applied for tasks like identifying functional modules in protein networks, predicting protein structures, and analyzing genetic sequences.

9. **Natural Language Processing (NLP)**: Graphs are used to represent relationships between words or documents in text data. Algorithms like PageRank or community detection are applied for tasks like document clustering, sentiment analysis, and information retrieval.

10. **Game Development**: Graphs are used to model game worlds, where nodes represent game objects like characters, items, and locations, and edges represent relationships or interactions between them. Graph algorithms are applied for tasks like pathfinding, AI behavior modeling, and game state analysis.

These are just a few examples of the wide-ranging applications of graphs in various fields. The flexibility and power of graph algorithms make them indispensable tools for solving complex problems across domains.

### 1. Algorithms & Data Structures (C++): Graph Algorithms: Bellman Ford Algorithm

The Bellman-Ford algorithm is a popular algorithm used for finding the shortest paths from a single source vertex to all other vertices in a weighted graph, even in the presence of negative weight edges, as long as there are no negative weight cycles reachable from the source vertex. Here's how it works:

1. Initialize distances: Set the distance to the source vertex to 0, and set the distance to all other vertices to infinity.
2. Relax edges: Iterate over all edges in the graph and relax each edge. Relaxing an edge means attempting to improve the shortest path to the destination vertex using the current shortest path to the source vertex and the weight of the edge.
3. Repeat relaxation: Repeat step 2 for |V| - 1 times, where |V| is the number of vertices in the graph. This ensures that the shortest paths are found even in the presence of negative weight edges, as the longest possible shortest path in a graph with |V| vertices is of length |V| - 1.
4. Check for negative weight cycles: After performing |V| - 1 iterations of relaxation, if there are still improvements to be made to the distances, then there must be a negative weight cycle in the graph reachable from the source vertex.

Here's a C++ implementation of the Bellman-Ford algorithm:

```cpp
#include <iostream>
#include <vector>
#include <limits>

using namespace std;

struct Edge {
    int source, destination, weight;
};

void bellmanFord(vector<Edge>& edges, int numVertices, int source) {
    vector<int> distance(numVertices, numeric_limits<int>::max());
    distance[source] = 0;

    for (int i = 0; i < numVertices - 1; ++i) {
        for (const auto& edge : edges) {
            if (distance[edge.source] != numeric_limits<int>::max() &&
                distance[edge.source] + edge.weight < distance[edge.destination]) {
                distance[edge.destination] = distance[edge.source] + edge.weight;
            }
        }
    }

    // Check for negative weight cycles
    for (const auto& edge : edges) {
        if (distance[edge.source] != numeric_limits<int>::max() &&
            distance[edge.source] + edge.weight < distance[edge.destination]) {
            cout << "Graph contains negative weight cycle reachable from source vertex." << endl;
            return;
        }
    }

    // Print shortest distances
    cout << "Shortest distances from source vertex " << source << ":" << endl;
    for (int i = 0; i < numVertices; ++i) {
        cout << "Vertex " << i << ": " << distance[i] << endl;
    }
}

int main() {
    int numVertices = 5;
    int source = 0; // Source vertex

    // Example graph
    vector<Edge> edges = {
        {0, 1, -1},
        {0, 2, 4},
        {1, 2, 3},
        {1, 3, 2},
        {1, 4, 2},
        {3, 2, 5},
        {3, 1, 1},
        {4, 3, -3}
    };

    bellmanFord(edges, numVertices, source);

    return 0;
}
```

This code demonstrates the Bellman-Ford algorithm with an example graph. You can modify the `edges` vector to represent your own graph.

### 1. Algorithms & Data Structures (C++): Graph Algorithms: Bellman-Ford Algorithm

The Bellman-Ford algorithm is a popular algorithm used to find the shortest paths from a source vertex to all other vertices in a weighted graph. It can handle graphs with negative edge weights and detect negative cycles. Here's a basic explanation of the algorithm along with a C++ implementation:

### Algorithm Explanation

1. **Initialization:** Initialize distances from the source vertex to all other vertices as INFINITY and to itself as 0.
2. **Relaxation:** Relax all edges (v, u) one by one. A relaxation step updates the distance of u if we find a shorter path from the source to u through v.
3. **Repeat:** Repeat the relaxation step for |V| - 1 times where |V| is the number of vertices in the graph. This ensures that the shortest paths are calculated accurately.
4. **Negative Cycle Detection:** After |V| - 1 iterations, if there's still a vertex that can be relaxed, then there exists a negative cycle in the graph.

### C++ Implementation

```cpp
#include <iostream>
#include <vector>
#include <limits>

using namespace std;

#define INF numeric_limits<int>::max()

// Graph edge structure
struct Edge {
    int src, dest, weight;
};

// Bellman-Ford algorithm function
void bellmanFord(vector<Edge>& edges, int V, int E, int src) {
    vector<int> dist(V, INF); // Initialize distances from src to all other vertices as INF
    dist[src] = 0; // Distance from src to itself is 0
    
    // Relax all edges V-1 times
    for (int i = 0; i < V - 1; ++i) {
        for (int j = 0; j < E; ++j) {
            int u = edges[j].src;
            int v = edges[j].dest;
            int weight = edges[j].weight;
            if (dist[u] != INF && dist[u] + weight < dist[v])
                dist[v] = dist[u] + weight;
        }
    }
    
    // Check for negative cycles
    for (int i = 0; i < E; ++i) {
        int u = edges[i].src;
        int v = edges[i].dest;
        int weight = edges[i].weight;
        if (dist[u] != INF && dist[u] + weight < dist[v]) {
            cout << "Graph contains negative cycle!" << endl;
            return;
        }
    }
    
    // Print shortest distances
    cout << "Vertex   Distance from Source" << endl;
    for (int i = 0; i < V; ++i)
        cout << i << "\t\t" << dist[i] << endl;
}

int main() {
    int V, E;
    cout << "Enter number of vertices and edges: ";
    cin >> V >> E;
    
    vector<Edge> edges(E);
    cout << "Enter source, destination, and weight for each edge:" << endl;
    for (int i = 0; i < E; ++i)
        cin >> edges[i].src >> edges[i].dest >> edges[i].weight;
    
    int src;
    cout << "Enter source vertex: ";
    cin >> src;
    
    bellmanFord(edges, V, E, src);
    
    return 0;
}
```

### Example Input

```bash
Number of vertices and edges: 5 8
Edges:
0 1 -1
0 2 4
1 2 3
1 3 2
1 4 2
3 2 5
3 1 1
4 3 -3
Source vertex: 0
```

### Output

```bash
Vertex   Distance from Source
0       0
1       -1
2       2
3       -2
4       1
```

This implementation calculates the shortest distances from the source vertex (0 in this case) to all other vertices in the given graph.

### 1. Algorithms & Data Structures (C++): Graph Algorithms: Bellman-Ford algorithm implementation

Sure! Here's a basic implementation of the Bellman-Ford algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <limits>

using namespace std;

struct Edge {
    int source, destination, weight;
};

void BellmanFord(vector<Edge>& edges, int numVertices, int source) {
    vector<int> distance(numVertices, numeric_limits<int>::max());
    distance[source] = 0;

    // Relax all edges numVertices - 1 times
    for (int i = 1; i < numVertices; ++i) {
        for (const auto& edge : edges) {
            if (distance[edge.source] != numeric_limits<int>::max() &&
                distance[edge.source] + edge.weight < distance[edge.destination]) {
                distance[edge.destination] = distance[edge.source] + edge.weight;
            }
        }
    }

    // Check for negative weight cycles
    for (const auto& edge : edges) {
        if (distance[edge.source] != numeric_limits<int>::max() &&
            distance[edge.source] + edge.weight < distance[edge.destination]) {
            cout << "Graph contains negative weight cycle\n";
            return;
        }
    }

    // Print the shortest distances
    cout << "Vertex   Distance from Source\n";
    for (int i = 0; i < numVertices; ++i) {
        cout << i << "\t\t" << distance[i] << "\n";
    }
}

int main() {
    vector<Edge> edges = {
        {0, 1, 6}, {0, 2, 7}, {1, 2, 8}, {1, 3, 5},
        {1, 4, -4}, {2, 3, -3}, {2, 4, 9}, {3, 1, -2},
        {4, 0, 2}, {4, 3, 7}
    };

    int numVertices = 5; // Number of vertices in the graph
    int source = 0; // Source vertex

    BellmanFord(edges, numVertices, source);

    return 0;
}
```

This implementation assumes that the graph is represented using a vector of edges. Each edge has a source, destination, and weight. The `BellmanFord` function calculates the shortest distances from the source vertex to all other vertices using the Bellman-Ford algorithm. If the graph contains a negative weight cycle, it will detect and report it. Finally, it prints the shortest distances from the source vertex to all other vertices.

### 1. Algorithms & Data Structures (C++): Graph Algorithms: Bellman-Ford algorithm visualisation

Visualizing the Bellman-Ford algorithm can be really helpful for understanding how it works. Here's a basic outline of how you could visualize it in C++:

1. **Graph Representation**: Start by representing your graph. You can use an adjacency list or matrix to represent the graph.

2. **Edge Structure**: Define a structure to represent edges of the graph. Each edge should have a source, destination, and weight.

3. **Bellman-Ford Function**: Write a function to implement the Bellman-Ford algorithm. This function will take the graph and the source vertex as input and return the shortest distances from the source vertex to all other vertices.

4. **Visualization**: Use libraries like Graphviz to visualize the graph and highlight the vertices and edges that are being processed by the algorithm at each step.

Here's a simplified example of how you might implement this in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Structure to represent an edge
struct Edge {
    int source, destination, weight;
};

// Function to implement Bellman-Ford algorithm
void bellmanFord(vector<Edge>& edges, int numVertices, int source) {
    // Initialize distances from source to all other vertices as infinite
    vector<int> distance(numVertices, INT_MAX);
    distance[source] = 0;

    // Relax all edges |V| - 1 times
    for (int i = 0; i < numVertices - 1; ++i) {
        for (const auto& edge : edges) {
            int u = edge.source;
            int v = edge.destination;
            int weight = edge.weight;
            if (distance[u] != INT_MAX && distance[u] + weight < distance[v]) {
                distance[v] = distance[u] + weight;
            }
        }
    }

    // Check for negative-weight cycles
    for (const auto& edge : edges) {
        int u = edge.source;
        int v = edge.destination;
        int weight = edge.weight;
        if (distance[u] != INT_MAX && distance[u] + weight < distance[v]) {
            cout << "Graph contains negative-weight cycle\n";
            return;
        }
    }

    // Print shortest distances
    cout << "Vertex\tDistance from Source\n";
    for (int i = 0; i < numVertices; ++i) {
        cout << i << "\t" << distance[i] << "\n";
    }
}

int main() {
    // Example graph
    vector<Edge> edges = {
        {0, 1, 4}, {0, 2, 8}, {1, 2, -3}, {1, 3, 6}, {2, 3, 9}
    };
    int numVertices = 4; // Number of vertices in the graph
    int source = 0; // Source vertex

    // Call Bellman-Ford algorithm
    bellmanFord(edges, numVertices, source);

    return 0;
}
```

This code doesn't include visualization; you would need to integrate a library like Graphviz to visualize the graph and the algorithm's progress.

### 1. Algorithms & Data Structures (C++): Graph Algorithms: Breadth-First Search

Breadth-First Search (BFS) is a fundamental graph traversal algorithm that explores all the vertices in a graph at a given depth before moving on to the vertices at the next depth level. It operates on graphs with or without weights and can be used to find shortest paths, solve puzzles, or traverse trees.

Here's a basic implementation of BFS in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

// Graph class representing an undirected graph using adjacency list representation
class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V), adj(V) {}

    // Function to add an edge to the graph
    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u); // Assuming an undirected graph
    }

    // Breadth First Search traversal starting from given vertex
    void BFS(int start) {
        // Mark all the vertices as not visited
        vector<bool> visited(V, false);

        // Create a queue for BFS
        queue<int> q;

        // Mark the current node as visited and enqueue it
        visited[start] = true;
        q.push(start);

        while (!q.empty()) {
            // Dequeue a vertex from queue and print it
            int u = q.front();
            cout << u << " ";
            q.pop();

            // Get all adjacent vertices of the dequeued vertex u
            // If an adjacent vertex has not been visited, then mark it
            // visited and enqueue it
            for (int v : adj[u]) {
                if (!visited[v]) {
                    visited[v] = true;
                    q.push(v);
                }
            }
        }
    }
};

int main() {
    // Create a graph given in the example
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 3);

    cout << "Breadth First Traversal (starting from vertex 0): ";
    g.BFS(0);

    return 0;
}
```

In this code:

- The `Graph` class represents an undirected graph using an adjacency list.
- The `addEdge` function is used to add edges between vertices.
- The `BFS` function performs breadth-first search traversal starting from a given vertex.
- In the `main` function, a graph is created and edges are added to it. Then, BFS is called with a starting vertex.

This code demonstrates a basic BFS traversal in C++. You can modify it as needed for your specific use case or graph representation.

### 1. Algorithms & Data Structures (C++): Graph Algorithms: Breadth-first search implementation

Breadth-First Search (BFS) is a fundamental graph traversal algorithm that explores all the vertices in a graph, starting from a chosen source vertex and moving systematically through the graph by exploring all the vertices at the present depth before moving on to the vertices at the next depth level.

Here's a simple implementation of BFS in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

// Graph class representing an undirected graph using adjacency list representation
class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list representation

public:
    Graph(int V) : V(V), adj(V) {}

    // Function to add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w);
        adj[w].push_back(v); // Assuming undirected graph
    }

    // Function to perform BFS traversal
    void BFS(int source) {
        // Mark all vertices as not visited
        vector<bool> visited(V, false);

        // Create a queue for BFS
        queue<int> q;

        // Mark the current node as visited and enqueue it
        visited[source] = true;
        q.push(source);

        while (!q.empty()) {
            // Dequeue a vertex from queue and print it
            int currentVertex = q.front();
            cout << currentVertex << " ";
            q.pop();

            // Get all adjacent vertices of the dequeued vertex currentVertex
            // If an adjacent has not been visited, mark it visited and enqueue it
            for (int adjacent : adj[currentVertex]) {
                if (!visited[adjacent]) {
                    visited[adjacent] = true;
                    q.push(adjacent);
                }
            }
        }
    }
};

int main() {
    // Create a graph
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 3);

    cout << "Breadth First Traversal (starting from vertex 0): ";
    g.BFS(0);

    return 0;
}
```

In this code:

- The `Graph` class represents an undirected graph using an adjacency list.
- The `addEdge` method adds an edge between two vertices.
- The `BFS` method performs the Breadth-First Search traversal starting from a given source vertex.
- Inside the `BFS` method, a queue is used to keep track of the vertices to be visited next. The algorithm starts from the source vertex, marks it as visited, and enqueues it. Then, while the queue is not empty, it dequeues a vertex, prints it, and enqueues all its unvisited adjacent vertices.

You can customize the graph by adding or removing edges in the `main` function and change the source vertex for traversal in the `BFS` function call.

### 1. Algorithms & Data Structures (C++): Graph Algorithms: Depth-First Search

Depth-First Search (DFS) is a fundamental algorithm for traversing or searching tree or graph data structures. It starts at a designated node (often called the "source" or "root" node) and explores as far as possible along each branch before backtracking.

In C++, you can implement DFS using either recursion or iteration (using a stack). Here's a basic implementation of DFS using recursion for a graph represented using an adjacency list:

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>

using namespace std;

// Depth-First Search function
void DFS(int node, vector<vector<int>>& graph, vector<bool>& visited) {
    visited[node] = true;
    cout << node << " "; // Printing the node being visited

    for (int neighbor : graph[node]) {
        if (!visited[neighbor]) {
            DFS(neighbor, graph, visited);
        }
    }
}

int main() {
    int n = 6; // Number of nodes
    vector<vector<int>> graph(n);

    // Add edges to the graph (undirected graph)
    graph[0].push_back(1);
    graph[0].push_back(2);
    graph[1].push_back(3);
    graph[1].push_back(4);
    graph[2].push_back(5);

    vector<bool> visited(n, false);

    // Start DFS from node 0
    cout << "Depth-First Search starting from node 0:\n";
    DFS(0, graph, visited);
    cout << endl;

    return 0;
}
```

This code demonstrates DFS starting from node 0 in a graph with 6 nodes. It assumes the graph is represented using an adjacency list. You can modify the `main` function to start DFS from any other node by changing the parameter passed to the `DFS` function.

Remember, DFS can be used for many graph-related tasks, such as finding connected components, detecting cycles, and solving maze problems.

### 1. Algorithms & Data Structures (C++): Graph Algorithms: Depth-first search and stack memory visualisation

Depth-first search (DFS) is a fundamental graph traversal algorithm used to explore nodes and edges of a graph. It starts at a selected node (often called the "source" or "root" node) and explores as far as possible along each branch before backtracking.

To visualize the stack memory usage during DFS in C++, you can implement DFS recursively and print the state of the stack at each recursive call. Here's a simple example of how you might do this:

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

// A utility function to add an edge in an undirected graph
void addEdge(vector<int> adj[], int u, int v) {
    adj[u].push_back(v);
    adj[v].push_back(u); // assuming undirected graph
}

// Recursive function to perform DFS
void DFSUtil(vector<int> adj[], int v, vector<bool>& visited, stack<int>& Stack) {
    // Mark the current node as visited
    visited[v] = true;

    // Print current vertex
    cout << v << " ";

    // Recur for all the vertices adjacent to this vertex
    for (int u : adj[v]) {
        if (!visited[u]) {
            // Push the current node onto the stack
            Stack.push(u);
            // Recur for next vertex
            DFSUtil(adj, u, visited, Stack);
        }
    }
}

// The function to do DFS traversal. It uses recursive DFSUtil()
void DFS(vector<int> adj[], int V, int start) {
    vector<bool> visited(V, false); // Mark all the vertices as not visited
    stack<int> Stack;

    // Call the recursive helper function to print DFS traversal
    DFSUtil(adj, start, visited, Stack);

    // Continue DFS from non-visited vertices (in case of disconnected graph)
    for (int i = 0; i < V; ++i) {
        if (!visited[i]) {
            DFSUtil(adj, i, visited, Stack);
        }
    }
}

int main() {
    // Create a graph given in the example
    int V = 5;
    vector<int> adj[V];
    addEdge(adj, 0, 1);
    addEdge(adj, 0, 2);
    addEdge(adj, 1, 3);
    addEdge(adj, 1, 4);

    cout << "Depth First Traversal (starting from vertex 0): ";
    DFS(adj, V, 0);
    cout << endl;

    return 0;
}
```

In this example, `DFSUtil` is a recursive function that performs the actual DFS traversal. Inside `DFSUtil`, the stack is used to keep track of the nodes to be visited next. At each step of the recursion, the current node is pushed onto the stack, and then DFS is called recursively for its adjacent nodes. When backtracking occurs (i.e., when there are no more unvisited adjacent nodes), the node is popped from the stack.

By printing the elements of the stack at each step of the recursion, you can visualize the stack memory usage during DFS traversal.

### 1. Algorithms & Data Structures (C++): Graph Algorithms: Depth-first search implementation

Sure, here's a basic implementation of Depth-first Search (DFS) for graphs in C++:

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

// Graph class
class Graph {
    int V; // number of vertices
    vector<vector<int>> adj; // adjacency list

public:
    Graph(int V) {
        this->V = V;
        adj.resize(V);
    }

    // function to add an edge to graph
    void addEdge(int v, int w) {
        adj[v].push_back(w);
    }

    // Depth First Search traversal
    void DFS(int start) {
        // array to keep track of visited vertices
        vector<bool> visited(V, false);
        
        // stack for DFS traversal
        stack<int> stack;
        
        // push the start vertex onto the stack
        stack.push(start);
        
        // mark the start vertex as visited
        visited[start] = true;

        cout << "Depth First Traversal: ";
        
        while (!stack.empty()) {
            // pop a vertex from stack and print it
            int current = stack.top();
            cout << current << " ";
            stack.pop();

            // Get all adjacent vertices of the popped vertex.
            // If an adjacent has not been visited, then push it to the stack.
            for (auto it = adj[current].begin(); it != adj[current].end(); ++it) {
                if (!visited[*it]) {
                    stack.push(*it);
                    visited[*it] = true;
                }
            }
        }
    }
};

// Driver program to test DFS
int main() {
    Graph g(5);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(2, 4);
    g.addEdge(3, 4);

    cout << "Following is Depth First Traversal "
            "(starting from vertex 0) \n";
    g.DFS(0);

    return 0;
}
```

This implementation uses a stack to keep track of vertices to visit next. It starts from a given vertex, marks it as visited, and then iterates through its adjacent vertices. If any adjacent vertex is not visited, it is pushed onto the stack, and the process continues until the stack is empty.

### 1. Algorithms & Data Structures (C++): Graph Algorithms: Dijkstra algorithm implementation

Certainly! Here's a basic implementation of Dijkstra's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>

using namespace std;

// Define infinity as a large value
const int INF = numeric_limits<int>::max();

// Define a structure to represent a weighted edge in the graph
struct Edge {
    int to;
    int weight;
    Edge(int t, int w) : to(t), weight(w) {}
};

// Define a structure to represent a vertex in the graph
struct Vertex {
    int id;
    int distance;
    Vertex(int i, int d) : id(i), distance(d) {}
};

// Define a custom comparator for vertices in priority queue
struct VertexComparator {
    bool operator()(const Vertex& v1, const Vertex& v2) const {
        return v1.distance > v2.distance;
    }
};

// Dijkstra's algorithm function
vector<int> dijkstra(const vector<vector<Edge>>& graph, int source) {
    int n = graph.size(); // Number of vertices
    vector<int> distances(n, INF); // Initialize distances to infinity
    priority_queue<Vertex, vector<Vertex>, VertexComparator> pq;
    
    distances[source] = 0; // Distance from source to itself is 0
    pq.push(Vertex(source, 0)); // Push source vertex to priority queue
    
    while (!pq.empty()) {
        Vertex curr = pq.top();
        pq.pop();
        
        // Iterate through all adjacent vertices of current vertex
        for (const Edge& edge : graph[curr.id]) {
            int newDistance = curr.distance + edge.weight;
            // Update distance if newDistance is shorter
            if (newDistance < distances[edge.to]) {
                distances[edge.to] = newDistance;
                pq.push(Vertex(edge.to, newDistance));
            }
        }
    }
    
    return distances;
}

int main() {
    // Example graph representation
    int numVertices = 6;
    vector<vector<Edge>> graph(numVertices);
    // Add edges to the graph
    graph[0].push_back(Edge(1, 5));
    graph[0].push_back(Edge(2, 3));
    graph[1].push_back(Edge(3, 6));
    graph[1].push_back(Edge(2, 2));
    graph[2].push_back(Edge(4, 4));
    graph[2].push_back(Edge(5, 2));
    graph[2].push_back(Edge(3, 7));
    graph[3].push_back(Edge(4, -1));
    graph[3].push_back(Edge(5, 1));
    graph[4].push_back(Edge(5, -2));

    // Run Dijkstra's algorithm from vertex 0
    vector<int> distances = dijkstra(graph, 0);

    // Output the shortest distances from vertex 0 to all other vertices
    cout << "Shortest distances from vertex 0:\n";
    for (int i = 0; i < numVertices; ++i) {
        cout << "Vertex " << i << ": " << distances[i] << endl;
    }

    return 0;
}
```

This code implements Dijkstra's algorithm to find the shortest paths from a single source vertex to all other vertices in a weighted graph. The graph is represented using an adjacency list. The `dijkstra` function takes the graph and the source vertex as input and returns a vector containing the shortest distances from the source vertex to all other vertices. Finally, in the `main` function, an example graph is constructed, and Dijkstra's algorithm is executed from vertex 0. The shortest distances are then printed out.

### 1. Algorithms & Data Structures (C++): Graph Algorithms: Dijkstra algorithm visualization

Visualizing Dijkstra's algorithm can greatly aid in understanding how it works. Here's a high-level overview of how you might go about visualizing it:

1. **Graph Representation**: Start by representing your graph. You can do this using an adjacency list or adjacency matrix. For visualization purposes, an adjacency list might be more intuitive.

2. **Visualization Framework**: Choose a framework or library to help with visualization. Popular choices for C++ include SFML, OpenGL, or even simple console-based output.

3. **Node and Edge Rendering**: Implement rendering functions to display nodes and edges of the graph. Each node could be represented as a circle or a square, and edges as lines connecting them.

4. **Dijkstra's Algorithm Implementation**: Implement Dijkstra's algorithm. As the algorithm progresses, mark nodes as visited, display the shortest path found so far, and update the distances from the source node.

5. **Animation and Interaction**: Add animation to show how the algorithm progresses. You could highlight the current node being visited, display the tentative distances, and update them as the algorithm progresses. Allow for user interaction to start the algorithm, pause, or step through it.

6. **Final Path Highlighting**: Once the algorithm completes, highlight the shortest path from the source node to the destination node.

Here's a simple pseudocode representation of Dijkstra's algorithm:

```plaintext
function Dijkstra(Graph, source):
    dist[source] = 0
    create vertex set Q

    for each vertex v in Graph:
        if v ≠ source:
            dist[v] = INFINITY
        add v to Q

    while Q is not empty:
        u = vertex in Q with min dist[u]
        remove u from Q

        for each neighbor v of u:
            alt = dist[u] + length(u, v)
            if alt < dist[v]:
                dist[v] = alt
                prev[v] = u

    return dist[], prev[]
```

In your visualization, you would show the current `dist` values and `prev` pointers for each node as the algorithm progresses, updating them whenever a shorter path is found.

Remember to encapsulate your code properly, separating concerns between the visualization logic and the algorithm itself. This makes your code more modular and easier to maintain.

### 1. Algorithms & Data Structures (C++): Breadth First Search Implementation

Sure, here's a simple implementation of Breadth First Search (BFS) in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

// Graph class
class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V) {
        adj.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w); // Add w to v’s list
    }

    // Breadth First Search
    void BFS(int start) {
        // Mark all the vertices as not visited
        vector<bool> visited(V, false);

        // Create a queue for BFS
        queue<int> q;

        // Mark the current node as visited and enqueue it
        visited[start] = true;
        q.push(start);

        while (!q.empty()) {
            // Dequeue a vertex from queue and print it
            int current = q.front();
            cout << current << " ";
            q.pop();

            // Get all adjacent vertices of the dequeued vertex current.
            // If an adjacent has not been visited, then mark it visited and enqueue it
            for (int i : adj[current]) {
                if (!visited[i]) {
                    visited[i] = true;
                    q.push(i);
                }
            }
        }
    }
};

int main() {
    // Create a graph
    Graph g(6);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 4);
    g.addEdge(3, 4);
    g.addEdge(3, 5);
    g.addEdge(4, 5);

    cout << "BFS traversal starting from vertex 0: ";
    g.BFS(0);

    return 0;
}
```

In this implementation, we have a `Graph` class that represents a graph using adjacency lists. The `addEdge` function adds an edge between two vertices. The `BFS` function performs the Breadth First Search traversal starting from a given vertex. We use a `queue` to keep track of the vertices to visit next.

### 1. Algorithms & Data Structures (C++): Breadth First Search in Graph

Breadth-First Search (BFS) is a fundamental graph traversal algorithm used to explore nodes in a graph. It starts at a chosen node and explores all of its neighbors at the current depth level before moving on to the nodes at the next depth level. Here's a simple implementation of BFS in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

// Graph class representing an undirected graph using adjacency lists
class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V), adj(V) {}

    // Function to add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w); // Add w to v's list
        adj[w].push_back(v); // Add v to w's list (for undirected graph)
    }

    // BFS traversal from a given source vertex
    void BFS(int s) {
        // Mark all the vertices as not visited
        vector<bool> visited(V, false);

        // Create a queue for BFS
        queue<int> queue;

        // Mark the current node as visited and enqueue it
        visited[s] = true;
        queue.push(s);

        // 'i' will be used to get all adjacent vertices of a vertex
        vector<int>::iterator i;

        while (!queue.empty()) {
            // Dequeue a vertex from the queue and print it
            s = queue.front();
            cout << s << " ";
            queue.pop();

            // Get all adjacent vertices of the dequeued vertex s
            // If an adjacent vertex has not been visited, mark it visited and enqueue it
            for (i = adj[s].begin(); i != adj[s].end(); ++i) {
                if (!visited[*i]) {
                    visited[*i] = true;
                    queue.push(*i);
                }
            }
        }
    }
};

int main() {
    // Create a graph given in the example
    Graph g(6);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(2, 4);
    g.addEdge(2, 5);

    cout << "Breadth First Traversal (starting from vertex 0): ";
    g.BFS(0);

    return 0;
}
```

This code demonstrates BFS traversal starting from vertex 0 in a graph with 6 vertices. You can modify the `main()` function to create your own graph and specify the starting vertex for the BFS traversal.

### 1. Algorithms & Data Structures (C++): Breadth First Search in Graphs

Breadth-First Search (BFS) is an algorithm used for traversing or searching tree or graph data structures. It explores all the neighboring nodes at the present depth before moving on to the nodes at the next depth level. BFS is typically implemented using a queue data structure.

Here's a basic implementation of BFS in C++ for graphs represented using an adjacency list:

```cpp
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

// Graph class representing the graph using adjacency list
class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) {
        this->V = V;
        adj.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w); // Add w to v’s list
    }

    // BFS traversal from a given source vertex
    void BFS(int s) {
        // Mark all the vertices as not visited
        vector<bool> visited(V, false);

        // Create a queue for BFS
        queue<int> q;

        // Mark the current node as visited and enqueue it
        visited[s] = true;
        q.push(s);

        while (!q.empty()) {
            // Dequeue a vertex from queue and print it
            s = q.front();
            cout << s << " ";
            q.pop();

            // Get all adjacent vertices of the dequeued vertex s.
            // If an adjacent vertex has not been visited, then mark it
            // visited and enqueue it
            for (auto i = adj[s].begin(); i != adj[s].end(); ++i) {
                if (!visited[*i]) {
                    visited[*i] = true;
                    q.push(*i);
                }
            }
        }
    }
};

int main() {
    // Create a graph given in the example
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "Breadth First Traversal (starting from vertex 2):\n";
    g.BFS(2);

    return 0;
}
```

In this implementation:

- `Graph` class represents the graph using an adjacency list.
- `addEdge` function is used to add an edge between two vertices.
- `BFS` function performs the Breadth-First Search traversal starting from a given source vertex `s`.
- Inside `BFS`, a queue `q` is used to keep track of nodes to visit next.
- The `visited` array is used to mark visited nodes to avoid cycles.

You can modify this code according to your requirements and the specific representation of your graph.

### 1. Algorithms & Data Structures (C++): Breadth First Search in Undirected Graphs : Finding Connected Components

Sure, let's delve into implementing Breadth First Search (BFS) to find connected components in an undirected graph using C++. First, we need to define the Graph class and the BFS function.

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V), adj(V) {}

    void addEdge(int v, int w) {
        adj[v].push_back(w);
        adj[w].push_back(v); // Undirected graph
    }

    void BFS(int start, vector<bool>& visited) {
        queue<int> q;
        q.push(start);
        visited[start] = true;

        while (!q.empty()) {
            int v = q.front();
            q.pop();
            cout << v << " ";

            for (int u : adj[v]) {
                if (!visited[u]) {
                    visited[u] = true;
                    q.push(u);
                }
            }
        }
    }

    int connectedComponents() {
        vector<bool> visited(V, false);
        int components = 0;

        for (int v = 0; v < V; ++v) {
            if (!visited[v]) {
                cout << "Connected component " << components + 1 << ": ";
                BFS(v, visited);
                cout << endl;
                components++;
            }
        }

        return components;
    }
};

int main() {
    Graph g(6); // Create a graph with 6 vertices

    // Add edges
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(3, 4);

    cout << "Number of connected components: " << g.connectedComponents() << endl;

    return 0;
}
```

This code defines a `Graph` class that represents an undirected graph using an adjacency list. The `addEdge` function is used to add edges to the graph. The `BFS` function performs Breadth First Search traversal starting from a given vertex. The `connectedComponents` function finds all connected components in the graph by performing BFS from each unvisited vertex.

In the `main` function, an example graph with 6 vertices and some edges is created and `connectedComponents` is called to find the number of connected components in the graph and print them out.

### 1. Algorithms & Data Structures (C++): Breadth First Search Over Binary Weighted Graphs

Sure! Breadth First Search (BFS) is a fundamental algorithm for traversing or searching tree or graph data structures. It explores all the neighbor nodes at the present depth before moving on to the nodes at the next depth level. In the context of a binary weighted graph, BFS can be applied to find the shortest path from a source node to a destination node, provided the graph is unweighted or the edges have uniform weights.

Here's how you can implement BFS over a binary weighted graph in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

// Structure to represent a node in the graph
struct Node {
    int value;
    vector<Node*> neighbors;
    bool visited;

    Node(int val) : value(val), visited(false) {}
};

// Function to perform Breadth First Search on the graph
void BFS(Node* start) {
    if (start == nullptr)
        return;

    queue<Node*> q;
    start->visited = true;
    q.push(start);

    while (!q.empty()) {
        Node* current = q.front();
        q.pop();
        cout << current->value << " ";

        // Traverse all the neighbors of the current node
        for (Node* neighbor : current->neighbors) {
            if (!neighbor->visited) {
                neighbor->visited = true;
                q.push(neighbor);
            }
        }
    }
}

int main() {
    // Creating nodes
    Node* node1 = new Node(1);
    Node* node2 = new Node(2);
    Node* node3 = new Node(3);
    Node* node4 = new Node(4);
    Node* node5 = new Node(5);

    // Constructing the binary weighted graph
    node1->neighbors = {node2, node3};
    node2->neighbors = {node4};
    node3->neighbors = {node4, node5};
    node4->neighbors = {};
    node5->neighbors = {};

    cout << "BFS traversal starting from node 1: ";
    BFS(node1);

    // Memory cleanup
    delete node1;
    delete node2;
    delete node3;
    delete node4;
    delete node5;

    return 0;
}
```

In this code:

- We define a `Node` structure to represent each node in the graph. Each node contains its value, a vector of neighbor nodes, and a boolean flag indicating whether the node has been visited during traversal.
- The `BFS` function performs Breadth First Search starting from a given node. It uses a queue to keep track of nodes to visit next.
- In the `main` function, we construct a binary weighted graph with five nodes and edges connecting them as specified. Then, we call the `BFS` function starting from node 1 to perform the traversal.

This implementation demonstrates BFS traversal on a binary graph represented using adjacency lists.

### 1. Algorithms & Data Structures (C++): Breadth First Search to find No of Connected component

Sure, here's a C++ implementation of Breadth First Search (BFS) to find the number of connected components in an undirected graph:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

// Function to perform BFS traversal
void BFS(int node, vector<int> adj[], vector<bool>& visited) {
    queue<int> q;
    q.push(node);
    visited[node] = true;

    while (!q.empty()) {
        int curr = q.front();
        q.pop();

        for (int neighbor : adj[curr]) {
            if (!visited[neighbor]) {
                q.push(neighbor);
                visited[neighbor] = true;
            }
        }
    }
}

// Function to find the number of connected components
int countConnectedComponents(int n, vector<int> adj[]) {
    vector<bool> visited(n + 1, false);
    int connectedComponents = 0;

    for (int i = 1; i <= n; ++i) {
        if (!visited[i]) {
            BFS(i, adj, visited);
            connectedComponents++;
        }
    }

    return connectedComponents;
}

int main() {
    // Example graph representation (adjacency list)
    int n = 6; // Number of nodes
    vector<int> adj[n + 1];

    // Add edges
    adj[1].push_back(2);
    adj[2].push_back(1);
    adj[2].push_back(3);
    adj[3].push_back(2);
    adj[4].push_back(5);
    adj[5].push_back(4);
    adj[5].push_back(6);
    adj[6].push_back(5);

    // Find the number of connected components
    int numConnectedComponents = countConnectedComponents(n, adj);
    cout << "Number of connected components: " << numConnectedComponents << endl;

    return 0;
}
```

In this implementation:

1. The `BFS` function performs a breadth-first search traversal starting from a given node, marking all reachable nodes as visited.
2. The `countConnectedComponents` function iterates through all nodes of the graph. If a node has not been visited yet, it starts a BFS traversal from that node and increments the count of connected components.
3. In the `main` function, you can define the graph using an adjacency list representation and then call `countConnectedComponents` to find the number of connected components in the graph.

This code assumes that the graph is represented using an adjacency list. Each element of the `adj` vector represents a node, and the vector associated with each node contains the indices of nodes that are connected to it.

### 1. Algorithms & Data Structures (C++): Breadth First Search Traversal

Breadth First Search (BFS) is a fundamental algorithm used to traverse or search tree or graph data structures. It starts at a given node (often referred to as the "root" node), explores all of the neighbor nodes at the present depth prior to moving on to nodes at the next depth level.

Here's a basic implementation of BFS traversal in C++ for a graph represented using adjacency lists:

```cpp
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

// Graph class representing adjacency list
class Graph {
    int V; // Number of vertices

    // Array of vectors representing adjacency lists
    vector<int> *adj;

public:
    Graph(int V); // Constructor

    // Function to add an edge to the graph
    void addEdge(int v, int w);

    // Function to perform BFS traversal from a given source vertex
    void BFS(int s);
};

// Constructor to initialize the graph
Graph::Graph(int V) {
    this->V = V;
    adj = new vector<int>[V];
}

// Function to add an edge to the graph
void Graph::addEdge(int v, int w) {
    adj[v].push_back(w); // Add w to v’s list.
}

// Function to perform BFS traversal from a given source vertex
void Graph::BFS(int s) {
    // Mark all the vertices as not visited
    vector<bool> visited(V, false);

    // Create a queue for BFS
    queue<int> queue;

    // Mark the current node as visited and enqueue it
    visited[s] = true;
    queue.push(s);

    // 'i' will be used to get all adjacent vertices of a vertex
    while (!queue.empty()) {
        // Dequeue a vertex from queue and print it
        s = queue.front();
        cout << s << " ";
        queue.pop();

        // Get all adjacent vertices of the dequeued vertex s
        // If an adjacent vertex has not been visited, then mark it visited and enqueue it
        for (auto i = adj[s].begin(); i != adj[s].end(); ++i) {
            if (!visited[*i]) {
                visited[*i] = true;
                queue.push(*i);
            }
        }
    }
}

int main() {
    // Create a graph given in the example
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "Breadth First Traversal (starting from vertex 2): ";
    g.BFS(2);

    return 0;
}
```

In this implementation, the `Graph` class represents an undirected graph using an adjacency list. The `addEdge` function adds an edge between two vertices. The `BFS` function performs the BFS traversal from a given source vertex `s`. It uses a queue to keep track of the vertices to visit next.

When executed, this code will output the BFS traversal starting from a specified source vertex.

### 1. Algorithms & Data Structures (C++): Breadth First Search vs Depth First Search

Breadth First Search (BFS) and Depth First Search (DFS) are fundamental graph traversal algorithms used in computer science, particularly in the realm of algorithms and data structures. Here's a breakdown of each:

1. **Breadth First Search (BFS)**:
   - BFS explores nodes level by level starting from the root or any arbitrary node.
   - It visits all the nodes at the present depth level before moving on to the nodes at the next depth level.
   - It uses a queue data structure to keep track of the nodes to be explored next.
   - BFS is optimal for finding the shortest path in an unweighted graph, as it guarantees to find the shortest path between the starting point and any other reachable node.
   - BFS is typically used in scenarios such as finding the shortest path, testing bipartiteness, and finding connected components in an undirected graph.

2. **Depth First Search (DFS)**:
   - DFS explores as far as possible along each branch before backtracking.
   - It starts at the root or any arbitrary node and explores as far as possible along each branch before backtracking.
   - It uses a stack data structure (or recursion) to keep track of the nodes to be explored next.
   - DFS does not necessarily find the shortest path; it may get stuck in a long path and not explore other shorter paths.
   - DFS is used in scenarios such as topological sorting, finding connected components in a graph, and detecting cycles in a graph.

**Comparison**:

- **Space Complexity**: BFS generally requires more memory than DFS because BFS needs to store all the nodes at a given level in memory.
- **Time Complexity**: Both algorithms have the same time complexity — O(V + E), where V is the number of vertices and E is the number of edges. However, in practice, BFS may be faster in finding shortest paths in sparse graphs, while DFS may be faster in dense graphs.
- **Applications**: BFS is useful for finding the shortest path, while DFS is better suited for problems requiring exploring deep into the graph.

In C++, you can implement both algorithms using either iterative or recursive approaches, depending on the requirements of the problem and your preference. Each has its own strengths and weaknesses, so understanding when to use BFS or DFS is crucial for efficient problem-solving.

### 1. Algorithms & Data Structures (C++): Breadth First Search vs Dijkstra vs Bellman Ford

Breadth First Search (BFS), Dijkstra's algorithm, and Bellman-Ford algorithm are fundamental techniques in computer science for solving various graph-related problems. Here's a comparison of these algorithms:

1. **Breadth First Search (BFS)**:
   - BFS is a graph traversal algorithm that explores all the vertices in a graph at the current depth before moving to the vertices at the next depth level.
   - It works well for finding the shortest path in an unweighted graph.
   - BFS guarantees the shortest path in an unweighted graph because it explores nodes in order of their distance from the starting node.
   - However, BFS does not work well for weighted graphs since it doesn't take edge weights into account.

2. **Dijkstra's Algorithm**:
   - Dijkstra's algorithm is a single-source shortest path algorithm that works for both weighted and unweighted graphs.
   - It uses a priority queue (usually implemented with a min-heap) to greedily select the closest vertex to the source vertex.
   - Dijkstra's algorithm works by continually expanding the frontier of known vertices until it reaches the destination vertex.
   - It guarantees the shortest path from the source vertex to all other vertices in the graph when all edge weights are non-negative.
   - Dijkstra's algorithm doesn't work correctly if there are negative edge weights in the graph.

3. **Bellman-Ford Algorithm**:
   - Bellman-Ford is another single-source shortest path algorithm that can handle graphs with negative edge weights.
   - It iteratively relaxes the edges of the graph until it finds the shortest paths from the source vertex to all other vertices.
   - Bellman-Ford can detect negative cycles in a graph.
   - It guarantees finding the shortest path from the source vertex to all other vertices in the graph if there are no negative cycles reachable from the source vertex.
   - Bellman-Ford is slower than Dijkstra's algorithm, especially for graphs with non-negative edge weights, but it's more versatile due to its ability to handle negative edge weights.

In summary, BFS is suitable for unweighted graphs, Dijkstra's algorithm is suitable for finding the shortest path in weighted graphs with non-negative edge weights, and Bellman-Ford is suitable for graphs with negative edge weights and can detect negative cycles. The choice of algorithm depends on the specific characteristics of the graph and the requirements of the problem at hand.

### 1. Algorithms & Data Structures (C++): Breadth First Search vs Dijkstra vs Bellman Ford vs Floyd Warshall

Breadth First Search (BFS), Dijkstra's algorithm, Bellman-Ford algorithm, and Floyd-Warshall algorithm are all fundamental algorithms in computer science, particularly in the realm of graph theory and network analysis. Here's a brief comparison of each:

1. **Breadth First Search (BFS)**:
   - BFS is primarily used for traversing or searching tree or graph data structures.
   - It explores all the vertices at the present "depth" level before moving on to the vertices at the next depth level.
   - BFS is not designed to find the shortest path in weighted graphs, but it can be adapted to find the shortest unweighted path from a source node to all other nodes in a graph.
   - Time complexity: O(V + E), where V is the number of vertices and E is the number of edges.

2. **Dijkstra's Algorithm**:
   - Dijkstra's algorithm is used to find the shortest path from a source node to all other nodes in a weighted graph, where all edge weights are non-negative.
   - It maintains a set of vertices whose shortest distance from the source node is known and continually selects the vertex with the shortest distance to expand next.
   - Dijkstra's algorithm guarantees the shortest path when all edge weights are non-negative.
   - Time complexity: O((V + E) log V) with the use of a priority queue (with Fibonacci heap), or O(V^2) with an array-based implementation, where V is the number of vertices and E is the number of edges.

3. **Bellman-Ford Algorithm**:
   - Bellman-Ford algorithm is used to find the shortest path from a single source node to all other nodes in a weighted graph, even when edge weights can be negative.
   - It iteratively relaxes edges, updating the shortest distance estimates until convergence.
   - Bellman-Ford can detect negative weight cycles.
   - Time complexity: O(VE), where V is the number of vertices and E is the number of edges.

4. **Floyd-Warshall Algorithm**:
   - Floyd-Warshall algorithm is used to find the shortest paths between all pairs of vertices in a weighted graph, even when edge weights can be negative.
   - It uses dynamic programming to calculate the shortest paths between all pairs of vertices.
   - It's efficient for dense graphs (where the number of edges is close to V^2) but less efficient for sparse graphs.
   - Time complexity: O(V^3), where V is the number of vertices.

In summary, BFS is primarily used for unweighted graphs and traversal, Dijkstra's algorithm is for finding the shortest paths in weighted graphs with non-negative weights, Bellman-Ford algorithm is for weighted graphs with possibly negative weights and detection of negative cycles, and Floyd-Warshall algorithm is for finding shortest paths between all pairs of vertices in weighted graphs with possibly negative weights. Each algorithm has its own use cases and performance characteristics, and the choice depends on the specific requirements of the problem at hand.

### 1. Algorithms & Data Structures (C++): Breadth First Search: Code

Certainly! Here's a simple implementation of Breadth First Search (BFS) in C++ for a graph represented using an adjacency list:

```cpp
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

// Function to perform BFS traversal of the graph
void BFS(vector<vector<int>>& graph, int start) {
    int n = graph.size();
    vector<bool> visited(n, false); // Mark all vertices as not visited

    // Create a queue for BFS
    queue<int> bfsQueue;

    // Mark the current node as visited and enqueue it
    visited[start] = true;
    bfsQueue.push(start);

    while (!bfsQueue.empty()) {
        // Dequeue a vertex from queue and print it
        int currentVertex = bfsQueue.front();
        cout << currentVertex << " ";
        bfsQueue.pop();

        // Get all adjacent vertices of the dequeued vertex currentVertex
        // If an adjacent has not been visited, then mark it visited
        // and enqueue it
        for (int i = 0; i < graph[currentVertex].size(); ++i) {
            int adjVertex = graph[currentVertex][i];
            if (!visited[adjVertex]) {
                visited[adjVertex] = true;
                bfsQueue.push(adjVertex);
            }
        }
    }
}

int main() {
    // Example graph represented using an adjacency list
    vector<vector<int>> graph = {
        {1, 2},     // 0 is connected to 1 and 2
        {0, 2, 3},  // 1 is connected to 0, 2, and 3
        {0, 1, 4},  // 2 is connected to 0, 1, and 4
        {1},        // 3 is connected to 1
        {2}         // 4 is connected to 2
    };

    cout << "BFS Traversal starting from vertex 0: ";
    BFS(graph, 0); // Start BFS traversal from vertex 0

    return 0;
}
```

This code demonstrates BFS traversal starting from vertex 0 in a graph represented using an adjacency list. You can modify the `graph` vector to represent your own graph and change the starting vertex accordingly.

### 1. Algorithms & Data Structures (C++): Breadth First Traversal

Breadth-first traversal (BFS) is an algorithm for traversing or searching tree or graph data structures. It starts at the tree root (or some arbitrary node for a graph), and explores all the neighbor nodes at the present depth prior to moving on to the nodes at the next depth level.

In C++, you can implement BFS using a queue data structure to keep track of the nodes to be visited. Here's a basic example of BFS implementation for a graph represented using an adjacency list:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

// Function to perform Breadth First Traversal
void BFS(vector<vector<int>>& graph, int start) {
    vector<bool> visited(graph.size(), false);
    queue<int> q;
    
    // Mark the start node as visited and enqueue it
    visited[start] = true;
    q.push(start);
    
    while (!q.empty()) {
        // Dequeue a vertex from queue and print it
        int current = q.front();
        cout << current << " ";
        q.pop();
        
        // Get all adjacent vertices of the dequeued vertex current
        // If an adjacent vertex has not been visited, then mark it visited and enqueue it
        for (int i = 0; i < graph[current].size(); ++i) {
            int neighbor = graph[current][i];
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                q.push(neighbor);
            }
        }
    }
}

int main() {
    int numVertices = 6; // Number of vertices in the graph
    vector<vector<int>> graph(numVertices);

    // Add edges to the graph
    graph[0].push_back(1);
    graph[0].push_back(2);
    graph[1].push_back(3);
    graph[1].push_back(4);
    graph[2].push_back(4);
    graph[3].push_back(5);
    graph[4].push_back(5);

    cout << "Breadth First Traversal starting from vertex 0: ";
    BFS(graph, 0);

    return 0;
}
```

In this example:

- The graph is represented using an adjacency list.
- The `BFS` function takes the graph and the starting vertex as input and performs BFS traversal.
- It maintains a queue to keep track of the nodes to visit next.
- It marks nodes as visited to avoid processing them multiple times.

This code performs BFS traversal starting from vertex 0. You can modify it according to your specific graph representation and requirements.

### 1. Algorithms & Data Structures (C++): Breadth-First Traversal

Breadth-first traversal (BFS) is a fundamental algorithm for traversing or searching tree or graph data structures. It explores all the neighboring nodes at the present depth prior to moving on to the nodes at the next depth level. Here's how you can implement BFS in C++:

```cpp
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

// Graph class represents a directed graph using adjacency list representation
class Graph {
    int V;    // Number of vertices
    vector<int> *adj;    // Pointer to array containing adjacency lists

public:
    Graph(int V);    // Constructor
    void addEdge(int v, int w);    // Function to add an edge to graph
    void BFS(int s);    // BFS traversal from a given source s
};

Graph::Graph(int V) {
    this->V = V;
    adj = new vector<int>[V];
}

void Graph::addEdge(int v, int w) {
    adj[v].push_back(w);    // Add w to v’s list
}

void Graph::BFS(int s) {
    // Mark all the vertices as not visited
    vector<bool> visited(V, false);

    // Create a queue for BFS
    queue<int> queue;

    // Mark the current node as visited and enqueue it
    visited[s] = true;
    queue.push(s);

    while (!queue.empty()) {
        // Dequeue a vertex from queue and print it
        s = queue.front();
        cout << s << " ";
        queue.pop();

        // Get all adjacent vertices of the dequeued vertex s. If an adjacent has not been visited, then mark it visited and enqueue it
        for (auto i = adj[s].begin(); i != adj[s].end(); ++i) {
            if (!visited[*i]) {
                visited[*i] = true;
                queue.push(*i);
            }
        }
    }
}

// Driver program to test methods of graph class
int main() {
    // Create a graph given in the above diagram
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "Breadth First Traversal (starting from vertex 2): ";
    g.BFS(2);

    return 0;
}
```

In this code:

- `Graph` class represents the graph using an adjacency list.
- `addEdge` function is used to add an edge to the graph.
- `BFS` function performs the breadth-first traversal starting from the given source vertex `s`.
- `main` function demonstrates the usage of the `Graph` class by creating a graph and performing BFS traversal starting from vertex 2.

You can modify the `main` function to create your own graph and start BFS traversal from any vertex.

### 1. Algorithms & Data Structures (C++): breadthFirstSearch()

Sure! A `breadthFirstSearch()` algorithm is used to traverse or search a graph or tree data structure in a breadth-first manner. This means that it explores all the neighbor nodes at the present depth before moving on to the nodes at the next depth level.

Here's a basic implementation of the `breadthFirstSearch()` algorithm in C++ using a graph represented using an adjacency list:

```cpp
#include <iostream>
#include <queue>
#include <vector>
#include <unordered_set>

using namespace std;

// Graph class representing the graph using an adjacency list
class Graph {
    int V; // Number of vertices

    // Pointer to an array containing adjacency lists
    vector<vector<int>> adj;

public:
    Graph(int V); // Constructor

    // Function to add an edge to the graph
    void addEdge(int v, int w);

    // Breadth-first search starting from a given vertex
    void breadthFirstSearch(int s);
};

Graph::Graph(int V) {
    this->V = V;
    adj.resize(V);
}

void Graph::addEdge(int v, int w) {
    adj[v].push_back(w); // Add w to v’s list.
}

void Graph::breadthFirstSearch(int s) {
    // Mark all the vertices as not visited
    vector<bool> visited(V, false);

    // Create a queue for BFS
    queue<int> queue;

    // Mark the current node as visited and enqueue it
    visited[s] = true;
    queue.push(s);

    while (!queue.empty()) {
        // Dequeue a vertex from queue and print it
        s = queue.front();
        cout << s << " ";
        queue.pop();

        // Get all adjacent vertices of the dequeued vertex s
        // If an adjacent has not been visited, then mark it
        // visited and enqueue it
        for (auto i = adj[s].begin(); i != adj[s].end(); ++i) {
            if (!visited[*i]) {
                visited[*i] = true;
                queue.push(*i);
            }
        }
    }
}

// Test the BFS algorithm
int main() {
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "Breadth First Traversal (starting from vertex 2): ";
    g.breadthFirstSearch(2);

    return 0;
}
```

This code demonstrates how to perform a breadth-first search on a graph represented using an adjacency list. It starts the BFS from a specified starting vertex (in this case, vertex 2) and prints out the traversal order. You can modify the `main()` function to create a graph according to your requirements and start the BFS from any vertex.

### 1. Algorithms & Data Structures (C++): breadthFirstSearchRecursive()

Certainly! Implementing a breadth-first search (BFS) algorithm recursively in C++ can be a bit unconventional since BFS is typically implemented using iteration and a queue. However, it's possible to achieve a recursive solution with the help of auxiliary data structures like queues or lists. Here's a basic implementation of breadth-first search using recursion in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

// Define a simple graph node structure
struct Node {
    int data;
    vector<Node*> neighbors;
    bool visited;

    Node(int value) : data(value), visited(false) {}
};

// Function to add an edge between two nodes
void addEdge(Node* u, Node* v) {
    u->neighbors.push_back(v);
}

// Recursive Breadth-First Search function
void breadthFirstSearchRecursive(queue<Node*>& q) {
    if (q.empty())
        return;

    Node* current = q.front();
    q.pop();
    cout << current->data << " ";

    // Visit all unvisited neighbors
    for (Node* neighbor : current->neighbors) {
        if (!neighbor->visited) {
            neighbor->visited = true;
            q.push(neighbor);
        }
    }

    // Recursively continue BFS
    breadthFirstSearchRecursive(q);
}

// Wrapper function to initiate BFS from a starting node
void breadthFirstSearch(Node* start) {
    queue<Node*> q;
    start->visited = true;
    q.push(start);
    breadthFirstSearchRecursive(q);
}

int main() {
    // Create a simple graph
    Node* node1 = new Node(1);
    Node* node2 = new Node(2);
    Node* node3 = new Node(3);
    Node* node4 = new Node(4);
    Node* node5 = new Node(5);

    addEdge(node1, node2);
    addEdge(node1, node3);
    addEdge(node2, node4);
    addEdge(node3, node4);
    addEdge(node3, node5);

    // Perform BFS starting from node1
    cout << "BFS Traversal starting from node 1: ";
    breadthFirstSearch(node1);

    // Clean up dynamically allocated memory
    delete node1;
    delete node2;
    delete node3;
    delete node4;
    delete node5;

    return 0;
}
```

In this implementation:

- We define a basic structure for a graph node (`Node`) which contains the node's data, a list of its neighbors, and a boolean flag indicating whether the node has been visited during traversal.
- The `addEdge` function is used to create connections between nodes in the graph.
- The `breadthFirstSearchRecursive` function takes a queue of nodes as an argument and performs the BFS recursively. It pops a node from the queue, visits it, marks it as visited, and then recursively calls itself with the unvisited neighbors of the current node.
- The `breadthFirstSearch` function is a wrapper function that initiates the BFS traversal from a starting node. It initializes the queue with the starting node and calls the recursive BFS function.
- In the `main` function, we create a simple graph, initiate BFS from a starting node, and print the traversal sequence.

Remember to handle memory deallocation properly, especially when working with dynamic memory allocation (`new` and `delete`).

### 1. Algorithms & Data Structures (C++): Graph Algorithms: Dijkstra's Shortest Path Algorithm

Dijkstra's algorithm is a classic algorithm in computer science used to find the shortest path between nodes in a graph, which may represent, for example, road networks or computer networks. It works on graphs with non-negative edge weights and is efficient for finding the shortest path from a single source vertex to all other vertices in the graph.

Here's a basic overview of how Dijkstra's algorithm works:

1. **Initialization**: Assign a tentative distance value to every node. Set the distance to the source node as 0 and all other nodes as infinity.

2. **Selection of the Node with the Smallest Distance**: Choose the unvisited node with the smallest tentative distance and set it as the current node.

3. **Update Distances**: For each neighbor of the current node, calculate the tentative distance from the source node. Compare this value with the current assigned value, and update it if the new value is smaller.

4. **Mark Node as Visited**: Once all neighbors of the current node have been considered, mark the current node as visited.

5. **Repeat**: Select the unvisited node with the smallest tentative distance, and repeat steps 3 and 4 until all nodes have been visited.

6. **Optimization**: Dijkstra's algorithm can be optimized using a priority queue (min-heap) data structure to efficiently select the node with the smallest tentative distance.

Here's a basic implementation of Dijkstra's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>

using namespace std;

#define INF numeric_limits<int>::max()

typedef pair<int, int> pii; // (node, distance)

void dijkstra(vector<vector<pii>>& graph, int source) {
    int n = graph.size();
    vector<int> dist(n, INF);
    dist[source] = 0;
    
    priority_queue<pii, vector<pii>, greater<pii>> pq;
    pq.push({0, source});
    
    while (!pq.empty()) {
        int u = pq.top().second;
        int d = pq.top().first;
        pq.pop();
        
        if (d > dist[u]) continue;
        
        for (auto& neighbor : graph[u]) {
            int v = neighbor.first;
            int w = neighbor.second;
            if (dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;
                pq.push({dist[v], v});
            }
        }
    }
    
    // Print shortest distances from source
    for (int i = 0; i < n; ++i) {
        cout << "Distance from source to node " << i << ": ";
        if (dist[i] == INF)
            cout << "INF" << endl;
        else
            cout << dist[i] << endl;
    }
}

int main() {
    int n, m;
    cout << "Enter number of nodes and edges: ";
    cin >> n >> m;
    
    vector<vector<pii>> graph(n);
    cout << "Enter edges (node1 node2 weight):" << endl;
    for (int i = 0; i < m; ++i) {
        int u, v, w;
        cin >> u >> v >> w;
        graph[u].push_back({v, w});
        graph[v].push_back({u, w}); // For undirected graph
    }
    
    int source;
    cout << "Enter source node: ";
    cin >> source;
    
    dijkstra(graph, source);
    
    return 0;
}
```

This code takes input for the graph in the form of edges and weights, constructs the graph, and then applies Dijkstra's algorithm from a given source node. Finally, it prints the shortest distances from the source node to all other nodes in the graph.

### 1. Algorithms & Data Structures (C++): Graph Algorithms: Graph theory

Graph theory is a fascinating branch of mathematics and computer science that deals with the study of graphs. In the context of algorithms and data structures, graphs are abstract representations of networks consisting of nodes (vertices) and edges (connections between nodes).

Here are some key concepts and terms in graph theory:

1. **Graph**: A graph \( G \) is defined as a pair \( (V, E) \), where \( V \) is a set of vertices (nodes) and \( E \) is a set of edges (connections between nodes).

2. **Directed Graph**: In a directed graph, each edge has a direction associated with it, indicating the flow or relationship between vertices.

3. **Undirected Graph**: In an undirected graph, edges have no direction, and they simply represent a connection between two vertices.

4. **Weighted Graph**: A weighted graph is a graph in which each edge is assigned a numerical value, called a weight, representing some property such as distance, cost, or capacity.

5. **Degree**: The degree of a vertex in a graph is the number of edges incident to that vertex. In a directed graph, there are two degrees: in-degree (number of incoming edges) and out-degree (number of outgoing edges).

6. **Path**: A path in a graph is a sequence of vertices where each adjacent pair of vertices is connected by an edge.

7. **Cycle**: A cycle is a path in which the first and last vertices are the same.

8. **Connected Graph**: A graph is connected if there is a path between every pair of vertices.

9. **Disconnected Graph**: A graph is disconnected if there are two or more vertices with no path between them.

10. **Tree**: A tree is a connected graph with no cycles.

11. **Spanning Tree**: A spanning tree of a connected graph \( G \) is a subgraph that is a tree containing all the vertices of \( G \).

Graph algorithms are used to solve various real-world problems involving networks and relationships, such as finding the shortest path between two nodes, determining the most efficient route in a transportation network, analyzing social networks, and optimizing computer networks.

Some common graph algorithms include:

1. **Breadth-First Search (BFS)**: Used to traverse or search a graph by exploring all the neighbors of a node before moving on to the next level of nodes.

2. **Depth-First Search (DFS)**: Another graph traversal algorithm that explores as far as possible along each branch before backtracking.

3. **Dijkstra's Algorithm**: Finds the shortest path between two vertices in a weighted graph.

4. **Bellman-Ford Algorithm**: Similar to Dijkstra's algorithm but can handle graphs with negative edge weights.

5. **Prim's Algorithm**: Finds the minimum spanning tree of a connected, undirected graph.

6. **Kruskal's Algorithm**: Another algorithm for finding the minimum spanning tree using a different approach.

7. **Floyd-Warshall Algorithm**: Computes the shortest paths between all pairs of vertices in a weighted graph.

These algorithms form the backbone of graph theory and are fundamental tools in computer science for solving a wide range of problems efficiently.

### 1. Algorithms & Data Structures (C++): Graph Algorithms: Graph Traversal

Graph traversal algorithms are fundamental techniques used to visit all the nodes in a graph. They're essential for tasks like searching, finding paths, and discovering connected components. In C++, you can implement graph traversal using various techniques such as Depth-First Search (DFS) and Breadth-First Search (BFS). Here's a brief overview of each:

1. **Depth-First Search (DFS)**:
   - DFS explores a graph by going as deep as possible along each branch before backtracking.
   - It's often implemented using a stack or recursion.
   - Pseudocode for DFS:

   ```bash
   DFS(vertex v):
       mark v as visited
       for each neighbor u of v:
           if u is not visited:
               DFS(u)

   ```

   - In C++, you can implement DFS using recursion or by utilizing an explicit stack.

2. **Breadth-First Search (BFS)**:
   - BFS explores a graph by visiting all neighbors of a node before moving on to the next level of nodes.
   - It's usually implemented using a queue data structure.
   - Pseudocode for BFS:

   ```plaintext
   BFS(starting vertex s):
       create an empty queue Q
       enqueue s into Q
       mark s as visited
       while Q is not empty:
           v = dequeue from Q
           for each neighbor u of v:
               if u is not visited:
                   mark u as visited
                   enqueue u into Q
   ```

   - In C++, you can implement BFS using a queue.

3. **Applications**:
   - Graph traversal algorithms are used in various applications such as finding paths, cycle detection, connected components, and topological sorting.
   - DFS can be used to check for cycles in a graph, whereas BFS can be used to find the shortest path in an unweighted graph.

Here's a simple example of DFS implementation in C++:

```cpp
#include <iostream>
#include <vector>
#include <stack>
using namespace std;

void DFS(vector<vector<int>>& graph, int start) {
    int n = graph.size();
    vector<bool> visited(n, false);
    stack<int> stk;

    stk.push(start);
    visited[start] = true;

    while (!stk.empty()) {
        int v = stk.top();
        stk.pop();
        cout << v << " ";

        for (int u : graph[v]) {
            if (!visited[u]) {
                stk.push(u);
                visited[u] = true;
            }
        }
    }
}

int main() {
    // Example graph represented as an adjacency list
    vector<vector<int>> graph = {
        {1, 2},
        {0, 2, 3},
        {0, 1, 3},
        {1, 2, 4},
        {3}
    };

    cout << "DFS traversal starting from node 0:\n";
    DFS(graph, 0);

    return 0;
}
```

This code demonstrates how to perform DFS traversal on a graph represented as an adjacency list. You can modify it to implement BFS or apply these algorithms to solve specific graph problems.

### 1. Algorithms & Data Structures (C++): Graph Algorithms: Greedy algorithm or dynamic programming approach?

Choosing between a greedy algorithm and a dynamic programming approach for graph algorithms in C++ depends on the specific problem you're trying to solve and the characteristics of the graph.

Here's a general guideline:

1. **Greedy Algorithm**:
   - Greedy algorithms make locally optimal choices at each step with the hope of finding a global optimum.
   - They are usually simpler to implement and more efficient in terms of time complexity compared to dynamic programming.
   - However, they may not always lead to the globally optimal solution, as they do not consider the entire problem space.
   - Greedy algorithms are suitable for problems where making the locally optimal choice at each step leads to the globally optimal solution. Examples include minimum spanning tree algorithms like Kruskal's and Prim's.

2. **Dynamic Programming**:
   - Dynamic programming breaks down a complex problem into simpler subproblems and solves each subproblem only once, storing the solutions to avoid redundant computations.
   - It is typically used when the problem exhibits overlapping subproblems and optimal substructure properties.
   - Dynamic programming solutions are often more difficult to design and implement but guarantee finding the globally optimal solution.
   - Dynamic programming is suitable for problems like shortest path algorithms (e.g., Dijkstra's algorithm, Bellman-Ford algorithm), where the optimal solution can be built from optimal solutions to subproblems.

So, if the problem at hand can be solved by making locally optimal choices and these choices lead to the globally optimal solution, a greedy algorithm might be more appropriate. Otherwise, if the problem requires considering all possible solutions and making decisions based on optimal substructure, dynamic programming would be a better choice.

However, there are cases where neither approach may be suitable, and other algorithmic paradigms such as divide and conquer or backtracking may be more appropriate. Understanding the problem constraints and characteristics is key to selecting the most suitable algorithmic approach.

### 1. Algorithms & Data Structures (C++): Graph Algorithms: Memory management: Breadth First Search vs Depth First Search

In terms of memory management, Breadth First Search (BFS) and Depth First Search (DFS) algorithms operate differently due to their traversal strategies.

1. **Breadth First Search (BFS)**:
   - **Memory Usage**: BFS typically uses more memory compared to DFS. This is because BFS explores all nodes at a given depth level before moving to the next level. As a result, it needs to keep track of all the nodes at each level in a queue until it explores all nodes at that level.
   - **Queue Usage**: BFS uses a queue data structure to keep track of the nodes to be explored. This queue can grow quite large, especially in graphs with a large branching factor or depth.
   - **Space Complexity**: The space complexity of BFS is O(|V| + |E|), where |V| is the number of vertices and |E| is the number of edges.

2. **Depth First Search (DFS)**:
   - **Memory Usage**: DFS typically uses less memory compared to BFS. This is because DFS explores as far as possible along each branch before backtracking, which means it only needs to keep track of the current path.
   - **Stack Usage**: DFS uses a stack (usually implemented via recursion or an explicit stack data structure) to keep track of the nodes to be explored. The depth of recursion or the size of the stack is bounded by the maximum depth of the recursion tree, which is typically smaller than the number of nodes at a given depth in BFS.
   - **Space Complexity**: The space complexity of DFS is O(|V|) if implemented using recursion and O(|V| + |E|) if implemented using an explicit stack to handle backtracking in case of cycles.

In summary, BFS tends to consume more memory due to the queue used to store nodes at each level, while DFS typically uses less memory as it explores deeper before backtracking. However, the choice between BFS and DFS depends on the specific problem requirements, such as the need for shortest paths (BFS) or topological ordering (DFS), as well as the structure of the graph and memory constraints.

### 1. Algorithms & Data Structures (C++): Graph Algorithms: Shortest path algorithms applications

Shortest path algorithms have numerous applications across various domains, from network routing and transportation systems to social network analysis and game AI. In the context of graph algorithms, particularly in C++, here are some common applications:

1. **Dijkstra's Algorithm**:
   - **Navigation Systems**: Finding the shortest path between two locations on a map, considering factors like distance or time.
   - **Network Routing**: Used in routers to find the shortest path for data packets through a network.
   - **Traffic Management**: Optimizing traffic flow by finding the quickest routes for vehicles.

2. **Bellman-Ford Algorithm**:
   - **Networks with Negative Weights**: Unlike Dijkstra's algorithm, Bellman-Ford can handle graphs with negative edge weights. It's used in scenarios where edges can represent costs or losses.
   - **Arbitrage Detection**: In finance, it can be applied to detect arbitrage opportunities in markets where exchange rates are involved.

3. **Floyd-Warshall Algorithm**:
   - **All Pairs Shortest Path**: Finding the shortest path between all pairs of vertices in a weighted graph. Commonly used in scenarios where the shortest paths between all pairs of vertices are required.
   - **Traffic Analysis**: Modeling traffic flow to determine optimal routes and potential congestion points.

4. **A* Search Algorithm**:
   - **Pathfinding in Games**: A* is commonly used in video games for pathfinding of characters or NPCs. It's efficient and can find the shortest path between two points while considering obstacles or terrain costs.
   - **Robotics and Autonomous Vehicles**: Planning paths for robots or autonomous vehicles to navigate through environments efficiently while avoiding obstacles.

5. **Topological Sorting**:
   - **Task Scheduling**: Organizing tasks or dependencies such that all dependencies are satisfied before executing a task. It's used in build systems, job scheduling, and dependency resolution.
   - **Course Prerequisites**: Determining the order in which courses should be taken based on prerequisites.

6. **Minimum Spanning Tree (MST) Algorithms**:
   - **Network Design**: Finding the minimum cost subgraph that connects all vertices in a graph. Applications include designing communication networks, electrical grid planning, and designing transportation networks.

7. **Bidirectional Search**:
   - **Optimizing Pathfinding**: Used in scenarios where both the start and end points are known, bidirectional search explores the graph from both directions simultaneously, often leading to faster searches.

These are just a few examples of how shortest path algorithms are applied in various domains. In each case, the specific algorithm chosen depends on the characteristics of the problem, such as the presence of negative weights, the need for all-pairs shortest paths, or the efficiency requirements of the application.

### 1. Algorithms & Data Structures (C++): Graph Algorithms: WebCrawler (core of search engines)

Building a web crawler, which is indeed at the core of many search engines, involves several key algorithms and data structures. Here's a basic outline of how you might implement a web crawler in C++, focusing on the core components:

### Data Structures

1. **Graph Representation**: Websites and their links can be represented as a graph. You can use an adjacency list or adjacency matrix to represent this graph.

2. **Queue or Stack**: You'll need a data structure to store URLs that need to be crawled. A queue or a stack (depending on whether you want breadth-first or depth-first crawling) can be used for this purpose.

3. **Set or Hash Table**: To keep track of visited URLs and avoid revisiting them, you'll need a data structure to store visited URLs efficiently. A set or hash table is suitable for this.

### Algorithms

1. **Breadth-First Search (BFS) or Depth-First Search (DFS)**: These are the core graph traversal algorithms that you'll use to visit web pages starting from a given seed URL. BFS is usually preferred for web crawling to ensure a more systematic exploration of the web.

2. **HTML Parsing**: You'll need an HTML parser to extract links from web pages. Libraries like libxml2 or Boost's Spirit parser can be helpful here.

3. **URL Normalization and Canonicalization**: URLs can have various formats and representations. Normalizing and canonicalizing URLs help in ensuring that duplicate URLs are detected accurately.

### Steps

1. **Seed URL**: Start with a seed URL that you want to crawl.

2. **Fetch Web Page**: Fetch the HTML content of the seed URL.

3. **Parse HTML**: Extract links from the fetched HTML content.

4. **Normalize and Canonicalize URLs**: Normalize and canonicalize the extracted URLs to avoid duplicates.

5. **Add to Queue**: Add the extracted URLs to the queue (or stack) for further crawling.

6. **Repeat**: Repeat steps 2-5 until you reach the desired depth or until there are no more URLs to crawl.

7. **Store Data**: Store the crawled data (e.g., web page content, metadata) in a suitable data structure or database.

8. **Respect Robots.txt**: Follow the guidelines specified in the `robots.txt` file of websites to avoid crawling disallowed pages.

9. **Politeness**: Implement politeness policies to avoid overloading servers with requests. This may include adding delays between requests or limiting the number of requests per second.

10. **Error Handling**: Implement error handling mechanisms to deal with cases such as unreachable URLs, server errors, etc.

Here's a simplified example code snippet in C++ for a basic web crawler:

```cpp
#include <iostream>
#include <queue>
#include <set>
#include <string>

// Function to fetch HTML content of a URL
std::string fetchHTML(const std::string& url) {
    // Code to fetch HTML content from URL
}

// Function to extract links from HTML content
std::set<std::string> extractLinks(const std::string& html) {
    // Code to parse HTML and extract links
}

// Function to normalize and canonicalize URLs
std::string normalizeURL(const std::string& url) {
    // Code to normalize URL
}

void crawl(const std::string& seedURL, int maxDepth) {
    std::queue<std::string> urlQueue;
    std::set<std::string> visited;

    urlQueue.push(seedURL);
    visited.insert(seedURL);

    while (!urlQueue.empty() && maxDepth > 0) {
        std::string currentURL = urlQueue.front();
        urlQueue.pop();
        
        std::string html = fetchHTML(currentURL);
        std::set<std::string> links = extractLinks(html);

        for (const std::string& link : links) {
            std::string normalizedURL = normalizeURL(link);
            if (visited.find(normalizedURL) == visited.end()) {
                urlQueue.push(normalizedURL);
                visited.insert(normalizedURL);
            }
        }

        maxDepth--;
    }
}

int main() {
    std::string seedURL = "https://example.com";
    int maxDepth = 3;
    crawl(seedURL, maxDepth);
    return 0;
}
```

This is a very basic implementation. Real-world web crawlers would need to handle various edge cases, such as handling redirects, dealing with different types of links (relative, absolute, etc.), handling different content types, and respecting web standards and conventions. Additionally, concurrency and distributed crawling are also essential considerations for efficient web crawling at scale.

### 1. Algorithms & Data Structures (C++): Graph Algorithms: What is the critical path method (CPM)?

The Critical Path Method (CPM) is a technique used in project management to determine the longest sequence of dependent tasks and their durations within a project. While it's commonly associated with project management, it can also be applied in various other domains, including graph algorithms.

In the context of graph algorithms, the CPM is used to find the longest path in a directed acyclic graph (DAG). Each vertex in the graph represents a task, and directed edges between vertices represent dependencies between tasks. The weight of each edge typically represents the duration or cost of completing the task.

The critical path in this context refers to the longest path through the graph, which represents the minimum time required to complete the project. Tasks on this critical path cannot be delayed without delaying the entire project. Therefore, identifying the critical path helps project managers focus on the tasks that are most crucial for meeting deadlines.

Here's a basic outline of how CPM is applied in the context of graph algorithms:

1. **Construct the Graph**: Represent the project tasks as vertices and the dependencies between tasks as directed edges. Assign weights to the edges representing the time or cost required to complete each task.

2. **Topological Sorting**: Ensure that the graph is a Directed Acyclic Graph (DAG) by performing a topological sort. This step is necessary to ensure that tasks are processed in the correct order, respecting their dependencies.

3. **Forward Pass**: Calculate the earliest start time (ES) and earliest finish time (EF) for each task. Start from the initial node(s) and propagate forward, considering the durations of tasks and their dependencies.

4. **Backward Pass**: Calculate the latest start time (LS) and latest finish time (LF) for each task. Start from the final node(s) and propagate backward, considering the project deadline and dependencies.

5. **Identify the Critical Path**: The critical path consists of tasks with zero slack, meaning their ES and LS are equal. These tasks represent the longest path through the graph and are critical for project completion time.

By identifying the critical path using CPM, project managers can allocate resources effectively, identify potential bottlenecks, and ensure that the project is completed within the required timeframe.

### 1. Algorithms & Data Structures (C++): Graph Algorithms: What is the shortest path problem?

The shortest path problem is a classic problem in computer science and graph theory that seeks to find the shortest path between two vertices in a graph. The "shortest path" typically refers to the path with the minimum total weight or cost.

There are several variations of the shortest path problem, depending on the nature of the graph and the weights associated with its edges:

1. **Single-Source Shortest Path (SSSP):** Given a graph and a source vertex, find the shortest paths from the source vertex to all other vertices in the graph.

2. **Single-Destination Shortest Path:** Given a graph and a destination vertex, find the shortest paths from all other vertices to the destination vertex.

3. **Single-Pair Shortest Path:** Given a graph and two specific vertices (source and destination), find the shortest path between them.

4. **All-Pairs Shortest Path:** Find the shortest paths between all pairs of vertices in the graph.

Common algorithms used to solve these problems include:

- **Dijkstra's Algorithm:** Finds the shortest path from a single source vertex to all other vertices in a weighted graph with non-negative edge weights.

- **Bellman-Ford Algorithm:** Finds the shortest paths from a single source vertex to all other vertices in a weighted graph, even in the presence of negative edge weights, but detects negative weight cycles.

- **Floyd-Warshall Algorithm:** Computes the shortest paths between all pairs of vertices in a weighted graph, handling both positive and negative edge weights, but is less efficient than Dijkstra's or Bellman-Ford for single-source/single-pair problems.

Each of these algorithms has its own strengths and limitations, and the choice of algorithm depends on factors such as the characteristics of the graph and the specific requirements of the problem at hand.

### 1. Algorithms & Data Structures (C++): Graph breadth first search

Breadth-first search (BFS) is an algorithm used for traversing or searching tree or graph data structures. In the context of graphs, it systematically explores all the neighbor nodes at the present depth prior to moving on to the nodes at the next depth level. Here's a simple implementation of BFS for graphs in C++:

```cpp
#include <iostream>
#include <list>
#include <queue>

using namespace std;

// Graph class representing a directed graph using adjacency list representation
class Graph {
    int V; // Number of vertices

    // Pointer to an array containing adjacency lists
    list<int> *adj;

public:
    Graph(int V); // Constructor
    void addEdge(int v, int w); // Function to add an edge to the graph
    void BFS(int s); // Breadth-first search starting from vertex s
};

Graph::Graph(int V) {
    this->V = V;
    adj = new list<int>[V];
}

void Graph::addEdge(int v, int w) {
    adj[v].push_back(w); // Add w to v's list
}

void Graph::BFS(int s) {
    // Mark all the vertices as not visited
    bool *visited = new bool[V];
    for(int i = 0; i < V; i++)
        visited[i] = false;

    // Create a queue for BFS
    queue<int> queue;

    // Mark the current node as visited and enqueue it
    visited[s] = true;
    queue.push(s);

    while(!queue.empty()) {
        // Dequeue a vertex from queue and print it
        s = queue.front();
        cout << s << " ";
        queue.pop();

        // Get all adjacent vertices of the dequeued vertex s
        // If an adjacent has not been visited, then mark it visited
        // and enqueue it
        for(auto i = adj[s].begin(); i != adj[s].end(); ++i) {
            if(!visited[*i]) {
                visited[*i] = true;
                queue.push(*i);
            }
        }
    }
}

int main() {
    // Create a graph given in the example
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "Breadth First Traversal (starting from vertex 2): ";
    g.BFS(2);

    return 0;
}
```

This program demonstrates BFS traversal on a directed graph. You can create a `Graph` object, add edges using the `addEdge` method, and then perform BFS traversal using the `BFS` method. In this example, the BFS traversal starts from vertex 2. You can change the starting vertex as per your requirements.

### 1. Algorithms & Data Structures (C++): Graph breadth first search: Complexity analysis

The breadth-first search (BFS) algorithm is used to traverse or search a graph or tree data structure. In terms of complexity analysis:

1. **Time Complexity**:
   - In the worst-case scenario, where all vertices and edges need to be explored, the time complexity of BFS is O(V + E), where V is the number of vertices and E is the number of edges.
   - Visiting each vertex and each edge once contributes to this time complexity. The algorithm explores all vertices reachable from the source vertex, and the edges are traversed only once.

2. **Space Complexity**:
   - The space complexity of BFS is also O(V) where V is the number of vertices.
   - This space is needed for maintaining the queue used in the BFS traversal, which can store at most all the vertices in the graph at the same time during the traversal.

3. **Additional considerations**:
   - In adjacency list representation, where each vertex maintains a list of adjacent vertices, the space complexity for storing the graph is O(V + E), where V is the number of vertices and E is the number of edges.
   - The adjacency matrix representation of the graph also requires O(V^2) space.

4. **Optimizations and variations**:
   - In some cases, particularly when the graph is known to be sparse, using adjacency lists can reduce memory usage and improve performance compared to an adjacency matrix.
   - Various optimizations like using hash sets or boolean arrays to keep track of visited vertices can be employed to reduce redundant traversals and improve efficiency.
   - Parallelization techniques can also be applied to BFS for performance improvements in large graphs.

In summary, BFS provides a linear time complexity relative to the size of the graph, making it an efficient algorithm for searching and exploring graphs.

### 1. Algorithms & Data Structures (C++): Graph Coloring

Graph coloring is a fundamental problem in computer science and involves assigning colors to vertices of a graph in such a way that no two adjacent vertices have the same color. This problem has various applications, including register allocation in compilers, scheduling problems, and map coloring.

In C++, you can implement graph coloring using various algorithms such as backtracking, greedy algorithms, or constraint satisfaction algorithms like the Welsh–Powell algorithm or the DSatur algorithm. Here's a basic outline of how you could implement a simple graph coloring algorithm using backtracking:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Graph class representing an undirected graph using adjacency lists
class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V), adj(V) {}

    // Function to add an edge between two vertices
    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u);
    }

    // Function to check if it's safe to color vertex v with color c
    bool isSafe(int v, vector<int>& color, int c) {
        for (int u : adj[v]) {
            if (color[u] == c)
                return false;
        }
        return true;
    }

    // Recursive function to assign colors to vertices using backtracking
    bool graphColoringUtil(vector<int>& color, int v, int numColors) {
        if (v == V)
            return true;

        for (int c = 1; c <= numColors; ++c) {
            if (isSafe(v, color, c)) {
                color[v] = c;
                if (graphColoringUtil(color, v + 1, numColors))
                    return true;
                color[v] = 0; // Backtrack
            }
        }
        return false;
    }

    // Function to perform graph coloring
    void graphColoring(int numColors) {
        vector<int> color(V, 0); // Initialize all vertices with no color

        if (graphColoringUtil(color, 0, numColors)) {
            cout << "Graph can be colored with " << numColors << " colors. Colors of vertices:\n";
            for (int i = 0; i < V; ++i)
                cout << "Vertex " << i << ": Color " << color[i] << "\n";
        } else {
            cout << "Graph cannot be colored with " << numColors << " colors.\n";
        }
    }
};

int main() {
    Graph g(5); // Create a graph with 5 vertices

    // Add edges
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(2, 3);
    g.addEdge(3, 4);

    int numColors = 3; // Number of colors
    g.graphColoring(numColors);

    return 0;
}
```

This code defines a `Graph` class representing an undirected graph using adjacency lists. It includes functions to add edges, check if it's safe to color a vertex, and a recursive function to perform graph coloring using backtracking. Finally, in the `main` function, it creates a sample graph, specifies the number of colors, and calls the `graphColoring` function to perform graph coloring.

### 1. Algorithms & Data Structures (C++): Graph Data

Graphs are fundamental data structures used to represent connections or relationships between pairs of objects. In C++, graphs can be implemented using various data structures. Here's a brief overview of some common graph representations and algorithms:

### Graph Representations

1. **Adjacency Matrix**: In this representation, a matrix of size \( V \times V \) is used, where \( V \) is the number of vertices in the graph. Each cell \( (i, j) \) in the matrix contains either 0 or 1, indicating whether there is an edge from vertex \( i \) to vertex \( j \).

2. **Adjacency List**: Here, each vertex in the graph is associated with a list of its neighboring vertices. This representation is more memory-efficient than the adjacency matrix for sparse graphs.

### Graph Traversal Algorithms

1. **Depth-First Search (DFS)**: DFS explores as far as possible along each branch before backtracking. It can be implemented recursively or using a stack.

2. **Breadth-First Search (BFS)**: BFS explores all the neighbor nodes at the present depth prior to moving on to the nodes at the next depth level. It can be implemented using a queue.

### Graph Shortest Path Algorithms

1. **Dijkstra's Algorithm**: It finds the shortest path from a given source vertex to all other vertices in the graph with non-negative edge weights.

2. **Bellman-Ford Algorithm**: It finds the shortest path from a given source vertex to all other vertices in the graph, even in the presence of negative edge weights.

### Minimum Spanning Tree Algorithms

1. **Kruskal's Algorithm**: It finds a minimum spanning tree for a connected weighted graph. It grows a forest of trees, adding edges to connect separate trees until all the vertices are connected.

2. **Prim's Algorithm**: Similar to Kruskal's algorithm, Prim's algorithm finds a minimum spanning tree for a connected weighted graph. However, it grows the tree from a single source vertex.

### Graph Coloring Algorithms

1. **Greedy Coloring Algorithm**: Assign colors to vertices of a graph in a way that no two adjacent vertices share the same color. This algorithm assigns colors one by one to the vertices, considering the least used color at every step.

2. **Backtracking Algorithm**: It exhaustively searches through all possible vertex-coloring combinations until a proper coloring is found.

### Topological Sorting Algorithm

1. **Kahn's Algorithm**: It is used to linearly order a directed acyclic graph (DAG) such that for every directed edge \( (u, v) \), vertex \( u \) comes before \( v \) in the ordering.

### Network Flow Algorithms

1. **Ford-Fulkerson Algorithm (with Edmonds-Karp optimization)**: It is used to find the maximum flow in a flow network.

2. **Minimum Cut Algorithm**: It is used to find the minimum cut in a flow network.

These are some of the fundamental algorithms and representations related to graph data structures in C++. Depending on the specific requirements of your application, you may need to choose the appropriate representation and algorithm.

### 1. Algorithms & Data Structures (C++): Basics of Graph Data Structure

Graph data structures are fundamental in computer science and are used to represent connections or relationships between pairs of objects. Let's delve into the basics of implementing graph data structures in C++.

### Representations of Graphs

#### 1. **Adjacency Matrix:**

- An adjacency matrix is a 2D array of size V x V, where V is the number of vertices in the graph.
- The cell (i, j) represents if there is an edge from vertex i to vertex j.
- For an undirected graph, the matrix is symmetric.
- This representation is efficient for dense graphs but consumes more space for sparse graphs.

#### 2. **Adjacency List:**

- An adjacency list represents a graph as an array of lists.
- The array size is equal to the number of vertices in the graph.
- Each element of the array is a list that contains all the adjacent vertices of a vertex.
- This representation is more memory-efficient for sparse graphs.

### C++ Implementation

#### 1. Adjacency Matrix

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency matrix

public:
    Graph(int vertices) : V(vertices) {
        adj.resize(V, vector<int>(V, 0));
    }

    void addEdge(int u, int v) {
        adj[u][v] = 1;
        adj[v][u] = 1; // For undirected graph
    }

    void printGraph() {
        for (int i = 0; i < V; ++i) {
            cout << "Adjacency list of vertex " << i << ":\n";
            for (int j = 0; j < V; ++j) {
                if (adj[i][j])
                    cout << "-> " << j << " ";
            }
            cout << "\n";
        }
    }
};

int main() {
    Graph g(5);
    g.addEdge(0, 1);
    g.addEdge(0, 4);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 3);
    g.addEdge(3, 4);

    g.printGraph();

    return 0;
}
```

#### 2. Adjacency List

```cpp
#include <iostream>
#include <list>

using namespace std;

class Graph {
    int V; // Number of vertices
    list<int> *adj; // Array of lists

public:
    Graph(int vertices) : V(vertices) {
        adj = new list<int>[V];
    }

    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u); // For undirected graph
    }

    void printGraph() {
        for (int i = 0; i < V; ++i) {
            cout << "Adjacency list of vertex " << i << ":\n";
            for (auto v : adj[i])
                cout << "-> " << v << " ";
            cout << "\n";
        }
    }
};

int main() {
    Graph g(5);
    g.addEdge(0, 1);
    g.addEdge(0, 4);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 3);
    g.addEdge(3, 4);

    g.printGraph();

    return 0;
}
```

These implementations cover the basic concepts of representing graphs in C++ using adjacency matrix and adjacency list. You can further extend these implementations by adding functionalities like depth-first search (DFS) or breadth-first search (BFS) traversal algorithms.

### 1. Algorithms & Data Structures (C++): Bellman Ford

Bellman-Ford is a popular algorithm used to find the shortest paths from a source vertex to all other vertices in a weighted graph, even in the presence of negative weight edges, provided that there are no negative weight cycles reachable from the source vertex. Here's a basic implementation of the Bellman-Ford algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <climits>

using namespace std;

struct Edge {
    int source, destination, weight;
};

void bellmanFord(vector<Edge>& edges, int numVertices, int source) {
    vector<int> distance(numVertices, INT_MAX);
    distance[source] = 0;

    // Relax all edges |V| - 1 times
    for (int i = 0; i < numVertices - 1; ++i) {
        for (const Edge& edge : edges) {
            if (distance[edge.source] != INT_MAX &&
                distance[edge.source] + edge.weight < distance[edge.destination]) {
                distance[edge.destination] = distance[edge.source] + edge.weight;
            }
        }
    }

    // Check for negative weight cycles
    for (const Edge& edge : edges) {
        if (distance[edge.source] != INT_MAX &&
            distance[edge.source] + edge.weight < distance[edge.destination]) {
            cout << "Graph contains a negative weight cycle" << endl;
            return;
        }
    }

    // Print shortest distances
    cout << "Shortest distances from source " << source << ":\n";
    for (int i = 0; i < numVertices; ++i) {
        cout << "Vertex " << i << ": " << distance[i] << endl;
    }
}

int main() {
    int numVertices, numEdges;
    cout << "Enter the number of vertices and edges: ";
    cin >> numVertices >> numEdges;

    vector<Edge> edges(numEdges);
    cout << "Enter source, destination, and weight for each edge:" << endl;
    for (int i = 0; i < numEdges; ++i) {
        cin >> edges[i].source >> edges[i].destination >> edges[i].weight;
    }

    int source;
    cout << "Enter the source vertex: ";
    cin >> source;

    bellmanFord(edges, numVertices, source);

    return 0;
}
```

In this implementation, the `Edge` structure represents an edge in the graph with its source vertex, destination vertex, and weight. The `bellmanFord` function takes the vector of edges, the number of vertices, and the source vertex as parameters. It initializes an array `distance` to store the shortest distances from the source vertex to all other vertices. It then iterates through all edges `|V| - 1` times, where `|V|` is the number of vertices, and relaxes the edges if a shorter path is found. Finally, it checks for negative weight cycles and prints the shortest distances from the source vertex to all other vertices.

You can run this code and input the number of vertices, edges, the source vertex, and the edges with their weights to find the shortest paths using the Bellman-Ford algorithm.

### 1. Algorithms & Data Structures (C++): Bellman Ford Algorithm

The Bellman-Ford algorithm is a popular algorithm used to find the shortest paths from a single source vertex to all other vertices in a weighted graph, even in the presence of negative weight edges, provided there are no negative weight cycles reachable from the source vertex. Here's a brief explanation of how the algorithm works:

1. **Initialization**: Start by setting the distance to the source vertex as 0 and all other distances to infinity.

2. **Relax Edges**: Iterate over all edges in the graph and relax each edge. Relaxing an edge means updating the distance to the target vertex if a shorter path is found through the current edge.

3. **Repeat Relaxation**: Repeat the relaxation process |V| - 1 times, where |V| is the number of vertices in the graph. This ensures that the shortest path distances are correctly calculated.

4. **Check for Negative Cycles**: After performing |V| - 1 iterations, check for any negative cycles. A negative cycle occurs if further relaxation is possible after the |V| - 1 iterations. If a negative cycle is found, the algorithm indicates that no shortest paths exist due to the negative cycle.

5. **Output**: After completing the iterations, the shortest path distances from the source vertex to all other vertices are calculated.

Here's a simple implementation of the Bellman-Ford algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <limits>

using namespace std;

struct Edge {
    int source, target, weight;
};

void bellmanFord(vector<Edge>& edges, int V, int source) {
    vector<int> distance(V, numeric_limits<int>::max());
    distance[source] = 0;

    // Relax edges repeatedly
    for (int i = 0; i < V - 1; ++i) {
        for (const auto& edge : edges) {
            int u = edge.source;
            int v = edge.target;
            int w = edge.weight;
            if (distance[u] != numeric_limits<int>::max() && distance[u] + w < distance[v]) {
                distance[v] = distance[u] + w;
            }
        }
    }

    // Check for negative cycles
    for (const auto& edge : edges) {
        int u = edge.source;
        int v = edge.target;
        int w = edge.weight;
        if (distance[u] != numeric_limits<int>::max() && distance[u] + w < distance[v]) {
            cout << "Graph contains negative cycle" << endl;
            return;
        }
    }

    // Print shortest distances
    cout << "Shortest distances from source vertex " << source << ":" << endl;
    for (int i = 0; i < V; ++i) {
        cout << "Vertex " << i << ": " << distance[i] << endl;
    }
}

int main() {
    int V, E;
    cout << "Enter number of vertices and edges: ";
    cin >> V >> E;

    vector<Edge> edges(E);
    cout << "Enter source, target, and weight for each edge:" << endl;
    for (int i = 0; i < E; ++i) {
        cin >> edges[i].source >> edges[i].target >> edges[i].weight;
    }

    int source;
    cout << "Enter source vertex: ";
    cin >> source;

    bellmanFord(edges, V, source);

    return 0;
}
```

This code snippet allows you to input the graph as a list of edges and then calculates the shortest distances from a specified source vertex using the Bellman-Ford algorithm.

### 1. Algorithms & Data Structures (C++): Bellman Ford Algorithm with negative cycle

The Bellman-Ford algorithm is used to find the shortest paths from a single source vertex to all other vertices in a weighted graph. It works even when there are negative edge weights, but it cannot handle negative cycles. However, it can detect the presence of a negative cycle in the graph.

Here's a C++ implementation of the Bellman-Ford algorithm that can detect negative cycles:

```cpp
#include <iostream>
#include <vector>
#include <limits>

using namespace std;

struct Edge {
    int source, destination, weight;
};

void bellmanFord(vector<Edge>& edges, int vertices, int source) {
    vector<int> distance(vertices, numeric_limits<int>::max());
    distance[source] = 0;

    // Relax all edges for |V| - 1 times
    for (int i = 1; i < vertices; ++i) {
        for (const auto& edge : edges) {
            if (distance[edge.source] != numeric_limits<int>::max() &&
                distance[edge.source] + edge.weight < distance[edge.destination]) {
                distance[edge.destination] = distance[edge.source] + edge.weight;
            }
        }
    }

    // Check for negative cycles
    for (const auto& edge : edges) {
        if (distance[edge.source] != numeric_limits<int>::max() &&
            distance[edge.source] + edge.weight < distance[edge.destination]) {
            cout << "Graph contains a negative cycle!" << endl;
            return;
        }
    }

    // Print distances
    cout << "Vertex   Distance from Source\n";
    for (int i = 0; i < vertices; ++i)
        cout << i << "\t\t" << distance[i] << endl;
}

int main() {
    vector<Edge> edges = {
        {0, 1, -1},
        {0, 2, 4},
        {1, 2, 3},
        {1, 3, 2},
        {1, 4, 2},
        {3, 2, 5},
        {3, 1, 1},
        {4, 3, -3}
    };

    int vertices = 5;
    int source = 0;

    bellmanFord(edges, vertices, source);

    return 0;
}
```

This code first initializes the distance to all vertices to infinity except the source vertex, which is set to 0. Then, it relaxes all edges for |V| - 1 times, where |V| is the number of vertices. After that, it checks for any negative cycles by relaxing all edges once more. If it finds any vertex whose distance can still be updated after the final relaxation step, it concludes that there's a negative cycle in the graph. Otherwise, it prints the shortest distances from the source vertex to all other vertices.

### 1. Algorithms & Data Structures (C++): Bellman-Ford Algorithm

The Bellman-Ford algorithm is a popular algorithm used to find the shortest paths from a single source vertex to all other vertices in a weighted graph, even if the graph contains negative weight edges. It's less efficient than Dijkstra's algorithm for graphs with non-negative edge weights, but it handles negative edge weights and can detect negative cycles.

Here's a basic implementation of the Bellman-Ford algorithm in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

struct Edge {
    int source, destination, weight;
};

void bellmanFord(vector<Edge>& edges, int numVertices, int source) {
    vector<int> distance(numVertices, INT_MAX);
    distance[source] = 0;

    // Relax all edges |V| - 1 times
    for (int i = 1; i <= numVertices - 1; ++i) {
        for (const Edge& edge : edges) {
            int u = edge.source;
            int v = edge.destination;
            int weight = edge.weight;
            if (distance[u] != INT_MAX && distance[u] + weight < distance[v]) {
                distance[v] = distance[u] + weight;
            }
        }
    }

    // Check for negative weight cycles
    for (const Edge& edge : edges) {
        int u = edge.source;
        int v = edge.destination;
        int weight = edge.weight;
        if (distance[u] != INT_MAX && distance[u] + weight < distance[v]) {
            cout << "Graph contains negative weight cycle\n";
            return;
        }
    }

    // Print shortest distances
    cout << "Vertex   Distance from Source\n";
    for (int i = 0; i < numVertices; ++i) {
        cout << i << "\t\t" << distance[i] << "\n";
    }
}

int main() {
    vector<Edge> edges = {
        {0, 1, 4}, {0, 2, 3}, {1, 2, -2}, {1, 3, 4}, {1, 4, 3}, {3, 2, 5}, {3, 1, 1}, {4, 3, -5}
    };

    int numVertices = 5; // Number of vertices in the graph
    int source = 0; // Source vertex

    bellmanFord(edges, numVertices, source);

    return 0;
}
```

This code snippet demonstrates the basic implementation of the Bellman-Ford algorithm. It finds the shortest paths from a given source vertex to all other vertices in the graph. The `Edge` struct represents the edges of the graph with source, destination, and weight. The `bellmanFord` function calculates the shortest paths using the Bellman-Ford algorithm, and the `main` function demonstrates how to use this function with a sample graph.

### 1. Algorithms & Data Structures (C++): Dealing With Negative Cycles In The Bellman Ford Algorithm

Dealing with negative cycles in the Bellman-Ford algorithm requires some additional considerations compared to handling negative weights alone. A negative cycle is a cycle in the graph where the sum of the weights of the edges along the cycle is negative. Bellman-Ford algorithm detects negative cycles by running one extra iteration over all edges after the normal iterations. Here's how you can modify the Bellman-Ford algorithm in C++ to detect and handle negative cycles:

```cpp
#include <iostream>
#include <vector>

using namespace std;

struct Edge {
    int source, destination, weight;
};

void BellmanFord(vector<Edge>& edges, int V, int E, int source) {
    vector<int> distance(V, INT_MAX);
    distance[source] = 0;

    // Relax all edges V-1 times
    for (int i = 1; i <= V - 1; ++i) {
        for (int j = 0; j < E; ++j) {
            int u = edges[j].source;
            int v = edges[j].destination;
            int weight = edges[j].weight;
            if (distance[u] != INT_MAX && distance[u] + weight < distance[v]) {
                distance[v] = distance[u] + weight;
            }
        }
    }

    // Check for negative cycles
    for (int i = 0; i < E; ++i) {
        int u = edges[i].source;
        int v = edges[i].destination;
        int weight = edges[i].weight;
        if (distance[u] != INT_MAX && distance[u] + weight < distance[v]) {
            cout << "Graph contains negative cycle\n";
            return;
        }
    }

    // Print the distance array
    cout << "Vertex Distance from Source:\n";
    for (int i = 0; i < V; ++i) {
        cout << i << "\t\t" << distance[i] << endl;
    }
}

int main() {
    int V = 5; // Number of vertices
    int E = 8; // Number of edges

    // Example graph
    vector<Edge> edges = {
        {0, 1, -1}, {0, 2, 4}, {1, 2, 3}, {1, 3, 2}, 
        {1, 4, 2}, {3, 2, 5}, {3, 1, 1}, {4, 3, -3}
    };

    int source = 0; // Source vertex

    BellmanFord(edges, V, E, source);

    return 0;
}
```

In this code:

- We represent the graph using a vector of edges (`edges`), where each edge contains source, destination, and weight.
- The `BellmanFord` function iterates over all edges V-1 times to relax the edges and update the distance array.
- After V-1 iterations, an additional iteration is performed to check for negative cycles. If any distance is updated after this iteration, it indicates the presence of a negative cycle.
- If a negative cycle is detected, the algorithm terminates and outputs a message indicating the presence of a negative cycle.
- Otherwise, it prints the shortest distances from the source vertex to all other vertices.

This modified version of the Bellman-Ford algorithm can handle negative cycles in C++.

### 1. Algorithms & Data Structures (C++): Graph depth first search

Depth First Search (DFS) is a fundamental algorithm for traversing or searching tree or graph data structures. In the context of graphs, it starts at a selected vertex (often called the "source" vertex) and explores as far as possible along each branch before backtracking.

Here's a basic implementation of DFS for a graph represented using adjacency lists in C++:

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

// Graph class representing a directed graph using adjacency lists
class Graph {
    int V; // Number of vertices

    // Pointer to an array containing adjacency lists
    vector<vector<int>> adj;

public:
    Graph(int V) : V(V), adj(V) {} // Constructor

    // Function to add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w); // Add w to v’s list.
    }

    // Depth First Search traversal starting from a given vertex
    void DFS(int v) {
        // Mark all the vertices as not visited
        vector<bool> visited(V, false);

        // Create a stack for DFS
        stack<int> stack;

        // Push the current source node.
        stack.push(v);

        while (!stack.empty()) {
            // Pop a vertex from stack and print it
            v = stack.top();
            stack.pop();

            // Stack may contain the same vertex twice. So, to avoid processing
            // a vertex more than once, use a visited array.
            if (!visited[v]) {
                cout << v << " ";
                visited[v] = true;

                // Get all adjacent vertices of the popped vertex and
                // push the ones that are not yet visited
                for (auto it = adj[v].begin(); it != adj[v].end(); ++it) {
                    if (!visited[*it])
                        stack.push(*it);
                }
            }
        }
    }
};

int main() {
    // Create a graph given in the example
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "Depth First Traversal (starting from vertex 2): ";
    g.DFS(2);

    return 0;
}
```

This code demonstrates DFS on a graph with 4 vertices, represented using adjacency lists. You can adjust the graph size and edges as per your requirements. When you run this code, it will perform DFS starting from a specified vertex (in this case, vertex 2) and print the traversal order.

### 1. Algorithms & Data Structures (C++): Graph depth first search: Complexity analysis

In graph theory, Depth-First Search (DFS) is a fundamental algorithm used for traversing or searching tree or graph data structures. When discussing the complexity of DFS, we usually consider both time complexity and space complexity.

1. **Time Complexity**:
   - The time complexity of DFS is often expressed in terms of the number of vertices (|V|) and the number of edges (|E|) in the graph.
   - In the worst-case scenario, DFS visits every vertex and every edge once. This gives a time complexity of O(|V| + |E|).
   - However, it's important to note that the time complexity might vary based on the representation of the graph. For example, if the graph is represented using an adjacency matrix, the time complexity might be higher due to the need to check all possible edges for each vertex.

2. **Space Complexity**:
   - The space complexity of DFS is primarily determined by the recursion stack or the auxiliary data structures used to keep track of visited vertices and the traversal path.
   - In the worst-case scenario, the space complexity of DFS can be O(|V|) if the graph is connected and all vertices are reachable from the starting vertex. This is because the recursion stack can hold at most |V| vertices.
   - Additionally, if an auxiliary data structure like a visited array is used to keep track of visited vertices, its space complexity would be O(|V|) as well.
   - If the graph is represented using an adjacency matrix, the space complexity might be higher due to the need for additional memory to store the matrix.

Overall, the time complexity of DFS is typically O(|V| + |E|), and the space complexity is O(|V|) considering a graph represented using adjacency lists and utilizing recursion for traversal. However, variations can occur depending on the specific implementation and graph representation.

### 1. Algorithms & Data Structures (C++): Graph Graph Terminology

Graphs are fundamental data structures in computer science used to represent relationships between pairs of objects. Here's some essential terminology related to graphs:

1. **Vertex (Node)**: A fundamental unit of a graph. It represents an entity, often depicted as a circle in visual representations.

2. **Edge (Link, Arc)**: A connection between two vertices. It may be directed or undirected, depending on whether the relationship it represents has a directionality.

3. **Directed Graph (Digraph)**: A graph in which edges have a direction, indicating a one-way relationship from one vertex to another.

4. **Undirected Graph**: A graph in which edges have no direction. The relationship between vertices is mutual.

5. **Weighted Graph**: A graph in which each edge has an associated numerical value, called a weight, representing the cost or distance between the vertices it connects.

6. **Degree of a Vertex**: The number of edges incident to a vertex. In directed graphs, there may be separate counts for in-degree (number of edges coming into a vertex) and out-degree (number of edges going out of a vertex).

7. **Path**: A sequence of vertices in which each adjacent pair is connected by an edge. Paths may be simple (no repeated vertices) or allow cycles.

8. **Cycle**: A path that starts and ends at the same vertex, allowing for repeated vertices and edges.

9. **Connected Graph**: A graph in which there is a path between every pair of vertices.

10. **Disconnected Graph**: A graph with at least two vertices for which there is no path connecting them.

11. **Tree**: A connected graph with no cycles. A tree with a designated root vertex is called a rooted tree.

12. **Forest**: A disjoint set of trees.

13. **Graph Traversal**: Visiting every vertex and edge in a graph systematically. Common traversal algorithms include Depth-First Search (DFS) and Breadth-First Search (BFS).

14. **Adjacency Matrix**: A two-dimensional array where the presence or absence of an edge between two vertices is represented by a boolean value or a weight.

15. **Adjacency List**: A data structure representing a graph where each vertex is associated with a list of its neighboring vertices.

16. **Topological Sorting**: Arranging the vertices of a directed acyclic graph (DAG) in such a linear order that for every directed edge u -> v, vertex u comes before vertex v in the ordering.

17. **Minimum Spanning Tree (MST)**: A subgraph of a weighted, connected graph that includes all the vertices and is a tree. It has the minimum possible sum of edge weights among all such trees.

Understanding these terms is crucial for effectively working with graphs and implementing algorithms that utilize them, such as shortest path algorithms, network flow algorithms, and graph traversals.

### 1. Algorithms & Data Structures (C++): Graph Implementation

Implementing graphs in C++ involves creating data structures to represent the graph itself and implementing various algorithms for traversal, searching, and other operations. Here's a basic implementation of an undirected graph using adjacency lists:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Structure to represent an edge in the graph
struct Edge {
    int to;
    Edge(int _to) : to(_to) {}
};

// Graph class
class Graph {
private:
    vector<vector<Edge>> adjList;
    int numVertices;

public:
    // Constructor
    Graph(int V) : numVertices(V) {
        adjList.resize(V);
    }

    // Function to add an edge between two vertices
    void addEdge(int from, int to) {
        adjList[from].push_back(Edge(to));
        adjList[to].push_back(Edge(from)); // For undirected graph
    }

    // Function to print the graph
    void printGraph() {
        for (int i = 0; i < numVertices; ++i) {
            cout << "Adjacency list of vertex " << i << ": ";
            for (const Edge& edge : adjList[i]) {
                cout << edge.to << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph graph(5);

    // Add some edges
    graph.addEdge(0, 1);
    graph.addEdge(0, 4);
    graph.addEdge(1, 2);
    graph.addEdge(1, 3);
    graph.addEdge(1, 4);
    graph.addEdge(2, 3);
    graph.addEdge(3, 4);

    // Print the graph
    graph.printGraph();

    return 0;
}
```

This code defines a simple undirected graph with adjacency lists. Each vertex in the graph is represented by an integer index. The `Graph` class contains a vector of vectors (`adjList`) to represent adjacency lists for each vertex. The `addEdge` function adds an edge between two vertices, and `printGraph` prints the adjacency list representation of the graph.

You can expand upon this basic implementation by adding more functionality, such as algorithms for graph traversal (DFS, BFS), shortest path algorithms (Dijkstra's, Bellman-Ford), and minimum spanning tree algorithms (Prim's, Kruskal's).

### 1. Algorithms & Data Structures (C++): Graph Key Concepts

Graphs are fundamental data structures used to represent relationships between pairs of objects. In C++, you can implement graphs using various techniques, such as adjacency matrix, adjacency list, or an edge list. Here are some key concepts related to graphs and their implementation in C++:

1. **Graph Representation**:
   - **Adjacency Matrix**: A 2D array where each cell (i, j) represents whether there is an edge between vertices i and j.
   - **Adjacency List**: A vector or array of lists/arrays where each list/array contains the neighbors of a vertex.
   - **Edge List**: A list of tuples (or pairs) representing edges and optionally their weights.

2. **Graph Traversal**:
   - **Breadth-First Search (BFS)**: Visit nodes level by level starting from a source vertex.
   - **Depth-First Search (DFS)**: Explore as far as possible along each branch before backtracking.

3. **Shortest Path Algorithms**:
   - **Dijkstra's Algorithm**: Finds the shortest path from a source node to all other nodes in a weighted graph.
   - **Bellman-Ford Algorithm**: Computes the shortest paths from a single source vertex to all other vertices in a weighted graph, even if it contains negative weight edges.
   - **Floyd-Warshall Algorithm**: Finds the shortest paths between all pairs of vertices in a weighted graph.

4. **Minimum Spanning Tree (MST)**:
   - **Kruskal's Algorithm**: Finds the minimum spanning tree of a connected, undirected graph.
   - **Prim's Algorithm**: Another algorithm to find the minimum spanning tree.

5. **Topological Sorting**: Arranges the vertices of a directed acyclic graph (DAG) into a linear ordering such that for every directed edge uv from vertex u to vertex v, u comes before v in the ordering.

6. **Graph Coloring**: Assigns colors to the vertices of a graph in such a way that no two adjacent vertices have the same color.

7. **Strongly Connected Components (SCC)**:
   - **Kosaraju's Algorithm**: Finds all strongly connected components in a directed graph.

8. **Applications**:
   - Graphs are used to model networks, social networks, transportation systems, etc.
   - Google Maps uses graph algorithms to find the shortest path between two locations.
   - Social media platforms use graph algorithms for friend recommendations.

When implementing these algorithms in C++, you'll typically use data structures like vectors, arrays, priority queues, and possibly custom data structures for efficient graph manipulation and traversal. Additionally, you might need to implement classes for vertices and edges depending on the complexity of your graph operations.

### 1. Algorithms & Data Structures (C++): Graph Key Terms

Sure, here are some key terms related to graphs in the context of algorithms and data structures:

1. **Graph**: A mathematical structure consisting of a set of vertices (nodes) and a set of edges (connections) that link pairs of vertices.

2. **Vertex (Node)**: A fundamental unit of a graph, representing a point or an entity. Vertices are connected by edges.

3. **Edge**: A connection between two vertices in a graph, often representing relationships or interactions between the corresponding entities.

4. **Directed Graph (Digraph)**: A graph in which edges have a direction associated with them. That is, the connection from one vertex to another is one-way.

5. **Undirected Graph**: A graph in which edges have no direction associated with them. The connections between vertices are bidirectional.

6. **Weighted Graph**: A graph in which each edge has an associated weight or cost, representing some quantitative value such as distance, time, or cost.

7. **Degree of a Vertex**: The number of edges incident to a vertex. In directed graphs, there are separate measures for in-degree (number of incoming edges) and out-degree (number of outgoing edges) of a vertex.

8. **Path**: A sequence of vertices in which each vertex is connected to the next vertex by an edge.

9. **Cycle**: A path that starts and ends at the same vertex, traversing a sequence of edges and vertices.

10. **Connected Graph**: A graph in which there is a path between every pair of vertices.

11. **Disconnected Graph**: A graph with at least two vertices for which there is no path connecting some pair of vertices.

12. **Tree**: A connected graph with no cycles. A tree with a designated root node is called a rooted tree.

13. **Spanning Tree**: A subgraph of a graph that is a tree and includes all the vertices of the original graph.

14. **Adjacency Matrix**: A two-dimensional array used to represent a graph, where the presence or absence of an edge between vertices is indicated by the entries of the matrix.

15. **Adjacency List**: A data structure that represents a graph as an array of lists, where each list corresponds to a vertex and contains all the vertices adjacent to it.

16. **Depth-First Search (DFS)**: A graph traversal algorithm that explores as far as possible along each branch before backtracking. It can be used to detect cycles, find connected components, and solve other graph-related problems.

17. **Breadth-First Search (BFS)**: A graph traversal algorithm that explores all the vertices at the present depth before moving to the vertices at the next depth level. It can be used to find the shortest path in unweighted graphs and to solve other graph-related problems.

18. **Topological Sorting**: Arranging the vertices of a directed acyclic graph (DAG) into a linear order such that for every directed edge u → v, vertex u comes before vertex v in the order.

19. **Minimum Spanning Tree (MST)**: A spanning tree of a connected, undirected graph that has the minimum possible total edge weight.

20. **Shortest Path**: The path between two vertices in a graph with the minimum sum of edge weights.

Understanding these terms is crucial for effectively working with graphs and implementing graph algorithms in C++ or any other programming language.

### 1. Algorithms & Data Structures (C++): Graph Problems

Graph problems in algorithms and data structures are fascinating and widely applicable. Here are some classic graph problems commonly encountered in computer science:

1. **Graph Representation**: Before diving into specific problems, it's important to understand different representations of graphs, such as adjacency matrix, adjacency list, and edge list. Each has its own advantages and use cases.

2. **Depth-First Search (DFS)**: DFS is a fundamental graph traversal algorithm. It explores as far as possible along each branch before backtracking. DFS is often used to solve problems like finding connected components, cycle detection, and topological sorting.

3. **Breadth-First Search (BFS)**: BFS is another fundamental graph traversal algorithm. It explores the neighbor vertices before moving to the next level of vertices. BFS is used for shortest path algorithms (like Dijkstra's and Bellman-Ford), connected components, and network analysis.

4. **Shortest Paths**:
   - **Dijkstra's Algorithm**: Finds the shortest paths from a single source vertex to all other vertices in a weighted graph with non-negative edge weights.
   - **Bellman-Ford Algorithm**: Finds the shortest paths from a single source vertex to all other vertices in a weighted graph with negative edge weights and detects negative cycles.
   - **Floyd-Warshall Algorithm**: Finds the shortest paths between all pairs of vertices in a weighted graph.

5. **Minimum Spanning Trees (MST)**:
   - **Kruskal's Algorithm**: Finds a minimum spanning tree for a connected, undirected graph.
   - **Prim's Algorithm**: Finds a minimum spanning tree for a connected, undirected graph with weighted edges.

6. **Graph Coloring**: Assigns colors to vertices of a graph such that no two adjacent vertices have the same color. Applications include register allocation in compilers, scheduling problems, and map coloring.

7. **Network Flow**:
   - **Ford-Fulkerson Algorithm**: Computes the maximum flow in a flow network.
   - **Edmonds-Karp Algorithm**: A specific implementation of the Ford-Fulkerson algorithm that uses BFS to find augmenting paths, ensuring a time complexity of O(VE^2).

8. **Eulerian and Hamiltonian Paths and Cycles**:
   - **Eulerian Path/Cycle**: A path/cycle that visits every edge exactly once.
   - **Hamiltonian Path/Cycle**: A path/cycle that visits every vertex exactly once.

9. **Topological Sorting**: Orders the vertices of a directed graph such that for every directed edge uv from vertex u to vertex v, u comes before v in the ordering. Topological sorting is used in task scheduling, dependency resolution, and course scheduling.

10. **Bipartite Graphs**: A graph whose vertices can be divided into two disjoint sets such that every edge connects a vertex from one set to the other. Problems related to bipartite graphs include matching problems and graph coloring.

These are just some of the many graph problems in algorithms and data structures. Each problem has its own set of algorithms and techniques for efficient solution.

### 1. Algorithms & Data Structures (C++): A maximum Path

A "maximum path" problem typically involves finding the path with the highest sum or some other maximum criteria in a given structure, such as a tree or a graph. Let's focus on a typical scenario: finding the maximum sum path in a binary tree. Here's a simple C++ implementation using recursion:

```cpp
#include <iostream>
#include <algorithm>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

int maxPathSumUtil(TreeNode* root, int &maxSum) {
    if (!root) return 0;
    
    // Get the maximum sum of left and right subtrees
    int leftSum = max(0, maxPathSumUtil(root->left, maxSum));
    int rightSum = max(0, maxPathSumUtil(root->right, maxSum));
    
    // Update the maximum path sum found so far
    maxSum = max(maxSum, leftSum + rightSum + root->val);
    
    // Return the maximum sum of one side plus the current node's value
    return max(leftSum, rightSum) + root->val;
}

int maxPathSum(TreeNode* root) {
    int maxSum = INT_MIN;
    maxPathSumUtil(root, maxSum);
    return maxSum;
}

int main() {
    TreeNode* root = new TreeNode(10);
    root->left = new TreeNode(2);
    root->right = new TreeNode(10);
    root->left->left = new TreeNode(20);
    root->left->right = new TreeNode(1);
    root->right->right = new TreeNode(-25);
    root->right->right->left = new TreeNode(3);
    root->right->right->right = new TreeNode(4);
    
    cout << "Maximum path sum is " << maxPathSum(root) << endl;
    
    return 0;
}
```

This code defines a binary tree node and provides a function `maxPathSum` to find the maximum path sum. The `maxPathSumUtil` function is a recursive helper function that calculates the maximum path sum starting from a given node. The `main` function provides an example usage scenario.

This algorithm has a time complexity of O(n), where n is the number of nodes in the tree, because it traverses each node once.

### 1. Algorithms & Data Structures (C++): Adjacency List

An adjacency list is a popular way to represent graphs in computer science, especially in the context of implementing graph algorithms. In C++, you can implement an adjacency list using various data structures, such as vectors, lists, or maps, depending on your requirements. Here's a basic implementation of an adjacency list using a vector of lists:

```cpp
#include <iostream>
#include <vector>
#include <list>

using namespace std;

class Graph {
    int V; // Number of vertices

    // Array of lists to store adjacency lists
    vector<list<int>> adjList;

public:
    // Constructor
    Graph(int V) : V(V) {
        // Resize the vector to hold V lists
        adjList.resize(V);
    }

    // Function to add an edge from v to w
    void addEdge(int v, int w) {
        adjList[v].push_back(w);
    }

    // Function to print the adjacency list representation of the graph
    void printAdjList() {
        for (int v = 0; v < V; ++v) {
            cout << "Adjacency list of vertex " << v << ": ";
            for (int neighbor : adjList[v]) {
                cout << neighbor << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph graph(5);

    // Add some edges
    graph.addEdge(0, 1);
    graph.addEdge(0, 4);
    graph.addEdge(1, 2);
    graph.addEdge(1, 3);
    graph.addEdge(1, 4);
    graph.addEdge(2, 3);
    graph.addEdge(3, 4);

    // Print the adjacency list
    graph.printAdjList();

    return 0;
}
```

In this implementation:

- We define a `Graph` class to encapsulate the graph operations.
- The constructor initializes the number of vertices and resizes the `adjList` vector to accommodate `V` lists.
- `addEdge()` function adds an edge from vertex `v` to vertex `w` by appending `w` to the list corresponding to vertex `v`.
- `printAdjList()` function iterates over each vertex and prints its adjacency list.

You can further extend this implementation to include other functionalities such as removing edges, checking for the presence of edges, etc., depending on your requirements.

### 1. Algorithms & Data Structures (C++): Adjacency List Representation

Sure, adjacency list representation is a popular way to represent graphs in computer science, particularly for sparse graphs. In C++, you can implement an adjacency list using `std::vector` or `std::list`. Here's a basic implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Graph class
class Graph {
    int V; // Number of vertices

    // Array of vectors to represent adjacency list
    vector<int> *adj;

public:
    // Constructor
    Graph(int V) {
        this->V = V;
        adj = new vector<int>[V];
    }

    // Function to add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w); // Add w to v�s list
        adj[w].push_back(v); // Add v to w's list (for undirected graph)
    }

    // Function to print the adjacency list representation of the graph
    void printAdjList() {
        for (int v = 0; v < V; ++v) {
            cout << "Adjacency list of vertex " << v << ": ";
            for (auto it = adj[v].begin(); it != adj[v].end(); ++it)
                cout << *it << " ";
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph g(5);

    // Add edges
    g.addEdge(0, 1);
    g.addEdge(0, 4);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 3);
    g.addEdge(3, 4);

    // Print adjacency list representation
    g.printAdjList();

    return 0;
}
```

This code creates a graph with 5 vertices and adds some edges. Then, it prints out the adjacency list representation of the graph. Each vertex is associated with a vector storing its adjacent vertices.

### 1. Algorithms & Data Structures (C++): Adjacency List Representation with Node Class

Certainly! Below is an example of implementing an adjacency list representation of a graph in C++ using a node class:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Node class to represent each vertex in the graph
class Node {
public:
    int value;
    vector<Node*> neighbors;

    Node(int val) : value(val) {}

    // Add a neighbor to the node
    void addNeighbor(Node* neighbor) {
        neighbors.push_back(neighbor);
    }
};

// Graph class to represent the entire graph
class Graph {
public:
    vector<Node*> nodes;

    // Add a node to the graph
    void addNode(Node* node) {
        nodes.push_back(node);
    }

    // Add an edge between two nodes
    void addEdge(Node* from, Node* to) {
        from->addNeighbor(to);
        // For undirected graphs, uncomment the following line
        // to->addNeighbor(from);
    }

    // Print the adjacency list representation of the graph
    void printAdjacencyList() {
        for (Node* node : nodes) {
            cout << "Adjacency list of node " << node->value << ": ";
            for (Node* neighbor : node->neighbors) {
                cout << neighbor->value << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create graph nodes
    Node* node1 = new Node(1);
    Node* node2 = new Node(2);
    Node* node3 = new Node(3);
    Node* node4 = new Node(4);

    // Create a graph
    Graph graph;

    // Add nodes to the graph
    graph.addNode(node1);
    graph.addNode(node2);
    graph.addNode(node3);
    graph.addNode(node4);

    // Add edges to the graph
    graph.addEdge(node1, node2);
    graph.addEdge(node1, node3);
    graph.addEdge(node2, node3);
    graph.addEdge(node2, node4);
    graph.addEdge(node3, node4);

    // Print the adjacency list representation of the graph
    graph.printAdjacencyList();

    // Clean up memory
    delete node1;
    delete node2;
    delete node3;
    delete node4;

    return 0;
}
```

This code demonstrates the implementation of a simple undirected graph using adjacency lists in C++. Each node in the graph is represented by the `Node` class, which contains a value and a list of neighboring nodes. The `Graph` class manages the nodes and provides methods to add nodes and edges, as well as to print the adjacency list representation of the graph.

### 1. Algorithms & Data Structures (C++): Adjacency Lists Representation of Graphs

Sure! In C++, you can represent a graph using adjacency lists. In this representation, each vertex of the graph is associated with a list of its neighboring vertices. Here's a basic implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Class to represent a graph using adjacency list representation
class Graph {
    int V; // Number of vertices

    // Array of vectors to represent adjacency lists
    vector<int> *adj;

public:
    // Constructor
    Graph(int V) {
        this->V = V;
        adj = new vector<int>[V];
    }

    // Function to add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w); // Add w to v's list
    }

    // Function to print the adjacency list representation of the graph
    void printAdjacencyList() {
        for (int v = 0; v < V; ++v) {
            cout << "Adjacency list of vertex " << v << ": ";
            for (auto it = adj[v].begin(); it != adj[v].end(); ++it)
                cout << *it << " ";
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph g(5);

    // Add edges
    g.addEdge(0, 1);
    g.addEdge(0, 4);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 3);
    g.addEdge(3, 4);

    // Print adjacency list representation of the graph
    g.printAdjacencyList();

    return 0;
}
```

In this implementation:

- The `Graph` class represents the graph using an adjacency list.
- The constructor initializes the number of vertices and creates an array of vectors to store the adjacency lists.
- The `addEdge` function is used to add an edge between two vertices. It takes two vertices `v` and `w` as parameters and adds `w` to the adjacency list of `v`.
- The `printAdjacencyList` function prints the adjacency list representation of the graph.

You can modify the `main` function to create graphs of different sizes and add edges as required.

### 1. Algorithms & Data Structures (C++): Adjacency Matrix

An adjacency matrix is a common way to represent graphs using a matrix, typically a 2D array. In this representation, rows and columns correspond to vertices, and the elements of the matrix indicate whether there is an edge between two vertices.

In the case of a weighted graph, the elements of the matrix can represent the weights of the edges.

Here's a basic implementation of an adjacency matrix for an unweighted graph in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector<vector<bool>> adjMatrix; // Adjacency matrix

public:
    // Constructor
    Graph(int vertices) {
        V = vertices;
        // Initialize the adjacency matrix with all values initially false (no edges)
        adjMatrix.assign(V, vector<bool>(V, false));
    }

    // Function to add an edge between vertices u and v
    void addEdge(int u, int v) {
        adjMatrix[u][v] = true;
        adjMatrix[v][u] = true; // For undirected graph
    }

    // Function to print the adjacency matrix
    void printAdjMatrix() {
        for (int i = 0; i < V; ++i) {
            for (int j = 0; j < V; ++j) {
                cout << adjMatrix[i][j] << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 4 vertices
    Graph graph(4);

    // Add some edges
    graph.addEdge(0, 1);
    graph.addEdge(0, 2);
    graph.addEdge(1, 3);
    graph.addEdge(2, 3);

    // Print the adjacency matrix
    graph.printAdjMatrix();

    return 0;
}
```

This code defines a `Graph` class with functions to add edges and print the adjacency matrix. You can modify this implementation to support weighted graphs by using a different type for the adjacency matrix (e.g., `vector<vector<int>>` for integer weights).

Remember, the space complexity of an adjacency matrix is O(V^2), where V is the number of vertices. This can be inefficient for sparse graphs where there are relatively few edges. In such cases, an adjacency list representation might be more suitable.

### 1. Algorithms & Data Structures (C++): Adjacency Matrix Representation of Graphs

In C++, representing a graph using an adjacency matrix involves using a 2D array where the value at `matrix[i][j]` represents the weight of the edge from node `i` to node `j`. If there is no edge between two nodes, the value can be set to a special marker like infinity or -1.

Here's a simple implementation of an adjacency matrix representation of a graph in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

const int INF = 1e9; // Infinity value for non-existent edges

class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adjMatrix; // Adjacency matrix representation

public:
    // Constructor
    Graph(int vertices) {
        V = vertices;
        // Initialize the adjacency matrix with INF initially
        adjMatrix.assign(V, vector<int>(V, INF));
    }

    // Function to add an edge from vertex u to vertex v with weight w
    void addEdge(int u, int v, int w) {
        adjMatrix[u][v] = w;
    }

    // Function to print the adjacency matrix
    void printMatrix() {
        cout << "Adjacency Matrix:" << endl;
        for (int i = 0; i < V; ++i) {
            for (int j = 0; j < V; ++j) {
                if (adjMatrix[i][j] == INF)
                    cout << "INF\t";
                else
                    cout << adjMatrix[i][j] << "\t";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 4 vertices
    Graph g(4);

    // Add some edges
    g.addEdge(0, 1, 5);
    g.addEdge(0, 2, 3);
    g.addEdge(1, 2, 2);
    g.addEdge(1, 3, 6);
    g.addEdge(2, 3, 7);

    // Print the adjacency matrix
    g.printMatrix();

    return 0;
}
```

This code creates a simple undirected graph with 4 vertices and adds some edges with their respective weights. Then it prints the adjacency matrix. You can modify the `addEdge` function to suit your specific needs, such as handling directed graphs or weighted graphs differently.

### 1. Algorithms & Data Structures (C++): MMI

MMI (Maximal Matching Interface) typically refers to a concept in graph theory and combinatorial optimization, particularly in the context of matching algorithms. In algorithms and data structures, it often relates to finding the largest possible matching in a graph.

Here's a basic approach to implement MMI in C++ using the maximum cardinality matching algorithm (e.g., using Ford-Fulkerson algorithm):

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <cstring>

using namespace std;

const int MAXN = 1005; // Maximum number of vertices

vector<int> adj[MAXN]; // Adjacency list representation

bool visited[MAXN];
int match[MAXN];

bool dfs(int u) {
    if (visited[u]) return false;
    visited[u] = true;
    for (int v : adj[u]) {
        if (match[v] == -1 || dfs(match[v])) {
            match[v] = u;
            return true;
        }
    }
    return false;
}

int maximumMatching(int n) {
    memset(match, -1, sizeof(match));
    int matching = 0;
    for (int i = 0; i < n; ++i) {
        memset(visited, false, sizeof(visited));
        if (dfs(i)) ++matching;
    }
    return matching;
}

int main() {
    int n, m; // Number of vertices and edges respectively
    cin >> n >> m;

    // Input edges
    for (int i = 0; i < m; ++i) {
        int u, v;
        cin >> u >> v;
        adj[u].push_back(v);
        adj[v].push_back(u); // Assuming undirected graph
    }

    // Compute maximal matching
    int matching = maximumMatching(n);

    cout << "Size of Maximal Matching: " << matching << endl;

    return 0;
}
```

In this implementation, `adj` is the adjacency list representation of the graph, and the `maximumMatching` function computes the size of the maximal matching using a DFS-based algorithm. The `main` function takes input for the graph and outputs the size of the maximal matching. You can further extend or optimize this code depending on your specific requirements and constraints.

### 1. Algorithms & Data Structures (C++): All Pairs Shortest Path

The All Pairs Shortest Path (APSP) problem involves finding the shortest paths between all pairs of vertices in a weighted graph. One of the most well-known algorithms for solving this problem is the Floyd-Warshall algorithm, which is efficient for dense graphs. Here's a basic explanation of how it works in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

const int INF = 1e9; // Infinity value to represent unreachable nodes

// Function to find the shortest paths between all pairs of vertices
void floydWarshall(vector<vector<int>>& graph, int V) {
    vector<vector<int>> dist(V, vector<int>(V, INF)); // Initialize distances with infinity

    // Copy the graph to dist matrix
    for (int i = 0; i < V; ++i)
        for (int j = 0; j < V; ++j)
            dist[i][j] = graph[i][j];

    // Update distances by considering all vertices as intermediate vertices
    for (int k = 0; k < V; ++k) {
        for (int i = 0; i < V; ++i) {
            for (int j = 0; j < V; ++j) {
                // If vertex k is on the shortest path from i to j,
                // then update the value of dist[i][j]
                if (dist[i][k] != INF && dist[k][j] != INF && dist[i][k] + dist[k][j] < dist[i][j]) {
                    dist[i][j] = dist[i][k] + dist[k][j];
                }
            }
        }
    }

    // Output the shortest distances between every pair of vertices
    for (int i = 0; i < V; ++i) {
        for (int j = 0; j < V; ++j) {
            if (dist[i][j] == INF)
                cout << "INF\t";
            else
                cout << dist[i][j] << "\t";
        }
        cout << endl;
    }
}

int main() {
    // Example graph represented as an adjacency matrix
    vector<vector<int>> graph = {
        {0, 5, INF, 10},
        {INF, 0, 3, INF},
        {INF, INF, 0, 1},
        {INF, INF, INF, 0}
    };

    int V = graph.size();
    floydWarshall(graph, V);
    return 0;
}
```

In this implementation, `INF` represents infinity or unreachable vertices. The `floydWarshall` function iterates through all pairs of vertices and checks if there is a shorter path through the intermediate vertex `k`. If such a path exists, it updates the distance accordingly. Finally, it outputs the shortest distances between every pair of vertices.

### 1. Algorithms & Data Structures (C++): All pairs shortest path problem

The All Pairs Shortest Path (APSP) problem is a classic problem in computer science where you want to find the shortest paths between all pairs of vertices in a weighted graph. There are several algorithms to solve this problem, with some of the most notable ones being Floyd-Warshall and Johnson's algorithm. Let's focus on the Floyd-Warshall algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <limits>

using namespace std;

const int INF = numeric_limits<int>::max(); // Infinity value

// Function to find the shortest paths between all pairs of vertices
void floydWarshall(vector<vector<int>>& graph, int V) {
    // Initialize the distance matrix with the given graph
    vector<vector<int>> dist = graph;

    // Iterate through all vertices one by one
    for (int k = 0; k < V; k++) {
        // Pick all vertices as source one by one
        for (int i = 0; i < V; i++) {
            // Pick all vertices as destination for the above picked source
            for (int j = 0; j < V; j++) {
                // If vertex k is on the shortest path from i to j,
                // then update the value of dist[i][j]
                if (dist[i][k] != INF && dist[k][j] != INF && 
                    dist[i][k] + dist[k][j] < dist[i][j]) {
                    dist[i][j] = dist[i][k] + dist[k][j];
                }
            }
        }
    }

    // Print the shortest distances between every pair of vertices
    for (int i = 0; i < V; i++) {
        for (int j = 0; j < V; j++) {
            if (dist[i][j] == INF) {
                cout << "INF ";
            } else {
                cout << dist[i][j] << " ";
            }
        }
        cout << endl;
    }
}

int main() {
    int V; // Number of vertices
    cout << "Enter the number of vertices: ";
    cin >> V;

    // Initialize the graph with adjacency matrix representation
    vector<vector<int>> graph(V, vector<int>(V, INF));

    // Input the graph
    cout << "Enter the weighted adjacency matrix of the graph (enter INF for infinity):\n";
    for (int i = 0; i < V; i++) {
        for (int j = 0; j < V; j++) {
            cin >> graph[i][j];
        }
    }

    // Call the Floyd-Warshall algorithm function
    floydWarshall(graph, V);

    return 0;
}
```

This code implements the Floyd-Warshall algorithm to find the shortest paths between all pairs of vertices in a graph. It takes the weighted adjacency matrix of the graph as input and outputs the shortest distances between every pair of vertices. You can enter the number of vertices and the weighted adjacency matrix interactively.

### 1. Algorithms & Data Structures (C++): Breadth First Search

Breadth First Search (BFS) is a fundamental algorithm used for traversing or searching tree or graph data structures. It explores all the nodes at the current depth before moving on to the nodes at the next depth level. This means it visits all the neighbors of a node before visiting any of their children.

In C++, BFS can be implemented using a queue data structure. Here's a basic outline of how BFS works:

```cpp
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

// Represents a graph using adjacency list representation
class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V); // Constructor
    void addEdge(int v, int w); // Function to add an edge to the graph
    void BFS(int s); // Breadth First Search starting from vertex s
};

Graph::Graph(int V) {
    this->V = V;
    adj.resize(V);
}

void Graph::addEdge(int v, int w) {
    adj[v].push_back(w); // Add w to v’s list.
}

void Graph::BFS(int s) {
    // Mark all the vertices as not visited
    vector<bool> visited(V, false);

    // Create a queue for BFS
    queue<int> queue;

    // Mark the current node as visited and enqueue it
    visited[s] = true;
    queue.push(s);

    while (!queue.empty()) {
        // Dequeue a vertex from queue and print it
        s = queue.front();
        cout << s << " ";
        queue.pop();

        // Get all adjacent vertices of the dequeued vertex s
        // If an adjacent vertex has not been visited, then mark it visited and enqueue it
        for (auto i = adj[s].begin(); i != adj[s].end(); ++i) {
            if (!visited[*i]) {
                visited[*i] = true;
                queue.push(*i);
            }
        }
    }
}

// Driver code
int main() {
    // Create a graph given in the example
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "Breadth First Traversal (starting from vertex 2): ";
    g.BFS(2);

    return 0;
}
```

In this example, the graph is represented using an adjacency list. The `BFS` function takes the starting vertex `s` as an argument and traverses the graph in a breadth-first manner starting from `s`. It uses a queue to keep track of the nodes to be visited. The `visited` array is used to keep track of visited nodes to avoid revisiting them.

This implementation outputs the Breadth First Traversal starting from vertex 2 for the given example graph. You can modify the `main` function to create and traverse any graph you want.

### 1. Algorithms & Data Structures (C++): Breadth First Search (Breadth First Search)

Breadth First Search (BFS) is a fundamental algorithm used for traversing or searching tree or graph data structures. It starts at a specific node and explores all of its neighbors at the present depth before moving on to nodes at the next depth level. BFS uses a queue data structure to keep track of the nodes to be visited.

Here's a basic implementation of BFS in C++:

```cpp
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

// Graph representation using adjacency list
class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int v) : V(v) {
        adj.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int u, int v) {
        adj[u].push_back(v);
    }

    // Function to perform Breadth First Search
    void BFS(int start) {
        // Mark all vertices as not visited
        vector<bool> visited(V, false);

        // Create a queue for BFS
        queue<int> queue;

        // Mark the current node as visited and enqueue it
        visited[start] = true;
        queue.push(start);

        // Traverse the graph
        while (!queue.empty()) {
            // Dequeue a vertex from queue and print it
            int current = queue.front();
            cout << current << " ";
            queue.pop();

            // Get all adjacent vertices of the dequeued vertex current
            // If an adjacent has not been visited, then mark it visited and enqueue it
            for (int adjVertex : adj[current]) {
                if (!visited[adjVertex]) {
                    visited[adjVertex] = true;
                    queue.push(adjVertex);
                }
            }
        }
    }
};

int main() {
    // Create a graph given in the example
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "Breadth First Traversal (starting from vertex 2): ";
    g.BFS(2);

    return 0;
}
```

This code demonstrates BFS on a graph represented using an adjacency list. You can modify it according to your requirements and the way your graph is represented.

### 1. Algorithms & Data Structures (C++): Build Roads

To implement an algorithm for building roads in C++, you typically want to find a minimal spanning tree (MST) of a given graph. Prim's or Kruskal's algorithm are commonly used for this purpose. Here's a basic outline of how you might implement Kruskal's algorithm to build roads:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

struct Edge {
    int u, v, weight;
};

class Graph {
    int V;
    vector<Edge> edges;

public:
    Graph(int V) : V(V) {}

    void addEdge(int u, int v, int weight) {
        edges.push_back({u, v, weight});
    }

    int findParent(vector<int>& parent, int i) {
        if (parent[i] == -1)
            return i;
        return findParent(parent, parent[i]);
    }

    void unionSets(vector<int>& parent, int u, int v) {
        int uSet = findParent(parent, u);
        int vSet = findParent(parent, v);
        parent[uSet] = vSet;
    }

    void buildRoads() {
        sort(edges.begin(), edges.end(), [](const Edge& a, const Edge& b) {
            return a.weight < b.weight;
        });

        vector<int> parent(V, -1);
        cout << "Minimum Spanning Tree edges (u-v) with weights:\n";
        for (const Edge& edge : edges) {
            int u = edge.u;
            int v = edge.v;
            int uSet = findParent(parent, u);
            int vSet = findParent(parent, v);
            if (uSet != vSet) {
                cout << u << "-" << v << " (" << edge.weight << ")\n";
                unionSets(parent, uSet, vSet);
            }
        }
    }
};

int main() {
    int V, E;
    cout << "Enter the number of vertices and edges: ";
    cin >> V >> E;

    Graph graph(V);
    cout << "Enter edges (u v weight):\n";
    for (int i = 0; i < E; ++i) {
        int u, v, weight;
        cin >> u >> v >> weight;
        graph.addEdge(u, v, weight);
    }

    graph.buildRoads();

    return 0;
}
```

This code takes input of the number of vertices and edges, followed by the details of each edge (source, destination, weight). Then, it builds the MST using Kruskal's algorithm and outputs the edges forming the minimum spanning tree. These edges represent the roads that need to be built.

### 1. Algorithms & Data Structures (C++): Classification of Edges in Depth First Search of Directed Graph

In Depth First Search (DFS) of a directed graph, edges can be classified into four types based on how they are encountered during the traversal:

1. **Tree edges**: These are the edges that are used to discover new vertices. When you traverse from a vertex to one of its unvisited neighbors, the edge you traverse is a tree edge. These edges form the spanning tree of the graph rooted at the starting vertex of the DFS traversal.

2. **Back edges**: These are the edges that connect a vertex to one of its ancestors in the DFS tree. In other words, if there is an edge (u, v) such that vertex v is an ancestor of vertex u in the DFS tree, then (u, v) is a back edge. Back edges indicate the presence of cycles in the graph.

3. **Forward edges**: These are the edges that connect a vertex to one of its descendants in the DFS tree, but they are not tree edges. In other words, if there is an edge (u, v) such that vertex u is a descendant of vertex v in the DFS tree, then (u, v) is a forward edge.

4. **Cross edges**: These are the edges that connect vertices that are neither ancestors nor descendants of each other in the DFS tree. In other words, if there is an edge (u, v) such that neither vertex u is an ancestor of vertex v nor vertex v is an ancestor of vertex u in the DFS tree, then (u, v) is a cross edge.

Here's how you can classify edges during a DFS traversal of a directed graph in C++:

```cpp
#include <iostream>
#include <vector>
using namespace std;

enum EdgeType { TREE, BACK, FORWARD, CROSS };

void dfs(int u, vector<vector<int>>& graph, vector<bool>& visited, vector<int>& parent, vector<EdgeType>& edgeType) {
    visited[u] = true;
    for (int v : graph[u]) {
        if (!visited[v]) {
            parent[v] = u;
            edgeType[v] = TREE;
            dfs(v, graph, visited, parent, edgeType);
        } else {
            if (parent[u] == v)
                edgeType[v] = TREE;
            else if (parent[v] == u)
                edgeType[v] = BACK;
            else if (parent[u] < v)
                edgeType[v] = FORWARD;
            else
                edgeType[v] = CROSS;
        }
    }
}

void classifyEdges(vector<vector<int>>& graph, vector<EdgeType>& edgeType) {
    int n = graph.size();
    vector<bool> visited(n, false);
    vector<int> parent(n, -1);
    for (int u = 0; u < n; ++u) {
        if (!visited[u]) {
            edgeType[u] = TREE;
            dfs(u, graph, visited, parent, edgeType);
        }
    }
}

int main() {
    int n = 4;
    vector<vector<int>> graph(n);
    graph[0].push_back(1);
    graph[0].push_back(2);
    graph[1].push_back(2);
    graph[2].push_back(0);
    graph[2].push_back(3);
    graph[3].push_back(3);

    vector<EdgeType> edgeType(n);
    classifyEdges(graph, edgeType);

    cout << "Edge Types:\n";
    for (int i = 0; i < n; ++i) {
        cout << "Edge from 0 to " << i << " is ";
        switch (edgeType[i]) {
            case TREE: cout << "Tree edge\n"; break;
            case BACK: cout << "Back edge\n"; break;
            case FORWARD: cout << "Forward edge\n"; break;
            case CROSS: cout << "Cross edge\n"; break;
        }
    }

    return 0;
}
```

This code snippet demonstrates how to classify edges during a DFS traversal of a directed graph in C++. It uses an enumeration `EdgeType` to represent the different types of edges and a DFS function to traverse the graph and classify the edges accordingly.

### 1. Algorithms & Data Structures (C++): Classification of Edges in Depth First Search of Undirected Graph

In Depth First Search (DFS) of an undirected graph, edges can be classified based on the order in which they are traversed. There are typically three classifications:

1. **Tree edges**: These are the edges that are discovered during the DFS traversal and form the spanning tree of the graph. When DFS visits a vertex that has not been visited before, it explores all edges incident to that vertex. Each time DFS discovers a new vertex, it follows one of the undiscovered edges incident to that vertex to discover new vertices. These edges form the tree structure of the DFS traversal. Tree edges are the primary edges of the DFS tree.

2. **Back edges**: Back edges are the edges that connect a vertex to one of its ancestors in the DFS tree. In other words, if while traversing from vertex u to vertex v, if v is an ancestor of u in the DFS tree, then the edge (u, v) is a back edge. Back edges indicate the presence of cycles in the graph.

3. **Forward edges** and **cross edges**: These edges are not present in a DFS tree. They connect vertices that are neither ancestor nor descendant in the DFS tree.

   - **Forward edges**: An edge (u, v) is a forward edge if u is a descendant of v in the DFS tree but (u, v) is not a tree edge.

   - **Cross edges**: An edge (u, v) is a cross edge if u and v are neither ancestors nor descendants of each other in the DFS tree.

These classifications are useful in various graph algorithms and analyses, such as cycle detection and topological sorting. Implementing DFS with edge classification in C++ involves tracking the states of vertices and edges during the traversal. You can achieve this by maintaining additional information during the DFS traversal, such as the discovery and finish times of vertices, and analyzing the relationships between vertices based on these timestamps.

### 1. Algorithms & Data Structures (C++): Comparison Of Graph Representations

In C++, graphs can be represented in various ways, each with its advantages and disadvantages. The choice of representation depends on factors like the type of graph (directed or undirected), the operations to be performed frequently, and memory constraints. Here's a comparison of common graph representations:

1. **Adjacency Matrix:**
   - A 2D array of size V x V (where V is the number of vertices).
   - If graph is weighted, matrix stores weights of edges, otherwise 0 or 1 indicating presence or absence of edge.
   - Pros:
     - Simple to implement.
     - Easy to access the weight of an edge between two vertices.
     - Checking whether there is an edge between two vertices takes O(1) time.
   - Cons:
     - Consumes more space for sparse graphs (graphs with fewer edges).
     - Adding or removing vertices is costly (O(V^2)).
     - Iterating over all edges takes O(V^2) time.

2. **Adjacency List:**
   - Array of lists, where each element is a list of vertices adjacent to the corresponding vertex.
   - Can be implemented using arrays, vectors, or linked lists.
   - Pros:
     - Memory efficient for sparse graphs.
     - Adding or removing vertices/edges is efficient (O(1) or O(E)).
     - Iterating over all edges takes O(V + E) time.
   - Cons:
     - Accessing the weight of an edge between two vertices might be slower compared to adjacency matrix.
     - Less convenient for dense graphs.

3. **Edge List:**
   - A list of edges, where each edge is represented as a pair (u, v) denoting an edge between vertex u and vertex v.
   - Can be augmented with a third element for weighted graphs.
   - Pros:
     - Very memory efficient for sparse graphs.
     - Efficient for certain algorithms like Kruskal's Minimum Spanning Tree algorithm.
   - Cons:
     - Checking for existence of an edge between two vertices may require traversing the entire list.
     - Not suitable for algorithms requiring quick access to adjacent vertices.

4. **Compact Representations (Bitsets, Bitboards, etc.):**
   - Especially useful for very dense graphs or specialized scenarios.
   - Pros:
     - Extremely memory efficient for large, dense graphs.
     - Fast bitwise operations for certain graph algorithms.
   - Cons:
     - Limited to certain types of graphs and operations.
     - Implementations can be complex and require careful handling.

The choice of representation depends heavily on the characteristics of the graph and the operations you intend to perform on it. For example, if memory is a concern and the graph is sparse, an adjacency list might be preferable. If the graph is dense and memory isn't a concern, an adjacency matrix might be more efficient.

### 1. Algorithms & Data Structures (C++): Condensed Component Graph

A Condensed Component Graph (CCG) is a representation used in graph theory to simplify complex graphs by condensing strongly connected components into single nodes. This condensed graph retains essential information about the original graph's structure while simplifying it for certain operations or analyses.

Here's a high-level overview of how you can implement a Condensed Component Graph in C++:

1. **Identify Strongly Connected Components (SCCs)**:
   - Implement a Strongly Connected Components algorithm like Tarjan's Algorithm or Kosaraju's Algorithm to identify SCCs in the original graph.
   - Store the SCCs in a data structure such as a vector or a list.

2. **Build the Condensed Graph**:
   - Create a new graph structure for the condensed graph. You can use an adjacency list or matrix representation depending on the size and characteristics of your graph.
   - Iterate through each SCC in the original graph.
   - For each SCC, collapse it into a single node and add it to the condensed graph.
   - Traverse the original graph's edges. For each edge `(u, v)`, if `u` and `v` belong to different SCCs, add an edge from the condensed node representing `u`'s SCC to the condensed node representing `v`'s SCC in the condensed graph.

3. **Implement Graph Data Structures**:
   - Define classes or structs to represent both the original and condensed graphs.
   - Each node in the graph should contain information about its outgoing edges or adjacent nodes.

4. **Implement Graph Traversal and Operations**:
   - Implement algorithms like Breadth-First Search (BFS) or Depth-First Search (DFS) to traverse the condensed graph.
   - You may also want to implement other operations such as finding shortest paths, detecting cycles, or performing topological sorting on the condensed graph.

5. **Test Your Implementation**:
   - Create test cases to ensure that your implementation of the Condensed Component Graph produces correct results.
   - Test it on graphs of various sizes and complexities to verify its efficiency and accuracy.

Here's a basic example of how you might represent a Condensed Component Graph in C++:

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>

using namespace std;

// Structure to represent a graph node
struct Node {
    vector<int> neighbors;
};

// Condensed Component Graph
class CondensedGraph {
private:
    vector

<pair<int, unordered_set<int>>> condensed_graph;

public:
    // Add an edge between two SCCs in the condensed graph
    void addEdge(int u, int v) {
        condensed_graph[u].second.insert(v);
    }

    // Print the condensed graph
    void printCondensedGraph() {
        for (auto& [node, neighbors] : condensed_graph) {
            cout << "Node " << node << ": ";
            for (int neighbor : neighbors) {
                cout << neighbor << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a sample graph
    vector<Node> graph(5);
    graph[0].neighbors = {1};
    graph[1].neighbors = {2};
    graph[2].neighbors = {0, 3};
    graph[3].neighbors = {4};
    graph[4].neighbors = {3};

    // Perform SCC algorithm to find strongly connected components
    // Implement this part using Tarjan's Algorithm or Kosaraju's Algorithm

    // Create a CondensedGraph object
    CondensedGraph condensedGraph;

    // Add edges between SCCs in the condensed graph
    // Implement this part based on the SCC results

    // Print the condensed graph
    condensedGraph.printCondensedGraph();

    return 0;
}
```

This code provides a basic framework for implementing a Condensed Component Graph in C++. You'll need to complete it by implementing SCC algorithms and the logic to add edges between SCCs in the condensed graph. Additionally, you may need to refine and optimize the implementation based on your specific requirements and the characteristics of your input graphs.

### 1. Algorithms & Data Structures (C++): Connected and Biconnected Components

Connected components and biconnected components are fundamental concepts in graph theory and are essential in understanding the connectivity of graphs. Here's a brief overview and some C++ implementations for finding connected and biconnected components in a graph:

#### Connected Components

In a graph, connected components are subsets of vertices in which every vertex is reachable from every other vertex in the same subset. You can find connected components using depth-first search (DFS) or breadth-first search (BFS) algorithms.

Here's a simple C++ implementation using DFS to find connected components:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

class Graph {
    int V;
    vector<vector<int>> adj;

    void DFSUtil(int v, vector<bool>& visited) {
        visited[v] = true;
        cout << v << " ";

        for (int i : adj[v]) {
            if (!visited[i])
                DFSUtil(i, visited);
        }
    }

public:
    Graph(int V) {
        this->V = V;
        adj.resize(V);
    }

    void addEdge(int v, int w) {
        adj[v].push_back(w);
        adj[w].push_back(v); // For undirected graph
    }

    void connectedComponents() {
        vector<bool> visited(V, false);
        for (int v = 0; v < V; ++v) {
            if (!visited[v]) {
                DFSUtil(v, visited);
                cout << endl;
            }
        }
    }
};

int main() {
    Graph g(5);
    g.addEdge(1, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 4);
    cout << "Connected components:\n";
    g.connectedComponents();
    return 0;
}
```

#### Biconnected Components

Biconnected components are maximal biconnected subgraphs. A biconnected graph is a connected and has no articulation points. You can find biconnected components using the Tarjan's algorithm or the Hopcroft-Tarjan algorithm.

Here's a basic implementation of Tarjan's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <stack>
#include <algorithm>

using namespace std;

class Graph {
    int V;
    vector<vector<int>> adj;
    vector<int> low;
    vector<int> disc;
    vector<bool> visited;
    stack<pair<int, int>> st;
    int time;

    void DFS(int u, int parent = -1) {
        disc[u] = low[u] = time++;
        visited[u] = true;
        int children = 0;

        for (int v : adj[u]) {
            if (!visited[v]) {
                children++;
                st.push({u, v});
                DFS(v, u);
                low[u] = min(low[u], low[v]);

                if ((parent == -1 && children > 1) || (parent != -1 && low[v] >= disc[u])) {
                    while (st.top() != make_pair(u, v)) {
                        cout << st.top().first << "-" << st.top().second << " ";
                        st.pop();
                    }
                    cout << st.top().first << "-" << st.top().second << endl;
                    st.pop();
                }
            } else if (v != parent && disc[v] < low[u]) {
                low[u] = disc[v];
                st.push({u, v});
            }
        }
    }

public:
    Graph(int V) {
        this->V = V;
        adj.resize(V);
        low.resize(V, -1);
        disc.resize(V, -1);
        visited.resize(V, false);
        time = 0;
    }

    void addEdge(int v, int w) {
        adj[v].push_back(w);
        adj[w].push_back(v); // For undirected graph
    }

    void biconnectedComponents() {
        for (int i = 0; i < V; ++i) {
            if (!visited[i])
                DFS(i);
        }

        while (!st.empty()) {
            cout << st.top().first << "-" << st.top().second << " ";
            st.pop();
        }
        cout << endl;
    }
};

int main() {
    Graph g(5);
    g.addEdge(1, 0);
    g.addEdge(0, 2);
    g.addEdge(2, 1);
    g.addEdge(0, 3);
    g.addEdge(3, 4);
    cout << "Biconnected components:\n";
    g.biconnectedComponents();
    return 0;
}
```

These are basic implementations, and you may need to optimize them for performance depending on the size of your graph. Additionally, you might want to implement more advanced algorithms if you're working with larger graphs.

### 1. Algorithms & Data Structures (C++): Connected Cities

To implement a solution for finding if two cities are connected or not, you can use the concept of graph traversal. Here's a simple approach using C++:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
#include <queue>
#include <string>

using namespace std;

// Function to check if two cities are connected
bool isConnected(const unordered_map<string, vector<string>>& graph, const string& start, const string& end) {
    if (start == end) return true; // Same city is always connected
    
    unordered_map<string, bool> visited;
    queue<string> q;
    
    q.push(start);
    visited[start] = true;
    
    while (!q.empty()) {
        string current = q.front();
        q.pop();
        
        for (const string& neighbor : graph.at(current)) {
            if (neighbor == end) return true; // Found the destination city
            
            if (!visited[neighbor]) {
                q.push(neighbor);
                visited[neighbor] = true;
            }
        }
    }
    
    return false; // Couldn't reach destination
}

int main() {
    // Create a graph representing cities and their connections
    unordered_map<string, vector<string>> graph;
    graph["New York"].push_back("Boston");
    graph["Boston"].push_back("New York");
    graph["Boston"].push_back("Chicago");
    graph["Chicago"].push_back("Boston");
    graph["Chicago"].push_back("Los Angeles");
    graph["Los Angeles"].push_back("Chicago");
    graph["Los Angeles"].push_back("San Francisco");
    graph["San Francisco"].push_back("Los Angeles");
    
    // Test cases
    cout << "Are New York and Boston connected? " << (isConnected(graph, "New York", "Boston") ? "Yes" : "No") << endl;
    cout << "Are New York and San Francisco connected? " << (isConnected(graph, "New York", "San Francisco") ? "Yes" : "No") << endl;
    cout << "Are Chicago and Los Angeles connected? " << (isConnected(graph, "Chicago", "Los Angeles") ? "Yes" : "No") << endl;
    cout << "Are Chicago and New York connected? " << (isConnected(graph, "Chicago", "New York") ? "Yes" : "No") << endl;
    
    return 0;
}
```

This code defines a simple graph where each city is associated with a list of neighboring cities. The `isConnected` function uses breadth-first search (BFS) to traverse the graph and check if there is a path between two cities. Finally, the `main` function tests the `isConnected` function with some sample queries. You can expand this code further based on your requirements and the complexity of your data.

### 1. Algorithms & Data Structures (C++): Connectivity in Directed Graphs

Connectivity in directed graphs refers to the ability to determine whether there exists a path between any two vertices in the graph. There are several algorithms to solve this problem, each with its own advantages and use cases. One common approach is to use depth-first search (DFS) or breadth-first search (BFS) to explore the graph and check for connectivity.

Here's a basic implementation in C++ using DFS:

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

    void DFSUtil(int v, vector<bool>& visited);

public:
    Graph(int V);
    void addEdge(int v, int w);
    bool isReachable(int v, int w);
};

Graph::Graph(int V) {
    this->V = V;
    adj.resize(V);
}

void Graph::addEdge(int v, int w) {
    adj[v].push_back(w);
}

void Graph::DFSUtil(int v, vector<bool>& visited) {
    visited[v] = true;

    for (int i : adj[v]) {
        if (!visited[i]) {
            DFSUtil(i, visited);
        }
    }
}

bool Graph::isReachable(int v, int w) {
    vector<bool> visited(V, false);
    DFSUtil(v, visited);
    return visited[w];
}

int main() {
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    int u = 1, v = 3;
    if (g.isReachable(u, v))
        cout << "There is a path from " << u << " to " << v << endl;
    else
        cout << "There is no path from " << u << " to " << v << endl;

    return 0;
}
```

This code creates a directed graph and implements a method `isReachable()` to determine if there's a path between two given vertices using DFS. You can extend this code to suit your specific needs or use other algorithms like BFS or even more sophisticated ones like Tarjan's algorithm for strongly connected components.

### 1. Algorithms & Data Structures (C++): Connectivity in Undirected Graph

To implement connectivity in an undirected graph using C++, you can use Depth First Search (DFS) or Breadth First Search (BFS) algorithms. Here's a simple implementation using DFS:

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V), adj(V) {}

    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u); // Since it's an undirected graph
    }

    void DFSUtil(int v, vector<bool>& visited) {
        visited[v] = true;
        for (int u : adj[v]) {
            if (!visited[u])
                DFSUtil(u, visited);
        }
    }

    bool isConnected() {
        vector<bool> visited(V, false);
        DFSUtil(0, visited); // Start DFS from vertex 0

        // Check if all vertices are visited
        for (int i = 0; i < V; ++i) {
            if (!visited[i])
                return false;
        }
        return true;
    }
};

int main() {
    Graph g(5); // Create a graph with 5 vertices
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(3, 4);

    if (g.isConnected())
        cout << "The graph is connected." << endl;
    else
        cout << "The graph is not connected." << endl;

    return 0;
}
```

This code defines a `Graph` class with methods to add edges between vertices and to check if the graph is connected using DFS. In the `main()` function, a graph is created with five vertices and edges are added between them. Finally, it checks if the graph is connected or not.

You can run this code, and it should output whether the graph is connected or not based on the edges you define.

### 1. Algorithms & Data Structures (C++): Create a graph

Sure! Here's a simple implementation of an undirected graph in C++ using adjacency lists:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    // Constructor
    Graph(int vertices) {
        V = vertices;
        adj.resize(V);
    }

    // Function to add an edge between two vertices
    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u); // For undirected graph
    }

    // Function to print the graph
    void printGraph() {
        for (int i = 0; i < V; ++i) {
            cout << "Vertex " << i << " is connected to:";
            for (int j = 0; j < adj[i].size(); ++j) {
                cout << " " << adj[i][j];
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph graph(5);

    // Add some edges
    graph.addEdge(0, 1);
    graph.addEdge(0, 4);
    graph.addEdge(1, 2);
    graph.addEdge(1, 3);
    graph.addEdge(1, 4);
    graph.addEdge(2, 3);
    graph.addEdge(3, 4);

    // Print the graph
    graph.printGraph();

    return 0;
}
```

This code creates an undirected graph with 5 vertices and adds some edges between them. Finally, it prints out the adjacency list representation of the graph.

### 1. Algorithms & Data Structures (C++): Create Graph - Add Vertex

Sure, I can guide you through creating a graph and adding a vertex in C++. Here's a basic implementation using adjacency list representation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Class representing a graph
class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    // Constructor
    Graph(int vertices) : V(vertices) {
        adj.resize(V);
    }

    // Function to add an edge between two vertices
    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u); // Uncomment this line if it's an undirected graph
    }

    // Function to add a vertex
    void addVertex() {
        V++;
        adj.resize(V);
    }

    // Function to print the adjacency list
    void printGraph() {
        for (int i = 0; i < V; ++i) {
            cout << "Adjacency list of vertex " << i << ": ";
            for (int j : adj[i]) {
                cout << j << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 4 vertices
    Graph g(4);

    // Add some edges
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 3);

    // Print the graph
    g.printGraph();

    // Add a new vertex
    g.addVertex();

    // Print the graph again to see the added vertex
    cout << "\nGraph after adding a vertex:\n";
    g.printGraph();

    return 0;
}
```

This code defines a simple undirected graph class where you can add vertices and edges. The `addVertex` function increases the number of vertices and resizes the adjacency list accordingly. You can add edges between vertices using the `addEdge` function. Finally, the `printGraph` function prints the adjacency list representation of the graph.

### 1. Algorithms & Data Structures (C++): Cycle Detection in Undirected Graphs

Detecting cycles in an undirected graph is a fundamental problem in computer science. One common approach to solve this problem is by using Depth-First Search (DFS). Here's a C++ implementation:

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>

using namespace std;

class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

    // Utility function for DFS
    bool isCyclicUtil(int v, vector<bool>& visited, int parent) {
        visited[v] = true;

        // Go through all adjacent vertices
        for (int i : adj[v]) {
            if (!visited[i]) {
                if (isCyclicUtil(i, visited, v))
                    return true;
            }
            // If an adjacent vertex is visited and not the parent of the current vertex,
            // then there is a cycle
            else if (i != parent)
                return true;
        }
        return false;
    }

public:
    Graph(int V) {
        this->V = V;
        adj.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w);
        adj[w].push_back(v); // Undirected graph
    }

    // Function to check for cycles using DFS
    bool isCyclic() {
        // Mark all vertices as not visited
        vector<bool> visited(V, false);

        // Call the recursive helper function to detect cycle in different DFS trees
        for (int i = 0; i < V; i++)
            if (!visited[i])
                if (isCyclicUtil(i, visited, -1))
                    return true;

        return false;
    }
};

int main() {
    Graph g(5); // Create a graph with 5 vertices

    // Add edges
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    if (g.isCyclic())
        cout << "Graph contains cycle\n";
    else
        cout << "Graph doesn't contain cycle\n";

    return 0;
}
```

This code defines a `Graph` class with methods to add edges and detect cycles. The `isCyclicUtil` function performs a DFS traversal of the graph and checks for cycles at each step. If an adjacent vertex is visited and not the parent of the current vertex, then there's a cycle. Finally, the `isCyclic` function iterates through all vertices and calls `isCyclicUtil` for each unvisited vertex.

### 1. Algorithms & Data Structures (C++): Cycle Detection used in Kruskals

In Kruskal's algorithm, cycle detection is crucial to ensure that adding an edge to the minimum spanning tree doesn't create a cycle. This process typically involves a data structure called a disjoint-set (also known as union-find) data structure.

Here's a brief overview of how cycle detection is used in Kruskal's algorithm:

1. **Sort Edges**: First, the edges of the graph are sorted in non-decreasing order of their weights.

2. **Initialize Disjoint Set**: Each vertex of the graph is initially in its own disjoint set.

3. **Iterate Through Sorted Edges**: Starting from the edge with the smallest weight, iterate through all the edges.

4. **Check for Cycles**: For each edge, check if its endpoints belong to the same disjoint set. If they do, adding this edge would create a cycle, so skip it. If they don't, merge the sets of the endpoints and include this edge in the minimum spanning tree.

5. **Repeat**: Repeat step 4 until all vertices are connected or all edges are exhausted.

Here's a simplified version of the algorithm:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Structure to represent an edge
struct Edge {
    int src, dest, weight;
};

// Structure to represent a disjoint set
struct DisjointSet {
    vector<int> parent, rank;
    
    DisjointSet(int n) {
        parent.resize(n);
        rank.resize(n, 0);
        for (int i = 0; i < n; ++i)
            parent[i] = i;
    }

    // Find the parent of a set
    int find(int x) {
        if (parent[x] != x)
            parent[x] = find(parent[x]);
        return parent[x];
    }

    // Union two sets by rank
    void merge(int x, int y) {
        int xRoot = find(x);
        int yRoot = find(y);

        if (xRoot == yRoot) return;

        if (rank[xRoot] < rank[yRoot])
            parent[xRoot] = yRoot;
        else if (rank[xRoot] > rank[yRoot])
            parent[yRoot] = xRoot;
        else {
            parent[yRoot] = xRoot;
            rank[xRoot]++;
        }
    }
};

// Function to find the minimum spanning tree using Kruskal's algorithm
vector<Edge> kruskalMST(vector<Edge>& edges, int V) {
    // Sort edges by weight
    sort(edges.begin(), edges.end(), [](const Edge& a, const Edge& b) {
        return a.weight < b.weight;
    });

    DisjointSet ds(V);
    vector<Edge> result;

    for (const auto& edge : edges) {
        int srcRoot = ds.find(edge.src);
        int destRoot = ds.find(edge.dest);

        if (srcRoot != destRoot) {
            result.push_back(edge);
            ds.merge(srcRoot, destRoot);
        }
    }

    return result;
}

int main() {
    int V = 4;
    vector<Edge> edges = {
        {0, 1, 10},
        {0, 2, 6},
        {0, 3, 5},
        {1, 3, 15},
        {2, 3, 4}
    };

    vector<Edge> MST = kruskalMST(edges, V);

    for (const auto& edge : MST) {
        cout << edge.src << " - " << edge.dest << " : " << edge.weight << endl;
    }

    return 0;
}
```

This code represents a basic implementation of Kruskal's algorithm in C++. It sorts the edges by weight, then iterates through them, adding each edge to the MST if it doesn't create a cycle.

### 1. Algorithms & Data Structures (C++): Data Structure : Graph

Graphs are fundamental data structures used to model connections or relationships between items. They consist of nodes (vertices) and edges (connections between vertices). In C++, graphs can be implemented using various techniques, each with its advantages and disadvantages. Here's an overview of some common approaches:

1. **Adjacency Matrix**:
   - In this representation, a 2D array is used where the rows and columns represent vertices, and the presence of an edge between two vertices is indicated by a value in the corresponding cell.
   - Works well for dense graphs (graphs with many edges).
   - Requires O(V^2) space, where V is the number of vertices.
   - Accessing whether an edge exists between two vertices is efficient (O(1)).

2. **Adjacency List**:
   - In this representation, each vertex maintains a list of adjacent vertices.
   - Memory-efficient for sparse graphs (graphs with few edges).
   - Requires O(V + E) space, where V is the number of vertices and E is the number of edges.
   - Traversal through the edges of a vertex is efficient, but checking existence of an edge between two vertices may take longer (O(E)).

3. **Edge List**:
   - In this representation, edges are stored as pairs of vertices.
   - Simplest representation, but not very efficient for most operations.
   - Suitable for certain algorithms like Kruskal's Minimum Spanning Tree algorithm.
   - Requires O(E) space, where E is the number of edges.

4. **Incidence Matrix**:
   - In this representation, rows represent vertices and columns represent edges. Each cell indicates whether a vertex is incident to an edge.
   - Less commonly used due to its inefficiency for most graph operations.
   - Requires O(V * E) space.

Graphs can also be categorized based on whether they are directed or undirected, weighted or unweighted. Additionally, they can have cycles or be acyclic. Algorithms on graphs include traversal algorithms (e.g., Depth-First Search, Breadth-First Search), shortest path algorithms (e.g., Dijkstra's algorithm, Bellman-Ford algorithm), and spanning tree algorithms (e.g., Prim's algorithm, Kruskal's algorithm).

In C++, you can implement graphs using standard data structures like vectors, lists, and maps, or you can use specialized graph libraries like Boost Graph Library (BGL) for more advanced operations.

### 1. Algorithms & Data Structures (C++): Data Structures: Graphs

Graphs are fundamental data structures used to represent connections or relationships between pairs of objects. In a graph, these objects are called vertices (or nodes), and the connections between them are called edges. Graphs are used to model various real-world scenarios such as social networks, transportation networks, computer networks, and more.

There are several types of graphs:

1. **Undirected Graph**: In this type of graph, edges have no direction. If there is an edge between vertex A and vertex B, it implies that there is a connection between A and B, and vice versa.

2. **Directed Graph (Digraph)**: Here, edges have a direction associated with them. If there is an edge from vertex A to vertex B, it does not necessarily imply that there is an edge from B to A.

3. **Weighted Graph**: In this type of graph, each edge has an associated weight or cost. These weights can represent distances, costs, or any other quantitative measure associated with the connection between vertices.

4. **Sparse Graph**: A graph is considered sparse if it has relatively few edges compared to the number of vertices.

5. **Dense Graph**: A graph is dense if it has a large number of edges relative to the number of vertices.

Graphs can be represented using different data structures, including:

1. **Adjacency Matrix**: A two-dimensional array (matrix) where the value at index (i, j) represents whether there is an edge between vertex i and vertex j. For weighted graphs, this value can represent the weight of the edge.

2. **Adjacency List**: For each vertex, maintain a list of adjacent vertices. This can be implemented using an array of lists, a hashmap, or other data structures.

3. **Edge List**: A list of all the edges in the graph. Each edge is represented as a tuple (or object) containing the vertices it connects and possibly its weight.

Graph traversal algorithms are used to visit all the vertices in a graph. Some common graph traversal algorithms include:

1. **Depth-First Search (DFS)**: Traverse as far as possible along each branch before backtracking. It can be implemented recursively or using a stack.

2. **Breadth-First Search (BFS)**: Explore all the neighbor vertices at the present depth before moving to the vertices at the next depth level. It can be implemented using a queue.

Graph algorithms solve various problems on graphs, such as finding shortest paths, detecting cycles, determining connectivity, and more.

C++ provides a versatile platform for implementing graph-related algorithms and data structures. Standard Template Library (STL) containers like vectors, queues, and maps are often used in conjunction with custom classes to represent graphs efficiently. Additionally, libraries like Boost.Graph provide advanced graph data structures and algorithms for C++ developers.

### 1. Algorithms & Data Structures (C++): Depth First - Pre-Order Traversal

Depth-first traversal, specifically pre-order traversal, is a fundamental algorithm used to visit all the nodes in a tree or graph. In the case of trees, it's usually implemented recursively. Here's how you can implement pre-order traversal for a binary tree in C++:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void preOrderTraversal(TreeNode* root) {
    if (root == nullptr)
        return;

    // Process current node
    std::cout << root->val << " ";

    // Recur on left subtree
    preOrderTraversal(root->left);

    // Recur on right subtree
    preOrderTraversal(root->right);
}

int main() {
    /* Constructed binary tree is
              1
            /   \
           2     3
          / \
         4   5
    */
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    std::cout << "Preorder traversal of binary tree is \n";
    preOrderTraversal(root);

    return 0;
}
```

In this implementation:

- We define a `TreeNode` struct to represent the nodes of the binary tree.
- The `preOrderTraversal` function takes a pointer to the root node and recursively traverses the tree in pre-order.
- For each node, we first process the node itself, then recursively call `preOrderTraversal` on its left subtree, and finally on its right subtree.

When you run this code, it will output the pre-order traversal of the binary tree:

```bash
Preorder traversal of binary tree is 
1 2 4 5 3 
```

### 1. Algorithms & Data Structures (C++): Depth First Search

Depth First Search (DFS) is a fundamental graph traversal algorithm used to explore all the vertices of a graph or tree. It starts at a chosen vertex and explores as far as possible along each branch before backtracking.

Here's a basic implementation of Depth First Search in C++ for an adjacency list representation of a graph:

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

// Graph class representing an undirected graph using adjacency list
class Graph {
    int V; // Number of vertices

    // Pointer to an array containing adjacency lists
    vector<int> *adj;

public:
    Graph(int V); // Constructor

    // Function to add an edge to the graph
    void addEdge(int v, int w);

    // DFS traversal of the vertices reachable from a given vertex
    void DFS(int v);
};

Graph::Graph(int V) {
    this->V = V;
    adj = new vector<int>[V];
}

void Graph::addEdge(int v, int w) {
    adj[v].push_back(w); // Add w to v’s list
}

void Graph::DFS(int v) {
    // Mark all vertices as not visited
    vector<bool> visited(V, false);

    // Create a stack for DFS
    stack<int> stack;

    // Mark the current node as visited and push it
    visited[v] = true;
    stack.push(v);

    while (!stack.empty()) {
        // Pop a vertex from stack and print it
        v = stack.top();
        cout << v << " ";
        stack.pop();

        // Get all adjacent vertices of the popped vertex.
        // If an adjacent has not been visited, then mark it
        // visited and push it to the stack.
        for (auto i = adj[v].begin(); i != adj[v].end(); ++i) {
            if (!visited[*i]) {
                visited[*i] = true;
                stack.push(*i);
            }
        }
    }
}

int main() {
    // Create a graph given in the above diagram
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "Depth First Traversal (starting from vertex 2): ";
    g.DFS(2);
    cout << endl;

    return 0;
}
```

This code defines a `Graph` class to represent an undirected graph using an adjacency list. It provides methods to add edges and perform DFS traversal from a given vertex. In the `main` function, a sample graph is created, and DFS traversal is performed starting from vertex 2.

### 1. Algorithms & Data Structures (C++): Depth First Search for Disconnected Graph

Depth First Search (DFS) is a fundamental graph traversal algorithm used to explore the vertices of a graph. When dealing with a disconnected graph (a graph with multiple disconnected components), you can apply DFS separately to each component to visit all vertices.

Here's how you can implement DFS for a disconnected graph in C++:

```cpp
#include <iostream>
#include <vector>
#include <stack>
#include <unordered_set>

using namespace std;

// Define a graph class
class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V), adj(V) {}

    // Function to add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w);
        adj[w].push_back(v); // For undirected graph
    }

    // DFS traversal from a given vertex
    void DFSUtil(int v, unordered_set<int>& visited) {
        // Mark the current node as visited and print it
        visited.insert(v);
        cout << v << " ";

        // Recur for all the vertices adjacent to this vertex
        for (int u : adj[v]) {
            if (visited.find(u) == visited.end()) {
                DFSUtil(u, visited);
            }
        }
    }

    // DFS traversal of the vertices reachable from a given vertex
    void DFS(int v) {
        unordered_set<int> visited;

        // Call the recursive helper function
        DFSUtil(v, visited);

        // Traverse the remaining vertices that may not be reachable from the given vertex
        for (int i = 0; i < V; ++i) {
            if (visited.find(i) == visited.end()) {
                DFSUtil(i, visited);
            }
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph g(5);
    // Add edges
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(3, 4);

    cout << "Depth First Traversal for disconnected graph:" << endl;
    g.DFS(0); // Start DFS from vertex 0

    return 0;
}
```

This code defines a Graph class with methods to add edges and perform DFS traversal. The `DFSUtil` method is a recursive utility function to perform DFS from a given vertex, and the `DFS` method starts DFS traversal from a given vertex and handles disconnected components by traversing each of them. Finally, the `main` function demonstrates how to use this class to perform DFS on a disconnected graph.

### 1. Algorithms & Data Structures (C++): Depth First Search implementation

Certainly! Here's a simple implementation of Depth First Search (DFS) in C++:

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

// Function to perform Depth First Search
void dfs(vector<vector<int>>& graph, int start) {
    int n = graph.size();
    vector<bool> visited(n, false);
    stack<int> s;

    s.push(start);

    while (!s.empty()) {
        int current = s.top();
        s.pop();

        if (!visited[current]) {
            visited[current] = true;
            cout << current << " ";

            for (int neighbor : graph[current]) {
                if (!visited[neighbor]) {
                    s.push(neighbor);
                }
            }
        }
    }
}

int main() {
    // Example graph represented as adjacency list
    vector<vector<int>> graph = {
        {1, 2},     // Node 0 is connected to nodes 1 and 2
        {0, 3, 4},  // Node 1 is connected to nodes 0, 3, and 4
        {0, 5},     // Node 2 is connected to nodes 0 and 5
        {1},        // Node 3 is connected to node 1
        {1},        // Node 4 is connected to node 1
        {2}         // Node 5 is connected to node 2
    };

    cout << "Depth First Search starting from node 0:" << endl;
    dfs(graph, 0); // Start DFS from node 0
    cout << endl;

    return 0;
}
```

In this implementation:

- We use a stack to keep track of the nodes to be visited.
- We maintain a boolean array to mark visited nodes to avoid visiting the same node twice.
- The `dfs` function takes the adjacency list representation of the graph and the starting node as parameters and performs Depth First Search starting from the given node.

You can modify the `graph` variable to represent any graph you want to perform DFS on, and you can change the starting node by passing a different value to the `dfs` function call in the `main` function.

### 1. Algorithms & Data Structures (C++): Depth First Search Important Properties

Depth First Search (DFS) is a fundamental algorithm used for traversing or searching tree or graph data structures. In C++, DFS can be implemented recursively or iteratively using a stack. Here are some important properties of DFS:

1. **Depth-first nature**: DFS explores as far as possible along each branch before backtracking. This means it goes deeper into the structure before backtracking to explore other branches.

2. **Stack-based recursion or explicit stack**: In the recursive implementation, DFS utilizes the call stack for backtracking. Alternatively, an explicit stack can be used in an iterative implementation.

3. **Visited nodes**: DFS keeps track of visited nodes to prevent revisiting the same node. This is crucial to avoid infinite loops in cyclic graphs.

4. **Applications**:
    - **Traversal**: DFS is used to traverse trees and graphs efficiently. It's often used in conjunction with other algorithms, like topological sorting.
    - **Cycle detection**: DFS can be used to detect cycles in graphs. If a back edge (an edge pointing to an ancestor in the DFS tree) is found during the traversal, it indicates the presence of a cycle.
    - **Connected components**: DFS can find connected components in an undirected graph. Starting DFS from each unvisited node identifies each connected component.
    - **Pathfinding**: While not the most efficient algorithm for finding shortest paths, DFS can be used in certain scenarios where path length is less critical, or when the graph has specific characteristics.

5. **Time Complexity**: The time complexity of DFS is O(V + E), where V is the number of vertices and E is the number of edges. This is because, in the worst-case scenario, every vertex and every edge will be visited once.

6. **Space Complexity**: The space complexity of DFS is O(V) for the recursive implementation, where V is the maximum depth of the recursion stack. In the iterative implementation, the space complexity is O(V) as well, due to the stack used for maintaining the traversal.

7. **Order of visiting nodes**: Depending on the implementation, DFS can visit nodes in different orders. For example, in a recursive implementation, nodes are typically visited in postorder (visiting children before visiting the node itself), while in an iterative implementation, nodes can be visited in preorder (visiting the node before its children) or postorder depending on how the stack is managed.

Understanding these properties can help in efficiently utilizing DFS for various tasks in algorithmic problem-solving and software development.

### 1. Algorithms & Data Structures (C++): Depth First Search in Graphs

Depth First Search (DFS) is a fundamental algorithm used for traversing or searching tree or graph data structures. Here's how you can implement DFS in C++ for graphs represented using an adjacency list.

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

// Function to perform Depth First Search
void DFS(vector<vector<int>>& graph, int start) {
    int numVertices = graph.size();
    vector<bool> visited(numVertices, false);
    stack<int> s;

    // Push the start node onto the stack and mark it as visited
    s.push(start);
    visited[start] = true;

    cout << "Depth First Traversal: ";
    while (!s.empty()) {
        int current = s.top();
        s.pop();
        cout << current << " ";

        // Explore all adjacent vertices of the current vertex
        for (int neighbor : graph[current]) {
            if (!visited[neighbor]) {
                s.push(neighbor);
                visited[neighbor] = true;
            }
        }
    }
    cout << endl;
}

int main() {
    // Example graph represented using an adjacency list
    vector<vector<int>> graph = {
        {1, 2},     // Adjacent vertices of node 0
        {0, 3, 4},  // Adjacent vertices of node 1
        {0, 5},     // Adjacent vertices of node 2
        {1},        // Adjacent vertices of node 3
        {1},        // Adjacent vertices of node 4
        {2}         // Adjacent vertices of node 5
    };

    // Start DFS traversal from node 0
    DFS(graph, 0);

    return 0;
}
```

This code defines a `DFS` function that takes a graph represented as an adjacency list and a starting node as input. It initializes a stack to keep track of nodes to be visited, marks the starting node as visited, and then iterates through the graph using a stack-based approach to perform DFS traversal. Finally, it prints the order of traversal.

### 1. Algorithms & Data Structures (C++): Depth First Search InOrder

Depth First Search (DFS) is a fundamental algorithm for traversing or searching tree or graph data structures. In the case of binary trees, InOrder traversal visits nodes in the following order: left subtree, current node, right subtree. Here's how you can implement Depth First Search InOrder traversal in C++ for a binary tree:

```cpp
#include <iostream>
using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void inOrderDFS(TreeNode* root) {
    if (root == nullptr) return;
    
    // Traverse the left subtree
    inOrderDFS(root->left);
    
    // Visit the current node
    cout << root->val << " ";
    
    // Traverse the right subtree
    inOrderDFS(root->right);
}

int main() {
    // Creating a sample binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    
    // Performing InOrder DFS traversal
    cout << "InOrder DFS traversal: ";
    inOrderDFS(root);
    cout << endl;
    
    return 0;
}
```

In this code:

- `TreeNode` struct represents each node in the binary tree.
- `inOrderDFS` function recursively performs the InOrder traversal of the binary tree.
- `main` function creates a sample binary tree and calls `inOrderDFS` to perform InOrder traversal.

You can modify the `TreeNode` struct and the sample binary tree according to your requirements.

### 1. Algorithms & Data Structures (C++): Depth First Search Iterative

Depth First Search (DFS) is a graph traversal algorithm that explores as far as possible along each branch before backtracking. Implementing DFS iteratively in C++ typically involves using a stack data structure to keep track of nodes to visit. Here's a simple implementation of DFS iteratively in C++:

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

// Define the graph as an adjacency list
class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V) {
        adj.resize(V);
    }

    // Add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w);
    }

    // Depth First Search
    void DFS(int start) {
        vector<bool> visited(V, false); // Initialize all vertices as not visited
        stack<int> stack; // Stack to store vertices

        // Push the start node onto the stack and mark it as visited
        stack.push(start);
        visited[start] = true;

        while (!stack.empty()) {
            // Pop a vertex from the stack and print it
            int current = stack.top();
            stack.pop();
            cout << current << " ";

            // Get all adjacent vertices of the popped vertex
            // If an adjacent has not been visited, mark it visited and push it onto the stack
            for (int adjacent : adj[current]) {
                if (!visited[adjacent]) {
                    visited[adjacent] = true;
                    stack.push(adjacent);
                }
            }
        }
    }
};

int main() {
    // Create a graph
    Graph g(5);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(2, 4);

    cout << "Depth First Traversal (starting from vertex 0): ";
    g.DFS(0);

    return 0;
}
```

In this code:

- We first define a `Graph` class to represent the graph as an adjacency list.
- The `addEdge` method is used to add edges to the graph.
- The `DFS` method performs the depth-first search starting from a given vertex.
- Inside the `DFS` method, we use a stack to keep track of vertices to visit.
- We mark each visited vertex as we visit it to avoid revisiting vertices.
- The main function demonstrates how to use the `Graph` class and performs DFS starting from vertex 0.

### 1. Algorithms & Data Structures (C++): Depth First Search PostOrder

Depth First Search (DFS) is a fundamental algorithm for traversing or searching tree or graph data structures. Post-order traversal is one of the traversal methods in DFS. It visits nodes in the following order: left, right, root. In other words, it visits the children nodes before the parent node.

Here's a simple implementation of Depth First Search (Post-order traversal) in C++ for a binary tree:

```cpp
#include <iostream>
#include <stack>
using namespace std;

// Definition for a binary tree node
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void postOrderDFS(TreeNode* root) {
    if (root == nullptr) return;

    stack<TreeNode*> nodes;
    TreeNode* prev = nullptr;

    do {
        while (root != nullptr) {
            nodes.push(root);
            root = root->left;
        }

        while (root == nullptr && !nodes.empty()) {
            root = nodes.top();

            if (root->right == nullptr || root->right == prev) {
                cout << root->val << " "; // Process the node
                nodes.pop();
                prev = root;
                root = nullptr;
            } else {
                root = root->right;
            }
        }
    } while (!nodes.empty());
}

// Function to create a new tree node
TreeNode* newNode(int val) {
    TreeNode* temp = new TreeNode(val);
    return temp;
}

int main() {
    // Constructing a sample binary tree
    TreeNode* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);

    cout << "Post-order traversal of binary tree using DFS: ";
    postOrderDFS(root);
    cout << endl;

    return 0;
}
```

In this implementation, a stack is used to perform the DFS traversal iteratively. We keep track of the previously visited node to determine whether to move to the right child or to backtrack.

### 1. Algorithms & Data Structures (C++): Depth First Search PreOrder

Depth First Search (DFS) is a fundamental algorithm used for traversing or searching tree or graph data structures. In a PreOrder traversal, you visit each node and process it before visiting its children nodes. Here's how you can implement Depth First Search PreOrder traversal in C++ for a binary tree:

```cpp
#include <iostream>
#include <stack>
using namespace std;

// Definition for a binary tree node
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

void dfsPreOrder(TreeNode* root) {
    if (root == nullptr)
        return;

    stack<TreeNode*> nodeStack;
    nodeStack.push(root);

    while (!nodeStack.empty()) {
        TreeNode* node = nodeStack.top();
        nodeStack.pop();

        // Process current node
        cout << node->val << " ";

        // Push right child first so that it is processed after the left child
        if (node->right)
            nodeStack.push(node->right);
        if (node->left)
            nodeStack.push(node->left);
    }
}

int main() {
    // Creating a sample binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(7);

    // Perform DFS PreOrder traversal
    cout << "DFS PreOrder Traversal: ";
    dfsPreOrder(root);
    cout << endl;

    return 0;
}
```

In this code:

- `dfsPreOrder` function implements the DFS PreOrder traversal using a stack to keep track of nodes.
- We start by pushing the root node onto the stack.
- We then enter a loop where we pop a node from the stack, process it, and push its children onto the stack. Note that we push the right child before the left child onto the stack, ensuring that the left child is processed first (this adheres to the PreOrder traversal).
- The process continues until the stack is empty.

You can modify the TreeNode struct and the creation of the binary tree in the `main` function to suit your specific needs.

### 1. Algorithms & Data Structures (C++): Depth First Search Recursion

Depth First Search (DFS) is a fundamental algorithm for traversing or searching tree or graph data structures. In DFS, you start from a selected node (often called the "root" node) and explore as far as possible along each branch before backtracking. Recursion is a natural approach to implement DFS. Here's how you can implement DFS using recursion in C++:

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>

using namespace std;

// Define a class for a graph node
class Node {
public:
    int val;
    vector<Node*> neighbors;
    
    Node(int _val) : val(_val) {}
};

// DFS function
void dfs(Node* node, unordered_set<Node*>& visited) {
    // Check if the current node has been visited
    if (visited.find(node) != visited.end())
        return;
    
    // Mark the current node as visited
    visited.insert(node);
    
    // Process the current node
    cout << node->val << " ";
    
    // Recursively visit all unvisited neighbors
    for (Node* neighbor : node->neighbors) {
        dfs(neighbor, visited);
    }
}

int main() {
    // Create a graph (Example)
    Node* node1 = new Node(1);
    Node* node2 = new Node(2);
    Node* node3 = new Node(3);
    Node* node4 = new Node(4);
    Node* node5 = new Node(5);

    node1->neighbors.push_back(node2);
    node1->neighbors.push_back(node3);
    node2->neighbors.push_back(node4);
    node3->neighbors.push_back(node4);
    node3->neighbors.push_back(node5);
    
    // Perform DFS
    unordered_set<Node*> visited;
    dfs(node1, visited);
    
    // Clean up memory
    delete node1;
    delete node2;
    delete node3;
    delete node4;
    delete node5;

    return 0;
}
```

In this example, we define a `Node` class representing each node in the graph, with an integer value and a vector of pointers to neighboring nodes. The `dfs` function takes a starting node and a set of visited nodes as input. It recursively explores the graph depth-first, marking each visited node and printing its value.

Finally, in the `main` function, we create an example graph, initiate the DFS traversal from a starting node, and clean up the dynamically allocated memory.

### 1. Algorithms & Data Structures (C++): Depth First Search through Stack

Certainly! Depth-First Search (DFS) is a fundamental algorithm used for traversing or searching tree or graph data structures. It explores as far as possible along each branch before backtracking.

In C++, you can implement DFS using a stack for iterative traversal. Here's a basic implementation for traversing a graph represented as an adjacency list:

```cpp
#include <iostream>
#include <vector>
#include <stack>
#include <unordered_set>

using namespace std;

// Graph representation using adjacency list
class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj;

public:
    Graph(int V) : V(V), adj(V) {}

    // Add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w);
    }

    // Depth First Search using a stack
    void DFS(int start) {
        // Stack for DFS traversal
        stack<int> stk;

        // Set to keep track of visited vertices
        unordered_set<int> visited;

        // Push the start vertex onto the stack
        stk.push(start);

        // DFS traversal loop
        while (!stk.empty()) {
            // Pop a vertex from stack
            int v = stk.top();
            stk.pop();

            // If this vertex is not visited yet, visit it and mark as visited
            if (visited.find(v) == visited.end()) {
                cout << v << " ";
                visited.insert(v);
            }

            // Push all adjacent vertices of the popped vertex to the stack
            for (auto it = adj[v].rbegin(); it != adj[v].rend(); ++it) {
                if (visited.find(*it) == visited.end()) {
                    stk.push(*it);
                }
            }
        }
    }
};

int main() {
    // Create a graph
    Graph g(5);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(2, 4);

    cout << "Depth First Traversal (starting from vertex 0): ";
    g.DFS(0);

    return 0;
}
```

This code represents a simple undirected graph with adjacency lists. The DFS function iteratively traverses the graph starting from a specified vertex, pushing vertices onto the stack until there are no more unvisited vertices. When visiting a vertex, it prints its value and marks it as visited, then proceeds to explore its unvisited neighbors by pushing them onto the stack. This process continues until the stack becomes empty.

### 1. Algorithms & Data Structures (C++): Depth First Search to find No of Connected component

Certainly! Depth First Search (DFS) is a popular algorithm for traversing or searching tree or graph data structures. To find the number of connected components in an undirected graph using DFS, you can follow these steps:

1. Implement the DFS algorithm to traverse the graph.
2. Keep track of visited vertices to ensure each vertex is visited only once.
3. Initialize a counter to count the number of connected components.
4. For each unvisited vertex, start DFS traversal from that vertex and mark all reachable vertices as visited. Increment the counter by 1 after each DFS traversal completes, indicating the discovery of a new connected component.
5. Repeat step 4 until all vertices are visited.

Here's a sample implementation in C++:

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>

using namespace std;

// Function to perform Depth First Search
void DFS(int node, vector<vector<int>>& graph, vector<bool>& visited) {
    visited[node] = true;
    for (int neighbor : graph[node]) {
        if (!visited[neighbor]) {
            DFS(neighbor, graph, visited);
        }
    }
}

// Function to find the number of connected components in a graph
int findConnectedComponents(vector<vector<int>>& graph) {
    int n = graph.size();
    vector<bool> visited(n, false);
    int connectedComponents = 0;

    for (int i = 0; i < n; ++i) {
        if (!visited[i]) {
            DFS(i, graph, visited);
            connectedComponents++;
        }
    }

    return connectedComponents;
}

int main() {
    // Example graph representation using adjacency list
    vector<vector<int>> graph = {
        {1, 3},     // Node 0 is connected to nodes 1 and 3
        {0, 2},     // Node 1 is connected to nodes 0 and 2
        {1},        // Node 2 is connected to node 1
        {0, 4},     // Node 3 is connected to nodes 0 and 4
        {3}         // Node 4 is connected to node 3
    };

    int components = findConnectedComponents(graph);
    cout << "Number of connected components: " << components << endl;

    return 0;
}
```

This code will output the number of connected components in the given graph. You can modify the `graph` variable to represent any graph in the form of an adjacency list.

### 1. Algorithms & Data Structures (C++): Depth First Search Traversal

Depth First Search (DFS) is a fundamental graph traversal algorithm that explores as far as possible along each branch before backtracking. In C++, you can implement DFS using various data structures such as adjacency lists or adjacency matrices to represent graphs. Here's a basic implementation of DFS using an adjacency list representation:

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

// Graph class representing the graph using adjacency list
class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V), adj(V) {}

    // Function to add an edge to the graph
    void addEdge(int u, int v) {
        adj[u].push_back(v);
    }

    // Depth First Search traversal
    void DFS(int start) {
        // Vector to keep track of visited vertices
        vector<bool> visited(V, false);

        // Stack for DFS traversal
        stack<int> stack;

        // Push the starting vertex to the stack
        stack.push(start);

        // Mark the starting vertex as visited
        visited[start] = true;

        // Loop until the stack is empty
        while (!stack.empty()) {
            // Get the top vertex from the stack
            int current = stack.top();
            cout << current << " ";
            stack.pop();

            // Visit all adjacent vertices of the current vertex
            for (int v : adj[current]) {
                if (!visited[v]) {
                    // Mark the adjacent vertex as visited and push it to the stack
                    visited[v] = true;
                    stack.push(v);
                }
            }
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph g(5);

    // Add edges to the graph
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    
    cout << "DFS Traversal starting from vertex 0: ";
    g.DFS(0);
    cout << endl;

    return 0;
}
```

This code demonstrates DFS traversal starting from a given vertex in a graph represented using an adjacency list. The algorithm visits each vertex exactly once and explores as far as possible along each branch before backtracking.

### 1. Algorithms & Data Structures (C++): Depth First Search: InOrder

In C++, implementing an InOrder Depth First Search (DFS) algorithm typically involves traversing a binary tree. Here's a basic implementation of the InOrder DFS algorithm:

```cpp
#include <iostream>
#include <stack>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

void inOrderDFS(TreeNode* root) {
    if (root == nullptr)
        return;
    
    stack<TreeNode*> s;
    TreeNode* current = root;
    
    while (current != nullptr || !s.empty()) {
        while (current != nullptr) {
            s.push(current);
            current = current->left;
        }
        
        current = s.top();
        s.pop();
        
        cout << current->val << " "; // Process the current node
        
        current = current->right;
    }
}

int main() {
    // Sample binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    
    cout << "InOrder DFS traversal: ";
    inOrderDFS(root);
    cout << endl;
    
    return 0;
}
```

Explanation:

- The `inOrderDFS` function performs InOrder DFS traversal iteratively using a stack.
- We start with the root node and traverse to the leftmost node while pushing each node onto the stack.
- Once we reach a leaf node or a node with no left child, we pop the node from the stack, process it, and move to its right child.
- This process continues until the stack becomes empty and all nodes are traversed.

You can modify this code according to your requirements or integrate it into your larger project as needed.

### 1. Algorithms & Data Structures (C++): Depth First Search: PostOrder

Depth First Search (DFS) is a fundamental algorithm for traversing or searching tree or graph data structures. Post-order traversal is one of the methods of DFS where each node is processed after all its children are processed.

In the context of a tree, a post-order traversal visits the nodes in the following order:

1. Left subtree
2. Right subtree
3. Root node

Here's a simple implementation of post-order traversal using DFS in C++:

```cpp
#include <iostream>
#include <vector>
using namespace std;

// Define a structure for tree nodes
struct TreeNode {
    int val;
    vector<TreeNode*> children;
    TreeNode(int x) : val(x) {}
};

// Function to perform post-order traversal
void postOrder(TreeNode* root) {
    if (root == nullptr) return;

    // Traverse all children
    for (auto child : root->children) {
        postOrder(child);
    }

    // Process the current node
    cout << root->val << " ";
}

int main() {
    // Create a sample tree
    TreeNode* root = new TreeNode(1);
    root->children.push_back(new TreeNode(2));
    root->children.push_back(new TreeNode(3));
    root->children[0]->children.push_back(new TreeNode(4));
    root->children[0]->children.push_back(new TreeNode(5));
    root->children[1]->children.push_back(new TreeNode(6));
    root->children[1]->children.push_back(new TreeNode(7));

    // Perform post-order traversal
    cout << "Post-order traversal: ";
    postOrder(root);

    return 0;
}
```

In this code:

- We define a `TreeNode` struct to represent the nodes of the tree. Each node contains a value and a vector of child nodes.
- The `postOrder` function recursively traverses the tree in post-order fashion.
- In the `main` function, we create a sample tree and call the `postOrder` function to perform post-order traversal.

### 1. Algorithms & Data Structures (C++): Depth First Search: PreOrder

Depth-first search (DFS) is a fundamental algorithm for traversing or searching tree or graph data structures. In the case of trees, there are three common orders in which you can visit nodes: PreOrder, InOrder, and PostOrder. PreOrder traversal visits the current node before its child nodes.

Here's how you can implement Depth First Search using PreOrder traversal in C++ for a binary tree:

```cpp
#include <iostream>
#include <stack>

using namespace std;

// Node structure for binary tree
struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;

    TreeNode(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Function to perform PreOrder DFS traversal
void preOrderDFS(TreeNode* root) {
    if (root == nullptr) return;

    // Create a stack to store nodes
    stack<TreeNode*> nodeStack;
    nodeStack.push(root);

    while (!nodeStack.empty()) {
        TreeNode* current = nodeStack.top();
        nodeStack.pop();

        // Process current node
        cout << current->data << " ";

        // Push right child first, so that it's processed after left child (since it's a stack)
        if (current->right)
            nodeStack.push(current->right);
        if (current->left)
            nodeStack.push(current->left);
    }
}

int main() {
    // Example tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    cout << "PreOrder traversal of the binary tree: ";
    preOrderDFS(root);
    cout << endl;

    // Clean up memory (deallocate tree nodes)
    // Your cleanup code may vary depending on the implementation
    // (e.g., using smart pointers or a different memory management strategy)
    delete root->left->right;
    delete root->left->left;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

This code demonstrates the PreOrder traversal of a binary tree using an iterative approach with a stack. It starts from the root node, then moves to the left child if it exists, then to the right child. This process continues recursively until all nodes are visited.

### 1. Algorithms & Data Structures (C++): Depth First Search: PreOrder - Code

Sure, here's a simple implementation of Depth First Search (DFS) using the pre-order traversal technique in C++:

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

// Define a graph class
class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    // Constructor
    Graph(int vertices) : V(vertices) {
        adj.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w); // Add w to v’s list
    }

    // Depth First Search - Preorder Traversal
    void DFS_PreOrder(int start) {
        vector<bool> visited(V, false); // Mark all vertices as not visited
        stack<int> stack; // Create a stack for DFS
        stack.push(start); // Push the current source node
        visited[start] = true; // Mark the start node as visited

        while (!stack.empty()) {
            int current = stack.top(); // Get the top element of the stack
            stack.pop(); // Pop the top element

            cout << current << " "; // Print the current node

            // Traverse all adjacent vertices of the popped vertex
            // If an adjacent vertex has not been visited, then mark it visited and push it to the stack
            for (auto it = adj[current].begin(); it != adj[current].end(); ++it) {
                if (!visited[*it]) {
                    visited[*it] = true;
                    stack.push(*it);
                }
            }
        }
    }
};

int main() {
    // Create a graph
    Graph g(5);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);

    cout << "Depth First Traversal (Preorder) starting from vertex 0: ";
    g.DFS_PreOrder(0);
    cout << endl;

    return 0;
}
```

This code defines a Graph class with methods to add edges and perform a Depth First Search using the pre-order traversal technique. In the `main()` function, a simple graph is created and DFS_PreOrder method is called to traverse the graph starting from vertex 0.

### 1. Algorithms & Data Structures (C++): Depth First Search: PreOrder, InOrder, PostOrder

Depth First Search (DFS) is a fundamental algorithm used to traverse or search through a tree or graph data structure. It explores as far as possible along each branch before backtracking. There are three common ways to traverse a tree using DFS: PreOrder, InOrder, and PostOrder.

Here's how you can implement these traversal algorithms in C++:

1. **PreOrder Traversal**: In a PreOrder traversal, the root node is visited first, followed by recursively visiting the left subtree and then the right subtree.

```cpp
#include <iostream>

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void preOrderTraversal(TreeNode* root) {
    if (root == nullptr)
        return;

    std::cout << root->val << " "; // Visit the current node
    preOrderTraversal(root->left); // Recur on left subtree
    preOrderTraversal(root->right); // Recur on right subtree
}

// Example usage:
// TreeNode* root = new TreeNode(1);
// root->left = new TreeNode(2);
// root->right = new TreeNode(3);
// preOrderTraversal(root);
```

1. **InOrder Traversal**: In an InOrder traversal, the left subtree is recursively visited, then the root node is visited, and finally, the right subtree is visited.

```cpp
void inOrderTraversal(TreeNode* root) {
    if (root == nullptr)
        return;

    inOrderTraversal(root->left); // Recur on left subtree
    std::cout << root->val << " "; // Visit the current node
    inOrderTraversal(root->right); // Recur on right subtree
}

// Example usage:
// TreeNode* root = new TreeNode(1);
// root->left = new TreeNode(2);
// root->right = new TreeNode(3);
// inOrderTraversal(root);
```

1. **PostOrder Traversal**: In a PostOrder traversal, the left subtree is recursively visited, then the right subtree is visited, and finally, the root node is visited.

```cpp
void postOrderTraversal(TreeNode* root) {
    if (root == nullptr)
        return;

    postOrderTraversal(root->left); // Recur on left subtree
    postOrderTraversal(root->right); // Recur on right subtree
    std::cout << root->val << " "; // Visit the current node
}

// Example usage:
// TreeNode* root = new TreeNode(1);
// root->left = new TreeNode(2);
// root->right = new TreeNode(3);
// postOrderTraversal(root);
```

In each of these implementations, we're recursively traversing the tree while visiting the nodes in the desired order and printing or processing the value of each node accordingly.

### 1. Algorithms & Data Structures (C++): Depth-First Traversal

Depth-first traversal is a fundamental technique used in graph algorithms, tree traversal, and other related problems. It explores as far as possible along each branch before backtracking. In C++, you can implement depth-first traversal using recursion or an explicit stack.

Here's a basic implementation of depth-first traversal for a binary tree using recursion:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void dfs(TreeNode* root) {
    if (root == nullptr) return;

    // Process the current node
    std::cout << root->val << " ";

    // Recursively traverse the left subtree
    dfs(root->left);

    // Recursively traverse the right subtree
    dfs(root->right);
}

int main() {
    // Example usage
    // Create a binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    // Perform depth-first traversal
    std::cout << "Depth-First Traversal: ";
    dfs(root);

    // Clean up memory
    delete root->left->left;
    delete root->left->right;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

In this implementation, the `dfs` function performs the depth-first traversal. It first processes the current node, then recursively traverses the left subtree, and finally recursively traverses the right subtree.

Remember to handle memory management properly to avoid memory leaks, especially in more complex data structures.

For graphs, you can similarly implement depth-first traversal using either recursion or an explicit stack. The key is to maintain a visited set to avoid visiting the same node more than once.

### 1. Algorithms & Data Structures (C++): depthFirstSearch()

Sure, here's a basic implementation of depth-first search (DFS) in C++ for a graph represented using adjacency lists:

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

// Function to perform Depth First Search
void depthFirstSearch(int start, vector<vector<int>>& graph, vector<bool>& visited) {
    stack<int> s;
    s.push(start);

    while (!s.empty()) {
        int current = s.top();
        s.pop();

        if (!visited[current]) {
            visited[current] = true;
            cout << current << " ";

            // Traverse all the adjacent vertices of current vertex
            for (int i = 0; i < graph[current].size(); ++i) {
                int adjacent = graph[current][i];
                if (!visited[adjacent]) {
                    s.push(adjacent);
                }
            }
        }
    }
}

int main() {
    // Number of vertices
    int V = 5;

    // Adjacency list representation of graph
    vector<vector<int>> graph(V);
    graph[0] = {1, 2};
    graph[1] = {0, 2, 3};
    graph[2] = {0, 1, 3};
    graph[3] = {1, 2, 4};
    graph[4] = {3};

    // Visited array to keep track of visited vertices
    vector<bool> visited(V, false);

    cout << "Depth First Search starting from vertex 0: ";
    depthFirstSearch(0, graph, visited);
    cout << endl;

    return 0;
}
```

In this code:

- We represent the graph using an adjacency list, which is a vector of vectors.
- The `depthFirstSearch` function takes the starting vertex, the adjacency list representation of the graph, and a vector to keep track of visited vertices.
- We use a stack to keep track of vertices to visit. We start by pushing the starting vertex onto the stack.
- While the stack is not empty, we pop a vertex from the stack and process it. If it's not visited, we mark it as visited, print it, and push all its unvisited adjacent vertices onto the stack.
- We demonstrate the DFS by calling the `depthFirstSearch` function with the starting vertex as 0.

This implementation assumes an undirected graph. For a directed graph, you may need to modify the adjacency list accordingly.

### 1. Algorithms & Data Structures (C++): Dijastra Algorithm

Enable to get response this time. Exiting

### 1. Algorithms & Data Structures (C++): Dijastra Algorithm: Implementation

Sure! Here's a basic implementation of Dijkstra's algorithm in C++ for finding the shortest paths from a single source vertex to all other vertices in a weighted graph:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <climits>

using namespace std;

#define INF INT_MAX

// Graph edge representation
struct Edge {
    int dest;
    int weight;
};

// Graph representation using adjacency list
class Graph {
    int V; // Number of vertices
    vector<vector<Edge>> adj;

public:
    Graph(int V) : V(V), adj(V) {}

    // Add an edge to the graph
    void addEdge(int src, int dest, int weight) {
        adj[src].push_back({dest, weight});
        // For undirected graph
        // adj[dest].push_back({src, weight});
    }

    // Dijkstra's algorithm for single source shortest paths
    void dijkstra(int src) {
        vector<int> dist(V, INF); // Initialize distances to all vertices as infinite
        dist[src] = 0; // Distance from source vertex to itself is 0

        // Min heap to store vertices with their distances from the source
        priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
        pq.push({0, src}); // Push the source vertex with distance 0

        while (!pq.empty()) {
            int u = pq.top().second;
            pq.pop();

            // Iterate through all adjacent vertices of u
            for (const Edge& edge : adj[u]) {
                int v = edge.dest;
                int weight = edge.weight;

                // If a shorter path is found
                if (dist[u] != INF && dist[u] + weight < dist[v]) {
                    dist[v] = dist[u] + weight;
                    pq.push({dist[v], v});
                }
            }
        }

        // Print shortest distances from the source
        cout << "Shortest distances from vertex " << src << ":\n";
        for (int i = 0; i < V; ++i) {
            if (dist[i] == INF)
                cout << i << ": INF\n";
            else
                cout << i << ": " << dist[i] << "\n";
        }
    }
};

int main() {
    // Create a graph
    Graph g(6);
    g.addEdge(0, 1, 4);
    g.addEdge(0, 2, 1);
    g.addEdge(1, 3, 1);
    g.addEdge(2, 1, 2);
    g.addEdge(2, 3, 5);
    g.addEdge(3, 4, 3);
    g.addEdge(4, 5, 2);

    // Source vertex
    int source = 0;

    // Run Dijkstra's algorithm
    g.dijkstra(source);

    return 0;
}
```

This implementation assumes a simple directed graph with non-negative weights on the edges. It uses adjacency list representation of the graph and a priority queue (min-heap) to efficiently select the next vertex with the smallest distance.

### 1. Algorithms & Data Structures (C++): Dijikstra

Dijkstra's algorithm is a fundamental algorithm in graph theory used to find the shortest path between nodes in a graph, particularly when all edge weights are non-negative. Here's a basic implementation of Dijkstra's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>

using namespace std;

// Define infinity as a very large value
const int INF = numeric_limits<int>::max();

// Define a structure to represent a graph edge
struct Edge {
    int to;
    int weight;
    Edge(int t, int w) : to(t), weight(w) {}
};

// Define a comparison function for the priority queue
struct Compare {
    bool operator()(const pair<int, int>& a, const pair<int, int>& b) {
        return a.second > b.second;
    }
};

// Dijkstra's algorithm function
vector<int> dijkstra(const vector<vector<Edge>>& graph, int source) {
    int n = graph.size(); // Number of nodes
    vector<int> dist(n, INF); // Initialize distances to infinity
    dist[source] = 0; // Distance from source to itself is 0

    priority_queue<pair<int, int>, vector<pair<int, int>>, Compare> pq;
    pq.push({source, 0});

    while (!pq.empty()) {
        int u = pq.top().first;
        int d = pq.top().second;
        pq.pop();

        // Skip if the distance to u in pq is already greater than the calculated distance
        if (d > dist[u]) continue;

        // Traverse all neighbors of u
        for (const Edge& e : graph[u]) {
            int v = e.to;
            int w = e.weight;
            // Relaxation step
            if (dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;
                pq.push({v, dist[v]});
            }
        }
    }

    return dist;
}

int main() {
    // Example usage
    int n = 5; // Number of nodes
    vector<vector<Edge>> graph(n);
    
    // Adding edges to the graph
    graph[0].push_back(Edge(1, 10));
    graph[0].push_back(Edge(2, 5));
    graph[1].push_back(Edge(2, 2));
    graph[1].push_back(Edge(3, 1));
    graph[2].push_back(Edge(1, 3));
    graph[2].push_back(Edge(3, 9));
    graph[2].push_back(Edge(4, 2));
    graph[3].push_back(Edge(4, 4));
    graph[4].push_back(Edge(3, 6));
    
    int source = 0; // Source node
    vector<int> distances = dijkstra(graph, source);

    // Output the shortest distances from the source
    for (int i = 0; i < n; ++i) {
        cout << "Distance from node " << source << " to node " << i << " is " << distances[i] << endl;
    }

    return 0;
}
```

In this implementation:

- We represent the graph using an adjacency list, where `graph[i]` contains a list of edges going out from node `i`.
- The `dijkstra` function takes the graph and the source node as input and returns a vector of distances, where `dist[i]` represents the shortest distance from the source node to node `i`.
- We use a priority queue (`pq`) to efficiently select the node with the smallest distance from the source node at each step.
- The algorithm iterates until the priority queue is empty, updating distances as it goes.

Remember that Dijkstra's algorithm works correctly only on graphs with non-negative edge weights.

### 1. Algorithms & Data Structures (C++): Dijkshtra's Algorithm

Dijkstra's Algorithm is a fundamental algorithm in computer science, used to find the shortest path between nodes in a graph, which may represent, for example, road networks or computer networks. Here's an overview of how it works:

1. **Initialization**: Assign a tentative distance value to every node. Set it to zero for the initial node and to infinity for all other nodes. Set the initial node as the current node.

2. **Selection of next node**: For the current node, consider all of its neighbors and calculate their tentative distances through the current node. Compare the newly calculated tentative distance to the current assigned value and assign the smaller one. After considering all neighbors, mark the current node as visited and remove it from the unvisited set.

3. **Termination condition**: Stop if the destination node has been visited or if the smallest tentative distance among the nodes in the unvisited set is infinity.

4. **Loop**: Repeat steps 2 and 3 until the destination node is visited or the smallest tentative distance among the nodes in the unvisited set is infinity. If the latter occurs, then there is no path between the initial node and the destination node.

5. **Backtracking for the shortest path**: Once the algorithm has determined the shortest path to the destination node, it can trace back the path by checking the predecessors of each node starting from the destination node until it reaches the initial node.

Here's a simple implementation of Dijkstra's Algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>

using namespace std;

#define INF numeric_limits<int>::max()

// Function to implement Dijkstra's algorithm
void dijkstra(vector<vector<pair<int, int>>>& graph, int source) {
    int num_nodes = graph.size();
    vector<int> distance(num_nodes, INF);
    vector<bool> visited(num_nodes, false);
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;

    distance[source] = 0;
    pq.push({0, source});

    while (!pq.empty()) {
        int u = pq.top().second;
        pq.pop();
        if (visited[u]) continue;
        visited[u] = true;

        for (auto& edge : graph[u]) {
            int v = edge.first;
            int w = edge.second;
            if (distance[u] + w < distance[v]) {
                distance[v] = distance[u] + w;
                pq.push({distance[v], v});
            }
        }
    }

    // Print shortest distances
    cout << "Shortest distances from node " << source << ":\n";
    for (int i = 0; i < num_nodes; ++i) {
        cout << "Node " << i << ": " << distance[i] << "\n";
    }
}

int main() {
    // Example graph representation
    int num_nodes = 5;
    vector<vector<pair<int, int>>> graph(num_nodes);

    // Adding edges to the graph
    graph[0].push_back({1, 10});
    graph[0].push_back({2, 5});
    graph[1].push_back({2, 2});
    graph[1].push_back({3, 1});
    graph[2].push_back({1, 3});
    graph[2].push_back({3, 9});
    graph[2].push_back({4, 2});
    graph[3].push_back({4, 4});
    graph[4].push_back({3, 6});

    // Calling Dijkstra's algorithm
    dijkstra(graph, 0);

    return 0;
}
```

This code finds the shortest paths from a given source node to all other nodes in the graph. You can modify the graph representation and the source node to test different scenarios.

### 1. Algorithms & Data Structures (C++): Dijkstra Algorithm Testing

Testing Dijkstra's algorithm is crucial to ensure its correctness and efficiency. Here's a simple guide on how to test Dijkstra's algorithm implemented in C++:

1. **Test on Small Graphs**: Start by testing the algorithm on small graphs with known shortest paths. Create a few small graphs with a handful of nodes and edges, and calculate the shortest path manually. Then, compare the output of your implementation with the expected result.

2. **Test on Large Graphs**: Once your implementation passes the tests on small graphs, test it on larger graphs. Use graphs with more nodes and edges to evaluate the algorithm's scalability and performance. You can generate random graphs or use existing datasets for testing.

3. **Test on Special Cases**: Test the algorithm on special cases, such as graphs with negative edge weights (if your implementation supports them) or graphs with negative cycles. Ensure that the algorithm handles these cases correctly.

4. **Test Edge Cases**: Test the algorithm with edge cases, such as graphs with only one node, graphs with no edges, or graphs with disconnected components. Make sure that the algorithm behaves as expected in these scenarios.

5. **Test Performance**: Measure the algorithm's performance on different sizes of graphs. Record the execution time for various input sizes and compare it with the expected time complexity of Dijkstra's algorithm (O((V+E)logV), where V is the number of vertices and E is the number of edges).

6. **Test Robustness**: Test the algorithm's robustness by introducing invalid input, such as null pointers or invalid edge weights. Ensure that the algorithm handles such cases gracefully without crashing or producing incorrect results.

7. **Test with Libraries**: Compare the results of your implementation with well-known graph libraries or online graph tools that provide Dijkstra's algorithm functionality. This can help validate the correctness of your implementation.

8. **Test with Visualization**: Visualize the output of your algorithm on different graphs to verify that the shortest paths are correctly computed. There are various graph visualization tools available that can help you visualize the graph and the shortest paths.

By thoroughly testing your implementation of Dijkstra's algorithm using these strategies, you can ensure that it behaves correctly under various scenarios and provides accurate results.

### 1. Algorithms & Data Structures (C++): Dijkstra Algorithm with negative cycle

Implementing Dijkstra's algorithm to handle graphs with negative cycles is a bit tricky because Dijkstra's algorithm doesn't work correctly when negative edges are present. However, you can modify the algorithm to detect negative cycles. Here's a basic outline:

1. **Initialize distances**: Initialize the distance of the source node to itself as 0 and all other distances to infinity.
2. **Relax edges**: Iterate through all edges (u, v) and relax them if a shorter path to v through u is found.
3. **Detect negative cycles**: After relaxing all edges |V| - 1 times, iterate through all edges again. If you find any edge (u, v) where dist[u] + weight(u, v) < dist[v], then a negative cycle is present.
4. **Handle negative cycles**: If a negative cycle is detected, you can't find the shortest paths reliably, as the concept of a "shortest path" doesn't exist in the presence of negative cycles.

Here's a sample implementation in C++:

```cpp
#include <iostream>
#include <vector>
#include <limits>

using namespace std;

struct Edge {
    int source, destination, weight;
};

void relax(int u, int v, int w, vector<int> &dist) {
    if (dist[u] != INT_MAX && dist[u] + w < dist[v]) {
        dist[v] = dist[u] + w;
    }
}

bool detectNegativeCycle(vector<Edge> &edges, int V, vector<int> &dist) {
    for (Edge edge : edges) {
        int u = edge.source;
        int v = edge.destination;
        int w = edge.weight;
        if (dist[u] != INT_MAX && dist[u] + w < dist[v]) {
            return true; // Negative cycle detected
        }
    }
    return false;
}

void printShortestPaths(vector<int> &dist, int V) {
    cout << "Vertex Distance from Source" << endl;
    for (int i = 0; i < V; ++i) {
        cout << i << "\t\t" << dist[i] << endl;
    }
}

void dijkstra(vector<Edge> &edges, int V, int source) {
    vector<int> dist(V, INT_MAX);
    dist[source] = 0;

    // Relax all edges |V| - 1 times
    for (int i = 0; i < V - 1; ++i) {
        for (Edge edge : edges) {
            relax(edge.source, edge.destination, edge.weight, dist);
        }
    }

    // Check for negative cycles
    if (detectNegativeCycle(edges, V, dist)) {
        cout << "Graph contains negative cycle!" << endl;
        return;
    }

    printShortestPaths(dist, V);
}

int main() {
    int V = 5; // Number of vertices
    int source = 0; // Source vertex

    vector<Edge> edges = {
        {0, 1, 4},
        {0, 2, 5},
        {1, 2, -2},
        {2, 3, 4},
        {3, 1, -1}
    };

    dijkstra(edges, V, source);

    return 0;
}
```

In this code, `detectNegativeCycle` function checks if there is any vertex `v` for which `dist[u] + weight(u, v) < dist[v]`. If such a vertex is found, it indicates the presence of a negative cycle. If no negative cycle is detected, the shortest paths are printed using the `printShortestPaths` function.

### 1. Algorithms & Data Structures (C++): Dijkstra Algorithms

Dijkstra's algorithm is a fundamental algorithm in computer science used to find the shortest paths between nodes in a graph, particularly in the context of weighted graphs where each edge has a non-negative weight. Here's a basic overview of how Dijkstra's algorithm works:

1. **Initialization**: Assign a tentative distance value to every node. Set the initial node's distance to 0 and all other nodes' distances to infinity. Keep track of which nodes are "unvisited".

2. **Selecting the nearest node**: Select the unvisited node with the smallest tentative distance. For the initial node, this will be the one with a distance of 0.

3. **Updating distances**: For the current node, consider all of its unvisited neighbors and calculate their tentative distances through the current node. Compare the newly calculated tentative distance to the current assigned value and assign the smaller one.

4. **Mark the current node as visited**: Once all of the neighbors of the current node have been considered, mark the current node as visited and remove it from the list of unvisited nodes.

5. **Termination condition**: Repeat steps 2-4 until either all nodes have been visited or the smallest tentative distance among the unvisited nodes is infinity (indicating that there are no more reachable nodes).

6. **Optimization**: Instead of searching through all unvisited nodes to find the one with the smallest tentative distance in each iteration, you can use a priority queue (min-heap) to efficiently select the node with the smallest tentative distance.

Here's a simple implementation of Dijkstra's algorithm in C++ using a priority queue:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>

using namespace std;

#define INF numeric_limits<int>::max()

// Data structure to represent a graph edge
struct Edge {
    int destination;
    int weight;
};

// Data structure to represent a graph
class Graph {
    int V; // Number of vertices
    vector<vector<Edge>> adjList; // Adjacency list

public:
    Graph(int vertices) : V(vertices) {
        adjList.resize(V);
    }

    // Add an edge to the graph
    void addEdge(int src, int dest, int weight) {
        adjList[src].push_back({dest, weight});
    }

    // Dijkstra's algorithm to find shortest paths from source to all other vertices
    void dijkstra(int source) {
        vector<int> dist(V, INF); // Initialize distances to infinity
        dist[source] = 0; // Distance from source to itself is 0

        // Priority queue to store vertices that are being processed
        priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
        pq.push({0, source});

        while (!pq.empty()) {
            int u = pq.top().second;
            pq.pop();

            // Traverse all adjacent vertices of u
            for (const auto& edge : adjList[u]) {
                int v = edge.destination;
                int weight = edge.weight;

                // If the distance to v through u is shorter than current distance to v, update it
                if (dist[u] != INF && dist[u] + weight < dist[v]) {
                    dist[v] = dist[u] + weight;
                    pq.push({dist[v], v});
                }
            }
        }

        // Print shortest distances
        cout << "Shortest distances from source vertex " << source << ":\n";
        for (int i = 0; i < V; ++i) {
            if (dist[i] == INF)
                cout << "Vertex " << i << ": unreachable\n";
            else
                cout << "Vertex " << i << ": " << dist[i] << '\n';
        }
    }
};

int main() {
    int V = 6; // Number of vertices
    Graph graph(V);

    // Example graph
    graph.addEdge(0, 1, 5);
    graph.addEdge(0, 2, 1);
    graph.addEdge(1, 3, 3);
    graph.addEdge(1, 4, 6);
    graph.addEdge(2, 1, 1);
    graph.addEdge(2, 3, 7);
    graph.addEdge(3, 4, 2);
    graph.addEdge(4, 5, 1);

    graph.dijkstra(0); // Finding shortest paths from vertex 0

    return 0;
}
```

This code demonstrates Dijkstra's algorithm applied to a simple graph with weighted edges. You can adjust the graph by adding or removing edges and vertices to test the algorithm further.

### 1. Algorithms & Data Structures (C++): Dijkstra Implementation

Sure, Dijkstra's algorithm is a popular algorithm for finding the shortest path from a starting node to all other nodes in a weighted graph. Below is a simple implementation of Dijkstra's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>

using namespace std;

#define INF numeric_limits<int>::max()

// Define a structure to represent a weighted edge
struct Edge {
    int to;
    int weight;
    Edge(int t, int w) : to(t), weight(w) {}
};

// Define a structure to represent a vertex
struct Vertex {
    int id;
    int distance;
    Vertex(int i, int d) : id(i), distance(d) {}
    // Overload the comparison operator for priority queue
    bool operator<(const Vertex& other) const {
        return distance > other.distance;
    }
};

// Dijkstra's algorithm implementation
vector<int> dijkstra(vector<vector<Edge>>& graph, int source) {
    int n = graph.size();
    vector<int> distance(n, INF);
    distance[source] = 0;
    
    // Priority queue to store vertices ordered by their distances
    priority_queue<Vertex> pq;
    pq.push(Vertex(source, 0));
    
    while (!pq.empty()) {
        Vertex current = pq.top();
        pq.pop();
        
        // Iterate over all neighboring vertices of current vertex
        for (Edge& e : graph[current.id]) {
            int new_distance = current.distance + e.weight;
            // If a shorter path is found, update the distance and push the vertex into the priority queue
            if (new_distance < distance[e.to]) {
                distance[e.to] = new_distance;
                pq.push(Vertex(e.to, new_distance));
            }
        }
    }
    
    return distance;
}

int main() {
    // Example graph represented as an adjacency list
    vector<vector<Edge>> graph = {
        {{1, 4}, {2, 1}},       // Node 0
        {{3, 2}},                // Node 1
        {{1, 5}, {3, 3}},        // Node 2
        {{4, 6}},                // Node 3
        {}                       // Node 4
    };
    
    int source = 0;
    vector<int> distances = dijkstra(graph, source);
    
    // Output the shortest distances from the source to all other nodes
    cout << "Shortest distances from node " << source << ":\n";
    for (int i = 0; i < distances.size(); ++i) {
        cout << "Node " << i << ": " << distances[i] << endl;
    }
    
    return 0;
}
```

This code includes the Dijkstra's algorithm implementation along with a simple example graph represented as an adjacency list. You can modify the `graph` variable to represent your own graph and specify the `source` node from which you want to find the shortest paths.

### 1. Algorithms & Data Structures (C++): Dijkstra's Algorithm

Dijkstra's algorithm is a popular method for finding the shortest path between nodes in a graph, especially when all edge weights are non-negative. Here's a high-level overview of how it works:

1. **Initialization**: Initialize a priority queue (or a min-heap) to store nodes, and set the distance of the starting node to 0 and all other nodes to infinity. Mark all nodes as unvisited.

2. **Relaxation Loop**: Repeat until the priority queue is empty:
   a. Extract the node with the smallest distance from the priority queue.
   b. For each neighbor of the current node that has not been visited:
      - Calculate the distance from the starting node to this neighbor through the current node.
      - If this distance is shorter than the previously recorded distance to the neighbor, update the distance.
      - Update the priority queue with the new distance.

3. **Termination**: When the priority queue becomes empty, all reachable nodes have been visited, and the shortest distances from the starting node to all other nodes have been found.

Here's a basic implementation of Dijkstra's algorithm in C++ using priority_queue and adjacency list representation:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>

using namespace std;

typedef pair<int, int> pii; // pair of (distance, node)

void dijkstra(vector<vector<pii>>& graph, int start, vector<int>& dist) {
    int n = graph.size();
    priority_queue<pii, vector<pii>, greater<pii>> pq; // min-heap

    dist.assign(n, numeric_limits<int>::max());
    dist[start] = 0;
    pq.push({0, start});

    while (!pq.empty()) {
        int u = pq.top().second;
        int d = pq.top().first;
        pq.pop();

        if (d > dist[u]) continue; // Skip if already relaxed

        for (const auto& neighbor : graph[u]) {
            int v = neighbor.first;
            int w = neighbor.second;

            if (dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;
                pq.push({dist[v], v});
            }
        }
    }
}

int main() {
    int n, m;
    cin >> n >> m; // Number of nodes and edges

    vector<vector<pii>> graph(n);
    for (int i = 0; i < m; ++i) {
        int u, v, w;
        cin >> u >> v >> w; // Edge (u, v) with weight w
        graph[u].push_back({v, w});
        graph[v].push_back({u, w}); // Uncomment for undirected graph
    }

    int start = 0; // Starting node
    vector<int> dist;
    dijkstra(graph, start, dist);

    cout << "Shortest distances from node " << start << ":\n";
    for (int i = 0; i < n; ++i) {
        cout << "Node " << i << ": " << dist[i] << "\n";
    }

    return 0;
}
```

In this code, `graph` is represented as an adjacency list where each element is a pair (v, w), indicating an edge from node `u` to node `v` with weight `w`. The `dijkstra` function calculates the shortest distances from the `start` node to all other nodes and stores them in the `dist` vector.

### 1. Algorithms & Data Structures (C++): Dijkstra's Algorithm for SSSP

Sure, Dijkstra's algorithm is a widely used algorithm for finding the shortest paths between nodes in a graph, which may represent, for example, road networks. Here's a basic implementation of Dijkstra's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <climits>

using namespace std;

#define INF INT_MAX // Infinity

// Edge structure to represent edges in the graph
struct Edge {
    int to;
    int weight;
    Edge(int _to, int _weight) : to(_to), weight(_weight) {}
};

// Graph class to represent the graph
class Graph {
private:
    int V; // Number of vertices
    vector<vector<Edge>> adj; // Adjacency list

public:
    Graph(int vertices) : V(vertices) {
        adj.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int from, int to, int weight) {
        adj[from].push_back(Edge(to, weight));
    }

    // Dijkstra's algorithm to find the shortest path from source to all vertices
    vector<int> dijkstra(int source) {
        vector<int> dist(V, INF); // Initialize distances to infinity
        dist[source] = 0; // Distance to source is 0
        priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq; // Min heap

        // Push the source node into the priority queue
        pq.push({0, source});

        while (!pq.empty()) {
            int u = pq.top().second; // Extract the vertex with minimum distance
            pq.pop();

            // Traverse all adjacent vertices of u
            for (Edge e : adj[u]) {
                int v = e.to;
                int weight = e.weight;

                // Relaxation step
                if (dist[v] > dist[u] + weight) {
                    dist[v] = dist[u] + weight;
                    pq.push({dist[v], v});
                }
            }
        }

        return dist;
    }
};

int main() {
    int V = 6; // Number of vertices
    Graph g(V);

    // Add edges to the graph
    g.addEdge(0, 1, 5);
    g.addEdge(0, 2, 3);
    g.addEdge(1, 3, 6);
    g.addEdge(1, 4, 2);
    g.addEdge(2, 1, 1);
    g.addEdge(2, 4, 7);
    g.addEdge(3, 4, 4);
    g.addEdge(3, 5, 2);
    g.addEdge(4, 5, 5);

    int source = 0; // Source vertex

    // Find shortest paths from source
    vector<int> shortestPaths = g.dijkstra(source);

    // Print shortest paths from source
    cout << "Shortest paths from vertex " << source << ":\n";
    for (int i = 0; i < V; ++i) {
        cout << "Vertex " << i << ": " << shortestPaths[i] << endl;
    }

    return 0;
}
```

In this implementation, the `Graph` class represents a graph using an adjacency list. The `addEdge` function adds edges to the graph. The `dijkstra` function finds the shortest paths from a given source vertex to all other vertices using Dijkstra's algorithm. Finally, in the `main` function, a graph is created, edges are added to it, and then Dijkstra's algorithm is applied to find the shortest paths from a specified source vertex.

### 1. Algorithms & Data Structures (C++): Dijkstra's Algorithm Visualization

Creating a visualization for Dijkstra's Algorithm in C++ can be quite exciting! You can use various graphics libraries like SFML or SDL to create a graphical representation of the algorithm's execution. Here's a basic outline of how you could approach it:

1. **Graph Representation**: Implement a graph data structure to represent the nodes and edges. You could use an adjacency list or matrix to represent the graph.

2. **Priority Queue**: Use a priority queue to keep track of the nodes with the minimum distance. In C++, you can use `std::priority_queue` for this purpose.

3. **Dijkstra's Algorithm Implementation**: Write the Dijkstra's algorithm function. It should iterate through the nodes, updating the distances and predecessors as necessary.

4. **Visualization**: Use a graphics library to visualize the graph and the algorithm's progress. You can represent nodes as circles and edges as lines. Highlight the nodes that are currently being visited or have been visited.

Here's a simple example to get you started:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>

// Node structure
struct Node {
    int id;
    int distance;
    bool visited;
};

// Graph representation using adjacency list
using Graph = std::vector<std::vector<std::pair<int, int>>>;

// Dijkstra's Algorithm function
void dijkstra(Graph& graph, int start) {
    int n = graph.size();
    std::vector<Node> nodes(n, {0, std::numeric_limits<int>::max(), false});
    nodes[start].distance = 0;

    // Priority queue to store nodes with minimum distance
    std::priority_queue<std::pair<int, int>, std::vector<std::pair<int, int>>, std::greater<std::pair<int, int>>> pq;
    pq.push({0, start});

    while (!pq.empty()) {
        int u = pq.top().second;
        pq.pop();
        nodes[u].visited = true;

        // Update distances of adjacent nodes
        for (const auto& neighbor : graph[u]) {
            int v = neighbor.first;
            int weight = neighbor.second;
            if (!nodes[v].visited && nodes[u].distance + weight < nodes[v].distance) {
                nodes[v].distance = nodes[u].distance + weight;
                pq.push({nodes[v].distance, v});
            }
        }
    }

    // Output the shortest distances
    for (int i = 0; i < n; ++i) {
        std::cout << "Shortest distance from node " << start << " to node " << i << " is " << nodes[i].distance << std::endl;
    }
}

int main() {
    // Example graph representation (weighted directed graph)
    Graph graph = {
        {{1, 4}, {2, 1}},    // Node 0
        {{3, 2}},            // Node 1
        {{1, 5}, {3, 3}},    // Node 2
        {{4, 6}},            // Node 3
        {{}}                 // Node 4
    };

    dijkstra(graph, 0); // Execute Dijkstra's algorithm from node 0

    return 0;
}
```

This code provides a basic implementation of Dijkstra's algorithm in C++. To visualize it, you'll need to integrate a graphics library and update the code accordingly.

### 1. Algorithms & Data Structures (C++): Dijkstras Algorithm

Dijkstra's algorithm is a popular algorithm in computer science used to find the shortest paths between nodes in a weighted graph. It was conceived by Dutch computer scientist Edsger W. Dijkstra in 1956 and is widely used in various applications including routing, network protocols, and optimization problems. Here's an overview of how Dijkstra's algorithm works and an implementation in C++:

#### How Dijkstra's Algorithm Works

1. **Initialization**: Start with a source node and set its distance from itself to 0, and all other nodes' distances to infinity. Also, maintain a priority queue or some other data structure to keep track of the next closest node to explore.

2. **Relaxation**: For each node, consider all its neighboring nodes and update their distance from the source if a shorter path is found through the current node.

3. **Selection of Next Node**: Choose the node with the smallest tentative distance from the source, which has not been visited yet.

4. **Repeat**: Continue the process until all nodes have been visited or the destination node is reached.

#### Implementation in C++

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>

using namespace std;

#define INF numeric_limits<int>::max()

// Graph edge representation
struct Edge {
    int to;
    int weight;
    Edge(int t, int w) : to(t), weight(w) {}
};

// Dijkstra's algorithm
vector<int> dijkstra(const vector<vector<Edge>>& graph, int source) {
    int n = graph.size();
    vector<int> dist(n, INF);
    vector<bool> visited(n, false);
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;

    dist[source] = 0;
    pq.push({0, source});

    while (!pq.empty()) {
        int u = pq.top().second;
        pq.pop();

        if (visited[u]) continue;
        visited[u] = true;

        for (const Edge& e : graph[u]) {
            int v = e.to;
            int w = e.weight;

            if (dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;
                pq.push({dist[v], v});
            }
        }
    }

    return dist;
}

int main() {
    int n, m; // Number of nodes and edges
    cin >> n >> m;

    vector<vector<Edge>> graph(n);

    // Reading edges
    for (int i = 0; i < m; ++i) {
        int u, v, w; // Edge from u to v with weight w
        cin >> u >> v >> w;
        graph[u].emplace_back(v, w);
    }

    int source; // Source node
    cin >> source;

    vector<int> shortest_paths = dijkstra(graph, source);

    // Output shortest paths from source to all other nodes
    for (int i = 0; i < n; ++i) {
        if (shortest_paths[i] == INF) {
            cout << "INF ";
        } else {
            cout << shortest_paths[i] << " ";
        }
    }
    cout << endl;

    return 0;
}
```

This code demonstrates Dijkstra's algorithm for finding the shortest paths from a source node to all other nodes in a graph represented as an adjacency list. You can customize it according to your specific needs and graph representation.

### 1. Algorithms & Data Structures (C++): Directed acyclic graphs in dynamic programming

Directed Acyclic Graphs (DAGs) are often used in dynamic programming to efficiently solve a variety of problems. One of the key characteristics of DAGs is that they contain no directed cycles, meaning you can traverse the graph from any starting node and never encounter the same node twice. This property makes them well-suited for dynamic programming, where solutions to subproblems can be stored and reused to avoid redundant computations.

Here's a general approach to using dynamic programming with DAGs in C++:

1. **Topological Ordering**: Since DAGs have no cycles, they can be linearly ordered such that if there is a directed edge from node u to node v, then u comes before v in the ordering. You can use algorithms like Kahn's algorithm or Depth-First Search (DFS) to find a topological ordering of the nodes in the graph.

2. **Define Subproblems**: Once you have a topological ordering, you can define subproblems based on this ordering. Typically, a subproblem corresponds to finding the optimal solution for a certain node given the optimal solutions for its predecessors in the topological order.

3. **Recurrence Relation**: Define a recurrence relation that expresses the optimal solution to a subproblem in terms of the optimal solutions to its predecessor subproblems.

4. **Dynamic Programming Table**: Create a table or array to store the solutions to the subproblems. You'll iterate through the nodes in the topological order, computing and storing the solutions to the subproblems.

5. **Compute Optimal Solutions**: Traverse the DAG in the topological order, computing the optimal solution for each node using the recurrence relation and the solutions to its predecessor subproblems.

Here's a simple example in C++ that illustrates how to find the longest path in a DAG using dynamic programming:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <climits>

using namespace std;

// Function to perform topological sorting using DFS
void topologicalSort(int node, vector<bool>& visited, vector<vector<int>>& adj, vector<int>& order) {
    visited[node] = true;
    for (int v : adj[node]) {
        if (!visited[v]) {
            topologicalSort(v, visited, adj, order);
        }
    }
    order.push_back(node);
}

// Function to find the longest path in a DAG using dynamic programming
int longestPathDAG(vector<vector<int>>& adj, int source, int destination) {
    int n = adj.size();
    vector<int> order;
    vector<bool> visited(n, false);
    for (int i = 0; i < n; ++i) {
        if (!visited[i]) {
            topologicalSort(i, visited, adj, order);
        }
    }
    reverse(order.begin(), order.end());

    vector<int> dist(n, INT_MIN);
    dist[source] = 0;
    for (int u : order) {
        if (dist[u] != INT_MIN) {
            for (int v : adj[u]) {
                dist[v] = max(dist[v], dist[u] + 1);
            }
        }
    }
    return dist[destination];
}

int main() {
    // Example graph represented as an adjacency list
    vector<vector<int>> adj = {
        {1, 2},
        {3},
        {3},
        {4},
        {5},
        {}
    };

    int longestPath = longestPathDAG(adj, 0, 5);
    cout << "Longest path length: " << longestPath << endl; // Output: Longest path length: 4

    return 0;
}
```

This example finds the longest path in a DAG from a source node to a destination node using dynamic programming. You can adapt this approach to solve various other problems on DAGs efficiently.

### 1. Algorithms & Data Structures (C++): Directed Graph

A directed graph, also known as a digraph, is a graph where edges have a direction. This means that the edges are ordered pairs of vertices. In C++, you can represent a directed graph using various data structures. One common approach is to use an adjacency list or an adjacency matrix.

Here's an example implementation of a directed graph using an adjacency list in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V) {
        adj.resize(V);
    }

    // Function to add an edge from u to v
    void addEdge(int u, int v) {
        adj[u].push_back(v);
    }

    // Function to print the adjacency list representation of the graph
    void printGraph() {
        for (int u = 0; u < V; ++u) {
            cout << "Vertex " << u << " is connected to:";
            for (int v : adj[u]) {
                cout << " " << v;
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 4 vertices
    Graph graph(4);

    // Add edges
    graph.addEdge(0, 1);
    graph.addEdge(0, 2);
    graph.addEdge(1, 2);
    graph.addEdge(2, 0);
    graph.addEdge(2, 3);
    graph.addEdge(3, 3);

    // Print the adjacency list representation of the graph
    graph.printGraph();

    return 0;
}
```

In this implementation, `Graph` is a class representing the directed graph. It has a member variable `adj` which is a vector of vectors to store the adjacency list. The `addEdge` function is used to add edges to the graph, and `printGraph` function is used to print the adjacency list representation of the graph.

You can further extend this implementation by adding more functionalities like BFS (Breadth First Search) or DFS (Depth First Search) traversal for directed graphs, finding cycles, shortest paths, etc.

### 1. Algorithms & Data Structures (C++): Directed Graph Implementation - Adjacency List

Sure, implementing a directed graph using an adjacency list in C++ is a fundamental data structure task. Below is a basic implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adjList; // Adjacency list

public:
    // Constructor
    Graph(int vertices) {
        V = vertices;
        adjList.resize(V);
    }

    // Function to add an edge from vertex u to vertex v
    void addEdge(int u, int v) {
        adjList[u].push_back(v);
    }

    // Function to print the adjacency list representation of the graph
    void printGraph() {
        for (int i = 0; i < V; ++i) {
            cout << "Adjacency list of vertex " << i << ": ";
            for (int j = 0; j < adjList[i].size(); ++j) {
                cout << adjList[i][j] << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph g(5);

    // Add edges
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(2, 4);
    g.addEdge(3, 4);

    // Print the adjacency list representation of the graph
    g.printGraph();

    return 0;
}
```

This code creates a class `Graph` with member functions to add edges and print the adjacency list representation of the graph. In the `main()` function, an instance of the `Graph` class is created with 5 vertices, and some edges are added. Finally, the adjacency list representation is printed.

### 1. Algorithms & Data Structures (C++): Directed Graph Implementation - Adjacency Matrix

Implementing a directed graph using an adjacency matrix in C++ involves representing connections between vertices using a 2D array. Here's a basic implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class DirectedGraph {
private:
    int numVertices;
    vector<vector<bool>> adjacencyMatrix;

public:
    DirectedGraph(int numVertices) {
        this->numVertices = numVertices;
        adjacencyMatrix.resize(numVertices, vector<bool>(numVertices, false));
    }

    void addEdge(int from, int to) {
        if (from >= 0 && from < numVertices && to >= 0 && to < numVertices) {
            adjacencyMatrix[from][to] = true;
        } else {
            cerr << "Invalid vertex index" << endl;
        }
    }

    void removeEdge(int from, int to) {
        if (from >= 0 && from < numVertices && to >= 0 && to < numVertices) {
            adjacencyMatrix[from][to] = false;
        } else {
            cerr << "Invalid vertex index" << endl;
        }
    }

    bool hasEdge(int from, int to) {
        if (from >= 0 && from < numVertices && to >= 0 && to < numVertices) {
            return adjacencyMatrix[from][to];
        } else {
            cerr << "Invalid vertex index" << endl;
            return false;
        }
    }

    void printGraph() {
        for (int i = 0; i < numVertices; ++i) {
            for (int j = 0; j < numVertices; ++j) {
                cout << adjacencyMatrix[i][j] << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    DirectedGraph graph(5);

    graph.addEdge(0, 1);
    graph.addEdge(0, 3);
    graph.addEdge(1, 2);
    graph.addEdge(2, 3);
    graph.addEdge(3, 4);

    cout << "Adjacency Matrix Representation:" << endl;
    graph.printGraph();

    return 0;
}
```

This code defines a `DirectedGraph` class with methods to add edges, remove edges, check if an edge exists, and print the adjacency matrix representation of the graph. In the main function, an instance of the `DirectedGraph` class is created, edges are added, and then the adjacency matrix is printed.

This implementation assumes that the vertices are indexed from 0 to `numVertices - 1`. It's a basic implementation; you can extend it by adding more functionalities like checking for cycles, finding shortest paths, etc., depending on your requirements.

### 1. Algorithms & Data Structures (C++): Directed Graphs

Directed graphs, also known as digraphs, are graphs where edges have a direction associated with them. They consist of a set of vertices (nodes) and a set of directed edges (arcs) where each edge is represented as an ordered pair of vertices.

In C++, you can represent a directed graph using various data structures. One common approach is to use an adjacency list or an adjacency matrix.

Here's a basic implementation of a directed graph using an adjacency list:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V) {
        adj.resize(V);
    }

    // Function to add an edge from v to w
    void addEdge(int v, int w) {
        adj[v].push_back(w);
    }

    // Function to print the adjacency list representation of the graph
    void printGraph() {
        for (int v = 0; v < V; ++v) {
            cout << "Adjacency list of vertex " << v << ": ";
            for (int w : adj[v]) {
                cout << w << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph graph(5);

    // Add some directed edges
    graph.addEdge(0, 1);
    graph.addEdge(0, 2);
    graph.addEdge(1, 3);
    graph.addEdge(2, 3);
    graph.addEdge(3, 4);

    // Print the adjacency list representation of the graph
    graph.printGraph();

    return 0;
}
```

In this implementation, the `Graph` class represents a directed graph. It has a private member `adj`, which is a vector of vectors representing the adjacency list. Each element of `adj` is a vector containing the indices of vertices that are adjacent to the corresponding vertex.

You can add edges to the graph using the `addEdge` method and print the adjacency list using the `printGraph` method.

This is a basic example. Depending on your specific requirements, you may need to add more functionalities such as checking for cycles, finding shortest paths, or performing other graph algorithms.

### 1. Algorithms & Data Structures (C++): Directed Graphs & SCC's

Directed graphs and strongly connected components (SCCs) are fundamental concepts in graph theory and are crucial in various computer science applications, including network analysis, routing algorithms, and compilers. Let's delve into them:

#### Directed Graphs

A directed graph, or digraph, consists of a set of vertices/nodes and a set of directed edges/links connecting pairs of vertices. Each edge has a direction, indicating a one-way relationship between nodes.

In C++, you can represent a directed graph using adjacency lists or adjacency matrices.

#### Adjacency List Representation

In an adjacency list representation, each vertex of the graph is associated with a list of its neighboring vertices.

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V), adj(V) {}

    // Function to add an edge to the graph
    void addEdge(int u, int v) {
        adj[u].push_back(v);
    }

    // Function to print the adjacency list representation of the graph
    void printGraph() {
        for (int u = 0; u < V; ++u) {
            cout << "Adjacency list of vertex " << u << ": ";
            for (int v : adj[u]) {
                cout << v << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph graph(5);

    // Add edges
    graph.addEdge(0, 1);
    graph.addEdge(1, 2);
    graph.addEdge(2, 3);
    graph.addEdge(3, 4);
    graph.addEdge(4, 0);

    // Print the graph
    graph.printGraph();

    return 0;
}
```

#### Strongly Connected Components (SCCs)

A strongly connected component of a directed graph is a maximal set of vertices such that there is a directed path between every pair of vertices within the set.

#### Kosaraju's Algorithm

Kosaraju's algorithm is a linear-time algorithm to find all the strongly connected components in a directed graph.

Here's how it works:

1. Perform a Depth First Search (DFS) on the graph and keep track of the order in which vertices finish DFS traversal.
2. Reverse the graph (i.e., reverse the direction of all edges).
3. Perform DFS on the reversed graph starting from vertices in the order obtained in step 1. Each DFS traversal starting from an unvisited vertex yields a strongly connected component.

Let's implement Kosaraju's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <stack>
#include <algorithm>

using namespace std;

class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list
    vector<bool> visited; // To keep track of visited vertices

public:
    Graph(int V) : V(V), adj(V), visited(V, false) {}

    // Function to add an edge to the graph
    void addEdge(int u, int v) {
        adj[u].push_back(v);
    }

    // Function to perform DFS
    void DFS(int v, stack<int> &s) {
        visited[v] = true;
        for (int u : adj[v]) {
            if (!visited[u]) {
                DFS(u, s);
            }
        }
        s.push(v);
    }

    // Function to perform DFS on the reversed graph
    void DFSReverse(int v, vector<int> &component) {
        visited[v] = true;
        component.push_back(v);
        for (int u : adj[v]) {
            if (!visited[u]) {
                DFSReverse(u, component);
            }
        }
    }

    // Function to find strongly connected components
    vector<vector<int>> findSCCs() {
        stack<int> s;
        vector<vector<int>> SCCs;

        // Step 1: Perform DFS and fill the stack
        for (int v = 0; v < V; ++v) {
            if (!visited[v]) {
                DFS(v, s);
            }
        }

        // Step 2: Reverse the graph
        reverse(adj.begin(), adj.end());

        // Step 3: Perform DFS on the reversed graph
        fill(visited.begin(), visited.end(), false);
        while (!s.empty()) {
            int v = s.top();
            s.pop();
            if (!visited[v]) {
                vector<int> component;
                DFSReverse(v, component);
                SCCs.push_back(component);
            }
        }

        return SCCs;
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph graph(5);

    // Add edges
    graph.addEdge(0, 1);
    graph.addEdge(1, 2);
    graph.addEdge(2, 0);
    graph.addEdge(1, 3);
    graph.addEdge(3, 4);

    // Find strongly connected components
    vector<vector<int>> SCCs = graph.findSCCs();

    // Print SCCs
    cout << "Strongly Connected Components:\n";
    for (const auto &component : SCCs) {
        for (int v : component) {
            cout << v << " ";
        }
        cout << endl;
    }

    return 0;
}
```

This code demonstrates how to find strongly connected components in a directed graph using Kosaraju's algorithm in C++.

### 1. Algorithms & Data Structures (C++): Directed vs Undirected graphs

Directed and undirected graphs are fundamental concepts in graph theory and have significant implications for algorithms and data structures. Let's break down their differences and explore how they affect the implementation and usage of algorithms in C++.

#### Directed Graphs

1. **Definition**: In a directed graph, also known as a digraph, edges have a direction. Each edge connects two vertices and has an associated direction, indicating a one-way relationship between the vertices.

2. **Representation**: Directed graphs can be represented using adjacency lists or adjacency matrices. In C++, adjacency lists are commonly used due to their efficiency in representing sparse graphs.

3. **Applications**: Directed graphs are useful in modeling relationships where there is a clear directionality. Examples include social networks (where edges represent "follow" relationships), transportation networks (where edges represent one-way streets or flight routes), and dependency graphs in software engineering.

4. **Algorithms**: Algorithms such as depth-first search (DFS), breadth-first search (BFS), topological sorting, and finding strongly connected components are commonly applied to directed graphs.

#### Undirected Graphs

1. **Definition**: In an undirected graph, edges have no direction. They simply represent a connection between two vertices without any notion of directionality.

2. **Representation**: Similar to directed graphs, undirected graphs can be represented using adjacency lists or adjacency matrices. Again, adjacency lists are preferred for their efficiency, especially for sparse graphs.

3. **Applications**: Undirected graphs are useful for modeling symmetric relationships where the direction of the relationship is irrelevant. Examples include social networks (where edges represent friendships), road networks (where edges represent two-way streets), and communication networks.

4. **Algorithms**: Common algorithms for undirected graphs include DFS, BFS, finding connected components, minimum spanning tree (e.g., Prim's or Kruskal's algorithm), and shortest path algorithms (e.g., Dijkstra's algorithm or Bellman-Ford algorithm).

In C++, you can implement both directed and undirected graphs using classes and data structures. Here's a brief overview of how you might implement a simple undirected graph using an adjacency list:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adjList; // Adjacency list

public:
    Graph(int vertices) : V(vertices) {
        adjList.resize(V);
    }

    void addEdge(int u, int v) {
        adjList[u].push_back(v);
        adjList[v].push_back(u); // For undirected graph, add edge in both directions
    }

    void printGraph() {
        for (int i = 0; i < V; ++i) {
            cout << "Adjacency list of vertex " << i << ": ";
            for (int v : adjList[i]) {
                cout << v << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 3);
    g.printGraph();
    return 0;
}
```

For a directed graph, you'd only add one edge when adding an edge between two vertices, and you'd typically need to implement different algorithms accordingly.

Understanding the distinction between directed and undirected graphs is crucial for effectively applying graph algorithms and solving various real-world problems efficiently.

### 1. Algorithms & Data Structures (C++): Djkitras Algorithm

It seems like you may be referring to the Dijkstra's algorithm, named after Dutch computer scientist Edsger W. Dijkstra. This algorithm is a fundamental technique in graph theory and computer science for finding the shortest paths between nodes in a graph, which may represent, for example, road networks or computer networks.

Here's a brief overview of how Dijkstra's algorithm works:

1. **Initialization**: Assign a tentative distance value to every node. Set the initial node's distance to zero and all other nodes' distances to infinity. Keep track of the previous node that leads to each node in the shortest path.

2. **Selection of the next node**: Among the nodes whose distance is not yet finalized, select the one with the smallest tentative distance.

3. **Update distances**: For the selected node, consider all of its neighbors and calculate their tentative distances by summing the node's distance with the weight of the edge connecting them. If this tentative distance is smaller than the previously assigned distance, update the neighbor's distance.

4. **Mark the selected node as visited**: Once all neighbors have been considered, mark the selected node as visited.

5. **Repeat**: Repeat steps 2 to 4 until all nodes have been visited.

6. **Path reconstruction**: After the algorithm completes, the shortest path from the initial node to any other node can be obtained by backtracking from the destination node using the information stored during the algorithm's execution.

Dijkstra's algorithm is commonly implemented using a priority queue or a heap data structure to efficiently select the node with the smallest tentative distance in each iteration.

Here's a simple implementation of Dijkstra's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>

using namespace std;

#define INF numeric_limits<int>::max()

// Edge structure to represent graph edges
struct Edge {
    int dest;
    int weight;
};

// Function to implement Dijkstra's algorithm
void dijkstra(const vector<vector<Edge>>& graph, int source) {
    int n = graph.size(); // Number of nodes in the graph
    vector<int> dist(n, INF); // Array to store shortest distances
    vector<bool> visited(n, false); // Array to track visited nodes

    // Priority queue to store nodes based on their distance
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;

    // Initialize distance from source to itself
    dist[source] = 0;
    pq.push({0, source});

    // Dijkstra's algorithm
    while (!pq.empty()) {
        int u = pq.top().second;
        pq.pop();

        // Skip if node is already visited
        if (visited[u]) continue;

        visited[u] = true;

        // Update distance for each neighbor of u
        for (const Edge& edge : graph[u]) {
            int v = edge.dest;
            int weight = edge.weight;
            if (dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
                pq.push({dist[v], v});
            }
        }
    }

    // Print shortest distances from source
    cout << "Shortest distances from node " << source << ":\n";
    for (int i = 0; i < n; ++i) {
        cout << "Node " << i << ": " << dist[i] << "\n";
    }
}

int main() {
    // Example graph represented as an adjacency list
    vector<vector<Edge>> graph = {
        {{1, 4}, {2, 1}},    // Node 0
        {{3, 2}},            // Node 1
        {{1, 3}, {3, 5}},    // Node 2
        {{4, 3}},            // Node 3
        {}                   // Node 4
    };

    dijkstra(graph, 0); // Find shortest paths from node 0

    return 0;
}
```

This code demonstrates Dijkstra's algorithm with a sample graph represented as an adjacency list. You can modify the `graph` variable to represent your specific graph and call the `dijkstra` function with the appropriate source node.

### 1. Algorithms & Data Structures (C++): Dry run for All pair shortest path

Sure, let's do a dry run for the All Pair Shortest Path algorithm using Floyd-Warshall's algorithm in C++.

```cpp
#include <iostream>
#include <vector>
using namespace std;

#define INF 99999

void printMatrix(vector<vector<int>>& dist) {
    int V = dist.size();
    for (int i = 0; i < V; i++) {
        for (int j = 0; j < V; j++) {
            if (dist[i][j] == INF)
                cout << "INF ";
            else
                cout << dist[i][j] << " ";
        }
        cout << endl;
    }
}

void floydWarshall(vector<vector<int>>& graph) {
    int V = graph.size();
    vector<vector<int>> dist(V, vector<int>(V));

    for (int i = 0; i < V; i++) {
        for (int j = 0; j < V; j++) {
            dist[i][j] = graph[i][j];
        }
    }

    for (int k = 0; k < V; k++) {
        for (int i = 0; i < V; i++) {
            for (int j = 0; j < V; j++) {
                if (dist[i][k] != INF && dist[k][j] != INF && dist[i][k] + dist[k][j] < dist[i][j])
                    dist[i][j] = dist[i][k] + dist[k][j];
            }
        }
    }

    printMatrix(dist);
}

int main() {
    vector<vector<int>> graph = {
        {0,   5,  INF, 10},
        {INF, 0,   3, INF},
        {INF, INF, 0,   1},
        {INF, INF, INF, 0}
    };
    floydWarshall(graph);
    return 0;
}
```

Now, let's do a dry run for this algorithm:

1. **Initialization**: We initialize a matrix `dist` with the same values as the input graph. We'll use this matrix to store the shortest distances between all pairs of vertices.

2. **Iteration**: We iterate over all vertices as intermediate vertices. Let the intermediate vertex be 'k'. For every pair (i, j) of source and destination vertices, we check if vertex 'k' can be included in the shortest path from 'i' to 'j'. If including vertex 'k' shortens the path, we update the value of `dist[i][j]` to the new shorter path.

3. **Termination**: After the completion of the above process, the 'dist' matrix will contain the shortest distance between all pairs of vertices.

4. **Printing**: Finally, we print the 'dist' matrix which represents the shortest distances between all pairs of vertices.

Let's execute this code with the provided graph:

```plaintext
0 5 8 9 
INF 0 3 4 
INF INF 0 1 
INF INF INF 0 
```

This output indicates the shortest distances between all pairs of vertices in the given graph.

### 1. Algorithms & Data Structures (C++): Graph Representation

In C++, graphs can be represented using various data structures such as adjacency matrix, adjacency list, or an edge list. Here's a brief overview of each representation:

1. **Adjacency Matrix**:
   - An adjacency matrix is a 2D array of size V x V, where V is the number of vertices in the graph.
   - If there is an edge between vertex i and vertex j, then matrix[i][j] = 1, otherwise matrix[i][j] = 0 (or some other value to represent weights in a weighted graph).
   - It's efficient for dense graphs but consumes more space for sparse graphs.

```cpp
#include <iostream>
#include <vector>

using namespace std;

const int MAX = 100;
int graph[MAX][MAX];

// Initialize graph with all zeros
void initGraph(int V) {
    for (int i = 0; i < V; ++i)
        for (int j = 0; j < V; ++j)
            graph[i][j] = 0;
}

// Add edge to the graph
void addEdge(int u, int v) {
    graph[u][v] = 1;
    graph[v][u] = 1; // If it's an undirected graph
}

int main() {
    int V = 5; // Number of vertices
    initGraph(V);

    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 2);
    addEdge(2, 3);
    addEdge(3, 4);

    // Print the adjacency matrix
    for (int i = 0; i < V; ++i) {
        for (int j = 0; j < V; ++j)
            cout << graph[i][j] << " ";
        cout << endl;
    }

    return 0;
}
```

1. **Adjacency List**:
   - An adjacency list is a collection of lists or arrays where each list/array represents the vertices adjacent to a particular vertex.
   - It's more memory-efficient for sparse graphs.

```cpp
#include <iostream>
#include <vector>

using namespace std;

vector<int> adjList[MAX];

// Add edge to the adjacency list
void addEdge(int u, int v) {
    adjList[u].push_back(v);
    adjList[v].push_back(u); // If it's an undirected graph
}

int main() {
    int V = 5; // Number of vertices

    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 2);
    addEdge(2, 3);
    addEdge(3, 4);

    // Print the adjacency list
    for (int i = 0; i < V; ++i) {
        cout << "Adjacency list of vertex " << i << ": ";
        for (int j : adjList[i])
            cout << j << " ";
        cout << endl;
    }

    return 0;
}
```

1. **Edge List**:
   - An edge list is a collection of edges represented as pairs (u, v), where u and v are vertices connected by an edge.
   - It's useful for certain algorithms and memory-efficient for very sparse graphs.

```cpp
#include <iostream>
#include <vector>

using namespace std;

struct Edge {
    int u, v;
};

vector<Edge> edges;

// Add edge to the edge list
void addEdge(int u, int v) {
    edges.push_back({u, v});
    edges.push_back({v, u}); // If it's an undirected graph
}

int main() {
    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 2);
    addEdge(2, 3);
    addEdge(3, 4);

    // Print the edge list
    cout << "Edge list:\n";
    for (const auto& edge : edges) {
        cout << edge.u << " -- " << edge.v << endl;
    }

    return 0;
}
```

Choose the representation based on the characteristics of your graph and the operations you need to perform efficiently.

### 1. Algorithms & Data Structures (C++): Graph Representations

Graphs can be represented in various ways in C++. The choice of representation depends on factors like the type of graph (directed or undirected), the operations to be performed on the graph, and the efficiency required for those operations. Here are some common representations:

1. **Adjacency Matrix:**
   - In this representation, a 2D array (matrix) is used where the rows and columns represent the vertices of the graph.
   - If the graph is undirected, `matrix[i][j]` and `matrix[j][i]` are set to 1 if there is an edge between vertices `i` and `j`. For directed graphs, only one of these may be set, depending on the direction of the edge.
   - This representation consumes more memory, especially for sparse graphs, but offers faster edge retrieval (O(1) time complexity).

2. **Adjacency List:**
   - In this representation, each vertex of the graph maintains a list of adjacent vertices.
   - This can be implemented using arrays, linked lists, or other data structures.
   - For example, in C++, you can use a vector of vectors, where the outer vector represents each vertex and the inner vector represents its adjacent vertices.
   - This representation consumes less memory, especially for sparse graphs, and is more efficient for iterating over vertices and their neighbors.

3. **Edge List:**
   - This representation simply stores a list of edges. Each edge is represented as a pair of vertices.
   - It can be implemented using arrays or vectors of pairs.
   - This representation is memory efficient but less efficient for operations like finding all neighbors of a vertex.

Here's a basic example of how you might implement an adjacency list representation in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
    int V; // Number of vertices
    vector<vector<int>> adjList; // Adjacency list

public:
    Graph(int V) {
        this->V = V;
        adjList.resize(V);
    }

    // Function to add an edge from v to w
    void addEdge(int v, int w) {
        adjList[v].push_back(w);
        // For undirected graphs, uncomment the line below
        // adjList[w].push_back(v);
    }

    // Function to print the adjacency list representation of the graph
    void printGraph() {
        for (int v = 0; v < V; ++v) {
            cout << "Adjacency list of vertex " << v << ": ";
            for (auto w : adjList[v])
                cout << "-> " << w;
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph g(5);
    // Add edges
    g.addEdge(0, 1);
    g.addEdge(0, 4);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 3);
    g.addEdge(3, 4);

    // Print the adjacency list representation of the graph
    g.printGraph();

    return 0;
}
```

This is just a basic overview, and there are more advanced techniques and representations depending on the specific needs of your application and the algorithms you plan to implement.

### 1. Algorithms & Data Structures (C++): Graph Representations: Adjacency Lists

In the realm of algorithms and data structures, graph representations play a crucial role in efficiently storing and manipulating graph data. One popular representation is the adjacency list. In C++, you can implement adjacency lists using various data structures like vectors, lists, or sets, depending on your specific requirements.

Here's a basic implementation of an adjacency list representation for a graph using C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to add an edge to the graph
void addEdge(vector<vector<int>>& adj, int u, int v) {
    // Assuming an undirected graph
    adj[u].push_back(v);
    adj[v].push_back(u);
}

// Function to print the adjacency list representation of the graph
void printGraph(const vector<vector<int>>& adj) {
    for (int i = 0; i < adj.size(); ++i) {
        cout << "Adjacency list of vertex " << i << ": ";
        for (int j = 0; j < adj[i].size(); ++j) {
            cout << adj[i][j] << " ";
        }
        cout << endl;
    }
}

int main() {
    int V = 5; // Number of vertices

    // Create an adjacency list representation using vectors
    vector<vector<int>> adj(V);

    // Add edges
    addEdge(adj, 0, 1);
    addEdge(adj, 0, 4);
    addEdge(adj, 1, 2);
    addEdge(adj, 1, 3);
    addEdge(adj, 1, 4);
    addEdge(adj, 2, 3);
    addEdge(adj, 3, 4);

    // Print the adjacency list representation of the graph
    printGraph(adj);

    return 0;
}
```

In this code:

- `addEdge()` function adds an edge between two vertices `u` and `v`.
- `printGraph()` function prints the adjacency list representation of the graph.
- In the `main()` function, we create an adjacency list (`adj`) using a vector of vectors. Each vector represents the list of vertices adjacent to a particular vertex.

Feel free to modify this code according to your specific needs or to optimize it further.

### 1. Algorithms & Data Structures (C++): Graph Representations: Adjacency Matrix

In C++, an adjacency matrix is a common way to represent a graph. It's a 2D array where the value at `matrix[i][j]` represents whether there is an edge from vertex `i` to vertex `j`.

Here's a simple implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
private:
    int numVertices;
    vector<vector<int>> adjMatrix;

public:
    Graph(int numVertices) {
        this->numVertices = numVertices;
        adjMatrix.resize(numVertices, vector<int>(numVertices, 0));
    }

    void addEdge(int source, int destination) {
        // Assuming undirected graph
        adjMatrix[source][destination] = 1;
        adjMatrix[destination][source] = 1;
    }

    void printMatrix() {
        cout << "Adjacency Matrix:" << endl;
        for (int i = 0; i < numVertices; ++i) {
            for (int j = 0; j < numVertices; ++j) {
                cout << adjMatrix[i][j] << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    Graph graph(5); // Example: Graph with 5 vertices
    graph.addEdge(0, 1);
    graph.addEdge(0, 4);
    graph.addEdge(1, 2);
    graph.addEdge(1, 3);
    graph.addEdge(1, 4);
    graph.addEdge(2, 3);
    graph.addEdge(3, 4);

    graph.printMatrix();

    return 0;
}
```

In this example:

- We define a `Graph` class with a constructor to initialize the number of vertices and create an empty adjacency matrix.
- The `addEdge` method adds an edge between two vertices by setting the corresponding positions in the adjacency matrix to 1.
- The `printMatrix` method simply prints the adjacency matrix.

This is a basic implementation; you can extend it to support weighted graphs by storing weights instead of just 0 and 1. Also, remember this approach consumes more memory, especially for sparse graphs.

### 1. Algorithms & Data Structures (C++): Graph Representations: Packed Adjacency List

A packed adjacency list is a space-efficient way to represent a graph, especially when memory is a concern and the graph is sparse. In this representation, you store all the edges of the graph in a single array, which is essentially a packed version of the adjacency list.

Here's how you can implement a packed adjacency list in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Edge structure to represent an edge between two nodes
struct Edge {
    int to;  // destination node of the edge
    int weight;  // weight/cost of the edge (if the graph is weighted)
    
    Edge(int _to, int _weight) : to(_to), weight(_weight) {}
};

// Graph class
class Graph {
private:
    int numNodes;  // number of nodes in the graph
    vector<Edge> edges;  // array to store all edges (packed representation)
    vector<int> offsets;  // array to store offsets to edges of each node
    
public:
    // Constructor
    Graph(int n) : numNodes(n), offsets(n + 1, 0) {}

    // Add an edge to the graph
    void addEdge(int from, int to, int weight = 1) {
        edges.push_back(Edge(to, weight));  // add the edge to the edges array
        offsets[from + 1]++;  // increment the offset for the next node
    }

    // Build the packed representation of the graph
    void build() {
        for (int i = 1; i <= numNodes; ++i) {
            offsets[i] += offsets[i - 1];  // cumulative sum to get the offsets
        }
    }

    // Get the neighbors of a node
    vector<Edge> getNeighbors(int node) {
        vector<Edge> neighbors;
        for (int i = offsets[node]; i < offsets[node + 1]; ++i) {
            neighbors.push_back(edges[i]);
        }
        return neighbors;
    }
};

int main() {
    // Example usage
    int numNodes = 5;
    Graph graph(numNodes);

    // Add edges
    graph.addEdge(0, 1);
    graph.addEdge(0, 3);
    graph.addEdge(1, 2);
    graph.addEdge(1, 3);
    graph.addEdge(2, 4);
    graph.addEdge(3, 2);
    graph.addEdge(4, 0);

    // Build the packed representation
    graph.build();

    // Get neighbors of each node
    for (int i = 0; i < numNodes; ++i) {
        cout << "Neighbors of node " << i << ": ";
        vector<Edge> neighbors = graph.getNeighbors(i);
        for (const Edge& edge : neighbors) {
            cout << edge.to << " ";
        }
        cout << endl;
    }

    return 0;
}
```

In this implementation:

- The `Edge` struct represents an edge between two nodes. It contains the destination node (`to`) and optionally a weight/cost (`weight`).
- The `Graph` class maintains three private members: `numNodes` (number of nodes), `edges` (vector to store all edges), and `offsets` (vector to store offsets to edges of each node).
- The `addEdge` method adds an edge to the graph. It appends the edge to the `edges` array and increments the appropriate offset in the `offsets` array.
- The `build` method calculates cumulative sums of the `offsets` array to prepare it for efficient neighbor retrieval.
- The `getNeighbors` method retrieves the neighbors of a given node by accessing the appropriate range in the `edges` array using the offsets.

This implementation is efficient in terms of memory usage, especially for sparse graphs, as it avoids storing redundant information.

### 1. Algorithms & Data Structures (C++): Graph Sequence (Graph + Dynamic Programming)

Certainly! Graph sequences can be a fascinating topic that combines both graph theory and dynamic programming. Let's break it down.

#### Graphs

A graph is a collection of nodes (vertices) and edges that connect these nodes. Graphs can be represented in many ways, including adjacency lists, adjacency matrices, edge lists, etc. In C++, you might use classes or data structures to represent graphs.

```cpp
class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V) {
        adj.resize(V);
    }

    void addEdge(int u, int v) {
        adj[u].push_back(v);
        // For undirected graph, add adj[v].push_back(u);
    }

    vector<int>& getNeighbors(int u) {
        return adj[u];
    }

    int getVertexCount() {
        return V;
    }
};
```

#### Dynamic Programming on Graphs

Dynamic programming on graphs involves breaking down a problem into smaller subproblems and solving each subproblem only once, storing the results to avoid redundant computations. Common dynamic programming techniques on graphs include shortest path algorithms (like Dijkstra's or Floyd-Warshall), tree dynamic programming, and more.

Here's a basic example of dynamic programming on a graph, finding the shortest path between two nodes using Dijkstra's algorithm:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>
using namespace std;

const int INF = numeric_limits<int>::max();

vector<int> dijkstra(Graph& graph, int source) {
    int V = graph.getVertexCount();
    vector<int> dist(V, INF);
    dist[source] = 0;
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    pq.push({0, source});

    while (!pq.empty()) {
        int u = pq.top().second;
        int d = pq.top().first;
        pq.pop();

        if (d > dist[u]) continue;

        for (int v : graph.getNeighbors(u)) {
            int w = 1; // Weight of edge u->v (assuming unweighted graph)
            if (dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;
                pq.push({dist[v], v});
            }
        }
    }

    return dist;
}
```

#### Graph Sequence

A graph sequence refers to a sequence of graphs that often exhibit some sort of pattern or relationship between them. For example, in the context of dynamic programming, you might be interested in finding the shortest path in a series of graphs that evolve over time or change based on certain conditions.

Combining graph theory with dynamic programming allows you to solve complex problems efficiently by breaking them down into smaller, more manageable subproblems. Graph sequences are just one example of how these two concepts can be combined to tackle real-world problems.

Would you like to explore a specific problem or concept related to graph sequences further?

### 1. Algorithms & Data Structures (C++): Graph Terminology

Sure! Let's delve into some fundamental graph terminology in the context of algorithms and data structures in C++.

1. **Graph**: A graph is a collection of nodes (vertices) and edges that connect pairs of nodes. In C++, graphs can be represented using adjacency matrices, adjacency lists, or other data structures.

2. **Vertex (Node)**: A vertex, or node, is a fundamental unit of a graph. It represents an entity and can have associated data.

3. **Edge**: An edge is a connection between two vertices in a graph. It can be directed or undirected, depending on whether it has a specific direction associated with it.

4. **Directed Graph**: In a directed graph, edges have a direction associated with them. If an edge connects vertex A to vertex B, it means that there is a directed path from A to B.

5. **Undirected Graph**: In an undirected graph, edges do not have a direction associated with them. If an edge connects vertex A to vertex B, it implies that there is a connection between A and B without specifying a direction.

6. **Weighted Graph**: In a weighted graph, each edge has an associated weight or cost. These weights can represent various things such as distance, cost, time, etc.

7. **Path**: A path in a graph is a sequence of vertices where each adjacent pair is connected by an edge. The length of a path is the number of edges it contains.

8. **Cycle**: A cycle in a graph is a path that starts and ends at the same vertex, traversing through other vertices and edges in between.

9. **Connected Graph**: A connected graph is a graph in which there is a path between every pair of vertices. In a directed graph, this implies that there is a directed path between every pair of vertices.

10. **Disconnected Graph**: A disconnected graph is a graph in which there are two or more vertices with no path connecting them.

11. **Degree**: The degree of a vertex is the number of edges incident to it. In a directed graph, the in-degree of a vertex is the number of edges pointing towards it, and the out-degree is the number of edges pointing away from it.

12. **Adjacency Matrix**: An adjacency matrix is a square matrix used to represent a graph. The element in row \( i \) and column \( j \) represents the presence or absence of an edge between vertex \( i \) and vertex \( j \).

13. **Adjacency List**: An adjacency list is a collection of lists or arrays used to represent a graph. Each list represents the vertices adjacent to a particular vertex.

These are some of the fundamental terms you'll encounter when working with graphs in the context of algorithms and data structures in C++. Understanding these terms is crucial for implementing graph algorithms effectively.

### 1. Algorithms & Data Structures (C++): Graph Traversal - Breadth First Search (Breadth First Search)

Breadth First Search (BFS) is a fundamental graph traversal algorithm used to explore nodes in a graph level by level. It starts at a chosen node (often referred to as the "source" node) and explores all of its neighbors at the present depth before moving on to nodes at the next depth level. BFS is typically implemented using a queue data structure.

Here's a simple implementation of BFS in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

// Graph class representing an undirected graph using adjacency list representation
class Graph {
    int V; // Number of vertices

    // Pointer to an array containing adjacency lists
    vector<vector<int>> adj;

public:
    Graph(int V) : V(V) {
        adj.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w); // Add w to v’s list
        adj[w].push_back(v); // Add v to w’s list
    }

    // Function to perform BFS traversal starting from a given source vertex
    void BFS(int s) {
        // Mark all vertices as not visited
        vector<bool> visited(V, false);

        // Create a queue for BFS
        queue<int> q;

        // Mark the current node as visited and enqueue it
        visited[s] = true;
        q.push(s);

        while (!q.empty()) {
            // Dequeue a vertex from the queue and print it
            int current = q.front();
            cout << current << " ";
            q.pop();

            // Get all adjacent vertices of the dequeued vertex current
            // If an adjacent vertex has not been visited, mark it visited and enqueue it
            for (int i = 0; i < adj[current].size(); ++i) {
                int adjVertex = adj[current][i];
                if (!visited[adjVertex]) {
                    visited[adjVertex] = true;
                    q.push(adjVertex);
                }
            }
        }
    }
};

int main() {
    // Create a graph given in the example
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "Breadth First Traversal (starting from vertex 2): ";
    g.BFS(2); // Starting BFS from vertex 2
    cout << endl;

    return 0;
}
```

In this code:

- The `Graph` class represents an undirected graph using an adjacency list representation.
- The `addEdge` function is used to add an edge between two vertices.
- The `BFS` function performs a breadth-first traversal starting from a given source vertex `s`.
- Inside the `BFS` function, a `visited` array is used to keep track of visited vertices to avoid processing them more than once.
- A queue `q` is used to keep track of the nodes to be visited next. The BFS algorithm repeatedly dequeues a vertex from the queue, visits all its adjacent vertices, marks them as visited, and enqueues them if they have not been visited before.
- In the `main` function, a sample graph is created and BFS is performed starting from vertex 2.

### 1. Algorithms & Data Structures (C++): Graph Traversal - Breadth First Search and Depth First Search

Breadth First Search (BFS) and Depth First Search (DFS) are fundamental graph traversal algorithms used to visit and explore all the nodes in a graph. Here's a brief explanation of both in the context of C++:

#### Breadth First Search (BFS)

BFS explores a graph level by level, starting from a chosen node (usually the source node). It explores all the neighbors of the current node before moving on to the next level of neighbors.

##### C++ Implementation

```cpp
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

void BFS(vector<vector<int>>& graph, int start) {
    int n = graph.size();
    vector<bool> visited(n, false);
    queue<int> q;

    visited[start] = true;
    q.push(start);

    while (!q.empty()) {
        int curr = q.front();
        q.pop();
        cout << curr << " ";

        for (int neighbor : graph[curr]) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                q.push(neighbor);
            }
        }
    }
}

int main() {
    // Example usage
    vector<vector<int>> graph = {
        {1, 2},     // Neighbors of node 0
        {0, 3, 4},  // Neighbors of node 1
        {0, 5},     // Neighbors of node 2
        {1},        // Neighbors of node 3
        {1},        // Neighbors of node 4
        {2}         // Neighbors of node 5
    };

    cout << "BFS traversal starting from node 0: ";
    BFS(graph, 0);

    return 0;
}
```

#### Depth First Search (DFS)

DFS explores a graph by going as deep as possible along each branch before backtracking. It explores as far as possible along each branch before backtracking.

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

void DFSUtil(vector<vector<int>>& graph, int node, vector<bool>& visited) {
    visited[node] = true;
    cout << node << " ";

    for (int neighbor : graph[node]) {
        if (!visited[neighbor]) {
            DFSUtil(graph, neighbor, visited);
        }
    }
}

void DFS(vector<vector<int>>& graph, int start) {
    int n = graph.size();
    vector<bool> visited(n, false);

    DFSUtil(graph, start, visited);
}

int main() {
    // Example usage
    vector<vector<int>> graph = {
        {1, 2},     // Neighbors of node 0
        {0, 3, 4},  // Neighbors of node 1
        {0, 5},     // Neighbors of node 2
        {1},        // Neighbors of node 3
        {1},        // Neighbors of node 4
        {2}         // Neighbors of node 5
    };

    cout << "DFS traversal starting from node 0: ";
    DFS(graph, 0);

    return 0;
}
```

Both algorithms visit each node exactly once in the case of a connected graph. They differ in the order in which they visit nodes and how they store the nodes yet to be visited. BFS uses a queue, while DFS typically uses a stack (or recursion, which implicitly uses a stack).

### 1. Algorithms & Data Structures (C++): Graph Traversal - Depth First And Breadth First

Certainly! In C++, both depth-first search (DFS) and breadth-first search (BFS) are fundamental graph traversal algorithms used to visit all the vertices of a graph. Let's discuss each of them and provide implementations.

#### Depth-First Search (DFS)

DFS explores as far as possible along each branch before backtracking. It can be implemented using recursion or a stack.

Here's a recursive implementation of DFS:

```cpp
#include <iostream>
#include <vector>
#include <stack>
using namespace std;

class Graph {
    int V;
    vector<vector<int>> adj;

    void DFSUtil(int v, vector<bool>& visited) {
        visited[v] = true;
        cout << v << " ";

        for (int u : adj[v]) {
            if (!visited[u])
                DFSUtil(u, visited);
        }
    }

public:
    Graph(int V) {
        this->V = V;
        adj.resize(V);
    }

    void addEdge(int v, int w) {
        adj[v].push_back(w);
    }

    void DFS(int v) {
        vector<bool> visited(V, false);
        DFSUtil(v, visited);
    }
};

int main() {
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "DFS traversal starting from vertex 2: ";
    g.DFS(2);

    return 0;
}
```

#### Breadth-First Search (BFS)

BFS explores all the vertices at the present depth before moving to the vertices at the next depth level. It uses a queue data structure.

Here's an implementation of BFS:

```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

class Graph {
    int V;
    vector<vector<int>> adj;

public:
    Graph(int V) {
        this->V = V;
        adj.resize(V);
    }

    void addEdge(int v, int w) {
        adj[v].push_back(w);
    }

    void BFS(int v) {
        vector<bool> visited(V, false);
        queue<int> q;

        visited[v] = true;
        q.push(v);

        while (!q.empty()) {
            v = q.front();
            cout << v << " ";
            q.pop();

            for (int u : adj[v]) {
                if (!visited[u]) {
                    visited[u] = true;
                    q.push(u);
                }
            }
        }
    }
};

int main() {
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "BFS traversal starting from vertex 2: ";
    g.BFS(2);

    return 0;
}
```

Both DFS and BFS have their unique advantages and use cases. DFS is often preferred for topological sorting, detecting cycles in graphs, and solving puzzles. BFS, on the other hand, is commonly used in finding the shortest path and minimum spanning tree for unweighted graphs.

### 1. Algorithms & Data Structures (C++): Graph Traversal - Depth First Search (Depth First Search)

Depth First Search (DFS) is a fundamental graph traversal algorithm that explores as far as possible along each branch before backtracking. It's commonly used to traverse or search through a graph or tree structure. Here's how you can implement DFS in C++:

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

// Graph class representing the graph
class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V) {
        adj.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w); // Add w to v's list
    }

    // Depth First Search
    void DFS(int v) {
        // Mark all the vertices as not visited
        vector<bool> visited(V, false);

        // Create a stack for DFS
        stack<int> stack;

        // Push the current source node
        stack.push(v);

        while (!stack.empty()) {
            // Pop a vertex from stack and print it
            v = stack.top();
            stack.pop();

            // Stack may contain same vertex twice. So, we need to print the popped item only if it's not visited.
            if (!visited[v]) {
                cout << v << " ";
                visited[v] = true; // Mark the current node as visited

                // Get all adjacent vertices of the popped vertex v. If an adjacent has not been visited, then push it to the stack.
                for (auto i = adj[v].begin(); i != adj[v].end(); ++i)
                    if (!visited[*i])
                        stack.push(*i);
            }
        }
    }
};

int main() {
    // Create a graph given in the example
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "Depth First Traversal (starting from vertex 2): ";
    g.DFS(2);
    cout << endl;

    return 0;
}
```

In this code:

- We represent the graph using an adjacency list.
- The `DFS` function takes a starting vertex as an argument and explores the graph from that vertex.
- We use a stack to keep track of the vertices to be visited next.
- We mark visited vertices to avoid processing them multiple times.
- The `main` function demonstrates how to create a graph and call the DFS function.

You can modify this code according to your specific requirements, such as inputting a graph from the user or adapting it for a different problem context.

### 1. Algorithms & Data Structures (C++): Graph Traversals

Graph traversals are fundamental operations in graph theory and are crucial for exploring and analyzing graphs. In C++, you can implement various graph traversal algorithms using different data structures like adjacency lists or matrices. Two common graph traversal algorithms are Depth-First Search (DFS) and Breadth-First Search (BFS). Here's how you can implement them:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <stack>

using namespace std;

// Graph class representing an undirected graph using adjacency lists
class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V), adj(V) {}

    // Function to add an edge to the graph
    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u); // Assuming undirected graph
    }

    // Depth-First Search traversal starting from vertex v
    void DFS(int v) {
        vector<bool> visited(V, false);
        stack<int> stack;
        stack.push(v);

        while (!stack.empty()) {
            v = stack.top();
            stack.pop();

            if (!visited[v]) {
                cout << v << " ";
                visited[v] = true;

                for (int u : adj[v]) {
                    if (!visited[u])
                        stack.push(u);
                }
            }
        }
    }

    // Breadth-First Search traversal starting from vertex v
    void BFS(int v) {
        vector<bool> visited(V, false);
        queue<int> queue;
        visited[v] = true;
        queue.push(v);

        while (!queue.empty()) {
            v = queue.front();
            cout << v << " ";
            queue.pop();

            for (int u : adj[v]) {
                if (!visited[u]) {
                    visited[u] = true;
                    queue.push(u);
                }
            }
        }
    }
};

int main() {
    // Create a graph
    Graph g(5);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(2, 4);

    cout << "Depth-First Search starting from vertex 0: ";
    g.DFS(0);
    cout << endl;

    cout << "Breadth-First Search starting from vertex 0: ";
    g.BFS(0);
    cout << endl;

    return 0;
}
```

In this code:

- The `Graph` class represents an undirected graph using an adjacency list.
- The `addEdge` method is used to add edges to the graph.
- The `DFS` method performs a Depth-First Search traversal starting from a given vertex.
- The `BFS` method performs a Breadth-First Search traversal starting from a given vertex.

You can modify this code according to your needs or extend it to implement other graph traversal algorithms.

### 1. Algorithms & Data Structures (C++): Graph Using An Adjacency List And Adjacency Set

Sure! Here's an implementation of a graph using both an adjacency list and an adjacency set in C++:

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector

<pair<int, unordered_set<int>>> adj_list; // Adjacency list representation
    vector



<pair<int, unordered_set<int>>> adj_set; // Adjacency set representation

public:
    Graph(int vertices) : V(vertices) {
        adj_list.resize(V);
        adj_set.resize(V);
    }

    void addEdge(int u, int v) {
        // Adding edge to adjacency list
        adj_list[u].second.insert(v);
        adj_list[v].second.insert(u);
        
        // Adding edge to adjacency set
        adj_set[u].second.insert(v);
        adj_set[v].second.insert(u);
    }

    void printAdjList() {
        cout << "Adjacency List:\n";
        for (int i = 0; i < V; ++i) {
            cout << i << " -> ";
            for (const auto& pair : adj_list[i].second) {
                cout << pair << " ";
            }
            cout << "\n";
        }
    }

    void printAdjSet() {
        cout << "Adjacency Set:\n";
        for (int i = 0; i < V; ++i) {
            cout << i << " -> ";
            for (const auto& vertex : adj_set[i].second) {
                cout << vertex << " ";
            }
            cout << "\n";
        }
    }
};

int main() {
    Graph graph(5);
    graph.addEdge(0, 1);
    graph.addEdge(0, 4);
    graph.addEdge(1, 2);
    graph.addEdge(1, 3);
    graph.addEdge(1, 4);
    graph.addEdge(2, 3);
    graph.addEdge(3, 4);

    graph.printAdjList();
    cout << "\n";
    graph.printAdjSet();

    return 0;
}
```

In this implementation, the `Graph` class contains private data members for the number of vertices (`V`) and two vectors for the adjacency list (`adj_list`) and the adjacency set (`adj_set`). The `addEdge` function is used to add edges between vertices, and both the adjacency list and adjacency set are updated accordingly. Finally, the `printAdjList` and `printAdjSet` functions are used to print out the adjacency list and adjacency set, respectively.

### 1. Algorithms & Data Structures (C++): Graph Using An Adjacency Matrix

Creating a graph using an adjacency matrix in C++ involves representing connections between vertices in a 2D array. Each cell of the matrix will indicate whether there's an edge between two vertices. Here's a simple implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
private:
    int numVertices;
    vector<vector<int>> adjMatrix;

public:
    // Constructor
    Graph(int numVertices) {
        this->numVertices = numVertices;
        adjMatrix.resize(numVertices, vector<int>(numVertices, 0));
    }

    // Add edge between two vertices
    void addEdge(int src, int dest) {
        // Assuming undirected graph, so setting both src->dest and dest->src
        adjMatrix[src][dest] = 1;
        adjMatrix[dest][src] = 1;
    }

    // Display the adjacency matrix
    void display() {
        for (int i = 0; i < numVertices; ++i) {
            for (int j = 0; j < numVertices; ++j) {
                cout << adjMatrix[i][j] << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph graph(5);

    // Add some edges
    graph.addEdge(0, 1);
    graph.addEdge(0, 4);
    graph.addEdge(1, 2);
    graph.addEdge(1, 3);
    graph.addEdge(1, 4);
    graph.addEdge(2, 3);
    graph.addEdge(3, 4);

    // Display the adjacency matrix
    cout << "Adjacency Matrix:" << endl;
    graph.display();

    return 0;
}
```

This code creates a `Graph` class that represents an undirected graph using an adjacency matrix. You can add edges between vertices using the `addEdge` method, and then display the adjacency matrix using the `display` method. In the `main` function, a sample graph is created with 5 vertices and some edges are added to it. Finally, the adjacency matrix is displayed.

### 1. Algorithms & Data Structures (C++): Graph: Add Edge

Adding an edge to a graph data structure involves connecting two vertices and potentially assigning a weight to the edge if the graph is weighted. Below is an example of how you can implement adding an edge to a graph in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Representation of a graph using adjacency list
class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adjList; // Adjacency list

public:
    Graph(int vertices) : V(vertices) {
        adjList.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int u, int v) {
        // For an undirected graph, we add edges from both vertices
        adjList[u].push_back(v);
        adjList[v].push_back(u);
    }

    // Function to print the adjacency list representation of the graph
    void printGraph() {
        for (int i = 0; i < V; ++i) {
            cout << "Adjacency list of vertex " << i << ": ";
            for (int j = 0; j < adjList[i].size(); ++j) {
                cout << adjList[i][j] << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph g(5);

    // Add edges to the graph
    g.addEdge(0, 1);
    g.addEdge(0, 4);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 3);
    g.addEdge(3, 4);

    // Print the adjacency list representation of the graph
    g.printGraph();

    return 0;
}
```

In this example, we represent the graph using an adjacency list. The `addEdge` function adds an edge between two vertices `u` and `v` by adding `v` to the adjacency list of `u`, and vice versa since this is an undirected graph. The `printGraph` function is used to print the adjacency list representation of the graph for visualization.

### 1. Algorithms & Data Structures (C++): Graph: Add Vertex

To add a vertex to a graph in C++, you typically need to maintain a data structure to represent the graph. One common approach is to use an adjacency list or an adjacency matrix to represent the connections between vertices. Here's an example of how you can add a vertex to a graph using an adjacency list:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
private:
    vector<vector<int>> adjacencyList;

public:
    Graph(int vertices) {
        adjacencyList.resize(vertices);
    }

    // Function to add an edge between two vertices
    void addEdge(int src, int dest) {
        adjacencyList[src].push_back(dest);
        // For undirected graph, uncomment the line below
        // adjacencyList[dest].push_back(src);
    }

    // Function to add a vertex to the graph
    void addVertex() {
        // Add an empty vector to represent the new vertex
        adjacencyList.push_back({});
    }

    // Function to display the adjacency list representation of the graph
    void display() {
        for (int i = 0; i < adjacencyList.size(); ++i) {
            cout << "Vertex " << i << " connects to:";
            for (int j = 0; j < adjacencyList[i].size(); ++j) {
                cout << " " << adjacencyList[i][j];
            }
            cout << endl;
        }
    }
};

int main() {
    Graph graph(4); // Create a graph with 4 vertices

    // Add some edges
    graph.addEdge(0, 1);
    graph.addEdge(0, 2);
    graph.addEdge(1, 2);
    graph.addEdge(2, 3);

    // Display the original graph
    cout << "Original Graph:" << endl;
    graph.display();

    // Add a vertex
    graph.addVertex();

    // Display the updated graph
    cout << "\nGraph after adding a vertex:" << endl;
    graph.display();

    return 0;
}
```

In this example, the `Graph` class maintains an adjacency list (`vector<vector<int>> adjacencyList`) where each element of the outer vector represents a vertex, and the inner vector contains the indices of vertices that the corresponding vertex is connected to. The `addVertex()` function simply adds an empty vector to the `adjacencyList`, representing a new vertex without any connections.

### 1. Algorithms & Data Structures (C++): Graph: Adjacency List

In C++, implementing a graph using an adjacency list is a common approach. This representation stores a graph as an array of lists, where each list represents the neighbors of a particular vertex. Here's a basic implementation:

```cpp
#include <iostream>
#include <list>
#include <vector>

using namespace std;

class Graph {
    int V; // Number of vertices
    vector<list<int>> adjList; // Array of lists to store adjacency lists

public:
    Graph(int vertices) : V(vertices) {
        adjList.resize(V); // Resize the array of lists
    }

    // Function to add an edge to the graph
    void addEdge(int u, int v) {
        // Add v to u's list
        adjList[u].push_back(v);
        // For an undirected graph, add u to v's list as well
        adjList[v].push_back(u);
    }

    // Function to print the adjacency list representation of the graph
    void printGraph() {
        for (int i = 0; i < V; ++i) {
            cout << "Vertex " << i << ":";
            for (int neighbor : adjList[i]) {
                cout << " -> " << neighbor;
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph graph(5);

    // Add edges
    graph.addEdge(0, 1);
    graph.addEdge(0, 4);
    graph.addEdge(1, 2);
    graph.addEdge(1, 3);
    graph.addEdge(1, 4);
    graph.addEdge(2, 3);
    graph.addEdge(3, 4);

    // Print the adjacency list representation of the graph
    graph.printGraph();

    return 0;
}
```

In this code:

- The `Graph` class represents an undirected graph using an adjacency list.
- The constructor takes the number of vertices as an argument and initializes the adjacency list.
- The `addEdge` function adds an edge between two vertices by adding the corresponding vertices to each other's adjacency lists.
- The `printGraph` function prints the adjacency list representation of the graph.

This implementation allows for efficient insertion and deletion of edges, and it's also memory-efficient for sparse graphs.

### 1. Algorithms & Data Structures (C++): Graph: Adjacency List Representation

In C++, representing a graph using an adjacency list is a common and efficient method. Here's a basic implementation of a graph using adjacency lists:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Class to represent a graph
class Graph {
    int V; // Number of vertices

    // Array of vectors to represent adjacency lists
    vector<int> *adj;

public:
    // Constructor
    Graph(int V) {
        this->V = V;
        adj = new vector<int>[V];
    }

    // Function to add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w); // Add w to v’s list
        adj[w].push_back(v); // If the graph is undirected, add this line too
    }

    // Function to print the adjacency list representation of the graph
    void printGraph() {
        for (int v = 0; v < V; ++v) {
            cout << "Adjacency list of vertex " << v << "\nhead ";
            for (auto x : adj[v])
                cout << "-> " << x;
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph g(5);
    // Add some edges
    g.addEdge(0, 1);
    g.addEdge(0, 4);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 3);
    g.addEdge(3, 4);
    // Print the adjacency list representation of the graph
    g.printGraph();
    return 0;
}
```

In this implementation:

- The `Graph` class represents the graph.
- `V` is the number of vertices in the graph.
- `adj` is a pointer to an array of vectors. Each vector represents the adjacency list for a vertex.
- The `addEdge` function adds an edge between two vertices.
- The `printGraph` function prints the adjacency list representation of the graph.

This implementation is for an undirected graph. If you want to represent a directed graph, you only need to add edges in one direction (from source to destination) in the `addEdge` function.

### 1. Algorithms & Data Structures (C++): Graph: Adjacency List Representation with Node Class

Sure, I can provide you with an example of representing a graph using adjacency list representation in C++. Here's a basic implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Class to represent a node in the graph
class Node {
public:
    int value;
    Node(int v) : value(v) {}
};

// Class to represent a graph using adjacency list
class Graph {
public:
    vector<Node*> nodes; // vector of pointers to nodes
    vector<vector<int>> adjacencyList; // adjacency list

    // Constructor
    Graph(int n) {
        nodes.resize(n);
        adjacencyList.resize(n);
        for (int i = 0; i < n; ++i) {
            nodes[i] = new Node(i); // creating nodes with values 0 to n-1
        }
    }

    // Function to add an edge between two nodes
    void addEdge(int u, int v) {
        adjacencyList[u].push_back(v); // adding v to u's adjacency list
        adjacencyList[v].push_back(u); // adding u to v's adjacency list (for undirected graph)
    }

    // Function to print the adjacency list representation of the graph
    void printGraph() {
        for (int i = 0; i < nodes.size(); ++i) {
            cout << "Adjacency list of node " << nodes[i]->value << ": ";
            for (int j = 0; j < adjacencyList[i].size(); ++j) {
                cout << adjacencyList[i][j] << " ";
            }
            cout << endl;
        }
    }

    // Destructor to free memory
    ~Graph() {
        for (int i = 0; i < nodes.size(); ++i) {
            delete nodes[i];
        }
    }
};

int main() {
    // Creating a graph with 5 nodes
    Graph graph(5);

    // Adding edges to the graph
    graph.addEdge(0, 1);
    graph.addEdge(0, 2);
    graph.addEdge(1, 3);
    graph.addEdge(2, 4);
    graph.addEdge(3, 4);

    // Printing the adjacency list representation of the graph
    graph.printGraph();

    return 0;
}
```

In this example, we have a `Node` class to represent each node in the graph. The `Graph` class maintains a vector of pointers to nodes and an adjacency list to represent the graph. The `addEdge` function is used to add an edge between two nodes, and the `printGraph` function prints the adjacency list representation of the graph. Finally, the destructor is implemented to free the memory allocated for nodes when the graph object is destroyed.

### 1. Algorithms & Data Structures (C++): Graph: Adjacency Matrix

Sure, I can provide an example implementation of a graph using an adjacency matrix in C++. An adjacency matrix is a 2D array of size V x V where V is the number of vertices in the graph. The value of matrix[i][j] is 1 if there is an edge from vertex i to vertex j, otherwise 0.

Here's a simple implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adjMatrix; // Adjacency matrix

public:
    // Constructor
    Graph(int vertices) {
        V = vertices;
        adjMatrix.resize(V, vector<int>(V, 0)); // Initialize all elements to 0
    }

    // Function to add an edge to the graph
    void addEdge(int src, int dest) {
        // Since it's an undirected graph, we need to add edges in both directions
        adjMatrix[src][dest] = 1;
        adjMatrix[dest][src] = 1;
    }

    // Function to print the adjacency matrix
    void printMatrix() {
        for (int i = 0; i < V; ++i) {
            for (int j = 0; j < V; ++j) {
                cout << adjMatrix[i][j] << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 4 vertices
    Graph graph(4);

    // Add edges
    graph.addEdge(0, 1);
    graph.addEdge(0, 2);
    graph.addEdge(1, 2);
    graph.addEdge(2, 3);

    // Print the adjacency matrix
    cout << "Adjacency Matrix:" << endl;
    graph.printMatrix();

    return 0;
}
```

In this implementation, we create a `Graph` class with methods to add edges and print the adjacency matrix. In the `main()` function, we create a graph with 4 vertices and add some edges to it. Finally, we print the adjacency matrix.

### 1. Algorithms & Data Structures (C++): Graph: All Paths From Source to Target

To find all paths from a source to a target in a graph, you can use depth-first search (DFS). Here's a C++ implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void dfs(vector<vector<int>>& graph, int node, int target, vector<int>& path, vector<vector<int>>& allPaths) {
    path.push_back(node);

    if (node == target) {
        allPaths.push_back(path);
    } else {
        for (int neighbor : graph[node]) {
            dfs(graph, neighbor, target, path, allPaths);
        }
    }

    path.pop_back();
}

vector<vector<int>> allPathsSourceTarget(vector<vector<int>>& graph) {
    vector<vector<int>> allPaths;
    vector<int> path;

    int source = 0;
    int target = graph.size() - 1;

    dfs(graph, source, target, path, allPaths);

    return allPaths;
}

int main() {
    vector<vector<int>> graph = {{1, 2}, {3}, {3}, {}};
    vector<vector<int>> allPaths = allPathsSourceTarget(graph);

    cout << "All paths from source to target:" << endl;
    for (const auto& path : allPaths) {
        for (int node : path) {
            cout << node << " ";
        }
        cout << endl;
    }

    return 0;
}
```

In this code:

- `dfs` function performs a depth-first search starting from the source node and explores all possible paths until the target node is reached. It stores all paths found in the `allPaths` vector.
- `allPathsSourceTarget` function initializes the path vector and calls the `dfs` function with the source and target nodes.
- In the `main` function, we create a sample graph and print all the paths found from the source to the target.

You can customize the graph as per your requirement.

### 1. Algorithms & Data Structures (C++): Graph: Big O

The Big O notation for algorithms and data structures can vary depending on the specific operations being performed and the underlying implementation. For graphs in C++, here are some common operations and their typical Big O complexities:

1. **Space Complexity:**
   - The space complexity of a graph is typically O(V + E), where V is the number of vertices and E is the number of edges. This accounts for the space required to store the vertices and edges, often in adjacency lists or matrices.

2. **Time Complexity:**
   - **Adding/Removing a Vertex:** O(1) to O(V) - Adding or removing a vertex can require updating adjacency lists or matrices. In the worst case, removing a vertex might require updating all edges.
   - **Adding/Removing an Edge:** O(1) to O(V) - Adding or removing an edge might involve updating adjacency lists or matrices. In the worst case, adding or removing an edge might require updating all edges connected to the vertex.
   - **Finding if an Edge Exists:** O(degree) - In adjacency lists, it's typically O(degree), where degree is the number of edges incident to a vertex. In adjacency matrices, it's O(1).
   - **Traversing all Vertices/Edges:** O(V + E) - Traversing all vertices or edges typically involves visiting each vertex once and each edge once, which gives O(V + E) time complexity.
   - **Depth-First Search (DFS) and Breadth-First Search (BFS):** O(V + E) - Both DFS and BFS visit each vertex and edge once, giving O(V + E) time complexity.
   - **Shortest Path Algorithms (e.g., Dijkstra's, Bellman-Ford):** O((V + E) log V) - For Dijkstra's algorithm with a binary heap, and O(VE) for Bellman-Ford. These algorithms typically involve visiting each vertex and edge, with additional operations for updating priority queues or distance arrays.
   - **Minimum Spanning Tree Algorithms (e.g., Prim's, Kruskal's):** O(E log V) - For Prim's algorithm with a binary heap, and O(E log E) for Kruskal's algorithm with sorting. These algorithms involve sorting edges and/or maintaining priority queues.

These complexities are based on typical implementations and assumptions. Actual performance can vary based on factors like the specific graph structure, the chosen algorithm, and the efficiency of underlying data structures.

### 1. Algorithms & Data Structures (C++): Graph: Breadth First Search

Breadth First Search (BFS) is a fundamental algorithm for traversing or searching tree or graph data structures. It starts at a designated node (often called the "root" in a tree) and explores all the neighbor nodes at the present depth before moving on to the nodes at the next depth level.

In the context of graphs, BFS can be used to find the shortest path from a source node to any other reachable node, provided all edges have the same weight (unweighted graph). It can also be used to answer questions about connectivity and reachability within the graph.

Here's a basic implementation of BFS in C++ for an adjacency list representation of a graph:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <unordered_set>

using namespace std;

// Graph representation using adjacency list
class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj;

public:
    Graph(int V) : V(V) {
        adj.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w);
    }

    // Function to perform BFS traversal from a given source vertex
    void BFS(int s) {
        vector<bool> visited(V, false); // Mark all vertices as not visited
        queue<int> q; // Create a queue for BFS

        visited[s] = true; // Mark the current node as visited and enqueue it
        q.push(s);

        while (!q.empty()) {
            // Dequeue a vertex from the queue and print it
            s = q.front();
            cout << s << " ";
            q.pop();

            // Get all adjacent vertices of the dequeued vertex s. If an adjacent has not been visited, then mark it visited and enqueue it
            for (auto i = adj[s].begin(); i != adj[s].end(); ++i) {
                if (!visited[*i]) {
                    visited[*i] = true;
                    q.push(*i);
                }
            }
        }
    }
};

int main() {
    Graph g(4); // Create a graph with 4 vertices

    // Add edges
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "Breadth First Traversal starting from vertex 2: ";
    g.BFS(2);

    return 0;
}
```

In this implementation:

- The `Graph` class represents the graph using an adjacency list.
- The `addEdge` function adds an edge between two vertices.
- The `BFS` function performs breadth-first traversal starting from a given source vertex `s`. It uses a queue to keep track of the vertices to be visited next.
- The `visited` vector keeps track of visited vertices to avoid revisiting them.

This code demonstrates BFS on a simple graph with four vertices. You can modify the `main` function to create and traverse other graphs as needed.

### 1. Algorithms & Data Structures (C++): Graph: Cycles

In C++, detecting cycles in a graph is a fundamental task in graph theory. There are several algorithms to achieve this, such as Depth-First Search (DFS) or Breadth-First Search (BFS). Here's a basic implementation of cycle detection in an undirected graph using DFS:

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>

using namespace std;

class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list representation

    bool isCyclicUtil(int v, vector<bool>& visited, int parent) {
        visited[v] = true; // Mark the current node as visited

        // Recur for all the vertices adjacent to this vertex
        for (int i : adj[v]) {
            // If an adjacent is not visited, then recur for that adjacent
            if (!visited[i]) {
                if (isCyclicUtil(i, visited, v))
                    return true;
            }
            // If an adjacent is visited and not the parent of the current vertex, then there is a cycle
            else if (i != parent)
                return true;
        }
        return false;
    }

public:
    Graph(int V) {
        this->V = V;
        adj.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w);
        adj[w].push_back(v); // Graph is undirected
    }

    // Function to detect cycle in the graph
    bool isCyclic() {
        // Mark all the vertices as not visited and not part of recursion stack
        vector<bool> visited(V, false);

        // Call the recursive helper function to detect cycle in different DFS trees
        for (int i = 0; i < V; i++)
            if (!visited[i] && isCyclicUtil(i, visited, -1))
                return true;

        return false;
    }
};

int main() {
    Graph g(5); // Number of vertices

    // Adding edges
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    if (g.isCyclic())
        cout << "Graph contains cycle";
    else
        cout << "Graph doesn't contain cycle";

    return 0;
}
```

This implementation uses DFS to traverse the graph and detects a cycle by maintaining a recursive call stack. It also keeps track of visited vertices and the parent of the current vertex to determine if there is a back edge pointing to an already visited vertex (except its parent). If such an edge is found, a cycle is detected.

### 1. Algorithms & Data Structures (C++): Exercise: Guess The Graph

Sure, let's dive into the exercise!

#### Problem Statement: Guess The Graph

You are given a set of edges representing a graph. The task is to determine the type of the graph based on the given edges. The types of graphs you need to identify are:

1. **Undirected Graph**: A graph where edges have no orientation. If there's an edge between nodes A and B, it implies there's also an edge between B and A.
2. **Directed Graph**: A graph where edges have direction. If there's an edge from node A to node B, it doesn't necessarily mean there's an edge from B to A.
3. **Weighted Graph**: A graph where edges have weights assigned to them.
4. **Cyclic Graph**: A graph containing at least one cycle.
5. **Acyclic Graph**: A graph containing no cycles.

Your task is to write a C++ program that reads in the edges of a graph and determines its type. You can assume that the input will be well-formed, with each edge represented as a pair of integers (source, destination), and in the case of weighted graphs, an additional weight associated with each edge.

Your program should output the type(s) of the graph based on the input provided.

Let's start by outlining how you might approach this problem. Do you have any initial thoughts or ideas on how to tackle it?

### 1. Algorithms & Data Structures (C++): Find The Shortest Path In A Weighted Graphs - Fewer Edges Better

To find the shortest path in a weighted graph with fewer edges being preferable, you can use algorithms like Dijkstra's algorithm or A* search algorithm. However, since you prefer fewer edges, Dijkstra's algorithm will suit your needs better.

Here's a simplified implementation of Dijkstra's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>

using namespace std;

// Data structure to represent a weighted edge
struct Edge {
    int dest;
    int weight;
};

// Data structure to represent a graph
class Graph {
    int V; // Number of vertices

    // Adjacency list representation of the graph
    vector<vector<Edge>> adj;

public:
    Graph(int V) : V(V) {
        adj.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int src, int dest, int weight) {
        adj[src].push_back({dest, weight});
        // For fewer edges, don't add the edge to the destination vertex.
        // adj[dest].push_back({src, weight});
    }

    // Function to find the shortest path from a given source vertex
    void shortestPath(int src) {
        // Create a priority queue to store vertices and their distances
        priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;

        // Vector to store distances from source
        vector<int> dist(V, numeric_limits<int>::max());

        // Insert source vertex into the priority queue
        pq.push({0, src});
        dist[src] = 0;

        while (!pq.empty()) {
            // Extract the vertex with minimum distance value
            int u = pq.top().second;
            pq.pop();

            // Update distance value of adjacent vertices
            for (const auto& edge : adj[u]) {
                int v = edge.dest;
                int weight = edge.weight;

                // If the new distance is shorter than the current distance, update it
                if (dist[v] > dist[u] + weight) {
                    dist[v] = dist[u] + weight;
                    pq.push({dist[v], v});
                }
            }
        }

        // Print shortest distances
        cout << "Shortest distances from vertex " << src << ":\n";
        for (int i = 0; i < V; ++i) {
            cout << "Vertex " << i << ": " << dist[i] << '\n';
        }
    }
};

int main() {
    // Create a graph
    Graph g(5);
    g.addEdge(0, 1, 10);
    g.addEdge(0, 2, 5);
    g.addEdge(1, 2, 3);
    g.addEdge(1, 3, 1);
    g.addEdge(2, 1, 2);
    g.addEdge(2, 3, 9);
    g.addEdge(2, 4, 2);
    g.addEdge(3, 4, 4);

    // Find shortest paths from vertex 0
    g.shortestPath(0);

    return 0;
}
```

This code demonstrates Dijkstra's algorithm for finding the shortest path from a given source vertex in a weighted graph. By not adding edges in reverse (e.g., from destination back to source), we ensure that the paths with fewer edges are preferred.

### 1. Algorithms & Data Structures (C++): Find the Town Judge

To find the town judge in a town where there may be a judge or not, you can use a graph-based approach. In this problem, each person in the town is represented by a node, and if person A trusts person B, there's a directed edge from A to B. The town judge is someone who is trusted by everyone else but trusts no one themselves. This means the town judge has an in-degree of N - 1 (where N is the number of people) and an out-degree of 0.

Here's a C++ implementation of the algorithm using adjacency lists:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int findJudge(int N, vector<vector<int>>& trust) {
    // Initialize vectors to store in-degree and out-degree of each person
    vector<int> inDegree(N + 1, 0); // 1-indexed
    vector<int> outDegree(N + 1, 0); // 1-indexed
    
    // Calculate in-degree and out-degree for each person
    for (const auto& t : trust) {
        outDegree[t[0]]++;
        inDegree[t[1]]++;
    }
    
    // Find the potential town judge
    for (int i = 1; i <= N; ++i) {
        if (inDegree[i] == N - 1 && outDegree[i] == 0) {
            return i; // Found the town judge
        }
    }
    
    return -1; // No town judge found
}

int main() {
    // Example usage
    int N = 4;
    vector<vector<int>> trust = {{1, 3}, {1, 4}, {2, 3}, {2, 4}, {4, 3}};
    cout << "The town judge is at position: " << findJudge(N, trust) << endl;
    
    return 0;
}
```

This code first calculates the in-degree and out-degree for each person based on the given trust relationships. Then, it iterates through each person to find the one with an in-degree of N - 1 and an out-degree of 0, which represents the town judge. If such a person is found, their position (index) is returned; otherwise, -1 is returned to indicate that there is no town judge.

### 1. Algorithms & Data Structures (C++): Finding Path in a Graph

To find a path in a graph, you can use various algorithms, such as Depth-First Search (DFS) or Breadth-First Search (BFS). Here's a basic implementation of both algorithms in C++ to find a path between two nodes in an unweighted graph represented using an adjacency list:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <stack>

using namespace std;

// Graph class
class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V), adj(V) {}

    // Add an edge between two vertices
    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u); // If graph is undirected
    }

    // DFS traversal
    bool DFS(int source, int destination) {
        vector<bool> visited(V, false);
        stack<int> st;
        st.push(source);

        while (!st.empty()) {
            int u = st.top();
            st.pop();

            if (u == destination)
                return true;

            if (!visited[u]) {
                visited[u] = true;
                for (int v : adj[u]) {
                    if (!visited[v])
                        st.push(v);
                }
            }
        }

        return false;
    }

    // BFS traversal
    bool BFS(int source, int destination) {
        vector<bool> visited(V, false);
        queue<int> q;
        q.push(source);

        while (!q.empty()) {
            int u = q.front();
            q.pop();

            if (u == destination)
                return true;

            if (!visited[u]) {
                visited[u] = true;
                for (int v : adj[u]) {
                    if (!visited[v])
                        q.push(v);
                }
            }
        }

        return false;
    }
};

int main() {
    Graph g(6); // Create a graph with 6 vertices

    // Add edges
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(2, 4);
    g.addEdge(3, 5);
    g.addEdge(4, 5);

    int source = 0;
    int destination = 5;

    // Check if there is a path using DFS
    if (g.DFS(source, destination))
        cout << "Path exists between " << source << " and " << destination << " using DFS\n";
    else
        cout << "No path exists between " << source << " and " << destination << " using DFS\n";

    // Check if there is a path using BFS
    if (g.BFS(source, destination))
        cout << "Path exists between " << source << " and " << destination << " using BFS\n";
    else
        cout << "No path exists between " << source << " and " << destination << " using BFS\n";

    return 0;
}
```

This code defines a `Graph` class with methods for adding edges and performing DFS and BFS traversal. You can modify the `main()` function to test with different graphs and source-destination pairs.

### 1. Algorithms & Data Structures (C++): Finding Shortest path in an unweighted graph

In an unweighted graph, finding the shortest path between two vertices typically involves using breadth-first search (BFS) algorithm. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

// Function to perform BFS and find the shortest path
vector<int> shortestPathBFS(const vector<vector<int>>& graph, int start, int end) {
    int n = graph.size();
    vector<bool> visited(n, false);
    vector<int> parent(n, -1);
    vector<int> distance(n, -1);

    queue<int> q;
    q.push(start);
    visited[start] = true;
    distance[start] = 0;

    while (!q.empty()) {
        int current = q.front();
        q.pop();

        if (current == end) {
            vector<int> path;
            while (current != -1) {
                path.push_back(current);
                current = parent[current];
            }
            reverse(path.begin(), path.end());
            return path;
        }

        for (int neighbor : graph[current]) {
            if (!visited[neighbor]) {
                q.push(neighbor);
                visited[neighbor] = true;
                parent[neighbor] = current;
                distance[neighbor] = distance[current] + 1;
            }
        }
    }

    // If no path found
    return {};
}

int main() {
    // Example graph representation (adjacency list)
    vector<vector<int>> graph = {
        {1, 3},     // Node 0
        {0, 2, 4},  // Node 1
        {1, 5},     // Node 2
        {0, 4},     // Node 3
        {1, 3, 5},  // Node 4
        {2, 4}      // Node 5
    };

    int start = 0;  // Starting node
    int end = 5;    // Ending node

    vector<int> shortestPath = shortestPathBFS(graph, start, end);

    if (!shortestPath.empty()) {
        cout << "Shortest Path from " << start << " to " << end << ": ";
        for (int node : shortestPath) {
            cout << node << " ";
        }
        cout << endl;
    } else {
        cout << "No path exists from " << start << " to " << end << endl;
    }

    return 0;
}
```

This code defines a function `shortestPathBFS` that takes an adjacency list representation of an unweighted graph along with the start and end vertices. It returns the shortest path between the start and end vertices as a vector of integers representing the vertices in the path. If no path exists, it returns an empty vector. The `main` function provides an example usage of this function.

### 1. Algorithms & Data Structures (C++): Flood Fill - Graphs

Flood fill is a common algorithm used in image processing and computer graphics to determine a region connected to a given node in a multi-dimensional array. It's typically used to determine the area connected to a certain point with the same color in a two-dimensional image or matrix.

Here's a basic implementation of flood fill in C++ using recursion:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Define directions: up, down, left, right
int dr[] = {-1, 1, 0, 0};
int dc[] = {0, 0, -1, 1};

// Function to perform flood fill
void floodFill(vector<vector<int>>& image, int sr, int sc, int newColor, int originalColor) {
    // Base case: if current pixel is out of bounds or not the original color, return
    if (sr < 0 || sr >= image.size() || sc < 0 || sc >= image[0].size() || image[sr][sc] != originalColor) {
        return;
    }
    
    // Change the color of the current pixel
    image[sr][sc] = newColor;
    
    // Recursively call flood fill for neighboring pixels
    for (int i = 0; i < 4; ++i) {
        floodFill(image, sr + dr[i], sc + dc[i], newColor, originalColor);
    }
}

int main() {
    // Example usage
    vector<vector<int>> image = {
        {1, 1, 1, 1, 1},
        {1, 1, 0, 0, 1},
        {1, 0, 1, 0, 1},
        {1, 0, 0, 1, 1},
        {1, 1, 1, 1, 1}
    };
    
    int sr = 2, sc = 2; // Starting position
    int newColor = 2;   // New color to fill
    int originalColor = image[sr][sc]; // Original color
    
    floodFill(image, sr, sc, newColor, originalColor);
    
    // Output the result
    for (const auto& row : image) {
        for (int val : row) {
            cout << val << " ";
        }
        cout << endl;
    }
    
    return 0;
}
```

In this implementation:

- `floodFill()` function performs the actual flood fill. It takes the image, starting row and column, the new color to fill, and the original color of the starting pixel.
- Base case checks if the current pixel is out of bounds or not of the original color.
- If the base case is not met, it changes the color of the current pixel and recursively calls `floodFill()` for its neighbors.
- `main()` function provides an example usage, defining an image as a 2D vector and performing flood fill from a starting point.

You can adjust the starting point, original color, and new color according to your requirements.

### 1. Algorithms & Data Structures (C++): Floyd Warshall

Floyd Warshall is a classic algorithm used for finding the shortest paths in a weighted graph with positive or negative edge weights (but with no negative cycles). It's an all-pairs shortest path algorithm, meaning it computes the shortest path between every pair of vertices in a graph. Here's a basic implementation of the Floyd Warshall algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <climits>

using namespace std;

// Function to perform Floyd Warshall algorithm
void floydWarshall(vector<vector<int>>& graph) {
    int V = graph.size();
    
    // Initialize distances matrix
    vector<vector<int>> dist(V, vector<int>(V, INT_MAX));
    
    // Initialize distances to self as 0
    for(int i = 0; i < V; ++i)
        dist[i][i] = 0;
    
    // Update distances matrix
    for(int k = 0; k < V; ++k) {
        for(int i = 0; i < V; ++i) {
            for(int j = 0; j < V; ++j) {
                if(graph[i][k] != INT_MAX && graph[k][j] != INT_MAX && 
                   dist[i][k] + dist[k][j] < dist[i][j]) {
                    dist[i][j] = dist[i][k] + dist[k][j];
                }
            }
        }
    }
    
    // Print the shortest distances
    cout << "Shortest distances between every pair of vertices:\n";
    for(int i = 0; i < V; ++i) {
        for(int j = 0; j < V; ++j) {
            if(dist[i][j] == INT_MAX)
                cout << "INF ";
            else
                cout << dist[i][j] << " ";
        }
        cout << endl;
    }
}

int main() {
    // Example graph represented as adjacency matrix
    vector<vector<int>> graph = {
        {0, 5, INT_MAX, 10},
        {INT_MAX, 0, 3, INT_MAX},
        {INT_MAX, INT_MAX, 0, 1},
        {INT_MAX, INT_MAX, INT_MAX, 0}
    };

    // Applying Floyd Warshall algorithm
    floydWarshall(graph);
    
    return 0;
}
```

This code defines the Floyd Warshall algorithm to find the shortest distances between all pairs of vertices in a given graph. It initializes a distance matrix with the initial graph's edge weights and iteratively updates the matrix until it contains the shortest distances between all pairs of vertices. Finally, it prints the shortest distances between all pairs of vertices.

### 1. Algorithms & Data Structures (C++): Floyd Warshall Algorithm

The Floyd Warshall algorithm is a dynamic programming algorithm used for finding shortest paths in a weighted graph with positive or negative edge weights (but with no negative cycles). It works for both directed and undirected graphs. The algorithm computes the shortest distance between every pair of vertices in the graph. It's named after Robert Floyd and Stephen Warshall, who independently discovered it in 1959 and 1962, respectively.

Here's a basic outline of the algorithm:

1. Initialize a 2D array `dist` where `dist[i][j]` represents the shortest distance between vertex `i` and vertex `j`.
2. Initialize the `dist` matrix such that `dist[i][j] = INF` for all pairs `(i, j)` where there is no direct edge between `i` and `j`, and `dist[i][i] = 0`.
3. For each vertex `k`, iterate over all pairs of vertices `(i, j)`, and update `dist[i][j]` if the distance from `i` to `j` through vertex `k` is shorter than the current value of `dist[i][j]`. The update rule is: `dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])`.

Here's a simple implementation of the Floyd Warshall algorithm in C++:

```cpp
#include <iostream>
#include <vector>
using namespace std;

#define INF 99999

void floydWarshall(vector<vector<int>>& graph, int V) {
    vector<vector<int>> dist(graph);

    // Main algorithm to find shortest paths
    for (int k = 0; k < V; k++) {
        for (int i = 0; i < V; i++) {
            for (int j = 0; j < V; j++) {
                if (dist[i][k] != INF && dist[k][j] != INF && dist[i][k] + dist[k][j] < dist[i][j]) {
                    dist[i][j] = dist[i][k] + dist[k][j];
                }
            }
        }
    }

    // Print the shortest distances
    cout << "Shortest distances between every pair of vertices:\n";
    for (int i = 0; i < V; i++) {
        for (int j = 0; j < V; j++) {
            if (dist[i][j] == INF) cout << "INF\t";
            else cout << dist[i][j] << "\t";
        }
        cout << endl;
    }
}

int main() {
    int V;
    cout << "Enter the number of vertices: ";
    cin >> V;

    vector<vector<int>> graph(V, vector<int>(V, INF));

    cout << "Enter the adjacency matrix for the graph (INF for infinity):\n";
    for (int i = 0; i < V; i++) {
        for (int j = 0; j < V; j++) {
            cin >> graph[i][j];
        }
    }

    floydWarshall(graph, V);

    return 0;
}
```

This implementation takes input as an adjacency matrix and prints the shortest distances between every pair of vertices. You can modify it according to your needs.

### 1. Algorithms & Data Structures (C++): Floyd Warshall with negative cycle

Implementing the Floyd-Warshall algorithm in C++ with support for detecting negative cycles is a valuable skill. Here's a basic implementation:

```cpp
#include <iostream>
#include <vector>
#include <climits>

using namespace std;

#define INF INT_MAX

// Structure to represent a weighted edge
struct Edge {
    int src, dest, weight;
};

// Function to detect negative cycles using Floyd-Warshall algorithm
bool detectNegativeCycle(vector<vector<int>>& dist, int V) {
    for (int i = 0; i < V; i++) {
        if (dist[i][i] < 0) {
            return true; // Negative cycle detected
        }
    }
    return false;
}

// Function to print the distance matrix
void printSolution(vector<vector<int>>& dist, int V) {
    cout << "Shortest distances between every pair of vertices:\n";
    for (int i = 0; i < V; i++) {
        for (int j = 0; j < V; j++) {
            if (dist[i][j] == INF)
                cout << "INF\t";
            else
                cout << dist[i][j] << "\t";
        }
        cout << endl;
    }
}

// Floyd Warshall algorithm with negative cycle detection
void floydWarshall(vector<Edge>& edges, int V) {
    // Initialize distance matrix with INF
    vector<vector<int>> dist(V, vector<int>(V, INF));

    // Initialize diagonal elements as 0
    for (int i = 0; i < V; i++)
        dist[i][i] = 0;

    // Set distances to actual edge weights
    for (auto edge : edges)
        dist[edge.src][edge.dest] = edge.weight;

    // Main algorithm
    for (int k = 0; k < V; k++) {
        for (int i = 0; i < V; i++) {
            for (int j = 0; j < V; j++) {
                if (dist[i][k] != INF && dist[k][j] != INF &&
                    dist[i][k] + dist[k][j] < dist[i][j]) {
                    dist[i][j] = dist[i][k] + dist[k][j];
                }
            }
        }
    }

    // Check for negative cycles
    if (detectNegativeCycle(dist, V))
        cout << "Graph contains negative cycle(s).\n";
    else
        printSolution(dist, V);
}

int main() {
    // Example graph
    int V = 4; // Number of vertices
    vector<Edge> edges = {
        {0, 1, 5}, {0, 3, 10}, {1, 2, 3}, {2, 3, 1}, {3, 0, -7}
    };

    floydWarshall(edges, V);

    return 0;
}
```

This code detects negative cycles in the graph using the Floyd-Warshall algorithm. If a negative cycle is detected, it prints a message indicating the presence of a negative cycle; otherwise, it prints the shortest distances between every pair of vertices.

### 1. Algorithms & Data Structures (C++): Graph

Graphs are fundamental data structures in computer science that model relationships between entities. They consist of a set of vertices (nodes) and a set of edges (connections) that link pairs of vertices. Graphs are widely used in various applications such as social networks, routing algorithms, recommendation systems, and more. In C++, you can implement graphs using various representations such as adjacency matrix, adjacency list, or edge list. Here's a brief overview of these representations:

1. **Adjacency Matrix**: In this representation, a 2D array is used to store whether there is an edge between two vertices. If there is an edge from vertex `i` to vertex `j`, `matrix[i][j]` is set to 1, otherwise, it's set to 0. This representation is suitable for dense graphs but can be inefficient for sparse graphs due to its space complexity.

2. **Adjacency List**: In this representation, each vertex maintains a list of its adjacent vertices. This can be implemented using an array of lists, a vector of lists, or a hashmap where the key is the vertex and the value is a list of adjacent vertices. This representation is more memory efficient for sparse graphs.

3. **Edge List**: In this representation, each edge is represented as a pair of vertices. You can use a vector or list of pairs to store the edges. This representation is simple and space-efficient but might not be efficient for certain graph algorithms that require quick access to adjacent vertices.

Here's a basic example of implementing an undirected graph using an adjacency list in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V), adj(V) {}

    // Function to add an edge between vertices u and v
    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u); // For undirected graph
    }

    // Function to print the adjacency list representation of the graph
    void printGraph() {
        for (int v = 0; v < V; ++v) {
            cout << "Adjacency list of vertex " << v << ":\n";
            cout << "head";
            for (int i : adj[v])
                cout << " -> " << i;
            cout << endl;
        }
    }
};

int main() {
    Graph g(4); // Create a graph with 4 vertices
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(2, 3);

    g.printGraph();

    return 0;
}
```

This code creates an undirected graph with 4 vertices and adds some edges between them. Then, it prints the adjacency list representation of the graph.

### 1. Algorithms & Data Structures (C++): Graph: Depth First Search

Depth First Search (DFS) is a fundamental algorithm for traversing or searching tree or graph data structures. In the context of graphs, it explores as far as possible along each branch before backtracking.

Here's a basic implementation of Depth First Search in C++ for an adjacency list representation of a graph:

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

// Structure to represent a graph
class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V) {
        adj.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w);
    }

    // Depth First Search traversal from a given source vertex
    void DFS(int s) {
        // Vector to keep track of visited vertices
        vector<bool> visited(V, false);
        
        // Stack for DFS traversal
        stack<int> stack;

        // Push the source vertex onto the stack
        stack.push(s);

        while (!stack.empty()) {
            // Pop a vertex from stack and print it
            s = stack.top();
            stack.pop();

            // Stack may contain same vertex twice, so we need to print the popped item only if it's not visited
            if (!visited[s]) {
                cout << s << " ";
                visited[s] = true;
            }

            // Get all adjacent vertices of the popped vertex s. If an adjacent vertex has not been visited, then push it to the stack.
            for (auto it = adj[s].begin(); it != adj[s].end(); ++it) {
                if (!visited[*it]) {
                    stack.push(*it);
                }
            }
        }
    }
};

int main() {
    // Create a graph
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "Depth First Traversal starting from vertex 2: ";
    g.DFS(2);

    return 0;
}
```

This code represents a graph using an adjacency list and performs Depth First Search starting from a specified vertex. It prints the vertices visited during the traversal.

DFS can also be implemented recursively. Here's how you could do it:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

    // Recursive function for DFS traversal
    void DFSUtil(int v, vector<bool>& visited) {
        // Mark the current node as visited and print it
        visited[v] = true;
        cout << v << " ";

        // Recur for all the vertices adjacent to this vertex
        for (auto it = adj[v].begin(); it != adj[v].end(); ++it) {
            if (!visited[*it]) {
                DFSUtil(*it, visited);
            }
        }
    }

public:
    Graph(int V) : V(V) {
        adj.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w);
    }

    // Depth First Search traversal from a given source vertex
    void DFS(int v) {
        // Vector to keep track of visited vertices
        vector<bool> visited(V, false);
        
        // Call the recursive helper function to print DFS traversal
        DFSUtil(v, visited);
    }
};

int main() {
    // Create a graph
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "Depth First Traversal starting from vertex 2: ";
    g.DFS(2);

    return 0;
}
```

Both implementations achieve the same goal but through different means: one using a stack explicitly and the other using recursion.

### 1. Algorithms & Data Structures (C++): Graph: Dijkshtra's Algorithm

Dijkstra's algorithm is a fundamental algorithm in the field of graph theory and is used to find the shortest paths between nodes in a graph, particularly in graphs with non-negative edge weights. It's widely used in various applications, such as network routing protocols and GPS navigation systems.

Here's a high-level overview of how Dijkstra's algorithm works:

1. **Initialization**: Assign a tentative distance value to every node. Set the initial node's distance to 0 and all other nodes' distances to infinity. Maintain a priority queue (or a min-heap) to store nodes based on their tentative distances.

2. **Selecting the Shortest Path Node**: Extract the node with the smallest tentative distance from the priority queue.

3. **Relaxation**: For the current node, update the distances of its adjacent nodes if the path through the current node is shorter than the previously known path. This step ensures that the distances are always the shortest possible.

4. **Repeat**: Repeat steps 2 and 3 until all nodes have been visited or the destination node has been reached.

5. **Result**: Once the algorithm terminates, the shortest path from the source node to every other node (or the destination node) is known.

Here's a simple implementation of Dijkstra's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <climits>

using namespace std;

#define INF INT_MAX

// Structure to represent a node in the graph
struct Node {
    int id;
    int distance;

    Node(int _id, int _distance) : id(_id), distance(_distance) {}

    // Overloading comparison operator for priority queue
    bool operator<(const Node &other) const {
        return distance > other.distance; // Min-heap based on distance
    }
};

// Dijkstra's algorithm function
void dijkstra(vector<vector<pair<int, int>>> &graph, int source) {
    int n = graph.size(); // Number of nodes in the graph
    vector<int> dist(n, INF); // Array to store distances from the source node
    priority_queue<Node> pq; // Priority queue to store nodes based on tentative distances

    // Initialization
    dist[source] = 0;
    pq.push(Node(source, 0));

    while (!pq.empty()) {
        // Selecting the node with the shortest tentative distance
        Node current = pq.top();
        pq.pop();

        int u = current.id;
        
        // Relaxation
        for (auto neighbor : graph[u]) {
            int v = neighbor.first;
            int weight = neighbor.second;
            if (dist[u] != INF && dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
                pq.push(Node(v, dist[v]));
            }
        }
    }

    // Print the shortest distances from the source node
    cout << "Shortest distances from node " << source << ":\n";
    for (int i = 0; i < n; ++i) {
        cout << "Node " << i << ": ";
        if (dist[i] == INF)
            cout << "INF\n";
        else
            cout << dist[i] << "\n";
    }
}

int main() {
    // Example graph representation (adjacency list)
    int n = 5; // Number of nodes
    vector<vector<pair<int, int>>> graph(n);

    // Adding edges to the graph (node, weight)
    graph[0].push_back(make_pair(1, 10));
    graph[0].push_back(make_pair(2, 5));
    graph[1].push_back(make_pair(2, 2));
    graph[1].push_back(make_pair(3, 1));
    graph[2].push_back(make_pair(1, 3));
    graph[2].push_back(make_pair(3, 9));
    graph[2].push_back(make_pair(4, 2));
    graph[3].push_back(make_pair(4, 4));
    graph[4].push_back(make_pair(3, 6));

    // Calling Dijkstra's algorithm from node 0
    dijkstra(graph, 0);

    return 0;
}
```

This code demonstrates Dijkstra's algorithm using an adjacency list representation for the graph. You can modify the graph and the source node as needed for your specific use case.

### 1. Algorithms & Data Structures (C++): Graph: Find Star in the graph

To find a star in a graph, you need to define what constitutes a "star." Typically, in graph theory, a star is a special kind of graph where one node (called the center) is connected to all other nodes (called leaves) in the graph.

Here's how you can find a star in a graph using C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to find if the given graph is a star or not
bool isStar(const vector<vector<int>>& graph) {
    int n = graph.size();
    
    // Count the number of edges for each node
    vector<int> degree(n, 0);
    for (int i = 0; i < n; ++i) {
        for (int j : graph[i]) {
            degree[j]++;
        }
    }
    
    // Count the number of nodes with degree n-1
    int center = -1;
    int leafCount = 0;
    for (int i = 0; i < n; ++i) {
        if (degree[i] == n - 1) {
            center = i;
        } else if (degree[i] == 1) {
            leafCount++;
        } else {
            return false; // Not a star
        }
    }
    
    // The center should be connected to all other nodes
    return (center != -1 && leafCount == n - 1);
}

int main() {
    // Example graph represented as an adjacency list
    vector<vector<int>> graph = {
        {1, 2, 3}, // Node 0 is connected to nodes 1, 2, and 3
        {0},       // Node 1 is connected to node 0
        {0},       // Node 2 is connected to node 0
        {0}        // Node 3 is connected to node 0
    };
    
    if (isStar(graph)) {
        cout << "The given graph is a star." << endl;
    } else {
        cout << "The given graph is not a star." << endl;
    }
    
    return 0;
}
```

This code defines a function `isStar()` that takes a graph represented as an adjacency list and returns true if the graph is a star, and false otherwise. The main function provides an example of how to use this function with a sample graph.

### 1. Algorithms & Data Structures (C++): Graph: Kahn's Algorithm (Modified Breadth First Search)

Kahn's Algorithm is a classic algorithm used for Topological Sorting, which is an ordering of the vertices of a directed graph such that for every directed edge uv from vertex u to vertex v, u comes before v in the ordering. This algorithm is based on the concept of maintaining a set of vertices with no incoming edges (i.e., vertices with in-degree 0) and gradually removing them from the graph.

Here's a modified version of Kahn's Algorithm implemented in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V), adj(V) {}

    // Function to add an edge from u to v
    void addEdge(int u, int v) {
        adj[u].push_back(v);
    }

    // Kahn's Algorithm for Topological Sorting
    vector<int> topologicalSort() {
        vector<int> inDegree(V, 0);
        queue<int> q;
        vector<int> result;

        // Calculate in-degree of each vertex
        for (int u = 0; u < V; ++u) {
            for (int v : adj[u]) {
                inDegree[v]++;
            }
        }

        // Enqueue vertices with in-degree 0
        for (int u = 0; u < V; ++u) {
            if (inDegree[u] == 0) {
                q.push(u);
            }
        }

        while (!q.empty()) {
            int u = q.front();
            q.pop();
            result.push_back(u);

            // Reduce in-degree of adjacent vertices
            for (int v : adj[u]) {
                if (--inDegree[v] == 0) {
                    q.push(v);
                }
            }
        }

        // Check if graph has a cycle
        if (result.size() != V) {
            cout << "Graph has a cycle!" << endl;
            return vector<int>();
        }

        return result;
    }
};

int main() {
    int V = 6;
    Graph g(V);
    g.addEdge(5, 2);
    g.addEdge(5, 0);
    g.addEdge(4, 0);
    g.addEdge(4, 1);
    g.addEdge(2, 3);
    g.addEdge(3, 1);

    cout << "Topological Sorting Order: ";
    vector<int> result = g.topologicalSort();
    if (!result.empty()) {
        for (int u : result) {
            cout << u << " ";
        }
        cout << endl;
    }

    return 0;
}
```

This code demonstrates Kahn's Algorithm for Topological Sorting on a sample directed graph. The `Graph` class represents the graph, and `topologicalSort()` function returns a vector containing the vertices in topological order. If the graph has a cycle, it prints a message indicating that. Finally, in the `main()` function, an example graph is created, and its topological order is printed.

### 1. Algorithms & Data Structures (C++): Graph: Keys and Rooms

In the context of algorithms and data structures, the "Keys and Rooms" problem is a classic graph traversal problem. The problem statement typically goes like this:

Given a collection of rooms represented as a graph where each room is labeled with a distinct positive integer, and each room may have some keys to access other rooms. Keys are represented by the room numbers they can unlock. Starting with room 0, determine if you can visit every room.

This problem can be efficiently solved using graph traversal algorithms like Depth First Search (DFS) or Breadth First Search (BFS).

Here's a brief outline of how you can approach this problem in C++ using DFS:

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>

using namespace std;

void dfs(int room, vector<vector<int>>& rooms, unordered_set<int>& visited) {
    if (visited.count(room)) return; // Already visited
    visited.insert(room); // Mark the room as visited

    for (int key : rooms[room]) {
        dfs(key, rooms, visited); // Recursively visit neighboring rooms
    }
}

bool canVisitAllRooms(vector<vector<int>>& rooms) {
    unordered_set<int> visited;
    dfs(0, rooms, visited); // Start DFS from room 0

    return visited.size() == rooms.size(); // Check if all rooms are visited
}

int main() {
    vector<vector<int>> rooms = {{1}, {2}, {3}, {}};
    // Example input: {{1}, {2}, {3}, {}}, meaning room 0 has key to room 1, room 1 has key to room 2, and so on.

    if (canVisitAllRooms(rooms)) {
        cout << "You can visit every room." << endl;
    } else {
        cout << "You cannot visit every room." << endl;
    }

    return 0;
}
```

This code performs a DFS traversal starting from room 0 and marks all visited rooms. At the end, it checks if all rooms have been visited. If yes, then it returns true, otherwise false.

This problem demonstrates the application of graph traversal algorithms in solving real-world problems.

### 1. Algorithms & Data Structures (C++): Graph: No of Connected Component

To find the number of connected components in a graph using C++, you can use depth-first search (DFS) or breadth-first search (BFS) algorithms. Here's a simple implementation using DFS:

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

    void DFSUtil(int v, vector<bool>& visited);

public:
    Graph(int V); // Constructor
    void addEdge(int v, int w); // Function to add an edge to the graph
    int countConnectedComponents(); // Function to count connected components
};

Graph::Graph(int V) {
    this->V = V;
    adj.resize(V);
}

void Graph::addEdge(int v, int w) {
    adj[v].push_back(w);
    adj[w].push_back(v); // For undirected graph
}

void Graph::DFSUtil(int v, vector<bool>& visited) {
    visited[v] = true;

    for (int i = 0; i < adj[v].size(); ++i) {
        int neighbor = adj[v][i];
        if (!visited[neighbor])
            DFSUtil(neighbor, visited);
    }
}

int Graph::countConnectedComponents() {
    vector<bool> visited(V, false);
    int count = 0;

    for (int v = 0; v < V; ++v) {
        if (!visited[v]) {
            DFSUtil(v, visited);
            ++count;
        }
    }

    return count;
}

int main() {
    Graph g(5); // Create a graph with 5 vertices
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(3, 4);

    cout << "Number of connected components: " << g.countConnectedComponents() << endl;

    return 0;
}
```

This code defines a `Graph` class that represents an undirected graph using an adjacency list. The `countConnectedComponents` method uses DFS to traverse the graph and count the number of connected components. Finally, the `main` function demonstrates its usage. You can modify the `main` function and the graph edges as per your requirement.

### 1. Algorithms & Data Structures (C++): Graph: PreOrder, InOrder, PostOrder

In the context of graphs, terms like "PreOrder," "InOrder," and "PostOrder" are more commonly associated with tree traversals rather than graphs. However, if we're talking about graph traversals, the typical terms used are "Depth-First Search (DFS)" and "Breadth-First Search (BFS)."

DFS and BFS can be applied to both trees and graphs, but they have slightly different meanings when applied to graphs. In the case of graphs, DFS and BFS involve visiting all vertices or nodes of the graph, whereas in trees, they traverse through the nodes and their children.

Here's a brief overview of DFS and BFS in the context of graphs:

1. **Depth-First Search (DFS):**
   - DFS explores as far as possible along each branch before backtracking.
   - It starts at a given vertex and explores as far as possible along each branch before backtracking.
   - DFS is often implemented using recursion or a stack data structure.
   - DFS can be used to detect cycles in a graph.
   - The order of visiting nodes in DFS can be classified into three categories: PreOrder, InOrder, and PostOrder, but it's more common to use these terms in the context of tree traversals.

2. **Breadth-First Search (BFS):**
   - BFS explores all the neighbor nodes at the present depth before moving on to the nodes at the next depth level.
   - It starts at a given vertex and explores all of the neighbor vertices at the present depth prior to moving on to the vertices at the next depth level.
   - BFS is usually implemented using a queue data structure.
   - BFS is often used to find the shortest path between two vertices in an unweighted graph.
   - It guarantees the shortest path.

If you're interested in implementing DFS and BFS for graphs in C++, there are many online resources and textbooks available with code examples. Would you like an example of DFS and BFS implementation in C++?

### 1. Algorithms & Data Structures (C++): Graph: Remove Edge

To remove an edge from a graph in C++, you typically need to find the edge in the graph's data structure and then delete it. Assuming you're using an adjacency list representation for the graph, here's how you can remove an edge:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Class representing a graph using adjacency list
class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    // Constructor
    Graph(int V) : V(V) {
        adj.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u); // For undirected graph
    }

    // Function to remove an edge from the graph
    void removeEdge(int u, int v) {
        // Find the edge and remove it from both vertices' adjacency lists
        for (auto it = adj[u].begin(); it != adj[u].end(); ++it) {
            if (*it == v) {
                adj[u].erase(it);
                break;
            }
        }

        for (auto it = adj[v].begin(); it != adj[v].end(); ++it) {
            if (*it == u) {
                adj[v].erase(it);
                break;
            }
        }
    }

    // Function to print the graph
    void printGraph() {
        for (int i = 0; i < V; ++i) {
            cout << "Vertex " << i << ": ";
            for (int v : adj[i]) {
                cout << v << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 3);

    cout << "Original Graph:" << endl;
    g.printGraph();

    // Remove an edge
    cout << "\nRemoving edge (0, 2)..." << endl;
    g.removeEdge(0, 2);

    // Print the modified graph
    cout << "\nModified Graph:" << endl;
    g.printGraph();

    return 0;
}
```

This code demonstrates how to remove an edge (0, 2) from a graph represented using an adjacency list. The `removeEdge` function removes the specified edge from both vertices' adjacency lists.

### 1. Algorithms & Data Structures (C++): Graph: Remove Vertex

To remove a vertex from a graph in C++, you need to perform the following steps:

1. Remove the vertex from the adjacency list of all its neighboring vertices.
2. Remove the vertex itself from the graph.

Here's a basic implementation using an adjacency list representation:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V) {
        adj.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u); // Uncomment this line if the graph is undirected
    }

    // Function to remove a vertex from the graph
    void removeVertex(int v) {
        // Remove vertex from adjacency list of all neighboring vertices
        for (int i = 0; i < V; ++i) {
            adj[i].erase(remove(adj[i].begin(), adj[i].end(), v), adj[i].end());
        }
        
        // Remove vertex itself
        adj[v].clear();
    }

    // Function to print the adjacency list representation of the graph
    void printGraph() {
        for (int i = 0; i < V; ++i) {
            cout << "Adjacency list of vertex " << i << ": ";
            for (int j : adj[i]) {
                cout << j << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    Graph g(5); // Create a graph with 5 vertices
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(2, 4);
    g.addEdge(3, 4);
    
    cout << "Original graph:" << endl;
    g.printGraph();
    
    g.removeVertex(2); // Remove vertex 2
    
    cout << "\nGraph after removing vertex 2:" << endl;
    g.printGraph();
    
    return 0;
}
```

This code demonstrates how to remove a vertex from a graph represented using an adjacency list. Make sure to uncomment the line `adj[v].push_back(u);` in the `addEdge` function if the graph is undirected.

### 1. Algorithms & Data Structures (C++): Graph: Shortest Path Problem

The shortest path problem is a fundamental problem in graph theory and has many real-world applications, such as GPS navigation, network routing, and scheduling. In C++, you can solve the shortest path problem using various algorithms like Dijkstra's algorithm, Bellman-Ford algorithm, or Floyd-Warshall algorithm. Here's a basic implementation of Dijkstra's algorithm for finding the shortest path from a source vertex to all other vertices in a weighted graph:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>

using namespace std;

// Graph edge representation
struct Edge {
    int to;
    int weight;
    Edge(int _to, int _weight) : to(_to), weight(_weight) {}
};

// Graph representation using adjacency list
using Graph = vector<vector<Edge>>;

// Function to find the shortest paths using Dijkstra's algorithm
vector<int> dijkstra(const Graph& graph, int source) {
    int n = graph.size();
    vector<int> dist(n, numeric_limits<int>::max());
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;

    dist[source] = 0;
    pq.push({0, source});

    while (!pq.empty()) {
        int u = pq.top().second;
        int u_dist = pq.top().first;
        pq.pop();

        if (u_dist > dist[u])
            continue;

        for (const auto& edge : graph[u]) {
            int v = edge.to;
            int weight = edge.weight;
            if (dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
                pq.push({dist[v], v});
            }
        }
    }

    return dist;
}

int main() {
    // Example graph
    int num_vertices = 6;
    Graph graph(num_vertices);

    graph[0].push_back(Edge(1, 5));
    graph[0].push_back(Edge(2, 3));
    graph[1].push_back(Edge(3, 6));
    graph[1].push_back(Edge(2, 2));
    graph[2].push_back(Edge(4, 4));
    graph[2].push_back(Edge(5, 2));
    graph[2].push_back(Edge(3, 7));
    graph[3].push_back(Edge(4, -1));
    graph[4].push_back(Edge(5, -2));

    int source = 0;
    vector<int> shortest_paths = dijkstra(graph, source);

    cout << "Shortest paths from vertex " << source << ":\n";
    for (int i = 0; i < num_vertices; ++i) {
        cout << "Vertex " << i << ": " << shortest_paths[i] << endl;
    }

    return 0;
}
```

This code defines a simple undirected graph with weighted edges and uses Dijkstra's algorithm to find the shortest paths from a given source vertex to all other vertices. You can modify the `Graph` definition and the graph initialization part to represent your specific graph and solve the shortest path problem accordingly.

### 1. Algorithms & Data Structures (C++): Graph: Terminology

In the realm of algorithms and data structures, graphs are fundamental structures used to model relationships between objects. Here's some key terminology related to graphs:

1. **Vertex (or Node)**: A fundamental unit of a graph, representing an entity. In applications, vertices can represent various things like cities in a transportation network, web pages in a hyperlinked structure, or individuals in a social network.

2. **Edge (or Arc)**: A connection between two vertices. It may be directed (from one vertex to another) or undirected (bi-directional).

3. **Weight**: A numerical value assigned to an edge, representing some measure like distance, cost, or capacity.

4. **Directed Graph (or Digraph)**: A graph where edges have a direction, meaning they point from one vertex to another. The direction implies a relationship or flow between the vertices.

5. **Undirected Graph**: A graph where edges have no direction. Relationships between vertices are symmetric, and edges represent bidirectional connections.

6. **Degree**: For a vertex in an undirected graph, the degree is the number of edges incident to the vertex. In a directed graph, there are two degrees: the in-degree (number of edges coming into the vertex) and the out-degree (number of edges going out of the vertex).

7. **Path**: A sequence of vertices where each adjacent pair is connected by an edge. Paths can be simple (no repeated vertices) or allow revisiting vertices (cycles).

8. **Cycle**: A path that starts and ends at the same vertex, with no repeated edges (except for the final one connecting back to the start).

9. **Connected Graph**: An undirected graph where there is a path between every pair of vertices.

10. **Strongly Connected Graph**: A directed graph where there is a directed path between every pair of vertices.

11. **Component**: A maximal subgraph in an undirected graph where there is a path between every pair of vertices within the subgraph.

12. **Tree**: A connected graph with no cycles. A directed tree is a directed graph with a single vertex called the root, from which all other vertices are reachable via directed paths.

13. **Forest**: A disjoint set of trees.

14. **Spanning Tree**: A subgraph of a graph that is a tree and includes all the vertices of the original graph.

15. **Graph Traversal**: The process of systematically visiting all the vertices and edges of a graph. Common algorithms for graph traversal include Depth-First Search (DFS) and Breadth-First Search (BFS).

16. **Topological Sorting**: An ordering of the vertices of a directed graph such that for every directed edge uv from vertex u to vertex v, u comes before v in the ordering.

17. **Adjacency Matrix**: A two-dimensional array where the presence or absence of an edge between vertices is represented by 1 or 0, respectively.

18. **Adjacency List**: A data structure that represents a graph as an array of lists. Each element of the array represents a vertex, and the list associated with a vertex contains all the vertices adjacent to it.

Understanding these terms is crucial for designing, implementing, and analyzing algorithms that operate on graphs.

### 1. Algorithms & Data Structures (C++): Graph: Topological Ordering

Topological ordering is a fundamental concept in graph theory. It refers to arranging the vertices of a directed graph in such a way that if there is a directed edge from vertex \( u \) to vertex \( v \), then \( u \) comes before \( v \) in the ordering. In other words, it's an ordering of the vertices such that for every directed edge \( (u, v) \), vertex \( u \) comes before vertex \( v \).

Topological ordering is particularly useful in various applications, such as task scheduling, dependency resolution, and constraint satisfaction problems.

Here's a general approach to finding the topological ordering of a directed acyclic graph (DAG) using depth-first search (DFS) in C++:

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

// Function to perform DFS traversal and topological sorting
void topologicalSortUtil(int v, vector<bool>& visited, stack<int>& Stack, vector<vector<int>>& graph) {
    visited[v] = true; // Mark the current vertex as visited

    // Recur for all the vertices adjacent to this vertex
    for (int i = 0; i < graph[v].size(); ++i) {
        if (!visited[graph[v][i]])
            topologicalSortUtil(graph[v][i], visited, Stack, graph);
    }

    // Push the current vertex to the stack which stores the result
    Stack.push(v);
}

// Function to perform topological sorting
void topologicalSort(vector<vector<int>>& graph, int V) {
    stack<int> Stack; // A stack to store the vertices

    vector<bool> visited(V, false); // Mark all the vertices as not visited

    // Call the recursive helper function to store topological sort starting from all vertices one by one
    for (int i = 0; i < V; ++i) {
        if (!visited[i])
            topologicalSortUtil(i, visited, Stack, graph);
    }

    // Print the contents of the stack
    while (!Stack.empty()) {
        cout << Stack.top() << " ";
        Stack.pop();
    }
}

int main() {
    // Example graph represented as an adjacency list
    vector<vector<int>> graph = {
        {1, 2},     // 0 -> 1, 2
        {2, 3},     // 1 -> 2, 3
        {3},        // 2 -> 3
        {4},        // 3 -> 4
        {},         // 4 -> No outgoing edges
    };

    int V = graph.size(); // Number of vertices in the graph

    cout << "Topological ordering of the graph: ";
    topologicalSort(graph, V);

    return 0;
}
```

This code demonstrates the topological sorting of a directed acyclic graph represented as an adjacency list. The `topologicalSortUtil` function is a recursive function that performs DFS traversal and stores the vertices in a stack. After visiting all vertices, the main function prints the vertices in the order they were popped from the stack, giving the topological ordering.

### 1. Algorithms & Data Structures (C++): Graph: Topological Ordering using Breadth First Search

To perform topological ordering using Breadth First Search (BFS) in a graph implemented in C++, you can follow these steps:

1. Represent the graph: Define a graph class with appropriate data structures to store vertices and edges.
2. Implement BFS: Write a BFS function to traverse the graph and enqueue vertices based on their dependencies.
3. Implement topological ordering: Modify BFS to generate the topological ordering of the graph.

Here's a sample implementation:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V), adj(V) {}

    // Function to add an edge to the graph
    void addEdge(int u, int v) {
        adj[u].push_back(v);
    }

    // Function to perform topological sorting using BFS
    vector<int> topologicalSort() {
        vector<int> inDegree(V, 0); // Store in-degree of vertices
        for (int u = 0; u < V; ++u) {
            for (int v : adj[u]) {
                inDegree[v]++;
            }
        }

        queue<int> q;
        for (int u = 0; u < V; ++u) {
            if (inDegree[u] == 0) {
                q.push(u);
            }
        }

        vector<int> topoOrder;
        while (!q.empty()) {
            int u = q.front();
            q.pop();
            topoOrder.push_back(u);

            // Reduce in-degree of adjacent vertices
            for (int v : adj[u]) {
                inDegree[v]--;
                if (inDegree[v] == 0) {
                    q.push(v);
                }
            }
        }

        // Check for cycle
        if (topoOrder.size() != V) {
            cout << "Graph contains a cycle!" << endl;
            return {};
        }

        return topoOrder;
    }
};

int main() {
    Graph g(6);
    g.addEdge(5, 2);
    g.addEdge(5, 0);
    g.addEdge(4, 0);
    g.addEdge(4, 1);
    g.addEdge(2, 3);
    g.addEdge(3, 1);

    vector<int> order = g.topologicalSort();
    cout << "Topological Ordering: ";
    for (int v : order) {
        cout << v << " ";
    }
    cout << endl;

    return 0;
}
```

This code defines a `Graph` class with an adjacency list representation. The `topologicalSort` function performs BFS to generate the topological ordering of the graph. Finally, the `main` function demonstrates its usage by creating a sample graph and printing the topological ordering.

### 1. Algorithms & Data Structures (C++): Graph: Traversals

Graph traversals are fundamental operations in graph theory and are essential in understanding the structure and relationships within a graph. In C++, there are several algorithms for traversing graphs, including Depth-First Search (DFS) and Breadth-First Search (BFS). Here's how you can implement them:

1. **Depth-First Search (DFS)**:
   DFS explores as far as possible along each branch before backtracking. It is often implemented using recursion.

   ```cpp
   #include <iostream>
   #include <vector>
   #include <stack>
   using namespace std;

   void dfs(vector<vector<int>>& graph, int node, vector<bool>& visited) {
       visited[node] = true;
       cout << node << " ";

       for (int neighbor : graph[node]) {
           if (!visited[neighbor]) {
               dfs(graph, neighbor, visited);
           }
       }
   }

   void dfsTraversal(vector<vector<int>>& graph, int start) {
       int numNodes = graph.size();
       vector<bool> visited(numNodes, false);

       dfs(graph, start, visited);
   }

   int main() {
       // Example graph represented as an adjacency list
       vector<vector<int>> graph = {
           {1, 2},    // Node 0 is connected to nodes 1 and 2
           {0, 3, 4}, // Node 1 is connected to nodes 0, 3, and 4
           {0, 5},    // Node 2 is connected to nodes 0 and 5
           {1},       // Node 3 is connected to node 1
           {1},       // Node 4 is connected to node 1
           {2}        // Node 5 is connected to node 2
       };

       cout << "DFS Traversal starting from node 0: ";
       dfsTraversal(graph, 0);
       cout << endl;

       return 0;
   }
   ```

2. **Breadth-First Search (BFS)**:
   BFS explores neighbors of a node before moving on to the next level of neighbors. It is typically implemented using a queue.

   ```cpp
   #include <iostream>
   #include <vector>
   #include <queue>
   using namespace std;

   void bfs(vector<vector<int>>& graph, int start) {
       int numNodes = graph.size();
       vector<bool> visited(numNodes, false);
       queue<int> q;

       visited[start] = true;
       q.push(start);

       while (!q.empty()) {
           int node = q.front();
           q.pop();
           cout << node << " ";

           for (int neighbor : graph[node]) {
               if (!visited[neighbor]) {
                   visited[neighbor] = true;
                   q.push(neighbor);
               }
           }
       }
   }

   int main() {
       // Example graph represented as an adjacency list
       vector<vector<int>> graph = {
           {1, 2},    // Node 0 is connected to nodes 1 and 2
           {0, 3, 4}, // Node 1 is connected to nodes 0, 3, and 4
           {0, 5},    // Node 2 is connected to nodes 0 and 5
           {1},       // Node 3 is connected to node 1
           {1},       // Node 4 is connected to node 1
           {2}        // Node 5 is connected to node 2
       };

       cout << "BFS Traversal starting from node 0: ";
       bfs(graph, 0);
       cout << endl;

       return 0;
   }
   ```

These are basic implementations; you can customize them according to your specific requirements, such as keeping track of paths, distances, or modifying them for different types of graphs.

### 1. Algorithms & Data Structures (C++): Graph: Unordered Sets

In C++, the `unordered_set` container from the Standard Template Library (STL) can be useful for implementing certain graph algorithms efficiently. However, it's important to note that `unordered_set` is a set container that stores unique elements in no particular order, so it's typically used for implementing graph representations like an adjacency list.

Here's a basic example of how you might use `unordered_set` to represent an undirected graph:

```cpp
#include <iostream>
#include <unordered_set>
#include <vector>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    unordered_set<int>* adjList; // Adjacency list

public:
    Graph(int V) {
        this->V = V;
        adjList = new unordered_set<int>[V];
    }

    // Function to add an edge between vertices v and w
    void addEdge(int v, int w) {
        adjList[v].insert(w);
        adjList[w].insert(v); // For undirected graph
    }

    // Function to print the adjacency list representation of the graph
    void printGraph() {
        for (int v = 0; v < V; ++v) {
            cout << "Adjacency list of vertex " << v << ": ";
            for (auto it = adjList[v].begin(); it != adjList[v].end(); ++it)
                cout << *it << " ";
            cout << endl;
        }
    }
};

int main() {
    Graph g(5); // Create a graph with 5 vertices

    // Add edges
    g.addEdge(0, 1);
    g.addEdge(0, 4);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 3);
    g.addEdge(3, 4);

    // Print the adjacency list representation of the graph
    g.printGraph();

    return 0;
}
```

In this example:

- We define a `Graph` class with a private member `adjList`, which is an array of unordered sets. Each element of this array represents a vertex, and the unordered set associated with each vertex stores its adjacent vertices.
- The `addEdge` function adds an undirected edge between two vertices by inserting each vertex into the other's adjacency list.
- The `printGraph` function simply prints out the adjacency list representation of the graph.

This example demonstrates a basic usage of `unordered_set` for implementing an adjacency list representation of an undirected graph. Depending on the specific graph algorithm you're implementing, you might need to modify or extend this example accordingly.

### 1. Algorithms & Data Structures (C++): Graphs

Graphs are fundamental data structures used to model connections or relationships between pairs of objects. In C++, graphs can be implemented using various data structures such as adjacency matrix, adjacency list, or an edge list. Here's a brief overview of each:

1. **Adjacency Matrix**:
   - In an adjacency matrix, a 2D array is used to represent the connections between vertices.
   - If there are n vertices in the graph, the matrix is of size n x n.
   - Matrix[i][j] represents the edge between vertex i and vertex j.
   - This representation is suitable for dense graphs where the number of edges is close to the maximum possible.

2. **Adjacency List**:
   - In an adjacency list, each vertex of the graph maintains a list of adjacent vertices.
   - It is typically implemented using an array of lists (or vectors in C++).
   - Each entry in the array corresponds to a vertex, and the list contains the vertices adjacent to that vertex.
   - This representation is suitable for sparse graphs where the number of edges is much smaller compared to the number of vertices.

3. **Edge List**:
   - In an edge list, each edge of the graph is represented explicitly.
   - It is usually implemented using a vector or list of pairs (or structures in C++) where each pair represents an edge.
   - This representation is simple and efficient for storing and manipulating the edges of the graph.

Graph algorithms can be broadly categorized into two types: traversal algorithms and pathfinding algorithms.

Traversal algorithms explore or visit all vertices or edges of the graph. Common traversal algorithms include Depth-First Search (DFS) and Breadth-First Search (BFS).

Pathfinding algorithms aim to find paths between vertices in the graph. Common pathfinding algorithms include Dijkstra's algorithm for finding the shortest path between two vertices in a weighted graph, and the Bellman-Ford algorithm, which can handle graphs with negative edge weights. Additionally, there's the A* algorithm, which is an informed search algorithm commonly used for pathfinding in games and robotics.

C++ provides powerful standard libraries like STL (Standard Template Library) that can be leveraged for implementing and working with graphs efficiently. For instance, you can use containers like vectors, sets, and queues along with algorithms provided by the STL to perform graph operations effectively.

### 1. Algorithms & Data Structures (C++): Graphs ADT

In C++, implementing a Graph Abstract Data Type (ADT) involves defining the structure of a graph and the operations that can be performed on it. Here's a basic implementation of a Graph ADT using adjacency list representation:

```cpp
#include <iostream>
#include <vector>
#include <list>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector

<vector<int>> adj; // Adjacency list

public:
    Graph(int vertices) : V(vertices) {
        adj.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u); // For undirected graph
    }

    // Function to print the adjacency list representation of the graph
    void printGraph() {
        for (int v = 0; v < V; ++v) {
            cout << "Adjacency list of vertex " << v << ": ";
            for (const auto& vertex : adj[v]) {
                cout << "-> " << vertex;
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph g(5);

    // Add edges
    g.addEdge(0, 1);
    g.addEdge(0, 4);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 3);
    g.addEdge(3, 4);

    // Print the adjacency list representation of the graph
    g.printGraph();

    return 0;
}
```

This code defines a Graph class with methods to add edges and print the adjacency list representation of the graph. The `addEdge` method adds an edge between two vertices, and the `printGraph` method displays the adjacency list for each vertex. This implementation assumes an undirected graph.

### 1. Algorithms & Data Structures (C++): Graphs Algorithms

Graph algorithms are crucial in computer science and are widely used in various applications such as network routing, social network analysis, and recommendation systems. In C++, you can implement graph algorithms efficiently using different data structures like adjacency lists or adjacency matrices. Here are some common graph algorithms along with brief explanations:

1. **Breadth-First Search (BFS)**:
   - BFS is used to traverse or search a graph in a breadthward motion. It starts at a chosen vertex and explores all of the neighbor vertices at the present depth before moving on to the vertices at the next depth level.
   - It's often used to find the shortest path in an unweighted graph.
   - Implementation involves using a queue data structure.

2. **Depth-First Search (DFS)**:
   - DFS explores as far as possible along each branch before backtracking. It's often used for topological sorting, cycle detection, and connected components.
   - Implementation involves using recursion or a stack data structure.

3. **Dijkstra's Algorithm**:
   - Dijkstra's algorithm finds the shortest paths between nodes in a graph, which may represent, for example, road networks.
   - It's a greedy algorithm that iteratively selects the vertex with the shortest distance from the source vertex until all vertices are included.
   - It's typically implemented using a priority queue (min heap) or a set data structure.

4. **Bellman-Ford Algorithm**:
   - Similar to Dijkstra's algorithm, but it can handle graphs with negative edge weights (as long as there are no negative cycles).
   - It iterates over all edges multiple times, relaxing them to update the shortest path estimate.
   - Slower than Dijkstra's algorithm but more versatile due to handling negative weights.

5. **Floyd-Warshall Algorithm**:
   - Used to find the shortest paths between all pairs of vertices in a weighted graph.
   - It's based on dynamic programming and works for graphs with both positive and negative edge weights (but no negative cycles).
   - It's less efficient than Dijkstra's or Bellman-Ford for single-source shortest path problems but more efficient for all-pairs shortest paths.

6. **Topological Sorting**:
   - It's used to order the vertices of a directed graph in such a way that for every directed edge from vertex u to vertex v, u comes before v in the ordering.
   - It's useful in scheduling problems, such as in task scheduling or dependency resolution.

7. **Minimum Spanning Tree (MST)**:
   - Algorithms like Kruskal's and Prim's are used to find the minimum spanning tree of a graph, which is a subgraph that is a tree and connects all the vertices together with the minimum possible total edge weight.
   - Kruskal's algorithm is based on sorting the edges by weight and greedily adding them to the MST if they don't create a cycle.
   - Prim's algorithm starts from an arbitrary vertex and grows the MST by adding the lightest edge that connects a vertex in the MST to a vertex outside of it.

These are just a few examples, and there are many more graph algorithms depending on specific requirements and constraints of the problem at hand. Implementing these algorithms efficiently in C++ involves choosing appropriate data structures and paying attention to algorithmic complexity.

### 1. Algorithms & Data Structures (C++): Graphs as Trees

In C++, graphs can be represented using trees by employing various tree-based data structures. One common approach is to use an adjacency list or adjacency matrix to represent the graph and then traverse it using tree traversal algorithms like Depth-First Search (DFS) or Breadth-First Search (BFS). Here's a basic implementation using adjacency list and DFS:

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>

using namespace std;

// Graph class using adjacency list representation
class Graph {
    int V; // Number of vertices
    vector

<pair<int, unordered_set<int>>> adj; // Adjacency list

public:
    Graph(int V) : V(V), adj(V) {}

    // Function to add an edge to the graph
    void addEdge(int u, int v) {
        adj[u].second.insert(v); // Insert v into the adjacency list of u
        adj[v].second.insert(u); // For undirected graph, insert u into the adjacency list of v
    }

    // Depth-First Search traversal
    void DFSUtil(int v, vector<bool>& visited) {
        visited[v] = true;
        cout << v << " "; // Print the current vertex

        // Recursive DFS for all adjacent vertices
        for (auto& neighbor : adj[v].second) {
            if (!visited[neighbor]) {
                DFSUtil(neighbor, visited);
            }
        }
    }

    // Depth-First Search traversal starting from vertex v
    void DFS(int v) {
        vector<bool> visited(V, false); // Mark all vertices as not visited
        DFSUtil(v, visited);
    }
};

int main() {
    Graph g(5); // Create a graph with 5 vertices

    // Add edges
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);

    cout << "Depth-First Traversal starting from vertex 0: ";
    g.DFS(0); // Perform DFS starting from vertex 0

    return 0;
}
```

In this implementation:

- The `Graph` class represents an undirected graph using an adjacency list.
- `addEdge` function adds an edge between two vertices.
- `DFSUtil` is a recursive utility function used by the `DFS` function to perform Depth-First Search traversal starting from a given vertex.
- `DFS` function initializes the visited array and calls `DFSUtil` to start DFS traversal from the given vertex.
- In the `main` function, a `Graph` object `g` is created with 5 vertices, and edges are added using `addEdge` function. Then, DFS traversal is performed starting from vertex 0.

### 1. Algorithms & Data Structures (C++): Graphs Breadth First Search Traversal vs Depth First Search Traversal

Breadth First Search (BFS) and Depth First Search (DFS) are two fundamental algorithms for traversing graphs, each with its own advantages and use cases.

#### Breadth First Search (BFS)

1. **Order of traversal**: BFS traverses level by level, exploring all the vertices at the current depth before moving to the vertices at the next depth.
  
2. **Data Structure Used**: Typically, BFS uses a queue to keep track of vertices to visit next.
  
3. **Shortest Paths**: BFS is particularly useful for finding shortest paths in unweighted graphs because it explores all the neighbors of a vertex before moving to the next level.

4. **Memory Consumption**: It generally consumes more memory compared to DFS because it needs to keep track of all the vertices at the current level before moving to the next level.

5. **Applications**: BFS is often used in applications where the shortest path is required, like finding the shortest path in a maze, network routing, etc.

#### Depth First Search (DFS)

1. **Order of traversal**: DFS explores as far as possible along each branch before backtracking.
  
2. **Data Structure Used**: DFS typically uses a stack (or recursion, which utilizes the call stack) to keep track of vertices to visit next.
  
3. **Memory Consumption**: DFS generally consumes less memory compared to BFS because it only needs to keep track of the vertices along the current path from the root to the current vertex.
  
4. **Completeness**: DFS might not necessarily find the shortest path, but it's useful for many other tasks like topological sorting, cycle detection, etc.
  
5. **Applications**: DFS is often used in applications where we need to explore as far as possible along each branch, such as solving puzzles, maze generation, graph coloring, etc.

#### Choosing Between BFS and DFS

1. **Shortest Path**: If you need to find the shortest path in an unweighted graph, BFS is the better choice.
  
2. **Memory Usage**: If memory usage is a concern and the shortest path is not the primary objective, DFS might be preferred due to its lower memory consumption.
  
3. **Cycle Detection**: DFS is commonly used for cycle detection in graphs.
  
4. **Traversal Order**: Depending on the problem requirements, the order of traversal offered by BFS or DFS might be advantageous or disadvantageous.

In C++, you can implement both BFS and DFS using either iterative or recursive approaches, depending on the specific requirements of your problem and preferences for implementation style.

### 1. Algorithms & Data Structures (C++): Graphs Depth First Search Traversal

Depth First Search (DFS) is a fundamental graph traversal algorithm used to explore nodes and edges of a graph in a depthward motion. In C++, you can implement DFS using various data structures such as adjacency lists or adjacency matrices. Here's a basic implementation using adjacency lists:

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

// Graph class representing a graph using adjacency list
class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V), adj(V) {}

    // Function to add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w); // Add w to v's list
    }

    // Depth First Search traversal from a given source vertex
    void DFS(int v) {
        // Mark all vertices as not visited
        vector<bool> visited(V, false);

        // Create a stack for DFS
        stack<int> stack;

        // Push the current source node
        stack.push(v);

        while (!stack.empty()) {
            // Pop a vertex from stack and print it
            v = stack.top();
            stack.pop();

            // Stack may contain same vertex twice. So, 
            // we need to print the popped item only
            // if it is not visited.
            if (!visited[v]) {
                cout << v << " ";
                visited[v] = true;
            }

            // Get all adjacent vertices of the popped vertex v
            // If an adjacent has not been visited, then push it
            // to the stack.
            for (auto it = adj[v].begin(); it != adj[v].end(); ++it) {
                if (!visited[*it])
                    stack.push(*it);
            }
        }
    }
};

int main() {
    // Create a graph given in the above diagram
    Graph g(5);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(2, 4);

    cout << "Depth First Traversal (starting from vertex 0): ";
    g.DFS(0);

    return 0;
}
```

This code demonstrates how to implement DFS on a graph represented using adjacency lists. You can create a `Graph` object, add edges using the `addEdge` function, and then perform DFS from a starting vertex using the `DFS` function.

### 1. Algorithms & Data Structures (C++): Graphs Representation - Summary of Performance

When it comes to representing graphs in C++, the choice of data structure can significantly impact the performance of graph algorithms. Here's a summary of some common graph representations and their performance characteristics:

1. **Adjacency Matrix**:
   - **Description**: A 2D array (matrix) where the entry `matrix[i][j]` represents the edge weight between vertices `i` and `j`, or presence of an edge if unweighted.
   - **Pros**:
     - Simple and intuitive representation.
     - Constant time (`O(1)`) access to check if there is an edge between two vertices.
   - **Cons**:
     - Space inefficient for sparse graphs (graphs with fewer edges).
     - Consumes `O(V^2)` space where `V` is the number of vertices.
     - Adding or removing vertices is expensive (`O(V^2)`).

2. **Adjacency List**:
   - **Description**: An array of lists, where each element in the array represents a vertex, and the list associated with it contains its adjacent vertices.
   - **Pros**:
     - Space efficient for sparse graphs.
     - Memory consumption scales with the number of edges (`O(V + E)` where `E` is the number of edges).
     - Adding or removing vertices is relatively cheap (`O(1)`).
   - **Cons**:
     - Less efficient for dense graphs.
     - Accessing whether there's an edge between two vertices may take `O(V)` time in worst-case scenarios.

3. **Edge List**:
   - **Description**: A simple list of edges, where each edge is represented as a pair of vertices (or a tuple with additional information like weight).
   - **Pros**:
     - Very space efficient for sparse graphs.
     - Well-suited for algorithms where edge iteration is important.
   - **Cons**:
     - Checking for the existence of a specific edge may require searching through the list (`O(E)` time).
     - Not suitable for operations that require adjacency information of vertices.

4. **Sparse Matrices**:
   - **Description**: A variation of the adjacency matrix where space is saved by using techniques like compressed sparse row (CSR) or compressed sparse column (CSC).
   - **Pros**:
     - Space efficient for graphs with fewer edges.
     - Allows for `O(1)` access to neighbors of a vertex.
   - **Cons**:
     - Complexity in implementation compared to traditional adjacency matrix.
     - Some operations may still be `O(V^2)` in worst-case scenarios.

5. **Hash Map of Sets**:
   - **Description**: A hash map where the keys are vertices, and the associated values are sets containing the adjacent vertices.
   - **Pros**:
     - Efficient for both adding and removing vertices and edges.
     - Flexible and adaptable to different graph structures.
   - **Cons**:
     - Slightly less memory efficient compared to adjacency list for simple graphs.
     - Hash map overhead and collision resolution might introduce some performance overhead.

Choosing the right representation depends on the specific characteristics of the graph and the operations you intend to perform on it. For sparse graphs, adjacency lists or sparse matrices are generally preferred, while for dense graphs, adjacency matrices may be more suitable.

### 1. Algorithms & Data Structures (C++): Graphs Representations

In C++, graphs can be represented using various data structures. Here are some common representations:

1. **Adjacency Matrix**:
   In this representation, a 2D array (matrix) is used where the rows and columns represent vertices, and the value at matrix[i][j] indicates whether there is an edge between vertex i and vertex j. This representation is efficient for dense graphs but may waste space for sparse graphs.

   ```cpp
   const int MAX_VERTICES = 100;
   bool adjacencyMatrix[MAX_VERTICES][MAX_VERTICES];
   ```

2. **Adjacency List**:
   In this representation, each vertex has a list of its adjacent vertices. This can be implemented using an array of lists, or using a vector of vectors if the number of vertices is not fixed. This representation is efficient for sparse graphs.

   ```cpp
   #include <vector>
   using namespace std;

   const int MAX_VERTICES = 100;
   vector<int> adjacencyList[MAX_VERTICES];
   ```

3. **Edge List**:
   In this representation, you store a list of edges. Each edge is represented as a pair of vertices (or vertex indices) indicating the two endpoints of the edge, optionally with weights.

   ```cpp
   #include <vector>
   using namespace std;

   struct Edge {
       int src, dest, weight;
   };

   const int MAX_EDGES = 100;
   vector<Edge> edgeList;
   ```

4. **Adjacency Matrix (Weighted)**:
   Similar to the adjacency matrix representation, but instead of storing a boolean value, it stores the weight of the edge between vertices.

   ```cpp
   const int MAX_VERTICES = 100;
   int adjacencyMatrix[MAX_VERTICES][MAX_VERTICES];
   ```

5. **Adjacency List (Weighted)**:
   Similar to the adjacency list representation, but each edge is associated with a weight.

   ```cpp
   #include <vector>
   using namespace std;

   struct Edge {
       int dest, weight;
   };

   const int MAX_VERTICES = 100;
   vector<Edge> adjacencyList[MAX_VERTICES];
   ```

Choose the representation based on the characteristics of your graph (e.g., density, sparsity, weighted or unweighted edges) and the operations you need to perform efficiently (e.g., traversal, edge insertion/deletion, etc.).

### 1. Algorithms & Data Structures (C++): Graphs Section Graphs 10 Cool Applications

Graphs are incredibly versatile data structures with numerous applications across various domains. Here are 10 cool applications of graphs:

1. **Social Networks**: Social media platforms like Facebook, Twitter, and LinkedIn use graphs to represent connections between users. Graph algorithms help in suggesting friends, finding communities, and detecting influential users.

2. **Navigation Systems**: Applications like Google Maps utilize graphs to represent roads and intersections. Algorithms like Dijkstra's or A* are used to find the shortest path between locations.

3. **Recommendation Systems**: Graphs are used to model relationships between users and items in recommendation systems. Algorithms analyze these relationships to make personalized recommendations, as seen in platforms like Netflix or Amazon.

4. **Network Routing**: In telecommunications and computer networks, graphs model connections between devices. Routing algorithms find optimal paths for data packets to travel through the network.

5. **Genetics and Bioinformatics**: Graphs represent biological data such as protein interactions, genetic sequences, or evolutionary relationships between species. Graph algorithms help analyze and interpret this data for various biological studies.

6. **Epidemiology**: Graphs are used to model the spread of diseases within populations. Epidemic models utilize graph algorithms to simulate and predict the spread of diseases, aiding in public health decision-making.

7. **Recommendation Systems**: Graphs are used to model relationships between users and items in recommendation systems. Algorithms analyze these relationships to make personalized recommendations, as seen in platforms like Netflix or Amazon.

8. **Fraud Detection**: Financial institutions use graphs to model transactions between accounts. Graph algorithms help detect patterns indicative of fraudulent activities, such as money laundering or identity theft.

9. **Semantic Web**: Graphs represent semantic relationships between entities on the web. Technologies like RDF (Resource Description Framework) use graphs to enable semantic searching and reasoning on web data.

10. **Computer Graphics**: Graphs represent geometric data in computer graphics applications. Graph algorithms are used in tasks like rendering, collision detection, and animation.

These are just a few examples showcasing the versatility and significance of graphs in various fields. The combination of graph theory and algorithms has led to advancements in diverse domains, making them essential tools for problem-solving in modern technology and science.

### 1. Algorithms & Data Structures (C++): Graphs Types Of Graphs

Graphs are a fundamental data structure in computer science and are used to represent connections or relationships between pairs of objects. There are several types of graphs, each with unique properties and applications. In C++, these graphs can be implemented using various data structures such as adjacency matrix, adjacency list, or an edge list.

Here are some common types of graphs:

1. **Undirected Graph**: In an undirected graph, edges have no direction. If there is an edge between vertex A and vertex B, you can traverse it in both directions. Undirected graphs are often used to represent symmetric relationships.

2. **Directed Graph (Digraph)**: In a directed graph, edges have a direction. If there is an edge from vertex A to vertex B, you can traverse it only from A to B, not vice versa. Directed graphs are useful for representing asymmetric relationships, such as roads with one-way traffic.

3. **Weighted Graph**: Both undirected and directed graphs can be weighted, meaning each edge has a numerical value associated with it, called a weight. These weights can represent distances, costs, or any other relevant metric. Weighted graphs are used in applications where the strength of connections matters.

4. **Unweighted Graph**: In contrast to weighted graphs, unweighted graphs do not have weights associated with their edges. They are simpler and used when the presence of a connection is more important than its weight.

5. **Cyclic Graph**: A cyclic graph contains at least one cycle, meaning there is a path that starts and ends at the same vertex. Cyclic graphs are common in many real-world scenarios but can sometimes lead to issues in algorithms that assume acyclic graphs.

6. **Acyclic Graph**: An acyclic graph is a graph with no cycles. Directed acyclic graphs (DAGs) are particularly important and find applications in various algorithms like topological sorting and shortest path algorithms (e.g., DAG shortest paths).

7. **Connected Graph**: A graph is connected if there is a path between every pair of vertices. In an undirected graph, this means there are no isolated vertices. In a directed graph, it implies that there is a directed path between every pair of vertices.

8. **Disconnected Graph**: A graph is disconnected if it is composed of two or more connected components, meaning there are one or more pairs of vertices with no path between them.

9. **Bipartite Graph**: A bipartite graph is one whose vertices can be divided into two disjoint sets such that no two vertices within the same set are adjacent. Bipartite graphs find applications in matching problems and modeling certain types of relationships.

10. **Complete Graph**: In a complete graph, every pair of distinct vertices is connected by a unique edge. A complete graph with n vertices has n*(n-1)/2 edges in the case of undirected graphs and n*(n-1) edges in the case of directed graphs.

These are some of the most common types of graphs, each with its own set of properties and applications in various domains of computer science and beyond.

### 1. Algorithms & Data Structures (C++): Graphs: Add Edge

Adding an edge to a graph in C++ can be done using various data structures such as adjacency lists or adjacency matrices. Here's how you can add an edge to a graph using an adjacency list representation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to add an edge to an undirected graph
void addEdge(vector<vector<int>>& adj, int u, int v) {
    adj[u].push_back(v); // Add v to u's list
    adj[v].push_back(u); // Add u to v's list
}

int main() {
    int V = 5; // Number of vertices
    vector<vector<int>> adj(V); // Adjacency list representation

    // Adding edges
    addEdge(adj, 0, 1);
    addEdge(adj, 0, 4);
    addEdge(adj, 1, 2);
    addEdge(adj, 1, 3);
    addEdge(adj, 1, 4);
    addEdge(adj, 2, 3);
    addEdge(adj, 3, 4);

    // Print the adjacency list
    for (int i = 0; i < V; ++i) {
        cout << "Adjacency list of vertex " << i << ": ";
        for (int j = 0; j < adj[i].size(); ++j) {
            cout << adj[i][j] << " ";
        }
        cout << endl;
    }

    return 0;
}
```

This code represents an undirected graph using an adjacency list. The `addEdge` function adds an edge between vertices `u` and `v` by pushing `v` to the adjacency list of `u` and pushing `u` to the adjacency list of `v`. You can modify the code for a directed graph or for other representations like adjacency matrices if needed.

### 1. Algorithms & Data Structures (C++): Graphs: Adjacency List Representation

In C++, representing a graph using an adjacency list is quite efficient, especially for sparse graphs where there aren't many edges. Here's a basic implementation:

```cpp
#include <iostream>
#include <vector>
using namespace std;

// Structure to represent an edge
struct Edge {
    int destination;
    int weight;
};

// Class to represent a graph using adjacency list
class Graph {
private:
    int V; // Number of vertices
    vector<vector<Edge>> adjList; // Adjacency list
    
public:
    // Constructor
    Graph(int vertices) {
        V = vertices;
        adjList.resize(V);
    }
    
    // Function to add an edge to the graph
    void addEdge(int source, int destination, int weight = 1) {
        Edge edge = {destination, weight};
        adjList[source].push_back(edge);
    }
    
    // Function to print the adjacency list representation of the graph
    void printGraph() {
        for (int i = 0; i < V; ++i) {
            cout << "Vertex " << i << " :";
            for (auto& edge : adjList[i]) {
                cout << " -> " << edge.destination << " (Weight: " << edge.weight << ")";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph graph(5);
    
    // Add some edges
    graph.addEdge(0, 1, 10);
    graph.addEdge(0, 4, 5);
    graph.addEdge(1, 2, 6);
    graph.addEdge(1, 3, 15);
    graph.addEdge(2, 3, 4);
    graph.addEdge(4, 3, 2);
    
    // Print the adjacency list representation of the graph
    graph.printGraph();
    
    return 0;
}
```

This code defines a `Graph` class with member functions to add edges and print the adjacency list. It also defines a `Edge` struct to represent an edge in the graph. In the `main()` function, we create a graph with 5 vertices and add some edges to it. Finally, we print the adjacency list representation of the graph.

This implementation can be extended further to include additional functionality like removing edges, finding if there's an edge between two vertices, etc., based on your requirements.

### 1. Algorithms & Data Structures (C++): Graphs: Adjacency Matrix Representation

In C++, representing a graph using an adjacency matrix is straightforward. An adjacency matrix is a 2D array where each cell `matrix[i][j]` represents whether there is an edge from vertex `i` to vertex `j`. If the graph is unweighted, the cell value can be a binary indicator (0 or 1), representing absence or presence of an edge respectively. For weighted graphs, the cell can contain the weight of the edge.

Here's a basic implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
private:
    int numVertices;
    vector<vector<int>> adjMatrix;

public:
    Graph(int numVertices) {
        this->numVertices = numVertices;
        adjMatrix.resize(numVertices, vector<int>(numVertices, 0));
    }

    void addEdge(int src, int dest, int weight = 1) {
        // Assuming the graph is undirected
        adjMatrix[src][dest] = weight;
        adjMatrix[dest][src] = weight;
    }

    void printAdjMatrix() {
        cout << "Adjacency Matrix:" << endl;
        for (int i = 0; i < numVertices; ++i) {
            for (int j = 0; j < numVertices; ++j) {
                cout << adjMatrix[i][j] << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 4 vertices
    Graph graph(4);

    // Add edges
    graph.addEdge(0, 1);
    graph.addEdge(0, 2);
    graph.addEdge(1, 2);
    graph.addEdge(2, 3);

    // Print adjacency matrix
    graph.printAdjMatrix();

    return 0;
}
```

This code creates a simple undirected graph with 4 vertices and adds some edges between them. The adjacency matrix is then printed out. You can modify it to suit your specific requirements, like adding weighted edges or directed edges.

### 1. Algorithms & Data Structures (C++): Graphs: Breadth First Search (Breadth First Search)

Breadth First Search (BFS) is a fundamental graph traversal algorithm that explores the vertices of a graph level by level. It starts at a specified vertex (often called the "source" vertex) and systematically explores all the vertices that are reachable from that source vertex. BFS is often used to find the shortest path from a source vertex to all other vertices in an unweighted graph.

Here's a simple implementation of BFS in C++ using an adjacency list representation for the graph:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

// Graph class using adjacency list representation
class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V), adj(V) {}

    // Function to add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w);
    }

    // Function to perform Breadth First Search traversal
    void BFS(int s) {
        // Mark all vertices as not visited
        vector<bool> visited(V, false);

        // Create a queue for BFS
        queue<int> queue;

        // Mark the current node as visited and enqueue it
        visited[s] = true;
        queue.push(s);

        while (!queue.empty()) {
            // Dequeue a vertex from queue and print it
            int v = queue.front();
            cout << v << " ";
            queue.pop();

            // Get all adjacent vertices of the dequeued vertex v
            // If an adjacent has not been visited, mark it visited and enqueue it
            for (int& neighbor : adj[v]) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.push(neighbor);
                }
            }
        }
    }
};

int main() {
    // Create a graph
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "Breadth First Traversal (starting from vertex 2): ";
    g.BFS(2);

    return 0;
}
```

In this implementation:

- The `Graph` class represents an undirected graph using an adjacency list.
- The `addEdge` function adds an edge between two vertices.
- The `BFS` function performs the Breadth First Search traversal starting from a specified source vertex `s`.
- Inside the `BFS` function, a queue is used to keep track of vertices to be visited next.
- The `visited` vector is used to mark vertices that have been visited to prevent revisiting them.
- The BFS traversal starts from the source vertex, marking it as visited and enqueuing it. Then, it continues to dequeue vertices from the queue, visiting their adjacent vertices and enqueuing them if they haven't been visited yet.

You can modify this code according to your requirements and the specific graph representation you are using.

### 1. Algorithms & Data Structures (C++): Graphs: Edge List Representation

In C++, the edge list representation is one of the simplest ways to represent a graph. In this representation, you store all the edges of the graph in a list (or vector) of pairs. Each pair represents an edge, where the first element is the source vertex and the second element is the destination vertex.

Here's a basic implementation of an undirected graph using the edge list representation:

```cpp
#include <iostream>
#include <vector>
#include <utility> // for pair

using namespace std;

class Graph {
private:
    int V; // number of vertices
    vector<pair<int, int>> edges; // list of edges

public:
    Graph(int vertices) : V(vertices) {}

    // Function to add an edge to the graph
    void addEdge(int u, int v) {
        edges.push_back(make_pair(u, v)); // Adding the edge (u, v)
        edges.push_back(make_pair(v, u)); // Adding the corresponding edge (v, u) for an undirected graph
    }

    // Function to print the graph
    void printGraph() {
        cout << "Edge List Representation:\n";
        for (const auto& edge : edges) {
            cout << edge.first << " -- " << edge.second << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph graph(5);

    // Add edges to the graph
    graph.addEdge(0, 1);
    graph.addEdge(0, 4);
    graph.addEdge(1, 2);
    graph.addEdge(1, 3);
    graph.addEdge(1, 4);
    graph.addEdge(2, 3);
    graph.addEdge(3, 4);

    // Print the graph
    graph.printGraph();

    return 0;
}
```

In this implementation:

- The `Graph` class maintains the number of vertices `V` and a vector of pairs `edges` to store the edges.
- The `addEdge` function is used to add an edge to the graph. Since it's an undirected graph, for every edge `(u, v)`, we add `(u, v)` as well as `(v, u)` to the edge list.
- The `printGraph` function simply prints all the edges stored in the edge list.

This is a basic implementation of the edge list representation. It's simple and easy to understand, but it's not the most efficient for certain graph operations like checking if an edge exists or finding all neighbors of a vertex. Other representations like adjacency list or adjacency matrix may be more efficient for such operations depending on the specific requirements of your application.

### 1. Algorithms & Data Structures (C++): Graphs: Exercise: Check Balanced - LeetCode 110

LeetCode problem 110, "Check Balanced", is a classic problem in graph theory and can be solved using depth-first search (DFS). The problem asks you to determine whether a given undirected graph is a tree. A tree is a connected graph with no cycles.

Here's the general approach to solve this problem:

1. **Check for Cycle**: Use DFS to traverse the graph. While traversing, keep track of visited vertices and parent of each vertex. If you encounter a vertex that is already visited and it's not the parent of the current vertex, then there exists a cycle in the graph, and it cannot be a tree.

2. **Check for Connectivity**: After DFS traversal, check if all vertices are visited. If not, the graph is not connected, and hence not a tree.

3. **Final Check**: If the graph passes the above two conditions, it is a tree.

Here's a sample implementation in C++:

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>

using namespace std;

class Graph {
    vector<vector<int>> adj;

public:
    Graph(int n) : adj(n) {}

    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u);
    }

    bool isCyclicUtil(int v, vector<bool>& visited, int parent) {
        visited[v] = true;
        for (int u : adj[v]) {
            if (!visited[u]) {
                if (isCyclicUtil(u, visited, v))
                    return true;
            } else if (u != parent) {
                return true;
            }
        }
        return false;
    }

    bool isCyclic() {
        vector<bool> visited(adj.size(), false);
        for (int i = 0; i < adj.size(); ++i) {
            if (!visited[i] && isCyclicUtil(i, visited, -1))
                return true;
        }
        return false;
    }

    bool isConnected() {
        vector<bool> visited(adj.size(), false);
        dfs(0, visited);
        for (bool v : visited) {
            if (!v) return false; // Not all vertices are reachable
        }
        return true;
    }

    void dfs(int v, vector<bool>& visited) {
        visited[v] = true;
        for (int u : adj[v]) {
            if (!visited[u]) {
                dfs(u, visited);
            }
        }
    }
};

bool isValidTree(int n, vector<vector<int>>& edges) {
    if (edges.size() != n - 1) return false; // Necessary condition for a tree
    Graph graph(n);
    for (auto& edge : edges) {
        graph.addEdge(edge[0], edge[1]);
    }
    if (graph.isCyclic()) return false;
    if (!graph.isConnected()) return false;
    return true;
}

int main() {
    int n = 5;
    vector<vector<int>> edges = {{0, 1}, {0, 2}, {0, 3}, {1, 4}};
    cout << (isValidTree(n, edges) ? "Valid Tree" : "Not a Valid Tree") << endl;
    return 0;
}
```

This implementation checks whether the given graph is a valid tree or not. The `isValidTree` function returns true if the graph is a valid tree, otherwise false.

### 1. Algorithms & Data Structures (C++): Graphs: Exercise: First Common Ancestor - LeetCode 236

The problem you're referring to, LeetCode problem 236, is a classic algorithmic problem involving binary trees, not graphs. The problem is commonly known as "Lowest Common Ancestor (LCA) of a Binary Tree."

Here's the problem statement:

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

The definition of the LCA is the lowest node in the tree that has both `p` and `q` as descendants (where we allow a node to be a descendant of itself).

To solve this problem, you can use various approaches such as recursive DFS (Depth-First Search), iterative DFS, or even BFS (Breadth-First Search).

Here's a general outline of how you can solve this problem recursively:

1. Start from the root of the binary tree.
2. If the root is null or equal to either `p` or `q`, return the root.
3. Recursively search for `p` and `q` in the left and right subtrees.
4. If both `p` and `q` are found in different subtrees, return the current root as the LCA.
5. If only one of `p` or `q` is found, return that node as a potential ancestor for further search.
6. If neither `p` nor `q` is found, return null.

Here's a simple recursive C++ implementation:

```cpp
#include <iostream>

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (!root || root == p || root == q)
            return root;

        TreeNode* left = lowestCommonAncestor(root->left, p, q);
        TreeNode* right = lowestCommonAncestor(root->right, p, q);

        if (left && right) // If both p and q are found in different subtrees
            return root;
        else if (left) // If only p or q is found in the left subtree
            return left;
        else if (right) // If only p or q is found in the right subtree
            return right;
        else // If neither p nor q is found
            return nullptr;
    }
};

int main() {
    // Example usage
    Solution solution;
    TreeNode* root = new TreeNode(3);
    root->left = new TreeNode(5);
    root->right = new TreeNode(1);
    root->left->left = new TreeNode(6);
    root->left->right = new TreeNode(2);
    root->left->right->left = new TreeNode(7);
    root->left->right->right = new TreeNode(4);
    root->right->left = new TreeNode(0);
    root->right->right = new TreeNode(8);

    TreeNode* p = root->left;
    TreeNode* q = root->right;

    TreeNode* lca = solution.lowestCommonAncestor(root, p, q);
    if (lca)
        std::cout << "Lowest Common Ancestor: " << lca->val << std::endl;
    else
        std::cout << "No common ancestor found." << std::endl;

    // Don't forget to free the memory allocated for the tree nodes
    return 0;
}
```

This implementation will find the lowest common ancestor of the given two nodes `p` and `q` in the binary tree.

### 1. Algorithms & Data Structures (C++): Graphs: Exercise: List of Depths

The "List of Depths" problem is a classic graph traversal problem, often encountered in technical interviews or as an exercise in algorithms and data structures courses. The task is to create a linked list of all the nodes at each depth of a binary tree. Here's a basic outline of how you might approach this problem:

1. **Define Node Structure**: Define a structure for a binary tree node. Each node should contain data, a pointer to the left child, and a pointer to the right child.

2. **Breadth-First Search (BFS)**: Implement a BFS traversal of the binary tree. BFS is typically used for this problem because it naturally explores nodes level by level, which is what we need for creating the list of depths.

3. **List of Lists**: While performing BFS, keep track of the depth of each node. As you encounter nodes at each depth, add them to a linked list specific to that depth.

4. **Return List of Lists**: Once BFS is complete, you will have a list of linked lists, where each linked list contains nodes at a particular depth. Return this list of lists as the result.

Here's a simple pseudocode to illustrate this approach:

```plaintext
listOfDepths(root):
    if root is null:
        return null
        
    queue = new Queue
    enqueue(root)
    depthList = new List of Lists
    
    while queue is not empty:
        depthNodes = new List
        size = queue.size()
        for i from 1 to size:
            node = dequeue()
            depthNodes.add(node)
            if node.left is not null:
                queue.enqueue(node.left)
            if node.right is not null:
                queue.enqueue(node.right)
        depthList.add(depthNodes)
    
    return depthList
```

This pseudocode assumes a binary tree represented using nodes with left and right pointers. You can implement this in C++ by defining a `Node` structure and using a queue for BFS traversal. Then, you create a list of linked lists, with each linked list containing nodes at a specific depth.

Remember to handle the edge cases, such as when the root is null or when the tree has only one node. Additionally, make sure to properly deallocate memory to avoid memory leaks.

### 1. Algorithms & Data Structures (C++): Graphs: Exercise: Minimal Tree

Certainly! The exercise "Minimal Tree" typically involves constructing a binary search tree from a sorted array with minimal height. Here's a general approach in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

TreeNode* minimalTree(const vector<int>& sortedArray, int start, int end) {
    if (start > end) {
        return nullptr;
    }
    
    int mid = (start + end) / 2;
    TreeNode* root = new TreeNode(sortedArray[mid]);
    
    root->left = minimalTree(sortedArray, start, mid - 1);
    root->right = minimalTree(sortedArray, mid + 1, end);
    
    return root;
}

TreeNode* minimalTree(const vector<int>& sortedArray) {
    return minimalTree(sortedArray, 0, sortedArray.size() - 1);
}

// Function to print inorder traversal of the tree (for testing)
void inorderTraversal(TreeNode* root) {
    if (root == nullptr) {
        return;
    }
    
    inorderTraversal(root->left);
    cout << root->val << " ";
    inorderTraversal(root->right);
}

int main() {
    vector<int> sortedArray = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    TreeNode* root = minimalTree(sortedArray);
    
    // Print inorder traversal of the tree (to verify)
    inorderTraversal(root);
    
    // Don't forget to free the memory to avoid memory leaks
    // Implementation of freeing memory is left out for simplicity
    
    return 0;
}
```

This code defines a struct `TreeNode` for the binary tree nodes and provides a function `minimalTree` to construct the minimal binary search tree from a sorted array. The `main` function demonstrates how to use this function with a sorted array of integers. You can add more functionality or modify it according to your requirements.

### 1. Algorithms & Data Structures (C++): Graphs: Exercise: Route Between Nodes

Sure, I'd be happy to help with that! The "Route Between Nodes" problem is a classic graph traversal problem. The goal is to determine whether there is a path between two given nodes in a graph.

Here's a basic approach using breadth-first search (BFS) algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V) {
        adj.resize(V);
    }

    // Function to add an edge between two vertices
    void addEdge(int u, int v) {
        adj[u].push_back(v);
    }

    // Function to check if there is a path between two nodes using BFS
    bool isRoute(int start, int end) {
        if (start == end)
            return true;

        vector<bool> visited(V, false);
        queue<int> q;

        visited[start] = true;
        q.push(start);

        while (!q.empty()) {
            int u = q.front();
            q.pop();

            for (int v : adj[u]) {
                if (v == end)
                    return true;

                if (!visited[v]) {
                    visited[v] = true;
                    q.push(v);
                }
            }
        }

        return false;
    }
};

int main() {
    // Create a graph
    Graph g(6);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(2, 4);
    g.addEdge(3, 5);
    g.addEdge(4, 5);

    int start = 0, end = 5;
    if (g.isRoute(start, end))
        cout << "There is a route between " << start << " and " << end << endl;
    else
        cout << "There is no route between " << start << " and " << end << endl;

    return 0;
}
```

This code creates a graph using an adjacency list representation and then checks whether there is a route between two given nodes (start and end) using BFS traversal. If there is a route, it prints that there is a route; otherwise, it prints that there is no route.

You can modify the `main` function to test the code with different graph structures and node pairs.

### 1. Algorithms & Data Structures (C++): Graphs: Graphs - Degree of a Vertex

In graph theory, the degree of a vertex in a graph is the number of edges incident to it. In a directed graph, there are two types of degrees: in-degree and out-degree. The in-degree of a vertex is the number of edges that terminate at the vertex, while the out-degree is the number of edges that originate from the vertex.

Here's how you can represent and calculate the degree of a vertex in C++ using an adjacency list representation for an undirected graph:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to calculate the degree of a vertex in an undirected graph
int degreeOfVertex(const vector<vector<int>>& graph, int vertex) {
    return graph[vertex].size();
}

int main() {
    // Example graph represented as an adjacency list
    vector<vector<int>> graph = {
        {1, 2},     // vertex 0 is connected to vertices 1 and 2
        {0, 2, 3},  // vertex 1 is connected to vertices 0, 2, and 3
        {0, 1, 3},  // vertex 2 is connected to vertices 0, 1, and 3
        {1, 2}      // vertex 3 is connected to vertices 1 and 2
    };

    int vertex = 1; // Vertex whose degree needs to be calculated

    // Calculate and print the degree of the vertex
    cout << "Degree of vertex " << vertex << ": " << degreeOfVertex(graph, vertex) << endl;

    return 0;
}
```

In this example, the `degreeOfVertex` function takes the adjacency list representation of the graph and the vertex whose degree needs to be calculated. It returns the degree of that vertex by simply returning the size of the vector corresponding to that vertex in the adjacency list.

You can extend this code to handle directed graphs by considering both in-degree and out-degree for each vertex separately.

### 1. Algorithms & Data Structures (C++): Graphs: Path and Cycle

In C++, you can implement algorithms for graphs using various data structures like adjacency lists or adjacency matrices. Here's a basic implementation for finding paths and cycles in a graph represented using an adjacency list:

```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) {
        this->V = V;
        adj.resize(V);
    }

    void addEdge(int u, int v) {
        adj[u].push_back(v);
        // For undirected graph, add the reverse edge too
        // adj[v].push_back(u);
    }

    bool isReachable(int src, int dest) {
        vector<bool> visited(V, false);
        queue<int> q;

        visited[src] = true;
        q.push(src);

        while (!q.empty()) {
            int u = q.front();
            q.pop();

            for (int v : adj[u]) {
                if (v == dest)
                    return true;
                if (!visited[v]) {
                    visited[v] = true;
                    q.push(v);
                }
            }
        }
        return false;
    }

    bool hasCycleUtil(int v, vector<bool>& visited, vector<bool>& recStack) {
        if (!visited[v]) {
            visited[v] = true;
            recStack[v] = true;

            for (int u : adj[v]) {
                if (!visited[u] && hasCycleUtil(u, visited, recStack))
                    return true;
                else if (recStack[u])
                    return true;
            }
        }
        recStack[v] = false; // Remove the vertex from recursion stack
        return false;
    }

    bool hasCycle() {
        vector<bool> visited(V, false);
        vector<bool> recStack(V, false);

        for (int i = 0; i < V; i++) {
            if (hasCycleUtil(i, visited, recStack))
                return true;
        }
        return false;
    }
};

int main() {
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "Graph has cycle? " << (g.hasCycle() ? "Yes" : "No") << endl;

    cout << "Path from 1 to 3? " << (g.isReachable(1, 3) ? "Yes" : "No") << endl;

    return 0;
}
```

This code provides basic functionalities like adding edges to the graph, checking if there is a path between two vertices, and checking if the graph contains a cycle. You can modify and extend it based on your requirements and the specific algorithms you want to implement.

### 1. Algorithms & Data Structures (C++): Graphs: Remove Edge

To remove an edge from a graph in C++, you typically need to iterate through the adjacency list representation (or any other representation you're using) of the graph and remove the edge from the corresponding adjacency lists of the two vertices involved in the edge. Here's a basic implementation of removing an edge from an undirected graph represented using an adjacency list:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) {
        this->V = V;
        adj.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u); // Assuming undirected graph
    }

    // Function to remove an edge from the graph
    void removeEdge(int u, int v) {
        // Finding the edge in the adjacency list of u and removing it
        for (auto it = adj[u].begin(); it != adj[u].end(); ++it) {
            if (*it == v) {
                adj[u].erase(it);
                break;
            }
        }

        // Finding the edge in the adjacency list of v and removing it
        for (auto it = adj[v].begin(); it != adj[v].end(); ++it) {
            if (*it == u) {
                adj[v].erase(it);
                break;
            }
        }
    }

    // Function to print the graph
    void printGraph() {
        for (int i = 0; i < V; ++i) {
            cout << "Adjacency list of vertex " << i << ": ";
            for (int j : adj[i])
                cout << j << " ";
            cout << endl;
        }
    }
};

int main() {
    // Create a graph
    Graph g(5);
    g.addEdge(0, 1);
    g.addEdge(0, 4);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 3);
    g.addEdge(3, 4);

    cout << "Original Graph:" << endl;
    g.printGraph();

    // Remove an edge
    g.removeEdge(1, 3);

    cout << "\nGraph after removing edge (1, 3):" << endl;
    g.printGraph();

    return 0;
}
```

This code demonstrates how to create a graph, add edges to it, remove an edge, and print the resulting graph. The `removeEdge` function removes the edge between vertices `u` and `v` by iterating through their respective adjacency lists and removing the corresponding edge.

### 1. Algorithms & Data Structures (C++): Graphs: Remove Vertex

Removing a vertex from a graph involves deleting the vertex itself along with any edges connected to it. Here's a basic outline in C++ using an adjacency list representation for an undirected graph:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V) {
        adj.resize(V);
    }

    // Function to add an edge between two vertices
    void addEdge(int v, int w) {
        adj[v].push_back(w);
        adj[w].push_back(v); // Assuming undirected graph
    }

    // Function to remove a vertex from the graph
    void removeVertex(int v) {
        // Remove vertex from adjacency lists of all other vertices
        for (int i = 0; i < V; ++i) {
            if (i != v) {
                auto it = find(adj[i].begin(), adj[i].end(), v);
                if (it != adj[i].end()) {
                    adj[i].erase(it);
                }
            }
        }
        
        // Clear the adjacency list of the removed vertex
        adj[v].clear();
    }

    // Function to print the adjacency list representation of the graph
    void printGraph() {
        for (int v = 0; v < V; ++v) {
            cout << "Adjacency list of vertex " << v << ": ";
            for (int i = 0; i < adj[v].size(); ++i) {
                cout << adj[v][i] << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    Graph g(5); // Create a graph with 5 vertices
    g.addEdge(0, 1);
    g.addEdge(0, 4);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 3);
    g.addEdge(3, 4);

    cout << "Original graph:" << endl;
    g.printGraph();

    // Remove vertex 2
    g.removeVertex(2);

    cout << "Graph after removing vertex 2:" << endl;
    g.printGraph();

    return 0;
}
```

This code defines a `Graph` class with methods to add an edge, remove a vertex, and print the graph. In the `removeVertex` method, it removes the vertex from the adjacency lists of all other vertices and then clears the adjacency list of the removed vertex. Finally, the `main` function demonstrates how to use the `Graph` class to create a graph, remove a vertex, and print the resulting graph.

### 1. Algorithms & Data Structures (C++): Graphs: Subgraphs and Connected Components

Subgraphs and connected components are fundamental concepts in graph theory and are essential in understanding the structure and properties of graphs. Let's break down each concept:

#### Subgraphs

A subgraph of a graph G is a graph whose vertices and edges are subsets of the vertices and edges of G. In other words, if you have a graph G = (V, E) and another graph H = (V', E') such that V' is a subset of V and E' is a subset of E, then H is a subgraph of G.

Subgraphs can be categorized based on the relationships between their vertices and edges:

1. **Induced Subgraph**: An induced subgraph of G is obtained by including all vertices and edges of G that belong to a subset of vertices. In other words, an induced subgraph is formed by taking a subset of vertices and including all edges between those vertices that exist in the original graph.
2. **Spanning Subgraph**: A spanning subgraph of G is a subgraph that contains all the vertices of G. In other words, it's a subgraph that covers every vertex in the original graph.

In C++, you can represent a graph and its subgraphs using various data structures like adjacency matrix, adjacency list, or edge list, and then implement algorithms to find and manipulate subgraphs accordingly.

#### Connected Components

A connected component of an undirected graph is a subgraph in which every pair of vertices is connected by a path, and it is connected to no additional vertices in the supergraph. In other words, within a connected component, there is a path between every pair of vertices, and there are no edges connecting vertices from the component to vertices outside the component.

Connected components partition the vertices of a graph into disjoint sets, where each set corresponds to a connected component. Any graph can be broken down into its connected components.

In C++, you can find connected components using algorithms like Depth-First Search (DFS) or Breadth-First Search (BFS). These algorithms traverse the graph, marking visited vertices and identifying connected components along the way.

Here's a brief outline of how you might implement connected components using DFS in C++:

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>

using namespace std;

// DFS function to explore connected components
void DFS(const vector<vector<int>>& graph, int vertex, unordered_set<int>& visited, vector<int>& component) {
    visited.insert(vertex);
    component.push_back(vertex);
    for (int neighbor : graph[vertex]) {
        if (visited.find(neighbor) == visited.end()) {
            DFS(graph, neighbor, visited, component);
        }
    }
}

// Function to find connected components in an undirected graph
vector<vector<int>> findConnectedComponents(const vector<vector<int>>& graph) {
    int n = graph.size();
    unordered_set<int> visited;
    vector<vector<int>> components;

    for (int i = 0; i < n; ++i) {
        if (visited.find(i) == visited.end()) {
            vector<int> component;
            DFS(graph, i, visited, component);
            components.push_back(component);
        }
    }

    return components;
}

int main() {
    // Example graph representation (adjacency list)
    vector<vector<int>> graph = {{1, 2}, {0, 2}, {0, 1}, {4}, {3}};

    // Finding connected components
    vector<vector<int>> connectedComponents = findConnectedComponents(graph);

    // Output connected components
    cout << "Connected Components:\n";
    for (const auto& component : connectedComponents) {
        for (int vertex : component) {
            cout << vertex << " ";
        }
        cout << endl;
    }

    return 0;
}
```

This code demonstrates finding connected components in an undirected graph using DFS. You can represent the graph using an adjacency list and then use DFS to traverse the graph and identify connected components.

### 1. Algorithms & Data Structures (C++): Hamiltonian Cycles

Hamiltonian cycles are paths in a graph that visit each vertex exactly once and return to the starting vertex. Finding Hamiltonian cycles is an NP-complete problem, meaning there's no known polynomial-time solution for it. However, you can use backtracking algorithms to efficiently find Hamiltonian cycles in small to moderate-sized graphs.

Here's a basic outline of how you could implement a backtracking algorithm in C++ to find Hamiltonian cycles:

```cpp
#include <iostream>
#include <vector>
using namespace std;

const int MAX_VERTICES = 10; // Adjust this based on your graph size

vector<int> graph[MAX_VERTICES];
int path[MAX_VERTICES];
bool visited[MAX_VERTICES];

bool isHamiltonian(int v, int n, int pos) {
    if (pos == n) {
        // Check if there's an edge from the last vertex to the first vertex
        if (graph[path[pos - 1]][path[0]])
            return true;
        else
            return false;
    }

    for (int i = 0; i < graph[v].size(); ++i) {
        int u = graph[v][i];

        if (!visited[u]) {
            visited[u] = true;
            path[pos] = u;

            if (isHamiltonian(u, n, pos + 1))
                return true;

            visited[u] = false;
            path[pos] = -1;
        }
    }

    return false;
}

void findHamiltonianCycle(int n) {
    for (int i = 0; i < n; ++i)
        path[i] = -1;

    path[0] = 0;
    visited[0] = true;

    if (!isHamiltonian(0, n, 1)) {
        cout << "No Hamiltonian cycle found!" << endl;
        return;
    }

    cout << "Hamiltonian cycle found: ";
    for (int i = 0; i < n; ++i)
        cout << path[i] << " ";
    cout << path[0] << endl;
}

int main() {
    int n, m;
    cout << "Enter the number of vertices and edges: ";
    cin >> n >> m;

    cout << "Enter the edges (u v):" << endl;
    for (int i = 0; i < m; ++i) {
        int u, v;
        cin >> u >> v;
        graph[u].push_back(v);
        graph[v].push_back(u); // Uncomment this line for undirected graphs
    }

    findHamiltonianCycle(n);

    return 0;
}
```

This code defines a simple backtracking algorithm to find a Hamiltonian cycle in a graph represented as an adjacency list. Make sure to adjust `MAX_VERTICES` according to your graph's maximum number of vertices.

### 1. Algorithms & Data Structures (C++): Implementation of Breadth First Search

Certainly! Here's a simple implementation of Breadth First Search (BFS) in C++:

```cpp
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

// Graph class representing an undirected graph using adjacency list
class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V), adj(V) {}

    // Function to add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w); // Add w to v's list
        adj[w].push_back(v); // Add v to w's list
    }

    // Breadth First Search from a given source vertex
    void BFS(int s) {
        // Mark all vertices as not visited
        vector<bool> visited(V, false);

        // Create a queue for BFS
        queue<int> queue;

        // Mark the current node as visited and enqueue it
        visited[s] = true;
        queue.push(s);

        while (!queue.empty()) {
            // Dequeue a vertex from queue and print it
            int v = queue.front();
            cout << v << " ";
            queue.pop();

            // Get all adjacent vertices of the dequeued vertex v
            // If an adjacent vertex has not been visited, then mark it visited
            // and enqueue it
            for (auto it = adj[v].begin(); it != adj[v].end(); ++it) {
                if (!visited[*it]) {
                    visited[*it] = true;
                    queue.push(*it);
                }
            }
        }
    }
};

int main() {
    // Create a graph given in the example
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 3);

    cout << "Breadth First Traversal starting from vertex 0: ";
    g.BFS(0);

    return 0;
}
```

This code demonstrates a basic implementation of BFS using adjacency lists to represent an undirected graph. You can modify the `main` function to create your own graph and call the `BFS` function with different starting vertices.

### 1. Algorithms & Data Structures (C++): Implementation Of Dijkstra's Algorithm

Sure, here's an implementation of Dijkstra's Algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <climits>

using namespace std;

#define INF INT_MAX

// Structure to represent a node in the graph
struct Node {
    int id;
    int distance;

    Node(int _id, int _distance) : id(_id), distance(_distance) {}

    bool operator<(const Node &other) const {
        return distance > other.distance; // Priority queue is a min-heap, so we use '>' here
    }
};

// Function to implement Dijkstra's Algorithm
void dijkstra(vector<vector<pair<int, int>>> &graph, int start, vector<int> &distances) {
    int n = graph.size();
    distances.assign(n, INF);
    distances[start] = 0;

    // Priority queue to store nodes based on minimum distance
    priority_queue<Node> pq;
    pq.push(Node(start, 0));

    while (!pq.empty()) {
        Node u = pq.top();
        pq.pop();

        // Visit each neighbor of u
        for (auto &[v, weight] : graph[u.id]) {
            // Relaxation step
            if (distances[u.id] + weight < distances[v]) {
                distances[v] = distances[u.id] + weight;
                pq.push(Node(v, distances[v]));
            }
        }
    }
}

int main() {
    int n, m; // n -> number of nodes, m -> number of edges
    cout << "Enter number of nodes and edges: ";
    cin >> n >> m;

    vector<vector<pair<int, int>>> graph(n); // Adjacency list representation of graph

    cout << "Enter edges and their weights:\n";
    for (int i = 0; i < m; ++i) {
        int u, v, weight;
        cin >> u >> v >> weight;
        graph[u].push_back({v, weight});
        graph[v].push_back({u, weight}); // Uncomment this line for undirected graph
    }

    int start;
    cout << "Enter the starting node: ";
    cin >> start;

    vector<int> distances; // Store the shortest distances from the start node
    dijkstra(graph, start, distances);

    cout << "Shortest distances from node " << start << ":\n";
    for (int i = 0; i < n; ++i) {
        cout << "Node " << i << ": ";
        if (distances[i] == INF)
            cout << "INF\n";
        else
            cout << distances[i] << endl;
    }

    return 0;
}
```

This code prompts the user to input the number of nodes and edges, then the edges and their weights, and finally the starting node. It then computes and outputs the shortest distances from the starting node to all other nodes in the graph using Dijkstra's Algorithm.

### 1. Algorithms & Data Structures (C++): Implementation of Kruskal's Algorithm

Sure, here's a basic implementation of Kruskal's Algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

struct Edge {
    int src, dest, weight;
};

class Graph {
    int V;
    vector<Edge> edges;

public:
    Graph(int v) : V(v) {}

    void addEdge(int src, int dest, int weight) {
        edges.push_back({src, dest, weight});
    }

    // Find operation of Disjoint Set
    int findParent(vector<int>& parent, int i) {
        if (parent[i] == -1)
            return i;
        return findParent(parent, parent[i]);
    }

    // Union operation of Disjoint Set
    void unionSet(vector<int>& parent, int x, int y) {
        int xSet = findParent(parent, x);
        int ySet = findParent(parent, y);
        parent[xSet] = ySet;
    }

    // Kruskal's Algorithm
    void kruskalMST() {
        vector<Edge> result;
        int e = 0; // index variable, used for result[]
        int i = 0; // index variable, used for sorted edges
        sort(edges.begin(), edges.end(), [](Edge a, Edge b) { return a.weight < b.weight; });

        vector<int> parent(V, -1);

        while (e < V - 1 && i < edges.size()) {
            Edge next_edge = edges[i++];
            int x = findParent(parent, next_edge.src);
            int y = findParent(parent, next_edge.dest);

            if (x != y) {
                result.push_back(next_edge);
                unionSet(parent, x, y);
                e++;
            }
        }

        cout << "Edges of MST are:\n";
        for (auto edge : result) {
            cout << edge.src << " -- " << edge.dest << " with weight " << edge.weight << endl;
        }
    }
};

int main() {
    int V = 4; // Number of vertices
    Graph graph(V);

    // Add edges
    graph.addEdge(0, 1, 10);
    graph.addEdge(0, 2, 6);
    graph.addEdge(0, 3, 5);
    graph.addEdge(1, 3, 15);
    graph.addEdge(2, 3, 4);

    // Find MST using Kruskal's Algorithm
    graph.kruskalMST();

    return 0;
}
```

This code defines a Graph class and an Edge struct. The main functions are `addEdge()` to add edges to the graph, `kruskalMST()` to find the Minimum Spanning Tree (MST) using Kruskal's Algorithm, `findParent()` and `unionSet()` for the Disjoint Set operations required for Kruskal's Algorithm. Finally, in the `main()` function, we create a sample graph, add some edges to it, and find the MST using Kruskal's Algorithm.

### 1. Algorithms & Data Structures (C++): Implementation Of Prim's Algorithm

Prim's algorithm is a greedy algorithm used to find the minimum spanning tree (MST) of a connected, undirected graph. Here's a simple implementation of Prim's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <utility>
#include <climits>

using namespace std;

// Define a structure to represent edges in the graph
struct Edge {
    int destination;
    int weight;
};

// Function to implement Prim's algorithm
void primMST(vector<vector<Edge>>& graph, int numVertices) {
    // Priority queue to store vertices that are candidates for the MST
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;

    // Vector to keep track of the parent of each vertex in the MST
    vector<int> parent(numVertices, -1);

    // Vector to keep track of the minimum weight of each vertex
    vector<int> key(numVertices, INT_MAX);

    // Vector to keep track of whether a vertex is included in MST or not
    vector<bool> inMST(numVertices, false);

    // Add the first vertex to the MST
    pq.push({0, 0}); // weight, vertex
    key[0] = 0;

    while (!pq.empty()) {
        int u = pq.top().second; // Extract vertex with minimum weight
        pq.pop();

        // Include u in MST
        inMST[u] = true;

        // Explore all adjacent vertices of u
        for (const auto& edge : graph[u]) {
            int v = edge.destination;
            int weight = edge.weight;

            // If v is not in MST and its weight is less than current key of v,
            // update key and parent, and add it to the priority queue
            if (!inMST[v] && weight < key[v]) {
                key[v] = weight;
                parent[v] = u;
                pq.push({key[v], v});
            }
        }
    }

    // Print the edges of the MST
    cout << "Edges of Minimum Spanning Tree:" << endl;
    for (int i = 1; i < numVertices; ++i) {
        cout << "Edge: " << parent[i] << " - " << i << ", Weight: " << key[i] << endl;
    }
}

int main() {
    // Example graph representation (adjacency list)
    int numVertices = 5;
    vector<vector<Edge>> graph(numVertices);

    // Add edges to the graph
    graph[0].push_back({1, 2});
    graph[1].push_back({0, 2});

    graph[0].push_back({2, 3});
    graph[2].push_back({0, 3});

    graph[1].push_back({2, 1});
    graph[2].push_back({1, 1});

    graph[1].push_back({3, 4});
    graph[3].push_back({1, 4});

    graph[1].push_back({4, 5});
    graph[4].push_back({1, 5});

    graph[2].push_back({3, 6});
    graph[3].push_back({2, 6});

    graph[3].push_back({4, 7});
    graph[4].push_back({3, 7});

    // Call Prim's algorithm function
    primMST(graph, numVertices);

    return 0;
}
```

This code includes a `struct Edge` to represent edges in the graph, a function `primMST` to implement Prim's algorithm, and a `main` function where you can define your graph and call `primMST` function. This implementation assumes that the graph is represented using an adjacency list.

### 1. Algorithms & Data Structures (C++): Implementation Of The Bellman Ford Algorithm

Sure, I can outline the implementation of the Bellman-Ford algorithm in C++. This algorithm is used to find the shortest paths from a single source vertex to all other vertices in a weighted graph, even if the graph contains negative weight edges (as long as there are no negative cycles).

Here's a simple implementation:

```cpp
#include <iostream>
#include <vector>
#include <limits>

using namespace std;

struct Edge {
    int source, destination, weight;
};

class Graph {
    int V, E;
    vector<Edge> edges;

public:
    Graph(int vertices, int edgesCount) : V(vertices), E(edgesCount) {}

    void addEdge(int source, int destination, int weight) {
        edges.push_back({source, destination, weight});
    }

    void BellmanFord(int source) {
        vector<int> distance(V, numeric_limits<int>::max());
        distance[source] = 0;

        // Relax all edges V-1 times
        for (int i = 1; i <= V - 1; ++i) {
            for (const auto& edge : edges) {
                int u = edge.source;
                int v = edge.destination;
                int w = edge.weight;
                if (distance[u] != numeric_limits<int>::max() && distance[u] + w < distance[v]) {
                    distance[v] = distance[u] + w;
                }
            }
        }

        // Check for negative weight cycles
        for (const auto& edge : edges) {
            int u = edge.source;
            int v = edge.destination;
            int w = edge.weight;
            if (distance[u] != numeric_limits<int>::max() && distance[u] + w < distance[v]) {
                cout << "Graph contains negative weight cycle" << endl;
                return;
            }
        }

        // Print the distances
        cout << "Vertex   Distance from Source" << endl;
        for (int i = 0; i < V; ++i) {
            cout << i << "\t\t" << distance[i] << endl;
        }
    }
};

int main() {
    int V, E;
    cout << "Enter the number of vertices and edges: ";
    cin >> V >> E;

    Graph graph(V, E);

    cout << "Enter the source, destination, and weight for each edge:" << endl;
    for (int i = 0; i < E; ++i) {
        int source, destination, weight;
        cin >> source >> destination >> weight;
        graph.addEdge(source, destination, weight);
    }

    int source;
    cout << "Enter the source vertex: ";
    cin >> source;

    graph.BellmanFord(source);

    return 0;
}
```

This code defines a `Graph` class with an `Edge` struct representing edges in the graph. The `addEdge` function is used to add edges to the graph. The `BellmanFord` function implements the Bellman-Ford algorithm to find the shortest paths from a given source vertex. Finally, in the `main` function, you can input the graph's details and the source vertex to find the shortest paths from that vertex to all other vertices.

### 1. Algorithms & Data Structures (C++): Implementation Of The Shortest Path In An Unweighted Graph

Implementing the shortest path algorithm for an unweighted graph in C++ can be done using breadth-first search (BFS). Here's a simple implementation:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

// Function to perform BFS and find the shortest path in an unweighted graph
vector<int> shortestPath(vector<vector<int>>& graph, int start, int n) {
    vector<bool> visited(n, false); // To keep track of visited nodes
    vector<int> distance(n, -1);    // To store distances from the start node
    queue<int> q;                   // Queue for BFS

    // Initialize starting node
    visited[start] = true;
    distance[start] = 0;
    q.push(start);

    // BFS traversal
    while (!q.empty()) {
        int u = q.front();
        q.pop();

        // Traverse adjacent nodes
        for (int v : graph[u]) {
            if (!visited[v]) {
                visited[v] = true;
                distance[v] = distance[u] + 1;
                q.push(v);
            }
        }
    }

    return distance;
}

int main() {
    int n, m; // Number of nodes and edges respectively
    cout << "Enter the number of nodes and edges: ";
    cin >> n >> m;

    vector<vector<int>> graph(n); // Adjacency list representation of the graph

    // Input the edges of the graph
    cout << "Enter the edges (node pairs):\n";
    for (int i = 0; i < m; ++i) {
        int u, v;
        cin >> u >> v;
        // Assuming the graph is undirected
        graph[u].push_back(v);
        graph[v].push_back(u);
    }

    int start; // Starting node for shortest path calculation
    cout << "Enter the starting node: ";
    cin >> start;

    // Finding the shortest path using BFS
    vector<int> distances = shortestPath(graph, start, n);

    // Output the shortest distances from the start node to all other nodes
    cout << "Shortest distances from node " << start << ":\n";
    for (int i = 0; i < n; ++i) {
        cout << "Node " << i << ": " << distances[i] << "\n";
    }

    return 0;
}
```

In this code:

- We represent the graph as an adjacency list.
- We perform BFS starting from the given start node.
- During BFS traversal, we keep track of the distance of each node from the start node.
- Finally, we output the shortest distances from the start node to all other nodes.

This implementation assumes an undirected graph. If you're dealing with a directed graph, you'll need to adjust the adjacency list accordingly.

### 1. Algorithms & Data Structures (C++): Implementing Graphs

Implementing graphs in C++ typically involves using either an adjacency matrix or an adjacency list representation. Here, I'll show you how to implement an undirected graph using an adjacency list representation.

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adjList; // Adjacency list

public:
    // Constructor
    Graph(int vertices) : V(vertices) {
        adjList.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int u, int v) {
        adjList[u].push_back(v);
        adjList[v].push_back(u); // For undirected graph
    }

    // Function to print the adjacency list representation of the graph
    void printGraph() {
        for (int i = 0; i < V; ++i) {
            cout << "Adjacency list of vertex " << i << ": ";
            for (int j = 0; j < adjList[i].size(); ++j) {
                cout << adjList[i][j] << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph graph(5);

    // Add some edges
    graph.addEdge(0, 1);
    graph.addEdge(0, 4);
    graph.addEdge(1, 2);
    graph.addEdge(1, 3);
    graph.addEdge(1, 4);
    graph.addEdge(2, 3);
    graph.addEdge(3, 4);

    // Print the adjacency list representation of the graph
    graph.printGraph();

    return 0;
}
```

This code defines a `Graph` class with a constructor to initialize the number of vertices and an adjacency list. It has methods to add edges and print the graph's adjacency list. In the `main()` function, a graph with 5 vertices is created, and some edges are added. Finally, the adjacency list representation of the graph is printed.

You can extend this implementation by adding methods for other graph operations such as BFS, DFS, shortest path algorithms, etc., based on your requirements.

### 1. Algorithms & Data Structures (C++): Kosaraju Algorithm

The Kosaraju Algorithm is a popular algorithm used to find strongly connected components (SCCs) in a directed graph. SCCs are subsets of vertices in a graph where every vertex is reachable from every other vertex in that subset. Kosaraju's algorithm efficiently finds these SCCs. Here's a brief explanation of how it works:

1. **Step 1: Depth-First Search (DFS) to create a stack:** Perform a DFS traversal of the graph and push vertices onto a stack in the order in which they finish exploring, i.e., in the order of their finishing times.

2. **Step 2: Transpose the Graph:** Create a transpose of the original graph by reversing all the edges.

3. **Step 3: DFS on the Transposed Graph:** Pop vertices from the stack one by one and perform DFS on the transposed graph. Each DFS traversal from a vertex in the stack will give one strongly connected component.

Here's a basic implementation of Kosaraju's Algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <stack>
#include <algorithm>

using namespace std;

void dfs(int v, vector<bool>& visited, vector<vector<int>>& graph, stack<int>& Stack) {
    visited[v] = true;
    for (int u : graph[v]) {
        if (!visited[u]) {
            dfs(u, visited, graph, Stack);
        }
    }
    Stack.push(v);
}

void dfsTranspose(int v, vector<bool>& visited, vector<vector<int>>& transposeGraph) {
    cout << v << " ";
    visited[v] = true;
    for (int u : transposeGraph[v]) {
        if (!visited[u]) {
            dfsTranspose(u, visited, transposeGraph);
        }
    }
}

void kosaraju(int V, vector<vector<int>>& graph) {
    stack<int> Stack;
    vector<bool> visited(V, false);

    // Step 1: Fill the stack according to finishing times
    for (int i = 0; i < V; ++i) {
        if (!visited[i]) {
            dfs(i, visited, graph, Stack);
        }
    }

    // Step 2: Transpose the graph
    vector<vector<int>> transposeGraph(V);
    for (int i = 0; i < V; ++i) {
        for (int u : graph[i]) {
            transposeGraph[u].push_back(i);
        }
    }

    // Step 3: DFS on the transposed graph
    fill(visited.begin(), visited.end(), false);
    while (!Stack.empty()) {
        int v = Stack.top();
        Stack.pop();
        if (!visited[v]) {
            dfsTranspose(v, visited, transposeGraph);
            cout << endl;
        }
    }
}

int main() {
    int V, E;
    cout << "Enter the number of vertices and edges: ";
    cin >> V >> E;
    vector<vector<int>> graph(V);

    cout << "Enter the edges (source destination):" << endl;
    for (int i = 0; i < E; ++i) {
        int u, v;
        cin >> u >> v;
        graph[u].push_back(v);
    }

    cout << "Strongly Connected Components: " << endl;
    kosaraju(V, graph);

    return 0;
}
```

This code takes the number of vertices and edges as input, followed by the edges of the graph. It then prints the strongly connected components of the graph using Kosaraju's Algorithm.

### 1. Algorithms & Data Structures (C++): Kosaraju Algorithm for Strongly Connected Component

Kosaraju's algorithm is a popular algorithm used to find strongly connected components (SCCs) in a directed graph. SCCs are subsets of vertices within a graph where every vertex in the subset is reachable from every other vertex. Here's how Kosaraju's algorithm works:

1. **First DFS (Depth-First Search)**:
   - Perform a DFS traversal of the graph and keep track of the order in which vertices are finished (i.e., they've been fully explored).
   - At the end of this DFS traversal, store the vertices in a stack based on the order in which they were finished.

2. **Transpose the Graph**:
   - Create a new graph where all the edges are reversed. This is done by reversing the direction of each edge in the original graph.

3. **Second DFS**:
   - Pop vertices from the stack generated in the first step in the order of their finishing times.
   - For each popped vertex, if it has not been visited in the second DFS, start a new DFS from it.
   - Each DFS traversal from a new vertex in this step identifies a new strongly connected component.

Here's a C++ implementation of Kosaraju's algorithm:

```cpp
#include <iostream>
#include <vector>
#include <stack>
#include <algorithm>

using namespace std;

// Depth First Search (DFS)
void DFS(int node, vector<int> adj[], vector<bool>& visited, stack<int>& finishedStack) {
    visited[node] = true;
    for (int neighbor : adj[node]) {
        if (!visited[neighbor]) {
            DFS(neighbor, adj, visited, finishedStack);
        }
    }
    finishedStack.push(node); // Push the node to the stack after all its neighbors are visited
}

// Utility function to perform DFS on transposed graph
void DFSUtil(int node, vector<int> transpose[], vector<bool>& visited) {
    visited[node] = true;
    cout << node << " ";
    for (int neighbor : transpose[node]) {
        if (!visited[neighbor]) {
            DFSUtil(neighbor, transpose, visited);
        }
    }
}

// Function to find and print strongly connected components
void KosarajuSCC(int V, vector<int> adj[]) {
    vector<bool> visited(V, false);
    stack<int> finishedStack;

    // Step 1: First DFS to fill the stack based on finishing times
    for (int i = 0; i < V; ++i) {
        if (!visited[i]) {
            DFS(i, adj, visited, finishedStack);
        }
    }

    // Transpose the graph
    vector<int> transpose[V];
    for (int i = 0; i < V; ++i) {
        for (int neighbor : adj[i]) {
            transpose[neighbor].push_back(i);
        }
    }

    // Step 2: Reset visited array
    fill(visited.begin(), visited.end(), false);

    // Step 3: Second DFS to process the vertices in order of their finishing times
    while (!finishedStack.empty()) {
        int node = finishedStack.top();
        finishedStack.pop();
        if (!visited[node]) {
            cout << "SCC: ";
            DFSUtil(node, transpose, visited);
            cout << endl;
        }
    }
}

int main() {
    int V, E;
    cout << "Enter the number of vertices and edges: ";
    cin >> V >> E;

    vector<int> adj[V]; // Adjacency list representation

    cout << "Enter the edges (from -> to):\n";
    for (int i = 0; i < E; ++i) {
        int from, to;
        cin >> from >> to;
        adj[from].push_back(to);
    }

    cout << "Strongly Connected Components:\n";
    KosarajuSCC(V, adj);

    return 0;
}
```

This code prompts the user to enter the number of vertices and edges, followed by the edges of the directed graph. Then it prints the strongly connected components of the graph using Kosaraju's algorithm.

### 1. Algorithms & Data Structures (C++): Kruskal

Kruskal's algorithm is a popular algorithm in graph theory used for finding the minimum spanning tree of a connected, undirected graph. It is a greedy algorithm that finds a minimum spanning tree for a graph with \(V\) vertices and \(E\) edges. Here's how it works:

1. **Sort Edges**: First, sort all the edges in non-decreasing order of their weights.

2. **Initialize**: Create an empty set \(T\) to store the edges of the minimum spanning tree.

3. **Iterate Over Edges**: Iterate through the sorted edges. For each edge:

   - If adding the edge to \(T\) doesn't form a cycle, add it to \(T\). This can be checked using techniques like Union-Find data structure.

   - Otherwise, discard the edge.

4. **Finish**: Repeat this process until there are \(V-1\) edges in \(T\), which means the minimum spanning tree is complete.

Let's see how you can implement Kruskal's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Structure to represent an edge
struct Edge {
    int src, dest, weight;
};

// Structure to represent a subset for union-find
struct Subset {
    int parent, rank;
};

// Find operation of union-find
int find(vector<Subset>& subsets, int i) {
    if (subsets[i].parent != i)
        subsets[i].parent = find(subsets, subsets[i].parent);
    return subsets[i].parent;
}

// Union operation of union-find
void Union(vector<Subset>& subsets, int x, int y) {
    int xroot = find(subsets, x);
    int yroot = find(subsets, y);

    if (subsets[xroot].rank < subsets[yroot].rank)
        subsets[xroot].parent = yroot;
    else if (subsets[xroot].rank > subsets[yroot].rank)
        subsets[yroot].parent = xroot;
    else {
        subsets[yroot].parent = xroot;
        subsets[xroot].rank++;
    }
}

// Comparator to sort edges by weight
bool comp(Edge a, Edge b) {
    return a.weight < b.weight;
}

// Function to find minimum spanning tree using Kruskal's algorithm
void Kruskal(vector<Edge>& edges, int V) {
    // Sort all the edges by weight
    sort(edges.begin(), edges.end(), comp);

    // Allocate memory for subsets
    vector<Subset> subsets(V);

    // Create V subsets with single elements
    for (int v = 0; v < V; ++v) {
        subsets[v].parent = v;
        subsets[v].rank = 0;
    }

    vector<Edge> result; // Stores the resultant MST

    int i = 0, e = 0; // Index variables

    // Keep adding edges until V-1 edges are included
    while (e < V - 1 && i < edges.size()) {
        Edge next_edge = edges[i++];

        int x = find(subsets, next_edge.src);
        int y = find(subsets, next_edge.dest);

        // If including this edge doesn't cause cycle, include it
        if (x != y) {
            result.push_back(next_edge);
            Union(subsets, x, y);
            e++;
        }
    }

    // Print the edges of MST
    cout << "Edges of Minimum Spanning Tree:" << endl;
    for (i = 0; i < result.size(); ++i)
        cout << result[i].src << " - " << result[i].dest << " : " << result[i].weight << endl;
}

// Driver code
int main() {
    // Example graph representation (edges with weights)
    vector<Edge> edges = {
        {0, 1, 10}, {0, 2, 6}, {0, 3, 5},
        {1, 3, 15}, {2, 3, 4}
    };

    int V = 4; // Number of vertices

    Kruskal(edges, V);

    return 0;
}
```

This code demonstrates Kruskal's algorithm with a simple example graph. You can replace the example graph with your own graph representation to find the minimum spanning tree for your specific graph.

### 1. Algorithms & Data Structures (C++): Kruskal Algorithm

The Kruskal algorithm is a popular algorithm used to find the minimum spanning tree (MST) of a connected, undirected graph. The minimum spanning tree of a graph is a subset of the edges that form a tree that includes every vertex, where the total weight of all the edges in the tree is minimized.

Here's a basic outline of how the Kruskal algorithm works:

1. **Initialization**: Create a forest F (a set of trees), where each vertex in the graph is a separate tree.
  
2. **Sort Edges**: Sort all the edges in non-decreasing order of their weight.
  
3. **Iterate Over Edges**: Iterate through all the edges, starting from the one with the smallest weight.
  
4. **Check for Cycle**: For each edge, if adding it to the MST does not form a cycle, add it to the MST. To check for cycles, you can use techniques like Union-Find or Disjoint Set Data Structure.
  
5. **Termination**: Continue this process until there are V-1 edges in the MST, where V is the number of vertices in the graph.

Here's a simple implementation of Kruskal's algorithm in C++ using a Union-Find data structure:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

class UnionFind {
private:
    vector<int> parent, rank;

public:
    UnionFind(int n) {
        parent.resize(n);
        rank.resize(n, 0);
        for (int i = 0; i < n; ++i)
            parent[i] = i;
    }

    int find(int u) {
        if (parent[u] == u)
            return u;
        return parent[u] = find(parent[u]);
    }

    void merge(int u, int v) {
        int pu = find(u);
        int pv = find(v);
        if (pu != pv) {
            if (rank[pu] > rank[pv])
                parent[pv] = pu;
            else if (rank[pu] < rank[pv])
                parent[pu] = pv;
            else {
                parent[pv] = pu;
                rank[pu]++;
            }
        }
    }
};

struct Edge {
    int u, v, weight;
};

bool compareEdges(const Edge& e1, const Edge& e2) {
    return e1.weight < e2.weight;
}

vector<Edge> kruskalMST(vector<Edge>& edges, int n) {
    sort(edges.begin(), edges.end(), compareEdges);

    UnionFind uf(n);
    vector<Edge> mst;
    for (const Edge& edge : edges) {
        if (uf.find(edge.u) != uf.find(edge.v)) {
            mst.push_back(edge);
            uf.merge(edge.u, edge.v);
        }
    }
    return mst;
}

int main() {
    // Example usage
    int n = 4; // Number of vertices
    vector<Edge> edges = {{0, 1, 10}, {0, 2, 6}, {0, 3, 5}, {1, 3, 15}, {2, 3, 4}};
    
    vector<Edge> mst = kruskalMST(edges, n);
    
    cout << "Edges in MST:\n";
    for (const Edge& edge : mst)
        cout << edge.u << " - " << edge.v << " : " << edge.weight << "\n";
    
    return 0;
}
```

This code snippet demonstrates a basic implementation of Kruskal's algorithm using a Union-Find data structure to efficiently detect cycles and construct the MST.

### 1. Algorithms & Data Structures (C++): Kruskal's

Kruskal's algorithm is a popular algorithm used to find the minimum spanning tree (MST) of a connected, undirected graph. The idea behind Kruskal's algorithm is to start with an empty graph and repeatedly add the shortest edge to the MST, as long as adding the edge doesn't create a cycle.

Here's a basic outline of Kruskal's algorithm:

1. **Sort Edges**: Sort all the edges of the graph in non-decreasing order of their weights.
2. **Initialize MST**: Create an empty graph to store the MST.
3. **Iterate Over Edges**: Iterate through all the edges in the sorted order.
4. **Check for Cycle**: For each edge, if adding it to the MST does not create a cycle, add it to the MST.
5. **Repeat**: Repeat step 4 until there are \( V - 1 \) edges in the MST, where \( V \) is the number of vertices in the original graph.

Here's how you can implement Kruskal's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Structure to represent an edge
struct Edge {
    int src, dest, weight;
};

// Structure to represent a subset for union-find
struct Subset {
    int parent, rank;
};

class Graph {
    int V;
    vector<Edge> edges;

public:
    Graph(int V) : V(V) {}

    void addEdge(int src, int dest, int weight) {
        edges.push_back({src, dest, weight});
    }

    // Utility function to find the set of an element 'i'
    int find(vector<Subset>& subsets, int i) {
        if (subsets[i].parent != i)
            subsets[i].parent = find(subsets, subsets[i].parent);
        return subsets[i].parent;
    }

    // Utility function to perform union of two subsets
    void Union(vector<Subset>& subsets, int x, int y) {
        int xroot = find(subsets, x);
        int yroot = find(subsets, y);

        if (subsets[xroot].rank < subsets[yroot].rank)
            subsets[xroot].parent = yroot;
        else if (subsets[xroot].rank > subsets[yroot].rank)
            subsets[yroot].parent = xroot;
        else {
            subsets[yroot].parent = xroot;
            subsets[xroot].rank++;
        }
    }

    // Function to find MST using Kruskal's algorithm
    void KruskalMST() {
        vector<Edge> result;
        int e = 0;
        int i = 0;

        // Sort all the edges in non-decreasing order of their weight
        sort(edges.begin(), edges.end(), [](Edge a, Edge b) {
            return a.weight < b.weight;
        });

        // Allocate memory for creating V subsets
        vector<Subset> subsets(V);
        for (int v = 0; v < V; ++v) {
            subsets[v].parent = v;
            subsets[v].rank = 0;
        }

        // Number of edges to be taken is equal to V-1
        while (e < V - 1 && i < edges.size()) {
            // Pick the smallest edge
            Edge next_edge = edges[i++];

            int x = find(subsets, next_edge.src);
            int y = find(subsets, next_edge.dest);

            // If including this edge doesn't cause cycle, include it in result
            if (x != y) {
                result.push_back(next_edge);
                Union(subsets, x, y);
                ++e;
            }
        }

        // Print the MST
        cout << "Edges in the MST:" << endl;
        for (auto edge : result) {
            cout << edge.src << " - " << edge.dest << " : " << edge.weight << endl;
        }
    }
};

int main() {
    Graph graph(4);
    graph.addEdge(0, 1, 10);
    graph.addEdge(0, 2, 6);
    graph.addEdge(0, 3, 5);
    graph.addEdge(1, 3, 15);
    graph.addEdge(2, 3, 4);

    graph.KruskalMST();

    return 0;
}
```

This implementation assumes that the graph is represented using an adjacency list and uses the Union-Find algorithm for cycle detection. The time complexity of Kruskal's algorithm is \(O(E \log E)\), where \(E\) is the number of edges in the graph.

### 1. Algorithms & Data Structures (C++): Kruskal's Algorithm

Kruskal's algorithm is a popular algorithm in computer science used for finding the minimum spanning tree (MST) of a connected, undirected graph. The minimum spanning tree of a graph is a tree that spans all the vertices of the graph with the minimum possible total edge weight.

Here's a high-level overview of Kruskal's algorithm:

1. **Initialization**: Create a forest (a collection of trees), where each vertex in the graph is a separate tree.

2. **Sort Edges by Weight**: Sort all the edges of the graph in non-decreasing order of their weights.

3. **Iterate Through Edges**: Iterate through the sorted list of edges. For each edge:
   - If adding the edge to the MST does not form a cycle (i.e., the endpoints of the edge belong to different trees in the forest), add the edge to the MST and merge the two trees into one.
   - Otherwise, discard the edge.

4. **Termination**: Repeat step 3 until there are \( V - 1 \) edges in the MST, where \( V \) is the number of vertices in the graph.

5. **Output**: The resulting MST is the minimum spanning tree of the given graph.

Here's a simple implementation of Kruskal's algorithm in C++ using the Union-Find data structure for cycle detection:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

class UnionFind {
private:
    vector<int> parent, rank;

public:
    UnionFind(int n) {
        parent.resize(n);
        rank.resize(n, 0);
        for (int i = 0; i < n; ++i)
            parent[i] = i;
    }

    int find(int u) {
        if (parent[u] == u)
            return u;
        return parent[u] = find(parent[u]);
    }

    void merge(int u, int v) {
        int pu = find(u);
        int pv = find(v);
        if (pu == pv)
            return;
        if (rank[pu] < rank[pv])
            swap(pu, pv);
        parent[pv] = pu;
        if (rank[pu] == rank[pv])
            rank[pu]++;
    }
};

struct Edge {
    int u, v, weight;

    bool operator<(const Edge &other) const {
        return weight < other.weight;
    }
};

vector<Edge> kruskalMST(vector<Edge> &edges, int V) {
    sort(edges.begin(), edges.end());

    UnionFind uf(V);
    vector<Edge> MST;

    for (const Edge &edge : edges) {
        if (uf.find(edge.u) != uf.find(edge.v)) {
            MST.push_back(edge);
            uf.merge(edge.u, edge.v);
        }
    }

    return MST;
}

int main() {
    int V, E;
    cout << "Enter the number of vertices and edges: ";
    cin >> V >> E;

    vector<Edge> edges(E);
    cout << "Enter the edges (u, v, weight):\n";
    for (int i = 0; i < E; ++i)
        cin >> edges[i].u >> edges[i].v >> edges[i].weight;

    vector<Edge> MST = kruskalMST(edges, V);

    cout << "Minimum Spanning Tree Edges:\n";
    for (const Edge &edge : MST)
        cout << edge.u << " - " << edge.v << " : " << edge.weight << endl;

    return 0;
}
```

This implementation assumes that the graph is represented using an edge list, where each edge is represented as a struct containing the source vertex, destination vertex, and weight of the edge. The Union-Find data structure is used to efficiently detect cycles in the graph.

### 1. Algorithms & Data Structures (C++): Kruskal's Algorithm For a Minimal Spanning Tree

Kruskal's algorithm is a popular algorithm used to find the Minimum Spanning Tree (MST) of a connected, undirected graph. The MST of a graph is a subset of the edges that connects all the vertices together with the minimum possible total edge weight.

Here's a high-level overview of Kruskal's algorithm:

1. **Sort the Edges**: Sort all the edges in non-decreasing order of their weight.

2. **Initialize the MST**: Create an empty graph \( T \) representing the Minimum Spanning Tree.

3. **Iterate through Edges**: Iterate through all the sorted edges.

4. **Add Edges to MST**: For each edge, if including it in the MST does not form a cycle, add it to the MST. Otherwise, discard it.

5. **Stop Condition**: Stop when there are \( n-1 \) edges in the MST, where \( n \) is the number of vertices in the original graph.

Here's a simple implementation of Kruskal's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

struct Edge {
    int src, dest, weight;
};

class Graph {
public:
    int V, E;
    vector<Edge> edges;

    Graph(int V, int E) {
        this->V = V;
        this->E = E;
    }

    void addEdge(int src, int dest, int weight) {
        Edge edge = {src, dest, weight};
        edges.push_back(edge);
    }

    // Find parent of node i
    int find(vector<int>& parent, int i) {
        if (parent[i] == -1)
            return i;
        return find(parent, parent[i]);
    }

    // Perform union of two subsets
    void Union(vector<int>& parent, int x, int y) {
        int xset = find(parent, x);
        int yset = find(parent, y);
        parent[xset] = yset;
    }

    // Kruskal's MST algorithm
    void KruskalMST() {
        vector<Edge> result; // This will store the MST
        int e = 0; // An index variable, used for result[]
        int i = 0; // An index variable, used for sorted edges

        // Sort all the edges in non-decreasing order of their weight
        sort(edges.begin(), edges.end(), [](const Edge& a, const Edge& b) {
            return a.weight < b.weight;
        });

        // Allocate memory for creating V subsets
        vector<int> parent(V, -1);

        // Number of edges to be taken is equal to V-1
        while (e < V - 1 && i < E) {
            // Pick the smallest edge
            Edge next_edge = edges[i++];

            int x = find(parent, next_edge.src);
            int y = find(parent, next_edge.dest);

            // If including this edge doesn't cause cycle, include it in result and increment the index of result for next edge
            if (x != y) {
                result.push_back(next_edge);
                Union(parent, x, y);
                e++;
            }
        }

        // Print the contents of result[] to display the built MST
        cout << "Edges of Minimum Spanning Tree:" << endl;
        for (i = 0; i < e; ++i)
            cout << result[i].src << " -- " << result[i].dest << " == " << result[i].weight << endl;
    }
};

int main() {
    // Create a graph
    int V = 4; // Number of vertices
    int E = 5; // Number of edges
    Graph graph(V, E);

    // Add edges
    graph.addEdge(0, 1, 10);
    graph.addEdge(0, 2, 6);
    graph.addEdge(0, 3, 5);
    graph.addEdge(1, 3, 15);
    graph.addEdge(2, 3, 4);

    // Find Minimum Spanning Tree
    graph.KruskalMST();

    return 0;
}
```

This implementation assumes that the graph is represented using an adjacency list. The time complexity of Kruskal's algorithm is \(O(E \log E)\), where \(E\) is the number of edges.

### 1. Algorithms & Data Structures (C++): Kruskal's Minimum Cost Spanning Tree

Kruskal's algorithm is a popular algorithm for finding the Minimum Spanning Tree (MST) of a graph. An MST of a graph is a subset of the edges that connects all the vertices together without any cycles and with the minimum possible total edge weight. Kruskal's algorithm is greedy in nature and works by selecting edges in increasing order of their weights while avoiding the formation of cycles.

Here's a high-level overview of how Kruskal's algorithm works:

1. Sort all the edges in non-decreasing order of their weight.
2. Initialize an empty graph to hold the MST.
3. Iterate through the sorted edges and add each edge to the MST if adding it doesn't form a cycle.
4. Repeat step 3 until there are V-1 edges in the MST, where V is the number of vertices in the graph.

Here's a basic implementation of Kruskal's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Structure to represent an edge
struct Edge {
    int src, dest, weight;
};

// Structure to represent a subset for union-find
struct Subset {
    int parent, rank;
};

// A utility function to find set of an element i
int find(vector<Subset>& subsets, int i) {
    if (subsets[i].parent != i)
        subsets[i].parent = find(subsets, subsets[i].parent);
    return subsets[i].parent;
}

// A utility function to do union of two subsets
void Union(vector<Subset>& subsets, int x, int y) {
    int xroot = find(subsets, x);
    int yroot = find(subsets, y);

    if (subsets[xroot].rank < subsets[yroot].rank)
        subsets[xroot].parent = yroot;
    else if (subsets[xroot].rank > subsets[yroot].rank)
        subsets[yroot].parent = xroot;
    else {
        subsets[yroot].parent = xroot;
        subsets[xroot].rank++;
    }
}

// Comparison function to sort edges by their weight
bool compareEdges(const Edge& a, const Edge& b) {
    return a.weight < b.weight;
}

// Function to find MST using Kruskal's algorithm
void KruskalMST(vector<Edge>& edges, int V) {
    vector<Edge> result;
    int e = 0; // An index variable, used for result[]
    int i = 0; // An index variable, used for sorted edges

    // Sort all the edges in non-decreasing order of their weight
    sort(edges.begin(), edges.end(), compareEdges);

    // Allocate memory for creating V subsets
    vector<Subset> subsets(V);
    for (int v = 0; v < V; v++) {
        subsets[v].parent = v;
        subsets[v].rank = 0;
    }

    // Number of edges to be taken is equal to V-1
    while (e < V - 1 && i < edges.size()) {
        // Pick the smallest edge
        Edge next_edge = edges[i++];

        int x = find(subsets, next_edge.src);
        int y = find(subsets, next_edge.dest);

        // If including this edge doesn't cause cycle, include it in result
        if (x != y) {
            result.push_back(next_edge);
            Union(subsets, x, y);
            e++;
        }
    }

    // Print the constructed MST
    cout << "Edges of MST:\n";
    for (i = 0; i < result.size(); i++)
        cout << result[i].src << " - " << result[i].dest << " : " << result[i].weight << endl;
}

int main() {
    // Example graph represented by edges
    vector<Edge> edges = {
        {0, 1, 10},
        {0, 2, 6},
        {0, 3, 5},
        {1, 3, 15},
        {2, 3, 4}
    };
    int V = 4; // Number of vertices

    // Find the MST using Kruskal's algorithm
    KruskalMST(edges, V);

    return 0;
}
```

This code snippet demonstrates Kruskal's algorithm for finding the MST of a graph represented by edges. You can modify it according to your needs or integrate it into a larger project.

### 1. Algorithms & Data Structures (C++): Kruskals Algorithm

Kruskal's algorithm is a popular algorithm used to find the minimum spanning tree (MST) of a connected, undirected graph. The MST of a graph is a subset of edges that form a tree which includes every vertex, where the total weight of all edges in the tree is minimized.

Here's a basic outline of Kruskal's algorithm:

1. **Initialization**: Create a forest F (a set of trees), where each vertex in the graph is a separate tree.
2. **Sort Edges**: Sort all the edges in non-decreasing order of their weight.
3. **Iterate Through Edges**: Iterate through all edges in the sorted order.
4. **Check for Cycle**: For each edge, if including it in the MST doesn't form a cycle with the edges already in the MST, add it to the MST.
5. **Termination**: Continue this process until we include (V-1) edges, where V is the number of vertices in the graph.

Here's a simple implementation of Kruskal's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

struct Edge {
    int src, dest, weight;
};

class Graph {
    int V;
    vector<Edge> edges;

public:
    Graph(int v) : V(v) {}

    void addEdge(int src, int dest, int weight) {
        edges.push_back({src, dest, weight});
    }

    int find(vector<int>& parent, int i) {
        if (parent[i] == -1)
            return i;
        return find(parent, parent[i]);
    }

    void unionSet(vector<int>& parent, int x, int y) {
        int xroot = find(parent, x);
        int yroot = find(parent, y);
        parent[xroot] = yroot;
    }

    void kruskalMST() {
        vector<int> parent(V, -1);
        vector<Edge> result;
        sort(edges.begin(), edges.end(), [](Edge a, Edge b) {
            return a.weight < b.weight;
        });

        int edgeCount = 0;
        for (auto& edge : edges) {
            int x = find(parent, edge.src);
            int y = find(parent, edge.dest);

            if (x != y) {
                result.push_back(edge);
                unionSet(parent, x, y);
                edgeCount++;
            }
            if (edgeCount == V - 1)
                break;
        }

        cout << "Edges in MST:\n";
        for (auto& edge : result) {
            cout << edge.src << " - " << edge.dest << " : " << edge.weight << endl;
        }
    }
};

int main() {
    Graph g(4);
    g.addEdge(0, 1, 10);
    g.addEdge(0, 2, 6);
    g.addEdge(0, 3, 5);
    g.addEdge(1, 3, 15);
    g.addEdge(2, 3, 4);

    g.kruskalMST();

    return 0;
}
```

This implementation assumes an undirected graph and uses a disjoint-set data structure to efficiently detect cycles during the construction of the MST. The time complexity of Kruskal's algorithm is O(E log E), where E is the number of edges in the graph.

### 1. Algorithms & Data Structures (C++): Limitation of Dijikstra

Dijkstra's algorithm is a fundamental algorithm for finding the shortest path in a graph from a source node to all other nodes. While it's quite efficient in finding the shortest path in weighted graphs with non-negative edge weights, it does have some limitations:

1. **Doesn't Work with Negative Weights**: Dijkstra's algorithm doesn't work when the graph has edges with negative weights. This is because it relies on the property that once a node is marked as visited, its shortest path is finalized. With negative weights, it's possible to find a shorter path even after a node has been marked as visited.

2. **Doesn't Handle Graphs with Negative Cycles**: Even if all edge weights are non-negative, Dijkstra's algorithm can fail if the graph contains a negative cycle (a cycle whose total weight is negative). This is because in the presence of a negative cycle, there is no well-defined shortest path, as one can keep traversing the cycle to decrease the path length indefinitely.

3. **Inefficient for Dense Graphs**: While Dijkstra's algorithm performs well for sparse graphs (where the number of edges is much less than the number of nodes), it becomes inefficient for dense graphs. In dense graphs, the priority queue operations required by Dijkstra's algorithm can become quite expensive.

4. **Requires Priority Queue**: Dijkstra's algorithm requires a priority queue to efficiently select the next node to visit. Implementing a priority queue can add complexity to the algorithm, especially in languages like C++ where the standard library's priority queue doesn't support efficient decrease-key operations.

5. **Memory Usage**: In its typical form, Dijkstra's algorithm uses a lot of memory since it needs to keep track of the shortest distances from the source node to all other nodes in the graph. This memory requirement can be prohibitive for very large graphs.

These limitations make Dijkstra's algorithm unsuitable for certain types of graphs or situations. For cases where negative weights or negative cycles are present, algorithms like Bellman-Ford or Floyd-Warshall are more appropriate.

### 1. Algorithms & Data Structures (C++): Longest Path

To find the longest path in a graph, you can use either depth-first search (DFS) or breadth-first search (BFS) algorithms. Here's how you can implement it using DFS in C++:

```cpp
#include <iostream>
#include <vector>
#include <stack>
#include <algorithm>

using namespace std;

// Function to perform DFS and find the longest path
void dfs(vector<vector<int>>& graph, int node, vector<bool>& visited, stack<int>& s) {
    visited[node] = true;
    for (int i = 0; i < graph[node].size(); ++i) {
        if (!visited[graph[node][i]]) {
            dfs(graph, graph[node][i], visited, s);
        }
    }
    s.push(node);
}

// Function to find the longest path using DFS
vector<int> longestPath(vector<vector<int>>& graph, int V) {
    vector<bool> visited(V, false);
    stack<int> s;

    for (int i = 0; i < V; ++i) {
        if (!visited[i]) {
            dfs(graph, i, visited, s);
        }
    }

    vector<int> dist(V, INT_MIN);
    dist[s.top()] = 0;

    while (!s.empty()) {
        int node = s.top();
        s.pop();

        if (dist[node] != INT_MIN) {
            for (int i = 0; i < graph[node].size(); ++i) {
                if (dist[graph[node][i]] < dist[node] + 1) {
                    dist[graph[node][i]] = dist[node] + 1;
                }
            }
        }
    }

    return dist;
}

int main() {
    int V, E; // V is the number of vertices, E is the number of edges
    cout << "Enter the number of vertices and edges: ";
    cin >> V >> E;

    vector<vector<int>> graph(V);

    cout << "Enter the edges:\n";
    for (int i = 0; i < E; ++i) {
        int u, v;
        cin >> u >> v;
        graph[u].push_back(v);
    }

    vector<int> dist = longestPath(graph, V);

    int longest = *max_element(dist.begin(), dist.end());

    cout << "Longest Path Length: " << longest << endl;

    return 0;
}
```

This code first performs a topological sort using DFS to get the order of vertices, then it calculates the longest path using dynamic programming on the reversed graph. Finally, it prints the length of the longest path.

### 1. Algorithms & Data Structures (C++): Longest Possible Route

To find the longest possible route in a graph using C++, you can use depth-first search (DFS) or breadth-first search (BFS) algorithms. Here's an example implementation using DFS:

```cpp
#include <iostream>
#include <vector>
#include <stack>
#include <algorithm>

using namespace std;

// Structure to represent an edge
struct Edge {
    int to;
    int weight;
};

// Function to perform depth-first search
void dfs(int node, const vector<vector<Edge>>& graph, vector<bool>& visited, vector<int>& distances) {
    visited[node] = true;
    for (const Edge& edge : graph[node]) {
        if (!visited[edge.to]) {
            distances[edge.to] = distances[node] + edge.weight;
            dfs(edge.to, graph, visited, distances);
        }
    }
}

// Function to find the longest path in a graph using DFS
int longestPath(const vector<vector<Edge>>& graph) {
    int n = graph.size();
    vector<bool> visited(n, false);
    vector<int> distances(n, 0);

    // Perform DFS from each node
    for (int i = 0; i < n; ++i) {
        if (!visited[i]) {
            dfs(i, graph, visited, distances);
        }
    }

    // Find the node farthest from the starting node
    int farthestNode = max_element(distances.begin(), distances.end()) - distances.begin();

    // Reset visited array and distances array
    fill(visited.begin(), visited.end(), false);
    fill(distances.begin(), distances.end(), 0);

    // Perform DFS from the farthest node
    dfs(farthestNode, graph, visited, distances);

    // Return the maximum distance found
    return *max_element(distances.begin(), distances.end());
}

int main() {
    int n; // Number of nodes
    cin >> n;

    // Create the graph
    vector<vector<Edge>> graph(n);

    // Input edges
    for (int i = 0; i < n - 1; ++i) {
        int from, to, weight;
        cin >> from >> to >> weight;
        graph[from].push_back({to, weight});
        graph[to].push_back({from, weight}); // Assuming undirected graph
    }

    // Find the longest path
    int longest = longestPath(graph);
    cout << "Longest possible route length: " << longest << endl;

    return 0;
}
```

This code represents a graph as an adjacency list. It uses DFS to find the longest path in the graph. The `Edge` struct represents an edge with its destination node and weight. The `dfs` function performs depth-first search to calculate distances from a starting node. Finally, the `longestPath` function iterates over each node to find the farthest node from the starting node and then performs DFS again from that farthest node to find the longest path.

### 1. Algorithms & Data Structures (C++): Network Algorithms

Network algorithms in the context of computer science typically involve solving problems related to networks, which could be anything from computer networks to social networks. Here are some common network algorithms implemented in C++:

1. **Breadth-First Search (BFS)**:
   - Used to traverse or search a graph or tree data structure.
   - It explores all the nodes at the present depth before moving on to the nodes at the next depth level.
   - Helpful in finding the shortest path in an unweighted graph.

2. **Depth-First Search (DFS)**:
   - Similar to BFS but explores as far as possible along each branch before backtracking.
   - Used for topological sorting, strongly connected components, and solving maze problems.

3. **Dijkstra's Algorithm**:
   - Finds the shortest path between nodes in a graph, particularly in weighted graphs.
   - Works well for non-negative edge weights.
   - Can be implemented using priority queues or sets.

4. **Bellman-Ford Algorithm**:
   - Another algorithm to find the shortest path between nodes in a graph.
   - Can handle negative edge weights unlike Dijkstra's algorithm.
   - Typically slower than Dijkstra's algorithm.

5. **Floyd-Warshall Algorithm**:
   - Finds the shortest paths between all pairs of vertices in a weighted graph.
   - Can handle negative edge weights but not negative cycles.
   - Works well for dense graphs.

6. **Minimum Spanning Tree (MST) Algorithms**:
   - Prim's Algorithm: Constructs a minimum spanning tree for a weighted undirected graph.
   - Kruskal's Algorithm: Constructs a minimum spanning tree for a connected weighted graph.

7. **Max Flow Algorithms**:
   - Ford-Fulkerson Algorithm: Finds the maximum flow in a flow network.
   - Edmonds-Karp Algorithm: A specific implementation of the Ford-Fulkerson method using BFS.

8. **Network Flow Problems**:
   - Dinic's Algorithm: Finds the maximum flow in a flow network more efficiently than Ford-Fulkerson.

9. **Eulerian Path and Circuit Algorithms**:
   - Hierholzer's Algorithm: Finds an Eulerian cycle in a graph, if one exists.

10. **Bipartite Graphs**:
    - Bipartite Matching: Finding a maximum matching in a bipartite graph.
    - Hopcroft-Karp Algorithm: Efficient algorithm for finding maximum cardinality matching in bipartite graphs.

These are just a few examples of network algorithms implemented in C++. Each algorithm has its own use case and performance characteristics, so the choice of algorithm depends on the specific problem you're trying to solve and the characteristics of the data you're working with.

### 1. Algorithms & Data Structures (C++): Network Classes

Creating network classes in C++ involves structuring your code to represent network entities like nodes and edges, and implementing algorithms for tasks such as traversal, pathfinding, and connectivity checking. Here's a basic outline of how you might structure such classes:

1. **Node Class**: This represents a node in the network.

```cpp
class Node {
private:
    int id;
    // Additional properties like data, if needed
public:
    Node(int id) : id(id) {}
    int getId() const { return id; }
    // Additional methods as needed
};
```

1. **Edge Class**: This represents an edge connecting two nodes.

```cpp
class Edge {
private:
    Node* source;
    Node* destination;
    int weight; // If it's a weighted network
    // Additional properties as needed
public:
    Edge(Node* source, Node* destination, int weight = 1) 
        : source(source), destination(destination), weight(weight) {}
    Node* getSource() const { return source; }
    Node* getDestination() const { return destination; }
    int getWeight() const { return weight; }
    // Additional methods as needed
};
```

1. **Graph Class**: This represents the entire network and contains methods for manipulating nodes and edges.

```cpp
#include <vector>

class Graph {
private:
    std::vector<Node*> nodes;
    std::vector<Edge*> edges;
    // Additional properties and helper functions as needed
public:
    void addNode(Node* node) { nodes.push_back(node); }
    void addEdge(Edge* edge) { edges.push_back(edge); }
    // Methods for traversing, pathfinding, connectivity checking, etc.
};
```

With this basic structure in place, you can implement algorithms such as breadth-first search (BFS) or depth-first search (DFS) for traversing the network, Dijkstra's algorithm for finding shortest paths, or algorithms for checking connectivity like union-find. These algorithms would typically be implemented as member functions of the `Graph` class or as standalone functions that operate on a `Graph` object.

Remember to manage memory properly, either by using smart pointers (`std::shared_ptr` or `std::unique_ptr`) or by ensuring proper memory deallocation when objects are no longer needed. Also, consider adding error handling and input validation to your methods to handle unexpected situations gracefully.

### 1. Algorithms & Data Structures (C++): network delay time

The "network delay time" problem typically refers to finding the time it takes for a signal to travel through a network from a source node to a destination node. This problem is often framed in the context of graph theory and can be solved using algorithms like Dijkstra's algorithm or Bellman-Ford algorithm. Let's discuss a solution using Dijkstra's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <climits>

using namespace std;

// Structure to represent an edge in the graph
struct Edge {
    int to;
    int weight;
    Edge(int t, int w) : to(t), weight(w) {}
};

// Structure to represent a node in the graph
struct Node {
    int id;
    int dist;
    Node(int i, int d) : id(i), dist(d) {}
    bool operator>(const Node& other) const {
        return dist > other.dist;
    }
};

// Dijkstra's algorithm to find the shortest path
int networkDelayTime(vector<vector<Edge>>& graph, int N, int K) {
    vector<int> dist(N + 1, INT_MAX); // Initialize distances to infinity
    priority_queue<Node, vector<Node>, greater<Node>> pq;

    dist[K] = 0; // Distance to source node K is 0
    pq.push(Node(K, 0));

    while (!pq.empty()) {
        Node curr = pq.top();
        pq.pop();
        int u = curr.id;
        int d = curr.dist;

        if (d > dist[u]) // Skip if this node has been processed before
            continue;

        for (const Edge& edge : graph[u]) {
            int v = edge.to;
            int w = edge.weight;

            // Relaxation step
            if (dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;
                pq.push(Node(v, dist[v]));
            }
        }
    }

    int maxDelay = 0;
    for (int i = 1; i <= N; ++i) {
        if (dist[i] == INT_MAX) // If any node is unreachable, return -1
            return -1;
        maxDelay = max(maxDelay, dist[i]);
    }

    return maxDelay;
}

int main() {
    int N, M, K;
    // N: Number of nodes, M: Number of edges, K: Source node
    cin >> N >> M >> K;

    vector<vector<Edge>> graph(N + 1);
    // Input the edges of the graph
    for (int i = 0; i < M; ++i) {
        int u, v, w;
        cin >> u >> v >> w;
        graph[u].push_back(Edge(v, w));
    }

    int delay = networkDelayTime(graph, N, K);
    cout << "Network delay time: " << delay << endl;

    return 0;
}
```

In this code:

- We represent the graph using an adjacency list.
- We use Dijkstra's algorithm to find the shortest path from the source node K to all other nodes.
- We maintain a priority queue to efficiently select the node with the shortest distance.
- Finally, we find the maximum distance from the source node to any other node, which represents the network delay time.

Remember to input the number of nodes (N), number of edges (M), and the source node (K), followed by M lines representing the edges (u, v, w) where (u, v) is an edge from node u to node v with weight w.

### 1. Algorithms & Data Structures (C++): Network Delay Time - Graphs

The "Network Delay Time" problem typically involves finding the minimum time it takes for a signal to travel from a source node to all other nodes in a weighted directed graph. This problem can be solved efficiently using Dijkstra's algorithm, which is a popular algorithm for finding the shortest paths between nodes in a graph.

Here's a basic outline of how you can implement Dijkstra's algorithm in C++ to solve the Network Delay Time problem:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>

using namespace std;

#define INF numeric_limits<int>::max()

// Function to find the minimum delay time using Dijkstra's algorithm
int networkDelayTime(vector<vector<pair<int, int>>>& graph, int N, int K) {
    vector<int> dist(N + 1, INF);
    dist[K] = 0;

    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    pq.push({0, K});

    while (!pq.empty()) {
        int u = pq.top().second;
        pq.pop();

        for (auto& edge : graph[u]) {
            int v = edge.first;
            int weight = edge.second;
            if (dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
                pq.push({dist[v], v});
            }
        }
    }

    int max_delay = 0;
    for (int i = 1; i <= N; ++i) {
        if (dist[i] == INF) return -1; // There is no path to node i
        max_delay = max(max_delay, dist[i]);
    }
    return max_delay;
}

int main() {
    // Example usage
    int N = 4; // Number of nodes
    int K = 2; // Source node
    vector<vector<pair<int, int>>> graph(N + 1);
    // Input graph representation (node, weight)
    graph[2].push_back({1, 1});
    graph[2].push_back({3, 1});
    graph[3].push_back({4, 1});

    int delay = networkDelayTime(graph, N, K);
    if (delay == -1)
        cout << "Network Delay Time: Impossible to reach all nodes" << endl;
    else
        cout << "Network Delay Time: " << delay << endl;

    return 0;
}
```

In this code:

- `networkDelayTime` function takes the adjacency list representation of the graph, the number of nodes `N`, and the source node `K`.
- It initializes a vector `dist` to store the minimum delay time to reach each node from the source node `K`.
- It uses a priority queue `pq` to keep track of the nodes to visit next based on their distance from the source node.
- Dijkstra's algorithm iterates until the priority queue is empty, updating the minimum delay time to reach each node.
- Finally, it calculates the maximum delay time and returns it. If any node is unreachable, it returns -1.
- In the `main` function, you can define the graph and call `networkDelayTime` to get the result.

### 1. Algorithms & Data Structures (C++): Network Terminology

Certainly! Here's an overview of some common network terminology in the context of algorithms and data structures:

1. **Graph**: In network terminology, a graph is a collection of nodes (vertices) connected by edges. It's a fundamental data structure used to model relationships between objects. Graphs can be directed (edges have a specific direction) or undirected (edges have no specific direction).

2. **Node (Vertex)**: A fundamental unit of a graph. It represents an entity or an object within the network. In a social network, for example, nodes might represent individuals, while in a computer network, nodes could be computers or routers.

3. **Edge**: A connection between two nodes in a graph. It may be directional (directed edge) or undirectional (undirected edge), depending on whether there's a specific relationship direction between the nodes.

4. **Weighted Graph**: A graph in which each edge is assigned a numerical weight. These weights could represent various properties such as distance, cost, or capacity. Weighted graphs are commonly used to model real-world scenarios more accurately.

5. **Adjacency**: In the context of graphs, adjacency refers to the relationship between nodes that are directly connected by an edge. An adjacency matrix or adjacency list can represent this relationship.

6. **Adjacency Matrix**: A 2D array used to represent a graph. The element in the ith row and jth column of the matrix indicates whether there's an edge between the ith and jth nodes.

7. **Adjacency List**: A data structure that represents a graph as an array of linked lists or an associative array (map/dictionary). Each element in the array/map corresponds to a node, and the associated linked list or array contains the nodes adjacent to it.

8. **Path**: A sequence of edges that connects a sequence of vertices in a graph. Paths can be simple (no repeated vertices) or contain cycles (repeated vertices).

9. **Cycle**: A path in a graph that starts and ends at the same node, with no repeated edges (except the starting and ending node).

10. **Tree**: A special type of graph where any two nodes are connected by exactly one path. Trees have a hierarchical structure with a root node and may have parent-child relationships.

11. **Root**: In a tree data structure, the topmost node without a parent. It's the starting point of the tree structure.

12. **Leaf**: In a tree data structure, a node with no children. It's a terminal node in the hierarchy.

13. **Binary Tree**: A tree data structure in which each node has at most two children, typically referred to as the left child and the right child.

14. **Binary Search Tree (BST)**: A binary tree data structure in which the left child of a node contains values less than the node's value, and the right child contains values greater than the node's value. This property allows for efficient searching, insertion, and deletion operations.

These are some fundamental concepts in network terminology that are frequently encountered when dealing with algorithms and data structures related to networks.

### 1. Algorithms & Data Structures (C++): Number of jumps to reach n

To calculate the minimum number of jumps needed to reach a given position \( n \) in C++, you can use a dynamic programming approach. Here's a sample implementation:

```cpp
#include <iostream>
#include <vector>
#include <climits>

using namespace std;

int minJumps(vector<int>& arr, int n) {
    if (n <= 1)
        return 0;

    // If first element is 0, we can't move forward
    if (arr[0] == 0)
        return -1;

    // Initialize jumps[] with INT_MAX
    vector<int> jumps(n, INT_MAX);
    jumps[0] = 0;

    // Calculate minimum jumps required for each position
    for (int i = 1; i < n; i++) {
        for (int j = 0; j < i; j++) {
            // If we can reach position i from position j
            if (j + arr[j] >= i && jumps[j] != INT_MAX) {
                jumps[i] = min(jumps[i], jumps[j] + 1);
                break; // Once a jump is found, move to the next position
            }
        }
    }

    return (jumps[n - 1] != INT_MAX) ? jumps[n - 1] : -1; // Return -1 if not reachable
}

int main() {
    vector<int> arr = {2, 3, 1, 1, 2, 4, 2, 0, 1, 1}; // Sample array
    int n = arr.size();
    cout << "Minimum number of jumps to reach " << n << ": " << minJumps(arr, n) << endl;
    return 0;
}
```

This code finds the minimum number of jumps required to reach the last element of the array `arr`, given the constraints that each element of the array represents the maximum number of positions forward you can jump from that element, and that you can't jump to positions with a value of 0.

The `minJumps` function takes the array `arr` and its size `n` as inputs and returns the minimum number of jumps required. If it's not possible to reach the last element, it returns -1.

### 1. Algorithms & Data Structures (C++): Post-order traversal

In computer science, specifically in the context of trees and graphs, post-order traversal is a method of traversing through all the nodes in a tree data structure. It involves visiting the left and right subtrees of a node before visiting the node itself.

Here's how post-order traversal works:

1. Recursively traverse the left subtree.
2. Recursively traverse the right subtree.
3. Visit the node.

In C++, you can implement post-order traversal using recursion. Here's a basic example of how you might implement it for a binary tree:

```cpp
#include <iostream>

// Define the structure of a binary tree node
struct Node {
    int data;
    Node* left;
    Node* right;
    
    Node(int value) : data(value), left(nullptr), right(nullptr) {}
};

// Function to perform post-order traversal recursively
void postOrderTraversal(Node* root) {
    if (root == nullptr)
        return;

    // Traverse the left subtree
    postOrderTraversal(root->left);

    // Traverse the right subtree
    postOrderTraversal(root->right);

    // Visit the current node
    std::cout << root->data << " ";
}

// Function to create a sample binary tree
Node* createSampleTree() {
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    root->right->left = new Node(6);
    root->right->right = new Node(7);
    return root;
}

int main() {
    Node* root = createSampleTree();
    
    std::cout << "Post-order traversal: ";
    postOrderTraversal(root);
    std::cout << std::endl;
    
    return 0;
}
```

In this example, `Node` represents a basic node of the binary tree, and `postOrderTraversal` is a function that performs post-order traversal recursively. The `main` function creates a sample binary tree and then performs post-order traversal on it.

### 1. Algorithms & Data Structures (C++): Post-order Traversal Technique

Post-order traversal is a popular technique used in tree-based data structures, such as binary trees. It's called "post-order" because it traverses the nodes in the order of left subtree, right subtree, root. In other words, it visits the left child, then the right child, and finally the parent node.

Here's how you can implement post-order traversal in C++ using recursion:

```cpp
#include <iostream>

// Define the structure of a binary tree node
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to perform post-order traversal recursively
void postOrder(TreeNode* root) {
    if (root == nullptr) return;

    // Traverse left subtree
    postOrder(root->left);

    // Traverse right subtree
    postOrder(root->right);

    // Visit the current node
    std::cout << root->val << " ";
}

int main() {
    // Example of constructing a binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    // Perform post-order traversal starting from the root
    std::cout << "Post-order traversal: ";
    postOrder(root);

    return 0;
}
```

In this code:

- We first define a `TreeNode` struct to represent the nodes of the binary tree. Each node contains an integer value (`val`) and pointers to its left and right children.
- The `postOrder` function is a recursive function that performs post-order traversal. It first recursively traverses the left subtree, then the right subtree, and finally visits the current node.
- In the `main` function, we construct an example binary tree and call the `postOrder` function to perform post-order traversal starting from the root node.

This code will output the nodes of the binary tree in post-order traversal. You can modify it to suit your specific needs or integrate it into a larger program as necessary.

### 1. Algorithms & Data Structures (C++): PostOrder Traversal

In computer science, particularly in the realm of algorithms and data structures, a postorder traversal is a method for traversing a tree data structure. Specifically, in a postorder traversal, the algorithm visits the nodes in the following order: left subtree, right subtree, root node. This traversal strategy is often used in tree-related operations and is especially useful in scenarios where you need to process or manipulate nodes in a specific order.

Here's how you can implement a postorder traversal in C++ using recursion:

```cpp
#include <iostream>

// Define a simple binary tree node structure
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to perform postorder traversal recursively
void postorderTraversal(TreeNode* root) {
    if (root == nullptr) return;

    // Traverse left subtree
    postorderTraversal(root->left);

    // Traverse right subtree
    postorderTraversal(root->right);

    // Visit the root node
    std::cout << root->val << " ";
}

int main() {
    // Example tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    // Perform postorder traversal
    std::cout << "Postorder traversal: ";
    postorderTraversal(root);
    std::cout << std::endl;

    // Clean up memory
    // (In a real application, you would typically have more robust memory management)
    delete root->left->left;
    delete root->left->right;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

In this code:

- We define a simple `TreeNode` struct to represent the nodes in our binary tree.
- The `postorderTraversal` function is a recursive function that traverses the tree in a postorder manner: it first traverses the left subtree, then the right subtree, and finally visits the root node.
- In the `main` function, we create an example binary tree and perform a postorder traversal on it.

This implementation demonstrates the basic idea of performing a postorder traversal in C++. You can adapt it to your specific needs or modify it to work with other tree representations.

### 1. Algorithms & Data Structures (C++): Prim's

Prim's algorithm is a popular algorithm used to find the minimum spanning tree (MST) of a connected, undirected graph. Here's a high-level overview of how Prim's algorithm works:

1. **Initialization**: Start with an arbitrary vertex as the initial vertex of the MST. Let's call this vertex "current_vertex". Also, initialize an empty set or priority queue to keep track of vertices that are not yet included in the MST.

2. **Iterative Process**: Repeat the following steps until all vertices are included in the MST:
   - Find the edge with the minimum weight that connects the current_vertex to a vertex that is not yet included in the MST.
   - Add this edge to the MST.
   - Add the newly connected vertex to the set of vertices included in the MST.
   - Update the current_vertex to the newly added vertex.

3. **Termination**: When all vertices are included in the MST, the algorithm terminates.

4. **Output**: The set of edges selected during the process forms the minimum spanning tree.

Here's a simplified pseudocode representation of Prim's algorithm:

```
prim(Graph G):
    Initialize an empty set mstSet to keep track of vertices included in MST.
    Initialize a priority queue or min-heap (priority_queue) to store edge-weight pairs.

    Choose an arbitrary vertex as the starting vertex.
    Add the starting vertex to mstSet.

    while mstSet does not contain all vertices in G:
        for each edge e going out of vertices in mstSet:
            if the destination vertex of e is not in mstSet:
                add e to the priority queue

        pick the edge with the minimum weight from the priority queue
        add the destination vertex of the chosen edge to mstSet

    return mstSet
```

In this pseudocode:

- The priority queue ensures that we always select the edge with the minimum weight that connects a vertex in the MST to a vertex outside the MST.
- The mstSet keeps track of vertices already included in the MST.
- The algorithm continues until all vertices are included in the MST.

Implementing this algorithm in C++ involves creating appropriate data structures to represent the graph, such as adjacency lists or adjacency matrices, and implementing the priority queue or min-heap to efficiently retrieve the minimum-weight edge.

### 1. Algorithms & Data Structures (C++): Prim's Algorithm

Prim's algorithm is a greedy algorithm used to find a minimum spanning tree for a weighted undirected graph. It starts with an arbitrary vertex and grows the spanning tree by adding the cheapest edge that connects the tree to a vertex not yet in the tree until all vertices are included. Here's a basic implementation of Prim's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <utility>
#include <climits>

using namespace std;

// Define an edge structure
struct Edge {
    int to;
    int weight;
};

// Function to add an edge to the graph
void addEdge(vector<vector<Edge>>& graph, int from, int to, int weight) {
    graph[from].push_back({to, weight});
    graph[to].push_back({from, weight}); // for undirected graph
}

// Prim's algorithm function
int primMST(vector<vector<Edge>>& graph, int start) {
    int V = graph.size(); // number of vertices

    // Priority queue to store vertices that are candidates for MST
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;

    vector<int> key(V, INT_MAX); // Key values used to pick minimum weight edge
    vector<bool> inMST(V, false); // To represent set of vertices included in MST

    pq.push({0, start}); // Start from the given vertex
    key[start] = 0; // Key value for start vertex is 0

    int minCost = 0; // Initialize result

    while (!pq.empty()) {
        // Extract the vertex with minimum key value
        int u = pq.top().second;
        pq.pop();

        // Include the vertex in MST
        inMST[u] = true;

        // Update key value and add adjacent vertices to priority queue
        for (auto& edge : graph[u]) {
            int v = edge.to;
            int weight = edge.weight;
            if (!inMST[v] && weight < key[v]) {
                key[v] = weight;
                pq.push({key[v], v});
            }
        }
    }

    // Calculate total cost of MST
    for (int i = 0; i < V; ++i) {
        minCost += key[i];
    }

    return minCost;
}

int main() {
    int V = 5; // Number of vertices
    vector<vector<Edge>> graph(V); // Adjacency list representation of graph

    // Add edges
    addEdge(graph, 0, 1, 2);
    addEdge(graph, 0, 3, 6);
    addEdge(graph, 1, 2, 3);
    addEdge(graph, 1, 3, 8);
    addEdge(graph, 1, 4, 5);
    addEdge(graph, 2, 4, 7);
    addEdge(graph, 3, 4, 9);

    int startVertex = 0; // Start vertex for MST

    // Find the minimum cost of MST
    int minCost = primMST(graph, startVertex);

    cout << "Minimum Cost Spanning Tree: " << minCost << endl;

    return 0;
}
```

In this code:

- `addEdge` function is used to add edges to the graph.
- `primMST` function finds the minimum spanning tree using Prim's algorithm.
- `main` function sets up a sample graph and finds the minimum cost spanning tree from a chosen start vertex.

This code demonstrates how Prim's algorithm works and can be extended to handle larger graphs.

### 1. Algorithms & Data Structures (C++): Prim's Algorithm For a Minimal Spanning Tree

Prim's algorithm is a greedy algorithm used to find the minimum spanning tree (MST) of a connected, undirected graph. Here's a basic implementation of Prim's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <climits>

using namespace std;

// Edge structure to represent edges in the graph
struct Edge {
    int destination;
    int weight;
};

// Function to add an edge to the adjacency list of the graph
void addEdge(vector<vector<Edge>>& graph, int src, int dest, int weight) {
    Edge edge = {dest, weight};
    graph[src].push_back(edge);
    
    // Since the graph is undirected, add the edge from dest to src as well
    edge.destination = src;
    graph[dest].push_back(edge);
}

// Function to find the minimum spanning tree using Prim's algorithm
void primMST(vector<vector<Edge>>& graph, int V) {
    // Priority queue to store vertices that are candidates for inclusion in the MST
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;

    // Vector to store parent of each vertex in the MST
    vector<int> parent(V, -1);

    // Vector to store the weight of each vertex in the MST
    vector<int> key(V, INT_MAX);

    // Vector to keep track of whether a vertex is in the MST or not
    vector<bool> inMST(V, false);

    // Add the first vertex (0) to the MST
    pq.push({0, 0});
    key[0] = 0;

    while (!pq.empty()) {
        int u = pq.top().second;
        pq.pop();

        inMST[u] = true;

        // Iterate through all adjacent vertices of u
        for (const Edge& edge : graph[u]) {
            int v = edge.destination;
            int weight = edge.weight;

            // If v is not yet in the MST and weight of the edge (u,v) is less than current key of v
            if (!inMST[v] && weight < key[v]) {
                key[v] = weight;
                parent[v] = u;
                pq.push({key[v], v});
            }
        }
    }

    // Print the edges of the MST
    cout << "Edges of the Minimum Spanning Tree:" << endl;
    for (int i = 1; i < V; ++i)
        cout << parent[i] << " - " << i << endl;
}

int main() {
    int V = 5; // Number of vertices
    vector<vector<Edge>> graph(V);

    // Add edges to the graph
    addEdge(graph, 0, 1, 2);
    addEdge(graph, 0, 3, 6);
    addEdge(graph, 1, 2, 3);
    addEdge(graph, 1, 3, 8);
    addEdge(graph, 1, 4, 5);
    addEdge(graph, 2, 4, 7);
    addEdge(graph, 3, 4, 9);

    // Find and print the minimum spanning tree
    primMST(graph, V);

    return 0;
}
```

This code creates a simple undirected graph with some sample edges and vertices and then applies Prim's algorithm to find the minimum spanning tree. The `addEdge` function is used to add edges to the graph. The `primMST` function is responsible for finding the MST using Prim's algorithm. Finally, the main function initializes the graph, adds edges, and calls `primMST` to find and print the minimum spanning tree.

### 1. Algorithms & Data Structures (C++): Prim's Algorithm: Use Cases

Prim's algorithm is a widely used algorithm in computer science, particularly in the field of graph theory and network optimization. It is used to find the minimum spanning tree (MST) of a connected, undirected graph with weighted edges. Here are some common use cases for Prim's algorithm:

1. **Network Design**: Prim's algorithm can be used in network design problems where you want to connect a set of nodes (representing locations or endpoints) with minimum total cost, ensuring that all nodes are reachable and there are no cycles.

2. **Cable or Wire Layout**: In physical infrastructure projects like laying down cables or wires for communication or power transmission, Prim's algorithm can help in determining the most cost-effective layout to connect all the endpoints.

3. **Cluster Analysis**: In data analysis and machine learning, Prim's algorithm can be applied to cluster analysis problems where you want to group similar data points together while minimizing the total distance or cost of connecting them.

4. **Traffic Management**: In transportation systems, Prim's algorithm can be used to optimize traffic flow by determining the most efficient routes between locations or intersections, minimizing congestion and travel time.

5. **Routing in Computer Networks**: Prim's algorithm can be applied in computer networking to find the shortest path or optimal route between nodes in a network, considering factors such as latency or bandwidth.

6. **Wireless Sensor Networks**: In wireless sensor networks where energy conservation is crucial, Prim's algorithm can be used to construct a minimum energy-consuming spanning tree to optimize the network's lifetime.

7. **Spanning Tree Protocol (STP)**: In networking protocols like the Spanning Tree Protocol used in Ethernet networks, Prim's algorithm is employed to prevent loops in the network topology while ensuring connectivity.

8. **Power Distribution Networks**: Prim's algorithm can be utilized in designing power distribution networks to minimize the cost of laying down power lines while ensuring that all regions are adequately supplied with electricity.

9. **Urban Planning**: In urban planning, Prim's algorithm can assist in determining the layout of roads, bridges, and public transportation routes to optimize connectivity and minimize construction costs.

10. **Supply Chain Optimization**: Prim's algorithm can be used in supply chain management to optimize the transportation routes between warehouses, distribution centers, and retail stores, minimizing transportation costs and delivery times.

These are just a few examples of the diverse range of applications where Prim's algorithm can be employed to solve optimization problems efficiently. Its ability to find the minimum spanning tree makes it a valuable tool in various fields where minimizing costs or maximizing efficiency is essential.

### 1. Algorithms & Data Structures (C++): Prim's Minimum Cost Spanning Tree

Prim's algorithm is a greedy algorithm used to find the minimum spanning tree of a weighted undirected graph. It starts with an arbitrary vertex and grows the spanning tree by adding the cheapest edge that connects a vertex in the tree to a vertex outside the tree, until all vertices are included in the tree.

Here's a basic implementation of Prim's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <climits>

using namespace std;

// Structure to represent a graph edge
struct Edge {
    int dest;
    int weight;
};

// Structure to represent a node in the priority queue
struct PQNode {
    int vertex;
    int key;
};

// Comparison function for priority queue
struct Compare {
    bool operator()(const PQNode& a, const PQNode& b) {
        return a.key > b.key;
    }
};

// Function to find the minimum spanning tree using Prim's algorithm
void primMST(vector<vector<Edge>>& graph, int V) {
    vector<int> parent(V, -1); // Array to store the parent of each vertex in MST
    vector<int> key(V, INT_MAX); // Key values used to pick minimum weight edge in cut
    vector<bool> inMST(V, false); // To represent set of vertices included in MST

    priority_queue<PQNode, vector<PQNode>, Compare> pq;

    // Start with the first vertex
    key[0] = 0;
    pq.push({0, key[0]});

    // Loop through all vertices to construct MST
    while (!pq.empty()) {
        int u = pq.top().vertex;
        pq.pop();
        inMST[u] = true;

        // Explore all adjacent vertices of u
        for (auto& edge : graph[u]) {
            int v = edge.dest;
            int weight = edge.weight;

            // If v is not in MST and weight of (u,v) is smaller than current key of v
            if (!inMST[v] && weight < key[v]) {
                key[v] = weight;
                parent[v] = u;
                pq.push({v, key[v]});
            }
        }
    }

    // Print the edges of MST
    for (int i = 1; i < V; i++) {
        cout << "Edge: " << parent[i] << " - " << i << " Weight: " << key[i] << endl;
    }
}

int main() {
    int V, E;
    cout << "Enter the number of vertices and edges: ";
    cin >> V >> E;

    vector<vector<Edge>> graph(V);

    cout << "Enter edges with weights:\n";
    for (int i = 0; i < E; i++) {
        int src, dest, weight;
        cin >> src >> dest >> weight;
        graph[src].push_back({dest, weight});
        graph[dest].push_back({src, weight}); // Assuming undirected graph
    }

    cout << "Minimum Spanning Tree:\n";
    primMST(graph, V);

    return 0;
}
```

This implementation assumes an adjacency list representation of the graph. The `Edge` struct represents an edge with its destination vertex and weight. The `PQNode` struct is used to represent a node in the priority queue with the vertex and its key value. The `Compare` struct defines the comparison function for the priority queue. The `primMST` function takes the graph and the number of vertices as input and prints the edges of the minimum spanning tree.

You can input the number of vertices, the number of edges, and then input the edges along with their weights. The program will output the edges of the minimum spanning tree along with their weights.

### 1. Algorithms & Data Structures (C++): Prim's vs Kruskal

Prim's and Kruskal's algorithms are both used for finding the minimum spanning tree (MST) of a weighted graph. Here's a comparison between the two:

1. **Algorithm Type**:
   - Prim's: Prim's algorithm is a greedy algorithm.
   - Kruskal's: Kruskal's algorithm is also a greedy algorithm.

2. **Approach**:
   - Prim's: It grows the minimum spanning tree from an arbitrary vertex by adding the cheapest edge to the tree that doesn't form a cycle until all vertices are included.
   - Kruskal's: It selects edges in ascending order of weight and adds them to the growing forest (initially individual vertices) if they don't create a cycle until all vertices are connected.

3. **Complexity**:
   - Prim's: The time complexity of Prim's algorithm is O(V^2) with an adjacency matrix representation, and O(E log V) with an adjacency list representation using a priority queue.
   - Kruskal's: The time complexity of Kruskal's algorithm is O(E log E) with a sorting operation, where E is the number of edges.

4. **Edge Selection**:
   - Prim's: It selects the minimum-weight edge incident to the tree at each step.
   - Kruskal's: It selects edges based solely on weight, without considering the connectivity of the graph.

5. **Use Cases**:
   - Prim's: It's generally faster for dense graphs (graphs with a large number of edges).
   - Kruskal's: It's often preferred for sparse graphs (graphs with relatively few edges).

6. **Space Complexity**:
   - Prim's: Requires O(V) space for the priority queue plus O(V^2) or O(V) space for storing the adjacency matrix or adjacency list, respectively.
   - Kruskal's: Requires O(E + V) space for the disjoint-set data structure.

7. **Implementation**:
   - Prim's: Typically implemented using a priority queue for efficient selection of minimum-weight edges.
   - Kruskal's: Typically implemented using a disjoint-set data structure for efficient cycle detection.

8. **Parallelization**:
   - Kruskal's: Easier to parallelize since the edge selection is independent.
   - Prim's: More challenging to parallelize due to the dependency on the current tree.

In summary, both Prim's and Kruskal's algorithms are efficient ways to find the minimum spanning tree of a graph, but the choice between them often depends on the specific characteristics of the graph and the available resources.

### 1. Algorithms & Data Structures (C++): Prims

Prim's algorithm is a popular algorithm in computer science used to find the minimum spanning tree (MST) of a connected, undirected graph. The minimum spanning tree of a graph is a subgraph that is a tree (a graph with no cycles) and connects all the vertices together with the minimum possible total edge weight.

Here's a high-level overview of Prim's algorithm:

1. **Initialization**: Start with an arbitrary vertex as the initial tree. Initialize a set to keep track of vertices that are already included in the MST and a priority queue (or a min-heap) to store potential edges with their weights.

2. **Grow the Tree**: Repeat the following steps until all vertices are included in the MST:
   - Choose the vertex that is not in the MST and has the minimum edge weight connecting it to the MST.
   - Add this vertex and the corresponding edge to the MST.

3. **Termination**: When all vertices are included in the MST, stop.

Here's a basic implementation of Prim's algorithm in C++ using an adjacency matrix representation of the graph:

```cpp
#include <iostream>
#include <climits>
using namespace std;

#define V 5 // Number of vertices in the graph

int minKey(int key[], bool mstSet[]) {
    int min = INT_MAX, min_index;
    for (int v = 0; v < V; v++) {
        if (!mstSet[v] && key[v] < min) {
            min = key[v];
            min_index = v;
        }
    }
    return min_index;
}

void printMST(int parent[], int graph[V][V]) {
    cout << "Edge \tWeight\n";
    for (int i = 1; i < V; i++)
        cout << parent[i] << " - " << i << " \t" << graph[i][parent[i]] << " \n";
}

void primMST(int graph[V][V]) {
    int parent[V]; // Array to store constructed MST
    int key[V]; // Key values used to pick minimum weight edge in cut
    bool mstSet[V]; // To represent set of vertices included in MST

    // Initialize all keys as INFINITE
    for (int i = 0; i < V; i++) {
        key[i] = INT_MAX;
        mstSet[i] = false;
    }

    // Always include first vertex in MST.
    key[0] = 0; // Make key 0 so that this vertex is picked as first vertex
    parent[0] = -1; // First node is always root of MST

    // The MST will have V vertices
    for (int count = 0; count < V - 1; count++) {
        int u = minKey(key, mstSet); // Pick the minimum key vertex from the set of vertices not yet included in MST
        mstSet[u] = true; // Add the picked vertex to the MST set

        // Update key value and parent index of the adjacent vertices of the picked vertex.
        for (int v = 0; v < V; v++) {
            if (graph[u][v] && !mstSet[v] && graph[u][v] < key[v]) {
                parent[v] = u;
                key[v] = graph[u][v];
            }
        }
    }

    // Print the constructed MST
    printMST(parent, graph);
}

int main() {
    // Example graph represented by adjacency matrix
    int graph[V][V] = {{0, 2, 0, 6, 0},
                       {2, 0, 3, 8, 5},
                       {0, 3, 0, 0, 7},
                       {6, 8, 0, 0, 9},
                       {0, 5, 7, 9, 0}};

    primMST(graph);

    return 0;
}
```

This code demonstrates Prim's algorithm for finding the MST of a given graph. The `main` function initializes an example graph and calls the `primMST` function to find the minimum spanning tree. The `primMST` function implements the algorithm itself, while the `minKey` function is a helper function used to find the vertex with the minimum key value that has not yet been included in the MST. Finally, the `printMST` function is used to print the edges and weights of the minimum spanning tree.

### 1. Algorithms & Data Structures (C++): Prims Algorithm

Prim's algorithm is a greedy algorithm that finds a minimum spanning tree for a weighted undirected graph. It starts with an arbitrary vertex and grows the spanning tree by adding the cheapest edge that connects the tree to a vertex not yet in the tree. Here's a basic implementation of Prim's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <climits>

using namespace std;

#define INF INT_MAX

// Structure to represent a weighted edge
struct Edge {
    int to, weight;
    Edge(int _to, int _weight) : to(_to), weight(_weight) {}
};

// Function to find the minimum spanning tree using Prim's algorithm
void primMST(vector<vector<Edge>>& graph, int V) {
    vector<int> parent(V, -1); // Array to store constructed MST
    vector<int> key(V, INF);   // Key values used to pick minimum weight edge
    vector<bool> inMST(V, false); // To represent set of vertices not yet included in MST

    // Priority queue to store vertices that are being preprocessed.
    // This is used to find the minimum edge weight.
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;

    // Start with vertex 0
    int src = 0;
    pq.push(make_pair(0, src));
    key[src] = 0;

    while (!pq.empty()) {
        int u = pq.top().second;
        pq.pop();
        inMST[u] = true;

        // Iterate through all adjacent vertices of u
        for (auto& edge : graph[u]) {
            int v = edge.to;
            int weight = edge.weight;

            // If v is not in MST and weight of (u,v) is smaller than current key of v
            if (!inMST[v] && weight < key[v]) {
                key[v] = weight;
                parent[v] = u;
                pq.push(make_pair(key[v], v));
            }
        }
    }

    // Print the constructed MST
    cout << "Edge \tWeight\n";
    for (int i = 1; i < V; ++i)
        cout << parent[i] << " - " << i << "\t" << graph[i][parent[i]].weight << "\n";
}

int main() {
    int V, E;
    cout << "Enter number of vertices and edges: ";
    cin >> V >> E;

    // Adjacency list representation of graph
    vector<vector<Edge>> graph(V);

    cout << "Enter edges with weights (from to weight):\n";
    for (int i = 0; i < E; ++i) {
        int from, to, weight;
        cin >> from >> to >> weight;
        graph[from].push_back(Edge(to, weight));
        graph[to].push_back(Edge(from, weight)); // Undirected graph
    }

    // Find and print MST using Prim's algorithm
    primMST(graph, V);

    return 0;
}
```

This code snippet defines a basic implementation of Prim's algorithm in C++. It takes input for the number of vertices and edges, and then takes input for the edges with their respective weights. Finally, it prints the edges of the minimum spanning tree along with their weights.

### 1. Algorithms & Data Structures (C++): Prims Explaination

Prim's algorithm is a method used in computer science to find the minimum spanning tree (MST) of a connected, undirected graph. The minimum spanning tree of a graph is a subgraph that is a tree and connects all the vertices together with the minimum possible total edge weight.

Here's a step-by-step explanation of how Prim's algorithm works:

1. **Start with an arbitrary vertex**: Choose any vertex to start building the minimum spanning tree.

2. **Initialize**: Create an empty set to store the vertices included in the MST and a priority queue (or a min-heap) to store the edges that connect the vertices in the MST to those outside the MST. Initialize the priority queue with the edges connected to the chosen vertex.

3. **Iterate until all vertices are included in the MST**:
   - While the priority queue is not empty, repeatedly do the following:
     - Remove the edge with the minimum weight from the priority queue. Let's call this edge (u, v).
     - If vertex v is not in the MST (i.e., it has not been visited yet):
       - Add vertex v to the MST.
       - Add edge (u, v) to the MST.
       - Add all edges connected to vertex v (excluding those leading back to vertices already in the MST) to the priority queue.

4. **Finish**: When all vertices are included in the MST, stop.

5. **Output**: The MST is the set of edges that have been added during the process.

Prim's algorithm ensures that at each step, it adds the minimum-weight edge that connects a vertex in the MST to a vertex outside the MST. This process continues until all vertices are included in the MST, resulting in the minimum spanning tree. The time complexity of Prim's algorithm is O(V^2) using an adjacency matrix or O(E log V) using a priority queue implementation, where V is the number of vertices and E is the number of edges in the graph.

In C++, you can implement Prim's algorithm using adjacency lists or adjacency matrices to represent the graph, along with priority queues or heaps for efficient selection of minimum-weight edges.

### 1. Algorithms & Data Structures (C++): Prims: Commutable Islands

Prim's algorithm is a method used to find the minimum spanning tree (MST) of a weighted undirected graph. It's a greedy algorithm that starts with an arbitrary vertex and repeatedly grows a tree by adding the cheapest edge that connects a vertex in the tree to a vertex outside the tree until all vertices are included.

In the context of "Commutable Islands," which seems like a graph problem, it's likely that you have a set of islands (vertices) and bridges connecting them (edges), each with a certain cost. The task may be to find the minimum cost to connect all islands, or to determine the cost of the minimum spanning tree (MST) of the graph representing these islands and bridges.

Here's a basic outline of how you might implement Prim's algorithm in C++ for this problem:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <climits>

using namespace std;

// Structure to represent a vertex and its corresponding cost
struct Node {
    int vertex;
    int cost;
};

// Function to implement Prim's algorithm
int primMST(vector<vector<Node>>& graph) {
    int n = graph.size(); // Number of vertices
    vector<bool> visited(n, false); // To keep track of visited vertices
    int minCost = 0; // Total cost of MST

    // Priority queue to store vertices along with their costs
    priority_queue<Node, vector<Node>, greater<Node>> pq;

    // Start from the first vertex
    pq.push({0, 0});

    while (!pq.empty()) {
        // Extract the vertex with the minimum cost
        Node curr = pq.top();
        pq.pop();

        int u = curr.vertex;
        int cost = curr.cost;

        // If vertex u is already visited, skip it
        if (visited[u])
            continue;

        // Mark vertex u as visited
        visited[u] = true;

        // Add the cost of the edge to the total cost
        minCost += cost;

        // Visit all adjacent vertices of u
        for (const auto& neighbor : graph[u]) {
            int v = neighbor.vertex;
            int weight = neighbor.cost;
            if (!visited[v])
                pq.push({v, weight});
        }
    }

    return minCost;
}

int main() {
    // Example graph representation (adjacency list)
    vector<vector<Node>> graph = {
        {{1, 2}, {2, 3}},
        {{0, 2}, {2, 4}, {3, 5}},
        {{0, 3}, {1, 4}, {3, 6}},
        {{1, 5}, {2, 6}}
    };

    int minCost = primMST(graph);
    cout << "Minimum cost to connect all islands: " << minCost << endl;

    return 0;
}
```

In this implementation, `Node` represents a vertex and its corresponding cost. The `primMST` function calculates the minimum cost to connect all islands using Prim's algorithm. The `main` function provides an example graph represented as an adjacency list and calculates the minimum cost. You can adjust the graph representation and input as per your specific problem requirements.

### 1. Algorithms & Data Structures (C++): Prims: Commutable Islands explain

Prim's algorithm is a popular algorithm used to find the minimum spanning tree (MST) of a weighted undirected graph. It's quite similar to Dijkstra's algorithm in its approach but focuses on finding the minimum spanning tree rather than the shortest path.

Here's how Prim's algorithm works:

1. **Start with an arbitrary vertex**: Choose any vertex to start the tree. This vertex will be the root of the MST.

2. **Grow the tree incrementally**: At each step, consider all the edges that connect the tree to vertices not yet in the tree. Choose the edge with the smallest weight and add the vertex at the other end of the edge to the tree. This ensures that the tree grows in such a way that it spans all the vertices while minimizing the total weight of the edges.

3. **Repeat until all vertices are in the tree**: Continue adding vertices to the tree until all vertices are included.

The algorithm is greedy, meaning it makes the locally optimal choice at each step with the hope of finding the globally optimal solution.

Now, when it comes specifically to "Commutable Islands," it sounds like you're dealing with a problem where the vertices of the graph represent islands and the edges represent the cost of building a bridge between two islands. The goal is likely to find the minimum cost of building bridges to connect all the islands.

So, you can use Prim's algorithm in this scenario to find the minimum cost of building bridges such that all islands are connected. The resulting minimum spanning tree would represent the optimal solution, where each island is reachable from every other island, and the total cost of building the bridges is minimized.

In C++, you can implement Prim's algorithm using a priority queue to efficiently select the minimum weight edge at each step. The data structures needed would typically include a priority queue, an array to keep track of visited vertices, and possibly a data structure to represent the graph itself, such as an adjacency list or adjacency matrix.

Would you like to see a code example in C++ for implementing Prim's algorithm for finding the minimum spanning tree?

### 1. Algorithms & Data Structures (C++): Properties of Graph - Directed and Undirected

Directed and undirected graphs are fundamental concepts in graph theory and are crucial in various applications such as network analysis, social network modeling, and routing algorithms. Here's a breakdown of their properties:

**Directed Graph:**

1. **Edges:** Each edge has a direction associated with it. It indicates a one-way relationship between two vertices.
2. **Connectivity:** The connectivity between two vertices may not be symmetric. In other words, if there is an edge from vertex A to vertex B, it doesn't necessarily imply that there is an edge from B to A.
3. **Degree:** The degree of a vertex in a directed graph is divided into two types:
   - **In-Degree:** The number of edges entering a vertex.
   - **Out-Degree:** The number of edges leaving a vertex.
4. **Cycles:** Directed graphs can contain directed cycles, where starting from a vertex, following the direction of edges, you can reach back to the same vertex.

**Undirected Graph:**

1. **Edges:** Each edge does not have a specific direction associated with it. It indicates a two-way relationship between two vertices.
2. **Connectivity:** The connectivity between two vertices is symmetric. If there is an edge between vertex A and vertex B, it implies that there is also an edge between B and A.
3. **Degree:** In an undirected graph, the degree of a vertex represents the number of edges incident to that vertex, irrespective of direction.
4. **Cycles:** Undirected graphs can also contain cycles, where you can traverse through edges and return to the same vertex without following a specific direction.

**Shared Properties:**

1. **Adjacency Matrix/Lists:** Both directed and undirected graphs can be represented using adjacency matrices or adjacency lists.
2. **Connectivity:** Both types of graphs can have connected components, where a subset of vertices are connected to each other, and there are no connections between these components.
3. **Traversal:** Algorithms like Depth-First Search (DFS) and Breadth-First Search (BFS) can be applied to both types of graphs for various purposes like traversal, connectivity checking, and finding paths.
4. **Weighted Graphs:** Both directed and undirected graphs can have weights associated with their edges, indicating the cost or distance between vertices.

Understanding these properties is crucial for designing algorithms and data structures tailored to the specific requirements of directed or undirected graphs in various applications.

### 1. Algorithms & Data Structures (C++): Properties of Graphs

Graphs in computer science are fundamental data structures used to represent relationships between pairs of objects. Here are some key properties of graphs:

1. **Vertices (Nodes)**: Graphs consist of a set of vertices (also known as nodes) that represent the entities in the graph. These entities could be anything, such as cities in a map, people in a social network, or tasks in a project.

2. **Edges (Links)**: Edges are the connections between vertices. They represent relationships or associations between the entities represented by the vertices. An edge may be directed or undirected. In a directed graph, edges have a direction indicating a one-way relationship, while in an undirected graph, edges have no direction, indicating a two-way relationship.

3. **Weighted/Unweighted Graphs**: In some graphs, edges are assigned weights or costs. These weights represent the "cost" of traversing from one vertex to another. For example, in a graph representing a road network, weights could represent distances between cities. In contrast, unweighted graphs have edges with no associated weights.

4. **Connectedness**: A graph is connected if there is a path between every pair of vertices in the graph. In other words, there are no isolated vertices or disjoint components in a connected graph. If a graph is not connected, it may consist of multiple connected components.

5. **Directed vs. Undirected Graphs**: Directed graphs (also called digraphs) have edges with a direction. This means that the relationship between two vertices is one-way. Undirected graphs have edges with no inherent direction, meaning the relationship between vertices is symmetric.

6. **Cyclic vs. Acyclic Graphs**: A graph containing at least one cycle (a path that starts and ends at the same vertex) is called cyclic. In contrast, a graph that contains no cycles is called acyclic. Directed acyclic graphs (DAGs) are particularly important in many applications, such as representing dependencies or precedence relationships.

7. **Degree of a Vertex**: The degree of a vertex is the number of edges incident to it. In a directed graph, vertices have both in-degree (number of edges entering the vertex) and out-degree (number of edges leaving the vertex). In an undirected graph, all edges have the same degree.

8. **Adjacency Matrix and Adjacency List**: Graphs can be represented in computer memory using different data structures. An adjacency matrix is a 2D array where the presence or absence of an edge between two vertices is represented by a value in the matrix. An adjacency list is a collection of lists or arrays, where each vertex has a list of its adjacent vertices.

Understanding these properties is crucial for effectively applying algorithms and solving problems on graphs.

### 1. Algorithms & Data Structures (C++): Recursive Implementation of Depth First Search

Sure, here's a simple implementation of Depth First Search (DFS) using recursion in C++:

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>

using namespace std;

// Node structure representing each node in the graph
struct Node {
    int val;
    vector<Node*> neighbors;
    Node(int x) : val(x), neighbors(vector<Node*>()) {}
};

class Graph {
private:
    unordered_set<Node*> visited;

public:
    void dfs(Node* node) {
        // Check if the node has been visited before
        if (visited.find(node) != visited.end())
            return;

        // Mark the current node as visited
        visited.insert(node);
        cout << node->val << " ";

        // Explore all neighbors of the current node
        for (Node* neighbor : node->neighbors) {
            dfs(neighbor);
        }
    }
};

int main() {
    // Create a sample graph
    Node* node1 = new Node(1);
    Node* node2 = new Node(2);
    Node* node3 = new Node(3);
    Node* node4 = new Node(4);
    Node* node5 = new Node(5);

    node1->neighbors.push_back(node2);
    node1->neighbors.push_back(node3);
    node2->neighbors.push_back(node4);
    node3->neighbors.push_back(node5);

    Graph graph;
    cout << "DFS traversal starting from node 1: ";
    graph.dfs(node1);

    // Clean up memory
    delete node1;
    delete node2;
    delete node3;
    delete node4;
    delete node5;

    return 0;
}
```

In this implementation:

- We define a `Node` struct to represent each node in the graph. Each node contains a value and a vector of pointers to its neighboring nodes.
- We define a `Graph` class with a `dfs` method to perform the depth-first search traversal.
- The `dfs` method takes a starting node as input and recursively explores all reachable nodes from that node.
- We use an `unordered_set` to keep track of visited nodes to avoid visiting the same node multiple times.
- In the `main` function, we create a sample graph and call the `dfs` method starting from a chosen node.

Remember to deallocate memory for dynamically allocated nodes after their use to avoid memory leaks.

### 1. Algorithms & Data Structures (C++): Remove Maximum Number of Edges

Removing the maximum number of edges from a graph typically involves finding a way to disconnect the maximum number of vertices while still keeping the graph connected. One common problem related to this is finding the maximum number of edges to remove to disconnect a tree. However, I'll provide a more general approach to remove the maximum number of edges from a graph in C++.

Here's a general outline of the approach:

1. **Representation of Graph**: You need a way to represent the graph. You can use an adjacency list or adjacency matrix depending on the size of the graph.

2. **Depth-First Search (DFS) or Breadth-First Search (BFS)**: Start with any vertex of the graph and perform a DFS or BFS traversal. During the traversal, keep track of the number of vertices visited. This will give you an idea of the connected components of the graph.

3. **Count Edges to Remove**: After performing the traversal, you'll have an idea of the number of connected components in the graph. To maximize the number of removed edges, you typically want to disconnect the largest connected component from the rest of the graph. Calculate the number of edges you would need to remove to disconnect this largest component from the rest of the graph.

4. **Implementation**: Implement the necessary functions for graph representation, DFS/BFS traversal, and edge removal calculation.

Here's a simplified example in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj;

public:
    Graph(int V) : V(V) {
        adj.resize(V);
    }

    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u);
    }

    // Depth First Search
    void DFSUtil(int v, vector<bool>& visited, int& count) {
        visited[v] = true;
        count++;
        for (int u : adj[v]) {
            if (!visited[u])
                DFSUtil(u, visited, count);
        }
    }

    int countEdgesToRemove() {
        vector<bool> visited(V, false);
        int max_count = 0;
        for (int v = 0; v < V; ++v) {
            if (!visited[v]) {
                int count = 0;
                DFSUtil(v, visited, count);
                max_count = max(max_count, count);
            }
        }
        return V - max_count;
    }
};

int main() {
    int n, m; // Number of vertices and edges
    cin >> n >> m;

    Graph g(n);

    // Read edges
    for (int i = 0; i < m; ++i) {
        int u, v;
        cin >> u >> v;
        g.addEdge(u, v);
    }

    cout << "Maximum number of edges to remove: " << g.countEdgesToRemove() << endl;

    return 0;
}
```

This is a basic example. Depending on your specific problem constraints and requirements, you might need to modify and optimize this code.

### 1. Algorithms & Data Structures (C++): Representation of Directed Graphs

In C++, directed graphs can be represented using various data structures, depending on the requirements of the application, such as memory efficiency, speed of operations (like adding/removing edges or vertices), and ease of traversal. The most common representations are:

1. **Adjacency Matrix**:
   - An adjacency matrix is a 2D array (or vector of vectors) where the cell at row \( i \) and column \( j \) indicates whether there is a directed edge from vertex \( i \) to vertex \( j \).
   - **Pros**:
     - Simple and easy to implement.
     - Efficient for dense graphs where the number of edges is close to the number of vertices squared.
     - Constant time complexity \( O(1) \) for checking if an edge exists between two vertices.
   - **Cons**:
     - Requires \( O(V^2) \) space, which is inefficient for sparse graphs.
     - Adding or removing edges is not as efficient as in other representations.

   ```cpp
   #include <vector>
   using namespace std;

   class Graph {
       int numVertices;
       vector<vector<bool>> adjMatrix;

   public:
       Graph(int vertices) {
           numVertices = vertices;
           adjMatrix.resize(vertices, vector<bool>(vertices, false));
       }

       void addEdge(int start, int end) {
           adjMatrix[start][end] = true;
       }

       void removeEdge(int start, int end) {
           adjMatrix[start][end] = false;
       }

       bool isEdge(int start, int end) {
           return adjMatrix[start][end];
       }
   };
   ```

2. **Adjacency List**:
   - An adjacency list is an array (or vector) of lists (or vectors), where the list at index \( i \) contains all the vertices that vertex \( i \) has edges to.
   - **Pros**:
     - More space-efficient for sparse graphs.
     - Easier to iterate over the edges of a vertex.
   - **Cons**:
     - Checking for the existence of an edge takes \( O(V) \) time in the worst case (though on average, it might be faster).
     - Slightly more complex to implement compared to the adjacency matrix.

   ```cpp
   #include <vector>
   using namespace std;

   class Graph {
       int numVertices;
       vector<vector<int>> adjList;

   public:
       Graph(int vertices) {
           numVertices = vertices;
           adjList.resize(vertices);
       }

       void addEdge(int start, int end) {
           adjList[start].push_back(end);
       }

       void removeEdge(int start, int end) {
           adjList[start].erase(remove(adjList[start].begin(), adjList[start].end(), end), adjList[start].end());
       }

       vector<int> getAdjVertices(int vertex) {
           return adjList[vertex];
       }
   };
   ```

3. **Edge List**:
   - An edge list is simply a list of edges where each edge is represented as a pair (or tuple) of vertices.
   - **Pros**:
     - Very simple to implement.
     - Efficient for algorithms that work with edges directly.
   - **Cons**:
     - Inefficient for operations like checking for the existence of a specific edge or finding all neighbors of a vertex.

   ```cpp
   #include <vector>
   using namespace std;

   class Graph {
       vector<pair<int, int>> edgeList;

   public:
       void addEdge(int start, int end) {
           edgeList.push_back(make_pair(start, end));
       }

       void removeEdge(int start, int end) {
           edgeList.erase(remove(edgeList.begin(), edgeList.end(), make_pair(start, end)), edgeList.end());
       }

       vector<pair<int, int>> getEdges() {
           return edgeList;
       }
   };
   ```

#### Choosing the Right Representation

- **Adjacency Matrix**: Best for dense graphs and when quick edge look-up is needed.
- **Adjacency List**: Best for sparse graphs and when iterating over neighbors is a common operation.
- **Edge List**: Useful for edge-centric operations or when graph structure is simple and edge operations are primary.

#### Example Usage

Here's a quick example showing how to use an adjacency list representation in practice:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
    int numVertices;
    vector<vector<int>> adjList;

public:
    Graph(int vertices) {
        numVertices = vertices;
        adjList.resize(vertices);
    }

    void addEdge(int start, int end) {
        adjList[start].push_back(end);
    }

    vector<int> getAdjVertices(int vertex) {
        return adjList[vertex];
    }

    void printGraph() {
        for (int i = 0; i < numVertices; i++) {
            cout << "Vertex " << i << ":";
            for (int v : adjList[i]) {
                cout << " " << v;
            }
            cout << endl;
        }
    }
};

int main() {
    Graph g(5);
    g.addEdge(0, 1);
    g.addEdge(0, 4);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 3);
    g.addEdge(3, 4);

    g.printGraph();

    return 0;
}
```

This code will create a graph with 5 vertices and a set of directed edges, then print the adjacency list representation of the graph.

### 1. Algorithms & Data Structures (C++): Representation of Graph : Adjacency List

In C++, you can represent a graph using an adjacency list. An adjacency list is a collection of lists or arrays to represent the connections between vertices in a graph. Each vertex has a list of adjacent vertices, indicating which vertices are directly connected to it. Here's a basic implementation of a graph using an adjacency list in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Class to represent a graph using adjacency list
class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    // Constructor
    Graph(int vertices) {
        V = vertices;
        adj.resize(V);
    }

    // Function to add an edge between two vertices
    void addEdge(int src, int dest) {
        adj[src].push_back(dest); // Add dest to src's list
        adj[dest].push_back(src); // Add src to dest's list if undirected graph
    }

    // Function to print the adjacency list representation of the graph
    void printGraph() {
        for (int v = 0; v < V; ++v) {
            cout << "Adjacency list of vertex " << v << ":\n";
            cout << "head ";
            for (int i : adj[v]) {
                cout << "-> " << i;
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph graph(5);
    
    // Add edges
    graph.addEdge(0, 1);
    graph.addEdge(0, 4);
    graph.addEdge(1, 2);
    graph.addEdge(1, 3);
    graph.addEdge(1, 4);
    graph.addEdge(2, 3);
    graph.addEdge(3, 4);

    // Print the adjacency list representation of the graph
    graph.printGraph();

    return 0;
}
```

In this code:

- The `Graph` class represents a graph using an adjacency list.
- The `adj` vector is a vector of vectors. Each element of `adj` represents a list of adjacent vertices for a particular vertex.
- The `addEdge` function adds an edge between two vertices by adding each vertex to the other's adjacency list.
- The `printGraph` function prints the adjacency list representation of the graph.

You can customize this implementation according to your requirements, such as adding functions for traversing the graph, checking for the existence of an edge, or implementing other graph algorithms.

### 1. Algorithms & Data Structures (C++): Representation of Graph : Adjacency Matrix

In C++, you can represent a graph using an adjacency matrix. An adjacency matrix is a 2D array where each cell `matrix[i][j]` represents whether there is an edge between vertex `i` and vertex `j`. Here's a basic implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adjMatrix;

public:
    // Constructor
    Graph(int vertices) : V(vertices) {
        // Resize the adjacency matrix to VxV and initialize with zeros
        adjMatrix.resize(V, vector<int>(V, 0));
    }

    // Function to add an edge between vertices u and v
    void addEdge(int u, int v) {
        adjMatrix[u][v] = 1; // For an undirected graph, you might also set adjMatrix[v][u] = 1
    }

    // Function to print the adjacency matrix
    void printAdjMatrix() {
        for (int i = 0; i < V; ++i) {
            for (int j = 0; j < V; ++j) {
                cout << adjMatrix[i][j] << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 4 vertices
    Graph g(4);

    // Add edges
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    // Print the adjacency matrix
    cout << "Adjacency Matrix:" << endl;
    g.printAdjMatrix();

    return 0;
}
```

This code creates a graph with 4 vertices and adds some edges. Then, it prints the adjacency matrix. Note that in this example, the graph is assumed to be undirected, so if an edge is added between vertices `u` and `v`, an edge will also exist between vertices `v` and `u`. If you want to represent a directed graph, you need to consider directionality while adding edges.

### 1. Algorithms & Data Structures (C++): Representation of Undirected Graph

In C++, an undirected graph can be represented using various data structures. One of the most common representations is using an adjacency list or an adjacency matrix. Here's how you can represent an undirected graph using both approaches:

### Adjacency List Representation

In this representation, each vertex of the graph is associated with a list of its neighboring vertices.

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V) {
        adj.resize(V);
    }

    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u); // For undirected graph
    }

    void printGraph() {
        for (int v = 0; v < V; ++v) {
            cout << "Adjacency list of vertex " << v << ": ";
            for (auto neighbor : adj[v]) {
                cout << neighbor << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph g(5);

    // Add edges
    g.addEdge(0, 1);
    g.addEdge(0, 4);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 3);
    g.addEdge(3, 4);

    // Print the adjacency list representation of the graph
    g.printGraph();

    return 0;
}
```

### Adjacency Matrix Representation

In this representation, a matrix of size VxV is used where V is the number of vertices. A cell (i, j) in the matrix represents whether there is an edge between vertices i and j.

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector<vector<bool>> adj; // Adjacency matrix

public:
    Graph(int V) : V(V) {
        adj.resize(V, vector<bool>(V, false));
    }

    void addEdge(int u, int v) {
        adj[u][v] = true;
        adj[v][u] = true; // For undirected graph
    }

    void printGraph() {
        for (int i = 0; i < V; ++i) {
            for (int j = 0; j < V; ++j) {
                cout << adj[i][j] << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph g(5);

    // Add edges
    g.addEdge(0, 1);
    g.addEdge(0, 4);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 3);
    g.addEdge(3, 4);

    // Print the adjacency matrix representation of the graph
    g.printGraph();

    return 0;
}
```

Both representations have their advantages and disadvantages. The adjacency list representation is more memory efficient for sparse graphs, while the adjacency matrix representation is more efficient for dense graphs and allows constant time edge weight lookup. Choose the representation that best suits your specific application requirements.

### 1. Algorithms & Data Structures (C++): Representing A Graph

In C++, you have a few options for representing a graph, each with its own strengths and weaknesses depending on the specific use case. Here's an overview of some common representations:

1. **Adjacency Matrix**:
   - In an adjacency matrix, you represent the graph as a 2D array where `matrix[i][j]` is true if there is an edge from vertex `i` to vertex `j`, and false otherwise.
   - This representation is simple and allows for fast lookups of whether an edge exists between two vertices.
   - However, it consumes a lot of memory, especially for sparse graphs (graphs with relatively few edges).

```cpp
#include <vector>
using namespace std;

class Graph {
private:
    int V;
    vector<vector<bool>> adjMatrix;

public:
    Graph(int vertices) : V(vertices) {
        adjMatrix.resize(V, vector<bool>(V, false));
    }

    void addEdge(int i, int j) {
        adjMatrix[i][j] = true;
        // For undirected graph, uncomment the line below
        // adjMatrix[j][i] = true;
    }

    bool isEdge(int i, int j) {
        return adjMatrix[i][j];
    }
};
```

1. **Adjacency List**:
   - In an adjacency list, you represent the graph as an array of lists. Each element of the array represents a vertex, and the list associated with each vertex contains all the vertices adjacent to it.
   - This representation is more memory-efficient for sparse graphs.
   - Traversing neighbors of a vertex is straightforward, but checking if there is an edge between two vertices is less efficient compared to the adjacency matrix.

```cpp
#include <vector>
#include <list>
using namespace std;

class Graph {
private:
    int V;
    vector

```cpp
    <list<int>> adjList;

public:
    Graph(int vertices) : V(vertices) {
        adjList.resize(V);
    }

    void addEdge(int i, int j) {
        adjList[i].push_back(j);
        // For undirected graph, uncomment the line below
        // adjList[j].push_back(i);
    }

    bool isEdge(int i, int j) {
        for (int neighbor : adjList[i]) {
            if (neighbor == j)
                return true;
        }
        return false;
    }
};
```

1. **Edge List**:
   - In an edge list, you represent the graph as a list of edges, where each edge is represented as a pair of vertices.
   - This representation is simple and memory-efficient for very sparse graphs.
   - However, operations like checking if there is an edge between two vertices or finding all neighbors of a vertex can be less efficient compared to the adjacency list.

```cpp
#include <vector>
#include <utility>
using namespace std;

class Graph {
private:
    int V;
    vector<pair<int, int>> edgeList;

public:
    Graph(int vertices) : V(vertices) {}

    void addEdge(int i, int j) {
        edgeList.push_back({i, j});
        // For undirected graph, uncomment the line below
        // edgeList.push_back({j, i});
    }

    bool isEdge(int i, int j) {
        for (auto edge : edgeList) {
            if (edge.first == i && edge.second == j)
                return true;
            // For undirected graph, uncomment the line below
            // if (edge.first == j && edge.second == i)
            //     return true;
        }
        return false;
    }
};
```

Choose the representation based on your requirements regarding memory usage, ease of implementation, and the specific operations you'll be performing frequently on the graph.

### 1. Algorithms & Data Structures (C++): Representing of Graphs:  Adjacency Matrix

Sure! In C++, an adjacency matrix is a common way to represent a graph. It's a 2D array where each cell (i, j) represents whether there is an edge from vertex i to vertex j. Here's an example of how you can implement an adjacency matrix for a graph:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
private:
    int numVertices;
    vector<vector<int>> adjMatrix;

public:
    Graph(int numVertices) {
        this->numVertices = numVertices;
        // Initialize the adjacency matrix with all zeros
        adjMatrix.resize(numVertices, vector<int>(numVertices, 0));
    }

    void addEdge(int src, int dest) {
        // Since it's an undirected graph, edges are symmetric
        adjMatrix[src][dest] = 1;
        adjMatrix[dest][src] = 1;
    }

    void printAdjMatrix() {
        cout << "Adjacency Matrix:" << endl;
        for (int i = 0; i < numVertices; ++i) {
            for (int j = 0; j < numVertices; ++j) {
                cout << adjMatrix[i][j] << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph graph(5);

    // Add some edges
    graph.addEdge(0, 1);
    graph.addEdge(0, 4);
    graph.addEdge(1, 2);
    graph.addEdge(1, 3);
    graph.addEdge(1, 4);
    graph.addEdge(2, 3);
    graph.addEdge(3, 4);

    // Print the adjacency matrix
    graph.printAdjMatrix();

    return 0;
}
```

In this implementation:

- The `Graph` class represents an undirected graph using an adjacency matrix.
- The `addEdge` function adds an edge between two vertices by setting the corresponding cells in the matrix to 1.
- The `printAdjMatrix` function simply prints out the adjacency matrix.
- In the `main` function, we create a graph with 5 vertices, add some edges, and then print the adjacency matrix.

### 1. Algorithms & Data Structures (C++): Representing of Graphs: Adjacency List

Representing graphs using an adjacency list is a common approach in computer science and is particularly efficient for sparse graphs (graphs where the number of edges is much less than the maximum number of edges). In C++, you can represent an adjacency list using various data structures such as vectors, lists, or maps. Here's a basic implementation using vectors of lists:

```cpp
#include <iostream>
#include <vector>
#include <list>

using namespace std;

class Graph {
    int V; // Number of vertices
    vector

<int, list<int>> adjList;

public:
    Graph(int vertices) : V(vertices) {
        // Resize the adjacency list to accommodate 'V' vertices
        adjList.resize(V);
    }

    // Function to add an edge from vertex 'src' to vertex 'dest'
    void addEdge(int src, int dest) {
        // Assuming the graph is undirected, add edges in both directions
        adjList[src].push_back(dest);
        adjList[dest].push_back(src);
    }

    // Function to print the adjacency list representation of the graph
    void printAdjList() {
        for (int i = 0; i < V; ++i) {
            cout << "Adjacency list of vertex " << i << ": ";
            for (int neighbor : adjList[i]) {
                cout << neighbor << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph g(5);

    // Add some edges
    g.addEdge(0, 1);
    g.addEdge(0, 4);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 3);
    g.addEdge(3, 4);

    // Print the adjacency list
    g.printAdjList();

    return 0;
}
```

In this implementation:

- The class `Graph` represents the graph structure.
- `V` holds the number of vertices in the graph.
- `adjList` is a vector of lists where each index `i` corresponds to a vertex, and `adjList[i]` contains the list of vertices adjacent to vertex `i`.
- The `addEdge` function adds an edge between two vertices by pushing their respective indices into each other's adjacency lists.
- The `printAdjList` function simply prints out the adjacency list representation of the graph.

This implementation is suitable for representing an undirected graph. If you want to represent a directed graph, you would only push the destination vertex to the adjacency list of the source vertex in the `addEdge` function.

### 1. Algorithms & Data Structures (C++): Ring MST

A Ring Minimum Spanning Tree (Ring MST) is a variation of the Minimum Spanning Tree problem where the resultant tree forms a ring, meaning it has a cycle of length equal to the number of vertices in the graph. A spanning tree is a subset of the edges of a connected, edge-weighted graph that connects all the vertices together without any cycles and with the minimum possible total edge weight.

Implementing a Ring MST algorithm typically involves modifying an existing MST algorithm to ensure that the resulting spanning tree forms a ring. One common algorithm used for finding MSTs is Kruskal's algorithm or Prim's algorithm. Here's a high-level approach to modifying Kruskal's algorithm for Ring MST:

1. Run Kruskal's algorithm to find the Minimum Spanning Tree (MST) of the given graph.
2. After obtaining the MST, check if it forms a ring.
3. If the MST doesn't form a ring, add the minimum weight edge that completes the ring while avoiding creating cycles.
4. Return the resultant ring MST.

Below is a simplified implementation of Kruskal's algorithm in C++ along with modifications to ensure that the resultant tree forms a ring:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Data structure to represent a graph edge
struct Edge {
    int src, dest, weight;
};

// Data structure to represent a graph
class Graph {
public:
    vector<Edge> edges; // array to store graph edges
    int V; // number of vertices

    // Constructor
    Graph(int V) {
        this->V = V;
    }

    // Function to add an edge to the graph
    void addEdge(int src, int dest, int weight) {
        edges.push_back({src, dest, weight});
    }

    // Kruskal's algorithm to find MST
    vector<Edge> kruskalMST() {
        vector<Edge> result;

        // Sort all the edges in non-decreasing order of their weight
        sort(edges.begin(), edges.end(), [](const Edge& a, const Edge& b) {
            return a.weight < b.weight;
        });

        // Create disjoint sets
        vector<int> parent(V, -1);

        int edgeCount = 0;
        int i = 0;
        // Number of edges to be taken is equal to V-1
        while (edgeCount < V - 1 && i < edges.size()) {
            Edge next_edge = edges[i++];

            // Find root endpoints of the current edge
            int x = find(parent, next_edge.src);
            int y = find(parent, next_edge.dest);

            // If including this edge does't cause cycle, include it
            if (x != y) {
                result.push_back(next_edge);
                unionSet(parent, x, y);
                edgeCount++;
            }
        }

        return result;
    }

private:
    // Find set of an element i
    int find(vector<int>& parent, int i) {
        if (parent[i] == -1)
            return i;
        return find(parent, parent[i]);
    }

    // Perform union of two subsets
    void unionSet(vector<int>& parent, int x, int y) {
        int xset = find(parent, x);
        int yset = find(parent, y);
        parent[xset] = yset;
    }
};

// Function to check if the MST forms a ring
bool formsRingMST(const Graph& g, const vector<Edge>& mst) {
    // A spanning tree with V vertices has exactly V-1 edges
    if (mst.size() != g.V - 1)
        return false;

    // Check if the MST contains any vertex with degree > 2
    vector<int> degree(g.V, 0);
    for (const auto& edge : mst) {
        degree[edge.src]++;
        degree[edge.dest]++;
    }
    for (int d : degree) {
        if (d > 2)
            return false;
    }

    return true;
}

// Function to find the minimum weight edge that completes the ring
Edge findMinWeightEdge(const Graph& g, const vector<Edge>& mst) {
    // Initialize minimum weight to infinity
    Edge minEdge = {-1, -1, INT_MAX};

    // Iterate through all edges not present in MST
    for (const auto& edge : g.edges) {
        if (find(mst.begin(), mst.end(), edge) == mst.end()) {
            // Update minEdge if weight of current edge is less than minEdge
            if (edge.weight < minEdge.weight)
                minEdge = edge;
        }
    }

    return minEdge;
}

// Function to convert MST to ring MST
vector<Edge> convertToRingMST(const Graph& g, const vector<Edge>& mst) {
    if (!formsRingMST(g, mst)) {
        // Find the minimum weight edge that completes the ring
        Edge minEdge = findMinWeightEdge(g, mst);

        // Add the minimum weight edge to MST to complete the ring
        vector<Edge> ringMST = mst;
        ringMST.push_back(minEdge);
        return ringMST;
    }
    return mst;
}

int main() {
    // Create a graph
    int V = 4;
    Graph g(V);

    // Add edges
    g.addEdge(0, 1, 10);
    g.addEdge(0, 2, 6);
    g.addEdge(0, 3, 5);
    g.addEdge(1, 3, 15);
    g.addEdge(2, 3, 4);

    // Find MST
    vector<Edge> mst = g.kruskalMST();

    // Convert MST to Ring MST
    vector<Edge> ringMST = convertToRingMST(g, mst);

    // Output the edges of the Ring MST
    cout << "Edges of the Ring MST:\n";
    for (const auto& edge : ringMST) {
        cout << edge.src << " - " << edge.dest << " : " << edge.weight << "\n";
    }

    return 0;
}
```

This code demonstrates a basic implementation of Kruskal's algorithm to find the MST of a given graph, followed by modifications to ensure the resultant tree forms a ring.

### 1. Algorithms & Data Structures (C++): SCC Theory

SCC (Strongly Connected Components) theory is a fundamental concept in graph theory and algorithms, especially in the context of directed graphs. In simple terms, SCC refers to subsets of vertices in a directed graph where every vertex in the subset is reachable from every other vertex in the same subset.

Here's an overview of SCC theory and how it's relevant in algorithms and data structures:

### Definition

1. **Strongly Connected Component (SCC):** In a directed graph, an SCC is a maximal set of vertices such that there is a directed path from any vertex to any other vertex in the same set.

### Algorithmic Importance

1. **Kosaraju's Algorithm:** One of the classic algorithms for finding SCCs in a directed graph. It has a time complexity of O(V + E) where V is the number of vertices and E is the number of edges.

2. **Tarjan's Algorithm:** Another algorithm used for finding SCCs. It's based on depth-first search (DFS) and has a similar time complexity to Kosaraju's algorithm.

### Applications

1. **Graph Analysis:** SCCs help in understanding the underlying structure of directed graphs. They can reveal important patterns and relationships within the data.

2. **Component-based Systems:** SCCs are used in systems where components need to interact with each other. For example, in a network, SCCs can represent clusters of interconnected nodes.

3. **Compiler Design:** SCCs play a crucial role in compiler optimizations and code generation. They help in analyzing the flow of control within the program.

### Implementation in C++

Here's a high-level overview of how you can implement Kosaraju's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <stack>
#include <algorithm>

using namespace std;

// Depth-first search for the first pass
void dfs1(vector<vector<int>>& adj, int v, vector<bool>& visited, stack<int>& s) {
    visited[v] = true;
    for (int u : adj[v]) {
        if (!visited[u])
            dfs1(adj, u, visited, s);
    }
    s.push(v);
}

// Depth-first search for the second pass
void dfs2(vector<vector<int>>& adj, int v, vector<bool>& visited) {
    visited[v] = true;
    // Here, you can process the vertices in the SCC
    for (int u : adj[v]) {
        if (!visited[u])
            dfs2(adj, u, visited);
    }
}

// Kosaraju's Algorithm
void kosaraju(vector<vector<int>>& adj, int V) {
    vector<bool> visited(V, false);
    stack<int> s;

    // First pass: fill stack with the finishing times
    for (int i = 0; i < V; ++i) {
        if (!visited[i])
            dfs1(adj, i, visited, s);
    }

    // Transpose the graph
    vector<vector<int>> transpose(V);
    for (int i = 0; i < V; ++i) {
        for (int j : adj[i])
            transpose[j].push_back(i);
    }

    // Second pass: process vertices in order defined by stack
    fill(visited.begin(), visited.end(), false);
    while (!s.empty()) {
        int v = s.top();
        s.pop();
        if (!visited[v]) {
            dfs2(transpose, v, visited);
            // Here, you can output or process the SCC
            cout << endl;
        }
    }
}

int main() {
    int V, E;
    cout << "Enter the number of vertices and edges: ";
    cin >> V >> E;

    vector<vector<int>> adj(V);
    cout << "Enter the edges (format: source destination):" << endl;
    for (int i = 0; i < E; ++i) {
        int u, v;
        cin >> u >> v;
        adj[u].push_back(v);
    }

    kosaraju(adj, V);

    return 0;
}
```

### Conclusion

Understanding SCC theory and algorithms is crucial for various applications involving directed graphs. Whether it's for analyzing networks, optimizing compilers, or designing component-based systems, SCCs provide valuable insights into the structure and connectivity of directed graphs. Implementing algorithms like Kosaraju's or Tarjan's can be an enriching exercise to deepen your understanding of graph algorithms in C++.

### 1. Algorithms & Data Structures (C++): Shortest Grid Path

To implement the shortest path algorithm for a grid in C++, you can use Breadth-First Search (BFS) or Dijkstra's algorithm. Here's a simple implementation using BFS:

```cpp
#include <iostream>
#include <queue>
#include <vector>
#include <utility>

using namespace std;

const int MAXN = 1005; // Maximum grid size

int dr[] = {1, -1, 0, 0}; // Possible movements: down, up, right, left
int dc[] = {0, 0, 1, -1};

int shortestPath(vector<vector<char>>& grid, pair<int, int> start, pair<int, int> end) {
    int rows = grid.size();
    int cols = grid[0].size();
    vector<vector<bool>> visited(rows, vector<bool>(cols, false));

    queue<pair<pair<int, int>, int>> q;
    q.push({start, 0}); // Start with the initial position and distance 0
    visited[start.first][start.second] = true;

    while (!q.empty()) {
        pair<pair<int, int>, int> current = q.front();
        q.pop();
        int r = current.first.first;
        int c = current.first.second;
        int dist = current.second;

        if (r == end.first && c == end.second) // If we reach the destination
            return dist;

        // Check all possible moves
        for (int i = 0; i < 4; ++i) {
            int nr = r + dr[i];
            int nc = c + dc[i];
            if (nr >= 0 && nr < rows && nc >= 0 && nc < cols && grid[nr][nc] != '#' && !visited[nr][nc]) {
                q.push({{nr, nc}, dist + 1});
                visited[nr][nc] = true;
            }
        }
    }

    return -1; // If destination is unreachable
}

int main() {
    int rows, cols;
    cin >> rows >> cols; // Input the grid size
    vector<vector<char>> grid(rows, vector<char>(cols));

    // Input the grid
    for (int i = 0; i < rows; ++i)
        for (int j = 0; j < cols; ++j)
            cin >> grid[i][j];

    pair<int, int> start, end;
    cin >> start.first >> start.second; // Input the start position
    cin >> end.first >> end.second;     // Input the end position

    int shortestDistance = shortestPath(grid, start, end);
    cout << "Shortest distance from start to end: " << shortestDistance << endl;

    return 0;
}
```

In this code:

- The grid is represented by a 2D vector of characters.
- '#' represents obstacles, and other characters represent open paths.
- The `shortestPath` function takes the grid, starting point, and ending point as input and returns the shortest distance from the starting point to the ending point.
- BFS is used to explore all possible paths from the starting point until the destination is reached.
- We keep track of visited cells to avoid revisiting them.
- The main function reads input for the grid, start, and end positions, then calls `shortestPath` and prints the result.

You can modify the code according to your requirements and input format.

### 1. Algorithms & Data Structures (C++): Shortest Path

Shortest path algorithms are fundamental in computer science and are used in various applications such as network routing, GPS navigation, and even in games. There are several algorithms to find the shortest path in a graph, each with its own characteristics and use cases. In C++, you can implement these algorithms using different data structures like arrays, linked lists, priority queues, or even custom data structures depending on the requirements of the problem.

Here's a brief overview of some popular shortest path algorithms:

1. **Dijkstra's Algorithm**: This algorithm finds the shortest path from a source vertex to all other vertices in a weighted graph with non-negative edge weights. It uses a priority queue to greedily select the vertex with the smallest distance from the source and updates the distances to adjacent vertices.

2. **Bellman-Ford Algorithm**: Unlike Dijkstra's algorithm, Bellman-Ford can handle graphs with negative edge weights, but it is slower. It iterates over all edges multiple times, relaxing them to find the shortest path. It can also detect negative cycles.

3. **Floyd-Warshall Algorithm**: This algorithm finds the shortest paths between all pairs of vertices in a weighted graph. It works for both positive and negative edge weights (but no negative cycles). It uses dynamic programming to build a matrix of shortest distances.

4. **A* Search Algorithm**: A* is a best-first search algorithm that finds the shortest path from a start node to a goal node in a graph, using a heuristic function to guide the search. It combines the benefits of Dijkstra's algorithm and greedy search.

5. **Bidirectional Search**: This is not exactly an algorithm but a technique to find the shortest path between two vertices by simultaneously performing a forward search from the source vertex and a backward search from the destination vertex, meeting in the middle.

Implementing these algorithms involves understanding the underlying principles and data structures involved. In C++, you might use classes and structs to represent graphs and vertices, and standard library containers like vectors, sets, maps, or priority queues to manage data efficiently.

Would you like more details on any specific algorithm or its implementation in C++?

### 1. Algorithms & Data Structures (C++): Shortest Path Algorithm

Certainly! One of the most commonly used algorithms for finding the shortest path in a graph is Dijkstra's algorithm. It works well for graphs with non-negative edge weights. Here's an overview of how it works and an implementation in C++:

### Dijkstra's Algorithm Overview

1. **Initialization**:
   - Assign a distance value to every vertex in the graph. Initialize all distances as INFINITE and assign distance 0 to the source vertex.
   - Create a set that will hold vertices that are being processed. Initially, this set is empty.

2. **While the set is not empty**:
   - Extract the vertex with the minimum distance from the set. Let's call this vertex `u`.
   - For every vertex `v` adjacent to `u`:
     - If the distance of `v` can be improved by going through `u`, update the distance of `v`.
     - If `v` is not in the set, add it.

3. **Repeat step 2** until the set is empty or the destination vertex is extracted.

### Implementation in C++

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>

using namespace std;

const int INF = numeric_limits<int>::max();

// Graph represented as adjacency list
class Graph {
    int V; // Number of vertices

    // Pair of vertex and its corresponding weight
    typedef pair<int, int> iPair;
    vector<vector<iPair>> adj;

public:
    Graph(int V);
    void addEdge(int u, int v, int w);
    void shortestPath(int src);
};

Graph::Graph(int V) {
    this->V = V;
    adj.resize(V);
}

void Graph::addEdge(int u, int v, int w) {
    adj[u].push_back(make_pair(v, w));
    adj[v].push_back(make_pair(u, w)); // For undirected graph
}

void Graph::shortestPath(int src) {
    // Create a priority queue to store vertices that are being processed
    priority_queue<iPair, vector<iPair>, greater<iPair>> pq;

    // Create a vector for distances initialized to INF
    vector<int> dist(V, INF);

    // Insert source vertex into the priority queue and set its distance to 0
    pq.push(make_pair(0, src));
    dist[src] = 0;

    while (!pq.empty()) {
        int u = pq.top().second;
        pq.pop();

        // Visit all adjacent vertices of u
        for (auto& neighbor : adj[u]) {
            int v = neighbor.first;
            int weight = neighbor.second;

            // If there is a shorter path to v through u
            if (dist[v] > dist[u] + weight) {
                // Update distance of v
                dist[v] = dist[u] + weight;
                pq.push(make_pair(dist[v], v));
            }
        }
    }

    // Print the distances
    cout << "Shortest distances from source vertex " << src << ":\n";
    for (int i = 0; i < V; ++i) {
        cout << "Vertex " << i << ": ";
        if (dist[i] == INF)
            cout << "INF\n";
        else
            cout << dist[i] << endl;
    }
}

int main() {
    int V = 6;
    Graph g(V);

    // Example graph
    g.addEdge(0, 1, 4);
    g.addEdge(0, 2, 3);
    g.addEdge(1, 2, 1);
    g.addEdge(1, 3, 2);
    g.addEdge(2, 3, 4);
    g.addEdge(3, 4, 2);
    g.addEdge(4, 5, 6);

    int source = 0;
    g.shortestPath(source);

    return 0;
}
```

This implementation finds the shortest paths from a given source vertex to all other vertices in the graph. You can adjust the `addEdge` function to construct your graph and then call `shortestPath` with the desired source vertex.

### 1. Algorithms & Data Structures (C++): Shortest Path Algorithms

Shortest path algorithms are essential in computer science for solving various problems related to finding the shortest route between nodes in a graph. Here, we will cover some of the most widely used shortest path algorithms, focusing on their implementation and usage in C++.

### Common Shortest Path Algorithms

1. **Dijkstra's Algorithm**
2. **Bellman-Ford Algorithm**
3. **Floyd-Warshall Algorithm**
4. **A* Search Algorithm**

### Dijkstra's Algorithm

**Purpose:** Finds the shortest path from a source node to all other nodes in a weighted graph with non-negative weights.

**Steps:**

1. Initialize the distance to the source node as 0 and to all other nodes as infinity.
2. Use a priority queue to keep track of the next node with the shortest tentative distance.
3. Continuously extract the node with the minimum distance from the priority queue and update the distances to its neighbors.

**C++ Implementation:**

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <climits>

using namespace std;

typedef pair<int, int> pii; // pair: (distance, vertex)

vector<int> dijkstra(int V, vector<vector<pii>>& adj, int source) {
    priority_queue<pii, vector<pii>, greater<pii>> pq;
    vector<int> dist(V, INT_MAX);
    pq.push({0, source});
    dist[source] = 0;

    while (!pq.empty()) {
        int u = pq.top().second;
        pq.pop();

        for (auto& neighbor : adj[u]) {
            int v = neighbor.first;
            int weight = neighbor.second;

            if (dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
                pq.push({dist[v], v});
            }
        }
    }
    return dist;
}

int main() {
    int V = 5;
    vector<vector<pii>> adj(V);
    adj[0].push_back({1, 10});
    adj[0].push_back({4, 5});
    adj[1].push_back({2, 1});
    adj[1].push_back({4, 2});
    adj[2].push_back({3, 4});
    adj[3].push_back({2, 6});
    adj[4].push_back({1, 3});
    adj[4].push_back({2, 9});
    adj[4].push_back({3, 2});

    vector<int> distances = dijkstra(V, adj, 0);

    for (int i = 0; i < V; ++i) {
        cout << "Distance from 0 to " << i << " is " << distances[i] << endl;
    }
    return 0;
}
```

### Bellman-Ford Algorithm

**Purpose:** Finds the shortest paths from a source node to all other nodes in a weighted graph, even with negative weights.

**Steps:**

1. Initialize the distance to the source node as 0 and to all other nodes as infinity.
2. Relax all edges V-1 times, where V is the number of vertices.
3. Check for negative weight cycles by performing a final relaxation step.

**C++ Implementation:**

```cpp
#include <iostream>
#include <vector>
#include <climits>

using namespace std;

struct Edge {
    int src, dest, weight;
};

vector<int> bellmanFord(int V, vector<Edge>& edges, int source) {
    vector<int> dist(V, INT_MAX);
    dist[source] = 0;

    for (int i = 1; i <= V - 1; ++i) {
        for (auto& edge : edges) {
            if (dist[edge.src] != INT_MAX && dist[edge.src] + edge.weight < dist[edge.dest]) {
                dist[edge.dest] = dist[edge.src] + edge.weight;
            }
        }
    }

    for (auto& edge : edges) {
        if (dist[edge.src] != INT_MAX && dist[edge.src] + edge.weight < dist[edge.dest]) {
            cout << "Graph contains negative weight cycle" << endl;
            return {};
        }
    }
    return dist;
}

int main() {
    int V = 5;
    vector<Edge> edges = {
        {0, 1, -1}, {0, 2, 4}, {1, 2, 3}, {1, 3, 2},
        {1, 4, 2}, {3, 2, 5}, {3, 1, 1}, {4, 3, -3}
    };

    vector<int> distances = bellmanFord(V, edges, 0);

    for (int i = 0; i < V; ++i) {
        cout << "Distance from 0 to " << i << " is " << distances[i] << endl;
    }
    return 0;
}
```

### Floyd-Warshall Algorithm

**Purpose:** Computes shortest paths between all pairs of vertices in a weighted graph.

**Steps:**

1. Initialize the distance matrix with edge weights, setting the diagonal to 0.
2. Update the matrix using the formula: if `dist[i][j] > dist[i][k] + dist[k][j]`, then `dist[i][j] = dist[i][k] + dist[k][j]`.

**C++ Implementation:**

```cpp
#include <iostream>
#include <vector>
#include <climits>

using namespace std;

void floydWarshall(vector<vector<int>>& graph) {
    int V = graph.size();
    vector<vector<int>> dist = graph;

    for (int k = 0; k < V; ++k) {
        for (int i = 0; i < V; ++i) {
            for (int j = 0; j < V; ++j) {
                if (dist[i][k] != INT_MAX && dist[k][j] != INT_MAX && dist[i][k] + dist[k][j] < dist[i][j]) {
                    dist[i][j] = dist[i][k] + dist[k][j];
                }
            }
        }
    }

    for (int i = 0; i < V; ++i) {
        for (int j = 0; j < V; ++j) {
            if (dist[i][j] == INT_MAX)
                cout << "INF ";
            else
                cout << dist[i][j] << " ";
        }
        cout << endl;
    }
}

int main() {
    vector<vector<int>> graph = {
        {0, 3, INT_MAX, 7},
        {8, 0, 2, INT_MAX},
        {5, INT_MAX, 0, 1},
        {2, INT_MAX, INT_MAX, 0}
    };

    floydWarshall(graph);

    return 0;
}
```

### A* Search Algorithm

**Purpose:** Finds the shortest path between a start node and a goal node using heuristics to guide the search.

**Steps:**

1. Initialize the open set with the start node.
2. Continuously extract the node with the lowest `f` value (`f = g + h`, where `g` is the cost to reach the node and `h` is the heuristic estimate to the goal).
3. Update the neighbors' costs and add them to the open set if they have not been evaluated or a shorter path is found.

**C++ Implementation:**

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <cmath>
#include <climits>
#include <tuple>

using namespace std;

typedef pair<int, int> pii;

int heuristic(pii a, pii b) {
    return abs(a.first - b.first) + abs(a.second - b.second);
}

vector<pii> aStar(vector<vector<int>>& grid, pii start, pii goal) {
    int rows = grid.size();
    int cols = grid[0].size();
    vector<vector<int>> g(rows, vector<int>(cols, INT_MAX));
    vector<vector<int>> f(rows, vector<int>(cols, INT_MAX));
    vector<vector<pii>> came_from(rows, vector<pii>(cols, {-1, -1}));
    priority_queue<tuple<int, int, int>, vector<tuple<int, int, int>>, greater<tuple<int, int, int>>> openSet;

    g[start.first][start.second] = 0;
    f[start.first][start.second] = heuristic(start, goal);
    openSet.push({f[start.first][start.second], start.first, start.second});

    while (!openSet.empty()) {
        auto [current_f, x, y] = openSet.top();
        openSet.pop();

        if (make_pair(x, y) == goal) {
            vector<pii> path;
            for (pii at = goal; at != make_pair(-1, -1); at = came_from[at.first][at.second]) {
                path.push_back(at);
            }
            reverse(path.begin(), path.end());
            return path;
        }

        vector<pii> neighbors = {{x - 1, y}, {x + 1, y}, {x, y - 1}, {x, y + 1}};
        for (auto& neighbor : neighbors) {
            int nx = neighbor.first, ny = neighbor.second;
            if (nx >= 0 && ny >= 0 && nx < rows && ny < cols && grid[nx][ny] == 0) {
                int tentative_g = g[x][y] + 1;
                if (tentative_g

 < g[nx][ny]) {
                    came_from[nx][ny] = {x, y};
                    g[nx][ny] = tentative_g;
                    f[nx][ny] = g[nx][ny] + heuristic({nx, ny}, goal);
                    openSet.push({f[nx][ny], nx, ny});
                }
            }
        }
    }

    return {}; // Return an empty path if no path is found
}

int main() {
    vector<vector<int>> grid = {
        {0, 1, 0, 0, 0},
        {0, 1, 0, 1, 0},
        {0, 0, 0, 1, 0},
        {0, 1, 1, 1, 0},
        {0, 0, 0, 0, 0}
    };

    pii start = {0, 0};
    pii goal = {4, 4};

    vector<pii> path = aStar(grid, start, goal);

    if (!path.empty()) {
        cout << "Path found:" << endl;
        for (auto& p : path) {
            cout << "(" << p.first << ", " << p.second << ") ";
        }
        cout << endl;
    } else {
        cout << "No path found." << endl;
    }

    return 0;
}
```

### Conclusion

Each of these algorithms has its own use cases and complexities:

- **Dijkstra's Algorithm** is efficient for graphs with non-negative weights.
- **Bellman-Ford Algorithm** handles graphs with negative weights and detects negative weight cycles.
- **Floyd-Warshall Algorithm** computes shortest paths between all pairs of nodes and is useful for dense graphs.
- **A* Search Algorithm** is suitable for pathfinding on grids or maps where heuristic guidance can significantly speed up the search.

When implementing these algorithms, choosing the right one depends on the specific requirements and constraints of your problem domain.

### 1. Algorithms & Data Structures (C++): Shortest Path by Topological Sort

Using topological sorting to find the shortest path in a directed acyclic graph (DAG) is a classic algorithmic technique. The basic idea is to perform a topological sort on the graph, then relax each edge in topological order. This ensures that when you relax an edge (u, v), node u has already been processed, guaranteeing that the shortest path to u has been found before considering v.

Here's a high-level overview of how you can implement this algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>

using namespace std;

const int INF = numeric_limits<int>::max();

// Directed edge
struct Edge {
    int to, weight;
    Edge(int t, int w) : to(t), weight(w) {}
};

// Graph represented using adjacency list
class Graph {
    int V; // Number of vertices
    vector<vector<Edge>> adj;

public:
    Graph(int V) : V(V), adj(V) {}

    // Add directed edge
    void addEdge(int from, int to, int weight) {
        adj[from].emplace_back(to, weight);
    }

    // Topological sort
    void topologicalSortUtil(int v, vector<bool>& visited, stack<int>& stack) {
        visited[v] = true;
        for (const auto& edge : adj[v]) {
            if (!visited[edge.to])
                topologicalSortUtil(edge.to, visited, stack);
        }
        stack.push(v);
    }

    vector<int> shortestPath(int src) {
        stack<int> stack;
        vector<bool> visited(V, false);

        // Perform topological sort
        for (int i = 0; i < V; ++i) {
            if (!visited[i])
                topologicalSortUtil(i, visited, stack);
        }

        // Initialize distances to all vertices as infinite and
        // distance to source as 0
        vector<int> dist(V, INF);
        dist[src] = 0;

        // Process vertices in topological order
        while (!stack.empty()) {
            int u = stack.top();
            stack.pop();

            // Update distances to all adjacent vertices of the popped vertex
            for (const auto& edge : adj[u]) {
                int v = edge.to;
                int weight = edge.weight;
                if (dist[u] != INF && dist[u] + weight < dist[v]) {
                    dist[v] = dist[u] + weight;
                }
            }
        }

        return dist;
    }
};

int main() {
    int V, E; // Number of vertices and edges
    cin >> V >> E;

    Graph graph(V);

    // Input format: from to weight
    for (int i = 0; i < E; ++i) {
        int from, to, weight;
        cin >> from >> to >> weight;
        graph.addEdge(from, to, weight);
    }

    int src; // Source vertex
    cin >> src;

    vector<int> shortestDistances = graph.shortestPath(src);

    // Output shortest distances from source vertex
    cout << "Shortest distances from vertex " << src << ":\n";
    for (int i = 0; i < V; ++i) {
        cout << "Vertex " << i << ": ";
        if (shortestDistances[i] == INF)
            cout << "INF\n";
        else
            cout << shortestDistances[i] << "\n";
    }

    return 0;
}
```

In this code:

- The `Edge` struct represents a directed edge with a destination vertex `to` and a weight.
- The `Graph` class represents the graph using an adjacency list and provides methods to add edges and compute the shortest path.
- The `topologicalSortUtil` function performs a depth-first search (DFS) traversal and pushes vertices onto a stack based on their finishing times.
- The `shortestPath` function first performs topological sorting, then iterates over the vertices in topological order and relaxes all outgoing edges.
- The `main` function reads the input graph and source vertex, then prints the shortest distances from the source vertex to all other vertices.

### 1. Algorithms & Data Structures (C++): Shortest Path Dijkstra's Algorithm

Dijkstra's algorithm is a classic algorithm used to find the shortest paths between nodes in a graph, which may represent, for example, road networks or computer networks. Here's a basic implementation of Dijkstra's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>

using namespace std;

#define INF numeric_limits<int>::max()

// Define a structure to represent a weighted edge
struct Edge {
    int to;
    int weight;
    Edge(int t, int w) : to(t), weight(w) {}
};

// Define a function to perform Dijkstra's algorithm
vector<int> dijkstra(vector<vector<Edge>>& graph, int start) {
    int n = graph.size();
    vector<int> dist(n, INF); // Initialize distances with infinity
    dist[start] = 0; // Distance from start node to itself is 0

    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    pq.push({0, start}); // Push the start node into the priority queue

    while (!pq.empty()) {
        int u = pq.top().second;
        int d = pq.top().first;
        pq.pop();

        // If we've already found a shorter path to u, continue
        if (d > dist[u]) continue;

        // Explore neighbors of u
        for (const Edge& e : graph[u]) {
            int v = e.to;
            int w = e.weight;
            if (dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;
                pq.push({dist[v], v});
            }
        }
    }

    return dist;
}

int main() {
    int n = 5; // Number of nodes
    vector<vector<Edge>> graph(n);

    // Add edges to the graph
    graph[0].push_back(Edge(1, 10));
    graph[0].push_back(Edge(2, 5));
    graph[1].push_back(Edge(2, 2));
    graph[1].push_back(Edge(3, 1));
    graph[2].push_back(Edge(1, 3));
    graph[2].push_back(Edge(3, 9));
    graph[2].push_back(Edge(4, 2));
    graph[3].push_back(Edge(4, 4));
    graph[4].push_back(Edge(3, 6));

    int startNode = 0; // Starting node for Dijkstra's algorithm

    vector<int> shortestDistances = dijkstra(graph, startNode);

    // Output the shortest distances from the start node
    for (int i = 0; i < n; ++i) {
        cout << "Shortest distance from node " << startNode << " to node " << i << " is " << shortestDistances[i] << endl;
    }

    return 0;
}
```

This code demonstrates Dijkstra's algorithm on a sample graph represented as an adjacency list. You can modify the `graph` variable to represent your own graph, and adjust `startNode` accordingly. This algorithm will find the shortest paths from the `startNode` to all other nodes in the graph.

### 1. Algorithms & Data Structures (C++): Shortest Path In A Weighted Graph: Greedy Algorithm

The shortest path problem in a weighted graph involves finding the shortest path between two vertices, where the edges have associated weights. One approach to solve this problem is using greedy algorithms. In this context, Dijkstra's algorithm is a well-known and widely-used greedy algorithm.

Dijkstra's algorithm works by iteratively selecting the vertex with the shortest distance from the source vertex that has not yet been visited. Here's a basic outline of how Dijkstra's algorithm works:

1. Initialize distances: Assign a distance value to every vertex in the graph. Initialize the distance of the source vertex to 0 and all other vertices to infinity.
2. Mark all vertices as unvisited.
3. Repeat the following until all vertices are visited:
   a. Select the unvisited vertex with the smallest distance from the source vertex. This vertex is now considered visited.
   b. For the selected vertex, update the distance of its neighboring vertices by adding the weight of the edge connecting the current vertex to each neighboring vertex. If this new distance is shorter than the previously known distance, update the distance.
4. Continue until all vertices are visited or until the destination vertex is reached.

Here's a simple implementation of Dijkstra's algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>

using namespace std;

#define INF numeric_limits<int>::max()

// Function to perform Dijkstra's algorithm
void dijkstra(vector<vector<pair<int, int>>>& graph, int source, vector<int>& distances) {
    int V = graph.size();
    distances.assign(V, INF);
    vector<bool> visited(V, false);
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;

    distances[source] = 0;
    pq.push({0, source});

    while (!pq.empty()) {
        int u = pq.top().second;
        pq.pop();

        if (visited[u])
            continue;

        visited[u] = true;

        for (auto& neighbor : graph[u]) {
            int v = neighbor.first;
            int weight = neighbor.second;

            if (!visited[v] && distances[u] + weight < distances[v]) {
                distances[v] = distances[u] + weight;
                pq.push({distances[v], v});
            }
        }
    }
}

int main() {
    int V, E; // Number of vertices and edges
    cin >> V >> E;

    vector<vector<pair<int, int>>> graph(V); // Adjacency list representation of the graph

    // Reading edges
    for (int i = 0; i < E; ++i) {
        int u, v, w; // Edge from u to v with weight w
        cin >> u >> v >> w;
        graph[u].push_back({v, w});
        // If the graph is undirected, you might also want to add this line:
        // graph[v].push_back({u, w});
    }

    int source; // Source vertex
    cin >> source;

    vector<int> distances; // Stores shortest distances from the source vertex
    dijkstra(graph, source, distances);

    // Output shortest distances from the source vertex
    cout << "Shortest distances from vertex " << source << ":\n";
    for (int i = 0; i < V; ++i) {
        cout << "Vertex " << i << ": ";
        if (distances[i] == INF)
            cout << "INF";
        else
            cout << distances[i];
        cout << endl;
    }

    return 0;
}
```

This code demonstrates Dijkstra's algorithm for finding the shortest path from a source vertex to all other vertices in a weighted graph. Make sure to represent your graph appropriately using an adjacency list or adjacency matrix. Additionally, adjust the input and output methods as per your requirements.

### 1. Algorithms & Data Structures (C++): Shortest Path In An Unweighted Graph: The Distance Table

In an unweighted graph, finding the shortest path from a source vertex to all other vertices can be efficiently done using BFS (Breadth-First Search). The distance table stores the shortest distance from the source vertex to each vertex in the graph.

Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

// Function to perform BFS and fill the distance table
void shortestPath(vector<vector<int>>& graph, int source, vector<int>& distance) {
    int n = graph.size();
    vector<bool> visited(n, false);
    queue<int> q;

    // Mark source vertex as visited and enqueue it
    visited[source] = true;
    q.push(source);
    distance[source] = 0;

    while (!q.empty()) {
        int u = q.front();
        q.pop();

        // Visit all adjacent vertices of u
        for (int v : graph[u]) {
            // If v is not visited yet, mark it visited, enqueue it,
            // and update its distance from the source
            if (!visited[v]) {
                visited[v] = true;
                q.push(v);
                distance[v] = distance[u] + 1;
            }
        }
    }
}

int main() {
    // Example graph represented as an adjacency list
    vector<vector<int>> graph = {
        {1, 3},     // Adjacent vertices of vertex 0
        {0, 2, 3},  // Adjacent vertices of vertex 1
        {1, 4},     // Adjacent vertices of vertex 2
        {0, 1, 4},  // Adjacent vertices of vertex 3
        {2, 3}      // Adjacent vertices of vertex 4
    };

    int source = 0; // Source vertex

    // Initialize distance table with a large value (infinity)
    vector<int> distance(graph.size(), INT_MAX);

    // Compute shortest paths from the source vertex
    shortestPath(graph, source, distance);

    // Print the distance table
    cout << "Distance Table from vertex " << source << ":\n";
    for (int i = 0; i < graph.size(); ++i) {
        cout << "Vertex " << i << ": " << distance[i] << " units\n";
    }

    return 0;
}
```

In this code:

- `shortestPath` function performs BFS on the graph starting from the source vertex and fills the distance table.
- `main` function demonstrates the usage of the `shortestPath` function with an example graph represented as an adjacency list. It initializes the distance table with infinity and prints the distance from the source vertex to all other vertices.

You can modify the graph as per your requirement and test the code.

### 1. Algorithms & Data Structures (C++): Shortest Path using Breadth First Search

Sure, implementing the shortest path using Breadth First Search (BFS) in C++ is a common and useful technique. Here's a basic example of how you can do it:

```cpp
#include <iostream>
#include <queue>
#include <vector>
#include <climits>

using namespace std;

// Structure to represent a graph edge
struct Edge {
    int src, dest;
};

class Graph {
    int V; // Number of vertices
    vector<vector<int>> adjList; // Adjacency list representation of graph

public:
    Graph(int vertices) {
        V = vertices;
        adjList.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int src, int dest) {
        adjList[src].push_back(dest);
        adjList[dest].push_back(src); // For undirected graph
    }

    // Function to find the shortest path from source to all other vertices using BFS
    vector<int> shortestPath(int source) {
        vector<int> dist(V, INT_MAX); // Initialize distances with infinity
        dist[source] = 0; // Distance from source to itself is 0

        queue<int> q;
        q.push(source);

        while (!q.empty()) {
            int u = q.front();
            q.pop();

            // Visit all adjacent vertices of u
            for (int v : adjList[u]) {
                if (dist[v] == INT_MAX) { // If v is not visited
                    dist[v] = dist[u] + 1;
                    q.push(v);
                }
            }
        }

        return dist;
    }
};

int main() {
    // Create a graph
    Graph g(6);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(2, 3);
    g.addEdge(3, 4);
    g.addEdge(2, 5);
    g.addEdge(4, 5);

    // Find shortest paths from source vertex 0
    vector<int> shortestDistances = g.shortestPath(0);

    // Output the shortest distances from source to all vertices
    cout << "Shortest distances from source vertex 0:\n";
    for (int i = 0; i < shortestDistances.size(); ++i) {
        cout << "Vertex " << i << ": " << shortestDistances[i] << endl;
    }

    return 0;
}
```

In this code:

- `Graph` is a class representing an undirected graph using adjacency lists.
- `addEdge` function adds edges to the graph.
- `shortestPath` function calculates the shortest distance from a given source vertex to all other vertices using BFS.
- `main` function demonstrates the usage by creating a graph, adding some edges, and finding the shortest paths from a chosen source vertex.

You can modify this code to suit your specific needs, such as changing the graph structure or implementing other functionalities related to graphs and BFS.

### 1. Algorithms & Data Structures (C++): Shortest Paths

Shortest path algorithms are fundamental in graph theory and have many practical applications, such as in routing, network optimization, and more. In C++, several algorithms can be implemented to find the shortest path in a graph. Here, we will cover some of the most commonly used algorithms: Dijkstra's algorithm, Bellman-Ford algorithm, and Floyd-Warshall algorithm.

### 1. Dijkstra's Algorithm

Dijkstra's algorithm finds the shortest path from a single source node to all other nodes in a graph with non-negative edge weights. It uses a priority queue to repeatedly select the node with the smallest known distance.

#### Implementation

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <climits>

using namespace std;

typedef pair<int, int> pii; // (distance, vertex)

// Function to implement Dijkstra's Algorithm
void dijkstra(vector<vector<pii>>& graph, int src) {
    int V = graph.size();
    vector<int> dist(V, INT_MAX);
    priority_queue<pii, vector<pii>, greater<pii>> pq;
    
    dist[src] = 0;
    pq.push({0, src});
    
    while (!pq.empty()) {
        int u = pq.top().second;
        pq.pop();
        
        for (auto& edge : graph[u]) {
            int v = edge.first;
            int weight = edge.second;
            
            if (dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
                pq.push({dist[v], v});
            }
        }
    }
    
    // Output the distances
    for (int i = 0; i < V; ++i) {
        cout << "Distance from " << src << " to " << i << " is " << dist[i] << endl;
    }
}

int main() {
    int V = 5;
    vector<vector<pii>> graph(V);
    
    // Adding edges (u, v, w)
    graph[0].push_back({1, 10});
    graph[0].push_back({4, 5});
    graph[1].push_back({2, 1});
    graph[1].push_back({4, 2});
    graph[2].push_back({3, 4});
    graph[3].push_back({0, 7});
    graph[4].push_back({1, 3});
    graph[4].push_back({2, 9});
    graph[4].push_back({3, 2});
    
    dijkstra(graph, 0);

    return 0;
}
```

### 2. Bellman-Ford Algorithm

The Bellman-Ford algorithm computes shortest paths from a single source node to all other nodes in a graph, and it can handle graphs with negative edge weights. It uses a relaxation technique and iterates over all edges.

#### Implementation

```cpp
#include <iostream>
#include <vector>
#include <climits>

using namespace std;

struct Edge {
    int src, dest, weight;
};

// Function to implement Bellman-Ford Algorithm
void bellmanFord(vector<Edge>& edges, int V, int src) {
    vector<int> dist(V, INT_MAX);
    dist[src] = 0;

    for (int i = 1; i < V; ++i) {
        for (auto& edge : edges) {
            if (dist[edge.src] != INT_MAX && dist[edge.src] + edge.weight < dist[edge.dest]) {
                dist[edge.dest] = dist[edge.src] + edge.weight;
            }
        }
    }

    // Check for negative-weight cycles
    for (auto& edge : edges) {
        if (dist[edge.src] != INT_MAX && dist[edge.src] + edge.weight < dist[edge.dest]) {
            cout << "Graph contains negative weight cycle" << endl;
            return;
        }
    }

    // Output the distances
    for (int i = 0; i < V; ++i) {
        cout << "Distance from " << src << " to " << i << " is " << dist[i] << endl;
    }
}

int main() {
    int V = 5;
    vector<Edge> edges;
    
    // Adding edges (u, v, w)
    edges.push_back({0, 1, -1});
    edges.push_back({0, 2, 4});
    edges.push_back({1, 2, 3});
    edges.push_back({1, 3, 2});
    edges.push_back({1, 4, 2});
    edges.push_back({3, 2, 5});
    edges.push_back({3, 1, 1});
    edges.push_back({4, 3, -3});
    
    bellmanFord(edges, V, 0);

    return 0;
}
```

### 3. Floyd-Warshall Algorithm

The Floyd-Warshall algorithm finds shortest paths between all pairs of nodes. It works with both positive and negative weights (but no negative cycles) and uses a dynamic programming approach.

#### Implementation

```cpp
#include <iostream>
#include <vector>

using namespace std;

#define INF INT_MAX

// Function to implement Floyd-Warshall Algorithm
void floydWarshall(vector<vector<int>>& graph) {
    int V = graph.size();
    vector<vector<int>> dist = graph;

    for (int k = 0; k < V; ++k) {
        for (int i = 0; i < V; ++i) {
            for (int j = 0; j < V; ++j) {
                if (dist[i][k] != INF && dist[k][j] != INF && dist[i][k] + dist[k][j] < dist[i][j]) {
                    dist[i][j] = dist[i][k] + dist[k][j];
                }
            }
        }
    }

    // Output the distances
    for (int i = 0; i < V; ++i) {
        for (int j = 0; j < V; ++j) {
            if (dist[i][j] == INF) {
                cout << "INF ";
            } else {
                cout << dist[i][j] << " ";
            }
        }
        cout << endl;
    }
}

int main() {
    int V = 4;
    vector<vector<int>> graph = {
        {0, 5, INF, 10},
        {INF, 0, 3, INF},
        {INF, INF, 0, 1},
        {INF, INF, INF, 0}
    };
    
    floydWarshall(graph);

    return 0;
}
```

### Summary

- **Dijkstra's Algorithm**: Efficient for graphs with non-negative weights and provides shortest paths from a single source.
- **Bellman-Ford Algorithm**: Handles graphs with negative weights and detects negative weight cycles.
- **Floyd-Warshall Algorithm**: Computes shortest paths between all pairs of nodes and handles graphs with both positive and negative weights (without negative cycles).

Each algorithm has its own use case and complexity characteristics, making them suitable for different scenarios in computing shortest paths in graphs.

### 1. Algorithms & Data Structures (C++): Shortest Paths Algorithms

Shortest paths algorithms are a fundamental topic in algorithms and data structures, particularly for problems involving weighted graphs. They aim to find the minimum path or distance from a source node to a target node (or to all nodes) in a weighted graph. Here are some key algorithms for finding shortest paths in C++:

### 1. Dijkstra's Algorithm

**Purpose**: Finds the shortest path from a single source to all other nodes in a graph with non-negative weights.

**Complexity**: O((V + E) log V), where V is the number of vertices and E is the number of edges (using a priority queue).

**Steps**:

1. Initialize distances from the source to all vertices as infinite, except the source itself, which is set to 0.
2. Use a priority queue to select the vertex with the smallest distance.
3. Update the distances to its neighbors.
4. Repeat until all vertices are processed.

**C++ Implementation**:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>
using namespace std;

typedef pair<int, int> iPair;

void dijkstra(const vector<vector<iPair>>& adj, int src) {
    priority_queue<iPair, vector<iPair>, greater<iPair>> pq;
    int V = adj.size();
    vector<int> dist(V, numeric_limits<int>::max());

    pq.push(make_pair(0, src));
    dist[src] = 0;

    while (!pq.empty()) {
        int u = pq.top().second;
        pq.pop();

        for (auto& x : adj[u]) {
            int v = x.first;
            int weight = x.second;

            if (dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
                pq.push(make_pair(dist[v], v));
            }
        }
    }

    for (int i = 0; i < V; ++i)
        cout << "Vertex " << i << " Distance from Source: " << dist[i] << endl;
}

int main() {
    int V = 5;
    vector<vector<iPair>> adj(V);

    adj[0].push_back(make_pair(1, 9));
    adj[0].push_back(make_pair(2, 6));
    adj[0].push_back(make_pair(3, 5));
    adj[0].push_back(make_pair(4, 3));

    adj[2].push_back(make_pair(1, 2));
    adj[2].push_back(make_pair(3, 4));

    dijkstra(adj, 0);

    return 0;
}
```

### 2. Bellman-Ford Algorithm

**Purpose**: Finds shortest paths from a single source to all vertices, and can handle graphs with negative weights.

**Complexity**: O(VE), where V is the number of vertices and E is the number of edges.

**Steps**:

1. Initialize distances from the source to all vertices as infinite, except the source itself, which is set to 0.
2. Relax all edges V-1 times.
3. Check for negative-weight cycles.

**C++ Implementation**:

```cpp
#include <iostream>
#include <vector>
#include <limits>
using namespace std;

struct Edge {
    int src, dest, weight;
};

void bellmanFord(const vector<Edge>& edges, int V, int src) {
    vector<int> dist(V, numeric_limits<int>::max());
    dist[src] = 0;

    for (int i = 1; i <= V - 1; ++i) {
        for (const auto& edge : edges) {
            int u = edge.src;
            int v = edge.dest;
            int weight = edge.weight;

            if (dist[u] != numeric_limits<int>::max() && dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
            }
        }
    }

    for (const auto& edge : edges) {
        int u = edge.src;
        int v = edge.dest;
        int weight = edge.weight;

        if (dist[u] != numeric_limits<int>::max() && dist[u] + weight < dist[v]) {
            cout << "Graph contains negative weight cycle" << endl;
            return;
        }
    }

    for (int i = 0; i < V; ++i)
        cout << "Vertex " << i << " Distance from Source: " << dist[i] << endl;
}

int main() {
    int V = 5;
    vector<Edge> edges = {
        {0, 1, -1}, {0, 2, 4},
        {1, 2, 3}, {1, 3, 2}, {1, 4, 2},
        {3, 2, 5}, {3, 1, 1},
        {4, 3, -3}
    };

    bellmanFord(edges, V, 0);

    return 0;
}
```

### 3. Floyd-Warshall Algorithm

**Purpose**: Finds shortest paths between all pairs of vertices.

**Complexity**: O(V^3), where V is the number of vertices.

**Steps**:

1. Initialize the distance matrix with direct edge weights or infinity where there is no edge.
2. Update the distance matrix considering each vertex as an intermediate point.

**C++ Implementation**:

```cpp
#include <iostream>
#include <vector>
using namespace std;

const int INF = 1e7;

void floydWarshall(vector<vector<int>>& graph) {
    int V = graph.size();
    vector<vector<int>> dist = graph;

    for (int k = 0; k < V; ++k) {
        for (int i = 0; i < V; ++i) {
            for (int j = 0; j < V; ++j) {
                if (dist[i][k] + dist[k][j] < dist[i][j])
                    dist[i][j] = dist[i][k] + dist[k][j];
            }
        }
    }

    for (int i = 0; i < V; ++i) {
        for (int j = 0; j < V; ++j) {
            if (dist[i][j] == INF)
                cout << "INF ";
            else
                cout << dist[i][j] << " ";
        }
        cout << endl;
    }
}

int main() {
    vector<vector<int>> graph = {
        {0, 3, INF, 5},
        {2, 0, INF, 4},
        {INF, 1, 0, INF},
        {INF, INF, 2, 0}
    };

    floydWarshall(graph);

    return 0;
}
```

These algorithms cover a range of scenarios for shortest path problems and can be implemented efficiently using C++. Understanding the trade-offs in complexity and suitability for different types of graphs (e.g., presence of negative weights, dense vs. sparse graphs) is key to choosing the appropriate algorithm.

### 1. Algorithms & Data Structures (C++): Shortest Paths in Graph

Shortest path algorithms are fundamental in graph theory and have numerous applications in various fields like network routing, transportation, and even gaming. In C++, you can implement several algorithms to find the shortest path in a graph. The two most common algorithms are Dijkstra's algorithm and the Bellman-Ford algorithm. Here's a brief overview of both:

1. **Dijkstra's Algorithm**: This algorithm finds the shortest path from a starting node to all other nodes in a weighted graph with non-negative edge weights. It maintains a priority queue to select the next node to visit based on the shortest known distance from the starting node. The algorithm continues until all nodes have been visited or the destination node has been reached.

   ```cpp
   #include <iostream>
   #include <vector>
   #include <queue>
   #include <limits>

   using namespace std;

   const int INF = numeric_limits<int>::max();

   void dijkstra(vector<vector<pair<int, int>>>& graph, int start, vector<int>& dist) {
       priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
       dist[start] = 0;
       pq.push({0, start});

       while (!pq.empty()) {
           int u = pq.top().second;
           int d = pq.top().first;
           pq.pop();

           if (d > dist[u]) continue;

           for (auto& edge : graph[u]) {
               int v = edge.first;
               int w = edge.second;
               if (dist[u] + w < dist[v]) {
                   dist[v] = dist[u] + w;
                   pq.push({dist[v], v});
               }
           }
       }
   }

   int main() {
       int n, m; // Number of nodes and edges
       cin >> n >> m;

       vector<vector<pair<int, int>>> graph(n);
       for (int i = 0; i < m; ++i) {
           int u, v, w; // Edge from u to v with weight w
           cin >> u >> v >> w;
           graph[u].push_back({v, w});
           graph[v].push_back({u, w}); // Remove this line for directed graphs
       }

       int start; // Starting node
       cin >> start;

       vector<int> dist(n, INF);
       dijkstra(graph, start, dist);

       for (int i = 0; i < n; ++i) {
           if (dist[i] != INF) {
               cout << "Shortest distance from " << start << " to " << i << " is " << dist[i] << endl;
           } else {
               cout << "No path from " << start << " to " << i << endl;
           }
       }

       return 0;
   }
   ```

2. **Bellman-Ford Algorithm**: This algorithm can handle graphs with negative edge weights and detects negative cycles. It iterates over all edges multiple times, relaxing them to find the shortest paths.

   ```cpp
   #include <iostream>
   #include <vector>
   #include <limits>

   using namespace std;

   const int INF = numeric_limits<int>::max();

   struct Edge {
       int src, dest, weight;
   };

   void bellmanFord(vector<Edge>& edges, int V, int start) {
       vector<int> dist(V, INF);
       dist[start] = 0;

       for (int i = 0; i < V - 1; ++i) {
           for (auto& edge : edges) {
               int u = edge.src;
               int v = edge.dest;
               int w = edge.weight;
               if (dist[u] != INF && dist[u] + w < dist[v]) {
                   dist[v] = dist[u] + w;
               }
           }
       }

       // Check for negative cycles
       for (auto& edge : edges) {
           int u = edge.src;
           int v = edge.dest;
           int w = edge.weight;
           if (dist[u] != INF && dist[u] + w < dist[v]) {
               cout << "Graph contains negative cycle\n";
               return;
           }
       }

       for (int i = 0; i < V; ++i) {
           if (dist[i] != INF) {
               cout << "Shortest distance from " << start << " to " << i << " is " << dist[i] << endl;
           } else {
               cout << "No path from " << start << " to " << i << endl;
           }
       }
   }

   int main() {
       int V, E; // Number of vertices and edges
       cin >> V >> E;

       vector<Edge> edges(E);
       for (int i = 0; i < E; ++i) {
           cin >> edges[i].src >> edges[i].dest >> edges[i].weight;
       }

       int start; // Starting node
       cin >> start;

       bellmanFord(edges, V, start);

       return 0;
   }
   ```

Both algorithms have their advantages and use cases. Dijkstra's algorithm is generally faster for graphs with non-negative edge weights, while Bellman-Ford is more versatile as it can handle negative edge weights and detect negative cycles.

### 1. Algorithms & Data Structures (C++): Single Source Shortest Path

Single Source Shortest Path (SSSP) is a fundamental problem in graph theory, where the objective is to find the shortest paths from a given source vertex to all other vertices in a weighted graph. In C++, this problem can be addressed using various algorithms depending on the nature of the graph (e.g., whether it has negative weights, is directed, or undirected). Here are some common algorithms used to solve the SSSP problem:

### 1. Dijkstra's Algorithm

Dijkstra's algorithm is efficient for graphs with non-negative weights. It uses a priority queue to repeatedly extract the vertex with the minimum distance and update the distances of its adjacent vertices.

#### Implementation using C++

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <utility>
#include <limits>

using namespace std;

const int INF = numeric_limits<int>::max();

void dijkstra(int source, vector<vector<pair<int, int>>> &adjList, vector<int> &dist) {
    int n = adjList.size();
    dist.assign(n, INF);
    dist[source] = 0;

    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    pq.push({0, source});

    while (!pq.empty()) {
        int u = pq.top().second;
        int d = pq.top().first;
        pq.pop();

        if (d != dist[u]) continue;

        for (auto &edge : adjList[u]) {
            int v = edge.first;
            int weight = edge.second;

            if (dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
                pq.push({dist[v], v});
            }
        }
    }
}

int main() {
    int V = 5;
    vector<vector<pair<int, int>>> adjList(V);

    adjList[0].push_back({1, 10});
    adjList[0].push_back({4, 3});
    adjList[1].push_back({2, 2});
    adjList[1].push_back({4, 4});
    adjList[2].push_back({3, 9});
    adjList[3].push_back({2, 7});
    adjList[4].push_back({1, 1});
    adjList[4].push_back({2, 8});
    adjList[4].push_back({3, 2});

    vector<int> dist;
    dijkstra(0, adjList, dist);

    for (int i = 0; i < V; ++i) {
        cout << "Distance from 0 to " << i << " is " << dist[i] << endl;
    }

    return 0;
}
```

### 2. Bellman-Ford Algorithm

Bellman-Ford algorithm works with graphs that may have negative weights. It is capable of detecting negative weight cycles.

#### Implementation using C++

```cpp
#include <iostream>
#include <vector>
#include <utility>
#include <limits>

using namespace std;

const int INF = numeric_limits<int>::max();

bool bellmanFord(int source, int V, vector<vector<pair<int, int>>> &edges, vector<int> &dist) {
    dist.assign(V, INF);
    dist[source] = 0;

    for (int i = 1; i < V; ++i) {
        for (auto &edge : edges) {
            int u = edge[0].first;
            int v = edge[0].second;
            int weight = edge[1].first;
            if (dist[u] != INF && dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
            }
        }
    }

    for (auto &edge : edges) {
        int u = edge[0].first;
        int v = edge[0].second;
        int weight = edge[1].first;
        if (dist[u] != INF && dist[u] + weight < dist[v]) {
            return false;  // Negative weight cycle detected
        }
    }

    return true;
}

int main() {
    int V = 5;
    vector<vector<pair<int, int>>> edges = {
        {{0, 1}, {10}},
        {{0, 4}, {3}},
        {{1, 2}, {2}},
        {{1, 4}, {4}},
        {{2, 3}, {9}},
        {{3, 2}, {7}},
        {{4, 1}, {1}},
        {{4, 2}, {8}},
        {{4, 3}, {2}}
    };

    vector<int> dist;
    if (bellmanFord(0, V, edges, dist)) {
        for (int i = 0; i < V; ++i) {
            cout << "Distance from 0 to " << i << " is " << dist[i] << endl;
        }
    } else {
        cout << "Negative weight cycle detected!" << endl;
    }

    return 0;
}
```

### 3. Floyd-Warshall Algorithm

Floyd-Warshall is an all-pairs shortest path algorithm but can be adapted for SSSP by focusing on a specific source. It works with graphs that have negative weights but no negative weight cycles.

#### Simplified for SSSP (just for illustration, not typically used this way)

```cpp
#include <iostream>
#include <vector>
#include <limits>

using namespace std;

const int INF = numeric_limits<int>::max();

void floydWarshall(int source, int V, vector<vector<int>> &dist) {
    for (int k = 0; k < V; ++k) {
        for (int i = 0; i < V; ++i) {
            for (int j = 0; j < V; ++j) {
                if (dist[i][k] < INF && dist[k][j] < INF) {
                    dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j]);
                }
            }
        }
    }

    for (int i = 0; i < V; ++i) {
        cout << "Distance from " << source << " to " << i << " is " << dist[source][i] << endl;
    }
}

int main() {
    int V = 4;
    vector<vector<int>> dist = {
        {0, 3, INF, 5},
        {2, 0, INF, 4},
        {INF, 1, 0, INF},
        {INF, INF, 2, 0}
    };

    floydWarshall(0, V, dist);

    return 0;
}
```

### Summary

- **Dijkstra's Algorithm** is best for non-negative weight graphs.
- **Bellman-Ford Algorithm** handles graphs with negative weights and detects negative weight cycles.
- **Floyd-Warshall Algorithm** is generally used for all-pairs shortest path but can be adapted for SSSP.

Each algorithm has its own use cases, strengths, and weaknesses, making them suitable for different types of graphs and requirements.

### 1. Algorithms & Data Structures (C++): Single Source Shortest Path Problem (SSSPP)

The Single Source Shortest Path Problem (SSSPP) is a fundamental problem in graph theory, where the goal is to find the shortest paths from a given source vertex to all other vertices in a weighted graph. Here, we'll discuss two classic algorithms used to solve the SSSPP: Dijkstra's algorithm and the Bellman-Ford algorithm, both of which are commonly implemented in C++.

### 1. Dijkstra's Algorithm

Dijkstra's algorithm is an efficient algorithm for finding the shortest paths from a single source vertex to all other vertices in a graph with non-negative edge weights. It uses a priority queue to greedily select the next vertex with the smallest tentative distance.

#### Implementation Steps

1. **Initialize Distances**: Set the distance to the source vertex to 0 and all other vertices to infinity.
2. **Priority Queue**: Use a min-heap (priority queue) to keep track of vertices to be processed.
3. **Relaxation**: For each vertex, update the distances to its neighbors if a shorter path is found.

#### C++ Code

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <utility>
#include <limits>

using namespace std;

typedef pair<int, int> pii;

void dijkstra(int source, vector<vector<pii>>& adj) {
    int n = adj.size();
    vector<int> dist(n, numeric_limits<int>::max());
    dist[source] = 0;

    priority_queue<pii, vector<pii>, greater<pii>> pq;
    pq.push({0, source});

    while (!pq.empty()) {
        int u = pq.top().second;
        pq.pop();

        for (auto& edge : adj[u]) {
            int v = edge.first;
            int weight = edge.second;

            if (dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
                pq.push({dist[v], v});
            }
        }
    }

    for (int i = 0; i < n; ++i) {
        cout << "Distance from source " << source << " to vertex " << i << " is " << dist[i] << endl;
    }
}

int main() {
    int n, m;
    cin >> n >> m;

    vector<vector<pii>> adj(n);
    for (int i = 0; i < m; ++i) {
        int u, v, w;
        cin >> u >> v >> w;
        adj[u].push_back({v, w});
        adj[v].push_back({u, w}); // If the graph is undirected
    }

    int source;
    cin >> source;

    dijkstra(source, adj);

    return 0;
}
```

### 2. Bellman-Ford Algorithm

The Bellman-Ford algorithm is capable of handling graphs with negative edge weights and can detect negative weight cycles. It works by relaxing all edges up to \( V-1 \) times, where \( V \) is the number of vertices.

#### Implementation Steps

1. **Initialize Distances**: Set the distance to the source vertex to 0 and all other vertices to infinity.
2. **Relaxation**: Iterate \( V-1 \) times, relaxing all edges.
3. **Check for Negative Cycles**: Check for negative weight cycles by performing one more relaxation round.

#### C++ Code

```cpp
#include <iostream>
#include <vector>
#include <limits>

using namespace std;

struct Edge {
    int u, v, weight;
};

void bellman_ford(int source, int n, vector<Edge>& edges) {
    vector<int> dist(n, numeric_limits<int>::max());
    dist[source] = 0;

    for (int i = 0; i < n - 1; ++i) {
        for (const Edge& edge : edges) {
            if (dist[edge.u] != numeric_limits<int>::max() && dist[edge.u] + edge.weight < dist[edge.v]) {
                dist[edge.v] = dist[edge.u] + edge.weight;
            }
        }
    }

    for (const Edge& edge : edges) {
        if (dist[edge.u] != numeric_limits<int>::max() && dist[edge.u] + edge.weight < dist[edge.v]) {
            cout << "Graph contains a negative weight cycle" << endl;
            return;
        }
    }

    for (int i = 0; i < n; ++i) {
        cout << "Distance from source " << source << " to vertex " << i << " is " << dist[i] << endl;
    }
}

int main() {
    int n, m;
    cin >> n >> m;

    vector<Edge> edges(m);
    for (int i = 0; i < m; ++i) {
        cin >> edges[i].u >> edges[i].v >> edges[i].weight;
    }

    int source;
    cin >> source;

    bellman_ford(source, n, edges);

    return 0;
}
```

### Key Differences

- **Dijkstra's Algorithm**: Efficient for graphs with non-negative weights, has a time complexity of \( O((V + E) \log V) \) with a priority queue.
- **Bellman-Ford Algorithm**: Handles negative weights and detects negative weight cycles, with a time complexity of \( O(VE) \).

Both algorithms are essential for solving SSSPP in different types of graphs and have their specific use cases and limitations.

### 1. Algorithms & Data Structures (C++): Solution - Shortest Grid Path

Certainly! Here's a C++ solution for finding the shortest path in a grid using Breadth-First Search (BFS) algorithm:

```cpp
#include <iostream>
#include <queue>
#include <vector>
#include <utility>

using namespace std;

// Define direction vectors (right, down, left, up)
const int dx[] = {1, 0, -1, 0};
const int dy[] = {0, 1, 0, -1};

// Function to check if a cell is valid
bool isValid(int x, int y, int n, int m, vector<vector<bool>>& visited) {
    return x >= 0 && x < n && y >= 0 && y < m && !visited[x][y];
}

// Function to find the shortest path in a grid
int shortestPath(vector<vector<char>>& grid) {
    int n = grid.size();
    int m = grid[0].size();
    
    // Initialize visited array
    vector<vector<bool>> visited(n, vector<bool>(m, false));

    // Initialize queue for BFS
    queue<pair<int, int>> q;

    // Start BFS from top-left corner
    q.push({0, 0});
    visited[0][0] = true;
    int steps = 0;

    while (!q.empty()) {
        int sz = q.size();
        for (int i = 0; i < sz; ++i) {
            auto [x, y] = q.front();
            q.pop();

            // If reached the bottom-right cell, return steps
            if (x == n - 1 && y == m - 1)
                return steps;

            // Explore all possible directions
            for (int j = 0; j < 4; ++j) {
                int newX = x + dx[j];
                int newY = y + dy[j];

                // Check if the new cell is valid and not visited
                if (isValid(newX, newY, n, m, visited) && grid[newX][newY] != '#') {
                    q.push({newX, newY});
                    visited[newX][newY] = true;
                }
            }
        }
        // Increment steps after exploring all cells at current level
        steps++;
    }

    // If the bottom-right cell is not reachable
    return -1;
}

int main() {
    // Example usage
    vector<vector<char>> grid = {
        {'S', '.', '.', '#', '.', '.', '.'},
        {'.', '#', '.', '.', '.', '#', '.'},
        {'.', '#', '.', '.', '.', '.', '.'},
        {'.', '.', '#', '#', '.', '.', '.'},
        {'#', '.', '#', 'E', '.', '#', '.'}
    };

    int shortest = shortestPath(grid);
    if (shortest == -1)
        cout << "No path found!";
    else
        cout << "Shortest path length: " << shortest << endl;

    return 0;
}
```

In this solution:

- We perform a Breadth-First Search (BFS) traversal of the grid.
- We keep track of visited cells to avoid revisiting them.
- We use a queue to explore neighboring cells in a breadth-first manner.
- We stop when we reach the bottom-right cell and return the number of steps taken to reach it.
- If the bottom-right cell is not reachable, we return -1.
- The grid is represented by a 2D vector of characters where 'S' represents the start cell, 'E' represents the end cell, '.' represents an empty cell, and '#' represents an obstacle.

### 1. Algorithms & Data Structures (C++): Solving maze routing problems

Solving maze routing problems involves finding a path from the starting point to the destination within a maze, navigating through obstacles. Here's a high-level approach using C++ and common algorithms and data structures:

1. **Representing the Maze**:
   - You can represent the maze as a 2D grid. Each cell can represent a passage or a wall.
   - Define a data structure to represent the maze. You can use a 2D array or a vector of vectors in C++.

2. **Depth-First Search (DFS)** or **Breadth-First Search (BFS)**:
   - Both DFS and BFS are popular algorithms for traversing graphs.
   - DFS explores as far as possible along each branch before backtracking.
   - BFS explores the neighbor nodes at the current depth before moving on to nodes at the next depth.
   - Choose DFS if you want to explore as deep as possible before backtracking, or BFS if you want to find the shortest path.

3. **Algorithm Steps**:
   - Start from the entrance of the maze.
   - Explore adjacent cells.
   - If a cell is unvisited and accessible, mark it as visited and continue exploration.
   - Repeat until reaching the destination or all accessible cells have been explored.

4. **Backtracking**:
   - When using DFS, if you reach a dead end, backtrack to the last junction and explore another path.
   - Use a stack to keep track of the path during DFS.

5. **Queue for BFS**:
   - Use a queue to implement BFS. When exploring a cell, enqueue its neighboring cells.

6. **Path Finding**:
   - Once you reach the destination, trace back the path from the destination to the start.
   - This can be done by storing the parent of each cell during traversal.

7. **Implementation** (Basic Pseudocode):

```cpp
// Pseudocode for DFS

DFS(maze, start, end):
    stack.push(start)
    while stack is not empty:
        current = stack.top()
        stack.pop()
        if current == end:
            // Path found
            return path
        mark current as visited
        for each neighbor of current:
            if neighbor is accessible and not visited:
                stack.push(neighbor)
                set parent of neighbor to current
    // No path found
    return empty path

// Pseudocode for BFS

BFS(maze, start, end):
    queue.enqueue(start)
    while queue is not empty:
        current = queue.front()
        queue.dequeue()
        if current == end:
            // Path found
            return path
        mark current as visited
        for each neighbor of current:
            if neighbor is accessible and not visited:
                queue.enqueue(neighbor)
                set parent of neighbor to current
    // No path found
    return empty path
```

8. **Optimizations**:
   - Use memoization or dynamic programming to avoid redundant computations.
   - Implement heuristics if you want to use A* search for more efficient pathfinding.

9. **Testing**:
   - Test your implementation with various maze configurations, including mazes with multiple solutions or no solution at all.

10. **Error Handling**:

- Handle cases where the start or end points are invalid, or the maze is not navigable.

By following these steps and using appropriate algorithms and data structures, you can effectively solve maze routing problems in C++.

### 1. Algorithms & Data Structures (C++): Special Paths

Special paths in algorithms and data structures can encompass various concepts, each with its unique characteristics and applications. Here's a rundown of some special paths commonly encountered in algorithms and data structures, along with their definitions and applications:

1. **Shortest Path**:
   - **Definition**: The shortest path between two vertices in a graph is the path with the minimum sum of edge weights.
   - **Algorithms**: Dijkstra's algorithm, Bellman-Ford algorithm, Floyd-Warshall algorithm.
   - **Applications**: Routing in computer networks, GPS navigation, transportation networks optimization.

2. **Longest Path**:
   - **Definition**: The longest path between two vertices in a graph is the path with the maximum sum of edge weights.
   - **Algorithms**: Topological sorting followed by dynamic programming.
   - **Applications**: Critical path analysis, project scheduling, resource allocation.

3. **Minimum Spanning Tree**:
   - **Definition**: A minimum spanning tree of a connected, undirected graph is a subgraph that is a tree and connects all the vertices together with the minimum possible total edge weight.
   - **Algorithms**: Prim's algorithm, Kruskal's algorithm.
   - **Applications**: Network design, clustering, approximation algorithms.

4. **Maximum Flow**:
   - **Definition**: The maximum flow between a source node and a sink node in a flow network is the maximum amount of flow that can be pushed from the source to the sink without violating capacity constraints.
   - **Algorithms**: Ford-Fulkerson algorithm, Edmonds-Karp algorithm, Dinic's algorithm.
   - **Applications**: Network flow optimization, transportation planning, resource allocation.

5. **All Pairs Shortest Paths**:
   - **Definition**: Finding the shortest paths between all pairs of vertices in a graph.
   - **Algorithms**: Floyd-Warshall algorithm, Johnson's algorithm.
   - **Applications**: Path planning in robotics, distance calculation in geographic information systems.

6. **Hamiltonian Path**:
   - **Definition**: A Hamiltonian path is a path in an undirected or directed graph that visits each vertex exactly once.
   - **Algorithms**: Backtracking, dynamic programming.
   - **Applications**: Traveling salesman problem, circuit design, optimization problems.

7. **Eulerian Path**:
   - **Definition**: An Eulerian path is a path in a graph that visits every edge exactly once.
   - **Algorithms**: Fleury's algorithm, Hierholzer's algorithm.
   - **Applications**: Network routing, DNA sequencing, graph theory.

Understanding and efficiently solving problems involving these special paths is crucial in various fields, including computer science, operations research, and engineering.

### 1. Algorithms & Data Structures (C++): Storing Weighted Graphs

Storing weighted graphs efficiently in C++ requires choosing a data structure that balances ease of implementation, memory usage, and computational efficiency for common operations like adding edges, removing edges, and querying edge weights. Two common ways to represent weighted graphs are the adjacency matrix and the adjacency list. Let's delve into both:

1. **Adjacency Matrix**:
   - In an adjacency matrix, you represent the graph as a 2D array. The element at row 'i' and column 'j' represents the weight of the edge between vertex 'i' and vertex 'j'.
   - If there is no edge between vertices 'i' and 'j', you can represent it with a special value (like infinity or -1).
   - This representation is efficient for querying whether there's an edge between two vertices in constant time (`O(1)`), but it consumes `O(V^2)` space, where 'V' is the number of vertices.

2. **Adjacency List**:
   - In an adjacency list, you represent the graph as an array (or vector) of lists (or vectors), where each list corresponds to a vertex, and contains pairs representing adjacent vertices and their corresponding edge weights.
   - This representation is more memory-efficient for sparse graphs because it only uses as much space as needed for the edges present in the graph.
   - However, querying whether there's an edge between two vertices takes `O(V)` time in the worst case, where 'V' is the number of vertices.

For weighted graphs, you can extend these basic representations by augmenting the data structures to store the weights associated with each edge.

Here's a basic implementation using an adjacency list for a weighted graph in C++:

```cpp
#include <iostream>
#include <vector>
#include <utility>

using namespace std;

// Edge structure to represent weighted edges
struct Edge {
    int dest;
    int weight;
};

// Weighted Graph class using adjacency list representation
class WeightedGraph {
private:
    int V; // Number of vertices
    vector<vector<Edge>> adjList; // Adjacency list representation

public:
    WeightedGraph(int vertices) : V(vertices) {
        adjList.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int src, int dest, int weight) {
        Edge edge;
        edge.dest = dest;
        edge.weight = weight;
        adjList[src].push_back(edge);
    }

    // Function to print the adjacency list
    void printGraph() {
        for (int v = 0; v < V; ++v) {
            cout << "Vertex " << v << ":\n";
            for (const Edge& edge : adjList[v]) {
                cout << " -> " << edge.dest << " (weight: " << edge.weight << ")\n";
            }
            cout << endl;
        }
    }
};

int main() {
    WeightedGraph graph(4);
    graph.addEdge(0, 1, 10);
    graph.addEdge(0, 2, 5);
    graph.addEdge(1, 2, 3);
    graph.addEdge(2, 3, 7);
    graph.printGraph();
    return 0;
}
```

This code demonstrates how to represent a weighted graph using an adjacency list and add weighted edges to it. You can extend it further by implementing functions for other common operations on graphs.

### 1. Algorithms & Data Structures (C++): Surrounded Regions

The Surrounded Regions problem is a classic problem in algorithms and data structures. The problem usually involves a 2D grid of characters where some cells are filled with 'X' (representing walls) and some cells are filled with 'O' (representing regions). The task is to capture all regions surrounded by 'X' with 'O'.

Here's a typical approach to solve this problem using depth-first search (DFS) or breadth-first search (BFS) algorithms:

1. First, iterate through the border of the grid. For each 'O' cell found on the border, perform a DFS or BFS to mark all connected 'O' cells as safe (not surrounded by 'X').
2. Next, iterate through the entire grid. For each 'O' cell encountered:
   - If it's marked as safe, leave it as 'O' (not surrounded).
   - If it's not marked as safe, change it to 'X' (surrounded by 'X').

Here's a high-level implementation in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void dfs(vector<vector<char>>& board, int i, int j) {
    int m = board.size();
    int n = board[0].size();

    if (i < 0 || j < 0 || i >= m || j >= n || board[i][j] != 'O')
        return;

    board[i][j] = 'Y'; // Mark as safe temporarily

    // Explore neighboring cells
    dfs(board, i + 1, j);
    dfs(board, i - 1, j);
    dfs(board, i, j + 1);
    dfs(board, i, j - 1);
}

void solve(vector<vector<char>>& board) {
    int m = board.size();
    if (m == 0) return;
    int n = board[0].size();

    // Mark safe cells connected to the border
    for (int i = 0; i < m; ++i) {
        dfs(board, i, 0);          // Left border
        dfs(board, i, n - 1);      // Right border
    }
    for (int j = 0; j < n; ++j) {
        dfs(board, 0, j);          // Top border
        dfs(board, m - 1, j);      // Bottom border
    }

    // Change remaining 'O's to 'X's and revert 'Y's back to 'O's
    for (int i = 0; i < m; ++i) {
        for (int j = 0; j < n; ++j) {
            if (board[i][j] == 'O') board[i][j] = 'X';
            else if (board[i][j] == 'Y') board[i][j] = 'O';
        }
    }
}

// Helper function to print the board
void printBoard(const vector<vector<char>>& board) {
    for (const auto& row : board) {
        for (char cell : row) {
            cout << cell << " ";
        }
        cout << endl;
    }
}

int main() {
    vector<vector<char>> board = {
        {'X', 'X', 'X', 'X'},
        {'X', 'O', 'O', 'X'},
        {'X', 'X', 'O', 'X'},
        {'X', 'O', 'X', 'X'}
    };

    cout << "Original Board:" << endl;
    printBoard(board);

    solve(board);

    cout << "\nSurrounded Regions Board:" << endl;
    printBoard(board);

    return 0;
}
```

This code first marks all the safe 'O' regions connected to the border, then changes the remaining 'O's to 'X's as they are surrounded by 'X's, and finally reverts the temporarily marked 'Y's back to 'O's.

### 1. Algorithms & Data Structures (C++): Surrounded Regions - Graphs

The "Surrounded Regions" problem is a classic algorithmic problem where you're given a 2D board containing 'X's and 'O's. Your task is to capture all regions surrounded by 'X's. A region is captured by flipping all 'O's into 'X's if it's surrounded by 'X's.

To solve this problem efficiently, you can use graph traversal techniques like Depth-First Search (DFS) or Breadth-First Search (BFS). Here's a basic outline of how you can approach this problem using DFS:

1. **Traverse the boundary**: Start traversing the boundary of the board. Whenever you encounter an 'O', perform a DFS from that position to mark all connected 'O's as safe (not surrounded by 'X's). Mark them temporarily as something like 'Y'.

2. **Flip**: After traversing the boundary, iterate through the entire board. For every 'O' encountered, it means it's not connected to the boundary, so flip it to 'X'. And every 'Y' encountered, change it back to 'O' (as it's not surrounded by 'X's).

Here's a sample implementation in C++:

```cpp
#include <vector>

using namespace std;

// Helper function to perform DFS
void dfs(vector<vector<char>>& board, int i, int j) {
    if (i < 0 || i >= board.size() || j < 0 || j >= board[0].size() || board[i][j] != 'O') {
        return;
    }
    board[i][j] = 'Y'; // Mark the 'O' as safe temporarily
    // Explore its neighbors
    dfs(board, i + 1, j);
    dfs(board, i - 1, j);
    dfs(board, i, j + 1);
    dfs(board, i, j - 1);
}

void solve(vector<vector<char>>& board) {
    if (board.empty()) return;
    int rows = board.size();
    int cols = board[0].size();

    // Traverse the boundary and mark connected 'O's as safe
    for (int i = 0; i < rows; ++i) {
        dfs(board, i, 0);            // left side
        dfs(board, i, cols - 1);     // right side
    }
    for (int j = 0; j < cols; ++j) {
        dfs(board, 0, j);            // top side
        dfs(board, rows - 1, j);     // bottom side
    }

    // Flip the 'O's to 'X's and 'Y's back to 'O's
    for (int i = 0; i < rows; ++i) {
        for (int j = 0; j < cols; ++j) {
            if (board[i][j] == 'O') {
                board[i][j] = 'X';
            } else if (board[i][j] == 'Y') {
                board[i][j] = 'O';
            }
        }
    }
}
```

This code performs a DFS traversal starting from the boundary cells, marking all 'O's connected to the boundary as 'Y'. Then, it iterates over the entire board, flipping 'O's to 'X's and 'Y's back to 'O's. This ensures that only 'O's that are not surrounded by 'X's are flipped.

### 1. Algorithms & Data Structures (C++): Terms of Graphs

Sure, here are some fundamental terms related to graphs in the context of algorithms and data structures:

1. **Graph**: A graph is a collection of nodes (vertices) and edges that connect pairs of nodes.

2. **Vertex (Node)**: A vertex or node is a fundamental unit of a graph. It represents an entity, and it can have associated attributes.

3. **Edge (Link)**: An edge or link is a connection between two vertices. It can be directed or undirected and may have associated weights.

4. **Directed Graph (Digraph)**: In a directed graph, edges have a direction, indicating a one-way connection between vertices.

5. **Undirected Graph**: In an undirected graph, edges do not have a direction, and connections between vertices are bidirectional.

6. **Weighted Graph**: A weighted graph is a graph in which each edge has an associated weight or cost.

7. **Adjacency Matrix**: An adjacency matrix is a 2D array used to represent connections between vertices in a graph. Each cell in the matrix represents whether there is an edge between two vertices.

8. **Adjacency List**: An adjacency list is a collection of lists or arrays used to represent connections between vertices. Each vertex in the graph has a list of adjacent vertices.

9. **Degree of a Vertex**: The degree of a vertex is the number of edges incident to it. In a directed graph, the in-degree and out-degree of a vertex represent the number of incoming and outgoing edges, respectively.

10. **Path**: A path in a graph is a sequence of vertices where each adjacent pair is connected by an edge.

11. **Cycle**: A cycle is a path that starts and ends at the same vertex, traversing through a sequence of edges.

12. **Connected Graph**: A connected graph is a graph in which there is a path between every pair of vertices.

13. **Disconnected Graph**: A disconnected graph is a graph that has at least two vertices such that there is no path between them.

14. **Spanning Tree**: A spanning tree of a connected graph is a subgraph that is a tree and includes all the vertices of the original graph.

15. **Topological Sorting**: Topological sorting is the process of arranging the vertices of a directed graph in a linear order such that for every directed edge uv from vertex u to vertex v, u comes before v in the order.

16. **Depth-First Search (DFS)**: DFS is an algorithm for traversing or searching tree or graph data structures. It starts at the root (selecting some arbitrary node as the root in the case of a graph) and explores as far as possible along each branch before backtracking.

17. **Breadth-First Search (BFS)**: BFS is an algorithm for traversing or searching tree or graph data structures. It starts at the root (selecting some arbitrary node as the root in the case of a graph) and explores all of the neighbor vertices at the present depth prior to moving on to the vertices at the next depth level.

These terms provide a foundational understanding of graphs and their associated concepts in the context of algorithms and data structures.

### 1. Algorithms & Data Structures (C++): The Vertex Cover Problem

The Vertex Cover Problem is a classic problem in computer science and graph theory. In this problem, you're given an undirected graph, and the task is to find the smallest set of vertices such that each edge in the graph is incident to at least one vertex in the set. This set of vertices is called the vertex cover of the graph.

Here's a basic approach to solve the Vertex Cover Problem using a simple algorithm:

### Algorithm

1. Start with an empty set `VC` (Vertex Cover).
2. Repeat until all edges are covered:
   a. Pick an uncovered edge `(u, v)`.
   b. Add both `u` and `v` to `VC`.
3. Return `VC` as the minimum vertex cover.

### Implementation in C++

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>

using namespace std;

class Graph {
    int V;
    vector<vector<int>> adj;

public:
    Graph(int V) : V(V) {
        adj.resize(V);
    }

    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u);
    }

    vector<int> findVertexCover() {
        vector<int> vertexCover;
        unordered_set<int> coveredEdges;

        for (int u = 0; u < V; ++u) {
            for (int v : adj[u]) {
                if (coveredEdges.find(v) == coveredEdges.end()) {
                    // Add u and v to the vertex cover
                    vertexCover.push_back(u);
                    vertexCover.push_back(v);
                    coveredEdges.insert(u);
                    coveredEdges.insert(v);
                }
            }
        }

        return vertexCover;
    }
};

int main() {
    Graph g(5);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(3, 4);

    vector<int> vertexCover = g.findVertexCover();

    cout << "Minimum Vertex Cover: ";
    for (int v : vertexCover) {
        cout << v << " ";
    }
    cout << endl;

    return 0;
}
```

This is a basic implementation of the algorithm in C++. You can optimize this algorithm further, especially for larger graphs, using more sophisticated data structures and algorithms like approximation algorithms or dynamic programming.

### 1. Algorithms & Data Structures (C++): Topological Sort

Topological sort is a fundamental algorithm in graph theory used to order the vertices of a directed graph such that for every directed edge from vertex u to vertex v, u comes before v in the ordering. This is applicable only for Directed Acyclic Graphs (DAGs). Here's how you can implement topological sort in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

// Function to perform topological sort
void topologicalSortUtil(int v, vector<int> adj[], vector<bool>& visited, queue<int>& q) {
    visited[v] = true; // Mark current vertex as visited
    // Traverse all adjacent vertices of the current vertex
    for (int u : adj[v]) {
        if (!visited[u]) // If adjacent vertex is not visited, recursively call the function
            topologicalSortUtil(u, adj, visited, q);
    }
    q.push(v); // Push the current vertex to the queue
}

// Function to perform topological sort
void topologicalSort(int V, vector<int> adj[]) {
    vector<bool> visited(V, false); // Initialize all vertices as not visited
    queue<int> q; // Queue to store the topologically sorted order
    // Call the recursive utility function for all vertices one by one
    for (int i = 0; i < V; ++i) {
        if (!visited[i]) // If vertex is not visited, call the utility function
            topologicalSortUtil(i, adj, visited, q);
    }
    // Print the topologically sorted order
    while (!q.empty()) {
        cout << q.front() << " ";
        q.pop();
    }
}

int main() {
    int V = 6; // Number of vertices
    vector<int> adj[V]; // Adjacency list representation of the graph
    // Add edges
    adj[5].push_back(2);
    adj[5].push_back(0);
    adj[4].push_back(0);
    adj[4].push_back(1);
    adj[2].push_back(3);
    adj[3].push_back(1);
    // Perform topological sort
    cout << "Topological Sort: ";
    topologicalSort(V, adj);
    return 0;
}
```

This code will output the topologically sorted order of vertices in the given directed graph. You can adjust the `V` variable and the adjacency list `adj` to fit your specific graph.

### 1. Algorithms & Data Structures (C++): Topological Sort Algorithm

Topological sorting is a technique used to order the vertices of a directed graph such that for every directed edge from vertex u to vertex v, u comes before v in the ordering. This is only possible for Directed Acyclic Graphs (DAGs). A topological ordering doesn't have to be unique; multiple valid orderings can exist for a given DAG.

Here's a basic algorithm for topological sorting using depth-first search (DFS):

1. Perform a DFS traversal of the graph.
2. During the DFS traversal, keep track of vertices in the order they finish exploring (i.e., just before backtracking).
3. Reverse the order obtained from the DFS. This reversed order gives the topological ordering of the vertices.

Here's a C++ implementation of the topological sort algorithm:

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

    // Recursive function for DFS traversal
    void topologicalSortUtil(int v, vector<bool>& visited, stack<int>& stack) {
        visited[v] = true;

        // Recur for all the vertices adjacent to this vertex
        for (int i : adj[v]) {
            if (!visited[i])
                topologicalSortUtil(i, visited, stack);
        }

        // Push current vertex to stack which stores result
        stack.push(v);
    }

public:
    Graph(int V) : V(V), adj(V) {}

    // Function to add an edge to the graph
    void addEdge(int u, int v) {
        adj[u].push_back(v);
    }

    // Function to perform topological sort
    void topologicalSort() {
        stack<int> stack;
        vector<bool> visited(V, false);

        // Call the recursive helper function to store Topological Sort
        // starting from all vertices one by one
        for (int i = 0; i < V; ++i) {
            if (!visited[i])
                topologicalSortUtil(i, visited, stack);
        }

        // Print contents of stack
        while (!stack.empty()) {
            cout << stack.top() << " ";
            stack.pop();
        }
    }
};

int main() {
    Graph g(6);
    g.addEdge(5, 2);
    g.addEdge(5, 0);
    g.addEdge(4, 0);
    g.addEdge(4, 1);
    g.addEdge(2, 3);
    g.addEdge(3, 1);

    cout << "Topological Sort of the given graph is: ";
    g.topologicalSort();

    return 0;
}
```

In this example, we create a graph with 6 vertices and add directed edges between them. Then, we call the `topologicalSort()` function to perform the topological sort and print the result.

### 1. Algorithms & Data Structures (C++): Topological Sort In A Graph

Topological sorting is a way of arranging the vertices of a directed graph such that for every directed edge from vertex A to vertex B, vertex A comes before vertex B in the ordering. This is applicable only for Directed Acyclic Graphs (DAGs). Here's a simple implementation of topological sort in C++ using Depth First Search (DFS):

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

    void topologicalSortUtil(int v, vector<bool>& visited, stack<int>& stack);

public:
    Graph(int V); // Constructor
    void addEdge(int v, int w); // Function to add an edge to graph
    void topologicalSort(); // Prints topological sort of the complete graph
};

Graph::Graph(int V) {
    this->V = V;
    adj.resize(V);
}

void Graph::addEdge(int v, int w) {
    adj[v].push_back(w); // Add w to v's adjacency list
}

// A recursive function used by topologicalSort
void Graph::topologicalSortUtil(int v, vector<bool>& visited, stack<int>& stack) {
    // Mark the current node as visited
    visited[v] = true;

    // Recur for all the vertices adjacent to this vertex
    for (auto i = adj[v].begin(); i != adj[v].end(); ++i)
        if (!visited[*i])
            topologicalSortUtil(*i, visited, stack);

    // Push current vertex to stack which stores result
    stack.push(v);
}

// The function to do Topological Sort. It uses recursive topologicalSortUtil()
void Graph::topologicalSort() {
    stack<int> stack;

    // Mark all the vertices as not visited
    vector<bool> visited(V, false);

    // Call the recursive helper function to store Topological Sort starting from all vertices one by one
    for (int i = 0; i < V; i++)
        if (!visited[i])
            topologicalSortUtil(i, visited, stack);

    // Print contents of stack
    while (!stack.empty()) {
        cout << stack.top() << " ";
        stack.pop();
    }
}

int main() {
    // Create a graph given in the above diagram
    Graph g(6);
    g.addEdge(5, 2);
    g.addEdge(5, 0);
    g.addEdge(4, 0);
    g.addEdge(4, 1);
    g.addEdge(2, 3);
    g.addEdge(3, 1);

    cout << "Topological Sort of the given graph \n";
    g.topologicalSort();

    return 0;
}
```

In this implementation, we use a stack to store the vertices. Once all adjacent vertices of a vertex are visited, we push the vertex onto the stack. Finally, we print the contents of the stack to get the topological order.

Make sure to create a `Graph` object and add edges to it using the `addEdge` method before calling `topologicalSort`. This example illustrates a simple directed acyclic graph and demonstrates the topological sorting of its vertices.

### 1. Algorithms & Data Structures (C++): Transitive closure of a directed graph and Path Matrix

To compute the transitive closure of a directed graph and the path matrix in C++, you can use algorithms like Warshall's algorithm. Here's a brief explanation of the algorithm and its implementation:

#### Warshall's Algorithm

Warshall's algorithm is a classical method for finding the transitive closure of a directed graph. It's based on dynamic programming and works by iteratively updating a matrix representing the reachability between pairs of vertices.

Here's the high-level idea:

1. Initialize a matrix `reach[][]` where `reach[i][j]` will be 1 if vertex `j` is reachable from vertex `i`, and 0 otherwise.
2. Initialize `reach[][]` with the adjacency matrix of the given graph.
3. For each vertex `k`, check if vertex `k` can be reached from vertex `i` and vertex `j` can be reached from vertex `k`. If so, set `reach[i][j]` to 1.
4. After completing the process for all vertices, `reach[][]` will contain the transitive closure of the graph.

#### Implementation

```cpp
#include <iostream>
#include <vector>
using namespace std;

void transitiveClosure(const vector<vector<int>>& graph, vector<vector<int>>& reach) {
    int V = graph.size();

    // Initialize reach[][] with the adjacency matrix of the graph
    for (int i = 0; i < V; ++i) {
        for (int j = 0; j < V; ++j) {
            reach[i][j] = graph[i][j];
        }
    }

    // Compute transitive closure using Warshall's algorithm
    for (int k = 0; k < V; ++k) {
        for (int i = 0; i < V; ++i) {
            for (int j = 0; j < V; ++j) {
                reach[i][j] = reach[i][j] || (reach[i][k] && reach[k][j]);
            }
        }
    }
}

int main() {
    // Example graph represented using adjacency matrix
    vector<vector<int>> graph = {
        {0, 1, 0, 0},
        {0, 0, 0, 1},
        {0, 0, 0, 0},
        {0, 0, 1, 0}
    };
    int V = graph.size();

    // Initialize a matrix to store the transitive closure
    vector<vector<int>> reach(V, vector<int>(V, 0));

    // Compute transitive closure
    transitiveClosure(graph, reach);

    // Output the transitive closure matrix
    cout << "Transitive Closure:\n";
    for (int i = 0; i < V; ++i) {
        for (int j = 0; j < V; ++j) {
            cout << reach[i][j] << " ";
        }
        cout << endl;
    }

    return 0;
}
```

This code initializes a graph and computes its transitive closure using Warshall's algorithm. You can extend this code to also compute the path matrix if needed. The path matrix represents the length of the shortest path between every pair of vertices in the graph.

### 1. Algorithms & Data Structures (C++): Travel by Car

Travel by car involves several algorithms and data structures, especially when considering navigation, route planning, and optimization. Here's a breakdown of how algorithms and data structures come into play:

1. **Graph Representation**: Roads, intersections, and highways can be represented as a graph where nodes represent locations and edges represent roads connecting these locations. This graph can be either directed or undirected depending on the road system.

2. **Graph Search Algorithms**: Algorithms like Dijkstra's algorithm or A* search are commonly used for finding the shortest path between two locations on the road network. These algorithms take into account factors such as distance, time, traffic conditions, and sometimes even user preferences like avoiding toll roads or highways.

3. **Map Data Structures**: Storing and accessing map data efficiently is crucial for navigation systems. Hash tables or balanced binary search trees can be used to store mapping between location names or coordinates and their corresponding graph nodes.

4. **GPS and Sensor Data**: Modern cars are equipped with GPS sensors that provide real-time location data. Algorithms for processing this data, such as Kalman filters for sensor fusion, are essential for accurate positioning and navigation.

5. **Dynamic Programming**: When optimizing routes, dynamic programming techniques can be applied to solve problems like the traveling salesman problem (TSP), where the goal is to find the shortest route that visits a set of locations exactly once and returns to the starting point.

6. **Traffic Prediction**: Machine learning algorithms can analyze historical traffic data to predict future traffic conditions. These predictions can be used to adjust route recommendations in real-time, helping drivers avoid congested areas.

7. **Concurrency and Parallelism**: In some cases, concurrent or parallel algorithms may be used to process large volumes of data efficiently, such as when calculating routes for multiple users simultaneously or when updating navigation instructions in real-time based on changing conditions.

8. **Geospatial Data Structures**: Geospatial data structures like quad trees or R-trees can be used for indexing and querying spatial data efficiently, which is useful for tasks like finding nearby points of interest or determining which roads intersect a given area.

9. **Memory Management**: Efficient memory management is important for storing and processing large amounts of map and sensor data. Data structures like dynamic arrays or linked lists may be used to manage memory allocation and deallocation.

10. **User Interface**: While not strictly algorithmic, designing a user-friendly interface for inputting destinations, displaying maps, and providing turn-by-turn navigation instructions involves considerations of human-computer interaction and usability principles.

These are just some of the ways in which algorithms and data structures are used in the context of traveling by car. The field is continually evolving with advancements in technology and the increasing complexity of transportation systems.

### 1. Algorithms & Data Structures (C++): Traversal in Graph

Traversal in a graph is the process of visiting all the vertices and edges of the graph in a systematic way. There are several algorithms for graph traversal, the two most common being Depth-First Search (DFS) and Breadth-First Search (BFS). Here's how you can implement both in C++:

#### Depth-First Search (DFS)

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

class Graph {
    int V;
    vector<vector<int>> adj;

public:
    Graph(int V) : V(V), adj(V) {}

    void addEdge(int u, int v) {
        adj[u].push_back(v);
    }

    void DFSUtil(int v, vector<bool>& visited) {
        visited[v] = true;
        cout << v << " ";

        for (int i : adj[v]) {
            if (!visited[i]) {
                DFSUtil(i, visited);
            }
        }
    }

    void DFS(int v) {
        vector<bool> visited(V, false);
        DFSUtil(v, visited);
    }
};

int main() {
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "Depth First Traversal (starting from vertex 2): ";
    g.DFS(2);

    return 0;
}
```

#### Breadth-First Search (BFS)

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

class Graph {
    int V;
    vector<vector<int>> adj;

public:
    Graph(int V) : V(V), adj(V) {}

    void addEdge(int u, int v) {
        adj[u].push_back(v);
    }

    void BFS(int v) {
        vector<bool> visited(V, false);
        queue<int> q;

        visited[v] = true;
        q.push(v);

        while (!q.empty()) {
            v = q.front();
            cout << v << " ";
            q.pop();

            for (int i : adj[v]) {
                if (!visited[i]) {
                    visited[i] = true;
                    q.push(i);
                }
            }
        }
    }
};

int main() {
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "Breadth First Traversal (starting from vertex 2): ";
    g.BFS(2);

    return 0;
}
```

In both cases, the graph is represented using an adjacency list. The DFS and BFS algorithms visit each vertex once, so the time complexity is O(V + E), where V is the number of vertices and E is the number of edges.

### 1. Algorithms & Data Structures (C++): Types of Graph

In C++, graphs can be implemented using various data structures such as adjacency matrix, adjacency list, edge list, and others. Graphs can be classified into different types based on various properties. Here are some common types of graphs:

1. **Directed Graph (Digraph)**:
   - In a directed graph, edges have a direction. It means that the pair of vertices (u, v) doesn't necessarily imply the existence of the edge (v, u).
   - In C++, you can represent a directed graph using adjacency lists or adjacency matrix.

2. **Undirected Graph**:
   - In an undirected graph, edges do not have a direction. If there is an edge between vertices u and v, it implies that there is also an edge between vertices v and u.
   - You can represent an undirected graph using adjacency lists, adjacency matrix, or edge list.

3. **Weighted Graph**:
   - In a weighted graph, each edge has an associated weight or cost. This weight could represent distances, costs, or any other quantitative value.
   - Weighted graphs can be directed or undirected.
   - Commonly represented using adjacency lists or matrix with additional weight information.

4. **Unweighted Graph**:
   - In an unweighted graph, edges do not have any associated weight.
   - Similar to weighted graphs, they can be directed or undirected.
   - Often represented using adjacency lists or matrices without weight information.

5. **Cyclic Graph**:
   - A cyclic graph contains at least one cycle, i.e., a path that starts and ends at the same vertex.
   - Cycles can be present in directed and undirected graphs.

6. **Acyclic Graph**:
   - An acyclic graph does not contain any cycles.
   - Directed acyclic graphs (DAGs) are particularly important in many applications, such as task scheduling and dependency management.

7. **Connected Graph**:
   - A connected graph is one in which there is a path between every pair of vertices.
   - In directed graphs, this means that for every pair of vertices u and v, there is a path from u to v and a path from v to u.

8. **Disconnected Graph**:
   - A disconnected graph has at least two vertices with no path connecting them.
   - It consists of two or more connected components.

9. **Bipartite Graph**:
   - A bipartite graph is one whose vertices can be divided into two disjoint sets such that every edge connects a vertex in one set to a vertex in the other set.
   - Useful in modeling relationships such as "employer-employee" or "student-course."

10. **Complete Graph**:
    - In a complete graph, there is an edge between every pair of distinct vertices.
    - Representing a complete graph using adjacency matrix results in a fully filled matrix.

These are the fundamental types of graphs encountered in algorithmic problem-solving and real-world applications, each with its own set of properties and use cases. Depending on the problem at hand, you may choose the appropriate type of graph representation and algorithm to efficiently solve it.

### 1. Algorithms & Data Structures (C++): Types Of Graphs

In algorithms and data structures, graphs are fundamental structures used to represent relationships between objects. In C++, graphs can be implemented using various data structures such as adjacency matrix, adjacency list, or edge list. Graphs can be categorized based on various characteristics, including:

1. **Directed vs. Undirected Graphs:**
   - In an undirected graph, edges have no direction, meaning they represent symmetric relationships. If node A is connected to node B, then node B is also connected to node A.
   - In a directed graph (digraph), edges have a direction. If node A is connected to node B, it doesn't necessarily imply that node B is connected to node A.

2. **Weighted vs. Unweighted Graphs:**
   - In a weighted graph, each edge has an associated weight or cost.
   - In an unweighted graph, all edges have the same weight or no weight at all, and only the presence or absence of an edge is significant.

3. **Cyclic vs. Acyclic Graphs:**
   - A cyclic graph contains at least one cycle, which is a path that starts and ends at the same vertex.
   - An acyclic graph does not contain any cycles.

4. **Connected vs. Disconnected Graphs:**
   - A connected graph has a path between every pair of vertices.
   - A disconnected graph consists of two or more connected components, where there is no path between vertices in different components.

5. **Bipartite Graphs:**
   - A bipartite graph is a graph whose vertices can be divided into two disjoint sets such that every edge connects a vertex from one set to the other, and no two vertices within the same set are adjacent.

6. **Complete Graphs:**
   - A complete graph is a graph in which there is an edge between every pair of distinct vertices.

7. **Sparse vs. Dense Graphs:**
   - A sparse graph has relatively few edges compared to the maximum number of edges possible.
   - A dense graph has close to the maximum number of edges possible.

These are some common categorizations of graphs, each with its own properties and applications in various domains, including computer science, social networks, transportation networks, and more. Understanding these types of graphs is crucial for selecting appropriate algorithms and data structures for solving graph-related problems efficiently.

### 1. Algorithms & Data Structures (C++): Understanding The Breadth First Search

Breadth First Search (BFS) is a fundamental algorithm used to traverse or search trees or graphs. It starts at a chosen node (often referred to as the "source" node) and explores all of the neighbor nodes at the present depth before moving on to nodes at the next depth level. This process continues until all nodes reachable from the source node have been explored. BFS is commonly implemented using a queue data structure.

Here's a step-by-step explanation of how BFS works:

1. **Initialization**: Begin with a source node and mark it as visited. Enqueue this node into a queue data structure.

2. **Exploration**: While the queue is not empty, repeat the following steps:
   - Dequeue a node from the front of the queue.
   - Explore all unvisited neighbor nodes of the dequeued node.
   - Mark each visited neighbor node and enqueue it into the queue.

3. **Termination**: Repeat step 2 until the queue is empty, meaning all reachable nodes have been visited.

4. **Output**: The visited nodes, in the order they were visited, represent the traversal sequence of the graph or tree.

Let's illustrate BFS with a simple example:

Suppose we have a graph represented as an adjacency list:

```
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D', 'E'],
    'C': ['A', 'F'],
    'D': ['B'],
    'E': ['B', 'F'],
    'F': ['C', 'E']
}
```

Starting from node 'A', a BFS traversal would proceed as follows:

1. Begin at node 'A', mark it as visited, and enqueue it.
2. Dequeue 'A', visit its neighbors 'B' and 'C', mark them as visited, and enqueue them.
3. Dequeue 'B', visit its unvisited neighbor 'D', mark it as visited, and enqueue it.
4. Dequeue 'C', visit its unvisited neighbor 'F', mark it as visited, and enqueue it.
5. Dequeue 'D' and 'F' (in any order), and since they have no unvisited neighbors, move on.
6. Dequeue 'E', visit its unvisited neighbor 'F', mark it as visited, and enqueue it.
7. Dequeue 'F', which has no unvisited neighbors, and move on.
8. The queue is now empty, and the traversal is complete.

The BFS traversal order in this example would be: A, B, C, D, E, F.

In C++, BFS can be implemented using the STL queue. Here's a basic C++ implementation for the above example:

```cpp
#include <iostream>
#include <unordered_map>
#include <queue>
#include <vector>
#include <string>
#include <algorithm>

using namespace std;

void bfs(const unordered_map<char, vector<char>>& graph, char start) {
    queue<char> q;
    unordered_map<char, bool> visited;

    q.push(start);
    visited[start] = true;

    while (!q.empty()) {
        char current = q.front();
        q.pop();
        cout << current << " ";

        for (char neighbor : graph.at(current)) {
            if (!visited[neighbor]) {
                q.push(neighbor);
                visited[neighbor] = true;
            }
        }
    }
}

int main() {
    unordered_map<char, vector<char>> graph = {
        {'A', {'B', 'C'}},
        {'B', {'A', 'D', 'E'}},
        {'C', {'A', 'F'}},
        {'D', {'B'}},
        {'E', {'B', 'F'}},
        {'F', {'C', 'E'}}
    };

    cout << "BFS Traversal Order: ";
    bfs(graph, 'A');
    cout << endl;

    return 0;
}
```

This code defines a graph represented as an adjacency list and performs BFS starting from node 'A'. The output will be the BFS traversal order.

### 1. Algorithms & Data Structures (C++): Understanding The Depth First Search

Depth First Search (DFS) is a fundamental graph traversal algorithm used to explore all the vertices of a graph or tree. It starts at a chosen vertex and explores as far as possible along each branch before backtracking. This algorithm is extensively used in various applications such as finding connected components, determining paths, and solving puzzles.

Let's delve into understanding how DFS works in the context of a graph traversal using C++:

#### Graph Representation

To begin with, let's represent the graph using adjacency lists. Here's a simple implementation:

```cpp
#include <iostream>
#include <vector>
#include <stack>
#include <unordered_set>

using namespace std;

class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    Graph(int V) : V(V), adj(V) {}

    // Function to add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w); // Add w to v's list
    }

    // Depth First Search traversal
    void DFS(int start) {
        // Mark all the vertices as not visited
        vector<bool> visited(V, false);

        // Create a stack for DFS
        stack<int> stack;

        // Push the current source node
        stack.push(start);

        while (!stack.empty()) {
            // Pop a vertex from stack and print it
            int current = stack.top();
            stack.pop();

            // Stack may contain same vertex twice.
            // So, we need to print the popped item only
            // if it's not visited.
            if (!visited[current]) {
                cout << current << " ";
                visited[current] = true;
            }

            // Get all adjacent vertices of the popped vertex.
            // If an adjacent vertex has not been visited,
            // then push it to the stack.
            for (int v : adj[current]) {
                if (!visited[v]) {
                    stack.push(v);
                }
            }
        }
    }
};
```

#### Main Function for Demonstration

Here's a simple demonstration of how to use the above graph representation and DFS traversal:

```cpp
int main() {
    Graph g(4); // Create a graph with 4 vertices

    // Add edges
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "Depth First Traversal (starting from vertex 2):\n";
    g.DFS(2); // Perform DFS starting from vertex 2

    return 0;
}
```

#### Output

```
Depth First Traversal (starting from vertex 2):
2 3 0 1
```

This output demonstrates the order in which vertices are visited during the Depth First Search traversal starting from vertex 2.

Understanding DFS is crucial as it serves as a base for several other algorithms and is an essential tool in the toolbox of any programmer or computer scientist working with graphs and trees.

### 1. Algorithms & Data Structures (C++): Undirected Graph

Sure! An undirected graph is a type of graph in which edges have no direction. This means that if there is an edge between node A and node B, you can travel from A to B and from B to A. Here's a basic implementation of an undirected graph in C++ using adjacency lists:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class UndirectedGraph {
private:
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    // Constructor to initialize the graph with V vertices
    UndirectedGraph(int V) : V(V) {
        adj.resize(V);
    }

    // Function to add an edge between vertices u and v
    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u);
    }

    // Function to print the adjacency list representation of the graph
    void printGraph() {
        for (int i = 0; i < V; ++i) {
            cout << "Adjacency list of vertex " << i << ": ";
            for (int j : adj[i]) {
                cout << j << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    UndirectedGraph g(4); // Create a graph with 4 vertices

    // Add edges
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(2, 3);

    // Print the adjacency list representation of the graph
    g.printGraph();

    return 0;
}
```

In this implementation:

- The `UndirectedGraph` class represents the undirected graph.
- `V` represents the number of vertices in the graph.
- `adj` is a vector of vectors, where `adj[i]` stores all the vertices adjacent to vertex `i`.
- The `addEdge` function adds an edge between vertices `u` and `v` by pushing `v` into the adjacency list of `u` and vice versa.
- The `printGraph` function prints the adjacency list representation of the graph.

You can create an object of the `UndirectedGraph` class and add edges between vertices as required. Finally, you can print the adjacency list to visualize the graph.

### 1. Algorithms & Data Structures (C++): Undirected Graph Implementation - Adjacency List

Sure, I can provide you with a basic implementation of an undirected graph using an adjacency list representation in C++. Here's a simple example:

```cpp
#include <iostream>
#include <list>
#include <vector>

using namespace std;

class Graph {
private:
    int V; // Number of vertices
    vector

<pair<int, int>> adj; // Adjacency list representation

public:
    Graph(int V) {
        this->V = V;
        adj.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(make_pair(w, 0)); // Adding w to v's list
        adj[w].push_back(make_pair(v, 0)); // Adding v to w's list
    }

    // Function to print the adjacency list representation of the graph
    void printGraph() {
        for (int v = 0; v < V; ++v) {
            cout << "Adjacency list of vertex " << v << endl;
            cout << "head";
            for (auto it = adj[v].begin(); it != adj[v].end(); ++it)
                cout << " -> " << it->first;
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 5 vertices
    Graph g(5);

    // Add edges to the graph
    g.addEdge(0, 1);
    g.addEdge(0, 4);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(2, 3);
    g.addEdge(3, 4);

    // Print the adjacency list representation of the graph
    g.printGraph();

    return 0;
}
```

This code creates a class `Graph` which represents an undirected graph using an adjacency list. The adjacency list is implemented using a vector of lists, where each element of the vector represents a vertex, and the list associated with each vertex contains the vertices adjacent to it.

In the `addEdge` function, when an edge is added between vertices `v` and `w`, the function appends `w` to the adjacency list of `v` and appends `v` to the adjacency list of `w`.

The `printGraph` function prints the adjacency list representation of the graph.

In the `main` function, a graph with 5 vertices is created, and some edges are added to it. Finally, the adjacency list representation of the graph is printed.

### 1. Algorithms & Data Structures (C++): Undirected Graph Implementation - Adjacency Matrix

Implementing an undirected graph using an adjacency matrix in C++ involves creating a 2D array where each cell represents an edge between two vertices. Here's a basic implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Graph {
private:
    int numVertices;
    vector<vector<int>> adjacencyMatrix;

public:
    Graph(int n) : numVertices(n), adjacencyMatrix(n, vector<int>(n, 0)) {}

    void addEdge(int src, int dest) {
        // Assuming vertices are indexed from 0 to numVertices - 1
        if (src >= 0 && src < numVertices && dest >= 0 && dest < numVertices) {
            adjacencyMatrix[src][dest] = 1;
            adjacencyMatrix[dest][src] = 1; // Since it's an undirected graph
        } else {
            cout << "Invalid vertices!\n";
        }
    }

    void display() {
        cout << "Adjacency Matrix:\n";
        for (int i = 0; i < numVertices; ++i) {
            for (int j = 0; j < numVertices; ++j) {
                cout << adjacencyMatrix[i][j] << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    Graph g(5); // Creating a graph with 5 vertices

    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(2, 4);
    g.addEdge(3, 4);

    g.display();

    return 0;
}
```

In this implementation:

- `Graph` class represents the undirected graph.
- `numVertices` stores the number of vertices in the graph.
- `adjacencyMatrix` is a 2D vector representing the adjacency matrix.
- `addEdge` function adds an edge between two vertices. Since it's an undirected graph, it adds edges in both directions.
- `display` function prints the adjacency matrix to the console.

You can modify and extend this implementation as needed for your specific requirements.

### 1. Algorithms & Data Structures (C++): Valid Breadth First Search?

Sure, here's a simple implementation of a Breadth First Search (BFS) algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

// Define the graph as an adjacency list
vector<vector<int>> graph;

// Function to perform BFS
bool bfs(int start, int target) {
    vector<bool> visited(graph.size(), false); // Keep track of visited nodes
    queue<int> q; // Queue for BFS traversal

    visited[start] = true;
    q.push(start);

    while (!q.empty()) {
        int current = q.front();
        q.pop();

        // If the current node is the target, return true
        if (current == target)
            return true;

        // Traverse all adjacent vertices of current vertex
        for (int neighbor : graph[current]) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                q.push(neighbor);
            }
        }
    }

    // If target is not found
    return false;
}

int main() {
    // Example usage
    int n, m; // Number of nodes and edges
    cin >> n >> m;
    graph.resize(n);

    // Input edges
    for (int i = 0; i < m; ++i) {
        int u, v;
        cin >> u >> v;
        graph[u].push_back(v);
        graph[v].push_back(u); // Uncomment if the graph is undirected
    }

    int start, target;
    cin >> start >> target;

    if (bfs(start, target))
        cout << "Target is reachable from start.";
    else
        cout << "Target is not reachable from start.";

    return 0;
}
```

This code snippet defines a simple BFS algorithm to check if there is a path from a start node to a target node in an undirected graph represented using an adjacency list. It reads the number of nodes, edges, and the edges themselves from the standard input, then performs the BFS starting from the given start node and checks if the target node is reachable.

### 1. Algorithms & Data Structures (C++): Vertex Cover (greedy)

A vertex cover of an undirected graph is a subset of its vertices such that for every edge (u, v) of the graph, either 'u' or 'v' (or both) is in the vertex cover. The problem of finding the minimum size vertex cover of a graph is known to be NP-hard, but there exist efficient approximation algorithms.

One such approximation algorithm is the greedy algorithm for vertex cover. The greedy algorithm iteratively selects vertices such that each selected vertex covers an uncovered edge. Here's how you can implement the greedy algorithm for vertex cover in C++:

```cpp
#include <iostream>
#include <vector>
#include <set>

using namespace std;

// Function to find vertex cover using greedy algorithm
void vertexCoverGreedy(const vector<vector<int>>& graph) {
    int V = graph.size();
    set<int> cover; // To store the vertex cover
    
    // Initialize all edges as not covered
    vector<bool> covered(V, false);
    
    // Iterate through all edges
    for (int u = 0; u < V; ++u) {
        if (!covered[u]) {
            // Find the first uncovered edge
            for (int v : graph[u]) {
                if (!covered[v]) {
                    // Select either u or v into cover
                    cover.insert(u);
                    cover.insert(v);
                    covered[u] = true;
                    covered[v] = true;
                    break;
                }
            }
        }
    }
    
    // Output the vertex cover
    cout << "Vertex Cover: ";
    for (int v : cover) {
        cout << v << " ";
    }
    cout << endl;
}

int main() {
    // Example graph represented as adjacency list
    vector<vector<int>> graph = {
        {1, 2},     // Adjacency list for vertex 0
        {0, 3, 4},  // Adjacency list for vertex 1
        {0, 4, 5},  // Adjacency list for vertex 2
        {1},        // Adjacency list for vertex 3
        {1, 2},     // Adjacency list for vertex 4
        {2}         // Adjacency list for vertex 5
    };

    vertexCoverGreedy(graph);

    return 0;
}
```

This code snippet demonstrates the greedy algorithm for finding a vertex cover in an undirected graph represented using an adjacency list. You can replace the example graph with your own graph representation to test the algorithm.

### 1. Algorithms & Data Structures (C++): Vertex Cover Dynammic Programming

Dynamic programming is a powerful technique for solving optimization problems by breaking them down into simpler subproblems and storing the solutions to avoid redundant computations. When it comes to solving problems related to graphs, such as finding a vertex cover, dynamic programming can be applied effectively.

A vertex cover of a graph is a set of vertices such that each edge of the graph is incident to at least one vertex in the set. The vertex cover problem aims to find the smallest vertex cover in a given graph.

Here's a general outline of how you can use dynamic programming to solve the vertex cover problem in C++:

1. **Define the subproblem:** Let's define the subproblem as finding the minimum vertex cover for a subtree rooted at a particular node in the graph.

2. **Formulate the recursive solution:** For each node in the graph, we have two choices:
   - Include the current node in the vertex cover and exclude its children.
   - Exclude the current node and include its children in the vertex cover.

3. **Memoization/Tabulation:** Store the solutions to subproblems to avoid redundant computations. You can use memoization (top-down approach) or tabulation (bottom-up approach) depending on your preference.

4. **Base cases:** Define the base cases where the recursion ends, typically when the subtree has no nodes.

5. **Combine solutions:** Combine the solutions of subproblems to solve the main problem.

Here's a simple implementation of the vertex cover problem using dynamic programming in C++:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
#include <algorithm>

using namespace std;

unordered_map<int, vector<int>> adj;
unordered_map<int, int> dp;

int minVertexCover(int node, int parent) {
    if (adj[node].empty()) return 0; // Base case: leaf node

    if (dp.find(node) != dp.end())
        return dp[node];

    int include = 1; // Include the current node
    for (int child : adj[node]) {
        if (child == parent) continue;
        include += minVertexCover(child, node);
    }

    int exclude = adj[node].size(); // Exclude the current node
    for (int child : adj[node]) {
        if (child == parent) continue;
        for (int grandchild : adj[child]) {
            if (grandchild == node) continue;
            exclude += minVertexCover(grandchild, child);
        }
    }

    return dp[node] = min(include, exclude);
}

int main() {
    // Example graph: {0: [1, 2], 1: [0, 3], 2: [0, 4], 3: [1], 4: [2]}
    adj[0] = {1, 2};
    adj[1] = {0, 3};
    adj[2] = {0, 4};
    adj[3] = {1};
    adj[4] = {2};

    cout << "Minimum vertex cover size: " << minVertexCover(0, -1) << endl;

    return 0;
}
```

This code calculates the minimum size of a vertex cover in the given graph using dynamic programming. It uses memoization to avoid redundant computations. You can adjust it according to your specific requirements and graph representation.

### 1. Algorithms & Data Structures (C++): Walk

Certainly! "Walk" in the context of algorithms and data structures often refers to traversing through a data structure, such as a tree or a graph, visiting each node or vertex in a specific order. Here's a brief overview:

#### Tree Traversal

In trees, you typically encounter three types of traversals:

1. **Inorder Traversal:** In this traversal, you start from the left subtree, then visit the root, and finally the right subtree. This traversal is commonly used with binary search trees.

   ```cpp
   void inorderTraversal(Node* root) {
       if (root == nullptr) return;
       inorderTraversal(root->left);
       cout << root->data << " ";
       inorderTraversal(root->right);
   }
   ```

2. **Preorder Traversal:** Here, you visit the root before its children. It's useful for making a copy of the tree.

   ```cpp
   void preorderTraversal(Node* root) {
       if (root == nullptr) return;
       cout << root->data << " ";
       preorderTraversal(root->left);
       preorderTraversal(root->right);
   }
   ```

3. **Postorder Traversal:** In this traversal, you visit the children before the root. It's often used to delete a tree.

   ```cpp
   void postorderTraversal(Node* root) {
       if (root == nullptr) return;
       postorderTraversal(root->left);
       postorderTraversal(root->right);
       cout << root->data << " ";
   }
   ```

#### Graph Traversal

Graph traversal can be more complex because graphs can have cycles and aren't necessarily hierarchical. Common graph traversal algorithms include:

1. **Depth-First Search (DFS):** This algorithm explores as far as possible along each branch before backtracking. It's often implemented recursively or using a stack.

   ```cpp
   void DFS(int vertex, vector<bool>& visited, vector<vector<int>>& adjList) {
       visited[vertex] = true;
       cout << vertex << " ";
       for (int neighbor : adjList[vertex]) {
           if (!visited[neighbor]) {
               DFS(neighbor, visited, adjList);
           }
       }
   }
   ```

2. **Breadth-First Search (BFS):** BFS explores neighbors of a vertex before moving to the next level of vertices. It's typically implemented using a queue.

   ```cpp
   void BFS(int start, vector<bool>& visited, vector<vector<int>>& adjList) {
       queue<int> q;
       q.push(start);
       visited[start] = true;
       while (!q.empty()) {
           int current = q.front();
           q.pop();
           cout << current << " ";
           for (int neighbor : adjList[current]) {
               if (!visited[neighbor]) {
                   visited[neighbor] = true;
                   q.push(neighbor);
               }
           }
       }
   }
   ```

These are just basic implementations. Depending on the specific requirements and characteristics of the data structures or algorithms you're dealing with, there might be variations or optimizations possible.

### 1. Algorithms & Data Structures (C++): Weighted and Directed Graph

In C++, implementing a weighted and directed graph involves creating a data structure to represent vertices and edges, and then implementing algorithms to manipulate and traverse this graph. Here's a basic implementation using adjacency lists:

```cpp
#include <iostream>
#include <vector>
#include <utility>

using namespace std;

// Edge represents a weighted edge in the graph
struct Edge {
    int destination;
    int weight;

    Edge(int dest, int w) : destination(dest), weight(w) {}
};

// Graph class represents a weighted directed graph
class Graph {
private:
    int V; // Number of vertices
    vector<vector<Edge>> adjList; // Adjacency list

public:
    // Constructor
    Graph(int vertices) : V(vertices), adjList(vertices) {}

    // Function to add an edge to the graph
    void addEdge(int src, int dest, int weight) {
        adjList[src].push_back(Edge(dest, weight));
    }

    // Function to print the graph
    void printGraph() {
        for (int i = 0; i < V; ++i) {
            cout << "Vertex " << i << ":\n";
            for (const Edge& edge : adjList[i]) {
                cout << " -> " << edge.destination << " (weight: " << edge.weight << ")\n";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 4 vertices
    Graph graph(4);

    // Add edges to the graph
    graph.addEdge(0, 1, 5);
    graph.addEdge(0, 2, 3);
    graph.addEdge(1, 2, 2);
    graph.addEdge(1, 3, 6);
    graph.addEdge(2, 3, 7);

    // Print the graph
    graph.printGraph();

    return 0;
}
```

This code creates a weighted directed graph with 4 vertices and adds some edges to it. The `printGraph()` function is used to print the adjacency list representation of the graph.

You can extend this code by adding various algorithms like Dijkstra's algorithm for finding shortest paths, Kruskal's algorithm for finding minimum spanning trees, or any other algorithms that suit your requirements.

### 1. Algorithms & Data Structures (C++): Weighted Directed Graph

Sure! A weighted directed graph is a data structure that consists of a set of vertices/nodes connected by directed edges, where each edge has a weight assigned to it. This weight represents some numerical value associated with the edge, such as distance, cost, or time.

In C++, you can represent a weighted directed graph using various data structures. One common approach is to use an adjacency list or an adjacency matrix to store the graph.

Here's a simple implementation of a weighted directed graph using an adjacency list:

```cpp
#include <iostream>
#include <vector>
#include <utility>

using namespace std;

// Class to represent a weighted directed graph
class WeightedDirectedGraph {
private:
    int V; // Number of vertices
    vector<vector<pair<int, int>>> adjList; // Adjacency list representation

public:
    // Constructor
    WeightedDirectedGraph(int vertices) : V(vertices) {
        adjList.resize(V);
    }

    // Function to add an edge from vertex u to vertex v with weight w
    void addEdge(int u, int v, int w) {
        adjList[u].push_back(make_pair(v, w));
    }

    // Function to print the graph
    void printGraph() {
        for (int i = 0; i < V; ++i) {
            cout << "Vertex " << i << " --> ";
            for (auto edge : adjList[i]) {
                cout << "(" << edge.first << ", " << edge.second << ") ";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 4 vertices
    WeightedDirectedGraph graph(4);

    // Add some weighted edges
    graph.addEdge(0, 1, 5);
    graph.addEdge(0, 2, 10);
    graph.addEdge(1, 2, 3);
    graph.addEdge(2, 3, 7);

    // Print the graph
    graph.printGraph();

    return 0;
}
```

In this implementation:

- The `WeightedDirectedGraph` class represents the weighted directed graph.
- `V` represents the number of vertices in the graph.
- `adjList` is a vector of vectors of pairs, where `adjList[i]` stores a list of pairs `(v, w)`, representing an edge from vertex `i` to vertex `v` with weight `w`.
- The `addEdge` function adds a directed edge from vertex `u` to vertex `v` with weight `w` to the adjacency list.
- The `printGraph` function prints the adjacency list representation of the graph.

You can further extend this implementation by adding functions for traversing the graph, finding shortest paths, etc., depending on your requirements.

### 1. Algorithms & Data Structures (C++): Weighted Graph

Creating a weighted graph in C++ involves defining a data structure to represent the graph and implementing various operations such as adding vertices, adding edges with weights, and traversing the graph. Here's a basic implementation of a weighted graph using adjacency lists:

```cpp
#include <iostream>
#include <vector>
#include <utility>

using namespace std;

// Edge structure to represent edges with weights
struct Edge {
    int destination;
    int weight;
};

// Weighted Graph class
class WeightedGraph {
private:
    int numVertices;
    vector<vector<Edge>> adjList;

public:
    WeightedGraph(int V) : numVertices(V), adjList(V) {}

    // Function to add an edge with weight
    void addEdge(int src, int dest, int weight) {
        Edge edge;
        edge.destination = dest;
        edge.weight = weight;
        adjList[src].push_back(edge);
        // For undirected graph, add edge from dest to src as well
        // adjList[dest].push_back({src, weight});
    }

    // Function to print the graph
    void printGraph() {
        for (int i = 0; i < numVertices; ++i) {
            cout << "Vertex " << i << " is connected to:\n";
            for (const auto& edge : adjList[i]) {
                cout << "\tVertex " << edge.destination << " with weight " << edge.weight << "\n";
            }
        }
    }
};

int main() {
    // Create a weighted graph with 4 vertices
    WeightedGraph graph(4);

    // Add some weighted edges
    graph.addEdge(0, 1, 5);
    graph.addEdge(0, 2, 7);
    graph.addEdge(1, 2, 3);
    graph.addEdge(1, 3, 2);
    graph.addEdge(2, 3, 1);

    // Print the graph
    graph.printGraph();

    return 0;
}
```

This code demonstrates the basic structure of a weighted graph in C++. The `WeightedGraph` class maintains a vector of vectors, where each inner vector represents the adjacency list for a vertex. Each element of the inner vector is an `Edge` structure containing the destination vertex and the weight of the edge.

You can add more functionality to this class, such as methods for traversing the graph (e.g., depth-first search, breadth-first search), finding shortest paths (e.g., Dijkstra's algorithm, Bellman-Ford algorithm), or minimum spanning tree algorithms (e.g., Prim's algorithm, Kruskal's algorithm).

### 1. Algorithms & Data Structures (C++): Weighted Graphs

Weighted graphs are graphs where each edge has an associated numerical value called weight. These weights could represent various things depending on the application, such as distance, cost, time, etc. Weighted graphs are used in various algorithms, particularly in solving optimization problems.

In C++, you can represent a weighted graph using various data structures. One common approach is to use an adjacency list or an adjacency matrix to store the graph's structure, along with an additional structure to store edge weights.

Here's an example of representing a weighted graph using an adjacency list in C++:

```cpp
#include <iostream>
#include <vector>
#include <utility> // for pair

using namespace std;

// Structure to represent a weighted edge
struct Edge {
    int dest;
    int weight;
    Edge(int d, int w) : dest(d), weight(w) {}
};

// Weighted Graph class
class WeightedGraph {
private:
    int V; // Number of vertices
    vector<vector<Edge>> adjList; // Adjacency list representation

public:
    WeightedGraph(int vertices) : V(vertices), adjList(vertices) {}

    // Function to add an edge to the graph
    void addEdge(int src, int dest, int weight) {
        adjList[src].push_back(Edge(dest, weight));
        // If the graph is undirected, uncomment the next line
        // adjList[dest].push_back(Edge(src, weight)); 
    }

    // Function to print the graph
    void printGraph() {
        for (int i = 0; i < V; ++i) {
            cout << "Vertex " << i << " connects to:\n";
            for (const Edge& e : adjList[i]) {
                cout << "\tVertex " << e.dest << " with weight " << e.weight << endl;
            }
        }
    }
};

int main() {
    // Create a graph with 4 vertices
    WeightedGraph graph(4);

    // Add some weighted edges
    graph.addEdge(0, 1, 2);
    graph.addEdge(0, 2, 3);
    graph.addEdge(1, 2, 1);
    graph.addEdge(2, 3, 5);

    // Print the graph
    graph.printGraph();

    return 0;
}
```

In this code:

- `Edge` struct represents a weighted edge with destination vertex and weight.
- `WeightedGraph` class represents the weighted graph using an adjacency list.
- `addEdge` function adds a weighted edge between two vertices.
- `printGraph` function prints the graph with vertices and their adjacent vertices along with their weights.

You can extend this implementation to include various algorithms like Dijkstra's algorithm, Bellman-Ford algorithm, etc., which are commonly used with weighted graphs for tasks like finding shortest paths, minimum spanning trees, etc.

### 1. Algorithms & Data Structures (C++): Weighted Undirected Graph

Sure, I can help you with that! A weighted undirected graph is a data structure that consists of a set of vertices connected by edges, where each edge has a weight associated with it. Here's a simple implementation of a weighted undirected graph in C++ using adjacency list representation:

```cpp
#include <iostream>
#include <vector>
#include <utility>

using namespace std;

// Edge structure to represent an edge with its weight
struct Edge {
    int dest;
    int weight;
};

// Weighted Undirected Graph class
class Graph {
private:
    int V; // Number of vertices
    vector<vector<Edge>> adjList; // Adjacency list to store the edges

public:
    // Constructor
    Graph(int vertices) : V(vertices) {
        adjList.resize(V);
    }

    // Function to add an edge between two vertices with a given weight
    void addEdge(int src, int dest, int weight) {
        Edge edge1 = {dest, weight};
        Edge edge2 = {src, weight};
        adjList[src].push_back(edge1);
        adjList[dest].push_back(edge2);
    }

    // Function to print the graph
    void printGraph() {
        for (int i = 0; i < V; ++i) {
            cout << "Vertex " << i << " is connected to:" << endl;
            for (const auto& edge : adjList[i]) {
                cout << " -> " << edge.dest << " (weight: " << edge.weight << ")";
            }
            cout << endl;
        }
    }
};

int main() {
    // Create a graph with 4 vertices
    Graph graph(4);

    // Add edges with weights
    graph.addEdge(0, 1, 10);
    graph.addEdge(0, 2, 20);
    graph.addEdge(1, 2, 30);
    graph.addEdge(1, 3, 40);
    graph.addEdge(2, 3, 50);

    // Print the graph
    graph.printGraph();

    return 0;
}
```

In this implementation, each vertex of the graph is represented by an integer from 0 to V-1, where V is the total number of vertices. The adjacency list is a vector of vectors, where each element of the outer vector represents a vertex, and each element of the inner vector represents an edge incident to that vertex.

The `addEdge` function adds an edge between two vertices, `src` and `dest`, with the given weight. Since the graph is undirected, edges are added to both vertices' adjacency lists.

The `printGraph` function prints the adjacency list representation of the graph, displaying each vertex along with its adjacent vertices and the corresponding edge weights.

You can modify this implementation as per your requirements or use it as a reference to implement other graph algorithms. Let me know if you need further clarification or assistance!

### 1. Algorithms & Data Structures (C++): Weighted vs Unweighted Graphs

Weighted and unweighted graphs are two fundamental concepts in graph theory, and they have distinct characteristics and applications.

1. **Unweighted Graphs**:
   - In an unweighted graph, each edge has the same value or weight, typically considered to be 1.
   - Unweighted graphs are used to represent relationships where there is no notion of "cost" or "distance" associated with traversing from one vertex to another.
   - Examples of unweighted graphs include social networks where edges represent friendships, or a map where vertices are locations and edges represent roads with no consideration of distance.
   - Common algorithms for unweighted graphs include breadth-first search (BFS) and depth-first search (DFS).

2. **Weighted Graphs**:
   - In a weighted graph, each edge has an associated numerical value called weight. This weight could represent distance, cost, time, or any other metric depending on the application.
   - Weighted graphs are used when there is a notion of "cost" or "distance" associated with traversing from one vertex to another.
   - Examples of weighted graphs include road networks where edges represent roads with distances, or airline networks where edges represent flight routes with travel times.
   - Common algorithms for weighted graphs include Dijkstra's algorithm for finding the shortest path, and minimum spanning tree algorithms like Prim's and Kruskal's algorithms.

In terms of implementation in C++:

- For unweighted graphs, you can represent the graph using adjacency lists or adjacency matrices. Since all edges have the same weight, you don't need to store weights explicitly.
- For weighted graphs, you typically use adjacency lists to represent the graph structure efficiently, and you'll need to store the weights along with the vertices and edges.

Here's a simple example of representing a weighted graph in C++ using an adjacency list:

```cpp
#include <iostream>
#include <vector>
#include <utility> // for pair

using namespace std;

// Weighted graph represented using adjacency list
class Graph {
    int V;
    vector<pair<int, int>> *adj;

public:
    Graph(int V) {
        this->V = V;
        adj = new vector<pair<int, int>>[V];
    }

    void addEdge(int u, int v, int weight) {
        adj[u].push_back(make_pair(v, weight));
        adj[v].push_back(make_pair(u, weight)); // For undirected graph
    }

    void printGraph() {
        for (int i = 0; i < V; ++i) {
            cout << "Adjacency list of vertex " << i << "\n";
            for (const auto& edge : adj[i]) {
                cout << " -> " << edge.first << " (weight: " << edge.second << ")\n";
            }
            cout << endl;
        }
    }
};

int main() {
    Graph g(4);
    g.addEdge(0, 1, 10);
    g.addEdge(0, 2, 6);
    g.addEdge(1, 3, 5);
    g.addEdge(2, 3, 15);
    g.printGraph();
    return 0;
}
```

This code represents a weighted graph with four vertices and adds some weighted edges between them. The `printGraph` function prints the adjacency list representation of the graph along with the weights.

### 1. Algorithms & Data Structures (C++): What are graphs

Graphs are a fundamental data structure in computer science used to represent relationships between pairs of objects. A graph consists of a set of vertices (also called nodes) and a set of edges (also called links or arcs) that connect these vertices.

In a graph, vertices typically represent entities, and edges represent the relationships between these entities. Graphs can be used to model various real-world scenarios such as social networks, transportation networks, computer networks, and more.

Graphs can be categorized based on various properties:

1. **Directed vs. Undirected Graphs:** In a directed graph, edges have a direction, meaning they go from one vertex to another. In an undirected graph, edges have no direction, and they simply indicate a connection between vertices without any specified direction.

2. **Weighted vs. Unweighted Graphs:** In a weighted graph, each edge has an associated weight or cost. This weight can represent various metrics such as distance, cost, time, etc. In an unweighted graph, all edges are considered to have the same weight.

3. **Cyclic vs. Acyclic Graphs:** A cyclic graph contains at least one cycle, which is a path that starts and ends at the same vertex. An acyclic graph, also known as a DAG (Directed Acyclic Graph), does not contain any cycles.

4. **Connected vs. Disconnected Graphs:** A connected graph is a graph in which there is a path between every pair of vertices. A disconnected graph consists of two or more connected components, where each component is a connected subgraph, but there are no edges between vertices in different components.

Graphs can be represented in various ways, including adjacency matrix, adjacency list, and adjacency set. Algorithms and operations on graphs include traversal algorithms like Depth-First Search (DFS) and Breadth-First Search (BFS), shortest path algorithms like Dijkstra's algorithm and Bellman-Ford algorithm, minimum spanning tree algorithms like Prim's algorithm and Kruskal's algorithm, and many more.

### 1. Algorithms & Data Structures (C++): What are Graphs ?

Graphs are a fundamental data structure in computer science used to represent connections or relationships between pairs of objects. A graph consists of a set of vertices (also known as nodes or points) and a set of edges (also known as links or lines) that connect pairs of vertices.

In a graph:

- Vertices represent entities, such as cities in a map, computers in a network, or individuals in a social network.
- Edges represent relationships or connections between pairs of vertices. These connections can be directed (one-way) or undirected (two-way), weighted (have a value associated with them), or unweighted.

Graphs can be used to model a wide range of real-world scenarios, including:

- Social networks, where vertices represent people and edges represent friendships or connections between them.
- Transportation networks, where vertices represent locations and edges represent roads or routes between them.
- Computer networks, where vertices represent devices (such as routers or computers) and edges represent connections between them.
- Recommendations systems, where vertices represent users or items and edges represent interactions or similarities between them.

Graphs can be classified into various types based on their properties:

1. **Directed vs. Undirected**: In directed graphs (also called digraphs), edges have a direction, while in undirected graphs, edges have no direction.
2. **Weighted vs. Unweighted**: In weighted graphs, each edge has an associated weight or cost, while in unweighted graphs, all edges have the same weight.
3. **Sparse vs. Dense**: A graph is sparse if it has relatively few edges compared to the maximum possible number of edges, while it is dense if it has close to the maximum possible number of edges.
4. **Cyclic vs. Acyclic**: A graph is cyclic if it contains at least one cycle (a sequence of vertices where the first and last vertices are the same), while it is acyclic if it contains no cycles.
5. **Connected vs. Disconnected**: A graph is connected if there is a path between every pair of vertices, while it is disconnected if there are one or more pairs of vertices with no path between them.

Graphs can be represented and implemented using various data structures, including adjacency matrices, adjacency lists, and edge lists, each with its own advantages and disadvantages in terms of memory usage and performance. Algorithms for graphs include traversal algorithms (such as depth-first search and breadth-first search), shortest path algorithms (such as Dijkstra's algorithm and Bellman-Ford algorithm), and minimum spanning tree algorithms (such as Prim's algorithm and Kruskal's algorithm), among others.

### 1. Algorithms & Data Structures (C++): What does the graph data structure look like?

In C++, graphs can be represented in several ways, each with its own advantages and use cases. The two most common representations are the adjacency matrix and the adjacency list.

1. **Adjacency Matrix:**
   In this representation, a 2D array is used where the rows and columns represent the vertices of the graph, and the value at `matrix[i][j]` represents the presence or absence of an edge between vertices `i` and `j`. If the graph is weighted, instead of just indicating presence/absence, the weight of the edge can be stored at `matrix[i][j]`.

   ```cpp
   const int MAX_VERTICES = 100;
   int graph[MAX_VERTICES][MAX_VERTICES];
   ```

   This representation is efficient for dense graphs (graphs with many edges), as it allows constant-time lookup to determine whether there's an edge between any two vertices. However, it consumes more memory for sparse graphs (graphs with fewer edges).

2. **Adjacency List:**
   In this representation, each vertex of the graph is associated with a list of its neighboring vertices. This can be implemented using an array of lists, or using a vector of vectors in C++.

   ```cpp
   #include <vector>
   using namespace std;

   vector<int> adj[MAX_VERTICES];
   ```

   Each element `adj[i]` contains a list of integers representing the vertices adjacent to vertex `i`. If the graph is weighted, each element can be a pair `(vertex, weight)`.

   This representation is more memory-efficient for sparse graphs, but lookup time for specific edges can be longer, typically O(E) where E is the number of edges.

These are the basic representations, but depending on the specific requirements and operations needed for your graph algorithms, you might choose different representations or even custom implementations.

### 1. Algorithms & Data Structures (C++): What exactly are graphs?

Graphs are fundamental data structures in computer science used to represent relationships between pairs of objects. They consist of two main components: vertices (also called nodes) and edges.

1. **Vertices (Nodes)**: These are the entities in the graph. Each vertex typically represents an object or a distinct entity in the system being modeled. For example, in a social network graph, vertices could represent individual users, while in a map application, vertices might represent cities or locations.

2. **Edges**: These are the connections between vertices. An edge between two vertices signifies a relationship or interaction between them. Edges can be directed or undirected. In a directed graph, edges have a direction, indicating a one-way relationship between vertices. In an undirected graph, edges do not have a direction, signifying a bidirectional relationship between vertices. For example, in a social network graph, a directed edge could represent "follows" relationship, while an undirected edge could represent "friendship".

Graphs can be classified based on various properties:

1. **Directed vs. Undirected**: As mentioned earlier, directed graphs have edges with a direction, while undirected graphs do not.

2. **Weighted vs. Unweighted**: In weighted graphs, each edge has a numerical value associated with it, representing some kind of cost, distance, or capacity. Unweighted graphs, on the other hand, do not have these associated values.

3. **Cyclic vs. Acyclic**: A graph is cyclic if there exists a path that starts and ends at the same vertex, forming a cycle. An acyclic graph does not contain any cycles.

4. **Connected vs. Disconnected**: A connected graph is one in which there is a path between every pair of vertices. A disconnected graph consists of two or more connected components, meaning there are groups of vertices that are not connected to each other.

Graphs are used in a wide range of applications including network optimization, social network analysis, routing algorithms, recommendation systems, and much more. They offer a flexible and powerful way to model complex relationships and structures.

### 1. Algorithms & Data Structures (C++): What is a Graph? Why Graph?

A graph in computer science is a non-linear data structure consisting of nodes (vertices) and edges connecting these nodes. It's a powerful abstraction used to represent a wide range of real-world relationships and networks, such as social networks, transportation networks, computer networks, and more.

In a graph:

- **Nodes (Vertices)**: These are the entities in the graph. They can represent any discrete object, concept, or entity. For example, in a social network graph, nodes could represent individuals, and in a computer network graph, nodes could represent devices.
  
- **Edges (Connections)**: These are the links between the nodes and represent the relationships or connections between them. Edges can be directed (one-way) or undirected (two-way), weighted (having a value associated with them, indicating the cost, distance, etc., of the connection), or unweighted.

**Why Graphs?**

1. **Modeling Relationships**: Graphs are excellent for modeling relationships between different entities. For instance, in a social network, nodes represent individuals, and edges represent friendships.

2. **Flexibility**: Graphs are incredibly flexible and can represent a wide variety of relationships and structures. Whether it's a simple tree-like structure or a complex interconnected network, graphs can handle it.

3. **Problem Solving**: Many real-world problems can be effectively solved using graph algorithms. Tasks such as finding the shortest path between two points, determining the most efficient route through a network, or identifying clusters of related entities can all be accomplished with graph algorithms.

4. **Optimization**: Graphs provide a framework for optimization problems. Algorithms like Dijkstra's algorithm for finding the shortest path, or Prim's algorithm for finding the minimum spanning tree, are crucial in optimization tasks.

5. **Network Analysis**: Graphs are used extensively in network analysis to understand the structure and behavior of complex systems. They help in identifying key nodes, analyzing connectivity patterns, and predicting behavior.

In essence, graphs provide a versatile and powerful tool for representing, analyzing, and solving problems related to interconnected data. This makes them a fundamental concept in computer science and a key topic in algorithms and data structures.

### 1. Algorithms & Data Structures (C++): What is The Bellman-Ford Algorithm? - Conceptualizing Dynamic Programming

The Bellman-Ford algorithm is a popular method for finding the shortest path from a single source vertex to all other vertices in a weighted graph. It's particularly useful when dealing with graphs that may contain negative weight edges, unlike Dijkstra's algorithm which requires all edge weights to be non-negative.

Here's a conceptual breakdown of how the Bellman-Ford algorithm works:

1. **Initialization**: Start by initializing the distances from the source vertex to all other vertices in the graph. Initially, set the distance to the source vertex as 0 and the distance to all other vertices as infinity.

2. **Relaxation**: The algorithm iterates over all edges in the graph for a total of |V| - 1 times, where |V| is the number of vertices in the graph. In each iteration, it relaxes the edges, meaning it tries to improve the current best distance estimates to each vertex by considering all the edges in the graph.

3. **Edge Relaxation**: For each edge (u, v) in the graph, where u is the source vertex and v is the destination vertex, the algorithm checks if the distance from the source vertex to v via u is shorter than the currently known distance to v. If it is, the distance to v is updated to the new shorter distance.

4. **Detection of Negative Cycles**: After the |V| - 1 iterations, an additional check is performed to detect negative cycles. If during any iteration, the algorithm still finds a shorter path, it indicates the presence of a negative cycle. A negative cycle is a cycle in the graph where the total sum of the edge weights is negative.

5. **Output**: If there are no negative cycles, the algorithm returns the shortest distances from the source vertex to all other vertices in the graph. If there are negative cycles, the algorithm indicates that the graph contains one, and it may not produce meaningful results.

Bellman-Ford algorithm is a dynamic programming approach as it builds up solutions to subproblems and eventually solves the main problem. It ensures that the shortest path estimates are progressively updated based on previous computations until the optimal solution is achieved.

### 1. Algorithms & Data Structures (C++): What is topological sorting

Topological sorting is a technique used in graph theory, particularly with directed acyclic graphs (DAGs). It arranges the vertices of a graph in such an order that for any directed edge from vertex u to vertex v, u comes before v in the ordering.

In simpler terms, it's like arranging tasks based on their dependencies so that you can execute them in the correct order. Imagine you have tasks where some tasks must be completed before others can begin. Topological sorting helps you find a sequence in which you can complete all tasks without violating any dependencies.

For example, consider a project with tasks represented as vertices and dependencies represented as directed edges. Topological sorting helps you find an order in which you can complete all tasks without violating any dependencies.

However, it's important to note that topological sorting is only applicable to directed acyclic graphs (DAGs). If the graph contains cycles, it's not possible to perform a topological sort because the dependencies become cyclic, resulting in an undefined ordering.

In C++, you can implement topological sorting using algorithms like depth-first search (DFS). The basic idea is to perform a depth-first search on the graph and assign a post-order number to each vertex. After the DFS, vertices are outputted in reverse post-order, which is a valid topological ordering of the graph.

### 1. Algorithms & Data Structures (C++): Why Bellman Ford runs V-1 times?

The Bellman-Ford algorithm is used to find the shortest paths from a single source vertex to all other vertices in a weighted graph. It is similar to Dijkstra's algorithm but can handle graphs with negative edge weights, although it doesn't work with negative cycles.

The reason why Bellman-Ford runs V-1 times is because it guarantees finding the shortest paths from the source vertex to all other vertices in at most V-1 iterations, where V is the number of vertices in the graph. This is due to the fact that the shortest path between any two vertices in a graph with V vertices contains at most V-1 edges.

In each iteration, Bellman-Ford relaxes (updates) the distances to all vertices by considering all the edges in the graph. After V-1 iterations, the distances to all vertices will be updated to their shortest possible values. If there are no negative cycles in the graph, then further iterations will not change the distances, as any shortest path cannot contain more than V-1 edges.

So, running Bellman-Ford for V-1 iterations ensures that the algorithm finds the shortest paths from the source vertex to all other vertices in the graph. If the graph contains a negative cycle reachable from the source vertex, the algorithm will detect it during the V-1 iterations, as the distances to some vertices will continue to decrease in subsequent iterations.

### 1. Algorithms & Data Structures (C++): Why does Breadth First Search not work with weighted Graph?

Breadth First Search (BFS) is primarily designed for unweighted graphs where the cost of moving from one node to another is considered constant. When applied to weighted graphs, where each edge has a weight or cost associated with it, BFS might not produce the desired results or may even fail to work correctly due to several reasons:

1. **Lack of Greediness**: BFS explores nodes in a level-wise manner, expanding outward from the starting node. It doesn't consider the weight of edges, so it's not suitable for scenarios where the shortest path is desired, especially in weighted graphs where the shortest path may not be the one with the fewest edges.

2. **Incorrect Path Selection**: In a weighted graph, BFS may find a path with fewer edges but greater total weight, which could be suboptimal or incorrect if the goal is to find the shortest path based on weight.

3. **Inefficient or Incorrect Path Finding**: BFS doesn't take into account the weights of edges, so it may not necessarily find the path with the minimum total weight. In certain cases, it may find a path with a higher total weight while ignoring shorter paths with lower total weight.

To handle weighted graphs, Dijkstra's algorithm or A* algorithm are typically used. These algorithms consider the weights of edges and are designed specifically for finding the shortest path in weighted graphs. Dijkstra's algorithm guarantees the shortest path in non-negative weighted graphs, while A* algorithm is a more efficient variant which uses heuristics to guide the search towards the goal node.

### 1. Algorithms & Data Structures (C++): Why does Depth First Search not work for SSSP?

Depth First Search (DFS) is not well-suited for Single-Source Shortest Path (SSSP) problems primarily due to its nature of exploration. DFS is a traversal algorithm that explores as far as possible along each branch before backtracking. While this approach is excellent for exploring or searching a graph, it does not guarantee the shortest path between two nodes.

Here are a few reasons why DFS is not suitable for SSSP:

1. **Non-optimal paths**: DFS explores the graph deeply before considering neighboring vertices. It may find a path from the source to the destination, but it is not guaranteed to be the shortest path. DFS does not consider the weight of edges, which is essential for finding the shortest path.

2. **Backtracking**: DFS explores one branch of the graph as far as possible before backtracking to explore other branches. This approach can lead to inefficiency, as it may explore many unnecessary paths before finding the shortest one.

3. **Lack of information**: DFS does not maintain information about the shortest path found so far. It simply explores the graph until it reaches the destination node. Without keeping track of the path length, DFS cannot guarantee the shortest path.

For Single-Source Shortest Path problems, algorithms like Dijkstra's algorithm or Bellman-Ford algorithm are more appropriate. These algorithms consider the weight of edges and maintain information about the shortest path found so far, ensuring that they find the shortest path from the source to all other nodes in the graph.

### 1. Algorithms & Data Structures (C++): Why Floyd Warshall?

The Floyd-Warshall algorithm is a fundamental algorithm in computer science, particularly in the realm of graph theory and dynamic programming. It is primarily used for finding the shortest paths in a weighted graph with positive or negative edge weights (but without negative cycles). Here's why it's important:

1. **All Pairs Shortest Path (APSP) Problem**: Floyd-Warshall solves the APSP problem efficiently, meaning it finds the shortest path between all pairs of vertices in a graph.

2. **Versatility**: Unlike some other shortest path algorithms like Dijkstra's or Bellman-Ford, Floyd-Warshall works for graphs with negative weights as long as there are no negative cycles. This makes it suitable for a wider range of applications.

3. **Efficiency**: Although its time complexity is O(V^3), where V is the number of vertices in the graph, it is often quite efficient in practice for small to medium-sized graphs. Its simplicity and ease of implementation also contribute to its popularity.

4. **Dynamic Programming**: Floyd-Warshall is a classic example of dynamic programming, showcasing how optimal solutions to subproblems can be used to find the optimal solution to the overall problem.

5. **Transitive Closure**: The algorithm can also be used to find the transitive closure of a directed graph, which is another important application in graph theory.

Overall, Floyd-Warshall is valuable because it provides a simple and efficient solution to a fundamental problem in graph theory, making it a key tool in algorithmic problem-solving and optimization.

### 1. Algorithms & Data Structures (C++): Cycle Detection in Directed Graph

Detecting cycles in a directed graph is a fundamental problem in computer science and is often encountered in various applications like detecting deadlocks in resource allocation systems or in network routing algorithms. One popular algorithm to accomplish this is Depth-First Search (DFS). Here's how you can implement cycle detection in a directed graph using DFS in C++:

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

class Graph {
    int V; // Number of vertices

    // Pointer to an array containing adjacency lists
    vector<int> *adj;

    // Recursive helper function for DFS
    bool isCyclicUtil(int v, vector<bool> &visited, vector<bool> &recStack) {
        if (!visited[v]) {
            visited[v] = true;
            recStack[v] = true;

            // Recur for all the vertices adjacent to this vertex
            for (int i : adj[v]) {
                if (!visited[i] && isCyclicUtil(i, visited, recStack))
                    return true;
                else if (recStack[i])
                    return true;
            }
        }
        recStack[v] = false; // Remove the vertex from recursion stack
        return false;
    }

public:
    Graph(int V) {
        this->V = V;
        adj = new vector<int>[V];
    }

    ~Graph() {
        delete[] adj;
    }

    // Function to add an edge to the graph
    void addEdge(int v, int w) {
        adj[v].push_back(w);
    }

    // Function to detect cycle using DFS
    bool isCyclic() {
        vector<bool> visited(V, false);
        vector<bool> recStack(V, false);

        // Call the recursive helper function to detect cycle in different DFS trees
        for (int i = 0; i < V; i++) {
            if (isCyclicUtil(i, visited, recStack))
                return true;
        }
        return false;
    }
};

int main() {
    Graph g(4); // Create a graph with 4 vertices

    // Add edges
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    if (g.isCyclic())
        cout << "Graph contains cycle";
    else
        cout << "Graph doesn't contain cycle";
    
    return 0;
}
```

This code uses DFS to traverse the graph. It maintains two arrays: `visited` and `recStack`. The `visited` array keeps track of the vertices visited during DFS traversal, while the `recStack` array keeps track of the vertices that are part of the current DFS traversal path. If we encounter a vertex that is already in the recursion stack, it indicates the presence of a cycle.
