
### 1. Algorithms & Data Structures (C++): Disjoint Set

Disjoint Set, also known as Union-Find, is a data structure that keeps track of a set of elements partitioned into disjoint (non-overlapping) subsets. It provides two main operations:

1. **Union:** Merge two subsets into a single subset.
2. **Find:** Determine which subset a particular element is in. This operation can be used for checking whether two elements are in the same subset.

Here's a basic implementation of Disjoint Set in C++ using both the union by rank and path compression techniques:

```cpp
#include <iostream>
#include <vector>

class DisjointSet {
private:
    std::vector<int> parent;
    std::vector<int> rank;

public:
    DisjointSet(int n) {
        parent.resize(n);
        rank.resize(n, 0);
        // Initially, each element is its own parent (representing a single-element set)
        for (int i = 0; i < n; ++i) {
            parent[i] = i;
        }
    }

    // Find operation with path compression
    int find(int x) {
        if (x != parent[x]) {
            parent[x] = find(parent[x]);
        }
        return parent[x];
    }

    // Union operation with union by rank
    void Union(int x, int y) {
        int xRoot = find(x);
        int yRoot = find(y);

        if (xRoot == yRoot) return;

        if (rank[xRoot] < rank[yRoot]) {
            parent[xRoot] = yRoot;
        } else if (rank[xRoot] > rank[yRoot]) {
            parent[yRoot] = xRoot;
        } else {
            parent[yRoot] = xRoot;
            rank[xRoot]++;
        }
    }
};

int main() {
    int n = 5; // Number of elements
    DisjointSet ds(n);

    // Example usage
    ds.Union(0, 1);
    ds.Union(2, 3);
    ds.Union(0, 4);

    std::cout << "Are 1 and 4 in the same set? " << (ds.find(1) == ds.find(4) ? "Yes" : "No") << std::endl;
    std::cout << "Are 2 and 4 in the same set? " << (ds.find(2) == ds.find(4) ? "Yes" : "No") << std::endl;

    return 0;
}
```

This implementation uses the "union by rank" heuristic for merging subsets and "path compression" technique for speeding up the find operation by making the found root of the representative elements point directly to the root. These optimizations ensure efficient time complexities for both operations, leading to nearly constant time for each operation on average.

### 1. Algorithms & Data Structures (C++): Disjoint Set for Cycle Detection

In C++, you can implement a Disjoint Set data structure to detect cycles efficiently. Disjoint Set is commonly used in conjunction with other algorithms, such as Kruskal's Minimum Spanning Tree algorithm and cycle detection. Here's a basic implementation of Disjoint Set along with cycle detection using union-find:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class DisjointSet {
private:
    vector<int> parent;
    vector<int> rank;

public:
    DisjointSet(int n) {
        parent.resize(n);
        rank.resize(n, 0);
        // Initialize each element as its own parent
        for (int i = 0; i < n; ++i)
            parent[i] = i;
    }

    // Find the parent of the set containing element x
    int find(int x) {
        if (x != parent[x])
            parent[x] = find(parent[x]);
        return parent[x];
    }

    // Union the sets containing elements x and y
    void unionSets(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);
        if (rootX != rootY) {
            if (rank[rootX] < rank[rootY])
                parent[rootX] = rootY;
            else if (rank[rootX] > rank[rootY])
                parent[rootY] = rootX;
            else {
                parent[rootY] = rootX;
                rank[rootX]++;
            }
        }
    }
};

bool hasCycle(vector<pair<int, int>>& edges, int n) {
    DisjointSet ds(n);

    for (auto& edge : edges) {
        int u = edge.first;
        int v = edge.second;

        int parentU = ds.find(u);
        int parentV = ds.find(v);

        // If both vertices are in the same set, a cycle is detected
        if (parentU == parentV)
            return true;

        // Otherwise, union the sets of the two vertices
        ds.unionSets(parentU, parentV);
    }

    return false;
}

int main() {
    int n = 4; // Number of vertices
    vector<pair<int, int>> edges = {{0, 1}, {1, 2}, {2, 3}, {3, 0}}; // Example edges

    if (hasCycle(edges, n))
        cout << "Graph contains a cycle.\n";
    else
        cout << "Graph doesn't contain a cycle.\n";

    return 0;
}
```

In this implementation, we create a `DisjointSet` class which allows us to perform operations like finding the parent of an element and unioning two sets. The `hasCycle` function takes a vector of edges and the number of vertices as input, then iterates over each edge, checking if its endpoints belong to the same set. If they do, a cycle is detected; otherwise, the sets are unioned. Finally, the main function demonstrates how to use this implementation by creating an example graph and checking for cycles.

### 1. Algorithms & Data Structures (C++): Disjoint Set in C++

A disjoint set (also known as a union-find data structure) is a data structure that keeps track of a set of elements partitioned into a number of disjoint (non-overlapping) subsets. Here's an implementation of a disjoint set in C++:

```cpp
#include <vector>

class DisjointSet {
private:
    std::vector<int> parent;
    std::vector<int> rank;

public:
    DisjointSet(int n) {
        parent.resize(n);
        rank.resize(n, 0);
        for (int i = 0; i < n; ++i)
            parent[i] = i;
    }

    int find(int x) {
        if (parent[x] != x)
            parent[x] = find(parent[x]);
        return parent[x];
    }

    void union_sets(int x, int y) {
        int root_x = find(x);
        int root_y = find(y);
        if (root_x != root_y) {
            if (rank[root_x] < rank[root_y])
                std::swap(root_x, root_y);
            parent[root_y] = root_x;
            if (rank[root_x] == rank[root_y])
                rank[root_x]++;
        }
    }
};
```

This implementation uses both the path compression and union by rank optimizations to ensure efficient operations. Path compression optimizes the `find` operation by making each node point directly to the root of its set, reducing the time complexity of subsequent finds. Union by rank optimizes the `union_sets` operation by always attaching the smaller tree to the root of the larger tree, which helps keep the tree balanced and ensures logarithmic time complexity for the operation.

Here's how you can use the `DisjointSet` class:

```cpp
#include <iostream>

int main() {
    int n = 5; // number of elements
    DisjointSet ds(n);

    ds.union_sets(0, 2);
    ds.union_sets(1, 3);
    ds.union_sets(2, 4);

    std::cout << "Parent of 0: " << ds.find(0) << std::endl; // Should print 2
    std::cout << "Parent of 1: " << ds.find(1) << std::endl; // Should print 3
    std::cout << "Parent of 2: " << ds.find(2) << std::endl; // Should print 2
    std::cout << "Parent of 3: " << ds.find(3) << std::endl; // Should print 3
    std::cout << "Parent of 4: " << ds.find(4) << std::endl; // Should print 2

    return 0;
}
```

This example demonstrates how to create a disjoint set with 5 elements and perform union operations between them, followed by finding their parent elements.

### 1. Algorithms & Data Structures (C++): Disjoint Set Union

Disjoint Set Union (DSU), also known as Union-Find, is a data structure and algorithm used to efficiently solve problems involving disjoint sets. It maintains a collection of disjoint (non-overlapping) sets and supports two main operations:

1. **Union**: Merge two sets into one.
2. **Find**: Determine which set a particular element belongs to.

Here's a basic implementation of DSU in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class DisjointSet {
private:
    vector<int> parent;
    vector<int> rank;

public:
    DisjointSet(int n) {
        parent.resize(n);
        rank.resize(n);
        // Initially, each element is its own parent and has rank 0
        for (int i = 0; i < n; ++i) {
            parent[i] = i;
            rank[i] = 0;
        }
    }

    int find(int x) {
        if (x != parent[x]) {
            // Path compression: make the parent of x point to the root of its set
            parent[x] = find(parent[x]);
        }
        return parent[x];
    }

    void unionSets(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);

        if (rootX != rootY) {
            // Union by rank: attach the smaller rank tree under the root of the higher rank tree
            if (rank[rootX] < rank[rootY]) {
                parent[rootX] = rootY;
            } else if (rank[rootX] > rank[rootY]) {
                parent[rootY] = rootX;
            } else {
                parent[rootY] = rootX;
                rank[rootX]++;
            }
        }
    }
};

int main() {
    DisjointSet dsu(5); // Create a disjoint set with 5 elements

    dsu.unionSets(0, 2);
    dsu.unionSets(1, 4);
    dsu.unionSets(3, 2);

    // Output: 2
    cout << "Parent of 3: " << dsu.find(3) << endl;
    
    // Output: 4
    cout << "Parent of 1: " << dsu.find(1) << endl;

    return 0;
}
```

This implementation utilizes both path compression and union by rank optimizations to achieve efficient performance. Path compression ensures that the find operation runs in nearly constant time, and union by rank ensures that the depth of the trees remains small, resulting in efficient union operations.

### 1. Algorithms & Data Structures (C++): Disjoint Set Union Data Structure

The Disjoint Set Union (DSU) data structure, also known as the Union-Find data structure, is a data structure that keeps track of a collection of disjoint sets, where each set is represented by one of its members. It provides two main operations: **union**, which merges two sets together, and **find**, which determines which set a particular element belongs to.

Here's a simple implementation of the DSU data structure in C++:

```cpp
#include <vector>

class DSU {
private:
    std::vector<int> parent;
    std::vector<int> rank;

public:
    DSU(int n) {
        parent.resize(n);
        rank.resize(n, 1);  // Initialize rank of each element as 1
        // Initially, each element is its own parent
        for (int i = 0; i < n; ++i)
            parent[i] = i;
    }

    // Find operation: returns the representative of the set containing x
    int find(int x) {
        if (parent[x] != x)
            parent[x] = find(parent[x]);  // Path compression
        return parent[x];
    }

    // Union operation: merges the sets containing x and y
    void unite(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);
        if (rootX != rootY) {
            // Union by rank
            if (rank[rootX] < rank[rootY])
                parent[rootX] = rootY;
            else if (rank[rootX] > rank[rootY])
                parent[rootY] = rootX;
            else {
                parent[rootY] = rootX;
                rank[rootX]++;
            }
        }
    }
};
```

In this implementation:

- The `parent` vector holds the parent of each element. Initially, each element is its own parent, representing a singleton set.
- The `rank` vector holds the rank of each element. Rank is used to keep the tree balanced during union operations.
- The `find` function recursively finds the representative of the set containing a given element `x`, while performing path compression to optimize future queries.
- The `unite` function merges the sets containing elements `x` and `y`. It uses the ranks of the sets to decide which one becomes the parent during the union operation, which helps in keeping the tree balanced.

This DSU implementation has an almost constant time complexity for both `find` and `unite` operations, making it very efficient for a wide range of applications, such as Kruskal's algorithm for finding minimum spanning trees and detecting cycles in a graph.

### 1. Algorithms & Data Structures (C++): Disjoint Sets and Kruskal's Algorithm

Sure! Disjoint Sets and Kruskal's Algorithm are both fundamental concepts in the field of algorithms and data structures, especially in the context of graph theory and spanning tree algorithms. Let me break down each concept:

#### Disjoint Sets

Disjoint Sets, also known as Union-Find or Merge-Find data structure, is used to maintain a collection of disjoint sets and efficiently perform operations like finding which set an element belongs to, merging two sets, and determining whether two elements belong to the same set. It's commonly used in algorithms like Kruskal's Algorithm for finding minimum spanning trees.

In C++, Disjoint Sets can be implemented using either the array-based approach or the tree-based approach (also known as union by rank and path compression). Here's a basic implementation of the array-based approach:

```cpp
#include <vector>

class DisjointSets {
private:
    std::vector<int> parent;
    std::vector<int> rank;

public:
    DisjointSets(int n) {
        parent.resize(n);
        rank.resize(n, 0);
        for (int i = 0; i < n; ++i)
            parent[i] = i;
    }

    int find(int x) {
        if (parent[x] != x)
            parent[x] = find(parent[x]); // Path compression
        return parent[x];
    }

    void merge(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);
        if (rootX != rootY) {
            if (rank[rootX] < rank[rootY])
                parent[rootX] = rootY;
            else if (rank[rootX] > rank[rootY])
                parent[rootY] = rootX;
            else {
                parent[rootY] = rootX;
                rank[rootX]++;
            }
        }
    }
};
```

#### Kruskal's Algorithm

Kruskal's Algorithm is a greedy algorithm used to find the minimum spanning tree of a connected, undirected graph. It operates by adding edges in increasing order of their weights while avoiding the formation of cycles. Here's how it works:

1. Sort all the edges in non-decreasing order of their weight.
2. Initialize an empty graph to store the minimum spanning tree.
3. Iterate through the sorted edges and add each edge to the minimum spanning tree if it doesn't form a cycle with the edges already added.

Here's a basic implementation of Kruskal's Algorithm using Disjoint Sets:

```cpp
#include <vector>
#include <algorithm>

struct Edge {
    int src, dest, weight;
};

class Graph {
private:
    int V;
    std::vector<Edge> edges;

public:
    Graph(int V) : V(V) {}

    void addEdge(int src, int dest, int weight) {
        edges.push_back({src, dest, weight});
    }

    std::vector<Edge> kruskalMST() {
        std::vector<Edge> result;
        DisjointSets ds(V);

        // Sort edges by weight
        std::sort(edges.begin(), edges.end(), [](const Edge& a, const Edge& b) {
            return a.weight < b.weight;
        });

        for (const auto& edge : edges) {
            int rootSrc = ds.find(edge.src);
            int rootDest = ds.find(edge.dest);

            if (rootSrc != rootDest) {
                result.push_back(edge);
                ds.merge(rootSrc, rootDest);
            }
        }

        return result;
    }
};
```

These are basic implementations and can be optimized further based on specific requirements and constraints.

### 1. Algorithms & Data Structures (C++): Disjoint Subsets

Disjoint Set or Union-Find data structure is used to efficiently perform operations on disjoint sets. It has two main operations: merging sets and finding the representative element of a set. Below is a C++ implementation of Disjoint Set using both the union by rank and path compression optimizations, which ensures efficient performance.

```cpp
#include <iostream>
#include <vector>

using namespace std;

class DisjointSet {
private:
    vector<int> parent;
    vector<int> rank;

public:
    DisjointSet(int n) {
        parent.resize(n);
        rank.resize(n, 0);
        // Initially, each element is its own parent
        for (int i = 0; i < n; ++i)
            parent[i] = i;
    }

    // Find operation with path compression
    int find(int x) {
        if (parent[x] != x)
            parent[x] = find(parent[x]); // Path compression
        return parent[x];
    }

    // Union operation by rank
    void merge(int x, int y) {
        int xRoot = find(x);
        int yRoot = find(y);

        // If x and y are already in the same set
        if (xRoot == yRoot)
            return;

        // Attach smaller rank tree under root of higher rank tree
        if (rank[xRoot] < rank[yRoot])
            parent[xRoot] = yRoot;
        else if (rank[xRoot] > rank[yRoot])
            parent[yRoot] = xRoot;
        else {
            // If ranks are the same, make one as root and increment its rank by one
            parent[yRoot] = xRoot;
            rank[xRoot]++;
        }
    }
};

int main() {
    int n = 5; // Number of elements
    DisjointSet ds(n);

    // Example usage
    ds.merge(0, 2);
    ds.merge(4, 2);
    ds.merge(3, 1);

    // Check if elements are in the same set
    cout << "Are 0 and 4 in the same set? " << (ds.find(0) == ds.find(4) ? "Yes" : "No") << endl;
    cout << "Are 1 and 3 in the same set? " << (ds.find(1) == ds.find(3) ? "Yes" : "No") << endl;

    return 0;
}
```

This implementation has a time complexity of approximately O(log n) for both find and merge operations, where n is the number of elements. This efficiency is achieved due to the path compression and union by rank optimizations.

### 1. Algorithms & Data Structures (C++): Immutable Sets

Immutable sets in C++ can be implemented using various data structures, but one common choice is a balanced binary search tree (BST), such as a red-black tree. The key idea behind immutable sets is that once created, they cannot be modified. Instead, any operation that would modify the set returns a new set with the desired changes, leaving the original set unchanged. Here's a basic implementation of an immutable set using a red-black tree:

```cpp
#include <iostream>
#include <memory>

enum class Color { RED, BLACK };

template <typename T>
class ImmutableSet {
private:
    struct Node {
        T data;
        std::shared_ptr<Node> left;
        std::shared_ptr<Node> right;
        Color color;

        Node(const T& val, Color col = Color::RED)
            : data(val), left(nullptr), right(nullptr), color(col) {}
    };

    std::shared_ptr<Node> root;

    std::shared_ptr<Node> insert(const std::shared_ptr<Node>& node, const T& val) const {
        if (!node) {
            return std::make_shared<Node>(val);
        }

        if (val < node->data) {
            return std::make_shared<Node>(node->data, node->color, insert(node->left, val), node->right);
        } else if (val > node->data) {
            return std::make_shared<Node>(node->data, node->color, node->left, insert(node->right, val));
        } else {
            // If the value already exists in the set, return the same set
            return node;
        }
    }

public:
    ImmutableSet() : root(nullptr) {}

    ImmutableSet(const ImmutableSet& other) : root(other.root) {}

    ImmutableSet insert(const T& val) const {
        return ImmutableSet(insert(root, val));
    }

    bool contains(const T& val) const {
        std::shared_ptr<Node> current = root;
        while (current) {
            if (val < current->data) {
                current = current->left;
            } else if (val > current->data) {
                current = current->right;
            } else {
                return true;
            }
        }
        return false;
    }
};

int main() {
    ImmutableSet<int> set;
    set = set.insert(5).insert(3).insert(8).insert(1);

    std::cout << "Set contains 3: " << std::boolalpha << set.contains(3) << std::endl;
    std::cout << "Set contains 6: " << std::boolalpha << set.contains(6) << std::endl;

    return 0;
}
```

In this implementation:

- Each node of the red-black tree contains a value of type `T`, pointers to its left and right children, and a color (either red or black).
- ImmutableSet class maintains a pointer to the root node of the tree.
- The `insert` method creates and returns a new set with the value inserted. Since sets are immutable, the original set remains unchanged.
- The `contains` method searches for a value in the set and returns true if found, false otherwise.

This implementation provides immutable sets with logarithmic time complexity for insertion and searching operations.

### 1. Algorithms & Data Structures (C++): Inclusion Exclusion

Inclusion-Exclusion is a principle in combinatorics and set theory that allows you to calculate the size of the union of multiple sets by considering their intersections. In algorithmic terms, it's often used to count or enumerate elements satisfying certain properties.

Here's a basic explanation of how it works:

1. **Inclusion Principle**: If you want to count the total number of elements in the union of several sets, you simply add the sizes of each set.

    For example, if you have sets A, B, and C, then the size of their union (denoted as \(|A \cup B \cup C|\)) is:

    \[|A \cup B \cup C| = |A| + |B| + |C|\]

2. **Exclusion Principle**: However, when you do the above, you count the elements that are in the intersection of two sets twice. To correct this, you need to subtract the sizes of the intersections of all pairs of sets.

    For two sets, A and B, the size of their union can be calculated as:

    \[|A \cup B| = |A| + |B| - |A \cap B|\]

    This removes the double counting of elements that are in both A and B.

3. **Generalization**: For more than two sets, you need to alternately add and subtract the sizes of intersections of all possible combinations of sets.

    For three sets, A, B, and C, the size of their union is:

    \[|A \cup B \cup C| = |A| + |B| + |C| - |A \cap B| - |A \cap C| - |B \cap C| + |A \cap B \cap C|\]

    Here, you add the sizes of individual sets, then subtract the sizes of all possible intersections of pairs of sets, and finally, add back the size of the intersection of all three sets to correct for the triple counting.

In coding, you can implement this principle using loops and conditional statements to iterate through all combinations of sets and calculate the size of their intersections and unions accordingly. It's particularly useful in counting problems or when dealing with probabilities involving multiple events.

### 1. Algorithms & Data Structures (C++): Inclusion Exclusion Principle

The Inclusion-Exclusion Principle is a counting technique often used in combinatorics and probability theory to find the size of the union of multiple sets. In the context of algorithms and data structures, it can be used to efficiently compute certain quantities or solve problems involving combinations of sets.

Here's how the principle works:

Let \( A_1, A_2, \ldots, A_n \) be \( n \) finite sets. The principle states that the size of the union of these sets is given by:

\[ |A_1 \cup A_2 \cup \ldots \cup A_n| = \sum_{i=1}^{n} |A_i| - \sum_{1 \leq i < j \leq n} |A_i \cap A_j| + \sum_{1 \leq i < j < k \leq n} |A_i \cap A_j \cap A_k| - \ldots + (-1)^{n+1} |A_1 \cap A_2 \cap \ldots \cap A_n| \]

In simpler terms, you start by summing the sizes of individual sets, then subtract the sizes of all pairwise intersections, then add back the sizes of all triple intersections, subtract quadruple intersections, and so on, alternating signs.

In C++, you can implement this principle using loops and nested loops to iterate over combinations of sets and compute the intersection sizes. Here's a basic example:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main() {
    // Example sets
    vector<int> A = {1, 2, 3};
    vector<int> B = {3, 4, 5};
    vector<int> C = {5, 6, 7};

    // Compute the size of the union using inclusion-exclusion principle
    int unionSize = 0;
    vector<vector<int>> sets = {A, B, C};
    int n = sets.size();

    for (int i = 0; i < n; ++i) {
        unionSize += sets[i].size();
        for (int j = i + 1; j < n; ++j) {
            vector<int> intersection;
            set_intersection(sets[i].begin(), sets[i].end(), sets[j].begin(), sets[j].end(), back_inserter(intersection));
            if ((j - i) % 2 == 1) {
                unionSize -= intersection.size();
            } else {
                unionSize += intersection.size();
            }
        }
    }

    cout << "Size of the union: " << unionSize << endl;

    return 0;
}
```

This code demonstrates how to compute the size of the union of three sets using the inclusion-exclusion principle. You can extend it to more sets by adding them to the `sets` vector and adjusting the loop accordingly.

### 1. Algorithms & Data Structures (C++): Independent Set

An independent set in a graph is a set of vertices such that no two vertices in the set are adjacent. In other words, in an independent set, no two vertices share an edge. Finding the maximum independent set in a graph is a classic problem in computer science.

Here's a basic approach to find the maximum independent set in a graph:

1. **Brute Force**: Generate all possible subsets of vertices and check if each subset forms an independent set. This approach is not efficient for large graphs due to the exponential number of subsets.

2. **Dynamic Programming (DP)**: Use dynamic programming to solve the problem efficiently. You can use a DP table where `dp[i]` represents the size of the maximum independent set in the subgraph induced by vertices `1` through `i`. The recurrence relation could be:

    ```bash
    dp[i] = max(dp[i-1], dp[i-2] + 1)
    ```

    Here, `dp[i-1]` represents the case where vertex `i` is not included in the independent set, and `dp[i-2] + 1` represents the case where vertex `i` is included, and we skip its neighbor.

3. **Greedy Algorithms**: Greedy algorithms can also be employed, although they might not always yield the optimal solution. One simple greedy approach is to iteratively select vertices with the least number of neighbors until no such vertex remains.

4. **Backtracking**: Another approach is to use backtracking, where you try all possible combinations of vertices and select the one that forms the largest independent set.

Here's a basic example of a brute force implementation in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

bool isIndependentSet(const vector<vector<int>>& graph, const vector<int>& subset) {
    for (int i : subset) {
        for (int j : subset) {
            if (i != j && graph[i][j]) {
                return false;
            }
        }
    }
    return true;
}

void findIndependentSets(const vector<vector<int>>& graph, vector<int>& subset, int index) {
    if (index == graph.size()) {
        if (isIndependentSet(graph, subset)) {
            for (int v : subset) {
                cout << v << " ";
            }
            cout << endl;
        }
        return;
    }
    subset.push_back(index);
    findIndependentSets(graph, subset, index + 1);
    subset.pop_back();
    findIndependentSets(graph, subset, index + 1);
}

int main() {
    vector<vector<int>> graph = {
        {0, 1, 1, 0},
        {1, 0, 1, 1},
        {1, 1, 0, 1},
        {0, 1, 1, 0}
    };

    vector<int> subset;
    findIndependentSets(graph, subset, 0);

    return 0;
}
```

This is a brute force approach that prints all independent sets in a given graph. For larger graphs, more efficient algorithms like dynamic programming or greedy algorithms would be preferred.

### 1. Algorithms & Data Structures (C++): Ordering Subsets

Ordering subsets in C++ involves generating permutations of a given set of elements. There are various algorithms to achieve this, but one common approach is to use recursion. Here's a simple implementation of generating permutations of a set of elements in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Function to generate permutations recursively
void generatePermutations(vector<int>& nums, int start, vector<vector<int>>& result) {
    if (start == nums.size()) {
        result.push_back(nums);
        return;
    }
    for (int i = start; i < nums.size(); ++i) {
        swap(nums[start], nums[i]);
        generatePermutations(nums, start + 1, result);
        swap(nums[start], nums[i]); // Backtrack
    }
}

// Function to print permutations
void printPermutations(const vector<vector<int>>& result) {
    for (const auto& permutation : result) {
        for (int num : permutation) {
            cout << num << " ";
        }
        cout << endl;
    }
}

int main() {
    vector<int> nums = {1, 2, 3};
    vector<vector<int>> result;
    
    generatePermutations(nums, 0, result);
    
    cout << "Permutations of {1, 2, 3}:" << endl;
    printPermutations(result);
    
    return 0;
}
```

This code will generate all permutations of the elements in the vector `nums`. The `generatePermutations` function recursively generates permutations by swapping elements. The `printPermutations` function simply prints out the permutations generated.

You can modify this code according to your needs, such as changing the input vector or adapting it to other data types.

### 1. Algorithms & Data Structures (C++): Set: Find Pairs

Sure, finding pairs in a set involves iterating through the set and checking for pairs that meet certain criteria. Here's a simple C++ code snippet to find pairs in a set:

```cpp
#include <iostream>
#include <set>
#include <utility>

using namespace std;

// Function to find pairs in a set
void findPairs(const set<int>& mySet, int targetSum) {
    set<pair<int, int>> pairs;

    for (auto it1 = mySet.begin(); it1 != mySet.end(); ++it1) {
        for (auto it2 = next(it1); it2 != mySet.end(); ++it2) {
            if (*it1 + *it2 == targetSum) {
                pairs.insert({*it1, *it2});
            }
        }
    }

    // Print pairs
    cout << "Pairs with sum " << targetSum << ":\n";
    for (const auto& pair : pairs) {
        cout << pair.first << " + " << pair.second << " = " << targetSum << endl;
    }
}

int main() {
    set<int> mySet = {1, 2, 3, 4, 5, 6, 7, 8, 9};
    int targetSum = 10;
    findPairs(mySet, targetSum);
    return 0;
}
```

This code defines a `findPairs` function that takes a set and a target sum as input. It iterates through the set using nested loops and checks if the sum of two elements equals the target sum. If a pair is found, it's inserted into another set to avoid duplicates. Finally, it prints all the pairs found with the target sum.

### 1. Algorithms & Data Structures (C++): Set: Has Unique Chars

Certainly! If you want to check if a string has all unique characters using C++, you can utilize the Set data structure. Here's how you can implement it:

```cpp
#include <iostream>
#include <unordered_set>
#include <string>

bool hasUniqueChars(const std::string& str) {
    std::unordered_set<char> charSet;
    for (char c : str) {
        if (charSet.find(c) != charSet.end()) {
            return false; // If character is already in set, it's not unique
        }
        charSet.insert(c);
    }
    return true; // All characters are unique
}

int main() {
    std::string testString = "abcdefg";
    if (hasUniqueChars(testString)) {
        std::cout << "All characters in '" << testString << "' are unique." << std::endl;
    } else {
        std::cout << "String '" << testString << "' does not have all unique characters." << std::endl;
    }
    return 0;
}
```

This code defines a function `hasUniqueChars` that takes a string as input and returns true if all characters in the string are unique, and false otherwise. It iterates over each character in the string, checking whether it's already in the set. If it's found in the set, it means the character is not unique, and the function returns false. Otherwise, it adds the character to the set. Finally, it returns true if the loop completes without finding any duplicate characters.

### 1. Algorithms & Data Structures (C++): Set: Longest Consecutive Sequence

To find the longest consecutive sequence in a set of integers using C++, you can utilize a hash set or unordered_set for efficient lookup. Here's a basic implementation:

```cpp
#include <iostream>
#include <unordered_set>
#include <vector>

using namespace std;

int longestConsecutiveSequence(const vector<int>& nums) {
    unordered_set<int> numSet(nums.begin(), nums.end());
    int longestSequence = 0;

    for (int num : numSet) {
        // Only process if the current number is the start of a sequence
        if (numSet.find(num - 1) == numSet.end()) {
            int currentNum = num;
            int currentSequence = 1;

            // Check for consecutive numbers in increasing order
            while (numSet.find(currentNum + 1) != numSet.end()) {
                currentNum++;
                currentSequence++;
            }

            longestSequence = max(longestSequence, currentSequence);
        }
    }

    return longestSequence;
}

int main() {
    vector<int> nums = {100, 4, 200, 1, 3, 2};

    int longestSequence = longestConsecutiveSequence(nums);

    cout << "The length of the longest consecutive sequence is: " << longestSequence << endl;

    return 0;
}
```

In this implementation:

1. We create an unordered_set `numSet` to store all the numbers for fast lookup.
2. We iterate through the set, and for each number `num`, we check if `num - 1` exists in the set. If it doesn't, then `num` is the start of a sequence.
3. Starting from this number, we keep incrementing `currentNum` and counting until we find the end of the consecutive sequence.
4. We update `longestSequence` with the maximum value between itself and the current sequence length.
5. Finally, we return the longest consecutive sequence length found.

### 1. Algorithms & Data Structures (C++): Set: Remove Duplicates

To remove duplicates from a set in C++, you can use the `std::set` container from the Standard Template Library (STL). The `std::set` automatically removes duplicate elements upon insertion, as it stores unique elements only. Here's a simple example:

```cpp
#include <iostream>
#include <set>

int main() {
    std::set<int> mySet = {1, 2, 3, 2, 4, 5, 1};

    // Print the set before removing duplicates
    std::cout << "Set before removing duplicates: ";
    for (const auto& elem : mySet) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    // No need to remove duplicates explicitly; std::set does it automatically

    // Print the set after removing duplicates
    std::cout << "Set after removing duplicates: ";
    for (const auto& elem : mySet) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this example, when you insert duplicate elements into the `std::set`, they are automatically removed, leaving only the unique elements. As a result, you don't need to perform an explicit removal operation for duplicates.

### 1. Algorithms & Data Structures (C++): Sets

Sets in C++ are containers that store unique elements following a specific order. They are typically implemented as binary search trees or hash tables, ensuring fast retrieval, insertion, and deletion of elements. C++ provides the `std::set` and `std::unordered_set` classes for ordered and unordered sets, respectively, in its Standard Template Library (STL).

Here's a brief overview of both:

1. **std::set**:
   - Implemented as a binary search tree.
   - Elements are sorted in ascending order by default.
   - Operations like insertion, deletion, and search have a time complexity of O(log n), where n is the number of elements in the set.
   - No duplicate elements are allowed; each element is unique.

   ```cpp
   #include <set>
   #include <iostream>

   int main() {
       std::set<int> mySet;

       mySet.insert(10);
       mySet.insert(20);
       mySet.insert(10); // Ignored, as 10 is already present

       for (int x : mySet) {
           std::cout << x << " ";
       }
       // Output: 10 20

       return 0;
   }
   ```

2. **std::unordered_set**:
   - Implemented as a hash table.
   - Elements are not sorted; they are stored in an unordered fashion.
   - Operations like insertion, deletion, and search have an average time complexity of O(1).
   - No duplicate elements are allowed; each element is unique.

   ```cpp
   #include <unordered_set>
   #include <iostream>

   int main() {
       std::unordered_set<int> mySet;

       mySet.insert(10);
       mySet.insert(20);
       mySet.insert(10); // Ignored, as 10 is already present

       for (int x : mySet) {
           std::cout << x << " ";
       }
       // Output: 10 20 (Order may vary)

       return 0;
   }
   ```

Both `std::set` and `std::unordered_set` offer efficient ways to work with sets of elements in C++, with different performance characteristics depending on whether you need ordered or unordered behavior.

### 1. Algorithms & Data Structures (C++): Subset Sum

Subset sum is a classic problem in computer science and falls under the category of dynamic programming. In the subset sum problem, you're given a set of numbers and a target sum, and you need to determine whether there exists a subset of the given set that adds up to the target sum. Here's a basic approach to solving the subset sum problem in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

bool subsetSum(vector<int>& nums, int target) {
    int n = nums.size();
    vector<vector<bool>> dp(n + 1, vector<bool>(target + 1, false));

    // Base case: an empty subset can always form sum 0
    for (int i = 0; i <= n; ++i) {
        dp[i][0] = true;
    }

    // Fill the DP table
    for (int i = 1; i <= n; ++i) {
        for (int j = 1; j <= target; ++j) {
            if (j < nums[i - 1]) {
                // If the current element is greater than the current sum, it can't be included
                dp[i][j] = dp[i - 1][j];
            } else {
                // If the current element can be included or excluded to form the sum
                dp[i][j] = dp[i - 1][j] || dp[i - 1][j - nums[i - 1]];
            }
        }
    }

    // The target sum can be formed if the last cell is true
    return dp[n][target];
}

int main() {
    vector<int> nums = {3, 34, 4, 12, 5, 2};
    int target = 9;

    if (subsetSum(nums, target)) {
        cout << "Subset with the given sum exists." << endl;
    } else {
        cout << "No subset with the given sum exists." << endl;
    }

    return 0;
}
```

This code defines a function `subsetSum` that takes a vector of integers `nums` representing the set of numbers and an integer `target` representing the target sum. It returns true if there exists a subset of `nums` that adds up to `target`, otherwise false.

The function uses dynamic programming to build a 2D DP table `dp`, where `dp[i][j]` represents whether it's possible to form sum `j` using the first `i` elements of `nums`. It initializes the DP table with base cases and fills it iteratively. Finally, it returns the value of `dp[n][target]`, where `n` is the size of `nums`.

You can modify the `nums` and `target` variables in the `main` function to test the code with different inputs.

### 1. Algorithms & Data Structures (C++): Subset sum (problem)

The Subset Sum problem is a classic algorithmic problem in computer science. The problem can be defined as follows:

Given a set of positive integers and a target sum, determine if there is a subset of the given set that adds up to the target sum.

Here's a C++ implementation of the Subset Sum problem using dynamic programming:

```cpp
#include <iostream>
#include <vector>

bool isSubsetSum(const std::vector<int>& nums, int target) {
    int n = nums.size();
    std::vector<std::vector<bool>> dp(n + 1, std::vector<bool>(target + 1, false));

    // Base case: if target is 0, empty subset always exists
    for (int i = 0; i <= n; ++i)
        dp[i][0] = true;

    for (int i = 1; i <= n; ++i) {
        for (int j = 1; j <= target; ++j) {
            if (nums[i - 1] <= j)
                dp[i][j] = dp[i - 1][j - nums[i - 1]] || dp[i - 1][j];
            else
                dp[i][j] = dp[i - 1][j];
        }
    }

    return dp[n][target];
}

int main() {
    std::vector<int> nums = {3, 34, 4, 12, 5, 2};
    int target = 9;
    if (isSubsetSum(nums, target))
        std::cout << "Subset with the given sum exists.\n";
    else
        std::cout << "No subset with the given sum exists.\n";
    return 0;
}
```

This implementation uses a dynamic programming approach where `dp[i][j]` represents whether it's possible to achieve a sum of `j` using the first `i` elements of the array `nums`. The time complexity of this solution is O(n * target), where n is the number of elements in the input array and target is the target sum.

### 1. Algorithms & Data Structures (C++): Subset sum (solution)

Sure, here's a C++ implementation of the subset sum problem using dynamic programming:

```cpp
#include <iostream>
#include <vector>

bool subsetSum(const std::vector<int>& nums, int target) {
    int n = nums.size();
    std::vector<std::vector<bool>> dp(n + 1, std::vector<bool>(target + 1, false));

    // Base case: If target is 0, we can always form an empty subset.
    for (int i = 0; i <= n; ++i) {
        dp[i][0] = true;
    }

    // DP to fill the dp table
    for (int i = 1; i <= n; ++i) {
        for (int j = 1; j <= target; ++j) {
            if (j < nums[i - 1]) {
                dp[i][j] = dp[i - 1][j];
            } else {
                dp[i][j] = dp[i - 1][j] || dp[i - 1][j - nums[i - 1]];
            }
        }
    }

    return dp[n][target];
}

int main() {
    std::vector<int> nums = {2, 3, 7, 8, 10};
    int target = 11;
    
    if (subsetSum(nums, target)) {
        std::cout << "There exists a subset that sums up to the target.\n";
    } else {
        std::cout << "No subset sums up to the target.\n";
    }

    return 0;
}
```

This code defines a function `subsetSum` that takes a vector of integers `nums` and an integer `target` and returns `true` if there exists a subset of `nums` that sums up to `target`, and `false` otherwise. It uses dynamic programming to efficiently solve the problem in O(n * target) time complexity, where n is the number of elements in `nums`.

### 1. Algorithms & Data Structures (C++): Subset Sum Queries

For solving subset sum queries efficiently, you can use dynamic programming. Here's an outline of how you can implement this in C++:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>

using namespace std;

// Function to compute the subset sum queries
vector<bool> subsetSumQueries(const vector<int>& nums, const vector<int>& queries) {
    int n = nums.size();
    int maxSum = *max_element(nums.begin(), nums.end());

    // Creating a hash table to store the results of subset sums
    unordered_map<int, bool> dp;
    dp[0] = true; // Empty set has a sum of 0

    // Precomputing the subset sums
    for (int num : nums) {
        unordered_map<int, bool> temp(dp);
        for (auto it = dp.begin(); it != dp.end(); ++it) {
            temp[it->first + num] = true;
        }
        dp = temp;
    }

    // Vector to store the results of queries
    vector<bool> results;

    // Checking if each query is possible or not
    for (int q : queries) {
        if (q <= maxSum && dp[q]) {
            results.push_back(true);
        } else {
            results.push_back(false);
        }
    }

    return results;
}

int main() {
    // Example usage
    vector<int> nums = {3, 34, 4, 12, 5, 2};
    vector<int> queries = {1, 7, 9, 10, 30};

    vector<bool> results = subsetSumQueries(nums, queries);

    cout << "Results of subset sum queries:" << endl;
    for (bool res : results) {
        cout << (res ? "Yes" : "No") << endl;
    }

    return 0;
}
```

This code uses dynamic programming to compute all possible subset sums of the given array `nums`. Then, for each query in the `queries` array, it checks if the subset sum is possible or not.

Make sure to handle large inputs efficiently, as the time complexity of this solution can be exponential in the worst case. You can optimize it further by using memoization or other techniques like bitmasking.

### 1. Algorithms & Data Structures (C++): Subset Sum to X

Certainly! The Subset Sum problem is a classic problem in computer science and can be solved using dynamic programming. The problem statement is as follows: given a set of integers and a target sum X, determine if there is a subset of the integers that adds up to X.

Here's a C++ implementation of the Subset Sum problem using dynamic programming:

```cpp
#include <iostream>
#include <vector>

bool isSubsetSum(const std::vector<int>& nums, int target) {
    int n = nums.size();
    std::vector<std::vector<bool>> dp(n + 1, std::vector<bool>(target + 1, false));

    // If the target is 0, then the subset with 0 elements always forms the target sum.
    for (int i = 0; i <= n; ++i)
        dp[i][0] = true;

    // Fill the dp table
    for (int i = 1; i <= n; ++i) {
        for (int j = 1; j <= target; ++j) {
            if (nums[i - 1] <= j) {
                // Either include the current number or exclude it.
                dp[i][j] = dp[i - 1][j - nums[i - 1]] || dp[i - 1][j];
            } else {
                // If the current number is greater than the target, exclude it.
                dp[i][j] = dp[i - 1][j];
            }
        }
    }

    // The target sum is achievable if and only if dp[n][target] is true.
    return dp[n][target];
}

int main() {
    std::vector<int> nums = {3, 34, 4, 12, 5, 2}; // Sample set of integers
    int target = 9; // Sample target sum

    if (isSubsetSum(nums, target)) {
        std::cout << "Subset with sum " << target << " exists.\n";
    } else {
        std::cout << "No subset with sum " << target << " exists.\n";
    }

    return 0;
}
```

In this implementation, we create a 2D DP table where `dp[i][j]` represents whether it's possible to form the sum `j` using the first `i` elements of the array. We fill up the DP table iteratively, considering whether we can include or exclude each number in the subset sum calculation. Finally, we return `true` if `dp[n][target]` is `true`, indicating that the target sum is achievable.

### 1. Algorithms & Data Structures (C++): Subsets - Backtracking

Sure, I can help you with that. In C++, you can use backtracking to generate all subsets of a given set. Here's a basic implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void generateSubsets(vector<int>& nums, int start, vector<int>& subset, vector<vector<int>>& result) {
    // Add the current subset to the result
    result.push_back(subset);
    
    // Iterate over remaining elements
    for (int i = start; i < nums.size(); ++i) {
        // Include the current element in the subset
        subset.push_back(nums[i]);
        
        // Recur with next element starting from i+1
        generateSubsets(nums, i + 1, subset, result);
        
        // Exclude the current element from the subset (backtrack)
        subset.pop_back();
    }
}

vector<vector<int>> subsets(vector<int>& nums) {
    vector<vector<int>> result;
    vector<int> subset;
    
    // Generate subsets starting from index 0
    generateSubsets(nums, 0, subset, result);
    
    return result;
}

int main() {
    vector<int> nums = {1, 2, 3};
    vector<vector<int>> subsets = subsets(nums);
    
    // Print all subsets
    for (auto& subset : subsets) {
        cout << "[ ";
        for (int num : subset) {
            cout << num << " ";
        }
        cout << "]" << endl;
    }
    
    return 0;
}
```

This code defines a function `generateSubsets` which recursively generates all subsets of a given vector of integers `nums`, starting from index `start`. The function maintains a current subset and adds it to the result at each recursive call. It includes the current element in the subset, recurses to generate subsets with the next elements, and then excludes the current element from the subset (backtracks).

The `subsets` function initializes an empty result vector and an empty subset vector, and then calls `generateSubsets` to generate all subsets starting from index 0.

In the `main` function, you can test the `subsets` function by providing a vector of integers. It prints all the subsets generated.

### 1. Algorithms & Data Structures (C++): Subsets that sum up to k

To find subsets of a given set of numbers that sum up to a specific value \( k \), you can use backtracking. Here's a simple C++ implementation to achieve that:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void findSubsets(vector<int>& nums, int target, int index, vector<int>& current, vector<vector<int>>& result) {
    // If target is 0, we found a subset
    if (target == 0) {
        result.push_back(current);
        return;
    }

    // If target is negative or all elements are processed
    if (target < 0 || index == nums.size()) {
        return;
    }

    // Include the current element
    current.push_back(nums[index]);
    findSubsets(nums, target - nums[index], index + 1, current, result);
    current.pop_back(); // Backtrack

    // Exclude the current element
    findSubsets(nums, target, index + 1, current, result);
}

vector<vector<int>> subsetsSumK(vector<int>& nums, int k) {
    vector<vector<int>> result;
    vector<int> current;
    findSubsets(nums, k, 0, current, result);
    return result;
}

int main() {
    vector<int> nums = {1, 2, 3, 4, 5};
    int k = 7;
    vector<vector<int>> subsets = subsetsSumK(nums, k);

    cout << "Subsets that sum up to " << k << ":\n";
    for (const auto& subset : subsets) {
        cout << "[ ";
        for (int num : subset) {
            cout << num << " ";
        }
        cout << "]\n";
    }

    return 0;
}
```

This code defines a function `subsetsSumK` that takes a vector of integers `nums` and an integer `k`. It returns a vector of vectors containing subsets of `nums` that sum up to `k`.

The `findSubsets` function performs backtracking to generate all possible subsets. It starts from the beginning of the vector `nums` and considers two cases for each element at index `index`: including it in the current subset or excluding it. If the target sum is achieved (`target == 0`), the current subset is added to the result.

In the `main` function, you can define your set of numbers in the `nums` vector and the target sum `k`. Then, it calls `subsetsSumK` and prints out the resulting subsets.

### 1. Algorithms & Data Structures (C++): Subsets that sum up to k: Complexity analysis

To analyze the complexity of finding subsets that sum up to a given value \( k \) in an array, let's outline a common approach using backtracking:

1. **Generate Subsets**: Generate all possible subsets of the array.
2. **Check Sum**: For each subset generated, check if the sum equals \( k \).

Let's break down the complexity of each step:

### Step 1: Generate Subsets

Generating all subsets of a set involves generating all possible combinations of elements. The number of subsets of a set with \( n \) elements is \( 2^n \). This is because each element can either be present or absent in a subset, leading to a total of \( 2^n \) possible combinations.

Therefore, the complexity of generating all subsets is \( O(2^n) \).

### Step 2: Check Sum

For each subset generated, we need to calculate the sum of its elements and compare it with \( k \). This involves iterating through each element in the subset and summing them up. The number of elements in a subset can vary from 0 to \( n \), where \( n \) is the number of elements in the array.

Worst-case scenario: All subsets need to be considered. For each subset, the sum needs to be calculated, which would take \( O(n) \) time. Since there are \( 2^n \) subsets, the overall time complexity for this step is \( O(n \cdot 2^n) \).

### Overall Complexity

The overall complexity is dominated by the second step, as it is higher than the first step.

Thus, the overall time complexity for finding subsets that sum up to \( k \) in an array of size \( n \) is \( O(n \cdot 2^n) \).

It's worth noting that this is an exponential-time algorithm, which means it might not be efficient for large input sizes. However, for small input sizes, it can work well. If optimization is required for larger inputs, more sophisticated algorithms like dynamic programming or memoization can be considered.

### 1. Algorithms & Data Structures (C++): Union & Find Ops

In C++, Union-Find operations are commonly used to solve problems involving disjoint sets or connected components efficiently. Here's a basic implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class UnionFind {
private:
    vector<int> parent;
    vector<int> rank;

public:
    UnionFind(int n) {
        parent.resize(n);
        rank.resize(n);
        // Initialize each element as a separate set
        for (int i = 0; i < n; ++i) {
            parent[i] = i;
            rank[i] = 0;
        }
    }

    // Find the parent of a set
    int find(int x) {
        if (parent[x] != x) {
            parent[x] = find(parent[x]); // Path compression
        }
        return parent[x];
    }

    // Union two sets
    void unionSets(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);

        if (rootX != rootY) {
            // Attach smaller rank tree under root of higher rank tree
            if (rank[rootX] < rank[rootY]) {
                parent[rootX] = rootY;
            } else if (rank[rootX] > rank[rootY]) {
                parent[rootY] = rootX;
            } else {
                parent[rootY] = rootX;
                rank[rootX]++;
            }
        }
    }

    // Check if two elements belong to the same set
    bool isConnected(int x, int y) {
        return find(x) == find(y);
    }
};

int main() {
    int n = 5; // Number of elements
    UnionFind uf(n);

    uf.unionSets(0, 1);
    uf.unionSets(2, 3);
    uf.unionSets(0, 4);

    cout << uf.isConnected(1, 4) << endl; // Output: 1 (true)
    cout << uf.isConnected(2, 4) << endl; // Output: 0 (false)

    return 0;
}
```

This implementation uses both path compression and union by rank optimizations to achieve amortized constant time complexity for both find and union operations.

### 1. Algorithms & Data Structures (C++): Union By Rank

Union by rank is a technique used in disjoint-set data structures (also known as union-find data structures) to optimize the union operation. The basic idea is to always attach the smaller tree to the root of the larger tree during a union operation. This helps keep the height of the trees low, which in turn improves the efficiency of other operations like find.

Here's how union by rank works:

1. Each element initially starts as its own set with a rank of 0.
2. When performing a union operation between two sets, the set with the smaller rank is merged into the set with the larger rank.
3. If the ranks of the two sets are equal, one of them is chosen arbitrarily to be the root, and the rank of the resulting set is incremented by 1.
4. During the find operation, paths are compressed, meaning that each node encountered on the path to the root is directly linked to the root. This optimization ensures that subsequent find operations are faster.

Here's a basic implementation of union by rank in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class DisjointSet {
private:
    vector<int> parent;
    vector<int> rank;

public:
    DisjointSet(int n) {
        parent.resize(n);
        rank.resize(n, 0);
        for (int i = 0; i < n; ++i)
            parent[i] = i;
    }

    int find(int x) {
        if (parent[x] != x)
            parent[x] = find(parent[x]);
        return parent[x];
    }

    void unite(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);
        if (rootX == rootY)
            return;

        if (rank[rootX] < rank[rootY])
            parent[rootX] = rootY;
        else if (rank[rootX] > rank[rootY])
            parent[rootY] = rootX;
        else {
            parent[rootY] = rootX;
            rank[rootX]++;
        }
    }
};

int main() {
    DisjointSet ds(5);
    ds.unite(0, 2);
    ds.unite(4, 2);
    ds.unite(3, 1);

    cout << "Are 0 and 1 in the same set? " << (ds.find(0) == ds.find(1) ? "Yes" : "No") << endl;
    cout << "Are 3 and 4 in the same set? " << (ds.find(3) == ds.find(4) ? "Yes" : "No") << endl;

    return 0;
}
```

This implementation creates a disjoint set with five elements and performs union operations on them. Finally, it checks whether certain elements belong to the same set.

### 1. Algorithms & Data Structures (C++): Unique Subset

To create a unique subset of elements from an array using C++, you can employ a combination of algorithms and data structures. One approach is to use a set data structure to store unique elements while iterating through the array. Here's a simple implementation:

```cpp
#include <iostream>
#include <vector>
#include <set>

// Function to generate unique subsets
void generateUniqueSubsets(std::vector<int>& nums, int index, std::vector<int>& subset, std::set<std::vector<int>>& result) {
    // Add the current subset to the result set
    result.insert(subset);

    // Iterate through the array starting from the current index
    for (int i = index; i < nums.size(); ++i) {
        // Include the current element in the subset
        subset.push_back(nums[i]);

        // Recursive call with the next index and updated subset
        generateUniqueSubsets(nums, i + 1, subset, result);

        // Exclude the current element from the subset (backtracking)
        subset.pop_back();
    }
}

// Function to print all subsets
void printSubsets(const std::set<std::vector<int>>& subsets) {
    for (const auto& subset : subsets) {
        std::cout << "[ ";
        for (int num : subset) {
            std::cout << num << " ";
        }
        std::cout << "]\n";
    }
}

int main() {
    std::vector<int> nums = {1, 2, 2};
    std::set<std::vector<int>> result;
    std::vector<int> subset;

    // Generate unique subsets
    generateUniqueSubsets(nums, 0, subset, result);

    // Print the unique subsets
    std::cout << "Unique Subsets:\n";
    printSubsets(result);

    return 0;
}
```

This code defines a recursive function `generateUniqueSubsets` that explores all possible subsets of the given array `nums`, ensuring uniqueness by utilizing a set `result`. Each time a subset is generated, it's added to the set. Finally, the `printSubsets` function is used to print all the unique subsets.

For input `[1, 2, 2]`, the output will be:

```bash
Unique Subsets:
[ ]
[ 1 ]
[ 1 2 ]
[ 1 2 2 ]
[ 2 ]
[ 2 2 ]
```

### 1. Algorithms & Data Structures (C++): Unique Subset

To create a unique subset of elements from an array using C++, you can employ a combination of algorithms and data structures. One approach is to use a set data structure to store unique elements while iterating through the array. Here's a simple implementation:

```cpp
#include <iostream>
#include <vector>
#include <set>

// Function to generate unique subsets
void generateUniqueSubsets(std::vector<int>& nums, int index, std::vector<int>& subset, std::set<std::vector<int>>& result) {
    // Add the current subset to the result set
    result.insert(subset);

    // Iterate through the array starting from the current index
    for (int i = index; i < nums.size(); ++i) {
        // Include the current element in the subset
        subset.push_back(nums[i]);

        // Recursive call with the next index and updated subset
        generateUniqueSubsets(nums, i + 1, subset, result);

        // Exclude the current element from the subset (backtracking)
        subset.pop_back();
    }
}

// Function to print all subsets
void printSubsets(const std::set<std::vector<int>>& subsets) {
    for (const auto& subset : subsets) {
        std::cout << "[ ";
        for (int num : subset) {
            std::cout << num << " ";
        }
        std::cout << "]\n";
    }
}

int main() {
    std::vector<int> nums = {1, 2, 2};
    std::set<std::vector<int>> result;
    std::vector<int> subset;

    // Generate unique subsets
    generateUniqueSubsets(nums, 0, subset, result);

    // Print the unique subsets
    std::cout << "Unique Subsets:\n";
    printSubsets(result);

    return 0;
}
```

This code defines a recursive function `generateUniqueSubsets` that explores all possible subsets of the given array `nums`, ensuring uniqueness by utilizing a set `result`. Each time a subset is generated, it's added to the set. Finally, the `printSubsets` function is used to print all the unique subsets.

For input `[1, 2, 2]`, the output will be:

```bash
Unique Subsets:
[ ]
[ 1 ]
[ 1 2 ]
[ 1 2 2 ]
[ 2 ]
[ 2 2 ]
```