### 1. Algorithms & Data Structures (C++): Average Case Analysis of Binary Search

Analyzing the average case of binary search involves understanding the probability distribution of the search key in the sorted array. In a typical scenario, we assume that the search key is equally likely to be any element of the array. Let's denote the length of the array as \( n \).

1. **Step-by-step Analysis:**

    - In each step of the binary search, we halve the search space.
    - At each step, we choose the middle element of the remaining array to compare with the search key.
    - If the search key matches the middle element, the search terminates successfully.
    - Otherwise, we discard half of the remaining elements based on the comparison.

2. **Probability of Key Being in a Subarray:**

    - For binary search to be successful, the key must lie within the subarray we're currently searching.
    - Suppose we're searching in a subarray of length \( m \).
    - The probability that the key is in this subarray is \( \frac{1}{m} \), assuming the key is equally likely to be any element.

3. **Number of Comparisons:**

    - Let \( X \) be the random variable representing the number of comparisons needed for a successful search.
    - \( X = 1 \) if the key is at the middle of the array.
    - \( X = 2 \) if the key is in one of the two remaining halves.
    - In general, \( X = \lceil \log_2 n \rceil \) where \( n \) is the length of the array.

4. **Average Case Analysis:**

    - To find the average number of comparisons, we compute the expected value of \( X \).
    - \( E[X] = \sum_{m=1}^{n} \left( \frac{1}{m} \times m \right) = \sum_{m=1}^{n} 1 = n \).

So, the average case time complexity of binary search is \( O(n) \).

However, it's important to note that in practical scenarios, binary search's average case behavior is often considered \( O(\log n) \), because typically, the elements in the array are uniformly distributed, and on average, the search space reduces by half in each step. This discrepancy arises because the average number of comparisons is not the same as the time complexity. The average number of comparisons is \( O(n) \), but the time complexity, considering the number of elements that need to be accessed, is \( O(\log n) \).

### 1. Algorithms & Data Structures (C++): 4 Pointers Technique

The "4 Pointers Technique" is a strategy often employed in certain algorithms and data structures problems, particularly in the context of linked lists or trees. It involves using four pointers to traverse and manipulate the structure efficiently. Here's a brief overview of how it works:

1. **Two Pointers for Iteration**: These two pointers are typically used to traverse through the data structure simultaneously. For example, in a linked list, you might have one pointer (let's call it `slow_ptr`) moving one node at a time, and another pointer (let's call it `fast_ptr`) moving two nodes at a time. This can be useful in algorithms like detecting cycles in a linked list (Floyd's Cycle Detection Algorithm) or finding the middle element of a linked list.

2. **Two Pointers for Manipulation or State Tracking**: These pointers are used for various purposes like maintaining state, reversing elements, or breaking and reconnecting links in the data structure. For example, in problems involving reversing a linked list in parts, you might use two pointers to mark the start and end of the portion to be reversed.

Here's a simple example in C++ demonstrating how the 4 pointers technique can be used to find the middle of a linked list:

```cpp
#include <iostream>

struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* findMiddle(ListNode* head) {
    if (!head) return nullptr;

    ListNode *slow_ptr = head;
    ListNode *fast_ptr = head;

    while (fast_ptr && fast_ptr->next) {
        slow_ptr = slow_ptr->next;
        fast_ptr = fast_ptr->next->next;
    }

    return slow_ptr;
}

int main() {
    // Example usage
    ListNode *head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);

    ListNode *middle = findMiddle(head);
    if (middle)
        std::cout << "Middle element: " << middle->val << std::endl;
    else
        std::cout << "List is empty" << std::endl;

    return 0;
}
```

In this example, `slow_ptr` moves one step at a time while `fast_ptr` moves two steps at a time. When `fast_ptr` reaches the end of the list, `slow_ptr` will be at the middle node.

### 1. Algorithms & Data Structures (C++): Advanced Binary Search

Advanced binary search techniques can optimize searching in sorted arrays and can be useful in various scenarios. Here are a few advanced techniques in C++ for binary search:

1. **First Occurrence of an Element**: To find the first occurrence of an element in a sorted array, you can modify the binary search algorithm slightly. Once you find the element, instead of returning, continue searching towards the left to ensure you find the first occurrence.

```cpp
int firstOccurrence(vector<int>& arr, int target) {
    int left = 0, right = arr.size() - 1, result = -1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) {
            result = mid;
            right = mid - 1; // Continue searching towards left
        } else if (arr[mid] < target)
            left = mid + 1;
        else
            right = mid - 1;
    }
    return result;
}
```

1. **Last Occurrence of an Element**: Similar to finding the first occurrence, but this time, continue searching towards the right once you find the element.

```cpp
int lastOccurrence(vector<int>& arr, int target) {
    int left = 0, right = arr.size() - 1, result = -1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) {
            result = mid;
            left = mid + 1; // Continue searching towards right
        } else if (arr[mid] < target)
            left = mid + 1;
        else
            right = mid - 1;
    }
    return result;
}
```

1. **Count Occurrences of an Element**: Using the first and last occurrence techniques, you can easily count the occurrences of an element.

```cpp
int countOccurrences(vector<int>& arr, int target) {
    int first = firstOccurrence(arr, target);
    int last = lastOccurrence(arr, target);
    if (first == -1 || last == -1) return 0;
    return last - first + 1;
}
```

These advanced techniques improve the efficiency of binary search in specific scenarios, especially when dealing with sorted arrays with duplicate elements. Always ensure that the array is sorted before applying these techniques.

### 1. Algorithms & Data Structures (C++): Advanced Binary Search : Find Minimum Element in Sorted Rotated Array

To find the minimum element in a sorted rotated array using a binary search approach, you can use the following C++ code:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int findMin(vector<int>& nums) {
    int left = 0, right = nums.size() - 1;

    while (left < right) {
        int mid = left + (right - left) / 2;

        // If mid element is greater than the last element, then the minimum element lies to the right of mid.
        if (nums[mid] > nums[right]) {
            left = mid + 1;
        }
        // If mid element is less than the last element, then the minimum element lies to the left of or is equal to mid.
        else if (nums[mid] < nums[right]) {
            right = mid;
        }
        // If mid element is same as the last element, move the right pointer to the left.
        else {
            right--;
        }
    }

    // At the end of the loop, left will point to the minimum element.
    return nums[left];
}

int main() {
    vector<int> nums = {4, 5, 6, 7, 0, 1, 2};
    cout << "Minimum element: " << findMin(nums) << endl;

    return 0;
}
```

In this code:

- We initialize two pointers, `left` and `right`, which represent the start and end of the array respectively.
- We then use a while loop to perform binary search.
- Inside the loop, we calculate the mid index.
- We compare the element at the mid index with the element at the right index.
- If the element at mid is greater than the element at right, it means the minimum element lies to the right of mid, so we update the `left` pointer to `mid + 1`.
- If the element at mid is less than the element at right, it means the minimum element lies to the left of or is equal to mid, so we update the `right` pointer to `mid`.
- If the element at mid is equal to the element at right, we move the `right` pointer one step to the left (`right--`).
- Eventually, `left` will point to the minimum element, and we return `nums[left]`.

This algorithm has a time complexity of O(log N), where N is the number of elements in the array.

### 1. Algorithms & Data Structures (C++): Advanced Binary Search : Implement Square root

Certainly! Implementing square root using binary search in C++ is an interesting problem. Here's a simple implementation:

```cpp
#include <iostream>

double squareRoot(double x, double precision = 0.0001) {
    if (x == 0 || x == 1) // Square root of 0 or 1 is the number itself
        return x;

    double low = 0;
    double high = x;
    double mid, sqr;

    while (high - low > precision) {
        mid = low + (high - low) / 2;
        sqr = mid * mid;

        if (sqr == x)
            return mid;
        else if (sqr < x)
            low = mid;
        else
            high = mid;
    }

    return low + (high - low) / 2;
}

int main() {
    double num;
    std::cout << "Enter a number to find its square root: ";
    std::cin >> num;
    
    if (num < 0) {
        std::cout << "Square root of a negative number is not defined." << std::endl;
    } else {
        std::cout << "Square root of " << num << " is approximately " << squareRoot(num) << std::endl;
    }

    return 0;
}
```

This code defines a `squareRoot` function that takes a number `x` and an optional precision parameter (defaulting to `0.0001`). It then performs a binary search to find the square root of the number within the given precision. Finally, it has a `main` function to take input from the user and display the result.

This implementation will converge to the square root of the input number with the specified precision. You can adjust the precision according to your requirements.

### 1. Algorithms & Data Structures (C++): Algorithm for evaluating Postfix expression

Sure! Evaluating a postfix expression involves scanning the expression from left to right and performing operations on operands based on the encountered operators. Here's an algorithm to evaluate a postfix expression in C++:

```cpp
#include <iostream>
#include <stack>
#include <string>

using namespace std;

// Function to evaluate postfix expression
int evaluatePostfix(const string& expression) {
    stack<int> operandStack;

    // Iterate through each character in the expression
    for (char c : expression) {
        // If current character is an operand, push it onto the stack
        if (isdigit(c)) {
            operandStack.push(c - '0'); // Convert char to int
        } else {
            // If current character is an operator, pop two operands from stack
            int operand2 = operandStack.top();
            operandStack.pop();
            int operand1 = operandStack.top();
            operandStack.pop();

            // Perform operation based on current operator
            switch (c) {
                case '+':
                    operandStack.push(operand1 + operand2);
                    break;
                case '-':
                    operandStack.push(operand1 - operand2);
                    break;
                case '*':
                    operandStack.push(operand1 * operand2);
                    break;
                case '/':
                    operandStack.push(operand1 / operand2);
                    break;
            }
        }
    }

    // Result will be the only element left on the stack
    return operandStack.top();
}

int main() {
    string expression = "235*+"; // Example postfix expression: 2 + (3 * 5)
    cout << "Result: " << evaluatePostfix(expression) << endl;
    return 0;
}
```

This algorithm first initializes an empty stack to store operands. It then iterates through each character in the postfix expression. If the current character is an operand (a digit), it's pushed onto the stack. If it's an operator, two operands are popped from the stack, the operation is performed, and the result is pushed back onto the stack. Finally, the result of the expression is the only element left on the stack.

### 1. Algorithms & Data Structures (C++): Algorithms: Searching

Certainly! Searching algorithms are a fundamental part of computer science and play a crucial role in various applications. Here's an overview of some common searching algorithms in C++:

1. **Linear Search**:
   - It sequentially checks each element of the data structure until the desired element is found or all the elements have been checked.
   - It has a time complexity of O(n) in the worst case.

```cpp
#include <iostream>
using namespace std;

int linearSearch(int arr[], int n, int key) {
    for (int i = 0; i < n; ++i) {
        if (arr[i] == key)
            return i; // Element found, return its index
    }
    return -1; // Element not found
}

int main() {
    int arr[] = {5, 2, 8, 10, 3};
    int n = sizeof(arr) / sizeof(arr[0]);
    int key = 8;
    int index = linearSearch(arr, n, key);
    if (index != -1)
        cout << "Element found at index: " << index << endl;
    else
        cout << "Element not found" << endl;
    return 0;
}
```

1. **Binary Search** (for sorted arrays):
   - It works by repeatedly dividing the search interval in half until the target element is found.
   - It has a time complexity of O(log n) in the worst case.

```cpp
#include <iostream>
using namespace std;

int binarySearch(int arr[], int l, int r, int key) {
    while (l <= r) {
        int mid = l + (r - l) / 2;
        if (arr[mid] == key)
            return mid; // Element found, return its index
        if (arr[mid] < key)
            l = mid + 1; // Discard left half
        else
            r = mid - 1; // Discard right half
    }
    return -1; // Element not found
}

int main() {
    int arr[] = {2, 3, 5, 8, 10};
    int n = sizeof(arr) / sizeof(arr[0]);
    int key = 8;
    int index = binarySearch(arr, 0, n - 1, key);
    if (index != -1)
        cout << "Element found at index: " << index << endl;
    else
        cout << "Element not found" << endl;
    return 0;
}
```

These are just two of the many searching algorithms available. Depending on the context and constraints of your problem, you might need to choose a different algorithm.

### 1. Algorithms & Data Structures (C++): Analayis of Binary Search

Binary search is a fundamental algorithm in computer science used to efficiently locate a target value within a sorted array. Its time complexity is O(log n), where n is the number of elements in the array. Let's break down the algorithm and analyze its key aspects:

1. **Input**: Binary search requires a sorted array as input. This is crucial for the algorithm to work correctly.

2. **Divide and Conquer**: Binary search follows a divide and conquer approach. It repeatedly divides the search interval in half until the target value is found or the interval becomes empty.

3. **Midpoint Calculation**: At each step, binary search calculates the midpoint of the current search interval. This is typically done by taking the average of the low and high indices: `mid = (low + high) / 2`. Alternatively, to avoid potential overflow, `mid = low + (high - low) / 2` can be used.

4. **Comparison with Target**: After calculating the midpoint, binary search compares the value at the midpoint with the target value. If they are equal, the algorithm terminates, and the index of the target value is returned. If the target value is less than the value at the midpoint, the search continues in the lower half of the array. Otherwise, the search continues in the upper half.

5. **Recursive or Iterative Implementation**: Binary search can be implemented recursively or iteratively. The recursive implementation typically has a clearer and more concise structure, while the iterative implementation may be more efficient in terms of space due to avoiding function call overhead.

6. **Termination**: Binary search terminates when the search interval is empty (indicating that the target value is not present in the array) or when the target value is found.

7. **Time Complexity**: Binary search has a time complexity of O(log n), where n is the number of elements in the array. This is because the search interval is halved in each step, leading to a logarithmic time complexity.

8. **Space Complexity**: Binary search has a space complexity of O(1) for the iterative implementation and O(log n) for the recursive implementation due to the function call stack.

9. **Edge Cases**: Binary search should handle edge cases such as empty arrays or arrays with only one element gracefully.

10. **Precondition**: It's important to ensure that the input array is sorted before applying binary search. If the array is not sorted, the algorithm may not produce correct results.

In summary, binary search is a powerful and efficient algorithm for searching for a target value in a sorted array. Its logarithmic time complexity makes it particularly useful for large datasets where efficiency is crucial. However, it requires the input array to be sorted, and careful implementation is necessary to handle all edge cases correctly.

### 1. Algorithms & Data Structures (C++): Analysis of Binary Search

Binary search is a fundamental algorithm for searching in a sorted array or list. It follows a divide-and-conquer approach to efficiently find the position of a target value within the array.

Here's a breakdown of the analysis of binary search:

#### Time Complexity

- **Best Case:** O(1) - This occurs when the target element is found at the middle of the array in the first comparison.
- **Worst Case:** O(log n) - This happens when the target element is not present in the array, and the search divides the array into halves until it reaches a single element or an empty subarray.
- **Average Case:** O(log n) - On average, binary search will divide the array in half for each comparison until the target element is found or determined to be absent.

#### Space Complexity

Binary search typically has a space complexity of O(1) because it doesn't require any extra space proportional to the size of the input array. It performs the search iteratively or recursively without using additional data structures.

#### Key Points

- Binary search is efficient for large datasets because it eliminates half of the remaining elements in each step.
- It requires the array to be sorted initially, which might require additional preprocessing time if the array isn't sorted.
- It's important to ensure that the array remains sorted if it's being modified after sorting, otherwise binary search may give incorrect results.
- Binary search can be implemented iteratively or recursively. The choice between them doesn't affect the time complexity but may affect the space complexity and readability of the code.

#### Limitations

- Binary search requires the array to be sorted, which might not always be feasible or efficient.
- It's not suitable for dynamic datasets that frequently change, as resorting the array after every modification can be costly.
- Binary search doesn't work on unsorted arrays and is not applicable to linked lists directly.

#### Example Code (Iterative Implementation in C++)

```cpp
#include <iostream>
#include <vector>

int binarySearch(const std::vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (arr[mid] == target)
            return mid;

        if (arr[mid] < target)
            left = mid + 1;
        else
            right = mid - 1;
    }

    return -1; // Target not found
}

int main() {
    std::vector<int> arr = {1, 3, 5, 7, 9, 11, 13, 15};
    int target = 7;
    int index = binarySearch(arr, target);
    if (index != -1)
        std::cout << "Element found at index " << index << std::endl;
    else
        std::cout << "Element not found" << std::endl;
    return 0;
}
```

This code snippet demonstrates an iterative binary search implementation in C++. It searches for a target element within a sorted vector and returns its index if found, otherwise, it returns -1.

### 1. Algorithms & Data Structures (C++): Binary Search

Binary search is a fundamental algorithm used to efficiently locate a target value within a sorted array. It works by repeatedly dividing the search interval in half. Here's how it works in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Binary search function
int binarySearch(vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        // Check if target is present at mid
        if (arr[mid] == target)
            return mid;

        // If target is greater, ignore left half
        if (arr[mid] < target)
            left = mid + 1;
        // If target is smaller, ignore right half
        else
            right = mid - 1;
    }

    // If target is not present in the array
    return -1;
}

// Example usage
int main() {
    vector<int> arr = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int target = 7;
    int index = binarySearch(arr, target);
    if (index != -1)
        cout << "Element found at index " << index << endl;
    else
        cout << "Element not found" << endl;
    return 0;
}
```

In this implementation:

1. We initialize two pointers, `left` and `right`, which represent the current search interval.
2. We repeatedly calculate the middle index (`mid`) of the search interval and compare the element at that index with the target value.
3. If the target value matches the element at `mid`, we return `mid`.
4. If the target value is greater than the element at `mid`, we update `left` to `mid + 1` to search in the right half of the array.
5. If the target value is smaller than the element at `mid`, we update `right` to `mid - 1` to search in the left half of the array.
6. We repeat steps 2-5 until `left` is greater than `right`, which indicates that the target value is not present in the array.

Binary search has a time complexity of O(log n) since it divides the search interval in half with each iteration, making it much more efficient than linear search for large arrays.

### 1. Algorithms & Data Structures (C++): Binary Search : Find First & Last Occurence

Sure, binary search is a widely used algorithm for searching a sorted array efficiently. The basic idea is to repeatedly divide the search interval in half until the value is found or the interval is empty.

Here's how you can modify the basic binary search algorithm to find the first and last occurrences of a given target value in a sorted array:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to find the first occurrence of target in nums
int findFirstOccurrence(vector<int>& nums, int target) {
    int left = 0, right = nums.size() - 1;
    int result = -1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (nums[mid] == target) {
            result = mid;
            right = mid - 1; // Continue searching in the left half
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }

    return result;
}

// Function to find the last occurrence of target in nums
int findLastOccurrence(vector<int>& nums, int target) {
    int left = 0, right = nums.size() - 1;
    int result = -1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (nums[mid] == target) {
            result = mid;
            left = mid + 1; // Continue searching in the right half
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }

    return result;
}

int main() {
    vector<int> nums = {1, 2, 2, 2, 4, 4, 4, 5, 6};
    int target = 4;

    int firstOccurrence = findFirstOccurrence(nums, target);
    int lastOccurrence = findLastOccurrence(nums, target);

    cout << "First occurrence of " << target << " at index: " << firstOccurrence << endl;
    cout << "Last occurrence of " << target << " at index: " << lastOccurrence << endl;

    return 0;
}
```

In the `findFirstOccurrence` function, we search for the target value and keep updating the result whenever we find it. We also adjust the `right` pointer to continue searching in the left half.

In the `findLastOccurrence` function, we similarly search for the target value and keep updating the result whenever we find it. We adjust the `left` pointer to continue searching in the right half.

This way, we can efficiently find both the first and last occurrences of the target value in a sorted array using binary search.

### 1. Algorithms & Data Structures (C++): Binary Search : Search in Rotated Sorted Array

Sure! Searching in a rotated sorted array is a common problem where an array that was originally sorted in ascending order has been rotated at some pivot unknown to you beforehand. Here's how you can implement binary search to find an element in such an array in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int searchInRotatedSortedArray(vector<int>& nums, int target) {
    int left = 0;
    int right = nums.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (nums[mid] == target)
            return mid;

        // Left half is sorted
        if (nums[left] <= nums[mid]) {
            // Check if target lies in the left half
            if (nums[left] <= target && target < nums[mid])
                right = mid - 1;
            else
                left = mid + 1;
        }
        // Right half is sorted
        else {
            // Check if target lies in the right half
            if (nums[mid] < target && target <= nums[right])
                left = mid + 1;
            else
                right = mid - 1;
        }
    }

    // If element is not found
    return -1;
}

int main() {
    vector<int> nums = {4, 5, 6, 7, 0, 1, 2};
    int target = 0;
    int index = searchInRotatedSortedArray(nums, target);
    if (index != -1)
        cout << "Element found at index: " << index << endl;
    else
        cout << "Element not found" << endl;
    return 0;
}
```

In this code:

1. We define a function `searchInRotatedSortedArray` that takes a vector of integers `nums` representing the rotated sorted array and an integer `target` that we want to search for.

2. We initialize two pointers `left` and `right` representing the start and end of the array respectively.

3. We use a while loop to perform binary search until `left` is less than or equal to `right`.

4. Inside the loop, we calculate the middle index `mid`.

5. We check if the middle element is equal to the target. If it is, we return the index of the middle element.

6. If the left half of the array is sorted (i.e., `nums[left] <= nums[mid]`), we check if the target lies within the left half. If it does, we update `right` to `mid - 1`; otherwise, we update `left` to `mid + 1`.

7. If the right half of the array is sorted, we check if the target lies within the right half. If it does, we update `left` to `mid + 1`; otherwise, we update `right` to `mid - 1`.

8. If the element is not found, we return -1.

9. In the `main` function, we create a sample rotated sorted array `nums`, specify the `target` element we want to search for, and call the `searchInRotatedSortedArray` function. We then print the result accordingly.

### 1. Algorithms & Data Structures (C++): Binary Search (Implementation)

Sure, here's a simple implementation of the binary search algorithm in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to perform binary search
int binarySearch(vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        // If the element is present at the middle itself
        if (arr[mid] == target)
            return mid;

        // If the element is smaller than mid, then it can only be present in the left subarray
        if (arr[mid] > target)
            right = mid - 1;

        // Else the element can only be present in the right subarray
        else
            left = mid + 1;
    }

    // If the element is not present in the array
    return -1;
}

int main() {
    vector<int> arr = {2, 5, 8, 12, 16, 23, 38, 56, 72, 91};
    int target = 23;

    int result = binarySearch(arr, target);
    if (result != -1)
        cout << "Element found at index " << result << endl;
    else
        cout << "Element not found in the array" << endl;

    return 0;
}
```

This code defines a `binarySearch` function that takes a sorted vector of integers and a target integer to search for. It returns the index of the target if found, otherwise, it returns -1. The `main` function demonstrates how to use this function by searching for a target integer in a sorted vector.

### 1. Algorithms & Data Structures (C++): Binary Search (Iterative Method)

Sure, here's a simple implementation of the binary search algorithm using the iterative method in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int binarySearch(vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        // Check if target is present at mid
        if (arr[mid] == target) {
            return mid;
        }

        // If target is greater, ignore left half
        if (arr[mid] < target) {
            left = mid + 1;
        }
        // If target is smaller, ignore right half
        else {
            right = mid - 1;
        }
    }

    // If target is not present in array
    return -1;
}

int main() {
    vector<int> arr = {2, 3, 4, 10, 40};
    int target = 10;
    int result = binarySearch(arr, target);
    if (result != -1) {
        cout << "Element found at index " << result << endl;
    } else {
        cout << "Element not found in array" << endl;
    }
    return 0;
}
```

This code defines a function `binarySearch` that takes a sorted vector and a target integer as input, and returns the index of the target if found, or -1 if not found. The main function demonstrates how to use this function with a sample array and target value.

### 1. Algorithms & Data Structures (C++): Binary Search (Theory)

Binary search is a fundamental algorithm used to efficiently locate a target value within a sorted array or list. It follows a divide-and-conquer approach, reducing the search space in half with each iteration. Here's a theoretical overview of how binary search works:

1. **Requirements**: Binary search requires that the elements in the array are sorted in ascending order. This is crucial for the algorithm to function correctly.

2. **Procedure**:
   - Start with defining the range where the target value might exist. Initially, this range is the entire array.
   - Calculate the midpoint of the current range.
   - Compare the target value with the element at the midpoint.
     - If the target value matches the midpoint element, the search is successful, and the index of the midpoint is returned.
     - If the target value is less than the midpoint element, the search continues on the left half of the current range.
     - If the target value is greater than the midpoint element, the search continues on the right half of the current range.
   - Repeat this process until the target value is found or the search range is empty.

3. **Pseudocode**:

   ```bash
   function binarySearch(array, target):
       left = 0
       right = length(array) - 1
       
       while left <= right:
           mid = (left + right) / 2
           if array[mid] == target:
               return mid
           else if array[mid] < target:
               left = mid + 1
           else:
               right = mid - 1
       
       return NOT_FOUND
   ```

4. **Time Complexity**: Binary search has a time complexity of O(log n), where n is the number of elements in the array. This is because with each iteration, the search space is halved.

5. **Space Complexity**: Binary search has a space complexity of O(1), as it only requires a constant amount of extra space for storing indices and variables.

6. **Edge Cases**:
   - If the array is empty, the search will immediately return a "not found" result.
   - If the target value is not in the array, the search will terminate when the search range becomes empty.

Binary search is a highly efficient algorithm for finding elements in sorted arrays, making it a fundamental tool in algorithm design and optimization.

### 1. Algorithms & Data Structures (C++): Binary Search Algorithm

Binary search is a fundamental algorithm used for searching within a sorted array. It works by repeatedly dividing the search interval in half.

Here's a simple implementation of the binary search algorithm in C++:

```cpp
#include <iostream>
#include <vector>

// Function to perform binary search
int binarySearch(const std::vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        // Check if the target is present at mid
        if (arr[mid] == target)
            return mid;

        // If target is greater, ignore left half
        if (arr[mid] < target)
            left = mid + 1;
        // If target is smaller, ignore right half
        else
            right = mid - 1;
    }

    // If the element is not present in the array
    return -1;
}

int main() {
    std::vector<int> arr = {1, 3, 5, 7, 9, 11, 13, 15};
    int target = 7;
    int index = binarySearch(arr, target);
    if (index != -1)
        std::cout << "Element found at index: " << index << std::endl;
    else
        std::cout << "Element not found in the array" << std::endl;
    return 0;
}
```

In this implementation:

- We define a function `binarySearch` that takes a sorted vector `arr` and the target element `target`.
- We initialize two pointers, `left` and `right`, representing the start and end of the search interval, respectively.
- We enter a while loop that continues until `left` is less than or equal to `right`.
- Inside the loop, we calculate the middle index of the current search interval (`mid`).
- We compare the element at the middle index with the target:
  - If they are equal, we return the index.
  - If the middle element is less than the target, we adjust `left` to `mid + 1` to search in the right half.
  - If the middle element is greater than the target, we adjust `right` to `mid - 1` to search in the left half.
- If the while loop exits without finding the target, we return -1 to indicate that the target element is not present in the array.

The `main` function demonstrates how to use the `binarySearch` function by searching for the element `7` in the array `arr`.

### 1. Algorithms & Data Structures (C++): Binary Search Complexity

Binary search is a fundamental algorithm used for searching in sorted arrays or lists. It works by repeatedly dividing the search interval in half until the target element is found or the interval is empty. In each step, it compares the target value with the middle element of the array and decides to continue the search on the left or right half.

The time complexity of binary search is O(log n), where n is the number of elements in the array. This is because with each step, the search interval is divided in half, reducing the search space exponentially. As a result, even for very large arrays, binary search can find the target element efficiently.

However, it's important to note that binary search requires the array to be sorted initially. Sorting the array itself might take O(n log n) time using algorithms like quicksort or mergesort. But if the array is already sorted, binary search provides a fast way to locate elements with a time complexity of O(log n).

In terms of space complexity, binary search typically requires only O(1) extra space, as it doesn't require any additional data structures beyond a few variables to keep track of the search interval.

So, in summary:

- Time complexity: O(log n)
- Space complexity: O(1)

### 1. Algorithms & Data Structures (C++): Binary Search Iterative Algorithm

Certainly! Below is an implementation of the iterative version of the binary search algorithm in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to perform binary search iteratively
int binarySearch(vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        // Check if target is present at mid
        if (arr[mid] == target)
            return mid;

        // If target is greater, ignore left half
        if (arr[mid] < target)
            left = mid + 1;

        // If target is smaller, ignore right half
        else
            right = mid - 1;
    }

    // If target is not found in the array
    return -1;
}

int main() {
    vector<int> arr = {2, 4, 6, 8, 10, 12, 14, 16, 18, 20};
    int target = 12;

    int result = binarySearch(arr, target);
    if (result != -1)
        cout << "Element found at index " << result << endl;
    else
        cout << "Element not found in the array" << endl;

    return 0;
}
```

This code defines a `binarySearch` function that takes a sorted vector `arr` and a target value `target` as input. It iteratively searches for the target value using the binary search algorithm. The `main` function demonstrates its usage by searching for a target value in a sorted array.

### 1. Algorithms & Data Structures (C++): Binary Search on Array

Certainly! Binary search is a fundamental algorithm used to efficiently locate a target value within a sorted array. Here's a simple implementation of binary search in C++:

```cpp
#include <iostream>
#include <vector>

// Binary search function
int binarySearch(const std::vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        // Check if target is present at mid
        if (arr[mid] == target)
            return mid;

        // If target greater, ignore left half
        if (arr[mid] < target)
            left = mid + 1;
        // If target is smaller, ignore right half
        else
            right = mid - 1;
    }

    // If target is not found in the array
    return -1;
}

int main() {
    std::vector<int> arr = {2, 4, 6, 8, 10, 12, 14, 16, 18, 20};
    int target = 14;

    int result = binarySearch(arr, target);

    if (result != -1)
        std::cout << "Element found at index " << result << std::endl;
    else
        std::cout << "Element not found in the array" << std::endl;

    return 0;
}
```

This code demonstrates how to perform a binary search on a sorted array of integers. Here's a breakdown of the binary search algorithm:

1. Initialize two pointers, `left` and `right`, to the start and end of the array respectively.
2. While `left` is less than or equal to `right`, continue searching.
3. Calculate the middle index of the array.
4. If the target value is found at the middle index, return the index.
5. If the target value is greater than the middle element, ignore the left half by updating `left` to `mid + 1`.
6. If the target value is smaller than the middle element, ignore the right half by updating `right` to `mid - 1`.
7. Repeat steps 2-6 until the target is found or `left` is greater than `right`.

This algorithm has a time complexity of O(log n), where n is the number of elements in the array, because it halves the search space in each iteration.

### 1. Algorithms & Data Structures (C++): Binary Search Recursive Algorithm

Sure, I can provide you with an example of a recursive binary search algorithm implemented in C++.

Here's how you can write it:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Recursive binary search function
int binarySearchRecursive(const vector<int> &arr, int low, int high, int target) {
    if (low <= high) {
        int mid = low + (high - low) / 2;
        
        // If the element is present at the middle itself
        if (arr[mid] == target)
            return mid;
        
        // If the element is smaller than mid, then it can only be present in left subarray
        if (arr[mid] > target)
            return binarySearchRecursive(arr, low, mid - 1, target);
        
        // Else the element can only be present in right subarray
        return binarySearchRecursive(arr, mid + 1, high, target);
    }
    
    // Element is not present in array
    return -1;
}

int main() {
    vector<int> arr = {2, 3, 4, 10, 40};
    int target = 10;
    int n = arr.size();
    int result = binarySearchRecursive(arr, 0, n - 1, target);
    if (result != -1)
        cout << "Element found at index " << result << endl;
    else
        cout << "Element not found in array" << endl;
    return 0;
}
```

In this code:

- `binarySearchRecursive` is the recursive function that takes the vector `arr`, the indices `low` and `high`, and the `target` element to be searched for.
- Inside the function, it checks if `low` is less than or equal to `high`. If not, it means the element is not present in the array, and it returns -1.
- If `low` is less than or equal to `high`, it calculates the `mid` index and checks if the element at `mid` is equal to the `target`.
- If it is, it returns the `mid` index.
- If the `target` is less than the element at `mid`, it recursively searches in the left subarray.
- If the `target` is greater than the element at `mid`, it recursively searches in the right subarray.
- The `main` function initializes an example array, sets a target element, calls the `binarySearchRecursive` function, and prints the result.

This code assumes that the array is sorted in ascending order.

### 1. Algorithms & Data Structures (C++): Binary Search Using Divide and Conquer Apprach

Certainly! Binary search is a fundamental algorithm used to efficiently locate a target value within a sorted array. Here's how you can implement it in C++ using the divide and conquer approach:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to perform binary search
int binarySearch(const vector<int>& arr, int target, int left, int right) {
    // Base case: If the left index exceeds the right index, the element is not found
    if (left > right) {
        return -1;
    }

    // Calculate the middle index of the array
    int mid = left + (right - left) / 2;

    // If the middle element is the target, return its index
    if (arr[mid] == target) {
        return mid;
    }
    // If the target is less than the middle element, search the left half of the array
    else if (target < arr[mid]) {
        return binarySearch(arr, target, left, mid - 1);
    }
    // If the target is greater than the middle element, search the right half of the array
    else {
        return binarySearch(arr, target, mid + 1, right);
    }
}

int main() {
    vector<int> arr = {1, 3, 5, 7, 9, 11, 13, 15, 17, 19};
    int target = 11;
    int index = binarySearch(arr, target, 0, arr.size() - 1);
    
    if (index != -1) {
        cout << "Element found at index: " << index << endl;
    } else {
        cout << "Element not found in the array." << endl;
    }

    return 0;
}
```

This implementation recursively searches for the target element within the specified range of indices `left` and `right`. If the middle element is the target, it returns its index. Otherwise, it recursively searches the left or right half of the array based on whether the target is less than or greater than the middle element, respectively. If the element is not found within the specified range, it returns -1.

### 1. Algorithms & Data Structures (C++): Binary Search using Iterations

Certainly! Binary search is an efficient algorithm for finding a target value within a sorted array. Here's a C++ implementation of binary search using iterations:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to perform binary search
int binarySearch(vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        // Check if target is present at mid
        if (arr[mid] == target)
            return mid;

        // If target is greater, ignore left half
        if (arr[mid] < target)
            left = mid + 1;

        // If target is smaller, ignore right half
        else
            right = mid - 1;
    }

    // Target not found
    return -1;
}

int main() {
    vector<int> arr = {1, 3, 5, 7, 9, 11, 13, 15, 17, 19};
    int target = 11;

    int result = binarySearch(arr, target);
    if (result != -1)
        cout << "Element found at index " << result << endl;
    else
        cout << "Element not found in array" << endl;

    return 0;
}
```

Explanation:

1. We define a function `binarySearch` that takes a sorted vector `arr` and a target value `target`.
2. We initialize two pointers `left` and `right` to the beginning and end of the array, respectively.
3. We enter a loop that continues until `left` is less than or equal to `right`.
4. Inside the loop, we calculate the `mid` index as the average of `left` and `right`.
5. We check if the element at the `mid` index is equal to the target. If it is, we return the index.
6. If the element at `mid` is less than the target, we update `left` to `mid + 1` to search the right half of the array.
7. If the element at `mid` is greater than the target, we update `right` to `mid - 1` to search the left half of the array.
8. If the loop exits without finding the target, we return -1 to indicate that the target is not present in the array.
9. In the `main` function, we create a sorted vector `arr` and a target value `target`.
10. We call the `binarySearch` function with these inputs and print the result.

This implementation has a time complexity of O(log n) because it halves the search space in each iteration.

### 1. Algorithms & Data Structures (C++): Binary Search using Recursion

Certainly! Binary search is a classic algorithm for searching for a target value within a sorted array. Here's how you can implement it using recursion in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Recursive binary search function
int binarySearch(vector<int>& arr, int target, int low, int high) {
    if (low > high) {
        // Base case: if low index exceeds high index, target not found
        return -1;
    }

    // Calculate the middle index
    int mid = low + (high - low) / 2;

    if (arr[mid] == target) {
        // Base case: target found at middle index
        return mid;
    } else if (arr[mid] > target) {
        // If target is less than the element at mid, search the left half
        return binarySearch(arr, target, low, mid - 1);
    } else {
        // If target is greater than the element at mid, search the right half
        return binarySearch(arr, target, mid + 1, high);
    }
}

int main() {
    vector<int> arr = {1, 3, 5, 7, 9, 11, 13, 15, 17, 19};
    int target = 13;
    int index = binarySearch(arr, target, 0, arr.size() - 1);
    if (index != -1) {
        cout << "Element found at index " << index << endl;
    } else {
        cout << "Element not found in the array" << endl;
    }
    return 0;
}
```

In this implementation:

- `binarySearch` is a recursive function that takes the sorted array `arr`, the `target` value to search for, and the indices `low` and `high` representing the range of the array to search within.
- At each step, it calculates the middle index `mid` of the range and compares the element at that index with the target.
- If the element at `mid` matches the target, it returns `mid`.
- If the target is less than the element at `mid`, it recursively searches the left half of the array.
- If the target is greater than the element at `mid`, it recursively searches the right half of the array.
- The process continues until the base case is reached (either the target is found or the range is empty).

### 1. Algorithms & Data Structures (C++): Branch & Bound

Branch and bound is a technique used in algorithm design to solve optimization problems, such as finding the best solution among a large set of possibilities. It's commonly employed in combinatorial optimization problems where exhaustive search is impractical due to the large search space. The basic idea behind branch and bound is to divide the problem into smaller subproblems, solve them recursively, and use bounds to eliminate certain branches of the search tree that are not promising.

In the context of algorithms and data structures, here's how branch and bound typically works:

1. **Problem Formulation**: First, the optimization problem is formulated in terms of decision variables and an objective function to optimize. For example, in the traveling salesman problem, the decision variables represent the order of visiting cities, and the objective function is to minimize the total distance traveled.

2. **Branching**: The problem is divided into smaller subproblems by making decisions at each step. These decisions create branches in a search tree. Each node in the tree represents a subproblem, and the branches represent the decisions made to reach that subproblem.

3. **Bounding**: At each node of the search tree, upper and lower bounds are computed for the objective function. These bounds are used to determine whether it's worthwhile to explore the subtree rooted at that node. If the upper bound of a node is worse than the best solution found so far, or if the lower bound is worse than the best feasible solution found so far, the subtree rooted at that node can be pruned.

4. **Searching**: The search proceeds by systematically exploring the search tree, typically using depth-first or breadth-first search strategies. At each node, the bounding step is used to determine whether to continue exploring its children or prune the subtree.

5. **Termination**: The search continues until all branches of the search tree have been explored or pruned. Once the entire search space has been traversed, the best solution found during the search process is returned as the optimal solution to the optimization problem.

In C++, branch and bound algorithms can be implemented using recursive functions or with explicit stack-based or queue-based traversal of the search tree. Careful design of bounding functions is crucial for the efficiency of branch and bound algorithms, as tighter bounds can lead to more aggressive pruning of the search space. Additionally, efficient data structures for storing partial solutions and bounds are important for reducing memory consumption and improving runtime performance.

### 1. Algorithms & Data Structures (C++): Branch And Bound

Branch and Bound is a classic algorithmic technique used for solving optimization problems, particularly combinatorial optimization problems, where the goal is to find the best solution among a large set of possibilities. It is often used in problems like the traveling salesman problem, the knapsack problem, or graph coloring problems.

In the context of combinatorial optimization, the Branch and Bound algorithm works by exploring the solution space systematically. It maintains a tree structure where each node represents a partial solution to the problem. The algorithm iteratively explores nodes of this tree, gradually narrowing down the search space until it finds the optimal solution or determines that no better solution can be found.

Here's a high-level overview of how the Branch and Bound algorithm typically works:

1. **Initialization**: Start with an empty or initial solution and initialize the best solution found so far to some initial value (usually infinity for minimization problems or negative infinity for maximization problems).

2. **Branching**: At each step, choose a variable to branch on. This involves partitioning the current problem into smaller subproblems by considering different choices for the selected variable. Each choice creates a new node in the search tree.

3. **Bounding**: For each new node created in the tree, calculate a bound (lower or upper bound) on the objective function value for the corresponding partial solution. This bound helps in deciding whether to explore the subtree rooted at that node further.

4. **Pruning**: If the bound for a node is worse than the best solution found so far, prune (discard) the subtree rooted at that node, as it cannot contain the optimal solution.

5. **Selection**: Choose the next node to explore based on some strategy, such as depth-first search, breadth-first search, or best-first search. This strategy may also involve using a priority queue to prioritize nodes with the most promising bounds.

6. **Termination**: Continue exploring nodes until either all nodes have been explored or the bound for the best node found so far cannot be improved upon. In the latter case, terminate the algorithm and return the best solution found.

Branch and Bound can be implemented recursively or iteratively, depending on the problem and personal preference. It's a powerful technique but can be computationally expensive, especially for large problem instances. Efficient bounding strategies and clever variable selection methods are crucial for improving its performance.

In C++, you would typically implement Branch and Bound using a combination of data structures like trees (often implemented using structs or classes) and algorithms for tree traversal (such as depth-first search or breadth-first search). You'll also need to define appropriate data structures and functions for representing the problem domain and calculating bounds.

### 1. Algorithms & Data Structures (C++): Common Divide and Conquer algorithms

Divide and conquer algorithms are essential in computer science and are often used to solve various problems efficiently. Here are some common divide and conquer algorithms implemented in C++:

1. **Binary Search**:
   - It is used to find the position of a target value within a sorted array.
   - Time Complexity: O(log n)

   ```cpp
   int binarySearch(vector<int>& arr, int target) {
       int left = 0, right = arr.size() - 1;
       while (left <= right) {
           int mid = left + (right - left) / 2;
           if (arr[mid] == target)
               return mid;
           else if (arr[mid] < target)
               left = mid + 1;
           else
               right = mid - 1;
       }
       return -1; // not found
   }
   ```

2. **Merge Sort**:
   - It is a sorting algorithm that follows the divide and conquer strategy.
   - Time Complexity: O(n log n)

   ```cpp
   void merge(vector<int>& arr, int left, int mid, int right) {
       int n1 = mid - left + 1;
       int n2 = right - mid;

       vector<int> L(n1), R(n2);

       for (int i = 0; i < n1; i++)
           L[i] = arr[left + i];
       for (int j = 0; j < n2; j++)
           R[j] = arr[mid + 1 + j];

       int i = 0, j = 0, k = left;
       while (i < n1 && j < n2) {
           if (L[i] <= R[j])
               arr[k++] = L[i++];
           else
               arr[k++] = R[j++];
       }

       while (i < n1)
           arr[k++] = L[i++];
       while (j < n2)
           arr[k++] = R[j++];
   }

   void mergeSort(vector<int>& arr, int left, int right) {
       if (left < right) {
           int mid = left + (right - left) / 2;
           mergeSort(arr, left, mid);
           mergeSort(arr, mid + 1, right);
           merge(arr, left, mid, right);
       }
   }
   ```

3. **Quick Sort**:
   - It is another efficient sorting algorithm based on the divide and conquer approach.
   - Time Complexity: O(n log n) (average case), O(n^2) (worst case)

   ```cpp
   int partition(vector<int>& arr, int low, int high) {
       int pivot = arr[high];
       int i = low - 1;
       for (int j = low; j < high; j++) {
           if (arr[j] < pivot) {
               i++;
               swap(arr[i], arr[j]);
           }
       }
       swap(arr[i + 1], arr[high]);
       return i + 1;
   }

   void quickSort(vector<int>& arr, int low, int high) {
       if (low < high) {
           int pi = partition(arr, low, high);
           quickSort(arr, low, pi - 1);
           quickSort(arr, pi + 1, high);
       }
   }
   ```

These are just a few examples of common divide and conquer algorithms. There are many others, such as Strassen's algorithm for matrix multiplication, Karatsuba algorithm for fast multiplication, etc. Each of these algorithms follows the same basic principle of breaking down a problem into smaller subproblems, solving them independently, and then combining the results.

### 1. Algorithms & Data Structures (C++): Coprime Divisor

To find the coprime divisor of a given number \( n \) in C++, you can implement a simple algorithm. The coprime divisor of a number \( n \) is any divisor \( d \) of \( n \) such that \( \text{gcd}(n, d) = 1 \), where \( \text{gcd} \) denotes the greatest common divisor. Here's a C++ implementation using the Euclidean algorithm to find the greatest common divisor:

```cpp
#include <iostream>

// Function to find the greatest common divisor (GCD) using the Euclidean algorithm
int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

// Function to find the coprime divisor of a number n
int coprime_divisor(int n) {
    // Finding coprime divisor
    for (int i = 2; i <= n; ++i) {
        if (n % i == 0 && gcd(n, i) == 1) {
            return i;
        }
    }
    // If no coprime divisor found, return -1
    return -1;
}

int main() {
    int n;
    std::cout << "Enter a number: ";
    std::cin >> n;
    int result = coprime_divisor(n);
    if (result != -1) {
        std::cout << "Coprime divisor of " << n << " is: " << result << std::endl;
    } else {
        std::cout << "No coprime divisor found for " << n << std::endl;
    }
    return 0;
}
```

This code first defines a function `gcd` to calculate the greatest common divisor using the Euclidean algorithm. Then, it defines a function `coprime_divisor` to find a coprime divisor of a given number. Finally, in the `main` function, it takes input from the user, calls the `coprime_divisor` function, and prints the result.

### 1. Algorithms & Data Structures (C++): Divide & Conquer

Divide and conquer is a fundamental algorithmic technique where you break down a problem into smaller, more manageable parts, solve each part independently, and then combine the solutions to form the solution to the original problem. This approach is particularly useful for solving problems that can be broken down into subproblems of the same type.

In C++, you can implement divide and conquer algorithms using recursion or iteration. Here's a general outline of how divide and conquer works, along with some common examples:

1. **Divide**: Break the problem into smaller, more manageable subproblems. This often involves dividing the input data into two or more smaller parts.

2. **Conquer**: Solve each subproblem recursively. If the subproblem is small enough, solve it directly (base case). Otherwise, recursively apply the same divide-and-conquer strategy to solve each subproblem.

3. **Combine**: Combine the solutions of the subproblems to form the solution to the original problem. This step typically involves merging or aggregating the solutions from the subproblems.

Here are some classic examples of algorithms that use the divide-and-conquer approach:

1. **Binary Search**: Search for a target value in a sorted array by repeatedly dividing the search interval in half.

2. **Merge Sort**: Sort an array by recursively dividing it into halves, sorting each half, and then merging the sorted halves.

3. **Quick Sort**: Sort an array by selecting a "pivot" element and partitioning the array into two subarrays such that elements less than the pivot are on the left and elements greater than the pivot are on the right. Recursively apply quicksort to the subarrays.

4. **Strassen's Algorithm**: Multiply two matrices using a recursive approach that breaks down the matrices into smaller submatrices.

5. **Closest Pair of Points**: Find the two closest points among a set of points in a plane using a divide-and-conquer approach.

When implementing divide-and-conquer algorithms in C++, pay attention to the base case of the recursion, as well as the termination condition to avoid infinite recursion. Also, be mindful of the overhead associated with recursion, especially for large problem sizes, and consider using iterative approaches or optimization techniques where appropriate.

### 1. Algorithms & Data Structures (C++): Divide and Conquer

Divide and conquer is a powerful algorithmic paradigm in computer science and is widely used in various algorithms and data structures. The basic idea behind divide and conquer is to break down a problem into smaller, more manageable subproblems, solve each subproblem independently, and then combine the solutions to the subproblems to obtain the solution to the original problem.

Here's how the divide and conquer paradigm typically works:

1. **Divide**: Break the problem into smaller, more manageable subproblems. This step involves dividing the problem into two or more smaller instances of the same problem. This can be done recursively until the subproblems become simple enough to solve directly.

2. **Conquer**: Solve the subproblems recursively. Each subproblem is solved independently, usually using the same divide and conquer approach. This step involves recursively solving the subproblems until they reach a base case, where they can be solved directly.

3. **Combine**: Combine the solutions of the subproblems to solve the original problem. Once the solutions to the subproblems are obtained, they are combined in a meaningful way to obtain the solution to the original problem.

Common examples of algorithms and data structures that use the divide and conquer approach include:

- **Merge Sort**: A sorting algorithm that divides the array into two halves, sorts each half separately, and then merges the sorted halves.
- **Quick Sort**: Another sorting algorithm that partitions the array into two subarrays based on a pivot element, recursively sorts each subarray, and then combines them.
- **Binary Search**: A search algorithm that divides the search space in half at each step, discarding the half that does not contain the target element.
- **Strassen's Algorithm**: A method for multiplying large matrices that divides the matrices into smaller submatrices, recursively computes partial products, and then combines them.
- **Closest Pair of Points**: An algorithm that finds the closest pair of points in a set by dividing the set into smaller subsets, solving the problem recursively, and then combining the solutions.

In C++, you can implement divide and conquer algorithms using recursive functions, which call themselves on smaller instances of the problem until they reach a base case. The base case is a simple instance of the problem that can be solved directly without further recursion.

### 1. Algorithms & Data Structures (C++): Divide and Conquer - countZeroes

The `countZeroes` algorithm using the divide and conquer approach aims to count the number of zeroes in a sorted array of 1s and 0s. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int countZeroes(const vector<int>& arr, int left, int right) {
    if (left > right) // Base case: no elements in the subarray
        return 0;

    int mid = left + (right - left) / 2; // Calculate the middle index

    // If the middle element is 1, then all zeroes are to the right
    if (arr[mid] == 1)
        return countZeroes(arr, mid + 1, right);
    // If the middle element is 0, then it's a zero and there might be more on the left
    else
        return (right - mid + 1) + countZeroes(arr, left, mid - 1);
}

int main() {
    vector<int> arr = {0, 0, 0, 1, 1, 1, 1, 1}; // Example sorted array

    int count = countZeroes(arr, 0, arr.size() - 1);
    cout << "Number of zeroes: " << count << endl;

    return 0;
}
```

In this algorithm, we recursively divide the array into halves until we find a portion of the array containing only zeroes. We then count the number of zeroes in that portion and combine the counts from the left and right subarrays.

### 1. Algorithms & Data Structures (C++): Divide and Conquer - findRotatedIndex

The `findRotatedIndex` function is a common problem in algorithms and data structures, particularly when dealing with sorted arrays that have been rotated at some unknown pivot point. The task is to find the index of a given target element in the rotated sorted array efficiently. Here's a C++ implementation using the divide and conquer approach:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int binarySearch(const vector<int>& nums, int target, int left, int right) {
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target)
            return mid;
        else if (nums[mid] < target)
            left = mid + 1;
        else
            right = mid - 1;
    }
    return -1; // Not found
}

int findPivot(const vector<int>& nums, int left, int right) {
    if (left > right)
        return -1; // No pivot found
    int mid = left + (right - left) / 2;
    if (mid < right && nums[mid] > nums[mid + 1])
        return mid; // Pivot found
    if (mid > left && nums[mid] < nums[mid - 1])
        return mid - 1; // Pivot found
    if (nums[left] >= nums[mid])
        return findPivot(nums, left, mid - 1); // Search in the left half
    return findPivot(nums, mid + 1, right); // Search in the right half
}

int findRotatedIndex(const vector<int>& nums, int target) {
    int pivot = findPivot(nums, 0, nums.size() - 1);
    if (pivot == -1)
        return binarySearch(nums, target, 0, nums.size() - 1);
    if (nums[pivot] == target)
        return pivot;
    if (nums[0] <= target)
        return binarySearch(nums, target, 0, pivot - 1);
    return binarySearch(nums, target, pivot + 1, nums.size() - 1);
}

int main() {
    vector<int> rotatedArray = {4, 5, 6, 7, 0, 1, 2};
    int target = 0;
    int index = findRotatedIndex(rotatedArray, target);
    if (index != -1)
        cout << "Element " << target << " found at index " << index << endl;
    else
        cout << "Element " << target << " not found." << endl;
    return 0;
}
```

In this implementation:

- `findRotatedIndex` is the main function that finds the target element in the rotated sorted array.
- `binarySearch` is a helper function to perform binary search within a range of indices.
- `findPivot` is a helper function to find the pivot element which indicates the rotation point in the array.

The overall time complexity of this algorithm is O(log n), where n is the number of elements in the array.

### 1. Algorithms & Data Structures (C++): Divide and Conquer - sortedFrequency

The "sortedFrequency" problem in the context of algorithms and data structures involves finding the frequency of a given number in a sorted array efficiently, often using a divide and conquer approach. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to find the first occurrence of a number in a sorted array
int findFirstOccurrence(const vector<int>& arr, int target) {
    int low = 0;
    int high = arr.size() - 1;
    int result = -1;

    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] == target) {
            result = mid;
            high = mid - 1; // Continue searching on the left side
        } else if (arr[mid] < target) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }

    return result;
}

// Function to find the last occurrence of a number in a sorted array
int findLastOccurrence(const vector<int>& arr, int target) {
    int low = 0;
    int high = arr.size() - 1;
    int result = -1;

    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] == target) {
            result = mid;
            low = mid + 1; // Continue searching on the right side
        } else if (arr[mid] < target) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }

    return result;
}

// Function to find the frequency of a number in a sorted array
int sortedFrequency(const vector<int>& arr, int target) {
    int firstOccurrence = findFirstOccurrence(arr, target);
    int lastOccurrence = findLastOccurrence(arr, target);

    if (firstOccurrence == -1 || lastOccurrence == -1) {
        return 0; // If the number doesn't exist in the array
    }

    return lastOccurrence - firstOccurrence + 1;
}

int main() {
    vector<int> arr = {1, 1, 2, 2, 2, 3, 4, 4, 5, 5, 5, 5};
    int target = 2;
    cout << "Frequency of " << target << " in the array: " << sortedFrequency(arr, target) << endl;
    return 0;
}
```

In this code:

- `findFirstOccurrence` finds the index of the first occurrence of the target number using binary search.
- `findLastOccurrence` finds the index of the last occurrence of the target number using binary search.
- `sortedFrequency` calculates the frequency of the target number by subtracting the index of the first occurrence from the index of the last occurrence and adding 1.

This approach has a time complexity of O(log n), where n is the number of elements in the array, as it performs binary search twice.

### 1. Algorithms & Data Structures (C++): Divide and Conquer Algorithms

Divide and conquer algorithms are a fundamental paradigm in computer science and are often used to solve problems efficiently by breaking them down into smaller, more manageable subproblems. In C++, you can implement divide and conquer algorithms using recursion or iterative approaches. Here's an overview along with some examples:

#### Overview of Divide and Conquer

1. **Divide**: Break the problem into smaller subproblems that are similar to the original problem but are simpler to solve.

2. **Conquer**: Recursively solve these subproblems. If the subproblems are small enough, solve them directly using a base case.

3. **Combine**: Merge the solutions of the subproblems to solve the original problem.

#### Example 1: Binary Search

Binary search is a classic example of a divide and conquer algorithm used to search for a target element in a sorted array.

```cpp
int binarySearch(vector<int>& arr, int target, int left, int right) {
    if (left > right) return -1; // Base case: element not found

    int mid = left + (right - left) / 2;

    if (arr[mid] == target) return mid; // Found the target
    else if (arr[mid] < target) return binarySearch(arr, target, mid + 1, right); // Search right half
    else return binarySearch(arr, target, left, mid - 1); // Search left half
}

int main() {
    vector<int> arr = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int target = 7;
    int index = binarySearch(arr, target, 0, arr.size() - 1);
    if (index != -1)
        cout << "Element found at index " << index << endl;
    else
        cout << "Element not found" << endl;
    return 0;
}
```

#### Example 2: Merge Sort

Merge sort is another classic divide and conquer algorithm used for sorting arrays.

```cpp
void merge(vector<int>& arr, int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;

    vector<int> L(n1), R(n2);

    for (int i = 0; i < n1; i++)
        L[i] = arr[left + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[mid + 1 + j];

    int i = 0, j = 0, k = left;

    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k++] = L[i++];
        } else {
            arr[k++] = R[j++];
        }
    }

    while (i < n1) {
        arr[k++] = L[i++];
    }

    while (j < n2) {
        arr[k++] = R[j++];
    }
}

void mergeSort(vector<int>& arr, int left, int right) {
    if (left >= right) return;

    int mid = left + (right - left) / 2;
    mergeSort(arr, left, mid);
    mergeSort(arr, mid + 1, right);
    merge(arr, left, mid, right);
}

int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    int n = arr.size();

    mergeSort(arr, 0, n - 1);

    cout << "Sorted array: ";
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;

    return 0;
}
```

These examples demonstrate the divide and conquer approach in action. Binary search divides the array in half for each recursive call, while merge sort divides the array into smaller halves until it's sorted. Both algorithms demonstrate the divide-and-conquer strategy, breaking down the problem into smaller, more manageable parts, solving them, and then combining the results.

### 1. Algorithms & Data Structures (C++): Euclid's Algorithm

Euclid's Algorithm is a classic method for finding the greatest common divisor (GCD) of two integers. It's based on the principle that the GCD of two numbers also divides their difference, which allows for recursively finding the GCD.

Here's a simple implementation of Euclid's Algorithm in C++:

```cpp
#include <iostream>

// Function to find the GCD of two numbers using Euclid's Algorithm
int gcd(int a, int b) {
    // Base case: if b is 0, then GCD is a
    if (b == 0)
        return a;
    // Recursive case: call gcd with b and the remainder of a divided by b
    return gcd(b, a % b);
}

int main() {
    int num1, num2;
    std::cout << "Enter two numbers: ";
    std::cin >> num1 >> num2;
    // Output the GCD of the two numbers
    std::cout << "GCD of " << num1 << " and " << num2 << " is " << gcd(num1, num2) << std::endl;
    return 0;
}
```

In this implementation:

1. The `gcd` function takes two integers, `a` and `b`, and recursively finds their GCD.
2. The base case is when `b` becomes 0, indicating that `a` is the GCD.
3. Otherwise, it calls itself with `b` and the remainder of `a` divided by `b`.
4. In the `main` function, it takes two numbers from the user and outputs their GCD using the `gcd` function.

This algorithm is efficient and has a time complexity of O(log(min(a, b))), where a and b are the two input numbers. It's commonly used in various mathematical computations and is one of the fundamental algorithms in number theory and computer science.

### 1. Algorithms & Data Structures (C++): Evaluate Reverse Polish Notation

Evaluating Reverse Polish Notation (RPN) involves evaluating expressions written in postfix notation, where operators come after their operands. For instance, the expression "3 + 4" would be written as "3 4 +".

Here's a basic algorithm to evaluate RPN expressions using C++:

```cpp
#include <iostream>
#include <stack>
#include <string>
#include <sstream>

using namespace std;

int evalRPN(string tokens) {
    stack<int> stk;
    stringstream ss(tokens);
    string token;

    while (ss >> token) {
        if (token == "+" || token == "-" || token == "*" || token == "/") {
            int operand2 = stk.top();
            stk.pop();
            int operand1 = stk.top();
            stk.pop();

            if (token == "+")
                stk.push(operand1 + operand2);
            else if (token == "-")
                stk.push(operand1 - operand2);
            else if (token == "*")
                stk.push(operand1 * operand2);
            else if (token == "/")
                stk.push(operand1 / operand2);
        } else {
            stk.push(stoi(token));
        }
    }

    return stk.top();
}

int main() {
    string expression = "3 4 +"; // Example expression
    cout << "Result: " << evalRPN(expression) << endl;
    return 0;
}
```

In this code:

- We use a stack to keep track of operands.
- We tokenize the input string using a `stringstream` and iterate through each token.
- If the token is an operator, we pop the top two elements from the stack, apply the operator, and push the result back onto the stack.
- If the token is an operand, we convert it to an integer and push it onto the stack.
- At the end, the top of the stack contains the final result.

You can modify the `main` function to input any RPN expression as a string and get the result. For example, you can use `"3 4 + 2 *"` to evaluate "(3 + 4) * 2", or `"5 1 2 + 4 * + 3 -"` to evaluate "5 + ((1 + 2) * 4) - 3".

### 1. Algorithms & Data Structures (C++): Even and Odd Numbers Rearrangement

Sure, I can help with that! Rearranging even and odd numbers in an array in C++ can be achieved using a simple algorithm that involves swapping elements. Here's a basic implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void rearrangeEvenOdd(vector<int>& arr) {
    int left = 0;
    int right = arr.size() - 1;

    while (left < right) {
        // Move left pointer until it points to an odd number
        while (arr[left] % 2 == 0 && left < right) {
            left++;
        }
        // Move right pointer until it points to an even number
        while (arr[right] % 2 != 0 && left < right) {
            right--;
        }
        // Swap the elements pointed by left and right pointers
        if (left < right) {
            swap(arr[left], arr[right]);
            left++;
            right--;
        }
    }
}

int main() {
    vector<int> arr = {12, 34, 45, 9, 8, 90, 3};
    
    cout << "Original array: ";
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;
    
    rearrangeEvenOdd(arr);
    
    cout << "Array after rearrangement: ";
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}
```

This code defines a function `rearrangeEvenOdd` that takes a vector of integers as input and rearranges its elements so that even numbers appear before odd numbers. It uses two pointers, one starting from the beginning of the array (`left`) and the other starting from the end (`right`). These pointers move towards each other, swapping elements as needed until they meet.

The `main` function demonstrates how to use this function with an example array. The original array is printed, then `rearrangeEvenOdd` is called to rearrange its elements, and finally, the rearranged array is printed.

### 1. Algorithms & Data Structures (C++): Exhaustive Search

Exhaustive search, also known as brute-force search, is a straightforward algorithmic technique for solving computational problems by systematically enumerating all possible candidates for the solution and checking whether each candidate satisfies the problem's constraints. In the context of algorithms and data structures, exhaustive search can be applied to various types of problems, including searching, optimization, and decision-making.

Here's a basic outline of how an exhaustive search algorithm works:

1. **Generate Candidates**: Generate all possible candidate solutions to the problem. This often involves generating permutations, combinations, or subsets of elements, depending on the problem requirements.

2. **Evaluate Candidates**: For each generated candidate solution, evaluate whether it satisfies the problem's constraints or criteria. This evaluation typically involves some form of computation or comparison.

3. **Update Solution**: Keep track of the best solution found so far, based on the problem's objective function or criteria.

4. **Repeat**: Continue generating and evaluating candidate solutions until all possibilities have been explored.

5. **Return Solution**: Return the best solution found during the search process.

Despite its simplicity, exhaustive search can be computationally expensive, especially for large problem instances, because it explores the entire search space. However, it is guaranteed to find the optimal solution (if one exists) for problems where the search space is finite and feasible to explore.

Here's a simple example in C++ demonstrating an exhaustive search approach for finding the maximum element in an array:

```cpp
#include <iostream>
#include <vector>

int findMax(const std::vector<int>& arr) {
    int maxVal = arr[0]; // Initialize maxVal with the first element
    for (int i = 1; i < arr.size(); ++i) {
        if (arr[i] > maxVal) {
            maxVal = arr[i]; // Update maxVal if a larger element is found
        }
    }
    return maxVal;
}

int main() {
    std::vector<int> arr = {5, 9, 3, 7, 2, 8};
    int maxElement = findMax(arr);
    std::cout << "Maximum element: " << maxElement << std::endl;
    return 0;
}
```

In this example, the `findMax` function iterates through the array `arr`, comparing each element to the current maximum value (`maxVal`). If an element greater than `maxVal` is found, `maxVal` is updated accordingly. Finally, the maximum element found is returned. This is a simple illustration of exhaustive search, where all elements of the array are examined to find the maximum.

### 1. Algorithms & Data Structures (C++): Fast Mutiplication

Fast multiplication algorithms are crucial in various fields, especially in computer science and mathematics. In C++, one popular algorithm for fast multiplication is the Karatsuba algorithm. It's a divide-and-conquer algorithm that reduces the multiplication of two n-digit numbers to three multiplications of n/2-digit numbers, along with some additional additions and subtractions.

Here's a simplified implementation of the Karatsuba algorithm in C++:

```cpp
#include <iostream>
#include <string>
#include <algorithm>

using namespace std;

string add(string a, string b) {
    string result;
    int carry = 0;
    int i = a.size() - 1, j = b.size() - 1;

    while (i >= 0 || j >= 0 || carry) {
        int sum = carry;
        if (i >= 0) sum += a[i--] - '0';
        if (j >= 0) sum += b[j--] - '0';
        carry = sum / 10;
        result += to_string(sum % 10);
    }

    reverse(result.begin(), result.end());
    return result;
}

string karatsuba(string num1, string num2) {
    int n = num1.size();
    if (n == 1) {
        int res = (num1[0] - '0') * (num2[0] - '0');
        return to_string(res);
    }

    int m = n / 2;

    string high1 = num1.substr(0, m);
    string low1 = num1.substr(m);
    string high2 = num2.substr(0, m);
    string low2 = num2.substr(m);

    string z0 = karatsuba(low1, low2);
    string z1 = karatsuba(add(low1, high1), add(low2, high2));
    string z2 = karatsuba(high1, high2);

    z1 = add(z1, "-" + z0);
    z1 = add(z1, "-" + z2);

    string result = z2;
    for (int i = 0; i < 2 * m; ++i)
        z2 += "0";
    for (int i = 0; i < m; ++i)
        z1 += "0";
    result = add(result, z1);
    result = add(result, z0);

    return result;
}

int main() {
    string num1 = "1234";
    string num2 = "5678";

    cout << "Product: " << karatsuba(num1, num2) << endl;

    return 0;
}
```

This code implements the Karatsuba algorithm for multiplying two large numbers represented as strings. It recursively divides the numbers until they become single digits, then performs the multiplication and combines the results following the algorithm's logic.

### 1. Algorithms & Data Structures (C++): Find First & Last Occurence

Certainly! Finding the first and last occurrences of an element in a sorted array can be efficiently done using binary search. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to find the first occurrence of target in nums
int findFirstOccurrence(vector<int>& nums, int target) {
    int low = 0, high = nums.size() - 1;
    int firstOccurrence = -1;
    
    while (low <= high) {
        int mid = low + (high - low) / 2;
        
        if (nums[mid] == target) {
            firstOccurrence = mid;
            high = mid - 1; // continue searching towards the left
        } else if (nums[mid] < target) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }
    
    return firstOccurrence;
}

// Function to find the last occurrence of target in nums
int findLastOccurrence(vector<int>& nums, int target) {
    int low = 0, high = nums.size() - 1;
    int lastOccurrence = -1;
    
    while (low <= high) {
        int mid = low + (high - low) / 2;
        
        if (nums[mid] == target) {
            lastOccurrence = mid;
            low = mid + 1; // continue searching towards the right
        } else if (nums[mid] < target) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }
    
    return lastOccurrence;
}

int main() {
    vector<int> nums = {1, 2, 2, 3, 3, 3, 4, 5, 5, 6};
    int target = 3;
    
    int first = findFirstOccurrence(nums, target);
    int last = findLastOccurrence(nums, target);
    
    if (first != -1 && last != -1) {
        cout << "First occurrence of " << target << " is at index " << first << endl;
        cout << "Last occurrence of " << target << " is at index " << last << endl;
    } else {
        cout << "Target not found in the array." << endl;
    }
    
    return 0;
}
```

This code first defines two functions: `findFirstOccurrence` and `findLastOccurrence`, which use binary search to find the first and last occurrences of a target element in a sorted array, respectively. Then, in the `main` function, you can test these functions with a sample array and target element.

### 1. Algorithms & Data Structures (C++): Finding Number

Sure, let's discuss how to find a number in C++ using algorithms and data structures. There are several approaches we can take depending on the context and constraints of the problem. Here's a basic example using linear search and binary search:

1. **Linear Search**:
   - In linear search, you iterate through each element of the array sequentially until you find the desired element or reach the end of the array.
   - This is a simple approach but not very efficient, especially for large arrays.

   ```cpp
   #include <iostream>
   using namespace std;

   int linearSearch(int arr[], int n, int target) {
       for (int i = 0; i < n; i++) {
           if (arr[i] == target)
               return i; // return index if found
       }
       return -1; // return -1 if not found
   }

   int main() {
       int arr[] = {1, 2, 3, 4, 5};
       int target = 3;
       int n = sizeof(arr) / sizeof(arr[0]);
       int index = linearSearch(arr, n, target);
       if (index != -1)
           cout << "Element found at index " << index << endl;
       else
           cout << "Element not found" << endl;
       return 0;
   }
   ```

2. **Binary Search**:
   - Binary search works on sorted arrays. It repeatedly divides the search interval in half until the target is found or the interval is empty.
   - It's much faster than linear search, especially for large datasets.

   ```cpp
   #include <iostream>
   using namespace std;

   int binarySearch(int arr[], int l, int r, int target) {
       while (l <= r) {
           int mid = l + (r - l) / 2;
           if (arr[mid] == target)
               return mid;
           if (arr[mid] < target)
               l = mid + 1;
           else
               r = mid - 1;
       }
       return -1; // return -1 if not found
   }

   int main() {
       int arr[] = {1, 2, 3, 4, 5};
       int target = 3;
       int n = sizeof(arr) / sizeof(arr[0]);
       int index = binarySearch(arr, 0, n - 1, target);
       if (index != -1)
           cout << "Element found at index " << index << endl;
       else
           cout << "Element not found" << endl;
       return 0;
   }
   ```

These are just basic examples. Depending on your requirements, you might need to implement more advanced algorithms or data structures. Let me know if you have any specific requirements or questions!

### 1. Algorithms & Data Structures (C++): Floyd's Tortoise And Hare Explanation

Floyd's Tortoise and Hare algorithm is a clever technique used to detect cycles in a linked list or any sequence of elements. It's named after Robert W. Floyd, who first described it, and the classic story of the tortoise and the hare race.

Here's how it works:

1. **Initialization**: Start with two pointers, often referred to as the "tortoise" and the "hare," both initially pointing to the beginning of the sequence.

2. **Movement**: In each iteration, move the tortoise one step forward and the hare two steps forward through the sequence.

3. **Cycle Detection**: If there's a cycle in the sequence, the hare will eventually catch up to the tortoise because it moves twice as fast. Once they meet at some point within the cycle, you know there's a cycle.

4. **Finding the Start of the Cycle (Optional)**: After detecting the cycle, reset one of the pointers (either the tortoise or the hare) to the beginning of the sequence, while keeping the other pointer where it is. Then, move both pointers one step at a time until they meet again. The point at which they meet is the start of the cycle.

In C++, you can implement Floyd's Tortoise and Hare algorithm like this for a linked list:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* next;
};

bool hasCycle(Node* head) {
    if (!head || !head->next) return false;

    Node* tortoise = head;
    Node* hare = head;

    while (hare && hare->next) {
        tortoise = tortoise->next;
        hare = hare->next->next;
        if (tortoise == hare) return true; // cycle detected
    }

    return false; // no cycle
}

int main() {
    // Example usage
    Node* head = new Node{1, nullptr};
    head->next = new Node{2, nullptr};
    head->next->next = new Node{3, nullptr};
    head->next->next->next = head->next; // Creating a cycle

    std::cout << std::boolalpha << hasCycle(head) << std::endl; // Output: true

    // Don't forget to deallocate memory to avoid memory leaks
    // Deallocation code goes here...

    return 0;
}
```

This code demonstrates how to check for a cycle in a linked list using Floyd's Tortoise and Hare algorithm. It runs in O(n) time complexity where n is the number of nodes in the linked list.

### 1. Algorithms & Data Structures (C++): Floyd's Tortoise And Hare Implementation

Floyd's Tortoise and Hare algorithm, also known as cycle detection algorithm, is used to detect a cycle in a sequence of values. It's particularly useful in linked lists but can be adapted to various scenarios including arrays. Here's a C++ implementation of Floyd's Tortoise and Hare algorithm:

```cpp
#include <iostream>

// Node definition for a linked list
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
        if (slow == fast) // If the pointers meet, there's a cycle
            return true;

        slow = slow->next;
        fast = fast->next->next;
    }

    return false; // If we reach here, there's no cycle
}

int main() {
    // Example usage:
    ListNode *head = new ListNode(3);
    head->next = new ListNode(2);
    head->next->next = new ListNode(0);
    head->next->next->next = new ListNode(-4);
    // Creating a cycle
    head->next->next->next->next = head->next;

    if (hasCycle(head))
        std::cout << "Cycle detected!\n";
    else
        std::cout << "No cycle detected.\n";

    // Free memory (cleanup)
    ListNode *current = head;
    while (current != nullptr) {
        ListNode *temp = current;
        current = current->next;
        delete temp;
    }

    return 0;
}
```

In this implementation, we have a `hasCycle` function that takes the head of a linked list as input and returns true if there's a cycle in the list, and false otherwise. It uses the slow and fast pointer technique to traverse the list. If there's a cycle, eventually the fast pointer will catch up to the slow pointer. If there's no cycle, the fast pointer will reach the end of the list.

### 1. Algorithms & Data Structures (C++): GCD

Certainly! GCD stands for Greatest Common Divisor, which is the largest number that divides two integers without leaving a remainder. There are several algorithms to compute the GCD of two numbers. One of the most common algorithms is the Euclidean Algorithm.

Here's how you can implement the Euclidean Algorithm to find the GCD of two numbers in C++:

```cpp
#include <iostream>

// Function to compute GCD using Euclidean algorithm
int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

int main() {
    int num1, num2;
    std::cout << "Enter two numbers: ";
    std::cin >> num1 >> num2;

    int result = gcd(num1, num2);
    std::cout << "GCD of " << num1 << " and " << num2 << " is " << result << std::endl;

    return 0;
}
```

This code defines a `gcd` function that takes two integers `a` and `b` and returns their GCD using the Euclidean algorithm. In the `main` function, it prompts the user to enter two numbers, computes their GCD using the `gcd` function, and then prints the result.

You can compile and run this code to find the GCD of any two numbers.

### 1. Algorithms & Data Structures (C++): GCD Complexity

The complexity of finding the greatest common divisor (GCD) of two integers is crucial for understanding algorithm performance. The traditional method, often learned in school, is the Euclidean algorithm. Its complexity is logarithmic in the smaller of the two numbers. Let's delve into it:

#### Euclidean Algorithm

1. **Algorithm**:
   Given two integers `a` and `b`, where `a >= b`:
   - If `b` divides `a` evenly, then `b` is the GCD.
   - Otherwise, the GCD of `a` and `b` is the same as the GCD of `b` and the remainder of `a / b`.

2. **Complexity**:
   - **Best Case**: O(1) when `b` evenly divides `a`.
   - **Worst Case**: O(log min(a, b)) when `a` and `b` are consecutive Fibonacci numbers.

#### Implementation in C++

```cpp
int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}
```

This implementation continuously replaces `a` with `b` and `b` with the remainder of `a / b` until `b` becomes zero, at which point `a` contains the GCD.

#### Complexity Analysis

The number of steps in the Euclidean algorithm depends on how quickly `a` and `b` decrease towards the base case (`b = 0`). In the worst case, when `a` and `b` are consecutive Fibonacci numbers, the number of steps is logarithmic in the smaller of the two numbers.

#### Example

Let's take an example with `a = 55` and `b = 34` (consecutive Fibonacci numbers):

- 55 % 34 = 21
- 34 % 21 = 13
- 21 % 13 = 8
- 13 % 8 = 5
- 8 % 5 = 3
- 5 % 3 = 2
- 3 % 2 = 1
- 2 % 1 = 0

So, the GCD of 55 and 34 is 1, and the algorithm takes 8 steps, which is logarithmic in the smaller number (34 in this case).

### 1. Algorithms & Data Structures (C++): GCD on Directed Path

To find the greatest common divisor (GCD) on a directed path in a graph, you would typically perform a depth-first search (DFS) or breadth-first search (BFS) traversal to traverse the path and compute the GCD of the values associated with the vertices on that path. Here's a basic outline of how you could implement this in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Structure to represent a directed edge
struct Edge {
    int from, to;
};

// Function to compute GCD of two numbers
int gcd(int a, int b) {
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to find GCD on a directed path
int gcdOnPath(vector<vector<int>>& graph, vector<int>& values, vector<Edge>& path, int start, int end) {
    int result = values[start]; // Initialize with starting value
    for (const Edge& edge : path) {
        if (edge.from == start) {
            result = gcd(result, values[edge.to]);
            start = edge.to;
        }
    }
    return result;
}

int main() {
    // Example graph represented as an adjacency list
    int n = 5; // Number of vertices
    vector<vector<int>> graph(n);
    graph[0].push_back(1);
    graph[1].push_back(2);
    graph[2].push_back(3);
    graph[3].push_back(4);

    // Values associated with each vertex
    vector<int> values = {12, 18, 24, 30, 36};

    // Example directed path
    vector<Edge> path = {{0, 1}, {1, 2}, {2, 3}, {3, 4}};

    // Compute GCD on the directed path
    int start = 0, end = 4;
    int result = gcdOnPath(graph, values, path, start, end);
    cout << "GCD on path from " << start << " to " << end << ": " << result << endl;

    return 0;
}
```

In this example:

- The `gcd` function computes the greatest common divisor using the Euclidean algorithm.
- The `gcdOnPath` function traverses the directed path specified by the `path` vector, computing the GCD of the values associated with the vertices on that path.
- The `main` function sets up an example graph, values associated with each vertex, and a directed path. It then calls `gcdOnPath` to compute the GCD on the specified path.

You can customize the example graph, vertex values, and directed path as needed for your application.

### 1. Algorithms & Data Structures (C++): GCD or HCF Using Recursion

Certainly! Here's a C++ implementation of finding the greatest common divisor (GCD) or highest common factor (HCF) of two numbers using recursion:

```cpp
#include <iostream>

// Function to find the GCD/HCF of two numbers using recursion
int gcd(int a, int b) {
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

int main() {
    int num1, num2;
    std::cout << "Enter two numbers: ";
    std::cin >> num1 >> num2;

    // Ensure positive numbers for the algorithm
    num1 = abs(num1);
    num2 = abs(num2);

    // Calculate GCD/HCF
    int result = gcd(num1, num2);

    std::cout << "GCD/HCF of " << num1 << " and " << num2 << " is: " << result << std::endl;

    return 0;
}
```

This code defines a `gcd` function that takes two integers `a` and `b` and returns their GCD/HCF using recursion. In the `main` function, it takes two numbers from the user, ensures they are positive, and then calculates their GCD/HCF using the `gcd` function. Finally, it prints the result.

### 1. Algorithms & Data Structures (C++): GCD Sort of an Array

To implement GCD sort of an array in C++, you need to follow these steps:

1. Define a function to compute the GCD (Greatest Common Divisor) of two numbers.
2. Define a function to sort the array based on GCD.
3. Use these functions to implement GCD sort.

Here's the C++ implementation:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Function to calculate GCD of two numbers
int gcd(int a, int b) {
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Comparator function to sort based on GCD
bool compare(int a, int b) {
    return gcd(a, b) < gcd(b, a);
}

// Function to perform GCD sort
void gcdSort(vector<int>& arr) {
    sort(arr.begin(), arr.end(), compare);
}

int main() {
    vector<int> arr = {5, 10, 15, 20, 25, 30};
    cout << "Original Array: ";
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;

    gcdSort(arr);

    cout << "Array after GCD Sort: ";
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}
```

This code first defines functions to compute the GCD of two numbers and a comparator function to sort the array based on GCD. Then, it defines a function to perform GCD sort. Finally, it demonstrates the usage of these functions in the `main()` function.

### 1. Algorithms & Data Structures (C++): GCD using Extended Euclidean Algorithm

Certainly! The Extended Euclidean Algorithm is a method used to find the greatest common divisor (GCD) of two numbers. It also computes the coefficients \(x\) and \(y\) such that \(ax + by = \text{gcd}(a, b)\). Here's how you can implement it in C++:

```cpp
#include <iostream>

using namespace std;

// Function to calculate GCD using Extended Euclidean Algorithm
int extended_gcd(int a, int b, int &x, int &y) {
    if (a == 0) {
        x = 0;
        y = 1;
        return b;
    }

    int x1, y1;
    int gcd = extended_gcd(b % a, a, x1, y1);

    x = y1 - (b / a) * x1;
    y = x1;

    return gcd;
}

int main() {
    int a, b;
    cout << "Enter two numbers: ";
    cin >> a >> b;

    int x, y;
    int gcd = extended_gcd(a, b, x, y);

    cout << "GCD(" << a << ", " << b << ") = " << gcd << endl;
    cout << "Coefficients (x, y): " << x << ", " << y << endl;

    return 0;
}
```

In this code:

- The function `extended_gcd` recursively calculates the GCD and updates the coefficients \(x\) and \(y\) accordingly.
- In the `main` function, you can input two numbers, and it will output their GCD and the coefficients \(x\) and \(y\).

### 1. Algorithms & Data Structures (C++): Geometric Algorithms - Convex Hull

The Convex Hull problem is a fundamental geometric algorithm used to find the smallest convex polygon that encloses a given set of points in a plane. In C++, you can implement various algorithms to solve this problem, such as Graham's scan, Jarvis march (gift wrapping), or Andrew's monotone chain.

Here's a basic implementation of the Jarvis March algorithm:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Structure to represent a 2D point
struct Point {
    int x, y;
};

// Utility function to find the orientation of triplet (p, q, r)
int orientation(Point p, Point q, Point r) {
    int val = (q.y - p.y) * (r.x - q.x) - (q.x - p.x) * (r.y - q.y);
    if (val == 0) return 0;     // Collinear
    return (val > 0) ? 1 : 2;   // Clockwise or counterclockwise
}

// Jarvis March algorithm to find convex hull
vector<Point> convexHull(vector<Point>& points) {
    int n = points.size();
    if (n < 3) return {}; // Convex hull not possible

    // Find the leftmost point
    int left = 0;
    for (int i = 1; i < n; i++) {
        if (points[i].x < points[left].x)
            left = i;
    }

    int p = left, q;
    vector<bool> visited(n, false);
    vector<Point> hull;

    // Start from the leftmost point and keep moving clockwise
    // until we reach the start point again
    do {
        hull.push_back(points[p]);
        visited[p] = true;

        q = (p + 1) % n;
        for (int i = 0; i < n; i++) {
            if (orientation(points[p], points[i], points[q]) == 2)
                q = i;
        }

        p = q;
    } while (p != left);

    return hull;
}

int main() {
    vector<Point> points = {{0, 3}, {1, 1}, {2, 2}, {4, 4}, 
                            {0, 0}, {1, 2}, {3, 1}, {3, 3}};
    
    vector<Point> hull = convexHull(points);

    cout << "Convex Hull points:\n";
    for (auto p : hull) {
        cout << "(" << p.x << ", " << p.y << ")\n";
    }

    return 0;
}
```

This code defines a `Point` structure to represent 2D points and implements the Jarvis March algorithm to find the convex hull of a given set of points. The `orientation()` function determines the orientation of three points, which is used to find the next point in the convex hull computation. Finally, the `main()` function demonstrates how to use the `convexHull()` function.

### 1. Algorithms & Data Structures (C++): Greatest Common Divisor

Sure, implementing the Greatest Common Divisor (GCD) algorithm in C++ is straightforward. There are several ways to compute the GCD of two numbers, but one of the most common algorithms is the Euclidean algorithm. Here's how you can implement it:

```cpp
#include <iostream>

// Function to find the greatest common divisor (GCD) of two numbers using the Euclidean algorithm
int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

int main() {
    int num1, num2;
    std::cout << "Enter two numbers: ";
    std::cin >> num1 >> num2;

    // Call the gcd function and print the result
    std::cout << "GCD of " << num1 << " and " << num2 << " is: " << gcd(num1, num2) << std::endl;

    return 0;
}
```

In this code:

- The `gcd` function takes two integers `a` and `b` as input and returns their greatest common divisor.
- Inside the `gcd` function, the Euclidean algorithm is applied iteratively until `b` becomes 0. At each iteration, `b` is replaced by the remainder of `a` divided by `b`, and `a` is replaced by the previous value of `b`.
- Finally, the function returns the value of `a`, which is the GCD of the original `a` and `b`.

You can compile and run this code to find the GCD of any two numbers you input.

### 1. Algorithms & Data Structures (C++): Greedy Algorithm

A Greedy Algorithm is an approach to solve optimization problems by making the locally optimal choice at each step with the hope of finding a global optimum. The strategy is to make the choice that seems best at the moment and then solve the subproblem that arises after that choice.

#### Characteristics of Greedy Algorithms

1. **Greedy Choice Property**: A global optimum can be arrived at by selecting a local optimum (the best available choice at the current stage) without reconsideration.

2. **Optimal Substructure**: An optimal solution to the problem contains optimal solutions to its subproblems. This means that you can solve the problem by solving its smaller subproblems.

#### Examples of Greedy Algorithms

1. **Dijkstra's Algorithm**: Used to find the shortest path between nodes in a graph.
2. **Prim's Algorithm**: Finds the minimum spanning tree for a weighted undirected graph.
3. **Kruskal's Algorithm**: Another algorithm for finding the minimum spanning tree.
4. **Huffman Coding**: A method of data compression that uses variable-length codes to represent characters in a message, with shorter codes for more frequent characters.

#### Implementing Greedy Algorithms in C++

Let's take a simple example of the coin change problem. Given a set of coin denominations and a target amount, find the minimum number of coins needed to make that amount.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int minCoins(vector<int>& coins, int target) {
    sort(coins.begin(), coins.end(), greater<int>()); // Sort coins in descending order
    int count = 0;
    for (int i = 0; i < coins.size(); ++i) {
        while (target >= coins[i]) {
            target -= coins[i];
            count++;
        }
    }
    return count;
}

int main() {
    vector<int> coins = {25, 10, 5, 1}; // Available coin denominations
    int target = 63; // Target amount
    cout << "Minimum coins required: " << minCoins(coins, target) << endl;
    return 0;
}
```

In this example, the greedy approach is to always pick the largest denomination that is less than or equal to the remaining target amount. We continue this until the target amount becomes 0.

#### Limitations of Greedy Algorithms

While Greedy Algorithms are intuitive and relatively easy to implement, they don't always guarantee an optimal solution. In some cases, they may produce a suboptimal solution. Therefore, it's important to analyze the problem carefully to ensure that the greedy approach works correctly.

### 1. Algorithms & Data Structures (C++): Greedy Algorithms

Greedy algorithms are a class of algorithms that aim to find the optimal solution to a given problem by making a series of locally optimal choices. At each step, a greedy algorithm selects the best option available without considering the global context. While this approach may not always lead to the globally optimal solution, it often produces solutions that are close to optimal and is particularly useful for optimization problems where finding the exact solution is computationally expensive.

In C++, implementing greedy algorithms typically involves defining the problem, identifying the criteria for making greedy choices, and iteratively making those choices until a solution is found. Here's a simple example of a greedy algorithm implemented in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Function to solve the coin change problem using a greedy algorithm
vector<int> coinChangeGreedy(int amount, const vector<int>& coins) {
    vector<int> result;
    int n = coins.size();

    // Sort coins in descending order
    sort(coins.begin(), coins.end(), greater<int>());

    // Greedy approach: Start with the largest coin denomination
    for (int i = 0; i < n; ++i) {
        while (amount >= coins[i]) {
            result.push_back(coins[i]);
            amount -= coins[i];
        }
    }

    // If amount is not fully covered, no solution exists
    if (amount > 0) {
        cout << "No solution exists." << endl;
        result.clear();
    }

    return result;
}

int main() {
    vector<int> coins = {25, 10, 5, 1}; // Coin denominations
    int amount = 47; // Amount to make change for

    cout << "Coin denominations: ";
    for (int coin : coins) {
        cout << coin << " ";
    }
    cout << endl;

    cout << "Amount to make change for: " << amount << endl;

    // Solve using greedy algorithm
    vector<int> change = coinChangeGreedy(amount, coins);

    // Display the result
    cout << "Greedy solution: ";
    if (!change.empty()) {
        for (int coin : change) {
            cout << coin << " ";
        }
        cout << endl;
    }

    return 0;
}
```

In this example, the `coinChangeGreedy` function implements a greedy algorithm to solve the coin change problem, where given a certain amount and a set of coin denominations, the goal is to find the minimum number of coins needed to make up that amount. The algorithm sorts the coin denominations in descending order and iteratively selects the largest coin denomination that does not exceed the remaining amount until the amount becomes zero or no solution exists.

While greedy algorithms can be simple and efficient, it's important to note that they may not always produce the optimal solution for every problem. Careful analysis is required to ensure that the greedy approach is applicable and yields satisfactory results.

### 1. Algorithms & Data Structures (C++): Greedy Algorithms (Insertion Sort, Selection Sort, Prim, Kruskal, Topological )

Certainly! Let's briefly discuss each of these greedy algorithms along with their implementations in C++:

1. **Insertion Sort**:
   - It's a simple sorting algorithm that builds the final sorted array (or list) one item at a time.
   - At each iteration, the algorithm takes the next element from the input data and inserts it into its correct position in the already sorted part of the array.
   - Time Complexity: O(n^2) average and worst-case performance.

   ```cpp
   void insertionSort(int arr[], int n) {
       for (int i = 1; i < n; ++i) {
           int key = arr[i];
           int j = i - 1;
           while (j >= 0 && arr[j] > key) {
               arr[j + 1] = arr[j];
               j = j - 1;
           }
           arr[j + 1] = key;
       }
   }
   ```

2. **Selection Sort**:
   - It sorts an array by repeatedly finding the minimum element (considering ascending order) from the unsorted part and putting it at the beginning.
   - Time Complexity: O(n^2) as there are two nested loops.

   ```cpp
   void selectionSort(int arr[], int n) {
       for (int i = 0; i < n - 1; ++i) {
           int min_idx = i;
           for (int j = i + 1; j < n; ++j)
               if (arr[j] < arr[min_idx])
                   min_idx = j;
           swap(arr[min_idx], arr[i]);
       }
   }
   ```

3. **Prim's Algorithm**:
   - It's a greedy algorithm that finds a minimum spanning tree for a weighted undirected graph.
   - It starts with an arbitrary node and grows the spanning tree by adding the cheapest edge that connects the tree to a new node.
   - Time Complexity: O(V^2) using an adjacency matrix or O(E log V) using a binary heap for priority queue.

4. **Kruskal's Algorithm**:
   - Another greedy algorithm for finding a minimum spanning tree.
   - It builds the spanning tree by adding edges one at a time into the empty spanning tree, starting with the smallest edge until the tree forms a minimum spanning tree.
   - Time Complexity: O(E log V), where E is the number of edges and V is the number of vertices.

5. **Topological Sorting**:
   - It's used for ordering vertices in a directed graph so that for every directed edge u -> v, vertex u comes before v in the ordering.
   - Topological sorting is not possible if the graph has cycles.
   - Time Complexity: O(V + E) using Depth First Search (DFS) traversal.

Implementations of Prim's, Kruskal's, and topological sorting might be a bit more involved, involving data structures like priority queues and graphs. If you're interested, I can provide those implementations too!

### 1. Algorithms & Data Structures (C++): Grid

Sure! "Grid" is a common data structure used in programming, particularly in problems related to grids, matrices, or 2D arrays. In C++, you can represent a grid using a 2D array, a vector of vectors, or a custom class.

Here's an example of representing a grid using a 2D array in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

const int ROWS = 3;
const int COLS = 3;

int main() {
    // Define a 2D array to represent the grid
    int grid[ROWS][COLS] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    // Accessing elements in the grid
    cout << "Element at row 0, column 1: " << grid[0][1] << endl;
    
    // Traversing the grid
    cout << "Grid elements: " << endl;
    for (int i = 0; i < ROWS; ++i) {
        for (int j = 0; j < COLS; ++j) {
            cout << grid[i][j] << " ";
        }
        cout << endl;
    }

    return 0;
}
```

This example demonstrates how to create a 3x3 grid using a 2D array and how to access and traverse its elements.

You can also use vectors of vectors for more flexibility and dynamic sizing:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    // Define a vector of vectors to represent the grid
    vector<vector<int>> grid = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    // Accessing elements in the grid
    cout << "Element at row 0, column 1: " << grid[0][1] << endl;
    
    // Traversing the grid
    cout << "Grid elements: " << endl;
    for (const auto& row : grid) {
        for (int element : row) {
            cout << element << " ";
        }
        cout << endl;
    }

    return 0;
}
```

This version uses vectors of vectors to create a 3x3 grid and demonstrates accessing and traversing its elements.

You can choose the representation based on your requirements regarding memory efficiency, ease of use, and flexibility.

### 1. Algorithms & Data Structures (C++): How to solve Fibonacci series using Divide and Conquer approach?

To solve the Fibonacci series using the Divide and Conquer approach in C++, you can implement a recursive function that divides the problem into smaller subproblems and then combines their solutions. Here's a sample implementation:

```cpp
#include <iostream>
using namespace std;

// Function to calculate Fibonacci number using Divide and Conquer
int fibonacci(int n) {
    if (n <= 1)
        return n;
    
    // Divide the problem into two subproblems
    int a = fibonacci(n / 2);
    int b = fibonacci(n / 2 - 1);
    
    // Combine the solutions of subproblems
    if (n % 2 == 0)
        return a * (2 * b + a);
    else
        return a * a + b * b;
}

int main() {
    int n;
    cout << "Enter the value of n: ";
    cin >> n;
    
    cout << "Fibonacci number at position " << n << " is: " << fibonacci(n) << endl;
    
    return 0;
}
```

In this implementation, the `fibonacci` function recursively divides the problem into two subproblems, each of size approximately `n/2`. It then combines the solutions of these subproblems to find the Fibonacci number for the given position `n`. This approach has a time complexity of O(log n).

### 1. Algorithms & Data Structures (C++): Implementation and worst case complexity of Binary Search

Binary search is a fundamental algorithm for searching in a sorted array. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Binary search function
int binarySearch(vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        // Check if target is present at mid
        if (arr[mid] == target) {
            return mid;
        }
        // If target greater, ignore left half
        else if (arr[mid] < target) {
            left = mid + 1;
        }
        // If target is smaller, ignore right half
        else {
            right = mid - 1;
        }
    }

    // If target is not found
    return -1;
}

int main() {
    vector<int> arr = {2, 3, 4, 10, 40};
    int target = 10;
    int index = binarySearch(arr, target);
    if (index != -1) {
        cout << "Element found at index: " << index << endl;
    } else {
        cout << "Element not found" << endl;
    }
    return 0;
}
```

In the worst-case scenario, binary search has a time complexity of O(log n), where n is the number of elements in the sorted array. This is because in each step, the search space is halved. This makes binary search very efficient, especially for large arrays.

### 1. Algorithms & Data Structures (C++): Improving Linear Search

Improving linear search in C++ can be done through various techniques to enhance its efficiency. Although linear search has a time complexity of O(n), which means it's not the most efficient algorithm for large datasets, there are still ways to optimize it within its limitations. Here are some techniques you can employ:

1. **Early Termination**: Stop the search as soon as the element is found. This can save time if the target element is found early in the array.

```cpp
template<typename T>
int linearSearch(const T arr[], int size, const T& target) {
    for (int i = 0; i < size; ++i) {
        if (arr[i] == target) {
            return i; // Return index if found
        }
    }
    return -1; // Not found
}
```

1. **Move-to-Front (MTF)**: If an element is found, move it to the front of the array. This improves the average-case performance, especially if the same elements are searched for frequently.

```cpp
template<typename T>
int linearSearchMTF(T arr[], int size, const T& target) {
    for (int i = 0; i < size; ++i) {
        if (arr[i] == target) {
            if (i != 0) {
                // Swap the found element with the first element
                std::swap(arr[i], arr[0]);
            }
            return 0; // Element found at the beginning
        }
    }
    return -1; // Not found
}
```

1. **Transposition**: If an element is found, swap it with the previous element. This may improve the performance by reducing the number of swaps compared to MTF.

```cpp
template<typename T>
int linearSearchTransposition(T arr[], int size, const T& target) {
    for (int i = 0; i < size; ++i) {
        if (arr[i] == target) {
            if (i != 0) {
                // Swap the found element with the previous element
                std::swap(arr[i], arr[i - 1]);
            }
            return i; // Return index if found
        }
    }
    return -1; // Not found
}
```

1. **Sentinel Search**: Place the target element at the end of the array. This eliminates the need for bounds checking within the loop, improving performance slightly.

```cpp
template<typename T>
int linearSearchSentinel(T arr[], int size, const T& target) {
    // Place the target element at the end temporarily
    std::swap(arr[size - 1], target);

    int i = 0;
    // Search loop with guaranteed termination
    while (arr[i] != target) {
        ++i;
    }

    // Restore the array
    std::swap(arr[size - 1], target);

    if (i < size - 1 || arr[size - 1] == target) {
        return i; // Return index if found
    } else {
        return -1; // Not found
    }
}
```

These techniques can enhance the performance of linear search under specific conditions. However, for significantly large datasets or frequent searches, consider using more efficient algorithms like binary search (for sorted data) or hash tables (for unsorted data).

### 1. Algorithms & Data Structures (C++): Interpolation Search

Interpolation search is an algorithm used for searching a target value in a sorted array. It's an improvement over binary search for cases where the elements in the array are uniformly distributed.

Here's how interpolation search works:

1. Calculate the position using interpolation formula:
   \[ \text{pos} = \text{low} + \left( \frac{\text{high} - \text{low}}{\text{arr[high]} - \text{arr[low]}} \right) \times (\text{key} - \text{arr[low]}) \]

2. If the calculated position is out of the array bounds, set it to the nearest bound.

3. Compare the element at the calculated position with the target value.

4. If the element at the calculated position is equal to the target value, return the position.

5. If the element at the calculated position is greater than the target value, search in the left subarray.

6. If the element at the calculated position is less than the target value, search in the right subarray.

7. Repeat the process until the element is found or the subarray becomes empty.

Here's a sample implementation in C++:

```cpp
#include <iostream>
using namespace std;

int interpolationSearch(int arr[], int n, int key) {
    int low = 0, high = n - 1;

    while (low <= high && key >= arr[low] && key <= arr[high]) {
        if (low == high) {
            if (arr[low] == key)
                return low;
            return -1;
        }

        int pos = low + ((double)(high - low) / (arr[high] - arr[low])) * (key - arr[low]);

        if (arr[pos] == key)
            return pos;
        else if (arr[pos] < key)
            low = pos + 1;
        else
            high = pos - 1;
    }

    return -1;
}

int main() {
    int arr[] = {2, 4, 6, 8, 10, 12, 14, 16, 18, 20};
    int n = sizeof(arr) / sizeof(arr[0]);
    int key = 16;
    int index = interpolationSearch(arr, n, key);
    if (index != -1)
        cout << "Element found at index " << index << endl;
    else
        cout << "Element not found" << endl;
    return 0;
}
```

This implementation assumes that the array is sorted in ascending order. The time complexity of interpolation search is \(O(\log \log n)\) on average, where \(n\) is the number of elements in the array. However, in the worst-case scenario, it can degrade to \(O(n)\) if the elements are not uniformly distributed.

### 1. Algorithms & Data Structures (C++): Intersection of List

To find the intersection of two lists in C++, you can use several approaches, depending on whether the lists are sorted, unsorted, singly linked, doubly linked, or if you have additional memory available. Here's a straightforward approach for two unsorted singly linked lists with no extra memory usage:

```cpp
#include <iostream>
#include <unordered_set>

struct Node {
    int data;
    Node* next;
};

void push(Node*& head, int newData) {
    Node* newNode = new Node;
    newNode->data = newData;
    newNode->next = head;
    head = newNode;
}

Node* findIntersection(Node* list1, Node* list2) {
    std::unordered_set<int> seen;

    // Traverse list1 and store elements in set
    while (list1 != nullptr) {
        seen.insert(list1->data);
        list1 = list1->next;
    }

    Node* intersection = nullptr;
    Node* tail = nullptr;

    // Traverse list2, if element exists in set, it's an intersection
    while (list2 != nullptr) {
        if (seen.find(list2->data) != seen.end()) {
            // Add to intersection list
            if (intersection == nullptr) {
                intersection = new Node;
                intersection->data = list2->data;
                intersection->next = nullptr;
                tail = intersection;
            } else {
                tail->next = new Node;
                tail = tail->next;
                tail->data = list2->data;
                tail->next = nullptr;
            }
        }
        list2 = list2->next;
    }

    return intersection;
}

void printList(Node* head) {
    while (head != nullptr) {
        std::cout << head->data << " ";
        head = head->next;
    }
    std::cout << std::endl;
}

int main() {
    Node* list1 = nullptr;
    Node* list2 = nullptr;

    // Constructing list1: 3->6->9->15->30
    push(list1, 30);
    push(list1, 15);
    push(list1, 9);
    push(list1, 6);
    push(list1, 3);

    // Constructing list2: 10->15->30
    push(list2, 30);
    push(list2, 15);
    push(list2, 10);

    std::cout << "List 1: ";
    printList(list1);
    std::cout << "List 2: ";
    printList(list2);

    Node* intersection = findIntersection(list1, list2);

    std::cout << "Intersection: ";
    printList(intersection);

    return 0;
}
```

This code first inserts all elements from the first list into an unordered set. Then, it traverses the second list and checks if each element exists in the set. If it does, the element is added to the intersection list. Finally, it returns the intersection list.

### 1. Algorithms & Data Structures (C++): Introduction and greedy approaches

Sure! Let's start with an introduction to algorithms and data structures in C++.

**Algorithms** are step-by-step procedures or formulas for solving problems. They are essential in computer science because they help programmers write efficient and optimized code.

**Data structures** are ways of organizing and storing data in a computer so that it can be accessed and modified efficiently. They are the building blocks of algorithms and are crucial for managing data effectively.

C++ is a powerful programming language commonly used for implementing algorithms and data structures due to its efficiency and flexibility. Now, let's delve into one category of algorithms: greedy algorithms.

**Greedy algorithms** are a class of algorithms that make a sequence of choices, each of which is the best at that moment, without considering the long-term consequences. Greedy algorithms are simple and easy to implement, but they don't always guarantee an optimal solution for every problem.

Here's an example of a greedy algorithm:

**Problem:** Suppose you have a set of coins of different denominations, and you want to find the minimum number of coins required to make a certain amount of money.

**Algorithm:**

1. Sort the coins in descending order based on their denominations.
2. Initialize a variable `totalCoins` to 0 to keep track of the total number of coins used.
3. Iterate through the sorted coins:
   - While the current coin value is less than or equal to the remaining amount:
     - Add 1 to `totalCoins`.
     - Subtract the value of the current coin from the remaining amount.
4. Once the remaining amount becomes 0, return `totalCoins`.

Let's implement this algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int minCoins(vector<int>& coins, int amount) {
    sort(coins.begin(), coins.end(), greater<int>());
    int totalCoins = 0;
    for (int coin : coins) {
        while (coin <= amount) {
            totalCoins++;
            amount -= coin;
        }
    }
    return totalCoins;
}

int main() {
    vector<int> coins = {25, 10, 5, 1}; // Denominations of coins
    int amount = 47; // Amount to make
    cout << "Minimum number of coins required: " << minCoins(coins, amount) << endl;
    return 0;
}
```

In this example, we have coins of denominations 25, 10, 5, and 1, and we want to make an amount of 47. The `minCoins` function calculates the minimum number of coins required using a greedy approach.

That's a basic introduction to algorithms, data structures, and greedy approaches in C++. Let me know if you'd like to explore more algorithms or data structures!

### 1. Algorithms & Data Structures (C++): Lazy Propagation

Lazy propagation is a technique used in algorithms and data structures, particularly in the context of segment trees, to efficiently handle updates and queries on a range of elements. It's commonly used when you need to perform a large number of updates and queries on segments of an array or any other data structure.

In lazy propagation, instead of updating the values of all elements in a range immediately, we postpone the updates until they are needed. When a query is made for a particular range, we apply all pending updates to that range and propagate the updates lazily to its children.

Here's a basic overview of how lazy propagation works in the context of a segment tree:

1. **Initialization**: Initially, all elements of the segment tree and lazy tree are set to some default value.

2. **Lazy Update**: When an update operation (such as incrementing all elements in a range by a certain value) is to be performed on a range, instead of updating the actual elements, we update a corresponding range in the lazy tree. This update is done in constant time.

3. **Propagation**: When a query operation (such as finding the sum of elements in a range) is made on a range, before accessing the elements in that range, we first check if there are any pending updates for that range in the lazy tree. If there are, we apply those updates to the actual elements in the segment tree and propagate the updates to the children in the lazy tree.

4. **Querying**: Once all pending updates are applied, we perform the query operation on the range as usual.

Here's a simple example of lazy propagation in C++ for range sum queries and range updates:

```cpp
#include <iostream>
#include <vector>

using namespace std;

const int MAXN = 100000;

int lazy[4 * MAXN];
int tree[4 * MAXN];

// Lazy update function
void lazyUpdate(int node, int start, int end, int l, int r, int val) {
    if (lazy[node] != 0) {
        tree[node] += (end - start + 1) * lazy[node];
        if (start != end) {
            lazy[node * 2] += lazy[node];
            lazy[node * 2 + 1] += lazy[node];
        }
        lazy[node] = 0;
    }
    if (start > end || start > r || end < l)
        return;
    if (start >= l && end <= r) {
        tree[node] += (end - start + 1) * val;
        if (start != end) {
            lazy[node * 2] += val;
            lazy[node * 2 + 1] += val;
        }
        return;
    }
    int mid = (start + end) / 2;
    lazyUpdate(node * 2, start, mid, l, r, val);
    lazyUpdate(node * 2 + 1, mid + 1, end, l, r, val);
    tree[node] = tree[node * 2] + tree[node * 2 + 1];
}

// Query function
int query(int node, int start, int end, int l, int r) {
    if (start > end || start > r || end < l)
        return 0;
    if (lazy[node] != 0) {
        tree[node] += (end - start + 1) * lazy[node];
        if (start != end) {
            lazy[node * 2] += lazy[node];
            lazy[node * 2 + 1] += lazy[node];
        }
        lazy[node] = 0;
    }
    if (start >= l && end <= r)
        return tree[node];
    int mid = (start + end) / 2;
    int p1 = query(node * 2, start, mid, l, r);
    int p2 = query(node * 2 + 1, mid + 1, end, l, r);
    return (p1 + p2);
}

int main() {
    // Example usage
    vector<int> arr = {1, 3, 5, 7, 9, 11};
    int n = arr.size();
    // Build the segment tree
    // Note: Function to build the segment tree is not shown here
    // It's assumed that the tree has been built already
    // Perform lazy updates
    lazyUpdate(1, 0, n - 1, 0, 3, 3); // Increment elements from index 0 to 3 by 3
    // Perform queries
    cout << query(1, 0, n - 1, 0, 5) << endl; // Output: 54 (1+3+8+10+12+14)
    return 0;
}
```

This example demonstrates lazy propagation for range updates (incrementing elements in a range) and range sum queries. The `lazyUpdate` function handles lazy updates, while the `query` function handles queries on the segment tree.

### 1. Algorithms & Data Structures (C++): LCS Top Down

In C++, implementing the Longest Common Subsequence (LCS) problem using the top-down approach typically involves dynamic programming and memoization. Here's a simple implementation:

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

// Function to calculate LCS using top-down approach
int LCS(string& s1, string& s2, int m, int n, vector<vector<int>>& memo) {
    // Base case: if any of the strings is empty
    if (m == 0 || n == 0)
        return 0;

    // If the subproblem has already been computed, return its result from memoization
    if (memo[m][n] != -1)
        return memo[m][n];

    // If the characters match, include them in LCS
    if (s1[m - 1] == s2[n - 1])
        return memo[m][n] = 1 + LCS(s1, s2, m - 1, n - 1, memo);
    // If characters don't match, move in either of the two strings and find LCS
    else
        return memo[m][n] = max(LCS(s1, s2, m, n - 1, memo), LCS(s1, s2, m - 1, n, memo));
}

// Wrapper function for LCS calculation
int LongestCommonSubsequence(string& s1, string& s2) {
    int m = s1.length();
    int n = s2.length();
    vector<vector<int>> memo(m + 1, vector<int>(n + 1, -1)); // Memoization table

    return LCS(s1, s2, m, n, memo);
}

int main() {
    string s1 = "AGGTAB";
    string s2 = "GXTXAYB";
    cout << "Length of Longest Common Subsequence: " << LongestCommonSubsequence(s1, s2) << endl;
    return 0;
}
```

In this code:

- `LCS` is the recursive function that calculates the length of the longest common subsequence of two given strings `s1` and `s2`.
- `LongestCommonSubsequence` is a wrapper function to initialize memoization and call the `LCS` function.
- `memo` is a 2D vector used for memoization. It stores the results of subproblems to avoid redundant calculations.
- The time complexity of this implementation is O(m*n), where m and n are the lengths of the input strings `s1` and `s2`, respectively. The space complexity is also O(m*n) due to the memoization table.

### 1. Algorithms & Data Structures (C++): Linear Search

Sure! Linear search is one of the simplest searching algorithms. It iterates through each element in a list sequentially until it finds the target value or reaches the end of the list.

Here's a basic implementation of linear search in C++:

```cpp
#include <iostream>
#include <vector>

// Function to perform linear search
int linearSearch(std::vector<int>& arr, int target) {
    for (int i = 0; i < arr.size(); ++i) {
        if (arr[i] == target) {
            return i; // Return the index if found
        }
    }
    return -1; // Return -1 if not found
}

int main() {
    std::vector<int> arr = {2, 4, 6, 8, 10, 12, 14};

    int target = 8;
    int index = linearSearch(arr, target);

    if (index != -1) {
        std::cout << "Element found at index: " << index << std::endl;
    } else {
        std::cout << "Element not found" << std::endl;
    }

    return 0;
}
```

In this code:

- The `linearSearch` function takes a vector of integers `arr` and an integer `target` to search for.
- It iterates through each element of the vector using a for loop.
- If the target value is found at index `i`, it returns the index.
- If the target value is not found after iterating through the entire vector, it returns -1.
- In the `main` function, we create a vector `arr` and call `linearSearch` with a target value of `8`.
- If the target is found, it prints the index; otherwise, it prints "Element not found".

This implementation has a time complexity of O(n), where n is the number of elements in the vector.

### 1. Algorithms & Data Structures (C++): Linear Search Algorithm

The linear search algorithm is one of the simplest searching algorithms. It sequentially checks each element of the data structure until a match is found or the entire structure has been searched. Here's a basic implementation of the linear search algorithm in C++:

```cpp
#include <iostream>
#include <vector>

// Function to perform linear search
int linearSearch(const std::vector<int>& arr, int target) {
    for (int i = 0; i < arr.size(); ++i) {
        if (arr[i] == target) {
            return i;  // Return the index where target is found
        }
    }
    return -1;  // Return -1 if target is not found
}

int main() {
    std::vector<int> array = {5, 2, 4, 7, 9, 1, 6};
    int target = 7;
    
    int index = linearSearch(array, target);
    if (index != -1) {
        std::cout << "Element found at index: " << index << std::endl;
    } else {
        std::cout << "Element not found in the array." << std::endl;
    }
    
    return 0;
}
```

This code defines a function `linearSearch` that takes a vector of integers `arr` and a target integer `target` to search for. It iterates through each element of the vector using a loop and compares each element with the target. If the target is found, it returns the index where it's located; otherwise, it returns -1 to indicate that the target is not present in the array.

In the `main` function, we create a vector `array` containing some integers and specify a `target` integer to search for. We then call the `linearSearch` function with these parameters and print the result.

Keep in mind that linear search has a time complexity of O(n), where n is the number of elements in the array. This means the time it takes to execute the algorithm increases linearly with the size of the array. For large arrays, more efficient algorithms like binary search (if the array is sorted) or hash tables may be more appropriate.

### 1. Algorithms & Data Structures (C++): Linear Search Time Complexity

The time complexity of a linear search algorithm in C++ is O(n), where 'n' is the number of elements in the array being searched. This means that the time taken to execute the algorithm grows linearly with the size of the input array.

In a linear search, each element of the array is sequentially compared with the target element until a match is found or the end of the array is reached. Therefore, if the target element is located at the end of the array or is not present at all, the algorithm will need to iterate through all 'n' elements in the worst-case scenario, resulting in a time complexity of O(n).

### 1. Algorithms & Data Structures (C++): Master Method

The Master Theorem is a handy tool used to analyze the time complexity of recursive algorithms, particularly those that follow a divide-and-conquer approach. It provides a straightforward way to determine the time complexity of such algorithms without needing to go through a rigorous recurrence relation solving process.

The standard form of the Master Theorem is usually presented in terms of a recurrence relation of the form:

\[ T(n) = aT\left(\frac{n}{b}\right) + f(n) \]

Where:

- \( T(n) \) is the time complexity of the algorithm.
- \( a \) represents the number of recursive subproblems.
- \( \frac{n}{b} \) represents the size of each subproblem.
- \( f(n) \) represents the time complexity of dividing the problem and combining the results.

The Master Theorem states that the time complexity \( T(n) \) can be expressed in terms of three cases:

1. **Case 1:** If \( f(n) = O(n^{\log_b a - \epsilon}) \) for some constant \( \epsilon > 0 \), where \( a > b^{\epsilon} \), then \( T(n) = \Theta(n^{\log_b a}) \).

2. **Case 2:** If \( f(n) = \Theta(n^{\log_b a}) \), then \( T(n) = \Theta(n^{\log_b a} \log n) \).

3. **Case 3:** If \( f(n) = \Omega(n^{\log_b a + \epsilon}) \) for some constant \( \epsilon > 0 \), where \( a < b^{\epsilon} \), and if \( af\left(\frac{n}{b}\right) \leq kf(n) \) for some constant \( k < 1 \) and sufficiently large \( n \), then \( T(n) = \Theta(f(n)) \).

In these cases:

- Case 1 typically covers scenarios where the divide-and-conquer dominates the overall time complexity.
- Case 2 occurs when both the divide-and-conquer and the combining steps contribute equally to the time complexity.
- Case 3 arises when the combining step dominates the time complexity.

Applying the Master Theorem can greatly simplify the analysis of recursive algorithms, especially when their structure closely resembles the form of the theorem. However, it's important to note that not all recursive algorithms fit neatly into this framework, and in such cases, alternative methods may be required to analyze their time complexity.

### 1. Algorithms & Data Structures (C++): Master's Theorem

The Master Theorem is a useful tool for analyzing the time complexity of divide-and-conquer algorithms, particularly those that can be represented using recurrence relations. It provides a straightforward way to determine the asymptotic behavior of such algorithms. The theorem is particularly handy when dealing with algorithms that split the problem into subproblems of equal size.

The general form of the Master Theorem can be stated as follows:

Suppose we have a recurrence relation of the form:

\[ T(n) = aT\left(\frac{n}{b}\right) + f(n) \]

Where:

- \( n \) is the size of the problem.
- \( a \) is the number of subproblems in the recursion.
- \( b \) is the factor by which the problem size is reduced in each recursive call.
- \( f(n) \) is the cost of dividing the problem and combining the results.

The Master Theorem then provides a solution for \( T(n) \) in terms of \( a \), \( b \), and \( f(n) \) in three cases, depending on the relationship between \( f(n) \) and \( n^{\log_b a} \):

1. If \( f(n) = O(n^{\log_b a - \epsilon}) \) for some constant \( \epsilon > 0 \), then \( T(n) = \Theta(n^{\log_b a}) \).
2. If \( f(n) = \Theta(n^{\log_b a}) \), then \( T(n) = \Theta(n^{\log_b a} \log n) \).
3. If \( f(n) = \Omega(n^{\log_b a + \epsilon}) \) for some constant \( \epsilon > 0 \), and if \( af\left(\frac{n}{b}\right) \leq kf(n) \) for some constant \( k < 1 \) and sufficiently large \( n \), then \( T(n) = \Theta(f(n)) \).

These cases cover most common recurrence relations encountered in algorithm analysis. By identifying which case applies to a given recurrence relation, you can easily determine the asymptotic behavior of the algorithm without needing to solve the recurrence explicitly. This simplifies the analysis of divide-and-conquer algorithms significantly.

### 1. Algorithms & Data Structures (C++): Meet in the Middle

"Meet in the Middle" (MITM) is a clever algorithmic technique used to optimize certain types of exhaustive search problems by dividing the search space into two halves and searching each half separately. It's particularly useful for problems where the search space is too large to explore entirely, but can be divided into two smaller, manageable parts. It's commonly applied in tasks like finding subsets or combinations that satisfy certain conditions, or solving problems involving large data sets.

Here's a basic outline of how the "Meet in the Middle" technique works:

1. **Divide the Problem**: Split the problem into two halves, typically of equal size if possible. Each half represents a sub-problem that can be solved independently.

2. **Preprocessing**: Solve each sub-problem separately. This often involves generating all possible combinations, permutations, or subsets of elements in each half and storing them in a suitable data structure, such as a hash table or a sorted array.

3. **Search**: Once both halves have been preprocessed, iterate through one half and for each element, search for its complement (the matching element) in the other half. The complement may be found using a binary search, hash table lookup, or other efficient searching techniques.

4. **Combine Results**: Combine the results obtained from the two halves to find the overall solution to the original problem.

One classic example where "Meet in the Middle" can be applied is in the subset sum problem: given a set of integers, find whether there exists a subset whose sum equals a given target value. By splitting the set into two halves, generating all possible sums for each half, and then searching for complements between the two halves, we can efficiently find if such a subset exists.

In C++, you would implement the "Meet in the Middle" technique using appropriate data structures and algorithms for preprocessing and searching, depending on the problem at hand. This might involve using STL containers like vectors, sets, or maps, along with algorithms like binary search or hashing functions.

Here's a simplified example in C++ for the subset sum problem using the "Meet in the Middle" technique:

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>

using namespace std;

bool subsetSumExists(const vector<int>& nums, int target) {
    int n = nums.size();
    int half = n / 2;
    
    // Preprocess first half
    unordered_set<int> sums1;
    for (int mask = 0; mask < (1 << half); ++mask) {
        int sum = 0;
        for (int i = 0; i < half; ++i) {
            if (mask & (1 << i)) {
                sum += nums[i];
            }
        }
        sums1.insert(sum);
    }
    
    // Preprocess second half
    unordered_set<int> sums2;
    for (int mask = 0; mask < (1 << (n - half)); ++mask) {
        int sum = 0;
        for (int i = 0; i < (n - half); ++i) {
            if (mask & (1 << i)) {
                sum += nums[half + i];
            }
        }
        sums2.insert(sum);
    }
    
    // Search for complement
    for (int sum : sums1) {
        if (sums2.count(target - sum) > 0) {
            return true;
        }
    }
    
    return false;
}

int main() {
    vector<int> nums = {3, 1, 7, 5, 9};
    int target = 10;
    
    if (subsetSumExists(nums, target)) {
        cout << "Subset with sum " << target << " exists." << endl;
    } else {
        cout << "No subset with sum " << target << " exists." << endl;
    }
    
    return 0;
}
```

This code demonstrates how to apply the "Meet in the Middle" technique to efficiently solve the subset sum problem. It divides the set of numbers into two halves, generates all possible subset sums for each half, and then searches for complements between the two halves to determine if a subset with the given sum exists.

### 1. Algorithms & Data Structures (C++): Path Compression

Path compression is a key optimization technique used in disjoint-set data structures, particularly in the context of union-find algorithms like disjoint-set forests. It's commonly employed to improve the efficiency of finding the representative (also known as the root) of a disjoint set.

In disjoint-set data structures, each element belongs to a set, and each set has a representative element. Path compression works by making every node on the path from a given node to its root point directly to the root. This process effectively shortens the paths within the tree-like structure of disjoint sets, leading to faster subsequent operations.

Here's how path compression typically works in a disjoint-set forest implemented using C++:

```cpp
#include <iostream>
#include <vector>

class DisjointSet {
private:
    std::vector<int> parent;

public:
    DisjointSet(int size) : parent(size) {
        for (int i = 0; i < size; ++i)
            parent[i] = i;
    }

    int find(int x) {
        if (parent[x] != x)
            parent[x] = find(parent[x]); // Path compression
        return parent[x];
    }

    void unionSets(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);
        if (rootX != rootY)
            parent[rootY] = rootX;
    }
};

int main() {
    DisjointSet ds(10); // Creating a disjoint set with 10 elements

    ds.unionSets(0, 1);
    ds.unionSets(2, 3);
    ds.unionSets(4, 5);
    ds.unionSets(6, 7);
    ds.unionSets(8, 9);

    // Before path compression
    std::cout << "Before path compression:\n";
    for (int i = 0; i < 10; ++i)
        std::cout << "Parent of " << i << ": " << ds.find(i) << "\n";

    // Perform path compression by calling find() on each element
    for (int i = 0; i < 10; ++i)
        ds.find(i);

    // After path compression
    std::cout << "\nAfter path compression:\n";
    for (int i = 0; i < 10; ++i)
        std::cout << "Parent of " << i << ": " << ds.find(i) << "\n";

    return 0;
}
```

In this example, `find(x)` method is responsible for path compressio

### 1. Algorithms & Data Structures (C++): Pattern Pre-Processing

Pattern pre-processing in algorithms and data structures involves optimizing patterns or data structures before they are used in operations like searching, matching, or any other relevant task. In the context of string matching algorithms like the Knuth-Morris-Pratt (KMP) algorithm or the Boyer-Moore algorithm, pre-processing often involves building auxiliary data structures or tables to accelerate the matching process.

In C++, pattern pre-processing can be implemented using various techniques depending on the problem requirements and constraints. Here are some common examples:

1. **Prefix Function (for KMP Algorithm)**:
   In the KMP algorithm, the prefix function is pre-processed from the pattern to determine the longest proper prefix that is also a suffix at each position in the pattern. This information helps in avoiding unnecessary comparisons during the string matching process.

2. **Bad Character and Good Suffix Heuristics (for Boyer-Moore Algorithm)**:
   In the Boyer-Moore algorithm, pre-processing involves generating tables that store information about the rightmost occurrence of each character in the pattern (bad character heuristic) and also information about the longest suffix of the pattern that matches a suffix of the text (good suffix heuristic). These tables are used to determine the shift distance during the matching process, improving the efficiency of the algorithm.

3. **Building Suffix Arrays or Suffix Trees**:
   Suffix arrays or suffix trees can be pre-processed from the input string to efficiently solve various string-related problems like substring search, longest common substring, etc. These data structures capture all the suffixes of the input string in a compact form, allowing for faster queries and operations.

4. **Trie Construction**:
   Tries are often pre-processed data structures used for efficient string storage and retrieval operations. They can be constructed from a set of strings beforehand and then queried efficiently during runtime.

5. **Hashing**:
   Pre-computing hash values of substrings or patterns can be useful for quick pattern matching using techniques like Rabin-Karp algorithm. Hash values can be computed for each substring of the text and compared against the hash value of the pattern, reducing the number of character comparisons needed.

These are just a few examples, and there are many other techniques for pattern pre-processing depending on the specific problem at hand. The goal is to perform any necessary computations or build necessary data structures beforehand to optimize the performance of subsequent operations.

### 1. Algorithms & Data Structures (C++): Patterns

Patterns in algorithms and data structures often refer to common solutions or approaches to solving particular problems. Here are some key patterns you might encounter:

1. **Divide and Conquer**: This pattern involves breaking a problem into smaller sub-problems, solving each sub-problem recursively, and then combining the solutions to solve the original problem. Examples include binary search, merge sort, and quicksort.

2. **Dynamic Programming**: In this pattern, solutions to sub-problems are memoized (stored) to avoid redundant computations. It's useful for optimization problems where solutions to larger problems depend on solutions to smaller problems. Examples include the Fibonacci sequence, shortest path problems, and knapsack problems.

3. **Greedy Algorithms**: Greedy algorithms make locally optimal choices at each step with the hope of finding a global optimum. They're usually efficient but might not always produce the best solution. Examples include Dijkstra's algorithm for finding the shortest path in a graph and the greedy activity selection algorithm.

4. **Backtracking**: Backtracking is a brute-force algorithmic technique that incrementally builds candidates for a solution and abandons a candidate ("backtracks") as soon as it determines that the candidate cannot possibly be completed to a valid solution. Examples include the N-Queens problem and Sudoku solver.

5. **Graph Algorithms**: Algorithms dealing with graphs, such as depth-first search (DFS) and breadth-first search (BFS), are crucial for solving various problems involving networks, connectivity, and shortest paths.

6. **Tree Algorithms**: This includes algorithms that operate on trees, such as tree traversal (pre-order, in-order, post-order), finding the lowest common ancestor (LCA), and building balanced trees (AVL trees, Red-Black trees).

7. **String Matching Algorithms**: These algorithms are designed to find occurrences or patterns within strings efficiently. Examples include the Knuth-Morris-Pratt (KMP) algorithm and the Boyer-Moore algorithm.

8. **Bit Manipulation**: Bit manipulation involves manipulating individual bits within a binary representation of data. This can be used for tasks such as bitwise AND, OR, XOR operations, setting or clearing specific bits, or checking parity.

9. **Hashing**: Hashing involves converting data into a fixed-size string of characters, typically for the purpose of indexing and rapid data retrieval. Hash tables are a common data structure based on hashing, offering constant-time average-case performance for insertions, deletions, and lookups.

10. **Parallel and Concurrent Algorithms**: With the advent of multi-core processors and distributed systems, algorithms designed to work efficiently in parallel or concurrent environments have become increasingly important. Examples include parallel sorting algorithms and concurrent data structures like concurrent queues and skip lists.

Understanding these patterns can help you recognize similarities between different problems and apply appropriate solutions effectively.n. It recursively traverses the tree structure from the given node `x` up to its root, and during this traversal, it makes each node encountered directly point to the root. This process optimizes future queries by making the trees flatter and reducing the time complexity of subsequent `find()` operations.

Path compression significantly improves the performance of operations on disjoint-set data structures, especially in scenarios where there are a lot of queries involving finding the representatives of elements.

### 1. Algorithms & Data Structures (C++): Problem with Linear Search

If you're encountering an issue with your linear search implementation in C++, there could be several reasons for it. Here's a basic implementation of linear search in C++:

```cpp
#include <iostream>
using namespace std;

// Function to perform linear search
int linearSearch(int arr[], int n, int key) {
    for (int i = 0; i < n; ++i) {
        if (arr[i] == key) {
            return i; // Return the index where key is found
        }
    }
    return -1; // Return -1 if key is not found
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int n = sizeof(arr) / sizeof(arr[0]);
    int key = 3;
    int result = linearSearch(arr, n, key);
    if (result != -1) {
        cout << "Element found at index " << result << endl;
    } else {
        cout << "Element not found" << endl;
    }
    return 0;
}
```

If you're encountering issues, here are some things to check:

1. **Incorrect array size**: Ensure that the size of the array you're passing to the linear search function (`n`) is correct. Using `sizeof(arr) / sizeof(arr[0])` as shown in the example above is a common way to find the size of the array in C++.

2. **Correct key**: Double-check that the key you're searching for is correct. If it's not found, the function will return -1.

3. **Array elements**: Make sure the elements in the array are in the order you expect. Linear search searches through the array sequentially, so if the array is not sorted, the key may not be found.

4. **Function call**: Ensure you're calling the `linearSearch` function with the correct arguments.

If you're still having issues, providing more details about the problem you're encountering can help in diagnosing the issue further.

### 1. Algorithms & Data Structures (C++): Quick Select

Quick select is an algorithm for finding the k-th smallest element in an unordered list. It's a variation of the quicksort algorithm, designed to select the k-th smallest element in expected linear time complexity.

Here's a basic outline of the Quick Select algorithm:

1. **Partitioning**: Just like in quicksort, you choose a pivot element and partition the array around it, such that elements less than the pivot are on its left, and elements greater are on its right.

2. **Selection**: Once the partitioning is done, you have three cases:
   - If the pivot's index is equal to k, then you've found the k-th smallest element, and you return it.
   - If the pivot's index is greater than k, then you recursively apply the algorithm to the left subarray.
   - If the pivot's index is less than k, then you recursively apply the algorithm to the right subarray, but you look for the (k - pivot's index - 1) smallest element in the right subarray.

This approach significantly reduces the average time complexity compared to sorting the entire array.

Here's a simple implementation in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high];
    int i = low - 1;
    for (int j = low; j < high; ++j) {
        if (arr[j] <= pivot) {
            ++i;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return i + 1;
}

int quickSelect(vector<int>& arr, int low, int high, int k) {
    if (low <= high) {
        int pivotIndex = partition(arr, low, high);
        if (pivotIndex == k) {
            return arr[pivotIndex];
        } else if (pivotIndex < k) {
            return quickSelect(arr, pivotIndex + 1, high, k);
        } else {
            return quickSelect(arr, low, pivotIndex - 1, k);
        }
    }
    return -1; // If k is out of bounds or array is empty
}

int main() {
    vector<int> arr = {7, 10, 4, 3, 20, 15};
    int k = 2; // Finding the 2nd smallest element
    int result = quickSelect(arr, 0, arr.size() - 1, k - 1);
    if (result != -1) {
        cout << "The " << k << "-th smallest element is: " << result << endl;
    } else {
        cout << "Invalid input" << endl;
    }
    return 0;
}
```

This implementation finds the k-th smallest element (0-based index), so if you want the k-th smallest element, you should pass k-1 as the argument to `quickSelect`.

### 1. Algorithms & Data Structures (C++): Rotated Search

The rotated search problem involves searching for a target element in a sorted array that has been rotated an unknown number of times. For example, the array [4, 5, 6, 7, 0, 1, 2] has been rotated twice to the right.

Here's a C++ implementation of a binary search algorithm to find the index of a target element in a rotated sorted array:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int search(const vector<int>& nums, int target) {
    int left = 0;
    int right = nums.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (nums[mid] == target)
            return mid;

        // Check if the left half is sorted
        if (nums[left] <= nums[mid]) {
            // Check if the target is within the left half
            if (nums[left] <= target && target < nums[mid])
                right = mid - 1;
            else
                left = mid + 1;
        } else { // Right half is sorted
            // Check if the target is within the right half
            if (nums[mid] < target && target <= nums[right])
                left = mid + 1;
            else
                right = mid - 1;
        }
    }
    return -1; // Target not found
}

int main() {
    vector<int> nums = {4, 5, 6, 7, 0, 1, 2};
    int target = 0;
    int index = search(nums, target);
    if (index != -1)
        cout << "Target " << target << " found at index " << index << endl;
    else
        cout << "Target " << target << " not found in the array." << endl;
    return 0;
}
```

This algorithm has a time complexity of O(log n), where n is the number of elements in the array, because it uses a binary search approach.

### 1. Algorithms & Data Structures (C++): Runner Technique

The "Runner Technique" is a common approach used in algorithms and data structures, especially in scenarios involving linked lists. It involves using two pointers that traverse the data structure at different speeds, often one faster than the other. This technique is useful for solving problems related to cycle detection, finding the midpoint of a list, and more.

In the context of linked lists, here's a brief explanation of how the Runner Technique works:

1. **Slow Runner:** One pointer moves through the list node by node.
2. **Fast Runner:** Another pointer moves through the list at a faster pace, typically advancing two or more steps at a time.

By utilizing these two pointers in tandem, you can achieve various tasks efficiently. For example:

- **Cycle Detection:** If there's a cycle in a linked list, the fast runner will eventually meet the slow runner at some point within the cycle.
- **Finding Midpoint:** The slow runner moves one step at a time, while the fast runner moves two steps at a time. When the fast runner reaches the end of the list, the slow runner will be at the midpoint.

Here's a simple example in C++ demonstrating how you might use the Runner Technique to find the midpoint of a linked list:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* next;
    Node(int value) : data(value), next(nullptr) {}
};

Node* findMidpoint(Node* head) {
    if (head == nullptr)
        return nullptr;

    Node* slow = head;
    Node* fast = head;

    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;          // Move slow pointer one step
        fast = fast->next->next;    // Move fast pointer two steps
    }

    return slow;
}

int main() {
    // Creating a sample linked list: 1 -> 2 -> 3 -> 4 -> 5
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->next = new Node(3);
    head->next->next->next = new Node(4);
    head->next->next->next->next = new Node(5);

    Node* midpoint = findMidpoint(head);
    if (midpoint != nullptr) {
        std::cout << "Midpoint of the list is: " << midpoint->data << std::endl;
    } else {
        std::cout << "List is empty." << std::endl;
    }

    // Clean up memory (not shown in many examples but essential)
    while (head != nullptr) {
        Node* temp = head;
        head = head->next;
        delete temp;
    }

    return 0;
}
```

This code will output "Midpoint of the list is: 3", demonstrating the Runner Technique in action.

### 1. Algorithms & Data Structures (C++): Running Median

Implementing a running median algorithm involves continuously calculating the median of a stream of numbers as they arrive or change. One common approach is to use two heaps, a max-heap and a min-heap, to maintain the lower and upper halves of the sorted data respectively. This allows for efficient access to the middle elements.

Here's a basic implementation of a running median in C++ using two priority queues:

```cpp
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

class RunningMedian {
private:
    priority_queue<int> maxHeap; // Stores the smaller half of the numbers
    priority_queue<int, vector<int>, greater<int>> minHeap; // Stores the larger half of the numbers

public:
    void insert(int num) {
        if (maxHeap.empty() || num <= maxHeap.top()) {
            maxHeap.push(num);
        } else {
            minHeap.push(num);
        }

        // Balance the heaps
        if (maxHeap.size() > minHeap.size() + 1) {
            minHeap.push(maxHeap.top());
            maxHeap.pop();
        } else if (minHeap.size() > maxHeap.size() + 1) {
            maxHeap.push(minHeap.top());
            minHeap.pop();
        }
    }

    double getMedian() const {
        if (maxHeap.size() == minHeap.size()) {
            return (maxHeap.top() + minHeap.top()) / 2.0;
        } else if (maxHeap.size() > minHeap.size()) {
            return maxHeap.top();
        } else {
            return minHeap.top();
        }
    }
};

int main() {
    RunningMedian rm;
    vector<int> nums = {2, 5, 1, 7, 3, 6, 8, 4};

    cout << "Running Medians: ";
    for (int num : nums) {
        rm.insert(num);
        cout << rm.getMedian() << " ";
    }
    cout << endl;

    return 0;
}
```

In this implementation, we use a max-heap (`priority_queue`) to store the smaller half of the numbers and a min-heap to store the larger half. We balance the heaps such that the size difference between them is at most 1. Then, the median can be found by either taking the average of the top elements of both heaps or by simply taking the top element of the heap with the larger size.

### 1. Algorithms & Data Structures (C++): Running Median Class

Creating a running median class involves maintaining a data structure that efficiently updates the median as new elements are added or removed from a sequence of numbers. One common approach is to use two heaps: a max-heap to store the smaller half of the numbers and a min-heap to store the larger half.

Here's a basic implementation of a running median class in C++ using two priority queues:

```cpp
#include <queue>
#include <vector>
#include <functional>

class RunningMedian {
private:
    std::priority_queue<int, std::vector<int>, std::less<int>> maxHeap; // max heap for the smaller half
    std::priority_queue<int, std::vector<int>, std::greater<int>> minHeap; // min heap for the larger half

public:
    void insert(int num) {
        if (maxHeap.empty() || num <= maxHeap.top()) {
            maxHeap.push(num);
        } else {
            minHeap.push(num);
        }

        // Rebalance the heaps if necessary
        if (maxHeap.size() > minHeap.size() + 1) {
            minHeap.push(maxHeap.top());
            maxHeap.pop();
        } else if (minHeap.size() > maxHeap.size()) {
            maxHeap.push(minHeap.top());
            minHeap.pop();
        }
    }

    double getMedian() const {
        if (maxHeap.size() == minHeap.size()) {
            return (maxHeap.top() + minHeap.top()) / 2.0;
        } else {
            return maxHeap.top();
        }
    }
};
```

You can use this class like so:

```cpp
#include <iostream>

int main() {
    RunningMedian rm;

    rm.insert(5);
    std::cout << "Median: " << rm.getMedian() << std::endl; // Output: 5.0

    rm.insert(10);
    std::cout << "Median: " << rm.getMedian() << std::endl; // Output: 7.5

    rm.insert(2);
    std::cout << "Median: " << rm.getMedian() << std::endl; // Output: 5.0

    rm.insert(15);
    std::cout << "Median: " << rm.getMedian() << std::endl; // Output: 7.5

    return 0;
}
```

This implementation ensures that the median can be retrieved in constant time and that the heaps remain balanced as elements are inserted.

### 1. Algorithms & Data Structures (C++): Search

Sure, searching algorithms in computer science are crucial for finding specific elements within a collection of data efficiently. Here's an overview of some common searching algorithms in C++:

1. **Linear Search**:
   - It sequentially checks each element of the list until a match is found or the whole list has been searched.
   - Implementation in C++:

   ```cpp
   int linearSearch(int arr[], int n, int x) {
       for (int i = 0; i < n; i++) {
           if (arr[i] == x) {
               return i; // Element found at index i
           }
       }
       return -1; // Element not found
   }
   ```

2. **Binary Search**:
   - Requires the input list to be sorted.
   - It repeatedly divides the search interval in half until the target element is found or the interval is empty.
   - Implementation in C++:

   ```cpp
   int binarySearch(int arr[], int left, int right, int x) {
       while (left <= right) {
           int mid = left + (right - left) / 2;
           if (arr[mid] == x) {
               return mid; // Element found at index mid
           }
           if (arr[mid] < x) {
               left = mid + 1; // Search in the right half
           } else {
               right = mid - 1; // Search in the left half
           }
       }
       return -1; // Element not found
   }
   ```

3. **Interpolation Search**:
   - An improvement over binary search for uniformly distributed sorted arrays.
   - It calculates the probable position of the target element based on its value and the range of values in the array.
   - Implementation in C++:

   ```cpp
   int interpolationSearch(int arr[], int n, int x) {
       int low = 0, high = n - 1;
       while (low <= high && x >= arr[low] && x <= arr[high]) {
           int pos = low + ((double)(high - low) / (arr[high] - arr[low])) * (x - arr[low]);
           if (arr[pos] == x) {
               return pos; // Element found at index pos
           }
           if (arr[pos] < x) {
               low = pos + 1; // Search in the right half
           } else {
               high = pos - 1; // Search in the left half
           }
       }
       return -1; // Element not found
   }
   ```

4. **Hashing (using Hash Tables)**:
   - It involves mapping keys to specific positions in a data structure called a hash table.
   - Efficient for searching, inserting, and deleting operations, with an average time complexity of O(1).
   - Implementation in C++ using `std::unordered_map`:

   ```cpp
   #include <unordered_map>
   #include <iostream>
   
   int main() {
       std::unordered_map<int, std::string> hashTable;
       // Inserting elements into the hash table
       hashTable[1] = "One";
       hashTable[2] = "Two";
       hashTable[3] = "Three";

       // Searching for an element
       int key = 2;
       if (hashTable.find(key) != hashTable.end()) {
           std::cout << "Element found: " << hashTable[key] << std::endl;
       } else {
           std::cout << "Element not found" << std::endl;
       }

       return 0;
   }
   ```

These are some of the common searching algorithms used in C++. Each has its advantages and use cases depending on the nature of the data and the specific requirements of the problem.

### 1. Algorithms & Data Structures (C++): Search Algorithms

Sure, let's discuss some common search algorithms in C++. Here are a few:

1. **Linear Search**:
   - It sequentially checks each element of the list until a match is found or the whole list has been searched.
   - Time complexity: O(n), where n is the number of elements in the list.

   ```cpp
   int linearSearch(int arr[], int n, int target) {
       for (int i = 0; i < n; ++i) {
           if (arr[i] == target)
               return i;  // Return the index if target is found
       }
       return -1; // Return -1 if target is not found
   }
   ```

2. **Binary Search**:
   - It requires that the elements of the list are sorted.
   - It repeatedly divides in half the portion of the list that could contain the target value, until it narrows down to the target.
   - Time complexity: O(log n), where n is the number of elements in the list.

   ```cpp
   int binarySearch(int arr[], int n, int target) {
       int left = 0, right = n - 1;
       while (left <= right) {
           int mid = left + (right - left) / 2;
           if (arr[mid] == target)
               return mid;
           else if (arr[mid] < target)
               left = mid + 1;
           else
               right = mid - 1;
       }
       return -1; // Return -1 if target is not found
   }
   ```

3. **Ternary Search**:
   - It is similar to binary search but divides the array into three parts instead of two.
   - Time complexity: O(log3 n).

   ```cpp
   int ternarySearch(int arr[], int left, int right, int target) {
       if (right >= left) {
           int mid1 = left + (right - left) / 3;
           int mid2 = right - (right - left) / 3;

           if (arr[mid1] == target)
               return mid1;
           if (arr[mid2] == target)
               return mid2;

           if (target < arr[mid1])
               return ternarySearch(arr, left, mid1 - 1, target);
           else if (target > arr[mid2])
               return ternarySearch(arr, mid2 + 1, right, target);
           else
               return ternarySearch(arr, mid1 + 1, mid2 - 1, target);
       }
       return -1; // Return -1 if target is not found
   }
   ```

These are just a few examples of search algorithms in C++. Depending on the specific problem and constraints, other algorithms or variations of these algorithms might be more appropriate.

### 1. Algorithms & Data Structures (C++): Search Algorithms: Binary search implementation

Sure, here's a basic implementation of the binary search algorithm in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Binary search function
int binarySearch(vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        // If the element is present at the middle
        if (arr[mid] == target)
            return mid;

        // If target is greater, ignore left half
        if (arr[mid] < target)
            left = mid + 1;

        // If target is smaller, ignore right half
        else
            right = mid - 1;
    }

    // If the element is not present in the array
    return -1;
}

// Example usage
int main() {
    vector<int> arr = {1, 3, 5, 7, 9, 11, 13, 15, 17, 19};
    int target = 11;
    int result = binarySearch(arr, target);
    if (result != -1)
        cout << "Element found at index " << result << endl;
    else
        cout << "Element not found in the array" << endl;

    return 0;
}
```

In this implementation, the `binarySearch` function takes a sorted vector of integers `arr` and the target value `target` to search for. It returns the index of the target if found, otherwise, it returns -1.

The algorithm starts with defining two pointers, `left` and `right`, which represent the range in which the target could be located. It iteratively narrows down this range by halving it at each step and comparing the target with the middle element of the current range. Depending on whether the target is greater or smaller than the middle element, the algorithm discards one half of the range and continues the search in the other half.

The `main` function demonstrates how to use the `binarySearch` function with an example array and target value.

### 1. Algorithms & Data Structures (C++): Search Algorithms: What is binary (logarithmic) search?

Binary search, also known as logarithmic search, is a search algorithm used to find the position of a target value within a sorted array. It works by repeatedly dividing the search interval in half. Here's how it works:

1. **Initialization**: Begin with the entire array.

2. **Compare**: Check the middle element of the array.

3. **Divide**: If the middle element is the target value, the search is complete. If not, compare the target value with the middle element. If the target value is less than the middle element, search the left half of the array. Otherwise, search the right half.

4. **Repeat**: Continue this process recursively on the selected half until the target value is found or the search interval is empty.

Binary search has a time complexity of O(log n), where n is the number of elements in the array. This is because with each iteration, the search space is halved, leading to a logarithmic growth rate.

It's important to note that binary search requires the array to be sorted in ascending or descending order beforehand. If the array is not sorted, binary search cannot guarantee correct results. Additionally, binary search is most efficient for large arrays where the cost of sorting is outweighed by the benefit of fast searches.

### 1. Algorithms & Data Structures (C++): Search All

In C++, there are various algorithms and data structures that you can utilize for searching. Here's an overview of some commonly used ones:

#### Algorithms

1. **Linear Search**:
   - Simplest form of searching.
   - Traverse the array sequentially until the desired element is found.
   - Time complexity: O(n) in the worst case.

2. **Binary Search**:
   - Applicable only to sorted arrays.
   - Divide and conquer approach.
   - Time complexity: O(log n) in the worst case.

3. **Hashing**:
   - Utilizes a hash function to map keys to their associated values in a hash table.
   - Provides constant time complexity on average for search operations (O(1)).

#### Data Structures

1. **Arrays**:
   - Simplest data structure for storing elements.
   - Suitable for linear search.

2. **Linked Lists**:
   - Consist of nodes where each node points to the next node in the sequence.
   - Suitable for linear search.
   - Time complexity for search: O(n).

3. **Binary Search Trees (BST)**:
   - A binary tree in which each node has at most two children.
   - Left child nodes have smaller values and right child nodes have larger values.
   - Suitable for binary search.
   - Average time complexity for search: O(log n) in balanced trees; worst-case time complexity: O(n) in degenerate trees.

4. **Hash Tables**:
   - Utilizes a hash function to map keys to their associated values.
   - Provides constant time complexity for search operations on average (O(1)).

#### Example (Binary Search)

```cpp
#include <iostream>
#include <vector>

// Function for binary search
int binarySearch(std::vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (arr[mid] == target) {
            return mid; // Element found
        } else if (arr[mid] < target) {
            left = mid + 1; // Search right half
        } else {
            right = mid - 1; // Search left half
        }
    }

    return -1; // Element not found
}

// Example usage
int main() {
    std::vector<int> arr = {2, 5, 8, 12, 16, 23, 38, 56, 72, 91};
    int target = 23;
    int index = binarySearch(arr, target);
    if (index != -1) {
        std::cout << "Element found at index " << index << std::endl;
    } else {
        std::cout << "Element not found" << std::endl;
    }
    return 0;
}
```

This code demonstrates a binary search on a sorted vector.

### 1. Algorithms & Data Structures (C++): Searching

Searching algorithms are fundamental to computer science and are used to find elements within a collection of data. In C++, there are several common searching algorithms, each with its own advantages and use cases. Here are some of the most frequently used searching algorithms:

1. **Linear Search**: This is the simplest searching algorithm that sequentially checks each element of the data structure until the desired element is found or the end of the data structure is reached. Linear search works well for small datasets but can be inefficient for large datasets.

    ```cpp
    int linearSearch(int arr[], int n, int key) {
        for (int i = 0; i < n; i++) {
            if (arr[i] == key)
                return i; // Return the index if element is found
        }
        return -1; // Return -1 if element is not found
    }
    ```

2. **Binary Search**: This is a more efficient searching algorithm applicable only to sorted arrays. It works by repeatedly dividing the search interval in half until the value is found or the interval is empty. Binary search has a time complexity of O(log n).

    ```cpp
    int binarySearch(int arr[], int left, int right, int key) {
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (arr[mid] == key)
                return mid; // Return index if element is found
            if (arr[mid] < key)
                left = mid + 1; // Continue searching in the right half
            else
                right = mid - 1; // Continue searching in the left half
        }
        return -1; // Return -1 if element is not found
    }
    ```

3. **Interpolation Search**: This is an improved version of binary search for uniformly distributed sorted arrays. Instead of always dividing the search interval in half, interpolation search uses a formula to guess the position of the key based on its value. It has an average time complexity of O(log log n) if the elements are uniformly distributed.

4. **Ternary Search**: Ternary search is a divide-and-conquer algorithm similar to binary search but divides the search interval into three parts instead of two. It requires that the data structure should be sorted and is suitable for finding an element in unimodal functions (functions that are initially increasing and then decreasing, or vice versa).

5. **Hashing**: Hashing is a technique that maps keys of a certain type to values of another type, allowing for efficient retrieval of data. In C++, this is commonly implemented using the unordered_map or unordered_set containers from the C++ Standard Library.

These are some of the basic searching algorithms in C++. Depending on the specific requirements of your problem, you might choose one algorithm over another to achieve the desired efficiency and performance.

### 1. Algorithms & Data Structures (C++): Searching & Sorting

Certainly! Algorithms and data structures are fundamental concepts in computer science and software development. Let's delve into some common searching and sorting algorithms in C++.

### Searching Algorithms

#### 1. Linear Search

- **Description**: Linear search iterates through each element in a collection until the target element is found or the end of the collection is reached.
- **Time Complexity**: O(n) in the worst-case scenario.

   ```cpp
   int linearSearch(int arr[], int n, int target) {
       for (int i = 0; i < n; ++i) {
           if (arr[i] == target)
               return i; // Return index of target if found
       }
       return -1; // Return -1 if target not found
   }
   ```

#### 2. Binary Search

- **Description**: Binary search requires a sorted array and divides the search interval in half at each step.
- **Time Complexity**: O(log n) in the worst-case scenario.

   ```cpp
   int binarySearch(int arr[], int left, int right, int target) {
       while (left <= right) {
           int mid = left + (right - left) / 2;
           if (arr[mid] == target)
               return mid; // Return index of target if found
           if (arr[mid] < target)
               left = mid + 1;
           else
               right = mid - 1;
       }
       return -1; // Return -1 if target not found
   }
   ```

### Sorting Algorithms

#### 1. Bubble Sort

- **Description**: Bubble sort repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order.
- **Time Complexity**: O(n^2) in the worst-case scenario.

   ```cpp
   void bubbleSort(int arr[], int n) {
       for (int i = 0; i < n - 1; ++i) {
           for (int j = 0; j < n - i - 1; ++j) {
               if (arr[j] > arr[j + 1]) {
                   // Swap arr[j] and arr[j + 1]
                   int temp = arr[j];
                   arr[j] = arr[j + 1];
                   arr[j + 1] = temp;
               }
           }
       }
   }
   ```

#### 2. Merge Sort

- **Description**: Merge sort divides the array into two halves, sorts each half, and then merges them back together.
- **Time Complexity**: O(n log n) in all cases.

   ```cpp
   void merge(int arr[], int left, int mid, int right) {
       int n1 = mid - left + 1;
       int n2 = right - mid;

       // Create temporary arrays
       int L[n1], R[n2];
       for (int i = 0; i < n1; ++i)
           L[i] = arr[left + i];
       for (int j = 0; j < n2; ++j)
           R[j] = arr[mid + 1 + j];

       // Merge the temporary arrays back into arr[left..right]
       int i = 0, j = 0, k = left;
       while (i < n1 && j < n2) {
           if (L[i] <= R[j])
               arr[k++] = L[i++];
           else
               arr[k++] = R[j++];
       }

       // Copy the remaining elements of L[] and R[], if any
       while (i < n1)
           arr[k++] = L[i++];
       while (j < n2)
           arr[k++] = R[j++];
   }

   void mergeSort(int arr[], int left, int right) {
       if (left < right) {
           int mid = left + (right - left) / 2;

           // Sort first and second halves
           mergeSort(arr, left, mid);
           mergeSort(arr, mid + 1, right);

           // Merge the sorted halves
           merge(arr, left, mid, right);
       }
   }
   ```

These are just a few examples of searching and sorting algorithms in C++. There are many more algorithms out there, each with its own characteristics and use cases.

### 1. Algorithms & Data Structures (C++): Searching + Traversal

Certainly! In C++, there are various algorithms and data structures commonly used for searching and traversal. Here's a brief overview of some of them:

### Searching Algorithms

1. **Linear Search:**
   - Simplest searching algorithm that sequentially checks each element until the desired element is found or the end of the array is reached.
   - Time Complexity: O(n) where n is the number of elements in the array.

2. **Binary Search:**
   - Requires the array to be sorted.
   - Divides the array into halves and eliminates the half in which the target cannot lie.
   - Time Complexity: O(log n) where n is the number of elements in the array.

3. **Hashing:**
   - Utilizes a hash function to map keys to indices in a data structure called a hash table.
   - Provides constant-time average-case performance for insertion, deletion, and retrieval of elements.
   - Common hash table implementations include unordered_map and unordered_set in C++.

### Tree Traversal

1. **Depth-First Traversal:**
   - In-order traversal: Left subtree, root, right subtree.
   - Pre-order traversal: Root, left subtree, right subtree.
   - Post-order traversal: Left subtree, right subtree, root.

2. **Breadth-First Traversal:**
   - Also known as level-order traversal.
   - Visits all nodes of a level before going to the next level.

### Graph Traversal

1. **Depth-First Search (DFS):**
   - Visits nodes in depthward motion.
   - Uses a stack (or recursion) to keep track of vertices.
   - Suitable for topological sorting, connected components, and detecting cycles.

2. **Breadth-First Search (BFS):**
   - Visits nodes in breadthward motion.
   - Uses a queue to keep track of vertices.
   - Suitable for finding shortest paths and connected components.

### C++ Implementations

Here's a simple example of binary search in C++:

```cpp
#include <iostream>
#include <vector>

int binarySearch(const std::vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;
        
        if (arr[mid] == target)
            return mid;
        else if (arr[mid] < target)
            left = mid + 1;
        else
            right = mid - 1;
    }

    return -1; // Not found
}

int main() {
    std::vector<int> arr = {2, 3, 5, 7, 11, 13, 17, 19, 23, 29};
    int target = 13;

    int index = binarySearch(arr, target);
    if (index != -1)
        std::cout << "Element found at index " << index << std::endl;
    else
        std::cout << "Element not found" << std::endl;

    return 0;
}
```

For tree and graph traversal, you would need to have appropriate data structures like binary trees, graphs, etc., and implement the traversal algorithms accordingly. Let me know if you need more examples or details on any specific algorithm!

### 1. Algorithms & Data Structures (C++): Searching Algorithms

Sure, here's an overview of some common searching algorithms in C++:

1. **Linear Search**:
   - This is the simplest searching algorithm that iterates through each element in the array until the desired element is found.
   - Time complexity: O(n) in the worst case.

```cpp
int linearSearch(int arr[], int n, int key) {
    for (int i = 0; i < n; i++) {
        if (arr[i] == key)
            return i;  // Return the index if found
    }
    return -1;  // Return -1 if not found
}
```

1. **Binary Search**:
   - Works on sorted arrays by repeatedly dividing the search interval in half until the element is found or the interval is empty.
   - Requires a sorted array.
   - Time complexity: O(log n) in the worst case.

```cpp
int binarySearch(int arr[], int left, int right, int key) {
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == key)
            return mid;  // Return the index if found
        if (arr[mid] < key)
            left = mid + 1;
        else
            right = mid - 1;
    }
    return -1;  // Return -1 if not found
}
```

1. **Interpolation Search**:
   - An improvement over binary search for uniformly distributed arrays.
   - Instead of dividing the search space in half, it uses a formula to approximate the position of the target element.
   - Time complexity: O(log log n) on average.

```cpp
int interpolationSearch(int arr[], int n, int key) {
    int low = 0, high = n - 1;
    while (low <= high && key >= arr[low] && key <= arr[high]) {
        int pos = low + ((double)(high - low) / (arr[high] - arr[low])) * (key - arr[low]);
        if (arr[pos] == key)
            return pos;
        if (arr[pos] < key)
            low = pos + 1;
        else
            high = pos - 1;
    }
    return -1;  // Return -1 if not found
}
```

These are some of the basic searching algorithms in C++. Depending on the scenario and requirements, other algorithms like ternary search, exponential search, etc., can also be used.

### 1. Algorithms & Data Structures (C++): Selections

Sure, let's delve into algorithms and data structures in C++ focusing on selection algorithms.

#### Selection Algorithms

Selection algorithms are used to find the kth smallest or largest element in an array or sequence. Here are a few commonly used selection algorithms:

1. **Selection Sort**:
   - Although primarily a sorting algorithm, it can be modified to find the kth smallest or largest element by performing only the necessary number of iterations.

2. **Quickselect**:
   - This is an efficient algorithm based on the partitioning technique used in Quicksort. It selects the kth element in expected linear time O(n), where n is the number of elements.

3. **Heapselect**:
   - This algorithm utilizes the properties of heaps to find the kth smallest or largest element in linear time. It maintains a min-heap for finding the kth largest element or a max-heap for finding the kth smallest element.

#### Implementation Example (Quickselect)

Here's a simple implementation of the Quickselect algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high];
    int i = low - 1;

    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return i + 1;
}

int quickselect(vector<int>& arr, int low, int high, int k) {
    if (low <= high) {
        int pivotIndex = partition(arr, low, high);
        if (pivotIndex == k) {
            return arr[pivotIndex];
        } else if (pivotIndex < k) {
            return quickselect(arr, pivotIndex + 1, high, k);
        } else {
            return quickselect(arr, low, pivotIndex - 1, k);
        }
    }
    return -1; // Error case
}

int main() {
    vector<int> arr = {7, 10, 4, 3, 20, 15};
    int k = 3; // Find the 3rd smallest element

    int result = quickselect(arr, 0, arr.size() - 1, k - 1);
    if (result != -1)
        cout << "The " << k << "th smallest element is: " << result << endl;
    else
        cout << "Invalid input or k out of range." << endl;

    return 0;
}
```

This code snippet demonstrates the Quickselect algorithm to find the kth smallest element in an array.

### 1. Algorithms & Data Structures (C++): Sequential Search

Sequential search, also known as linear search, is a simple algorithm for finding a target value within a list. It sequentially checks each element of the list until a match is found or the entire list has been searched. Here's a basic implementation of sequential search in C++:

```cpp
#include <iostream>
#include <vector>

// Function to perform sequential search
int sequentialSearch(const std::vector<int>& arr, int target) {
    for (int i = 0; i < arr.size(); ++i) {
        if (arr[i] == target) {
            return i; // Return index of the target if found
        }
    }
    return -1; // Return -1 if target is not found
}

int main() {
    std::vector<int> data = {10, 5, 7, 3, 8, 2};
    int target = 8;

    int index = sequentialSearch(data, target);

    if (index != -1) {
        std::cout << "Target found at index " << index << std::endl;
    } else {
        std::cout << "Target not found" << std::endl;
    }

    return 0;
}
```

In this implementation:

- `sequentialSearch` function takes a vector `arr` and an integer `target` as input parameters.
- It iterates through each element of the vector using a `for` loop.
- Inside the loop, it checks if the current element is equal to the target value. If it finds a match, it returns the index of that element.
- If no match is found after iterating through the entire vector, it returns -1 to indicate that the target value is not present in the vector.
- In the `main` function, we create a vector `data` containing some integers and specify a `target` value to search for.
- We call the `sequentialSearch` function with the `data` vector and `target` value and store the result in the `index` variable.
- Finally, we check if the `index` returned by the `sequentialSearch` function is not equal to -1, indicating that the target was found, and display the index. Otherwise, we print that the target was not found.

Sequential search has a time complexity of O(n), where n is the number of elements in the list. It's straightforward and easy to implement, but not very efficient for large lists compared to more advanced search algorithms like binary search on sorted lists.

### 1. Algorithms & Data Structures (C++): Sliding Window

In computer science, a sliding window is a technique used to perform a series of operations on a specific window or sub-array of a larger array or string. It's particularly useful for solving problems involving strings, arrays, or other sequential data structures. The sliding window technique typically involves maintaining a set of elements within a fixed-size window that moves through the given data structure.

Here's an overview of how the sliding window technique works:

1. **Initialize:** Set up the initial window by defining its size and positioning it at the beginning of the array or string.

2. **Process:** Perform operations on the elements within the window.

3. **Slide:** Move the window by one position (either to the right or left, depending on the problem requirements).

4. **Repeat:** Repeat steps 2 and 3 until the window reaches the end of the array or string.

This technique is often used to efficiently solve problems that involve finding subarrays or substrings with certain properties (e.g., maximum sum, minimum length, distinct elements, etc.). By using a sliding window, you can reduce the time complexity of the solution from O(n^2) to O(n) or even O(n log n) in some cases.

Let's illustrate this with an example problem and its solution using the sliding window technique:

**Problem:** Given an array of integers and a target sum, find the length of the shortest contiguous subarray whose sum is at least the target sum.

**Solution:**

```cpp
#include <iostream>
#include <vector>

using namespace std;

int minSubArrayLen(int target, vector<int>& nums) {
    int n = nums.size();
    int minLength = INT_MAX;
    int windowSum = 0;
    int windowStart = 0;

    for (int windowEnd = 0; windowEnd < n; ++windowEnd) {
        windowSum += nums[windowEnd]; // Expand the window
        while (windowSum >= target) {
            minLength = min(minLength, windowEnd - windowStart + 1); // Update the minimum length
            windowSum -= nums[windowStart]; // Shrink the window
            ++windowStart;
        }
    }

    return (minLength == INT_MAX) ? 0 : minLength;
}

int main() {
    vector<int> nums = {2, 3, 1, 2, 4, 3};
    int target = 7;
    cout << "Length of the shortest subarray with sum at least " << target << ": " << minSubArrayLen(target, nums) << endl;
    return 0;
}
```

In this solution, we use two pointers `windowStart` and `windowEnd` to define the sliding window. We expand the window by moving `windowEnd` forward and shrink it by moving `windowStart` forward. We update the minimum length of the subarray that meets the condition as the window slides through the array.

### 1. Algorithms & Data Structures (C++): Sliding Window Housing (Two Pointer)

The sliding window technique is a common algorithmic pattern used to solve problems involving arrays or strings. It's particularly useful when you need to find a substring, subarray, or some other contiguous segment that satisfies certain constraints.

Here's a basic outline of how you might implement a sliding window algorithm in C++ to solve a housing problem, using two pointers:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to solve the housing problem using sliding window technique
int maxHousesWithinBudget(vector<int>& houses, int budget) {
    int maxHouses = 0;
    int windowSum = 0;
    int windowStart = 0;

    for (int windowEnd = 0; windowEnd < houses.size(); ++windowEnd) {
        // Expand the window by including the current house
        windowSum += houses[windowEnd];

        // Shrink the window if the current window sum exceeds the budget
        while (windowSum > budget) {
            windowSum -= houses[windowStart];
            windowStart++;
        }

        // Update the maximum number of houses if the current window is better
        maxHouses = max(maxHouses, windowEnd - windowStart + 1);
    }

    return maxHouses;
}

int main() {
    // Example usage
    vector<int> houses = {1, 3, 2, 1, 4, 5, 3, 2};
    int budget = 8;

    int maxHouses = maxHousesWithinBudget(houses, budget);
    cout << "Maximum number of houses within budget: " << maxHouses << endl;

    return 0;
}
```

In this example, the function `maxHousesWithinBudget` takes a vector representing the prices of houses and a budget as input, and it returns the maximum number of houses that can be bought within the budget. The sliding window is maintained between the `windowStart` and `windowEnd` indices. The `windowSum` variable keeps track of the sum of prices within the current window.

As you iterate through the array of house prices (`houses`), you continuously expand the window by including houses until the sum of prices within the window exceeds the budget. When this happens, you shrink the window by moving the `windowStart` pointer forward until the sum falls within the budget again.

Finally, you update the `maxHouses` variable to keep track of the maximum number of houses that can be bought within the budget.

### 1. Algorithms & Data Structures (C++): Sliding Window Implementation

Implementing a sliding window algorithm in C++ involves defining a window of a certain size that moves through an array or a string, performing operations or calculations within that window at each step. Here's a basic example of a sliding window algorithm to find the maximum sum subarray of a fixed size `k` within an array:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int maxSumSubarray(const vector<int>& nums, int k) {
    int n = nums.size();
    if (n < k || k <= 0)
        return -1; // Invalid input

    int windowSum = 0;
    for (int i = 0; i < k; i++) {
        windowSum += nums[i];
    }

    int maxSum = windowSum;
    for (int i = k; i < n; i++) {
        windowSum += nums[i] - nums[i - k];
        maxSum = max(maxSum, windowSum);
    }

    return maxSum;
}

int main() {
    vector<int> nums = {1, 3, -1, -3, 5, 3, 6, 7};
    int k = 3;
    int maxSum = maxSumSubarray(nums, k);
    cout << "Maximum sum of subarray of size " << k << ": " << maxSum << endl;

    return 0;
}
```

This code defines a function `maxSumSubarray` that takes a vector of integers `nums` and an integer `k` as input. It calculates the maximum sum of a subarray of size `k` using a sliding window approach.

Here's how the sliding window works:

1. We initialize `windowSum` to the sum of the first `k` elements of the array.
2. Then, we iterate through the array starting from the (`k+1`)th element.
3. At each step, we subtract the leftmost element of the current window and add the rightmost element to maintain the window size `k`.
4. We update `maxSum` whenever we find a greater sum within the window.
5. Finally, we return `maxSum` which holds the maximum sum of a subarray of size `k`.

You can modify this code to perform other operations within the sliding window, such as finding the maximum/minimum value, counting elements, or solving different problems altogether.

### 1. Algorithms & Data Structures (C++): Sliding Window Maximum

The sliding window maximum problem is a classic algorithmic problem where you're given an array of integers and a window of a fixed size which slides through the array. At each step, you need to find the maximum element within the window. This problem can be efficiently solved using a data structure like a deque (double-ended queue).

Here's a C++ implementation of the sliding window maximum problem using a deque:

```cpp
#include <iostream>
#include <vector>
#include <deque>

using namespace std;

vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    vector<int> result;
    deque<int> window;

    for (int i = 0; i < nums.size(); ++i) {
        // Remove elements outside the window
        while (!window.empty() && window.front() < i - k + 1) {
            window.pop_front();
        }
        
        // Remove smaller elements from the back
        while (!window.empty() && nums[window.back()] < nums[i]) {
            window.pop_back();
        }
        
        // Add current element to the window
        window.push_back(i);
        
        // Add maximum of the current window to result
        if (i >= k - 1) {
            result.push_back(nums[window.front()]);
        }
    }

    return result;
}

int main() {
    vector<int> nums = {1, 3, -1, -3, 5, 3, 6, 7};
    int k = 3;
    vector<int> result = maxSlidingWindow(nums, k);

    cout << "Maximums in sliding windows of size " << k << " are: ";
    for (int num : result) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}
```

This code maintains a deque `window` to store indices of elements within the current window. At each step, it updates the deque to maintain only the relevant elements for the current window, ensuring that the front of the deque always holds the maximum element's index.

### 1. Algorithms & Data Structures (C++): Sliding Window Maximum - Queue

Sure, the sliding window maximum problem is a classic problem in computer science where you are given an array of integers and a window of a certain size which slides from left to right through the array. At each step, you need to find the maximum value in the window. One efficient way to solve this problem is by using a data structure called a deque (double-ended queue).

Here's a C++ implementation of the sliding window maximum using a deque:

```cpp
#include <iostream>
#include <deque>
#include <vector>

using namespace std;

vector<int> slidingWindowMaximum(const vector<int>& nums, int k) {
    vector<int> result;
    deque<int> window;

    for (int i = 0; i < nums.size(); ++i) {
        // Remove elements outside the window's range
        while (!window.empty() && window.front() < i - k + 1) {
            window.pop_front();
        }

        // Remove smaller elements from the back
        while (!window.empty() && nums[window.back()] < nums[i]) {
            window.pop_back();
        }

        // Add current element index to the window
        window.push_back(i);

        // Add maximum element to the result for each window
        if (i >= k - 1) {
            result.push_back(nums[window.front()]);
        }
    }

    return result;
}

int main() {
    vector<int> nums = {1, 3, -1, -3, 5, 3, 6, 7};
    int k = 3;
    vector<int> result = slidingWindowMaximum(nums, k);

    cout << "Sliding window maximums: ";
    for (int num : result) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}
```

In this implementation:

- We use a deque `window` to store the indices of elements within the current window.
- At each step, we remove elements from the front of the deque if they are outside the window's range.
- We also remove smaller elements from the back of the deque, ensuring that only potentially maximum elements remain.
- We add the current element's index to the deque while maintaining the above conditions.
- Finally, we add the maximum element of each window to the result vector.

This algorithm runs in O(n) time complexity, where n is the number of elements in the input array `nums`.

### 1. Algorithms & Data Structures (C++): Sliding Window Problems

Sliding window problems are a class of algorithmic problems that involve iterating over a sequence of elements in a specific manner. The "window" in sliding window problems refers to a subset of elements within the sequence that moves or "slides" from the beginning to the end. These problems often require finding the optimal or specific pattern within the sliding window.

In C++, sliding window problems can be efficiently solved using pointers or indices to represent the beginning and end of the window. Here are some common sliding window problems and their solutions:

1. **Maximum Sum Subarray of Size K**:
   Given an array of integers and a positive integer k, find the maximum sum of a contiguous subarray of size k.

   ```cpp
   int maxSumSubarray(vector<int>& nums, int k) {
       int maxSum = 0;
       int windowSum = 0;
       int left = 0;

       for (int right = 0; right < nums.size(); ++right) {
           windowSum += nums[right];
           if (right >= k - 1) {
               maxSum = max(maxSum, windowSum);
               windowSum -= nums[left];
               left++;
           }
       }

       return maxSum;
   }
   ```

2. **Longest Substring Without Repeating Characters**:
   Given a string, find the length of the longest substring without repeating characters.

   ```cpp
   int lengthOfLongestSubstring(string s) {
       unordered_set<char> charSet;
       int maxLength = 0;
       int left = 0;

       for (int right = 0; right < s.size(); ++right) {
           while (charSet.count(s[right])) {
               charSet.erase(s[left]);
               left++;
           }
           charSet.insert(s[right]);
           maxLength = max(maxLength, right - left + 1);
       }

       return maxLength;
   }
   ```

3. **Smallest Subarray with a Given Sum**:
   Given an array of positive integers and a target sum, find the length of the smallest contiguous subarray with a sum greater than or equal to the target sum.

   ```cpp
   int smallestSubarrayWithSum(vector<int>& nums, int targetSum) {
       int minLength = INT_MAX;
       int windowSum = 0;
       int left = 0;

       for (int right = 0; right < nums.size(); ++right) {
           windowSum += nums[right];
           while (windowSum >= targetSum) {
               minLength = min(minLength, right - left + 1);
               windowSum -= nums[left];
               left++;
           }
       }

       return (minLength != INT_MAX) ? minLength : 0;
   }
   ```

These are just a few examples of sliding window problems in C++. Understanding the concept of the sliding window and practicing with different variations will help you tackle a wide range of algorithmic problems efficiently.

### 1. Algorithms & Data Structures (C++): Sliding Window Technique

The sliding window technique is a powerful algorithmic pattern used in solving problems that involve arrays or strings, particularly those that require finding a subset of elements that satisfy certain constraints. It's efficient because it avoids redundant computations by maintaining a window of elements as it traverses the array or string.

Here's a basic overview of how the sliding window technique works:

1. **Initialization**: Start with two pointers, usually at the beginning of the array or string. One pointer marks the start of the window (`left`), and the other marks the end of the window (`right`). Initialize any necessary variables or data structures.

2. **Expansion**: Move the `right` pointer to expand the window to the right, while the current window satisfies the given condition.

3. **Contraction**: Once the window no longer satisfies the condition, move the `left` pointer to shrink the window from the left until the condition is met again.

4. **Optimization (Optional)**: Keep track of the minimum or maximum window size, or any other relevant information during the process.

5. **Finalization**: Return the desired result after processing the entire array or string.

Here's a simple example in C++ demonstrating the sliding window technique for finding the maximum sum subarray of size `k` in an array:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int maxSumSubarray(const vector<int>& nums, int k) {
    int n = nums.size();
    int maxSum = 0;
    int windowSum = 0;

    for (int i = 0; i < k; ++i) {
        windowSum += nums[i];
    }

    maxSum = windowSum;

    for (int i = k; i < n; ++i) {
        windowSum += nums[i] - nums[i - k];
        maxSum = max(maxSum, windowSum);
    }

    return maxSum;
}

int main() {
    vector<int> nums = {4, 2, 1, 7, 8, 1, 2, 8, 1, 0};
    int k = 3;
    cout << "Maximum sum of subarray of size " << k << ": " << maxSumSubarray(nums, k) << endl;
    return 0;
}
```

This code finds the maximum sum of a subarray of size `k` using the sliding window technique. It maintains a window of size `k`, calculates the sum of elements in the window, and slides the window to the right until it reaches the end of the array.

### 1. Algorithms & Data Structures (C++): Sparse Search

Sparse search is an algorithm used to search for a target value in a sorted array of strings that may contain empty strings. It's similar to a binary search but handles empty strings efficiently. Here's a C++ implementation of the sparse search algorithm:

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

int sparseSearch(const vector<string>& arr, const string& target) {
    int low = 0;
    int high = arr.size() - 1;

    while (low <= high) {
        int mid = (low + high) / 2;

        // Adjust mid if it's pointing to an empty string
        if (arr[mid].empty()) {
            int left = mid - 1;
            int right = mid + 1;

            while (true) {
                if (left < low && right > high) {
                    return -1; // If left and right pointers are out of bounds
                } else if (left >= low && !arr[left].empty()) {
                    mid = left;
                    break;
                } else if (right <= high && !arr[right].empty()) {
                    mid = right;
                    break;
                }
                left--;
                right++;
            }
        }

        if (arr[mid] == target) {
            return mid;
        } else if (arr[mid] < target) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }

    return -1;
}

int main() {
    vector<string> arr = {"at", "", "", "", "ball", "", "", "car", "", "", "dad", "", ""};
    string target = "ball";

    int index = sparseSearch(arr, target);

    if (index != -1) {
        cout << "Found at index: " << index << endl;
    } else {
        cout << "Not found" << endl;
    }

    return 0;
}
```

In this implementation, the function `sparseSearch` takes a sorted vector of strings `arr` and a target string `target` to search for. It then performs a modified binary search. If the middle element is empty, it looks for the closest non-empty element and adjusts the mid accordingly. Then, it compares the middle element with the target and continues the search accordingly.

This algorithm maintains the time complexity of a binary search (O(log n)), even in the presence of empty strings in the array.

### 1. Algorithms & Data Structures (C++): Staircase Search

The "Staircase Search" algorithm is a problem-solving technique that involves searching for a target element in a two-dimensional array (matrix) that is sorted row-wise and column-wise. The algorithm gets its name because it's akin to climbing a staircase while searching for the target element.

Here's how the Staircase Search algorithm works:

1. Start at the top-right corner (or any corner) of the matrix.
2. Compare the target element with the current element:
   - If the target element is equal to the current element, return its position.
   - If the target element is less than the current element, move left in the same row (since elements to the left are smaller).
   - If the target element is greater than the current element, move down in the same column (since elements below are greater).
3. Repeat step 2 until the target element is found or until there are no more elements to compare (which means the target element isn't in the matrix).

Here's a simple implementation of the Staircase Search algorithm in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

pair<int, int> staircaseSearch(const vector<vector<int>>& matrix, int target) {
    int rows = matrix.size();
    if (rows == 0) return {-1, -1}; // Empty matrix
    int cols = matrix[0].size();
    
    // Start from the top-right corner
    int row = 0, col = cols - 1;
    
    while (row < rows && col >= 0) {
        if (matrix[row][col] == target) {
            return {row, col}; // Found the target
        } else if (matrix[row][col] < target) {
            // Move down in the same column
            row++;
        } else {
            // Move left in the same row
            col--;
        }
    }
    
    // Target not found
    return {-1, -1};
}

int main() {
    vector<vector<int>> matrix = {
        {1, 4, 7, 11},
        {2, 5, 8, 12},
        {3, 6, 9, 16},
        {10, 13, 14, 17}
    };

    int target = 6;
    pair<int, int> position = staircaseSearch(matrix, target);

    if (position.first != -1 && position.second != -1) {
        cout << "Target " << target << " found at position (" << position.first << ", " << position.second << ")." << endl;
    } else {
        cout << "Target " << target << " not found in the matrix." << endl;
    }

    return 0;
}
```

This implementation assumes the matrix is sorted row-wise and column-wise. It returns the position of the target element if found, or (-1, -1) if the target element is not present in the matrix.

### 1. Algorithms & Data Structures (C++): Ternary Search

Ternary search is a searching algorithm that operates on a sorted array. It's similar to binary search but divides the array into three parts instead of two. Here's how it works:

1. First, the array is divided into three parts instead of two, by calculating two midpoints: \(mid1 = low + (high - low)/3\) and \(mid2 = high - (high - low)/3\).
2. We compare the key we're searching for with the elements at mid1 and mid2.
3. If the key is equal to any of these elements, we return the index.
4. If the key is less than the element at mid1, we recursively search in the first third.
5. If the key is greater than the element at mid2, we recursively search in the last third.
6. If the key is between the elements at mid1 and mid2, we recursively search in the middle third.

Here's a C++ implementation of the ternary search algorithm:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to perform ternary search on a sorted vector
int ternarySearch(vector<int>& arr, int low, int high, int key) {
    if (high >= low) {
        int mid1 = low + (high - low) / 3;
        int mid2 = high - (high - low) / 3;

        // If key is equal to any of the mid elements
        if (arr[mid1] == key) return mid1;
        if (arr[mid2] == key) return mid2;

        // If key is less than the mid1 element, search in the first third
        if (key < arr[mid1])
            return ternarySearch(arr, low, mid1 - 1, key);
        // If key is greater than the mid2 element, search in the last third
        else if (key > arr[mid2])
            return ternarySearch(arr, mid2 + 1, high, key);
        // Otherwise, search in the middle third
        else
            return ternarySearch(arr, mid1 + 1, mid2 - 1, key);
    }
    // Key not found
    return -1;
}

int main() {
    vector<int> arr = {1, 3, 5, 7, 9, 11, 13, 15, 17};
    int key = 11;
    int index = ternarySearch(arr, 0, arr.size() - 1, key);
    if (index != -1)
        cout << "Element found at index " << index << endl;
    else
        cout << "Element not found" << endl;
    return 0;
}
```

In this implementation, we perform the ternary search recursively until the key is found or the search space is exhausted. It's important to note that the array must be sorted before applying the ternary search algorithm.

### 1. Algorithms & Data Structures (C++): Ternary Search - Finding maxima/minima of a parabola

Ternary search is a divide-and-conquer algorithm used to find the maximum or minimum value of a unimodal function within a given interval. It's similar to binary search but works on three intervals instead of two. Here's how you can use ternary search to find the maximum or minimum of a parabolic function in C++:

```cpp
#include <iostream>
#include <cmath>

using namespace std;

double f(double x) {
    // Define your parabolic function here
    return -(x - 3) * (x - 3) + 4; // Example: -(x - 3)^2 + 4
}

double ternary_search(double left, double right) {
    double epsilon = 1e-9; // Adjust according to precision needed
    while (right - left > epsilon) {
        double m1 = left + (right - left) / 3;
        double m2 = right - (right - left) / 3;
        if (f(m1) < f(m2))
            left = m1;
        else
            right = m2;
    }
    // The maximum/minimum is in the interval [left, right]
    return (left + right) / 2;
}

int main() {
    double left_bound = 0; // Lower bound of the interval
    double right_bound = 6; // Upper bound of the interval
    double result = ternary_search(left_bound, right_bound);
    cout << "Maximum/Minimum of the function: " << result << endl;
    return 0;
}
```

In this code:

- The `f` function represents the parabolic function you want to find the maximum or minimum of. Modify this function according to your specific parabola.
- The `ternary_search` function takes the left and right bounds of the interval and returns the x-value where the maximum or minimum of the function occurs.
- In the `main` function, you define the interval over which you want to search for the maximum or minimum value.

Remember, this implementation assumes that the function is unimodal over the given interval.

### 1. Algorithms & Data Structures (C++): Time Complexity of Binary Search

In the context of algorithms and data structures, binary search is a classic algorithm used to efficiently find a target value within a sorted array. Its time complexity is commonly analyzed in terms of big O notation.

The time complexity of binary search is O(log n), where n is the number of elements in the array. This means that as the size of the array grows, the time taken by the binary search algorithm increases logarithmically rather than linearly.

Here's a brief overview of how binary search works and why its time complexity is O(log n):

1. **Divide and Conquer Approach**: Binary search works by repeatedly dividing the search interval in half. It compares the target value with the middle element of the array and eliminates half of the remaining elements based on the comparison result.

2. **Halving the Search Space**: In each step of the algorithm, the search space is halved. This effectively reduces the number of elements that need to be considered in subsequent steps.

3. **Logarithmic Growth**: Because binary search continuously divides the search space in half, the number of steps required to find the target element grows logarithmically with the number of elements in the array. Specifically, the number of steps is proportional to log2(n), where n is the number of elements.

4. **Time Complexity Analysis**: Since each step of the binary search algorithm reduces the search space by half, the time complexity is logarithmic. In big O notation, this is denoted as O(log n).

Overall, binary search is an efficient algorithm for searching in sorted arrays due to its logarithmic time complexity, making it suitable for large datasets where linear search algorithms would be too slow.

### 1. Algorithms & Data Structures (C++): Traversal Linear Search

Linear search is one of the simplest searching algorithms. It sequentially checks each element of the list until a match is found or the entire list has been searched. Here's a basic implementation of linear search in C++:

```cpp
#include <iostream>
#include <vector>

// Function to perform linear search
int linearSearch(const std::vector<int>& arr, int key) {
    for (int i = 0; i < arr.size(); ++i) {
        if (arr[i] == key) {
            return i; // Return the index if key is found
        }
    }
    return -1; // Return -1 if key is not found
}

int main() {
    std::vector<int> arr = {5, 3, 8, 1, 9, 4, 6};
    int key = 9;
    
    int index = linearSearch(arr, key);
    if (index != -1) {
        std::cout << "Element found at index " << index << std::endl;
    } else {
        std::cout << "Element not found" << std::endl;
    }

    return 0;
}
```

In this implementation:

1. `linearSearch` function takes a vector `arr` and an integer `key` to search for.
2. It iterates through each element of the vector using a for loop.
3. If the current element is equal to the key, it returns the index of that element.
4. If the key is not found after iterating through the entire vector, it returns -1.
5. In the `main` function, we create a vector `arr` and specify the `key` to search for.
6. We call the `linearSearch` function and print the result accordingly.

This algorithm has a time complexity of O(n), where n is the number of elements in the list. It means that in the worst-case scenario, it may have to search through all elements in the list.

### 1. Algorithms & Data Structures (C++): Two Way Partitioning Algorithm

The Two-Way Partitioning Algorithm is a fundamental technique used in various sorting algorithms like Quicksort. In C++, it's commonly implemented as a subroutine within these sorting algorithms. The goal is to partition an array into two parts based on a pivot element: elements less than the pivot are placed before it, and elements greater than or equal to the pivot are placed after it. Here's a simple implementation of the Two-Way Partitioning Algorithm in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to perform the two-way partitioning
int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high]; // Choosing the last element as the pivot
    int i = low - 1; // Index of smaller element

    for (int j = low; j < high; j++) {
        // If the current element is smaller than or equal to the pivot
        if (arr[j] <= pivot) {
            i++; // Increment index of smaller element
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return i + 1;
}

// Function to print an array
void printArray(vector<int>& arr) {
    for (int i = 0; i < arr.size(); i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

// Main function to test the partitioning algorithm
int main() {
    vector<int> arr = {10, 7, 8, 9, 1, 5};
    int n = arr.size();
    cout << "Original array: ";
    printArray(arr);

    int pivotIndex = partition(arr, 0, n - 1);

    cout << "Array after partitioning: ";
    printArray(arr);

    cout << "Index of pivot element: " << pivotIndex << endl;

    return 0;
}
```

In this code:

- The `partition()` function takes an array `arr`, and two indices `low` and `high`, indicating the range of elements to partition.
- It chooses the last element (`arr[high]`) as the pivot.
- It iterates through the array from `low` to `high-1`, and for each element smaller than or equal to the pivot, it swaps it with the element at index `i`, where `i` is initially set to `low - 1`.
- Finally, it swaps the pivot element with the element at index `i + 1`, ensuring that all elements to the left of `i + 1` are smaller than or equal to the pivot, and all elements to the right are greater.

You can test this code with different arrays to observe the partitioning effect.

### 1. Algorithms & Data Structures (C++): Understanding Binary Search

Binary search is a fundamental algorithm used for searching a sorted array efficiently. Here's how it works:

1. **Input**:
   - A sorted array of elements.
   - The value we want to search for in the array.

2. **Procedure**:
   - Binary search starts by comparing the target value to the middle element of the array.
   - If the target value matches the middle element, the position is returned.
   - If the target value is less than the middle element, the search is narrowed to the lower half of the array.
   - If the target value is greater than the middle element, the search is narrowed to the upper half of the array.
   - The process continues recursively until the target value is found or the subarray to search becomes empty.

3. **Pseudocode**:

```plaintext
function binarySearch(array, target, low, high):
    if low > high:
        return -1 // Target not found

    mid = (low + high) / 2
    if array[mid] == target:
        return mid
    else if array[mid] > target:
        return binarySearch(array, target, low, mid - 1)
    else:
        return binarySearch(array, target, mid + 1, high)
```

1. **Time Complexity**:
   - Binary search has a time complexity of O(log n), where n is the number of elements in the array.
   - This is because with each comparison, the size of the array to search is halved.

1. **Space Complexity**:
   - Binary search typically has a space complexity of O(1) because it doesn't require additional space proportional to the input size beyond a few variables for indices and the target value.

1. **Key Points**:
   - Binary search only works on sorted arrays.
   - It's efficient for large datasets because it reduces the search space by half with each iteration.
   - It's a divide-and-conquer algorithm.

1. **Implementation in C++**:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int binarySearch(const vector<int>& arr, int target) {
    int low = 0;
    int high = arr.size() - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] == target)
            return mid;
        else if (arr[mid] < target)
            low = mid + 1;
        else
            high = mid - 1;
    }

    return -1; // Not found
}

int main() {
    vector<int> arr = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int target = 6;
    int index = binarySearch(arr, target);
    if (index != -1)
        cout << "Element found at index: " << index << endl;
    else
        cout << "Element not found" << endl;
    return 0;
}
```

This implementation of binary search uses an iterative approach instead of recursion.

### 1. Algorithms & Data Structures (C++): What is a Divide and Conquer Algorithm?

A Divide and Conquer Algorithm is a problem-solving strategy that works by breaking down a problem into smaller, more manageable subproblems, solving each subproblem independently, and then combining the solutions of the subproblems to solve the original problem. This approach typically involves three steps:

1. **Divide**: The original problem is divided into smaller, more manageable subproblems. This step can be repeated recursively until the subproblems become simple enough to solve directly.

2. **Conquer**: Each subproblem is solved independently. This is often the base case of the recursion where the problem is simple enough to solve directly without further subdivision.

3. **Combine**: The solutions of the subproblems are combined to solve the original problem. This step involves aggregating or merging the results obtained from solving the subproblems into a solution for the original problem.

Divide and Conquer algorithms are commonly used in various fields, including computer science, mathematics, and engineering, and they are known for their efficiency and scalability. Classic examples of Divide and Conquer algorithms include Merge Sort, Quick Sort, and Binary Search. These algorithms leverage the divide and conquer strategy to efficiently solve problems by breaking them down into smaller, more manageable parts.

### 1. Algorithms & Data Structures (C++): Wildcard Pattern Matching

Wildcard pattern matching is a common problem in computer science and is often encountered in various applications such as file systems, searching text, and network security. The problem involves matching a given pattern containing wildcard characters (* and ?) against a string.

Here's a basic approach to implement wildcard pattern matching in C++:

```cpp
#include <iostream>
#include <cstring>

using namespace std;

bool wildcardMatch(const char *pattern, const char *str) {
    // Base cases: if both pattern and string reach the end, they match
    if (*pattern == '\0' && *str == '\0')
        return true;

    // If the pattern is at *, then match any sequence of characters in the string
    if (*pattern == '*') {
        // Check for each possible starting position in the string
        while (*str != '\0') {
            if (wildcardMatch(pattern + 1, str))
                return true;
            str++;
        }
        return wildcardMatch(pattern + 1, str); // If * matches nothing
    }

    // If pattern character is '?' or matches current character in string
    if (*pattern == '?' || *pattern == *str)
        return wildcardMatch(pattern + 1, str + 1);

    // If characters don't match and pattern character is not '*'
    return false;
}

int main() {
    const char *pattern = "g*ks";
    const char *str = "geeks";
    if (wildcardMatch(pattern, str))
        cout << "Pattern matches the string\n";
    else
        cout << "Pattern does not match the string\n";

    return 0;
}
```

In this code:

- The `wildcardMatch` function takes two arguments, the pattern and the string, and returns true if the pattern matches the string, otherwise false.
- It uses recursion to explore all possible matches between the pattern and the string.
- If the current character in the pattern is '*', it tries all possible matches by recursively calling the function with the remaining pattern and string after '*', moving the string pointer one character forward each time.
- If the current character in the pattern is '?' or matches the current character in the string, it recursively calls the function with the remaining pattern and string, moving both pointers one character forward.
- If none of the above conditions are met, it returns false.

This is a basic implementation. Depending on your requirements, you may need to extend it to handle more complex scenarios or optimize it for better performance.

### 1. Algorithms & Data Structures (C++): Xor Guessing

XOR Guessing is a problem-solving technique that leverages the properties of the XOR (exclusive OR) operation to efficiently solve certain types of problems, particularly in the context of algorithms and data structures.

Here's a basic overview of how XOR Guessing works:

1. **XOR Operation**: The XOR operation returns true (1) if the operands have different boolean values, and false (0) if they have the same boolean value. In binary, it's represented as `0 ^ 0 = 0`, `0 ^ 1 = 1`, `1 ^ 0 = 1`, and `1 ^ 1 = 0`.

2. **Properties of XOR**:
   - XOR is commutative: `a ^ b = b ^ a`.
   - XOR is associative: `(a ^ b) ^ c = a ^ (b ^ c)`.
   - XOR of a number with itself is 0: `a ^ a = 0`.
   - XOR of a number with 0 is the number itself: `a ^ 0 = a`.

3. **Application**:
   - XOR can be used to efficiently find the unique element in an array where all other elements occur an even number of times. This is because XORing a number with itself results in 0, effectively canceling out even occurrences.
   - XOR can also be used to find missing or duplicate elements in an array, and to swap values without needing a temporary variable.

4. **XOR Guessing Algorithm**:
   - XOR Guessing is often used in programming challenges and competitive programming.
   - In these problems, you are typically given a sequence of numbers and tasked with finding a particular value or pattern.
   - By exploiting the properties of XOR, you can make educated guesses or deduce information about the sequence more efficiently than other methods.
   - Common applications include finding missing elements, identifying patterns, or solving puzzles.

5. **Example**:
   - Given an array where all elements occur twice except for one, you can find the unique element using XOR.
   - Iterate through the array and XOR each element with a variable initialized to 0.
   - Since XORing a number with itself results in 0, and XORing 0 with any number gives that number, after iterating through the array, the variable will hold the unique element.

Here's a simple C++ function to find the unique element in an array using XOR:

```cpp
#include <iostream>
#include <vector>

int findUnique(std::vector<int>& nums) {
    int result = 0;
    for (int num : nums) {
        result ^= num;
    }
    return result;
}

int main() {
    std::vector<int> nums = {2, 4, 6, 8, 4, 6, 2};
    std::cout << "Unique element: " << findUnique(nums) << std::endl;
    return 0;
}
```

This function will output the unique element in the array `{2, 4, 6, 8, 4, 6, 2}`, which in this case is `8`.

### 1. Algorithms & Data Structures (C++): Xor on Segment

Using XOR on segments of data can be a useful technique in various algorithmic problems, particularly in competitive programming and some real-world scenarios. It's often employed to efficiently handle range queries or updates.

In the context of competitive programming, XOR on a segment typically involves answering queries on a contiguous subarray of elements from an array. You might need to compute the XOR of all elements within that segment efficiently.

Here's a basic implementation in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to compute XOR of all elements in a given segment
int computeXOR(const vector<int>& arr, int left, int right) {
    int xor_result = 0;
    for (int i = left; i <= right; ++i) {
        xor_result ^= arr[i];
    }
    return xor_result;
}

int main() {
    // Example usage
    vector<int> arr = {3, 8, 6, 4, 2, 5, 10, 7};
    
    // Compute XOR of segment [2, 5] (0-indexed)
    int left = 2;
    int right = 5;
    int xor_result = computeXOR(arr, left, right);
    
    cout << "XOR of segment [" << left << ", " << right << "]: " << xor_result << endl;
    
    return 0;
}
```

This program demonstrates computing the XOR of a segment `[left, right]` of the given array `arr`. The `computeXOR` function iterates through the elements in the segment and calculates their XOR.

Keep in mind that this is a straightforward implementation. Depending on the problem constraints and the size of the array, you might need more efficient algorithms or data structures like segment trees or binary indexed trees (BIT) for faster computation, especially if you're dealing with a large number of queries or updates.

### 1. Algorithms & Data Structures (C++): Xor-Paths

XOR paths are an interesting problem in computer science where you navigate through a grid from one corner to another, allowed to move only down or right, and the goal is to find a path that maximizes the XOR value of the numbers encountered along the way. Here's a basic explanation of how you can approach this problem:

#### Algorithm

1. **Dynamic Programming (DP)**:
   - Start from the top-left corner of the grid.
   - For each cell (i, j), compute the maximum XOR value to reach that cell.
   - Use a 2D array to store these maximum XOR values.
   - The maximum XOR value to reach a cell (i, j) can be computed as:

     ```bash
     dp[i][j] = max(dp[i-1][j] XOR grid[i][j], dp[i][j-1] XOR grid[i][j])
     ```

   - Traverse the grid from top-left to bottom-right to fill up the DP table.
   - Finally, the maximum XOR value to reach the bottom-right corner is stored in dp[n-1][m-1], where n is the number of rows and m is the number of columns.

#### Example C++ Code

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int maxXorPath(vector<vector<int>>& grid) {
    int n = grid.size();
    int m = grid[0].size();

    vector<vector<int>> dp(n, vector<int>(m));

    dp[0][0] = grid[0][0];

    // Initialize the first row
    for (int j = 1; j < m; ++j) {
        dp[0][j] = dp[0][j - 1] ^ grid[0][j];
    }

    // Initialize the first column
    for (int i = 1; i < n; ++i) {
        dp[i][0] = dp[i - 1][0] ^ grid[i][0];
    }

    // Fill up the DP table
    for (int i = 1; i < n; ++i) {
        for (int j = 1; j < m; ++j) {
            dp[i][j] = max(dp[i - 1][j] ^ grid[i][j], dp[i][j - 1] ^ grid[i][j]);
        }
    }

    return dp[n - 1][m - 1];
}

int main() {
    vector<vector<int>> grid = {
        {1, 3, 5},
        {4, 1, 2},
        {7, 1, 1}
    };

    cout << "Maximum XOR path value: " << maxXorPath(grid) << endl;

    return 0;
}
```

This code demonstrates how to find the maximum XOR path value for a given grid. You can replace the `grid` variable in the `main()` function with any grid you want to test.

### 1. Algorithms & Data Structures (C++): Floyd's Cycle Detection Algorithm C++

Floyd's Cycle Detection Algorithm, also known as the Tortoise and Hare algorithm, is used to detect cycles in a sequence of values. It is particularly useful for detecting cycles in linked lists. Below is a C++ implementation of Floyd's Cycle Detection Algorithm.

### C++ Implementation

```cpp
#include <iostream>

// Definition for singly-linked list node
struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};

class Solution {
public:
    bool hasCycle(ListNode* head) {
        if (!head || !head->next) return false;
        
        ListNode* slow = head;
        ListNode* fast = head;
        
        while (fast && fast->next) {
            slow = slow->next;        // Move slow pointer by 1 step
            fast = fast->next->next;  // Move fast pointer by 2 steps
            
            if (slow == fast) {       // Cycle detected
                return true;
            }
        }
        
        return false; // No cycle detected
    }
};

int main() {
    // Example usage:
    ListNode* head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = head->next; // Create a cycle for testing
    
    Solution solution;
    if (solution.hasCycle(head)) {
        std::cout << "Cycle detected!" << std::endl;
    } else {
        std::cout << "No cycle detected." << std::endl;
    }

    // Note: In practice, you should properly free the allocated memory to avoid memory leaks.
    // This example code does not do so for simplicity and due to the cycle present in the list.

    return 0;
}
```

### Explanation

1. **ListNode Structure**:
    - The `ListNode` struct defines the structure of a node in a singly linked list, with an integer value and a pointer to the next node.

2. **Solution Class**:
    - The `Solution` class contains the `hasCycle` method which implements Floyd's Cycle Detection Algorithm.

3. **hasCycle Method**:
    - The method takes the head of a linked list as input and returns `true` if there is a cycle in the list, otherwise returns `false`.
    - It initializes two pointers, `slow` and `fast`, both starting at the head of the list.
    - The `slow` pointer moves one step at a time, while the `fast` pointer moves two steps at a time.
    - If there is a cycle, the `slow` and `fast` pointers will eventually meet at some node within the cycle.
    - If `fast` reaches the end of the list (`NULL`), it means there is no cycle.

4. **Main Function**:
    - The `main` function demonstrates how to create a linked list and test it for cycles using the `hasCycle` method.
    - In this example, a cycle is manually created in the list for testing purposes.

### Note

- The example linked list in the `main` function contains a cycle for demonstration. In real applications, ensure proper memory management and avoid creating such cycles unintentionally.
- Memory cleanup is not handled in this example. In practice, you should free the allocated memory to prevent memory leaks, especially when dealing with larger linked lists.

### 1. Algorithms & Data Structures (C++): Linked Lists: Detecting Linked Lists Loops

Detecting loops in a linked list is a classic problem in computer science. One efficient way to detect loops in a linked list is by using Floyd's Cycle Detection Algorithm, also known as the "tortoise and hare" algorithm.

Here's how it works:

1. Start with two pointers, often referred to as "slow" and "fast," both initially pointing to the head of the linked list.
2. Move the slow pointer one step at a time and the fast pointer two steps at a time.
3. If there is no loop, the fast pointer will eventually reach the end of the list.
4. If there is a loop, the fast pointer will eventually catch up to the slow pointer.

Here's the C++ implementation:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* next;
};

bool detectLoop(Node* head) {
    if (head == nullptr)
        return false;

    Node* slow = head;
    Node* fast = head;

    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;          // Move slow pointer by one step
        fast = fast->next->next;    // Move fast pointer by two steps

        // If slow and fast pointers meet, there is a loop
        if (slow == fast)
            return true;
    }

    // If the loop exits without any meeting, there's no loop
    return false;
}

int main() {
    // Create a sample linked list with a loop
    Node* head = new Node();
    head->data = 1;
    head->next = new Node();
    head->next->data = 2;
    head->next->next = new Node();
    head->next->next->data = 3;
    head->next->next->next = new Node();
    head->next->next->next->data = 4;
    head->next->next->next->next = head->next; // Create a loop

    // Detect loop
    if (detectLoop(head))
        std::cout << "Loop found in the linked list." << std::endl;
    else
        std::cout << "No loop found in the linked list." << std::endl;

    return 0;
}
```

In this code, the `detectLoop` function takes the head of the linked list as input and returns `true` if a loop is detected, and `false` otherwise. The `main` function demonstrates how to create a sample linked list with a loop and calls the `detectLoop` function to check for the loop.

### 1. Algorithms & Data Structures (C++): Tortoise and Hare algorithm C++

The Tortoise and Hare algorithm, also known as Floyd's cycle-finding algorithm, is a pointer algorithm that uses two pointers moving at different speeds to detect a cycle in a sequence. Here is a C++ implementation of this algorithm to detect a cycle in a linked list:

```cpp
#include <iostream>

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

class Solution {
public:
    bool hasCycle(ListNode *head) {
        if (head == nullptr) return false;

        ListNode *slow = head;
        ListNode *fast = head;

        while (fast != nullptr && fast->next != nullptr) {
            slow = slow->next;          // Move slow pointer by 1 step
            fast = fast->next->next;    // Move fast pointer by 2 steps

            if (slow == fast) {
                return true;            // Cycle detected
            }
        }

        return false;                   // No cycle
    }
};

// Helper function to create a cycle in the linked list for testing
void createCycle(ListNode *head, int pos) {
    if (pos == -1) return;

    ListNode *cycleNode = nullptr;
    ListNode *tail = head;
    int index = 0;
    
    while (tail->next != nullptr) {
        if (index == pos) {
            cycleNode = tail;
        }
        tail = tail->next;
        index++;
    }
    tail->next = cycleNode;
}

int main() {
    // Creating a linked list for testing
    ListNode *head = new ListNode(3);
    head->next = new ListNode(2);
    head->next->next = new ListNode(0);
    head->next->next->next = new ListNode(-4);

    // Create a cycle in the linked list
    createCycle(head, 1);

    Solution solution;
    if (solution.hasCycle(head)) {
        std::cout << "Cycle detected in the linked list." << std::endl;
    } else {
        std::cout << "No cycle in the linked list." << std::endl;
    }

    // Cleanup (in a real scenario, make sure to handle memory properly)
    // Avoid cleaning up in this demo as it creates a cycle and might lead to infinite loop
    // delete head->next->next->next;
    // delete head->next->next;
    // delete head->next;
    // delete head;

    return 0;
}
```

#### Explanation

1. **ListNode Structure**: Defines the structure of a node in the singly-linked list.
2. **Solution Class**: Contains the method `hasCycle` to detect if there's a cycle in the linked list.
3. **hasCycle Method**:
   - Initializes two pointers, `slow` and `fast`, both starting at the head of the list.
   - Moves `slow` by one step and `fast` by two steps in each iteration.
   - If `slow` and `fast` meet at any point, it confirms a cycle.
   - If `fast` or `fast->next` becomes `nullptr`, it means there is no cycle.
4. **createCycle Function**: Helper function to create a cycle in the linked list at a given position for testing purposes.
5. **main Function**: Sets up a linked list, introduces a cycle, and uses the `hasCycle` method to check for cycles.

#### Note

This implementation is basic and intended for demonstration. In real-world usage, you should include proper memory management to avoid memory leaks. Since creating a cycle can lead to infinite loops, careful handling is required when cleaning up the linked list.

### 1. Algorithms & Data Structures (C++): Array: Linear Search Technique

Linear search is a straightforward searching algorithm that checks each element in a collection until the desired element is found or the end of the collection is reached. Here's a simple implementation of linear search in C++:

```cpp
#include <iostream>

// Function to perform linear search
int linearSearch(int arr[], int n, int key) {
    for (int i = 0; i < n; ++i) {
        if (arr[i] == key) {
            return i; // Return the index if key is found
        }
    }
    return -1; // Return -1 if key is not found
}

int main() {
    int arr[] = {2, 5, 7, 9, 12, 15, 19, 22};
    int n = sizeof(arr) / sizeof(arr[0]);
    int key = 12;

    int result = linearSearch(arr, n, key);
    if (result != -1) {
        std::cout << "Element found at index " << result << std::endl;
    } else {
        std::cout << "Element not found" << std::endl;
    }

    return 0;
}
```

In this code:

- `linearSearch` function takes an array `arr`, its size `n`, and the key to be searched `key`.
- It iterates through each element of the array.
- If the current element matches the key, it returns the index of that element.
- If the key is not found after iterating through the entire array, it returns -1.
- In the `main` function, an example array `arr` is defined, and the `linearSearch` function is called with this array, its size, and the key to be searched.
- The result of the search is then printed.

This is a basic linear search implementation. While simple, it's not very efficient for large datasets as it has a time complexity of O(n), where n is the number of elements in the array.
