
### 1. Algorithms & Data Structures (C++): Leetcode: 3 Sum

The 3Sum problem on LeetCode is a classic algorithmic problem that involves finding all unique triplets in an array that sum up to zero. Here's a C++ implementation using a two-pointer approach:

```cpp
#include <vector>
#include <algorithm>

using namespace std;

class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> result;
        
        if (nums.size() < 3)
            return result;
        
        sort(nums.begin(), nums.end());
        
        for (int i = 0; i < nums.size() - 2; ++i) {
            // Skip duplicate values for the first element
            if (i > 0 && nums[i] == nums[i - 1])
                continue;
            
            int target = -nums[i];
            int left = i + 1;
            int right = nums.size() - 1;
            
            while (left < right) {
                int sum = nums[left] + nums[right];
                
                if (sum == target) {
                    result.push_back({nums[i], nums[left], nums[right]});
                    
                    // Skip duplicate values for the second element
                    while (left < right && nums[left] == nums[left + 1])
                        left++;
                    
                    // Skip duplicate values for the third element
                    while (left < right && nums[right] == nums[right - 1])
                        right--;
                    
                    left++;
                    right--;
                } else if (sum < target) {
                    left++;
                } else {
                    right--;
                }
            }
        }
        
        return result;
    }
};
```

This solution starts by sorting the input array. Then, it iterates through each element of the array. For each element, it uses two pointers (`left` and `right`) to find the other two elements such that the sum is equal to the negative of the current element. It skips duplicate values to avoid duplicates in the result.

### 1. Algorithms & Data Structures (C++): Leetcode: Alien Dictionary

The Alien Dictionary problem on LeetCode is a classic problem that involves sorting words in an alien language using a given alphabetical order. Here's a brief overview of the problem and a possible approach to solve it:

#### Problem Overview

You're given a list of strings representing words in an alien language sorted lexicographically based on a given alphabet. You need to determine the order of characters in the alien language.

#### Approach

1. **Build a Graph:** First, build a graph representing the relationships between characters based on the given words and their order.
2. **Topological Sorting:** Perform a topological sort on the graph to find the order of characters.
3. **Handle Edge Cases:** Handle cases where there might be cycles in the graph or ambiguous characters.

#### Steps in Detail

1. **Build Graph:**
   - Iterate through adjacent words.
   - Compare corresponding characters and add edges between them.
   - Break the loop when finding the first differing characters.

2. **Topological Sorting:**
   - Perform a DFS (Depth-First Search) on the graph.
   - Maintain a visited set to avoid cycles.
   - Keep track of the order of visited nodes.

3. **Handle Cycles:**
   - If a cycle is detected, the alien language order is ambiguous.
   - Handle such cases accordingly.

#### C++ Code Sketch

Here's a basic structure of how you can implement the solution:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
#include <unordered_set>

using namespace std;

class Solution {
public:
    string alienOrder(vector<string>& words) {
        unordered_map<char, unordered_set<char>> graph;
        unordered_map<char, int> indegree;
        buildGraph(words, graph, indegree);
        return topologicalSort(graph, indegree);
    }

private:
    void buildGraph(vector<string>& words, unordered_map<char, unordered_set<char>>& graph, unordered_map<char, int>& indegree) {
        // Implement graph building logic here
    }

    string topologicalSort(unordered_map<char, unordered_set<char>>& graph, unordered_map<char, int>& indegree) {
        // Implement topological sorting logic here
    }
};

int main() {
    Solution sol;
    vector<string> words = {"wrt", "wrf", "er", "ett", "rftt"};
    cout << "Alien Dictionary: " << sol.alienOrder(words) << endl;
    return 0;
}
```

#### Conclusion

This problem involves building a graph based on the given words and then performing a topological sort to determine the order of characters. Handling cycles and ambiguous cases is essential for a correct solution. This approach ensures efficiency and correctness when solving the Alien Dictionary problem.

### 1. Algorithms & Data Structures (C++): Leetcode: Array

Leetcode is a fantastic resource for practicing coding problems, including those related to arrays, which are fundamental data structures in programming. Here are some common array-related problems on Leetcode along with their solutions in C++:

1. **Two Sum**: Given an array of integers, return indices of the two numbers such that they add up to a specific target.

   ```cpp
   vector<int> twoSum(vector<int>& nums, int target) {
       unordered_map<int, int> numToIndex;
       for (int i = 0; i < nums.size(); ++i) {
           int complement = target - nums[i];
           if (numToIndex.count(complement))
               return {numToIndex[complement], i};
           numToIndex[nums[i]] = i;
       }
       return {}; // No solution found
   }
   ```

2. **Maximum Subarray**: Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

   ```cpp
   int maxSubArray(vector<int>& nums) {
       int maxSum = nums[0], currentSum = nums[0];
       for (int i = 1; i < nums.size(); ++i) {
           currentSum = max(nums[i], currentSum + nums[i]);
           maxSum = max(maxSum, currentSum);
       }
       return maxSum;
   }
   ```

3. **Rotate Array**: Rotate an array to the right by k steps, where k is non-negative.

   ```cpp
   void rotate(vector<int>& nums, int k) {
       int n = nums.size();
       k %= n;
       reverse(nums.begin(), nums.end());
       reverse(nums.begin(), nums.begin() + k);
       reverse(nums.begin() + k, nums.end());
   }
   ```

4. **Contains Duplicate**: Given an array of integers, find if the array contains any duplicates.

   ```cpp
   bool containsDuplicate(vector<int>& nums) {
       unordered_set<int> numSet;
       for (int num : nums) {
           if (numSet.count(num)) return true;
           numSet.insert(num);
       }
       return false;
   }
   ```

These are just a few examples. Leetcode offers a wide variety of array problems to practice, ranging from easy to hard difficulty levels. Working through them is a great way to solidify your understanding of arrays and improve your problem-solving skills!

### 1. Algorithms & Data Structures (C++): Leetcode: Best Time to Buy and Sell Stock

Certainly! The "Best Time to Buy and Sell Stock" problem on LeetCode is a classic algorithmic problem where you're given an array representing the prices of a stock on different days. The task is to find the maximum profit that can be achieved by making one transaction (buying and selling one share of the stock) given that you can only buy and sell the stock once.

Here's the problem statement:

**Problem Statement:**
Say you have an array `prices` for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.

**Example:**

```bash
Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.
```

**Approach (Brute Force):**
One naive approach is to consider every pair of days (i, j) and find the maximum difference `prices[j] - prices[i]` where `j > i`. However, this approach has a time complexity of O(n^2), which is not efficient.

**Optimized Approach:**
To solve this problem efficiently, you can iterate through the array once and keep track of the minimum price encountered so far (`minPrice`) and the maximum profit (`maxProfit`). At each step, you update `maxProfit` as the maximum of its current value and the difference between the current price and `minPrice`. This way, you ensure that you're considering the maximum profit achievable till the current day.

Here's the C++ code implementing this approach:

```cpp
#include <vector>
#include <algorithm>

class Solution {
public:
    int maxProfit(std::vector<int>& prices) {
        int minPrice = INT_MAX;
        int maxProfit = 0;
        
        for (int i = 0; i < prices.size(); ++i) {
            if (prices[i] < minPrice) {
                minPrice = prices[i];
            } else if (prices[i] - minPrice > maxProfit) {
                maxProfit = prices[i] - minPrice;
            }
        }
        
        return maxProfit;
    }
};
```

This solution has a time complexity of O(n), where n is the size of the `prices` array, as it only requires a single pass through the array.

### 1. Algorithms & Data Structures (C++): Leetcode: Binary

When diving into algorithms and data structures with C++, LeetCode is an excellent resource for practicing and mastering your skills. Binary problems often revolve around manipulating binary trees, searching and sorting algorithms, and bitwise operations. Here are some common types of binary problems you might encounter on LeetCode:

1. **Binary Tree Problems**: These involve tasks related to binary trees, such as traversals (pre-order, in-order, post-order), constructing binary trees, finding the maximum/minimum depth, checking if a tree is balanced, and solving problems like validating BST (Binary Search Tree).

2. **Binary Search Problems**: These typically involve searching for an element or determining properties of the element in a sorted array or matrix using binary search. You might encounter problems like finding the first/last occurrence of an element in a sorted array, searching in rotated sorted arrays, or finding peak elements.

3. **Bit Manipulation Problems**: These involve performing bitwise operations on integers. You might need to solve problems like finding the single non-duplicate element in an array, counting the number of set bits, or performing bitwise operations like XOR, AND, OR, etc.

4. **Dynamic Programming with Binary States**: Some dynamic programming problems involve using binary states to represent certain conditions. For example, in problems like the subset sum problem, you might represent whether an element is included or not with a binary state.

5. **Graph Problems with Binary Operations**: In some graph problems, you might need to use binary operations or bitwise operations to represent certain conditions or states efficiently. For example, you might use a bit mask to represent the visited nodes in a graph traversal.

To tackle these problems effectively, ensure you have a solid understanding of binary trees, binary search, bitwise operations, and dynamic programming techniques. Practicing regularly on LeetCode will help you sharpen your problem-solving skills and become proficient in algorithms and data structures with C++.

### 1. Algorithms & Data Structures (C++): Leetcode: Binary Tree Level Order Traversal

Certainly! The Binary Tree Level Order Traversal problem on LeetCode is a classic problem that involves traversing a binary tree level by level and returning its node values at each level in a nested list. Here's a C++ implementation using a breadth-first search (BFS) approach:

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
    if (root == nullptr) return result;

    queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        int levelSize = q.size();
        vector<int> currentLevel;

        for (int i = 0; i < levelSize; ++i) {
            TreeNode* currentNode = q.front();
            q.pop();
            currentLevel.push_back(currentNode->val);

            if (currentNode->left) q.push(currentNode->left);
            if (currentNode->right) q.push(currentNode->right);
        }

        result.push_back(currentLevel);
    }

    return result;
}

// Helper function to create a binary tree
TreeNode* createTree() {
    TreeNode* root = new TreeNode(3);
    root->left = new TreeNode(9);
    root->right = new TreeNode(20);
    root->right->left = new TreeNode(15);
    root->right->right = new TreeNode(7);
    return root;
}

// Helper function to print the result
void printResult(const vector<vector<int>>& result) {
    for (const auto& level : result) {
        for (int val : level) {
            cout << val << " ";
        }
        cout << endl;
    }
}

int main() {
    TreeNode* root = createTree();
    vector<vector<int>> result = levelOrder(root);
    printResult(result);
    return 0;
}
```

This implementation uses a queue to perform a level-order traversal of the binary tree. It starts from the root node and iteratively visits each node in the tree level by level, pushing its children nodes into the queue for the next level traversal. Finally, it returns a nested vector containing the node values at each level.

### 1. Algorithms & Data Structures (C++): Leetcode: Binary Tree Maximum Path Sum

To solve the "Binary Tree Maximum Path Sum" problem on LeetCode, you can use a recursive approach known as depth-first search (DFS) to traverse the binary tree. Here's a C++ implementation:

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
    int maxPathSum(TreeNode* root) {
        int maxSum = INT_MIN;
        maxPathSumHelper(root, maxSum);
        return maxSum;
    }

    int maxPathSumHelper(TreeNode* node, int& maxSum) {
        if (node == NULL) return 0;
        
        // Calculate the maximum sum of paths starting from the left and right children
        int leftMax = max(0, maxPathSumHelper(node->left, maxSum));
        int rightMax = max(0, maxPathSumHelper(node->right, maxSum));
        
        // Update the maximum path sum with the current node included
        maxSum = max(maxSum, leftMax + rightMax + node->val);
        
        // Return the maximum path sum starting from this node
        return max(leftMax, rightMax) + node->val;
    }
};

int main() {
    // Example usage
    TreeNode* root = new TreeNode(10);
    root->left = new TreeNode(2);
    root->right = new TreeNode(10);
    root->left->left = new TreeNode(20);
    root->left->right = new TreeNode(1);
    root->right->right = new TreeNode(-25);
    root->right->right->left = new TreeNode(3);
    root->right->right->right = new TreeNode(4);

    Solution sol;
    cout << "Maximum path sum: " << sol.maxPathSum(root) << endl;

    return 0;
}
```

In this implementation, `maxPathSumHelper` is a helper function that calculates the maximum path sum starting from the current node. It recursively computes the maximum path sums of the left and right subtrees, and updates `maxSum` with the maximum path sum found so far. Finally, it returns the maximum path sum starting from the current node.

The `maxPathSum` function simply initializes the `maxSum` variable and calls the helper function to compute the maximum path sum of the entire tree.

### 1. Algorithms & Data Structures (C++): Leetcode: Climbing Stairs

Sure, let's discuss the "Climbing Stairs" problem from LeetCode.

**Problem Statement:**

You are climbing a staircase. It takes n steps to reach the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

**Example:**

```bash
Input: n = 3
Output: 3
Explanation: There are three ways to climb to the top:
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

**Approach:**

This problem can be solved using dynamic programming. The idea is to recognize that the number of ways to climb to the ith step is the sum of the number of ways to climb to the (i-1)th step and the number of ways to climb to the (i-2)th step. This is because at any point, you can only take steps of size 1 or 2.

**Solution (C++):**

Here's a simple C++ implementation using dynamic programming:

```cpp
#include <vector>

class Solution {
public:
    int climbStairs(int n) {
        if (n <= 2)
            return n;
        
        std::vector<int> dp(n + 1, 0);
        dp[1] = 1;
        dp[2] = 2;
        
        for (int i = 3; i <= n; ++i) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        
        return dp[n];
    }
};
```

**Explanation:**

- We initialize a vector `dp` of size `n + 1` to store the number of ways to climb to each step from 0 to n.
- Base cases: `dp[1] = 1` (one way to climb to the 1st step) and `dp[2] = 2` (two ways to climb to the 2nd step).
- We iterate from 3 to n, calculating the number of ways to climb to each step using the formula `dp[i] = dp[i - 1] + dp[i - 2]`.
- Finally, we return `dp[n]`, which represents the number of ways to climb to the nth step.

### 1. Algorithms & Data Structures (C++): Leetcode: Clone Graph

To solve the "Clone Graph" problem on LeetCode, you essentially need to clone an undirected graph. Here's how you can approach it using C++:

```cpp
#include <unordered_map>
#include <unordered_set>
#include <vector>
#include <queue>

using namespace std;

// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> neighbors;
    
    Node() {
        val = 0;
        neighbors = vector<Node*>();
    }
    
    Node(int _val) {
        val = _val;
        neighbors = vector<Node*>();
    }
    
    Node(int _val, vector<Node*> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
};

class Solution {
public:
    Node* cloneGraph(Node* node) {
        if (node == nullptr) return nullptr;
        
        // Map to store original nodes and their corresponding cloned nodes
        unordered_map<Node*, Node*> visited;
        
        // Use BFS to traverse the original graph
        queue<Node*> q;
        q.push(node);
        
        // Clone the first node
        visited[node] = new Node(node->val);
        
        while (!q.empty()) {
            Node* curr = q.front();
            q.pop();
            
            // Iterate through the neighbors of the current node
            for (Node* neighbor : curr->neighbors) {
                // If the neighbor hasn't been visited yet, clone it and add to the queue
                if (visited.find(neighbor) == visited.end()) {
                    visited[neighbor] = new Node(neighbor->val);
                    q.push(neighbor);
                }
                // Update the neighbors of the cloned current node
                visited[curr]->neighbors.push_back(visited[neighbor]);
            }
        }
        
        // Return the cloned graph
        return visited[node];
    }
};
```

This solution uses BFS to traverse the graph and creates a clone of each node while maintaining the connections between them. The unordered_map `visited` is used to keep track of visited nodes in the original graph and their corresponding cloned nodes.

### 1. Algorithms & Data Structures (C++): Leetcode: Coin Change

"Coin Change" is a classic dynamic programming problem often encountered in coding interviews and competitive programming. The problem statement typically goes like this:

Given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money, return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return `-1`.

Here's an approach to solving this problem using dynamic programming in C++:

```cpp
#include <vector>
#include <climits>

using namespace std;

int coinChange(vector<int>& coins, int amount) {
    // Create a dp array to store the minimum number of coins needed to make up each amount
    vector<int> dp(amount + 1, INT_MAX);
    dp[0] = 0; // Base case: 0 coins needed to make 0 amount
    
    // Iterate through all possible amounts from 1 to the given amount
    for (int i = 1; i <= amount; ++i) {
        // Try using each coin denomination to make up the current amount
        for (int coin : coins) {
            // If the current coin denomination is less than or equal to the current amount
            if (coin <= i && dp[i - coin] != INT_MAX) {
                // Update the minimum number of coins needed to make up the current amount
                dp[i] = min(dp[i], dp[i - coin] + 1);
            }
        }
    }
    
    // If dp[amount] is still INT_MAX, it means no combination of coins can make up the amount
    return dp[amount] == INT_MAX ? -1 : dp[amount];
}

// Example usage:
int main() {
    vector<int> coins = {1, 2, 5}; // Example coin denominations
    int amount = 11; // Example amount
    int minCoins = coinChange(coins, amount);
    cout << "Minimum number of coins needed: " << minCoins << endl;
    return 0;
}
```

This solution utilizes bottom-up dynamic programming to build up the answer incrementally. The `dp` array is initialized with `INT_MAX`, except for `dp[0]` which is set to `0` since it requires 0 coins to make up an amount of 0. Then, for each amount from 1 to the given `amount`, it tries using each coin denomination to make up the current amount. If using a certain coin denomination results in a smaller number of coins needed compared to the current minimum, it updates the `dp` array accordingly. Finally, it returns `dp[amount]` if it's less than `INT_MAX`, otherwise `-1`.

### 1. Algorithms & Data Structures (C++): Leetcode: Combination Sum IV

Combination Sum IV is a classic dynamic programming problem on LeetCode. The problem statement typically asks you to find the number of combinations that sum up to a given target, using elements from a given array of numbers. The twist here is that you're counting combinations, not just finding whether a sum is possible or not.

Here's a basic approach to solve this problem using dynamic programming:

```cpp
#include <vector>

int combinationSum4(std::vector<int>& nums, int target) {
    std::vector<unsigned int> dp(target + 1); // dp[i] stores the number of combinations to make sum i
    dp[0] = 1; // Base case: 1 way to make sum 0
    
    for (int i = 1; i <= target; ++i) {
        for (int j = 0; j < nums.size(); ++j) {
            if (i - nums[j] >= 0) {
                dp[i] += dp[i - nums[j]]; // Update dp[i] by adding the number of combinations to make sum i - nums[j]
            }
        }
    }
    
    return dp[target];
}
```

In this solution:

- We use a vector `dp` to store the number of combinations to make each sum from 0 to the target.
- We initialize `dp[0]` to 1 because there is one way to make a sum of 0 (by choosing no element).
- We iterate from 1 to the target, and for each value `i`, we iterate through the given numbers.
- For each number `nums[j]`, if `i - nums[j]` is non-negative, it means we can use `nums[j]` to make the sum `i`, so we add the number of combinations to make `i - nums[j]` to `dp[i]`.
- Finally, we return `dp[target]`, which stores the number of combinations to make the target sum.

This solution has a time complexity of O(target * nums.size()) and a space complexity of O(target) since we are using dynamic programming to store intermediate results.

### 1. Algorithms & Data Structures (C++): Leetcode: Construct Binary Tree from Preorder and Inorder Traversal

Constructing a binary tree from its preorder and inorder traversals is a classic problem in algorithms and data structures. It's commonly asked in coding interviews and is an excellent exercise to understand tree traversal and recursion. Here's a C++ implementation for solving this problem using the LeetCode platform:

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
        // Create a map to store indices of elements in inorder traversal
        unordered_map<int, int> indexMap;
        for (int i = 0; i < inorder.size(); ++i) {
            indexMap[inorder[i]] = i;
        }
        
        return build(preorder, 0, preorder.size() - 1, inorder, 0, inorder.size() - 1, indexMap);
    }
    
    TreeNode* build(vector<int>& preorder, int preStart, int preEnd, vector<int>& inorder, int inStart, int inEnd, unordered_map<int, int>& indexMap) {
        if (preStart > preEnd || inStart > inEnd)
            return nullptr;
        
        // Root is the first element in preorder traversal
        int rootVal = preorder[preStart];
        TreeNode* root = new TreeNode(rootVal);
        
        // Find the index of root in inorder traversal
        int rootIndexInInorder = indexMap[rootVal];
        
        // Calculate the number of elements in the left subtree
        int leftSubtreeSize = rootIndexInInorder - inStart;
        
        // Recursively build left and right subtrees
        root->left = build(preorder, preStart + 1, preStart + leftSubtreeSize, inorder, inStart, rootIndexInInorder - 1, indexMap);
        root->right = build(preorder, preStart + leftSubtreeSize + 1, preEnd, inorder, rootIndexInInorder + 1, inEnd, indexMap);
        
        return root;
    }
};

// Function to print the inorder traversal of a binary tree
void printInorder(TreeNode* root) {
    if (root == nullptr)
        return;
    
    printInorder(root->left);
    cout << root->val << " ";
    printInorder(root->right);
}

int main() {
    Solution sol;
    vector<int> preorder = {3, 9, 20, 15, 7};
    vector<int> inorder = {9, 3, 15, 20, 7};
    TreeNode* root = sol.buildTree(preorder, inorder);
    
    cout << "Inorder Traversal of the constructed tree: ";
    printInorder(root);
    
    return 0;
}
```

This C++ solution follows the following approach:

1. We create a map to store the indices of elements in the inorder traversal. This map helps us efficiently find the index of any element in the inorder traversal.
2. We define a recursive function `build` that takes the preorder and inorder traversals along with their start and end indices. It constructs the binary tree recursively.
3. In each recursive call, we identify the root of the subtree by taking the first element in the preorder traversal. Then we find the index of this root in the inorder traversal.
4. We calculate the size of the left subtree and recursively build both the left and right subtrees.
5. Finally, we return the root of the subtree.
6. In the `main` function, we create a sample preorder and inorder traversal arrays, construct the binary tree using the `buildTree` function, and then print the inorder traversal to verify the correctness of the constructed tree.

### 1. Algorithms & Data Structures (C++): Leetcode: Container With Most Water

Sure! The problem "Container With Most Water" on LeetCode is a classic problem that can be solved using a two-pointer approach. Here's a C++ solution:

```cpp
#include <vector>
#include <algorithm>

using namespace std;

class Solution {
public:
    int maxArea(vector<int>& height) {
        int maxArea = 0;
        int left = 0;
        int right = height.size() - 1;
        
        while (left < right) {
            int minHeight = min(height[left], height[right]);
            int width = right - left;
            int area = minHeight * width;
            maxArea = max(maxArea, area);
            
            if (height[left] < height[right])
                left++;
            else
                right--;
        }
        
        return maxArea;
    }
};
```

Explanation:

- We use two pointers, `left` and `right`, initialized to the beginning and the end of the array respectively.
- At each step, we calculate the area formed by the lines at `left` and `right`, which is the minimum of the two heights multiplied by the width between them.
- We keep track of the maximum area found so far.
- We move the pointer pointing to the shorter line towards the other pointer, as moving the pointer pointing to the longer line cannot increase the area, and the only chance to get a larger area is to try a longer line. This is because if we keep the pointer to the shorter line and move the pointer to the longer line, the width will decrease, and the height of the shorter line won't increase, so the area won't increase either.
- We continue this process until the two pointers meet, and return the maximum area found.

### 1. Algorithms & Data Structures (C++): Leetcode: Contains Duplicate

Sure, I can provide you with a solution to the "Contains Duplicate" problem on LeetCode using C++. The problem statement typically goes like this:

Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

Here's a sample solution in C++:

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>

bool containsDuplicate(std::vector<int>& nums) {
    std::unordered_set<int> numSet;
    for (int num : nums) {
        if (numSet.find(num) != numSet.end()) {
            // Found a duplicate
            return true;
        } else {
            numSet.insert(num);
        }
    }
    return false;
}

int main() {
    std::vector<int> nums = {1, 2, 3, 4, 5}; // Example input
    std::cout << "Contains duplicate? " << (containsDuplicate(nums) ? "Yes" : "No") << std::endl;
    return 0;
}
```

Explanation:

- We use an unordered_set (`numSet`) to keep track of the unique elements we have encountered so far.
- We iterate through the input array (`nums`).
- For each element in `nums`, we check if it already exists in `numSet`. If it does, we've found a duplicate, so we return `true`.
- If the element does not exist in `numSet`, we insert it into `numSet`.
- If the loop completes without finding any duplicates, we return `false`.

This solution has a time complexity of O(n) because we only need to iterate through the array once, and each lookup and insertion operation in the unordered_set is on average O(1).

### 1. Algorithms & Data Structures (C++): Leetcode: Counting Bits

The "Counting Bits" problem on LeetCode is a classic dynamic programming question. The problem statement asks you to count the number of 1's in the binary representation of every number from 0 to n, where n is a non-negative integer.

Here's a C++ solution using dynamic programming:

```cpp
#include <vector>

std::vector<int> countBits(int num) {
    std::vector<int> result(num + 1, 0);
    for (int i = 1; i <= num; ++i) {
        // To count the number of set bits in i, we shift i to the right by one bit
        // and add the least significant bit of i to the number of set bits in i >> 1.
        // This is a classic dynamic programming approach.
        result[i] = result[i >> 1] + (i & 1);
    }
    return result;
}
```

Explanation:

- We initialize a vector `result` of size `num + 1` to store the counts of set bits for each number from 0 to `num`.
- We iterate from 1 to `num` and calculate the number of set bits for each number using dynamic programming.
- For each number `i`, we count the number of set bits in `i` as the number of set bits in `i >> 1` (right shift by one bit) plus the least significant bit of `i`, which is `(i & 1)`.

This solution has a time complexity of O(n) and a space complexity of O(n), where n is the given input number.

### 1. Algorithms & Data Structures (C++): Leetcode: Decode Ways

The "Decode Ways" problem on LeetCode is a classic dynamic programming problem. The task is to decode a given string, where each character represents a digit, into letters (A-Z) given that 'A' is mapped to 1, 'B' is mapped to 2, ..., 'Z' is mapped to 26. The goal is to count the number of ways to decode the string.

Here's a C++ solution using dynamic programming:

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

int numDecodings(string s) {
    int n = s.length();
    if (n == 0) return 0;
    
    vector<int> dp(n + 1, 0);
    dp[0] = 1; // Empty string can be decoded in one way

    // If the first character is '0', then there is no way to decode
    dp[1] = s[0] == '0' ? 0 : 1;
    
    for (int i = 2; i <= n; ++i) {
        // Single digit
        if (s[i - 1] != '0') {
            dp[i] += dp[i - 1];
        }
        
        // Double digits
        int twoDigits = stoi(s.substr(i - 2, 2));
        if (twoDigits >= 10 && twoDigits <= 26) {
            dp[i] += dp[i - 2];
        }
    }
    
    return dp[n];
}

int main() {
    string s = "226";
    cout << "Number of ways to decode: " << numDecodings(s) << endl;
    return 0;
}
```

Explanation:

- We use dynamic programming to solve the problem. `dp[i]` represents the number of ways to decode the string ending at index `i`.
- We initialize `dp[0]` as 1, because an empty string can be decoded in one way.
- If the first character is '0', then there is no way to decode it, so `dp[1]` is 0.
- Then we iterate through the string. For each character, we consider decoding it as a single digit and as part of a double digit.
- If the character itself is not '0', it can be decoded alone.
- If the current character and the previous character form a valid double digit, we add the number of ways to decode the string ending at index `i-2` to `dp[i]`.
- Finally, `dp[n]` contains the number of ways to decode the entire string `s`.
- The time complexity of this solution is O(n), where n is the length of the input string.

### 1. Algorithms & Data Structures (C++): Leetcode: Design Add and Search Words Data Structure

To implement the "Design Add and Search Words Data Structure" problem from LeetCode, you can use a Trie data structure. Here's a basic outline of how you can approach it in C++:

```cpp
#include <iostream>
#include <unordered_map>

using namespace std;

class TrieNode {
public:
    unordered_map<char, TrieNode*> children;
    bool isEnd;

    TrieNode() {
        isEnd = false;
    }
};

class WordDictionary {
private:
    TrieNode* root;

public:
    WordDictionary() {
        root = new TrieNode();
    }

    void addWord(string word) {
        TrieNode* node = root;
        for (char ch : word) {
            if (!node->children[ch])
                node->children[ch] = new TrieNode();
            node = node->children[ch];
        }
        node->isEnd = true;
    }

    bool searchUtil(string word, TrieNode* node, int index) {
        if (index == word.size()) {
            return node->isEnd;
        }

        char ch = word[index];
        if (ch == '.') { // If it's a wildcard
            for (auto& child : node->children) {
                if (searchUtil(word, child.second, index + 1))
                    return true;
            }
            return false;
        } else {
            if (node->children[ch])
                return searchUtil(word, node->children[ch], index + 1);
            else
                return false;
        }
    }

    bool search(string word) {
        return searchUtil(word, root, 0);
    }
};

int main() {
    WordDictionary obj;
    obj.addWord("bad");
    obj.addWord("dad");
    obj.addWord("mad");

    cout << boolalpha;
    cout << obj.search("pad") << endl; // false
    cout << obj.search("bad") << endl; // true
    cout << obj.search(".ad") << endl; // true
    cout << obj.search("b..") << endl; // true

    return 0;
}
```

This implementation uses a Trie to store words. For search operations, it handles wildcard characters ('.') by exploring all possible branches of the Trie at each level.

You can extend this implementation further to handle other functionalities or optimize it based on specific requirements.

### 1. Algorithms & Data Structures (C++): Leetcode: Detect Cycle in a Linked List

Detecting a cycle in a linked list is a classic problem in data structures. One common approach is to use Floyd's Tortoise and Hare algorithm, also known as the "fast and slow pointers" approach. Here's how you can implement it in C++:

```cpp
#include <iostream>

struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

bool hasCycle(ListNode *head) {
    if (!head || !head->next)
        return false;

    ListNode *slow = head;
    ListNode *fast = head->next;

    while (fast && fast->next) {
        if (slow == fast)
            return true;

        slow = slow->next;
        fast = fast->next->next;
    }

    return false;
}

int main() {
    // Example usage
    ListNode *head = new ListNode(3);
    head->next = new ListNode(2);
    head->next->next = new ListNode(0);
    head->next->next->next = new ListNode(-4);
    // Create a cycle
    head->next->next->next->next = head->next;

    if (hasCycle(head))
        std::cout << "The linked list contains a cycle.\n";
    else
        std::cout << "The linked list does not contain a cycle.\n";

    // Free memory
    ListNode *current = head;
    while (current) {
        ListNode *temp = current;
        current = current->next;
        delete temp;
    }

    return 0;
}
```

In this code:

- We define a `ListNode` structure to represent each node in the linked list.
- The `hasCycle` function takes the head of the linked list as input and returns `true` if there is a cycle in the list, and `false` otherwise.
- Inside `hasCycle`, we initialize two pointers: `slow` moves one step at a time, while `fast` moves two steps at a time.
- If there's a cycle in the linked list, eventually the fast pointer will catch up to the slow pointer.
- If `fast` reaches the end of the list (`nullptr`), then there's no cycle in the list.
- In the `main` function, we create a linked list with a cycle for demonstration purposes.

### 1. Algorithms & Data Structures (C++): Leetcode: Dynamic Programming

Sure! Dynamic programming (DP) is a technique used to solve problems by breaking them down into simpler subproblems and solving each subproblem only once, storing the results to avoid redundant calculations. It's especially useful for optimization problems where you need to find the best solution among a set of possible solutions.

LeetCode offers a plethora of dynamic programming problems across different difficulty levels. Here's a general approach you can take to solve dynamic programming problems on LeetCode using C++:

1. **Understand the Problem**: Read and understand the problem statement carefully. Identify the inputs, outputs, constraints, and any edge cases.

2. **Identify Recurrence Relation**: Dynamic programming problems can often be solved by defining a recurrence relation, which describes how to break down the problem into smaller subproblems. Identify this relation, which will help you define your DP state.

3. **Define DP Array/Variables**: Decide on the data structure to store intermediate results. This could be a 1D, 2D, or even higher-dimensional array depending on the problem. Initialize the DP array/variables with base cases.

4. **Fill the DP Table/Array**: Use the recurrence relation to iteratively fill the DP table/array from smaller subproblems to larger ones, ensuring that you only compute each subproblem once.

5. **Handle Edge Cases**: Make sure to handle any edge cases or boundary conditions properly.

6. **Compute Final Result**: Once the DP table/array is filled, the final result can be found either by looking up the value in the DP table/array or by maintaining additional information during the DP process.

7. **Code Implementation**: Write the code to implement the DP solution in C++.

8. **Optimize (if necessary)**: Sometimes, DP solutions can be optimized further by reducing the space complexity or by optimizing the time complexity through clever techniques.

Here's a simple example problem: **"Climbing Stairs"**. Given a staircase with n steps, you can climb either 1 or 2 steps at a time. In how many distinct ways can you climb to the top?

**Solution**:

```cpp
class Solution {
public:
    int climbStairs(int n) {
        if (n <= 1) return 1;
        vector<int> dp(n + 1, 0);
        dp[0] = 1;
        dp[1] = 1;
        for (int i = 2; i <= n; ++i) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
};
```

This is a basic dynamic programming problem where the recurrence relation is `dp[i] = dp[i - 1] + dp[i - 2]`, meaning the number of ways to reach step `i` is the sum of ways to reach step `i - 1` and `i - 2`.

### 1. Algorithms & Data Structures (C++): Leetcode: Encode and Decode Strings (Leetcode Premium)

Sure, here's a possible implementation of the "Encode and Decode Strings" problem from LeetCode using C++:

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

class Codec {
public:

    // Encodes a list of strings to a single string.
    string encode(vector<string>& strs) {
        string encoded;
        for (const string& str : strs) {
            encoded += to_string(str.length()) + "#" + str;
        }
        return encoded;
    }

    // Decodes a single string to a list of strings.
    vector<string> decode(string s) {
        vector<string> decoded;
        int i = 0;
        while (i < s.length()) {
            int delimiter_pos = s.find('#', i);
            int length = stoi(s.substr(i, delimiter_pos - i));
            decoded.push_back(s.substr(delimiter_pos + 1, length));
            i = delimiter_pos + length + 1;
        }
        return decoded;
    }
};

int main() {
    Codec codec;
    vector<string> original = {"hello", "world", "leetcode"};
    
    // Encode the list of strings
    string encoded_str = codec.encode(original);
    cout << "Encoded String: " << encoded_str << endl;

    // Decode the encoded string
    vector<string> decoded_strs = codec.decode(encoded_str);
    cout << "Decoded Strings:" << endl;
    for (const auto& str : decoded_strs) {
        cout << str << endl;
    }

    return 0;
}
```

In this implementation:

- The `encode` function concatenates the lengths of the strings with a "#" separator followed by the actual string.
- The `decode` function iterates through the encoded string, extracts the length of each string, and then extracts the substring accordingly.

This solution should pass the LeetCode tests for the problem "Encode and Decode Strings".

### 1. Algorithms & Data Structures (C++): Leetcode: Find Median From Data Stream

To solve the "Find Median from Data Stream" problem on LeetCode, you can use a combination of two heaps: a max-heap and a min-heap. This approach allows you to maintain the median in the data stream efficiently.

Here's how you can implement it in C++:

```cpp
#include <queue>
#include <vector>

class MedianFinder {
private:
    std::priority_queue<int> maxHeap; // Max heap for the smaller half of the numbers
    std::priority_queue<int, std::vector<int>, std::greater<int>> minHeap; // Min heap for the larger half of the numbers
    
public:
    /** initialize your data structure here. */
    MedianFinder() {
        
    }
    
    void addNum(int num) {
        if (maxHeap.empty() || num <= maxHeap.top()) {
            maxHeap.push(num);
        } else {
            minHeap.push(num);
        }
        
        // Balance the heaps
        if (maxHeap.size() > minHeap.size() + 1) {
            minHeap.push(maxHeap.top());
            maxHeap.pop();
        } else if (minHeap.size() > maxHeap.size()) {
            maxHeap.push(minHeap.top());
            minHeap.pop();
        }
    }
    
    double findMedian() {
        if (maxHeap.size() == minHeap.size()) {
            return (maxHeap.top() + minHeap.top()) / 2.0;
        } else {
            return maxHeap.top();
        }
    }
};
```

In this implementation:

- We maintain two heaps: a max-heap (`maxHeap`) and a min-heap (`minHeap`).
- We use the max-heap to store the smaller half of the numbers, and the min-heap to store the larger half.
- When adding a number:
  - If the number is less than or equal to the top element of the max-heap, we insert it into the max-heap.
  - Otherwise, we insert it into the min-heap.
  - After inserting, we balance the heaps so that the difference in sizes between the two heaps is at most 1.
- The median can be found as follows:
  - If the sizes of the heaps are equal, the median is the average of the top elements of both heaps.
  - If the sizes are different, the median is the top element of the max-heap.

### 1. Algorithms & Data Structures (C++): Leetcode: Find Minimum in Rotated Sorted Array

To solve the "Find Minimum in Rotated Sorted Array" problem on LeetCode using C++, you can use a binary search approach. Here's a step-by-step guide on how to implement it:

1. **Observation**: The minimum element in the rotated sorted array will always be the element for which the next element is greater than it.

2. **Binary Search Approach**:
   - Initialize two pointers, `left` and `right`, pointing to the start and end of the array respectively.
   - While `left` is less than `right`, do the following:
     - Calculate the middle index as `mid = (left + right) / 2`.
     - Check if the element at the middle index is greater than the element at the end index:
       - If true, then the minimum element lies in the right half, so update `left = mid + 1`.
       - Otherwise, the minimum element lies in the left half or is the middle element itself, so update `right = mid`.
   - Finally, return the element at the `left` index, which would be the minimum element.

Here's the implementation:

```cpp
#include <vector>

int findMin(std::vector<int>& nums) {
    int left = 0;
    int right = nums.size() - 1;

    while (left < right) {
        int mid = left + (right - left) / 2;
        
        // If the middle element is greater than the last element,
        // minimum element lies in the right half.
        if (nums[mid] > nums[right]) {
            left = mid + 1;
        } 
        // Otherwise, minimum element lies in the left half or is the middle element.
        else {
            right = mid;
        }
    }
    
    // Minimum element found at left pointer position.
    return nums[left];
}
```

This code should solve the problem efficiently in O(log n) time complexity, where n is the size of the input array.

### 1. Algorithms & Data Structures (C++): Leetcode: Graph

Sure, let's dive into some algorithms and data structures related to graphs in C++! Graph problems on platforms like LeetCode often involve implementing graph traversal algorithms like Breadth-First Search (BFS) or Depth-First Search (DFS), finding shortest paths, detecting cycles, and more. Here's a basic implementation of a graph using adjacency lists and BFS traversal:

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
    Graph(int v) : V(v), adj(v) {}

    // Function to add an edge to the graph
    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u); // For undirected graph
    }

    // BFS traversal from a given source vertex
    void BFS(int s) {
        vector<bool> visited(V, false);
        queue<int> q;
        
        visited[s] = true;
        q.push(s);

        while (!q.empty()) {
            int u = q.front();
            q.pop();
            cout << u << " ";

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
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 3);

    cout << "BFS traversal starting from vertex 0: ";
    g.BFS(0);

    return 0;
}
```

This code defines a `Graph` class with an adjacency list representation. It has functions to add edges and perform a BFS traversal from a given source vertex. You can customize it further for different graph problems on LeetCode by adding additional functionality like DFS, shortest path algorithms (Dijkstra's or Bellman-Ford), cycle detection (DFS-based or using disjoint sets), etc.

Feel free to ask if you have any questions or if you want to explore more graph algorithms or LeetCode problems!

### 1. Algorithms & Data Structures (C++): Leetcode: Graph Valid Tree

To determine if a given undirected graph is a valid tree, you need to check two conditions:

1. The graph must be fully connected. This means that every node must be reachable from any other node.
2. The graph must not contain any cycles.

Here's an outline of an algorithm to solve this problem using depth-first search (DFS):

1. Create an adjacency list to represent the graph.
2. Initialize a boolean array to keep track of visited nodes.
3. Perform a DFS traversal from any arbitrary node in the graph, marking visited nodes.
4. During the DFS traversal, if you encounter a node that is already visited, there's a cycle in the graph, so return false.
5. After DFS traversal, check if all nodes are visited. If not, the graph is not fully connected, so return false.
6. If both conditions are satisfied, return true.

Here's a C++ implementation of the algorithm:

```cpp
#include <vector>
#include <unordered_set>

using namespace std;

class Solution {
public:
    bool validTree(int n, vector<vector<int>>& edges) {
        // Create adjacency list
        vector

<vector<int>> adjList(n);
        for (const auto& edge : edges) {
            adjList[edge[0]].push_back(edge[1]);
            adjList[edge[1]].push_back(edge[0]);
        }
        
        // Initialize visited array
        vector<bool> visited(n, false);
        
        // Perform DFS traversal
        if (!dfs(adjList, visited, 0, -1)) // Start DFS from node 0
            return false;
        
        // Check if all nodes are visited
        for (bool v : visited) {
            if (!v)
                return false;
        }
        
        return true;
    }
    
private:
    bool dfs(vector<vector<int>>& adjList, vector<bool>& visited, int node, int parent) {
        // Mark current node as visited
        visited[node] = true;
        
        // Visit neighbors
        for (int neighbor : adjList[node]) {
            if (!visited[neighbor]) {
                if (!dfs(adjList, visited, neighbor, node)) // Recursive DFS
                    return false;
            } else if (neighbor != parent) {
                // If the neighbor is already visited and it's not the parent, then it's a cycle
                return false;
            }
        }
        
        return true;
    }
};
```

This algorithm has a time complexity of O(V + E), where V is the number of vertices and E is the number of edges in the graph.

### 1. Algorithms & Data Structures (C++): Leetcode: Group Anagrams

To solve the "Group Anagrams" problem on LeetCode using C++, you can use a hashmap to group anagrams together. Here's a step-by-step explanation of the approach:

1. Iterate through each string in the input vector.
2. For each string, sort its characters to create a canonical representation of the string.
3. Use this canonical representation as a key in a hashmap.
4. Group all strings with the same canonical representation (anagrams) together under this key.
5. After iterating through all strings, traverse the hashmap and collect the grouped anagrams into a result vector.

Here's a C++ implementation of this approach:

```cpp
#include <vector>
#include <string>
#include <unordered_map>
#include <algorithm>

using namespace std;

vector<vector<string>> groupAnagrams(vector<string>& strs) {
    unordered_map<string, vector<string>> anagramGroups;
    
    for (const string& str : strs) {
        string sortedStr = str; // Copy the string to sort it
        sort(sortedStr.begin(), sortedStr.end()); // Sort the characters
        
        // Use the sorted string as key in the hashmap
        anagramGroups[sortedStr].push_back(str);
    }
    
    vector<vector<string>> result;
    for (auto& pair : anagramGroups) {
        result.push_back(pair.second); // Collect all anagrams
    }
    
    return result;
}

// Example usage
int main() {
    vector<string> input = {"eat", "tea", "tan", "ate", "nat", "bat"};
    vector<vector<string>> groupedAnagrams = groupAnagrams(input);
    
    // Output the grouped anagrams
    for (const auto& group : groupedAnagrams) {
        for (const string& str : group) {
            cout << str << " ";
        }
        cout << endl;
    }
    
    return 0;
}
```

This implementation has a time complexity of O(n * m * log m), where n is the number of strings and m is the maximum length of a string. This is because sorting each string takes O(m * log m) time, and we do this for each of the n strings. The space complexity is O(n * m), considering the space used by the hashmap to store the groups.

### 1. Algorithms & Data Structures (C++): Leetcode: House Robber

The "House Robber" problem on LeetCode is a classic dynamic programming problem. The problem statement is as follows:

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. The only constraint stopping you from robbing each of them is that adjacent houses have security systems connected, and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given an integer array `nums` representing the amount of money of each house, return the maximum amount of money you can rob tonight without alerting the police.

Here's a simple approach to solve this problem using dynamic programming:

```cpp
#include <vector>
#include <algorithm>

int rob(std::vector<int>& nums) {
    int n = nums.size();
    if (n == 0) return 0;
    if (n == 1) return nums[0];
    
    std::vector<int> dp(n, 0);
    dp[0] = nums[0];
    dp[1] = std::max(nums[0], nums[1]);
    
    for (int i = 2; i < n; ++i) {
        dp[i] = std::max(dp[i - 1], dp[i - 2] + nums[i]);
    }
    
    return dp[n - 1];
}
```

This code defines a function `rob` that takes a vector of integers representing the money in each house and returns the maximum amount that can be robbed. It uses dynamic programming to solve the problem in linear time complexity.

### 1. Algorithms & Data Structures (C++): Leetcode: Implement Trie (Prefix Tree)

Sure, implementing a Trie, also known as a Prefix Tree, is a classic problem in data structures and algorithms. Here's a basic implementation of a Trie in C++:

```cpp
#include <iostream>
#include <unordered_map>

using namespace std;

// TrieNode represents each node in the Trie
class TrieNode {
public:
    unordered_map<char, TrieNode*> children;
    bool isEnd;

    TrieNode() {
        isEnd = false;
    }
};

class Trie {
private:
    TrieNode* root;

public:
    Trie() {
        root = new TrieNode();
    }

    // Insert a word into the Trie
    void insert(string word) {
        TrieNode* node = root;
        for (char ch : word) {
            if (node->children.find(ch) == node->children.end()) {
                node->children[ch] = new TrieNode();
            }
            node = node->children[ch];
        }
        node->isEnd = true;
    }

    // Search if a word exists in the Trie
    bool search(string word) {
        TrieNode* node = root;
        for (char ch : word) {
            if (node->children.find(ch) == node->children.end()) {
                return false;
            }
            node = node->children[ch];
        }
        return node->isEnd;
    }

    // Check if there is any word in the Trie that starts with the given prefix
    bool startsWith(string prefix) {
        TrieNode* node = root;
        for (char ch : prefix) {
            if (node->children.find(ch) == node->children.end()) {
                return false;
            }
            node = node->children[ch];
        }
        return true;
    }
};

int main() {
    Trie trie;

    // Insert some words into the Trie
    trie.insert("apple");
    trie.insert("app");
    trie.insert("banana");
    trie.insert("bat");
    
    // Search for words
    cout << trie.search("apple") << endl;    // Output: 1 (true)
    cout << trie.search("app") << endl;      // Output: 1 (true)
    cout << trie.search("banana") << endl;   // Output: 1 (true)
    cout << trie.search("bat") << endl;      // Output: 1 (true)
    cout << trie.search("orange") << endl;   // Output: 0 (false)

    // Check if there are words starting with the given prefixes
    cout << trie.startsWith("app") << endl;  // Output: 1 (true)
    cout << trie.startsWith("ban") << endl;  // Output: 1 (true)
    cout << trie.startsWith("cat") << endl;  // Output: 0 (false)

    return 0;
}
```

In this implementation:

- `TrieNode` represents each node in the Trie. It contains a map of child nodes and a boolean flag to indicate whether the current node represents the end of a word.
- `Trie` is the Trie data structure itself. It has methods for insertion, searching for a word, and checking if there are words starting with a given prefix.
- The `insert` method inserts a word into the Trie, creating new nodes as needed.
- The `search` method checks if a given word exists in the Trie.
- The `startsWith` method checks if there are any words in the Trie that start with a given prefix.

You can test this implementation with different words and prefixes to see how it behaves.

### 1. Algorithms & Data Structures (C++): Leetcode: Insert Interval

Sure! Here's a C++ solution for the "Insert Interval" problem on LeetCode:

```cpp
#include <vector>

using namespace std;

vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
    vector<vector<int>> result;
    int i = 0;
    int n = intervals.size();

    // Add all intervals that come before newInterval
    while (i < n && intervals[i][1] < newInterval[0]) {
        result.push_back(intervals[i]);
        i++;
    }

    // Merge overlapping intervals
    while (i < n && intervals[i][0] <= newInterval[1]) {
        newInterval[0] = min(newInterval[0], intervals[i][0]);
        newInterval[1] = max(newInterval[1], intervals[i][1]);
        i++;
    }

    // Add the merged interval
    result.push_back(newInterval);

    // Add all intervals that come after newInterval
    while (i < n) {
        result.push_back(intervals[i]);
        i++;
    }

    return result;
}

// Example usage
int main() {
    vector<vector<int>> intervals = {{1,3},{6,9}};
    vector<int> newInterval = {2,5};
    vector<vector<int>> result = insert(intervals, newInterval);
    // Output the result
    for (const auto& interval : result) {
        cout << "[" << interval[0] << "," << interval[1] << "] ";
    }
    cout << endl;
    return 0;
}
```

This solution works by iterating through the given intervals and performing three main steps:

1. Add all intervals that come before the new interval.
2. Merge overlapping intervals with the new interval.
3. Add all intervals that come after the new interval.

Finally, it returns the resulting intervals after insertion.

### 1. Algorithms & Data Structures (C++): Leetcode: Interval

To solve interval-related problems on LeetCode using C++, you typically deal with structures representing intervals and then implement algorithms to manipulate or process them. Here's a brief overview of how you might approach interval problems:

#### Interval Representation

You can represent an interval using a simple struct in C++:

```cpp
struct Interval {
    int start;
    int end;
    Interval() : start(0), end(0) {}
    Interval(int s, int e) : start(s), end(e) {}
};
```

#### Sorting Intervals

Many interval problems require sorting intervals based on their start or end points. You can use custom comparators with `std::sort` for this:

```cpp
bool compareStart(const Interval &a, const Interval &b) {
    return a.start < b.start;
}

bool compareEnd(const Interval &a, const Interval &b) {
    return a.end < b.end;
}

// Usage:
// std::sort(intervals.begin(), intervals.end(), compareStart);
// std::sort(intervals.begin(), intervals.end(), compareEnd);
```

#### Interval Merge

One common problem is merging overlapping intervals. You can achieve this by iterating through the intervals and merging overlapping ones:

```cpp
vector



```cpp
Interval> mergeIntervals(vector

```cpp


```cpp
Interval> mergeIntervals(vector<interval>& intervals) {
    if (intervals.empty()) return {};
    
    sort(intervals.begin(), intervals.end(), [](const Interval& a, const Interval& b) {
        return a.start < b.start;
    });
    
    vector

```cpp
Interval> merged;
    merged.push_back(intervals[0]);

    for (int i = 1; i < intervals.size(); ++i) {
        if (intervals[i].start <= merged.back().end) {
            merged.back().end = max(merged.back().end, intervals[i].end);
        } else {
            merged.push_back(intervals[i]);
        }
    }

    return merged;
}
```

This function `mergeIntervals` takes a vector of intervals, sorts them based on their start points, and then iterates through them to merge overlapping intervals.

You can further utilize this function or similar approaches to solve various interval-related problems on LeetCode.

### 1. Algorithms & Data Structures (C++): Leetcode: Invert/Flip Binary Tree

Sure, here's a C++ implementation to invert or flip a binary tree:

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

        // Swap left and right subtrees
        TreeNode* temp = root->left;
        root->left = invertTree(root->right);
        root->right = invertTree(temp);

        return root;
    }
};

// Helper function to print the tree in order
void printTree(TreeNode* root) {
    if (root == nullptr) return;
    printTree(root->left);
    std::cout << root->val << " ";
    printTree(root->right);
}

int main() {
    // Create a sample binary tree
    TreeNode* root = new TreeNode(4);
    root->left = new TreeNode(2);
    root->right = new TreeNode(7);
    root->left->left = new TreeNode(1);
    root->left->right = new TreeNode(3);
    root->right->left = new TreeNode(6);
    root->right->right = new TreeNode(9);

    // Print the original tree
    std::cout << "Original tree: ";
    printTree(root);
    std::cout << std::endl;

    // Invert the tree
    Solution sol;
    TreeNode* invertedRoot = sol.invertTree(root);

    // Print the inverted tree
    std::cout << "Inverted tree: ";
    printTree(invertedRoot);
    std::cout << std::endl;

    return 0;
}
```

This code defines a binary tree node structure (`TreeNode`) and a class (`Solution`) with a method `invertTree()` that takes the root of a binary tree and returns its inverted form. The `invertTree()` function recursively traverses the tree and swaps the left and right children of each node.

The `main()` function creates a sample binary tree, prints its original form, inverts it using the `invertTree()` method, and then prints the inverted form.

### 1. Algorithms & Data Structures (C++): Leetcode: Jump Game

Sure, here's a C++ solution for the "Jump Game" problem on LeetCode:

```cpp
#include <iostream>
#include <vector>

using namespace std;

bool canJump(vector<int>& nums) {
    int n = nums.size();
    int maxReach = 0;

    for (int i = 0; i < n; ++i) {
        if (i > maxReach) {
            return false;
        }
        maxReach = max(maxReach, i + nums[i]);
        if (maxReach >= n - 1) {
            return true;
        }
    }

    return false;
}

int main() {
    // Example usage:
    vector<int> nums = {2, 3, 1, 1, 4};
    cout << (canJump(nums) ? "true" : "false") << endl;

    return 0;
}
```

Explanation:

- The idea is to iterate through the array and keep track of the furthest index we can reach from the current position (`maxReach`).
- If at any point, the current index is beyond `maxReach`, it means we cannot proceed further and return `false`.
- If `maxReach` reaches or exceeds the last index, it means we can reach the end of the array and return `true`.
- Otherwise, return `false` at the end of the loop if the end of the array cannot be reached.

This solution has a time complexity of O(n), where n is the size of the input array.

### 1. Algorithms & Data Structures (C++): Leetcode: Kth Smallest Element in a Binary Search Trees

To find the Kth smallest element in a Binary Search Tree (BST), you can perform an in-order traversal of the tree, which will visit nodes in sorted order. While doing the traversal, keep track of the number of nodes visited. When the count reaches K, return the value of the current node.

Here's the C++ code to implement this:

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

int kthSmallest(TreeNode* root, int k) {
    stack<TreeNode*> st;
    TreeNode* curr = root;
    int count = 0;
    
    while (curr != nullptr || !st.empty()) {
        while (curr != nullptr) {
            st.push(curr);
            curr = curr->left;
        }
        curr = st.top();
        st.pop();
        count++;
        if (count == k) return curr->val;
        curr = curr->right;
    }
    return -1; // Kth smallest not found, assuming -1 as invalid input
}

// Example usage
int main() {
    TreeNode* root = new TreeNode(3);
    root->left = new TreeNode(1);
    root->right = new TreeNode(4);
    root->left->right = new TreeNode(2);

    int k = 3;
    cout << "The " << k << "th smallest element is: " << kthSmallest(root, k) << endl;

    return 0;
}
```

In this code:

- We use a stack to perform iterative in-order traversal of the BST.
- We keep track of the count of nodes visited.
- When the count reaches K, we return the value of the current node.
- We return -1 if the Kth smallest element is not found, assuming -1 as an invalid input.

You can customize the `main` function to test the code with different trees and values of K.

### 1. Algorithms & Data Structures (C++): Leetcode: Longest Common Subsequence

Sure! The Longest Common Subsequence (LCS) problem is a classic dynamic programming problem, often used to compare two strings and find the longest sequence of characters that are common to both strings. Here's how you can solve it using dynamic programming in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int longestCommonSubsequence(string text1, string text2) {
    int m = text1.size();
    int n = text2.size();
    
    // Create a 2D vector to store the lengths of LCS
    vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));
    
    // Fill the dp table
    for (int i = 1; i <= m; ++i) {
        for (int j = 1; j <= n; ++j) {
            if (text1[i - 1] == text2[j - 1]) {
                dp[i][j] = dp[i - 1][j - 1] + 1;
            } else {
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
            }
        }
    }
    
    // The length of LCS will be at the bottom-right corner of dp table
    return dp[m][n];
}

int main() {
    string text1 = "abcde";
    string text2 = "ace";
    cout << "Length of longest common subsequence: " << longestCommonSubsequence(text1, text2) << endl;
    return 0;
}
```

This code defines a function `longestCommonSubsequence` that takes two strings `text1` and `text2` as input and returns the length of the longest common subsequence. It uses a dynamic programming approach to fill a 2D vector `dp` where `dp[i][j]` represents the length of LCS of `text1[0...i-1]` and `text2[0...j-1]`. Finally, it returns `dp[m][n]`, where `m` and `n` are the lengths of the input strings `text1` and `text2` respectively.

You can modify the `main` function to test the function with different inputs.

### 1. Algorithms & Data Structures (C++): Leetcode: Longest Consecutive Sequence

The Longest Consecutive Sequence problem on LeetCode asks you to find the length of the longest consecutive elements sequence in an unsorted array of integers. Here's a C++ solution for it:

```cpp
#include <vector>
#include <unordered_set>

using namespace std;

int longestConsecutive(vector<int>& nums) {
    unordered_set<int> num_set;
    for (int num : nums) {
        num_set.insert(num);
    }

    int longest_streak = 0;

    for (int num : num_set) {
        // If the current number is the start of a sequence (i.e., no num-1 in the set),
        // then check how long the consecutive sequence is.
        if (num_set.find(num - 1) == num_set.end()) {
            int current_num = num;
            int current_streak = 1;

            // Check consecutive numbers after the current number.
            while (num_set.find(current_num + 1) != num_set.end()) {
                current_num++;
                current_streak++;
            }

            longest_streak = max(longest_streak, current_streak);
        }
    }

    return longest_streak;
}
```

This solution works as follows:

1. We first add all the numbers from the array into an unordered set for constant time lookup.
2. Then, we iterate through the set. For each number, if it is the start of a consecutive sequence (i.e., there's no `num-1` in the set), we calculate the length of the consecutive sequence.
3. We keep track of the longest consecutive sequence encountered.

The time complexity of this solution is O(n), where n is the number of elements in the input array, as each number is processed only once.

### 1. Algorithms & Data Structures (C++): Leetcode: Longest Increasing Subsequence

To solve the Longest Increasing Subsequence problem on LeetCode using C++, you can implement a dynamic programming approach. Here's a brief explanation of the algorithm:

1. Initialize an array `dp` of the same size as the input array, where `dp[i]` represents the length of the longest increasing subsequence ending at index `i`.
2. Initialize each element of `dp` to 1, as the minimum length of a subsequence is always 1.
3. Iterate over each element in the input array. For each element, iterate over all elements before it to find the longest increasing subsequence that ends at that element.
4. Update `dp[i]` to be the maximum of `dp[j] + 1` for all `j` less than `i`, where `nums[j] < nums[i]`.
5. After the iterations, find the maximum value in the `dp` array, which represents the length of the longest increasing subsequence.

Here's the C++ code implementing the above algorithm:

```cpp
#include <vector>
#include <algorithm>

using namespace std;

int lengthOfLIS(vector<int>& nums) {
    int n = nums.size();
    if (n == 0) return 0;
    
    vector<int> dp(n, 1); // Initialize dp array
    
    // Iterate over each element in nums
    for (int i = 1; i < n; ++i) {
        // Iterate over elements before i
        for (int j = 0; j < i; ++j) {
            if (nums[j] < nums[i]) {
                dp[i] = max(dp[i], dp[j] + 1); // Update dp[i]
            }
        }
    }
    
    // Find the maximum value in dp array
    int maxLen = *max_element(dp.begin(), dp.end());
    
    return maxLen;
}

// Example usage
int main() {
    vector<int> nums = {10, 9, 2, 5, 3, 7, 101, 18};
    int result = lengthOfLIS(nums);
    return 0;
}
```

This code snippet implements the dynamic programming solution for the Longest Increasing Subsequence problem in C++.

### 1. Algorithms & Data Structures (C++): Leetcode: Longest Palindromic Substring

To solve the Longest Palindromic Substring problem on LeetCode using C++, you can use either a dynamic programming approach or an expand around center approach. Here's a C++ implementation using the dynamic programming approach:

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

string longestPalindrome(string s) {
    int n = s.size();
    if (n <= 1)
        return s;

    vector<vector<bool>> dp(n, vector<bool>(n, false));
    int start = 0, maxLen = 1;

    // All substrings of length 1 are palindromes
    for (int i = 0; i < n; ++i)
        dp[i][i] = true;

    // Check for substrings of length 2
    for (int i = 0; i < n - 1; ++i) {
        if (s[i] == s[i + 1]) {
            dp[i][i + 1] = true;
            start = i;
            maxLen = 2;
        }
    }

    // Check for substrings of length > 2
    for (int len = 3; len <= n; ++len) {
        for (int i = 0; i <= n - len; ++i) {
            int j = i + len - 1;
            if (s[i] == s[j] && dp[i + 1][j - 1]) {
                dp[i][j] = true;
                start = i;
                maxLen = len;
            }
        }
    }

    return s.substr(start, maxLen);
}

int main() {
    string s = "babad";
    cout << "Longest Palindromic Substring: " << longestPalindrome(s) << endl;
    return 0;
}
```

This code implements a dynamic programming approach where `dp[i][j]` is true if the substring `s[i...j]` is a palindrome. It starts by checking all substrings of length 1 and 2 as potential palindromes and then extends this to longer substrings, updating `start` and `maxLen` accordingly. Finally, it returns the longest palindromic substring found.

You can replace the string `s` with any other string you want to test the function with.

### 1. Algorithms & Data Structures (C++): Leetcode: Longest Repeating Character Replacement

To solve the "Longest Repeating Character Replacement" problem on LeetCode, you can use a sliding window approach. Here's a high-level explanation of the algorithm in C++:

```cpp
#include <string>
#include <algorithm>

using namespace std;

int characterReplacement(string s, int k) {
    int n = s.size();
    int maxCount = 0; // Maximum count of repeating characters in the current window
    int maxLength = 0; // Maximum length of substring with repeating characters

    vector<int> count(26, 0); // Count of characters in the current window

    int start = 0; // Start of the current window

    // Iterate through the string
    for (int end = 0; end < n; end++) {
        maxCount = max(maxCount, ++count[s[end] - 'A']); // Update the count of the current character

        // If the length of the window minus the maximum count of repeating characters is greater than k,
        // we need to shrink the window
        if (end - start + 1 - maxCount > k) {
            count[s[start] - 'A']--; // Remove the character at the start of the window
            start++; // Shrink the window
        }

        // Update the maximum length of the substring
        maxLength = max(maxLength, end - start + 1);
    }

    return maxLength;
}

int main() {
    string s = "ABAB";
    int k = 2;
    cout << characterReplacement(s, k); // Output: 4
    return 0;
}
```

Explanation:

- We use a sliding window approach where we keep track of the count of each character in the current window.
- We maintain a variable `maxCount` to keep track of the maximum count of repeating characters in the current window.
- If the length of the window minus `maxCount` exceeds `k`, it means we need to shrink the window to maintain the condition that we can replace at most `k` characters.
- As we slide the window to the right, we update `maxCount` and `maxLength`.
- Finally, `maxLength` will hold the length of the longest substring with repeating characters after we have traversed the entire string.

### 1. Algorithms & Data Structures (C++): Leetcode: Longest Substring Without Repeating Characters

To solve the "Longest Substring Without Repeating Characters" problem on LeetCode using C++, you can use a sliding window approach. Here's a C++ implementation:

```cpp
#include <iostream>
#include <unordered_map>
#include <algorithm>

using namespace std;

int lengthOfLongestSubstring(string s) {
    unordered_map<char, int> charIndexMap;
    int maxLength = 0, startIndex = 0;

    for (int i = 0; i < s.size(); ++i) {
        if (charIndexMap.find(s[i]) != charIndexMap.end() && charIndexMap[s[i]] >= startIndex) {
            startIndex = charIndexMap[s[i]] + 1;
        }
        charIndexMap[s[i]] = i;
        maxLength = max(maxLength, i - startIndex + 1);
    }

    return maxLength;
}

int main() {
    string str = "abcabcbb";
    cout << "Length of the longest substring without repeating characters: " << lengthOfLongestSubstring(str) << endl;
    return 0;
}
```

In this solution:

- We use a hash map `charIndexMap` to store the index of the characters we have encountered.
- We maintain a `startIndex` to mark the starting index of the current substring without repeating characters.
- We iterate through the string, updating the `startIndex` when we encounter a repeating character.
- We update `maxLength` with the length of the current substring whenever we encounter a new character.
- Finally, we return the `maxLength`.

This solution has a time complexity of O(n), where n is the length of the input string, as we only iterate through the string once. The space complexity is O(min(m, n)), where m is the size of the character set (in this case, the ASCII character set) and n is the length of the string.

### 1. Algorithms & Data Structures (C++): Leetcode: Lowest Common Ancestor of a Binary Search Trees

To solve the Lowest Common Ancestor (LCA) problem in a Binary Search Tree (BST), you can follow these steps:

1. Start from the root node.
2. Compare the values of the current node with the values of the two nodes.
3. If the current node's value is greater than both nodes' values, move to the left subtree.
4. If the current node's value is smaller than both nodes' values, move to the right subtree.
5. If the current node's value lies between the two nodes' values, or one of the nodes' values is equal to the current node's value, then the current node is the LCA.
6. Repeat steps 3 to 5 until finding the LCA.

Here's a C++ implementation of the algorithm:

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

class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (!root) return nullptr;
        
        // If both nodes are smaller than the current node, go left
        if (p->val < root->val && q->val < root->val)
            return lowestCommonAncestor(root->left, p, q);
        
        // If both nodes are greater than the current node, go right
        if (p->val > root->val && q->val > root->val)
            return lowestCommonAncestor(root->right, p, q);
        
        // If the current node is between the two nodes or one of them is equal to the current node, return the current node
        return root;
    }
};

int main() {
    // Example usage
    TreeNode* root = new TreeNode(6);
    root->left = new TreeNode(2);
    root->right = new TreeNode(8);
    root->left->left = new TreeNode(0);
    root->left->right = new TreeNode(4);
    root->right->left = new TreeNode(7);
    root->right->right = new TreeNode(9);
    root->left->right->left = new TreeNode(3);
    root->left->right->right = new TreeNode(5);

    Solution sol;
    TreeNode* lca = sol.lowestCommonAncestor(root, root->left, root->right);
    cout << "LCA: " << lca->val << endl; // Output should be 6

    return 0;
}
```

This implementation runs in O(h) time complexity, where h is the height of the BST.

### 1. Algorithms & Data Structures (C++): Leetcode: Matrix

Sure, matrix-related problems on platforms like LeetCode often involve various algorithmic techniques and data structures. Here's an overview of some common matrix-related problems and the techniques used to solve them in C++:

1. **Matrix Traversal**:
   - **Problem**: Traverse the matrix in a specific order (e.g., spiral order, diagonal order).
   - **Approach**: Use nested loops to traverse the matrix while maintaining directions and boundaries.

2. **Matrix Manipulation**:
   - **Problem**: Perform operations like rotation, flipping, or transposition on the matrix.
   - **Approach**: Implement the required operations using nested loops or STL algorithms like `reverse()` or `rotate()`.

3. **Matrix Search**:
   - **Problem**: Search for an element in a sorted/rotated matrix.
   - **Approach**: Apply binary search or divide-and-conquer techniques after converting the matrix into a linear structure.

4. **Matrix Path Finding**:
   - **Problem**: Find a path from one point to another in the matrix (e.g., shortest path, unique paths).
   - **Approach**: Use techniques like Breadth-First Search (BFS) or Depth-First Search (DFS) to explore possible paths in the matrix.

5. **Matrix DP (Dynamic Programming)**:
   - **Problem**: Solve optimization problems using dynamic programming techniques on matrices (e.g., maximum sum submatrix, longest increasing path).
   - **Approach**: Define the DP state and transition rules based on the problem constraints, and then implement the DP algorithm using nested loops.

6. **Matrix Operations**:
   - **Problem**: Perform mathematical operations like multiplication or exponentiation on matrices.
   - **Approach**: Implement the operations efficiently using standard algorithms like Strassen's algorithm for matrix multiplication or exponentiation by squaring.

7. **Sparse Matrix Representation**:
   - **Problem**: Optimize the storage and operations for sparse matrices with a majority of zero elements.
   - **Approach**: Use specialized data structures like Coordinate List (COO), Compressed Sparse Row (CSR), or Compressed Sparse Column (CSC) formats for efficient representation and operations.

When tackling matrix problems on LeetCode or similar platforms, it's essential to understand the problem constraints and choose the appropriate algorithmic techniques and data structures accordingly. Additionally, testing your solutions with various test cases and considering edge cases can help ensure correctness and efficiency.

### 1. Algorithms & Data Structures (C++): Leetcode: Maximum Depth of Binary Tree

To solve the "Maximum Depth of Binary Tree" problem on LeetCode, you can use either Depth-First Search (DFS) or Breadth-First Search (BFS) algorithms. Here's a simple approach using DFS in C++:

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
    int maxDepth(TreeNode* root) {
        if (root == NULL) return 0;
        return 1 + max(maxDepth(root->left), maxDepth(root->right));
    }
};

int main() {
    // Example usage:
    // Create a binary tree
    TreeNode* root = new TreeNode(3);
    root->left = new TreeNode(9);
    root->right = new TreeNode(20);
    root->right->left = new TreeNode(15);
    root->right->right = new TreeNode(7);

    // Create a solution object
    Solution sol;

    // Get the maximum depth of the binary tree
    int depth = sol.maxDepth(root);
    cout << "Maximum Depth of Binary Tree: " << depth << endl;

    return 0;
}
```

This solution uses recursive DFS to traverse the tree and calculate the maximum depth. The `maxDepth` function returns 0 if the current node is NULL (i.e., the leaf node), and otherwise recursively calculates the maximum depth of its left and right subtrees, returning the maximum of the two plus 1.

Remember to test the code with various test cases including edge cases to ensure its correctness.

### 1. Algorithms & Data Structures (C++): Leetcode: Maximum Product Subarray

To solve the "Maximum Product Subarray" problem on LeetCode using C++, you can apply the concept of dynamic programming. Here's a step-by-step approach to solve it:

1. **Initialize Variables**:
   - Initialize `max_prod`, `min_prod`, and `result` variables to store the maximum product, minimum product, and final result respectively.
   - Initialize `n` to the size of the input array `nums`.

2. **Base Case Initialization**:
   - Set `max_prod` and `min_prod` to the first element of the array, `nums[0]`.
   - Set `result` to `max_prod`.

3. **Iterate Through Array**:
   - Iterate through the array starting from index 1.
   - At each step, update `max_prod` and `min_prod` based on the current element and the products calculated so far.

4. **Update Result**:
   - Update `result` to store the maximum of `result` and `max_prod`.

5. **Return Result**.

Here's the C++ code implementing the above steps:

```cpp
#include <vector>
#include <algorithm>

using namespace std;

class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int n = nums.size();
        if (n == 0) return 0;
        
        int max_prod = nums[0];
        int min_prod = nums[0];
        int result = nums[0];
        
        for (int i = 1; i < n; ++i) {
            if (nums[i] < 0)
                swap(max_prod, min_prod);
            
            max_prod = max(nums[i], max_prod * nums[i]);
            min_prod = min(nums[i], min_prod * nums[i]);
            
            result = max(result, max_prod);
        }
        
        return result;
    }
};
```

This code efficiently solves the problem in linear time complexity O(n), where n is the size of the input array `nums`.

### 1. Algorithms & Data Structures (C++): Leetcode: Maximum Subarray

To solve the "Maximum Subarray" problem on LeetCode, you can use Kadane's algorithm, which is an efficient algorithm for finding the maximum sum subarray within a given one-dimensional array of numbers. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int maxSubArray(vector<int>& nums) {
    int maxSum = nums[0]; // Initialize maxSum to the first element
    int currentSum = nums[0]; // Initialize currentSum to the first element
    
    // Iterate through the array starting from the second element
    for (int i = 1; i < nums.size(); ++i) {
        // Calculate the current sum by adding the current element to the current sum or starting a new subarray
        currentSum = max(nums[i], currentSum + nums[i]);
        
        // Update maxSum if the current sum is greater
        maxSum = max(maxSum, currentSum);
    }
    
    return maxSum;
}

int main() {
    // Example usage
    vector<int> nums = {-2, 1, -3, 4, -1, 2, 1, -5, 4};
    cout << "Maximum sum of subarray: " << maxSubArray(nums) << endl;
    return 0;
}
```

This code will output the maximum sum of a subarray, which in the example given would be 6 (from the subarray [4, -1, 2, 1]).

### 1. Algorithms & Data Structures (C++): Leetcode: Meeting Rooms

The "Meeting Rooms" problem on LeetCode is a classic algorithmic problem. Here's the problem statement:

**Problem Statement:**
Given an array of meeting time intervals where intervals[i] = [start_i, end_i], determine if a person could attend all meetings.

**Example:**

```bash
Input: [[0,30],[5,10],[15,20]]
Output: false
```

Explanation: The first meeting is between 0 and 30 minutes, the second is between 5 and 10 minutes, and the third is between 15 and 20 minutes. Since the second and third meetings overlap, the person cannot attend all meetings.

**Approach:**
One simple approach to solve this problem is to sort the meetings based on their start times. Then, iterate through the sorted array, and for each meeting, check if its start time is earlier than the end time of the previous meeting. If it is, then there is a conflict, and the person cannot attend all meetings.

**C++ Code:**

```cpp
#include <vector>
#include <algorithm>

bool canAttendMeetings(vector<vector<int>>& intervals) {
    // Sort meetings based on start time
    sort(intervals.begin(), intervals.end(), [](const vector<int>& a, const vector<int>& b) {
        return a[0] < b[0];
    });
    
    // Check for overlapping meetings
    for (int i = 1; i < intervals.size(); ++i) {
        if (intervals[i][0] < intervals[i-1][1]) // If the start time of the current meeting is earlier than the end time of the previous meeting
            return false; // There's a conflict
    }
    
    return true; // No conflicts found
}
```

This code sorts the intervals based on their start times in ascending order using the `sort()` function with a custom comparator. Then, it iterates through the sorted array and checks for any overlapping meetings. If it finds any overlap, it returns `false`, indicating that the person cannot attend all meetings. Otherwise, it returns `true`, indicating that all meetings can be attended without any conflicts.

### 1. Algorithms & Data Structures (C++): Leetcode: Merge Interval

To solve the "Merge Intervals" problem on LeetCode, you can follow these steps:

1. **Sort Intervals**: Start by sorting the intervals based on their start times. This is crucial for efficient merging.
2. **Merge Intervals**: Iterate through the sorted intervals. For each interval:
   - If it overlaps with the previous interval (i.e., the end time of the previous interval is greater than or equal to the start time of the current interval), merge them by updating the end time of the previous interval to the maximum of the two end times.
   - If it does not overlap, add the current interval to the merged intervals.
3. **Return Merged Intervals**: After iterating through all intervals, the merged intervals contain the final result.

Here's the C++ implementation:

```cpp
#include <vector>
#include <algorithm>

using namespace std;

vector<vector<int>> merge(vector<vector<int>>& intervals) {
    if (intervals.empty())
        return {};

    // Sort intervals based on start time
    sort(intervals.begin(), intervals.end(), [](const vector<int>& a, const vector<int>& b) {
        return a[0] < b[0];
    });

    vector<vector<int>> merged;
    merged.push_back(intervals[0]);

    for (int i = 1; i < intervals.size(); ++i) {
        if (merged.back()[1] >= intervals[i][0]) {
            // Overlapping intervals, update end time
            merged.back()[1] = max(merged.back()[1], intervals[i][1]);
        } else {
            // Non-overlapping intervals, add to merged
            merged.push_back(intervals[i]);
        }
    }

    return merged;
}
```

This code sorts the intervals based on their start times and then merges them efficiently. The time complexity of this solution is O(n log n), where n is the number of intervals, due to the sorting step. The merging step takes linear time, so the overall time complexity is dominated by the sorting.

### 1. Algorithms & Data Structures (C++): Leetcode: Merge K Sorted Lists

To merge k sorted lists in C++, you can use a priority queue (min-heap) to efficiently merge the lists. Here's how you can implement it:

```cpp
#include <queue>
#include <vector>

using namespace std;

struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

struct CompareNodes {
    bool operator()(ListNode* a, ListNode* b) {
        return a->val > b->val;
    }
};

class Solution {
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        // Define a min-heap priority queue
        priority_queue<ListNode*, vector<ListNode*>, CompareNodes> pq;

        // Push the head of each list into the priority queue
        for (auto head : lists) {
            if (head)
                pq.push(head);
        }

        ListNode dummy(0);
        ListNode* tail = &dummy;

        // Continue until all lists have been merged
        while (!pq.empty()) {
            // Get the node with the smallest value
            ListNode* minNode = pq.top();
            pq.pop();

            // Append the smallest node to the result list
            tail->next = minNode;
            tail = tail->next;

            // Move to the next node in the list
            if (minNode->next)
                pq.push(minNode->next);
        }

        return dummy.next;
    }
};
```

In this code:

- We define a `ListNode` struct representing a node in a linked list.
- We define a comparison function `CompareNodes` to compare `ListNode` pointers based on their `val`.
- The `mergeKLists` function takes a vector of pointers to ListNode (representing k sorted lists) as input and returns a pointer to the merged sorted list.
- We use a priority queue (`pq`) to store the heads of the k lists.
- We iterate until the priority queue is empty, each time:
  - Pop the smallest node (`minNode`) from the priority queue.
  - Append `minNode` to the result list.
  - Move to the next node in the list of `minNode` and push it into the priority queue if it exists.

This algorithm has a time complexity of O(n log k), where n is the total number of elements in all lists and k is the number of lists.

### 1. Algorithms & Data Structures (C++): Leetcode: Merge Two Sorted Lists

To merge two sorted lists in C++, you can create a new linked list by iterating through the input lists and comparing their elements. Here's a sample implementation:

```cpp
#include <iostream>

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        // Create a dummy node to simplify the code
        ListNode dummy(0);
        ListNode* tail = &dummy;

        while (l1 != nullptr && l2 != nullptr) {
            if (l1->val <= l2->val) {
                tail->next = l1;
                l1 = l1->next;
            } else {
                tail->next = l2;
                l2 = l2->next;
            }
            tail = tail->next;
        }

        // Append the remaining elements of l1 or l2, if any
        if (l1 != nullptr) {
            tail->next = l1;
        } else {
            tail->next = l2;
        }

        // Return the merged list, skipping the dummy node
        return dummy.next;
    }
};

// Utility function to print the linked list
void printList(ListNode* head) {
    while (head != nullptr) {
        std::cout << head->val << " ";
        head = head->next;
    }
    std::cout << std::endl;
}

int main() {
    // Example usage
    ListNode* l1 = new ListNode(1);
    l1->next = new ListNode(2);
    l1->next->next = new ListNode(4);

    ListNode* l2 = new ListNode(1);
    l2->next = new ListNode(3);
    l2->next->next = new ListNode(4);

    Solution solution;
    ListNode* mergedList = solution.mergeTwoLists(l1, l2);

    std::cout << "Merged List: ";
    printList(mergedList);

    return 0;
}
```

This code defines a `ListNode` struct representing a node in a singly-linked list and a `Solution` class with a method `mergeTwoLists` that merges two sorted lists. The `main` function demonstrates how to use this solution.

### 1. Algorithms & Data Structures (C++): Leetcode: Minimum Window Substring

The Minimum Window Substring problem on LeetCode is a classic algorithmic problem that can be solved using the sliding window technique. Here's the problem statement:

**Problem Statement:**
Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

**Example:**

```
Input: S = "ADOBECODEBANC", T = "ABC"
Output: "BANC"
```

To solve this problem efficiently, you can follow these steps:

1. Create two maps: one to count the characters in the target string `T`, and another to count the characters in the current window of the string `S`.
2. Use two pointers, `left` and `right`, to define the current window. Initially, both pointers point to the beginning of the string `S`.
3. Move the `right` pointer to the right until you find a window that contains all the characters of `T`.
4. Once you have found such a window, move the `left` pointer to the right until you can't shrink the window anymore without excluding characters from `T`.
5. Update the minimum window length and the start index if necessary.
6. Repeat steps 3 to 5 until you reach the end of the string `S`.

Here's a C++ implementation of the algorithm:

```cpp
#include <string>
#include <unordered_map>

using namespace std;

string minWindow(string s, string t) {
    unordered_map<char, int> targetFreq, windowFreq;
    for (char c : t)
        targetFreq[c]++;
    
    int left = 0, right = 0;
    int minLen = INT_MAX;
    int minStart = 0;
    int required = targetFreq.size();
    int formed = 0;
    
    while (right < s.length()) {
        char c = s[right];
        windowFreq[c]++;
        
        if (targetFreq.count(c) && windowFreq[c] == targetFreq[c])
            formed++;
        
        while (left <= right && formed == required) {
            if (right - left + 1 < minLen) {
                minLen = right - left + 1;
                minStart = left;
            }
            
            char leftChar = s[left];
            windowFreq[leftChar]--;
            
            if (targetFreq.count(leftChar) && windowFreq[leftChar] < targetFreq[leftChar])
                formed--;
            
            left++;
        }
        
        right++;
    }
    
    return minLen == INT_MAX ? "" : s.substr(minStart, minLen);
}

int main() {
    string S = "ADOBECODEBANC";
    string T = "ABC";
    string result = minWindow(S, T);
    cout << "Minimum window substring: " << result << endl;
    return 0;
}
```

This implementation has a time complexity of O(n), where n is the length of the string `S`.

### 1. Algorithms & Data Structures (C++): Leetcode: Missing Number

Sure, here's a C++ solution for the "Missing Number" problem on LeetCode:

```cpp
#include <vector>

class Solution {
public:
    int missingNumber(std::vector<int>& nums) {
        int n = nums.size();
        
        // Calculate the expected sum if all numbers from 0 to n were present
        int expectedSum = (n * (n + 1)) / 2;
        
        // Calculate the actual sum of numbers in the array
        int actualSum = 0;
        for (int num : nums) {
            actualSum += num;
        }
        
        // The difference between the expected sum and the actual sum will be the missing number
        return expectedSum - actualSum;
    }
};
```

Explanation:

- We first calculate the expected sum of numbers from 0 to n using the formula `(n * (n + 1)) / 2`, where n is the length of the array.
- We then iterate through the given array and calculate the actual sum of its elements.
- The difference between the expected sum and the actual sum will give us the missing number.

This solution has a time complexity of O(n) and a space complexity of O(1).

### 1. Algorithms & Data Structures (C++): Leetcode: Non-overlapping Intervals

The "Non-overlapping Intervals" problem on LeetCode is a classic interval scheduling problem. The goal is to find the minimum number of intervals that need to be removed to make all intervals non-overlapping. Here's the problem statement with a solution in C++:

**Problem Statement:**

Given a collection of intervals, find the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping.

**Example:**

```
Input: [[1,2],[2,3],[3,4],[1,3]]
Output: 1
Explanation: [1,3] can be removed and the rest of the intervals are non-overlapping.
```

**Solution (C++):**

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int eraseOverlapIntervals(vector<vector<int>>& intervals) {
    if (intervals.empty()) return 0;
    
    // Sort intervals based on their end time
    sort(intervals.begin(), intervals.end(), [](const vector<int>& a, const vector<int>& b) {
        return a[1] < b[1];
    });
    
    int end = intervals[0][1];
    int count = 1; // Count of non-overlapping intervals
    
    // Iterate through intervals, find non-overlapping intervals
    for (int i = 1; i < intervals.size(); ++i) {
        if (intervals[i][0] >= end) { // Non-overlapping
            ++count;
            end = intervals[i][1];
        }
    }
    
    // Total intervals minus non-overlapping intervals gives the minimum to be removed
    return intervals.size() - count;
}

int main() {
    vector<vector<int>> intervals = {{1,2},{2,3},{3,4},{1,3}};
    cout << "Minimum intervals to be removed: " << eraseOverlapIntervals(intervals) << endl;
    return 0;
}
```

This solution works by sorting the intervals based on their end times. Then, it iterates through the sorted intervals and counts the number of non-overlapping intervals. Finally, it returns the difference between the total number of intervals and the count of non-overlapping intervals.

### 1. Algorithms & Data Structures (C++): Leetcode: Number of 1 Bits

The problem "Number of 1 Bits" on LeetCode asks you to write a function that takes an unsigned integer and returns the number of '1' bits it has (also known as the Hamming weight).

Here's a simple C++ solution using bitwise operations:

```cpp
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int count = 0;
        while (n != 0) {
            count += n & 1; // Check if the least significant bit is set
            n >>= 1;        // Right shift to discard the least significant bit
        }
        return count;
    }
};
```

This solution iterates through each bit of the number `n`. In each iteration, it checks if the least significant bit (LSB) is set using the bitwise AND operation (`n & 1`). If it is set, it increments the count. Then, it right shifts `n` by one position (`n >>= 1`) to discard the checked bit. This process continues until `n` becomes zero, which means all bits have been checked.

You can also optimize this solution by using the Brian Kernighan's algorithm, which is a clever trick to count the number of set bits in a number in fewer iterations. Here's how you can implement it:

```cpp
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int count = 0;
        while (n != 0) {
            n &= (n - 1); // Unset the rightmost '1' bit
            count++;
        }
        return count;
    }
};
```

In each iteration, this algorithm unsets the rightmost '1' bit in the number using the expression `n &= (n - 1)`. It then increments the count. This process continues until `n` becomes zero.

### 1. Algorithms & Data Structures (C++): Leetcode: Number of Connected Components in an Undirected Graph

To solve the problem "Number of Connected Components in an Undirected Graph" on LeetCode using C++, you can use Depth First Search (DFS) or Breadth First Search (BFS) algorithms. Here's an example implementation using Depth First Search:

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>

using namespace std;

class Solution {
public:
    int countComponents(int n, vector<vector<int>>& edges) {
        vector

<int>> adjList(n); // Adjacency list representation of the graph
        vector<bool> visited(n, false); // To keep track of visited nodes
        int components = 0; // Count of connected components
        
        // Constructing the adjacency list
        for (const auto& edge : edges) {
            adjList[edge[0]].push_back(edge[1]);
            adjList[edge[1]].push_back(edge[0]);
        }
        
        // Performing Depth First Search
        for (int i = 0; i < n; ++i) {
            if (!visited[i]) {
                dfs(i, adjList, visited);
                components++; // Incrementing the count of connected components
            }
        }
        
        return components;
    }
    
    // Depth First Search function
    void dfs(int node, vector<vector<int>>& adjList, vector<bool>& visited) {
        visited[node] = true;
        
        for (int neighbor : adjList[node]) {
            if (!visited[neighbor]) {
                dfs(neighbor, adjList, visited);
            }
        }
    }
};

int main() {
    Solution sol;
    int n = 5;
    vector<vector<int>> edges = {{0, 1}, {1, 2}, {3, 4}};
    cout << "Number of connected components: " << sol.countComponents(n, edges) << endl;
    return 0;
}
```

This code defines a `Solution` class with a `countComponents` method that takes the number of nodes `n` and a vector of edges `edges`. It constructs an adjacency list representation of the graph and performs Depth First Search to count the number of connected components.

In the `main` function, an example graph is defined with 5 nodes and 3 edges, and the `countComponents` method is called to find the number of connected components in the graph.

### 1. Algorithms & Data Structures (C++): Leetcode: Number of Islands

The "Number of Islands" problem on LeetCode is a classic question that involves graph traversal, typically solved using Depth First Search (DFS) or Breadth First Search (BFS) algorithms. The problem statement goes something like this:

You are given a 2D grid of '1's (land) and '0's (water). An island is formed by connecting adjacent lands horizontally or vertically. You need to find the number of islands in the given grid.

Here's a general approach in C++ using Depth First Search (DFS):

```cpp
#include <vector>

class Solution {
public:
    int numIslands(std::vector<std::vector<char>>& grid) {
        if (grid.empty() || grid[0].empty()) return 0;
        
        int numIslands = 0;
        int rows = grid.size();
        int cols = grid[0].size();
        
        for (int i = 0; i < rows; ++i) {
            for (int j = 0; j < cols; ++j) {
                if (grid[i][j] == '1') {
                    ++numIslands;
                    dfs(grid, i, j);
                }
            }
        }
        
        return numIslands;
    }
    
private:
    void dfs(std::vector<std::vector<char>>& grid, int i, int j) {
        int rows = grid.size();
        int cols = grid[0].size();
        
        if (i < 0 || i >= rows || j < 0 || j >= cols || grid[i][j] != '1') return;
        
        grid[i][j] = '0'; // Marking visited
        
        dfs(grid, i + 1, j); // Explore down
        dfs(grid, i - 1, j); // Explore up
        dfs(grid, i, j + 1); // Explore right
        dfs(grid, i, j - 1); // Explore left
    }
};
```

In this solution, we traverse the grid and whenever we encounter a '1', we increment the island count and perform DFS to mark all connected '1's as visited. This way, we ensure that each island is counted only once.

### 1. Algorithms & Data Structures (C++): Leetcode: Pacific Atlantic Waterflow

"Pacific Atlantic Waterflow" is a classic algorithm problem on LeetCode. The task is to determine which cells in a matrix of heights can flow into both the Pacific and Atlantic oceans. Each cell can flow to its neighboring cells in the four cardinal directions (up, down, left, or right) if the neighboring cell's height is equal to or lower than the current cell's height. Pacific Ocean is represented by the first row and column of the matrix, and the Atlantic Ocean is represented by the last row and column of the matrix.

Here's a basic outline of how you can solve this problem in C++:

```cpp
#include <vector>
#include <queue>

using namespace std;

void dfs(vector<vector<int>>& matrix, int row, int col, vector<vector<bool>>& visited, int prevHeight) {
    int numRows = matrix.size();
    int numCols = matrix[0].size();
    
    if (row < 0 || row >= numRows || col < 0 || col >= numCols || visited[row][col] || matrix[row][col] < prevHeight)
        return;
    
    visited[row][col] = true;
    
    dfs(matrix, row + 1, col, visited, matrix[row][col]);
    dfs(matrix, row - 1, col, visited, matrix[row][col]);
    dfs(matrix, row, col + 1, visited, matrix[row][col]);
    dfs(matrix, row, col - 1, visited, matrix[row][col]);
}

vector<vector<int>> pacificAtlantic(vector<vector<int>>& matrix) {
    if (matrix.empty() || matrix[0].empty())
        return {};
    
    int numRows = matrix.size();
    int numCols = matrix[0].size();
    
    vector<vector<bool>> pacific(numRows, vector<bool>(numCols, false));
    vector<vector<bool>> atlantic(numRows, vector<bool>(numCols, false));
    
    // DFS from the Pacific
    for (int i = 0; i < numRows; ++i)
        dfs(matrix, i, 0, pacific, INT_MIN);
    for (int j = 0; j < numCols; ++j)
        dfs(matrix, 0, j, pacific, INT_MIN);
    
    // DFS from the Atlantic
    for (int i = 0; i < numRows; ++i)
        dfs(matrix, i, numCols - 1, atlantic, INT_MIN);
    for (int j = 0; j < numCols; ++j)
        dfs(matrix, numRows - 1, j, atlantic, INT_MIN);
    
    // Find cells that can flow into both oceans
    vector<vector<int>> result;
    for (int i = 0; i < numRows; ++i) {
        for (int j = 0; j < numCols; ++j) {
            if (pacific[i][j] && atlantic[i][j])
                result.push_back({i, j});
        }
    }
    
    return result;
}

int main() {
    vector<vector<int>> matrix = {
        {1, 2, 2, 3, 5},
        {3, 2, 3, 4, 4},
        {2, 4, 5, 3, 1},
        {6, 7, 1, 4, 5},
        {5, 1, 1, 2, 4}
    };

    vector<vector<int>> result = pacificAtlantic(matrix);
    
    // Output result
    for (const auto& coord : result) {
        cout << "(" << coord[0] << ", " << coord[1] << ") ";
    }
    
    return 0;
}
```

This solution involves Depth First Search (DFS) traversal starting from the borders of the matrix. We mark cells that are reachable from the Pacific and Atlantic oceans separately. Finally, we find cells that can flow into both oceans by checking where the two sets of reachable cells overlap.

### 1. Algorithms & Data Structures (C++): Leetcode: Palindromic Substrings

To solve the problem of finding palindromic substrings on LeetCode, you can use the following approach:

1. **Brute Force Approach**: Generate all possible substrings and check if each substring is a palindrome. This approach has a time complexity of O(n^3) where n is the length of the input string.

2. **Expand Around Center**: This approach exploits the property of palindromes where expanding from a center, you can check if the substring is a palindrome. You consider each character and treat it as a center and expand to both sides. This approach has a time complexity of O(n^2).

Here's the code implementation of the second approach in C++:

```cpp
class Solution {
public:
    int countSubstrings(string s) {
        int count = 0;
        for (int i = 0; i < s.size(); ++i) {
            count += expandAroundCenter(s, i, i); // odd length palindromes
            count += expandAroundCenter(s, i, i + 1); // even length palindromes
        }
        return count;
    }
    
    int expandAroundCenter(const string& s, int left, int right) {
        int count = 0;
        while (left >= 0 && right < s.size() && s[left] == s[right]) {
            ++count;
            --left;
            ++right;
        }
        return count;
    }
};
```

In this code, `expandAroundCenter` function is used to find the number of palindromic substrings by expanding around a center. The `countSubstrings` function iterates through each character and treats it as a center and counts the palindromic substrings.

This code should pass the tests on LeetCode for the Palindromic Substrings problem.

### 1. Algorithms & Data Structures (C++): Leetcode: Product of Array Except Self

Sure! The "Product of Array Except Self" problem on LeetCode asks you to return an array where each element is the product of all the elements in the array except itself. You're allowed to use division, but the twist is to solve it without division in linear time and with constant space complexity.

Here's how you can solve it in C++:

```cpp
#include <vector>

std::vector<int> productExceptSelf(std::vector<int>& nums) {
    int n = nums.size();
    std::vector<int> output(n, 1);

    int leftProduct = 1;
    for (int i = 0; i < n; ++i) {
        output[i] *= leftProduct;
        leftProduct *= nums[i];
    }

    int rightProduct = 1;
    for (int i = n - 1; i >= 0; --i) {
        output[i] *= rightProduct;
        rightProduct *= nums[i];
    }

    return output;
}
```

Explanation:

- We initialize `output` array with 1s because we will be multiplying by the left and right products later.
- In the first loop, we iterate through the array and calculate the product of all elements to the left of the current element and store it in the `output` array.
- In the second loop, we iterate through the array backward, calculating the product of all elements to the right of the current element and update the `output` array accordingly.

This solution has a time complexity of O(n) and space complexity of O(1) excluding the output array.

### 1. Algorithms & Data Structures (C++): Leetcode: Remove Nth Node From End Of List

Certainly! Removing the Nth node from the end of a linked list is a classic problem in data structures. Here's a C++ solution for the problem using two pointers:

```cpp
#include <iostream>

using namespace std;

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

ListNode* removeNthFromEnd(ListNode* head, int n) {
    ListNode* dummy = new ListNode(0);
    dummy->next = head;
    ListNode* fast = dummy;
    ListNode* slow = dummy;

    // Move fast pointer to the nth node from the beginning
    for (int i = 0; i < n; ++i) {
        fast = fast->next;
    }

    // Move fast to the end, maintaining the gap of n between fast and slow
    while (fast->next != NULL) {
        fast = fast->next;
        slow = slow->next;
    }

    // Delete the nth node from the end
    ListNode* temp = slow->next;
    slow->next = slow->next->next;
    delete temp;

    return dummy->next;
}

// Utility function to print the linked list
void printList(ListNode* head) {
    while (head != NULL) {
        cout << head->val << " ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    // Example usage
    ListNode* head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);

    cout << "Original List: ";
    printList(head);

    int n = 2;
    head = removeNthFromEnd(head, n);

    cout << "After removing " << n << "th node from end: ";
    printList(head);

    return 0;
}
```

This code defines a `ListNode` struct representing a node in the linked list. The `removeNthFromEnd` function takes the head of the linked list and the value of N as input and returns the head of the linked list after removing the Nth node from the end. It uses two pointers, fast and slow, to achieve this efficiently in a single pass.

### 1. Algorithms & Data Structures (C++): Leetcode: Reorder List

To solve the "Reorder List" problem on LeetCode, you'll need to reorder the nodes of a singly linked list in-place.

Here's the general approach you can take:

1. **Split the list in half**: Use a fast-slow pointer approach to find the middle of the linked list. After finding the middle, split the list into two halves.

2. **Reverse the second half**: Reverse the second half of the linked list.

3. **Merge the two halves**: Merge the first half and the reversed second half alternately.

Here's a C++ implementation of the algorithm:

```cpp
#include <iostream>

using namespace std;

struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

class Solution {
public:
    void reorderList(ListNode* head) {
        if (!head || !head->next) return;

        // Step 1: Split the list in half
        ListNode *slow = head, *fast = head;
        while (fast->next && fast->next->next) {
            slow = slow->next;
            fast = fast->next->next;
        }
        ListNode *secondHalf = slow->next;
        slow->next = nullptr;

        // Step 2: Reverse the second half
        ListNode *prev = nullptr, *curr = secondHalf, *next;
        while (curr) {
            next = curr->next;
            curr->next = prev;
            prev = curr;
            curr = next;
        }
        secondHalf = prev;

        // Step 3: Merge the two halves
        ListNode *first = head;
        while (first && secondHalf) {
            ListNode *firstNext = first->next;
            ListNode *secondNext = secondHalf->next;

            first->next = secondHalf;
            secondHalf->next = firstNext;

            first = firstNext;
            secondHalf = secondNext;
        }
    }
};

// Function to print the list
void printList(ListNode* head) {
    while (head) {
        cout << head->val << " ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    // Example usage
    ListNode *head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);

    Solution sol;
    sol.reorderList(head);
    printList(head); // Output: 1 5 2 4 3

    return 0;
}
```

This code defines a `ListNode` structure representing a node in a linked list and a `Solution` class with a `reorderList` method to perform the reordering. In the `main` function, an example linked list is created, and the `reorderList` method is called to reorder it. Finally, the reordered list is printed.

### 1. Algorithms & Data Structures (C++): Leetcode: Reverse a Linked List

Sure, here's the C++ code to reverse a linked list:

```cpp
#include <iostream>

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* reverseList(ListNode* head) {
    ListNode* prev = nullptr;
    ListNode* curr = head;
    ListNode* next = nullptr;
    
    while (curr != nullptr) {
        next = curr->next; // Store next node
        curr->next = prev; // Reverse current node's pointer
        prev = curr;       // Move pointers one position ahead
        curr = next;
    }
    
    return prev; // New head of the reversed list
}

// Utility function to print the linked list
void printList(ListNode* head) {
    while (head != nullptr) {
        std::cout << head->val << " ";
        head = head->next;
    }
    std::cout << std::endl;
}

int main() {
    // Create a sample linked list: 1 -> 2 -> 3 -> 4 -> 5
    ListNode* head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);
    
    std::cout << "Original list: ";
    printList(head);
    
    // Reverse the linked list
    head = reverseList(head);
    
    std::cout << "Reversed list: ";
    printList(head);
    
    return 0;
}
```

This code defines a `ListNode` struct representing a node in the linked list. The `reverseList` function reverses the given linked list in place and returns the new head of the reversed list. Finally, in the `main` function, a sample linked list is created, reversed, and printed before and after the reversal.

### 1. Algorithms & Data Structures (C++): Leetcode: Reverse Bits

To reverse bits in C++, you can use bitwise operations. Here's a simple implementation for the LeetCode problem "Reverse Bits":

```cpp
#include <cstdint>

uint32_t reverseBits(uint32_t n) {
    uint32_t reversed = 0;
    for (int i = 0; i < 32; ++i) {
        reversed <<= 1;         // Left shift 'reversed' to make room for the next bit
        reversed |= (n & 1);    // Set the least significant bit of 'reversed' to the least significant bit of 'n'
        n >>= 1;                // Right shift 'n' to get the next bit to reverse
    }
    return reversed;
}
```

This function iterates through each bit of the input number `n`, extracts the least significant bit using bitwise AND with `1`, and appends it to the `reversed` variable after shifting `reversed` left by one position. Finally, it returns the reversed number.

You can test this function with various inputs to verify its correctness.

### 1. Algorithms & Data Structures (C++): Leetcode: Rotate Image

The "Rotate Image" problem on LeetCode is a classic algorithm problem that involves rotating an N x N 2D matrix representing an image. The task is to rotate the image by 90 degrees (clockwise) in place.

Here's a common approach to solving this problem in C++:

```cpp
#include <vector>

using namespace std;

void rotate(vector<vector<int>>& matrix) {
    int n = matrix.size();
    
    // Transpose the matrix
    for (int i = 0; i < n; ++i) {
        for (int j = i; j < n; ++j) {
            swap(matrix[i][j], matrix[j][i]);
        }
    }
    
    // Reverse each row
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < n / 2; ++j) {
            swap(matrix[i][j], matrix[i][n - 1 - j]);
        }
    }
}
```

Explanation:

1. Transpose the matrix: Swap matrix[i][j] with matrix[j][i]. This step effectively reflects the matrix along its main diagonal.
2. Reverse each row: Iterate through each row and swap elements from the leftmost to the middle with elements from the rightmost to the middle.

This solution has a time complexity of O(N^2), where N is the number of rows (or columns) in the matrix. The space complexity is O(1) since the rotation is done in place without using extra space.

You can test this solution by passing a 2D vector representing the image to the `rotate` function.

### 1. Algorithms & Data Structures (C++): Leetcode: Same Tree

The "Same Tree" problem on LeetCode is a classic algorithm question that involves comparing two binary trees to determine if they are structurally identical or not. Here's how you can solve it in C++ using a recursive approach:

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
    bool isSameTree(TreeNode* p, TreeNode* q) {
        // If both trees are empty, they are identical
        if (p == nullptr && q == nullptr)
            return true;
        
        // If one tree is empty but the other is not, they are not identical
        if (p == nullptr || q == nullptr)
            return false;
        
        // If the values of the current nodes are not equal, they are not identical
        if (p->val != q->val)
            return false;
        
        // Recursively check the left and right subtrees
        return isSameTree(p->left, q->left) && isSameTree(p->right, q->right);
    }
};

int main() {
    // Example usage
    TreeNode* p = new TreeNode(1);
    p->left = new TreeNode(2);
    p->right = new TreeNode(3);

    TreeNode* q = new TreeNode(1);
    q->left = new TreeNode(2);
    q->right = new TreeNode(3);

    Solution solution;
    std::cout << "Are the trees identical? " << std::boolalpha << solution.isSameTree(p, q) << std::endl;

    // Clean up memory
    delete p->left;
    delete p->right;
    delete p;
    delete q->left;
    delete q->right;
    delete q;

    return 0;
}
```

In this code, the `isSameTree` function recursively compares the nodes of the two trees. It returns true if both trees are empty (indicating they are identical), false if one tree is empty while the other is not, and false if the values of the current nodes are different. Otherwise, it recursively compares the left and right subtrees.

### 1. Algorithms & Data Structures (C++): Leetcode: Search in Rotated Sorted Array

The "Search in Rotated Sorted Array" problem on LeetCode is a classic problem that can be solved using a modified binary search algorithm. Here's a C++ solution:

```cpp
#include <vector>

using namespace std;

class Solution {
public:
    int search(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size() - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                return mid;
            }
            
            // Check if left half is sorted
            if (nums[left] <= nums[mid]) {
                // If target is within the sorted half, search left
                if (nums[left] <= target && target < nums[mid]) {
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            } else { // Right half is sorted
                // If target is within the sorted half, search right
                if (nums[mid] < target && target <= nums[right]) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }
        }
        
        return -1; // Target not found
    }
};
```

This solution employs a binary search approach. We find the middle element and check if the left or right half is sorted. Based on that, we adjust our search area accordingly. This approach ensures that the time complexity remains O(log n), where n is the number of elements in the array.

### 1. Algorithms & Data Structures (C++): Leetcode: Serialize and Deserialize Binary Tree

Serializing and deserializing a binary tree is a common problem in programming interviews and coding competitions. It involves converting a binary tree into a string representation, and then reconstructing the original tree from that string. Here's how you can implement serialization and deserialization of a binary tree in C++:

```cpp
#include <iostream>
#include <sstream>
#include <string>
#include <queue>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Codec {
public:
    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        if (!root) return "X"; // Use X to represent null nodes
        return to_string(root->val) + "," + serialize(root->left) + "," + serialize(root->right);
    }

    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        stringstream ss(data);
        return deserializeHelper(ss);
    }

private:
    TreeNode* deserializeHelper(stringstream& ss) {
        string val;
        getline(ss, val, ',');
        if (val == "X") return nullptr; // Null node
        TreeNode* root = new TreeNode(stoi(val));
        root->left = deserializeHelper(ss);
        root->right = deserializeHelper(ss);
        return root;
    }
};

// Helper function to print the tree (for testing)
void printTree(TreeNode* root) {
    if (!root) return;
    cout << root->val << " ";
    printTree(root->left);
    printTree(root->right);
}

int main() {
    // Example usage
    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->right->left = new TreeNode(4);
    root->right->right = new TreeNode(5);

    Codec codec;
    string serialized = codec.serialize(root);
    cout << "Serialized: " << serialized << endl;

    TreeNode* deserialized = codec.deserialize(serialized);
    cout << "Deserialized: ";
    printTree(deserialized);

    return 0;
}
```

This code defines a `TreeNode` struct representing a node in the binary tree and a `Codec` class with `serialize` and `deserialize` methods. The `serialize` method recursively converts the binary tree to a string, and the `deserialize` method reconstructs the tree from the string. The "X" character is used to represent null nodes in the serialization process.

### 1. Algorithms & Data Structures (C++): Leetcode: Set Matrix Zeroes

To solve the "Set Matrix Zeroes" problem on LeetCode using C++, you can use a simple approach. Here's a step-by-step guide:

1. **Scan the Matrix**: Traverse through the matrix and mark the rows and columns that need to be zeroed out.

2. **Marking**: For each cell containing a zero, mark its corresponding row and column.

3. **Set Zeroes**: Iterate through the matrix again, setting the entire row and column to zero if either the row or column is marked.

Here's a C++ code implementing this algorithm:

```cpp
#include <vector>
using namespace std;

class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        int m = matrix.size();
        int n = matrix[0].size();

        bool firstRowZero = false;
        bool firstColZero = false;

        // Check if the first row has zeros
        for (int j = 0; j < n; ++j) {
            if (matrix[0][j] == 0) {
                firstRowZero = true;
                break;
            }
        }

        // Check if the first column has zeros
        for (int i = 0; i < m; ++i) {
            if (matrix[i][0] == 0) {
                firstColZero = true;
                break;
            }
        }

        // Mark rows and columns to be set to zero
        for (int i = 1; i < m; ++i) {
            for (int j = 1; j < n; ++j) {
                if (matrix[i][j] == 0) {
                    matrix[i][0] = 0;  // mark the row
                    matrix[0][j] = 0;  // mark the column
                }
            }
        }

        // Set zeroes except the first row and column
        for (int i = 1; i < m; ++i) {
            for (int j = 1; j < n; ++j) {
                if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                    matrix[i][j] = 0;
                }
            }
        }

        // Set first row to zero if necessary
        if (firstRowZero) {
            for (int j = 0; j < n; ++j) {
                matrix[0][j] = 0;
            }
        }

        // Set first column to zero if necessary
        if (firstColZero) {
            for (int i = 0; i < m; ++i) {
                matrix[i][0] = 0;
            }
        }
    }
};
```

This solution has a time complexity of O(m * n) and a space complexity of O(1), where m is the number of rows and n is the number of columns in the matrix.

### 1. Algorithms & Data Structures (C++): Leetcode: Spiral Order Traversal (Spiral Matrix)

Sure, here's a C++ implementation for the Spiral Order Traversal (Spiral Matrix) problem on LeetCode:

```cpp
#include <iostream>
#include <vector>

using namespace std;

vector<int> spiralOrder(vector<vector<int>>& matrix) {
    vector<int> result;
    if(matrix.empty()) return result;
    
    int rows = matrix.size();
    int cols = matrix[0].size();
    
    int top = 0, bottom = rows - 1, left = 0, right = cols - 1;
    
    while(top <= bottom && left <= right) {
        // Traverse top row
        for(int i = left; i <= right; ++i) {
            result.push_back(matrix[top][i]);
        }
        top++;
        
        // Traverse right column
        for(int i = top; i <= bottom; ++i) {
            result.push_back(matrix[i][right]);
        }
        right--;
        
        // Traverse bottom row
        if(top <= bottom) {
            for(int i = right; i >= left; --i) {
                result.push_back(matrix[bottom][i]);
            }
            bottom--;
        }
        
        // Traverse left column
        if(left <= right) {
            for(int i = bottom; i >= top; --i) {
                result.push_back(matrix[i][left]);
            }
            left++;
        }
    }
    
    return result;
}

int main() {
    vector<vector<int>> matrix = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    vector<int> result = spiralOrder(matrix);

    // Output the result
    for(int num : result) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}
```

This implementation uses the concept of four boundaries (top, bottom, left, right) to traverse the matrix in a spiral order. The loop continues until these boundaries meet each other. During each iteration, it traverses the top row, right column, bottom row, and left column respectively.

### 1. Algorithms & Data Structures (C++): Leetcode: Subtree of Another Tree

To solve the "Subtree of Another Tree" problem on LeetCode using C++, you typically use a recursive approach to traverse the main tree and check if any subtree matches the given subtree. Here's a step-by-step explanation of how to do it:

1. **Define TreeNode Structure**: First, you need to define the structure for a binary tree node.

```cpp
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
```

1. **Implement the isSubtree Function**: This function checks if a given subtree exists in the main tree.

```cpp
bool isSubtree(TreeNode* s, TreeNode* t) {
    if (!s) return false; // If main tree is empty, return false
    return isSameTree(s, t) || isSubtree(s->left, t) || isSubtree(s->right, t);
}
```

1. **Implement the isSameTree Function**: This function checks if two trees are identical.

```cpp
bool isSameTree(TreeNode* s, TreeNode* t) {
    if (!s && !t) return true; // Both trees are empty
    if (!s || !t) return false; // One tree is empty, the other is not
    return (s->val == t->val) && isSameTree(s->left, t->left) && isSameTree(s->right, t->right);
}
```

1. **Putting it All Together**: Call the `isSubtree` function with the root of the main tree and the root of the subtree you want to check.

Here's the full code:

```cpp
#include <iostream>

using namespace std;

struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

bool isSameTree(TreeNode* s, TreeNode* t) {
    if (!s && !t) return true; // Both trees are empty
    if (!s || !t) return false; // One tree is empty, the other is not
    return (s->val == t->val) && isSameTree(s->left, t->left) && isSameTree(s->right, t->right);
}

bool isSubtree(TreeNode* s, TreeNode* t) {
    if (!s) return false; // If main tree is empty, return false
    return isSameTree(s, t) || isSubtree(s->left, t) || isSubtree(s->right, t);
}

int main() {
    // Construct the main tree
    TreeNode* s = new TreeNode(3);
    s->left = new TreeNode(4);
    s->right = new TreeNode(5);
    s->left->left = new TreeNode(1);
    s->left->right = new TreeNode(2);

    // Construct the subtree
    TreeNode* t = new TreeNode(4);
    t->left = new TreeNode(1);
    t->right = new TreeNode(2);

    // Check if subtree exists
    if (isSubtree(s, t))
        cout << "Subtree exists." << endl;
    else
        cout << "Subtree does not exist." << endl;

    return 0;
}
```

This code should effectively determine whether one tree is a subtree of another.

### 1. Algorithms & Data Structures (C++): Leetcode: Sum of Two Integers

To solve the "Sum of Two Integers" problem on LeetCode using C++, you can use the bitwise XOR operation to find the sum of two integers without using the arithmetic operator '+'.

Here's the C++ code:

```cpp
class Solution {
public:
    int getSum(int a, int b) {
        while (b != 0) {
            int carry = (unsigned int)(a & b) << 1;
            a = a ^ b;
            b = carry;
        }
        return a;
    }
};
```

Explanation:

- The `getSum` function takes two integers `a` and `b` as input and returns their sum without using the arithmetic operator '+'.
- In each iteration of the while loop, we calculate the carry using bitwise AND operator `(a & b)` and left shift by 1 (`<< 1`). This is because in binary addition, when both bits are 1, it results in a carry to the next higher bit.
- We update `a` to hold the sum of `a` and `b` without considering the carry using the bitwise XOR operator `^`.
- We update `b` to hold the carry, and the loop continues until there is no carry left, i.e., `b` becomes 0.
- Finally, we return the value of `a`, which contains the sum of the two integers.

### 1. Algorithms & Data Structures (C++): Leetcode: Top K Frequent Elements

To solve the "Top K Frequent Elements" problem on LeetCode using C++, you can use a combination of a hash map and a min-heap (priority queue). Here's a step-by-step approach:

1. Create a hash map to store the frequency of each element.
2. Iterate through the array to populate the hash map.
3. Create a min-heap (priority queue) to keep track of the K most frequent elements.
4. Iterate through the hash map and add elements to the min-heap.
5. If the size of the min-heap exceeds K, pop the element with the minimum frequency.
6. Finally, the min-heap will contain the K most frequent elements.

Here's the C++ code implementing the above approach:

```cpp
#include <vector>
#include <unordered_map>
#include <queue>

class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        // Step 1: Create a hash map to store frequency of elements
        unordered_map<int, int> freqMap;
        for (int num : nums) {
            freqMap[num]++;
        }
        
        // Step 2: Create a min-heap (priority queue)
        auto cmp = [](pair<int, int>& a, pair<int, int>& b) {
            return a.second > b.second; // Compare frequencies
        };
        priority_queue<pair<int, int>, vector<pair<int, int>>, decltype(cmp)> minHeap(cmp);
        
        // Step 3: Iterate through the hash map and add elements to min-heap
        for (auto& entry : freqMap) {
            minHeap.push(entry);
            if (minHeap.size() > k) {
                minHeap.pop(); // Maintain size k
            }
        }
        
        // Step 4: Extract top K elements from min-heap
        vector<int> result;
        while (!minHeap.empty()) {
            result.push_back(minHeap.top().first); // Store the element
            minHeap.pop();
        }
        
        // Step 5: Reverse the result to get elements in descending order of frequency
        reverse(result.begin(), result.end());
        
        return result;
    }
};
```

This solution has a time complexity of O(n log k), where n is the number of elements in the input array and k is the value of the parameter `k`.

### 1. Algorithms & Data Structures (C++): Leetcode: Tree

Certainly! Trees are fundamental data structures in computer science and have various applications. Here's an overview of tree-related algorithms and data structures in C++ and how they can be applied to solve problems on platforms like LeetCode:

1. **Binary Tree**: A binary tree is a hierarchical data structure in which each node has at most two children, referred to as the left child and the right child.

   - **Implementation**: You can implement a binary tree using a class with left and right pointers for each node.

   - **Common Problems**: Problems involving binary tree traversal (pre-order, in-order, post-order), finding the maximum depth, checking if a tree is balanced, etc.

2. **Binary Search Tree (BST)**: A binary search tree is a special type of binary tree where the left child is less than the parent and the right child is greater.

   - **Implementation**: Similar to a binary tree, but with the property that for any node, all nodes in its left subtree have values less than its value, and all nodes in its right subtree have values greater.

   - **Common Problems**: Insertion, deletion, searching for a key, finding minimum and maximum elements, finding the successor or predecessor of a node, etc.

3. **Balanced Binary Search Tree (AVL Tree, Red-Black Tree)**: These are self-balancing binary search trees where the height difference between the left and right subtrees of any node is at most one.

   - **Implementation**: Requires additional balancing operations during insertion and deletion to maintain the balance property.

   - **Common Problems**: Similar to BST, but with additional considerations for balancing.

4. **Tree Traversal Algorithms**:

   - **In-order Traversal**: Traverse the left subtree, visit the root, then traverse the right subtree.

   - **Pre-order Traversal**: Visit the root, traverse the left subtree, then traverse the right subtree.

   - **Post-order Traversal**: Traverse the left subtree, traverse the right subtree, then visit the root.

   - **Level-order Traversal (BFS)**: Visit nodes level by level, starting from the root.

5. **Tree Manipulation and Construction**: Problems that involve manipulating trees, constructing trees from different representations (e.g., arrays), converting between different tree representations, etc.

6. **Tree Algorithms**: Various algorithms like Lowest Common Ancestor (LCA), Diameter of Binary Tree, Maximum Path Sum, etc., which are specific to trees.

When solving tree problems on platforms like LeetCode, understanding these concepts and having a good grasp of tree traversal, manipulation, and common algorithms will be beneficial. Additionally, it's crucial to be proficient in using pointers and recursion, as they are often used in tree-related algorithms and data structures in C++.

### 1. Algorithms & Data Structures (C++): Leetcode: Two Sum

Sure, here's a simple solution in C++ for the "Two Sum" problem on LeetCode:

```cpp
#include <vector>
#include <unordered_map>

std::vector<int> twoSum(std::vector<int>& nums, int target) {
    std::unordered_map<int, int> numMap;
    std::vector<int> result;

    for (int i = 0; i < nums.size(); ++i) {
        int complement = target - nums[i];
        if (numMap.find(complement) != numMap.end()) {
            result.push_back(numMap[complement]);
            result.push_back(i);
            return result;
        }
        numMap[nums[i]] = i;
    }

    return result; // If no solution is found
}
```

This solution uses a hash map (unordered_map in C++) to store each number's index as we iterate through the array. While iterating, it calculates the complement of the current number needed to reach the target. If this complement exists in the map, it means we've found the two numbers that sum up to the target, so we return their indices. If not, we continue the iteration until we find a solution or exhaust all possibilities.

### 1. Algorithms & Data Structures (C++): Leetcode: Unique Paths

"Unique Paths" is a classic dynamic programming problem on LeetCode. The problem statement goes like this:

You are given a grid of m x n size. Starting from the top-left corner, you want to reach the bottom-right corner. You can only move either down or right at any point in time. How many possible unique paths are there?

This problem can be efficiently solved using dynamic programming. Here's how you can approach it in C++:

```cpp
#include <vector>

int uniquePaths(int m, int n) {
    // Create a 2D vector to store the number of paths for each cell
    std::vector<std::vector<int>> dp(m, std::vector<int>(n, 1));

    // Fill the dp table
    for (int i = 1; i < m; ++i) {
        for (int j = 1; j < n; ++j) {
            dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
        }
    }

    // Return the number of unique paths to reach the bottom-right corner
    return dp[m - 1][n - 1];
}

// Example usage:
int main() {
    int m = 3, n = 7;
    int result = uniquePaths(m, n);
    std::cout << "Number of unique paths: " << result << std::endl;
    return 0;
}
```

This solution uses a 2D vector `dp` to store the number of unique paths to reach each cell. The base case is initialized to 1, as there's only one way to reach the cells in the first row and the first column. Then, it iterates through each cell, filling in the number of paths by summing up the number of paths from the cell above and the cell to the left. Finally, it returns the number of unique paths to reach the bottom-right corner, which is stored in `dp[m - 1][n - 1]`.

### 1. Algorithms & Data Structures (C++): Leetcode: Valid Anagram

To solve the "Valid Anagram" problem on LeetCode using C++, you can employ a simple and efficient approach using character frequency counting. Here's how you can do it:

```cpp
#include <iostream>
#include <unordered_map>
#include <string>

using namespace std;

bool isAnagram(string s, string t) {
    if (s.length() != t.length()) // If the lengths are different, they can't be anagrams
        return false;

    unordered_map<char, int> freq;

    // Count the frequency of characters in string s
    for (char c : s) {
        freq[c]++;
    }

    // Decrement the frequency of characters in string t
    // If at any point a character's frequency becomes negative or it doesn't exist in s, return false
    for (char c : t) {
        if (--freq[c] < 0)
            return false;
    }

    return true; // All characters in s and t have the same frequency
}

int main() {
    string s = "anagram";
    string t = "nagaram";

    if (isAnagram(s, t))
        cout << "The strings are anagrams.\n";
    else
        cout << "The strings are not anagrams.\n";

    return 0;
}
```

This code first checks if the lengths of the two strings are equal. If they're not, they can't be anagrams. Then, it uses an unordered map to count the frequency of characters in the first string. After that, it iterates through the second string and decrements the counts in the map. If at any point a character's count becomes negative or it doesn't exist in the first string, it returns false. Otherwise, it returns true.

### 1. Algorithms & Data Structures (C++): Leetcode: Valid Palindrome

To solve the "Valid Palindrome" problem on LeetCode using C++, you can follow these steps:

1. Define two pointers, one starting from the beginning of the string and the other from the end.
2. Iterate over the string until the pointers meet.
3. For each iteration, move the pointers inward, skipping non-alphanumeric characters.
4. Compare the characters pointed by the two pointers.
5. If at any point the characters are not equal, return false. If they are equal for all comparisons, return true.

Here's a C++ code snippet to implement this algorithm:

```cpp
#include <iostream>
#include <cctype>

bool isPalindrome(std::string s) {
    int left = 0;
    int right = s.length() - 1;
    
    while (left < right) {
        // Skip non-alphanumeric characters from left pointer
        while (left < right && !isalnum(s[left]))
            left++;
        // Skip non-alphanumeric characters from right pointer
        while (left < right && !isalnum(s[right]))
            right--;
        
        // Compare characters
        if (tolower(s[left]) != tolower(s[right]))
            return false;
        
        // Move pointers inward
        left++;
        right--;
    }
    return true;
}

int main() {
    std::string str = "A man, a plan, a canal: Panama";
    if (isPalindrome(str))
        std::cout << "The string is a palindrome.";
    else
        std::cout << "The string is not a palindrome.";
    
    return 0;
}
```

This code snippet defines a function `isPalindrome()` that checks whether a given string is a palindrome or not. The `main()` function demonstrates its usage by checking whether the example string "A man, a plan, a canal: Panama" is a palindrome.

### 1. Algorithms & Data Structures (C++): Leetcode: Valid Parentheses

Sure, here's a C++ solution to the "Valid Parentheses" problem on LeetCode:

```cpp
#include <iostream>
#include <stack>
#include <string>

using namespace std;

bool isValid(string s) {
    stack<char> parenthesesStack;

    for (char &c : s) {
        if (c == '(' || c == '[' || c == '{') {
            parenthesesStack.push(c);
        } else {
            if (parenthesesStack.empty()) return false;
            if ((c == ')' && parenthesesStack.top() != '(') ||
                (c == ']' && parenthesesStack.top() != '[') ||
                (c == '}' && parenthesesStack.top() != '{')) {
                return false;
            }
            parenthesesStack.pop();
        }
    }

    return parenthesesStack.empty();
}

int main() {
    string input;
    cout << "Enter a string containing parentheses: ";
    cin >> input;

    if (isValid(input)) {
        cout << "The parentheses are valid." << endl;
    } else {
        cout << "The parentheses are not valid." << endl;
    }

    return 0;
}
```

This solution uses a stack to keep track of the opening parentheses encountered. When a closing parenthesis is encountered, it checks if it matches the top of the stack. If it does, it pops the top element from the stack, indicating a matched pair. If the stack is empty when encountering a closing parenthesis or if the closing parenthesis doesn't match the top of the stack, the string is invalid. Finally, the function returns true if the stack is empty at the end, indicating all parentheses were matched.

### 1. Algorithms & Data Structures (C++): Leetcode: Validate Binary Search Tree

To validate a binary search tree (BST), you need to ensure that for every node in the tree, its value is greater than all values in its left subtree and less than all values in its right subtree. This can be efficiently implemented using a recursive approach. Here's a C++ implementation:

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

class Solution {
public:
    bool isValidBST(TreeNode* root) {
        return isValidBST(root, LONG_MIN, LONG_MAX);
    }
    
    bool isValidBST(TreeNode* root, long long minVal, long long maxVal) {
        if (!root)
            return true;
        
        if (root->val <= minVal || root->val >= maxVal)
            return false;
        
        return isValidBST(root->left, minVal, root->val) && isValidBST(root->right, root->val, maxVal);
    }
};

// Helper function to create a binary tree from an array (used for testing)
TreeNode* createBinaryTree(int arr[], int n, int i) {
    if (i >= n || arr[i] == -1)
        return nullptr;

    TreeNode* root = new TreeNode(arr[i]);
    root->left = createBinaryTree(arr, n, 2 * i + 1);
    root->right = createBinaryTree(arr, n, 2 * i + 2);

    return root;
}

int main() {
    int arr[] = {2, 1, 3};
    int n = sizeof(arr) / sizeof(arr[0]);
    TreeNode* root = createBinaryTree(arr, n, 0);

    Solution sol;
    if (sol.isValidBST(root))
        std::cout << "Valid BST" << std::endl;
    else
        std::cout << "Not a valid BST" << std::endl;

    return 0;
}
```

This code defines a `TreeNode` struct representing a node in the binary tree and a `Solution` class with the `isValidBST` method to check if a given binary tree is a valid BST. The `isValidBST` method takes a root node and recursively validates if each node's value falls within the appropriate range.

In the `main` function, a binary tree is created from an array for testing purposes, and then the `isValidBST` method is called to check if it's a valid BST.

### 1. Algorithms & Data Structures (C++): Leetcode: Word Break Problem

The Word Break problem is a classic dynamic programming problem. The problem statement typically goes like this: given a string and a dictionary of words, determine if the string can be segmented into a space-separated sequence of one or more dictionary words.

Here's a high-level approach to solving this problem:

1. **Dynamic Programming**: We can solve this problem using dynamic programming. We create a boolean array `dp[]` of size `n+1`, where `n` is the length of the input string. `dp[i]` will be true if the substring `s[0...i-1]` can be segmented into space-separated sequences of words from the dictionary, otherwise false.

2. **Iterative Approach**: We iterate through each position `i` of the input string, and for each position, we check if there is a word in the dictionary that ends at position `i` and if the substring before that word can be segmented. If both conditions are true, then `dp[i]` is set to true.

3. **Base Case**: `dp[0]` is always true, as an empty string is always present in the dictionary.

4. **Dictionary Lookup**: To efficiently check if a substring is present in the dictionary, we can use a hash set or a trie data structure for fast lookup.

Here's a sample implementation in C++:

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>

using namespace std;

bool wordBreak(string s, unordered_set<string>& wordDict) {
    int n = s.length();
    vector<bool> dp(n + 1, false);
    dp[0] = true;

    for (int i = 1; i <= n; ++i) {
        for (int j = 0; j < i; ++j) {
            if (dp[j] && wordDict.count(s.substr(j, i - j)) > 0) {
                dp[i] = true;
                break;
            }
        }
    }

    return dp[n];
}

int main() {
    string s = "leetcode";
    unordered_set<string> wordDict = {"leet", "code"};

    if (wordBreak(s, wordDict)) {
        cout << "The string can be segmented into words." << endl;
    } else {
        cout << "The string cannot be segmented into words." << endl;
    }

    return 0;
}
```

In this implementation, `wordBreak` function returns true if the string can be segmented into words from the dictionary, otherwise false. The `main` function demonstrates its usage with a sample input string and dictionary.

### 1. Algorithms & Data Structures (C++): Leetcode: Word Search

Sure, the "Word Search" problem on LeetCode is a classic example of backtracking. Here's a general approach in C++:

```cpp
#include <vector>
#include <string>

using namespace std;

class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        if (board.empty() || board[0].empty()) return false;
        
        int m = board.size();
        int n = board[0].size();
        
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (dfs(board, word, 0, i, j)) return true;
            }
        }
        
        return false;
    }
    
private:
    bool dfs(vector<vector<char>>& board, string& word, int idx, int i, int j) {
        if (idx == word.size()) return true;
        if (i < 0 || j < 0 || i >= board.size() || j >= board[0].size() || board[i][j] != word[idx]) return false;
        
        char temp = board[i][j];
        board[i][j] = '#'; // mark as visited
        
        bool found = dfs(board, word, idx + 1, i + 1, j) || dfs(board, word, idx + 1, i - 1, j) ||
                     dfs(board, word, idx + 1, i, j + 1) || dfs(board, word, idx + 1, i, j - 1);
        
        board[i][j] = temp; // restore
        
        return found;
    }
};
```

This solution uses depth-first search (DFS) and backtracking to explore all possible paths starting from each cell. It traverses the board and checks if the word can be found starting from each cell. The `dfs` function recursively explores neighboring cells to find the word. If a cell matches the current character in the word, it marks it as visited, explores its neighbors, and then unmarks it if the word cannot be formed through that path.


### 1. Algorithms & Data Structures (C++): Top 10 Big O Interview Questions (Amazon, Facebook, Apple and Microsoft)

Sure, here are some common algorithm and data structure interview questions that often come up in interviews at top tech companies like Amazon, Facebook, Apple, and Microsoft, along with their respective Big O complexities:

1. **Reverse a String**: Write a function to reverse a string in-place.
   - **Complexity**: O(n), where n is the length of the string.

2. **Find the Missing Number**: Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.
   - **Complexity**: O(n), where n is the length of the array.

3. **Check for Palindrome**: Determine if a given string is a palindrome.
   - **Complexity**: O(n), where n is the length of the string.

4. **Merge Two Sorted Lists**: Merge two sorted linked lists into one sorted linked list.
   - **Complexity**: O(n + m), where n and m are the lengths of the two lists.

5. **Binary Search**: Implement binary search on a sorted array.
   - **Complexity**: O(log n), where n is the number of elements in the array.

6. **Find Maximum Subarray Sum**: Given an array of integers, find the contiguous subarray with the largest sum.
   - **Complexity**: O(n), where n is the length of the array.

7. **Find Duplicate Number**: Given an array nums containing n + 1 integers where each integer is between 1 and n (inclusive), find the duplicate one.
   - **Complexity**: O(n), where n is the length of the array.

8. **Counting Sort**: Implement counting sort algorithm.
   - **Complexity**: O(n + k), where n is the number of elements in the array and k is the range of the input.

9. **Graph Traversal - Breadth First Search (BFS)**: Implement BFS for a graph.
   - **Complexity**: O(V + E), where V is the number of vertices and E is the number of edges in the graph.

10. **Graph Traversal - Depth First Search (DFS)**: Implement DFS for a graph.
    - **Complexity**: O(V + E), where V is the number of vertices and E is the number of edges in the graph.

These are just a few examples, but mastering these common interview questions and understanding their Big O complexities can greatly improve your performance in technical interviews with these companies.

### 1. Algorithms & Data Structures (C++): Top Interview Questions

Sure, here are some common interview questions on algorithms and data structures in C++:

1. **Array-related Questions:**
   - Find the maximum subarray sum.
   - Rotate an array to the right by k steps.
   - Implement an algorithm to find the intersection of two arrays.

2. **String-related Questions:**
   - Reverse a string.
   - Determine if a string has all unique characters.
   - Check if two strings are anagrams of each other.

3. **Linked List-related Questions:**
   - Reverse a linked list.
   - Detect a cycle in a linked list.
   - Find the intersection point of two linked lists.

4. **Tree and Graph-related Questions:**
   - Implement depth-first search (DFS) and breadth-first search (BFS) for a graph.
   - Find the lowest common ancestor (LCA) of two nodes in a binary tree.
   - Determine if a binary tree is a binary search tree (BST).

5. **Sorting and Searching Questions:**
   - Implement quicksort, mergesort, or heapsort.
   - Find the k-th largest/smallest element in an array.
   - Implement binary search in a sorted array.

6. **Dynamic Programming Questions:**
   - Calculate the nth Fibonacci number using dynamic programming.
   - Solve the 0/1 knapsack problem.
   - Longest increasing subsequence.

7. **Miscellaneous Questions:**
   - Implement a stack using arrays or linked lists.
   - Implement a queue using stacks.
   - Implement a priority queue.

Remember, in interviews, it's not just about solving the problem, but also about explaining your thought process, considering edge cases, and optimizing your solution if possible. Practice coding these questions, and also be prepared for variations or follow-up questions.
