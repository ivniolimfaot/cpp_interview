# AVL

## General

### 1. Algorithms & Data Structures (C++): Delete entire AVL

Deleting an entire AVL tree involves freeing memory for each node in the tree. Since AVL trees are self-balancing binary search trees, we can traverse the tree in post-order (left-right-root) and delete each node recursively. Here's how you can implement it in C++:

```cpp
#include <iostream>
using namespace std;

struct Node {
    int key;
    Node* left;
    Node* right;
    int height;
};

// Function to create a new node
Node* newNode(int key) {
    Node* node = new Node;
    node->key = key;
    node->left = node->right = nullptr;
    node->height = 1; // New node is initially at height 1
    return node;
}

// Function to delete an entire AVL tree
void deleteAVL(Node* root) {
    if (root == nullptr)
        return;

    // Delete nodes in post-order (left-right-root)
    deleteAVL(root->left);
    deleteAVL(root->right);

    // Delete current node
    delete root;
}

// Function to print in-order traversal of AVL tree
void inorderTraversal(Node* root) {
    if (root == nullptr)
        return;

    inorderTraversal(root->left);
    cout << root->key << " ";
    inorderTraversal(root->right);
}

int main() {
    Node* root = newNode(9);
    root->left = newNode(5);
    root->right = newNode(10);
    root->left->left = newNode(2);
    root->left->right = newNode(7);
    root->right->right = newNode(12);

    cout << "In-order traversal before deletion: ";
    inorderTraversal(root);
    cout << endl;

    deleteAVL(root);
    root = nullptr;

    cout << "In-order traversal after deletion: ";
    inorderTraversal(root);
    cout << endl;

    return 0;
}
```

In this code:

- `Node` struct represents a node in the AVL tree.
- `newNode` function creates a new node with the given key.
- `deleteAVL` function recursively deletes each node in post-order traversal.
- `inorderTraversal` function is used to print the inorder traversal of the tree.
- In the `main` function, an AVL tree is created and then deleted entirely.

### 1. Algorithms & Data Structures (C++): AVL & Red-Black Trees

AVL trees and Red-Black trees are two fundamental self-balancing binary search trees that ensure efficient insertion, deletion, and searching operations. Both maintain balance through rotations and colorings, but they have some differences in their balancing criteria and performance characteristics.

**AVL Trees:**

- Named after their inventors, Adelson-Velsky and Landis.
- Balance criteria: The balance factor of any node (the height difference between its left and right subtrees) must be either -1, 0, or 1. If it's not, rotations are performed to rebalance the tree.
- Balancing operations: Single and double rotations (left-left, right-right, left-right, right-left).
- Complexity:
  - Insertion, deletion, and searching: O(log n), where n is the number of nodes.
  - Requires more rotations for balancing, which can make insertion and deletion slightly slower compared to Red-Black trees.
- Best used when:
  - Searching operations are more frequent than insertion and deletion.
  - There are strict space constraints.

**Red-Black Trees:**

- Introduced by Rudolf Bayer in 1972 and later refined by Leonidas J. Guibas and Robert Sedgewick.
- Balance criteria: Each node is colored either red or black, and the tree must satisfy several properties, including no two adjacent red nodes and the same number of black nodes on any path from the root to a leaf.
- Balancing operations: Rotations and recoloring of nodes to maintain the properties.
- Complexity:
  - Insertion, deletion, and searching: O(log n), where n is the number of nodes.
  - Requires fewer rotations compared to AVL trees, making insertion and deletion slightly faster in practice.
- Best used when:
  - Insertions and deletions are more frequent than searches.
  - There's less concern about strictly optimal balancing and more focus on overall performance.

In summary, both AVL and Red-Black trees provide efficient operations for balanced binary search trees, but their suitability depends on the specific requirements of the application. AVL trees guarantee stricter balance, while Red-Black trees offer better overall performance in terms of insertion and deletion due to their looser balance criteria.

### 1. Algorithms & Data Structures (C++): AVL Delete

Certainly! An AVL tree is a self-balancing binary search tree. In an AVL tree, the heights of the two child subtrees of any node differ by at most one.

Deleting a node in an AVL tree involves two main steps:

1. Perform a standard binary search tree delete operation.
2. Update the balance factor of the nodes along the path traversed during the deletion and perform rotations to maintain the AVL property.

Here's a high-level overview of the AVL delete algorithm in C++:

```cpp
#include <iostream>

struct Node {
    int key;
    Node *left;
    Node *right;
    int height;
};

// Helper function to get the height of a node
int height(Node *node) {
    if (node == nullptr)
        return 0;
    return node->height;
}

// Helper function to get the maximum of two integers
int max(int a, int b) {
    return (a > b) ? a : b;
}

// Create a new AVL node
Node* newNode(int key) {
    Node* node = new Node();
    node->key = key;
    node->left = nullptr;
    node->right = nullptr;
    node->height = 1; // New node is initially added at leaf
    return node;
}

// Right rotate subtree rooted with y
Node* rightRotate(Node *y) {
    Node *x = y->left;
    Node *T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    return x;
}

// Left rotate subtree rooted with x
Node* leftRotate(Node *x) {
    Node *y = x->right;
    Node *T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    // Update heights
    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    return y;
}

// Get balance factor of node
int getBalance(Node *node) {
    if (node == nullptr)
        return 0;
    return height(node->left) - height(node->right);
}

// Recursive function to delete a node with given key from AVL tree
Node* deleteNode(Node *root, int key) {
    if (root == nullptr)
        return root;

    // Perform standard BST delete
    if (key < root->key)
        root->left = deleteNode(root->left, key);
    else if (key > root->key)
        root->right = deleteNode(root->right, key);
    else {
        // Node with only one child or no child
        if ((root->left == nullptr) || (root->right == nullptr)) {
            Node *temp = root->left ? root->left : root->right;

            // No child case
            if (temp == nullptr) {
                temp = root;
                root = nullptr;
            } else // One child case
                *root = *temp; // Copy the contents of non-empty child

            delete temp;
        } else {
            // Node with two children: Get the inorder successor (smallest
            // in the right subtree)
            Node *temp = root->right;
            while (temp->left != nullptr)
                temp = temp->left;

            // Copy the inorder successor's data to this node
            root->key = temp->key;

            // Delete the inorder successor
            root->right = deleteNode(root->right, temp->key);
        }
    }

    // If the tree had only one node then return
    if (root == nullptr)
        return root;

    // Update height of current node
    root->height = 1 + max(height(root->left), height(root->right));

    // Get the balance factor of this node to check whether this node became
    // unbalanced
    int balance = getBalance(root);

    // If this node becomes unbalanced, then there are four cases

    // Left Left Case
    if (balance > 1 && getBalance(root->left) >= 0)
        return rightRotate(root);

    // Left Right Case
    if (balance > 1 && getBalance(root->left) < 0) {
        root->left = leftRotate(root->left);
        return rightRotate(root);
    }

    // Right Right Case
    if (balance < -1 && getBalance(root->right) <= 0)
        return leftRotate(root);

    // Right Left Case
    if (balance < -1 && getBalance(root->right) > 0) {
        root->right = rightRotate(root->right);
        return leftRotate(root);
    }

    return root;
}

// Function to print inorder traversal of AVL tree
void inorder(Node *root) {
    if (root != nullptr) {
        inorder(root->left);
        std::cout << root->key << " ";
        inorder(root->right);
    }
}

// Test AVL delete
int main() {
    Node *root = nullptr;

    root = insert(root, 9);
    root = insert(root, 5);
    root = insert(root, 10);
    root = insert(root, 0);
    root = insert(root, 6);
    root = insert(root, 11);
    root = insert(root, -1);
    root = insert(root, 1);
    root = insert(root, 2);

    std::cout << "Inorder traversal of the constructed AVL tree is: ";
    inorder(root);
    std::cout << std::endl;

    root = deleteNode(root, 10);

    std::cout << "Inorder traversal after deletion of 10: ";
    inorder(root);
    std::cout << std::endl;

    return 0;
}
```

This code provides the basic implementation of AVL tree deletion in C++. You would need to implement the `insert` function for insertion and `main` function to test the AVL tree deletion.

### 1. Algorithms & Data Structures (C++): AVL Tree - LL Rotation

In AVL trees, LL rotation is a type of rotation used to balance the tree when a left-left imbalance occurs. An AVL tree is a self-balancing binary search tree where the balance factor of each node (the height difference between its left and right subtrees) is either -1, 0, or 1. When an insertion or deletion operation violates this property, rotations are performed to restore balance.

Here's how LL rotation works in C++:

```cpp
#include <iostream>
using namespace std;

// AVL Tree Node structure
struct Node {
    int key;
    Node *left;
    Node *right;
    int height;
};

// Function to get the height of a node
int height(Node *N) {
    if (N == nullptr)
        return 0;
    return N->height;
}

// Function to create a new AVL tree node
Node *newNode(int key) {
    Node *node = new Node();
    node->key = key;
    node->left = nullptr;
    node->right = nullptr;
    node->height = 1;
    return node;
}

// Function to perform LL rotation
Node *leftRotate(Node *x) {
    Node *y = x->left;
    Node *T2 = y->right;

    // Perform rotation
    y->right = x;
    x->left = T2;

    // Update heights
    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    // Return new root
    return y;
}

// Function to perform inorder traversal of AVL tree
void inorder(Node *root) {
    if (root != nullptr) {
        inorder(root->left);
        cout << root->key << " ";
        inorder(root->right);
    }
}

int main() {
    Node *root = nullptr;

    // Constructing the AVL tree
    root = newNode(10);
    root->left = newNode(5);
    root->right = newNode(15);
    root->left->left = newNode(2);
    root->left->right = newNode(7);

    // Before rotation
    cout << "Inorder traversal before LL rotation: ";
    inorder(root);
    cout << endl;

    // Performing LL rotation
    root = leftRotate(root);

    // After rotation
    cout << "Inorder traversal after LL rotation: ";
    inorder(root);
    cout << endl;

    return 0;
}
```

In this code:

- `Node` represents a node in the AVL tree.
- `newNode` function creates a new node with the given key.
- `height` function returns the height of the node.
- `leftRotate` function performs the LL rotation and returns the new root of the subtree.
- `inorder` function performs an inorder traversal of the AVL tree.
- In the `main` function, an AVL tree is constructed, and LL rotation is performed on it.

LL rotation specifically addresses the imbalance when a new node is inserted into the left subtree of the left child of a node, causing a height difference of 2. This rotation restores balance by making appropriate adjustments to the affected nodes' pointers and updating their heights.

### 1. Algorithms & Data Structures (C++): AVL Tree - LR Rotation

In an AVL tree, rotations are crucial for maintaining balance. The LR (Left-Right) rotation is a type of rotation used to balance the tree when the left subtree of a node is unbalanced to the right, and the right subtree of that left child is unbalanced to the left.

Here's how the LR rotation works:

1. Perform a left rotation on the left child.
2. Perform a right rotation on the root.

Let's say we have an unbalanced AVL tree with a structure like this:

```bash
     A
    /
   B
     \
      C
```

To balance it using the LR rotation, we follow these steps:

1. Left Rotate B:

```bash
     B
   /   \
  A     C
```

1. Right Rotate A:

```bash
     B
   /   \
  A     C
```

This restores balance to the tree. The LR rotation is essentially a combination of a left rotation and a right rotation.

In C++, you can implement these rotations as member functions of your AVL tree class. Here's a simplified example:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* left;
    Node* right;
    int height;
};

Node* leftRotate(Node* x) {
    Node* y = x->right;
    Node* T2 = y->left;

    y->left = x;
    x->right = T2;

    // Update heights
    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    return y;
}

Node* rightRotate(Node* y) {
    Node* x = y->left;
    Node* T2 = x->right;

    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    return x;
}

int height(Node* N) {
    if (N == nullptr)
        return 0;
    return N->height;
}
```

You would then use these rotation functions as needed during insertions and deletions to maintain the balance of the AVL tree.

### 1. Algorithms & Data Structures (C++): AVL Tree - RL Rotation

Sure, let's dive into AVL trees and specifically the RL rotation. AVL trees are self-balancing binary search trees, meaning they automatically maintain a balance factor to ensure that the tree remains relatively balanced, which helps in keeping the time complexity of operations like insertion, deletion, and searching logarithmic.

The RL rotation is a specific type of rotation used in AVL trees to balance the tree when it becomes unbalanced due to an insertion or deletion. The RL rotation is applied when a node's balance factor becomes greater than 1 and its right child's balance factor is less than 0.

Here's how the RL rotation works:

1. Perform a right rotation on the right child of the unbalanced node.
2. Perform a left rotation on the unbalanced node.

Let's illustrate this with an example:

Suppose we have an AVL tree where the balance factor of node A becomes greater than 1 and the balance factor of its right child B becomes less than 0. The tree might look like this:

```bash
      A
     / \
    B   C
   / \
  D   E
```

To balance this tree using RL rotation:

1. Perform a right rotation on B:

```bash
    B
   / \
  D   A
     / \
    E   C
```

1. Perform a left rotation on A:

```bash
    B
   / \
  D   A
     / \
    E   C
```

After the RL rotation, the tree becomes balanced:

```bash
      B
     / \
    D   A
       / \
      E   C
```

This is just one step in maintaining the balance of an AVL tree. After performing rotations, you may need to update the balance factors of the nodes and perform further rotations if necessary to ensure that the tree remains balanced.

### 1. Algorithms & Data Structures (C++): AVL Tree - RR Rotation

In an AVL tree, rotations are crucial for maintaining balance. RR rotation specifically addresses the issue where the right subtree of the right child of a node becomes heavier by one compared to the left subtree of the right child. This imbalance leads to a violation of the AVL property (the height difference between left and right subtrees should be at most 1). RR rotation helps to balance the tree while maintaining the AVL property.

Here's how RR rotation works in C++:

```cpp
#include <iostream>
using namespace std;

// Definition of a node in AVL tree
struct Node {
    int data;
    Node* left;
    Node* right;
    int height;
};

// Utility function to get height of a node
int height(Node* node) {
    if (node == nullptr)
        return 0;
    return node->height;
}

// Function to create a new node with given data
Node* newNode(int data) {
    Node* node = new Node;
    node->data = data;
    node->left = nullptr;
    node->right = nullptr;
    node->height = 1; // New node is initially at height 1
    return node;
}

// Function to perform right rotation (RR Rotation)
Node* rightRotate(Node* y) {
    Node* x = y->left;
    Node* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    // Return new root
    return x;
}

// Function to print preorder traversal of AVL tree
void preOrder(Node* root) {
    if (root != nullptr) {
        cout << root->data << " ";
        preOrder(root->left);
        preOrder(root->right);
    }
}

int main() {
    Node* root = nullptr;

    // Construct AVL tree
    root = newNode(10);
    root->left = newNode(5);
    root->right = newNode(20);
    root->right->left = newNode(15);
    root->right->right = newNode(25);

    cout << "Preorder traversal of AVL tree before RR rotation:\n";
    preOrder(root);
    cout << endl;

    // Perform RR rotation
    root = rightRotate(root);

    cout << "Preorder traversal of AVL tree after RR rotation:\n";
    preOrder(root);
    cout << endl;

    return 0;
}
```

In this code:

- `rightRotate` function performs the RR rotation. It takes the root of the unbalanced subtree (y) and rotates it with its left child (x), making x the new root of the subtree. T2 is the right subtree of x which becomes the left subtree of y after rotation.
- `preOrder` function is used to print the AVL tree in preorder traversal to observe the tree before and after the rotation.
- In the `main` function, an AVL tree is constructed and RR rotation is performed. Finally, the AVL tree is printed before and after the rotation to observe the changes.

### 1. Algorithms & Data Structures (C++): AVL Tree Class ADT

Sure, I can provide you with a basic implementation of an AVL tree class in C++. An AVL tree is a self-balancing binary search tree where the height of the two child subtrees of any node differs by at most one.

Here's a simple implementation of an AVL tree:

```cpp
#include <iostream>

template<typename T>
class AVLTree {
private:
    struct Node {
        T data;
        Node* left;
        Node* right;
        int height;

        Node(const T& val) : data(val), left(nullptr), right(nullptr), height(1) {}
    };

    Node* root;

    int getHeight(Node* node) {
        if (node == nullptr) return 0;
        return node->height;
    }

    int getBalanceFactor(Node* node) {
        if (node == nullptr) return 0;
        return getHeight(node->left) - getHeight(node->right);
    }

    Node* rotateRight(Node* y) {
        Node* x = y->left;
        Node* T2 = x->right;

        x->right = y;
        y->left = T2;

        y->height = 1 + std::max(getHeight(y->left), getHeight(y->right));
        x->height = 1 + std::max(getHeight(x->left), getHeight(x->right));

        return x;
    }

    Node* rotateLeft(Node* x) {
        Node* y = x->right;
        Node* T2 = y->left;

        y->left = x;
        x->right = T2;

        x->height = 1 + std::max(getHeight(x->left), getHeight(x->right));
        y->height = 1 + std::max(getHeight(y->left), getHeight(y->right));

        return y;
    }

    Node* insert(Node* node, const T& val) {
        if (node == nullptr) return new Node(val);

        if (val < node->data)
            node->left = insert(node->left, val);
        else if (val > node->data)
            node->right = insert(node->right, val);
        else
            return node; // Duplicate keys not allowed

        node->height = 1 + std::max(getHeight(node->left), getHeight(node->right));

        int balance = getBalanceFactor(node);

        // Left Left Case
        if (balance > 1 && val < node->left->data)
            return rotateRight(node);

        // Right Right Case
        if (balance < -1 && val > node->right->data)
            return rotateLeft(node);

        // Left Right Case
        if (balance > 1 && val > node->left->data) {
            node->left = rotateLeft(node->left);
            return rotateRight(node);
        }

        // Right Left Case
        if (balance < -1 && val < node->right->data) {
            node->right = rotateRight(node->right);
            return rotateLeft(node);
        }

        return node;
    }

    void inorderTraversal(Node* node) {
        if (node != nullptr) {
            inorderTraversal(node->left);
            std::cout << node->data << " ";
            inorderTraversal(node->right);
        }
    }

public:
    AVLTree() : root(nullptr) {}

    void insert(const T& val) {
        root = insert(root, val);
    }

    void inorderTraversal() {
        inorderTraversal(root);
        std::cout << std::endl;
    }
};

int main() {
    AVLTree<int> avlTree;
    avlTree.insert(10);
    avlTree.insert(20);
    avlTree.insert(30);
    avlTree.insert(40);
    avlTree.insert(50);
    avlTree.insert(25);

    std::cout << "Inorder traversal of the AVL tree: ";
    avlTree.inorderTraversal();

    return 0;
}
```

This implementation provides basic functionality for insertion and inorder traversal of an AVL tree. You can extend it to support deletion, search, and other operations as needed.

### 1. Algorithms & Data Structures (C++): AVL Tree Feeback Time

AVL trees are fascinating data structures, aren't they? They strike a balance between efficient insertion, deletion, and search operations by maintaining a height-balanced binary search tree. This balancing ensures that the tree remains relatively balanced, which in turn guarantees \(O(\log n)\) time complexity for basic operations.

When implementing AVL trees in C++, attention to detail is crucial. Ensuring that rotations are correctly implemented and maintaining the balance factor of each node accurately throughout operations is key. Debugging AVL tree implementations can be challenging due to the intricacies of tree rotations and node updates.

If you're seeking feedback on your AVL tree implementation, it would be helpful to provide more context or specific areas where you're encountering challenges. Whether it's related to understanding AVL tree rotations, implementing the balancing logic, or handling edge cases, I'm here to assist you.

### 1. Algorithms & Data Structures (C++): AVL Tree Rotations after Deletion

AVL trees are self-balancing binary search trees where the height difference between the left and right subtrees (balance factor) of any node is at most one. When performing deletion operations on an AVL tree, the tree may become unbalanced, violating the AVL property. To maintain balance, rotations are performed after deletion.

Here's a general overview of AVL tree rotations after deletion in C++:

1. **Perform the standard BST delete operation** to remove the node from the AVL tree.
2. **Update the height of each ancestor node** of the deleted node.
3. **Check the balance factor** of each ancestor node to ensure that the AVL property is maintained.
4. If an ancestor node becomes unbalanced, **perform rotations** to restore balance.

Here are the four possible cases of imbalance after deletion, along with the corresponding rotations:

1. **Left Left (LL) Case**: A node is deleted from the left subtree of the left child of the unbalanced node.
   - Perform a single right rotation.

2. **Left Right (LR) Case**: A node is deleted from the right subtree of the left child of the unbalanced node.
   - Perform a left rotation on the left child followed by a right rotation on the unbalanced node.

3. **Right Right (RR) Case**: A node is deleted from the right subtree of the right child of the unbalanced node.
   - Perform a single left rotation.

4. **Right Left (RL) Case**: A node is deleted from the left subtree of the right child of the unbalanced node.
   - Perform a right rotation on the right child followed by a left rotation on the unbalanced node.

Here's a C++ pseudocode for AVL tree rotations after deletion:

```cpp
// Perform standard BST delete operation
Node* deleteNode(Node* root, int key) {
    // Standard BST delete operation
    // Update height of the current node
    // Check balance factor to detect imbalance
    // Perform rotations if necessary
    return root;
}

// AVL tree rotation functions
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
```

These rotation functions can be used in the `deleteNode` function to handle each imbalance case accordingly.

Remember, maintaining the AVL property after deletion is crucial for the efficient performance of AVL trees.

### 1. Algorithms & Data Structures (C++): AVL Tree Rotations for Insertion

AVL trees are self-balancing binary search trees. When you insert a node into an AVL tree, you may disrupt its balance, violating the AVL property, which states that the heights of the two child subtrees of any node must differ by at most one. To restore balance, you may need to perform one or more rotations.

Here are the basic rotations for insertion in an AVL tree:

1. **Left Rotation**: Used when the balance factor of a node becomes +2 due to insertion into the right subtree of its right child.
2. **Right Rotation**: Used when the balance factor of a node becomes -2 due to insertion into the left subtree of its left child.
3. **Left-Right Rotation (Double Rotation)**: Used when the balance factor of a node becomes +2 due to insertion into the left subtree of its right child.
4. **Right-Left Rotation (Double Rotation)**: Used when the balance factor of a node becomes -2 due to insertion into the right subtree of its left child.

Below is an example implementation of these rotations in C++:

```cpp
struct Node {
    int data;
    Node* left;
    Node* right;
    int height;
};

// Function to perform a right rotation
Node* rightRotate(Node* y) {
    Node* x = y->left;
    Node* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    // Return new root
    return x;
}

// Function to perform a left rotation
Node* leftRotate(Node* x) {
    Node* y = x->right;
    Node* T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    // Update heights
    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    // Return new root
    return y;
}

// Function to insert a new node with given key in AVL tree
Node* insert(Node* node, int key) {
    // Perform normal BST insertion
    if (node == nullptr)
        return newNode(key);

    if (key < node->data)
        node->left = insert(node->left, key);
    else if (key > node->data)
        node->right = insert(node->right, key);
    else // Duplicate keys not allowed
        return node;

    // Update height of this ancestor node
    node->height = 1 + max(height(node->left), height(node->right));

    // Get the balance factor of this ancestor node to check whether this node became unbalanced
    int balance = getBalance(node);

    // If this node becomes unbalanced, there are four cases

    // Left Left Case
    if (balance > 1 && key < node->left->data)
        return rightRotate(node);

    // Right Right Case
    if (balance < -1 && key > node->right->data)
        return leftRotate(node);

    // Left Right Case
    if (balance > 1 && key > node->left->data) {
        node->left = leftRotate(node->left);
        return rightRotate(node);
    }

    // Right Left Case
    if (balance < -1 && key < node->right->data) {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }

    // Return the unchanged node pointer
    return node;
}
```

In this implementation, `height()` function returns the height of the tree rooted at the given node, and `getBalance()` function returns the balance factor of the node (height of left subtree - height of right subtree).

### 1. Algorithms & Data Structures (C++): AVL Tree: Rotations

In the context of AVL trees, rotations are fundamental operations used to maintain the balance property of the tree. AVL trees are a type of self-balancing binary search tree where the height difference between the left and right subtrees of any node (called the balance factor) is limited to {-1, 0, 1}.

When an insertion or deletion violates this balance property, rotations are performed to restore it. There are four types of rotations in AVL trees:

1. **Left Rotation**
2. **Right Rotation**
3. **Left-Right Rotation (Double Rotation)**
4. **Right-Left Rotation (Double Rotation)**

Let's discuss each rotation:

#### 1. Left Rotation

A left rotation is performed when the balance factor of a node becomes greater than 1 due to an insertion or deletion in the right subtree of its right child. This operation involves making the right child of the node its new root while the node becomes the left child of its former right child.

```bash
      A                   B
       \                 / \
        B         =>    A   C
         \
          C
```

#### 2. Right Rotation

A right rotation is performed when the balance factor of a node becomes less than -1 due to an insertion or deletion in the left subtree of its left child. This operation is the mirror image of the left rotation.

```bash
      C                  B
     /                  / \
    B          =>      A   C
   /
  A
```

#### 3. Left-Right Rotation (Double Rotation)

A left-right rotation is performed when the balance factor of a node becomes greater than 1 due to an insertion or deletion in the left subtree of its right child. It involves performing a left rotation on the right child followed by a right rotation on the original node.

```bash
      A                    A                   C
       \                    \                /   \
        C          =>        C       =>    B     A
       /                      \
      B                        B
```

#### 4. Right-Left Rotation (Double Rotation)

A right-left rotation is performed when the balance factor of a node becomes less than -1 due to an insertion or deletion in the right subtree of its left child. It involves performing a right rotation on the left child followed by a left rotation on the original node.

```bash
      C                  C                       A
     /                  /                      /    \
    A          =>      B            =>       A      C
     \                /
      B              A
```

These rotations ensure that the AVL tree remains balanced after insertions and deletions, thereby maintaining efficient search, insert, and delete operations. Implementing these rotations correctly is crucial for the proper functioning of an AVL tree.

### 1. Algorithms & Data Structures (C++): AVL Trees

AVL trees are self-balancing binary search trees. They were the first such structures to be invented. AVL trees maintain a property that for each node in the tree, the heights of its left and right subtrees can differ by at most one. This ensures that the tree remains balanced, and as a result, search, insert, and delete operations all have logarithmic time complexity in the worst case.

In C++, you can implement an AVL tree by defining a structure for a node and then implementing the necessary functions to perform various operations like insertion, deletion, rotation, and balancing. Here's a basic outline of how you might implement an AVL tree in C++:

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

// Function to get the height of a node
int height(Node* node) {
    if (node == nullptr)
        return 0;
    return node->height;
}

// Function to create a new node
Node* newNode(int key) {
    Node* node = new Node();
    node->data = key;
    node->left = nullptr;
    node->right = nullptr;
    node->height = 1; // new node is initially added at leaf
    return node;
}

// Function to perform right rotation
Node* rightRotate(Node* y) {
    Node* x = y->left;
    Node* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    // Return new root
    return x;
}

// Function to perform left rotation
Node* leftRotate(Node* x) {
    Node* y = x->right;
    Node* T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    // Update heights
    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    // Return new root
    return y;
}

// Get the balance factor of a node
int getBalance(Node* node) {
    if (node == nullptr)
        return 0;
    return height(node->left) - height(node->right);
}

// Function to insert a node into the AVL tree
Node* insert(Node* root, int key) {
    if (root == nullptr)
        return newNode(key);

    if (key < root->data)
        root->left = insert(root->left, key);
    else if (key > root->data)
        root->right = insert(root->right, key);
    else // Equal keys are not allowed in AVL trees
        return root;

    // Update height of this ancestor node
    root->height = 1 + max(height(root->left), height(root->right));

    // Get the balance factor of this ancestor node to check whether this node became unbalanced
    int balance = getBalance(root);

    // If the node is unbalanced, there are four possible cases

    // Left Left Case
    if (balance > 1 && key < root->left->data)
        return rightRotate(root);

    // Right Right Case
    if (balance < -1 && key > root->right->data)
        return leftRotate(root);

    // Left Right Case
    if (balance > 1 && key > root->left->data) {
        root->left = leftRotate(root->left);
        return rightRotate(root);
    }

    // Right Left Case
    if (balance < -1 && key < root->right->data) {
        root->right = rightRotate(root->right);
        return leftRotate(root);
    }

    // Return the unchanged node pointer
    return root;
}

// Function to print the AVL tree (inorder traversal)
void inorder(Node* root) {
    if (root != nullptr) {
        inorder(root->left);
        cout << root->data << " ";
        inorder(root->right);
    }
}

int main() {
    Node* root = nullptr;

    // Insert some nodes
    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 30);
    root = insert(root, 40);
    root = insert(root, 50);
    root = insert(root, 25);

    // Print inorder traversal of the AVL tree
    cout << "Inorder traversal of the AVL tree: ";
    inorder(root);
    cout << endl;

    return 0;
}
```

This is a basic implementation covering insertion and rotations to maintain balance. Similar functions can be added for deletion and other operations as well.

### 1. Algorithms & Data Structures (C++): AVL Tree

An AVL tree is a self-balancing binary search tree. In an AVL tree, the heights of the two child subtrees of any node differ by at most one. If, at any time, the height difference between two subtrees becomes greater than one, the tree is rebalanced to restore this property. This ensures that the tree remains balanced and maintains an O(log n) time complexity for insertion, deletion, and search operations.

Here's a basic overview of the AVL tree implementation in C++:

```cpp
#include <iostream>
using namespace std;

// AVL Node structure
struct Node {
    int key;
    Node* left;
    Node* right;
    int height;
};

// Function to get the height of a node
int height(Node* node) {
    if (node == nullptr)
        return 0;
    return node->height;
}

// Function to get the maximum of two integers
int max(int a, int b) {
    return (a > b) ? a : b;
}

// Function to create a new node with a given key
Node* newNode(int key) {
    Node* node = new Node();
    node->key = key;
    node->left = nullptr;
    node->right = nullptr;
    node->height = 1; // New node is initially at height 1
    return (node);
}

// Function to right rotate subtree rooted with y
Node* rightRotate(Node* y) {
    Node* x = y->left;
    Node* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    // Return new root
    return x;
}

// Function to left rotate subtree rooted with x
Node* leftRotate(Node* x) {
    Node* y = x->right;
    Node* T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    // Update heights
    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    // Return new root
    return y;
}

// Get Balance factor of node N
int getBalance(Node* node) {
    if (node == nullptr)
        return 0;
    return height(node->left) - height(node->right);
}

// Function to insert a new key in the AVL tree
Node* insert(Node* node, int key) {
    // Standard BST insertion
    if (node == nullptr)
        return (newNode(key));

    if (key < node->key)
        node->left = insert(node->left, key);
    else if (key > node->key)
        node->right = insert(node->right, key);
    else // Equal keys are not allowed in BST
        return node;

    // Update height of this ancestor node
    node->height = 1 + max(height(node->left), height(node->right));

    // Get the balance factor of this ancestor node to check whether this node became unbalanced
    int balance = getBalance(node);

    // If this node becomes unbalanced, then there are four cases

    // Left Left Case
    if (balance > 1 && key < node->left->key)
        return rightRotate(node);

    // Right Right Case
    if (balance < -1 && key > node->right->key)
        return leftRotate(node);

    // Left Right Case
    if (balance > 1 && key > node->left->key) {
        node->left = leftRotate(node->left);
        return rightRotate(node);
    }

    // Right Left Case
    if (balance < -1 && key < node->right->key) {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }

    // Return the (unchanged) node pointer
    return node;
}

// Function to print preorder traversal of the tree
void preOrder(Node* root) {
    if (root != nullptr) {
        cout << root->key << " ";
        preOrder(root->left);
        preOrder(root->right);
    }
}

// Test AVL Tree
int main() {
    Node* root = nullptr;

    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 30);
    root = insert(root, 40);
    root = insert(root, 50);
    root = insert(root, 25);

    /* The constructed AVL Tree would be
             30
            /  \
          20   40
         / \    \
        10 25   50
    */
    cout << "Preorder traversal of the constructed AVL tree is \n";
    preOrder(root);

    return 0;
}
```

This is a basic implementation of an AVL tree in C++. It includes functions for insertion, rotations, and preorder traversal. You can extend it by adding functions for deletion, searching, inorder traversal, and other operations as needed.

### 1. Algorithms & Data Structures (C++): Common Operations on AVL Trees

AVL trees are self-balancing binary search trees named after their inventors, Adelson-Velsky and Landis. They ensure that the tree remains balanced after insertions and deletions, which guarantees logarithmic time complexity for search, insertion, and deletion operations. Here are some common operations on AVL trees implemented in C++:

1. **Rotation Operations**:
   AVL trees use rotation operations to maintain balance. There are four types of rotations: left rotation, right rotation, left-right rotation, and right-left rotation. These rotations ensure that the balance factor of each node remains in the range [-1, 1].

   ```cpp
   // Left rotation
   Node* leftRotate(Node* x) {
       Node* y = x->right;
       x->right = y->left;
       y->left = x;
       updateHeight(x);
       updateHeight(y);
       return y;
   }

   // Right rotation
   Node* rightRotate(Node* y) {
       Node* x = y->left;
       y->left = x->right;
       x->right = y;
       updateHeight(y);
       updateHeight(x);
       return x;
   }

   // Left-Right rotation (Double rotation)
   Node* leftRightRotate(Node* z) {
       z->left = leftRotate(z->left);
       return rightRotate(z);
   }

   // Right-Left rotation (Double rotation)
   Node* rightLeftRotate(Node* z) {
       z->right = rightRotate(z->right);
       return leftRotate(z);
   }
   ```

2. **Insertion**:
   When inserting a node into the AVL tree, you perform a standard binary search tree insertion and then perform rotations to maintain balance.

   ```cpp
   Node* insert(Node* root, int key) {
       if (root == nullptr)
           return new Node(key);
       
       if (key < root->key)
           root->left = insert(root->left, key);
       else if (key > root->key)
           root->right = insert(root->right, key);
       else // Duplicate keys are not allowed
           return root;

       // Update height and balance factor
       updateHeight(root);

       // Check balance factor and perform rotations if needed
       int balance = getBalance(root);
       if (balance > 1 && key < root->left->key)
           return rightRotate(root);
       if (balance < -1 && key > root->right->key)
           return leftRotate(root);
       if (balance > 1 && key > root->left->key)
           return leftRightRotate(root);
       if (balance < -1 && key < root->right->key)
           return rightLeftRotate(root);
       
       return root;
   }
   ```

3. **Deletion**:
   When deleting a node, you perform a standard binary search tree deletion and then rebalance the tree if necessary.

   ```cpp
   Node* deleteNode(Node* root, int key) {
       if (root == nullptr)
           return root;
       
       if (key < root->key)
           root->left = deleteNode(root->left, key);
       else if (key > root->key)
           root->right = deleteNode(root->right, key);
       else {
           // Node with only one child or no child
           if (root->left == nullptr || root->right == nullptr) {
               Node* temp = root->left ? root->left : root->right;
               if (temp == nullptr) {
                   temp = root;
                   root = nullptr;
               } else
                   *root = *temp; // Copy the contents of the child
               delete temp;
           } else {
               // Node with two children: Get the inorder successor (smallest in the right subtree)
               Node* temp = minValueNode(root->right);
               root->key = temp->key;
               root->right = deleteNode(root->right, temp->key);
           }
       }

       // If the tree had only one node then return
       if (root == nullptr)
           return root;

       // Update height and balance factor
       updateHeight(root);

       // Check balance factor and perform rotations if needed
       int balance = getBalance(root);
       if (balance > 1 && getBalance(root->left) >= 0)
           return rightRotate(root);
       if (balance > 1 && getBalance(root->left) < 0)
           return leftRightRotate(root);
       if (balance < -1 && getBalance(root->right) <= 0)
           return leftRotate(root);
       if (balance < -1 && getBalance(root->right) > 0)
           return rightLeftRotate(root);

       return root;
   }
   ```

4. **Search**:
   Search in AVL trees follows the same logic as in binary search trees.

   ```cpp
   Node* search(Node* root, int key) {
       if (root == nullptr || root->key == key)
           return root;
       
       if (root->key < key)
           return search(root->right, key);
       
       return search(root->left, key);
   }
   ```

5. **Other Operations**:
   Other operations include finding the minimum and maximum values, finding the successor and predecessor, etc., which can be implemented similarly to binary search trees.

   ```cpp
   Node* minValueNode(Node* node) {
       Node* current = node;
       while (current->left != nullptr)
           current = current->left;
       return current;
   }

   Node* maxValueNode(Node* node) {
       Node* current = node;
       while (current->right != nullptr)
           current = current->right;
       return current;
   }
   ```

These are the fundamental operations commonly performed on AVL trees in C++. You can extend these implementations for other operations as per your requirements.

### 1. Algorithms & Data Structures (C++): AVL Red-Black Tree

AVL trees and red-black trees are both types of self-balancing binary search trees, commonly used in computer science for efficient data storage and retrieval. Although they serve similar purposes, they have different mechanisms for maintaining balance and certain performance characteristics.

1. **AVL Tree**:
   - Named after its inventors Adelson-Velsky and Landis, AVL trees maintain balance by enforcing a height balance condition. For every node in the tree, the heights of its left and right subtrees can differ by at most one.
   - To maintain balance, AVL trees perform rotations when necessary during insertion and deletion operations.
   - While AVL trees generally have faster lookup times compared to ordinary binary search trees, they may require more rotations during insertion and deletion, potentially resulting in slightly slower performance for these operations.
   - In C++, you can implement an AVL tree by defining a node structure and implementing rotation operations (left rotation, right rotation, etc.) and insertion/deletion algorithms that ensure the AVL property is maintained.

2. **Red-Black Tree**:
   - Red-black trees maintain balance by enforcing several properties:
     1. Every node is either red or black.
     2. The root is black.
     3. Every leaf (NIL) is black.
     4. If a node is red, then both its children are black.
     5. Every path from a node to its descendant NIL nodes must have the same number of black nodes, which ensures that the longest path is no more than twice the shortest path.
   - Red-black trees require fewer rotations during insertion and deletion compared to AVL trees because they relax the balance criteria slightly.
   - Although red-black trees may have slightly slower lookup times compared to AVL trees, their insertion and deletion operations tend to be faster.
   - In C++, you can implement a red-black tree by defining a node structure and implementing insertion, deletion, and balancing operations to maintain the red-black properties.

Both AVL trees and red-black trees are widely used in practice, and the choice between them often depends on the specific requirements of the application. If you're working in C++, you might find existing implementations of both AVL and red-black trees in standard libraries like `std::set` and `std::map`. These implementations are typically well-optimized and suitable for most use cases. However, implementing these trees yourself is a great exercise for understanding their inner workings and sharpening your skills in algorithm design and analysis.

### 1. Algorithms & Data Structures (C++): Delete a node from AVL (LL, LR, RR, RL)

Deleting a node from an AVL tree involves performing a removal operation similar to binary search trees, followed by rebalancing the tree to maintain the AVL property. The four cases you mentioned, LL, LR, RR, and RL, refer to the rotations needed after deletion to maintain the AVL balance.

Here's a general outline of how you can delete a node from an AVL tree in C++. We'll cover the four cases: LL, LR, RR, and RL.

Let's start with the basic structure of a node in the AVL tree:

```cpp
struct Node {
    int key;
    Node* left;
    Node* right;
    int height;
};
```

And here's the function to delete a node:

```cpp
Node* deleteNode(Node* root, int key) {
    if (root == nullptr)
        return root;

    if (key < root->key)
        root->left = deleteNode(root->left, key);
    else if (key > root->key)
        root->right = deleteNode(root->right, key);
    else {
        // Node with only one child or no child
        if (root->left == nullptr || root->right == nullptr) {
            Node* temp = root->left ? root->left : root->right;
            if (temp == nullptr) {
                temp = root;
                root = nullptr;
            } else
                *root = *temp; // Copy the contents of non-empty child

            delete temp;
        } else {
            // Node with two children: Get the inorder successor
            Node* temp = minValueNode(root->right);

            // Copy the inorder successor's data to this node
            root->key = temp->key;

            // Delete the inorder successor
            root->right = deleteNode(root->right, temp->key);
        }
    }

    // If the tree had only one node then return
    if (root == nullptr)
        return root;

    // Update the height of the current node
    root->height = 1 + max(height(root->left), height(root->right));

    // Check if this node became unbalanced
    int balance = getBalance(root);

    // Left Left Case
    if (balance > 1 && getBalance(root->left) >= 0)
        return rightRotate(root);

    // Left Right Case
    if (balance > 1 && getBalance(root->left) < 0) {
        root->left = leftRotate(root->left);
        return rightRotate(root);
    }

    // Right Right Case
    if (balance < -1 && getBalance(root->right) <= 0)
        return leftRotate(root);

    // Right Left Case
    if (balance < -1 && getBalance(root->right) > 0) {
        root->right = rightRotate(root->right);
        return leftRotate(root);
    }

    return root;
}
```

In this code:

- `rightRotate` and `leftRotate` are functions for performing right and left rotations, respectively.
- `getBalance` calculates the balance factor of a node.
- `height` calculates the height of a node.
- `minValueNode` finds the node with the minimum value in a subtree.

These helper functions are necessary to maintain the AVL tree property. Implementations of these functions are widely available and can be found easily.

Remember to handle memory management properly, ensuring that you deallocate memory for nodes that are deleted. Also, make sure to update the heights of the nodes correctly after deletion and rotation operations to maintain the AVL property.

### 1. Algorithms & Data Structures (C++): Delete a node from AVL

Deleting a node from an AVL (Adelson-Velsky and Landis) tree in C++ involves several steps to maintain the balance property of the tree. Here's a basic implementation of the delete operation for an AVL tree:

```cpp
#include <iostream>

using namespace std;

struct Node {
    int key;
    Node *left;
    Node *right;
    int height;
};

// Utility function to get the height of a node
int height(Node *N) {
    if (N == nullptr)
        return 0;
    return N->height;
}

// Utility function to get the maximum of two integers
int max(int a, int b) {
    return (a > b) ? a : b;
}

// Function to create a new node with given key
Node* newNode(int key) {
    Node* node = new Node();
    node->key = key;
    node->left = nullptr;
    node->right = nullptr;
    node->height = 1; // new node is initially added at leaf
    return node;
}

// A utility function to right rotate subtree rooted with y
Node* rightRotate(Node* y) {
    Node* x = y->left;
    Node* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    // Return new root
    return x;
}

// A utility function to left rotate subtree rooted with x
Node* leftRotate(Node* x) {
    Node* y = x->right;
    Node* T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    //  Update heights
    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    // Return new root
    return y;
}

// Get Balance factor of node N
int getBalance(Node *N) {
    if (N == nullptr)
        return 0;
    return height(N->left) - height(N->right);
}

// Recursive function to insert a key in the subtree rooted with node and returns the new root of the subtree.
Node* insert(Node* node, int key) {
    /* 1. Perform the normal BST insertion */
    if (node == nullptr)
        return newNode(key);

    if (key < node->key)
        node->left = insert(node->left, key);
    else if (key > node->key)
        node->right = insert(node->right, key);
    else // Equal keys are not allowed in BST
        return node;

    /* 2. Update height of this ancestor node */
    node->height = 1 + max(height(node->left), height(node->right));

    /* 3. Get the balance factor of this ancestor node to check whether this node became unbalanced */
    int balance = getBalance(node);

    // If this node becomes unbalanced, then there are 4 cases

    // Left Left Case
    if (balance > 1 && key < node->left->key)
        return rightRotate(node);

    // Right Right Case
    if (balance < -1 && key > node->right->key)
        return leftRotate(node);

    // Left Right Case
    if (balance > 1 && key > node->left->key) {
        node->left = leftRotate(node->left);
        return rightRotate(node);
    }

    // Right Left Case
    if (balance < -1 && key < node->right->key) {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }

    /* return the (unchanged) node pointer */
    return node;
}

// Function to delete a node from AVL tree
Node* deleteNode(Node* root, int key) {
    // STEP 1: PERFORM STANDARD BST DELETE
    if (root == nullptr)
        return root;

    // If the key to be deleted is smaller than the root's key, then it lies in the left subtree
    if (key < root->key)
        root->left = deleteNode(root->left, key);

    // If the key to be deleted is greater than the root's key, then it lies in the right subtree
    else if (key > root->key)
        root->right = deleteNode(root->right, key);

    // if key is same as root's key, then This is the node to be deleted
    else {
        // node with only one child or no child
        if ((root->left == nullptr) || (root->right == nullptr)) {
            Node* temp = root->left ? root->left : root->right;

            // No child case
            if (temp == nullptr) {
                temp = root;
                root = nullptr;
            } else // One child case
                *root = *temp; // Copy the contents of the non-empty child

            delete temp;
        } else {
            // node with two children: Get the inorder successor (smallest in the right subtree)
            Node* temp = root->right;
            while (temp->left != nullptr)
                temp = temp->left;

            // Copy the inorder successor's data to this node
            root->key = temp->key;

            // Delete the inorder successor
            root->right = deleteNode(root->right, temp->key);
        }
    }

    // If the tree had only one node then return
    if (root == nullptr)
        return root;

    // STEP 2: UPDATE HEIGHT OF THE CURRENT NODE
    root->height = 1 + max(height(root->left), height(root->right));

    // STEP 3: GET THE BALANCE FACTOR OF THIS NODE (to check whether this node became unbalanced)
    int balance = getBalance(root);

    // If this node becomes unbalanced, then there are 4 cases

    // Left Left Case
    if (balance > 1 && getBalance(root->left) >= 0)
        return rightRotate(root);

    // Left Right Case
    if (balance > 1 && getBalance(root->left) < 0) {
        root->left = leftRotate(root->left);
        return rightRotate(root);
    }

    // Right Right Case
    if (balance < -1 && getBalance(root->right) <= 0)
        return leftRotate(root);

    // Right Left Case
    if (balance < -1 && getBalance(root->right) > 0) {
        root->right = rightRotate(root->right);
        return leftRotate(root);
    }

    return root;
}

// A utility function to print preorder traversal of the tree.
// The function also prints height of every node
void preOrder(Node* root) {
    if (root != nullptr) {
        cout << root->key << " ";
        preOrder(root->left);
        preOrder(root->right);
    }
}

int main() {
    Node* root = nullptr;

    root = insert(root, 9

);
    root = insert(root, 5);
    root = insert(root, 10);
    root = insert(root, 0);
    root = insert(root, 6);
    root = insert(root, 11);
    root = insert(root, -1);
    root = insert(root, 1);
    root = insert(root, 2);

    cout << "Preorder traversal of the constructed AVL tree is \n";
    preOrder(root);

    root = deleteNode(root, 10);

    cout << "\nPreorder traversal after deletion of 10 \n";
    preOrder(root);

    return 0;
}
```

This code covers the basics of inserting and deleting nodes in an AVL tree while maintaining its balance property. You can further enhance it by adding additional features or error handling, depending on your requirements.

### 1. Algorithms & Data Structures (C++): Deletion from AVL Tree with Rotations

Sure, I can provide an overview of how deletion works in an AVL tree along with the necessary rotations in C++. Here's a step-by-step guide:

#### Deletion in AVL Tree

1. **Search for the Node to Delete**: First, locate the node that needs to be deleted, similar to deletion in a binary search tree.

2. **Perform Standard BST Delete**: Perform the standard deletion for a binary search tree:
   - If the node to be deleted has no children or only one child, simply remove it.
   - If the node has two children, find the inorder successor (or predecessor), copy its data to the node to be deleted, and delete the inorder successor (or predecessor).

3. **Update Heights and Balance Factors**: After deletion, update the heights and balance factors of the ancestor nodes of the deleted node.

4. **Check Balance Property and Perform Rotations**: If after deletion, the balance property (difference in heights of left and right subtrees) is violated, perform necessary rotations to rebalance the tree.

#### Rotations

AVL trees use rotations to maintain balance after insertion or deletion operations. There are four types of rotations:

1. Left Rotation
2. Right Rotation
3. Left-Right Rotation (Double Right)
4. Right-Left Rotation (Double Left)

##### Left Rotation

```plaintext
    A            B
   / \          / \
  B   T3  =>  T1  A
 / \              / \
T1  T2           T2  T3
```

##### Right Rotation

```plaintext
    A            B
   / \          / \
  T1  B   =>   A   T3
     / \      / \
    T2  B    T1  T2
```

##### Left-Right Rotation (Double Right)

```plaintext
    A            A           C
   / \          / \        /   \
  B   T4  =>  C   T4 =>  B     A
 / \          / \        / \   / \
T1  C        B   T3     T1 T2 T3 T4
   / \      / \
  T2  T3   T1  T2
```

##### Right-Left Rotation (Double Left)

```plaintext
    A            A            C
   / \          / \         /   \
  T1  B   =>  T1  C   =>  A     B
     / \          / \     / \   / \
    C   T4       B   T4  T1 T2 T3 T4
   / \          / \
  T2  T3       T2  T3
```

#### C++ Implementation

Here's a simple example of how deletion and rotations might be implemented in C++:

```cpp
struct Node {
    int key;
    Node *left;
    Node *right;
    int height;
};

int height(Node *N) {
    if (N == nullptr)
        return 0;
    return N->height;
}

int balanceFactor(Node *N) {
    if (N == nullptr)
        return 0;
    return height(N->left) - height(N->right);
}

Node* deleteNode(Node* root, int key) {
    // Perform standard BST delete
    
    // Update height of this ancestor node
    root->height = 1 + max(height(root->left), height(root->right));

    // Get the balance factor of this ancestor node to check whether this node became unbalanced
    int balance = balanceFactor(root);

    // If this node becomes unbalanced, perform rotations
    // Left Left Case
    if (balance > 1 && balanceFactor(root->left) >= 0)
        return rightRotate(root);

    // Left Right Case
    if (balance > 1 && balanceFactor(root->left) < 0) {
        root->left = leftRotate(root->left);
        return rightRotate(root);
    }

    // Right Right Case
    if (balance < -1 && balanceFactor(root->right) <= 0)
        return leftRotate(root);

    // Right Left Case
    if (balance < -1 && balanceFactor(root->right) > 0) {
        root->right = rightRotate(root->right);
        return leftRotate(root);
    }

    return root;
}

Node* rightRotate(Node *y) {
    Node *x = y->left;
    Node *T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    // Return new root
    return x;
}

Node* leftRotate(Node *x) {
    Node *y = x->right;
    Node *T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    // Update heights
    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    // Return new root
    return y;
}
```

This code gives you a basic understanding of how deletion and rotations work in an AVL tree. You can integrate this code into a full AVL tree implementation for a more complete solution.

### 1. Algorithms & Data Structures (C++): Deletion in AVL Tree

Deleting a node in an AVL tree involves two main steps: first, you perform a standard binary search tree deletion, and then you ensure that the AVL balance property is maintained by performing rotations if necessary. Here's a basic outline of how deletion in an AVL tree can be implemented in C++:

```cpp
#include <iostream>
using namespace std;

struct Node {
    int key;
    Node *left, *right;
    int height;
};

// Utility function to get the height of a node
int height(Node* node) {
    if (node == nullptr)
        return 0;
    return node->height;
}

// Utility function to get the balance factor of a node
int getBalance(Node* node) {
    if (node == nullptr)
        return 0;
    return height(node->left) - height(node->right);
}

// Function to create a new node with given key
Node* newNode(int key) {
    Node* node = new Node();
    node->key = key;
    node->left = node->right = nullptr;
    node->height = 1; // New node is initially added at leaf
    return node;
}

// Function to right rotate subtree rooted with y
Node* rightRotate(Node* y) {
    Node* x = y->left;
    Node* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    // Return new root
    return x;
}

// Function to left rotate subtree rooted with x
Node* leftRotate(Node* x) {
    Node* y = x->right;
    Node* T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    // Update heights
    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    // Return new root
    return y;
}

// Function to delete a node in AVL tree
Node* deleteNode(Node* root, int key) {
    if (root == nullptr)
        return root;

    // Perform standard BST delete
    if (key < root->key)
        root->left = deleteNode(root->left, key);
    else if (key > root->key)
        root->right = deleteNode(root->right, key);
    else {
        // Node with only one child or no child
        if ((root->left == nullptr) || (root->right == nullptr)) {
            Node* temp = root->left ? root->left : root->right;

            // No child case
            if (temp == nullptr) {
                temp = root;
                root = nullptr;
            } else // One child case
                *root = *temp; // Copy the contents of the non-empty child

            delete temp;
        } else {
            // Node with two children: Get the inorder successor (smallest in the right subtree)
            Node* temp = root->right;
            while (temp->left != nullptr)
                temp = temp->left;

            // Copy the inorder successor's data to this node
            root->key = temp->key;

            // Delete the inorder successor
            root->right = deleteNode(root->right, temp->key);
        }
    }

    // If the tree had only one node then return
    if (root == nullptr)
        return root;

    // Update height of the current node
    root->height = 1 + max(height(root->left), height(root->right));

    // Get the balance factor of this node to check whether this node became unbalanced
    int balance = getBalance(root);

    // If this node becomes unbalanced, then there are 4 cases

    // Left Left Case
    if (balance > 1 && getBalance(root->left) >= 0)
        return rightRotate(root);

    // Left Right Case
    if (balance > 1 && getBalance(root->left) < 0) {
        root->left = leftRotate(root->left);
        return rightRotate(root);
    }

    // Right Right Case
    if (balance < -1 && getBalance(root->right) <= 0)
        return leftRotate(root);

    // Right Left Case
    if (balance < -1 && getBalance(root->right) > 0) {
        root->right = rightRotate(root->right);
        return leftRotate(root);
    }

    return root;
}

// Function to print preorder traversal of the tree
void preOrder(Node* root) {
    if (root != nullptr) {
        cout << root->key << " ";
        preOrder(root->left);
        preOrder(root->right);
    }
}

// Driver program to test above functions
int main() {
    Node* root = nullptr;

    root = deleteNode(root, 9);

    cout << "Preorder traversal of the constructed AVL tree is \n";
    preOrder(root);

    return 0;
}
```

This code provides a basic implementation of deleting a node in an AVL tree in C++. You can use this code as a starting point and extend it based on your requirements or the specific behavior you want to implement.

### 1. Algorithms & Data Structures (C++): Why AVL Tree?

AVL trees are a type of self-balancing binary search tree. They were the first such data structure to be invented and are named after their inventors, Adelson-Velsky and Landis. AVL trees maintain their balance by ensuring that the heights of the two child subtrees of any node differ by at most one. This balancing property helps keep the tree's height logarithmic, which ensures efficient search, insertion, and deletion operations.

Here are some reasons why AVL trees are useful:

1. **Guaranteed Logarithmic Height**: In a balanced AVL tree, the height is guaranteed to be O(log n), where n is the number of nodes in the tree. This ensures that operations such as search, insertion, and deletion have efficient time complexity.

2. **Balancing**: AVL trees automatically balance themselves after insertion or deletion operations. This property ensures that the tree remains relatively balanced, leading to predictable and efficient performance.

3. **Supports Efficient Operations**: Due to their balanced nature, AVL trees support efficient search, insertion, and deletion operations with time complexity of O(log n), where n is the number of nodes in the tree.

4. **Optimized for Dynamic Sets**: AVL trees are particularly useful when dealing with dynamic sets where the number of elements changes over time. They efficiently handle insertions and deletions while maintaining balance.

5. **Versatility**: AVL trees can be used in a wide range of applications such as databases, indexing, and implementing balanced search trees in programming languages.

However, it's worth noting that AVL trees have some overhead in terms of memory due to the need to store balance factors or heights at each node. Additionally, the balancing operations may require more complex code compared to simpler data structures like binary search trees. In cases where the overhead of AVL trees is deemed too high or where simpler operations are sufficient, other data structures like red-black trees might be preferred.

### 1. Algorithms & Data Structures (C++): What is an AVL Tree?

An AVL tree is a self-balancing binary search tree. It was the first such data structure to be invented and is named after its inventors, Adelson-Velsky and Landis.

In an AVL tree, the heights of the two child subtrees of any node differ by at most one. If they differ by more than one, rebalancing is performed to restore this property, thus ensuring that the tree remains balanced. This balancing is achieved through rotation operations.

AVL trees are advantageous because they guarantee logarithmic time complexity for insertion, deletion, and search operations, just like other balanced binary search trees such as red-black trees. However, AVL trees can be slightly more rigidly balanced than red-black trees, which can lead to faster lookups but potentially slower insertion and deletion operations.

In terms of implementation, each node in an AVL tree typically stores a key (or data) along with pointers to its left and right children. Additionally, each node usually maintains a balance factor which indicates the difference in height between its left and right subtrees. Rotation operations are performed to maintain this balance factor within the range [-1, 0, 1] for each node.

### 1. Algorithms & Data Structures (C++): LR-Rotation on AVL Trees

Sure, I can explain the LR-Rotation operation on AVL trees.

An AVL tree is a self-balancing binary search tree where the height difference between the left and right subtrees (balance factor) of any node is at most 1. When an insertion or deletion operation violates this property, rotations are performed to restore balance.

LR-Rotation is a combination of two rotations: Left-Rotation followed by Right-Rotation. It is used to rebalance an AVL tree when a node's subtree is unbalanced to the left and the right subtree of that node is unbalanced to the right.

Here are the steps for performing an LR-Rotation:

1. Perform a Left-Rotation on the left child of the unbalanced node.
2. Perform a Right-Rotation on the unbalanced node.

Let's illustrate this with an example:

Suppose we have the following AVL tree where the subtree rooted at node `A` is unbalanced:

```bash
          A
         / \
        B   C
       /     \
      D       E
```

In this tree, node `A` has a balance factor of -2 because the left subtree (`B`) is taller by 2 levels than the right subtree (`C`). Node `B` also has a balance factor of -1 because it has only one child. So, to rebalance this tree, we'll perform an LR-Rotation.

Here are the steps:

1. Left-Rotation on node `B`:

```bash
     B
    / \
   D   A
       / \
      C   E
```

After the left rotation, node `B` becomes the root of this subtree.

1. Right-Rotation on node `A`:

```bash
      B
     / \
    D   A
       / \
      C   E
```

After the right rotation, node `A` becomes the right child of node `B`, and the subtree is now balanced.

This results in the following balanced tree:

```bash
       B
      / \
     D   A
        / \
       C   E
```

That's the LR-Rotation operation in AVL trees. It ensures that the balance factor of each node in the AVL tree is maintained within the allowable range (-1, 0, 1).

### 1. Algorithms & Data Structures (C++): General form of AVL Rotations

AVL rotations are a set of operations used to maintain the balance property of AVL trees after insertion or deletion operations. AVL trees are self-balancing binary search trees where the heights of the two child subtrees of any node differ by at most one. When this balance property is violated due to an insertion or deletion, rotations are performed to restore balance.

In general, there are four types of rotations in AVL trees:

1. **Left Rotation (LL Rotation)**: This rotation is performed when the balance factor of a node becomes +2 and the balance factor of its right child is +1 or 0.

2. **Right Rotation (RR Rotation)**: This rotation is performed when the balance factor of a node becomes -2 and the balance factor of its left child is -1 or 0.

3. **Left-Right Rotation (LR Rotation)**: This rotation is performed when the balance factor of a node becomes +2 and the balance factor of its right child is -1.

4. **Right-Left Rotation (RL Rotation)**: This rotation is performed when the balance factor of a node becomes -2 and the balance factor of its left child is +1.

Below is the general form of these rotations in C++:

```cpp
struct Node {
    int key;
    Node* left;
    Node* right;
    int height;
};

// Function to perform left rotation
Node* leftRotate(Node* y) {
    Node* x = y->right;
    Node* T2 = x->left;

    // Perform rotation
    x->left = y;
    y->right = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    return x;
}

// Function to perform right rotation
Node* rightRotate(Node* x) {
    Node* y = x->left;
    Node* T2 = y->right;

    // Perform rotation
    y->right = x;
    x->left = T2;

    // Update heights
    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    return y;
}

// Function to perform left-right rotation
Node* leftRightRotate(Node* z) {
    z->left = leftRotate(z->left);
    return rightRotate(z);
}

// Function to perform right-left rotation
Node* rightLeftRotate(Node* z) {
    z->right = rightRotate(z->right);
    return leftRotate(z);
}
```

In these functions, `height()` is a utility function to get the height of a node, and it's assumed to be defined elsewhere. These rotations maintain the AVL tree property while performing necessary re-balancing.

### 1. Algorithms & Data Structures (C++): Constructing an AVL Tree

Constructing an AVL tree in C++ involves implementing the AVL tree data structure and the necessary operations to maintain its balance. Here's a basic outline of how you can do it:

```cpp
#include <iostream>
using namespace std;

// Node structure for AVL tree
struct Node {
    int key;
    Node *left;
    Node *right;
    int height;
};

// Utility function to get height of the tree
int height(Node *node) {
    if (node == nullptr)
        return 0;
    return node->height;
}

// Utility function to get maximum of two integers
int max(int a, int b) {
    return (a > b) ? a : b;
}

// Function to create a new node with given key
Node* newNode(int key) {
    Node* node = new Node();
    node->key = key;
    node->left = nullptr;
    node->right = nullptr;
    node->height = 1; // new node is initially added at leaf
    return node;
}

// Function to right rotate subtree rooted with y
Node* rightRotate(Node* y) {
    Node* x = y->left;
    Node* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    // Return new root
    return x;
}

// Function to left rotate subtree rooted with x
Node* leftRotate(Node* x) {
    Node* y = x->right;
    Node* T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    // Update heights
    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    // Return new root
    return y;
}

// Get Balance factor of node N
int getBalance(Node* node) {
    if (node == nullptr)
        return 0;
    return height(node->left) - height(node->right);
}

// Function to insert a key into AVL tree
Node* insert(Node* node, int key) {
    // Perform normal BST insertion
    if (node == nullptr)
        return newNode(key);

    if (key < node->key)
        node->left = insert(node->left, key);
    else if (key > node->key)
        node->right = insert(node->right, key);
    else // Equal keys are not allowed in BST
        return node;

    // Update height of this ancestor node
    node->height = 1 + max(height(node->left), height(node->right));

    // Get the balance factor of this ancestor node to check whether this node became unbalanced
    int balance = getBalance(node);

    // If this node becomes unbalanced, then there are four cases:

    // Left Left Case
    if (balance > 1 && key < node->left->key)
        return rightRotate(node);

    // Right Right Case
    if (balance < -1 && key > node->right->key)
        return leftRotate(node);

    // Left Right Case
    if (balance > 1 && key > node->left->key) {
        node->left = leftRotate(node->left);
        return rightRotate(node);
    }

    // Right Left Case
    if (balance < -1 && key < node->right->key) {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }

    // return the unchanged node pointer
    return node;
}

// Function to print preorder traversal of AVL tree
void preOrder(Node* root) {
    if (root != nullptr) {
        cout << root->key << " ";
        preOrder(root->left);
        preOrder(root->right);
    }
}

int main() {
    Node* root = nullptr;

    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 30);
    root = insert(root, 40);
    root = insert(root, 50);
    root = insert(root, 25);

    /* The constructed AVL Tree would be
                30
               /  \
             20   40
            /  \    \
          10   25   50
    */

    cout << "Preorder traversal of the constructed AVL tree is \n";
    preOrder(root);

    return 0;
}
```

This code provides a basic implementation of an AVL tree in C++. You can extend it further by implementing additional operations like deletion, searching, etc., as per your requirements.

### 1. Algorithms & Data Structures (C++): Idea behind AVL Trees

AVL trees are a type of self-balancing binary search tree. The idea behind AVL trees is to maintain a balance factor for each node in the tree, ensuring that the height difference between the left and right subtrees (the balance factor) of any node is no more than 1. This balance factor helps in maintaining the efficiency of operations like insertion, deletion, and searching in the tree.

Here's a brief overview of the key concepts behind AVL trees:

1. **Binary Search Tree (BST) Property**: Like all binary search trees, AVL trees maintain the BST property, which means that for every node, all nodes in its left subtree have values less than the node's value, and all nodes in its right subtree have values greater than the node's value.

2. **Balanced Factor**: In addition to the BST property, AVL trees maintain a balance factor for each node. The balance factor is the difference between the height of the left subtree and the height of the right subtree. It can be one of {-1, 0, 1} for each node in the tree.

3. **Balancing Operations**: Whenever an insertion or deletion operation is performed that violates the balance property of the AVL tree, one or more rotations are applied to restore balance. The rotations include single rotations (left or right) and double rotations (combination of left and right rotations or right and left rotations).

4. **Rotations**: Rotations are the fundamental operations used to balance the tree. They change the structure of the tree while maintaining the BST property. Rotations are performed based on the imbalance detected in the tree after insertion or deletion.

5. **Height-Balanced Tree**: An AVL tree is said to be height-balanced if the balance factor of every node in the tree is either -1, 0, or 1. This ensures that the height of the tree remains logarithmic, which in turn guarantees efficient search, insertion, and deletion operations.

6. **Complexity**: The AVL tree ensures a worst-case time complexity of O(log n) for basic operations like search, insertion, and deletion, where 'n' is the number of nodes in the tree.

Overall, AVL trees are designed to maintain a balance between efficient search operations and efficient insertion/deletion operations by ensuring that the height of the tree remains as small as possible. This balance is achieved by performing rotations whenever necessary to keep the tree height-balanced.

### 1. Algorithms & Data Structures (C++): Generating AVL Tree

Generating an AVL tree involves inserting elements while maintaining the balance property of the AVL tree, which ensures that the height difference between the left and right subtrees of any node is no more than one. Here's a basic implementation in C++:

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
    int height;
};

// Function to get height of the tree
int height(Node* node) {
    if (node == nullptr)
        return 0;
    return node->height;
}

// Function to get the maximum of two integers
int max(int a, int b) {
    return (a > b) ? a : b;
}

// Function to create a new node
Node* newNode(int data) {
    Node* node = new Node();
    node->data = data;
    node->left = nullptr;
    node->right = nullptr;
    node->height = 1; // New node is initially at height 1
    return node;
}

// Function to right rotate subtree rooted with y
Node* rightRotate(Node* y) {
    Node* x = y->left;
    Node* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    // Return new root
    return x;
}

// Function to left rotate subtree rooted with x
Node* leftRotate(Node* x) {
    Node* y = x->right;
    Node* T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    // Update heights
    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    // Return new root
    return y;
}

// Get Balance factor of node
int getBalance(Node* node) {
    if (node == nullptr)
        return 0;
    return height(node->left) - height(node->right);
}

// Recursive function to insert a key in the subtree rooted with node and returns the new root of the subtree
Node* insert(Node* node, int key) {
    // Perform the normal BST insertion
    if (node == nullptr)
        return newNode(key);

    if (key < node->data)
        node->left = insert(node->left, key);
    else if (key > node->data)
        node->right = insert(node->right, key);
    else // Equal keys are not allowed in BST
        return node;

    // Update height of this ancestor node
    node->height = 1 + max(height(node->left), height(node->right));

    // Get the balance factor of this ancestor node to check whether this node became unbalanced
    int balance = getBalance(node);

    // If this node becomes unbalanced, then there are four cases

    // Left Left Case
    if (balance > 1 && key < node->left->data)
        return rightRotate(node);

    // Right Right Case
    if (balance < -1 && key > node->right->data)
        return leftRotate(node);

    // Left Right Case
    if (balance > 1 && key > node->left->data) {
        node->left = leftRotate(node->left);
        return rightRotate(node);
    }

    // Right Left Case
    if (balance < -1 && key < node->right->data) {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }

    // return the (unchanged) node pointer
    return node;
}

// Function to print preorder traversal of the tree
void preOrder(Node* root) {
    if (root != nullptr) {
        cout << root->data << " ";
        preOrder(root->left);
        preOrder(root->right);
    }
}

int main() {
    Node* root = nullptr;

    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 30);
    root = insert(root, 40);
    root = insert(root, 50);
    root = insert(root, 25);

    cout << "Preorder traversal of the constructed AVL tree is: \n";
    preOrder(root);

    return 0;
}
```

This code includes functions to create a new node, calculate height, rotate nodes for balancing, insert elements, and print the preorder traversal of the AVL tree. You can customize the `main()` function to insert elements according to your requirements and then print the tree.

### 1. Algorithms & Data Structures (C++): Height Analysis of AVL Trees

Analyzing the height of AVL trees in C++ involves understanding the properties of AVL trees and how their heights are maintained through rotations during insertion and deletion operations. Here's a basic implementation along with an analysis of the height:

```cpp
#include <iostream>
#include <algorithm>

using namespace std;

// Definition of a node in AVL tree
struct Node {
    int key;
    Node* left;
    Node* right;
    int height;
};

// Function to create a new node
Node* createNode(int key) {
    Node* newNode = new Node();
    newNode->key = key;
    newNode->left = nullptr;
    newNode->right = nullptr;
    newNode->height = 1; // new node is initially at height 1
    return newNode;
}

// Function to calculate height of a node
int height(Node* node) {
    if (node == nullptr)
        return 0;
    return node->height;
}

// Function to perform single right rotation
Node* rotateRight(Node* y) {
    Node* x = y->left;
    Node* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = 1 + max(height(y->left), height(y->right));
    x->height = 1 + max(height(x->left), height(x->right));

    // Return new root
    return x;
}

// Function to perform single left rotation
Node* rotateLeft(Node* x) {
    Node* y = x->right;
    Node* T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    // Update heights
    x->height = 1 + max(height(x->left), height(x->right));
    y->height = 1 + max(height(y->left), height(y->right));

    // Return new root
    return y;
}

// Function to get the balance factor of a node
int getBalance(Node* node) {
    if (node == nullptr)
        return 0;
    return height(node->left) - height(node->right);
}

// Function to insert a key into AVL tree
Node* insert(Node* root, int key) {
    // Perform normal BST insertion
    if (root == nullptr)
        return createNode(key);

    if (key < root->key)
        root->left = insert(root->left, key);
    else if (key > root->key)
        root->right = insert(root->right, key);
    else // Duplicate keys not allowed
        return root;

    // Update height of this ancestor node
    root->height = 1 + max(height(root->left), height(root->right));

    // Get the balance factor to check whether this node became unbalanced
    int balance = getBalance(root);

    // If this node becomes unbalanced, perform rotations
    // Left Left Case
    if (balance > 1 && key < root->left->key)
        return rotateRight(root);

    // Right Right Case
    if (balance < -1 && key > root->right->key)
        return rotateLeft(root);

    // Left Right Case
    if (balance > 1 && key > root->left->key) {
        root->left = rotateLeft(root->left);
        return rotateRight(root);
    }

    // Right Left Case
    if (balance < -1 && key < root->right->key) {
        root->right = rotateRight(root->right);
        return rotateLeft(root);
    }

    // Return the unchanged node pointer
    return root;
}

// Function to calculate the height of the AVL tree
int avlHeight(Node* root) {
    if (root == nullptr)
        return 0;
    return root->height;
}

int main() {
    Node* root = nullptr;

    // Insert some elements into the AVL tree
    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 30);
    root = insert(root, 40);
    root = insert(root, 50);
    root = insert(root, 25);

    // Print the height of the AVL tree
    cout << "Height of AVL tree is " << avlHeight(root) << endl;

    return 0;
}
```

In this implementation:

- The `Node` struct represents a node in the AVL tree with its key value, left and right child pointers, and height.
- The `createNode()` function creates a new node with the given key.
- `rotateRight()` and `rotateLeft()` perform right and left rotations, respectively, to balance the tree.
- `insert()` function inserts a new key into the AVL tree and maintains the balance using rotations.
- `avlHeight()` function calculates the height of the AVL tree.

The height of an AVL tree is important because it determines the time complexity of various operations such as insertion, deletion, and search. In an AVL tree, the height is guaranteed to be O(log n), where n is the number of nodes in the tree. This guarantees efficient search and other operations.

### 1. Algorithms & Data Structures (C++): Insert a node in AVL (all together)

Sure, I can provide you with a C++ implementation of inserting a node in an AVL tree. AVL trees are self-balancing binary search trees, so after insertion, we may need to perform rotations to maintain the balance property.

Here's a complete implementation:

```cpp
#include <iostream>
using namespace std;

// Structure for a node of the AVL tree
struct Node {
    int key;
    Node *left;
    Node *right;
    int height;
};

// Utility function to get the height of a node
int height(Node *N) {
    if (N == nullptr)
        return 0;
    return N->height;
}

// Utility function to get the maximum of two integers
int max(int a, int b) {
    return (a > b) ? a : b;
}

// Function to create a new node with the given key
Node* newNode(int key) {
    Node* node = new Node();
    node->key = key;
    node->left = nullptr;
    node->right = nullptr;
    node->height = 1; // New node is initially at height 1
    return node;
}

// Function to right rotate subtree rooted with y
Node* rightRotate(Node* y) {
    Node* x = y->left;
    Node* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    // Return new root
    return x;
}

// Function to left rotate subtree rooted with x
Node* leftRotate(Node* x) {
    Node* y = x->right;
    Node* T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    // Update heights
    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    // Return new root
    return y;
}

// Get Balance factor of node N
int getBalance(Node* N) {
    if (N == nullptr)
        return 0;
    return height(N->left) - height(N->right);
}

// Recursive function to insert a key in the subtree rooted with node and
// returns the new root of the subtree.
Node* insert(Node* node, int key) {
    // 1. Perform the normal BST insertion
    if (node == nullptr)
        return newNode(key);

    if (key < node->key)
        node->left = insert(node->left, key);
    else if (key > node->key)
        node->right = insert(node->right, key);
    else // Duplicate keys not allowed
        return node;

    // 2. Update height of this ancestor node
    node->height = 1 + max(height(node->left), height(node->right));

    // 3. Get the balance factor of this ancestor node to check whether
    // this node became unbalanced
    int balance = getBalance(node);

    // If this node becomes unbalanced, then there are four cases

    // Left Left Case
    if (balance > 1 && key < node->left->key)
        return rightRotate(node);

    // Right Right Case
    if (balance < -1 && key > node->right->key)
        return leftRotate(node);

    // Left Right Case
    if (balance > 1 && key > node->left->key) {
        node->left = leftRotate(node->left);
        return rightRotate(node);
    }

    // Right Left Case
    if (balance < -1 && key < node->right->key) {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }

    // return the (unchanged) node pointer
    return node;
}

// A utility function to print preorder traversal of the tree.
// The function also prints height of every node
void preOrder(Node* root) {
    if (root != nullptr) {
        cout << root->key << " ";
        preOrder(root->left);
        preOrder(root->right);
    }
}

int main() {
    Node* root = nullptr;

    /* Constructing tree given in the above figure */
    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 30);
    root = insert(root, 40);
    root = insert(root, 50);
    root = insert(root, 25);

    /* The constructed AVL Tree would be
            30
           /  \
         20   40
        /  \     \
       10  25    50
    */
    cout << "Preorder traversal of the constructed AVL tree is \n";
    preOrder(root);

    return 0;
}
```

This code provides a complete implementation of AVL tree insertion in C++. The `Node` structure represents each node in the AVL tree, and the `insert` function inserts a new node into the tree while maintaining its AVL property by performing rotations when necessary. Finally, the `preOrder` function is used to print the tree in preorder traversal.

### 1. Algorithms & Data Structures (C++): Insert a node in AVL (Left Left Condition)

Inserting a node into an AVL tree involves balancing the tree after insertion to maintain its AVL property, which ensures that the tree remains balanced. The Left Left (LL) condition occurs when a new node is inserted into the left subtree of the left child of a node, causing the balance factor of the node's left child to become +2 and triggering a rotation.

Here's how you can implement the insertion of a node in the AVL tree in C++ with the Left Left condition:

```cpp
#include <iostream>

// AVL Node structure
struct AVLNode {
    int data;
    AVLNode* left;
    AVLNode* right;
    int height; // Height of the node
};

// Function to calculate height of a node
int height(AVLNode* node) {
    if (node == nullptr)
        return 0;
    return node->height;
}

// Function to get the balance factor of a node
int balanceFactor(AVLNode* node) {
    if (node == nullptr)
        return 0;
    return height(node->left) - height(node->right);
}

// Function to create a new AVL node
AVLNode* createNode(int data) {
    AVLNode* newNode = new AVLNode;
    newNode->data = data;
    newNode->left = nullptr;
    newNode->right = nullptr;
    newNode->height = 1;
    return newNode;
}

// Function to perform left rotation
AVLNode* leftRotate(AVLNode* y) {
    AVLNode* x = y->right;
    AVLNode* T2 = x->left;

    // Perform rotation
    x->left = y;
    y->right = T2;

    // Update heights
    y->height = std::max(height(y->left), height(y->right)) + 1;
    x->height = std::max(height(x->left), height(x->right)) + 1;

    // Return new root
    return x;
}

// Function to perform right rotation
AVLNode* rightRotate(AVLNode* x) {
    AVLNode* y = x->left;
    AVLNode* T2 = y->right;

    // Perform rotation
    y->right = x;
    x->left = T2;

    // Update heights
    x->height = std::max(height(x->left), height(x->right)) + 1;
    y->height = std::max(height(y->left), height(y->right)) + 1;

    // Return new root
    return y;
}

// Function to insert a new node into AVL tree
AVLNode* insertNode(AVLNode* root, int data) {
    // Perform standard BST insertion
    if (root == nullptr)
        return createNode(data);

    if (data < root->data)
        root->left = insertNode(root->left, data);
    else if (data > root->data)
        root->right = insertNode(root->right, data);
    else // Duplicate keys not allowed
        return root;

    // Update height of this ancestor node
    root->height = 1 + std::max(height(root->left), height(root->right));

    // Get the balance factor of this ancestor node
    int balance = balanceFactor(root);

    // Left Left Case
    if (balance > 1 && data < root->left->data)
        return rightRotate(root);

    // ... Other rotation cases (Left Right, Right Left, Right Right) can be added here

    return root;
}

// Function to print AVL tree (inorder traversal)
void inorderTraversal(AVLNode* root) {
    if (root != nullptr) {
        inorderTraversal(root->left);
        std::cout << root->data << " ";
        inorderTraversal(root->right);
    }
}

int main() {
    AVLNode* root = nullptr;

    // Insert nodes into AVL tree
    root = insertNode(root, 10);
    root = insertNode(root, 20);
    root = insertNode(root, 30);
    root = insertNode(root, 40);
    root = insertNode(root, 50);
    root = insertNode(root, 25);

    // Print AVL tree
    std::cout << "Inorder traversal of AVL tree: ";
    inorderTraversal(root);
    std::cout << std::endl;

    return 0;
}
```

In this code:

- `insertNode()` function is used to insert a new node into the AVL tree.
- `leftRotate()` and `rightRotate()` functions are used for rotation during balancing.
- `balanceFactor()` function calculates the balance factor of a node.
- `height()` function calculates the height of a node.
- `inorderTraversal()` function is used to perform an inorder traversal of the AVL tree for printing.

This code demonstrates the insertion of nodes in an AVL tree with the Left Left (LL) condition. You can extend it to handle other rotation cases such as Left Right (LR), Right Left (RL), and Right Right (RR) as needed.

### 1. Algorithms & Data Structures (C++): Insert a node in AVL (Left Right Condition)

Inserting a node in an AVL tree with the left-right imbalance condition involves performing a left rotation followed by a right rotation. Here's the C++ implementation:

```cpp
#include <iostream>
using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    int height;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr), height(1) {}
};

// Function to calculate the height of a node
int height(TreeNode* node) {
    if (node == nullptr)
        return 0;
    return node->height;
}

// Function to perform a right rotation
TreeNode* rightRotate(TreeNode* y) {
    TreeNode* x = y->left;
    TreeNode* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    return x;
}

// Function to perform a left rotation
TreeNode* leftRotate(TreeNode* x) {
    TreeNode* y = x->right;
    TreeNode* T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    // Update heights
    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    return y;
}

// Get balance factor of a node
int getBalance(TreeNode* node) {
    if (node == nullptr)
        return 0;
    return height(node->left) - height(node->right);
}

// Function to insert a node into AVL tree
TreeNode* insert(TreeNode* root, int val) {
    // Perform standard BST insertion
    if (root == nullptr)
        return new TreeNode(val);

    if (val < root->val)
        root->left = insert(root->left, val);
    else if (val > root->val)
        root->right = insert(root->right, val);
    else // Duplicate keys not allowed
        return root;

    // Update height of this ancestor node
    root->height = 1 + max(height(root->left), height(root->right));

    // Get the balance factor of this ancestor node to check whether this node became unbalanced
    int balance = getBalance(root);

    // If this node becomes unbalanced, then there are 4 cases

    // Left Left Case
    if (balance > 1 && val < root->left->val)
        return rightRotate(root);

    // Right Right Case
    if (balance < -1 && val > root->right->val)
        return leftRotate(root);

    // Left Right Case
    if (balance > 1 && val > root->left->val) {
        root->left = leftRotate(root->left);
        return rightRotate(root);
    }

    // Right Left Case
    if (balance < -1 && val < root->right->val) {
        root->right = rightRotate(root->right);
        return leftRotate(root);
    }

    // Return the unchanged node pointer
    return root;
}

// Function to perform inorder traversal of AVL tree
void inorder(TreeNode* root) {
    if (root == nullptr)
        return;
    inorder(root->left);
    cout << root->val << " ";
    inorder(root->right);
}

int main() {
    TreeNode* root = nullptr;

    // Inserting nodes into AVL tree
    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 30);
    root = insert(root, 15);
    root = insert(root, 25);

    // Print inorder traversal of the AVL tree
    cout << "Inorder traversal of AVL tree: ";
    inorder(root);
    cout << endl;

    return 0;
}
```

In this code:

- `insert` function inserts a new node into the AVL tree and performs rotations if necessary to balance the tree.
- `leftRotate` and `rightRotate` functions perform left and right rotations, respectively.
- `getBalance` function calculates the balance factor of a given node.
- `height` function calculates the height of a given node.
- `main` function demonstrates the usage of the AVL tree by inserting some nodes and printing the inorder traversal of the tree.

This code demonstrates the insertion of nodes into an AVL tree while maintaining balance, including the left-right imbalance condition.

### 1. Algorithms & Data Structures (C++): Insert a node in AVL (method)

Sure, here's a C++ implementation of inserting a node into an AVL tree:

```cpp
#include <iostream>
using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    int height; // Height of the subtree rooted at this node
    TreeNode(int x) : val(x), left(NULL), right(NULL), height(1) {}
};

// Function to get the height of a node
int height(TreeNode* node) {
    if (node == NULL)
        return 0;
    return node->height;
}

// Function to get the balance factor of a node
int balanceFactor(TreeNode* node) {
    if (node == NULL)
        return 0;
    return height(node->left) - height(node->right);
}

// Function to update the height of a node
void updateHeight(TreeNode* node) {
    if (node != NULL)
        node->height = 1 + max(height(node->left), height(node->right));
}

// Function to perform a right rotation
TreeNode* rightRotate(TreeNode* y) {
    TreeNode* x = y->left;
    TreeNode* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    updateHeight(y);
    updateHeight(x);

    return x;
}

// Function to perform a left rotation
TreeNode* leftRotate(TreeNode* x) {
    TreeNode* y = x->right;
    TreeNode* T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    // Update heights
    updateHeight(x);
    updateHeight(y);

    return y;
}

// Function to insert a node into AVL tree
TreeNode* insert(TreeNode* root, int val) {
    // Perform normal BST insertion
    if (root == NULL)
        return new TreeNode(val);

    if (val < root->val)
        root->left = insert(root->left, val);
    else if (val > root->val)
        root->right = insert(root->right, val);
    else // Duplicate values are not allowed
        return root;

    // Update height of this ancestor node
    updateHeight(root);

    // Get the balance factor of this ancestor node to check whether this node became unbalanced
    int balance = balanceFactor(root);

    // If the node becomes unbalanced, there are 4 cases

    // Left Left Case
    if (balance > 1 && val < root->left->val)
        return rightRotate(root);

    // Right Right Case
    if (balance < -1 && val > root->right->val)
        return leftRotate(root);

    // Left Right Case
    if (balance > 1 && val > root->left->val) {
        root->left = leftRotate(root->left);
        return rightRotate(root);
    }

    // Right Left Case
    if (balance < -1 && val < root->right->val) {
        root->right = rightRotate(root->right);
        return leftRotate(root);
    }

    // If the node is balanced, return the unchanged node pointer
    return root;
}

// Function to print the inorder traversal of the AVL tree
void inorder(TreeNode* root) {
    if (root != NULL) {
        inorder(root->left);
        cout << root->val << " ";
        inorder(root->right);
    }
}

// Driver code
int main() {
    TreeNode* root = NULL;

    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 30);
    root = insert(root, 40);
    root = insert(root, 50);
    root = insert(root, 25);

    cout << "Inorder traversal of the constructed AVL tree is: ";
    inorder(root);
    cout << endl;

    return 0;
}
```

This code implements the insertion operation in an AVL tree in C++. It includes functions for right and left rotations, as well as balancing the tree after insertion.

### 1. Algorithms & Data Structures (C++): Insert a node in AVL (Right Left Condition)

Sure, inserting a node in an AVL tree requires ensuring that the balance factor of each node in the tree remains within the range of -1, 0, or 1. When inserting a new node, we may need to perform rotations to rebalance the tree. The Right-Left condition occurs when the balance factor of the left child of the newly inserted node becomes -2, and the balance factor of its right child becomes 1.

Here's the C++ code to insert a node in an AVL tree with the Right-Left condition:

```cpp
#include <iostream>
#include <algorithm>

using namespace std;

struct Node {
    int key;
    Node* left;
    Node* right;
    int height;
};

// Function to get the height of a node
int height(Node* node) {
    if (node == nullptr)
        return 0;
    return node->height;
}

// Function to get the balance factor of a node
int getBalance(Node* node) {
    if (node == nullptr)
        return 0;
    return height(node->left) - height(node->right);
}

// Function to create a new node
Node* newNode(int key) {
    Node* node = new Node;
    node->key = key;
    node->left = nullptr;
    node->right = nullptr;
    node->height = 1;
    return node;
}

// Function to perform right rotation
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

// Function to perform left rotation
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

// Function to insert a node in AVL tree
Node* insert(Node* root, int key) {
    // Perform normal BST insertion
    if (root == nullptr)
        return newNode(key);

    if (key < root->key)
        root->left = insert(root->left, key);
    else if (key > root->key)
        root->right = insert(root->right, key);
    else // Equal keys are not allowed in BST
        return root;

    // Update height of this ancestor node
    root->height = 1 + max(height(root->left), height(root->right));

    // Get the balance factor of this ancestor node to check whether this node became unbalanced
    int balance = getBalance(root);

    // If this node becomes unbalanced, then there are four cases

    // Left Left Case
    if (balance > 1 && key < root->left->key)
        return rightRotate(root);

    // Right Right Case
    if (balance < -1 && key > root->right->key)
        return leftRotate(root);

    // Right Left Case
    if (balance < -1 && key < root->right->key) {
        root->right = rightRotate(root->right);
        return leftRotate(root);
    }

    // Left Right Case
    if (balance > 1 && key > root->left->key) {
        root->left = leftRotate(root->left);
        return rightRotate(root);
    }

    // return the (unchanged) node pointer
    return root;
}

// Function to print the inorder traversal of the AVL tree
void inorder(Node* root) {
    if (root != nullptr) {
        inorder(root->left);
        cout << root->key << " ";
        inorder(root->right);
    }
}

// Driver code
int main() {
    Node* root = nullptr;

    /* Constructing tree given in the above figure */
    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 30);
    root = insert(root, 40);
    root = insert(root, 50);
    root = insert(root, 25);

    /* The constructed AVL Tree would be
               30
              /  \
            20   40
           /  \     \
          10  25    50
    */
    cout << "Inorder traversal of the constructed AVL tree is \n";
    inorder(root);

    return 0;
}
```

This code implements the insertion of a node in an AVL tree in C++ with the Right-Left condition handled.

### 1. Algorithms & Data Structures (C++): Insert a node in AVL (Right Right Condition)

In AVL trees, the Right-Right condition occurs when a new node is inserted into the right subtree of the right child of a node, causing an imbalance. To restore balance, a single left rotation is performed. Here's how you can implement the insertion of a node in this condition in C++:

```cpp
#include <iostream>

struct Node {
    int key;
    Node* left;
    Node* right;
    int height;
};

int max(int a, int b) {
    return (a > b) ? a : b;
}

int height(Node* node) {
    if (node == nullptr)
        return 0;
    return node->height;
}

Node* newNode(int key) {
    Node* node = new Node();
    node->key = key;
    node->left = nullptr;
    node->right = nullptr;
    node->height = 1; // New node is initially added at leaf
    return node;
}

Node* rightRotate(Node* y) {
    Node* x = y->left;
    Node* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    // Return new root
    return x;
}

Node* insert(Node* node, int key) {
    // Perform normal BST insertion
    if (node == nullptr)
        return newNode(key);

    if (key < node->key)
        node->left = insert(node->left, key);
    else if (key > node->key)
        node->right = insert(node->right, key);
    else // Duplicate keys not allowed
        return node;

    // Update height of this ancestor node
    node->height = 1 + max(height(node->left), height(node->right));

    // Get balance factor to check if this node became unbalanced
    int balance = height(node->left) - height(node->right);

    // If node becomes unbalanced, there are four cases to consider

    // Right-Right Case
    if (balance < -1 && key > node->right->key)
        return rightRotate(node);

    // Other cases would go here...

    // Return the unchanged node pointer
    return node;
}

void preOrder(Node* root) {
    if (root != nullptr) {
        std::cout << root->key << " ";
        preOrder(root->left);
        preOrder(root->right);
    }
}

int main() {
    Node* root = nullptr;

    // Insert nodes into the AVL tree
    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 30);
    root = insert(root, 40);
    root = insert(root, 50);
    root = insert(root, 25);

    std::cout << "Preorder traversal of the constructed AVL tree is \n";
    preOrder(root);

    return 0;
}
```

This code demonstrates the insertion of nodes into an AVL tree and handles the Right-Right condition by performing a single left rotation. You can extend it to handle other imbalance conditions as well.

### 1. Algorithms & Data Structures (C++): Height Balanced Binary Search Trees

Height-balanced binary search trees (BSTs) are a type of self-balancing binary search tree where the height difference between the left and right subtrees of any node is at most 1. This ensures that the tree remains balanced and the time complexity of various operations like insertion, deletion, and search remains logarithmic.

One popular height-balanced binary search tree is the AVL tree, named after its inventors Adelson-Velsky and Landis. AVL trees maintain balance by performing rotations upon insertion or deletion to ensure that the height difference of the left and right subtrees of any node is at most 1.

Here's a basic implementation of an AVL tree in C++:

```cpp
#include <iostream>
using namespace std;

// AVL Node
struct Node {
    int key;
    Node* left;
    Node* right;
    int height;
};

// Function to get the height of a node
int height(Node* node) {
    if (node == nullptr)
        return 0;
    return node->height;
}

// Function to get the maximum of two integers
int max(int a, int b) {
    return (a > b) ? a : b;
}

// Create a new AVL node
Node* newNode(int key) {
    Node* node = new Node();
    node->key = key;
    node->left = nullptr;
    node->right = nullptr;
    node->height = 1; // New node is initially added at leaf
    return node;
}

// Rotate right
Node* rightRotate(Node* y) {
    Node* x = y->left;
    Node* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    // Return new root
    return x;
}

// Rotate left
Node* leftRotate(Node* x) {
    Node* y = x->right;
    Node* T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    // Update heights
    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    // Return new root
    return y;
}

// Get balance factor of node
int getBalance(Node* node) {
    if (node == nullptr)
        return 0;
    return height(node->left) - height(node->right);
}

// Insert a new key into the tree
Node* insert(Node* node, int key) {
    // Perform the normal BST insertion
    if (node == nullptr)
        return newNode(key);

    if (key < node->key)
        node->left = insert(node->left, key);
    else if (key > node->key)
        node->right = insert(node->right, key);
    else // Equal keys are not allowed in BST
        return node;

    // Update height of this ancestor node
    node->height = 1 + max(height(node->left), height(node->right));

    // Get the balance factor of this ancestor node to check whether this node became unbalanced
    int balance = getBalance(node);

    // If this node becomes unbalanced, then there are four cases

    // Left Left Case
    if (balance > 1 && key < node->left->key)
        return rightRotate(node);

    // Right Right Case
    if (balance < -1 && key > node->right->key)
        return leftRotate(node);

    // Left Right Case
    if (balance > 1 && key > node->left->key) {
        node->left = leftRotate(node->left);
        return rightRotate(node);
    }

    // Right Left Case
    if (balance < -1 && key < node->right->key) {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }

    // return the (unchanged) node pointer
    return node;
}

// Function to print inorder traversal of the tree
void inorder(Node* root) {
    if (root != nullptr) {
        inorder(root->left);
        cout << root->key << " ";
        inorder(root->right);
    }
}

// Main function
int main() {
    Node* root = nullptr;

    // Inserting elements into the tree
    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 30);
    root = insert(root, 40);
    root = insert(root, 50);
    root = insert(root, 25);

    // Print inorder traversal of the AVL tree
    cout << "Inorder traversal of AVL tree: ";
    inorder(root);
    cout << endl;

    return 0;
}
```

This code demonstrates the basic operations of insertion into an AVL tree. Similar operations can be implemented for deletion and searching. The `insert()` function ensures that the tree remains balanced after each insertion by performing rotations when necessary. The `inorder()` function is used to print the inorder traversal of the AVL tree.

### 1. Algorithms & Data Structures (C++): LL Rotation on AVL

Sure, let's delve into performing a left-left rotation in an AVL tree. AVL trees are a type of self-balancing binary search tree where the heights of the two child subtrees of any node differ by at most one.

Here's a simple C++ implementation for a left-left rotation in an AVL tree:

```cpp
#include <iostream>
using namespace std;

// Structure for a node in the AVL tree
struct Node {
    int data;
    Node* left;
    Node* right;
    int height;
};

// Function to get height of a node
int height(Node* node) {
    if (node == nullptr)
        return 0;
    return node->height;
}

// Function to create a new node
Node* createNode(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->left = nullptr;
    newNode->right = nullptr;
    newNode->height = 1; // new node is initially added at leaf
    return newNode;
}

// Function to perform a left rotation
Node* leftRotate(Node* y) {
    Node* x = y->right;
    Node* T2 = x->left;

    // Perform rotation
    x->left = y;
    y->right = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    // Return new root
    return x;
}

// Function to perform an inorder traversal of the AVL tree
void inorderTraversal(Node* root) {
    if (root == nullptr)
        return;
    inorderTraversal(root->left);
    cout << root->data << " ";
    inorderTraversal(root->right);
}

int main() {
    Node* root = nullptr;
    root = createNode(10);
    root->left = createNode(5);
    root->right = createNode(15);
    root->left->left = createNode(2);
    root->left->right = createNode(8);

    cout << "Inorder traversal before rotation: ";
    inorderTraversal(root);
    cout << endl;

    root = leftRotate(root);

    cout << "Inorder traversal after left rotation: ";
    inorderTraversal(root);
    cout << endl;

    return 0;
}
```

This code demonstrates how to perform a left rotation on an AVL tree. The `leftRotate` function takes the node around which rotation is to be done (denoted by `y`), performs the rotation, updates the heights, and returns the new root of the subtree.

In the `main` function, an example AVL tree is constructed, and a left rotation is performed around the root node. Finally, the inorder traversal is printed before and after the rotation to verify the correctness of the rotation operation.

### 1. Algorithms & Data Structures (C++): LL-Rotation on AVL Trees

Sure, LL-Rotation is a rotation operation used in AVL trees to balance the tree when a node becomes unbalanced due to a left-left (LL) case. In this case, the left subtree of the left child of the unbalanced node is higher by two levels compared to the right subtree of the left child.

Here's how LL-Rotation works step by step:

1. **Identify the Unbalanced Node**: You start by identifying the unbalanced node, let's call it `A`.
2. **Identify the Left Child**: The left child of `A` is `B`.
3. **Perform the Rotation**:
    - Promote `B` as the new root by making `A` its right child.
    - If `B` had a right subtree, detach it and attach it as the left subtree of `A`.
4. **Update Heights**: Recalculate the heights of `A` and `B`.
5. **Return the New Root**: Return the new root of the subtree.

Here's a C++ implementation of the LL-Rotation operation:

```cpp
#include <iostream>
#include <algorithm>

using namespace std;

// AVL Tree Node
struct Node {
    int key;
    Node *left;
    Node *right;
    int height;
};

// Function to create a new AVL node
Node* newNode(int key) {
    Node* node = new Node();
    node->key = key;
    node->left = nullptr;
    node->right = nullptr;
    node->height = 1; // New node is initially added at leaf
    return(node);
}

// Function to get height of the tree
int height(Node* node) {
    if (node == nullptr)
        return 0;
    return node->height;
}

// Function to perform LL Rotation
Node* llRotate(Node* A) {
    Node* B = A->left;
    Node* temp = B->right;

    // Perform rotation
    B->right = A;
    A->left = temp;

    // Update heights
    A->height = max(height(A->left), height(A->right)) + 1;
    B->height = max(height(B->left), height(B->right)) + 1;

    // Return new root
    return B;
}

// Function to print pre-order traversal of the tree
void preOrder(Node* root) {
    if(root != nullptr) {
        cout << root->key << " ";
        preOrder(root->left);
        preOrder(root->right);
    }
}

int main() {
    Node* root = nullptr;

    /* Constructing tree given in the above figure */
    root = newNode(10);
    root->left = newNode(5);
    root->right = newNode(15);
    root->left->left = newNode(2);
    root->left->right = newNode(7);

    cout << "Pre-order traversal of the constructed AVL tree is \n";
    preOrder(root);

    // Perform LL Rotation
    root = llRotate(root);

    cout << "\nPre-order traversal after LL rotation of the constructed AVL tree is \n";
    preOrder(root);

    return 0;
}
```

This code demonstrates the LL-Rotation operation on an AVL tree. You can modify it according to your requirements or integrate it into your AVL tree implementation.

### 1. Algorithms & Data Structures (C++): Inserting in AVL with Rotations

In C++, implementing insertion in an AVL tree with rotations involves a few steps:

1. Perform a standard BST insertion.
2. Update the height of the current node.
3. Check balance factor to see if the tree has become unbalanced.
4. If unbalanced, perform rotations to balance the tree.

Here's a basic implementation:

```cpp
#include <iostream>
using namespace std;

// AVL tree node structure
struct Node {
    int key;
    Node *left, *right;
    int height;
};

// Calculate the height of a node
int height(Node *node) {
    if (node == nullptr)
        return 0;
    return node->height;
}

// Create a new node
Node* newNode(int key) {
    Node* node = new Node();
    node->key = key;
    node->left = node->right = nullptr;
    node->height = 1; // New node is initially added at leaf
    return(node);
}

// Right rotation
Node* rightRotate(Node* y) {
    Node* x = y->left;
    Node* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    // Return new root
    return x;
}

// Left rotation
Node* leftRotate(Node* x) {
    Node* y = x->right;
    Node* T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    // Update heights
    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    // Return new root
    return y;
}

// Get balance factor of a node
int getBalance(Node* node) {
    if (node == nullptr)
        return 0;
    return height(node->left) - height(node->right);
}

// Insert a new key into the tree
Node* insert(Node* node, int key) {
    // Perform standard BST insertion
    if (node == nullptr)
        return newNode(key);

    if (key < node->key)
        node->left = insert(node->left, key);
    else if (key > node->key)
        node->right = insert(node->right, key);
    else // Equal keys are not allowed in BST
        return node;

    // Update height of this ancestor node
    node->height = 1 + max(height(node->left), height(node->right));

    // Get the balance factor of this ancestor node
    int balance = getBalance(node);

    // If the node becomes unbalanced, there are 4 cases

    // Left Left Case
    if (balance > 1 && key < node->left->key)
        return rightRotate(node);

    // Right Right Case
    if (balance < -1 && key > node->right->key)
        return leftRotate(node);

    // Left Right Case
    if (balance > 1 && key > node->left->key) {
        node->left = leftRotate(node->left);
        return rightRotate(node);
    }

    // Right Left Case
    if (balance < -1 && key < node->right->key) {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }

    // return the (unchanged) node pointer
    return node;
}

// Print the tree in-order
void inOrder(Node* root) {
    if (root != nullptr) {
        inOrder(root->left);
        cout << root->key << " ";
        inOrder(root->right);
    }
}

// Driver program to test above functions
int main() {
    Node* root = nullptr;

    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 30);
    root = insert(root, 40);
    root = insert(root, 50);
    root = insert(root, 25);

    cout << "Inorder traversal of the constructed AVL tree is: ";
    inOrder(root);
    cout << endl;

    return 0;
}
```

This code provides the basic structure for an AVL tree with insertion and rotations in C++. You can test it by adding more insertions and checking if the tree remains balanced.

### 1. Algorithms & Data Structures (C++): Insertion in AVL Tree

Sure, I can guide you through inserting a node into an AVL tree in C++. An AVL tree is a self-balancing binary search tree where the heights of the two child subtrees of any node differ by at most one. Here's a basic implementation of insertion in an AVL tree:

```cpp
#include <iostream>
using namespace std;

// Node structure for AVL tree
struct Node {
    int data;
    Node* left;
    Node* right;
    int height; // Height of the node
};

// Function to get height of a node
int height(Node* node) {
    if (node == nullptr)
        return 0;
    return node->height;
}

// Function to get the balance factor of a node
int getBalance(Node* node) {
    if (node == nullptr)
        return 0;
    return height(node->left) - height(node->right);
}

// Function to create a new node
Node* createNode(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->left = nullptr;
    newNode->right = nullptr;
    newNode->height = 1; // New node is initially at height 1
    return newNode;
}

// Function to perform right rotation
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

// Function to perform left rotation
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

// Function to insert a node into the AVL tree
Node* insert(Node* root, int data) {
    // Perform standard BST insertion
    if (root == nullptr)
        return createNode(data);

    if (data < root->data)
        root->left = insert(root->left, data);
    else if (data > root->data)
        root->right = insert(root->right, data);
    else // Duplicate keys not allowed
        return root;

    // Update height of this ancestor node
    root->height = 1 + max(height(root->left), height(root->right));

    // Get the balance factor of this ancestor node to check whether this node became unbalanced
    int balance = getBalance(root);

    // If this node becomes unbalanced, there are four cases

    // Left Left Case
    if (balance > 1 && data < root->left->data)
        return rightRotate(root);

    // Right Right Case
    if (balance < -1 && data > root->right->data)
        return leftRotate(root);

    // Left Right Case
    if (balance > 1 && data > root->left->data) {
        root->left = leftRotate(root->left);
        return rightRotate(root);
    }

    // Right Left Case
    if (balance < -1 && data < root->right->data) {
        root->right = rightRotate(root->right);
        return leftRotate(root);
    }

    // If the tree is balanced, return the unchanged node
    return root;
}

// Function to print the inorder traversal of the AVL tree
void inOrder(Node* root) {
    if (root != nullptr) {
        inOrder(root->left);
        cout << root->data << " ";
        inOrder(root->right);
    }
}

int main() {
    Node* root = nullptr;

    // Inserting nodes into the AVL tree
    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 30);
    root = insert(root, 40);
    root = insert(root, 50);
    root = insert(root, 25);

    // Printing the inorder traversal of the AVL tree
    cout << "Inorder traversal of AVL tree: ";
    inOrder(root);
    cout << endl;

    return 0;
}
```

This code provides a basic implementation of insertion in an AVL tree in C++. It includes functions for creating nodes, calculating heights and balance factors, performing rotations, inserting nodes, and printing the inorder traversal of the AVL tree. You can extend it further based on your requirements.

### 1. Algorithms & Data Structures (C++): LR Rotation on AVL

Sure, let's talk about performing an LR rotation on an AVL tree in C++.

An AVL tree is a self-balancing binary search tree. LR rotation is one of the operations used to balance the tree when it becomes unbalanced due to insertions or deletions.

In an LR rotation, we first perform a right rotation on the left child of the node (to make it a right child), and then a left rotation on the node itself. This helps in restoring the balance factor of the tree.

Here's a basic implementation of an LR rotation on an AVL tree in C++:

```cpp
#include <iostream>

using namespace std;

// AVL Node structure
struct AVLNode {
    int data;
    AVLNode* left;
    AVLNode* right;
    int height;
};

// Function to get height of a node
int height(AVLNode* node) {
    if (node == nullptr)
        return 0;
    return node->height;
}

// Function to perform right rotation
AVLNode* rightRotate(AVLNode* y) {
    AVLNode* x = y->left;
    AVLNode* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    // Return new root
    return x;
}

// Function to perform left rotation
AVLNode* leftRotate(AVLNode* x) {
    AVLNode* y = x->right;
    AVLNode* T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    // Update heights
    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    // Return new root
    return y;
}

// Function to perform LR rotation
AVLNode* LRrotation(AVLNode* z) {
    z->left = leftRotate(z->left);
    return rightRotate(z);
}

// Function to create a new AVL node
AVLNode* newNode(int data) {
    AVLNode* node = new AVLNode();
    node->data = data;
    node->left = nullptr;
    node->right = nullptr;
    node->height = 1; // New node is initially added at leaf
    return node;
}

// Function to print the tree in in-order traversal
void inOrder(AVLNode* root) {
    if (root == nullptr)
        return;
    inOrder(root->left);
    cout << root->data << " ";
    inOrder(root->right);
}

// Driver code
int main() {
    AVLNode* root = nullptr;
    
    /* Constructing tree given in the above figure */
    root = newNode(30);
    root->left = newNode(20);
    root->right = newNode(40);
    root->left->left = newNode(10);
    root->left->right = newNode(25);
    
    cout << "Inorder traversal of the constructed AVL tree is \n";
    inOrder(root);
    cout << endl;

    // Performing LR rotation
    root = LRrotation(root);

    cout << "Inorder traversal after LR rotation \n";
    inOrder(root);

    return 0;
}
```

In this code:

- `AVLNode` is a structure representing a node in the AVL tree. It contains data, pointers to left and right children, and the height of the node.
- `rightRotate` and `leftRotate` functions perform right and left rotations, respectively.
- `LRrotation` function performs the LR rotation, which first applies a left rotation on the left child of the node and then a right rotation on the node itself.
- `newNode` function creates a new node with the given data.
- `inOrder` function performs an in-order traversal of the tree.
- In the `main` function, an AVL tree is constructed, and then LR rotation is performed on it. Finally, the tree is printed before and after the rotation.

### 1. Algorithms & Data Structures (C++): Performance Analysis of AVL Trees

Analyzing the performance of AVL trees involves understanding their time complexity for various operations such as insertion, deletion, and search. Here's a brief overview:

1. **Insertion**: When inserting a new node into an AVL tree, the tree may need to be rebalanced to maintain its height balance property. The worst-case time complexity for insertion is O(log n), where n is the number of nodes in the tree. This is because AVL trees are self-balancing, ensuring that the height of the tree remains O(log n) after each insertion.

2. **Deletion**: Similar to insertion, deletion in AVL trees may require rebalancing to maintain the AVL property. The worst-case time complexity for deletion is also O(log n) since it involves finding the node to delete and then rebalancing the tree if necessary.

3. **Search**: Searching for a node in an AVL tree also has a worst-case time complexity of O(log n). This is because AVL trees are binary search trees, and their structure ensures that the search space is halved at each step as you traverse down the tree.

4. **Rotation Operations**: Rotations are the fundamental operations used in AVL tree insertion and deletion to maintain balance. Single rotations (left or right) and double rotations (left-right or right-left) have a constant time complexity of O(1).

5. **Space Complexity**: The space complexity of an AVL tree is O(n), where n is the number of nodes in the tree. Each node requires a constant amount of memory, and the additional overhead for maintaining balance does not significantly affect the overall space complexity.

It's important to note that while AVL trees guarantee O(log n) time complexity for most operations, the constant factors involved may make them slower in practice compared to other balanced binary search trees like red-black trees. However, AVL trees are still valuable in scenarios where strict balance is required or where insertions and deletions are infrequent compared to searches.

### 1. Algorithms & Data Structures (C++): RL-Rotation on AVL Trees

Sure! RL-Rotation is a specific rotation operation used in AVL trees to balance the tree when a left-right imbalance occurs. In AVL trees, balancing is essential to maintain the height balance property, which ensures efficient search, insertion, and deletion operations.

Here's a brief overview of how RL-Rotation works:

1. **Identify the Imbalance**: RL-Rotation is performed when a node has a left subtree that is higher than its right subtree, and the left child of the node has a right subtree heavier than its left subtree.

2. **Perform a Double Rotation**: RL-Rotation involves two rotation operations. First, a single rotation is performed on the left child node using RR-Rotation (Right-Right Rotation), and then a single rotation is performed on the original node using LL-Rotation (Left-Left Rotation).

3. **Balance Factor Update**: After the rotations, the balance factors of the affected nodes and their ancestors are updated to ensure that the AVL tree properties are maintained.

Here's an example of how RL-Rotation is implemented in C++:

```cpp
#include <iostream>
using namespace std;

struct Node {
    int key;
    Node* left;
    Node* right;
    int height;
};

// Function to perform LL-Rotation
Node* leftRotate(Node* x) {
    Node* y = x->right;
    Node* T2 = y->left;

    y->left = x;
    x->right = T2;

    // Update heights
    x->height = max(x->left->height, x->right->height) + 1;
    y->height = max(y->left->height, y->right->height) + 1;

    return y;
}

// Function to perform RR-Rotation
Node* rightRotate(Node* y) {
    Node* x = y->left;
    Node* T2 = x->right;

    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(y->left->height, y->right->height) + 1;
    x->height = max(x->left->height, x->right->height) + 1;

    return x;
}

// Function to get the height of a node
int height(Node* N) {
    if (N == nullptr)
        return 0;
    return N->height;
}

// Function to perform RL-Rotation
Node* RLRotation(Node* z) {
    z->left = leftRotate(z->left); // Perform RR-Rotation on z's left child
    return rightRotate(z); // Perform LL-Rotation on z
}

// Function to create a new node
Node* newNode(int key) {
    Node* node = new Node();
    node->key = key;
    node->left = nullptr;
    node->right = nullptr;
    node->height = 1; // New node is initially added at leaf
    return node;
}

// Function to insert a new key in AVL tree
Node* insert(Node* node, int key) {
    // Perform standard BST insertion
    if (node == nullptr)
        return newNode(key);

    if (key < node->key)
        node->left = insert(node->left, key);
    else if (key > node->key)
        node->right = insert(node->right, key);
    else // Duplicate keys not allowed
        return node;

    // Update height of this ancestor node
    node->height = 1 + max(height(node->left), height(node->right));

    // Get the balance factor of this ancestor node to check whether this node became unbalanced
    int balance = height(node->left) - height(node->right);

    // If this node becomes unbalanced, then there are four cases

    // Left Left Case
    if (balance > 1 && key < node->left->key)
        return rightRotate(node);

    // Right Right Case
    if (balance < -1 && key > node->right->key)
        return leftRotate(node);

    // Left Right Case
    if (balance > 1 && key > node->left->key)
        return RLRotation(node);

    return node;
}

// Function to print the inorder traversal of the AVL tree
void inOrder(Node* root) {
    if (root != nullptr) {
        inOrder(root->left);
        cout << root->key << " ";
        inOrder(root->right);
    }
}

int main() {
    Node* root = nullptr;

    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 30);
    root = insert(root, 40);
    root = insert(root, 50);
    root = insert(root, 25);

    cout << "Inorder traversal of the AVL tree is: ";
    inOrder(root);
    cout << endl;

    return 0;
}
```

In this example, the `RLRotation` function performs the RL-Rotation. The `insert` function is used to insert new keys into the AVL tree while maintaining balance. Finally, the `inOrder` function is used to print the inorder traversal of the AVL tree to verify that it's balanced.

### 1. Algorithms & Data Structures (C++): Rotations on AVL Trees

Rotations are fundamental operations in AVL trees, a self-balancing binary search tree. AVL trees maintain balance by ensuring that the height difference between the left and right subtrees of any node is at most 1.

There are four types of rotations in AVL trees:

1. **Left Rotation (LL Rotation)**: This rotation is used to balance a node when its right subtree is heavier. It involves rotating the heavier node downwards to the left.

2. **Right Rotation (RR Rotation)**: This rotation is used to balance a node when its left subtree is heavier. It involves rotating the heavier node downwards to the right.

3. **Left-Right Rotation (LR Rotation)**: This rotation is a combination of left and right rotations. It is used to balance a node when its left subtree's right subtree is heavier.

4. **Right-Left Rotation (RL Rotation)**: This rotation is a combination of right and left rotations. It is used to balance a node when its right subtree's left subtree is heavier.

Here's a C++ implementation of AVL tree rotations:

```cpp
struct Node {
    int key;
    Node *left;
    Node *right;
    int height;
};

// Function to get the height of a node
int height(Node *node) {
    if (node == nullptr)
        return 0;
    return node->height;
}

// Function to perform a right rotation
Node* rightRotate(Node* y) {
    Node* x = y->left;
    Node* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = 1 + max(height(y->left), height(y->right));
    x->height = 1 + max(height(x->left), height(x->right));

    return x;
}

// Function to perform a left rotation
Node* leftRotate(Node* x) {
    Node* y = x->right;
    Node* T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    // Update heights
    x->height = 1 + max(height(x->left), height(x->right));
    y->height = 1 + max(height(y->left), height(y->right));

    return y;
}

// Function to perform a left-right rotation
Node* leftRightRotate(Node* z) {
    z->left = leftRotate(z->left);
    return rightRotate(z);
}

// Function to perform a right-left rotation
Node* rightLeftRotate(Node* z) {
    z->right = rightRotate(z->right);
    return leftRotate(z);
}
```

These functions can be used to perform rotations during insertion and deletion in an AVL tree to maintain its balance. Proper use of rotations ensures that the AVL tree remains balanced, optimizing search, insertion, and deletion operations.

### 1. Algorithms & Data Structures (C++): RR-Rotation on AVL Trees

Sure, I can explain the RR rotation on AVL trees.

AVL trees are a type of self-balancing binary search tree. They maintain their balance by ensuring that the heights of the left and right subtrees of any node differ by at most one. When this balance property is violated during insertion or deletion operations, rotations are performed to restore the balance.

An RR rotation is one of the rotation operations used in AVL trees. It is applied when a node becomes unbalanced due to a right-right case. A right-right case occurs when a node's right subtree is taller by two levels compared to its left subtree, and the imbalance exists in the right subtree of the right child of the unbalanced node.

Here's the general idea of an RR rotation:

1. Let's say we have a tree with an unbalanced node, let's call it "A", with its right child, "B", and B's right child, "C".

   ```bash
        A
         \
          B
           \
            C
   ```

2. To perform an RR rotation, we need to make B the new root of this subtree. B will replace A as the root, and A will become the left child of B. The right child of B (C) becomes the left child of A.

   ```bash
        B
       / \
      A   C
   ```

3. Now, we need to adjust the heights of nodes A and B. The height of A should be recalculated based on its new position, as well as the height of B.

4. Finally, the subtree rooted at B (including its left child, if any) may have additional nodes. We also need to recompute the height of this subtree.

This rotation operation helps maintain the balance property of the AVL tree. After performing the RR rotation, the heights of the left and right subtrees of every node along the path from the root to the newly rotated node are balanced within one level.

### 1. Algorithms & Data Structures (C++): Time and Space complexity of AVL Tree

An AVL (Adelson-Velsky and Landis) tree is a self-balancing binary search tree. In an AVL tree, the heights of the two child subtrees of any node differ by at most one. This property helps in maintaining balance during insertions and deletions, which ensures that the tree remains approximately balanced and guarantees a worst-case time complexity of O(log n) for insertion, deletion, and search operations.

Here's a breakdown of the time and space complexities for various operations on AVL trees:

1. **Insertion:**  
   - Time Complexity: O(log n)  
   - Space Complexity: O(log n) due to recursive calls on the stack (considering the worst-case scenario of a completely unbalanced tree).

2. **Deletion:**  
   - Time Complexity: O(log n)  
   - Space Complexity: O(log n) due to recursive calls on the stack.

3. **Search:**  
   - Time Complexity: O(log n)  
   - Space Complexity: O(1) for iterative search and O(log n) for recursive search (due to recursive calls on the stack).

4. **Balancing Operations (Rotation):**  
   - Time Complexity: O(1) per rotation operation.

5. **Space Complexity of the Tree:**  
   - Space Complexity: O(n) for storing n elements in the AVL tree. This includes space for storing the elements themselves and the necessary overhead for the tree structure.

Overall, AVL trees provide efficient time complexities for various operations, especially for insertion, deletion, and search, while ensuring that the tree remains balanced, leading to predictable performance in most cases. However, the space complexity can be relatively higher compared to simpler data structures like arrays or linked lists due to the overhead of maintaining the tree structure and balancing information.
