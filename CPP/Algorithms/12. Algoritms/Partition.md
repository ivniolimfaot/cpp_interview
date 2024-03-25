
### 1. Algorithms & Data Structures (C++): Partition Equal Sum Subset

Partition Equal Sum Subset is a classic problem in computer science and dynamic programming. The problem is to determine whether a given set can be partitioned into two subsets such that the sum of elements in both subsets is equal. Here's a C++ implementation using dynamic programming:

```cpp
#include <iostream>
#include <vector>

using namespace std;

bool canPartition(vector<int>& nums) {
    int totalSum = 0;
    for (int num : nums) {
        totalSum += num;
    }

    // If the total sum is odd, it can't be partitioned into two equal subsets
    if (totalSum % 2 != 0) {
        return false;
    }

    int target = totalSum / 2;
    vector<bool> dp(target + 1, false);
    dp[0] = true; // Base case: 0 can be achieved by not selecting any element

    for (int num : nums) {
        for (int i = target; i >= num; i--) {
            dp[i] = dp[i] || dp[i - num];
        }
    }

    return dp[target];
}

int main() {
    vector<int> nums = {1, 5, 11, 5}; // Example input
    if (canPartition(nums)) {
        cout << "Can be partitioned into two equal sum subsets." << endl;
    } else {
        cout << "Cannot be partitioned into two equal sum subsets." << endl;
    }
    return 0;
}
```

In this implementation, we use dynamic programming to solve the problem efficiently. We create a boolean array `dp` of size `target + 1`, where `target` is half of the total sum of elements in the input array. Each element `dp[i]` represents whether a subset sum of `i` can be achieved using elements from the input array.

We initialize `dp[0]` to `true` because it's always possible to achieve a subset sum of 0 by not selecting any element. Then, we iterate over the input array and update the `dp` array accordingly. Finally, we return `dp[target]`, which indicates whether it's possible to partition the array into two equal sum subsets.

### 1. Algorithms & Data Structures (C++): Partition List

Certainly! In computer science, partitioning a list typically refers to rearranging its elements based on a certain condition. In the context of a singly linked list, "Partition List" often refers to rearranging the list so that all nodes with values less than a given value come before all nodes with values greater than or equal to that value.

Here's a C++ implementation of partitioning a linked list around a given value:

```cpp
#include <iostream>

using namespace std;

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

ListNode* partition(ListNode* head, int x) {
    ListNode less_head(0); // Dummy head for nodes less than x
    ListNode greater_head(0); // Dummy head for nodes greater than or equal to x
    ListNode *less_ptr = &less_head;
    ListNode *greater_ptr = &greater_head;
    
    while (head != nullptr) {
        if (head->val < x) {
            less_ptr->next = head;
            less_ptr = less_ptr->next;
        } else {
            greater_ptr->next = head;
            greater_ptr = greater_ptr->next;
        }
        head = head->next;
    }
    
    // Combine less and greater lists
    greater_ptr->next = nullptr; // Terminate the greater list
    less_ptr->next = greater_head.next; // Append the greater list to the end of the less list
    
    return less_head.next;
}

// Utility function to print the linked list
void printList(ListNode* head) {
    while (head != nullptr) {
        cout << head->val << " ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    // Example usage
    ListNode* head = new ListNode(1);
    head->next = new ListNode(4);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(2);
    head->next->next->next->next = new ListNode(5);
    head->next->next->next->next->next = new ListNode(2);
    
    cout << "Original List: ";
    printList(head);
    
    int x = 3; // Partition around value 3
    ListNode* partitioned_head = partition(head, x);
    
    cout << "Partitioned List around " << x << ": ";
    printList(partitioned_head);
    
    // Clean up memory
    while (partitioned_head != nullptr) {
        ListNode* temp = partitioned_head;
        partitioned_head = partitioned_head->next;
        delete temp;
    }
    
    return 0;
}
```

This program defines a `ListNode` struct representing each node of the linked list. The `partition` function rearranges the nodes of the linked list around a given value `x`. It creates two separate linked lists: one for nodes with values less than `x`, and the other for nodes with values greater than or equal to `x`. Then it combines these lists and returns the head of the new partitioned list. Finally, in the `main` function, an example usage is demonstrated.

### 1. Algorithms & Data Structures (C++): Partition N into positive integers

Partitioning a positive integer \( N \) into positive integers means expressing \( N \) as the sum of positive integers. This problem can be approached using recursion, dynamic programming, or even mathematical techniques.

Here's a recursive approach in C++ to partition \( N \) into positive integers:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to print partitions
void printPartition(vector<int>& partition) {
    for (int i = 0; i < partition.size(); ++i) {
        cout << partition[i];
        if (i != partition.size() - 1)
            cout << " + ";
    }
    cout << endl;
}

// Recursive function to generate partitions
void generatePartitions(int n, vector<int>& partition) {
    if (n == 0) {
        // If n becomes 0, we have found a partition
        printPartition(partition);
        return;
    }
    
    // Try all numbers from 1 to n for partitioning
    for (int i = 1; i <= n; ++i) {
        if (!partition.empty() && i < partition.back())
            continue; // Skip if the number is less than the previous one to avoid duplicate partitions
        
        partition.push_back(i);
        generatePartitions(n - i, partition);
        partition.pop_back();
    }
}

int main() {
    int N;
    cout << "Enter a positive integer: ";
    cin >> N;

    vector<int> partition;
    cout << "Partitions of " << N << " are:" << endl;
    generatePartitions(N, partition);

    return 0;
}
```

This code will prompt the user to input a positive integer \( N \) and then print all possible partitions of \( N \) into positive integers.

Keep in mind that this is a brute-force approach and might not be efficient for large \( N \). Dynamic programming can be used to optimize the solution by avoiding recomputation of overlapping subproblems.

### 1. Algorithms & Data Structures (C++): Partition Problems

Partition problems in algorithms and data structures involve dividing a set of elements into multiple subsets according to certain constraints or criteria. These problems are commonly encountered in various areas of computer science, including dynamic programming, combinatorial optimization, and computational biology. Here's an overview of partition problems and how they're typically approached in C++:

1. **Partition Equal Subset Sum**:
   - Given a set of positive integers, determine if it can be partitioned into two subsets such that the sum of elements in both subsets is equal.
   - This problem can be solved using dynamic programming. You create a boolean DP array where dp[i][j] represents whether a subset of elements from the first i elements can sum up to j.
   - The time complexity of this solution is O(n*sum), where n is the number of elements in the set and sum is the total sum of all elements.

2. **Partition to K Equal Sum Subsets**:
   - Given an array of integers and a positive integer k, determine if it is possible to divide the array into k non-empty subsets with equal sums.
   - This problem can also be solved using dynamic programming. You can use a recursive approach where you try placing each element into one of the k subsets and check if the subsets have equal sums.
   - The time complexity of this solution is O(k * 2^n), where n is the number of elements in the array.

3. **Partition Problem (Subset Sum)**:
   - Given a set of non-negative integers, determine if it can be partitioned into two subsets such that the sum of elements in both subsets is the same.
   - This problem is a variation of the subset sum problem and can be solved using similar dynamic programming techniques.
   - The time complexity of the dynamic programming solution is O(n*sum), where n is the number of elements in the set and sum is the total sum of all elements.

4. **Balanced Partition Problem**:
   - Given a set of integers, partition the set into two subsets such that the difference between the sum of elements in both subsets is minimized.
   - This problem can be solved using dynamic programming or backtracking techniques. You can use a recursive approach to try all possible partitions and minimize the difference between subset sums.
   - The time complexity depends on the approach used, but typically it's exponential in the worst case.

When implementing these algorithms in C++, you can leverage standard library containers like vectors and arrays along with dynamic programming techniques to efficiently solve partition problems. Additionally, for optimization, you might need to handle cases with large inputs or specific constraints differently.
