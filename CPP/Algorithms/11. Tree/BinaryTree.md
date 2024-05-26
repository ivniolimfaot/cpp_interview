# Binary Tree

## General

### 1. Algorithms & Data Structures (C++): Binary Trees and it's Properties

Binary trees are fundamental data structures in computer science, consisting of nodes connected by edges where each node has at most two children, typically referred to as the left child and the right child. Here are some key properties and concepts related to binary trees:

1. **Binary Tree**: A binary tree is a hierarchical data structure composed of nodes, where each node has at most two children.

2. **Root**: The topmost node in a binary tree, from which all other nodes are descended.

3. **Parent, Child, Siblings**: In a binary tree, each node (except the root) has a parent node and zero, one, or two child nodes. Nodes that share the same parent are called siblings.

4. **Leaf Node**: A leaf node is a node with no children, i.e., it is a node without any outgoing edges.

5. **Internal Node**: An internal node is any node in the tree that is not a leaf, meaning it has at least one child.

6. **Depth and Height**: The depth of a node is the length of the path from the root to that node. The height of a tree is the length of the longest path from the root to a leaf node.

7. **Binary Search Tree (BST)**: A binary search tree is a binary tree in which for each node, all elements in its left subtree are less than or equal to the node's key, and all elements in its right subtree are greater than the node's key. This property enables efficient searching, insertion, and deletion operations.

8. **Traversal**: Binary trees can be traversed in different ways:
   - Inorder Traversal: Visit the left subtree, then the root, then the right subtree.
   - Preorder Traversal: Visit the root, then the left subtree, then the right subtree.
   - Postorder Traversal: Visit the left subtree, then the right subtree, then the root.

9. **Balanced Binary Trees**: A balanced binary tree is a binary tree in which the height of the left and right subtrees of any node differ by at most one. Examples include AVL trees and Red-Black trees.

10. **Complete Binary Trees**: A complete binary tree is a binary tree in which every level, except possibly the last, is completely filled, and all nodes are as far left as possible.

11. **Full Binary Trees**: A full binary tree is a binary tree in which every node other than the leaves has two children.

12. **Perfect Binary Trees**: A perfect binary tree is both full and complete, meaning all internal nodes have two children, and all leaves are at the same level.

Understanding these properties and concepts is crucial for efficiently implementing and utilizing binary trees in algorithms and data structures. In C++, you can implement binary trees using classes or structs, defining nodes with pointers to their left and right children.

### 1. Algorithms & Data Structures (C++): Binary Trees Problems

Binary trees are fascinating structures that provide a foundation for many fundamental algorithms and data structures. They're versatile and lend themselves to a wide range of problems. Here are some common problems involving binary trees in C++:

1. **Binary Tree Traversal**: Implement Depth-First Traversal methods like Preorder, Inorder, and Postorder traversal.

2. **Binary Search Tree (BST) Operations**: Implement insertion, deletion, and searching in a binary search tree.

3. **Check if a Binary Tree is a BST**: Write a function to check if a given binary tree is a binary search tree.

4. **Find Maximum Depth/Height of a Binary Tree**: Determine the maximum depth (or height) of a binary tree.

5. **Find Minimum Depth of a Binary Tree**: Determine the minimum depth of a binary tree (the shortest path from the root to a leaf node).

6. **Check if Two Binary Trees are Identical**: Write a function to check if two binary trees are identical.

7. **Find LCA (Lowest Common Ancestor) of Two Nodes in a Binary Tree**: Given two nodes in a binary tree, find their lowest common ancestor.

8. **Serialize and Deserialize a Binary Tree**: Implement functions to serialize a binary tree into a string and deserialize the string back into a tree.

9. **Mirror/Invert a Binary Tree**: Transform a binary tree into its mirror image.

10. **Find the Diameter of a Binary Tree**: Compute the diameter of a binary tree (the longest path between any two nodes).

11. **Path Sum**: Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

12. **Count the Number of Nodes in a Complete Binary Tree**: Count the number of nodes in a complete binary tree.

13. **Binary Tree Level Order Traversal**: Traverse a binary tree level by level and return the node values at each level.

14. **Convert Binary Tree to Doubly Linked List**: Convert a binary tree into a doubly linked list in place.

15. **Vertical Order Traversal of a Binary Tree**: Print binary tree in vertical order.

These are just a few examples of problems involving binary trees in C++. Each problem has its own set of algorithms and techniques to solve efficiently. Understanding and practicing these problems can help you become proficient in working with binary trees and related algorithms.

Sure, binary trees are fascinating data structures with a wide array of problems to solve. Here are some common binary tree problems along with brief descriptions:

1. **Binary Tree Traversal**:
   - **Inorder Traversal**: Traverse the left subtree, visit the root, then traverse the right subtree.
   - **Preorder Traversal**: Visit the root, traverse the left subtree, then traverse the right subtree.
   - **Postorder Traversal**: Traverse the left subtree, traverse the right subtree, then visit the root.

2. **Binary Tree Insertion & Deletion**:
   - Insertion involves finding the appropriate position for the new node and adding it.
   - Deletion involves finding the node to delete and rearranging the tree to maintain its properties.

3. **Binary Search Tree (BST) Problems**:
   - **Search**: Look for a given key in a binary search tree.
   - **Insertion & Deletion**: Maintain the binary search tree property while inserting or deleting nodes.
   - **Finding Minimum/Maximum**: Find the node with the smallest or largest key.
   - **Successor & Predecessor**: Find the next or previous node in an inorder traversal.

4. **Binary Tree Properties**:
   - **Height & Depth**: Calculate the height or depth of a binary tree.
   - **Size & Count**: Count the number of nodes in a binary tree.
   - **Check if Balanced**: Determine if a binary tree is balanced (the heights of the two subtrees of any node never differ by more than one).
   - **Check if Symmetric**: Determine if a binary tree is symmetric around its center.

5. **Binary Tree Path Problems**:
   - **Path Sum**: Check if there's a root-to-leaf path with a given sum.
   - **All Root-to-Leaf Paths**: Find all root-to-leaf paths in the binary tree.

6. **Binary Tree Conversion**:
   - **Convert Binary Tree to Doubly Linked List**: Rearrange the pointers of the binary tree to form a doubly linked list.

7. **Binary Tree Reconstruction**:
   - **Construct Binary Tree from Inorder and Preorder/Postorder Traversals**: Given the inorder and either preorder or postorder traversal of a binary tree, reconstruct the tree.
   - **Construct Binary Search Tree from Sorted Array**: Given a sorted array, construct a balanced binary search tree.

These are just a few examples, but there are many more problems and variations to explore within the realm of binary trees!

### 1. Algorithms & Data Structures (C++): Binary Trees: Array Representation of Binary Trees

In the array representation of binary trees, you can store the elements of a binary tree in an array such that you don't waste memory like you would with pointers, and you can still efficiently traverse the tree. This method is particularly useful when dealing with complete binary trees.

Here's how it works:

1. **Root at index 0**: The root of the tree is stored at index 0 of the array.

2. **Parent-Child Relationship**: For any node at index i:
   - Its left child is at index 2*i + 1.
   - Its right child is at index 2*i + 2.

3. **Empty Nodes**: If a node doesn't have a left or right child, the corresponding array indices will be empty.

This representation ensures that the elements of each level of the binary tree are stored consecutively in the array.

Here's a simple example to illustrate this in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class BinaryTree {
private:
    vector<int> treeArray;

public:
    BinaryTree() {}

    // Function to insert a node into the array representation of the binary tree
    void insert(int value) {
        treeArray.push_back(value);
    }

    // Function to print the array representation of the binary tree
    void printArray() {
        cout << "Array Representation of Binary Tree: ";
        for (int i = 0; i < treeArray.size(); i++) {
            cout << treeArray[i] << " ";
        }
        cout << endl;
    }
};

int main() {
    BinaryTree tree;

    // Inserting elements into the binary tree
    tree.insert(1);
    tree.insert(2);
    tree.insert(3);
    tree.insert(4);
    tree.insert(5);
    tree.insert(6);
    tree.insert(7);

    // Printing the array representation of the binary tree
    tree.printArray();

    return 0;
}
```

Output:

```bash
Array Representation of Binary Tree: 1 2 3 4 5 6 7 
```

In this example, the tree represented is:

```bash
      1
     / \
    2   3
   / \ / \
  4  5 6  7
```

And its array representation is `[1, 2, 3, 4, 5, 6, 7]`.

### 1. Algorithms & Data Structures (C++): Binary Tree Pruning

Pruning a binary tree involves removing nodes with certain properties from the tree while preserving the structural integrity of the tree. In the case of binary trees, pruning typically involves removing nodes with specific values or characteristics.

Here's how you can implement binary tree pruning in C++:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

TreeNode* pruneTree(TreeNode* root) {
    if (root == nullptr) {
        return nullptr;
    }

    // Recursively prune left and right subtrees
    root->left = pruneTree(root->left);
    root->right = pruneTree(root->right);

    // If the current node is a leaf node and its value is 0, prune it
    if (root->left == nullptr && root->right == nullptr && root->val == 0) {
        delete root;
        return nullptr;
    }

    return root;
}

// Utility function to print the tree (preorder traversal)
void printTree(TreeNode* root) {
    if (root == nullptr) {
        return;
    }
    std::cout << root->val << " ";
    printTree(root->left);
    printTree(root->right);
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(0);
    root->right = new TreeNode(1);
    root->left->left = new TreeNode(0);
    root->left->right = new TreeNode(0);
    root->right->left = new TreeNode(0);
    root->right->right = new TreeNode(1);

    std::cout << "Original tree: ";
    printTree(root);
    std::cout << std::endl;

    root = pruneTree(root);

    std::cout << "Pruned tree: ";
    printTree(root);
    std::cout << std::endl;

    return 0;
}
```

In this implementation:

- The `pruneTree` function recursively traverses the binary tree and prunes nodes with a value of 0 that have no children (i.e., leaf nodes).
- The `printTree` function is a utility function to print the binary tree using preorder traversal.
- In the `main` function, an example tree is created, pruned, and then printed before and after pruning.

You can modify this implementation to suit your specific requirements, such as different conditions for pruning or different node structures.

### 1. Algorithms & Data Structures (C++): Binary Tree Representation

Representing a binary tree in C++ involves defining a structure for each node and implementing various methods for tree traversal, insertion, deletion, and other operations. Here's a basic implementation:

```cpp
#include <iostream>

using namespace std;

// Define the structure for a binary tree node
struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;

    // Constructor
    TreeNode(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Function to create a new node
TreeNode* createNode(int data) {
    return new TreeNode(data);
}

// Function to insert a new node
void insert(TreeNode* &root, int data) {
    if (root == nullptr) {
        root = createNode(data);
        return;
    }

    if (data < root->data)
        insert(root->left, data);
    else
        insert(root->right, data);
}

// Function to perform inorder traversal
void inorder(TreeNode* root) {
    if (root == nullptr) return;

    inorder(root->left);
    cout << root->data << " ";
    inorder(root->right);
}

// Function to perform preorder traversal
void preorder(TreeNode* root) {
    if (root == nullptr) return;

    cout << root->data << " ";
    preorder(root->left);
    preorder(root->right);
}

// Function to perform postorder traversal
void postorder(TreeNode* root) {
    if (root == nullptr) return;

    postorder(root->left);
    postorder(root->right);
    cout << root->data << " ";
}

int main() {
    TreeNode* root = nullptr;

    // Insert elements into the tree
    insert(root, 10);
    insert(root, 5);
    insert(root, 15);
    insert(root, 3);
    insert(root, 7);

    // Display the tree using different traversal techniques
    cout << "Inorder traversal: ";
    inorder(root);
    cout << endl;

    cout << "Preorder traversal: ";
    preorder(root);
    cout << endl;

    cout << "Postorder traversal: ";
    postorder(root);
    cout << endl;

    return 0;
}
```

This code defines a `TreeNode` structure representing a node in the binary tree. It includes methods to insert nodes into the tree and perform different types of tree traversals (inorder, preorder, postorder). Finally, it demonstrates how to use these methods in the `main` function.

### 1. Algorithms & Data Structures (C++): Binary Tree Representation - Array Based

Representing a binary tree using an array is a common method that allows for efficient storage and traversal of the tree's elements. Each node of the binary tree is stored at a specific index in the array, and the relationships between nodes can be determined using simple arithmetic calculations.

Here's a basic implementation of representing a binary tree using an array in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Binary Tree Node
struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;
};

// Binary Tree Class
class BinaryTree {
private:
    vector<int> treeArray;

public:
    // Constructor
    BinaryTree() {}

    // Function to insert a node into the tree
    void insertNode(int data) {
        treeArray.push_back(data);
    }

    // Function to get the parent index of a given node index
    int getParentIndex(int childIndex) {
        return (childIndex - 1) / 2;
    }

    // Function to get the left child index of a given node index
    int getLeftChildIndex(int parentIndex) {
        return (2 * parentIndex) + 1;
    }

    // Function to get the right child index of a given node index
    int getRightChildIndex(int parentIndex) {
        return (2 * parentIndex) + 2;
    }

    // Function to get the value of a node at a given index
    int getNodeValue(int index) {
        if (index >= treeArray.size())
            return -1; // Invalid index
        return treeArray[index];
    }
};

int main() {
    BinaryTree tree;
    tree.insertNode(1);
    tree.insertNode(2);
    tree.insertNode(3);
    tree.insertNode(4);
    tree.insertNode(5);

    cout << "Parent of 2: " << tree.getNodeValue(tree.getParentIndex(1)) << endl;
    cout << "Left Child of 1: " << tree.getNodeValue(tree.getLeftChildIndex(0)) << endl;
    cout << "Right Child of 1: " << tree.getNodeValue(tree.getRightChildIndex(0)) << endl;

    return 0;
}
```

In this implementation:

- Each node of the binary tree is represented by an element in the `treeArray` vector.
- The parent-child relationships between nodes can be determined using index calculations.
- The root of the tree is stored at index 0. For any node at index `i`, its left child is at index `2*i + 1`, and its right child is at index `2*i + 2`.
- Functions like `getParentIndex`, `getLeftChildIndex`, and `getRightChildIndex` are provided to compute these relationships.
- Nodes are inserted into the treeArray using the `insertNode` function.
- You can access the value of a node at a given index using the `getNodeValue` function.

This representation allows for easy access to nodes and their relationships, making it suitable for various binary tree algorithms and operations.

### 1. Algorithms & Data Structures (C++): Binary Tree Representation - Linked Based

Sure, I can guide you through creating a binary tree representation using linked structures in C++. In a linked representation, each node in the tree contains pointers to its left and right children. Here's a basic implementation:

```cpp
#include <iostream>

using namespace std;

// Define the structure for a tree node
struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;

    // Constructor
    TreeNode(int value) : data(value), left(nullptr), right(nullptr) {}
};

// Function to insert a new node into the binary tree
void insert(TreeNode* &root, int value) {
    // If the tree is empty, create a new node and make it the root
    if (root == nullptr) {
        root = new TreeNode(value);
        return;
    }

    // Otherwise, traverse the tree to find the appropriate position
    if (value < root->data) {
        insert(root->left, value); // Recursively insert into the left subtree
    } else {
        insert(root->right, value); // Recursively insert into the right subtree
    }
}

// Function to traverse the tree in-order (left-root-right)
void inOrderTraversal(TreeNode* root) {
    if (root == nullptr) return;

    inOrderTraversal(root->left);
    cout << root->data << " ";
    inOrderTraversal(root->right);
}

int main() {
    // Initialize an empty tree
    TreeNode* root = nullptr;

    // Insert some values into the tree
    insert(root, 10);
    insert(root, 5);
    insert(root, 15);
    insert(root, 3);
    insert(root, 8);

    // Perform in-order traversal to display the contents of the tree
    cout << "In-order traversal: ";
    inOrderTraversal(root);
    cout << endl;

    return 0;
}
```

This code defines a `TreeNode` structure representing each node in the binary tree. The `insert` function is used to add nodes to the tree, maintaining the binary search tree property (smaller values to the left, larger values to the right). Finally, the `inOrderTraversal` function performs an in-order traversal of the tree, printing out the elements in sorted order.

### 1. Algorithms & Data Structures (C++): Binary Tree Right Side View

The binary tree right side view problem asks you to return all the nodes visible from the right side of the binary tree. Here's how you can solve it using C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

vector<int> rightSideView(TreeNode* root) {
    vector<int> result;
    if (!root) return result;

    queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        int size = q.size();
        for (int i = 0; i < size; ++i) {
            TreeNode* node = q.front();
            q.pop();

            if (i == size - 1) {
                result.push_back(node->val); // Rightmost node at each level
            }

            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }
    }

    return result;
}

// Utility function to create a new tree node.
TreeNode* newNode(int data) {
    TreeNode* node = new TreeNode(data);
    return node;
}

int main() {
    TreeNode* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->right = newNode(5);
    root->right->right = newNode(4);

    vector<int> result = rightSideView(root);

    cout << "Right side view of the binary tree: ";
    for (int i = 0; i < result.size(); ++i) {
        cout << result[i] << " ";
    }
    cout << endl;

    return 0;
}
```

This code defines a `TreeNode` structure and a function `rightSideView` to find the right side view of a binary tree. It uses a level-order traversal (BFS) to visit each level of the tree, keeping track of the rightmost node at each level. Finally, it returns a vector containing the values of these rightmost nodes.

### 1. Algorithms & Data Structures (C++): Binary Tree: K-th Level

To find all nodes at the K-th level of a binary tree, you can perform a level-order traversal (also known as breadth-first traversal) of the tree. This traversal visits all the nodes at each level before moving to the next level. Here's how you can implement this in C++:

```cpp
#include <iostream>
#include <queue>
using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

vector<int> nodesAtKthLevel(TreeNode* root, int k) {
    vector<int> result;
    if (root == nullptr || k < 1) {
        return result;
    }
    
    queue<TreeNode*> q;
    q.push(root);
    int level = 1;
    
    while (!q.empty() && level <= k) {
        int size = q.size();
        for (int i = 0; i < size; ++i) {
            TreeNode* curr = q.front();
            q.pop();
            if (level == k) {
                result.push_back(curr->val);
            }
            if (curr->left != nullptr) {
                q.push(curr->left);
            }
            if (curr->right != nullptr) {
                q.push(curr->right);
            }
        }
        level++;
    }
    
    return result;
}

int main() {
    // Example Usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(7);

    int k = 2;
    vector<int> nodes = nodesAtKthLevel(root, k);
    cout << "Nodes at level " << k << ": ";
    for (int node : nodes) {
        cout << node << " ";
    }
    cout << endl;

    // Clean up
    delete root->right->right;
    delete root->right->left;
    delete root->left->right;
    delete root->left->left;
    delete root->right;
    delete root->left;
    delete root;

    return 0;
}
```

This code defines a function `nodesAtKthLevel` that takes the root of the binary tree and the level `k` as input and returns a vector containing all the node values at the K-th level. It performs a level-order traversal using a queue. Finally, in the `main` function, an example usage is demonstrated with a sample binary tree.

### 1. Algorithms & Data Structures (C++): Binary Tree: Level Order Build

Sure! In C++, you can build a binary tree level by level using the level order traversal approach. This method typically involves using a queue to keep track of the nodes as you traverse the tree level by level.

Here's a basic implementation:

```cpp
#include <iostream>
#include <queue>

using namespace std;

// Define the structure of a binary tree node
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

// Function to build a binary tree level by level
TreeNode* levelOrderBuild(vector<int>& nums) {
    if (nums.empty()) return nullptr;
    
    TreeNode* root = new TreeNode(nums[0]);
    queue<TreeNode*> q;
    q.push(root);

    int i = 1;
    while (i < nums.size()) {
        TreeNode* current = q.front();
        q.pop();

        // Create left child if possible
        if (i < nums.size() && nums[i] != -1) {
            current->left = new TreeNode(nums[i]);
            q.push(current->left);
        }
        i++;

        // Create right child if possible
        if (i < nums.size() && nums[i] != -1) {
            current->right = new TreeNode(nums[i]);
            q.push(current->right);
        }
        i++;
    }
    return root;
}

// Function to print the tree using inorder traversal (for verification)
void inorderTraversal(TreeNode* root) {
    if (root == nullptr) return;
    inorderTraversal(root->left);
    cout << root->val << " ";
    inorderTraversal(root->right);
}

int main() {
    vector<int> nums = {1, 2, 3, 4, 5, -1, 6, -1, -1, 7}; // Example input
    TreeNode* root = levelOrderBuild(nums);

    // Print the tree to verify
    inorderTraversal(root);

    return 0;
}
```

This code builds a binary tree from a vector of integers `nums`, where `-1` denotes a null node. It uses a queue to keep track of the nodes while traversing the tree level by level. Finally, it prints the tree using inorder traversal for verification.

You can modify the input vector `nums` to create different binary trees.

### 1. Algorithms & Data Structures (C++): Binary Tree: Level Order Print

Sure! Level order traversal, also known as breadth-first traversal, is a method to traverse a binary tree by visiting nodes level by level, from left to right. Here's how you can implement level order traversal in C++:

```cpp
#include <iostream>
#include <queue>

using namespace std;

// Node definition for the binary tree
struct Node {
    int data;
    Node* left;
    Node* right;

    Node(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Function to perform level order traversal of a binary tree
void levelOrderPrint(Node* root) {
    if (root == nullptr) return;

    // Create a queue to store the nodes
    queue<Node*> q;
    q.push(root);

    while (!q.empty()) {
        // Get the front node of the queue and remove it
        Node* current = q.front();
        q.pop();

        // Print the data of the current node
        cout << current->data << " ";

        // Enqueue the left child if it exists
        if (current->left != nullptr) {
            q.push(current->left);
        }

        // Enqueue the right child if it exists
        if (current->right != nullptr) {
            q.push(current->right);
        }
    }
}

// Example usage
int main() {
    // Creating a binary tree
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    root->right->left = new Node(6);
    root->right->right = new Node(7);

    // Printing the level order traversal of the binary tree
    cout << "Level Order Traversal: ";
    levelOrderPrint(root);
    cout << endl;

    return 0;
}
```

This code defines a binary tree node structure and a function `levelOrderPrint` to perform level order traversal. The main function demonstrates how to use this function with an example binary tree.

### 1. Algorithms & Data Structures (C++): Binary Tree: Max Value

Sure, here's how you can find the maximum value in a binary tree using C++:

```cpp
#include <iostream>
#include <climits>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to find the maximum value in a binary tree
int maxInBinaryTree(TreeNode* root) {
    if (root == nullptr) {
        // If the tree is empty, return the minimum possible integer value
        return INT_MIN;
    } else {
        // Recursively find the maximum value in the left and right subtrees
        int maxValue = root->val;
        int leftMax = maxInBinaryTree(root->left);
        int rightMax = maxInBinaryTree(root->right);
        
        // Compare the maximum values of the current node, left subtree, and right subtree
        if (leftMax > maxValue)
            maxValue = leftMax;
        if (rightMax > maxValue)
            maxValue = rightMax;
        
        return maxValue;
    }
}

// Test program
int main() {
    // Create a sample binary tree
    TreeNode* root = new TreeNode(10);
    root->left = new TreeNode(5);
    root->right = new TreeNode(15);
    root->left->left = new TreeNode(3);
    root->left->right = new TreeNode(7);
    root->right->right = new TreeNode(18);

    // Find the maximum value in the binary tree
    int maxVal = maxInBinaryTree(root);
    std::cout << "Maximum value in the binary tree: " << maxVal << std::endl;

    // Clean up memory
    delete root->left->left;
    delete root->left->right;
    delete root->right->right;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

This code defines a `TreeNode` struct for the binary tree node and a function `maxInBinaryTree` to find the maximum value in the binary tree. In the `main` function, a sample binary tree is created, and then the maximum value in the tree is found using the `maxInBinaryTree` function. Finally, memory allocated for the tree nodes is freed to prevent memory leaks.

### 1. Algorithms & Data Structures (C++): Binary Tree: Min Depth

Certainly! In C++, you can find the minimum depth of a binary tree using a depth-first search (DFS) algorithm. Here's a simple implementation:

```cpp
#include <iostream>
#include <queue>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

int minDepth(TreeNode* root) {
    if (root == nullptr) return 0;

    queue<pair<TreeNode*, int>> q;
    q.push({root, 1});

    while (!q.empty()) {
        TreeNode* node = q.front().first;
        int depth = q.front().second;
        q.pop();

        // Check if the current node is a leaf node
        if (node->left == nullptr && node->right == nullptr) {
            return depth;
        }

        // Enqueue left child if it exists
        if (node->left) {
            q.push({node->left, depth + 1});
        }

        // Enqueue right child if it exists
        if (node->right) {
            q.push({node->right, depth + 1});
        }
    }

    return -1; // This line should never be reached for a non-empty binary tree
}

int main() {
    // Example usage:
    // Constructing a binary tree
    TreeNode* root = new TreeNode(3);
    root->left = new TreeNode(9);
    root->right = new TreeNode(20);
    root->right->left = new TreeNode(15);
    root->right->right = new TreeNode(7);

    cout << "Minimum depth of the binary tree: " << minDepth(root) << endl;

    // Deallocating memory (Optional)
    delete root->right->right;
    delete root->right->left;
    delete root->right;
    delete root->left;
    delete root;

    return 0;
}
```

This code implements a BFS traversal of the binary tree, keeping track of the depth of each node. It stops as soon as it reaches a leaf node and returns its depth.

### 1. Algorithms & Data Structures (C++): Binary Tree: Min Value

To find the minimum value in a binary tree implemented in C++, you typically perform a depth-first search (DFS) traversal, specifically an in-order traversal, as it visits nodes in non-decreasing order. Here's a basic implementation:

```cpp
#include <iostream>
#include <climits>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class BinaryTree {
public:
    int findMin(TreeNode* root) {
        if (root == nullptr)
            return INT_MAX; // Return maximum integer value if tree is empty
        
        int min_val = root->val; // Initialize min_val with root's value
        
        // Recursively find minimum value in left and right subtrees
        int left_min = findMin(root->left);
        int right_min = findMin(root->right);
        
        // Update min_val if minimum value is found in left or right subtree
        min_val = std::min(min_val, std::min(left_min, right_min));
        
        return min_val;
    }
};

int main() {
    // Example usage
    TreeNode* root = new TreeNode(5);
    root->left = new TreeNode(3);
    root->right = new TreeNode(8);
    root->left->left = new TreeNode(2);
    root->left->right = new TreeNode(4);
    
    BinaryTree tree;
    std::cout << "Minimum value in the binary tree: " << tree.findMin(root) << std::endl;

    // Clean up memory
    delete root->left->left;
    delete root->left->right;
    delete root->left;
    delete root->right;
    delete root;
    
    return 0;
}
```

In this code:

- The `TreeNode` struct represents a node in the binary tree.
- The `BinaryTree` class contains the `findMin` function, which recursively traverses the binary tree to find the minimum value.
- In the `main` function, an example binary tree is created and the `findMin` function is called on its root node.

Remember to free the allocated memory using `delete` to avoid memory leaks.

### 1. Algorithms & Data Structures (C++): Binary Trees: Important Terminologies

In the realm of algorithms and data structures, binary trees are fundamental structures used for organizing and storing data efficiently. Here are some important terminologies related to binary trees:

1. **Binary Tree**: A binary tree is a hierarchical data structure composed of nodes, where each node has at most two children, referred to as the left child and the right child.

2. **Root**: The topmost node of a binary tree is called the root. It is the starting point for traversing the tree.

3. **Node**: Each element in a binary tree is called a node. Each node contains a value and pointers or references to its left and right children.

4. **Parent Node**: A node which has one or more children is called a parent node.

5. **Child Node**: Nodes that are directly connected to a parent node are its children. A node can have at most two children.

6. **Leaf Node**: A leaf node is a node that does not have any children. In other words, it is a node with both left and right child pointers null.

7. **Internal Node**: Any node of a binary tree that has at least one child is called an internal node.

8. **Depth of a Node**: The depth of a node in a binary tree is the length of the path from the root to that node. The depth of the root is 0.

9. **Height of a Tree**: The height of a binary tree is the length of the longest path from the root node to a leaf node. Alternatively, it is the maximum depth of any node in the tree.

10. **Binary Search Tree (BST)**: A binary search tree is a special type of binary tree where the nodes are arranged in a specific order such that for each node, all elements in its left subtree are less than the node's value, and all elements in its right subtree are greater than the node's value. This ordering property enables efficient searching, insertion, and deletion operations.

11. **Traversal**: Traversal refers to visiting and processing each node in a binary tree in a specific order. Common traversal methods include in-order, pre-order, and post-order traversals.

12. **In-order Traversal**: In an in-order traversal, nodes are visited in the order: left, root, right. This traversal visits the nodes in non-decreasing order when applied to a binary search tree.

13. **Pre-order Traversal**: In a pre-order traversal, nodes are visited in the order: root, left, right.

14. **Post-order Traversal**: In a post-order traversal, nodes are visited in the order: left, right, root.

15. **Level-order Traversal**: In a level-order traversal, nodes are visited level by level, starting from the root and moving to the next level before traversing the nodes at that level from left to right.

These terminologies are fundamental for understanding and working with binary trees in algorithms and data structures, particularly in languages like C++.

### 1. Algorithms & Data Structures (C++): Binary Trees: Maximum Height for a Binary Tree

To find the maximum height of a binary tree with "n" nodes, we need to understand a few concepts. The height of a binary tree is the longest path from the root to a leaf node. In a binary tree, each node can have at most two children: left and right.

One approach to finding the maximum height is to realize that in a well-balanced binary tree, each level doubles the number of nodes compared to the previous level. This suggests that the height of a balanced binary tree is logarithmic with respect to the number of nodes.

For example, if there are 'n' nodes in the tree, the height 'h' would be roughly logarithmic, i.e., h ≈ log₂(n). This is because at each level, the number of nodes roughly doubles (since each node can have at most two children), and to get 'n' nodes, we need to double roughly 'log₂(n)' times.

However, if the binary tree is not balanced, the height can be worse, even linear (n-1) in the worst-case scenario, where the tree degenerates into a linked list.

In C++, you can implement a binary tree and a function to calculate its maximum height using a recursive approach. Here's a sample implementation:

```cpp
#include <iostream>
#include <algorithm>

struct Node {
    int data;
    Node* left;
    Node* right;
    
    Node(int val) : data(val), left(nullptr), right(nullptr) {}
};

int maxHeight(Node* node) {
    if (node == nullptr)
        return 0;
    else {
        int leftHeight = maxHeight(node->left);
        int rightHeight = maxHeight(node->right);
        
        return 1 + std::max(leftHeight, rightHeight);
    }
}

int main() {
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    root->right->left = new Node(6);
    root->right->right = new Node(7);

    std::cout << "Maximum height of the binary tree: " << maxHeight(root) << std::endl;

    return 0;
}
```

In this implementation, the `maxHeight` function recursively calculates the maximum height of the binary tree rooted at the given node by finding the maximum height of its left and right subtrees and adding 1 (to account for the current node). The `main` function demonstrates how to use this function with a sample binary tree.

### 1. Algorithms & Data Structures (C++): Binary Trees: Maximum number of Nodes Possible in a Binary Tree of Height "h"

In a binary tree, the maximum number of nodes possible in a tree of height "h" occurs when every level of the tree is completely filled, except possibly the last level, which is filled from left to right. This type of tree is called a "complete binary tree".

For a binary tree of height "h":

- The number of nodes at level 0 (root) is 1.
- The number of nodes at level 1 is 2 (each node at level 0 has two children).
- The number of nodes at level 2 is 4 (each node at level 1 has two children).
- The number of nodes at level 3 is 8 (each node at level 2 has two children).
- ...
- The number of nodes at level "h" is 2^h.

So, the maximum number of nodes in a binary tree of height "h" is the sum of nodes at all levels up to level "h", which can be calculated using the sum of a geometric series formula:

\[ \text{Total number of nodes} = 1 + 2 + 4 + 8 + \ldots + 2^h = \sum_{i=0}^{h} 2^i = 2^{h+1} - 1 \]

Therefore, the maximum number of nodes in a binary tree of height "h" is \(2^{h+1} - 1\).

### 1. Algorithms & Data Structures (C++): Binary Trees: Minimum Height for a Binary Tree with "n" Nodes

To find the minimum height for a binary tree with "n" nodes, we can utilize the property of a complete binary tree. A complete binary tree is a binary tree in which every level, except possibly the last, is completely filled, and all nodes are as far left as possible.

The minimum height of a binary tree with "n" nodes can be achieved when the tree is as complete as possible. The formula to calculate the minimum height of a binary tree with "n" nodes is:

\[ \text{Minimum Height} = \lceil \log_2(n+1) \rceil - 1 \]

Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <cmath>

using namespace std;

// Node definition
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to calculate minimum height of binary tree with n nodes
int minBinaryTreeHeight(int n) {
    return ceil(log2(n + 1)) - 1;
}

int main() {
    int n;
    cout << "Enter the number of nodes in the binary tree: ";
    cin >> n;

    int minHeight = minBinaryTreeHeight(n);
    cout << "Minimum height of binary tree with " << n << " nodes: " << minHeight << endl;

    return 0;
}
```

This code calculates the minimum height of a binary tree with "n" nodes using the formula mentioned above. You'll need to provide the number of nodes as input, and it will output the minimum height of the binary tree.

### 1. Algorithms & Data Structures (C++): Binary Trees: Minimum number of Nodes Possible in a Binary Tree of Height "h"

To determine the minimum number of nodes possible in a binary tree of height "h," you need to consider the characteristics of a binary tree. In a binary tree, each node can have at most two children, left and right. The minimum number of nodes in a binary tree of height "h" is achieved when the tree is complete or full.

A complete binary tree is a binary tree in which every level, except possibly the last, is completely filled, and all nodes are as far left as possible. A full binary tree is a binary tree in which every node other than the leaves has two children.

For a complete binary tree of height "h," the minimum number of nodes can be calculated using the formula:

\[2^{h+1} - 1\]

For a full binary tree of height "h," the minimum number of nodes can be calculated using the formula:

\[2^h - 1\]

Let's see how to implement this in C++:

```cpp
#include <iostream>
#include <cmath>

using namespace std;

// Function to calculate the minimum number of nodes in a complete binary tree
int minNodesInCompleteBinaryTree(int height) {
    return (pow(2, height + 1) - 1);
}

// Function to calculate the minimum number of nodes in a full binary tree
int minNodesInFullBinaryTree(int height) {
    return (pow(2, height) - 1);
}

int main() {
    int height;
    cout << "Enter the height of the binary tree: ";
    cin >> height;

    cout << "Minimum number of nodes in a complete binary tree of height " << height << " is: "
         << minNodesInCompleteBinaryTree(height) << endl;

    cout << "Minimum number of nodes in a full binary tree of height " << height << " is: "
         << minNodesInFullBinaryTree(height) << endl;

    return 0;
}
```

This code first takes the height of the binary tree as input and then calculates the minimum number of nodes for both complete and full binary trees using the provided formulas. Finally, it prints out the results.

### 1. Algorithms & Data Structures (C++): Binary Trees: Number of Binary Trees possible with n Nodes

To find the number of binary trees possible with `n` nodes, you can use the concept of Catalan numbers. The formula for Catalan numbers can be used to calculate this. Here's how you can do it:

```cpp
#include <iostream>
using namespace std;

// Function to calculate factorial
unsigned long long factorial(int n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}

// Function to calculate number of binary trees
unsigned long long numberOfBinaryTrees(int n) {
    // Use Catalan number formula
    return factorial(2 * n) / (factorial(n + 1) * factorial(n));
}

int main() {
    int n;
    cout << "Enter the number of nodes: ";
    cin >> n;
    cout <<

```cpp
    "Number of Binary Trees possible with " << n << " nodes: " << numberOfBinaryTrees(n) << endl;
    return 0;
}
```

This code calculates the number of binary trees possible with `n` nodes using the Catalan number formula. Make sure to include the `factorial` function defined above.

### 1. Algorithms & Data Structures (C++): Count Leaf Nodes of a Binary Tree

Counting the leaf nodes of a binary tree involves traversing the tree and identifying nodes that have no children (i.e., they are leaf nodes). You can accomplish this using a depth-first search (DFS) or breadth-first search (BFS) algorithm. Here's how you can implement it in C++ using a simple DFS approach:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to count leaf nodes in a binary tree
int countLeafNodes(TreeNode* root) {
    // Base case: if root is null, return 0
    if (root == nullptr)
        return 0;
    // If root is a leaf node, return 1
    if (root->left == nullptr && root->right == nullptr)
        return 1;
    // Recursively count leaf nodes in left and right subtrees
    return countLeafNodes(root->left) + countLeafNodes(root->right);
}

// Test the implementation
int main() {
    // Create a binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(7);

    // Count leaf nodes
    int leafCount = countLeafNodes(root);
    std::cout << "Number of leaf nodes: " << leafCount << std::endl;

    // Clean up memory
    delete root->left->left;
    delete root->left->right;
    delete root->right->left;
    delete root->right->right;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

This code defines a `TreeNode` struct representing a node in the binary tree and implements the `countLeafNodes` function to count the leaf nodes recursively. Finally, it tests the implementation by creating a binary tree and counting its leaf nodes.

### 1. Algorithms & Data Structures (C++): Count Number of Nodes in Binary Tree

To count the number of nodes in a binary tree, you can perform a depth-first search (DFS) traversal of the tree and count the nodes as you visit them. Here's a C++ implementation using a recursive approach:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

int countNodes(TreeNode* root) {
    if (root == nullptr)
        return 0;
    else
        return 1 + countNodes(root->left) + countNodes(root->right);
}

// Utility function to create a new binary tree node.
TreeNode* newNode(int data) {
    TreeNode* temp = new TreeNode(data);
    return temp;
}

int main() {
    // Creating a binary tree
    TreeNode* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);

    // Counting the number of nodes
    std::cout << "Number of nodes in the binary tree: " << countNodes(root) << std::endl;

    return 0;
}
```

In this code:

- `countNodes` is the recursive function that traverses the binary tree and counts the nodes.
- It returns 0 if the current node is null (indicating an empty subtree).
- Otherwise, it returns 1 (for the current node) plus the count of nodes in its left subtree and the count of nodes in its right subtree.
- In the `main()` function, a sample binary tree is created, and the `countNodes()` function is called to count the number of nodes in the tree.

### 1. Algorithms & Data Structures (C++): Convert Binary Search Tree To Sorted Doubly Linked List

To convert a Binary Search Tree (BST) to a sorted doubly linked list, you can perform an in-order traversal of the BST while updating the links to form the doubly linked list. Here's a C++ implementation:

```cpp
#include <iostream>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

// Definition for a doubly-linked list node.
struct DoublyListNode {
    int val;
    DoublyListNode* prev;
    DoublyListNode* next;
    DoublyListNode(int x) : val(x), prev(NULL), next(NULL) {}
};

class Solution {
public:
    DoublyListNode* treeToDoublyList(TreeNode* root) {
        if (!root) return nullptr;
        
        DoublyListNode* dummy = new DoublyListNode(0);
        DoublyListNode* prev = dummy;
        
        // Perform in-order traversal
        inorder(root, prev);
        
        // Adjust pointers to form a circular doubly linked list
        prev->next->prev = nullptr;
        dummy->next->prev = prev;
        
        return dummy->next;
    }
    
    // Recursive in-order traversal
    void inorder(TreeNode* root, DoublyListNode*& prev) {
        if (!root) return;
        
        inorder(root->left, prev);
        
        // Convert the current node to a doubly linked list node
        DoublyListNode* curr = new DoublyListNode(root->val);
        prev->next = curr;
        curr->prev = prev;
        prev = curr;
        
        inorder(root->right, prev);
    }
};

// Helper function to print the doubly linked list
void printDoublyList(DoublyListNode* head) {
    while (head) {
        cout << head->val << " ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(4);
    root->left = new TreeNode(2);
    root->right = new TreeNode(5);
    root->left->left = new TreeNode(1);
    root->left->right = new TreeNode(3);

    Solution sol;
    DoublyListNode* head = sol.treeToDoublyList(root);
    
    cout << "Doubly Linked List: ";
    printDoublyList(head);

    return 0;
}
```

In this implementation, the `treeToDoublyList` function converts a BST to a sorted doubly linked list. It initializes a dummy node to simplify the pointer adjustment and uses a helper function `inorder` to perform an in-order traversal of the BST, updating the `prev` pointer accordingly. Finally, it adjusts the pointers to form a circular doubly linked list and returns the head of the list.

### 1. Algorithms & Data Structures (C++): Creating Binary Trees

Creating binary trees in C++ involves defining a tree node structure and implementing various functions for tree operations such as insertion, deletion, searching, and traversal. Here's a basic example of how you can create a binary tree in C++:

```cpp
#include <iostream>
using namespace std;

// Define the structure of a tree node
struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;
    
    // Constructor
    TreeNode(int value) : data(value), left(nullptr), right(nullptr) {}
};

// Function to insert a new node in the binary tree
void insert(TreeNode*& root, int value) {
    if (root == nullptr) {
        root = new TreeNode(value);
    } else {
        if (value < root->data) {
            insert(root->left, value);
        } else {
            insert(root->right, value);
        }
    }
}

// Function to perform inorder traversal of the binary tree
void inorderTraversal(TreeNode* root) {
    if (root != nullptr) {
        inorderTraversal(root->left);
        cout << root->data << " ";
        inorderTraversal(root->right);
    }
}

int main() {
    TreeNode* root = nullptr;
    
    // Insert some nodes into the binary tree
    insert(root, 10);
    insert(root, 5);
    insert(root, 15);
    insert(root, 7);
    insert(root, 12);
    
    // Perform inorder traversal to display the elements of the tree
    cout << "Inorder Traversal: ";
    inorderTraversal(root);
    cout << endl;
    
    return 0;
}
```

This code creates a basic binary search tree (BST) in C++. The `TreeNode` struct represents each node in the tree, containing the data and pointers to the left and right children. The `insert` function inserts a new node into the tree while maintaining the binary search tree property. The `inorderTraversal` function performs an inorder traversal of the tree, printing out the values of the nodes in sorted order.

You can extend this code by implementing other tree operations such as deletion, searching, preorder traversal, and postorder traversal, as per your requirements. Additionally, you can enhance the code by adding error handling, balancing the tree, or implementing other types of binary trees (e.g., AVL trees, red-black trees).

### 1. Algorithms & Data Structures (C++): Building Sorted Trees

Building sorted trees, often referred to as binary search trees (BSTs), is a fundamental concept in computer science and can be implemented in C++. A binary search tree is a hierarchical data structure where each node has at most two children, referred to as the left child and the right child. In a sorted tree, the value of the left child is less than the value of its parent node, and the value of the right child is greater than or equal to the value of its parent node.

Here's a basic implementation of a sorted tree in C++:

```cpp
#include <iostream>

// Define the structure for a node in the tree
struct Node {
    int data;
    Node* left;
    Node* right;

    // Constructor
    Node(int value) : data(value), left(nullptr), right(nullptr) {}
};

// Function to insert a new node into the tree
Node* insert(Node* root, int value) {
    // If the tree is empty, create a new node and return it
    if (root == nullptr) {
        return new Node(value);
    }

    // Otherwise, recursively insert into the left or right subtree
    if (value < root->data) {
        root->left = insert(root->left, value);
    } else {
        root->right = insert(root->right, value);
    }

    return root;
}

// Function to traverse the tree in inorder (sorted) manner
void inorderTraversal(Node* root) {
    if (root != nullptr) {
        inorderTraversal(root->left);
        std::cout << root->data << " ";
        inorderTraversal(root->right);
    }
}

// Function to delete the entire tree to avoid memory leaks
void deleteTree(Node* root) {
    if (root != nullptr) {
        deleteTree(root->left);
        deleteTree(root->right);
        delete root;
    }
}

int main() {
    Node* root = nullptr;

    // Insert some values into the tree
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    insert(root, 60);
    insert(root, 80);

    // Print the tree in sorted order
    std::cout << "Inorder traversal of the tree: ";
    inorderTraversal(root);
    std::cout << std::endl;

    // Clean up memory by deleting the tree
    deleteTree(root);

    return 0;
}
```

This code defines a basic binary search tree and includes functions to insert nodes into the tree, traverse the tree in sorted order (inorder traversal), and delete the entire tree. You can test and extend this code as needed for your purposes.


### 1. Algorithms & Data Structures (C++): What is a Binary Tree?

A binary tree is a hierarchical data structure in computer science composed of nodes, where each node has at most two children, referred to as the left child and the right child. It's called a "binary" tree because each node can have at most two children.

Here are some key points about binary trees:

1. **Root**: The topmost node of the tree, from which all other nodes are descendants.

2. **Node**: Each element in a binary tree is called a node. Each node contains a piece of data and references to its left and right children, if they exist.

3. **Parent, Child, Sibling**: A node with children is called a parent node, and the nodes it points to are its children. Nodes with the same parent are called siblings.

4. **Leaf Node**: A node with no children is called a leaf node or a terminal node.

5. **Depth**: The depth of a node is the number of edges from the root to the node.

6. **Height**: The height of a tree is the maximum depth of any node in the tree.

Binary trees are commonly used for organizing and searching data efficiently. They can be used to implement various data structures such as binary search trees, binary heaps, and expression trees. They are also used in various algorithms such as tree traversals, sorting algorithms, and dynamic programming.

### 1. Algorithms & Data Structures (C++): Kth Smallest Element In Binary Search Trees

Sure, let's discuss how to find the Kth smallest element in a Binary Search Tree (BST) using C++.

First, let's briefly discuss what a BST is and how it works.

A Binary Search Tree is a binary tree where each node has at most two children, and the key (or value) of nodes in the left subtree is less than the key of the root node, and the key of nodes in the right subtree is greater than the key of the root node. This property makes it efficient to search for elements within the tree.

Now, to find the Kth smallest element in a BST, we can perform an in-order traversal of the BST, which would visit nodes in sorted order. During this traversal, we can keep track of the count of nodes visited. Once we reach the Kth node during the traversal, we return its value.

Here's a C++ implementation:

```cpp
#include <iostream>
using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    int kthSmallest(TreeNode* root, int k) {
        int count = 0;
        int result = -1;
        kthSmallestUtil(root, k, count, result);
        return result;
    }

private:
    void kthSmallestUtil(TreeNode* root, int k, int& count, int& result) {
        if (root == nullptr) return;
        
        // Traverse left subtree
        kthSmallestUtil(root->left, k, count, result);
        
        // Process current node
        count++;
        if (count == k) {
            result = root->val;
            return;
        }
        
        // Traverse right subtree
        kthSmallestUtil(root->right, k, count, result);
    }
};

// Function to create a new tree node
TreeNode* newNode(int val) {
    TreeNode* temp = new TreeNode(val);
    return temp;
}

int main() {
    // Creating a binary search tree
    TreeNode* root = newNode(5);
    root->left = newNode(3);
    root->right = newNode(7);
    root->left->left = newNode(2);
    root->left->right = newNode(4);
    root->right->left = newNode(6);
    root->right->right = newNode(8);

    Solution sol;
    int k = 3;
    cout << "Kth smallest element is: " << sol.kthSmallest(root, k) << endl;

    return 0;
}
```

In this code:

- We perform an in-order traversal of the BST.
- We maintain a count of nodes visited.
- Once the count reaches K, we store the value of that node and return it.

This code should output the Kth smallest element in the given BST. You can modify the tree structure or change the value of K to test different cases.

### 1. Algorithms & Data Structures (C++): Balanced binary tree

A balanced binary tree is a type of binary tree where the height difference between the left and right subtrees of any node is at most one. This ensures that the tree remains relatively balanced, which is crucial for maintaining efficient search, insertion, and deletion operations. One of the most common types of balanced binary trees is the AVL tree.

In C++, you can implement a balanced binary tree using the AVL tree data structure. Here's a basic implementation:

```cpp
#include <iostream>
#include <algorithm>

using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
    int height;
};

// Calculate the height of a node
int height(Node* node) {
    if (node == nullptr)
        return 0;
    return node->height;
}

// Create a new node
Node* createNode(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->left = nullptr;
    newNode->right = nullptr;
    newNode->height = 1; // New node is initially added at leaf
    return newNode;
}

// Perform a right rotation
Node* rightRotate(Node* y) {
    Node* x = y->left;
    Node* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    return x;
}

// Perform a left rotation
Node* leftRotate(Node* x) {
    Node* y = x->right;
    Node* T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    // Update heights
    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    return y;
}

// Get the balance factor of a node
int getBalance(Node* node) {
    if (node == nullptr)
        return 0;
    return height(node->left) - height(node->right);
}

// Insert a new node into the AVL tree
Node* insert(Node* node, int data) {
    // Perform standard BST insertion
    if (node == nullptr)
        return createNode(data);

    if (data < node->data)
        node->left = insert(node->left, data);
    else if (data > node->data)
        node->right = insert(node->right, data);
    else // Equal keys are not allowed in AVL
        return node;

    // Update height of this ancestor node
    node->height = 1 + max(height(node->left), height(node->right));

    // Get the balance factor to check if this node became unbalanced
    int balance = getBalance(node);

    // If node becomes unbalanced, there are four cases

    // Left Left Case
    if (balance > 1 && data < node->left->data)
        return rightRotate(node);

    // Right Right Case
    if (balance < -1 && data > node->right->data)
        return leftRotate(node);

    // Left Right Case
    if (balance > 1 && data > node->left->data) {
        node->left = leftRotate(node->left);
        return rightRotate(node);
    }

    // Right Left Case
    if (balance < -1 && data < node->right->data) {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }

    // Tree is balanced, return the unchanged node pointer
    return node;
}

// Print the inorder traversal of the tree
void inorderTraversal(Node* root) {
    if (root != nullptr) {
        inorderTraversal(root->left);
        cout << root->data << " ";
        inorderTraversal(root->right);
    }
}

int main() {
    Node* root = nullptr;

    // Insert elements into the tree
    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 30);
    root = insert(root, 40);
    root = insert(root, 50);
    root = insert(root, 25);

    cout << "Inorder traversal of the AVL tree: ";
    inorderTraversal(root);
    cout << endl;

    return 0;
}
```

This implementation includes the basic operations of an AVL tree: insertion and traversal. It ensures that the tree remains balanced after each insertion operation. You can further extend it to include deletion and other functionalities as needed.

### 1. Algorithms & Data Structures (C++): Balanced binary tree: Complexity analysis

Sure, let's dive into the complexity analysis of a balanced binary tree, also known as an AVL tree, in terms of operations such as insertion, deletion, and search.

1. **Insertion**:
   - The complexity of insertion in an AVL tree is \( O(\log n) \), where \( n \) is the number of nodes in the tree.
   - When you insert a node into the AVL tree, you may have to perform rotations to maintain the balance property of the AVL tree. Rotations have a time complexity of \( O(1) \) each, and in the worst case, you may need to perform \( O(\log n) \) rotations. However, since each rotation is \( O(1) \), the overall complexity remains \( O(\log n) \).

2. **Deletion**:
   - Similar to insertion, deletion also has a complexity of \( O(\log n) \) in AVL trees.
   - Deletion may require rotations to maintain the balance property, but again, the number of rotations needed is bounded by \( O(\log n) \).

3. **Search**:
   - Searching in a balanced binary tree also has a time complexity of \( O(\log n) \), where \( n \) is the number of nodes.
   - At each step of the search, you traverse either left or right subtree, effectively halving the number of nodes to search at each level.

4. **Space Complexity**:
   - The space complexity of an AVL tree is \( O(n) \), where \( n \) is the number of nodes in the tree.
   - This is because each node requires space to store data and pointers to its left and right children.

In summary, AVL trees provide efficient \( O(\log n) \) time complexity for insertion, deletion, and search operations, making them suitable for applications where efficient searching and balanced tree structures are required.

### 1. Algorithms & Data Structures (C++): Almost Complete Binary Tree

An almost complete binary tree is a binary tree in which all levels are completely filled except possibly for the last level, and the last level is filled from left to right. Here's a basic implementation of an almost complete binary tree in C++:

```cpp
#include <iostream>
#include <queue>
using namespace std;

// Node structure for the binary tree
struct Node {
    int data;
    Node* left;
    Node* right;
    
    Node(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Function to insert a new node in the almost complete binary tree
void insert(Node* &root, int val) {
    if (!root) {
        root = new Node(val);
        return;
    }
    
    queue<Node*> q;
    q.push(root);
    
    while (!q.empty()) {
        Node* temp = q.front();
        q.pop();
        
        if (!temp->left) {
            temp->left = new Node(val);
            return;
        } else if (!temp->right) {
            temp->right = new Node(val);
            return;
        } else {
            q.push(temp->left);
            q.push(temp->right);
        }
    }
}

// Function to perform level order traversal of the almost complete binary tree
void levelOrderTraversal(Node* root) {
    if (!root)
        return;
    
    queue<Node*> q;
    q.push(root);
    
    while (!q.empty()) {
        Node* temp = q.front();
        q.pop();
        
        cout << temp->data << " ";
        
        if (temp->left)
            q.push(temp->left);
        if (temp->right)
            q.push(temp->right);
    }
}

int main() {
    Node* root = nullptr;
    insert(root, 1);
    insert(root, 2);
    insert(root, 3);
    insert(root, 4);
    insert(root, 5);
    insert(root, 6);
    insert(root, 7);

    cout << "Level Order Traversal of the Almost Complete Binary Tree: ";
    levelOrderTraversal(root);
    cout << endl;

    return 0;
}
```

This code demonstrates how to insert nodes into an almost complete binary tree and perform a level order traversal. You can further extend or modify this code as per your requirements.

### 1. Algorithms & Data Structures (C++): Binary Tree

Sure, let's dive into the basics of implementing a binary tree in C++. A binary tree is a data structure composed of nodes, where each node has at most two children, referred to as the left child and the right child.

Here's a simple implementation of a binary tree node in C++:

```cpp
#include <iostream>

using namespace std;

// Define a Node structure for the binary tree
struct Node {
    int data;
    Node* left;
    Node* right;

    Node(int value) {
        data = value;
        left = nullptr;
        right = nullptr;
    }
};
```

Now, let's create a binary tree class and implement basic operations like insertion, traversal, and searching.

```cpp
class BinaryTree {
private:
    Node* root;

    // Helper function for inserting a node
    Node* insertHelper(Node* root, int value) {
        if (root == nullptr) {
            return new Node(value);
        }

        if (value < root->data) {
            root->left = insertHelper(root->left, value);
        } else if (value > root->data) {
            root->right = insertHelper(root->right, value);
        }

        return root;
    }

    // Helper function for inorder traversal
    void inorderHelper(Node* root) {
        if (root != nullptr) {
            inorderHelper(root->left);
            cout << root->data << " ";
            inorderHelper(root->right);
        }
    }

    // Helper function for searching a value
    bool searchHelper(Node* root, int value) {
        if (root == nullptr) {
            return false;
        }

        if (root->data == value) {
            return true;
        } else if (value < root->data) {
            return searchHelper(root->left, value);
        } else {
            return searchHelper(root->right, value);
        }
    }

public:
    BinaryTree() {
        root = nullptr;
    }

    // Insertion operation
    void insert(int value) {
        root = insertHelper(root, value);
    }

    // Inorder traversal
    void inorder() {
        inorderHelper(root);
        cout << endl;
    }

    // Search operation
    bool search(int value) {
        return searchHelper(root, value);
    }
};
```

With this implementation, you can create a binary tree object and perform operations like insertion, traversal, and searching:

```cpp
int main() {
    BinaryTree tree;

    tree.insert(50);
    tree.insert(30);
    tree.insert(70);
    tree.insert(20);
    tree.insert(40);
    tree.insert(60);
    tree.insert(80);

    cout << "Inorder traversal: ";
    tree.inorder();

    cout << "Is 40 in the tree? " << (tree.search(40) ? "Yes" : "No") << endl;
    cout << "Is 90 in the tree? " << (tree.search(90) ? "Yes" : "No") << endl;

    return 0;
}
```

This will output:

```bash
Inorder traversal: 20 30 40 50 60 70 80 
Is 40 in the tree? Yes
Is 90 in the tree? No
```

This is a basic implementation of a binary tree in C++. You can extend this implementation to include more operations or enhance its functionality as per your requirements.

### 1. Algorithms & Data Structures (C++): Binary Tree Class

Certainly! Below is a simple implementation of a binary tree class in C++. This class includes basic functionalities such as insertion, deletion, searching, and traversal (inorder, preorder, and postorder).

```cpp
#include <iostream>

using namespace std;

// Node structure
struct Node {
    int data;
    Node* left;
    Node* right;

    Node(int val) {
        data = val;
        left = nullptr;
        right = nullptr;
    }
};

// Binary Tree class
class BinaryTree {
private:
    Node* root;

    // Helper function for insertion
    Node* insertRecursive(Node* node, int key) {
        if (node == nullptr)
            return new Node(key);

        if (key < node->data)
            node->left = insertRecursive(node->left, key);
        else if (key > node->data)
            node->right = insertRecursive(node->right, key);

        return node;
    }

    // Helper function for inorder traversal
    void inorderTraversalRecursive(Node* node) {
        if (node == nullptr)
            return;

        inorderTraversalRecursive(node->left);
        cout << node->data << " ";
        inorderTraversalRecursive(node->right);
    }

    // Helper function for preorder traversal
    void preorderTraversalRecursive(Node* node) {
        if (node == nullptr)
            return;

        cout << node->data << " ";
        preorderTraversalRecursive(node->left);
        preorderTraversalRecursive(node->right);
    }

    // Helper function for postorder traversal
    void postorderTraversalRecursive(Node* node) {
        if (node == nullptr)
            return;

        postorderTraversalRecursive(node->left);
        postorderTraversalRecursive(node->right);
        cout << node->data << " ";
    }

    // Helper function for finding minimum value node
    Node* minValueNode(Node* node) {
        Node* current = node;
        while (current && current->left != nullptr)
            current = current->left;
        return current;
    }

    // Helper function for deleting a node
    Node* deleteNodeRecursive(Node* root, int key) {
        if (root == nullptr)
            return root;

        if (key < root->data)
            root->left = deleteNodeRecursive(root->left, key);
        else if (key > root->data)
            root->right = deleteNodeRecursive(root->right, key);
        else {
            if (root->left == nullptr) {
                Node* temp = root->right;
                delete root;
                return temp;
            } else if (root->right == nullptr) {
                Node* temp = root->left;
                delete root;
                return temp;
            }

            Node* temp = minValueNode(root->right);
            root->data = temp->data;
            root->right = deleteNodeRecursive(root->right, temp->data);
        }
        return root;
    }

public:
    BinaryTree() {
        root = nullptr;
    }

    // Insertion
    void insert(int key) {
        root = insertRecursive(root, key);
    }

    // Inorder traversal
    void inorderTraversal() {
        inorderTraversalRecursive(root);
        cout << endl;
    }

    // Preorder traversal
    void preorderTraversal() {
        preorderTraversalRecursive(root);
        cout << endl;
    }

    // Postorder traversal
    void postorderTraversal() {
        postorderTraversalRecursive(root);
        cout << endl;
    }

    // Deletion
    void deleteNode(int key) {
        root = deleteNodeRecursive(root, key);
    }
};

int main() {
    BinaryTree tree;
    tree.insert(50);
    tree.insert(30);
    tree.insert(20);
    tree.insert(40);
    tree.insert(70);
    tree.insert(60);
    tree.insert(80);

    cout << "Inorder traversal: ";
    tree.inorderTraversal();

    cout << "Preorder traversal: ";
    tree.preorderTraversal();

    cout << "Postorder traversal: ";
    tree.postorderTraversal();

    cout << "Deleting 20... \n";
    tree.deleteNode(20);
    cout << "Inorder traversal after deletion: ";
    tree.inorderTraversal();

    return 0;
}
```

This code provides a basic implementation of a binary tree class in C++. You can extend it by adding more functionalities like level order traversal, finding the height of the tree, etc., based on your requirements.

### 1. Algorithms & Data Structures (C++): Binary Tree Class using Queue

Sure, here's an implementation of a binary tree class in C++ using a queue for various operations like level order traversal:

```cpp
#include <iostream>
#include <queue>
using namespace std;

// Node structure for the binary tree
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Binary tree class
class BinaryTree {
private:
    TreeNode* root;

public:
    // Constructor
    BinaryTree() : root(nullptr) {}

    // Destructor to free allocated memory
    ~BinaryTree() {
        clear(root);
    }

    // Function to insert a value into the binary tree
    void insert(int val) {
        root = insertRecursive(root, val);
    }

    // Function to perform level order traversal using a queue
    void levelOrderTraversal() {
        if (root == nullptr)
            return;

        queue<TreeNode*> q;
        q.push(root);

        while (!q.empty()) {
            TreeNode* current = q.front();
            q.pop();
            cout << current->val << " ";

            if (current->left != nullptr)
                q.push(current->left);
            if (current->right != nullptr)
                q.push(current->right);
        }
    }

private:
    // Recursive function to insert a value into the binary tree
    TreeNode* insertRecursive(TreeNode* root, int val) {
        if (root == nullptr)
            return new TreeNode(val);

        if (val < root->val)
            root->left = insertRecursive(root->left, val);
        else if (val > root->val)
            root->right = insertRecursive(root->right, val);

        return root;
    }

    // Recursive function to clear the binary tree and free memory
    void clear(TreeNode* root) {
        if (root != nullptr) {
            clear(root->left);
            clear(root->right);
            delete root;
        }
    }
};

// Main function to test the binary tree implementation
int main() {
    BinaryTree tree;
    tree.insert(8);
    tree.insert(3);
    tree.insert(10);
    tree.insert(1);
    tree.insert(6);
    tree.insert(14);

    cout << "Level Order Traversal: ";
    tree.levelOrderTraversal();
    cout << endl;

    return 0;
}
```

This code defines a binary tree class with basic functionalities like insertion and level-order traversal using a queue. You can create a binary tree object, insert elements into it, and then perform level-order traversal to print the elements in the tree level by level.

### 1. Algorithms & Data Structures (C++): Binary Tree: Count Nodes

Sure, here's a simple C++ implementation to count the number of nodes in a binary tree:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

int countNodes(TreeNode* root) {
    if (root == nullptr)
        return 0;
    else
        return 1 + countNodes(root->left) + countNodes(root->right);
}

int main() {
    // Example Usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    std::cout << "Number of nodes in the binary tree: " << countNodes(root) << std::endl;

    // Don't forget to free the memory to avoid memory leaks
    delete root->left->left;
    delete root->left->right;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

This code recursively counts the nodes in the binary tree. The `countNodes` function returns 0 if the root is null (indicating an empty tree), otherwise, it returns 1 (for the current node) plus the counts of nodes in the left subtree and right subtree, recursively.

### 1. Algorithms & Data Structures (C++): Binary Tree: Diameter of Binary Tree

To find the diameter of a binary tree, you need to find the longest path between any two nodes in the tree. This path may or may not pass through the root.

Here's the C++ implementation using a recursive approach:

```cpp
#include <iostream>
#include <algorithm>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Helper function to calculate height of the tree
int height(TreeNode* root, int& diameter) {
    if (root == nullptr) return 0;
    
    // Recursively calculate height of left and right subtrees
    int left_height = height(root->left, diameter);
    int right_height = height(root->right, diameter);
    
    // Update the diameter if the current subtree's diameter is larger
    diameter = max(diameter, left_height + right_height);
    
    // Return the height of the current subtree
    return 1 + max(left_height, right_height);
}

int diameterOfBinaryTree(TreeNode* root) {
    if (root == nullptr) return 0;
    
    int diameter = 0;
    
    // Recursively calculate height and update diameter
    height(root, diameter);
    
    return diameter;
}

// Example usage
int main() {
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    
    cout << "Diameter of binary tree: " << diameterOfBinaryTree(root) << endl;
    
    // Clean up memory
    delete root->left->right;
    delete root->left->left;
    delete root->left;
    delete root->right;
    delete root;
    
    return 0;
}
```

This code computes the diameter of the binary tree by finding the height of each subtree recursively. During the height calculation, it updates the diameter if the sum of the heights of the left and right subtrees is greater than the current diameter. Finally, it returns the diameter of the binary tree.

### 1. Algorithms & Data Structures (C++): Binary Tree: Expression Tree

An expression tree is a specific type of binary tree used to represent expressions. Each node in the tree represents an operand or an operator. The leaves of the tree represent the operands, and the internal nodes represent the operators.

For example, consider the infix expression: `(3 + 4) * 5`.

This expression can be represented using an expression tree like this:

```bash
       *
     /   \
    +     5
   / \
  3   4
```

Here, the internal node `+` represents the addition operator, and the leaf nodes `3` and `4` represent the operands. The `*` operator is at the root, indicating multiplication.

To implement an expression tree in C++, you would typically define a node structure for the tree and then write functions to build and evaluate the tree.

Here's a basic example of how you might implement an expression tree in C++:

```cpp
#include <iostream>
#include <string>
#include <stack>

using namespace std;

// Node structure for the expression tree
struct TreeNode {
    string value;
    TreeNode* left;
    TreeNode* right;
    
    TreeNode(string val) : value(val), left(nullptr), right(nullptr) {}
};

// Function to check if a character is an operator
bool isOperator(char c) {
    return c == '+' || c == '-' || c == '*' || c == '/';
}

// Function to build an expression tree from a postfix expression
TreeNode* buildExpressionTree(const string& postfix) {
    stack<TreeNode*> st;

    for (char c : postfix) {
        if (isOperator(c)) {
            TreeNode* right = st.top();
            st.pop();
            TreeNode* left = st.top();
            st.pop();

            TreeNode* newNode = new TreeNode(string(1, c));
            newNode->left = left;
            newNode->right = right;

            st.push(newNode);
        } else {
            st.push(new TreeNode(string(1, c)));
        }
    }

    return st.top();
}

// Function to evaluate an expression tree
int evaluateExpressionTree(TreeNode* root) {
    if (!root) return 0;
    
    if (!root->left && !root->right) {
        return stoi(root->value);
    }

    int leftValue = evaluateExpressionTree(root->left);
    int rightValue = evaluateExpressionTree(root->right);

    if (root->value == "+")
        return leftValue + rightValue;
    else if (root->value == "-")
        return leftValue - rightValue;
    else if (root->value == "*")
        return leftValue * rightValue;
    else if (root->value == "/")
        return leftValue / rightValue;
    
    return 0;
}

int main() {
    // Example usage
    string postfix = "34+5*";
    TreeNode* root = buildExpressionTree(postfix);
    
    cout << "Postfix expression: " << postfix << endl;
    cout << "Result: " << evaluateExpressionTree(root) << endl;

    return 0;
}
```

This code builds an expression tree from a postfix expression and then evaluates it. You can modify it to handle other types of expressions or to support more operators and operands.

### 1. Algorithms & Data Structures (C++): Binary Tree: Extracting the Leaves from a Tree

To extract the leaves from a binary tree in C++, you can traverse the tree recursively and remove the leaf nodes while maintaining the tree structure. Here's a sample implementation:

```cpp
#include <iostream>

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void extractLeaves(TreeNode* root, TreeNode*& leaves) {
    if (!root) return;

    if (!root->left && !root->right) { // If it's a leaf node
        if (!leaves) {
            leaves = root;
        } else {
            TreeNode* temp = leaves;
            while (temp->right) {
                temp = temp->right;
            }
            temp->right = root;
        }
        return;
    }

    if (root->left) {
        extractLeaves(root->left, leaves);
        if (!root->left->left && !root->left->right) {
            delete root->left;
            root->left = nullptr;
        }
    }

    if (root->right) {
        extractLeaves(root->right, leaves);
        if (!root->right->left && !root->right->right) {
            delete root->right;
            root->right = nullptr;
        }
    }
}

void printLeaves(TreeNode* leaves) {
    while (leaves) {
        std::cout << leaves->val << " ";
        leaves = leaves->right;
    }
    std::cout << std::endl;
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(7);

    TreeNode* leaves = nullptr;
    extractLeaves(root, leaves);

    std::cout << "Extracted leaves: ";
    printLeaves(leaves);

    return 0;
}
```

In this code:

- `extractLeaves` function recursively traverses the tree and extracts the leaf nodes while updating the `leaves` pointer.
- `printLeaves` function is provided to print the extracted leaves.
- The `main` function is an example of how you can use these functions to extract and print the leaves of a binary tree.

### 1. Algorithms & Data Structures (C++): Binary Tree: Find Node

To find a node in a binary tree using C++, you can implement a recursive algorithm that traverses the tree until the desired node is found. Here's a basic implementation:

```cpp
#include <iostream>

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

TreeNode* findNode(TreeNode* root, int target) {
    if (root == nullptr || root->val == target) {
        return root;
    }
    
    // Check left subtree
    TreeNode* leftResult = findNode(root->left, target);
    if (leftResult != nullptr) {
        return leftResult;
    }
    
    // Check right subtree
    TreeNode* rightResult = findNode(root->right, target);
    if (rightResult != nullptr) {
        return rightResult;
    }
    
    // If not found in either subtree, return nullptr
    return nullptr;
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(7);

    int target = 5;
    TreeNode* result = findNode(root, target);
    
    if (result) {
        std::cout << "Node found with value: " << result->val << std::endl;
    } else {
        std::cout << "Node not found." << std::endl;
    }

    // Clean up memory
    // Implementation of deletion not provided in this example for simplicity
    return 0;
}
```

In this implementation, the `findNode` function takes the root of the binary tree and the target value to search for. It recursively traverses the tree, checking each node's value against the target value. If the target value is found at a node, the function returns that node; otherwise, it continues searching recursively in the left and right subtrees. If the target value is not found in the entire tree, the function returns `nullptr`.

### 1. Algorithms & Data Structures (C++): Binary Tree: Height of Tree

To find the height of a binary tree in C++, you can use a recursive approach. Here's a basic implementation:

```cpp
#include <iostream>
#include <algorithm> // for max function

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

int height(TreeNode* root) {
    // Base case: if the node is null, return 0
    if (root == nullptr)
        return 0;
    else {
        // Recursively find the height of the left and right subtrees
        int leftHeight = height(root->left);
        int rightHeight = height(root->right);

        // Return the height of the subtree rooted at this node
        return 1 + std::max(leftHeight, rightHeight);
    }
}

int main() {
    // Example binary tree:
    //      1
    //     / \
    //    2   3
    //   / \
    //  4   5
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    std::cout << "Height of the binary tree is: " << height(root) << std::endl;

    // Clean up memory
    delete root->left->right;
    delete root->left->left;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

In this code:

- The `TreeNode` structure represents a node in the binary tree, containing an integer value and pointers to its left and right children.
- The `height` function calculates the height of the binary tree recursively. If the root is `nullptr`, it returns 0. Otherwise, it recursively calculates the heights of the left and right subtrees and returns the maximum height plus 1.
- In the `main` function, an example binary tree is created, and its height is printed. Finally, memory allocated for the nodes is freed to avoid memory leaks.

### 1. Algorithms & Data Structures (C++): Binary Tree: Print Tree Recursive

Printing a binary tree recursively in C++ involves traversing the tree in some order (pre-order, in-order, or post-order) and printing the values of nodes as you visit them. Here's a simple implementation for printing a binary tree in in-order traversal recursively:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void printInOrder(TreeNode* root) {
    if (root == nullptr) return;

    // Traverse left subtree
    printInOrder(root->left);

    // Print the value of current node
    std::cout << root->val << " ";

    // Traverse right subtree
    printInOrder(root->right);
}

// Function to create a new node
TreeNode* createNode(int val) {
    return new TreeNode(val);
}

int main() {
    // Create a sample binary tree
    TreeNode* root = createNode(1);
    root->left = createNode(2);
    root->right = createNode(3);
    root->left->left = createNode(4);
    root->left->right = createNode(5);

    std::cout << "In-order traversal of binary tree: ";
    printInOrder(root);

    return 0;
}
```

This code defines a binary tree node structure `TreeNode` with an integer value, and left and right pointers. The `printInOrder` function recursively traverses the binary tree in in-order fashion (left subtree, root, right subtree), printing the value of each node. Finally, in the `main` function, a sample binary tree is created and its in-order traversal is printed.

You can modify this code to print the tree in pre-order or post-order traversal by changing the order in which the `printInOrder` function visits the nodes.

### 1. Algorithms & Data Structures (C++): Binary Tree: Remove Half Nodes

Removing half nodes from a binary tree involves deleting nodes that have only one child, thus maintaining the binary tree structure. Here's how you can implement this in C++:

```cpp
#include <iostream>
using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

// Function to remove half nodes from a binary tree
TreeNode* removeHalfNodes(TreeNode* root) {
    if (root == nullptr) return nullptr;
    
    root->left = removeHalfNodes(root->left);
    root->right = removeHalfNodes(root->right);
    
    if (root->left == nullptr && root->right != nullptr) {
        TreeNode* temp = root->right;
        delete root;
        return temp;
    }
    
    if (root->left != nullptr && root->right == nullptr) {
        TreeNode* temp = root->left;
        delete root;
        return temp;
    }
    
    return root;
}

// Function to print the binary tree (inorder traversal)
void printInorder(TreeNode* root) {
    if (root == nullptr) return;
    printInorder(root->left);
    cout << root->val << " ";
    printInorder(root->right);
}

// Utility function to create a new tree node
TreeNode* newNode(int data) {
    TreeNode* node = new TreeNode(data);
    return node;
}

int main() {
    TreeNode* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);

    cout << "Original tree (inorder): ";
    printInorder(root);
    cout << endl;

    root = removeHalfNodes(root);

    cout << "Tree after removing half nodes (inorder): ";
    printInorder(root);
    cout << endl;

    return 0;
}
```

This code defines a binary tree structure with nodes having an integer value. The `removeHalfNodes` function traverses the tree recursively and removes half nodes, i.e., nodes with only one child. Finally, it returns the modified root of the tree. The `printInorder` function performs an inorder traversal of the tree to print its elements. In the `main` function, we create a sample binary tree, remove half nodes, and print the modified tree.

### 1. Algorithms & Data Structures (C++): Binary Tree: Root to Node Path

Sure, I can guide you through implementing a function in C++ that finds the path from the root of a binary tree to a specific node. We'll implement a recursive approach for this task.

First, let's define the structure for a binary tree node:

```cpp
#include <iostream>
#include <vector>

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};
```

Now, let's write the function to find the path from the root to a given node:

```cpp
bool findPath(TreeNode* root, int target, std::vector<int>& path) {
    // Base case: if root is null, return false
    if (root == nullptr)
        return false;

    // Add current node's value to the path
    path.push_back(root->val);

    // If the current node is the target node, return true
    if (root->val == target)
        return true;

    // Recur for left and right subtrees
    if ((root->left && findPath(root->left, target, path)) || (root->right && findPath(root->right, target, path)))
        return true;

    // If target is not present in either left or right subtree of this node, remove it from path
    path.pop_back();
    return false;
}

std::vector<int> findPath(TreeNode* root, int target) {
    std::vector<int> path;
    findPath(root, target, path);
    return path;
}
```

This function takes the root of the binary tree and the value of the target node as input and returns a vector containing the path from the root to the target node.

Here's how you can use this function:

```cpp
int main() {
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(7);

    int target = 5;
    std::vector<int> path = findPath(root, target);

    if (!path.empty()) {
        std::cout << "Path from root to " << target << ": ";
        for (int val : path)
            std::cout << val << " ";
        std::cout << std::endl;
    } else {
        std::cout << "Target node not found!" << std::endl;
    }

    return 0;
}
```

This will output:

```bash
Path from root to 5: 1 2 5 
```

Feel free to modify the tree structure and the target node to test different scenarios.

### 1. Algorithms & Data Structures (C++): Binary Tree: Sum of Nodes

To calculate the sum of all nodes in a binary tree using C++, you can perform a simple recursive traversal of the tree. Here's a basic implementation:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to calculate the sum of all nodes in a binary tree
int sumOfNodes(TreeNode* root) {
    if (root == nullptr) // Base case: if the node is null, return 0
        return 0;
    return root->val + sumOfNodes(root->left) + sumOfNodes(root->right);
}

int main() {
    // Example usage:
    // Constructing a binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(7);

    // Calculate the sum of nodes
    int sum = sumOfNodes(root);
    std::cout << "Sum of all nodes in the binary tree: " << sum << std::endl;

    // Freeing memory (optional)
    // This step is important to avoid memory leaks
    delete root->left->left;
    delete root->left->right;
    delete root->right->left;
    delete root->right->right;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

In this code:

- We define a `TreeNode` struct to represent each node in the binary tree.
- The `sumOfNodes` function takes a pointer to the root of the binary tree and recursively calculates the sum of all nodes in the tree.
- In the `main` function, we construct a sample binary tree and calculate the sum of its nodes.
- Finally, we free the dynamically allocated memory to prevent memory leaks.

This implementation assumes that the binary tree nodes are allocated dynamically and that you're responsible for freeing the memory after use.

### 1. Algorithms & Data Structures (C++): Binary Tree: Take Input Level Wise

To take input level-wise for a binary tree in C++, you can follow a breadth-first traversal approach using a queue. Here's a basic implementation:

```cpp
#include <iostream>
#include <queue>
using namespace std;

// Define the structure of a binary tree node
struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;

    TreeNode(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Function to take input level-wise for a binary tree
TreeNode* takeInputLevelWise() {
    cout << "Enter the root value: ";
    int rootData;
    cin >> rootData;

    // Create the root node
    TreeNode* root = new TreeNode(rootData);

    // Create a queue to perform breadth-first traversal
    queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        // Get the front node from the queue
        TreeNode* currNode = q.front();
        q.pop();

        // Prompt for left child
        int leftChildData;
        cout << "Enter left child of " << currNode->data << " (or -1 if none): ";
        cin >> leftChildData;
        if (leftChildData != -1) {
            // Create left child node and link it
            currNode->left = new TreeNode(leftChildData);
            // Push it into the queue
            q.push(currNode->left);
        }

        // Prompt for right child
        int rightChildData;
        cout << "Enter right child of " << currNode->data << " (or -1 if none): ";
        cin >> rightChildData;
        if (rightChildData != -1) {
            // Create right child node and link it
            currNode->right = new TreeNode(rightChildData);
            // Push it into the queue
            q.push(currNode->right);
        }
    }

    return root;
}

// Function to print the binary tree (in-order traversal)
void printInOrder(TreeNode* root) {
    if (root == nullptr) return;

    printInOrder(root->left);
    cout << root->data << " ";
    printInOrder(root->right);
}

int main() {
    TreeNode* root = takeInputLevelWise();
    cout << "Binary Tree (In-order traversal): ";
    printInOrder(root);
    cout << endl;

    return 0;
}
```

This code will prompt the user to enter the root node first, then iteratively ask for left and right children for each node level by level until all levels of the binary tree are filled. Finally, it prints the binary tree using in-order traversal.

### 1. Algorithms & Data Structures (C++): Binary Tree: Take Input Recursive

Certainly! Taking input for a binary tree recursively typically involves traversing the tree in a certain order (usually pre-order, in-order, or post-order) and asking for user input at each node. Here's a sample C++ code to take input for a binary tree recursively:

```cpp
#include <iostream>

struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;

    TreeNode(int value) : data(value), left(nullptr), right(nullptr) {}
};

// Function to take input for a binary tree recursively
TreeNode* takeInput() {
    int data;
    std::cout << "Enter node value (or -1 for null): ";
    std::cin >> data;

    if (data == -1) {
        return nullptr; // Null node
    }

    TreeNode* root = new TreeNode(data);

    std::cout << "Enter left child of " << data << ":\n";
    root->left = takeInput(); // Recursive call for left subtree

    std::cout << "Enter right child of " << data << ":\n";
    root->right = takeInput(); // Recursive call for right subtree

    return root;
}

// Function to traverse and print binary tree (in-order)
void inorderTraversal(TreeNode* root) {
    if (root == nullptr) {
        return;
    }
    inorderTraversal(root->left);
    std::cout << root->data << " ";
    inorderTraversal(root->right);
}

int main() {
    TreeNode* root = takeInput();
    
    std::cout << "In-order traversal of the binary tree: ";
    inorderTraversal(root);
    std::cout << std::endl;

    // Free allocated memory
    // (not shown in this simplified example)
    
    return 0;
}
```

In this code:

- The `TreeNode` struct represents each node of the binary tree.
- The `takeInput()` function asks the user for input at each node, recursively creating the binary tree.
- The user is prompted to enter the value of each node, with -1 indicating a null node.
- The `inorderTraversal()` function is used to traverse and print the binary tree in in-order traversal.

You can modify this code to use pre-order or post-order traversal or include additional functionality as needed.

### 1. Algorithms & Data Structures (C++): Binary Tree: Target Path Sum

To find if there exists a path in a binary tree from the root to any leaf node whose sum equals a given target, you can use depth-first search (DFS). Here's how you can implement it in C++:

```cpp
#include <iostream>

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

bool hasPathSum(TreeNode* root, int targetSum) {
    if (root == nullptr) return false;
    // Check if the current node is a leaf node
    if (root->left == nullptr && root->right == nullptr) {
        return targetSum == root->val;
    }
    // Recursively check the left and right subtrees
    return hasPathSum(root->left, targetSum - root->val) || hasPathSum(root->right, targetSum - root->val);
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(5);
    root->left = new TreeNode(4);
    root->right = new TreeNode(8);
    root->left->left = new TreeNode(11);
    root->left->left->left = new TreeNode(7);
    root->left->left->right = new TreeNode(2);
    root->right->left = new TreeNode(13);
    root->right->right = new TreeNode(4);
    root->right->right->right = new TreeNode(1);

    int targetSum = 22;
    if (hasPathSum(root, targetSum)) {
        std::cout << "Path with sum " << targetSum << " exists." << std::endl;
    } else {
        std::cout << "No path with sum " << targetSum << " exists." << std::endl;
    }

    // Clean up
    delete root->right->right->right;
    delete root->right->right;
    delete root->right->left;
    delete root->right;
    delete root->left->left->right;
    delete root->left->left->left;
    delete root->left->left;
    delete root->left;
    delete root;

    return 0;
}
```

This code defines a `TreeNode` struct to represent the nodes in the binary tree. The `hasPathSum` function checks if there exists a path from the root to any leaf node such that the sum of values along the path equals the given target sum. If such a path exists, it returns `true`, otherwise `false`. Finally, in the `main` function, an example tree is constructed and checked for a target sum of 22.

### 1. Algorithms & Data Structures (C++): Binary Tree: Tree Diameter

To find the diameter of a binary tree, you need to find the longest path between any two nodes in the tree. The path doesn't necessarily have to pass through the root. The diameter of a binary tree is the maximum of the following three quantities:

1. Diameter of the left subtree.
2. Diameter of the right subtree.
3. Longest path between a node in the left subtree and a node in the right subtree, which can be calculated as the height of the left subtree plus the height of the right subtree plus 1 (to include the root node).

Here's a C++ implementation of finding the diameter of a binary tree:

```cpp
#include <iostream>
#include <algorithm>

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

int height(TreeNode* root) {
    if (root == nullptr)
        return 0;
    return 1 + std::max(height(root->left), height(root->right));
}

int diameter(TreeNode* root) {
    if (root == nullptr)
        return 0;

    int leftDiameter = diameter(root->left);
    int rightDiameter = diameter(root->right);

    int leftHeight = height(root->left);
    int rightHeight = height(root->right);

    return std::max({leftDiameter, rightDiameter, leftHeight + rightHeight + 1});
}

int main() {
    // Create a sample binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->right = new TreeNode(6);
    root->left->right->left = new TreeNode(7);
    root->left->right->right = new TreeNode(8);

    std::cout << "Diameter of the binary tree is: " << diameter(root) << std::endl;

    // Clean up memory
    delete root->left->right->left;
    delete root->left->right->right;
    delete root->left->right;
    delete root->left->left;
    delete root->right->right;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

This program calculates the diameter of a binary tree using a recursive approach. The `diameter` function recursively computes the diameter of each subtree and the height of each subtree, and then compares the diameters to find the maximum. The `height` function calculates the height of the subtree rooted at the given node.

### 1. Algorithms & Data Structures (C++): Binary Tree: Understanding different terminologies

Sure, let's delve into the key terminologies related to binary trees in the context of algorithms and data structures:

1. **Binary Tree**: A binary tree is a hierarchical data structure composed of nodes, where each node has at most two children, referred to as the left child and the right child.

2. **Node**: A fundamental building block of a binary tree. Each node contains some data and references to its left and right children (or null if they don't exist).

3. **Root**: The topmost node in a binary tree. It is the starting point for traversing the tree.

4. **Parent Node**: A node that has one or more child nodes.

5. **Child Node**: A node connected to another node in a tree via an edge from its parent.

6. **Leaf Node**: A node with no children, i.e., a node at the bottom of the tree.

7. **Internal Node**: A node with at least one child, i.e., a non-leaf node.

8. **Depth of a Node**: The depth of a node is the number of edges from the root node to that node. The depth of the root node is 0.

9. **Height of a Node**: The height of a node is the number of edges on the longest path from that node to a leaf node. The height of a leaf node is 0.

10. **Height of a Tree**: The height of a tree is the height of its root node. It represents the length of the longest path from the root node to a leaf node in the tree.

11. **Balanced Tree**: A binary tree is balanced if the height of the left and right subtrees of any node differ by at most one.

12. **Complete Binary Tree**: A binary tree in which every level, except possibly the last, is completely filled, and all nodes are as far left as possible.

13. **Full Binary Tree**: A binary tree in which every node other than the leaves has two children.

14. **Perfect Binary Tree**: A binary tree that is both full and complete. All leaf nodes are at the same level.

15. **Traversal**: The process of visiting and processing each node in a tree. Common tree traversal algorithms include in-order, pre-order, and post-order traversals.

16. **In-order Traversal**: Traverses the binary tree in the order: left child, parent, right child.

17. **Pre-order Traversal**: Traverses the binary tree in the order: parent, left child, right child.

18. **Post-order Traversal**: Traverses the binary tree in the order: left child, right child, parent.

These terminologies are essential for understanding, implementing, and analyzing algorithms and operations on binary trees.

### 1. Algorithms & Data Structures (C++): Binary Trees

Binary trees are fundamental data structures in computer science and are widely used in various algorithms and applications. They consist of nodes, where each node has at most two children, referred to as the left child and the right child. Here's a brief overview of binary trees in C++:

#### Node Structure

First, we define a structure for the tree node:

```cpp
struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int val) : data(val), left(nullptr), right(nullptr) {}
};
```

#### Insertion

To insert a new node into a binary tree:

```cpp
void insert(TreeNode*& root, int val) {
    if (root == nullptr) {
        root = new TreeNode(val);
        return;
    }
    if (val < root->data) {
        insert(root->left, val);
    } else {
        insert(root->right, val);
    }
}
```

#### Traversal

There are mainly three types of traversals in binary trees: inorder, preorder, and postorder. Here are the implementations:

```cpp
void inorder(TreeNode* root) {
    if (root == nullptr) return;
    inorder(root->left);
    cout << root->data << " ";
    inorder(root->right);
}

void preorder(TreeNode* root) {
    if (root == nullptr) return;
    cout << root->data << " ";
    preorder(root->left);
    preorder(root->right);
}

void postorder(TreeNode* root) {
    if (root == nullptr) return;
    postorder(root->left);
    postorder(root->right);
    cout << root->data << " ";
}
```

#### Search

Searching for a value in a binary tree:

```cpp
bool search(TreeNode* root, int val) {
    if (root == nullptr) return false;
    if (root->data == val) return true;
    if (val < root->data) return search(root->left, val);
    else return search(root->right, val);
}
```

#### Deletion

Deleting a node from the binary tree:

```cpp
TreeNode* minValueNode(TreeNode* node) {
    TreeNode* current = node;
    while (current && current->left != nullptr)
        current = current->left;
    return current;
}

TreeNode* deleteNode(TreeNode* root, int key) {
    if (root == nullptr) return root;
    if (key < root->data)
        root->left = deleteNode(root->left, key);
    else if (key > root->data)
        root->right = deleteNode(root->right, key);
    else {
        if (root->left == nullptr) {
            TreeNode* temp = root->right;
            delete root;
            return temp;
        } else if (root->right == nullptr) {
            TreeNode* temp = root->left;
            delete root;
            return temp;
        }
        TreeNode* temp = minValueNode(root->right);
        root->data = temp->data;
        root->right = deleteNode(root->right, temp->data);
    }
    return root;
}
```

#### Height

Calculating the height of a binary tree:

```cpp
int height(TreeNode* root) {
    if (root == nullptr) return -1;
    return max(height(root->left), height(root->right)) + 1;
}
```

These are basic operations on binary trees in C++. There are more advanced topics like balancing trees, threaded binary trees, AVL trees, Red-Black trees, etc., which provide improved performance for specific scenarios.

### 1. Algorithms & Data Structures (C++): Binary Trees: Binary Tree Representation

In C++, you can represent a binary tree using a struct to define the structure of a tree node, and then you can build the tree using these nodes. Here's a basic implementation of a binary tree:

```cpp
#include <iostream>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to create a new node.
TreeNode* newNode(int val) {
    TreeNode* node = new TreeNode(val);
    return node;
}

int main() {
    // Creating the tree
    TreeNode* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);

    // Traversing the tree (preorder traversal)
    cout << "Preorder traversal of the binary tree: ";
    preorder(root);
    cout << endl;

    return 0;
}
```

This code defines a basic binary tree structure using a `struct TreeNode`. Each node has an integer value and pointers to its left and right children. The `newNode` function is used to create a new node with a given value.

In the `main` function, a binary tree is created with seven nodes, and then a preorder traversal of the tree is performed. You'll need to implement the `preorder` function separately to traverse the tree in preorder.

### 1. Algorithms & Data Structures (C++): Binary Trees: Complete vs Full vs Perfect Binary Tree

Sure, let's break down the differences between complete, full, and perfect binary trees:

1. **Complete Binary Tree**:
   - In a complete binary tree, all levels except possibly the last are fully filled, and the last level is filled from left to right.
   - This means that every level, except possibly the last, is completely filled with nodes. And if the last level is not filled completely, the nodes are filled from left to right.
   - Complete binary trees are commonly used in heap data structures.

2. **Full Binary Tree**:
   - In a full binary tree, every node other than the leaves has two children.
   - This means that every node in the tree has either 0 or 2 children; there are no nodes with only one child.
   - Full binary trees are less common in practice compared to complete or perfect binary trees, but they are useful in some specific scenarios.

3. **Perfect Binary Tree**:
   - In a perfect binary tree, all interior nodes have two children, and all leaves have the same depth or same level.
   - This means that the tree is completely filled, and all levels are filled except for possibly the last level, which is filled from left to right.
   - Perfect binary trees are less common in practice due to their strict requirements, but they have some interesting properties. For example, the number of nodes at each level doubles as you progress down the tree.

In summary, complete binary trees are focused on filling levels from left to right, full binary trees ensure every node (except leaves) has two children, and perfect binary trees combine both properties with every level being completely filled. Each type of binary tree has its own set of properties and use cases depending on the requirements of the application.

### 1. Algorithms & Data Structures (C++): Binary Trees: Creating Binary Trees in the Heap Memory

Creating binary trees in heap memory in C++ involves dynamically allocating memory for each node and properly managing the pointers to build the tree structure. Here's a basic example of how you can create a binary tree in heap memory:

```cpp
#include <iostream>

// Define a structure for the tree node
struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;

    TreeNode(int value) : data(value), left(nullptr), right(nullptr) {}
};

// Function to insert a new node into the binary tree
void insert(TreeNode*& root, int value) {
    if (root == nullptr) {
        root = new TreeNode(value);
    } else {
        if (value < root->data) {
            insert(root->left, value);
        } else {
            insert(root->right, value);
        }
    }
}

// Function to print the binary tree using inorder traversal
void inorderTraversal(TreeNode* root) {
    if (root != nullptr) {
        inorderTraversal(root->left);
        std::cout << root->data << " ";
        inorderTraversal(root->right);
    }
}

int main() {
    TreeNode* root = nullptr;

    // Insert elements into the binary tree
    insert(root, 10);
    insert(root, 5);
    insert(root, 15);
    insert(root, 3);
    insert(root, 7);
    insert(root, 12);
    insert(root, 18);

    // Print the binary tree using inorder traversal
    std::cout << "Inorder Traversal: ";
    inorderTraversal(root);
    std::cout << std::endl;

    // Deallocate memory (optional)
    // You may want to deallocate memory if the tree is no longer needed
    // However, this may not be necessary in all cases, as the memory will be released when the program terminates
    // Implementing a proper destructor in the TreeNode structure is also a good practice

    return 0;
}
```

In this example:

- We define a `TreeNode` structure to represent each node in the binary tree. It contains an integer `data` field and pointers to the left and right child nodes.
- The `insert` function inserts a new node into the binary tree based on the value of the node.
- The `inorderTraversal` function performs an inorder traversal of the binary tree and prints the nodes.
- In the `main` function, we create an empty binary tree represented by a `root` pointer, and then we insert some elements into it.
- Finally, we print the binary tree using inorder traversal.

Remember that when using dynamically allocated memory, it's important to deallocate it properly to avoid memory leaks. In this example, memory deallocation is not explicitly shown, but you would typically implement a function to traverse the tree and delete each node when it's no longer needed. Alternatively, you can rely on the program's termination to release the memory, but this might not be suitable for long-running programs.

### 1. Algorithms & Data Structures (C++): Binary Trees: Depth of a node, Height of Node and Height of a Tree

Certainly! Let's dive into implementing these functionalities for binary trees in C++.

First, let's define a simple structure for a binary tree node:

```cpp
struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int val) : data(val), left(nullptr), right(nullptr) {}
};
```

Now, let's implement functions to find the depth of a node, the height of a node, and the height of the tree:

```cpp
#include <iostream>
#include <algorithm> // for max function

using namespace std;

// Function to find the depth of a node in a binary tree
int findDepth(TreeNode* root, TreeNode* node, int depth) {
    if (root == nullptr) return -1; // Base case
    if (root == node) return depth; // If the current node is the target node
    
    // Search in left and right subtrees
    int leftDepth = findDepth(root->left, node, depth + 1);
    int rightDepth = findDepth(root->right, node, depth + 1);
    
    // If node not found in left or right subtree
    if (leftDepth == -1 && rightDepth == -1)
        return -1;
    // If node found in left subtree
    else if (leftDepth != -1)
        return leftDepth;
    // If node found in right subtree
    else
        return rightDepth;
}

// Function to find the height of a node in a binary tree
int findHeight(TreeNode* node) {
    if (node == nullptr) return -1; // Base case
    return 1 + max(findHeight(node->left), findHeight(node->right));
}

// Function to find the height of a binary tree
int findTreeHeight(TreeNode* root) {
    if (root == nullptr) return -1; // Base case
    return 1 + max(findTreeHeight(root->left), findTreeHeight(root->right));
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

    // Finding depth of node 5
    TreeNode* node = root->left->right;
    cout << "Depth of node " << node->data << ": " << findDepth(root, node, 0) << endl;

    // Finding height of node 3
    node = root->right;
    cout << "Height of node " << node->data << ": " << findHeight(node) << endl;

    // Finding height of the tree
    cout << "Height of the tree: " << findTreeHeight(root) << endl;

    return 0;
}
```

This code demonstrates how to find the depth of a specific node, the height of a specific node, and the overall height of the binary tree. You can modify the tree structure and test with different inputs as needed.

### 1. Algorithms & Data Structures (C++): Binary Trees: Finding Number of Nodes in a Binary Tree

Certainly! Calculating the number of nodes in a binary tree can be done using various techniques, but one of the simplest methods is to traverse the entire tree and count the nodes. Here's a C++ implementation for that:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to count the number of nodes in a binary tree
int countNodes(TreeNode* root) {
    if (root == nullptr)
        return 0;
    return 1 + countNodes(root->left) + countNodes(root->right);
}

// Utility function to create a new binary tree node
TreeNode* newNode(int data) {
    TreeNode* node = new TreeNode(data);
    return node;
}

int main() {
    // Creating a sample binary tree
    TreeNode* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    
    // Counting the number of nodes
    int nodeCount = countNodes(root);
    
    std::cout << "Number of nodes in the binary tree: " << nodeCount << std::endl;
    
    return 0;
}
```

This code defines a binary tree node structure `TreeNode`, along with a function `countNodes` that recursively counts the nodes in the tree. The `main` function demonstrates how to use this function by creating a sample binary tree and then counting its nodes.

### 1. Algorithms & Data Structures (C++): Binary Trees: Finding the Height of a Binary Tree

To find the height of a binary tree, you can use a recursive approach where you traverse down the tree and calculate the height of the left and right subtrees. Here's a simple C++ implementation:

```cpp
#include <iostream>
#include <algorithm> // for std::max

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

int getHeight(TreeNode* root) {
    // Base case: if the root is null, height is 0
    if (root == nullptr)
        return 0;

    // Recursively calculate the height of the left and right subtrees
    int leftHeight = getHeight(root->left);
    int rightHeight = getHeight(root->right);

    // Return the maximum height of left and right subtrees plus 1 for the current node
    return 1 + std::max(leftHeight, rightHeight);
}

int main() {
    // Example usage:
    // Constructing a simple binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    std::cout << "Height of the binary tree is: " << getHeight(root) << std::endl;

    // Don't forget to free the allocated memory to prevent memory leaks
    delete root->left->right;
    delete root->left->left;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

This code defines a `TreeNode` struct representing a node in the binary tree and a `getHeight` function to calculate the height of the binary tree. The `getHeight` function recursively calculates the height of the left and right subtrees, and returns the maximum height of the subtrees plus one for the current node.

In the `main` function, an example binary tree is constructed, and its height is calculated and printed. Finally, memory allocated for the nodes is deallocated to prevent memory leaks.

### 1. Algorithms & Data Structures (C++): Binary Trees: Finding the Number of Internal Nodes in a Binary Tree

To find the number of internal nodes in a binary tree using C++, you can implement a simple recursive function that traverses the tree and counts the internal nodes. Here's a basic implementation:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to count internal nodes in a binary tree
int countInternalNodes(TreeNode* root) {
    if (root == nullptr) // Base case: if tree is empty or node is leaf
        return 0;
    if (root->left == nullptr && root->right == nullptr) // Base case: if node is leaf
        return 0;
    // Recursively count internal nodes in the left and right subtrees
    return 1 + countInternalNodes(root->left) + countInternalNodes(root->right);
}

int main() {
    // Example usage:
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(7);

    std::cout << "Number of internal nodes: " << countInternalNodes(root) << std::endl;

    // Clean up memory (optional)
    delete root->left->left;
    delete root->left->right;
    delete root->right->left;
    delete root->right->right;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

In this implementation, `countInternalNodes` recursively counts internal nodes. It returns 0 if the current node is null or if it is a leaf node. Otherwise, it recursively counts internal nodes in the left and right subtrees and adds 1 for the current node.

### 1. Algorithms & Data Structures (C++): Binary Trees: Finding the Number of Leaf Nodes in a Binary Tree

To find the number of leaf nodes in a binary tree, you typically traverse the tree recursively and count the nodes that have no children. Here's a C++ implementation for finding the number of leaf nodes in a binary tree:

```cpp
#include <iostream>

// Definition of a binary tree node
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to count the number of leaf nodes in a binary tree
int countLeafNodes(TreeNode* root) {
    if (root == nullptr) // Base case: empty tree
        return 0;
    else if (root->left == nullptr && root->right == nullptr) // Leaf node
        return 1;
    else // Recursively count leaf nodes in the left and right subtrees
        return countLeafNodes(root->left) + countLeafNodes(root->right);
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(7);

    std::cout << "Number of leaf nodes: " << countLeafNodes(root) << std::endl;

    // Free allocated memory
    // This part is important to prevent memory leaks
    delete root->left->left;
    delete root->left->right;
    delete root->right->left;
    delete root->right->right;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

This code defines a `TreeNode` structure representing a node in the binary tree and a `countLeafNodes` function to recursively count the leaf nodes. In the `main` function, an example binary tree is created, and the number of leaf nodes is printed. Finally, memory allocated for the tree nodes is freed to prevent memory leaks.

### 1. Algorithms & Data Structures (C++): Binary Trees: Relationship between Number of Leaf Nodes and Number of Internal Nodes

In a binary tree, the number of leaf nodes and internal nodes are related in a specific way.

Let's denote:

- \( n \) as the total number of nodes in the binary tree.
- \( l \) as the number of leaf nodes.
- \( i \) as the number of internal nodes.

For a binary tree:

1. Each internal node has exactly two children or no children.
2. Each leaf node has no children.

Based on these properties, we can establish a relationship between the number of leaf nodes (\( l \)) and the number of internal nodes (\( i \)).

Since each internal node has exactly two children, the total number of edges in the tree is \( n-1 \) (every node except the root has one incoming edge). Each internal node contributes two edges (one outgoing and one incoming), so the number of edges contributed by internal nodes is \( 2i \).

Since each leaf node has no children, it contributes one edge (the incoming edge), so the number of edges contributed by leaf nodes is \( l \).

Therefore, we have the equation:

\[ n - 1 = 2i + l \]

Or, rearranging the terms:

\[ l = n - 2i - 1 \]

This equation provides the relationship between the number of leaf nodes, the number of internal nodes, and the total number of nodes in a binary tree.

### 1. Algorithms & Data Structures (C++): Binary Trees: Time & Space Complexity : Constructing Binary Tree From Inorder & Preorder Trave

Constructing a binary tree from its inorder and preorder traversals is a common problem in computer science and requires a solid understanding of binary trees and tree traversal techniques. Let's discuss the approach to solving this problem and analyze its time and space complexity.

#### Approach

1. **Understanding Traversals**:
   - Inorder Traversal: Left, Root, Right
   - Preorder Traversal: Root, Left, Right

2. **Algorithm**:
   - The first element of the preorder traversal array is the root of the tree.
   - Find the root's position in the inorder traversal. All elements to the left of this position are in the left subtree, and all elements to the right are in the right subtree.
   - Recursively construct the left and right subtrees.

#### C++ Code

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

class Solution {
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        unordered_map<int, int> index_map;
        for (int i = 0; i < inorder.size(); ++i) {
            index_map[inorder[i]] = i;
        }
        return build(preorder, 0, preorder.size() - 1, inorder, 0, inorder.size() - 1, index_map);
    }

    TreeNode* build(vector<int>& preorder, int pre_start, int pre_end,
                    vector<int>& inorder, int in_start, int in_end,
                    unordered_map<int, int>& index_map) {
        if (pre_start > pre_end || in_start > in_end) return nullptr;

        int root_val = preorder[pre_start];
        TreeNode* root = new TreeNode(root_val);

        int root_index = index_map[root_val];
        int left_subtree_size = root_index - in_start;

        root->left = build(preorder, pre_start + 1, pre_start + left_subtree_size,
                           inorder, in_start, root_index - 1, index_map);
        root->right = build(preorder, pre_start + left_subtree_size + 1, pre_end,
                            inorder, root_index + 1, in_end, index_map);

        return root;
    }
};

// Helper function to print inorder traversal of the tree
void printInorder(TreeNode* root) {
    if (root == nullptr) return;
    printInorder(root->left);
    cout << root->val << " ";
    printInorder(root->right);
}

int main() {
    Solution solution;
    vector<int> preorder = {3, 9, 20, 15, 7};
    vector<int> inorder = {9, 3, 15, 20, 7};

    TreeNode* root = solution.buildTree(preorder, inorder);

    cout << "Inorder Traversal of Constructed Tree: ";
    printInorder(root);
    cout << endl;

    return 0;
}
```

#### Time Complexity

- **Construction**: Each node of the tree is visited exactly once, so the time complexity is O(n), where n is the number of nodes in the binary tree.

#### Space Complexity

- **Memory Usage**: The space complexity is O(n) due to the recursive calls and the unordered_map used for storing indices of elements in the inorder traversal.

This algorithm efficiently constructs the binary tree from its inorder and preorder traversals with linear time complexity.

### 1. Algorithms & Data Structures (C++): Binary Trees: Time & Space Complexity : Finding Number of Nodes in a Binary Tree

In a binary tree, the time and space complexity of finding the number of nodes depends on the approach used.

#### Approach 1: Recursive Approach

**Time Complexity:** \( O(n) \)

- In the worst-case scenario, where every node needs to be visited to count, the time complexity is linear, where \( n \) is the number of nodes in the tree.

**Space Complexity:** \( O(h) \)

- In the worst-case scenario, where the tree is completely unbalanced and resembles a linked list, the space complexity of the recursion stack is \( O(n) \).
- In a balanced binary tree, the height of the tree is \( O(\log n) \), so the space complexity would be \( O(\log n) \).

Here's a sample code in C++ for finding the number of nodes using recursion:

```cpp
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

int countNodes(TreeNode* root) {
    if (!root) return 0;
    return 1 + countNodes(root->left) + countNodes(root->right);
}
```

#### Approach 2: Iterative Approach (Using Queue)

**Time Complexity:** \( O(n) \)

- Similar to the recursive approach, we visit each node once, so the time complexity remains linear.

**Space Complexity:** \( O(w) \)

- \( w \) is the maximum width of the binary tree (the maximum number of nodes on any level).
- In the worst-case scenario, the space complexity of the queue would be \( O(w) \).

Here's a sample code in C++ for finding the number of nodes using an iterative approach with a queue:

```cpp
#include <queue>

int countNodes(TreeNode* root) {
    if (!root) return 0;
    
    std::queue<TreeNode*> q;
    q.push(root);
    int count = 0;
    
    while (!q.empty()) {
        TreeNode* node = q.front();
        q.pop();
        count++;
        if (node->left) q.push(node->left);
        if (node->right) q.push(node->right);
    }
    
    return count;
}
```

Both approaches have their advantages and disadvantages, depending on the specific context and requirements of the problem.

### 1. Algorithms & Data Structures (C++): Binary Trees: Time & Space Complexity : Finding the Height of a Binary Tree

To understand the time and space complexity of finding the height of a binary tree, let's first discuss the algorithm for finding the height of a binary tree and then analyze its complexity.

#### Algorithm for Finding Height of Binary Tree

The height of a binary tree is the longest path from the root node to any leaf node. Here's a simple recursive algorithm to find the height of a binary tree:

1. If the tree is empty (root is null), height is 0.
2. Otherwise, the height is the maximum of the height of the left subtree and the height of the right subtree, plus 1 (to account for the root node).

```cpp
int height(Node* root) {
    // Base case: empty tree
    if (root == nullptr) 
        return 0;
    else {
        // Recursive calls to find the height of left and right subtrees
        int left_height = height(root->left);
        int right_height = height(root->right);

        // Height of the tree is the maximum height of the left or right subtree + 1
        return max(left_height, right_height) + 1;
    }
}
```

#### Time Complexity Analysis

The time complexity of finding the height of a binary tree using this algorithm is \(O(n)\), where \(n\) is the number of nodes in the tree. This is because in the worst-case scenario, the algorithm needs to visit every node in the tree once to calculate its height.

#### Space Complexity Analysis

The space complexity of this algorithm is also \(O(n)\) due to the recursive calls. In the worst-case scenario, the recursive calls will create a call stack with a depth equal to the height of the binary tree, which can be \(O(n)\) for a skewed tree. Additionally, if we consider the space required for the function parameters and local variables in each recursive call, the total space complexity becomes \(O(n)\).

#### Summary

- **Time Complexity:** \(O(n)\)
- **Space Complexity:** \(O(n)\)

This algorithm efficiently finds the height of a binary tree by recursively traversing through its nodes, with both time and space complexities linearly proportional to the number of nodes in the tree.

### 1. Algorithms & Data Structures (C++): Binary Trees: Using Global Structure for Stack instead of Global Variable

Sure, in C++, you can implement a binary tree using a stack without relying on global variables by passing the stack as a parameter to your tree functions. Here's a basic example to illustrate this:

```cpp
#include <iostream>
#include <stack>

using namespace std;

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void inorderTraversal(TreeNode* root) {
    if (root == nullptr) return;
    
    stack<TreeNode*> nodeStack;
    TreeNode* curr = root;
    
    while (curr != nullptr || !nodeStack.empty()) {
        while (curr != nullptr) {
            nodeStack.push(curr);
            curr = curr->left;
        }
        
        curr = nodeStack.top();
        nodeStack.pop();
        cout << curr->val << " ";
        
        curr = curr->right;
    }
}

int main() {
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    
    cout << "Inorder traversal: ";
    inorderTraversal(root);
    
    return 0;
}
```

In this code:

- `inorderTraversal` function performs an inorder traversal of the binary tree iteratively using a stack.
- The `nodeStack` is created locally within the function, so it's not a global variable.
- The stack is passed as a parameter to the function, eliminating the need for global variables.

This way, you maintain encapsulation and can use the function `inorderTraversal` with different stacks for different binary trees.

### 1. Algorithms & Data Structures (C++): Build Tree - Boilerplate

Certainly! Here's a basic boilerplate code to build a binary tree in C++:

```cpp
#include <iostream>

// Define the structure for a tree node
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to create a new node
TreeNode* newNode(int val) {
    return new TreeNode(val);
}

// Function to insert a new node with given value
TreeNode* insert(TreeNode* root, int val) {
    if (root == nullptr) {
        return newNode(val);
    }
    if (val < root->val) {
        root->left = insert(root->left, val);
    } else {
        root->right = insert(root->right, val);
    }
    return root;
}

// Function to build a binary tree from an array
TreeNode* buildTree(int arr[], int n) {
    TreeNode* root = nullptr;
    for (int i = 0; i < n; ++i) {
        root = insert(root, arr[i]);
    }
    return root;
}

// Function to print the inorder traversal of the tree
void inorderTraversal(TreeNode* root) {
    if (root == nullptr) {
        return;
    }
    inorderTraversal(root->left);
    std::cout << root->val << " ";
    inorderTraversal(root->right);
}

int main() {
    int arr[] = {5, 3, 7, 2, 4, 6, 8}; // Example array to build the tree
    int n = sizeof(arr) / sizeof(arr[0]);
    
    TreeNode* root = buildTree(arr, n);

    std::cout << "Inorder traversal of the constructed tree: ";
    inorderTraversal(root);
    std::cout << std::endl;

    return 0;
}
```

This code defines a `TreeNode` structure representing a node in the binary tree. It provides functions to create a new node, insert a new node into the tree, build a binary tree from an array of integers, and perform an inorder traversal of the tree. Finally, the `main()` function demonstrates how to use these functions to build a tree and perform an inorder traversal.

### 1. Algorithms & Data Structures (C++): Check children-sum property in a binary tree

Checking the children-sum property in a binary tree involves ensuring that for every node in the tree, the sum of its children's values equals its own value. Here's a C++ implementation to check the children-sum property in a binary tree:

```cpp
#include <iostream>
using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to check if the children-sum property holds for a binary tree
bool checkChildrenSum(TreeNode* root) {
    // Base case: If the node is null, return true
    if (root == nullptr)
        return true;

    // If the node is a leaf node, return true
    if (root->left == nullptr && root->right == nullptr)
        return true;

    // Get the sum of children's values
    int childrenSum = 0;
    if (root->left != nullptr)
        childrenSum += root->left->val;
    if (root->right != nullptr)
        childrenSum += root->right->val;

    // Check if the children-sum property holds for the current node
    if (root->val == childrenSum)
        // Recursively check the children of the current node
        return checkChildrenSum(root->left) && checkChildrenSum(root->right);
    else
        return false;
}

int main() {
    // Example binary tree
    TreeNode* root = new TreeNode(10);
    root->left = new TreeNode(8);
    root->right = new TreeNode(2);
    root->left->left = new TreeNode(3);
    root->left->right = new TreeNode(5);
    root->right->left = new TreeNode(1);

    // Check if the children-sum property holds for the binary tree
    if (checkChildrenSum(root))
        cout << "The children-sum property holds for the binary tree.\n";
    else
        cout << "The children-sum property does not hold for the binary tree.\n";

    return 0;
}
```

This code defines a binary tree node structure `TreeNode` and a function `checkChildrenSum` to check the children-sum property recursively. In the `main` function, it creates an example binary tree and checks if the children-sum property holds for it.

### 1. Algorithms & Data Structures (C++): Check Completeness of A Binary Tree

To check the completeness of a binary tree in C++, you can use a breadth-first search (BFS) traversal technique. Here's how you can implement it:

```cpp
#include <iostream>
#include <queue>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

bool isCompleteTree(TreeNode* root) {
    if (!root) return true;

    queue<TreeNode*> q;
    q.push(root);
    bool end = false;

    while (!q.empty()) {
        TreeNode* node = q.front();
        q.pop();

        // If we have encountered a null node and there are still non-null nodes in the queue
        // then it's not a complete tree.
        if (node == nullptr) {
            end = true;
        } else {
            if (end) return false; // A non-null node after encountering a null node
            q.push(node->left);
            q.push(node->right);
        }
    }

    return true;
}

// Test the function
int main() {
    // Example 1
    TreeNode* root1 = new TreeNode(1);
    root1->left = new TreeNode(2);
    root1->right = new TreeNode(3);
    root1->left->left = new TreeNode(4);
    root1->left->right = new TreeNode(5);
    root1->right->left = new TreeNode(6);
    cout << "Is tree 1 complete? " << (isCompleteTree(root1) ? "Yes" : "No") << endl;

    // Example 2
    TreeNode* root2 = new TreeNode(1);
    root2->left = new TreeNode(2);
    root2->right = new TreeNode(3);
    root2->left->left = new TreeNode(4);
    root2->left->right = new TreeNode(5);
    root2->right->right = new TreeNode(6);
    cout << "Is tree 2 complete? " << (isCompleteTree(root2) ? "Yes" : "No") << endl;

    return 0;
}
```

This code defines a function `isCompleteTree` that takes the root of the binary tree as input and returns true if the tree is complete and false otherwise. The `main` function tests this function with two example trees.

### 1. Algorithms & Data Structures (C++): Complete Binary Tree

A complete binary tree is a special type of binary tree in which every level, except possibly the last, is completely filled, and all nodes are as far left as possible. This structure has some interesting properties and applications, particularly in heaps. Here's how you might implement a complete binary tree in C++:

```cpp
#include <iostream>
#include <queue>
using namespace std;

// Node structure for binary tree
struct Node {
    int data;
    Node* left;
    Node* right;
    
    Node(int val) {
        data = val;
        left = nullptr;
        right = nullptr;
    }
};

// Function to insert a new node in level order
Node* insert(Node* root, int data) {
    if (root == nullptr) {
        root = new Node(data);
        return root;
    }
    queue<Node*> q;
    q.push(root);
    while (!q.empty()) {
        Node* temp = q.front();
        q.pop();
        if (temp->left != nullptr)
            q.push(temp->left);
        else {
            temp->left = new Node(data);
            return root;
        }
        if (temp->right != nullptr)
            q.push(temp->right);
        else {
            temp->right = new Node(data);
            return root;
        }
    }
    return root;
}

// Function to print level order traversal of binary tree
void printLevelOrder(Node* root) {
    if (root == nullptr)
        return;
    queue<Node*> q;
    q.push(root);
    while (!q.empty()) {
        Node* temp = q.front();
        q.pop();
        cout << temp->data << " ";
        if (temp->left != nullptr)
            q.push(temp->left);
        if (temp->right != nullptr)
            q.push(temp->right);
    }
}

int main() {
    Node* root = nullptr;
    root = insert(root, 1);
    insert(root, 2);
    insert(root, 3);
    insert(root, 4);
    insert(root, 5);
    insert(root, 6);
    insert(root, 7);

    cout << "Level order traversal of binary tree: ";
    printLevelOrder(root);

    return 0;
}
```

This code defines a `Node` structure for the binary tree and provides functions for insertion and level order traversal. In the `insert` function, it maintains the property of a complete binary tree by inserting new nodes at the leftmost position possible. The `printLevelOrder` function is used to print the level order traversal of the binary tree.

### 1. Algorithms & Data Structures (C++): Count Operations of Binary Tree

Certainly! To count the number of operations (specifically, comparisons) in a binary tree, you typically traverse the tree and perform certain operations at each node. If you're counting comparisons, it usually involves comparing keys or values while traversing the tree.

Here's a basic implementation in C++ using a simple binary tree structure and counting the number of comparisons:

```cpp
#include <iostream>

using namespace std;

// Definition of a binary tree node
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to insert a node into the binary tree
TreeNode* insert(TreeNode* root, int val, int& comparisons) {
    if (root == nullptr) {
        comparisons++; // Count the comparison for finding an empty spot to insert
        return new TreeNode(val);
    }

    if (val < root->val) {
        comparisons++; // Count the comparison for comparison with current node's value
        root->left = insert(root->left, val, comparisons);
    } else if (val > root->val) {
        comparisons++; // Count the comparison for comparison with current node's value
        root->right = insert(root->right, val, comparisons);
    }
    return root;
}

// Function to count the number of operations (comparisons) when inserting elements into the binary tree
int countOperations(int arr[], int n) {
    TreeNode* root = nullptr;
    int comparisons = 0;
    for (int i = 0; i < n; ++i) {
        root = insert(root, arr[i], comparisons);
    }
    return comparisons;
}

int main() {
    int arr[] = {5, 3, 8, 1, 4, 7, 9};
    int n = sizeof(arr) / sizeof(arr[0]);

    int operations = countOperations(arr, n);
    cout << "Total operations (comparisons) performed: " << operations << endl;

    return 0;
}
```

In this implementation:

- We define a `TreeNode` struct to represent each node in the binary tree.
- The `insert` function inserts a new value into the binary tree while counting the number of comparisons made during the insertion process.
- The `countOperations` function takes an array of integers and counts the number of comparisons needed to insert each element into the binary tree.
- In the `main` function, we define an array of integers, insert them into the binary tree, and then print out the total number of comparisons performed.

This code provides a basic framework for counting operations (specifically, comparisons) in a binary tree in C++. You can extend it further to count other types of operations or to analyze different algorithms.

### 1. Algorithms & Data Structures (C++): Counting the Number of Nodes in a Binary Tree

Counting the number of nodes in a binary tree is a common operation in computer science. Here's how you can implement it in C++ using a recursive approach:

```cpp
#include <iostream>

// Definition for a binary tree node
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to count the number of nodes in a binary tree
int countNodes(TreeNode* root) {
    if (root == nullptr) // If tree is empty
        return 0;
    else
        return 1 + countNodes(root->left) + countNodes(root->right);
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    
    int nodeCount = countNodes(root);
    std::cout << "Number of nodes in the binary tree: " << nodeCount << std::endl;

    // Clean up memory (optional)
    // Note: In a real-world scenario, you'd likely have a proper function to deallocate tree nodes.
    delete root->left->right;
    delete root->left->left;
    delete root->right;
    delete root->left;
    delete root;

    return 0;
}
```

In this code:

- We define a `TreeNode` struct to represent each node in the binary tree.
- The `countNodes` function takes a pointer to the root of the binary tree as input and returns the count of nodes in the tree.
- It recursively counts nodes by adding 1 for the current node and recursively counting nodes in its left and right subtrees.
- In the `main` function, we create an example binary tree, count its nodes using `countNodes`, and print the result. Finally, we clean up dynamically allocated memory.

### 1. Algorithms & Data Structures (C++): Cousins in Binary Tree

To find if two nodes in a binary tree are cousins, you need to traverse the tree and keep track of the depth and parent of each node. If two nodes have the same depth but different parents, they are cousins. Here's a C++ implementation using a depth-first search (DFS) approach:

```cpp
#include <iostream>
#include <unordered_map>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

class Solution {
public:
    bool isCousins(TreeNode* root, int x, int y) {
        unordered_map<int, pair<int, TreeNode*>> nodeInfo; // map of node value to its depth and parent
        dfs(root, nullptr, 0, nodeInfo); // start DFS traversal from root

        // Check if both nodes exist and have different parents at the same depth
        return (nodeInfo.count(x) && nodeInfo.count(y) && 
                nodeInfo[x].first == nodeInfo[y].first && 
                nodeInfo[x].second != nodeInfo[y].second);
    }

private:
    // Depth-first search function
    void dfs(TreeNode* node, TreeNode* parent, int depth, unordered_map<int, pair<int, TreeNode*>>& nodeInfo) {
        if (node == nullptr) return;

        // Store depth and parent of the current node
        nodeInfo[node->val] = make_pair(depth, parent);

        // Recursive DFS for left and right children
        dfs(node->left, node, depth + 1, nodeInfo);
        dfs(node->right, node, depth + 1, nodeInfo);
    }
};

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->right = new TreeNode(4);
    root->right->right = new TreeNode(5);

    Solution sol;
    int x = 4, y = 5;
    if (sol.isCousins(root, x, y))
        cout << x << " and " << y << " are cousins." << endl;
    else
        cout << x << " and " << y << " are not cousins." << endl;

    // Free memory
    delete root->left->right;
    delete root->right->right;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

This code defines a `TreeNode` struct representing each node in the binary tree, and a `Solution` class with the `isCousins` method to determine if two nodes are cousins. It performs a DFS traversal of the tree to gather information about each node's depth and parent, then checks if the given nodes have the same depth but different parents.

### 1. Algorithms & Data Structures (C++): Create Binary Tree

Sure! Here's a simple implementation of a binary tree in C++:

```cpp
#include <iostream>

using namespace std;

// Define the structure of a node in the binary tree
struct Node {
    int data;
    Node* left;
    Node* right;

    Node(int value) {
        data = value;
        left = nullptr;
        right = nullptr;
    }
};

// Function to insert a new node into the binary tree
Node* insert(Node* root, int value) {
    if (root == nullptr) {
        root = new Node(value);
    } else {
        if (value <= root->data) {
            root->left = insert(root->left, value);
        } else {
            root->right = insert(root->right, value);
        }
    }
    return root;
}

// Function to traverse the binary tree in inorder (left, root, right) manner
void inorderTraversal(Node* root) {
    if (root != nullptr) {
        inorderTraversal(root->left);
        cout << root->data << " ";
        inorderTraversal(root->right);
    }
}

int main() {
    // Create an empty binary tree
    Node* root = nullptr;

    // Insert elements into the binary tree
    root = insert(root, 10);
    root = insert(root, 5);
    root = insert(root, 15);
    root = insert(root, 7);
    root = insert(root, 12);

    // Perform inorder traversal of the binary tree
    cout << "Inorder Traversal: ";
    inorderTraversal(root);
    cout << endl;

    return 0;
}
```

This code defines a basic binary tree structure with functions to insert nodes into the tree and perform an inorder traversal. You can modify and extend this code as needed for your specific requirements.

### 1. Algorithms & Data Structures (C++): Create Binary Trees

Sure, let's create a simple binary tree implementation in C++. We'll start with the Node structure for the tree and then create a BinaryTree class to manage the tree operations like insertion, deletion, traversal, etc.

```cpp
#include <iostream>

// Node structure for the binary tree
struct Node {
    int data;
    Node* left;
    Node* right;

    Node(int value) : data(value), left(nullptr), right(nullptr) {}
};

// BinaryTree class
class BinaryTree {
private:
    Node* root;

    // Private helper function for inserting a new node
    Node* insertNode(Node* root, int value) {
        if (root == nullptr) {
            return new Node(value);
        }
        if (value < root->data) {
            root->left = insertNode(root->left, value);
        } else {
            root->right = insertNode(root->right, value);
        }
        return root;
    }

    // Private helper function for traversing the tree (inorder)
    void inorderTraversal(Node* root) {
        if (root != nullptr) {
            inorderTraversal(root->left);
            std::cout << root->data << " ";
            inorderTraversal(root->right);
        }
    }

public:
    // Constructor
    BinaryTree() : root(nullptr) {}

    // Method to insert a new value into the tree
    void insert(int value) {
        root = insertNode(root, value);
    }

    // Method to perform inorder traversal of the tree
    void inorder() {
        inorderTraversal(root);
        std::cout << std::endl;
    }
};

// Main function for testing
int main() {
    BinaryTree tree;

    // Insert some values into the tree
    tree.insert(50);
    tree.insert(30);
    tree.insert(20);
    tree.insert(40);
    tree.insert(70);
    tree.insert(60);
    tree.insert(80);

    // Perform inorder traversal to display the tree
    std::cout << "Inorder Traversal: ";
    tree.inorder();

    return 0;
}
```

In this code:

- We define a `Node` struct to represent each node in the binary tree.
- The `BinaryTree` class manages the tree operations. It has a private `root` member, which is a pointer to the root node of the tree.
- The `insertNode` function is a private helper function that recursively inserts a new node into the tree based on the value.
- The `insert` method inserts a new value into the tree.
- The `inorderTraversal` function is a private helper function that performs an inorder traversal of the tree.
- The `inorder` method calls `inorderTraversal` to print the values of the tree in inorder traversal.
- In the `main` function, we create a `BinaryTree` object, insert some values into it, and then perform an inorder traversal to display the values of the tree.

### 1. Algorithms & Data Structures (C++): Creating Binary Tree

Creating a binary tree in C++ involves defining a structure for the tree nodes and implementing methods to manipulate the tree, such as insertion, deletion, and traversal. Here's a basic example:

```cpp
#include <iostream>

using namespace std;

// Define the structure for a binary tree node
struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;
    
    TreeNode(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Function to insert a new node in the binary tree
void insert(TreeNode* &root, int val) {
    if (root == nullptr) {
        root = new TreeNode(val);
    } else {
        if (val < root->data) {
            insert(root->left, val);
        } else {
            insert(root->right, val);
        }
    }
}

// Function to perform inorder traversal of the binary tree
void inorderTraversal(TreeNode* root) {
    if (root != nullptr) {
        inorderTraversal(root->left);
        cout << root->data << " ";
        inorderTraversal(root->right);
    }
}

int main() {
    // Initialize an empty binary tree
    TreeNode* root = nullptr;

    // Insert elements into the binary tree
    insert(root, 5);
    insert(root, 3);
    insert(root, 7);
    insert(root, 2);
    insert(root, 4);
    insert(root, 6);
    insert(root, 8);

    // Perform inorder traversal to display the elements
    cout << "Inorder Traversal: ";
    inorderTraversal(root);
    cout << endl;

    return 0;
}
```

This code defines a `TreeNode` struct representing each node in the binary tree. The `insert` function inserts a new node into the tree maintaining its binary search property. The `inorderTraversal` function performs an inorder traversal of the tree, printing out the elements in sorted order.

In the `main` function, we create an empty binary tree and insert some elements into it. Finally, we perform an inorder traversal to display the elements.

### 1. Algorithms & Data Structures (C++): Data Structure: Binary Tree

A binary tree is a hierarchical data structure composed of nodes, where each node has at most two children, referred to as the left child and the right child. The topmost node is called the root. Binary trees are widely used in computer science for various applications such as representing hierarchical data, searching, sorting, and more.

In C++, you can implement a binary tree using classes. Here's a basic implementation of a binary tree node and the binary tree itself:

```cpp
#include <iostream>

using namespace std;

// Node structure for the binary tree
struct Node {
    int data;
    Node* left;
    Node* right;

    Node(int value) {
        data = value;
        left = nullptr;
        right = nullptr;
    }
};

// Binary tree class
class BinaryTree {
private:
    Node* root;

    // Private helper function for inserting a node recursively
    Node* insertRecursively(Node* current, int value) {
        if (current == nullptr) {
            return new Node(value);
        }
        if (value < current->data) {
            current->left = insertRecursively(current->left, value);
        } else if (value > current->data) {
            current->right = insertRecursively(current->right, value);
        }
        return current;
    }

    // Private helper function for printing the tree (in-order traversal)
    void inOrderTraversal(Node* node) {
        if (node != nullptr) {
            inOrderTraversal(node->left);
            cout << node->data << " ";
            inOrderTraversal(node->right);
        }
    }

public:
    BinaryTree() {
        root = nullptr;
    }

    // Public function to insert a node into the binary tree
    void insert(int value) {
        root = insertRecursively(root, value);
    }

    // Public function to print the binary tree (in-order traversal)
    void print() {
        inOrderTraversal(root);
        cout << endl;
    }
};

// Example usage
int main() {
    BinaryTree tree;

    // Insert some values into the binary tree
    tree.insert(5);
    tree.insert(3);
    tree.insert(7);
    tree.insert(2);
    tree.insert(4);

    // Print the binary tree (in-order traversal)
    cout << "Binary Tree (In-order traversal): ";
    tree.print();

    return 0;
}
```

This code defines a `Node` struct representing a node in the binary tree and a `BinaryTree` class for managing the tree. It includes methods for inserting nodes into the tree and printing the tree using in-order traversal. You can extend this implementation by adding other operations like deletion, searching, or different traversal methods (pre-order, post-order).

### 1. Algorithms & Data Structures (C++): Delete a node from Binary Tree

To delete a node from a binary tree in C++, you need to consider three cases:

1. If the node to be deleted is a leaf node (has no children), simply remove it from the tree.
2. If the node to be deleted has only one child, bypass it by linking its parent directly to its child.
3. If the node to be deleted has two children, you can either replace it with its inorder successor or its inorder predecessor.

Here's a C++ implementation to delete a node from a binary tree:

```cpp
#include <iostream>

struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;

    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to find the node with minimum value in a tree
TreeNode* minValueNode(TreeNode* node) {
    TreeNode* current = node;
    // Loop down to find the leftmost leaf
    while (current && current->left != nullptr)
        current = current->left;
    return current;
}

// Function to delete a node from a binary tree
TreeNode* deleteNode(TreeNode* root, int key) {
    // Base case: if the tree is empty
    if (root == nullptr) return root;

    // If the key to be deleted is smaller than the root's key, then it lies in the left subtree
    if (key < root->val)
        root->left = deleteNode(root->left, key);
    // If the key to be deleted is greater than the root's key, then it lies in the right subtree
    else if (key > root->val)
        root->right = deleteNode(root->right, key);
    // If key is same as root's key, then this is the node to be deleted
    else {
        // Node with only one child or no child
        if (root->left == nullptr) {
            TreeNode* temp = root->right;
            delete root;
            return temp;
        } else if (root->right == nullptr) {
            TreeNode* temp = root->left;
            delete root;
            return temp;
        }

        // Node with two children: Get the inorder successor (smallest in the right subtree)
        TreeNode* temp = minValueNode(root->right);
        // Copy the inorder successor's content to this node
        root->val = temp->val;
        // Delete the inorder successor
        root->right = deleteNode(root->right, temp->val);
    }
    return root;
}

// Function to print the inorder traversal of the tree
void inorderTraversal(TreeNode* root) {
    if (root != nullptr) {
        inorderTraversal(root->left);
        std::cout << root->val << " ";
        inorderTraversal(root->right);
    }
}

int main() {
    // Create a binary tree
    TreeNode* root = new TreeNode(5);
    root->left = new TreeNode(3);
    root->right = new TreeNode(7);
    root->left->left = new TreeNode(2);
    root->left->right = new TreeNode(4);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(8);

    std::cout << "Inorder traversal before deletion: ";
    inorderTraversal(root);
    std::cout << std::endl;

    int key = 3;
    root = deleteNode(root, key);

    std::cout << "Inorder traversal after deletion of " << key << ": ";
    inorderTraversal(root);
    std::cout << std::endl;

    return 0;
}
```

This code demonstrates how to delete a node from a binary tree in C++. You can modify it as needed for your use case.

### 1. Algorithms & Data Structures (C++): Delete entire Binary Tree

To delete an entire binary tree in C++, you typically perform a post-order traversal and delete each node as you visit it. Here's a simple implementation:

```cpp
#include <iostream>

// Define the structure for a node in the binary tree
struct Node {
    int data;
    Node* left;
    Node* right;
    
    Node(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Function to delete a binary tree
void deleteBinaryTree(Node* root) {
    if (root == nullptr)
        return;
    
    // Delete left and right subtrees recursively
    deleteBinaryTree(root->left);
    deleteBinaryTree(root->right);
    
    // Delete the current node
    delete root;
}

int main() {
    // Example usage
    // Creating a binary tree
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);

    // Deleting the binary tree
    deleteBinaryTree(root);

    return 0;
}
```

This code will traverse the tree in a post-order manner, ensuring that child nodes are deleted before their parent. Finally, it deletes the root node. Make sure you call `deleteBinaryTree` with the root node of your binary tree to properly deallocate memory.

### 1. Algorithms & Data Structures (C++): Diameter Of A Binary Tree

To find the diameter of a binary tree, you need to calculate the longest path between any two nodes in the tree. The path may or may not pass through the root.

Here's a C++ implementation using depth-first search (DFS) to calculate the height of the tree and recursively find the diameter:

```cpp
#include <iostream>
#include <algorithm>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Helper function to calculate the height of a binary tree
int height(TreeNode* root) {
    if (root == nullptr)
        return 0;
    return 1 + max(height(root->left), height(root->right));
}

// Function to calculate the diameter of a binary tree
int diameterOfBinaryTree(TreeNode* root) {
    if (root == nullptr)
        return 0;
    
    // Calculate the height of the left and right subtrees
    int leftHeight = height(root->left);
    int rightHeight = height(root->right);
    
    // Calculate the diameter passing through the root
    int diameterThroughRoot = leftHeight + rightHeight;
    
    // Recursively calculate the diameters of the left and right subtrees
    int leftDiameter = diameterOfBinaryTree(root->left);
    int rightDiameter = diameterOfBinaryTree(root->right);
    
    // Return the maximum of the three diameters
    return max(diameterThroughRoot, max(leftDiameter, rightDiameter));
}

// Sample test case
int main() {
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    
    cout << "Diameter of the binary tree: " << diameterOfBinaryTree(root) << endl;
    
    return 0;
}
```

This code calculates the diameter of the binary tree using a recursive approach. The `height` function calculates the height of the tree, and the `diameterOfBinaryTree` function calculates the diameter by considering the diameter passing through the root and recursively calculating the diameters of the left and right subtrees. Finally, it returns the maximum of these three values.

### 1. Algorithms & Data Structures (C++): Diameter Of A Binary Tree - Binary Trees

To find the diameter of a binary tree, you need to find the longest path between any two nodes in the tree. This path may or may not pass through the root node. The diameter of a tree can be calculated as the maximum of the following:

1. Diameter of the left subtree.
2. Diameter of the right subtree.
3. Longest path between two nodes that passes through the root node (this can be calculated as the height of the left subtree + height of the right subtree + 1).

Here's a C++ implementation using a recursive approach:

```cpp
#include <iostream>
#include <algorithm>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

// Utility function to calculate the height of a binary tree
int height(TreeNode* root) {
    if (root == NULL)
        return 0;
    return max(height(root->left), height(root->right)) + 1;
}

// Function to calculate the diameter of a binary tree
int diameterOfBinaryTree(TreeNode* root) {
    if (root == NULL)
        return 0;

    // Calculate the height of the left and right subtrees
    int leftHeight = height(root->left);
    int rightHeight = height(root->right);

    // Calculate the diameter recursively for the left and right subtrees
    int leftDiameter = diameterOfBinaryTree(root->left);
    int rightDiameter = diameterOfBinaryTree(root->right);

    // Return the maximum of the three: left subtree diameter, right subtree diameter, or the sum of left and right subtree heights + 1
    return max(max(leftDiameter, rightDiameter), leftHeight + rightHeight);
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    cout << "Diameter of the binary tree is: " << diameterOfBinaryTree(root) << endl;

    return 0;
}
```

This code calculates the diameter of the binary tree in O(n^2) time complexity. You can optimize it to O(n) time complexity by combining the height calculation and diameter calculation in a single function and traversing the tree only once.

### 1. Algorithms & Data Structures (C++): Diameter Of A Binary Tree - Trees

Sure! Calculating the diameter of a binary tree involves finding the longest path between any two nodes in the tree. The path doesn't necessarily need to pass through the root node.

Here's how you can implement it in C++:

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

class Solution {
public:
    int diameterOfBinaryTree(TreeNode* root) {
        int diameter = 0;
        calculateDepth(root, diameter);
        return diameter;
    }

    int calculateDepth(TreeNode* node, int& diameter) {
        if (node == nullptr) return 0;

        // Recursively calculate the depth of the left and right subtrees
        int leftDepth = calculateDepth(node->left, diameter);
        int rightDepth = calculateDepth(node->right, diameter);

        // Update the diameter if the sum of the depths of the left and right subtrees is greater
        diameter = max(diameter, leftDepth + rightDepth);

        // Return the depth of the current node
        return 1 + max(leftDepth, rightDepth);
    }
};

// Helper function to create a binary tree from an array representation
TreeNode* createBinaryTree(const vector<int>& arr, int index) {
    TreeNode* root = nullptr;
    if (index < arr.size() && arr[index] != -1) {
        root = new TreeNode(arr[index]);
        root->left = createBinaryTree(arr, 2 * index + 1);
        root->right = createBinaryTree(arr, 2 * index + 2);
    }
    return root;
}

int main() {
    // Example usage
    vector<int> arr = {1, 2, 3, 4, 5}; // Example binary tree [1,2,3,4,5]
    TreeNode* root = createBinaryTree(arr, 0);
    
    Solution sol;
    int diameter = sol.diameterOfBinaryTree(root);
    cout << "Diameter of the binary tree: " << diameter << endl;

    return 0;
}
```

In this implementation:

- We define a `TreeNode` struct to represent each node in the binary tree.
- The `Solution` class contains a method `diameterOfBinaryTree` which calculates the diameter of the binary tree.
- The `calculateDepth` function is a helper function used to calculate the depth of each node recursively.
- In the `calculateDepth` function, for each node, we calculate the depth of its left and right subtrees recursively. We also update the diameter if the sum of the depths of the left and right subtrees is greater than the current diameter.
- The `main` function provides an example usage where a binary tree is created from an array representation, and the diameter is calculated using the `Solution` class.

### 1. Algorithms & Data Structures (C++): Diameter of Binary Tree

Calculating the diameter of a binary tree involves finding the longest path between any two nodes in the tree. The path may or may not pass through the root. The diameter can be calculated by first finding the height of the left and right subtrees for each node and then finding the maximum diameter among all nodes.

Here's a C++ implementation using a recursive approach:

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

// Utility function to find the height of a binary tree
int height(TreeNode* root, int& diameter) {
    if (root == nullptr)
        return 0;
    
    // Recursively calculate height of left and right subtrees
    int leftHeight = height(root->left, diameter);
    int rightHeight = height(root->right, diameter);
    
    // Update diameter if the current node forms part of the longest path
    diameter = max(diameter, leftHeight + rightHeight);
    
    // Return height of current node
    return 1 + max(leftHeight, rightHeight);
}

// Function to calculate the diameter of a binary tree
int diameterOfBinaryTree(TreeNode* root) {
    if (root == nullptr)
        return 0;
    
    int diameter = 0;
    height(root, diameter);
    return diameter;
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    
    cout << "Diameter of the binary tree: " << diameterOfBinaryTree(root) << endl;
    
    // Remember to free the memory
    delete root->left->right;
    delete root->left->left;
    delete root->left;
    delete root->right;
    delete root;
    
    return 0;
}
```

This code defines a `TreeNode` structure representing a node in the binary tree. The `diameterOfBinaryTree` function calculates the diameter of the binary tree using the `height` function, which computes the height of the binary tree and updates the diameter along the way. Finally, in the `main` function, an example binary tree is created and the diameter is printed.

### 1. Algorithms & Data Structures (C++): Evaluate a Binary Expression Tree

Evaluating a binary expression tree involves traversing the tree in a manner that respects the order of operations (parentheses, multiplication/division, addition/subtraction). Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <stack>
#include <string>
#include <cctype>

using namespace std;

// Define the binary tree node structure
struct TreeNode {
    string val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(string x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to evaluate a binary expression tree
int evaluateExpressionTree(TreeNode* root) {
    if (!root) return 0;
    
    stack<int> s;
    // Traverse the tree in postorder (left, right, root)
    stack<TreeNode*> nodes;
    nodes.push(root);
    while (!nodes.empty()) {
        TreeNode* current = nodes.top();
        nodes.pop();
        if (isdigit(current->val[0])) {
            s.push(stoi(current->val));
        } else {
            int op2 = s.top();
            s.pop();
            int op1 = s.top();
            s.pop();
            if (current->val == "+") {
                s.push(op1 + op2);
            } else if (current->val == "-") {
                s.push(op1 - op2);
            } else if (current->val == "*") {
                s.push(op1 * op2);
            } else if (current->val == "/") {
                s.push(op1 / op2);
            }
        }
        if (current->right) {
            nodes.push(current->right);
        }
        if (current->left) {
            nodes.push(current->left);
        }
    }
    return s.top();
}

int main() {
    // Construct the expression tree
    TreeNode* root = new TreeNode("+");
    root->left = new TreeNode("*");
    root->left->left = new TreeNode("5");
    root->left->right = new TreeNode("4");
    root->right = new TreeNode("-");
    root->right->left = new TreeNode("100");
    root->right->right = new TreeNode("20");

    // Evaluate the expression tree
    int result = evaluateExpressionTree(root);
    cout << "Result: " << result << endl;

    // Clean up allocated memory
    delete root->left->left;
    delete root->left->right;
    delete root->right->left;
    delete root->right->right;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

This code defines a `TreeNode` struct representing nodes in the expression tree, and an `evaluateExpressionTree` function to evaluate the expression tree. It uses a stack to keep track of operands while traversing the tree. Finally, it constructs an example expression tree, evaluates it, and prints the result.

### 1. Algorithms & Data Structures (C++): Find Height of Binary Tree

To find the height of a binary tree in C++, you can implement a recursive algorithm. Here's a simple example:

```cpp
#include <iostream>
#include <algorithm> // for max

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

int height(TreeNode* root) {
    if (root == nullptr) {
        return 0; // Height of an empty tree is 0
    } else {
        // Recursively find the height of the left and right subtrees
        int left_height = height(root->left);
        int right_height = height(root->right);
        
        // Return the maximum height of the left and right subtrees, plus 1 for the current node
        return 1 + std::max(left_height, right_height);
    }
}

int main() {
    // Example usage:
    // Constructing a binary tree:
    //        1
    //       / \
    //      2   3
    //     / \
    //    4   5
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    // Find the height of the binary tree
    int tree_height = height(root);
    std::cout << "Height of the binary tree: " << tree_height << std::endl;

    // Remember to free the memory allocated for the tree nodes
    delete root->left->right;
    delete root->left->left;
    delete root->right;
    delete root->left;
    delete root;

    return 0;
}
```

This code defines a `TreeNode` struct for the binary tree nodes and a `height` function to find the height of the binary tree. The `main` function demonstrates how to construct a binary tree and find its height.

### 1. Algorithms & Data Structures (C++): Find Height of Binary Tree

To find the height of a binary tree in C++, you can implement a recursive algorithm. Here's a simple example:

```cpp
#include <iostream>
#include <algorithm> // for max

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

int height(TreeNode* root) {
    if (root == nullptr) {
        return 0; // Height of an empty tree is 0
    } else {
        // Recursively find the height of the left and right subtrees
        int left_height = height(root->left);
        int right_height = height(root->right);
        
        // Return the maximum height of the left and right subtrees, plus 1 for the current node
        return 1 + std::max(left_height, right_height);
    }
}

int main() {
    // Example usage:
    // Constructing a binary tree:
    //        1
    //       / \
    //      2   3
    //     / \
    //    4   5
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    // Find the height of the binary tree
    int tree_height = height(root);
    std::cout << "Height of the binary tree: " << tree_height << std::endl;

    // Remember to free the memory allocated for the tree nodes
    delete root->left->right;
    delete root->left->left;
    delete root->right;
    delete root->left;
    delete root;

    return 0;
}
```

This code defines a `TreeNode` struct for the binary tree nodes and a `height` function to find the height of the binary tree. The `main` function demonstrates how to construct a binary tree and find its height.

### 1. Algorithms & Data Structures (C++): Finding Diameter in Binary Tree

To find the diameter of a binary tree in C++, you can use Depth First Search (DFS) to compute the height (or depth) of each subtree rooted at every node, and while doing so, keep track of the maximum diameter encountered. The diameter of the tree is the longest path between any two nodes in the tree.

Here's a C++ implementation:

```cpp
#include <iostream>
#include <algorithm>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

// Function to find the height of a binary tree
int height(TreeNode* root, int& diameter) {
    if (root == nullptr) return 0;

    // Recursively find the height of left and right subtrees
    int left_height = height(root->left, diameter);
    int right_height = height(root->right, diameter);

    // Update the diameter if the current node's subtree diameter is larger
    diameter = max(diameter, left_height + right_height);

    // Return the height of the current node's subtree
    return 1 + max(left_height, right_height);
}

// Function to find the diameter of a binary tree
int diameterOfBinaryTree(TreeNode* root) {
    if (root == nullptr) return 0;
    
    int diameter = 0;
    height(root, diameter);
    
    return diameter;
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    cout << "Diameter of the binary tree: " << diameterOfBinaryTree(root) << endl;

    // Delete dynamically allocated memory
    delete root->left->right;
    delete root->left->left;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

In this code:

- `height` function recursively computes the height of each subtree and updates the diameter if the sum of the heights of the left and right subtrees is greater than the current diameter.
- `diameterOfBinaryTree` function initializes the diameter to 0 and calls the `height` function to compute the diameter.
- In the `main` function, an example binary tree is created and the diameter is printed.

This implementation runs in O(n) time, where n is the number of nodes in the binary tree, since it visits each node exactly once.

### 1. Algorithms & Data Structures (C++): Finding Node in Binary Tree

In C++, you can find a node in a binary tree using various techniques such as depth-first search (DFS) or breadth-first search (BFS). Here's an example implementation of finding a node using DFS:

```cpp
#include <iostream>

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class BinaryTree {
public:
    TreeNode* findNode(TreeNode* root, int value) {
        if (root == nullptr || root->val == value) {
            return root;
        }

        // Search in the left subtree
        TreeNode* leftResult = findNode(root->left, value);
        if (leftResult != nullptr) {
            return leftResult;
        }

        // Search in the right subtree
        return findNode(root->right, value);
    }
};

int main() {
    // Example usage
    BinaryTree tree;

    // Create a binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(7);

    int valueToFind = 5;
    TreeNode* result = tree.findNode(root, valueToFind);

    if (result != nullptr) {
        std::cout << "Node with value " << valueToFind << " found in the binary tree." << std::endl;
    } else {
        std::cout << "Node with value " << valueToFind << " not found in the binary tree." << std::endl;
    }

    // Clean up memory
    // You should have a function to delete the tree to avoid memory leaks
    delete root->left->left;
    delete root->left->right;
    delete root->right->left;
    delete root->right->right;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

This code defines a binary tree structure and a class `BinaryTree` with a method `findNode` which performs a depth-first search to find the node with the given value. In the `main` function, an example usage of this method is demonstrated. Make sure to handle memory management properly, especially in a real-world application.

### 1. Algorithms & Data Structures (C++): Full Binary Tree

A full binary tree, also known as a proper binary tree or 2-tree, is a special type of binary tree in which every node other than the leaves has exactly two children. In a full binary tree, all leaf nodes are at the same level, and every non-leaf node has exactly two children.

Here's a basic implementation of a full binary tree in C++:

```cpp
#include <iostream>
#include <queue>
using namespace std;

// Node structure for the binary tree
struct Node {
    int data;
    Node* left;
    Node* right;

    Node(int value) {
        data = value;
        left = nullptr;
        right = nullptr;
    }
};

// Function to check if a binary tree is full
bool isFullBinaryTree(Node* root) {
    // If the tree is empty, it is full by definition
    if (root == nullptr)
        return true;
    
    // If the node has no children, it is a leaf and therefore full
    if (root->left == nullptr && root->right == nullptr)
        return true;
    
    // If the node has exactly two children, recursively check its subtrees
    if (root->left && root->right)
        return isFullBinaryTree(root->left) && isFullBinaryTree(root->right);
    
    // If any node has only one child, the tree is not full
    return false;
}

int main() {
    // Creating a sample full binary tree
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    root->right->left = new Node(6);
    root->right->right = new Node(7);

    // Check if the tree is a full binary tree
    if (isFullBinaryTree(root))
        cout << "The tree is a full binary tree." << endl;
    else
        cout << "The tree is not a full binary tree." << endl;

    return 0;
}
```

In this implementation:

- We define a `Node` struct to represent each node of the binary tree.
- The `isFullBinaryTree` function recursively checks whether the given binary tree is full or not.
- In the `main` function, we create a sample full binary tree and then call the `isFullBinaryTree` function to check if it's a full binary tree or not.

You can modify this code to suit your specific needs or integrate it into a larger program as necessary.

### 1. Algorithms & Data Structures (C++): Full Binary Tree: Number Of Nodes At Last Level

To find the number of nodes at the last level of a full binary tree, you can use the property that in a full binary tree, each level is completely filled except possibly for the last level, which is filled from left to right. Here's how you can calculate the number of nodes at the last level in C++:

```cpp
#include <iostream>
#include <cmath>

// Structure for a node in the binary tree
struct Node {
    int data;
    Node* left;
    Node* right;
    Node(int value) : data(value), left(nullptr), right(nullptr) {}
};

// Function to calculate the height of a full binary tree
int heightOfFullBinaryTree(Node* root) {
    if (root == nullptr)
        return 0;
    int height = 0;
    while (root->left != nullptr) {
        height++;
        root = root->left;
    }
    return height;
}

// Function to calculate the number of nodes at the last level of a full binary tree
int nodesAtLastLevel(Node* root) {
    int height = heightOfFullBinaryTree(root);
    return (height == 0) ? 1 : pow(2, height);
}

int main() {
    // Create a sample full binary tree
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    root->right->left = new Node(6);

    // Calculate the number of nodes at the last level
    int lastLevelNodes = nodesAtLastLevel(root);
    std::cout << "Number of nodes at the last level: " << lastLevelNodes << std::endl;

    // Clean up memory
    delete root->left->left;
    delete root->left->right;
    delete root->right->left;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

This program first calculates the height of the full binary tree using the `heightOfFullBinaryTree` function. Then, it computes the number of nodes at the last level using the formula \(2^{\text{height}}\), where `height` is the height of the tree.

### 1. Algorithms & Data Structures (C++): Full vs Complete Binary Tree

A full binary tree and a complete binary tree are two distinct concepts in the realm of algorithms and data structures, particularly in the context of binary trees.

1. **Full Binary Tree**:
   - A full binary tree is a tree in which every node other than the leaves has exactly two children.
   - In other words, every node in a full binary tree has either 0 or 2 children.
   - It's worth noting that the number of nodes in a full binary tree grows exponentially with the tree's height, following the formula \(2^h - 1\), where \(h\) is the height of the tree.

2. **Complete Binary Tree**:
   - A complete binary tree is a binary tree in which every level, except possibly the last, is completely filled, and all nodes are as far left as possible.
   - In simpler terms, all levels of the tree, except possibly the last one, are fully filled, and if the last level is not complete, the nodes are filled from left to right.
   - Complete binary trees are often used in heap data structures because they allow for efficient storage and traversal.
   - The number of nodes in a complete binary tree can vary but typically is between \(2^{h - 1}\) and \(2^h - 1\), where \(h\) is the height of the tree.

**Differences**:

1. **Node Structure**:
   - In a full binary tree, each node can have either 0 or 2 children.
   - In a complete binary tree, every level, except possibly the last one, is fully filled from left to right.

2. **Number of Nodes**:
   - The number of nodes in a full binary tree is \(2^h - 1\), where \(h\) is the height of the tree.
   - The number of nodes in a complete binary tree can vary but typically ranges between \(2^{h - 1}\) and \(2^h - 1\), where \(h\) is the height of the tree.

3. **Usage**:
   - Full binary trees are more of a theoretical concept and are less commonly used in practical applications.
   - Complete binary trees are frequently used in heap data structures and binary heaps due to their efficient storage properties.

In C++, you can implement both types of binary trees using different approaches, depending on your specific requirements and the problem you are solving.

### 1. Algorithms & Data Structures (C++): Full Vs Complete Vs Almost Complete Binary Trees

In the realm of algorithms and data structures, binary trees are fundamental structures used for organizing and storing data efficiently. Let's break down the concepts of full, complete, and almost complete binary trees in the context of C++.

1. **Full Binary Tree**:
   - In a full binary tree, every node has either zero or two children.
   - It's important to note that a full binary tree is not necessarily balanced, meaning the depths of the left and right subtrees of any node can differ by at most one.
   - In a full binary tree, if a node has a child, then it must have exactly two children.
   - Example:

     ```bash
           A
         /   \
        B     C
       / \   /
      D   E F
     ```

2. **Complete Binary Tree**:
   - A complete binary tree is a tree in which every level, except possibly the last, is completely filled, and all nodes are as far left as possible.
   - In a complete binary tree, if there are any missing nodes in the last level, they must appear as far left as possible.
   - Complete binary trees are often used in heaps, where elements are added from left to right.
   - Example:

     ```bash
           A
         /   \
        B     C
       / \   /
      D   E F
     ```

3. **Almost Complete Binary Tree**:
   - An almost complete binary tree is a binary tree in which all levels are completely filled except possibly for the last level, which is filled from left to right.
   - This means that all levels, except possibly the last, are completely filled, and the last level is filled from left to right but may not be completely filled.
   - Example:

     ```bash
           A
         /   \
        B     C
       / \   / \
      D   E F   G
     ```

In C++, you can implement these binary tree structures using various techniques, such as linked lists or arrays. Depending on your application and requirements (e.g., insertion and deletion efficiency, memory consumption), you may choose one representation over another.

### 1. Algorithms & Data Structures (C++): Full Vs Complete Vs Proper Binary Tree

In the realm of algorithms and data structures, binary trees are fundamental structures frequently encountered. Let's delve into each type you mentioned:

1. **Full Binary Tree**:
   - A full binary tree is a tree in which every node other than the leaves has exactly two children.
   - All leaves are at the same level, meaning the tree is completely filled.
   - Also known as a proper binary tree or 2-tree.

   Example:

   ```bash
         1
       /   \
      2     3
     / \   / \
    4   5 6   7
   ```

   In this example, every non-leaf node has two children, making it a full binary tree.

2. **Complete Binary Tree**:
   - A complete binary tree is a binary tree in which every level, except possibly the last, is completely filled, and all nodes are as far left as possible.
   - Essentially, it's a tree where nodes are added from left to right across each level.
   - The shape of a complete binary tree can be irregular at the last level, but all nodes must be as far left as possible.

   Example:

   ```bash
         1
       /   \
      2     3
     / \   /
    4   5 6
   ```

   In this example, all levels are completely filled except possibly the last, and nodes are filled from left to right.

3. **Proper Binary Tree**:
   - A proper binary tree is a tree in which every internal node has exactly two children.
   - It can have any arrangement of nodes as long as each internal node has two children.

   Example:

   ```bash
         1
       /   \
      2     3
     / \   
    4   5  
   ```

   In this example, every internal node has exactly two children, satisfying the definition of a proper binary tree.

So, to summarize:

- A **full binary tree** is one where every non-leaf node has exactly two children.
- A **complete binary tree** is one where every level, except possibly the last, is completely filled, and all nodes are as far left as possible.
- A **proper binary tree** is one where every internal node has exactly two children.

Each type of binary tree has its own properties and use cases in various algorithms and applications.

### 1. Algorithms & Data Structures (C++): Height and Count of Binary Tree

Sure, I can provide you with the code for calculating the height and count of a binary tree in C++. Here's a simple implementation using a binary tree structure:

```cpp
#include <iostream>
#include <queue>
using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to calculate the height of a binary tree
int height(TreeNode* root) {
    if (root == nullptr) return 0;
    int leftHeight = height(root->left);
    int rightHeight = height(root->right);
    return 1 + max(leftHeight, rightHeight);
}

// Function to count the number of nodes in a binary tree
int countNodes(TreeNode* root) {
    if (root == nullptr) return 0;
    return 1 + countNodes(root->left) + countNodes(root->right);
}

int main() {
    // Sample binary tree creation
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(7);

    cout << "Height of the binary tree: " << height(root) << endl;
    cout << "Number of nodes in the binary tree: " << countNodes(root) << endl;

    // Free memory
    delete root->left->left;
    delete root->left->right;
    delete root->right->left;
    delete root->right->right;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

This code calculates the height and count of nodes in a binary tree using recursive functions. The `height` function calculates the height of the tree, and the `countNodes` function counts the number of nodes. The `main` function demonstrates the usage by creating a sample binary tree and calling these functions. Finally, it frees the allocated memory to avoid memory leaks.

### 1. Algorithms & Data Structures (C++): Height of a Binary Tree

Calculating the height of a binary tree is a fundamental operation in tree-related algorithms and data structures. The height of a binary tree is defined as the maximum number of edges in any path from the root node to a leaf node. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <algorithm> // for max function

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

// Function to calculate the height of a binary tree
int height(TreeNode* root) {
    if (root == NULL) {
        return -1; // height of an empty tree is -1
    } else {
        // Recursively calculate the height of the left and right subtrees
        int leftHeight = height(root->left);
        int rightHeight = height(root->right);
        
        // Return the maximum of the heights of the left and right subtrees, plus 1 (for the root)
        return 1 + std::max(leftHeight, rightHeight);
    }
}

int main() {
    // Example usage:
    // Constructing a binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    // Calculating the height of the binary tree
    int treeHeight = height(root);
    std::cout << "Height of the binary tree: " << treeHeight << std::endl;

    // Clean up memory (optional)
    delete root->left->left;
    delete root->left->right;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

This code first defines a `TreeNode` structure to represent nodes in the binary tree. Then, it defines the `height` function which recursively calculates the height of the binary tree. Finally, in the `main` function, it constructs a binary tree, calculates its height using the `height` function, and prints the result.

### 1. Algorithms & Data Structures (C++): Height Operations of Binary Tree

In C++, you can define a binary tree and implement operations to find its height using recursion. Here's a basic implementation:

```cpp
#include <iostream>
#include <algorithm>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

// Function to find the height of a binary tree
int height(TreeNode* root) {
    if (root == NULL) // Base case: empty tree
        return 0;
    else {
        // Recursively calculate the height of the left and right subtrees
        int left_height = height(root->left);
        int right_height = height(root->right);
        
        // Height of the tree is the maximum of the heights of its left and right subtrees, plus 1 for the root
        return max(left_height, right_height) + 1;
    }
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    cout << "Height of the binary tree is: " << height(root) << endl;

    return 0;
}
```

In this code:

1. We define a `TreeNode` structure to represent each node of the binary tree. It contains a value (`val`) and pointers to its left and right children.
2. The `height` function recursively calculates the height of the binary tree. If the tree is empty (root is NULL), the height is 0. Otherwise, it recursively finds the heights of the left and right subtrees and returns the maximum of these heights plus 1 (for the root node).
3. In the `main` function, we create an example binary tree and print its height.

You can modify the `main` function to create different binary trees and test the `height` function.

### 1. Algorithms & Data Structures (C++): Height vs Node of Strict Binary Tree

In a strict binary tree, also known as a full binary tree, each node has either 0 or 2 children. The height of a binary tree is the maximum number of edges on the longest path from the root node to a leaf node. In a binary tree, the height is defined recursively as the height of the tallest subtree plus one (the root node itself).

Now, let's discuss the relationship between the height of a strict binary tree and the number of nodes it contains.

For a strict binary tree of height \( h \):

1. **Minimum number of nodes**: In a strict binary tree of height \( h \), the minimum number of nodes it can have is \( 2^{h} \). This is achieved when every level is completely filled except possibly the last level, which is filled from left to right.

2. **Maximum number of nodes**: The maximum number of nodes a strict binary tree of height \( h \) can have is \( 2^{h+1} - 1 \). This is achieved when every level is completely filled.

So, for a given height \( h \), the number of nodes in a strict binary tree can range from \( 2^{h} \) to \( 2^{h+1} - 1 \).

In C++, you could represent a strict binary tree using a class for nodes, with each node having pointers to its left and right children. You could then write functions to calculate the height of the tree and count the number of nodes recursively. Here's a simple example:

```cpp
#include <iostream>
#include <cmath>

class Node {
public:
    int data;
    Node* left;
    Node* right;

    Node(int value) : data(value), left(nullptr), right(nullptr) {}
};

int height(Node* root) {
    if (root == nullptr)
        return -1; // Empty tree has height -1
    else
        return 1 + std::max(height(root->left), height(root->right));
}

int countNodes(Node* root) {
    if (root == nullptr)
        return 0;
    else
        return 1 + countNodes(root->left) + countNodes(root->right);
}

int main() {
    // Constructing a binary tree
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);

    // Calculate height and number of nodes
    int treeHeight = height(root);
    int nodeCount = countNodes(root);

    std::cout << "Height of the tree: " << treeHeight << std::endl;
    std::cout << "Number of nodes: " << nodeCount << std::endl;

    return 0;
}
```

This code demonstrates how to calculate the height and count the number of nodes in a binary tree recursively in C++.

### 1. Algorithms & Data Structures (C++): Height vs Nodes in Binary Tree

In a binary tree, the relationship between height and the number of nodes can vary depending on the tree's structure.

1. **Maximum Number of Nodes in a Binary Tree of Height h**:
   - For a binary tree of height \( h \), the maximum number of nodes it can have is \( 2^{h+1} - 1 \). This is a result of each level of the tree having double the number of nodes compared to the previous level.

2. **Minimum Number of Nodes in a Binary Tree of Height h**:
   - The minimum number of nodes in a binary tree of height \( h \) is \( h+1 \). This is achieved when the tree is a degenerate tree or a skewed tree, where each node has only one child, except for the leaf nodes.

So, the relationship between height and the number of nodes can be expressed as follows:

- For a given height \( h \), the number of nodes can vary between \( h+1 \) (minimum) and \( 2^{h+1} - 1 \) (maximum).
- Generally, if you know the number of nodes in a binary tree, you can determine its height by performing a logarithmic operation based on the number of nodes. Conversely, if you know the height, you can determine the maximum and minimum number of nodes the tree can have.

### 1. Algorithms & Data Structures (C++): How do Binary Heaps work?

Binary heaps are a fundamental data structure used to implement priority queues, which are abstract data types that allow efficient access to the element with the highest (or lowest) priority. Binary heaps are particularly useful because they have efficient insertion, deletion, and retrieval times, all of which are logarithmic in the worst case.

Here's how binary heaps work:

1. **Binary Tree Structure**: Binary heaps are implemented as binary trees, specifically complete binary trees. In a complete binary tree, all levels of the tree are completely filled except possibly for the last level, which is filled from left to right.

2. **Heap Property**: Binary heaps come in two varieties: max heaps and min heaps. In a max heap, for any given node \( i \), the value of \( i \) is greater than or equal to the values of its children. In a min heap, the value of \( i \) is less than or equal to the values of its children. This property ensures that the root node contains the maximum (or minimum) element.

3. **Heap Operations**:
   - **Insertion**: When inserting a new element, it is placed at the next available position in the heap (usually at the bottom level and rightmost position). Then, the heap property is restored by swapping the new element with its parent until the heap property is satisfied.
   - **Deletion**: Removing the maximum (or minimum) element from the heap is done by removing the root node. After removal, the last element of the heap is moved to the root position, and then the heap property is restored by swapping the new root with its children as necessary.
   - **Peek**: The element with the highest (or lowest) priority can be retrieved without removing it from the heap. This is simply the value of the root node.
   - **Heapify**: It's a process to create a heap from an array of elements. This is often done when we need to convert an unordered array into a heap structure. Heapify operation takes linear time complexity.

4. **Implementation**:
   - Heaps are often implemented using arrays. In a binary heap, for any element at index \( i \), its left child is located at index \( 2i + 1 \) and its right child at index \( 2i + 2 \).
   - This array-based implementation allows for efficient memory usage and easy traversal of the heap.

Binary heaps are commonly used in algorithms like heap sort, priority queues, and graph algorithms like Dijkstra's shortest path algorithm and Prim's minimum spanning tree algorithm due to their efficient operations.

### 1. Algorithms & Data Structures (C++): How do you insert into a Binary Heap?

To insert an element into a binary heap in C++, you typically follow these steps:

1. **Append the element to the end of the heap**: Start by inserting the new element at the end of the array representing the heap.

2. **Heapify Up (percolate up)**: After inserting the element, compare it with its parent. If the element is smaller (in a min-heap) or larger (in a max-heap) than its parent, swap them. Repeat this process until the element is in the correct position in the heap.

Here's a sample C++ code to illustrate this process for inserting into a min-heap:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class MinHeap {
private:
    vector<int> heap;

    // Helper function to swap two elements
    void swap(int& a, int& b) {
        int temp = a;
        a = b;
        b = temp;
    }

    // Helper function to perform Heapify Up
    void heapifyUp(int index) {
        int parent = (index - 1) / 2;
        while (index > 0 && heap[index] < heap[parent]) {
            swap(heap[index], heap[parent]);
            index = parent;
            parent = (index - 1) / 2;
        }
    }

public:
    // Function to insert an element into the heap
    void insert(int value) {
        heap.push_back(value); // Append the element to the end
        heapifyUp(heap.size() - 1); // Perform Heapify Up from the inserted position
    }

    // Function to print the heap
    void printHeap() {
        for (int i = 0; i < heap.size(); i++) {
            cout << heap[i] << " ";
        }
        cout << endl;
    }
};

int main() {
    MinHeap minHeap;
    minHeap.insert(3);
    minHeap.insert(2);
    minHeap.insert(1);
    minHeap.insert(15);
    minHeap.insert(5);
    minHeap.insert(4);
    minHeap.insert(45);
    minHeap.printHeap(); // Output should be 1 2 4 15 5 3 45
    return 0;
}
```

This code defines a `MinHeap` class with `insert` and `printHeap` methods. The `insert` method adds an element to the heap and then calls `heapifyUp` to maintain the heap property. Finally, `printHeap` is used to print the heap after insertion.

### 1. Algorithms & Data Structures (C++): Inserting a node in Binary Tree

Sure! Inserting a node into a binary tree involves finding the appropriate location for the new node based on its value and then adding it there. Here's a basic C++ implementation:

```cpp
#include <iostream>

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void insert(TreeNode* &root, int val) {
    if (root == nullptr) {
        root = new TreeNode(val);
        return;
    }

    if (val < root->val) {
        insert(root->left, val);
    } else {
        insert(root->right, val);
    }
}

void inorderTraversal(TreeNode* root) {
    if (root == nullptr) return;

    inorderTraversal(root->left);
    std::cout << root->val << " ";
    inorderTraversal(root->right);
}

int main() {
    TreeNode* root = nullptr;
    
    // Inserting nodes into the binary tree
    insert(root, 5);
    insert(root, 3);
    insert(root, 7);
    insert(root, 1);
    insert(root, 4);
    insert(root, 6);
    insert(root, 8);

    // Print the inorder traversal of the binary tree
    std::cout << "Inorder Traversal: ";
    inorderTraversal(root);
    std::cout << std::endl;

    return 0;
}
```

In this code:

1. We define a `TreeNode` struct which represents each node in the binary tree. Each node contains an integer value (`val`) and pointers to its left and right children.

2. The `insert` function recursively inserts a new node with the given value into the binary tree. If the tree is empty (`root == nullptr`), it creates a new node and sets it as the root. Otherwise, it compares the value with the current node's value and decides whether to insert it into the left subtree or the right subtree accordingly.

3. The `inorderTraversal` function performs an inorder traversal of the binary tree, printing out the values of the nodes in sorted order.

4. In the `main` function, we create an empty binary tree and insert several nodes into it. Then, we print the inorder traversal of the tree to verify that the nodes are inserted correctly.

### 1. Algorithms & Data Structures (C++): Internal Nodes vs External Nodes in Binary Tree

In a binary tree, nodes can be categorized into two main types: internal nodes and external nodes (also known as leaf nodes).

1. **Internal Nodes**:
   - Internal nodes are nodes that have at least one child node.
   - These nodes reside between other nodes in the tree structure.
   - They typically have a left child, a right child, or both.

2. **External Nodes (Leaf Nodes)**:
   - External nodes, also known as leaf nodes, are nodes that do not have any children.
   - They are situated at the outermost ends of the tree branches.
   - Leaf nodes have no outgoing edges in the tree structure.

In a binary tree, the internal nodes form the internal structure of the tree, defining the hierarchical relationships between nodes, while the external nodes represent the endpoints of those hierarchical relationships. Understanding the distinction between internal and external nodes is crucial for implementing and analyzing algorithms and data structures that operate on binary trees, such as traversal algorithms, insertion, deletion, and searching.

### 1. Algorithms & Data Structures (C++): Internal Vs External Nodes of a Binary Tree

In the context of binary trees, internal and external nodes are often discussed in terms of their structural properties within the tree.

1. **Internal Nodes**:
   - An internal node is a node that has at least one child.
   - In a binary tree, an internal node typically has two children, though it may have only one child if it's a part of a degenerate tree (essentially a linked list).
   - Internal nodes are usually the ones that contain data or serve as branching points in the tree.
   - They are not leaf nodes (external nodes) because they have at least one child.

2. **External Nodes (Leaf Nodes)**:
   - An external node, also known as a leaf node, is a node that has no children.
   - In a binary tree, a leaf node represents the endpoints of a branch in the tree structure.
   - Leaf nodes do not contain any data in a binary search tree (BST), but they may contain data in other types of binary trees.
   - They are typically the endpoints where data is stored or where the search terminates.

Here's a basic C++ representation of binary tree nodes to illustrate these concepts:

```cpp
template<typename T>
struct TreeNode {
    T data;
    TreeNode<T>* left;
    TreeNode<T>* right;

    TreeNode(const T& value) : data(value), left(nullptr), right(nullptr) {}
};
```

In this example, `TreeNode` represents a basic node in a binary tree. Each node contains some data (`data`), and two pointers to other nodes, representing the left and right children (`left` and `right`). In this representation, leaf nodes (`External Nodes`) have `nullptr` as both `left` and `right`, while internal nodes have non-null pointers for at least one of their children.

### 1. Algorithms & Data Structures (C++): Internal vs External Nodes of Strict Binary Trees

In the context of strict binary trees, the terms "internal nodes" and "external nodes" refer to different parts of the tree structure:

1. **Internal Nodes**:
   - Internal nodes are nodes that have at least one child.
   - In a strict binary tree, internal nodes always have exactly two children (left and right).
   - These nodes represent points of branching or decision-making within the tree.
   - Internal nodes are not the leaf nodes (nodes with no children).

2. **External Nodes (Leaf Nodes)**:
   - External nodes, also known as leaf nodes, are nodes that have no children.
   - These are the endpoints of the tree branches.
   - In a strict binary tree, every external node will have a parent.
   - They represent the data elements or values stored in the tree.

Here's a simple C++ representation of a strict binary tree node:

```cpp
template<typename T>
struct TreeNode {
    T data;
    TreeNode* left;
    TreeNode* right;

    TreeNode(const T& value) : data(value), left(nullptr), right(nullptr) {}
};
```

In this structure, `left` and `right` pointers point to the left and right child nodes, respectively. When a node doesn't have a child, these pointers are set to `nullptr`.

You can traverse through a strict binary tree and identify internal and external nodes by checking whether a node has children or not. Here's a simple recursive function to count internal and external nodes:

```cpp
template<typename T>
void countInternalExternal(TreeNode<T>* root, int& internalCount, int& externalCount) {
    if (root == nullptr)
        return;

    if (root->left != nullptr || root->right != nullptr) {
        // Internal node
        internalCount++;
    } else {
        // External node
        externalCount++;
    }

    // Recursively count in the left and right subtrees
    countInternalExternal(root->left, internalCount, externalCount);
    countInternalExternal(root->right, internalCount, externalCount);
}
```

You can call this function with the root of your tree to count the number of internal and external nodes.

### 1. Algorithms & Data Structures (C++): Invert Binary Tree

Inverting a binary tree is a classic problem in computer science and can be implemented using recursion. Here's a C++ implementation:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        // Base case: if the node is null, return null
        if (root == nullptr)
            return nullptr;
        
        // Swap the left and right subtrees
        TreeNode* temp = root->left;
        root->left = invertTree(root->right);
        root->right = invertTree(temp);
        
        return root;
    }
};

// Function to print the binary tree in inorder traversal
void printInOrder(TreeNode* root) {
    if (root == nullptr)
        return;
    printInOrder(root->left);
    std::cout << root->val << " ";
    printInOrder(root->right);
}

int main() {
    // Create a binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    
    // Print the original tree
    std::cout << "Original tree: ";
    printInOrder(root);
    std::cout << std::endl;
    
    // Invert the binary tree
    Solution solution;
    TreeNode* invertedRoot = solution.invertTree(root);
    
    // Print the inverted tree
    std::cout << "Inverted tree: ";
    printInOrder(invertedRoot);
    std::cout << std::endl;
    
    return 0;
}
```

In this implementation, the `invertTree` function takes a pointer to the root of a binary tree and recursively inverts its left and right subtrees. Then, it swaps the left and right subtrees of the current node and returns the root of the modified tree.

You can use the `printInOrder` function to print the binary tree in inorder traversal before and after inverting it.

### 1. Algorithms & Data Structures (C++): Invert Binary Tree - Binary Trees

To invert a binary tree means to swap the left and right children of every node. It's a straightforward operation, typically implemented using recursion. Here's a C++ implementation:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        // Base case: if the root is null, return null
        if (root == nullptr)
            return nullptr;
        
        // Recursively invert left and right subtrees
        TreeNode* left = invertTree(root->left);
        TreeNode* right = invertTree(root->right);
        
        // Swap left and right subtrees
        root->left = right;
        root->right = left;
        
        return root;
    }
};

// Helper function to print the tree in inorder traversal
void inorderTraversal(TreeNode* root) {
    if (root != nullptr) {
        inorderTraversal(root->left);
        std::cout << root->val << " ";
        inorderTraversal(root->right);
    }
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(4);
    root->left = new TreeNode(2);
    root->right = new TreeNode(7);
    root->left->left = new TreeNode(1);
    root->left->right = new TreeNode(3);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(9);

    std::cout << "Original tree: ";
    inorderTraversal(root);
    std::cout << std::endl;

    Solution sol;
    TreeNode* invertedRoot = sol.invertTree(root);

    std::cout << "Inverted tree: ";
    inorderTraversal(invertedRoot);
    std::cout << std::endl;

    return 0;
}
```

This code defines a `TreeNode` struct representing a node in the binary tree, a `Solution` class with a method `invertTree` to invert the binary tree, and a `main` function demonstrating its usage with an example tree.

### 1. Algorithms & Data Structures (C++): Invert Binary Tree - Trees

Inverting a binary tree is a common algorithmic problem in computer science. The idea is to swap the left and right children of each node in the tree. This can be done recursively or iteratively. Here's a simple C++ implementation using recursion:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if (root == nullptr) {
            return nullptr;
        }
        
        // Swap left and right children
        TreeNode* temp = root->left;
        root->left = root->right;
        root->right = temp;
        
        // Recursively invert left and right subtrees
        invertTree(root->left);
        invertTree(root->right);
        
        return root;
    }
};

// Utility function to print the tree in inorder traversal
void printInOrder(TreeNode* root) {
    if (root == nullptr) {
        return;
    }
    printInOrder(root->left);
    std::cout << root->val << " ";
    printInOrder(root->right);
}

int main() {
    // Create a binary tree
    TreeNode* root = new TreeNode(4);
    root->left = new TreeNode(2);
    root->right = new TreeNode(7);
    root->left->left = new TreeNode(1);
    root->left->right = new TreeNode(3);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(9);

    // Print original tree
    std::cout << "Original tree (inorder): ";
    printInOrder(root);
    std::cout << std::endl;

    // Invert the tree
    Solution solution;
    TreeNode* invertedRoot = solution.invertTree(root);

    // Print inverted tree
    std::cout << "Inverted tree (inorder): ";
    printInOrder(invertedRoot);
    std::cout << std::endl;

    // Clean up memory
    // (This is omitted for brevity in this example)
    
    return 0;
}
```

This code defines a `TreeNode` struct representing a node in the binary tree and a `Solution` class with a method `invertTree` to invert the binary tree. The `invertTree` method swaps the left and right children of each node recursively. Finally, the `main` function demonstrates how to use this solution by creating a binary tree, inverting it, and printing the results.

This is a basic example. Depending on your use case, you might need to handle null pointers or use an iterative approach for large trees to avoid stack overflow due to recursion.

### 1. Algorithms & Data Structures (C++): Left View

The left view of a binary tree is the set of all nodes visible from the left side when looking from the root node to the rightmost node. Implementing the left view of a binary tree involves traversing the tree in a specific order and keeping track of the level of each node. Here's a C++ implementation using a recursive approach:

```cpp
#include <iostream>
#include <queue>
using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

void leftViewUtil(TreeNode* root, int level, int* max_level) {
    // Base Case
    if (root == NULL)
        return;

    // If this is the first node of its level
    if (*max_level < level) {
        cout << root->val << " ";
        *max_level = level;
    }

    // Recur for left and right subtrees
    leftViewUtil(root->left, level + 1, max_level);
    leftViewUtil(root->right, level + 1, max_level);
}

// Function to print left view of a binary tree
void leftView(TreeNode* root) {
    int max_level = 0;
    leftViewUtil(root, 1, &max_level);
}

// Test the left view function
int main() {
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->right = new TreeNode(4);
    root->right->left = new TreeNode(5);
    root->right->right = new TreeNode(6);
    root->right->left->left = new TreeNode(7);

    cout << "Left view of the binary tree: ";
    leftView(root);

    return 0;
}
```

This code defines a binary tree node structure (`TreeNode`) and implements a function `leftView` to print the left view of a binary tree. The `leftViewUtil` function is a recursive utility function that performs a depth-first traversal of the binary tree, keeping track of the level of each node. It prints the value of the leftmost node at each level encountered for the first time. Finally, the `main` function creates a sample binary tree and tests the `leftView` function.

### 1. Algorithms & Data Structures (C++): Level Order Build

Level order build is a technique used to construct a binary tree from its level order traversal. In this method, you are given an array representing the level order traversal of a binary tree, and you need to build the binary tree from it. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <queue>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

TreeNode* levelOrderBuild(vector<int>& nums) {
    if (nums.empty()) return nullptr;

    TreeNode* root = new TreeNode(nums[0]);
    queue<TreeNode*> q;
    q.push(root);

    int i = 1;
    while (!q.empty() && i < nums.size()) {
        TreeNode* current = q.front();
        q.pop();

        // Create left child if exists
        if (i < nums.size() && nums[i] != -1) {
            current->left = new TreeNode(nums[i]);
            q.push(current->left);
        }
        i++;

        // Create right child if exists
        if (i < nums.size() && nums[i] != -1) {
            current->right = new TreeNode(nums[i]);
            q.push(current->right);
        }
        i++;
    }

    return root;
}

// Function to print the inorder traversal of the binary tree
void inorderTraversal(TreeNode* root) {
    if (root) {
        inorderTraversal(root->left);
        cout << root->val << " ";
        inorderTraversal(root->right);
    }
}

int main() {
    // Example usage
    vector<int> nums = {3, 9, 20, -1, -1, 15, 7}; // Example level order traversal
    TreeNode* root = levelOrderBuild(nums);

    cout << "Inorder Traversal of the constructed tree: ";
    inorderTraversal(root);
    cout << endl;

    return 0;
}
```

In the above code:

- We define a `TreeNode` struct to represent each node of the binary tree.
- The `levelOrderBuild` function takes a vector `nums` representing the level order traversal of the binary tree and constructs the binary tree accordingly.
- We use a queue to keep track of the nodes at each level of the binary tree.
- We iterate over the elements of `nums`, creating nodes for each value encountered.
- `-1` is used to represent a null node (absence of a child).
- Finally, we print the inorder traversal of the constructed binary tree to verify its correctness.

You can modify the `TreeNode` struct or the traversal methods according to your requirements.

### 1. Algorithms & Data Structures (C++): Level Order Print

Level order printing is a common operation in tree-based data structures like binary trees and binary search trees. It involves traversing the tree level by level, starting from the root node and printing each level's nodes from left to right. This can be implemented using a queue data structure for breadth-first traversal. Below is a C++ implementation for level order printing of a binary tree:

```cpp
#include <iostream>
#include <queue>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

void printLevelOrder(TreeNode* root) {
    if (root == NULL)
        return;

    queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        int levelSize = q.size();

        for (int i = 0; i < levelSize; ++i) {
            TreeNode* node = q.front();
            q.pop();
            cout << node->val << " ";

            if (node->left != NULL)
                q.push(node->left);

            if (node->right != NULL)
                q.push(node->right);
        }

        cout << endl; // Move to the next level
    }
}

int main() {
    // Example tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(7);

    cout << "Level order traversal of binary tree:\n";
    printLevelOrder(root);

    return 0;
}
```

In this code:

- We define the `TreeNode` struct to represent nodes of the binary tree.
- The `printLevelOrder` function takes the root of the binary tree as input and prints its nodes in level order.
- We use a queue to perform breadth-first traversal. We push the root node into the queue initially.
- We then loop through the queue until it's empty. At each iteration, we process all nodes at the current level, printing their values and pushing their children (if any) into the queue.
- After printing all nodes at the current level, we move to the next level by printing a newline.

You can modify the `main` function to create your own binary trees and test the `printLevelOrder` function.

### 1. Algorithms & Data Structures (C++): LevelWise InputTree

A LevelWise InputTree refers to constructing a tree data structure in which nodes are inserted level by level, from left to right. This approach is commonly used in programming interviews and competitions. Here's a basic implementation of a binary tree in C++ using level-wise input:

```cpp
#include <iostream>
#include <queue>
using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to insert nodes level by level in a binary tree
TreeNode* levelWiseInput() {
    cout << "Enter the root value: ";
    int rootVal;
    cin >> rootVal;

    TreeNode* root = new TreeNode(rootVal);
    queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        TreeNode* currNode = q.front();
        q.pop();

        int leftVal, rightVal;
        cout << "Enter left child value of " << currNode->val << " (-1 for no left child): ";
        cin >> leftVal;
        if (leftVal != -1) {
            currNode->left = new TreeNode(leftVal);
            q.push(currNode->left);
        }

        cout << "Enter right child value of " << currNode->val << " (-1 for no right child): ";
        cin >> rightVal;
        if (rightVal != -1) {
            currNode->right = new TreeNode(rightVal);
            q.push(currNode->right);
        }
    }

    return root;
}

// Function to print the tree using inorder traversal
void inorderTraversal(TreeNode* root) {
    if (root == nullptr) return;
    inorderTraversal(root->left);
    cout << root->val << " ";
    inorderTraversal(root->right);
}

int main() {
    TreeNode* root = levelWiseInput();

    cout << "Inorder traversal of the constructed tree: ";
    inorderTraversal(root);
    cout << endl;

    return 0;
}
```

This code prompts the user to input values for each level of the binary tree, starting from the root and continuing level by level. It constructs the tree accordingly and then performs an inorder traversal to verify the correctness of the constructed tree.

### 1. Algorithms & Data Structures (C++): LevelWise PrintTree

Sure, a "LevelWise PrintTree" algorithm typically refers to printing a binary tree level by level. This is also known as a breadth-first traversal or level order traversal.

Here's a basic implementation of a binary tree in C++ along with a function to print the tree level by level:

```cpp
#include <iostream>
#include <queue>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to print a binary tree level by level
void printLevelOrder(TreeNode* root) {
    if (root == nullptr)
        return;

    // Create an empty queue for level order traversal
    queue<TreeNode*> q;

    // Enqueue root and initialize height
    q.push(root);

    while (!q.empty()) {
        // Print front of queue and remove it from queue
        TreeNode* tempNode = q.front();
        cout << tempNode->val << " ";
        q.pop();

        // Enqueue left child
        if (tempNode->left != nullptr)
            q.push(tempNode->left);

        // Enqueue right child
        if (tempNode->right != nullptr)
            q.push(tempNode->right);
    }
}

int main() {
    // Create a binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    cout << "Level Order traversal of binary tree is: ";
    printLevelOrder(root);

    return 0;
}
```

This code defines a simple binary tree structure and a function `printLevelOrder` to print the tree level by level. The `printLevelOrder` function uses a queue to keep track of nodes at each level. It starts from the root node, prints it, enqueues its children, and continues the process until all nodes are printed. This ensures that nodes at the same level are printed together before moving on to the next level.

### 1. Algorithms & Data Structures (C++): Linked Representation of Binary Tree

In C++, you can represent a binary tree using a linked representation where each node has pointers to its left and right children. Here's a simple implementation:

```cpp
#include <iostream>

// Define the structure of a tree node
struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;

    // Constructor
    TreeNode(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Function to create a new node
TreeNode* createNode(int data) {
    return new TreeNode(data);
}

// Function to insert a node into the binary tree
void insert(TreeNode*& root, int data) {
    if (root == nullptr) {
        root = createNode(data);
        return;
    }

    if (data < root->data) {
        insert(root->left, data);
    } else {
        insert(root->right, data);
    }
}

// Function to traverse the binary tree in-order
void inOrderTraversal(TreeNode* root) {
    if (root == nullptr) return;

    inOrderTraversal(root->left);
    std::cout << root->data << " ";
    inOrderTraversal(root->right);
}

int main() {
    TreeNode* root = nullptr;

    // Inserting elements into the binary tree
    insert(root, 5);
    insert(root, 3);
    insert(root, 7);
    insert(root, 1);
    insert(root, 4);

    // Printing the binary tree in-order
    std::cout << "In-order traversal: ";
    inOrderTraversal(root);
    std::cout << std::endl;

    return 0;
}
```

This code defines a `TreeNode` structure representing each node in the binary tree. The `insert` function is used to insert elements into the binary tree while maintaining the binary search tree property. The `inOrderTraversal` function traverses the binary tree in in-order (left, root, right) and prints the elements.

You can extend this implementation by adding functions for pre-order and post-order traversals, deletion of nodes, searching for a node, etc., depending on your requirements.

### 1. Algorithms & Data Structures (C++): Lowest common ancestor

Implementing the lowest common ancestor (LCA) algorithm in C++ typically involves using a binary tree or a binary search tree (BST). Here's a basic implementation using a binary tree:

```cpp
#include <iostream>

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    if (root == nullptr || root == p || root == q) {
        return root;
    }

    TreeNode* leftLCA = lowestCommonAncestor(root->left, p, q);
    TreeNode* rightLCA = lowestCommonAncestor(root->right, p, q);

    if (leftLCA && rightLCA) {
        return root;
    }

    return leftLCA ? leftLCA : rightLCA;
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(3);
    root->left = new TreeNode(5);
    root->right = new TreeNode(1);
    root->left->left = new TreeNode(6);
    root->left->right = new TreeNode(2);
    root->right->left = new TreeNode(0);
    root->right->right = new TreeNode(8);
    root->left->right->left = new TreeNode(7);
    root->left->right->right = new TreeNode(4);

    TreeNode* p = root->left;
    TreeNode* q = root->right;

    TreeNode* lca = lowestCommonAncestor(root, p, q);

    std::cout << "Lowest Common Ancestor: " << lca->val << std::endl;

    // Clean up
    delete root->left->right->right;
    delete root->left->right->left;
    delete root->right->right;
    delete root->right->left;
    delete root->left->right;
    delete root->left->left;
    delete root->right;
    delete root->left;
    delete root;

    return 0;
}
```

This implementation defines a `TreeNode` structure to represent each node in the binary tree. The `lowestCommonAncestor` function recursively traverses the tree to find the lowest common ancestor of two given nodes `p` and `q`. Finally, in the `main` function, it demonstrates the usage of this algorithm with an example binary tree.

### 1. Algorithms & Data Structures (C++): Lowest Common Ancestor - Binary Search Trees

Sure, the Lowest Common Ancestor (LCA) problem in Binary Search Trees (BSTs) is a classic problem in computer science. The problem involves finding the lowest (nearest) common ancestor of two nodes in a binary tree. In a BST, the LCA is defined as the node with the largest value smaller than the values of both nodes.

Here's a simple approach to find the LCA of two nodes in a BST:

1. Start from the root.
2. If both nodes are greater than the current node's value, move to the right subtree.
3. If both nodes are smaller than the current node's value, move to the left subtree.
4. If one node is smaller and the other is greater than the current node's value, then the current node is the LCA.
5. Repeat steps 2-4 until you find the LCA.

Here's a sample C++ code implementing this approach:

```cpp
#include <iostream>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        // Start from the root
        TreeNode* current = root;
        
        // Traverse the tree
        while (current != nullptr) {
            // If both nodes are greater than current, move to the right subtree
            if (p->val > current->val && q->val > current->val)
                current = current->right;
            // If both nodes are smaller than current, move to the left subtree
            else if (p->val < current->val && q->val < current->val)
                current = current->left;
            // If one node is smaller and the other is greater, current is the LCA
            else
                return current;
        }
        
        return nullptr; // No common ancestor found
    }
};

int main() {
    // Example usage
    Solution solution;

    // Create a BST
    TreeNode* root = new TreeNode(6);
    root->left = new TreeNode(2);
    root->right = new TreeNode(8);
    root->left->left = new TreeNode(0);
    root->left->right = new TreeNode(4);
    root->left->right->left = new TreeNode(3);
    root->left->right->right = new TreeNode(5);
    root->right->left = new TreeNode(7);
    root->right->right = new TreeNode(9);

    TreeNode* p = root->left->right->left;
    TreeNode* q = root->left->right->right;

    TreeNode* lca = solution.lowestCommonAncestor(root, p, q);
    if (lca)
        cout << "Lowest Common Ancestor: " << lca->val << endl;
    else
        cout << "No common ancestor found!" << endl;

    // Clean up memory
    // (In a real-world scenario, you should implement a proper destructor)
    delete root->right->right;
    delete root->right->left;
    delete root->left->right->right;
    delete root->left->right->left;
    delete root->left->right;
    delete root->left->left;
    delete root->right;
    delete root->left;
    delete root;

    return 0;
}
```

This code demonstrates how to find the LCA of two nodes (`p` and `q`) in a BST. In the example provided, the LCA of nodes 3 and 5 is node 4.

### 1. Algorithms & Data Structures (C++): Lowest Common Ancestor Binary Tree

Sure, here's an implementation of the Lowest Common Ancestor (LCA) algorithm for a binary tree in C++:

```cpp
#include <iostream>

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    // Base case: if root is null or if either p or q is found, return root
    if (root == nullptr || root == p || root == q) {
        return root;
    }

    // Search left and right subtrees for p and q
    TreeNode* leftLCA = lowestCommonAncestor(root->left, p, q);
    TreeNode* rightLCA = lowestCommonAncestor(root->right, p, q);

    // If both left and right subtrees return non-null, it means p and q are found in different subtrees,
    // hence, root is the LCA
    if (leftLCA && rightLCA) {
        return root;
    }

    // Otherwise, return the non-null result from left or right subtree
    return (leftLCA != nullptr) ? leftLCA : rightLCA;
}

int main() {
    // Construct the binary tree
    TreeNode* root = new TreeNode(3);
    root->left = new TreeNode(5);
    root->right = new TreeNode(1);
    root->left->left = new TreeNode(6);
    root->left->right = new TreeNode(2);
    root->right->left = new TreeNode(0);
    root->right->right = new TreeNode(8);
    root->left->right->left = new TreeNode(7);
    root->left->right->right = new TreeNode(4);

    // Define the nodes whose LCA needs to be found
    TreeNode* p = root->left;
    TreeNode* q = root->right;

    // Find the LCA of nodes p and q
    TreeNode* lca = lowestCommonAncestor(root, p, q);
    if (lca != nullptr) {
        std::cout << "Lowest Common Ancestor of " << p->val << " and " << q->val << " is: " << lca->val << std::endl;
    } else {
        std::cout << "Either one or both of the nodes are not present in the tree." << std::endl;
    }

    // Free memory
    delete root->left->right->right;
    delete root->left->right->left;
    delete root->right->right;
    delete root->right->left;
    delete root->left->right;
    delete root->left->left;
    delete root->right;
    delete root->left;
    delete root;

    return 0;
}
```

This implementation recursively searches for the LCA of two given nodes `p` and `q` in a binary tree. The main function constructs a sample binary tree and finds the LCA of two nodes. You can modify the binary tree structure and the nodes `p` and `q` as needed.

### 1. Algorithms & Data Structures (C++): Lowest Common Ancestor of a Binary Tree - Trees

Finding the Lowest Common Ancestor (LCA) of a Binary Tree is a fundamental problem in computer science and has various applications, especially in tree-related problems. Here's a common approach to finding the LCA of two nodes in a binary tree:

```cpp
#include <iostream>

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    // Base case: if the root is null or one of the nodes is found, return root
    if (root == nullptr || root == p || root == q) {
        return root;
    }

    // Search for LCA in left and right subtrees
    TreeNode* leftLCA = lowestCommonAncestor(root->left, p, q);
    TreeNode* rightLCA = lowestCommonAncestor(root->right, p, q);

    // If both left and right subtrees return a non-null value, then the current root is the LCA
    if (leftLCA && rightLCA) {
        return root;
    }

    // Otherwise, return whichever subtree returns a non-null value
    return leftLCA ? leftLCA : rightLCA;
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(3);
    root->left = new TreeNode(5);
    root->right = new TreeNode(1);
    root->left->left = new TreeNode(6);
    root->left->right = new TreeNode(2);
    root->right->left = new TreeNode(0);
    root->right->right = new TreeNode(8);
    root->left->right->left = new TreeNode(7);
    root->left->right->right = new TreeNode(4);

    TreeNode* p = root->left;
    TreeNode* q = root->right;
    TreeNode* lca = lowestCommonAncestor(root, p, q);
    if (lca)
        std::cout << "LCA: " << lca->val << std::endl;
    else
        std::cout << "No LCA found!" << std::endl;

    // Clean up
    delete root->left->right->right;
    delete root->left->right->left;
    delete root->right->right;
    delete root->right->left;
    delete root->left->right;
    delete root->left->left;
    delete root->right;
    delete root->left;
    delete root;

    return 0;
}
```

This algorithm has a time complexity of O(n), where n is the number of nodes in the binary tree, as each node is visited exactly once.

### 1. Algorithms & Data Structures (C++): Lowest common ancestor: Complexity analysis

The Lowest Common Ancestor (LCA) problem in a tree involves finding the lowest (i.e., deepest) node that is a common ancestor of two given nodes. In the case of a binary tree, several algorithms exist to solve this problem efficiently. One common approach is to preprocess the tree to facilitate fast LCA queries. Let's analyze the complexity of such an algorithm.

#### Preprocessing

1. **Tree Traversal:**
   - Preprocessing usually involves traversing the tree once to compute necessary information for each node, such as parent pointers, depths, or sparse tables.
   - Time Complexity: O(n), where n is the number of nodes in the tree.

2. **Sparse Table or Euler Tour:**
   - Additional structures like sparse tables or Euler tours are constructed to facilitate quick LCA queries.
   - Time Complexity: O(n log n) or O(n), depending on the method chosen.

#### LCA Query

1. **Sparse Table:**
   - After preprocessing, the LCA query operation typically requires constant time.
   - Time Complexity: O(1).

2. **Euler Tour:**
   - LCA queries using Euler tour generally involve finding the minimum element in a range or segment tree query.
   - Time Complexity: O(log n) per query, assuming segment tree implementation.

#### Overall Complexity

- Preprocessing: O(n) to O(n log n)
- Query: O(1) to O(log n)

#### Total Complexity

- For sparse table: O(n) preprocessing + O(1) query
- For Euler tour: O(n log n) preprocessing + O(log n) query

#### Space Complexity

- Preprocessing typically requires additional space to store the precomputed data structures.
- Space Complexity: O(n) to O(n log n), depending on the method used.

#### Conclusion

- The LCA problem can be efficiently solved using preprocessing techniques like sparse tables or Euler tours.
- The choice of algorithm depends on factors like the tree structure, memory constraints, and query frequency.
- Sparse tables offer constant-time queries but higher preprocessing overhead, while Euler tours provide faster preprocessing but slightly slower queries.
- The overall complexity is influenced by both preprocessing and query operations.

### 1. Algorithms & Data Structures (C++): Lowest Common Ancestors

Implementing the Lowest Common Ancestor (LCA) algorithm is crucial in tree-related problems. In a tree, the LCA of two nodes is the lowest node that has both of them as descendants. Here's a simple implementation of the LCA algorithm in C++:

```cpp
#include <iostream>
#include <vector>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (!root || root == p || root == q) return root;
        
        TreeNode* left = lowestCommonAncestor(root->left, p, q);
        TreeNode* right = lowestCommonAncestor(root->right, p, q);
        
        if (left && right) return root;
        return (left != NULL) ? left : right;
    }
};

int main() {
    // Sample tree creation
    TreeNode* root = new TreeNode(3);
    root->left = new TreeNode(5);
    root->right = new TreeNode(1);
    root->left->left = new TreeNode(6);
    root->left->right = new TreeNode(2);
    root->right->left = new TreeNode(0);
    root->right->right = new TreeNode(8);
    root->left->right->left = new TreeNode(7);
    root->left->right->right = new TreeNode(4);
    
    Solution sol;
    TreeNode* lca = sol.lowestCommonAncestor(root, root->left, root->right);
    cout << "LCA: " << lca->val << endl; // Expected output: 3
    
    return 0;
}
```

This implementation uses a recursive approach. The function `lowestCommonAncestor` takes the root of the tree and two nodes `p` and `q` as input and returns the LCA of `p` and `q`. It recursively searches for `p` and `q` in the left and right subtrees. If both `p` and `q` are found in different subtrees, then the current node is the LCA. Otherwise, it returns the non-null subtree where either `p` or `q` is found, which will further be traversed upwards to find the LCA.

### 1. Algorithms & Data Structures (C++): Max Depth of Binary Tree

To find the maximum depth of a binary tree in C++, you can use a recursive approach. Here's a simple implementation:

```cpp
#include <iostream>
#include <algorithm>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (root == nullptr) // Base case: if the root is null, return 0.
            return 0;
        else {
            // Recursively calculate the depth of the left and right subtrees
            int leftDepth = maxDepth(root->left);
            int rightDepth = maxDepth(root->right);
            
            // Return the maximum depth among left and right subtrees, plus 1 for the current node.
            return std::max(leftDepth, rightDepth) + 1;
        }
    }
};

int main() {
    // Example usage:
    TreeNode* root = new TreeNode(3);
    root->left = new TreeNode(9);
    root->right = new TreeNode(20);
    root->right->left = new TreeNode(15);
    root->right->right = new TreeNode(7);

    Solution solution;
    std::cout << "Max depth of the binary tree is: " << solution.maxDepth(root) << std::endl;

    // Clean up memory (not necessary in some environments but a good practice)
    delete root->left;
    delete root->right->left;
    delete root->right->right;
    delete root->right;
    delete root;

    return 0;
}
```

This code defines a `TreeNode` structure representing a node in the binary tree, and a `Solution` class with a method `maxDepth` to calculate the maximum depth of the binary tree. The `maxDepth` function recursively calculates the depth of the left and right subtrees and returns the maximum depth among them plus 1 for the current node.

### 1. Algorithms & Data Structures (C++): Maximum Depth Of A Binary Tree

Sure, here's how you can implement a function to find the maximum depth of a binary tree in C++ using a recursive approach:

```cpp
#include <iostream>
#include <algorithm>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

int maxDepth(TreeNode* root) {
    if (root == nullptr) // Base case: if the root is null, the depth is 0
        return 0;
    
    // Recursively find the maximum depth of the left and right subtrees
    int leftDepth = maxDepth(root->left);
    int rightDepth = maxDepth(root->right);
    
    // The depth of the current node is the maximum depth of its children plus 1
    return 1 + std::max(leftDepth, rightDepth);
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(3);
    root->left = new TreeNode(9);
    root->right = new TreeNode(20);
    root->right->left = new TreeNode(15);
    root->right->right = new TreeNode(7);

    std::cout << "Maximum depth of the binary tree is: " << maxDepth(root) << std::endl;

    // Remember to free allocated memory to avoid memory leaks
    delete root->left;
    delete root->right->left;
    delete root->right->right;
    delete root->right;
    delete root;

    return 0;
}
```

In this code:

- We define a `TreeNode` struct to represent each node in the binary tree.
- The `maxDepth` function recursively calculates the maximum depth of the binary tree. It returns 0 if the node is `nullptr` (base case). Otherwise, it recursively calculates the maximum depth of the left and right subtrees and returns the maximum of the two depths plus 1.
- In the `main` function, we create an example binary tree and call `maxDepth` to find its maximum depth. Finally, we free the allocated memory to avoid memory leaks.

### 1. Algorithms & Data Structures (C++): Maximum Depth Of A Binary Tree - Trees

Certainly! Calculating the maximum depth of a binary tree is a common problem in computer science. In C++, you can implement this using a recursive approach. Here's a basic outline:

```cpp
#include <iostream>
#include <algorithm> // for max()

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (root == nullptr) {
            return 0; // Base case: empty tree has depth 0
        }
        
        // Recursive calls to left and right subtrees
        int leftDepth = maxDepth(root->left);
        int rightDepth = maxDepth(root->right);
        
        // The depth of the tree is the maximum depth of its subtrees, plus 1 for the current node
        return std::max(leftDepth, rightDepth) + 1;
    }
};

// Utility function to create a new tree node
TreeNode* newNode(int val) {
    TreeNode* node = new TreeNode(val);
    return node;
}

int main() {
    TreeNode* root = newNode(3);
    root->left = newNode(9);
    root->right = newNode(20);
    root->right->left = newNode(15);
    root->right->right = newNode(7);

    Solution solution;
    std::cout << "Maximum depth of the binary tree is: " << solution.maxDepth(root) << std::endl;

    return 0;
}
```

This code defines a `TreeNode` struct to represent each node in the binary tree and a `Solution` class with a method `maxDepth` to find the maximum depth of the tree. The `maxDepth` function recursively calculates the depth of the left and right subtrees and returns the maximum depth among them plus one for the current node.

In the `main` function, a binary tree is created and the `maxDepth` method is called to find its maximum depth.

Remember to handle edge cases such as when the tree is empty (`root == nullptr`).

### 1. Algorithms & Data Structures (C++): Maximum Depth of Binary Tree

To find the maximum depth of a binary tree in C++, you can use a recursive approach. Here's a sample implementation:

```cpp
#include <iostream>
#include <algorithm> // for std::max

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (root == nullptr) // Base case: empty tree
            return 0;
        else {
            int leftDepth = maxDepth(root->left);
            int rightDepth = maxDepth(root->right);
            return 1 + std::max(leftDepth, rightDepth);
        }
    }
};

// Helper function to create a binary tree
TreeNode* createBinaryTree() {
    TreeNode* root = new TreeNode(3);
    root->left = new TreeNode(9);
    root->right = new TreeNode(20);
    root->right->left = new TreeNode(15);
    root->right->right = new TreeNode(7);
    return root;
}

int main() {
    Solution solution;
    TreeNode* root = createBinaryTree();
    std::cout << "Maximum depth of the binary tree: " << solution.maxDepth(root) << std::endl;
    return 0;
}
```

In this code:

- `TreeNode` represents each node in the binary tree.
- `maxDepth` function calculates the maximum depth of the binary tree recursively. It returns 0 if the current node is nullptr (indicating an empty subtree). Otherwise, it calculates the maximum depth of the left and right subtrees recursively and returns the maximum depth among them plus 1.
- `createBinaryTree` is a helper function to create a sample binary tree for testing purposes.
- In the `main` function, a binary tree is created, and the maximum depth of the tree is calculated using the `maxDepth` function and printed out.

### 1. Algorithms & Data Structures (C++): Merge Two Binary Trees

To merge two binary trees in C++, you can perform a recursive traversal of both trees and merge corresponding nodes. If a node exists in both trees, you can sum up their values and update the value of the corresponding node in one of the trees (or create a new node). If a node exists in only one tree, you can simply copy it to the merged tree. Here's a sample implementation:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    TreeNode* mergeTrees(TreeNode* t1, TreeNode* t2) {
        if (!t1) return t2;
        if (!t2) return t1;

        TreeNode* merged = new TreeNode(t1->val + t2->val);
        merged->left = mergeTrees(t1->left, t2->left);
        merged->right = mergeTrees(t1->right, t2->right);

        return merged;
    }
};

// Helper function to print binary tree (inorder traversal)
void printInorder(TreeNode* node) {
    if (node == nullptr) return;
    printInorder(node->left);
    std::cout << node->val << " ";
    printInorder(node->right);
}

int main() {
    Solution solution;

    // Example trees
    TreeNode* tree1 = new TreeNode(1);
    tree1->left = new TreeNode(3);
    tree1->left->left = new TreeNode(5);
    tree1->right = new TreeNode(2);

    TreeNode* tree2 = new TreeNode(2);
    tree2->left = new TreeNode(1);
    tree2->left->right = new TreeNode(4);
    tree2->right = new TreeNode(3);
    tree2->right->right = new TreeNode(7);

    // Merge trees
    TreeNode* mergedTree = solution.mergeTrees(tree1, tree2);

    // Print the merged tree (inorder traversal)
    std::cout << "Inorder traversal of merged tree: ";
    printInorder(mergedTree);

    return 0;
}
```

This code defines a `TreeNode` structure representing a node in the binary tree and a `Solution` class with a method `mergeTrees` which merges two binary trees recursively. In the `main()` function, it demonstrates how to use this method with two example trees and prints the inorder traversal of the merged tree.

### 1. Algorithms & Data Structures (C++): Minimum Depth of Binary Tree

To find the minimum depth of a binary tree in C++, you can use depth-first search (DFS) or breadth-first search (BFS) algorithms. Here's a simple implementation using BFS:

```cpp
#include <iostream>
#include <queue>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

int minDepth(TreeNode* root) {
    if (!root) return 0;

    queue<pair<TreeNode*, int>> q;
    q.push({root, 1});

    while (!q.empty()) {
        TreeNode* node = q.front().first;
        int depth = q.front().second;
        q.pop();

        if (!node->left && !node->right) { // If it's a leaf node
            return depth;
        }

        if (node->left) {
            q.push({node->left, depth + 1});
        }

        if (node->right) {
            q.push({node->right, depth + 1});
        }
    }

    return -1; // This line should not be reached if the tree is well-formed
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(3);
    root->left = new TreeNode(9);
    root->right = new TreeNode(20);
    root->right->left = new TreeNode(15);
    root->right->right = new TreeNode(7);

    cout << "Minimum depth of the binary tree: " << minDepth(root) << endl;

    // Don't forget to free the allocated memory
    delete root->left;
    delete root->right->left;
    delete root->right->right;
    delete root->right;
    delete root;

    return 0;
}
```

This code calculates the minimum depth of a binary tree using BFS. It starts from the root and traverses the tree level by level until it finds a leaf node. The depth is incremented as we go deeper into the tree. Once a leaf node is found, the depth at that point is returned as the minimum depth of the binary tree.

You can adjust the `TreeNode` struct and the example tree in the `main` function according to your requirements.

### 1. Algorithms & Data Structures (C++): Node structure for a Binary Tree

Sure, here's a simple C++ structure for a node in a binary tree:

```cpp
template<typename T>
struct TreeNode {
    T data;
    TreeNode<T>* left;
    TreeNode<T>* right;

    TreeNode(const T& value) : data(value), left(nullptr), right(nullptr) {}
};
```

In this structure:

- `data` represents the value stored in the node.
- `left` points to the left child of the node.
- `right` points to the right child of the node.

You can use this structure to build a binary tree in C++, where each node contains some data and pointers to its left and right children.

### 1. Algorithms & Data Structures (C++): Nodes at Distance K

To find all the nodes at a distance K from a given target node in a binary tree, you can perform a depth-first search (DFS) starting from the target node. While traversing, keep track of the distance of each node from the target node. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>

using namespace std;

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void dfs(TreeNode* node, int distance, unordered_map<TreeNode*, int>& distances) {
    if (node == nullptr) return;
    
    distances[node] = distance;
    
    dfs(node->left, distance + 1, distances);
    dfs(node->right, distance + 1, distances);
}

void findNodesAtDistanceK(TreeNode* root, TreeNode* target, int k, vector<int>& result, unordered_map<TreeNode*, int>& distances) {
    if (root == nullptr) return;
    
    if (distances.find(root) != distances.end())
        k = distances[root];
    
    if (k == 0) {
        result.push_back(root->val);
        return;
    }
    
    findNodesAtDistanceK(root->left, target, k - 1, result, distances);
    findNodesAtDistanceK(root->right, target, k - 1, result, distances);
}

vector<int> distanceK(TreeNode* root, TreeNode* target, int k) {
    unordered_map<TreeNode*, int> distances;
    dfs(target, 0, distances);
    
    vector<int> result;
    findNodesAtDistanceK(root, target, k, result, distances);
    
    return result;
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(3);
    root->left = new TreeNode(5);
    root->right = new TreeNode(1);
    root->left->left = new TreeNode(6);
    root->left->right = new TreeNode(2);
    root->right->left = new TreeNode(0);
    root->right->right = new TreeNode(8);
    root->left->right->left = new TreeNode(7);
    root->left->right->right = new TreeNode(4);

    TreeNode* target = root->left;
    int k = 2;

    vector<int> nodesAtDistanceK = distanceK(root, target, k);

    cout << "Nodes at distance " << k << " from target " << target->val << ": ";
    for (int nodeVal : nodesAtDistanceK) {
        cout << nodeVal << " ";
    }
    cout << endl;

    return 0;
}
```

This code first performs a DFS starting from the target node to calculate the distance of each node from the target. Then, it recursively finds the nodes at distance K from the target node by traversing the tree. Finally, it prints the nodes found at distance K from the target.

### 1. Algorithms & Data Structures (C++): Number of Binary Trees using N Nodes

Calculating the number of binary trees with N nodes is a classic problem in computer science. One way to approach this problem is by using dynamic programming.

Here's a C++ implementation to calculate the number of binary trees with N nodes:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to calculate the number of binary trees with n nodes
int numberOfBinaryTrees(int n) {
    // Create a vector to store the number of binary trees for each number of nodes
    vector<int> dp(n + 1, 0);

    // Base cases
    dp[0] = 1; // Empty tree is also a binary tree
    dp[1] = 1;

    // Fill the dp array bottom-up
    for (int i = 2; i <= n; ++i) {
        for (int j = 0; j < i; ++j) {
            dp[i] += dp[j] * dp[i - j - 1];
        }
    }

    return dp[n];
}

int main() {
    int n;
    cout << "Enter the number of nodes: ";
    cin >> n;
    cout << "Number of binary trees with " << n << " nodes: " << numberOfBinaryTrees(n) << endl;
    return 0;
}
```

This code defines a function `numberOfBinaryTrees` that takes an integer `n` as input and returns the number of binary trees with `n` nodes. It uses dynamic programming to build up the solution from smaller subproblems. The main function prompts the user to enter the number of nodes and then prints the result.

### 1. Algorithms & Data Structures (C++): Number Of Binary Trees with 'n' - Nodes

To find the number of binary trees with 'n' nodes, you can use dynamic programming. The problem can be solved using the concept of Catalan numbers. The formula for the nth Catalan number is given by:

\[ C(n) = \frac{{(2n)!}}{{(n + 1)! \cdot n!}} \]

Here's how you can implement this in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to calculate the binomial coefficient C(n, k)
unsigned long long binomialCoefficient(int n, int k) {
    if (k > n - k)
        k = n - k;

    unsigned long long res = 1;

    for (int i = 0; i < k; ++i) {
        res *= (n - i);
        res /= (i + 1);
    }

    return res;
}

// Function to calculate the number of binary trees with 'n' nodes
unsigned long long numberOfBinaryTrees(int n) {
    // Calculate the nth Catalan number
    unsigned long long catalan = binomialCoefficient(2 * n, n) / (n + 1);

    return catalan;
}

int main() {
    int n;
    cout << "Enter the number of nodes: ";
    cin >> n;
    
    unsigned long long numTrees = numberOfBinaryTrees(n);
    cout << "Number of binary trees with " << n << " nodes: " << numTrees << endl;

    return 0;
}
```

This code calculates the number of binary trees with 'n' nodes using the Catalan number formula and the binomial coefficient function to efficiently compute factorials.

### 1. Algorithms & Data Structures (C++): Number of Nodes in Binary Trees

To count the number of nodes in a binary tree, you can use a simple recursive algorithm. In C++, you can define a structure for the binary tree node and then implement a function to count the nodes recursively. Here's how you can do it:

```cpp
#include <iostream>

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

int countNodes(TreeNode* root) {
    if (root == nullptr)
        return 0;
    return 1 + countNodes(root->left) + countNodes(root->right);
}

int main() {
    // Example of creating a binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    
    // Counting nodes
    int nodeCount = countNodes(root);
    std::cout << "Number of nodes in the binary tree: " << nodeCount << std::endl;
    
    // Remember to free allocated memory
    delete root->left->left;
    delete root->left->right;
    delete root->left;
    delete root->right;
    delete root;
    
    return 0;
}
```

This code creates a binary tree with some example nodes and then counts the total number of nodes using the `countNodes` function. The function recursively traverses the tree and adds up the count of nodes in the left subtree, the count of nodes in the right subtree, and adds one for the root node.

### 1. Algorithms & Data Structures (C++): Print At Depth K

To print all the nodes at a given depth 'k' in a binary tree, you can use a simple recursive algorithm. Here's a basic implementation in C++:

```cpp
#include <iostream>
using namespace std;

// Definition of a binary tree node
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to print nodes at a given depth 'k'
void printAtDepthK(TreeNode* root, int k) {
    if (root == nullptr) // Base case: if the tree is empty
        return;
    if (k == 0) // Base case: if current node is at depth 'k'
        cout << root->val << " ";
    else { // Recursive case: explore left and right subtrees
        printAtDepthK(root->left, k - 1); // Recursive call for the left subtree
        printAtDepthK(root->right, k - 1); // Recursive call for the right subtree
    }
}

int main() {
    // Example binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(7);

    int k = 2; // Depth at which nodes are to be printed
    cout << "Nodes at depth " << k << ": ";
    printAtDepthK(root, k);
    cout << endl;

    return 0;
}
```

This code defines a basic binary tree node structure and a function `printAtDepthK()` which prints all nodes at a given depth 'k'. In the `main()` function, a binary tree is created as an example, and nodes at depth 'k' are printed.

Make sure you have a basic understanding of binary trees and recursion to grasp this code effectively.

### 1. Algorithms & Data Structures (C++): Print At LevelK

Printing nodes at a particular level \( k \) in a binary tree can be achieved through a simple depth-first search (DFS) algorithm with a slight modification. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <queue>
using namespace std;

// Structure for a node in the binary tree
struct Node {
    int data;
    Node* left;
    Node* right;

    Node(int value) {
        data = value;
        left = nullptr;
        right = nullptr;
    }
};

// Function to print nodes at a particular level k
void printAtLevelK(Node* root, int k) {
    if (root == nullptr)
        return;
    
    if (k == 0)
        cout << root->data << " ";
    else {
        printAtLevelK(root->left, k - 1);
        printAtLevelK(root->right, k - 1);
    }
}

int main() {
    // Creating a sample binary tree
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    root->right->left = new Node(6);
    root->right->right = new Node(7);

    int level = 2; // Level at which nodes are to be printed
    cout << "Nodes at level " << level << ": ";
    printAtLevelK(root, level);
    cout << endl;

    return 0;
}
```

In this code:

- `Node` is a simple structure representing a node in the binary tree.
- `printAtLevelK` is a recursive function that prints the nodes at level \( k \). It traverses the tree recursively, decrementing the level by 1 until it reaches the desired level. At level 0, it prints the data of the node.
- In the `main()` function, a sample binary tree is created, and then `printAtLevelK` is called with the root of the tree and the desired level to print.

### 1. Algorithms & Data Structures (C++): Print LevelWise

Printing a binary tree level-wise in C++ involves a breadth-first traversal of the tree, commonly implemented using a queue data structure. Here's a simple implementation:

```cpp
#include <iostream>
#include <queue>
using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

void printLevelWise(TreeNode* root) {
    if (root == NULL) return;

    queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        int levelSize = q.size(); // Number of nodes at current level

        for (int i = 0; i < levelSize; i++) {
            TreeNode* node = q.front();
            q.pop();
            cout << node->val << " ";

            // Enqueue left child
            if (node->left != NULL)
                q.push(node->left);

            // Enqueue right child
            if (node->right != NULL)
                q.push(node->right);
        }
        cout << endl; // Move to next level
    }
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(7);

    cout << "Level-wise traversal:\n";
    printLevelWise(root);

    return 0;
}
```

This code first creates a binary tree and then performs a level-wise traversal using a queue. It prints the elements of each level on a separate line.

### 1. Algorithms & Data Structures (C++): Program for Generating Binary Search Trees from Preorder

Certainly! Here's a C++ program to generate a Binary Search Tree (BST) from its preorder traversal:

```cpp
#include <iostream>
#include <vector>
using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to construct BST from its preorder traversal
TreeNode* bstFromPreorder(vector<int>& preorder, int& idx, int limit) {
    // Base case: If we reach the end of the vector or current element exceeds limit
    if (idx == preorder.size() || preorder[idx] > limit) {
        return nullptr;
    }
    
    // Create new node with current value
    TreeNode* root = new TreeNode(preorder[idx++]);
    
    // Recursively construct left and right subtrees
    root->left = bstFromPreorder(preorder, idx, root->val);
    root->right = bstFromPreorder(preorder, idx, limit);
    
    return root;
}

// Function to print inorder traversal of BST
void inorderTraversal(TreeNode* root) {
    if (root == nullptr) return;
    inorderTraversal(root->left);
    cout << root->val << " ";
    inorderTraversal(root->right);
}

int main() {
    // Example usage
    vector<int> preorder = {8, 5, 1, 7, 10, 12};
    int idx = 0; // starting index of preorder traversal
    
    TreeNode* root = bstFromPreorder(preorder, idx, INT_MAX);
    
    // Print inorder traversal of constructed BST
    inorderTraversal(root);
    
    return 0;
}
```

This program defines a `TreeNode` struct representing a node in the binary tree. The `bstFromPreorder` function recursively constructs the binary search tree from the preorder traversal vector. The `inorderTraversal` function is used to print the inorder traversal of the constructed BST. In the `main` function, an example preorder traversal vector is provided, and the BST is constructed and printed.

### 1. Algorithms & Data Structures (C++): Proper Binary Tree

Creating a proper binary tree in C++ involves defining a structure for the tree nodes and implementing various operations like insertion, deletion, traversal, etc. Here's a basic example of how you can define a proper binary tree and perform some common operations:

```cpp
#include <iostream>
using namespace std;

// Definition of a node in the binary tree
struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Function to insert a node into the binary tree
void insert(TreeNode* &root, int val) {
    if (root == nullptr) {
        root = new TreeNode(val);
        return;
    }
    if (val < root->data) {
        insert(root->left, val);
    } else {
        insert(root->right, val);
    }
}

// Function to perform inorder traversal of the binary tree
void inorder(TreeNode* root) {
    if (root == nullptr) return;
    inorder(root->left);
    cout << root->data << " ";
    inorder(root->right);
}

// Function to perform preorder traversal of the binary tree
void preorder(TreeNode* root) {
    if (root == nullptr) return;
    cout << root->data << " ";
    preorder(root->left);
    preorder(root->right);
}

// Function to perform postorder traversal of the binary tree
void postorder(TreeNode* root) {
    if (root == nullptr) return;
    postorder(root->left);
    postorder(root->right);
    cout << root->data << " ";
}

int main() {
    TreeNode* root = nullptr;
    insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    insert(root, 60);
    insert(root, 80);

    cout << "Inorder traversal: ";
    inorder(root);
    cout << endl;

    cout << "Preorder traversal: ";
    preorder(root);
    cout << endl;

    cout << "Postorder traversal: ";
    postorder(root);
    cout << endl;

    return 0;
}
```

This code defines a basic binary tree structure (`TreeNode`), along with functions to insert nodes into the tree and perform inorder, preorder, and postorder traversals. You can use this code as a starting point and extend it with additional functionalities as needed.

### 1. Algorithms & Data Structures (C++): Properties of Binary Trees

Binary trees are fundamental data structures in computer science, consisting of nodes where each node has at most two children, referred to as the left child and the right child. Here are some key properties of binary trees:

1. **Root**: The topmost node in a binary tree is called the root. It is the starting point for accessing the tree.

2. **Nodes**: Each element in a binary tree is called a node. Each node contains a value and references (pointers or links) to its left and right children.

3. **Parent, Child, Siblings**: A node in a binary tree has a parent node and can have at most two children nodes, referred to as the left child and the right child. Nodes with the same parent are called siblings.

4. **Leaf Nodes**: Nodes that do not have any children are called leaf nodes or terminal nodes. They are at the bottom level of the tree.

5. **Height**: The height of a binary tree is the length of the longest path from the root node to a leaf node. It represents the maximum number of edges in any path from the root node to a leaf node. The height of an empty tree is usually defined as -1, and the height of a tree with only one node (the root) is defined as 0.

6. **Depth**: The depth of a node is the length of the path from the root node to that node. The root node has a depth of 0.

7. **Binary Tree Traversal**: There are several ways to traverse a binary tree:
   - Inorder Traversal: Traverse the left subtree, visit the root, and traverse the right subtree.
   - Preorder Traversal: Visit the root, traverse the left subtree, and traverse the right subtree.
   - Postorder Traversal: Traverse the left subtree, traverse the right subtree, and visit the root.

8. **Balanced vs. Unbalanced Binary Trees**:
   - Balanced Binary Trees: A binary tree is considered balanced if the height of its left and right subtrees differ by at most one for every node in the tree. Examples of balanced binary trees include AVL trees and Red-Black trees.
   - Unbalanced Binary Trees: A binary tree is unbalanced if the height difference between its left and right subtrees is significant, leading to inefficient operations such as searching, insertion, and deletion.

9. **Complete Binary Trees**: A binary tree is complete if all levels are completely filled except possibly for the last level, which is filled from left to right. Complete binary trees are used in heap data structures.

10. **Full Binary Trees**: A binary tree is full if every node has either zero or two children, but not one. In other words, every node is either a leaf node or has two children.

11. **Perfect Binary Trees**: A perfect binary tree is both full and complete, meaning all internal nodes have exactly two children and all leaf nodes are at the same level.

Understanding these properties is essential for designing, analyzing, and implementing algorithms that operate on binary trees efficiently.

### 1. Algorithms & Data Structures (C++): Replace with Descendant Sum

To replace a node in a binary tree with the sum of its descendants in C++, you need to traverse the tree in a way that allows you to compute the sum of descendants for each node. One common approach is to use recursion. Here's how you can implement this:

```cpp
#include <iostream>
#include <unordered_map>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to replace each node's value with the sum of its descendants
void replaceWithDescendantSum(TreeNode* root, unordered_map<TreeNode*, int>& descendantSum) {
    if (root == nullptr)
        return;

    // Traverse the tree in postorder fashion
    replaceWithDescendantSum(root->left, descendantSum);
    replaceWithDescendantSum(root->right, descendantSum);

    // Calculate the sum of left and right descendants
    int leftSum = (root->left) ? descendantSum[root->left] : 0;
    int rightSum = (root->right) ? descendantSum[root->right] : 0;

    // Update the value of the current node with the sum of its descendants
    descendantSum[root] = root->val + leftSum + rightSum;
    root->val = leftSum + rightSum;
}

// Helper function to print the tree (for testing)
void printTree(TreeNode* root) {
    if (root == nullptr)
        return;

    printTree(root->left);
    cout << root->val << " ";
    printTree(root->right);
}

int main() {
    // Example tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(7);

    unordered_map<TreeNode*, int> descendantSum;

    // Replace each node's value with the sum of its descendants
    replaceWithDescendantSum(root, descendantSum);

    // Print the modified tree
    printTree(root);

    // Clean up
    delete root->right->right;
    delete root->right->left;
    delete root->left->right;
    delete root->left->left;
    delete root->right;
    delete root->left;
    delete root;

    return 0;
}
```

This code defines a `TreeNode` struct representing a node in the binary tree. The `replaceWithDescendantSum` function recursively computes the sum of descendants for each node and replaces its value. Finally, the `main` function demonstrates the usage of this function with an example binary tree.

### 1. Algorithms & Data Structures (C++): Representation of Almost Complete Binary Tree Using 1-D Array

Representing an almost complete binary tree using a 1-D array is a common technique used in computer science to efficiently store and manipulate binary trees. An almost complete binary tree is a binary tree in which every level, except possibly the last, is completely filled, and all nodes are as far left as possible.

Here's how you can represent an almost complete binary tree using a 1-D array:

1. **Indexing**: In a binary tree represented by a 1-D array, each node at index `i` has its left child at index `2*i + 1` and its right child at index `2*i + 2`.

2. **Array Initialization**: To initialize an array for an almost complete binary tree, you need to allocate enough space to hold all the nodes of the tree. You can calculate the required size based on the number of nodes in the tree.

3. **Storing Nodes**: Store the nodes of the binary tree in the array based on the indexing rules mentioned above. Start storing nodes from index 0, then move on to index 1, 2, 3, and so on, level by level.

Here's a basic implementation in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Structure for a node in the binary tree
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to represent an almost complete binary tree using a 1-D array
vector<int> treeToVector(TreeNode* root) {
    vector<int> result;
    if (root == nullptr)
        return result;

    vector<TreeNode*> queue;
    queue.push_back(root);

    while (!queue.empty()) {
        TreeNode* current = queue.front();
        queue.erase(queue.begin()); // Remove the front element
        if (current != nullptr) {
            result.push_back(current->val);
            queue.push_back(current->left);
            queue.push_back(current->right);
        } else {
            result.push_back(-1); // Represent null node with a special value, like -1
        }
    }
    return result;
}

int main() {
    // Example of an almost complete binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->left = new TreeNode(6);

    vector<int> treeArray = treeToVector(root);

    cout << "1-D Array Representation of the Almost Complete Binary Tree:" << endl;
    for (int val : treeArray) {
        cout << val << " ";
    }
    cout << endl;

    return 0;
}
```

This code converts the binary tree into a 1-D array representation and then prints it out. You may adjust it according to your requirements, such as handling null nodes differently or using a different way to represent them.

### 1. Algorithms & Data Structures (C++): Representation of Binary Tree

Representing a binary tree in C++ involves creating a data structure that can hold the nodes of the tree and their relationships. One common way to represent a binary tree is to use a struct to define the nodes and pointers to represent the relationships between nodes. Here's a simple example:

```cpp
#include <iostream>

// Define the structure for a node in the binary tree
struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;

    // Constructor to initialize the node with data
    TreeNode(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Function to create a new node
TreeNode* createNode(int data) {
    return new TreeNode(data);
}

int main() {
    // Creating a binary tree
    TreeNode* root = createNode(1);
    root->left = createNode(2);
    root->right = createNode(3);
    root->left->left = createNode(4);
    root->left->right = createNode(5);

    // Traversing the binary tree (just an example)
    std::cout << "Inorder traversal of binary tree: ";
    inorderTraversal(root);
    std::cout << std::endl;

    return 0;
}
```

In this representation:

- The `TreeNode` struct represents each node in the binary tree. It contains an integer data value and pointers to the left and right children.
- The `createNode` function creates a new node with the given data value and returns a pointer to it.
- In the `main` function, we create a binary tree with some sample data. You can modify this part to construct the tree as per your requirement.
- This example doesn't include a traversal function (`inorderTraversal` is used but not defined here). You can implement various tree traversal algorithms like inorder, preorder, postorder, etc., based on your requirements.

This is a basic representation. Depending on your specific use case, you might need to include additional features or functionalities in the node structure or elsewhere in your code.

### 1. Algorithms & Data Structures (C++): Reverse binary tree

Reversing a binary tree in C++ is a classic problem often tackled using recursion. Here's a simple implementation:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if (root == nullptr) return nullptr;

        // Swap the left and right subtrees
        TreeNode* temp = root->left;
        root->left = invertTree(root->right);
        root->right = invertTree(temp);

        return root;
    }
};

// Function to print the inorder traversal of the tree (for verification)
void printInorder(TreeNode* root) {
    if (root == nullptr) return;
    printInorder(root->left);
    std::cout << root->val << " ";
    printInorder(root->right);
}

int main() {
    // Example tree
    TreeNode* root = new TreeNode(4);
    root->left = new TreeNode(2);
    root->right = new TreeNode(7);
    root->left->left = new TreeNode(1);
    root->left->right = new TreeNode(3);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(9);

    // Create a solution object
    Solution solution;

    // Invert the tree
    TreeNode* invertedRoot = solution.invertTree(root);

    // Print the inorder traversal of the inverted tree
    std::cout << "Inorder traversal of the inverted tree: ";
    printInorder(invertedRoot);
    std::cout << std::endl;

    // Clean up memory
    // (In a real application, you would usually use smart pointers to manage memory automatically)
    delete invertedRoot->left->left;
    delete invertedRoot->left->right;
    delete invertedRoot->left;
    delete invertedRoot->right->left;
    delete invertedRoot->right->right;
    delete invertedRoot->right;
    delete invertedRoot;

    return 0;
}
```

This program demonstrates the reversal of a binary tree using recursion. The `invertTree` function takes the root of the tree as input and recursively inverts its left and right subtrees, swapping them at each node. Finally, it returns the root of the inverted tree. The `printInorder` function is used to verify the inversion by printing the inorder traversal of the inverted tree.

### 1. Algorithms & Data Structures (C++): Reverse binary tree: Complexity analysis

When analyzing the complexity of reversing a binary tree, we need to consider both time complexity and space complexity.

1. **Time Complexity**:

   Reversing a binary tree typically involves traversing each node once and swapping its left and right child pointers. There are several common traversal methods for binary trees, such as in-order, pre-order, and post-order traversal. Each of these traversal methods has a time complexity of O(n), where n is the number of nodes in the tree.

   Additionally, the swapping operation is constant time (O(1)).

   So, the overall time complexity for reversing a binary tree is O(n), where n is the number of nodes in the tree.

2. **Space Complexity**:

   The space complexity is determined by the stack space used during recursion if we use recursive traversal algorithms like pre-order, in-order, or post-order traversal. In the worst case, the space complexity for recursion is O(h), where h is the height of the binary tree. This is because the recursion depth could be as much as the height of the tree.

   If we use an iterative approach, such as level-order traversal using a queue, the space complexity would be O(w), where w is the maximum width of the tree (the maximum number of nodes at any level of the tree). In the worst case, this could be O(n), where n is the number of nodes in the tree if the tree is completely unbalanced.

So, to summarize:

- **Time Complexity**: O(n)
- **Space Complexity**:
  - If using recursion: O(h)
  - If using an iterative approach: O(w) or O(n)

### 1. Algorithms & Data Structures (C++): Reverse for Doubly Linked List

Certainly! Below is a C++ implementation to reverse a doubly linked list:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* prev;
    Node* next;
};

class DoublyLinkedList {
private:
    Node* head;
    Node* tail;

public:
    DoublyLinkedList() : head(nullptr), tail(nullptr) {}

    // Function to add a node at the end of the list
    void append(int data) {
        Node* newNode = new Node();
        newNode->data = data;
        newNode->prev = nullptr;
        newNode->next = nullptr;

        if (head == nullptr) {
            head = tail = newNode;
        } else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
    }

    // Function to reverse the doubly linked list
    void reverse() {
        Node* current = head;
        Node* temp = nullptr;

        while (current != nullptr) {
            // Swapping next and prev pointers of the current node
            temp = current->prev;
            current->prev = current->next;
            current->next = temp;

            // Moving to the next node
            current = current->prev;
        }

        // If the list is not empty, head should point to the last node
        if (temp != nullptr) {
            head = temp->prev;
        }
    }

    // Function to display the reversed list
    void display() {
        Node* current = head;
        while (current != nullptr) {
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }
};

int main() {
    DoublyLinkedList dll;
    dll.append(1);
    dll.append(2);
    dll.append(3);
    dll.append(4);
    dll.append(5);

    std::cout << "Original list: ";
    dll.display();

    dll.reverse();

    std::cout << "Reversed list: ";
    dll.display();

    return 0;
}
```

This code defines a `DoublyLinkedList` class with methods to append nodes, reverse the list, and display the list. In the `reverse` function, the list is reversed by swapping the `prev` and `next` pointers of each node.

### 1. Algorithms & Data Structures (C++): Searching for a node in Binary Tree

In C++, you can implement a binary tree and then perform a search for a specific node within it. Here's a basic implementation of a binary tree and a function to search for a node with a given value:

```cpp
#include <iostream>

// Node structure for the binary tree
struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;

    TreeNode(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Function to search for a node with a given value in the binary tree
TreeNode* searchNode(TreeNode* root, int val) {
    // Base cases: root is null or root has the target value
    if (root == nullptr || root->data == val) {
        return root;
    }

    // If the target value is less than the root's value, search in the left subtree
    if (val < root->data) {
        return searchNode(root->left, val);
    }
    // If the target value is greater than the root's value, search in the right subtree
    else {
        return searchNode(root->right, val);
    }
}

// Utility function to create a new binary tree node
TreeNode* createNode(int val) {
    return new TreeNode(val);
}

// Utility function to deallocate memory of the binary tree
void deleteTree(TreeNode* root) {
    if (root != nullptr) {
        deleteTree(root->left);
        deleteTree(root->right);
        delete root;
    }
}

int main() {
    // Creating a sample binary tree
    TreeNode* root = createNode(10);
    root->left = createNode(5);
    root->right = createNode(15);
    root->left->left = createNode(3);
    root->left->right = createNode(7);
    root->right->left = createNode(12);
    root->right->right = createNode(18);

    // Search for a node with value 7
    int targetValue = 7;
    TreeNode* result = searchNode(root, targetValue);

    if (result != nullptr) {
        std::cout << "Node with value " << targetValue << " found in the binary tree." << std::endl;
    } else {
        std::cout << "Node with value " << targetValue << " not found in the binary tree." << std::endl;
    }

    // Deallocate memory
    deleteTree(root);

    return 0;
}
```

This code defines a `TreeNode` struct representing each node in the binary tree. The `searchNode` function performs a recursive search starting from the root of the tree. Finally, in the `main` function, a sample binary tree is created, and then a search for a specific node value is performed.

### 1. Algorithms & Data Structures (C++): Strict Binary Tree

A strict binary tree, also known as a full binary tree, is a type of binary tree where each node in the tree has either 0 or 2 children. In other words, there are no nodes with only one child. Here's an implementation of a strict binary tree in C++:

```cpp
#include <iostream>
using namespace std;

// Define the structure for a tree node
struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;

    TreeNode(int value) : data(value), left(nullptr), right(nullptr) {}
};

// Function to insert a node into the tree
void insert(TreeNode* &root, int value) {
    if (root == nullptr) {
        root = new TreeNode(value);
    } else {
        if (value < root->data) {
            insert(root->left, value);
        } else {
            insert(root->right, value);
        }
    }
}

// Function to check if a binary tree is strict
bool isStrictBinaryTree(TreeNode* root) {
    if (root == nullptr)
        return true;
    
    // If a node has only one child, it's not a strict binary tree
    if ((root->left == nullptr && root->right != nullptr) || (root->left != nullptr && root->right == nullptr))
        return false;
    
    // Recursively check the left and right subtrees
    return isStrictBinaryTree(root->left) && isStrictBinaryTree(root->right);
}

int main() {
    TreeNode* root = nullptr;

    // Insert nodes into the tree
    insert(root, 5);
    insert(root, 3);
    insert(root, 7);
    insert(root, 2);
    insert(root, 4);
    insert(root, 6);
    insert(root, 8);

    // Check if the tree is a strict binary tree
    if (isStrictBinaryTree(root))
        cout << "The tree is a strict binary tree." << endl;
    else
        cout << "The tree is not a strict binary tree." << endl;

    return 0;
}
```

In this implementation, the `TreeNode` struct represents each node in the tree, containing an integer data value and pointers to the left and right children. The `insert` function is used to insert nodes into the tree. The `isStrictBinaryTree` function recursively checks if the given tree is a strict binary tree by ensuring that each node either has no children or has both left and right children. Finally, in the `main` function, we create a sample binary tree and check if it is a strict binary tree using the `isStrictBinaryTree` function.

### 1. Algorithms & Data Structures (C++): Strict vs Complete Binary Tree

A strict binary tree, also known as a full binary tree, is a tree in which each node has either 0 or 2 children. This means that every internal node has exactly two children, and every leaf node is at the same level. In a strict binary tree, the number of nodes doubles at each level as you move down the tree.

On the other hand, a complete binary tree is a binary tree in which every level, except possibly the last, is completely filled, and all nodes are as far left as possible. In a complete binary tree, the last level might not be completely filled, but all nodes are as left as possible.

Here's a comparison between the two:

1. **Node Structure**: In a strict binary tree, every node has either 0 or 2 children. In a complete binary tree, every node except possibly the last level's nodes has exactly 2 children, and the last level's nodes are filled from left to right.

2. **Shape**: The shape of a strict binary tree is such that each node has two children unless it's a leaf. The shape of a complete binary tree can vary, but it must be filled from left to right on every level except possibly the last.

3. **Height**: The height of both trees can vary, but the number of levels in a complete binary tree is typically fewer than or equal to that of a strict binary tree since a complete binary tree doesn't have any "gaps" in the levels.

4. **Application**: Strict binary trees are often used in various tree-based algorithms and data structures where having exactly two children for every node is essential. Complete binary trees are commonly used in heap data structures, where they ensure efficient access and insertion.

In terms of implementation, both types of trees can be represented using various data structures such as arrays or linked structures, depending on the specific requirements and use cases.

### 1. Algorithms & Data Structures (C++): Sum of left leaves

Certainly! The problem you're referring to, finding the sum of left leaves in a binary tree, is a classic one. Here's a C++ implementation using a recursive approach:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

int sumOfLeftLeaves(TreeNode* root) {
    if (!root) return 0;

    int sum = 0;

    // Check if the left child is a leaf node
    if (root->left && !root->left->left && !root->left->right) {
        sum += root->left->val;
    }

    // Recursively traverse both left and right subtrees
    sum += sumOfLeftLeaves(root->left);
    sum += sumOfLeftLeaves(root->right);

    return sum;
}

// Test the function
int main() {
    TreeNode* root = new TreeNode(3);
    root->left = new TreeNode(9);
    root->right = new TreeNode(20);
    root->right->left = new TreeNode(15);
    root->right->right = new TreeNode(7);

    std::cout << "Sum of left leaves: " << sumOfLeftLeaves(root) << std::endl;

    // Clean up memory
    delete root->left;
    delete root->right->left;
    delete root->right->right;
    delete root->right;
    delete root;

    return 0;
}
```

This code defines a `TreeNode` struct representing a node in the binary tree and implements the `sumOfLeftLeaves` function to compute the sum of left leaves. The function works recursively, traversing the tree and adding the values of left leaves to the `sum`. Finally, the `main` function demonstrates how to use this function with a sample binary tree.

### 1. Algorithms & Data Structures (C++): Symmetric Binary Tree

A symmetric binary tree, also known as a mirror image binary tree, is a tree data structure where the left subtree of each node is a mirror reflection of the right subtree. In other words, if you were to draw a vertical line through the root node of the tree, the structure to the left and right of the line would be identical.

Here's an approach to determine if a binary tree is symmetric in C++:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

// Helper function to check if two subtrees are mirrors of each other
bool isMirror(TreeNode* leftSubtree, TreeNode* rightSubtree) {
    // If both nodes are NULL, they are mirrors
    if (leftSubtree == NULL && rightSubtree == NULL)
        return true;
    // If one of the nodes is NULL and the other is not, they are not mirrors
    if (leftSubtree == NULL || rightSubtree == NULL)
        return false;
    // Check if the values are equal and their children are mirrors
    return (leftSubtree->val == rightSubtree->val) && 
           isMirror(leftSubtree->left, rightSubtree->right) &&
           isMirror(leftSubtree->right, rightSubtree->left);
}

// Main function to check if a binary tree is symmetric
bool isSymmetric(TreeNode* root) {
    // If the tree is empty, it is symmetric
    if (root == NULL)
        return true;
    // Check if the left and right subtrees are mirrors
    return isMirror(root->left, root->right);
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(2);
    root->left->left = new TreeNode(3);
    root->left->right = new TreeNode(4);
    root->right->left = new TreeNode(4);
    root->right->right = new TreeNode(3);

    if (isSymmetric(root))
        std::cout << "The tree is symmetric." << std::endl;
    else
        std::cout << "The tree is not symmetric." << std::endl;

    // Deallocate memory
    delete root->left->left;
    delete root->left->right;
    delete root->right->left;
    delete root->right->right;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

This code defines a `TreeNode` struct representing a node in the binary tree and provides a function `isSymmetric` to check whether the given binary tree is symmetric or not. The `isMirror` function checks if two given subtrees are mirrors of each other by recursively comparing their values and children.

### 1. Algorithms & Data Structures (C++): Taking Input LevelWise in Binary Tree

To take input level-wise in a binary tree using C++, you can use a queue data structure to keep track of the nodes at each level. Here's a basic implementation:

```cpp
#include <iostream>
#include <queue>

using namespace std;

// Define the structure for a binary tree node
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;

    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to create a binary tree level-wise
TreeNode* createLevelWise() {
    int val;
    cout << "Enter root value: ";
    cin >> val;

    if (val == -1) // Assume -1 as null marker
        return nullptr;

    TreeNode* root = new TreeNode(val);
    queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        TreeNode* curr = q.front();
        q.pop();

        int leftVal, rightVal;
        cout << "Enter left child value of " << curr->val << " (-1 if no left child): ";
        cin >> leftVal;
        if (leftVal != -1) {
            curr->left = new TreeNode(leftVal);
            q.push(curr->left);
        }

        cout << "Enter right child value of " << curr->val << " (-1 if no right child): ";
        cin >> rightVal;
        if (rightVal != -1) {
            curr->right = new TreeNode(rightVal);
            q.push(curr->right);
        }
    }

    return root;
}

// Function to traverse and print the binary tree in inorder
void inorder(TreeNode* root) {
    if (root) {
        inorder(root->left);
        cout << root->val << " ";
        inorder(root->right);
    }
}

int main() {
    TreeNode* root = createLevelWise();
    cout << "Inorder traversal of the binary tree: ";
    inorder(root);
    cout << endl;

    return 0;
}
```

In this code:

1. We define a `TreeNode` struct to represent each node of the binary tree.
2. The `createLevelWise` function takes input from the user level-wise using a queue. It prompts the user for each node's value and creates the tree accordingly.
3. We assume `-1` as a marker for null nodes (i.e., nodes with no child).
4. The `inorder` function is used to traverse and print the binary tree in inorder traversal.
5. In the `main` function, we call `createLevelWise` to create the binary tree and then print its inorder traversal.

### 1. Algorithms & Data Structures (C++): Threaded Binary Tree

A threaded binary tree is a binary tree in which every node has either one or two additional pointers, called "threads", that link to other nodes in the tree. These threads can be used to efficiently traverse the tree without using recursion or a stack. There are two types of threads: left threads and right threads.

In a threaded binary tree, a left thread of a node points to its in-order predecessor, and a right thread points to its in-order successor. If a node does not have a left child, its left thread points to the node that would be its in-order predecessor. Similarly, if a node does not have a right child, its right thread points to the node that would be its in-order successor.

Here's a basic implementation of a threaded binary tree in C++:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* left;
    Node* right;
    bool leftThread;
    bool rightThread;
};

Node* createThreadedNode(int data) {
    Node* newNode = new Node;
    newNode->data = data;
    newNode->left = nullptr;
    newNode->right = nullptr;
    newNode->leftThread = false;
    newNode->rightThread = false;
    return newNode;
}

void insert(Node*& root, int data) {
    Node* newNode = createThreadedNode(data);
    Node* prev = nullptr;
    Node* current = root;

    while (current) {
        prev = current;
        if (data < current->data) {
            if (!current->left) {
                newNode->left = current->left;
                newNode->right = current;
                newNode->leftThread = true;
                current->left = newNode;
                current->leftThread = false;
                return;
            }
            current = current->left;
        } else {
            if (current->rightThread) {
                newNode->left = current;
                newNode->right = current->right;
                newNode->rightThread = true;
                current->right = newNode;
                current->rightThread = false;
                return;
            }
            current = current->right;
        }
    }

    if (!prev) {
        root = newNode;
        return;
    }

    if (data < prev->data) {
        prev->left = newNode;
        prev->leftThread = true;
    } else {
        prev->right = newNode;
        prev->rightThread = true;
    }
}

Node* leftMost(Node* node) {
    if (!node)
        return nullptr;

    while (node->left)
        node = node->left;

    return node;
}

void inOrderTraversal(Node* root) {
    Node* current = leftMost(root);

    while (current) {
        std::cout << current->data << " ";

        if (current->rightThread)
            current = current->right;
        else
            current = leftMost(current->right);
    }
}

int main() {
    Node* root = nullptr;
    insert(root, 6);
    insert(root, 3);
    insert(root, 8);
    insert(root, 1);
    insert(root, 5);
    insert(root, 7);
    insert(root, 9);

    std::cout << "In-order traversal: ";
    inOrderTraversal(root);
    std::cout << std::endl;

    return 0;
}
```

This implementation demonstrates the insertion operation and in-order traversal of a threaded binary tree. The `insert` function inserts a new node into the tree, maintaining the threads appropriately. The `inOrderTraversal` function performs an in-order traversal of the threaded binary tree without using recursion.

### 1. Algorithms & Data Structures (C++): Threaded Binary Tree: Deletion

Deleting a node from a threaded binary tree in C++ involves handling different cases based on whether the node to be deleted has children and whether it is threaded to its successor or predecessor. Here's an outline of how you can implement the deletion operation for a threaded binary tree:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* left;
    Node* right;
    bool isThreaded; // indicates if the right pointer is a thread
};

// Helper function to find the in-order successor of a node
Node* findSuccessor(Node* node) {
    if (node == nullptr)
        return nullptr;
    if (node->isThreaded)
        return node->right;
    node = node->right;
    while (node->left != nullptr)
        node = node->left;
    return node;
}

// Function to delete a node from threaded binary tree
Node* deleteNode(Node* root, int key) {
    // Base case
    if (root == nullptr)
        return nullptr;

    // Searching for the node with the given key to delete
    Node* parent = nullptr;
    Node* current = root;
    while (current != nullptr) {
        if (current->data == key)
            break;
        parent = current;
        if (current->data < key) {
            if (!current->isThreaded)
                current = current->right;
            else
                break; // Node not found
        } else {
            current = current->left;
        }
    }

    // Node with key not found
    if (current == nullptr)
        return root;

    // Case 1: Node to be deleted has no children or is a leaf node
    if (current->left == nullptr && current->right == nullptr) {
        if (parent == nullptr) {
            delete current;
            return nullptr; // Tree becomes empty
        }
        if (parent->left == current) {
            parent->left = nullptr;
            parent->isThreaded = true;
        } else {
            parent->right = current->right;
        }
        delete current;
        return root;
    }

    // Case 2: Node to be deleted has only one child
    if (current->left == nullptr || current->right == nullptr) {
        Node* child = (current->left != nullptr) ? current->left : current->right;
        if (parent == nullptr) {
            delete current;
            return child;
        }
        if (parent->left == current)
            parent->left = child;
        else
            parent->right = child;
        delete current;
        return root;
    }

    // Case 3: Node to be deleted has both left and right children
    Node* successor = findSuccessor(current);
    int successorValue = successor->data;
    deleteNode(root, successorValue);
    current->data = successorValue;
    return root;
}

// Function to create a new node
Node* createNode(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->left = nullptr;
    newNode->right = nullptr;
    newNode->isThreaded = false;
    return newNode;
}

// Function to insert a new node into threaded binary tree
Node* insert(Node* root, int key) {
    if (root == nullptr)
        return createNode(key);
    Node* parent = nullptr;
    Node* current = root;
    while (current != nullptr) {
        parent = current;
        if (key < current->data) {
            if (current->left == nullptr) {
                current->left = createNode(key);
                current->isThreaded = true;
                current->left->right = current;
                break;
            }
            current = current->left;
        } else {
            if (current->isThreaded) {
                Node* temp = current->right;
                current->right = createNode(key);
                current->isThreaded = false;
                current->right->right = temp;
                break;
            }
            current = current->right;
        }
    }
    return root;
}

// Function to perform in-order traversal of threaded binary tree
void inOrderTraversal(Node* root) {
    if (root == nullptr)
        return;
    Node* current = root;
    while (current->left != nullptr)
        current = current->left;
    while (current != nullptr) {
        std::cout << current->data << " ";
        if (!current->isThreaded)
            current = current->right;
        else
            current = findSuccessor(current);
    }
}

int main() {
    Node* root = nullptr;
    root = insert(root, 20);
    insert(root, 10);
    insert(root, 30);
    insert(root, 5);
    insert(root, 15);

    std::cout << "In-order traversal before deletion: ";
    inOrderTraversal(root);
    std::cout << std::endl;

    root = deleteNode(root, 10);

    std::cout << "In-order traversal after deletion: ";
    inOrderTraversal(root);
    std::cout << std::endl;

    return 0;
}
```

This code provides a basic implementation of a threaded binary tree and the deletion operation. Make sure to test it thoroughly with different cases to ensure its correctness.

### 1. Algorithms & Data Structures (C++): Threaded Binary Tree: Insertion

A threaded binary tree is a binary tree in which every node has either a left or right child, or both, but unlike a regular binary tree, the child pointers of some nodes point to their in-order predecessor or successor rather than to their left or right child nodes. This threading allows for efficient traversal of the tree without recursion.

To insert a node into a threaded binary tree, you follow these steps:

1. Start from the root and traverse the tree to find the appropriate position to insert the new node, just like in a regular binary tree.
2. Once you find the position to insert the new node, you need to decide whether to make the new node the left or right child of its parent.
3. Update the threading pointers accordingly. If the node has no left child, set its left child to be the in-order predecessor of the new node. If the node has no right child, set its right child to be the in-order successor of the new node.
4. If the new node has both a left and right child, you can still insert it normally as a regular binary tree node.

Here's a C++ implementation of the insertion function for a threaded binary tree:

```cpp
#include <iostream>

struct Node {
    int key;
    Node *left, *right;
    bool isThreadedLeft, isThreadedRight;

    Node(int k) : key(k), left(nullptr), right(nullptr), isThreadedLeft(false), isThreadedRight(false) {}
};

class ThreadedBinaryTree {
private:
    Node *root;

    Node *insertRec(Node *root, int key) {
        if (root == nullptr)
            return new Node(key);

        if (key < root->key) {
            if (root->isThreadedLeft)
                root->isThreadedLeft = false;
            root->left = insertRec(root->left, key);
        } else if (key > root->key) {
            if (root->isThreadedRight)
                root->isThreadedRight = false;
            root->right = insertRec(root->right, key);
        }

        return root;
    }

public:
    ThreadedBinaryTree() : root(nullptr) {}

    void insert(int key) {
        root = insertRec(root, key);
    }

    void inorderTraversal() {
        Node *curr = root;
        while (curr != nullptr) {
            while (curr->left != nullptr && !curr->isThreadedLeft)
                curr = curr->left;
            std::cout << curr->key << " ";

            if (curr->isThreadedRight)
                curr = curr->right;
            else
                curr = curr->right;
        }
    }
};

int main() {
    ThreadedBinaryTree tree;
    tree.insert(10);
    tree.insert(5);
    tree.insert(20);
    tree.insert(8);
    tree.insert(15);

    std::cout << "Inorder traversal of threaded binary tree: ";
    tree.inorderTraversal();
    std::cout << std::endl;

    return 0;
}
```

In this code:

- `Node` represents a node in the threaded binary tree.
- `ThreadedBinaryTree` is the class representing the threaded binary tree and contains the insertion and traversal functions.
- `insertRec` is a recursive function to insert a node into the threaded binary tree.
- `inorderTraversal` performs an inorder traversal of the threaded binary tree.

This implementation assumes that the threaded binary tree is initially empty and only handles the insertion of new nodes. You may need to modify it further to handle other operations or edge cases based on your requirements.

### 1. Algorithms & Data Structures (C++): Traversing Binary Trees

Traversing binary trees is a fundamental operation in computer science and is often used in various algorithms and applications. In C++, there are three main methods for traversing binary trees: inorder, preorder, and postorder traversal. Here's a brief overview of each method:

1. **Inorder Traversal**: In inorder traversal, you recursively traverse the left subtree, visit the current node, and then recursively traverse the right subtree. This results in visiting nodes in non-decreasing order in a binary search tree (BST).

2. **Preorder Traversal**: In preorder traversal, you visit the current node, then recursively traverse the left subtree, and finally recursively traverse the right subtree. This is useful for creating a copy of the tree or prefix notation in expression evaluation.

3. **Postorder Traversal**: In postorder traversal, you recursively traverse the left subtree, then the right subtree, and finally visit the current node. This is often used in deleting or freeing the nodes of a tree.

Here's how you can implement these traversals in C++:

```cpp
#include <iostream>

// Define the structure of a binary tree node
struct Node {
    int data;
    Node* left;
    Node* right;

    Node(int value) : data(value), left(nullptr), right(nullptr) {}
};

// Inorder traversal
void inorderTraversal(Node* root) {
    if (root == nullptr) return;
    inorderTraversal(root->left);
    std::cout << root->data << " ";
    inorderTraversal(root->right);
}

// Preorder traversal
void preorderTraversal(Node* root) {
    if (root == nullptr) return;
    std::cout << root->data << " ";
    preorderTraversal(root->left);
    preorderTraversal(root->right);
}

// Postorder traversal
void postorderTraversal(Node* root) {
    if (root == nullptr) return;
    postorderTraversal(root->left);
    postorderTraversal(root->right);
    std::cout << root->data << " ";
}

int main() {
    // Example binary tree
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);

    std::cout << "Inorder traversal: ";
    inorderTraversal(root);
    std::cout << std::endl;

    std::cout << "Preorder traversal: ";
    preorderTraversal(root);
    std::cout << std::endl;

    std::cout << "Postorder traversal: ";
    postorderTraversal(root);
    std::cout << std::endl;

    return 0;
}
```

This code defines a binary tree node structure and implements the three traversal methods. In the `main()` function, it creates an example binary tree and demonstrates each traversal method.

### 1. Algorithms & Data Structures (C++): Univalued Binary Tree

Sure, here's an example implementation of a function to check if a binary tree is univalued (i.e., all nodes have the same value):

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

bool isUnivalTree(TreeNode* root) {
    if (root == nullptr) return true;
    
    // Check if the value of the current node is equal to the value of its children
    if ((root->left && root->val != root->left->val) ||
        (root->right && root->val != root->right->val)) {
        return false;
    }
    
    // Recursively check the left and right subtrees
    return isUnivalTree(root->left) && isUnivalTree(root->right);
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(1);
    root->right = new TreeNode(1);
    root->left->left = new TreeNode(1);
    root->left->right = new TreeNode(1);
    root->right->right = new TreeNode(1);
    
    if (isUnivalTree(root)) {
        cout << "The tree is univalued." << endl;
    } else {
        cout << "The tree is not univalued." << endl;
    }
    
    return 0;
}
```

This code defines a `TreeNode` struct representing a node in the binary tree. The `isUnivalTree` function checks if the given binary tree is univalued recursively by comparing the value of the current node with the values of its left and right children. If any child's value is different from the current node's value, it returns `false`. Otherwise, it recursively checks the left and right subtrees. The `main` function provides an example of how to use this function.

### 1. Algorithms & Data Structures (C++): Vertical Order Print

Vertical Order Print is a popular problem in data structures and algorithms where you need to print a binary tree vertically, meaning nodes with the same horizontal distance from the root are printed on the same line. This problem can be solved using various data structures like hash maps, queues, or even by leveraging the properties of binary trees.

Here's a basic approach to solve the Vertical Order Print problem in C++ using a hash map and a queue:

```cpp
#include <iostream>
#include <map>
#include <queue>
#include <vector>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void verticalOrderPrint(TreeNode* root) {
    if (!root)
        return;

    // Using a map to store nodes at each horizontal distance
    map<int, vector<int>> verticalMap;
    queue<pair<TreeNode*, int>> q; // Queue to do level order traversal along with horizontal distance
    q.push({root, 0});

    while (!q.empty()) {
        auto nodePair = q.front();
        q.pop();
        TreeNode* node = nodePair.first;
        int hd = nodePair.second;

        // Storing the node's value in the map based on its horizontal distance
        verticalMap[hd].push_back(node->val);

        // Enqueue left child with horizontal distance hd - 1
        if (node->left)
            q.push({node->left, hd - 1});

        // Enqueue right child with horizontal distance hd + 1
        if (node->right)
            q.push({node->right, hd + 1});
    }

    // Traverse the map and print nodes at each horizontal distance
    for (auto it = verticalMap.begin(); it != verticalMap.end(); ++it) {
        for (int val : it->second) {
            cout << val << " ";
        }
        cout << endl;
    }
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(7);

    cout << "Vertical order print:" << endl;
    verticalOrderPrint(root);

    return 0;
}
```

This code snippet demonstrates a basic implementation of the Vertical Order Print problem using a hash map and a queue for level-order traversal. It prints the nodes of the binary tree vertically, with nodes at the same horizontal distance printed on the same line.

### 1. Algorithms & Data Structures (C++): What are some different ways you can traverse Binary Trees?

Traversing binary trees, whether they're binary search trees (BSTs), balanced binary trees, or any other type, is a fundamental operation in computer science and programming. Here are some common ways to traverse binary trees, focusing on depth-first and breadth-first traversal techniques:

1. **Inorder Traversal**: In inorder traversal, you first visit the left subtree, then the root node, and finally the right subtree. This traversal results in visiting nodes in non-decreasing order in a BST.

2. **Preorder Traversal**: In preorder traversal, you visit the root node first, then recursively traverse the left subtree, and finally the right subtree. This is often used to create a copy of the tree.

3. **Postorder Traversal**: In postorder traversal, you visit the left subtree, then the right subtree, and finally the root node. This traversal is useful in deleting or freeing the nodes of the tree.

4. **Level Order Traversal (Breadth-First Traversal)**: Level order traversal visits nodes level by level, from left to right. You start from the root, then visit all nodes at level 1, then level 2, and so on. This traversal uses a queue data structure for efficient implementation.

Each of these traversal methods has its own use cases and advantages depending on the problem you're solving. For example, inorder traversal is useful for printing the elements of a BST in sorted order, while preorder and postorder traversals are useful for certain types of tree manipulations like serialization or deserialization. Level order traversal is often used to search for a specific node in a binary tree or to print the tree structure level by level.

In C++, you can implement these traversals recursively or iteratively, depending on your preference and the requirements of your application.

### 1. Algorithms & Data Structures (C++): Why are heaps complete binary tree

Heaps are implemented as complete binary trees because of the efficiency it brings to their operations. Here's why:

1. **Space Efficiency**: By ensuring that the tree is complete, you minimize wasted space. Complete binary trees fill nodes from left to right on each level, so there are no "gaps" as you might have in other types of binary trees. This compactness is essential for efficient memory usage.

2. **Efficient Insertion**: When you insert a new element into a heap, you add it at the next available position, maintaining the tree's completeness. This means you don't need to search for the right spot to maintain any specific ordering property; you simply append it to the end of the tree and then perform any necessary swaps to maintain the heap property (e.g., max heap or min heap property).

3. **Efficient Deletion (especially for Heaps)**: Similarly, when you remove an element from a heap, you typically remove the root node (for max or min heaps). After removing the root, you need to fill that position with another element while maintaining the heap property. Again, because of the complete binary tree property, you know exactly where to go to find the replacement (typically the last leaf node), ensuring that the tree remains complete.

4. **Simplified Implementation**: Implementing algorithms for heaps becomes more straightforward when the tree structure has this predictable, complete form. You can use simple arithmetic to compute the indices of parent, left child, and right child nodes without complex pointer manipulation or recursive algorithms.

In summary, the completeness of binary trees in heaps simplifies insertion, deletion, and traversal operations while optimizing memory usage, making it an ideal choice for implementing heaps efficiently.

### 1. Algorithms & Data Structures (C++): Linked Representation of Binary Tree

In C++, you can represent a binary tree using a linked representation where each node has pointers to its left and right children. Here's a simple implementation:

```cpp
#include <iostream>

// Define the structure of a tree node
struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;

    // Constructor
    TreeNode(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Function to create a new node
TreeNode* createNode(int data) {
    return new TreeNode(data);
}

// Function to insert a node into the binary tree
void insert(TreeNode*& root, int data) {
    if (root == nullptr) {
        root = createNode(data);
        return;
    }

    if (data < root->data) {
        insert(root->left, data);
    } else {
        insert(root->right, data);
    }
}

// Function to traverse the binary tree in-order
void inOrderTraversal(TreeNode* root) {
    if (root == nullptr) return;

    inOrderTraversal(root->left);
    std::cout << root->data << " ";
    inOrderTraversal(root->right);
}

int main() {
    TreeNode* root = nullptr;

    // Inserting elements into the binary tree
    insert(root, 5);
    insert(root, 3);
    insert(root, 7);
    insert(root, 1);
    insert(root, 4);

    // Printing the binary tree in-order
    std::cout << "In-order traversal: ";
    inOrderTraversal(root);
    std::cout << std::endl;

    return 0;
}
```

This code defines a `TreeNode` structure representing each node in the binary tree. The `insert` function is used to insert elements into the binary tree while maintaining the binary search tree property. The `inOrderTraversal` function traverses the binary tree in in-order (left, root, right) and prints the elements.

You can extend this implementation by adding functions for pre-order and post-order traversals, deletion of nodes, searching for a node, etc., depending on your requirements.

### 1. Algorithms & Data Structures (C++): Process For Solving Binary Tree Problems

Solving binary tree problems in C++ involves a systematic approach that combines understanding of algorithms, data structures, and the specific problem requirements. Here's a general process you can follow:

1. **Understand the Problem**: Carefully read and understand the problem statement. Identify what the problem is asking you to do with binary trees. Pay attention to any constraints or requirements mentioned.

2. **Review Binary Tree Basics**: Ensure you have a solid understanding of basic binary tree concepts such as nodes, edges, root, parent, children, height, depth, traversal methods (in-order, pre-order, post-order), and properties (complete binary tree, full binary tree, balanced binary tree, etc.).

3. **Choose an Algorithmic Approach**: Based on the problem requirements, select the appropriate algorithmic approach. Common approaches for binary tree problems include traversal algorithms (e.g., Depth-First Search, Breadth-First Search), recursive algorithms, divide and conquer, and dynamic programming.

4. **Implement Binary Tree Data Structure**: If the problem doesn't provide a binary tree implementation, create one. Define a `TreeNode` struct/class representing a node in the binary tree, and optionally, a `BinaryTree` class to encapsulate tree operations.

5. **Write Helper Functions**: Depending on the problem, you may need helper functions to perform tasks such as tree traversal, node insertion, deletion, etc.

6. **Implement the Solution**: Use the chosen algorithmic approach to solve the problem. If you're using recursion, write a recursive function that operates on the binary tree. Ensure your solution handles edge cases and boundary conditions appropriately.

7. **Test Your Solution**: Write test cases to verify that your solution works correctly for different inputs and edge cases. Test for both correctness and efficiency.

8. **Analyze Time and Space Complexity**: Analyze the time and space complexity of your solution. Ensure it meets the problem's constraints and performance requirements.

9. **Optimize if Necessary**: If your initial solution is not optimal, think about ways to optimize it. This could involve reducing time complexity, space complexity, or improving the algorithm's efficiency.

10. **Document Your Code**: Write clear and concise comments to explain your code's logic, algorithms used, and any assumptions made. This will make your code more readable and understandable for others (and your future self).

11. **Review and Refactor**: Review your code for readability, efficiency, and maintainability. Refactor as needed to improve code quality.

12. **Submit and Discuss**: If the problem is part of an interview or competition, submit your solution and be prepared to discuss your approach and reasoning with others.

By following this process, you can effectively approach and solve binary tree problems in C++, ensuring your solutions are correct, efficient, and maintainable.

### 1. Algorithms & Data Structures (C++): Stack Question: Binary Tree Postorder Traversal

Sure! Implementing postorder traversal of a binary tree using a stack is a common algorithmic problem. In postorder traversal, you visit the nodes in the order of left subtree, right subtree, and then the root node.

Here's how you can implement the postorder traversal of a binary tree using a stack in C++:

```cpp
#include <iostream>
#include <stack>
#include <vector>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

vector<int> postorderTraversal(TreeNode* root) {
    vector<int> result;
    stack<TreeNode*> s;
    TreeNode* prev = nullptr;
    TreeNode* current = root;

    while (current != nullptr || !s.empty()) {
        if (current != nullptr) {
            s.push(current);
            current = current->left;
        } else {
            TreeNode* temp = s.top()->right;
            if (temp == nullptr || temp == prev) {
                prev = s.top();
                result.push_back(prev->val);
                s.pop();
            } else {
                current = temp;
            }
        }
    }

    return result;
}

// Function to create a new TreeNode
TreeNode* createNode(int val) {
    TreeNode* newNode = new TreeNode(val);
    return newNode;
}

int main() {
    TreeNode* root = createNode(1);
    root->left = createNode(2);
    root->right = createNode(3);
    root->left->left = createNode(4);
    root->left->right = createNode(5);
    root->right->left = createNode(6);
    root->right->right = createNode(7);

    vector<int> result = postorderTraversal(root);
    cout << "Postorder Traversal: ";
    for (int val : result) {
        cout << val << " ";
    }
    cout << endl;

    return 0;
}
```

This code implements the postorder traversal iteratively using a stack. We keep track of the previously visited node to handle cases where we need to backtrack from the right subtree.

Hope this helps! Let me know if you have further questions!

### 1. Algorithms & Data Structures (C++): Binary Trees Traversal - Inorder

In C++, inorder traversal of a binary tree is typically implemented recursively. Here's how you can do it:

```cpp
#include <iostream>

// Define the structure of a binary tree node
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to perform inorder traversal recursively
void inorderTraversal(TreeNode* root) {
    if (root == nullptr) return;
    inorderTraversal(root->left); // Visit left subtree
    std::cout << root->val << " "; // Visit current node
    inorderTraversal(root->right); // Visit right subtree
}

// Function to create a new node
TreeNode* newNode(int val) {
    TreeNode* node = new TreeNode(val);
    return node;
}

int main() {
    // Create a sample binary tree
    TreeNode* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);

    std::cout << "Inorder traversal: ";
    inorderTraversal(root);
    std::cout << std::endl;

    return 0;
}
```

In this code:

- `TreeNode` represents each node in the binary tree, containing a value and pointers to its left and right children.
- `inorderTraversal` is a recursive function that performs the inorder traversal. It first traverses the left subtree, then visits the current node, and finally traverses the right subtree.
- `newNode` is a utility function to create a new tree node with a given value.
- In the `main` function, we create a sample binary tree and call the `inorderTraversal` function to print the inorder traversal of the tree.

### 1. Algorithms & Data Structures (C++): Binary Trees Traversal - Level Order

Level order traversal is a popular algorithm used to visit all the nodes of a binary tree level by level, from top to bottom and from left to right within each level. This traversal method is also known as breadth-first traversal. Here's how you can implement level order traversal in C++ using a queue:

```cpp
#include <iostream>
#include <queue>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void levelOrder(TreeNode* root) {
    if (root == nullptr) return;

    queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        TreeNode* current = q.front();
        q.pop();
        cout << current->val << " ";

        if (current->left != nullptr) {
            q.push(current->left);
        }
        if (current->right != nullptr) {
            q.push(current->right);
        }
    }
}

// Example usage
int main() {
    // Creating a sample binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    cout << "Level Order Traversal: ";
    levelOrder(root);

    return 0;
}
```

In this implementation, we use a queue to keep track of nodes at each level. We start by pushing the root node onto the queue. Then, in each iteration of the while loop, we pop a node from the front of the queue, print its value, and then push its left and right child nodes (if they exist) onto the queue. This process continues until the queue becomes empty, which indicates that we have traversed all nodes in level order.

### 1. Algorithms & Data Structures (C++): Binary Trees Traversal - Postorder

Postorder traversal in binary trees is a depth-first traversal technique. It traverses the tree in the order of left subtree, right subtree, root. Here's how you can implement it in C++ using recursion:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void postorderTraversal(TreeNode* root) {
    if (root == nullptr)
        return;

    // Traverse left subtree
    postorderTraversal(root->left);

    // Traverse right subtree
    postorderTraversal(root->right);

    // Visit root node
    std::cout << root->val << " ";
}

int main() {
    // Create a sample binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    std::cout << "Postorder traversal: ";
    postorderTraversal(root);

    return 0;
}
```

This code defines a simple binary tree structure and implements the postorder traversal function recursively. In the `main()` function, a sample binary tree is created, and the postorder traversal function is called to traverse it.

### 1. Algorithms & Data Structures (C++): Binary Trees Traversal - Preorder

In C++, you can implement binary tree traversal using various techniques. Here's how you can implement preorder traversal recursively:

```cpp
#include <iostream>

// Define the structure for a binary tree node
struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;

    TreeNode(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Function to perform preorder traversal
void preorderTraversal(TreeNode* root) {
    if (root == nullptr) return; // Base case: empty tree

    // Visit the current node
    std::cout << root->data << " ";

    // Recursively traverse the left subtree
    preorderTraversal(root->left);

    // Recursively traverse the right subtree
    preorderTraversal(root->right);
}

int main() {
    // Create a sample binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    // Perform preorder traversal
    std::cout << "Preorder Traversal: ";
    preorderTraversal(root);

    return 0;
}
```

In this code:

- We define the structure `TreeNode` to represent each node in the binary tree.
- The `preorderTraversal` function takes a pointer to the root of the tree and performs preorder traversal recursively.
- In the `main` function, we create a sample binary tree and call the `preorderTraversal` function to perform the traversal.

This code will output:

```bash
Preorder Traversal: 1 2 4 5 3
```

This represents the preorder traversal of the binary tree.

### 1. Algorithms & Data Structures (C++): Binary Tree: In-order traversal

In-order traversal is a popular technique for traversing binary trees. It's called "in-order" because it visits the nodes of the tree in the order: left child, parent, right child. This traversal method is commonly used for binary search trees because it visits the nodes in sorted order.

Here's how you can implement the in-order traversal of a binary tree in C++ using recursion:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void inOrderTraversal(TreeNode* root) {
    if (root == nullptr) return;

    // Traverse the left subtree
    inOrderTraversal(root->left);

    // Visit the current node
    std::cout << root->val << " ";

    // Traverse the right subtree
    inOrderTraversal(root->right);
}

int main() {
    // Creating a binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    std::cout << "In-order traversal: ";
    inOrderTraversal(root);

    // Clean up memory (optional)
    delete root->left->right;
    delete root->left->left;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

This code creates a binary tree, then performs an in-order traversal starting from the root node. It prints the values of the nodes in the sorted order. Finally, it releases the dynamically allocated memory used for the tree nodes.

### 1. Algorithms & Data Structures (C++): Binary Tree: Inorder Traversal

In C++, inorder traversal of a binary tree is typically implemented using recursion. Here's how you can do it:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void inorderTraversal(TreeNode* root) {
    if (root == nullptr) {
        return;
    }
    inorderTraversal(root->left); // Visit left subtree
    std::cout << root->val << " "; // Visit root node
    inorderTraversal(root->right); // Visit right subtree
}

// Test
int main() {
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    std::cout << "Inorder Traversal: ";
    inorderTraversal(root);

    return 0;
}
```

This code will output:

```plaintext
Inorder Traversal: 4 2 5 1 3
```

In the `inorderTraversal` function, we recursively traverse the left subtree, then visit the current node, and finally traverse the right subtree. This follows the left-root-right order of inorder traversal.

### 1. Algorithms & Data Structures (C++): Binary Tree: Iterative Inorder

Certainly! Iterative inorder traversal of a binary tree in C++ can be implemented using a stack. Here's how you can do it:

```cpp
#include <iostream>
#include <stack>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void inorderTraversal(TreeNode* root) {
    if (root == nullptr) return;

    stack<TreeNode*> nodeStack;
    TreeNode* current = root;

    while (current != nullptr || !nodeStack.empty()) {
        // Reach the leftmost node of the current subtree
        while (current != nullptr) {
            nodeStack.push(current);
            current = current->left;
        }

        // Current node is nullptr, so we backtrack and process the parent node
        current = nodeStack.top();
        nodeStack.pop();
        cout << current->val << " ";

        // Move to the right subtree
        current = current->right;
    }
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    cout << "Inorder traversal: ";
    inorderTraversal(root);
    cout << endl;

    return 0;
}
```

In this code:

- We use a stack to simulate the function call stack that is used in recursive inorder traversal.
- We start from the root and traverse left until we reach the leftmost node, pushing each node encountered onto the stack.
- Once we reach a nullptr (indicating the leftmost node of a subtree), we backtrack by popping nodes from the stack, processing each node's value, and moving to its right child if it exists.
- We repeat this process until the stack is empty and there are no more nodes to process.

This approach achieves inorder traversal iteratively without using recursion.

### 1. Algorithms & Data Structures (C++): Binary Tree: Iterative Preorder

Iterative Preorder Traversal is a method to traverse a binary tree iteratively without using recursion. In this traversal technique, the nodes are visited in the following order: root, left subtree, right subtree. Here's a C++ implementation:

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

void iterativePreorder(TreeNode* root) {
    if (root == nullptr)
        return;
    
    stack<TreeNode*> nodeStack;
    nodeStack.push(root);

    while (!nodeStack.empty()) {
        TreeNode* node = nodeStack.top();
        cout << node->val << " ";
        nodeStack.pop();

        if (node->right)
            nodeStack.push(node->right);
        if (node->left)
            nodeStack.push(node->left);
    }
}

int main() {
    /* Constructed binary tree is
            1
          /   \
         2     3
       /  \
      4    5
    */
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    cout << "Iterative Preorder traversal of binary tree is: ";
    iterativePreorder(root);
    cout << endl;

    return 0;
}
```

In this code:

1. We use a stack to keep track of the nodes to be visited.
2. We start by pushing the root node onto the stack.
3. We then loop until the stack becomes empty.
4. In each iteration, we pop a node from the stack and print its value.
5. If the popped node has a right child, we push it onto the stack first (because we want to process left subtree before the right).
6. If the popped node has a left child, we push it onto the stack next (because the left child should be processed next).
7. We repeat these steps until the stack becomes empty.

### 1. Algorithms & Data Structures (C++): Binary Tree: Iterative Traversals

In C++, you can implement iterative traversals of a binary tree using stacks. Here's how you can perform iterative traversals for the three main types: preorder, inorder, and postorder.

Let's start with a basic binary tree node structure:

```cpp
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};
```

#### Preorder Traversal

```cpp
#include <stack>

void preorderTraversal(TreeNode* root) {
    if (root == nullptr) return;

    std::stack<TreeNode*> stack;
    stack.push(root);

    while (!stack.empty()) {
        TreeNode* node = stack.top();
        stack.pop();
        std::cout << node->val << " ";

        if (node->right) stack.push(node->right);
        if (node->left) stack.push(node->left);
    }
}
```

#### Inorder Traversal

```cpp
#include <stack>

void inorderTraversal(TreeNode* root) {
    if (root == nullptr) return;

    std::stack<TreeNode*> stack;
    TreeNode* current = root;

    while (current != nullptr || !stack.empty()) {
        while (current != nullptr) {
            stack.push(current);
            current = current->left;
        }
        current = stack.top();
        stack.pop();
        std::cout << current->val << " ";
        current = current->right;
    }
}
```

#### Postorder Traversal

```cpp
#include <stack>

void postorderTraversal(TreeNode* root) {
    if (root == nullptr) return;

    std::stack<TreeNode*> stack;
    std::stack<int> output;
    stack.push(root);

    while (!stack.empty()) {
        TreeNode* node = stack.top();
        stack.pop();
        output.push(node->val);

        if (node->left) stack.push(node->left);
        if (node->right) stack.push(node->right);
    }

    while (!output.empty()) {
        std::cout << output.top() << " ";
        output.pop();
    }
}
```

These implementations use stacks to simulate the recursive calls. Each node is processed in a specific order according to the traversal type.

### 1. Algorithms & Data Structures (C++): Binary Tree: Level Order Traversal

Level order traversal of a binary tree involves visiting each level of the tree from top to bottom, left to right. It's also known as breadth-first traversal. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <queue>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

void levelOrder(TreeNode* root) {
    if (root == NULL) return;

    queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        int levelSize = q.size();
        for (int i = 0; i < levelSize; i++) {
            TreeNode* current = q.front();
            q.pop();
            cout << current->val << " ";

            if (current->left != NULL) {
                q.push(current->left);
            }
            if (current->right != NULL) {
                q.push(current->right);
            }
        }
        cout << endl;
    }
}

int main() {
    // Example usage:
    // Create a binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    cout << "Level order traversal of binary tree:" << endl;
    levelOrder(root);

    return 0;
}
```

This code demonstrates how to perform a level order traversal of a binary tree using a queue data structure to keep track of the nodes at each level. The `levelOrder` function takes the root of the binary tree as input and prints out the nodes at each level, starting from the root level.

### 1. Algorithms & Data Structures (C++): Binary Tree: Post Order Traversal

In C++, you can implement a post-order traversal of a binary tree using both iterative and recursive approaches. Here's how you can do it:

1. **Iterative Approach** using a stack:

```cpp
#include <iostream>
#include <stack>

using namespace std;

struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

void postOrderIterative(TreeNode* root) {
    if (root == nullptr)
        return;

    stack<TreeNode*> st1, st2;
    st1.push(root);

    while (!st1.empty()) {
        TreeNode* curr = st1.top();
        st1.pop();
        st2.push(curr);

        if (curr->left)
            st1.push(curr->left);

        if (curr->right)
            st1.push(curr->right);
    }

    while (!st2.empty()) {
        TreeNode* curr = st2.top();
        st2.pop();
        cout << curr->val << " ";
    }
}

int main() {
    // Sample tree creation
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    cout << "Post-order Traversal (Iterative): ";
    postOrderIterative(root);
    cout << endl;

    return 0;
}
```

1. **Recursive Approach**:

```cpp
#include <iostream>

using namespace std;

struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

void postOrderRecursive(TreeNode* root) {
    if (root == nullptr)
        return;

    postOrderRecursive(root->left);
    postOrderRecursive(root->right);
    cout << root->val << " ";
}

int main() {
    // Sample tree creation
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    cout << "Post-order Traversal (Recursive): ";
    postOrderRecursive(root);
    cout << endl;

    return 0;
}
```

Both approaches will print the nodes of the binary tree in post-order traversal.

### 1. Algorithms & Data Structures (C++): Binary Trees: Inorder Traversal

In C++, implementing an inorder traversal of a binary tree typically involves recursion. Here's a basic example of how you can perform an inorder traversal:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void inorderTraversal(TreeNode* root) {
    if (root == nullptr)
        return;
    
    // Traverse left subtree
    inorderTraversal(root->left);
    
    // Process current node
    std::cout << root->val << " ";
    
    // Traverse right subtree
    inorderTraversal(root->right);
}

// Function to create a new tree node
TreeNode* newNode(int val) {
    TreeNode* temp = new TreeNode(val);
    return temp;
}

int main() {
    // Creating a sample binary tree
    TreeNode* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);

    std::cout << "Inorder traversal of the binary tree: ";
    inorderTraversal(root);
    std::cout << std::endl;

    return 0;
}
```

In this code:

- The `TreeNode` struct defines the structure of a binary tree node, including its value, left child, and right child.
- The `inorderTraversal` function recursively traverses the binary tree in an inorder manner: left subtree, current node, right subtree.
- `newNode` is a helper function to create new tree nodes.
- In the `main` function, a sample binary tree is created, and its inorder traversal is performed.

This code will output:

```bash
Inorder traversal of the binary tree: 4 2 5 1 3
```

This represents the inorder traversal sequence of the binary tree.

### 1. Algorithms & Data Structures (C++): Binary Trees: Iterative Inorder Traversal

Iterative inorder traversal of a binary tree in C++ can be accomplished using a stack. Here's a basic implementation:

```cpp
#include <iostream>
#include <stack>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

void iterativeInorderTraversal(TreeNode* root) {
    if (root == nullptr)
        return;

    stack<TreeNode*> s;
    TreeNode* current = root;

    while (current != nullptr || !s.empty()) {
        // Traverse to the leftmost node of the current subtree
        while (current != nullptr) {
            s.push(current);
            current = current->left;
        }

        // Pop the top node from the stack
        current = s.top();
        s.pop();

        // Process the current node
        cout << current->val << " ";

        // Move to the right subtree
        current = current->right;
    }
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    cout << "Iterative inorder traversal: ";
    iterativeInorderTraversal(root);
    
    return 0;
}
```

In this implementation, we use a stack to simulate the recursion. We start with the root and go left until we reach a nullptr, pushing each node we encounter onto the stack. Once we reach a nullptr, we pop a node from the stack, process it, and then move to its right child. We repeat this process until the stack is empty and there are no more nodes to process. This way, we traverse the entire tree in inorder without using recursion.

### 1. Algorithms & Data Structures (C++): Binary Trees: Iterative Postorder Traversal

Iterative postorder traversal of a binary tree can be achieved using two stacks. Here's a C++ implementation:

```cpp
#include <iostream>
#include <stack>
using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

void iterativePostorder(TreeNode* root) {
    if (root == nullptr) return;

    stack<TreeNode*> s1, s2;
    s1.push(root);

    while (!s1.empty()) {
        TreeNode* node = s1.top();
        s1.pop();
        s2.push(node);

        if (node->left)
            s1.push(node->left);
        if (node->right)
            s1.push(node->right);
    }

    while (!s2.empty()) {
        cout << s2.top()->val << " ";
        s2.pop();
    }
}

int main() {
    // Example usage:
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(7);

    cout << "Iterative Postorder Traversal: ";
    iterativePostorder(root);

    // Clean up memory
    delete root->right->right;
    delete root->right->left;
    delete root->left->right;
    delete root->left->left;
    delete root->right;
    delete root->left;
    delete root;

    return 0;
}
```

In this implementation, we use two stacks. First, we traverse the tree using a modified version of preorder traversal, pushing the nodes onto `s2`. Then, we pop elements from `s2` to get the postorder traversal.

Please note the cleanup in the `main()` function to release memory allocated for the tree nodes.

### 1. Algorithms & Data Structures (C++): Binary Trees: Iterative Preorder - Alternate Approaches

Iterative preorder traversal of a binary tree is typically done using a stack. However, there are a few alternative approaches you can consider:

1. **Using Morris Traversal**:
   Morris Traversal allows for inorder traversal without using a stack or recursion. However, with a slight modification, you can adapt it to perform preorder traversal iteratively without using a stack. The idea is to modify the binary tree structure temporarily during traversal to maintain the links needed to move around the tree without using extra space.

   Here's a basic outline of the algorithm:
   - Initialize current as the root.
   - While current is not NULL:
     - If the current node's left child is NULL:
       - Print the current node's data.
       - Move to the right child.
     - Else:
       - Find the inorder predecessor of the current node (the rightmost node in the left subtree).
       - If the right child of the inorder predecessor is NULL:
         - Set the right child to the current node.
         - Print the current node's data.
         - Move to the left child.
       - Else:
         - Set the right child of the inorder predecessor to NULL.
         - Move to the right child.

   This approach modifies the structure of the tree, but it's a handy alternative if you want to avoid using a stack.

2. **Using Threaded Binary Trees**:
   Threaded Binary Trees are binary trees where the null pointers are used to link nodes during traversal. Specifically, a threaded binary tree is one where every node's right child either points to its inorder successor or a NULL value. By creating threaded binary trees, you can perform iterative preorder traversal without using a stack.

   Here's how it can be done:
   - Traverse the tree in preorder manner and find the predecessor of each node.
   - If the predecessor's right child is NULL, set it to the current node.
   - If the predecessor's right child is the current node, this indicates that we have visited the left subtree and we can print the current node's data and move to the right child.
   - If the predecessor's right child is not the current node, set it to NULL and move to the left child.

   Threaded binary trees require additional memory for maintaining thread pointers but allow for traversal without additional space.

Both of these approaches offer alternatives to the standard stack-based iterative preorder traversal, providing ways to traverse the binary tree iteratively without using a stack explicitly. Each has its own trade-offs in terms of memory usage and ease of implementation.

### 1. Algorithms & Data Structures (C++): Binary Trees: Level Order Traversal

Level order traversal is a fundamental algorithm used to visit all nodes of a binary tree level by level, starting from the root. Here's how you can implement level order traversal in C++ using a queue for breadth-first search:

```cpp
#include <iostream>
#include <queue>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void levelOrder(TreeNode* root) {
    if (root == nullptr)
        return;
    
    queue<TreeNode*> q;
    q.push(root);
    
    while (!q.empty()) {
        int levelSize = q.size(); // Number of nodes at current level
        
        // Process all nodes at current level
        for (int i = 0; i < levelSize; ++i) {
            TreeNode* node = q.front();
            q.pop();
            cout << node->val << " ";
            
            // Enqueue left and right children if they exist
            if (node->left)
                q.push(node->left);
            if (node->right)
                q.push(node->right);
        }
        cout << endl; // Move to the next level
    }
}

int main() {
    // Example tree:
    //       1
    //      / \
    //     2   3
    //    / \ / \
    //   4  5 6  7
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(7);

    cout << "Level order traversal of binary tree:" << endl;
    levelOrder(root);

    // Clean up memory
    delete root->right->right;
    delete root->right->left;
    delete root->left->right;
    delete root->left->left;
    delete root->right;
    delete root->left;
    delete root;
    
    return 0;
}
```

In this code:

1. We define a `TreeNode` structure to represent a node in the binary tree.
2. The `levelOrder` function performs the level order traversal using a queue. It starts by pushing the root node into the queue and then enters a loop where it processes each level one by one.
3. Inside the loop, it dequeues nodes one by one, prints their values, and enqueues their left and right children if they exist.
4. The `main` function demonstrates the usage of the `levelOrder` function with an example binary tree.

### 1. Algorithms & Data Structures (C++): Binary Trees: Postorder Traversal

In C++, you can implement the postorder traversal of a binary tree using recursion. Postorder traversal visits the nodes in the following order: left, right, root. Here's how you can implement it:

```cpp
#include <iostream>

// Define the structure of a binary tree node
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to perform postorder traversal of a binary tree
void postorderTraversal(TreeNode* root) {
    if (root == nullptr) return;
    
    // Traverse left subtree
    postorderTraversal(root->left);
    
    // Traverse right subtree
    postorderTraversal(root->right);
    
    // Visit the current node
    std::cout << root->val << " ";
}

int main() {
    // Create a binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    
    // Perform postorder traversal
    std::cout << "Postorder traversal: ";
    postorderTraversal(root);
    std::cout << std::endl;
    
    return 0;
}
```

This code defines a simple binary tree structure (`TreeNode`) and a function (`postorderTraversal`) to perform the postorder traversal. In the `main()` function, a binary tree is created and then the postorder traversal is performed on it. Finally, the nodes are printed in postorder traversal order.

### 1. Algorithms & Data Structures (C++): Binary Tree from given traversal list

Creating a binary tree from a given traversal list, such as preorder, inorder, or postorder, involves understanding the order in which the nodes are visited. Let's take the example of constructing a binary tree from preorder and inorder traversals. Here's how you can do it in C++:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

TreeNode* buildTreeHelper(const vector<int>& preorder, int preStart, int preEnd,
                          const vector<int>& inorder, int inStart, int inEnd,
                          unordered_map<int, int>& inorderMap) {
    if (preStart > preEnd || inStart > inEnd) return nullptr;

    int rootVal = preorder[preStart];
    TreeNode* root = new TreeNode(rootVal);

    int rootIndexInorder = inorderMap[rootVal];
    int numLeftNodes = rootIndexInorder - inStart;

    root->left = buildTreeHelper(preorder, preStart + 1, preStart + numLeftNodes,
                                 inorder, inStart, rootIndexInorder - 1, inorderMap);
    root->right = buildTreeHelper(preorder, preStart + numLeftNodes + 1, preEnd,
                                  inorder, rootIndexInorder + 1, inEnd, inorderMap);

    return root;
}

TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
    unordered_map<int, int> inorderMap;
    for (int i = 0; i < inorder.size(); ++i) {
        inorderMap[inorder[i]] = i;
    }

    return buildTreeHelper(preorder, 0, preorder.size() - 1,
                           inorder, 0, inorder.size() - 1,
                           inorderMap);
}

// Function to print the inorder traversal of a binary tree (for validation)
void inorderTraversal(TreeNode* root) {
    if (!root) return;
    inorderTraversal(root->left);
    cout << root->val << " ";
    inorderTraversal(root->right);
}

int main() {
    vector<int> preorder = {3, 9, 20, 15, 7};
    vector<int> inorder = {9, 3, 15, 20, 7};

    TreeNode* root = buildTree(preorder, inorder);

    cout << "Inorder Traversal of Constructed Tree: ";
    inorderTraversal(root);
    cout << endl;

    return 0;
}
```

In this code:

- `buildTree` function takes the preorder and inorder traversal lists and constructs the binary tree. It calls a helper function `buildTreeHelper`.
- `buildTreeHelper` recursively constructs the tree by finding the root node, locating the left and right subtrees in both preorder and inorder lists, and then recursively constructing left and right subtrees.
- `inorderMap` is used to quickly find the index of a node in the inorder traversal list, aiding in the construction of subtrees.
- `main` function is an example usage where we construct a binary tree using preorder and inorder traversals and print the inorder traversal of the constructed tree.

This approach can be extended to construct a binary tree from other traversal combinations as well.

### 1. Algorithms & Data Structures (C++): Binary Tree Inorder Traversal

Certainly! In C++, you can implement the inorder traversal of a binary tree using recursion. Here's how you can do it:

```cpp
#include <iostream>
using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

class Solution {
public:
    void inorderTraversal(TreeNode* root) {
        if (root == NULL)
            return;
        
        // Traverse left subtree
        inorderTraversal(root->left);
        
        // Visit current node
        cout << root->val << " ";
        
        // Traverse right subtree
        inorderTraversal(root->right);
    }
};

int main() {
    // Create a binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    
    Solution solution;
    
    // Perform inorder traversal
    cout << "Inorder traversal: ";
    solution.inorderTraversal(root);
    
    return 0;
}
```

This code defines a `TreeNode` structure to represent the nodes of the binary tree. Then, it defines a `Solution` class with a method `inorderTraversal()` that performs the inorder traversal recursively. Finally, in the `main()` function, a binary tree is created, and the inorder traversal is performed on it.

### 1. Algorithms & Data Structures (C++): Binary Tree InOrder Traversal - Trees

In C++, performing an in-order traversal of a binary tree is a common operation. It's a depth-first traversal method where you visit the left subtree, then the root, and finally the right subtree recursively. Here's how you can implement it:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    void inorderTraversal(TreeNode* root) {
        if (root == nullptr)
            return;
        
        inorderTraversal(root->left);    // Visit left subtree
        std::cout << root->val << " ";   // Visit root
        inorderTraversal(root->right);   // Visit right subtree
    }
};

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    
    Solution solution;
    std::cout << "Inorder traversal: ";
    solution.inorderTraversal(root);
    std::cout << std::endl;

    // Free memory
    delete root->left->left;
    delete root->left->right;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

This code creates a simple binary tree structure, performs an in-order traversal, and prints the values of the nodes in the traversal order. Make sure to free the allocated memory after usage to prevent memory leaks.

### 1. Algorithms & Data Structures (C++): Binary Tree Level Order Traversal

Sure, binary tree level order traversal is a classic problem in computer science. It's a way to traverse a binary tree level by level, visiting all nodes at each level from left to right. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

vector<vector<int>> levelOrder(TreeNode* root) {
    vector<vector<int>> result;
    if (root == NULL) return result;

    queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        int size = q.size();
        vector<int> level;

        for (int i = 0; i < size; i++) {
            TreeNode* node = q.front();
            q.pop();
            level.push_back(node->val);

            if (node->left != NULL) q.push(node->left);
            if (node->right != NULL) q.push(node->right);
        }

        result.push_back(level);
    }

    return result;
}

// Utility function to create a new tree node.
TreeNode* newNode(int data) {
    TreeNode* node = new TreeNode(data);
    return node;
}

int main() {
    /* Constructed binary tree is:
              1
            /   \
           2     3
          / \   / \
         4   5 6   7
    */
    TreeNode *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);

    vector<vector<int>> result = levelOrder(root);

    // Print the result
    cout << "Level order traversal of binary tree:" << endl;
    for (const auto& level : result) {
        for (int val : level) {
            cout << val << " ";
        }
        cout << endl;
    }

    return 0;
}
```

This implementation uses a queue to perform a breadth-first traversal of the binary tree. At each level, it records the values of the nodes and stores them in the result vector. Finally, it returns the result vector containing the level order traversal of the binary tree.

### 1. Algorithms & Data Structures (C++): Binary Tree Level Order Traversal - Binary Trees

Binary Tree Level Order Traversal is a classic problem in algorithms and data structures. The task is to traverse a binary tree level by level, from top to bottom, and from left to right, printing or processing the nodes at each level.

Here's a C++ implementation of the Binary Tree Level Order Traversal using a queue for breadth-first traversal:

```cpp
#include <iostream>
#include <queue>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

vector<vector<int>> levelOrder(TreeNode* root) {
    vector<vector<int>> result;
    if (root == nullptr)
        return result;

    queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        int levelSize = q.size();
        vector<int> levelNodes;

        for (int i = 0; i < levelSize; i++) {
            TreeNode* node = q.front();
            q.pop();
            levelNodes.push_back(node->val);

            if (node->left != nullptr)
                q.push(node->left);
            if (node->right != nullptr)
                q.push(node->right);
        }

        result.push_back(levelNodes);
    }

    return result;
}

// Helper function to create a binary tree
TreeNode* createTree(vector<int>& nodes, int index) {
    if (index >= nodes.size() || nodes[index] == -1)
        return nullptr;

    TreeNode* root = new TreeNode(nodes[index]);
    root->left = createTree(nodes, 2 * index + 1);
    root->right = createTree(nodes, 2 * index + 2);

    return root;
}

// Helper function to delete a binary tree
void deleteTree(TreeNode* root) {
    if (root == nullptr)
        return;

    deleteTree(root->left);
    deleteTree(root->right);
    delete root;
}

int main() {
    vector<int> nodes = {3, 9, 20, -1, -1, 15, 7}; // Example binary tree: [3,9,20,null,null,15,7]
    TreeNode* root = createTree(nodes, 0);

    vector<vector<int>> result = levelOrder(root);

    // Output the result
    cout << "Level Order Traversal:\n";
    for (const auto& level : result) {
        for (int val : level) {
            cout << val << " ";
        }
        cout << endl;
    }

    // Clean up
    deleteTree(root);

    return 0;
}
```

In this implementation, we use a queue to perform a breadth-first traversal of the binary tree. We enqueue nodes level by level, and for each level, we dequeue nodes and add their values to the current level's vector. Finally, we push this vector into the result vector.

This implementation ensures that nodes at the same level are processed before moving to the next level, achieving the level order traversal of the binary tree.

### 1. Algorithms & Data Structures (C++): Binary Tree Level Order Traversal - Trees

Binary Tree Level Order Traversal is a fundamental algorithm in computer science used to traverse a binary tree level by level, starting from the root node. This traversal technique is also known as Breadth-First Search (BFS). In C++, you can implement it using a queue data structure. Here's a basic implementation:

```cpp
#include <iostream>
#include <queue>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

vector<vector<int>> levelOrder(TreeNode* root) {
    vector<vector<int>> result;
    if (root == nullptr) return result;

    queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        int size = q.size();
        vector<int> level;
        for (int i = 0; i < size; ++i) {
            TreeNode* node = q.front();
            q.pop();
            level.push_back(node->val);
            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }
        result.push_back(level);
    }
    return result;
}

// Utility function to create a new tree node
TreeNode* newNode(int data) {
    TreeNode* node = new TreeNode(data);
    return node;
}

int main() {
    // Sample binary tree
    TreeNode* root = newNode(3);
    root->left = newNode(9);
    root->right = newNode(20);
    root->right->left = newNode(15);
    root->right->right = newNode(7);

    // Level Order Traversal
    vector<vector<int>> result = levelOrder(root);

    // Print the result
    cout << "Level Order Traversal:" << endl;
    for (const auto& level : result) {
        for (int val : level) {
            cout << val << " ";
        }
        cout << endl;
    }

    return 0;
}
```

This code defines a binary tree node structure (`TreeNode`), a function to perform level order traversal (`levelOrder`), and a utility function to create new tree nodes (`newNode`). In the `main` function, a sample binary tree is created and its level order traversal is printed.

### 1. Algorithms & Data Structures (C++): Binary Tree Traversal

Binary tree traversal is a fundamental operation in computer science and is often used to process or search for elements in a binary tree. There are three main types of binary tree traversal: **in-order traversal**, **pre-order traversal**, and **post-order traversal**.

Here's an overview of each traversal method and its implementation in C++:

#### 1. In-Order Traversal

In in-order traversal, the nodes are visited in the order (left subtree, root, right subtree).

```cpp
#include <iostream>

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void inOrderTraversal(TreeNode* root) {
    if (root == nullptr) return;

    inOrderTraversal(root->left);
    std::cout << root->val << " ";
    inOrderTraversal(root->right);
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    std::cout << "In-Order Traversal: ";
    inOrderTraversal(root);

    return 0;
}
```

#### 2. Pre-Order Traversal

In pre-order traversal, the nodes are visited in the order (root, left subtree, right subtree).

```cpp
void preOrderTraversal(TreeNode* root) {
    if (root == nullptr) return;

    std::cout << root->val << " ";
    preOrderTraversal(root->left);
    preOrderTraversal(root->right);
}
```

#### 3. Post-Order Traversal

In post-order traversal, the nodes are visited in the order (left subtree, right subtree, root).

```cpp
void postOrderTraversal(TreeNode* root) {
    if (root == nullptr) return;

    postOrderTraversal(root->left);
    postOrderTraversal(root->right);
    std::cout << root->val << " ";
}
```

You can use these traversal methods depending on your requirements, such as for printing tree elements, searching for a specific value, or performing other operations on the binary tree.

### 1. Algorithms & Data Structures (C++): Binary Tree Traversals

In C++, traversing a binary tree typically involves three main methods: inorder, preorder, and postorder traversals. Here's how you can implement these traversals using recursion:

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

// Inorder traversal: Left -> Root -> Right
void inorderTraversal(TreeNode* root) {
    if (root == nullptr) return;
    inorderTraversal(root->left);
    cout << root->val << " ";
    inorderTraversal(root->right);
}

// Preorder traversal: Root -> Left -> Right
void preorderTraversal(TreeNode* root) {
    if (root == nullptr) return;
    cout << root->val << " ";
    preorderTraversal(root->left);
    preorderTraversal(root->right);
}

// Postorder traversal: Left -> Right -> Root
void postorderTraversal(TreeNode* root) {
    if (root == nullptr) return;
    postorderTraversal(root->left);
    postorderTraversal(root->right);
    cout << root->val << " ";
}

int main() {
    // Example tree:
    //       1
    //      / \
    //     2   3
    //    / \
    //   4   5

    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    cout << "Inorder traversal: ";
    inorderTraversal(root);
    cout << endl;

    cout << "Preorder traversal: ";
    preorderTraversal(root);
    cout << endl;

    cout << "Postorder traversal: ";
    postorderTraversal(root);
    cout << endl;

    return 0;
}
```

This code will output:

```bash
Inorder traversal: 4 2 5 1 3 
Preorder traversal: 1 2 4 5 3 
Postorder traversal: 4 5 2 3 1 
```

Each of these traversals visits every node in the tree exactly once. In the inorder traversal, nodes are visited in non-decreasing order. In the preorder traversal, nodes are visited in the order of Root -> Left -> Right. In the postorder traversal, nodes are visited in the order of Left -> Right -> Root.

### 1. Algorithms & Data Structures (C++): Binary Tree: Construct Tree from PostOrder and Inorder Traversal

Constructing a binary tree from its postorder and inorder traversals involves a classic algorithm in computer science. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <unordered_map>
#include <vector>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

class Solution {
public:
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        unordered_map<int, int> inorder_map;
        for (int i = 0; i < inorder.size(); ++i) {
            inorder_map[inorder[i]] = i;
        }
        return buildTreeHelper(inorder, postorder, 0, inorder.size() - 1, 0, postorder.size() - 1, inorder_map);
    }

    TreeNode* buildTreeHelper(vector<int>& inorder, vector<int>& postorder, int in_start, int in_end, int post_start, int post_end, unordered_map<int, int>& inorder_map) {
        if (in_start > in_end || post_start > post_end) return nullptr;

        int root_val = postorder[post_end];
        TreeNode* root = new TreeNode(root_val);
        int root_index_inorder = inorder_map[root_val];

        int left_subtree_size = root_index_inorder - in_start;

        root->left = buildTreeHelper(inorder, postorder, in_start, root_index_inorder - 1, post_start, post_start + left_subtree_size - 1, inorder_map);
        root->right = buildTreeHelper(inorder, postorder, root_index_inorder + 1, in_end, post_start + left_subtree_size, post_end - 1, inorder_map);

        return root;
    }
};

// Function to print the tree in inorder traversal
void printInorder(TreeNode* node) {
    if (node == nullptr) return;
    printInorder(node->left);
    cout << node->val << " ";
    printInorder(node->right);
}

int main() {
    Solution solution;

    vector<int> inorder = {9, 3, 15, 20, 7};
    vector<int> postorder = {9, 15, 7, 20, 3};

    TreeNode* root = solution.buildTree(inorder, postorder);

    cout << "Inorder traversal of constructed tree: ";
    printInorder(root);
    cout << endl;

    return 0;
}
```

This code creates a binary tree given its inorder and postorder traversals. The `buildTree` function constructs the tree using helper function `buildTreeHelper`, which recursively constructs the tree. The `inorder_map` is used to efficiently find the index of the root in the inorder traversal. Finally, the `main` function demonstrates the usage of this code by constructing a tree and printing its inorder traversal.

### 1. Algorithms & Data Structures (C++): Binary Tree: Construct Tree from PreOrder and Inorder Traversal

Constructing a binary tree from its preorder and inorder traversals is a classic problem in computer science. Here's a C++ implementation of how you can achieve this:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

class Solution {
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        unordered_map<int, int> inorder_map;
        for (int i = 0; i < inorder.size(); ++i) {
            inorder_map[inorder[i]] = i;
        }
        return build(preorder, 0, preorder.size() - 1, inorder, 0, inorder.size() - 1, inorder_map);
    }

    TreeNode* build(vector<int>& preorder, int pre_start, int pre_end, 
                    vector<int>& inorder, int in_start, int in_end,
                    unordered_map<int, int>& inorder_map) {
        if (pre_start > pre_end || in_start > in_end) return nullptr;

        int root_val = preorder[pre_start];
        TreeNode* root = new TreeNode(root_val);

        int root_index_inorder = inorder_map[root_val];
        int left_subtree_size = root_index_inorder - in_start;

        root->left = build(preorder, pre_start + 1, pre_start + left_subtree_size, 
                           inorder, in_start, root_index_inorder - 1, inorder_map);

        root->right = build(preorder, pre_start + left_subtree_size + 1, pre_end, 
                            inorder, root_index_inorder + 1, in_end, inorder_map);

        return root;
    }
};

// Function to print the inorder traversal of a binary tree (for validation)
void inorderTraversal(TreeNode* root) {
    if (root) {
        inorderTraversal(root->left);
        cout << root->val << " ";
        inorderTraversal(root->right);
    }
}

int main() {
    // Example usage
    vector<int> preorder = {3, 9, 20, 15, 7};
    vector<int> inorder = {9, 3, 15, 20, 7};

    Solution sol;
    TreeNode* root = sol.buildTree(preorder, inorder);

    cout << "Inorder traversal of constructed tree: ";
    inorderTraversal(root);
    cout << endl;

    return 0;
}
```

This code constructs a binary tree from its preorder and inorder traversals. The `buildTree` function constructs the tree recursively. It utilizes a helper function `build` to recursively build subtrees. The `inorder_map` is used to efficiently find the indices of elements in the inorder traversal.

You can modify the `main` function to provide different preorder and inorder traversal sequences to test the implementation.

### 1. Algorithms & Data Structures (C++): Binary Tree: Post-order traversal

In C++, a post-order traversal of a binary tree involves visiting the left subtree, then the right subtree, and finally the root node. You can implement it recursively or iteratively using a stack. Here's how you can do it recursively:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

void postorderTraversal(TreeNode* root) {
    if (root == NULL) return;
    postorderTraversal(root->left);
    postorderTraversal(root->right);
    std::cout << root->val << " ";
}

int main() {
    // Example usage:
    // Constructing a simple binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    std::cout << "Post-order traversal: ";
    postorderTraversal(root);
    std::cout << std::endl;

    // Deallocate memory
    delete root->left->right;
    delete root->left->left;
    delete root->right;
    delete root->left;
    delete root;

    return 0;
}
```

This code defines a `TreeNode` struct and implements a `postorderTraversal` function to perform the post-order traversal recursively. It prints the values of the nodes in post-order. You can create a binary tree as per your requirements and then call the `postorderTraversal` function passing the root of the tree.

Would you like an explanation of the iterative approach or anything else related to this topic?

### 1. Algorithms & Data Structures (C++): Binary Tree: Postorder Traversal

In C++, you can implement the postorder traversal of a binary tree using both recursive and iterative approaches. Here's an example of both methods:

1. **Recursive Approach**:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void postorderTraversal(TreeNode* root) {
    if (root == nullptr) return;
    postorderTraversal(root->left);
    postorderTraversal(root->right);
    std::cout << root->val << " ";
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    std::cout << "Postorder traversal: ";
    postorderTraversal(root);
    
    return 0;
}
```

1. **Iterative Approach**:

For the iterative approach, we can use a stack to simulate the recursive call stack:

```cpp
#include <iostream>
#include <stack>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void postorderTraversal(TreeNode* root) {
    if (root == nullptr) return;

    std::stack<TreeNode*> stk;
    TreeNode* current = root;

    while (current != nullptr || !stk.empty()) {
        if (current != nullptr) {
            stk.push(current);
            current = current->left;
        } else {
            TreeNode* temp = stk.top()->right;
            if (temp == nullptr) {
                temp = stk.top();
                stk.pop();
                std::cout << temp->val << " ";
                while (!stk.empty() && temp == stk.top()->right) {
                    temp = stk.top();
                    stk.pop();
                    std::cout << temp->val << " ";
                }
            } else {
                current = temp;
            }
        }
    }
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    std::cout << "Postorder traversal: ";
    postorderTraversal(root);
    
    return 0;
}
```

Both implementations should print the postorder traversal of the binary tree.

### 1. Algorithms & Data Structures (C++): Binary Tree: Pre-order traversal

In C++, a pre-order traversal of a binary tree means visiting the root node first, then recursively traversing the left subtree, followed by the right subtree. You can implement it using both iterative and recursive approaches. Here's how you can do it recursively:

```cpp
#include <iostream>

struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int val) : data(val), left(nullptr), right(nullptr) {}
};

void preorderTraversal(TreeNode* root) {
    if (root == nullptr)
        return;
    
    std::cout << root->data << " "; // Process the current node
    preorderTraversal(root->left);   // Recursively traverse left subtree
    preorderTraversal(root->right);  // Recursively traverse right subtree
}

int main() {
    // Example tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    std::cout << "Preorder Traversal: ";
    preorderTraversal(root);
    std::cout << std::endl;

    // Clean up memory
    delete root->left->right;
    delete root->left->left;
    delete root->right;
    delete root->left;
    delete root;

    return 0;
}
```

Output:

```bash
Preorder Traversal: 1 2 4 5 3
```

This code creates a binary tree with some example nodes and performs a pre-order traversal on it. Adjust it according to your specific requirements or data structure if necessary.

### 1. Algorithms & Data Structures (C++): Binary Tree: Preorder Traversal

Certainly! Preorder traversal is one of the methods used to traverse a binary tree. In preorder traversal, you visit the root node first, then recursively do a preorder traversal of the left subtree, followed by a recursive preorder traversal of the right subtree. Here's how you can implement preorder traversal of a binary tree in C++:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void preorderTraversal(TreeNode* root) {
    if (root == nullptr) {
        return;
    }
    
    // Visit the root node
    std::cout << root->val << " ";
    
    // Traverse left subtree
    preorderTraversal(root->left);
    
    // Traverse right subtree
    preorderTraversal(root->right);
}

int main() {
    // Create a binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    
    // Perform preorder traversal
    std::cout << "Preorder traversal: ";
    preorderTraversal(root);
    std::cout << std::endl;
    
    return 0;
}
```

This code defines a binary tree node structure (`TreeNode`) and a function (`preorderTraversal`) to perform preorder traversal. In the `main()` function, a binary tree is created, and preorder traversal is performed starting from the root node. The output will display the values of the nodes visited in preorder traversal.

### 1. Algorithms & Data Structures (C++): Binary Tree: Traversals - Breadth-First

In breadth-first traversal of a binary tree, also known as level-order traversal, you visit all the nodes at each level before moving to the next level. This traversal strategy utilizes a queue data structure to keep track of the nodes to be visited. Here's how you can implement breadth-first traversal for a binary tree in C++:

```cpp
#include <iostream>
#include <queue>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void breadthFirstTraversal(TreeNode* root) {
    if (root == nullptr)
        return;

    queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        TreeNode* current = q.front();
        q.pop();
        cout << current->val << " ";

        if (current->left)
            q.push(current->left);
        if (current->right)
            q.push(current->right);
    }
}

// Sample usage
int main() {
    // Create a sample binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(7);

    cout << "Breadth-first traversal: ";
    breadthFirstTraversal(root);
    cout << endl;

    // Clean up
    delete root->right->right;
    delete root->right->left;
    delete root->left->right;
    delete root->left->left;
    delete root->right;
    delete root->left;
    delete root;

    return 0;
}
```

In this code:

- We define a `TreeNode` struct to represent each node in the binary tree.
- The `breadthFirstTraversal` function implements the breadth-first traversal using a queue.
- We create a sample binary tree in the `main` function and call `breadthFirstTraversal` to demonstrate the traversal.

This code should output the nodes of the binary tree in breadth-first order.

### 1. Algorithms & Data Structures (C++): Binary Tree: Traversals - Inorder

In C++, inorder traversal of a binary tree can be implemented using both recursive and iterative approaches. Here's how you can implement it using the recursive approach:

```cpp
#include <iostream>

// Binary Tree Node definition
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void inorderTraversal(TreeNode* root) {
    if (root == nullptr) return;

    inorderTraversal(root->left);
    std::cout << root->val << " ";
    inorderTraversal(root->right);
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    std::cout << "Inorder traversal: ";
    inorderTraversal(root);
    std::cout << std::endl;

    // Clean up memory
    delete root->left->left;
    delete root->left->right;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

This code defines a binary tree node structure and implements the inorder traversal recursively. The `inorderTraversal` function takes the root of the binary tree as input and prints the nodes in inorder traversal.

Remember to free up the memory allocated for the tree nodes after usage to avoid memory leaks.

If you prefer an iterative approach, you can use a stack data structure to simulate the function call stack in the recursive version. Would you like to see that as well?

### 1. Algorithms & Data Structures (C++): Binary Tree: Traversals - Postorder

In C++, performing a postorder traversal on a binary tree typically involves visiting the nodes in the order: left, right, root. Here's how you can implement postorder traversal using recursion:

```cpp
#include <iostream>

// Define the structure for a binary tree node
struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;

    TreeNode(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Function to perform postorder traversal
void postorderTraversal(TreeNode* root) {
    if (root == nullptr) {
        return;
    }

    // Visit left subtree
    postorderTraversal(root->left);

    // Visit right subtree
    postorderTraversal(root->right);

    // Visit root node
    std::cout << root->data << " ";
}

int main() {
    // Creating a sample binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    std::cout << "Postorder traversal: ";
    postorderTraversal(root);
    std::cout << std::endl;

    // Deallocate memory to prevent memory leaks (optional)
    // Deallocation in postorder manner to ensure safe deallocation
    // Note: This part is optional, as memory deallocation might not always be necessary depending on the context.
    delete root->left->left;
    delete root->left->right;
    delete root->right;
    delete root->left;
    delete root;

    return 0;
}
```

In this code:

- `TreeNode` is a struct representing a node in the binary tree.
- `postorderTraversal` is the function that performs postorder traversal recursively.
- In `main`, a sample binary tree is created and postorder traversal is performed on it.
- Finally, memory deallocation is done to prevent memory leaks.

This code prints the postorder traversal of the binary tree, which means it will print the values of nodes in the order left, right, root.

### 1. Algorithms & Data Structures (C++): Binary Tree: Traversals - Preorder

In C++, you can traverse a binary tree using the preorder traversal technique. Preorder traversal visits each node in the following order: root, left subtree, right subtree. Here's how you can implement it:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to perform preorder traversal of a binary tree
void preorderTraversal(TreeNode* root) {
    if (root == nullptr)
        return;

    // Process current node
    std::cout << root->val << " ";

    // Traverse left subtree
    preorderTraversal(root->left);

    // Traverse right subtree
    preorderTraversal(root->right);
}

int main() {
    // Example usage:
    // Creating a sample binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    std::cout << "Preorder traversal of the binary tree is: ";
    preorderTraversal(root);
    std::cout << std::endl;

    // Clean up memory
    delete root->left->right;
    delete root->left->left;
    delete root->right;
    delete root->left;
    delete root;

    return 0;
}
```

This code defines a binary tree node (`TreeNode`), implements the preorder traversal function (`preorderTraversal`), and demonstrates its usage in the `main` function. You can modify the binary tree structure and values according to your requirements.

### 1. Algorithms & Data Structures (C++): Binary Trees: Construct Binary Tree From Inorder & Preorder Traversal

To construct a binary tree from its inorder and preorder traversals, you need to follow these steps:

1. **Understand the traversal order**: Preorder traversal visits the root node first, then the left subtree, and finally the right subtree. Inorder traversal visits the left subtree first, then the root node, and finally the right subtree.

2. **Identify root node**: In preorder traversal, the first element is always the root node. Find this root node in the inorder traversal to determine the left and right subtrees.

3. **Recursively construct left and right subtrees**: Once you've identified the root node, you can recursively apply the same process to construct the left and right subtrees.

Here's the C++ code to achieve this:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        unordered_map<int, int> inorder_map;
        for (int i = 0; i < inorder.size(); ++i) {
            inorder_map[inorder[i]] = i;
        }
        return buildTreeHelper(preorder, 0, preorder.size(), inorder, 0, inorder.size(), inorder_map);
    }

    TreeNode* buildTreeHelper(vector<int>& preorder, int preStart, int preEnd, vector<int>& inorder, int inStart, int inEnd, unordered_map<int, int>& inorder_map) {
        if (preStart >= preEnd || inStart >= inEnd) return nullptr;

        int rootVal = preorder[preStart];
        TreeNode* root = new TreeNode(rootVal);

        int rootIndexInorder = inorder_map[rootVal];
        int leftSubtreeSize = rootIndexInorder - inStart;

        root->left = buildTreeHelper(preorder, preStart + 1, preStart + 1 + leftSubtreeSize, inorder, inStart, rootIndexInorder, inorder_map);
        root->right = buildTreeHelper(preorder, preStart + 1 + leftSubtreeSize, preEnd, inorder, rootIndexInorder + 1, inEnd, inorder_map);

        return root;
    }
};

// Function to print inorder traversal of a binary tree
void printInorder(TreeNode* node) {
    if (node == nullptr) return;

    printInorder(node->left);
    cout << node->val << " ";
    printInorder(node->right);
}

int main() {
    vector<int> preorder = {3, 9, 20, 15, 7};
    vector<int> inorder = {9, 3, 15, 20, 7};

    Solution sol;
    TreeNode* root = sol.buildTree(preorder, inorder);

    cout << "Inorder traversal of the constructed tree: ";
    printInorder(root);
    cout << endl;

    return 0;
}
```

This code defines a `Solution` class with a `buildTree` method that constructs the binary tree from preorder and inorder traversals. The `buildTreeHelper` function is a recursive helper function that constructs the tree recursively. Finally, in the `main` function, it creates a sample binary tree and prints its inorder traversal.

### 1. Algorithms & Data Structures (C++): Binary Trees: Construct Binary Tree From Inorder & Preorder Traversal Conti

Sure! Continuing from where we left off, let's implement the function to construct a binary tree from given inorder and preorder traversals in C++.

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        // Create a map to store the index of each element in inorder traversal
        unordered_map<int, int> inorder_map;
        for (int i = 0; i < inorder.size(); ++i) {
            inorder_map[inorder[i]] = i;
        }
        
        return buildTreeHelper(preorder, 0, preorder.size() - 1, inorder, 0, inorder.size() - 1, inorder_map);
    }
    
    TreeNode* buildTreeHelper(vector<int>& preorder, int preStart, int preEnd,
                              vector<int>& inorder, int inStart, int inEnd,
                              unordered_map<int, int>& inorder_map) {
        if (preStart > preEnd || inStart > inEnd) {
            return nullptr;
        }
        
        // The first element in preorder traversal is the root
        int rootVal = preorder[preStart];
        TreeNode* root = new TreeNode(rootVal);
        
        // Find the index of root in inorder traversal
        int rootIndex = inorder_map[rootVal];
        int numLeft = rootIndex - inStart; // Number of nodes in the left subtree
        
        // Recursively build left and right subtrees
        root->left = buildTreeHelper(preorder, preStart + 1, preStart + numLeft,
                                     inorder, inStart, rootIndex - 1, inorder_map);
        root->right = buildTreeHelper(preorder, preStart + numLeft + 1, preEnd,
                                      inorder, rootIndex + 1, inEnd, inorder_map);
        
        return root;
    }
};
```

In this code, we first build a map to store the index of each element in the inorder traversal. This map is used to quickly find the index of the root node in the inorder traversal, which helps in dividing the inorder traversal into left and right subtrees. Then, we recursively build the left and right subtrees using the indices obtained from the map.

### 1. Algorithms & Data Structures (C++): Binary Trees: Constructing Binary Trees from Inorder & Postorder Traversal

Constructing a binary tree from its inorder and postorder traversals is a common problem in computer science and often tackled in technical interviews. Here's a basic approach to solve it using C++:

```cpp
#include <iostream>
#include <unordered_map>
#include <vector>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        unordered_map<int, int> inorder_map;
        for (int i = 0; i < inorder.size(); ++i) {
            inorder_map[inorder[i]] = i;
        }
        return buildTreeHelper(inorder, 0, inorder.size() - 1, postorder, 0, postorder.size() - 1, inorder_map);
    }
    
    TreeNode* buildTreeHelper(vector<int>& inorder, int inStart, int inEnd,
                              vector<int>& postorder, int postStart, int postEnd,
                              unordered_map<int, int>& inorder_map) {
        if (inStart > inEnd || postStart > postEnd) return nullptr;
        
        int rootVal = postorder[postEnd];
        TreeNode* root = new TreeNode(rootVal);
        
        int rootIndexInorder = inorder_map[rootVal];
        int leftSubtreeSize = rootIndexInorder - inStart;
        
        root->left = buildTreeHelper(inorder, inStart, rootIndexInorder - 1,
                                     postorder, postStart, postStart + leftSubtreeSize - 1,
                                     inorder_map);
        
        root->right = buildTreeHelper(inorder, rootIndexInorder + 1, inEnd,
                                      postorder, postStart + leftSubtreeSize, postEnd - 1,
                                      inorder_map);
        
        return root;
    }
};

// Function to print inorder traversal of a binary tree
void printInorder(TreeNode* root) {
    if (root == nullptr) return;
    printInorder(root->left);
    cout << root->val << " ";
    printInorder(root->right);
}

int main() {
    // Example usage
    vector<int> inorder = {9, 3, 15, 20, 7};
    vector<int> postorder = {9, 15, 7, 20, 3};
    
    Solution solution;
    TreeNode* root = solution.buildTree(inorder, postorder);
    
    cout << "Inorder traversal of constructed tree:\n";
    printInorder(root);
    
    return 0;
}
```

In this code:

- `buildTree` is the main function that constructs the tree. It creates a map to store the indices of elements in the inorder traversal for quick lookup.
- `buildTreeHelper` is a recursive helper function that constructs the tree using inorder and postorder traversal arrays, along with the map for fast access to indices in the inorder traversal.
- `printInorder` is a utility function to print the inorder traversal of the constructed tree.
- In the `main` function, you can see an example usage of how to construct a binary tree using the inorder and postorder traversal arrays.

### 1. Algorithms & Data Structures (C++): Binary Trees: Constructing Binary Trees from Inorder & Preorder Traversal

Constructing a binary tree from its inorder and preorder traversals is a common problem in programming interviews and competitive programming. The idea is to use the preorder traversal to determine the root of the tree and then use the inorder traversal to determine the left and right subtrees.

Here's a step-by-step approach to construct a binary tree from the inorder and preorder traversals in C++:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

class Solution {
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        unordered_map<int, int> inorder_map;
        for (int i = 0; i < inorder.size(); ++i) {
            inorder_map[inorder[i]] = i;
        }
        return buildTreeHelper(preorder, 0, preorder.size() - 1, inorder, 0, inorder.size() - 1, inorder_map);
    }

private:
    TreeNode* buildTreeHelper(vector<int>& preorder, int preStart, int preEnd, vector<int>& inorder, int inStart, int inEnd, unordered_map<int, int>& inorder_map) {
        if (preStart > preEnd || inStart > inEnd) {
            return nullptr;
        }

        int rootVal = preorder[preStart];
        TreeNode* root = new TreeNode(rootVal);

        int rootIndexInorder = inorder_map[rootVal];
        int leftSubtreeSize = rootIndexInorder - inStart;

        root->left = buildTreeHelper(preorder, preStart + 1, preStart + leftSubtreeSize, inorder, inStart, rootIndexInorder - 1, inorder_map);
        root->right = buildTreeHelper(preorder, preStart + leftSubtreeSize + 1, preEnd, inorder, rootIndexInorder + 1, inEnd, inorder_map);

        return root;
    }
};

// Function to print inorder traversal of binary tree
void printInorder(TreeNode* node) {
    if (node == NULL)
        return;

    // left, root, right
    printInorder(node->left);
    cout << node->val << " ";
    printInorder(node->right);
}

int main() {
    Solution solution;
    vector<int> preorder = {3, 9, 20, 15, 7};
    vector<int> inorder = {9, 3, 15, 20, 7};

    TreeNode* root = solution.buildTree(preorder, inorder);

    cout << "Inorder traversal of constructed tree: ";
    printInorder(root);
    cout << endl;

    return 0;
}
```

This C++ code defines a `Solution` class with a `buildTree` method that takes vectors representing the preorder and inorder traversals of the tree. It constructs the binary tree recursively using helper functions `buildTreeHelper`. The `printInorder` function is used to verify the constructed tree.

Make sure to understand the logic behind the code, especially how the root of the tree is determined from the preorder traversal and how the left and right subtrees are identified using the inorder traversal.

### 1. Algorithms & Data Structures (C++): Binary Trees: Constructing Binary Trees from Traversals

Constructing binary trees from traversals is a fundamental problem in computer science and is often encountered in interviews and competitive programming. There are several approaches to solve this problem, depending on the type of traversal given. The most common traversals used for constructing binary trees are:

1. **Inorder Traversal**: Left-Root-Right
2. **Preorder Traversal**: Root-Left-Right
3. **Postorder Traversal**: Left-Right-Root

Here's a brief overview of how to construct a binary tree from each of these traversals:

#### 1. Constructing from Inorder and Preorder Traversals

Given the inorder and preorder traversals of a binary tree, you can construct the binary tree recursively using the following steps:

1. The first element of the preorder traversal is the root of the tree.
2. Find the root element in the inorder traversal. All elements to the left of the root in the inorder traversal represent the left subtree, and all elements to the right represent the right subtree.
3. Recur for the left and right subtrees using appropriate portions of the inorder and preorder traversals.

#### 2. Constructing from Inorder and Postorder Traversals

Given the inorder and postorder traversals of a binary tree, you can construct the binary tree recursively using the following steps:

1. The last element of the postorder traversal is the root of the tree.
2. Find the root element in the inorder traversal. All elements to the left of the root in the inorder traversal represent the left subtree, and all elements to the right represent the right subtree.
3. Recur for the left and right subtrees using appropriate portions of the inorder and postorder traversals.

#### 3. Constructing from Preorder and Postorder Traversals

Given the preorder and postorder traversals of a binary tree, you can construct the binary tree recursively using the following steps:

1. The first element of the preorder traversal is the root of the tree.
2. Find the root element in the postorder traversal. All elements to the left of the root in the postorder traversal represent the left subtree, and all elements to the right represent the right subtree.
3. Recur for the left and right subtrees using appropriate portions of the preorder and postorder traversals.

#### Implementation in C++

Here's a simplified C++ implementation for constructing a binary tree from inorder and preorder traversals:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>

using namespace std;

struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

TreeNode* buildTreeHelper(vector<int>& preorder, int& preIndex, vector<int>& inorder, int inStart, int inEnd, unordered_map<int, int>& indexMap) {
    if (inStart > inEnd) return nullptr;

    int rootValue = preorder[preIndex++];
    TreeNode* root = new TreeNode(rootValue);

    int inIndex = indexMap[rootValue];

    root->left = buildTreeHelper(preorder, preIndex, inorder, inStart, inIndex - 1, indexMap);
    root->right = buildTreeHelper(preorder, preIndex, inorder, inIndex + 1, inEnd, indexMap);

    return root;
}

TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
    unordered_map<int, int> indexMap;
    for (int i = 0; i < inorder.size(); ++i) {
        indexMap[inorder[i]] = i;
    }
    int preIndex = 0;
    return buildTreeHelper(preorder, preIndex, inorder, 0, inorder.size() - 1, indexMap);
}

void printInorder(TreeNode* root) {
    if (root) {
        printInorder(root->left);
        cout << root->val << " ";
        printInorder(root->right);
    }
}

int main() {
    vector<int> preorder = {3, 9, 20, 15, 7};
    vector<int> inorder = {9, 3, 15, 20, 7};

    TreeNode* root = buildTree(preorder, inorder);

    cout << "Inorder traversal of constructed tree: ";
    printInorder(root);
    cout << endl;

    return 0;
}
```

This code demonstrates how to construct a binary tree from inorder and preorder traversals. The `buildTree` function constructs the tree recursively using helper functions. The `printInorder` function is used to verify the correctness of the constructed tree by printing its inorder traversal.

### 1. Algorithms & Data Structures (C++): Binary Trees: How Dequeue Function Works during Level Order Traversal

In the context of binary trees and level order traversal in C++, a dequeue function (not to be confused with the data structure deque) would typically refer to removing an element from the front of a queue. In level order traversal, you traverse the binary tree level by level, visiting nodes from left to right on each level.

Here's a basic explanation of how the dequeue function would work during level order traversal:

1. **Initialization**: Start with an empty queue. Enqueue the root node of the binary tree onto the queue.

2. **Traversal**: While the queue is not empty, dequeue a node from the front of the queue. This dequeued node represents the current node being visited.

3. **Processing**: Process the dequeued node. This could involve printing its value, performing some operation, or anything else as per the requirements.

4. **Enqueue Children**: Enqueue the left child (if it exists) and then the right child (if it exists) of the dequeued node onto the queue. This ensures that the children of the current node will be visited in the next iterations.

5. **Repeat**: Repeat steps 2-4 until the queue becomes empty, indicating that all nodes have been visited.

Here's a simplified code snippet in C++ to demonstrate how the dequeue function would be used during level order traversal:

```cpp
#include <iostream>
#include <queue>

struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int val) : data(val), left(nullptr), right(nullptr) {}
};

void levelOrderTraversal(TreeNode* root) {
    if (root == nullptr)
        return;

    std::queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        TreeNode* current = q.front();
        q.pop();

        // Process current node
        std::cout << current->data << " ";

        // Enqueue left child
        if (current->left)
            q.push(current->left);

        // Enqueue right child
        if (current->right)
            q.push(current->right);
    }
}

int main() {
    // Example binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    std::cout << "Level order traversal: ";
    levelOrderTraversal(root);

    return 0;
}
```

In this code, the `levelOrderTraversal` function traverses the binary tree in level order using a queue. The `q.front()` function dequeues a node from the front of the queue, simulating the dequeue operation, and then its left and right children (if they exist) are enqueued onto the queue.

### 1. Algorithms & Data Structures (C++): Binary Trees: How Enqueue Function Works during Level Order Traversal

In the context of binary trees, an "enqueue" operation typically refers to adding nodes to a queue data structure during a level-order traversal. In level-order traversal, also known as breadth-first traversal, nodes are visited level by level, starting from the root.

Here's how the enqueue function works during level-order traversal in C++:

```cpp
#include <iostream>
#include <queue>

using namespace std;

// Binary tree node structure
struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Function to perform level order traversal of a binary tree
void levelOrderTraversal(TreeNode* root) {
    if (root == nullptr)
        return;

    // Create an empty queue for level order traversal
    queue<TreeNode*> q;

    // Enqueue the root
    q.push(root);

    // Loop until the queue is empty
    while (!q.empty()) {
        // Dequeue a node from the queue
        TreeNode* current = q.front();
        q.pop();

        // Process the current node (print its data, for example)
        cout << current->data << " ";

        // Enqueue the left child if it exists
        if (current->left != nullptr)
            q.push(current->left);

        // Enqueue the right child if it exists
        if (current->right != nullptr)
            q.push(current->right);
    }
}

int main() {
    // Create a binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(7);

    // Perform level order traversal
    cout << "Level Order Traversal: ";
    levelOrderTraversal(root);
    cout << endl;

    return 0;
}
```

Explanation:

1. We start with the root node and create an empty queue to store the nodes to be processed.
2. We enqueue the root node into the queue.
3. We enter a loop where we dequeue a node from the front of the queue.
4. We process the dequeued node (print its data, for example).
5. If the dequeued node has a left child, we enqueue it.
6. If the dequeued node has a right child, we enqueue it.
7. We continue this process until the queue becomes empty, which indicates that all nodes have been processed.

This way, the enqueue function works during level-order traversal by adding child nodes to the queue as they are encountered, ensuring that nodes are processed in a level-wise manner.

### 1. Algorithms & Data Structures (C++): Binary Trees: Preorder Traversal

In C++, you can implement the preorder traversal of a binary tree using recursion. Here's how you can do it:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void preorderTraversal(TreeNode* root) {
    if (root == nullptr) {
        return;
    }
    
    // Process the current node (print its value)
    std::cout << root->val << " ";

    // Recursively traverse the left subtree
    preorderTraversal(root->left);

    // Recursively traverse the right subtree
    preorderTraversal(root->right);
}

int main() {
    // Example usage:
    // Create a binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    
    // Perform preorder traversal
    std::cout << "Preorder traversal: ";
    preorderTraversal(root);
    std::cout << std::endl;

    // Free memory (optional but recommended)
    delete root->left->right;
    delete root->left->left;
    delete root->right;
    delete root->left;
    delete root;

    return 0;
}
```

This code defines a `TreeNode` structure representing a node in the binary tree. The `preorderTraversal` function performs a preorder traversal of the binary tree, printing the value of each node as it is visited. Finally, in the `main` function, we create a binary tree, perform preorder traversal on it, and free the allocated memory to avoid memory leaks.

### 1. Algorithms & Data Structures (C++): Binary Trees: Preorder Traversal without using Recursion

Certainly! Performing a preorder traversal of a binary tree without using recursion typically involves using a stack to mimic the function call stack that recursion would create. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <stack>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

void preorderTraversal(TreeNode* root) {
    if (root == nullptr) return;

    stack<TreeNode*> nodeStack;
    nodeStack.push(root);

    while (!nodeStack.empty()) {
        TreeNode* node = nodeStack.top();
        nodeStack.pop();
        cout << node->val << " ";

        // Push right child first, so left child will be processed first
        if (node->right != nullptr) {
            nodeStack.push(node->right);
        }
        if (node->left != nullptr) {
            nodeStack.push(node->left);
        }
    }
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    cout << "Preorder traversal without recursion: ";
    preorderTraversal(root);

    // Clean up memory
    delete root->left->left;
    delete root->left->right;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

In this code:

- We use a stack to store the nodes we've encountered but haven't yet processed.
- We start with the root node, push it onto the stack.
- While the stack is not empty, we pop a node, visit it, and then push its right and left children onto the stack (if they exist). This is done to ensure that the left subtree is processed before the right subtree, which is the characteristic of preorder traversal.

### 1. Algorithms & Data Structures (C++): Binary Trees: Push() and Pop() during Iterative Preorder Traversal

In C++, implementing iterative preorder traversal, as well as push and pop operations on a binary tree, involves using a stack data structure. Here's how you can implement the push() and pop() operations during iterative preorder traversal:

```cpp
#include <iostream>
#include <stack>
using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

class BinaryTree {
public:
    // Function to perform iterative preorder traversal
    void iterativePreorder(TreeNode* root) {
        if (!root) return;
        stack<TreeNode*> stk;
        stk.push(root);
        while (!stk.empty()) {
            TreeNode* node = stk.top();
            stk.pop();
            cout << node->val << " "; // Process the current node
            // Push right child first so that it is processed after left child
            if (node->right) stk.push(node->right);
            if (node->left) stk.push(node->left);
        }
    }

    // Function to push a new node into the binary tree
    void push(TreeNode*& root, int val) {
        TreeNode* newNode = new TreeNode(val);
        if (!root) {
            root = newNode;
            return;
        }
        stack<TreeNode*> stk;
        stk.push(root);
        while (!stk.empty()) {
            TreeNode* node = stk.top();
            stk.pop();
            if (!node->left) {
                node->left = newNode;
                return;
            } else {
                stk.push(node->left);
            }
            if (!node->right) {
                node->right = newNode;
                return;
            } else {
                stk.push(node->right);
            }
        }
    }

    // Function to pop the last node from the binary tree
    void pop(TreeNode*& root) {
        if (!root) return;
        stack<TreeNode*> stk;
        stk.push(root);
        TreeNode* prev = nullptr;
        while (!stk.empty()) {
            TreeNode* node = stk.top();
            stk.pop();
            if (node->left) {
                if (node->left == prev) {
                    delete node->left;
                    node->left = nullptr;
                    return;
                }
                stk.push(node->left);
            }
            if (node->right) {
                if (node->right == prev) {
                    delete node->right;
                    node->right = nullptr;
                    return;
                }
                stk.push(node->right);
            }
            prev = node;
        }
    }
};

int main() {
    BinaryTree tree;
    TreeNode* root = nullptr;
    tree.push(root, 1);
    tree.push(root, 2);
    tree.push(root, 3);
    tree.iterativePreorder(root); // Output: 1 2 3
    cout << endl;
    tree.pop(root);
    tree.iterativePreorder(root); // Output: 1 2
    cout << endl;
    return 0;
}
```

In this implementation:

- `iterativePreorder` performs the iterative preorder traversal using a stack.
- `push` function inserts a new node into the binary tree.
- `pop` function removes the last node from the binary tree.

Both `push` and `pop` functions use a similar approach, where a stack is used to traverse the tree iteratively until a suitable position for insertion/deletion is found.

### 1. Algorithms & Data Structures (C++): Binary Trees: Space Complexity : All 3 Traversals

In algorithms and data structures, particularly when dealing with binary trees in C++, space complexity can vary depending on the traversal method used. Let's discuss the space complexity of all three traversals: pre-order, in-order, and post-order.

1. **Pre-order Traversal:**
   - Pre-order traversal visits the root node, then recursively traverses the left subtree, and finally the right subtree.
   - In terms of space complexity, pre-order traversal generally requires O(h) additional space, where 'h' is the height of the binary tree. This is because pre-order traversal typically uses a stack to store nodes as it traverses the tree.
   - The maximum space required for the stack is O(h) because in the worst case, the stack may hold all the nodes on the path from the root to the deepest leaf.

2. **In-order Traversal:**
   - In-order traversal first recursively traverses the left subtree, then visits the root node, and finally traverses the right subtree.
   - Similar to pre-order traversal, in-order traversal also requires O(h) additional space for the stack, where 'h' is the height of the binary tree.
   - Again, the stack's maximum space requirement is O(h) because it may hold all the nodes on the path from the root to the deepest leaf.

3. **Post-order Traversal:**
   - Post-order traversal first recursively traverses the left subtree, then the right subtree, and finally visits the root node.
   - Post-order traversal also requires O(h) additional space for the stack, where 'h' is the height of the binary tree.
   - Like pre-order and in-order traversals, the stack's maximum space requirement is O(h).

In summary, all three traversals (pre-order, in-order, and post-order) have the same space complexity of O(h), where 'h' is the height of the binary tree. This space is mainly due to the stack used for recursion. The worst-case space complexity occurs when the binary tree is skewed, leading to a height of 'n' (number of nodes), resulting in O(n) space complexity for the stack.

### 1. Algorithms & Data Structures (C++): Binary Trees: Time & Space Complexity : Iterative Postorder Traversal

Iterative postorder traversal of a binary tree is a technique to visit all nodes of the tree in a specific order: left child, right child, root. Unlike the recursive approach, which uses function call stack, the iterative approach typically uses an auxiliary data structure like a stack or deque to simulate the call stack behavior.

Here's a brief overview of the time and space complexity of iterative postorder traversal:

#### Time Complexity

- **Best Case:** O(n) - This occurs when every node has both left and right children.
- **Average Case:** O(n) - Similar to the best case, on average, every node will be visited once.
- **Worst Case:** O(n) - This happens when the tree is skewed to the left or right, essentially becoming a linked list. In this case, each node will be visited once.

#### Space Complexity

- **Space Complexity:** O(h) - where h is the height of the binary tree.
  - In the worst-case scenario, when the binary tree is skewed, the space complexity can be O(n).
  - In the best-case scenario, when the binary tree is balanced, the space complexity can be O(log n).

#### Iterative Postorder Traversal Algorithm (Using Two Stacks)

1. Start with an empty stack.
2. Push the root node onto the stack.
3. Create a second stack to store the postorder traversal.
4. While the first stack is not empty, do the following:
   - Pop a node from the first stack and push it onto the second stack.
   - Push the left child and then the right child of the popped node onto the first stack.
5. Once all nodes have been processed, pop nodes from the second stack to get the postorder traversal.

This approach doesn't require recursion and uses two stacks to keep track of nodes and their order.

Implementing this approach involves a loop that traverses each node once and a stack to store nodes. Therefore, the time complexity is O(n), where n is the number of nodes in the tree. The space complexity depends on the height of the tree and can range from O(log n) to O(n).

### 1. Algorithms & Data Structures (C++): Binary Trees: Time & Space Complexity : Iterative Preorder Traversal

In iterative preorder traversal of a binary tree, you visit each node of the tree in a specific order: first the current node, then its left subtree, and finally its right subtree. This traversal technique can be implemented using a stack data structure to mimic the recursive approach.

Here's a basic outline of the iterative preorder traversal algorithm for a binary tree implemented in C++:

```cpp
#include <iostream>
#include <stack>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

void iterativePreorder(TreeNode* root) {
    if (root == nullptr) return;

    stack<TreeNode*> nodeStack;
    nodeStack.push(root);

    while (!nodeStack.empty()) {
        TreeNode* currentNode = nodeStack.top();
        nodeStack.pop();
        cout << currentNode->val << " ";

        // Push the right child first so that it is processed after the left child.
        if (currentNode->right)
            nodeStack.push(currentNode->right);
        if (currentNode->left)
            nodeStack.push(currentNode->left);
    }
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    cout << "Iterative Preorder Traversal: ";
    iterativePreorder(root);
    
    return 0;
}
```

**Time Complexity:**

- Since each node is visited once, the time complexity of iterative preorder traversal of a binary tree is O(n), where n is the number of nodes in the tree.

**Space Complexity:**

- The space complexity is O(h), where h is the height of the binary tree.
- In the worst case, the height of the stack can be equal to the height of the binary tree, which occurs in the case of a skewed tree. In the average case, the space complexity is O(log n) for a balanced binary tree.

### 1. Algorithms & Data Structures (C++): Binary Trees: Time & Space Complexity : Level Order Traversal

In binary trees, level order traversal, also known as breadth-first traversal, involves visiting all the nodes of a tree level by level, from left to right. This traversal can be implemented using various data structures such as queues. Let's break down the time and space complexity of level order traversal in a binary tree implemented in C++:

#### Time Complexity

The time complexity of level order traversal in a binary tree is O(n), where n is the number of nodes in the tree. This is because we need to visit each node exactly once.

#### Space Complexity

1. **Using a Queue:**
   - In the typical implementation using a queue, the space complexity is O(w), where w is the maximum width of the binary tree (i.e., the maximum number of nodes at any level).
   - In the worst-case scenario, the width of a binary tree can be equal to the number of nodes at the last level. Therefore, the space complexity in this case can be O(n/2) ≈ O(n), where n is the total number of nodes in the tree.

2. **Using Recursion:**
   - If we implement level order traversal using recursion, the space complexity will be O(h), where h is the height of the binary tree.
   - In the worst case, for a skewed binary tree, the height of the tree can be equal to the number of nodes in the tree. Therefore, the space complexity in this case can be O(n), where n is the total number of nodes in the tree.

#### C++ Implementation Using Queue

```cpp
#include <iostream>
#include <queue>
using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

void levelOrder(TreeNode* root) {
    if (root == NULL)
        return;

    queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        TreeNode* node = q.front();
        q.pop();
        cout << node->val << " ";

        if (node->left != NULL)
            q.push(node->left);
        if (node->right != NULL)
            q.push(node->right);
    }
}

int main() {
    // Example Usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    cout << "Level Order Traversal: ";
    levelOrder(root);

    return 0;
}
```

This implementation utilizes a queue to perform level order traversal. It has a time complexity of O(n) and a space complexity of O(n) in the worst case.

### 1. Algorithms & Data Structures (C++): Binary Trees: Time Complexity : All 3 Traversals

In the context of binary trees, there are three common types of traversals: in-order, pre-order, and post-order. Here's a brief explanation of each traversal type and its time complexity in terms of Big O notation:

1. **In-order Traversal**:
   - Visit the left subtree.
   - Visit the root node.
   - Visit the right subtree.

   Time Complexity: O(n)
   - In an in-order traversal, you visit every node exactly once, so the time complexity is linear in terms of the number of nodes (n).

2. **Pre-order Traversal**:
   - Visit the root node.
   - Visit the left subtree.
   - Visit the right subtree.

   Time Complexity: O(n)
   - Similar to in-order traversal, pre-order traversal also visits every node exactly once, leading to a linear time complexity.

3. **Post-order Traversal**:
   - Visit the left subtree.
   - Visit the right subtree.
   - Visit the root node.

   Time Complexity: O(n)
   - Like the other two traversal types, post-order traversal involves visiting every node exactly once, resulting in linear time complexity.

In each traversal type, you're visiting every node once, so the time complexity for all three traversals is O(n), where n is the number of nodes in the binary tree.

### 1. Algorithms & Data Structures (C++): Binary Trees: Tree Traversal and its Types

In C++, binary tree traversal is a fundamental operation that involves visiting each node exactly once in a specific order. There are three main types of binary tree traversals: preorder, inorder, and postorder.

Let's start with the definition of a binary tree node in C++:

```cpp
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};
```

Now, let's see how each traversal type works:

1. **Preorder Traversal**: In preorder traversal, we visit the root node first, then recursively visit the left subtree, and finally the right subtree.

```cpp
void preorderTraversal(TreeNode* root) {
    if (root == nullptr) return;
    cout << root->val << " "; // Process the current node
    preorderTraversal(root->left); // Recursively traverse left subtree
    preorderTraversal(root->right); // Recursively traverse right subtree
}
```

1. **Inorder Traversal**: In inorder traversal, we recursively visit the left subtree, then visit the root node, and finally the right subtree.

```cpp
void inorderTraversal(TreeNode* root) {
    if (root == nullptr) return;
    inorderTraversal(root->left); // Recursively traverse left subtree
    cout << root->val << " "; // Process the current node
    inorderTraversal(root->right); // Recursively traverse right subtree
}
```

1. **Postorder Traversal**: In postorder traversal, we recursively visit the left subtree, then the right subtree, and finally the root node.

```cpp
void postorderTraversal(TreeNode* root) {
    if (root == nullptr) return;
    postorderTraversal(root->left); // Recursively traverse left subtree
    postorderTraversal(root->right); // Recursively traverse right subtree
    cout << root->val << " "; // Process the current node
}
```

These functions can be called with the root of the binary tree to perform the respective traversal. Each traversal has its own use cases depending on the problem you are trying to solve.

### 1. Algorithms & Data Structures (C++): Constructing/Generating a Unique Binary Tree from Traversals

Constructing a binary tree from its traversals, such as pre-order, in-order, or post-order, is a common problem in computer science. Each traversal provides different pieces of information about the structure of the tree. For simplicity, let's consider constructing a binary tree from its pre-order and in-order traversals.

In pre-order traversal, the root node is visited first, followed by the left subtree, and then the right subtree. In in-order traversal, the left subtree is visited first, then the root node, and finally the right subtree.

Here's a general approach in C++:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        // Construct a hashmap to store the index of each element in inorder traversal
        unordered_map<int, int> inorder_map;
        for (int i = 0; i < inorder.size(); ++i) {
            inorder_map[inorder[i]] = i;
        }
        // Construct the tree recursively
        return buildTreeHelper(preorder, 0, preorder.size() - 1, inorder, 0, inorder.size() - 1, inorder_map);
    }
    
    TreeNode* buildTreeHelper(vector<int>& preorder, int pre_start, int pre_end, vector<int>& inorder, int in_start, int in_end, unordered_map<int, int>& inorder_map) {
        if (pre_start > pre_end || in_start > in_end) return nullptr;
        
        // Root node is the first element in preorder
        TreeNode* root = new TreeNode(preorder[pre_start]);
        
        // Find the index of root node in inorder traversal
        int root_index_inorder = inorder_map[root->val];
        
        // Calculate the number of nodes in the left subtree
        int num_left_nodes = root_index_inorder - in_start;
        
        // Recursively build left and right subtrees
        root->left = buildTreeHelper(preorder, pre_start + 1, pre_start + num_left_nodes, inorder, in_start, root_index_inorder - 1, inorder_map);
        root->right = buildTreeHelper(preorder, pre_start + num_left_nodes + 1, pre_end, inorder, root_index_inorder + 1, in_end, inorder_map);
        
        return root;
    }
};

// Utility function to print the tree in inorder traversal
void printInorder(TreeNode* root) {
    if (root == nullptr) return;
    printInorder(root->left);
    cout << root->val << " ";
    printInorder(root->right);
}

int main() {
    vector<int> preorder = {3, 9, 20, 15, 7};
    vector<int> inorder = {9, 3, 15, 20, 7};

    Solution solution;
    TreeNode* root = solution.buildTree(preorder, inorder);

    cout << "Inorder traversal of constructed tree: ";
    printInorder(root);
    cout << endl;

    return 0;
}
```

This code defines a `Solution` class with a `buildTree` method that constructs a binary tree from its preorder and inorder traversals. The `buildTreeHelper` method is a recursive function that builds the tree by dividing the traversals into left and right subtrees. Finally, the `main` function demonstrates how to use this solution by providing sample preorder and inorder traversals and printing the inorder traversal of the constructed tree.

You can adjust the code accordingly if you have different traversal inputs or need to construct the tree from post-order traversal as well.

### 1. Algorithms & Data Structures (C++): Easy way of remembering Binary Trees Traversals

Certainly! Binary tree traversals can be remembered using simple patterns or mnemonics. In C++, the three main traversals are:

1. **Inorder Traversal (Left, Root, Right)**:
   - To remember the order, think of it as "In-Order", where you first go left, then visit the root, and finally go right.
   - Recursive Implementation:

     ```cpp
     void inorderTraversal(TreeNode* root) {
         if (root != nullptr) {
             inorderTraversal(root->left);
             cout << root->val << " ";
             inorderTraversal(root->right);
         }
     }
     ```

2. **Preorder Traversal (Root, Left, Right)**:
   - Think of it as "Pre-Order", where you visit the root first, then go left, and finally go right.
   - Recursive Implementation:

     ```cpp
     void preorderTraversal(TreeNode* root) {
         if (root != nullptr) {
             cout << root->val << " ";
             preorderTraversal(root->left);
             preorderTraversal(root->right);
         }
     }
     ```

3. **Postorder Traversal (Left, Right, Root)**:
   - Think of it as "Post-Order", where you first go left, then go right, and finally visit the root.
   - Recursive Implementation:

     ```cpp
     void postorderTraversal(TreeNode* root) {
         if (root != nullptr) {
             postorderTraversal(root->left);
             postorderTraversal(root->right);
             cout << root->val << " ";
         }
     }
     ```

Remembering them in this order - Inorder, Preorder, Postorder - can also help because it follows a natural progression of visiting nodes. You can also try to remember them alphabetically: Inorder, Postorder, Preorder, or by the order of steps: Left, Right, Root.

With some practice, these traversals will become more intuitive and easier to remember!

### 1. Algorithms & Data Structures (C++): Function for Inorder Traversal

Sure, here's an example of a function for performing an inorder traversal of a binary tree in C++:

```cpp
#include <iostream>

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void inorderTraversal(TreeNode* root) {
    if (root == nullptr) return;

    // Traverse left subtree
    inorderTraversal(root->left);

    // Visit current node
    std::cout << root->val << " ";

    // Traverse right subtree
    inorderTraversal(root->right);
}

int main() {
    // Creating a binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    std::cout << "Inorder Traversal: ";
    inorderTraversal(root);
    std::cout << std::endl;

    return 0;
}
```

In this code:

- We define a `TreeNode` struct to represent each node of the binary tree.
- The `inorderTraversal` function recursively traverses the tree in inorder manner.
- In the `main` function, we create a binary tree and call the `inorderTraversal` function to perform the traversal.

This code outputs the inorder traversal of the binary tree. You can modify the `TreeNode` struct and the `main` function to create and traverse different binary trees as needed.

### 1. Algorithms & Data Structures (C++): Function for Postorder Traversal

Certainly! Here's a C++ function for performing a postorder traversal of a binary tree:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void postorderTraversal(TreeNode* root) {
    if (root == nullptr) return;

    // Traverse left subtree
    postorderTraversal(root->left);

    // Traverse right subtree
    postorderTraversal(root->right);

    // Visit the current node
    std::cout << root->val << " ";
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    std::cout << "Postorder traversal: ";
    postorderTraversal(root);

    return 0;
}
```

This function recursively traverses the binary tree in postorder, visiting the left subtree, then the right subtree, and finally the root node. In the `main()` function, an example binary tree is created and its postorder traversal is printed.

### 1. Algorithms & Data Structures (C++): Function for Preorder Traversal

Sure! Below is an example of a C++ function for performing a preorder traversal on a binary tree:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void preorderTraversal(TreeNode* root) {
    if (root == nullptr)
        return;

    // Print the current node's value
    std::cout << root->val << " ";

    // Traverse left subtree
    preorderTraversal(root->left);

    // Traverse right subtree
    preorderTraversal(root->right);
}

int main() {
    // Create a sample binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    // Perform preorder traversal
    std::cout << "Preorder traversal: ";
    preorderTraversal(root);

    return 0;
}
```

This code defines a simple binary tree structure and a function `preorderTraversal` to perform the preorder traversal. The function starts from the root node, prints its value, then recursively traverses the left subtree and then the right subtree, printing the value of each node encountered. Finally, the `main` function creates a sample binary tree, calls the `preorderTraversal` function on the root node, and prints the result.

### 1. Algorithms & Data Structures (C++): In-order Traversal Technique

In C++, the in-order traversal technique is a fundamental method used to traverse a binary tree. In this technique, the nodes are traversed in the order of left child, root, and then right child. This traversal technique is commonly used to retrieve data from a binary search tree in sorted order.

Here's how you can implement the in-order traversal technique recursively in C++:

```cpp
#include <iostream>

// Definition of a binary tree node
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to perform in-order traversal recursively
void inOrderTraversal(TreeNode* root) {
    if (root == nullptr) return;
    
    // Traverse the left subtree
    inOrderTraversal(root->left);
    
    // Visit the current node
    std::cout << root->val << " ";
    
    // Traverse the right subtree
    inOrderTraversal(root->right);
}

// Main function
int main() {
    // Create a binary tree
    TreeNode* root = new TreeNode(5);
    root->left = new TreeNode(3);
    root->right = new TreeNode(8);
    root->left->left = new TreeNode(2);
    root->left->right = new TreeNode(4);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(9);
    
    // Perform in-order traversal
    std::cout << "In-order traversal: ";
    inOrderTraversal(root);
    std::cout << std::endl;
    
    // Clean up memory
    // (In a real application, you might want to use smart pointers or implement proper memory management)
    delete root->right->right;
    delete root->right->left;
    delete root->left->right;
    delete root->left->left;
    delete root->right;
    delete root->left;
    delete root;
    
    return 0;
}
```

This code defines a binary tree node struct and a function `inOrderTraversal()` to perform the in-order traversal recursively. The `main()` function creates a binary tree, performs the in-order traversal, and then cleans up the allocated memory.

### 1. Algorithms & Data Structures (C++): Inorder Binary Tree Traversals

In C++, performing an inorder traversal of a binary tree is a common operation. An inorder traversal visits the nodes of a binary tree in the order: left, root, right. Here's how you can implement it using a recursive approach:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void inorderTraversal(TreeNode* root) {
    if (root == nullptr)
        return;
    // Traverse the left subtree
    inorderTraversal(root->left);
    // Visit the current node
    std::cout << root->val << " ";
    // Traverse the right subtree
    inorderTraversal(root->right);
}

// Example usage
int main() {
    // Create a binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    // Perform inorder traversal
    std::cout << "Inorder traversal: ";
    inorderTraversal(root);
    std::cout << std::endl;

    // Cleanup (optional)
    delete root->left->left;
    delete root->left->right;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

This code defines a `TreeNode` structure representing a node in the binary tree. The `inorderTraversal` function recursively traverses the tree in inorder fashion, printing the value of each node. In the `main` function, we create a sample binary tree, perform the inorder traversal, and then clean up the allocated memory.

Alternatively, you can implement the same algorithm iteratively using a stack data structure to simulate the recursion. Let me know if you want to see that implementation too!

### 1. Algorithms & Data Structures (C++): Inorder Traversal

In computer science, specifically in the context of tree data structures, the inorder traversal is a method used to visit all nodes in a binary tree. It's called "inorder" because the traversal visits nodes in the following order:

1. Left subtree
2. Root node
3. Right subtree

Here's how you can implement an inorder traversal in C++ using recursion:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void inorderTraversal(TreeNode* root) {
    if (root == nullptr) {
        return;
    }

    // Traverse left subtree
    inorderTraversal(root->left);

    // Visit the current node
    std::cout << root->val << " ";

    // Traverse right subtree
    inorderTraversal(root->right);
}

int main() {
    // Example usage:
    // Constructing a binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    std::cout << "Inorder traversal: ";
    inorderTraversal(root);
    std::cout << std::endl;

    // Remember to free the memory to avoid memory leaks
    delete root->left->left;
    delete root->left->right;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

This code first defines the `TreeNode` structure to represent a node in the binary tree. Then, the `inorderTraversal` function is defined recursively to traverse the tree in the specified order. Finally, in the `main` function, an example binary tree is constructed and its inorder traversal is printed. Make sure to free the allocated memory for the tree nodes to prevent memory leaks.

### 1. Algorithms & Data Structures (C++): InOrder Traversal Binary Tree

In C++, an in-order traversal of a binary tree visits the nodes in the following order: left child, parent, right child. Here's a simple implementation using a recursive approach:

```cpp
#include <iostream>

// Define the structure of a binary tree node
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to perform in-order traversal of a binary tree
void inOrderTraversal(TreeNode* root) {
    if (root == nullptr) return;

    // Traverse the left subtree
    inOrderTraversal(root->left);

    // Visit the current node
    std::cout << root->val << " ";

    // Traverse the right subtree
    inOrderTraversal(root->right);
}

// Function to create a new binary tree node
TreeNode* createNode(int val) {
    return new TreeNode(val);
}

int main() {
    // Create a sample binary tree
    TreeNode* root = createNode(1);
    root->left = createNode(2);
    root->right = createNode(3);
    root->left->left = createNode(4);
    root->left->right = createNode(5);

    // Perform in-order traversal
    std::cout << "In-order traversal: ";
    inOrderTraversal(root);
    std::cout << std::endl;

    return 0;
}
```

This program creates a simple binary tree and performs an in-order traversal, printing the values of the nodes as they are visited. You can modify the `createNode` function to create a binary tree of your choice for testing.

### 1. Algorithms & Data Structures (C++): Iterative InOrder Traversal of a Binary Tree

Iterative InOrder traversal of a binary tree can be implemented using a stack. Here's a simple C++ implementation:

```cpp
#include <iostream>
#include <stack>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

void iterativeInOrder(TreeNode* root) {
    if (root == nullptr) return;

    stack<TreeNode*> st;
    TreeNode* current = root;

    while (current != nullptr || !st.empty()) {
        // Traverse to the leftmost node of the current subtree
        while (current != nullptr) {
            st.push(current);
            current = current->left;
        }

        // Current is now null, meaning we've reached the leftmost node
        // Pop the top node from stack and print it
        current = st.top();
        st.pop();
        cout << current->val << " ";

        // Move to the right subtree
        current = current->right;
    }
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    cout << "InOrder Traversal (iterative): ";
    iterativeInOrder(root);
    cout << endl;

    // Don't forget to deallocate memory
    delete root->left->left;
    delete root->left->right;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

This code demonstrates an iterative InOrder traversal of a binary tree using a stack. The algorithm first traverses to the leftmost node of the current subtree, pushing all encountered nodes onto a stack. Then, it pops nodes from the stack, prints them, and moves to the right subtree of the popped node. This process continues until all nodes are traversed.

### 1. Algorithms & Data Structures (C++): Iterative PreOrder Traversal of a Binary Tree

Iterative PreOrder traversal of a binary tree involves visiting each node in the tree in the order of root, left subtree, and then right subtree, all done iteratively without using recursion. In C++, you can implement this using a stack data structure. Here's how you can do it:

```cpp
#include <iostream>
#include <stack>
using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

void iterativePreOrder(TreeNode* root) {
    if (root == nullptr)
        return;

    stack<TreeNode*> nodeStack;
    nodeStack.push(root);

    while (!nodeStack.empty()) {
        TreeNode* current = nodeStack.top();
        cout << current->val << " ";
        nodeStack.pop();

        // Push right child first and then left child
        if (current->right)
            nodeStack.push(current->right);
        if (current->left)
            nodeStack.push(current->left);
    }
}

int main() {
    /* Constructed binary tree is
                 1
               /   \
              2     3
             / \
            4   5   */
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    cout << "PreOrder Traversal of binary tree using iterative method:\n";
    iterativePreOrder(root);

    return 0;
}
```

This code implements the iterative PreOrder traversal of a binary tree using a stack. We start with the root node and push it onto the stack. Then, while the stack is not empty, we pop a node from the stack, print its value, and push its right child and left child (if they exist) onto the stack. This way, we ensure that the left child is visited before the right child.

### 1. Algorithms & Data Structures (C++): Level Order Traversal

Level order traversal is a fundamental algorithm used to visit all nodes of a binary tree or a binary search tree (BST) in a breadth-first manner. It starts at the root and visits all nodes at each level before moving to the next level.

In C++, you can implement level order traversal using a queue data structure. Here's a basic implementation for a binary tree:

```cpp
#include <iostream>
#include <queue>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void levelOrder(TreeNode* root) {
    if (root == nullptr) return;

    queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        int levelSize = q.size(); // Number of nodes at the current level

        // Traverse all nodes at the current level
        for (int i = 0; i < levelSize; ++i) {
            TreeNode* node = q.front();
            q.pop();
            cout << node->val << " ";

            // Enqueue the left and right children if they exist
            if (node->left != nullptr)
                q.push(node->left);
            if (node->right != nullptr)
                q.push(node->right);
        }

        cout << endl; // Move to the next level
    }
}

int main() {
    /* Constructed binary tree is:
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

    cout << "Level order traversal of binary tree:" << endl;
    levelOrder(root);

    return 0;
}
```

This code defines a binary tree node struct `TreeNode` and implements the `levelOrder` function to perform level order traversal. The `main` function creates a binary tree and calls the `levelOrder` function to print its level order traversal.

### 1. Algorithms & Data Structures (C++): Level Order Traversal of a Binary Tree

Level order traversal of a binary tree, also known as breadth-first traversal, visits nodes level by level, starting from the root node. Here's a C++ implementation using a queue:

```cpp
#include <iostream>
#include <queue>

using namespace std;

// Binary tree node structure
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to perform level order traversal of a binary tree
void levelOrder(TreeNode* root) {
    if (root == nullptr)
        return;

    queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        TreeNode* current = q.front();
        q.pop();
        cout << current->val << " ";

        if (current->left != nullptr)
            q.push(current->left);
        if (current->right != nullptr)
            q.push(current->right);
    }
}

int main() {
    // Create a sample binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(7);

    // Perform level order traversal
    cout << "Level Order Traversal: ";
    levelOrder(root);

    return 0;
}
```

This code defines a `TreeNode` structure representing a node in the binary tree. The `levelOrder` function performs level order traversal using a queue data structure. Finally, in the `main` function, a sample binary tree is created, and the level order traversal is performed starting from the root node.

### 1. Algorithms & Data Structures (C++): LevelOrder Traversal Binary Tree

Certainly! Level order traversal, also known as breadth-first traversal, is a method used to traverse and visit all the nodes of a binary tree level by level, from left to right. Here's how you can implement it in C++ using a queue for traversal:

```cpp
#include <iostream>
#include <queue>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

void levelOrder(TreeNode* root) {
    if (root == NULL)
        return;

    queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        TreeNode* current = q.front();
        q.pop();

        cout << current->val << " ";

        if (current->left != NULL)
            q.push(current->left);

        if (current->right != NULL)
            q.push(current->right);
    }
}

int main() {
    /* Example binary tree:
                1
               / \
              2   3
             / \
            4   5
    */

    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    cout << "Level Order traversal of binary tree is: ";
    levelOrder(root);
    cout << endl;

    return 0;
}
```

In this code:

1. We define a `TreeNode` struct to represent each node in the binary tree.
2. The `levelOrder` function performs level order traversal using a queue data structure.
3. We initialize a queue and push the root node into it.
4. We iterate over the queue until it becomes empty, processing each node:
   - Pop the front node of the queue.
   - Print its value.
   - If it has left and/or right children, push them into the queue.
5. In the `main` function, we create an example binary tree and call the `levelOrder` function to print its level order traversal.

### 1. Algorithms & Data Structures (C++): PostOrder Traversal Binary Tree

Sure, the postorder traversal of a binary tree is a way of visiting each node in a specific order: first the left subtree, then the right subtree, and finally the root node. Here's a C++ implementation of postorder traversal for a binary tree using recursion:

```cpp
#include <iostream>

// Define the structure of a binary tree node
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to perform postorder traversal recursively
void postorderTraversal(TreeNode* root) {
    if (root == nullptr) {
        return;
    }
    // Traverse left subtree
    postorderTraversal(root->left);
    // Traverse right subtree
    postorderTraversal(root->right);
    // Visit current node
    std::cout << root->val << " ";
}

int main() {
    // Create a sample binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    std::cout << "Postorder Traversal: ";
    postorderTraversal(root);
    std::cout << std::endl;

    // Free memory
    delete root->left->right;
    delete root->left->left;
    delete root->right;
    delete root->left;
    delete root;

    return 0;
}
```

This code defines a `TreeNode` structure to represent each node in the binary tree. The `postorderTraversal` function is then defined recursively to traverse the tree in postorder, printing out the value of each node as it is visited. Finally, in the `main` function, a sample binary tree is created, and its postorder traversal is printed.

You can run this code to see the postorder traversal of a binary tree.

### 1. Algorithms & Data Structures (C++): PostOrder Traversal of a Binary Tree

Certainly! Postorder traversal is a method of traversing through a binary tree where you visit the left subtree, then the right subtree, and finally the root node. Here's how you can implement postorder traversal of a binary tree in C++:

```cpp
#include <iostream>
using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

void postorderTraversal(TreeNode* root) {
    if (root == NULL) return;

    // Traverse the left subtree
    postorderTraversal(root->left);

    // Traverse the right subtree
    postorderTraversal(root->right);

    // Visit the root node
    cout << root->val << " ";
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    cout << "Postorder traversal: ";
    postorderTraversal(root);
    cout << endl;

    return 0;
}
```

In this code:

- We define a `TreeNode` struct to represent nodes in the binary tree.
- The `postorderTraversal` function takes a pointer to the root of the binary tree and performs postorder traversal recursively.
- The function first traverses the left subtree, then the right subtree, and finally visits the root node.
- In the `main` function, we create an example binary tree and call the `postorderTraversal` function to perform postorder traversal.

Feel free to adjust the code according to your needs or integrate it into your existing codebase!

### 1. Algorithms & Data Structures (C++): Preorder Binary Tree Traversal

Sure, I can help you with that! A preorder traversal is a type of depth-first traversal where you visit each node in the tree in the following order: root, left subtree, right subtree. In C++, you can implement preorder traversal of a binary tree using recursion. Here's how you can do it:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to perform preorder traversal
void preorderTraversal(TreeNode* root) {
    if (root == nullptr) {
        return;
    }

    // Visit the current node
    std::cout << root->val << " ";

    // Traverse left subtree
    preorderTraversal(root->left);

    // Traverse right subtree
    preorderTraversal(root->right);
}

int main() {
    // Example usage
    // Constructing a binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    std::cout << "Preorder traversal of the binary tree: ";
    preorderTraversal(root);
    std::cout << std::endl;

    // Clean up memory (freeing dynamically allocated nodes)
    delete root->left->left;
    delete root->left->right;
    delete root->left;
    delete root->right;
    delete root;

    return 0;
}
```

In this code:

1. We define a `TreeNode` struct to represent a node in the binary tree.
2. We define the `preorderTraversal` function which takes a pointer to the root of the binary tree as an argument and performs a preorder traversal.
3. In the `preorderTraversal` function, we first check if the root is `nullptr`, if so, we return immediately.
4. Then, we visit the current node by printing its value.
5. Next, we recursively call `preorderTraversal` on the left subtree of the current node.
6. Finally, we recursively call `preorderTraversal` on the right subtree of the current node.
7. In the `main` function, we construct an example binary tree and perform a preorder traversal on it. Finally, we clean up the dynamically allocated memory to avoid memory leaks.

### 1. Algorithms & Data Structures (C++): PreOrder Traversal

Preorder traversal is a type of tree traversal algorithm that visits the nodes in the order: root, left subtree, right subtree. Here's a basic implementation of preorder traversal for a binary tree in C++:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void preorderTraversal(TreeNode* root) {
    if (root == nullptr) {
        return;
    }
    // Visit the root node
    std::cout << root->val << " ";
    // Traverse left subtree
    preorderTraversal(root->left);
    // Traverse right subtree
    preorderTraversal(root->right);
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    std::cout << "Preorder traversal: ";
    preorderTraversal(root);

    return 0;
}
```

This code defines a simple binary tree structure (`TreeNode`) and the `preorderTraversal` function to perform the preorder traversal recursively. In the `main` function, an example binary tree is created, and the `preorderTraversal` function is called to print out the preorder traversal of the tree.

### 1. Algorithms & Data Structures (C++): PreOrder Traversal Binary Tree

In C++, a pre-order traversal of a binary tree involves visiting the root node first, then recursively traversing the left subtree, and finally the right subtree. Here's a basic implementation:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to perform preorder traversal of a binary tree
void preorderTraversal(TreeNode* root) {
    if (root == nullptr) return;
    
    // Visit the root node
    std::cout << root->val << " ";
    
    // Traverse left subtree
    preorderTraversal(root->left);
    
    // Traverse right subtree
    preorderTraversal(root->right);
}

int main() {
    // Creating a sample binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    
    std::cout << "Preorder traversal of binary tree: ";
    preorderTraversal(root);
    std::cout << std::endl;
    
    return 0;
}
```

This code defines a simple binary tree structure and implements a preorder traversal function `preorderTraversal`. The `main` function demonstrates its usage by creating a binary tree and calling the preorder traversal function on it.

### 1. Algorithms & Data Structures (C++): PreOrder Traversal of a Binary Tree

Certainly! Pre-order traversal is one of the fundamental algorithms used to traverse a binary tree. In pre-order traversal, you visit the root node first, then recursively traverse the left subtree, and finally traverse the right subtree. Here's how you can implement pre-order traversal of a binary tree in C++:

```cpp
#include <iostream>

// Definition of a binary tree node
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Function to perform pre-order traversal of a binary tree
void preorderTraversal(TreeNode* root) {
    if (root == nullptr)
        return;

    // Print the value of the current node
    std::cout << root->val << " ";

    // Recursively traverse the left subtree
    preorderTraversal(root->left);

    // Recursively traverse the right subtree
    preorderTraversal(root->right);
}

int main() {
    // Example usage
    // Create a binary tree
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    // Perform pre-order traversal
    std::cout << "Preorder traversal: ";
    preorderTraversal(root);
    std::cout << std::endl;

    return 0;
}
```

In this code:

- We define a struct `TreeNode` to represent a node in the binary tree, containing an integer value and pointers to its left and right children.
- The `preorderTraversal` function takes a pointer to the root of the binary tree and recursively performs the pre-order traversal, printing the value of each node.
- In the `main` function, we create an example binary tree and call `preorderTraversal` on its root to demonstrate the pre-order traversal.

You can customize the `TreeNode` struct and the example binary tree according to your requirements.

### 1. Algorithms & Data Structures (C++): Reverse Level Order Traversal

Reverse level order traversal is a tree traversal algorithm that visits the nodes of a binary tree level by level from bottom to top, i.e., starting from the deepest level and moving upwards towards the root. Here's a C++ implementation of the reverse level order traversal algorithm using a queue and a stack:

```cpp
#include <iostream>
#include <queue>
#include <stack>

using namespace std;

// Binary Tree Node
struct Node {
    int data;
    Node* left;
    Node* right;

    Node(int value) : data(value), left(nullptr), right(nullptr) {}
};

// Function to perform reverse level order traversal
void reverseLevelOrderTraversal(Node* root) {
    if (root == nullptr)
        return;

    queue<Node*> q;
    stack<Node*> s;
    q.push(root);

    // Traverse the tree level by level and push nodes to the stack
    while (!q.empty()) {
        Node* current = q.front();
        q.pop();
        s.push(current);

        // Enqueue the children of the current node
        if (current->right != nullptr)
            q.push(current->right);
        if (current->left != nullptr)
            q.push(current->left);
    }

    // Pop nodes from the stack to print in reverse order
    while (!s.empty()) {
        Node* current = s.top();
        cout << current->data << " ";
        s.pop();
    }
}

int main() {
    // Example binary tree
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    root->right->left = new Node(6);
    root->right->right = new Node(7);

    cout << "Reverse Level Order Traversal: ";
    reverseLevelOrderTraversal(root);
    cout << endl;

    return 0;
}
```

This code defines a `Node` structure for the binary tree and provides a function `reverseLevelOrderTraversal` to perform the reverse level order traversal. The traversal is done using a queue to keep track of nodes at each level and a stack to reverse the order of nodes. Finally, it prints the elements in reverse level order.

### 1. Algorithms & Data Structures (C++): Vertical Order Traversal

Vertical order traversal is a way to traverse a binary tree in a top-down manner where nodes at the same horizontal distance from the root are grouped together. For each group of nodes at the same horizontal distance, we visit them from top to bottom.

In C++, you can implement vertical order traversal using a map or unordered_map to store nodes at each horizontal distance. Here's a basic implementation:

```cpp
#include <iostream>
#include <vector>
#include <map>
#include <queue>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

vector<vector<int>> verticalTraversal(TreeNode* root) {
    vector<vector<int>> result;
    if (!root) return result;

    map<int, vector<int>> columns; // map to store nodes at each horizontal distance
    queue<pair<TreeNode*, int>> q; // queue for level order traversal

    q.push({root, 0}); // root has horizontal distance 0

    while (!q.empty()) {
        int size = q.size();
        map<int, vector<int>> temp; // temporary map to store nodes at current level

        for (int i = 0; i < size; ++i) {
            TreeNode* node = q.front().first;
            int col = q.front().second;
            q.pop();

            temp[col].push_back(node->val);

            if (node->left)
                q.push({node->left, col - 1}); // decrease horizontal distance for left child
            if (node->right)
                q.push({node->right, col + 1}); // increase horizontal distance for right child
        }

        // Merge temp into columns
        for (auto& entry : temp) {
            sort(entry.second.begin(), entry.second.end()); // sort nodes at same horizontal distance
            columns[entry.first].insert(columns[entry.first].end(), entry.second.begin(), entry.second.end());
        }
    }

    // Fill result vector from the map
    for (auto& entry : columns) {
        result.push_back(entry.second);
    }

    return result;
}

// Function to create a new TreeNode
TreeNode* createNode(int val) {
    return new TreeNode(val);
}

// Driver code
int main() {
    // Create a binary tree
    TreeNode* root = createNode(3);
    root->left = createNode(9);
    root->right = createNode(20);
    root->right->left = createNode(15);
    root->right->right = createNode(7);

    // Perform vertical order traversal
    vector<vector<int>> result = verticalTraversal(root);

    // Print the result
    cout << "Vertical Order Traversal:" << endl;
    for (const auto& col : result) {
        for (int val : col) {
            cout << val << " ";
        }
        cout << endl;
    }

    return 0;
}
```

This implementation uses level order traversal (BFS) and maintains a map to store nodes at each horizontal distance from the root. Finally, it constructs the result vector from the map. This code assumes that you already have a binary tree defined with TreeNode structure.

### 1. Algorithms & Data Structures (C++): Traversal Operation

Traversal operations are fundamental in algorithms and data structures, allowing us to visit and process each node or element in a data structure in a specific order. In the context of trees and graphs, traversal refers to the process of visiting all nodes/vertices in the structure exactly once.

In C++, traversal operations are commonly implemented using recursion or iterative techniques, depending on the specific data structure and traversal order desired. Here are some common traversal operations:

1. **Inorder Traversal**: For binary trees, visits nodes in the following order: left subtree, root, right subtree.

```cpp
void inorderTraversal(Node* root) {
    if (root == nullptr) return;
    inorderTraversal(root->left);
    cout << root->data << " ";
    inorderTraversal(root->right);
}
```

1. **Preorder Traversal**: Visits nodes in the following order: root, left subtree, right subtree.

```cpp
void preorderTraversal(Node* root) {
    if (root == nullptr) return;
    cout << root->data << " ";
    preorderTraversal(root->left);
    preorderTraversal(root->right);
}
```

1. **Postorder Traversal**: Visits nodes in the following order: left subtree, right subtree, root.

```cpp
void postorderTraversal(Node* root) {
    if (root == nullptr) return;
    postorderTraversal(root->left);
    postorderTraversal(root->right);
    cout << root->data << " ";
}
```

1. **Level Order Traversal (Breadth-First Traversal)**: Visits nodes level by level, from left to right.

```cpp
void levelOrderTraversal(Node* root) {
    if (root == nullptr) return;
    queue<Node*> q;
    q.push(root);
    while (!q.empty()) {
        Node* current = q.front();
        q.pop();
        cout << current->data << " ";
        if (current->left != nullptr)
            q.push(current->left);
        if (current->right != nullptr)
            q.push(current->right);
    }
}
```

For graphs, traversal algorithms like Depth-First Search (DFS) and Breadth-First Search (BFS) are commonly used. They can be implemented using similar recursive or iterative approaches, depending on the requirements of the problem.

These are just basic examples, and there can be variations and optimizations depending on specific requirements and the characteristics of the data structure being traversed.

### 1. Algorithms & Data Structures (C++): Path Sum - Binary Trees

Certainly! In C++, you can implement the path sum problem for binary trees using recursion. The problem statement usually goes like this: Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

Here's a simple implementation:

```cpp
#include <iostream>

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

bool hasPathSum(TreeNode* root, int sum) {
    if (!root) return false; // Base case: empty tree

    // Subtract the current node's value from the sum
    sum -= root->val;

    // If it's a leaf node and the sum becomes 0, then we found a valid path
    if (!root->left && !root->right) {
        return sum == 0;
    }

    // Recursively check the left and right subtrees
    return hasPathSum(root->left, sum) || hasPathSum(root->right, sum);
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(5);
    root->left = new TreeNode(4);
    root->right = new TreeNode(8);
    root->left->left = new TreeNode(11);
    root->left->left->left = new TreeNode(7);
    root->left->left->right = new TreeNode(2);
    root->right->left = new TreeNode(13);
    root->right->right = new TreeNode(4);
    root->right->right->right = new TreeNode(1);

    int sum = 22;
    if (hasPathSum(root, sum)) {
        std::cout << "There exists a root-to-leaf path with sum " << sum << std::endl;
    } else {
        std::cout << "No root-to-leaf path with sum " << sum << " exists" << std::endl;
    }

    // Clean up memory (not necessary for the algorithm, but good practice)
    delete root->right->right->right;
    delete root->right->right;
    delete root->right->left;
    delete root->right;
    delete root->left->left->right;
    delete root->left->left->left;
    delete root->left->left;
    delete root->left;
    delete root;

    return 0;
}
```

In this implementation, the `hasPathSum` function recursively checks whether there's a path from the root to a leaf node with the given sum. The base case is when we reach a leaf node, and the current `sum` equals the leaf node's value. If we find such a path, the function returns `true`. Otherwise, it returns `false`.

### 1. Algorithms & Data Structures (C++): Tree Traversal Techniques of a Binary Tree

In C++, there are several ways to traverse a binary tree, each with its own advantages and use cases. Here are the three main traversal techniques: **in-order**, **pre-order**, and **post-order** traversal.

#### In-order Traversal

In in-order traversal, the left subtree is recursively visited first, then the root node, and finally the right subtree. In a binary search tree (BST), this traversal would visit the nodes in ascending order.

```cpp
struct Node {
    int data;
    Node* left;
    Node* right;
};

void inOrderTraversal(Node* root) {
    if (root == nullptr)
        return;
    inOrderTraversal(root->left);
    cout << root->data << " ";
    inOrderTraversal(root->right);
}
```

#### Pre-order Traversal

In pre-order traversal, the root node is visited first, followed by the left subtree, and finally the right subtree.

```cpp
void preOrderTraversal(Node* root) {
    if (root == nullptr)
        return;
    cout << root->data << " ";
    preOrderTraversal(root->left);
    preOrderTraversal(root->right);
}
```

#### Post-order Traversal

In post-order traversal, the left and right subtrees are recursively visited before visiting the root node.

```cpp
void postOrderTraversal(Node* root) {
    if (root == nullptr)
        return;
    postOrderTraversal(root->left);
    postOrderTraversal(root->right);
    cout << root->data << " ";
}
```

#### Usage Example

To use these traversal functions, you can create a binary tree and call the respective traversal function with the root node.

```cpp
int main() {
    Node* root = new Node{1};
    root->left = new Node{2};
    root->right = new Node{3};
    root->left->left = new Node{4};
    root->left->right = new Node{5};

    cout << "In-order traversal: ";
    inOrderTraversal(root);
    cout << endl;

    cout << "Pre-order traversal: ";
    preOrderTraversal(root);
    cout << endl;

    cout << "Post-order traversal: ";
    postOrderTraversal(root);
    cout << endl;

    return 0;
}
```

This will output:

```bash
In-order traversal: 4 2 5 1 3 
Pre-order traversal: 1 2 4 5 3 
Post-order traversal: 4 5 2 3 1 
```

These traversal techniques are fundamental in many tree-related algorithms and are commonly used in problems involving binary trees.

### 1. Algorithms & Data Structures (C++): Trees: Binary Trees

Binary trees are fundamental data structures in computer science and are extensively used in various algorithms and applications. They consist of nodes where each node has at most two children, referred to as the left child and the right child. Here's an overview of binary trees in C++:

#### Binary Tree Node

First, you define a structure for the node of the binary tree:

```cpp
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};
```

#### Binary Tree Operations

1. **Insertion:**

```cpp
TreeNode* insert(TreeNode* root, int val) {
    if (root == nullptr)
        return new TreeNode(val);
    if (val < root->val)
        root->left = insert(root->left, val);
    else if (val > root->val)
        root->right = insert(root->right, val);
    return root;
}
```

1. **Search:**

```cpp
TreeNode* search(TreeNode* root, int val) {
    if (root == nullptr || root->val == val)
        return root;
    if (val < root->val)
        return search(root->left, val);
    return search(root->right, val);
}
```

1. **Deletion:**

```cpp
TreeNode* minValueNode(TreeNode* node) {
    TreeNode* current = node;
    while (current && current->left != nullptr)
        current = current->left;
    return current;
}

TreeNode* deleteNode(TreeNode* root, int key) {
    if (root == nullptr)
        return root;
    if (key < root->val)
        root->left = deleteNode(root->left, key);
    else if (key > root->val)
        root->right = deleteNode(root->right, key);
    else {
        if (root->left == nullptr) {
            TreeNode* temp = root->right;
            delete root;
            return temp;
        }
        else if (root->right == nullptr) {
            TreeNode* temp = root->left;
            delete root;
            return temp;
        }
        TreeNode* temp = minValueNode(root->right);
        root->val = temp->val;
        root->right = deleteNode(root->right, temp->val);
    }
    return root;
}
```

1. **Traversal:**

   - **Inorder Traversal:** Left, Root, Right
   - **Preorder Traversal:** Root, Left, Right
   - **Postorder Traversal:** Left, Right, Root

```cpp
void inorderTraversal(TreeNode* root) {
    if (root != nullptr) {
        inorderTraversal(root->left);
        cout << root->val << " ";
        inorderTraversal(root->right);
    }
}

void preorderTraversal(TreeNode* root) {
    if (root != nullptr) {
        cout << root->val << " ";
        preorderTraversal(root->left);
        preorderTraversal(root->right);
    }
}

void postorderTraversal(TreeNode* root) {
    if (root != nullptr) {
        postorderTraversal(root->left);
        postorderTraversal(root->right);
        cout << root->val << " ";
    }
}
```

These are some basic operations on binary trees in C++. You can extend this further by implementing additional functionalities like tree height, checking if a binary tree is balanced, finding the lowest common ancestor, etc.
