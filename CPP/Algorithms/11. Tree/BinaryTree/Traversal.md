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
