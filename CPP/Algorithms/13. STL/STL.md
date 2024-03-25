
### 1. Algorithms & Data Structures (C++): Iterators

Iterators in C++ are powerful tools that allow you to traverse through elements of containers like arrays, vectors, lists, maps, etc., without exposing the underlying structure of the container. They act as pointers to elements in the container and provide a uniform way to access or manipulate elements regardless of the container type.

Here's a brief overview of iterators in C++:

1. **Input Iterators**: These iterators support operations like reading values from the container. You can move them forward using the increment operator (++). They are typically used in algorithms where data is read-only, like `std::find`.

2. **Output Iterators**: They support operations for writing values into the container. They are advanced using the increment operator. Output iterators are useful for algorithms that write data into containers, like `std::copy`.

3. **Forward Iterators**: These are like input iterators, but they can be used multiple times to read or write data. They support both read and write operations.

4. **Bidirectional Iterators**: Bidirectional iterators can be moved in both directions (forward and backward). They support operations like increment and decrement.

5. **Random Access Iterators**: These are the most versatile iterators and provide all the functionality of bidirectional iterators, along with the ability to perform arithmetic operations like addition and subtraction. Random access iterators provide efficient access to elements at any position within the container.

Here's a simple example demonstrating the usage of iterators with a vector:

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};

    // Using iterators to traverse the vector
    std::vector<int>::iterator it;
    for (it = vec.begin(); it != vec.end(); ++it) {
        std::cout << *it << " ";
    }
    std::cout << std::endl;

    // Using range-based for loop (C++11)
    for (int num : vec) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this example, `vec.begin()` returns an iterator pointing to the beginning of the vector, and `vec.end()` returns an iterator pointing to the end (one past the last element) of the vector. We iterate through the vector using iterators and print each element.

### 1. Algorithms & Data Structures (C++): Lower Bound and Upper Bound

In C++, `lower_bound` and `upper_bound` are two important functions provided by the Standard Template Library (STL) in the `<algorithm>` header. They are used to perform binary search on sorted sequences.

1. **`lower_bound`**: This function returns an iterator pointing to the first element in the range [first, last) which is not less than (i.e., greater or equal to) the given value. If all elements in the range are less than the given value, it returns `last`.

2. **`upper_bound`**: This function returns an iterator pointing to the first element in the range [first, last) which is greater than the given value. If all elements in the range are less than or equal to the given value, it returns `last`.

Here's a simple example demonstrating the use of `lower_bound` and `upper_bound`:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> vec = {1, 2, 2, 3, 4, 4, 5, 6, 7};

    // Find the lower bound and upper bound of value 4
    auto lower = std::lower_bound(vec.begin(), vec.end(), 4);
    auto upper = std::upper_bound(vec.begin(), vec.end(), 4);

    // Print the lower and upper bound indices
    std::cout << "Lower bound of 4 is at index: " << (lower - vec.begin()) << std::endl;
    std::cout << "Upper bound of 4 is at index: " << (upper - vec.begin()) << std::endl;

    return 0;
}
```

Output:

```bash
Lower bound of 4 is at index: 4
Upper bound of 4 is at index: 6
```

In this example, the lower bound of value `4` is at index `4`, which is the first occurrence of `4`, and the upper bound is at index `6`, which is the position immediately after the last occurrence of `4`.

Both `lower_bound` and `upper_bound` have logarithmic complexity with respect to the size of the container since they use binary search.

### 1. Algorithms & Data Structures (C++): Pairs

In C++, a pair is a simple data structure that allows you to store two heterogeneous objects together. It's defined in the `<utility>` header. Pairs are commonly used in situations where you need to return two values from a function, or when you want to keep two pieces of data together.

Here's a basic example of how to use pairs in C++:

```cpp
#include <iostream>
#include <utility> // for pair

using namespace std;

int main() {
    // Creating a pair of integers
    pair<int, int> myPair;

    // Assigning values to the pair
    myPair.first = 10;
    myPair.second = 20;

    // Accessing values of the pair
    cout << "First value: " << myPair.first << endl;
    cout << "Second value: " << myPair.second << endl;

    // Creating a pair using make_pair function
    pair<string, double> anotherPair = make_pair("Height", 6.2);

    // Accessing values of the second pair
    cout << "Label: " << anotherPair.first << endl;
    cout << "Measurement: " << anotherPair.second << " feet" << endl;

    return 0;
}
```

In this example, the `pair` template is used to declare a pair of integers (`myPair`) and a pair of a string and a double (`anotherPair`). The `make_pair` function is used to initialize the second pair.

Pairs are commonly used in conjunction with other data structures like maps and sets, where they serve as key-value pairs. For example, in a map, each element is a pair consisting of a key and a value.

### 1. Algorithms & Data Structures (C++): reverse()

In C++, the `reverse()` function is a part of the Standard Template Library (STL) and is used to reverse the order of elements in a container like an array, vector, or string. It's a part of the `<algorithm>` header.

Here's a basic example of how to use `reverse()`:

```cpp
#include <iostream>
#include <algorithm>
#include <vector>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};

    // Reversing the vector
    std::reverse(vec.begin(), vec.end());

    // Printing the reversed vector
    for (int num : vec) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

Output:

```bash
5 4 3 2 1
```

This code reverses the order of elements in the vector `vec`. The `reverse()` function takes two iterators as arguments, marking the range of elements to be reversed. In this case, `vec.begin()` points to the beginning of the vector and `vec.end()` points to the element past the last element of the vector.

### 1. Algorithms & Data Structures (C++): Typical Runtime Functions

In C++, algorithms and data structures play a crucial role in writing efficient and maintainable code. Here are some typical runtime functions associated with common algorithms and data structures:

#### Algorithms

1. **Sorting:**
   - `std::sort()`: Used to sort elements in a range.
   - `std::stable_sort()`: Similar to `std::sort()` but maintains the relative order of equivalent elements.
   - `std::partial_sort()`: Sorts the first `n` elements in a range.

2. **Searching:**
   - `std::find()`: Finds the first occurrence of a value in a range.
   - `std::binary_search()`: Checks if an element exists in a sorted range using binary search.
   - `std::lower_bound()`, `std::upper_bound()`: Finds the lower/upper bound of a value in a sorted range.

3. **Heap Operations:**
   - `std::make_heap()`: Constructs a heap from a range of elements.
   - `std::push_heap()`, `std::pop_heap()`: Adds/removes elements from a heap.

4. **Permutations and Combinations:**
   - `std::next_permutation()`, `std::prev_permutation()`: Generates the next/previous lexicographically greater permutation of a range.

5. **Numeric Algorithms:**
   - `std::accumulate()`: Computes the sum of elements in a range.
   - `std::inner_product()`: Computes the inner product of two ranges.

#### Data Structures

1. **Arrays:**
   - Accessing elements: `O(1)`
   - Insertion/Deletion (at end): `O(1)` (if capacity allows), otherwise `O(n)`

2. **Linked Lists:**
   - Insertion/Deletion (at beginning): `O(1)`
   - Accessing elements (by index): `O(n)`

3. **Stacks:**
   - Push/Pop: `O(1)`

4. **Queues:**
   - Enqueue/Dequeue: `O(1)`

5. **Trees:**
   - Binary Search Tree (BST) Operations (average):
     - Insertion/Deletion/Search: `O(log n)`
   - Balanced Binary Search Tree (AVL, Red-Black Tree) Operations:
     - Insertion/Deletion/Search: `O(log n)`

6. **Hash Tables:**
   - Insertion/Deletion/Search (average case): `O(1)`
   - Insertion/Deletion/Search (worst case): `O(n)` (due to collisions)

7. **Graphs:**
   - Breadth-First Search (BFS): `O(V + E)` where `V` is the number of vertices and `E` is the number of edges.
   - Depth-First Search (DFS): `O(V + E)`

These complexities are typical cases and can vary based on the implementation and specific scenarios. Understanding these complexities is crucial for writing efficient algorithms and data structures in C++.

### 1. Algorithms & Data Structures (C++): Data Structures & STL Containers

Data structures and the Standard Template Library (STL) containers are fundamental components in C++ programming, offering efficient ways to organize and manipulate data. Here's a breakdown of some common data structures and how they relate to STL containers in C++:

1. **Arrays**:
   - Arrays are a basic data structure that stores elements of the same type in contiguous memory locations.
   - In C++, you can use native arrays (`int arr[5];`) or the STL array container (`std::array<int, 5> arr;`), which provides additional functionality like bounds checking and iterators.

2. **Vectors**:
   - Vectors are dynamic arrays that can grow and shrink in size automatically.
   - They are part of the STL (`std::vector`) and are widely used due to their flexibility and efficiency.
   - Vectors provide methods for insertion, deletion, and random access to elements.

3. **Linked Lists**:
   - Linked lists consist of nodes where each node contains a data element and a reference (pointer) to the next node in the sequence.
   - In C++, you can implement linked lists manually or use the STL `std::list` container, which is a doubly linked list.
   - `std::forward_list` is another STL container representing a singly linked list.

4. **Stacks**:
   - Stacks follow the Last In, First Out (LIFO) principle, where elements are added and removed from the same end (top).
   - The STL provides the `std::stack` adapter, which is implemented using a deque (double-ended queue) by default but can be customized to use other containers as well.

5. **Queues**:
   - Queues adhere to the First In, First Out (FIFO) principle, where elements are added at the back and removed from the front.
   - In addition to deque, the STL offers the `std::queue` adapter, implemented using deque by default, and `std::priority_queue`, which is a priority queue implemented using a heap.

6. **Maps**:
   - Maps (associative arrays) store key-value pairs and provide efficient lookup based on the keys.
   - In C++, `std::map` and `std::unordered_map` are the STL containers for ordered and unordered maps, respectively.
   - Maps are implemented using binary search trees (for `std::map`) or hash tables (for `std::unordered_map`), offering different performance characteristics.

7. **Sets**:
   - Sets store unique elements in sorted order, allowing efficient search, insertion, and deletion operations.
   - In C++, `std::set` and `std::unordered_set` are the STL containers for ordered and unordered sets, respectively.
   - Sets are implemented similarly to maps, but they only store keys (no values).

8. **Trees**:
   - Trees are hierarchical data structures composed of nodes connected by edges.
   - While there's no direct STL container for trees, you can implement various tree structures (e.g., binary search trees, AVL trees) manually or use third-party libraries.

STL containers offer efficient implementations of these data structures, making them convenient choices for most programming tasks. However, in certain cases, you might need to implement custom data structures tailored to specific requirements.