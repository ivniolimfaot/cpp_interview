# Algorithms

## General Info

### What is the complexity of an algorithm? [What does it depend on? - RETURN TO THIS]

There are 2 types of an algorithm complexity:

  ***Time Complexity***: The time complexity of an algorithm quantifies the amount of time taken by an algorithm to run as a function of the length of the input. Note that the time to run is a function of the length of the input and not the actual execution time of the machine on which the algorithm is running on.

To estimate the time complexity, we need to consider the cost of each fundamental instruction and the number of times the instruction is executed.

```cpp
int summ(int a, int b) 
{
  return a + b;  
}

```

The addition of two scalar numbers requires one addition operation. the time complexity of this algorithm is constant, so *T(n) = O(1)*.

**Order of growth** is how the time of execution depends on the length of the input. In the above example, it is clearly evident that the time of execution quadratically depends on the length of the array. Order of growth will help to compute the running time with ease.

  ***Space Complexity***. Problem-solving using computer requires memory to hold temporary data or final result while the program is in execution. The amount of memory required by the algorithm to solve given problem is called space complexity of the algorithm. The space complexity of an algorithm quantifies the amount of space taken by an algorithm to run as a function of the length of the input.

To estimate the memory requirement we need to focus on two parts:

1. *A fixed part:* It is independent of the input size. It includes memory for instructions (code), constants, variables, etc.
1. *A variable part:* It is dependent on the input size. It includes memory for recursion stack, referenced variables, etc.


### 78. What is O-notation and how to determine the complexity of any algorithm?

Big O notation, also known as O-notation, is a mathematical notation used in computer science to describe the asymptotic behavior of functions. In the context of algorithms, it's used to analyze the time complexity or space complexity of an algorithm, which helps in understanding how the algorithm's performance scales with the size of the input.

The notation O(f(n)) describes the upper bound of a function in terms of another function, typically in relation to the size of the input (n), as n approaches infinity. It represents the worst-case scenario for the growth rate of the function.

To determine the complexity of an algorithm using Big O notation, you generally follow these steps:

1. Identify the elementary operations: Break down the algorithm into basic operations that contribute to its execution time. These could be assignments, comparisons, arithmetic operations, etc.

2. Count the number of operations: Analyze how many times each operation is executed in terms of the input size.

3. Express the total count in terms of the input size: Write down a mathematical expression representing the total number of operations as a function of the input size.

4. Simplify and find the dominant term: Simplify the expression and identify the term that grows the fastest as the input size increases. This dominant term represents the time complexity of the algorithm.

5. Express the complexity using Big O notation: Write the complexity of the algorithm using O-notation, representing the upper bound of the growth rate.

Here are some common time complexities and their corresponding Big O notations:

* O(1): Constant time complexity. The algorithm's execution time is constant, regardless of the input size.
* O(log n): Logarithmic time complexity. The algorithm's execution time grows logarithmically with the input size.
* O(n): Linear time complexity. The algorithm's execution time grows linearly with the input size.
* O(n log n): Linearithmic time complexity. Common in efficient sorting algorithms like Merge Sort and Quick Sort.
* O(n^2): Quadratic time complexity. The algorithm's execution time grows quadratically with the input size.
* O(2^n): Exponential time complexity. The algorithm's execution time grows exponentially with the input size.

By analyzing the complexity of an algorithm, you can make informed decisions about its suitability for solving a particular problem and understand its performance characteristics as the input size increases.

Sure, here are examples of algorithms along with their time complexities in C++:

1. **Constant Time Complexity (O(1))**: Operations that take constant time regardless of the input size.

```cpp
#include <iostream>

// Function to print the first element of an array
void printFirstElement(int arr[], int size) {
    if (size > 0) {
        std::cout << "First element: " << arr[0] << std::endl;
    }
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int size = sizeof(arr) / sizeof(arr[0]);
    
    printFirstElement(arr, size);
    
    return 0;
}
```

1. **Linear Time Complexity (O(n))**: Operations that grow linearly with the size of the input.

```cpp
#include <iostream>

// Function to find the sum of elements in an array
int findSum(int arr[], int size) {
    int sum = 0;
    for (int i = 0; i < size; ++i) {
        sum += arr[i];
    }
    return sum;
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int size = sizeof(arr) / sizeof(arr[0]);
    
    std::cout << "Sum of elements: " << findSum(arr, size) << std::endl;
    
    return 0;
}
```

1. **Logarithmic Time Complexity (O(log n))**: Operations that grow logarithmically with the size of the input.

```cpp
#include <iostream>

// Function to perform binary search on a sorted array
int binarySearch(int arr[], int size, int target) {
    int left = 0;
    int right = size - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) {
            return mid;
        } else if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return -1;
}

int main() {
    int arr[] = {1, 3, 5, 7, 9, 11, 13, 15};
    int size = sizeof(arr) / sizeof(arr[0]);
    int target = 7;
    
    int index = binarySearch(arr, size, target);
    if (index != -1) {
        std::cout << "Element found at index " << index << std::endl;
    } else {
        std::cout << "Element not found" << std::endl;
    }
    
    return 0;
}
```

These examples demonstrate how to implement algorithms in C++ along with their corresponding time complexities.
