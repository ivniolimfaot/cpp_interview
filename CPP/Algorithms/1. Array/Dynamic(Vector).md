### 1. Algorithms & Data Structures (C++): Using Vector Container

Using the `std::vector` container in C++ for implementing algorithms and data structures provides a versatile and efficient way to manage dynamic arrays. Here are some common operations and scenarios where you might use `std::vector`:

1. **Dynamic Array**: `std::vector` provides a dynamic array that grows automatically as elements are inserted.

    ```cpp
    #include <vector>
    #include <iostream>

    int main() {
        std::vector<int> dynamicArray;
        dynamicArray.push_back(10);
        dynamicArray.push_back(20);
        dynamicArray.push_back(30);

        for (int num : dynamicArray) {
            std::cout << num << " ";
        }

        return 0;
    }
    ```

2. **Iterating over a Vector**:

    ```cpp
    for (auto it = dynamicArray.begin(); it != dynamicArray.end(); ++it) {
        std::cout << *it << " ";
    }
    ```

3. **Accessing Elements**:

    ```cpp
    int thirdElement = dynamicArray[2];
    ```

4. **Inserting and Erasing Elements**:

    ```cpp
    dynamicArray.insert(dynamicArray.begin() + 1, 15); // Insert 15 at index 1
    dynamicArray.erase(dynamicArray.begin() + 2); // Erase element at index 2
    ```

5. **Sorting**:

    ```cpp
    #include <algorithm>

    std::sort(dynamicArray.begin(), dynamicArray.end());
    ```

6. **Searching**:

    ```cpp
    #include <algorithm>

    auto it = std::find(dynamicArray.begin(), dynamicArray.end(), 20);
    if (it != dynamicArray.end()) {
        std::cout << "Element found at index " << std::distance(dynamicArray.begin(), it);
    } else {
        std::cout << "Element not found";
    }
    ```

7. **Resizing**:

    ```cpp
    dynamicArray.resize(10); // Resize to 10 elements
    ```

8. **Capacity**:

    ```cpp
    std::cout << "Size: " << dynamicArray.size() << std::endl;
    std::cout << "Capacity: " << dynamicArray.capacity() << std::endl;
    ```

9. **Clearing the Vector**:

    ```cpp
    dynamicArray.clear();
    ```

`std::vector` provides many other functionalities as well, making it one of the most versatile containers in the C++ Standard Library for managing dynamic arrays.

### 1. Algorithms & Data Structures (C++): Vector

Vectors in C++ are a versatile data structure provided by the Standard Template Library (STL). They are similar to arrays but with dynamic resizing capability, making them more flexible and efficient in many cases. Here's a brief overview:

#### Declaration

To use vectors, you need to include the `<vector>` header file.

```cpp
#include <vector>
```

#### Creating a Vector

You can create a vector for a specific data type like so:

```cpp
std::vector<int> myVector; // Creates an empty vector of integers
```

#### Initialization

Vectors can be initialized with a size and optionally with an initial value:

```cpp
std::vector<int> myVector(5); // Creates a vector of size 5 with default-initialized integers
std::vector<int> myVector(5, 10); // Creates a vector of size 5 with all elements initialized to 10
```

#### Accessing Elements

You can access elements using the same syntax as arrays:

```cpp
myVector[0] = 42; // Accessing and modifying the first element
int element = myVector[1]; // Accessing the second element
```

#### Iterating Over Elements

You can iterate over the elements of a vector using iterators or range-based for loops:

```cpp
for (auto it = myVector.begin(); it != myVector.end(); ++it) {
    // Access *it to get the element
}

// Or, using range-based for loop
for (int element : myVector) {
    // Access element directly
}
```

#### Modifying Vector Size

Vectors can dynamically resize themselves using the `push_back()` method to add elements:

```cpp
myVector.push_back(5); // Adds 5 to the end of the vector
```

You can also use `resize()` to change the size of the vector:

```cpp
myVector.resize(10); // Resizes the vector to have 10 elements
```

#### Other Useful Methods

* `size()`: Returns the number of elements in the vector.
* `empty()`: Returns true if the vector is empty.
* `clear()`: Removes all elements from the vector.

#### Efficiency

Vectors offer constant-time access to elements (`O(1)`), but resizing the vector can be costly if it exceeds its capacity, as it may require allocating new memory and copying existing elements (`O(n)` amortized time).

#### Memory Management

Vectors manage memory dynamically, automatically handling memory allocation and deallocation. They typically allocate more memory than needed to accommodate future growth efficiently.

#### When to Use

Vectors are suitable for situations where you need a dynamic array-like data structure with fast random access and insertion/deletion at the end. However, if you need frequent insertions or deletions in the middle, other data structures like linked lists might be more appropriate due to their better performance characteristics.

### 1. Algorithms & Data Structures (C++): Vector Class

Creating a vector class in C++ is a great exercise to understand how dynamic arrays work. Here's a basic implementation of a vector class along with some common operations like adding elements, accessing elements, and resizing the vector.

```cpp
#include <iostream>

template <typename T>
class Vector {
private:
    T* array;
    size_t capacity;
    size_t length;

public:
    Vector() : capacity(10), length(0) {
        array = new T[capacity];
    }

    ~Vector() {
        delete[] array;
    }

    // Add element at the end
    void push_back(const T& value) {
        if (length >= capacity) {
            resize(capacity * 2); // Double the capacity
        }
        array[length++] = value;
    }

    // Access element at index
    T& operator[](size_t index) {
        if (index >= length) {
            throw std::out_of_range("Index out of range");
        }
        return array[index];
    }

    // Get size of the vector
    size_t size() const {
        return length;
    }

    // Resize the vector
    void resize(size_t newCapacity) {
        T* newArray = new T[newCapacity];
        for (size_t i = 0; i < length; ++i) {
            newArray[i] = array[i];
        }
        delete[] array;
        array = newArray;
        capacity = newCapacity;
    }
};

int main() {
    Vector<int> vec;
    for (int i = 0; i < 20; ++i) {
        vec.push_back(i);
    }

    // Access elements and print
    for (size_t i = 0; i < vec.size(); ++i) {
        std::cout << vec[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

This is a very basic implementation that lacks many features a real-world vector implementation would have (like iterators, iterators range constructors, memory allocation optimizations, etc.), but it serves as a good starting point for understanding the basic functionality of vectors.

When implementing a vector class, remember to handle edge cases like out-of-bounds access and memory management properly. And it's always a good practice to test your implementation with various scenarios to ensure correctness.

### 1. Algorithms & Data Structures (C++): Vector Data Structure

Sure, let's dive into the vector data structure in C++.

In C++, a vector is a dynamic array that can resize itself automatically when it needs to accommodate more elements. It's part of the Standard Template Library (STL) and provides functionalities similar to arrays but with additional features such as dynamic resizing, bounds-checking, and convenience functions.

Here's a basic overview of how you can use vectors in C++:

#### Including the necessary header file

```cpp
#include <vector>
```

#### Declaring a vector

```cpp
std::vector<int> myVector; // Declares an empty vector of integers
```

#### Initializing a vector with elements

```cpp
std::vector<int> myVector = {1, 2, 3, 4, 5}; // Initializes a vector with 5 elements
```

#### Accessing elements

```cpp
int element = myVector[2]; // Accesses the third element (index 2) of the vector
```

#### Adding elements

```cpp
myVector.push_back(6); // Adds 6 to the end of the vector
```

#### Removing elements

```cpp
myVector.pop_back(); // Removes the last element from the vector
```

#### Size and capacity

```cpp
int size = myVector.size(); // Returns the number of elements in the vector
int capacity = myVector.capacity(); // Returns the current capacity of the vector
```

#### Iterating through the vector

```cpp
for (int i = 0; i < myVector.size(); ++i) {
    std::cout << myVector[i] << " ";
}
```

#### Using iterators

```cpp
for (auto it = myVector.begin(); it != myVector.end(); ++it) {
    std::cout << *it << " ";
}
```

#### Clearing the vector

```cpp
myVector.clear(); // Removes all elements from the vector
```

#### Checking if vector is empty

```cpp
if (myVector.empty()) {
    // Vector is empty
}
```

Vectors are quite versatile and provide a lot of functionalities, making them one of the most commonly used data structures in C++. They're especially handy when you need a dynamic array that can grow or shrink in size as needed.

### 1. Algorithms & Data Structures (C++): Vector Data Structures

Vectors are a fundamental data structure in C++ that provide dynamic array-like functionality with automatic resizing. They're part of the Standard Template Library (STL) and are widely used due to their flexibility and efficiency.

Here's a brief overview of vectors in C++:

1. **Declaration and Initialization:**

   ```cpp
   #include <vector>

   std::vector<int> vec; // Declares an empty vector of integers
   std::vector<int> vec2(5); // Declares a vector of 5 integers, initialized to 0
   std::vector<int> vec3 = {1, 2, 3}; // Declares and initializes a vector with values
   ```

2. **Accessing Elements:**

   ```cpp
   std::cout << vec[0]; // Accesses the first element (indexing starts from 0)
   ```

3. **Adding Elements:**

   ```cpp
   vec.push_back(10); // Adds an element with value 10 at the end
   ```

4. **Size and Capacity:**

   ```cpp
   vec.size(); // Returns the number of elements in the vector
   vec.capacity(); // Returns the number of elements that the vector can hold without reallocating memory
   ```

5. **Iteration:**

   ```cpp
   for (int i = 0; i < vec.size(); ++i) {
       std::cout << vec[i] << " ";
   }
   ```

6. **Iterators:**

   ```cpp
   for (auto it = vec.begin(); it != vec.end(); ++it) {
       std::cout << *it << " ";
   }
   ```

7. **Inserting and Erasing Elements:**

   ```cpp
   vec.insert(vec.begin() + 2, 20); // Inserts 20 at the third position
   vec.erase(vec.begin() + 1); // Removes the element at the second position
   ```

8. **Sorting:**

   ```cpp
   std::sort(vec.begin(), vec.end()); // Sorts the vector in ascending order
   ```

9. **Other Operations:**
   * `vec.empty()`: Checks if the vector is empty.
   * `vec.clear()`: Removes all elements from the vector.
   * `vec.pop_back()`: Removes the last element from the vector.
   * `vec.front()`, `vec.back()`: Accesses the first and last elements, respectively.

Vectors provide amortized constant time complexity O(1) for adding elements to the end, and linear time O(n) for inserting or removing elements at arbitrary positions. They also provide random access with constant time complexity O(1). However, inserting or removing elements from the beginning or middle of the vector can be costly because it may require shifting all subsequent elements.

### 1. Algorithms & Data Structures (C++): Vector of Vector

In C++, a vector of vectors is essentially a 2D dynamic array. It allows you to create a structure where each element is itself a vector, enabling you to represent a 2D grid or matrix. Here's how you can use it:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    // Creating a vector of vectors
    vector<vector<int>> matrix;

    // Adding elements to the matrix
    // Let's say we want a 3x3 matrix initialized with zeros
    int rows = 3;
    int cols = 3;
    for (int i = 0; i < rows; ++i) {
        vector<int> row;
        for (int j = 0; j < cols; ++j) {
            row.push_back(0); // Initializing each element with zero
        }
        matrix.push_back(row);
    }

    // Accessing and modifying elements
    matrix[0][0] = 1;
    matrix[1][1] = 2;
    matrix[2][2] = 3;

    // Displaying the matrix
    for (int i = 0; i < rows; ++i) {
        for (int j = 0; j < cols; ++j) {
            cout << matrix[i][j] << " ";
        }
        cout << endl;
    }

    return 0;
}
```

This code demonstrates how to create, initialize, access, and modify elements of a 3x3 matrix using a vector of vectors. You can adjust the size of the matrix by changing the `rows` and `cols` variables.

### 1. Algorithms & Data Structures (C++): Vector STL

The Vector STL (Standard Template Library) in C++ is a dynamic array that provides similar functionalities as arrays but with additional capabilities like dynamic resizing, easy insertion and deletion of elements, and automatic memory management. Here's a breakdown of some key aspects:

1. **Dynamic Resizing**: Unlike traditional arrays in C++, vectors can dynamically resize themselves to accommodate more elements. This means you don't need to specify the size upfront, and the vector can grow as needed.

2. **Automatic Memory Management**: Vectors handle memory allocation and deallocation automatically. You don't need to manage memory manually like you would with raw arrays, which helps prevent memory leaks and buffer overflows.

3. **Random Access**: Vectors support random access to elements, meaning you can access any element in constant time using array-like indexing.

4. **Insertion and Deletion**: Vectors provide efficient insertion and deletion of elements at the end (with `push_back()` and `pop_back()`) and in the middle (with `insert()` and `erase()`), although inserting or removing elements in the middle of a vector can be less efficient compared to other data structures like lists.

5. **Iterators**: Vectors support iterators, which allow you to traverse the elements of the vector using iterator-based loops or algorithms from the STL.

Here's a simple example demonstrating the basic usage of vectors:

```cpp
#include <iostream>
#include <vector>

int main() {
    // Declare an empty vector of integers
    std::vector<int> numbers;

    // Add elements to the vector
    numbers.push_back(10);
    numbers.push_back(20);
    numbers.push_back(30);

    // Access elements using indexing
    std::cout << "First element: " << numbers[0] << std::endl;
    std::cout << "Second element: " << numbers[1] << std::endl;

    // Iterate over the vector using iterators
    std::cout << "All elements:";
    for (auto it = numbers.begin(); it != numbers.end(); ++it) {
        std::cout << " " << *it;
    }
    std::cout << std::endl;

    // Remove the last element
    numbers.pop_back();

    // Insert an element at the beginning
    numbers.insert(numbers.begin(), 5);

    // Remove the second element
    numbers.erase(numbers.begin() + 1);

    // Print the modified vector
    std::cout << "Modified vector:";
    for (int num : numbers) {
        std::cout << " " << num;
    }
    std::cout << std::endl;

    return 0;
}
```

This code demonstrates basic operations such as adding elements, accessing elements, iterating through the vector, removing elements, and inserting elements at specific positions.

### 1. Algorithms & Data Structures (C++): Vector: Find Longest String

To find the longest string in a vector of strings in C++, you can iterate through the vector and keep track of the longest string found so far. Here's a simple example:

```cpp
#include <iostream>
#include <vector>
#include <string>

std::string findLongestString(const std::vector<std::string>& strings) {
    if (strings.empty()) {
        return ""; // Return empty string if vector is empty
    }

    std::string longest = strings[0]; // Assume first string is the longest
    for (const auto& str : strings) {
        if (str.length() > longest.length()) {
            longest = str; // Update longest string if a longer one is found
        }
    }
    return longest;
}

int main() {
    std::vector<std::string> strings = {"apple", "banana", "kiwi", "orange", "strawberry"};

    std::string longest = findLongestString(strings);
    if (longest.empty()) {
        std::cout << "Vector is empty!" << std::endl;
    } else {
        std::cout << "Longest string: " << longest << std::endl;
    }

    return 0;
}
```

In this code:

* The `findLongestString` function takes a vector of strings as input and returns the longest string found in the vector.
* Inside `findLongestString`, it first checks if the vector is empty and returns an empty string if it is.
* It then initializes the `longest` variable with the first string in the vector.
* It iterates through the vector and updates `longest` if it finds a string longer than the current `longest`.
* In the `main` function, we create a vector of strings and call `findLongestString` to find the longest string, then print it out.

### 1. Algorithms & Data Structures (C++): Vector: Find Max Min

To find the maximum and minimum elements in a vector in C++, you can use the `std::max_element` and `std::min_element` functions, respectively, which are provided by the `<algorithm>` header. Here's how you can do it:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> vec = {3, 7, 2, 9, 1, 5};
    
    // Finding maximum element
    auto max_itr = std::max_element(vec.begin(), vec.end());
    if (max_itr != vec.end()) {
        std::cout << "Maximum element: " << *max_itr << std::endl;
    } else {
        std::cout << "Vector is empty" << std::endl;
    }

    // Finding minimum element
    auto min_itr = std::min_element(vec.begin(), vec.end());
    if (min_itr != vec.end()) {
        std::cout << "Minimum element: " << *min_itr << std::endl;
    } else {
        std::cout << "Vector is empty" << std::endl;
    }

    return 0;
}
```

In this code:

* `std::max_element` returns an iterator pointing to the maximum element in the vector.
* `std::min_element` returns an iterator pointing to the minimum element in the vector.

Remember to include the necessary headers (`iostream`, `vector`, and `algorithm`) at the beginning of your code. This code will output the maximum and minimum elements of the vector `vec`.

### 1. Algorithms & Data Structures (C++): Vector: Inbuilt Searching

In C++, the `std::vector` container provides a method for searching elements, namely `std::find`, which is defined in the `<algorithm>` header. This function returns an iterator pointing to the first occurrence of the element in the vector, or the `end()` iterator if the element is not found.

Here's how you can use `std::find` with a vector:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> vec = {10, 20, 30, 40, 50};

    // Searching for element 30
    auto it = std::find(vec.begin(), vec.end(), 30);

    if (it != vec.end()) {
        std::cout << "Element found at index: " << std::distance(vec.begin(), it) << std::endl;
    } else {
        std::cout << "Element not found" << std::endl;
    }

    return 0;
}
```

In this example, `std::find` searches for the value `30` in the vector `vec`. If it finds the value, it returns an iterator pointing to that position. If not, it returns `vec.end()`. We then check if the iterator is equal to `vec.end()` to determine whether the element was found or not. If it's not equal, we print the index where the element was found; otherwise, we print that the element was not found.

This is a basic example, and you can extend it for more complex scenarios or different data types as needed.

### 1. Algorithms & Data Structures (C++): Vector: Max Profit

To find the maximum profit from buying and selling stocks represented by their prices on consecutive days, you can use the following algorithm implemented in C++ using vectors:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int maxProfit(std::vector<int>& prices) {
    int maxProfit = 0;
    int minPrice = INT_MAX; // Initialize minPrice to the maximum possible value

    for (int price : prices) {
        // Update minPrice to the lowest price encountered so far
        minPrice = std::min(minPrice, price);
        
        // Update maxProfit to the maximum profit encountered so far
        maxProfit = std::max(maxProfit, price - minPrice);
    }

    return maxProfit;
}

int main() {
    std::vector<int> prices = {7, 1, 5, 3, 6, 4}; // Example prices array
    int max_profit = maxProfit(prices);
    std::cout << "Maximum profit: " << max_profit << std::endl;
    return 0;
}
```

This algorithm iterates through the prices array once, keeping track of the minimum price seen so far and updating the maximum profit accordingly. Finally, it returns the maximum profit that can be obtained.

### 1. Algorithms & Data Structures (C++): Vector: Max Sub Array

The maximum subarray problem is a classic algorithmic problem where the task is to find the contiguous subarray within a one-dimensional array, containing at least one number, which has the largest sum. This problem can be solved efficiently using various algorithms, one of the most popular being Kadane's algorithm.

Here's how you can implement Kadane's algorithm in C++ to find the maximum subarray sum:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int maxSubArray(vector<int>& nums) {
    int maxSum = nums[0];
    int currentSum = nums[0];

    for (int i = 1; i < nums.size(); ++i) {
        // Choose between extending the previous subarray or start a new subarray
        currentSum = max(nums[i], currentSum + nums[i]);
        // Update maxSum if the current sum is greater
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

This code snippet defines the `maxSubArray` function which takes a vector of integers `nums` and returns the maximum subarray sum. The algorithm iterates through the array once, maintaining two variables `currentSum` and `maxSum`. `currentSum` tracks the maximum sum of subarrays ending at the current position, while `maxSum` keeps track of the overall maximum sum found so far. At each step, it decides whether to start a new subarray or extend the previous one based on which choice yields a larger sum. Finally, it returns the `maxSum`, which represents the maximum subarray sum.

### 1. Algorithms & Data Structures (C++): Vector: Remove Duplicates

To remove duplicates from a vector in C++, you can use various approaches. One common approach is to use the `std::sort` algorithm to sort the vector, then use `std::unique` to remove consecutive duplicates, and finally, erase the elements that `std::unique` moved to the end of the vector. Here's how you can implement it:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

void removeDuplicates(std::vector<int>& vec) {
    // Step 1: Sort the vector
    std::sort(vec.begin(), vec.end());
    
    // Step 2: Remove consecutive duplicates
    auto it = std::unique(vec.begin(), vec.end());
    
    // Step 3: Erase the duplicates
    vec.erase(it, vec.end());
}

int main() {
    std::vector<int> numbers = {1, 2, 3, 2, 4, 5, 3, 6, 7, 4};
    
    std::cout << "Original vector: ";
    for (int num : numbers) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
    
    removeDuplicates(numbers);
    
    std::cout << "Vector after removing duplicates: ";
    for (int num : numbers) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
    
    return 0;
}
```

This code will output:

```bash
Original vector: 1 2 3 2 4 5 3 6 7 4 
Vector after removing duplicates: 1 2 3 4 5 6 7 
```

This method has a time complexity of O(n log n) due to the sorting operation. If the vector is already sorted or if you want to maintain the original order of elements, you can use alternative approaches such as using a hash set to track unique elements.

### 1. Algorithms & Data Structures (C++): Vector: Remove Element

Certainly! In C++, the `std::vector` container provides a method called `erase` to remove elements. You can specify either an iterator to the element you want to remove or a range of elements to remove.

Here's how you can use `erase` to remove a specific element from a vector:

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};

    // Let's say we want to remove the element at index 2 (3rd element)
    size_t indexToRemove = 2;

    if (indexToRemove < vec.size()) {
        vec.erase(vec.begin() + indexToRemove); // erase() takes an iterator pointing to the element to remove
        std::cout << "Element at index " << indexToRemove << " removed.\n";
    } else {
        std::cerr << "Index out of range.\n";
    }

    // Print the elements after removal
    for (int num : vec) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this example, the element at index 2 (third element, since indexing starts from 0) is removed from the vector.

Remember, `erase` takes an iterator to the element you want to remove. So, `vec.begin() + indexToRemove` gives an iterator pointing to the element at the specified index.

### 1. Algorithms & Data Structures (C++): Vector: Rotate

In C++, rotating a vector involves shifting its elements either to the left or right by a specified number of positions. The `rotate` function in the `<algorithm>` header can be used for this purpose. Here's how you can use it:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};

    // Rotate left by 2 positions
    std::rotate(vec.begin(), vec.begin() + 2, vec.end());

    // Print the rotated vector
    for (int num : vec) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

This code will output:

```bash
3 4 5 1 2
```

The `rotate` function takes three arguments:

1. `first`: Iterator to the first element in the range.
2. `middle`: Iterator to the element that should become the new first element after rotation.
3. `last`: Iterator to the element past the end of the range.

In the example, `vec.begin()` points to the first element of the vector, `vec.begin() + 2` points to the third element (which becomes the first element after rotation), and `vec.end()` points to one past the last element of the vector.

If you want to rotate the vector to the right, you can simply adjust the `middle` iterator accordingly. For example, to rotate the vector right by 2 positions:

```cpp
std::rotate(vec.rbegin(), vec.rbegin() + 2, vec.rend());
```

This will rotate the vector to the right by 2 positions.

### 1. Algorithms & Data Structures (C++): Vectors

Vectors in C++ are a fundamental data structure provided by the Standard Template Library (STL) for dynamic arrays. They offer dynamic resizing, efficient random access, and contiguous memory allocation, making them a versatile choice for storing sequences of elements.

Here's a basic overview of vectors in C++:

#### Declaration

```cpp
#include <vector>

std::vector<int> vec;

```

#### Declaration and Initialization

Vectors can be declared and initialized in several ways:

1. **Empty Vector**:

```cpp
std::vector<int> vec; // Creates an empty vector of integers
```

1. **With Initial Size**:

```cpp
std::vector<int> vec(5); // Creates a vector of 5 integers, initialized to default value (0 for int)
```

1. **With Initial Size and Value**:

```cpp
std::vector<int> vec(5, 10); // Creates a vector of 5 integers, initialized to 10
```

1. **Using Initialization List**:

```cpp
std::vector<int> vec = {1, 2, 3, 4, 5}; // Creates a vector with specified elements
```

#### Accessing Elements

Vectors support random access, meaning you can access elements by their index.

```cpp
std::vector<int> vec = {1, 2, 3, 4, 5};
int firstElement = vec[0]; // Accessing the first element
int thirdElement = vec[2]; // Accessing the third element
```

#### Modifying Elements

You can modify elements in a vector similar to arrays.

```cpp
std::vector<int> vec = {1, 2, 3, 4, 5};
vec[0] = 10; // Modifying the first element
vec[2] = 30; // Modifying the third element
```

#### Vector Operations

* **Push Back**: Adds an element to the end of the vector.

  ```cpp
  vec.push_back(6);
  ```

* **Pop Back**: Removes the last element from the vector.

  ```cpp
  vec.pop_back();
  ```

* **Size**: Returns the number of elements in the vector.

  ```cpp
  int size = vec.size();
  ```

* **Iterating through Vector**:

  ```cpp
  for (int i = 0; i < vec.size(); ++i) {
      std::cout << vec[i] << " ";
  }
  ```

* **Range-based For Loop** (C++11 onwards):

  ```cpp
  for (int element : vec) {
      std::cout << element << " ";
  }
  ```

#### Vector Capacity

* **Capacity**: Returns the number of elements that can be held in currently allocated storage.

  ```cpp
  int capacity = vec.capacity();
  ```

* **Resizing**: Changes the number of elements stored in the vector.

  ```cpp
  vec.resize(10); // Resize to 10 elements
  ```

* **Reserve**: Requests that the vector capacity be at least enough to contain a specified number of elements.

  ```cpp
  vec.reserve(20); // Reserve capacity for at least 20 elements
  ```

#### Conclusion

Vectors in C++ provide dynamic array-like behavior with additional functionalities and are widely used due to their flexibility and efficiency.
