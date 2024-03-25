# STL

## General Info

### 118. What does the STL consist of?

In C++, the Standard Template Library (STL) is a powerful set of C++ template classes to provide general-purpose classes and functions with templates that implement many popular and commonly used algorithms and data structures like vectors, lists, queues, and stacks. The STL consists of several components:

1. **Containers**: These are classes that hold objects of a certain type. Common containers include:
   * **Vector**: Resizable array.
   * **List**: Doubly linked list.
   * **Deque**: Double-ended queue.
   * **Set**: Collection of unique keys, sorted by keys.
   * **Map**: Collection of key-value pairs, sorted by keys.
   * **Stack**: LIFO (Last In, First Out) data structure.
   * **Queue**: FIFO (First In, First Out) data structure.

2. **Algorithms**: These are functions that operate on sequences of elements. Some examples include:
   * **Sorting**: Sorts elements in a sequence (e.g., `sort()` function).
   * **Searching**: Finds elements in a sequence (e.g., `find()` function).
   * **Transformation**: Performs operations on elements (e.g., `transform()` function).

3. **Iterators**: These are objects that provide a way to traverse through the elements of a container. Iterators abstract the concept of a pointer, allowing generic algorithms to work with different types of containers.

4. **Function Objects (Functors)**: These are objects that can be called as if they were functions. They can be used as arguments to algorithms to customize their behavior.

The STL provides a powerful and efficient framework for C++ developers to work with data structures and algorithms, promoting code reuse, readability, and efficiency.

### 119. What algorithms have been used with STL? What is the advantage of using algorithms over handwritten functions?

STL (Standard Template Library) algorithms in C++ are a set of predefined functions for performing operations on containers and sequences like vectors, arrays, lists, etc. They provide efficient implementations for common tasks such as sorting, searching, and modifying elements within containers. These algorithms are provided as part of the C++ Standard Library and are declared in various headers like `<algorithm>`, `<numeric>`, `<functional>`, etc. Some commonly used STL algorithms include:

1. **Sorting Algorithms**:
   * `sort()`: Sorts elements in the specified range.
   * `stable_sort()`: Sorts elements in a stable manner (preserving the relative order of equal elements).
   * `partial_sort()`: Partially sorts the elements in the specified range.
   * `nth_element()`: Rearranges elements such that the element at the nth position will be in its sorted position.
2. **Searching Algorithms**:
   * `find()`: Searches for a value in a range.
   * `binary_search()`: Checks if a value exists in a sorted range.
   * `lower_bound()`, `upper_bound()`, `equal_range()`: Finds positions of elements in a sorted range.
3. **Permutation Algorithms**:
   * `next_permutation()`, `prev_permutation()`: Generates the next or previous lexicographically greater permutation of elements in a range.
4. **Element Operations**:
   * `count()`, `count_if()`: Counts occurrences of a value or elements satisfying a condition in a range.
   * `max_element()`, `min_element()`: Finds the maximum or minimum element in a range.
   * `accumulate()`, `reduce()`: Computes the sum of elements in a range.
5. **Set Operations**:
   * `set_union()`, `set_intersection()`, `set_difference()`, `set_symmetric_difference()`: Performs set operations on sorted ranges.

6. **Heap Operations**:
   * `make_heap()`, `push_heap()`, `pop_heap()`, `sort_heap()`: Operations on heaps (binary trees with specific properties).

7. **Other Algorithms**:
   * `for_each()`: Applies a function to each element in a range.
   * `transform()`: Applies a function to each element in a range and stores the result in another range.
   * `copy()`, `copy_if()`: Copies elements from one range to another.
   * `reverse()`, `rotate()`, `shuffle()`: Reverses, rotates, or shuffles elements in a range.

These are just a few examples, and the STL provides many more algorithms for various tasks. Utilizing these algorithms can lead to cleaner, more efficient, and more maintainable code.

Using STL (Standard Template Library) algorithms over handwritten functions offers several advantages:

1. **Readability and Maintainability**: STL algorithms use expressive names that clearly convey their purpose. This makes code more readable and understandable compared to handwritten functions, which may require additional comments or documentation to explain their functionality. Additionally, because STL algorithms are standardized and well-known, other developers familiar with C++ will quickly understand the code.

2. **Reusability**: STL algorithms are designed to be generic, meaning they can operate on various container types (e.g., vectors, arrays, lists) and element types (e.g., integers, strings, custom objects). This promotes code reuse since you can apply the same algorithm to different data structures without modification.

3. **Performance**: STL algorithms are highly optimized and implemented by experts, taking advantage of efficient algorithms and data structures. This often leads to better performance compared to handwritten functions, especially for complex operations like sorting and searching.

4. **Safety**: STL algorithms are thoroughly tested and validated, reducing the likelihood of bugs or errors. They handle edge cases and corner cases effectively, which can be challenging to address in handwritten functions.

5. **Maintained and Updated**: The STL is part of the C++ Standard Library, which is maintained and updated by a committee of experts. This ensures that algorithms are kept up-to-date with advancements in language features, optimizations, and best practices.

6. **Consistency**: Using STL algorithms promotes consistency in coding style and behavior across projects and teams. Developers don't need to reinvent the wheel by writing custom functions for common operations, leading to more consistent codebases.

7. **Ease of Integration**: Since STL algorithms are part of the standard library, they integrate seamlessly with other C++ features and libraries. They can be combined with lambda functions, function objects, and other language constructs to achieve complex behavior.

Overall, leveraging STL algorithms results in cleaner, more efficient, and more maintainable code, while also reducing the likelihood of errors and promoting code reuse.

### 120. Tell about the standard library containers vector, list, map, unordered_map

<--- Return later: Data sturctures & STL --->

### 121. What types of iterators do you know? How do they differ? What containers are they used in?

In C++, iterators are objects that allow traversal through the elements of a container (like arrays, vectors, lists, etc.) in a sequential manner. They provide a way to access the elements of a container without exposing its underlying representation.

Iterators abstract away the details of how the container stores its elements, allowing algorithms to work uniformly across different container types. They are essential components for many standard library algorithms and are heavily used in C++ programming.

Here's a brief overview of iterators in C++:

1. **Iterator Categories**:
   * Input iterators: These iterators support single-pass reading of elements from a container.
   * Output iterators: These iterators support single-pass writing of elements to a container.
   * Forward iterators: These iterators can be used to read and write elements in a forward direction.
   * Bidirectional iterators: These iterators support bidirectional movement (forward and backward) through the container.
   * Random access iterators: These iterators support random access to elements in a container, like array indexing.

2. **Iterator Operations**:
   * Dereferencing: Accessing the value pointed to by the iterator using the `*` operator.
   * Incrementing/Decrementing: Moving the iterator to the next/previous element using the `++` and `--` operators.
   * Arithmetic operations: Random access iterators support addition and subtraction operations to move the iterator by a specific number of elements.
   * Comparison: Iterators can be compared using relational operators (`==`, `!=`, `<`, `>`, `<=`, `>=`).

3. **Iterator Traits**:
   * The `std::iterator_traits` template provides a way to obtain information about the properties of iterators, such as the iterator category.

4. **Iterator Adapters**:
   * C++ also provides iterator adapters like `std::back_insert_iterator`, `std::front_insert_iterator`, and `std::insert_iterator`, which adapt containers for use with algorithms that require output iterators.

5. **Standard Library Support**:
   * C++ standard library containers like vectors, lists, maps, and sets provide iterators for traversal.

Here's a simple example demonstrating the use of iterators to iterate over a vector in C++:

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};

    // Using iterators to traverse the vector
    for (auto it = vec.begin(); it != vec.end(); ++it) {
        std::cout << *it << " ";
    }

    return 0;
}
```

This code snippet iterates over a vector using iterators and prints each element.

### 122. What is the difference between std::set, std::map std::unordered_multimap?

<--- Return later: Data sturctures & STL --->

### 123. What is the remove-erase idiom?

In C++, there's no built-in function or idiom called "remove-erase." However, I believe you might be referring to the common idiom used with containers like vectors to remove elements based on a certain condition and then erase them from the container.

Here's an example of how you can achieve this using the erase-remove idiom with vectors:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> numbers = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

    // Remove even numbers
    numbers.erase(std::remove_if(numbers.begin(), numbers.end(),
                                 [](int n){ return n % 2 == 0; }),
                  numbers.end());

    // Print remaining numbers
    for (int num : numbers) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this example, `std::remove_if` is used to move all elements satisfying a condition (in this case, even numbers) to the end of the vector. Then, `vector::erase` is used to remove those elements from the vector.

This is a common idiom used in C++ when you want to remove elements from a container based on a certain condition.

### 124. How to get the smallest value of a type?

In C++, you can use the `std::numeric_limits` template class from the `<limits>` header to get the smallest value of a particular type. Here's how you can do it:

```cpp
#include <iostream>
#include <limits>

int main() {
    // For integer types
    std::cout << "Smallest value for int: " << std::numeric_limits<int>::min() << std::endl;
    // For floating-point types
    std::cout << "Smallest value for float: " << std::numeric_limits<float>::min() << std::endl;
    return 0;
}
```

This code snippet demonstrates how to get the smallest value for `int` and `float` types. You can replace `int` and `float` with any other built-in type like `double`, `short`, `long`, etc., to get the smallest value for that type. The `min()` member function of `std::numeric_limits` template class returns the smallest finite value representable by the given type.

### 125. What is the difference between std::map and std::hashmap?

<--- Return later: Data sturctures & STL --->

### 126. How to count the number of elements in std::list?

<--- Return later: Data sturctures & STL --->

### 128. What is the difference between vector and list and when is it better to use them?

<--- Return later: Data sturctures & STL --->

## STL/Algorithms

### 108. What algorithms from STL did you use? What are missing?

<--- Return later: Alghoritms and Data Structures --->

### 109. What features should a class have to be an iterator?

In C++, to create an iterator class, you need to ensure that it supports the following features and functionality:

1. **Constructor(s)**: The iterator class should have constructor(s) to initialize its internal state. This might include initializing pointers or other data members.

2. **Destructor**: It's essential to have a destructor to clean up resources if the iterator manages any.

3. **Increment Operator (`operator++`)**: Implement the `operator++` to move the iterator to the next element in the sequence. Typically, this means advancing the internal state of the iterator.

4. **Dereference Operator (`operator*` or `operator->`)**: Implement the `operator*` to allow dereferencing the iterator, returning a reference to the current element. If your iterator is meant to behave like a pointer, you might also implement `operator->`.

5. **Equality Comparison Operators (`operator==`, `operator!=`)**: Implement these operators to compare two iterators for equality. `operator==` should return `true` if both iterators point to the same element, and `operator!=` should return `true` if they point to different elements.

6. **Validity Check**: Ensure that the iterator can check for validity, indicating whether it's currently pointing to a valid element in the sequence or if it has reached the end.

7. **Copy Constructor and Assignment Operator (optional)**: Depending on your requirements, you might also want to implement these to support copying iterators.

8. **Move Constructor and Move Assignment Operator (optional)**: For efficiency and flexibility, consider implementing move semantics for your iterator class.

Here's a basic example of what such a class might look like:

```cpp
template<typename T>
class MyIterator {
private:
    T* ptr;
public:
    MyIterator(T* p) : ptr(p) {}
    ~MyIterator() {}

    // Increment operator
    MyIterator& operator++() {
        ++ptr;
        return *this;
    }

    // Dereference operator
    T& operator*() const {
        return *ptr;
    }

    // Equality comparison operators
    bool operator==(const MyIterator& other) const {
        return ptr == other.ptr;
    }

    bool operator!=(const MyIterator& other) const {
        return !(*this == other);
    }

    // Validity check
    bool isValid() const {
        // Implement based on your logic
        // For example, check if ptr is within valid range
    }
};
```

This is a basic outline, and you may need to customize it according to your specific use case or the requirements of the container you're iterating over. Additionally, if you're implementing an iterator for a specific container, you might want to look into iterator categories and traits to ensure compatibility with standard library algorithms.

### 110. What are the iterators?

In C++, iterators are objects that allow you to traverse through the elements of a container (such as arrays, vectors, lists, etc.) in a sequential manner. They serve as a generalized interface for accessing the elements of a container without exposing the underlying data structure details.

Iterators provide a way to navigate through the elements of a container and perform various operations like reading, modifying, or deleting elements. They abstract away the specific implementation details of the container, making the code more generic and reusable.

There are different types of iterators in C++, including:

1. **Input iterators**: These iterators support reading values from a sequence of elements but may only be used in a single pass, meaning once you read an element, you cannot go back to it.

2. **Output iterators**: These iterators support writing values to a sequence of elements but, like input iterators, may only be used in a single pass.

3. **Forward iterators**: These iterators can be used to read and write values from a sequence of elements in a single pass. They also support moving forward through the sequence.

4. **Bidirectional iterators**: These iterators support both forward and backward traversal of elements in a sequence.

5. **Random access iterators**: These iterators provide the most functionality. They allow you to access elements randomly, meaning you can jump to any element in constant time. They support arithmetic operations like addition and subtraction to navigate through the sequence efficiently.

Iterators in C++ can be used with standard library containers like `std::vector`, `std::list`, `std::map`, etc. They are typically manipulated using operators such as `++` (increment), `--` (decrement), `*` (dereference), and `->` (member access).

Here's a simple example demonstrating the usage of iterators in C++:

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};

    // Using iterators to print elements of the vector
    std::cout << "Vector elements: ";
    for (auto it = vec.begin(); it != vec.end(); ++it) {
        std::cout << *it << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this example, `vec.begin()` returns an iterator pointing to the beginning of the vector, and `vec.end()` returns an iterator pointing to one past the last element of the vector. We iterate through the vector using these iterators and print each element.

### 111. Tell us about the iterators invalidation

In C++, iterators can become invalidated under certain circumstances. Iterator invalidation occurs when the iterator is no longer guaranteed to remain valid due to changes in the underlying container. It's essential to be aware of iterator invalidation rules to avoid undefined behavior in your code. Here are some common scenarios where iterator invalidation can occur in C++:

1. **Insertion and Deletion**: When elements are inserted or deleted from a container, iterators pointing to elements within the container might become invalidated. This is particularly relevant for containers like vectors, deques, lists, and maps.

2. **Resizing Containers**: Resizing a container (e.g., using `resize()` for vectors or `rehash()` for unordered maps) may invalidate iterators that point to elements beyond the new size or capacity of the container.

3. **Reallocating Memory**: Containers like `std::vector` may reallocate memory when they reach their capacity limit, invalidating iterators to elements within the vector.

4. **Clearing Containers**: Clearing a container (`clear()` function) invalidates all iterators and references to elements in the container.

5. **Swapping Containers**: Swapping the contents of two containers (`swap()` function or `std::swap()`) can invalidate iterators if the containers' sizes or internal structures differ significantly.

6. **Sorting Operations**: Certain sorting operations (`sort()`, `stable_sort()`, etc.) can invalidate iterators or references to elements within the sorted range.

7. **Using Erase or Remove Algorithms**: Algorithms like `std::remove()` followed by `std::erase()` can invalidate iterators pointing to elements that are removed from the container.

8. **Using Container Adaptors**: Some container adaptors (`std::stack`, `std::queue`, etc.) do not support iterators at all, so attempting to use them may result in compilation errors or undefined behavior.

To mitigate iterator invalidation issues, follow these best practices:

* **Use Stable Containers**: Choose containers that offer stability of iterators, such as `std::list`, when frequent insertions/deletions are expected.
* **Use Iterator Validity Guarantees**: Understand the iterator validity guarantees provided by various container operations and avoid using invalidated iterators.
* **Re-acquire Iterators**: After modifying a container in a way that could invalidate iterators, re-acquire them if needed to ensure they remain valid.
* **Use Algorithms**: Prefer using algorithms from the Standard Library over manually iterating through containers whenever possible, as they often handle iterator invalidation internally.
* **Know Your Containers**: Be aware of the specific iterator invalidation rules for each container type you're working with.

By understanding iterator invalidation and following these best practices, you can write safer and more reliable C++ code.

Sure, here's an example demonstrating iterator invalidation in C++ using a `std::vector`:

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> numbers = {1, 2, 3, 4, 5};

    // Iterator pointing to the third element
    auto it = numbers.begin() + 2; // points to 3

    // Inserting an element before the third element
    numbers.insert(numbers.begin() + 2, 10);

    // Accessing elements using the iterator
    std::cout << "Elements after insertion: ";
    for (auto num : numbers) {
        std::cout << num << " "; // 1 2 10 3 4 5
    }
    std::cout << std::endl;

    // Attempting to access the element through the invalidated iterator
    std::cout << "Accessing element through invalidated iterator: " << *it << std::endl;
    // This will likely result in undefined behavior because 'it' is invalidated by the insertion

    return 0;
}
```

In this example, we have a `std::vector` called `numbers` with elements {1, 2, 3, 4, 5}. We then create an iterator `it` pointing to the third element (value 3).

Next, we insert the value 10 before the third element using `numbers.insert(numbers.begin() + 2, 10)`. This insertion operation invalidates any iterators pointing to elements after the insertion point, including our iterator `it`.

Attempting to dereference the iterator `it` after the insertion operation is undefined behavior because it has been invalidated. This demonstrates the importance of being aware of iterator invalidation when working with containers in C++.

### 112. How to optimize the removal of an element from the middle of a vector?

To optimize the removal of an element from the middle of a vector in C++, you can follow these steps:

1. **Use the Erase-Remove idiom**: This involves using the `std::remove` algorithm along with the `erase` member function of the vector to efficiently remove elements from the vector.

2. **Use iterators**: Iterators allow you to efficiently traverse the vector and perform removal operations without expensive copying.

Here's an example demonstrating how to remove an element from the middle of a vector:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};

    // Element to remove
    int elementToRemove = 3;

    // Find the element in the vector
    auto it = std::find(vec.begin(), vec.end(), elementToRemove);

    if (it != vec.end()) {
        // Efficiently remove the element
        vec.erase(it);

        // Print the updated vector
        for (int num : vec) {
            std::cout << num << " ";
        }
        std::cout << std::endl;
    } else {
        std::cout << "Element not found" << std::endl;
    }

    return 0;
}
```

This code efficiently removes the specified element from the middle of the vector using iterators. The `std::find` algorithm is used to locate the element, and if found, the `erase` member function is called to remove it.

Remember, the complexity of erasing an element from the middle of a vector using this approach is O(n), where n is the number of elements in the vector after the erased element. This is because all subsequent elements need to be shifted to fill the gap left by the removed element.

### 113. How is the vector implemented?

`std::vector` is a standard container in C++ provided by the Standard Template Library (STL) that represents a dynamic array. It is part of the C++ Standard Library and provides functionalities similar to built-in arrays, but with additional features such as automatic memory management, dynamic resizing, and a variety of member functions to manipulate the elements it contains.

Here's a simplified version of how `std::vector` might be implemented:

```cpp
template <typename T>
class vector {
private:
    T* data; // Pointer to the dynamically allocated array
    size_t capacity; // Total capacity of the array
    size_t size; // Number of elements currently stored in the vector

public:
    // Constructor
    vector() : data(nullptr), capacity(0), size(0) {}

    // Destructor
    ~vector() {
        delete[] data; // Free dynamically allocated memory
    }

    // Function to add an element to the end of the vector
    void push_back(const T& value) {
        if (size >= capacity) {
            // If capacity is not sufficient, reallocate memory
            if (capacity == 0)
                capacity = 1; // Start with capacity 1
            else
                capacity *= 2; // Double the capacity

            // Allocate new memory
            T* newData = new T[capacity];

            // Copy existing elements to the new memory
            for (size_t i = 0; i < size; ++i) {
                newData[i] = data[i];
            }

            // Free old memory
            delete[] data;

            // Update pointer to the new memory
            data = newData;
        }

        // Add the new element
        data[size++] = value;
    }

    // Function to get the element at a specific index
    T& operator[](size_t index) {
        if (index < size)
            return data[index];
        throw std::out_of_range("Index out of range");
    }

    // Function to get the number of elements stored in the vector
    size_t get_size() const {
        return size;
    }

    // Function to get the total capacity of the vector
    size_t get_capacity() const {
        return capacity;
    }
};
```

This implementation is a simplified version and does not include all the features and optimizations present in the standard library `std::vector`. It demonstrates the basic functionality of dynamically allocating memory, resizing when necessary, adding elements, and accessing elements by index. Additionally, it lacks error handling and exception safety features present in the standard library version.

### 114. How is the list implemented?

Implementing `std::list` in C++ from scratch can be quite complex, as it's a doubly linked list container with various functionalities adhering to the C++ Standard Library specifications. However, I can provide you with a simplified version of how you could implement a basic doubly linked list in C++. This won't cover all the functionalities of `std::list`, but it should give you a starting point:

```cpp
#include <iostream>

template<typename T>
class ListNode {
public:
    T data;
    ListNode* prev;
    ListNode* next;

    ListNode(const T& data) : data(data), prev(nullptr), next(nullptr) {}
};

template<typename T>
class LinkedList {
private:
    ListNode<T>* head;
    ListNode<T>* tail;
    size_t size;

public:
    LinkedList() : head(nullptr), tail(nullptr), size(0) {}

    ~LinkedList() {
        clear();
    }

    void push_back(const T& data) {
        ListNode<T>* newNode = new ListNode<T>(data);
        if (empty()) {
            head = newNode;
            tail = newNode;
        } else {
            newNode->prev = tail;
            tail->next = newNode;
            tail = newNode;
        }
        size++;
    }

    void pop_back() {
        if (empty()) return;

        ListNode<T>* nodeToRemove = tail;
        tail = tail->prev;
        if (tail)
            tail->next = nullptr;
        else
            head = nullptr;
        delete nodeToRemove;
        size--;
    }

    T& back() {
        return tail->data;
    }

    const T& back() const {
        return tail->data;
    }

    bool empty() const {
        return size == 0;
    }

    size_t getSize() const {
        return size;
    }

    void clear() {
        while (!empty()) {
            pop_back();
        }
    }
};

int main() {
    LinkedList<int> myList;
    myList.push_back(5);
    myList.push_back(10);
    myList.push_back(15);

    std::cout << "Size of list: " << myList.getSize() << std::endl;
    std::cout << "Back element: " << myList.back() << std::endl;

    myList.pop_back();

    std::cout << "Size of list after popping back: " << myList.getSize() << std::endl;
    std::cout << "New back element: " << myList.back() << std::endl;

    return 0;
}
```

This is a very basic implementation that covers adding elements to the back, removing elements from the back, getting the size, and checking if the list is empty. For a full implementation of `std::list`, you would need to add more functionalities like iterators, insertions, deletions, etc.

### 115. How to extend STL containers?

Extending STL containers in C++ typically involves either creating custom container classes that inherit from the STL containers or using template specialization to extend the behavior of existing containers. Here's how you can approach both methods:

#### Method 1: Inheritance

```cpp
#include <iostream>
#include <vector>

// Custom Vector class extending std::vector
template<typename T>
class CustomVector : public std::vector<T> {
public:
    // Constructor
    CustomVector() : std::vector<T>() {}

    // Additional functionality
    void customFunction() {
        // Your custom function implementation here
        std::cout << "Custom function called." << std::endl;
    }
};

int main() {
    CustomVector<int> customVec;
    customVec.push_back(10);
    customVec.customFunction();
    return 0;
}
```

#### Method 2: Template specialization

```cpp
#include <iostream>
#include <vector>

// Template specialization for std::vector
template<typename T>
class ExtendedContainer<std::vector<T>> {
public:
    // Additional functionality
    void customFunction(const std::vector<T>& vec) {
        // Your custom function implementation here
        std::cout << "Custom function called with vector size: " << vec.size() << std::endl;
    }
};

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};
    ExtendedContainer<std::vector<int>> extContainer;
    extContainer.customFunction(vec);
    return 0;
}
```

Both of these methods allow you to extend the behavior of STL containers. Method 1 is generally more straightforward and flexible, as it allows you to add member functions directly to the extended container class. Method 2 can be useful if you want to extend behavior for multiple container types simultaneously, but it requires more advanced template specialization knowledge. Choose the method that best fits your requirements and preferences.

### 116. What are the algorithms in STL?

STL (Standard Template Library) in C++ provides several algorithms that operate on sequences such as vectors, lists, and arrays. These algorithms are defined in header files like `<algorithm>`, `<numeric>`, `<functional>`, etc. Here are some of the commonly used algorithms in STL:

1. **Non-modifying sequence operations**:
   * `std::all_of`, `std::any_of`, `std::none_of`: Check if a condition holds for all, any, or none of the elements in a sequence.
   * `std::count`, `std::count_if`: Count occurrences of elements in a sequence.
   * `std::find`, `std::find_if`, `std::find_if_not`: Find elements in a sequence.
   * `std::equal`, `std::equal_range`: Check equality of two sequences.
   * `std::search`, `std::search_n`: Search for subsequence or consecutive occurrences of an element.
   * `std::lexicographical_compare`: Compare two sequences lexicographically.

2. **Modifying sequence operations**:
   * `std::copy`, `std::copy_if`, `std::copy_n`, `std::copy_backward`: Copy elements from one sequence to another.
   * `std::move`, `std::move_backward`: Move elements from one sequence to another.
   * `std::swap`, `std::swap_ranges`: Swap elements or ranges of elements between sequences.
   * `std::fill`, `std::fill_n`: Fill elements with a value.
   * `std::generate`, `std::generate_n`: Generate elements using a function.
   * `std::replace`, `std::replace_if`, `std::replace_copy`, `std::replace_copy_if`: Replace elements in a sequence.

3. **Sorting and related operations**:
   * `std::sort`, `std::partial_sort`, `std::nth_element`: Sort elements in a sequence.
   * `std::merge`, `std::inplace_merge`: Merge sorted sequences.
   * `std::partition`, `std::stable_partition`: Partition a sequence according to a predicate.
   * `std::next_permutation`, `std::prev_permutation`: Rearrange elements into the next or previous lexicographically greater permutation.
   * `std::is_sorted`, `std::is_sorted_until`: Check if a sequence is sorted.

4. **Binary search operations**:
   * `std::binary_search`: Check if an element exists in a sorted sequence.
   * `std::lower_bound`, `std::upper_bound`, `std::equal_range`: Find the lower, upper bound, or range of elements in a sorted sequence.

5. **Numeric algorithms**:
   * `std::accumulate`: Accumulate values in a sequence.
   * `std::inner_product`: Compute the inner product of two sequences.
   * `std::partial_sum`, `std::inclusive_scan`, `std::exclusive_scan`: Compute partial sums or scans of elements in a sequence.

These are just a subset of the algorithms provided by the STL. They are highly optimized and provide efficient solutions for common operations on sequences.

### 117. What is the difference between vector, deque, list, set in STL?

In C++, the Standard Template Library (STL) provides various container classes, each with its own characteristics and use cases. Here's a brief overview of the differences between vector, deque, list, and set:

1. **Vector (`std::vector`)**:
   * Implemented as a dynamic array that can resize itself dynamically.
   * Elements are stored in contiguous memory locations, which allows for efficient random access.
   * Adding or removing elements from the end of the vector is efficient (`O(1)` amortized time complexity), but adding or removing elements from the middle or front is less efficient (`O(n)` time complexity).
   * Suitable for situations where random access and dynamic resizing are important.

2. **Deque (`std::deque`)**:
   * Stands for double-ended queue.
   * Implemented as a sequence of individual dynamically allocated arrays.
   * Allows for efficient insertion and deletion at both ends (`front` and `back`) of the deque (`O(1)` time complexity).
   * Supports random access (`[]` operator), but accessing elements in the middle is less efficient compared to vectors (`O(n)` time complexity).
   * Suitable for situations where frequent insertion and deletion at both ends are required, and random access to elements is also necessary.

3. **List (`std::list`)**:
   * Implemented as a doubly linked list.
   * Supports efficient insertion and deletion anywhere in the list (`O(1)` time complexity), regardless of the size of the list.
   * Does not support random access directly; accessing elements requires traversing the list from the beginning or end (`O(n)` time complexity).
   * Iterators are invalidated only when the erased element is the one referred to by the iterator.
   * Suitable for situations where frequent insertion and deletion operations are required, and random access is not needed.

4. **Set (`std::set`)**:
   * Represents a sorted associative container that contains unique elements.
   * Implemented as a balanced binary search tree (usually Red-Black Tree).
   * Provides logarithmic time complexity (`O(log n)`) for insertion, deletion, and search operations.
   * Does not allow duplicate elements.
   * Elements are automatically sorted in ascending order.
   * Suitable for situations where you need a sorted collection of unique elements and fast search, insertion, and deletion operations.

In summary:

* Use `std::vector` when you need dynamic resizing with efficient random access.
* Use `std::deque` when you need efficient insertion and deletion at both ends with some random access capability.
* Use `std::list` when you need efficient insertion and deletion anywhere in the list and don't require random access.
* Use `std::set` when you need a sorted collection of unique elements with fast search, insertion, and deletion operations.

### 118. When should I use map? When - unordered_map? What is the complexity of searching and inserting in these containers?

In C++, `std::map` is a container that stores elements formed by a combination of a key value and a mapped value. It's typically implemented as a balanced binary search tree, providing logarithmic time complexity for most operations.

You should consider using `std::map` when:

1. **You need a key-value pair association**: If your data requires a mapping between keys and values, `std::map` provides an efficient way to do so. It ensures uniqueness of keys, maintaining them in sorted order.

2. **Efficient searching and retrieval by key**: If you need to search for elements by their associated keys, `std::map` offers efficient lookup time (logarithmic complexity). This makes it suitable for scenarios where frequent lookups by key are required.

3. **Ordered traversal**: If you need to traverse elements in a specific order (typically sorted order), `std::map` ensures that elements are ordered by their keys, allowing for ordered traversal.

4. **Automatic sorting**: `std::map` automatically maintains the elements sorted according to the keys. This can be useful if your data needs to remain sorted, saving you the effort of manual sorting.

However, there are some considerations to keep in mind:

* **Memory overhead**: `std::map` typically has higher memory overhead compared to other containers due to its tree-based structure.
* **Insertion and deletion cost**: While searching is efficient, insertion and deletion operations might be slower compared to unordered containers like `std::unordered_map` due to the balancing required to maintain the tree structure.
* **Keys must be comparable**: Keys in a `std::map` must be comparable using the less-than operator (`operator<`). This imposes a requirement on the key type.

Overall, `std::map` is a versatile container suitable for situations where ordered associative mapping and efficient key-based retrieval are required. However, if your use case doesn't require ordered traversal or if you need faster insertion and deletion operations, you might want to consider other containers like `std::unordered_map` or `std::unordered_set`.

In C++, `std::unordered_map` is a container that stores elements formed by a combination of a key value and a mapped value, much like `std::map`. However, unlike `std::map`, it is implemented using hash tables, providing constant-time average complexity for most operations, such as insertion, deletion, and lookup.

You should consider using `std::unordered_map` when:

1. **You need a key-value pair association**: Similar to `std::map`, if your data requires a mapping between keys and values, `std::unordered_map` provides an efficient way to achieve this.

2. **Fast insertion, deletion, and lookup**: `std::unordered_map` offers constant-time average complexity for insertion, deletion, and lookup operations. This makes it suitable for scenarios where high-speed access to elements is crucial.

3. **No need for ordered traversal**: If the order of elements doesn't matter or if you can tolerate an unordered traversal, `std::unordered_map` can be more efficient than `std::map`.

4. **Hashing is available for the key type**: Since `std::unordered_map` uses hash tables, the key type must support hashing. Most built-in types in C++ and many user-defined types can be hashed easily, but if you have custom key types, you need to provide a hash function.

Considerations for using `std::unordered_map`:

* **Hash collisions**: In cases where multiple keys map to the same hash value (collisions), performance might degrade as elements need to be stored in a way that handles collisions efficiently.
* **Unordered traversal**: As the name suggests, elements in `std::unordered_map` are not stored in any particular order, so if ordered traversal is necessary, `std::map` might be a better choice.

In summary, `std::unordered_map` is suitable for scenarios where you need fast access to elements and the order of elements is not important. It's particularly efficient for large datasets or scenarios where performance is critical. However, if you need ordered traversal or if you have specific requirements regarding key ordering, you might prefer `std::map`.

The complexity of searching and inserting in `std::map` and `std::unordered_map` differs due to their underlying data structures.

1. **std::map**:
   * **Searching (find operation)**: The complexity for searching in a `std::map` is logarithmic (`O(log n)`), where `n` is the number of elements in the map. This is because `std::map` typically uses a balanced binary search tree (usually a red-black tree) to store its elements, ensuring logarithmic search time.
   * **Inserting (insert operation)**: The complexity for inserting in a `std::map` is also logarithmic (`O(log n)`). This is because insertion involves finding the correct position in the tree to place the new element, which requires traversing the tree, typically with a cost proportional to the logarithm of the number of elements.

2. **std::unordered_map**:
   * **Searching (find operation)**: The complexity for searching in an `std::unordered_map` is constant on average (`O(1)`). This is because `std::unordered_map` uses a hash table to store its elements. Hash tables provide constant-time average complexity for searching, assuming a good hash function and uniform distribution of keys.
   * **Inserting (insert operation)**: The complexity for inserting in an `std::unordered_map` is also constant on average (`O(1)`). Similar to searching, insertion into a hash table has constant-time average complexity, assuming a good hash function and uniform distribution of keys.

It's important to note that while `std::unordered_map` offers constant-time average complexity for searching and inserting, in the worst-case scenario, both operations can degrade to linear time (`O(n)`), particularly if there are many hash collisions. However, the use of good hash functions and appropriate load factors can mitigate this risk.

In summary, if you need fast searching and inserting operations and can tolerate unordered traversal, `std::unordered_map` might be the preferable choice. However, if you need ordered traversal or if your dataset is relatively small and you can tolerate slightly slower operations, `std::map` might be more appropriate.

### 119. How to check if there are elements in the container? Why is calling container.size() a bad practice?

In C++, there are various ways to check if a container has elements. The most common way is to check the `size()` of the container, but there are other methods depending on the type of container. Here's how you can do it for different types of containers:

1. **Using `empty()` function**: Most containers in C++ have an `empty()` member function which returns `true` if the container is empty, and `false` otherwise. This is often the preferred method as it's more readable and idiomatic.

    ```cpp
    #include <iostream>
    #include <vector>

    int main() {
        std::vector<int> vec;
        if (vec.empty()) {
            std::cout << "Vector is empty" << std::endl;
        } else {
            std::cout << "Vector is not empty" << std::endl;
        }
        return 0;
    }
    ```

2. **Using `size()` function**: This method is not recommended if you're only interested in checking if the container is empty because `empty()` is more efficient for most containers. However, if you also need to know the size of the container later, then `size()` can be useful.

    ```cpp
    #include <iostream>
    #include <vector>

    int main() {
        std::vector<int> vec;
        if (vec.size() == 0) {
            std::cout << "Vector is empty" << std::endl;
        } else {
            std::cout << "Vector is not empty" << std::endl;
        }
        return 0;
    }
    ```

3. **Using iterator**: For containers that don't have `empty()` or `size()` functions, you can use iterators to check if the container is empty. If the iterator is equal to `container.end()`, then the container is empty.

    ```cpp
    #include <iostream>
    #include <list>

    int main() {
        std::list<int> lst;
        if (lst.begin() == lst.end()) {
            std::cout << "List is empty" << std::endl;
        } else {
            std::cout << "List is not empty" << std::endl;
        }
        return 0;
    }
    ```

These are some common methods, but the choice of method depends on the specific container and the context of your program.

Calling `container.size()` is not necessarily a bad practice; in fact, it's often a perfectly acceptable and efficient way to check the number of elements in a container. However, there are situations where using `size()` might not be the best choice compared to `empty()`.

Here are a few reasons why `empty()` might be preferred over `size()` in some cases:

1. **Readability and Intent**: Using `empty()` explicitly communicates the intent that you're checking whether the container is empty. This can make the code more readable and easier to understand for other developers.

2. **Performance**: For some container types, like `std::list`, `empty()` may be more efficient than `size()`. For instance, `empty()` for a linked list can be a constant-time operation, while `size()` might require traversing the entire list.

3. **Conciseness**: `empty()` is more concise than comparing `size()` with zero. It's a single function call that directly expresses the desired check.

However, there are situations where you need to know both whether the container is empty and its size. In such cases, using `empty()` to check for emptiness and `size()` when you need the actual size might be the best approach.

Ultimately, whether to use `empty()` or `size()` depends on factors such as readability, performance considerations, and the specific requirements of your code. In many cases, either choice is fine, but it's essential to consider these factors when making the decision.

### 120. What is exception safety guarantee? What kind of exception safety guarantee do STL containers have?

Exception safety guarantee, in the context of C++ Standard Template Library (STL), refers to the level of assurance provided by a function or operation that uses exceptions. It outlines how a function behaves in the presence of exceptions, ensuring that the program remains in a consistent and predictable state even if an exception is thrown.

There are typically three levels of exception safety guarantees:

1. **No-throw guarantee (or strong guarantee)**: This is the highest level of exception safety. It ensures that if an operation fails (throws an exception), the state of the program remains unchanged, as if the operation hadn't been attempted at all. This implies that if an exception occurs, the program is still in a valid and consistent state. Functions that provide this guarantee are said to be exception-safe.

2. **Basic guarantee (or simple guarantee)**: This level of exception safety guarantees that if an operation fails, the program remains in a valid state, but not necessarily in the same state as before the operation. Some resources might have been allocated or modified, but the program will not enter into an invalid or inconsistent state. This level ensures that there are no memory leaks or resource leaks, and any resources that were acquired are properly released. However, the state of the program might have changed, and some invariants could be broken.

3. **No guarantee (or no-throw or weak guarantee)**: This level of exception safety provides no guarantees about the program state in case of an exception. The function might leave the program in an inconsistent state, with resources leaked or partially modified. This level of guarantee is considered the least desirable, as it makes reasoning about the behavior of the program in the presence of exceptions difficult.

When designing or using functions in the STL or any other library, it's important to consider and document the exception safety guarantees they provide. This helps users understand the behavior of these functions in exceptional conditions and write more robust and reliable code. Additionally, providing strong exception safety guarantees is considered good practice in library design.

STL containers typically provide a strong exception safety guarantee, also known as the "no-throw guarantee" or "strong guarantee." This means that operations performed on STL containers ensure that if an exception occurs during the operation, the container remains in its original state, with no changes applied. The operation either succeeds entirely or has no effect at all.

STL containers achieve this guarantee by employing various techniques, such as using copy-and-swap idiom, ensuring strong exception safety for their internal data structures, and properly managing resources during operations.

It's important to note that while most STL containers offer a strong exception safety guarantee, not all operations on containers may provide the same level of guarantee. Users should consult the documentation for specific containers and operations to understand the exception safety guarantees provided by each. Additionally, custom allocators and other configurations may influence the exception safety guarantees of container operations.

### 121. Tell us about the types of smart pointers and the counting of references in them?

In C++, smart pointers are used to manage dynamically allocated memory in a safer and more efficient manner compared to raw pointers. They automatically handle memory deallocation when the pointer is no longer needed, preventing memory leaks and dangling pointers. There are mainly three types of smart pointers in C++:

1. **std::unique_ptr**:
   * Represents exclusive ownership of a dynamically allocated object.
   * Ensures that only one pointer at a time can own the allocated resource.
   * Cannot be copied, only moved.
   * Uses move semantics to transfer ownership.
   * When the unique_ptr goes out of scope or is explicitly reset, the associated resource is automatically deallocated.

2. **std::shared_ptr**:
   * Allows multiple pointers to share ownership of the same dynamically allocated object.
   * Uses reference counting to keep track of how many pointers are referencing the object.
   * When the last shared_ptr referencing the object goes out of scope or is reset, the associated resource is deallocated.
   * Overhead of atomic operations for thread safety in reference counting.

3. **std::weak_ptr**:
   * Provides a non-owning "weak" reference to an object managed by std::shared_ptr.
   * Doesn't affect the reference count.
   * Allows observing an object without preventing it from being deallocated.
   * Used to break circular references between std::shared_ptr instances.

Counting references in smart pointers, especially in std::shared_ptr, is done automatically through the reference counting mechanism. Each std::shared_ptr instance keeps track of the number of shared_ptrs that share ownership of the dynamically allocated object. When the count reaches zero (meaning there are no more shared_ptrs referring to the object), the object is deallocated.

Here's a basic example demonstrating the usage of std::shared_ptr:

```cpp
#include <memory>
#include <iostream>

int main() {
    // Creating a dynamically allocated integer
    std::shared_ptr<int> sharedPtr(new int(42));

    // Creating another shared pointer pointing to the same object
    std::shared_ptr<int> anotherSharedPtr = sharedPtr;

    // Printing the reference count
    std::cout << "Reference count: " << sharedPtr.use_count() << std::endl;

    // Resetting one of the shared pointers
    sharedPtr.reset();

    // Printing the reference count after reset
    std::cout << "Reference count after reset: " << anotherSharedPtr.use_count() << std::endl;

    return 0;
}
```

In this example, both `sharedPtr` and `anotherSharedPtr` share ownership of the dynamically allocated integer. The reference count is obtained using the `use_count()` function, and it's decremented when one of the shared pointers is reset or goes out of scope.

### When can std::vector use std::move?

In C++, `std::move` is used to convert a value to an rvalue, allowing the resources owned by that value to be moved instead of copied. `std::move` is typically used in situations where you want to transfer ownership of resources efficiently, such as when passing arguments to functions or returning values from functions.

For `std::vector`, `std::move` is particularly useful when you want to efficiently move the contents of one vector into another, or when you want to move elements within a vector. Here are a few common scenarios where `std::move` can be used with `std::vector`:

1. **Move construction and move assignment**: When constructing or assigning one vector from another, you can use `std::move` to efficiently move the contents of the source vector into the destination vector.

    ```cpp
    std::vector<int> source = {1, 2, 3, 4, 5};
    std::vector<int> destination = std::move(source); // Move construction
    ```

2. **Moving elements within a vector**: You can use `std::move` to move elements within a vector, for example, when you want to rearrange elements or when you're erasing elements from a vector.

    ```cpp
    std::vector<std::string> strings = {"hello", "world", "foo", "bar"};
    std::move(strings.begin() + 1, strings.begin() + 3, strings.begin() + 2); // Move "world" and "foo" to the third position
    ```

3. **Inserting elements**: When inserting elements into a vector, you can use `std::move` to move elements efficiently, especially when you're inserting elements from another vector or temporary objects.

    ```cpp
    std::vector<std::string> destination;
    std::vector<std::string> source = {"apple", "banana", "cherry"};
    destination.insert(destination.end(), std::make_move_iterator(source.begin()), std::make_move_iterator(source.end()));
    ```

In summary, `std::move` can be used with `std::vector` to efficiently move its contents, either into another vector or within the same vector. However, it's essential to understand the ownership semantics and potential consequences of moving elements, especially when dealing with dynamically allocated resources or objects with complex internal states.

### 51. Tell us about your favorite search algorithm

Quick Sort is a highly efficient sorting algorithm that works by partitioning an array into two sub-arrays, then recursively sorting each sub-array. It follows the divide-and-conquer paradigm. Here's a brief overview of how Quick Sort works:

1. **Choose a Pivot:** Select a pivot element from the array. This can be done in various ways, such as selecting the first element, last element, median-of-three, or a random element.

2. **Partitioning:** Rearrange the array in such a way that all elements less than the pivot are moved to its left, and all elements greater than the pivot are moved to its right. After partitioning, the pivot element is in its correct sorted position.

3. **Recursion:** Recursively apply the above steps to the sub-arrays on the left and right of the pivot, until the entire array is sorted.

4. **Combine:** As the sub-arrays are sorted in place, no further combining step is necessary.

The efficiency of Quick Sort largely depends on the choice of the pivot element. If the pivot is chosen poorly, such as always selecting the smallest or largest element, it can lead to poor performance. However, on average, Quick Sort has a time complexity of O(n log n), making it one of the fastest sorting algorithms in practice.

Here's a simple implementation of the Quick Sort algorithm in Python:

```python
def quick_sort(arr):
    if len(arr) <= 1:
        return arr
    else:
        pivot = arr[0]
        less_than_pivot = [x for x in arr[1:] if x <= pivot]
        greater_than_pivot = [x for x in arr[1:] if x > pivot]
        return quick_sort(less_than_pivot) + [pivot] + quick_sort(greater_than_pivot)

# Example usage:
my_array = [3, 6, 8, 10, 1, 2, 1]
sorted_array = quick_sort(my_array)
print(sorted_array)
```

This implementation selects the first element as the pivot and partitions the array around it. It then recursively sorts the sub-arrays to the left and right of the pivot until the entire array is sorted.

Certainly! Here's an implementation of the Quick Sort algorithm in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to partition the array and return the index of the pivot element
int partition(vector<int> &arr, int low, int high) {
    int pivot = arr[high]; // Choosing the last element as the pivot
    int i = low - 1; // Index of the smaller element

    for (int j = low; j < high; j++) {
        if (arr[j] <= pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]); // Placing the pivot element in its correct position
    return i + 1;
}

// Recursive function to perform quick sort
void quickSort(vector<int> &arr, int low, int high) {
    if (low < high) {
        // Partitioning index
        int pi = partition(arr, low, high);

        // Sorting sub-arrays recursively
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

int main() {
    vector<int> arr = {3, 6, 8, 10, 1, 2, 1};
    int n = arr.size();

    quickSort(arr, 0, n - 1);

    cout << "Sorted array: ";
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;

    return 0;
}
```

In this C++ implementation:

* The `partition` function takes the last element of the array as the pivot and rearranges the elements so that all elements smaller than the pivot are on its left, and all elements greater than the pivot are on its right.
* The `quickSort` function recursively sorts the sub-arrays.
* In the `main` function, we initialize an array, call `quickSort` to sort it, and then print the sorted array.

### What are lock-free and wait-free algorithms? What are their differences and ways of implementation?

Lock-free algorithms are a type of concurrent programming paradigm used in computer science, particularly in multi-threaded environments. In traditional multi-threaded programming, threads often synchronize access to shared resources using locks. However, locks can introduce contention and potential deadlocks, reducing parallelism and performance. Lock-free algorithms aim to circumvent these issues by allowing multiple threads to operate on shared data structures without blocking or waiting for locks.

Key characteristics of lock-free algorithms include:

1. **Non-blocking Progress**: Lock-free algorithms guarantee that at least one thread will make progress even if other threads are delayed or fail to complete their operations.

2. **No Deadlocks**: Since lock-free algorithms do not use locks for synchronization, they inherently avoid deadlock situations where threads wait indefinitely for resources held by other threads.

3. **High Concurrency**: Lock-free algorithms promote high concurrency by enabling multiple threads to access shared data structures simultaneously without contention or blocking.

4. **Scalability**: Lock-free algorithms often exhibit better scalability compared to lock-based approaches, as they reduce contention and allow more parallelism.

Lock-free algorithms can be challenging to design and implement due to the absence of locks for synchronization. Common techniques used in lock-free algorithm design include atomic operations, compare-and-swap (CAS), and memory barriers. These techniques ensure that concurrent operations on shared data structures are performed atomically and in a consistent manner.

Some examples of lock-free algorithms and data structures include:

* **Lock-Free Linked Lists**: These data structures allow multiple threads to insert, delete, and search for elements concurrently without using locks.
* **Lock-Free Queues**: Lock-free queues enable multiple threads to enqueue and dequeue elements concurrently without contention.
* **Lock-Free Hash Tables**: These data structures support concurrent insertions, deletions, and lookups without using locks.

Lock-free algorithms are particularly useful in high-performance computing scenarios, such as real-time systems, parallel computing, and distributed systems, where scalability and responsiveness are critical requirements. However, designing and implementing lock-free algorithms require careful consideration of memory ordering, atomicity, and potential race conditions. Additionally, verifying the correctness of lock-free algorithms can be challenging due to their non-deterministic nature and potential for subtle concurrency bugs.

In C++, implementing lock-free algorithms involves using specific constructs provided by the language and its standard library, particularly the `<atomic>` header and atomic operations. Here are some C++ specifics when it comes to lock-free programming:

1. **Atomic Types**: C++ provides atomic versions of fundamental data types like `int`, `bool`, etc., through the `<atomic>` header. These atomic types ensure that operations on them are performed atomically without the need for explicit locking.

   ```cpp
   #include <atomic>
   std::atomic<int> atomicInt{0};
   atomicInt.store(42); // Atomic store operation
   int value = atomicInt.load(); // Atomic load operation
   ```

2. **Atomic Operations**: C++ provides atomic operations like `store`, `load`, `exchange`, `compare_exchange_weak`, and `compare_exchange_strong` for atomic types. These operations perform the specified operation atomically.

   ```cpp
   std::atomic<int> atomicInt{0};
   atomicInt.store(42, std::memory_order_relaxed); // Store operation with relaxed memory order
   int oldValue = atomicInt.exchange(10); // Atomically exchange value and set to 10
   ```

3. **Memory Ordering**: Atomic operations can specify memory ordering constraints using `std::memory_order` enum. This allows fine-grained control over the visibility and ordering of memory operations.

   ```cpp
   std::atomic<int> atomicInt{0};
   atomicInt.store(42, std::memory_order_release); // Release semantics
   int value = atomicInt.load(std::memory_order_acquire); // Acquire semantics
   ```

4. **Lock-Free Data Structures**: C++ doesn't provide built-in lock-free data structures in its standard library, but you can implement them using atomic operations. Common lock-free data structures like lock-free queues, stacks, and linked lists can be constructed using atomic types and operations.

   ```cpp
   template <typename T>
   class LockFreeQueue {
   public:
       void enqueue(const T& value) {
           Node* newNode = new Node(value);
           Node* oldTail = tail.load();
           while (true) {
               if (oldTail == tail.load()) {
                   Node* oldNext = oldTail->next.load();
                   if (oldNext == nullptr) {
                       if (oldTail->next.compare_exchange_weak(oldNext, newNode)) {
                           tail.compare_exchange_strong(oldTail, newNode);
                           return;
                       }
                   } else {
                       tail.compare_exchange_strong(oldTail, oldNext);
                   }
               }
           }
       }
       // Other methods like dequeue, etc.
   private:
       struct Node {
           T data;
           std::atomic<Node*> next;
           Node(const T& value) : data(value), next(nullptr) {}
       };
       std::atomic<Node*> head;
       std::atomic<Node*> tail;
   };
   ```

5. **Memory Model**: C++11 introduced a memory model that specifies how threads interact with memory. Understanding this memory model is crucial when designing lock-free algorithms, as it defines the behavior of atomic operations and memory visibility across threads.

Lock-free programming in C++ requires a deep understanding of atomic operations, memory ordering, and the C++ memory model. While the language provides powerful primitives for lock-free programming, implementing correct and efficient lock-free algorithms can still be challenging and requires careful consideration of concurrency issues.

Wait-free algorithms represent a more stringent form of concurrency control than lock-free algorithms. In a wait-free algorithm, every thread is guaranteed to complete its operation in a finite number of steps, regardless of the behavior or progress of other threads. This means that no thread is ever forced to wait indefinitely for the completion of another thread's operation.

Here are some key aspects and characteristics of wait-free algorithms:

1. **Guaranteed Progress**: Wait-free algorithms ensure that every thread, regardless of contention or system load, will complete its operation within a bounded number of steps.

2. **No Blocking**: Unlike lock-free algorithms where threads may occasionally stall or wait for the completion of other threads' operations, wait-free algorithms completely eliminate any form of blocking or stalling.

3. **Independence**: Threads executing wait-free algorithms operate independently of one another. They do not rely on the progress or completion of other threads' operations to make progress themselves.

4. **Performance and Scalability**: Wait-free algorithms typically exhibit excellent performance and scalability since they guarantee constant-time progress for each thread, even under high contention.

5. **Complexity**: Designing and implementing wait-free algorithms is generally more challenging than lock-free algorithms. Ensuring wait-freedom often requires intricate synchronization techniques and careful consideration of shared data structures and memory management.

Wait-free algorithms are particularly important in real-time systems, high-performance computing, and safety-critical applications where bounded execution times and responsiveness are paramount. However, achieving wait-freedom can be difficult and may not always be feasible for all types of algorithms or data structures.

It's worth noting that wait-free algorithms are a subset of lock-free algorithms. While all wait-free algorithms are lock-free, not all lock-free algorithms are wait-free. Wait-freedom represents a stronger guarantee of progress and concurrency control compared to lock-freedom.

Implementing wait-free algorithms in C++ involves similar concepts as lock-free algorithms, but with an additional requirement of ensuring that every thread completes its operation within a bounded number of steps, regardless of the behavior of other threads. Here's how you can approach wait-free programming in C++:

1. **Atomic Operations**: Use atomic operations provided by the `<atomic>` header to ensure that operations on shared data are performed atomically without the need for explicit locking.

```cpp
#include <atomic>
std::atomic<int> sharedData{0};

void incrementData() {
    sharedData.fetch_add(1, std::memory_order_relaxed);
}
```

1. **Memory Ordering**: Specify memory ordering constraints using `std::memory_order` enum to control the visibility and ordering of memory operations. It's essential to ensure that the memory ordering is carefully chosen to maintain the wait-free property.

```cpp
#include <atomic>
std::atomic<int> sharedData{0};

void incrementData() {
    sharedData.fetch_add(1, std::memory_order_release);
}
```

1. **Algorithm Design**: Design algorithms in such a way that every thread is guaranteed to complete its operation within a bounded number of steps, irrespective of other threads' behavior. This may involve careful consideration of data structures and synchronization techniques.

```cpp
template <typename T>
class WaitFreeQueue {
public:
    bool enqueue(const T& value) {
        Node* newNode = new Node(value);
        Node* oldHead = head.load();
        newNode->next = oldHead;
        while (!head.compare_exchange_weak(oldHead, newNode)) {
            newNode->next = oldHead;
        }
        return true;
    }

    bool dequeue(T& value) {
        Node* oldHead = head.load();
        if (oldHead == nullptr)
            return false;
        Node* newHead = oldHead->next;
        value = oldHead->data;
        delete oldHead;
        while (!head.compare_exchange_weak(oldHead, newHead)) {
            if (oldHead == nullptr)
                return false;
            newHead = oldHead->next;
            value = oldHead->data;
            delete oldHead;
        }
        return true;
    }

private:
    struct Node {
        T data;
        Node* next;
        Node(const T& value) : data(value), next(nullptr) {}
    };

    std::atomic<Node*> head{nullptr};
};
```

1. **Memory Model**: Understand the C++ memory model and ensure that your implementation complies with it to avoid data races and undefined behavior.

Wait-free programming in C++ requires a deep understanding of concurrent programming concepts, atomic operations, memory ordering, and algorithm design. While achieving wait-freedom can be challenging, it ensures predictable and bounded behavior, making it suitable for real-time systems and critical applications where responsiveness is crucial.

Lock-free and wait-free algorithms are both concurrency control techniques used in multi-threaded programming, but they differ in their guarantees and implementation approaches:

1. **Guarantees**:

   * **Lock-Free**: In lock-free algorithms, at least one thread is guaranteed to make progress despite the presence of contention or delays caused by other threads. Lock-free algorithms ensure that threads do not block each other, but they do not guarantee a bounded number of steps for each thread's operation to complete.

   * **Wait-Free**: Wait-free algorithms go a step further by guaranteeing that every thread completes its operation within a bounded number of steps, regardless of contention or other threads' behavior. Wait-free algorithms provide stronger progress guarantees compared to lock-free algorithms.

2. **Implementation**:

   * **Lock-Free**: Lock-free algorithms are typically implemented using atomic operations and synchronization primitives such as compare-and-swap (CAS), load-link/store-conditional (LL/SC), and memory barriers. These algorithms ensure that threads can make progress without being blocked by others, even if they may occasionally experience delays due to contention.

   * **Wait-Free**: Wait-free algorithms require careful design and implementation to ensure that every thread completes its operation within a bounded number of steps. This often involves more complex synchronization techniques, such as optimistic concurrency control, hazard pointers, or fine-grained locking. Wait-free algorithms must guarantee that no thread ever waits indefinitely for the completion of another thread's operation.

3. **Concurrency Control**:

   * **Lock-Free**: Lock-free algorithms allow multiple threads to operate concurrently on shared data structures without blocking each other. They ensure progress by ensuring that operations eventually succeed, even if they may experience retries or delays due to contention.

   * **Wait-Free**: Wait-free algorithms provide stronger concurrency guarantees by ensuring that every thread completes its operation within a bounded number of steps, regardless of contention or other threads' behavior. This eliminates the possibility of threads waiting indefinitely for the completion of others' operations.

4. **Use Cases**:

   * **Lock-Free**: Lock-free algorithms are suitable for scenarios where responsiveness and scalability are important, but a bounded completion time for each thread's operation is not strictly required. They are commonly used in high-performance computing, real-time systems, and distributed systems.

   * **Wait-Free**: Wait-free algorithms are ideal for real-time systems and safety-critical applications where bounded execution times and responsiveness are critical requirements. They ensure that every thread makes progress within a predictable timeframe, which is essential for meeting strict timing constraints.

In summary, while both lock-free and wait-free algorithms aim to provide non-blocking concurrency control, wait-free algorithms offer stronger guarantees by ensuring that every thread completes its operation within a bounded number of steps. Implementing wait-free algorithms requires more sophisticated synchronization techniques compared to lock-free algorithms. Choosing between lock-free and wait-free algorithms depends on the specific requirements and constraints of the application, particularly regarding timing guarantees and responsiveness.

### 53. Describe the purpose of execution policy for parallel algorithms

In C++, the execution policy for parallel algorithms serves as a mechanism for specifying the execution strategy or constraints for algorithms that can be executed in parallel. It allows developers to control how computations are parallelized, offering flexibility and optimization opportunities.

The purpose of the execution policy includes:

1. **Control over Parallelism**: Different execution policies enable developers to control the level of parallelism applied to an algorithm. This could involve specifying whether parallel execution should be allowed, or whether the algorithm should execute sequentially.

2. **Performance Optimization**: By choosing the appropriate execution policy, developers can optimize the performance of their algorithms based on the characteristics of the underlying hardware. For example, they can select policies that exploit multi-core processors or take advantage of vectorization instructions.

3. **Safety and Correctness**: Certain execution policies offer guarantees regarding data dependencies and thread safety, helping developers avoid race conditions and other concurrency issues. By adhering to these policies, developers can write parallel algorithms with confidence in their correctness.

4. **Compatibility and Portability**: Standardizing execution policies promotes code portability across different platforms and libraries. Developers can rely on a consistent interface for specifying parallelism, regardless of the underlying execution environment.

5. **Ease of Use and Maintenance**: Execution policies provide a clear and expressive means of expressing parallelism in code. They encapsulate parallelization concerns within the algorithm implementation, making the code easier to understand, maintain, and debug.

Overall, execution policies in C++ facilitate the development of efficient and scalable parallel algorithms while offering developers control, performance optimization, safety, portability, and ease of use. They are an essential feature for modern C++ programming, particularly in applications where parallel processing is crucial for performance gains.

Sure, let's consider an example using the `std::for_each` algorithm from the C++ Standard Library along with different execution policies.

Suppose we have a vector of integers and we want to square each element of the vector in parallel. We can achieve this using the `std::for_each` algorithm with different execution policies. Here's how you can do it:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <execution> // for parallel execution policies

int main() {
    // Create a vector of integers
    std::vector<int> numbers = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

    // Function to square a number
    auto square = [](int& n) { n *= n; };

    // Sequential execution (default)
    std::for_each(numbers.begin(), numbers.end(), square);
    
    // Output the results
    std::cout << "Sequential Result:";
    for (const auto& num : numbers) {
        std::cout << " " << num;
    }
    std::cout << std::endl;

    // Parallel execution with std::execution::seq (sequential)
    std::for_each(std::execution::seq, numbers.begin(), numbers.end(), square);

    // Output the results
    std::cout << "Parallel (Sequential) Result:";
    for (const auto& num : numbers) {
        std::cout << " " << num;
    }
    std::cout << std::endl;

    // Parallel execution with std::execution::par (parallel)
    std::for_each(std::execution::par, numbers.begin(), numbers.end(), square);

    // Output the results
    std::cout << "Parallel Result:";
    for (const auto& num : numbers) {
        std::cout << " " << num;
    }
    std::cout << std::endl;

    return 0;
}
```

In this example:

* We define a vector `numbers` containing some integers.
* We define a lambda function `square` which squares a given integer.
* We use `std::for_each` with different execution policies:
  * `std::execution::seq`: This enforces sequential execution, i.e., it doesn't parallelize the operation.
  * `std::execution::par`: This requests parallel execution, allowing the implementation to execute the operation in parallel if possible.

Finally, we output the results after each operation to see the effect of the different execution policies.

### 83. What are the standard containers and what structures are they based on?

<--- Return later: Data structures --->
