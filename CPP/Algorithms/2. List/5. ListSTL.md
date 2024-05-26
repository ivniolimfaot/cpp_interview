
### 1. Algorithms & Data Structures (C++): List vs Linked List

In C++, both lists and linked lists are fundamental data structures, but they serve different purposes and have different characteristics.

**List (std::list)**:

1. **Implementation**: Lists in C++ are typically implemented as doubly-linked lists. This means that each element of the list contains pointers to both the next and the previous elements in the list.
  
2. **Insertion and Deletion**: Insertion and deletion operations in a list are efficient, even at arbitrary positions within the list. This is because inserting or deleting an element in a linked list only requires updating the pointers of adjacent nodes.

3. **Access Time**: Accessing elements in a list is slower compared to arrays or vectors because lists don't support random access. To access an element at a specific position, you have to traverse the list from the beginning or end until you reach the desired position.

4. **Iterators**: Lists support bidirectional iterators, meaning you can traverse the elements forwards and backwards efficiently.

5. **Memory Overhead**: Lists have a higher memory overhead compared to arrays or vectors because of the additional memory required for storing the pointers to the next and previous elements.

**Linked List**:

1. **Flexibility**: Linked lists are more flexible than arrays or vectors because they don't require contiguous memory allocation. They can easily grow or shrink in size without the need for reallocation.

2. **Implementation**: There are different types of linked lists such as singly-linked lists, doubly-linked lists, and circular linked lists. Each type has its own advantages and use cases. Singly-linked lists only have pointers to the next element, while doubly-linked lists have pointers to both the next and previous elements.

3. **Insertion and Deletion**: Similar to lists, insertion and deletion operations in linked lists are efficient because they only involve updating pointers. However, the efficiency may vary depending on whether it's a singly or doubly-linked list and the position of insertion/deletion.

4. **Access Time**: Accessing elements in a linked list is slower compared to arrays, vectors, or lists because linked lists don't support random access. You have to traverse the list from the beginning (or end, in the case of doubly-linked lists) until you reach the desired position.

5. **Memory Overhead**: Linked lists also have a higher memory overhead compared to arrays or vectors due to the pointers required for linking the elements.

**Summary**:

- Use lists (std::list) when you need efficient insertion and deletion operations at arbitrary positions and don't require frequent random access.
- Use linked lists when you need flexibility in memory allocation, such as when you expect frequent insertions or deletions at the beginning or middle of the list, or when contiguous memory allocation is not feasible.

### 1. Algorithms & Data Structures (C++): List: Find Longest String

To find the longest string in a list of strings in C++, you can iterate through the list and keep track of the longest string encountered so far. Here's a simple example using a `std::vector` to represent the list of strings:

```cpp
#include <iostream>
#include <vector>
#include <string>

std::string findLongestString(const std::vector<std::string>& strings) {
    if (strings.empty()) {
        // Handle empty list case
        return "";
    }
    
    std::string longest = strings[0]; // Assume first string is the longest
    
    // Iterate through the list starting from the second string
    for (size_t i = 1; i < strings.size(); ++i) {
        if (strings[i].length() > longest.length()) {
            longest = strings[i];
        }
    }
    
    return longest;
}

int main() {
    std::vector<std::string> strings = {"apple", "banana", "orange", "kiwi", "strawberry"};
    
    std::string longest = findLongestString(strings);
    
    if (longest.empty()) {
        std::cout << "List is empty." << std::endl;
    } else {
        std::cout << "Longest string: " << longest << std::endl;
    }
    
    return 0;
}
```

In this code:

- The function `findLongestString` takes a vector of strings as input and returns the longest string found in the list.
- Inside the function, it first checks if the list is empty. If it is, it returns an empty string.
- Otherwise, it assumes the first string in the list is the longest.
- It then iterates through the remaining strings in the list and updates the `longest` variable if it encounters a longer string.
- Finally, it returns the longest string found.
- In the `main` function, a sample list of strings is created, and the `findLongestString` function is called to find the longest string.

### 1. Algorithms & Data Structures (C++): List: Find Max Min

To find the maximum and minimum elements in a list using C++, you can iterate through the list and keep track of the maximum and minimum elements found so far. Here's a simple implementation:

```cpp
#include <iostream>
#include <vector>
#include <limits> // for numeric_limits

// Function to find maximum and minimum elements in a list
void findMaxMin(const std::vector<int>& nums, int& maxElement, int& minElement) {
    // Initialize max and min to the first element of the list
    maxElement = std::numeric_limits<int>::min();
    minElement = std::numeric_limits<int>::max();

    // Iterate through the list
    for (int num : nums) {
        // Update max if current element is greater
        if (num > maxElement)
            maxElement = num;
        
        // Update min if current element is smaller
        if (num < minElement)
            minElement = num;
    }
}

int main() {
    // Sample list
    std::vector<int> nums = {5, 3, 9, 1, 7, 2};

    // Variables to store maximum and minimum elements
    int maxElement, minElement;

    // Find maximum and minimum elements
    findMaxMin(nums, maxElement, minElement);

    // Output the results
    std::cout << "Maximum element: " << maxElement << std::endl;
    std::cout << "Minimum element: " << minElement << std::endl;

    return 0;
}
```

In this code:

- `findMaxMin` function takes a `std::vector<int>` representing the list of numbers, and two integer references `maxElement` and `minElement` to store the maximum and minimum elements found.
- We initialize `maxElement` to the minimum possible integer value and `minElement` to the maximum possible integer value.
- We then iterate through the list, updating `maxElement` and `minElement` accordingly.
- Finally, in the `main` function, we call `findMaxMin` with our sample list, and print out the results.

### 1. Algorithms & Data Structures (C++): List: Max Profit

Sure, let's create a C++ function to find the maximum profit that can be obtained by buying and selling a stock given its price on different days. We can solve this problem using a simple algorithm that iterates through the prices and keeps track of the minimum price seen so far and the maximum profit that can be obtained.

Here's the implementation:

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int maxProfit(std::vector<int>& prices) {
    if (prices.empty())
        return 0;
    
    int minPrice = prices[0];
    int maxProfit = 0;
    
    for (int i = 1; i < prices.size(); ++i) {
        maxProfit = std::max(maxProfit, prices[i] - minPrice);
        minPrice = std::min(minPrice, prices[i]);
    }
    
    return maxProfit;
}

int main() {
    // Example usage
    std::vector<int> prices = {7, 1, 5, 3, 6, 4};
    std::cout << "Maximum profit: " << maxProfit(prices) << std::endl;
    return 0;
}
```

This code defines a function `maxProfit` which takes a vector of stock prices and returns the maximum profit that can be obtained by buying and selling the stock once. The `main()` function provides an example of how to use this function with a vector of prices.

The algorithm iterates through the prices, keeping track of the minimum price seen so far (`minPrice`) and updating the maximum profit (`maxProfit`) if a higher profit can be obtained by selling at the current price. Finally, it returns the maximum profit.

### 1. Algorithms & Data Structures (C++): List: Max Sub Array

The maximum subarray problem is a classic problem in computer science and is often used to illustrate various algorithmic techniques, such as dynamic programming or the divide and conquer approach. Here's a simple implementation of finding the maximum subarray sum using Kadane's algorithm, which is an efficient dynamic programming approach:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int maxSubArray(vector<int>& nums) {
    int maxSum = nums[0];
    int currentSum = nums[0];
    
    for (int i = 1; i < nums.size(); ++i) {
        currentSum = max(nums[i], currentSum + nums[i]);
        maxSum = max(maxSum, currentSum);
    }
    
    return maxSum;
}

int main() {
    vector<int> nums = {-2, 1, -3, 4, -1, 2, 1, -5, 4};
    cout << "Maximum subarray sum: " << maxSubArray(nums) << endl;
    return 0;
}
```

This code finds the maximum sum of a contiguous subarray within the input array `nums`. The time complexity of this algorithm is O(n), where n is the size of the input array.

### 1. Algorithms & Data Structures (C++): List: Remove Duplicates

To remove duplicates from a list in C++, you can use various approaches. One common method is to use a set to keep track of elements you've seen so far. Here's a sample implementation:

```cpp
#include <iostream>
#include <list>
#include <unordered_set>

template <typename T>
void removeDuplicates(std::list<T>& lst) {
    std::unordered_set<T> seen;
    auto it = lst.begin();
    while (it != lst.end()) {
        if (seen.find(*it) != seen.end()) {
            it = lst.erase(it);
        } else {
            seen.insert(*it);
            ++it;
        }
    }
}

int main() {
    std::list<int> myList = {1, 2, 3, 2, 4, 5, 3, 6, 7, 4};
    
    std::cout << "Original List: ";
    for (const auto& item : myList) {
        std::cout << item << " ";
    }
    std::cout << std::endl;
    
    removeDuplicates(myList);
    
    std::cout << "List after removing duplicates: ";
    for (const auto& item : myList) {
        std::cout << item << " ";
    }
    std::cout << std::endl;
    
    return 0;
}
```

This code defines a function `removeDuplicates` that takes a list by reference and removes duplicates using an unordered set to track elements that have been seen. Then, in the `main` function, it demonstrates how to use this function by creating a list of integers, removing duplicates, and printing the result.

### 1. Algorithms & Data Structures (C++): List: Remove Element

To remove an element from a list in C++, you have several options depending on the specific requirements and constraints of your program. One common approach is to use the `std::list` container provided by the C++ Standard Library. Here's how you can remove an element from a `std::list`:

```cpp
#include <iostream>
#include <list>

int main() {
    std::list<int> myList = {1, 2, 3, 4, 5};

    // Remove element with value 3
    myList.remove(3);

    // Print the modified list
    for (int elem : myList) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this example, the `remove()` member function of `std::list` is used to remove all elements with the specified value from the list.

If you need more control over the removal process, or if you're implementing your own linked list data structure, you'll need to manually traverse the list to find the element to remove and then adjust the pointers accordingly. Here's a basic example of how you might do this:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* next;
    
    Node(int value) : data(value), next(nullptr) {}
};

void removeElement(Node*& head, int value) {
    Node* current = head;
    Node* prev = nullptr;

    // Traverse the list to find the element
    while (current != nullptr && current->data != value) {
        prev = current;
        current = current->next;
    }

    // If element found, remove it
    if (current != nullptr) {
        if (prev == nullptr) {
            // If the element to be removed is the head
            head = current->next;
        } else {
            prev->next = current->next;
        }
        delete current;
    }
}

void printList(Node* head) {
    Node* current = head;
    while (current != nullptr) {
        std::cout << current->data << " ";
        current = current->next;
    }
    std::cout << std::endl;
}

int main() {
    // Creating a sample linked list: 1 -> 2 -> 3 -> 4 -> 5
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->next = new Node(3);
    head->next->next->next = new Node(4);
    head->next->next->next->next = new Node(5);

    // Removing element with value 3
    removeElement(head, 3);

    // Printing the modified list
    printList(head);

    // Freeing memory
    Node* current = head;
    while (current != nullptr) {
        Node* next = current->next;
        delete current;
        current = next;
    }

    return 0;
}
```

This code defines a simple linked list data structure and a function `removeElement()` to remove a specified value from the list.

### 1. Algorithms & Data Structures (C++): List: Rotate

Rotating a list in C++ involves shifting its elements by a certain number of positions. There are multiple ways to implement this operation, but let's discuss a simple approach using an array-based list. Here's a basic implementation of a function to rotate a list:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to rotate a list to the left by 'shift' positions
void rotateList(vector<int>& arr, int shift) {
    int n = arr.size();
    if (n == 0) return; // Empty list

    shift = shift % n; // Handle shifts larger than the list size

    if (shift < 0) {
        shift += n; // Convert negative shift to positive
    }

    // Reverse the first part of the list (0 to shift-1)
    reverse(arr.begin(), arr.begin() + shift);

    // Reverse the second part of the list (shift to n-1)
    reverse(arr.begin() + shift, arr.end());

    // Reverse the entire list
    reverse(arr.begin(), arr.end());
}

// Function to display a list
void displayList(const vector<int>& arr) {
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;
}

int main() {
    vector<int> myList = {1, 2, 3, 4, 5};

    cout << "Original List: ";
    displayList(myList);

    int shiftAmount = 2; // Number of positions to rotate
    rotateList(myList, shiftAmount);

    cout << "List after rotating left by " << shiftAmount << " positions: ";
    displayList(myList);

    return 0;
}
```

This implementation rotates the list to the left by a specified number of positions. It utilizes the `reverse()` function from the `<algorithm>` header to reverse different parts of the list.

Remember to include necessary headers (`iostream`, `<vector>`, and `<algorithm>`) at the beginning of your program. This implementation assumes that you're using a vector to represent your list. If you're using a different data structure, you'll need to adjust the implementation accordingly.

### 1. Algorithms & Data Structures (C++): Lists

Certainly! Lists are fundamental data structures in computer science that store a collection of items, where each item holds a relative position with respect to the others. In C++, lists can be implemented in various ways, each with its own advantages and disadvantages. Here's a brief overview of some common types of lists and their implementations in C++:

1. **Array-based Lists:**
   - **Vector**: The `std::vector` in C++ is a dynamic array that can resize itself automatically when needed. It provides constant time access to elements and amortized constant time insertion at the end.

   ```cpp
   #include <vector>
   std::vector<int> myVector;
   ```

2. **Linked Lists:**
   - **Singly Linked List**: Each element in the list contains a reference to the next element in the sequence.

   ```cpp
   struct Node {
       int data;
       Node* next;
   };
   ```

   - **Doubly Linked List**: Each element contains references to both the next and previous elements.

   ```cpp
   struct Node {
       int data;
       Node* prev;
       Node* next;
   };
   ```

3. **Forward List**:
   - `std::forward_list` is a singly linked list provided by the C++ standard library. It allows forward traversal only (from beginning to end) and does not support bidirectional traversal like the doubly linked list.

   ```cpp
   #include <forward_list>
   std::forward_list<int> myForwardList;
   ```

4. **Circular Linked List**:
   - In this list, the last node points back to the first node, forming a circle.

   ```cpp
   struct Node {
       int data;
       Node* next;
   };
   ```

5. **Other Implementations**:
   - Apart from the standard implementations, you can create your own custom implementations of lists based on the specific requirements of your application.

Each type of list has its own advantages and use cases. For example, arrays (like vectors) provide fast access to elements through indexing but may be inefficient for insertions and deletions at arbitrary positions. Linked lists, on the other hand, allow efficient insertions and deletions anywhere in the list but may have slower access times.

When choosing a list implementation, it's essential to consider the operations you'll perform most frequently and the performance characteristics of each implementation with respect to those operations.

### 1. Algorithms & Data Structures (C++): Merge 2 sorted List

Certainly! Merging two sorted lists is a fundamental operation in algorithms and data structures. Here's a C++ implementation of merging two sorted lists:

```cpp
#include <iostream>
#include <vector>

using namespace std;

vector<int> mergeSortedLists(const vector<int>& list1, const vector<int>& list2) {
    vector<int> mergedList;
    int i = 0, j = 0;

    // Compare elements from both lists and insert them into the merged list
    while (i < list1.size() && j < list2.size()) {
        if (list1[i] < list2[j]) {
            mergedList.push_back(list1[i]);
            i++;
        } else {
            mergedList.push_back(list2[j]);
            j++;
        }
    }

    // Insert remaining elements from list1, if any
    while (i < list1.size()) {
        mergedList.push_back(list1[i]);
        i++;
    }

    // Insert remaining elements from list2, if any
    while (j < list2.size()) {
        mergedList.push_back(list2[j]);
        j++;
    }

    return mergedList;
}

int main() {
    // Example usage
    vector<int> list1 = {1, 3, 5, 7, 9};
    vector<int> list2 = {2, 4, 6, 8, 10};

    vector<int> mergedList = mergeSortedLists(list1, list2);

    // Print the merged list
    cout << "Merged List: ";
    for (int num : mergedList) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}
```

In this code:

- We define a function `mergeSortedLists` that takes two sorted lists (`list1` and `list2`) as input and returns a new sorted list which is a result of merging `list1` and `list2`.
- We initialize two pointers `i` and `j` to iterate over `list1` and `list2` respectively.
- We compare elements at these pointers from both lists and insert the smaller one into the `mergedList`, advancing the respective pointer.
- We repeat this process until we have iterated over all elements in both lists.
- Finally, we append any remaining elements from `list1` or `list2` to the `mergedList`.
- In the `main` function, we provide example usage by merging two predefined sorted lists and printing the result.

### 1. Algorithms & Data Structures (C++): Merge 2 sorted List (Recursive)

Sure, here's a C++ implementation of merging two sorted lists recursively:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if (l1 == nullptr)
            return l2;
        if (l2 == nullptr)
            return l1;
        
        if (l1->val < l2->val) {
            l1->next = mergeTwoLists(l1->next, l2);
            return l1;
        } else {
            l2->next = mergeTwoLists(l1, l2->next);
            return l2;
        }
    }
};

// Utility function to print the list
void printList(ListNode* head) {
    while (head) {
        cout << head->val << " ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    Solution solution;

    // Example lists
    ListNode* l1 = new ListNode(1);
    l1->next = new ListNode(3);
    l1->next->next = new ListNode(5);

    ListNode* l2 = new ListNode(2);
    l2->next = new ListNode(4);
    l2->next->next = new ListNode(6);

    cout << "List 1: ";
    printList(l1);
    cout << "List 2: ";
    printList(l2);

    ListNode* mergedList = solution.mergeTwoLists(l1, l2);
    cout << "Merged List: ";
    printList(mergedList);

    return 0;
}
```

This code defines a `ListNode` struct for representing each node in the linked list, a `Solution` class with a method `mergeTwoLists` that recursively merges two sorted linked lists, and a `main` function to demonstrate its usage.

### 1. Algorithms & Data Structures (C++): Merge 2 Sorted Lists

Certainly! Merging two sorted lists in C++ is a common operation in programming. You can accomplish this task efficiently using pointers to iterate through the lists. Here's a simple implementation:

```cpp
#include <iostream>

using namespace std;

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    ListNode dummy(0); // dummy node to simplify code
    ListNode* tail = &dummy;

    while (l1 && l2) {
        if (l1->val <= l2->val) {
            tail->next = l1;
            l1 = l1->next;
        } else {
            tail->next = l2;
            l2 = l2->next;
        }
        tail = tail->next;
    }

    // Append remaining elements of l1 or l2 (if any)
    tail->next = l1 ? l1 : l2;

    return dummy.next;
}

// Utility function to print the linked list
void printList(ListNode* head) {
    while (head) {
        cout << head->val << " ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    // Creating example lists
    ListNode* l1 = new ListNode(1);
    l1->next = new ListNode(3);
    l1->next->next = new ListNode(5);

    ListNode* l2 = new ListNode(2);
    l2->next = new ListNode(4);
    l2->next->next = new ListNode(6);

    cout << "List 1: ";
    printList(l1);
    cout << "List 2: ";
    printList(l2);

    // Merging lists
    ListNode* mergedList = mergeTwoLists(l1, l2);

    cout << "Merged List: ";
    printList(mergedList);

    // Clean up
    delete l1;
    delete l2;

    // Free memory for merged list
    ListNode* temp;
    while (mergedList) {
        temp = mergedList;
        mergedList = mergedList->next;
        delete temp;
    }

    return 0;
}
```

This code defines a structure for a singly-linked list node, and then implements the `mergeTwoLists` function which merges two sorted lists into a single sorted list. The `main` function demonstrates how to use this function with example lists. Finally, it includes a utility function `printList` to print the merged list.

### 1. Algorithms & Data Structures (C++): Remove nth Node from end of list

Certainly! Removing the nth node from the end of a singly linked list involves a two-pass algorithm in which you first find the length of the list, and then traverse it again to find the node to remove. However, you can optimize this process into a one-pass algorithm using two pointers.

Here's how you can implement it in C++:

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
    // Create a dummy node to handle edge cases like removing the first node
    ListNode* dummy = new ListNode(0);
    dummy->next = head;
    
    // Initialize two pointers, first and second, both pointing to dummy node
    ListNode* first = dummy;
    ListNode* second = dummy;
    
    // Move the second pointer n+1 steps forward
    for (int i = 0; i <= n; i++) {
        second = second->next;
    }
    
    // Move both pointers until second reaches the end of the list
    while (second != NULL) {
        first = first->next;
        second = second->next;
    }
    
    // Now, first points to the (n-1)th node from the end
    // Remove the nth node from the end
    ListNode* temp = first->next;
    first->next = first->next->next;
    delete temp;
    
    return dummy->next; // Return the modified head
}

// Utility function to print the linked list
void printList(ListNode* head) {
    ListNode* temp = head;
    while (temp != NULL) {
        cout << temp->val << " ";
        temp = temp->next;
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

    cout << "Original list: ";
    printList(head);

    int n = 2;
    head = removeNthFromEnd(head, n);

    cout << "List after removing " << n << "th node from end: ";
    printList(head);

    // Free memory
    while (head != NULL) {
        ListNode* temp = head;
        head = head->next;
        delete temp;
    }

    return 0;
}
```

This implementation runs in a single pass through the list, making it more efficient than the two-pass approach.

### 1. Algorithms & Data Structures (C++): Removing the Lowest Number Appearing in Two Lists from the Lists

To remove the lowest number appearing in two lists in C++, you can follow these steps:

1. Find the minimum number in both lists.
2. Remove the first occurrence of the minimum number from both lists.

Here's a sample implementation:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

// Function to remove the first occurrence of a number from a vector
void removeNumber(std::vector<int>& vec, int num) {
    auto it = std::find(vec.begin(), vec.end(), num);
    if (it != vec.end()) {
        vec.erase(it);
    }
}

// Function to remove the lowest number appearing in two lists
void removeLowestInTwoLists(std::vector<int>& list1, std::vector<int>& list2) {
    // Find the minimum number in list1
    int minNum1 = *std::min_element(list1.begin(), list1.end());
    
    // Find the minimum number in list2
    int minNum2 = *std::min_element(list2.begin(), list2.end());
    
    // Find the overall minimum number
    int minNum = std::min(minNum1, minNum2);
    
    // Remove the minimum number from both lists
    removeNumber(list1, minNum);
    removeNumber(list2, minNum);
}

int main() {
    std::vector<int> list1 = {5, 3, 7, 2, 9};
    std::vector<int> list2 = {4, 1, 2, 8, 6};
    
    std::cout << "Original lists:\n";
    std::cout << "List 1: ";
    for (int num : list1) {
        std::cout << num << " ";
    }
    std::cout << "\nList 2: ";
    for (int num : list2) {
        std::cout << num << " ";
    }
    
    removeLowestInTwoLists(list1, list2);
    
    std::cout << "\n\nLists after removing the lowest number appearing in both lists:\n";
    std::cout << "List 1: ";
    for (int num : list1) {
        std::cout << num << " ";
    }
    std::cout << "\nList 2: ";
    for (int num : list2) {
        std::cout << num << " ";
    }
    
    return 0;
}
```

This code finds the minimum number in each list using `std::min_element`, then removes the lowest number from both lists using the `removeNumber` function. Finally, it displays the lists before and after the removal.

### 1. Algorithms & Data Structures (C++): Reorder List

Reordering a singly linked list in C++ can be achieved by dividing the list into two halves, reversing the second half, and then merging the two halves alternatively. Below is a C++ implementation of the reorder list algorithm:

```cpp
#include <iostream>

using namespace std;

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

class Solution {
public:
    void reorderList(ListNode* head) {
        if (!head || !head->next) return;

        // Step 1: Find the middle of the list
        ListNode *slow = head, *fast = head;
        while (fast->next && fast->next->next) {
            slow = slow->next;
            fast = fast->next->next;
        }

        // Step 2: Reverse the second half of the list
        ListNode *prev = nullptr, *curr = slow->next, *temp;
        slow->next = nullptr;
        while (curr) {
            temp = curr->next;
            curr->next = prev;
            prev = curr;
            curr = temp;
        }

        // Step 3: Merge the two halves alternatively
        ListNode *first = head, *second = prev;
        while (second) {
            ListNode *temp1 = first->next;
            ListNode *temp2 = second->next;
            first->next = second;
            second->next = temp1;
            first = temp1;
            second = temp2;
        }
    }
};

// Utility function to print the linked list
void printList(ListNode* head) {
    while (head) {
        cout << head->val << " ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    ListNode *head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);

    cout << "Original list: ";
    printList(head);

    Solution sol;
    sol.reorderList(head);

    cout << "Reordered list: ";
    printList(head);

    return 0;
}
```

This program defines a `ListNode` structure for a singly-linked list and a `Solution` class with the `reorderList()` function that reorders the list according to the algorithm described above. The `main()` function creates a sample linked list, calls the `reorderList()` function, and then prints the original and reordered lists.

### 1. Algorithms & Data Structures (C++): Reverse a List

Sure! In C++, you can reverse a list using various approaches. One simple approach is to iterate through the list and swap elements from the beginning and end until you reach the middle of the list. Here's how you can implement this:

```cpp
#include <iostream>
#include <list>

using namespace std;

// Function to reverse a list
void reverseList(list<int>& lst) {
    auto start = lst.begin();
    auto end = prev(lst.end());

    while (start != end && start != next(end)) {
        // Swap elements
        swap(*start, *end);
        // Move iterators
        start++;
        end--;
    }
}

int main() {
    list<int> myList = {1, 2, 3, 4, 5};

    cout << "Original list: ";
    for (const auto& elem : myList) {
        cout << elem << " ";
    }
    cout << endl;

    reverseList(myList);

    cout << "Reversed list: ";
    for (const auto& elem : myList) {
        cout << elem << " ";
    }
    cout << endl;

    return 0;
}
```

This code defines a function `reverseList` that takes a list by reference and reverses it in place. The `main` function demonstrates how to use this function by creating a list of integers, printing it, reversing it, and printing the reversed list.

### 1. Algorithms & Data Structures (C++): Sort List

Sorting a list in C++ can be done using various algorithms. One of the most commonly used algorithms is the Merge Sort due to its efficiency and stability. Here's a simple implementation of sorting a list using Merge Sort:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Merge two sorted subarrays [left, mid] and [mid+1, right]
void merge(vector<int>& arr, int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;

    // Create temp arrays
    vector<int> L(n1), R(n2);

    // Copy data to temp arrays L[] and R[]
    for (int i = 0; i < n1; i++)
        L[i] = arr[left + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[mid + 1 + j];

    // Merge the temp arrays back into arr[left, right]
    int i = 0; // Initial index of first subarray
    int j = 0; // Initial index of second subarray
    int k = left; // Initial index of merged subarray

    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        } else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }

    // Copy the remaining elements of L[], if there are any
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    // Copy the remaining elements of R[], if there are any
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

// Merge sort function
void mergeSort(vector<int>& arr, int left, int right) {
    if (left < right) {
        // Find the middle point
        int mid = left + (right - left) / 2;

        // Sort first and second halves
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);

        // Merge the sorted halves
        merge(arr, left, mid, right);
    }
}

// Function to print the sorted array
void printArray(const vector<int>& arr) {
    for (int i : arr)
        cout << i << " ";
    cout << endl;
}

int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    int n = arr.size();

    cout << "Original array:" << endl;
    printArray(arr);

    mergeSort(arr, 0, n - 1);

    cout << "Sorted array:" << endl;
    printArray(arr);

    return 0;
}
```

In this implementation, the `mergeSort` function recursively divides the array into halves until each subarray contains only one element. Then, the `merge` function is called to merge the sorted subarrays into a single sorted array.

You can replace the vector `arr` with any list of integers you want to sort.
