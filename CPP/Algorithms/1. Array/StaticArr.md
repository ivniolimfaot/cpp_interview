# Arrays

### 1. Algorithms & Data Structures (C++): Advantages and Disadvantages of Arrays

Arrays are fundamental data structures in computer science and are widely used for storing collections of elements of the same data type in memory. Here are some advantages and disadvantages of using arrays in C++:

#### Advantages

1. **Fast Access:** Arrays provide constant-time access to elements, meaning accessing any element requires only a single operation, typically using the index of the element.

2. **Memory Efficiency:** Arrays allocate memory in a contiguous block, which makes them memory-efficient. This contiguous allocation also makes them cache-friendly, as adjacent elements are stored close to each other in memory.

3. **Simple Implementation:** Arrays are straightforward to implement and use, making them suitable for a wide range of applications.

4. **Support for Random Access:** Arrays allow for random access, meaning you can access any element directly using its index.

#### Disadvantages

1. **Fixed Size:** Arrays have a fixed size, meaning you need to know the number of elements in advance. This limitation makes it challenging to dynamically resize arrays, especially when the number of elements changes frequently.

2. **No Built-in Resize:** In C++, native arrays do not provide built-in resize operations. If you need to resize an array dynamically, you have to allocate a new array and copy the elements from the old array to the new one, which can be inefficient.

3. **Contiguous Memory Requirement:** Arrays require contiguous memory allocation, which may not always be available, especially for large arrays. This limitation can lead to memory fragmentation issues.

4. **Inefficient Insertions and Deletions:** Insertions and deletions in arrays, especially in the middle or beginning, can be inefficient. Insertions and deletions may require shifting elements to accommodate the change, which can result in a time complexity of O(n), where n is the number of elements.

5. **Wasted Space:** If the array size is larger than the number of elements it holds, there may be wasted space, leading to inefficient memory usage.

In summary, arrays offer fast and efficient element access, making them suitable for scenarios where the size of the collection is known in advance and where random access is important. However, their fixed size and inefficient resizing operations make them less suitable for dynamic collections where elements are frequently added or removed.

### 1. Algorithms & Data Structures (C++): Array

Sure! Arrays are fundamental data structures in programming languages, including C++. An array is a collection of elements stored in contiguous memory locations, where each element can be accessed directly by its index or position.

In C++, arrays can be declared using square brackets `[]`. Here's how you declare an array of integers with a fixed size:

```cpp
int myArray[5]; // Declares an array of integers with size 5
```

You can also initialize the array at the time of declaration:

```cpp
int myArray[5] = {1, 2, 3, 4, 5}; // Initializes the array with values 1, 2, 3, 4, 5
```

Once declared, you can access individual elements of the array using square brackets and the index:

```cpp
int x = myArray[0]; // Accesses the first element of the array
int y = myArray[2]; // Accesses the third element of the array
```

It's important to remember that array indices in C++ start from 0, so the first element of an array has index 0, the second has index 1, and so on.

Arrays in C++ have a fixed size, meaning once you declare an array, its size cannot be changed. However, you can use dynamic memory allocation to create arrays of varying sizes at runtime using pointers or container classes like `std::vector`.

Here's a simple example demonstrating the use of arrays in C++:

```cpp
#include <iostream>

int main() {
    int myArray[5] = {1, 2, 3, 4, 5};

    // Print array elements
    std::cout << "Array elements: ";
    for (int i = 0; i < 5; ++i) {
        std::cout << myArray[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

This code declares an array of integers, initializes it with values, and then prints each element of the array.

#### Array Operations

Arrays support various operations like insertion, deletion, searching, and sorting. However, since arrays in C++ have a fixed size determined at compile time, adding or removing elements from an array can be cumbersome.

#### Iterating Through an Array

You can use loops like `for` or `while` to iterate through the elements of an array.

Example using a `for` loop:

```cpp
for(int i = 0; i < 5; ++i) {
    cout << numbers[i] << " "; // Prints each element of the array
}
```

#### Characteristics of Arrays

* **Fast Access:** Accessing an element by index in an array is fast because the location of each element is known and can be directly accessed using its index.
  
* **Fixed Size:** In C++, arrays have a fixed size determined at compile time, which cannot be changed during runtime. This limitation can be overcome by using dynamic arrays (e.g., `std::vector`).

* **Contiguous Memory:** Array elements are stored in contiguous memory locations, which enables efficient memory access and cache utilization.

* **Homogeneous Elements:** Arrays can only contain elements of the same data type.

Arrays are powerful and efficient data structures for storing and manipulating collections of elements in C++. However, their fixed size and lack of built-in dynamic resizing may limit their flexibility in certain scenarios.

### 1. Algorithms & Data Structures (C++): Array ADT

An Array Abstract Data Type (ADT) is a fundamental concept in computer science and programming, providing a way to store and manipulate a collection of elements in contiguous memory locations. Here's a basic outline of how you might implement an Array ADT in C++:

```cpp
#include <iostream>

template <typename T>
class Array {
private:
    T* data; // Pointer to the dynamically allocated array
    int size; // Number of elements in the array
    int capacity; // Capacity of the array

public:
    // Constructor
    Array(int capacity) {
        this->capacity = capacity;
        size = 0;
        data = new T[capacity];
    }

    // Destructor
    ~Array() {
        delete[] data;
    }

    // Function to insert an element at the end of the array
    void insert(T element) {
        if (size < capacity) {
            data[size++] = element;
        } else {
            // Resize the array if it's full
            resize(capacity * 2);
            data[size++] = element;
        }
    }

    // Function to resize the array
    void resize(int newCapacity) {
        T* newData = new T[newCapacity];
        for (int i = 0; i < size; ++i) {
            newData[i] = data[i];
        }
        delete[] data;
        data = newData;
        capacity = newCapacity;
    }

    // Function to access an element at a specific index
    T& at(int index) {
        if (index >= 0 && index < size) {
            return data[index];
        } else {
            throw std::out_of_range("Index out of bounds");
        }
    }

    // Function to get the size of the array
    int getSize() const {
        return size;
    }

    // Function to get the capacity of the array
    int getCapacity() const {
        return capacity;
    }
};
```

This is a simple implementation of an array ADT in C++. It provides basic functionality like insertion, resizing, accessing elements by index, and querying the size and capacity of the array. You can extend this implementation by adding more functionalities like deletion, searching, sorting, etc., depending on your requirements.

### 1. Algorithms & Data Structures (C++): Array Data Structure

#### Array Size

```cpp
int size = sizeof(numbers) / sizeof(numbers[0]);
// This calculates the size of the array.
// sizeof(numbers) returns the total size of the array in bytes,
// and sizeof(numbers[0]) returns the size of one element in bytes.
```

#### Iterating Through an Array

```cpp
for (int i = 0; i < size; ++i) {
    // Access and process each element
    cout << numbers[i] << " ";
}
```

#### Array in Function

```cpp
// Arrays are passed to functions by reference (address), not by value.
void printArray(int arr[], int size) {
    for (int i = 0; i < size; ++i) {
        cout << arr[i] << " ";
    }
}
```

#### Dynamic Arrays

```cpp
// C++ also supports dynamic arrays using pointers.
int *dynamicArray = new int[10]; // Creates an array of size 10

// Remember to delete the dynamic array to avoid memory leaks.
delete[] dynamicArray;
```

#### Standard Library Array

```cpp
#include <array>
// Syntax:
std::array<dataType, size> arrayName;

// Example:
std::array<int, 5> arr = {1, 2, 3, 4, 5};
```

Arrays are simple but powerful data structures. However, they have fixed size, and resizing them can be inefficient. In situations where dynamic resizing is required, other data structures like vectors (from the Standard Template Library) are preferred.

### 1. Algorithms & Data Structures (C++): Array Representation by Compiler

In C++, arrays are represented in memory as contiguous blocks of memory. When you declare an array, the compiler allocates memory for all its elements in a single block. The elements of the array are stored one after the other in memory, and you can access them using their indices.

### 1. Algorithms & Data Structures (C++): Array STL

In C++, the Standard Template Library (STL) provides a rich set of tools for working with arrays and other data structures. The array container in STL provides a convenient way to work with fixed-size arrays. Here's a brief overview of using the array container in C++:

#### Including the Necessary Header

You need to include the `<array>` header to use the array container.

```cpp
#include <array>
```

#### Declaring an Array

To declare an array, you specify the data type and the size of the array within angle brackets.

```cpp
std::array<int, 5> myArray; // declares an array of 5 integers
```

#### Initializing an Array

You can initialize the array at the time of declaration.

```cpp
std::array<int, 5> myArray = {1, 2, 3, 4, 5}; // initializes array with values
```

#### Accessing Elements

You can access elements of the array using the `[]` operator or using the `at()` member function, which performs bounds checking.

```cpp
int x = myArray[0]; // Accessing first element
int y = myArray.at(1); // Accessing second element
```

#### Iterating Over Elements

You can iterate over the elements of the array using iterators or range-based for loops.

```cpp
for (int i = 0; i < myArray.size(); ++i) {
    // Accessing elements using index
    std::cout << myArray[i] << " ";
}

// Using range-based for loop
for (const auto& element : myArray) {
    std::cout << element << " ";
}
```

#### Additional Features

STL array provides additional features like `size()`, `empty()`, `fill()`, and `swap()`.

* `size()`: Returns the size of the array.
* `empty()`: Checks if the array is empty.
* `fill()`: Fills the array with a specified value.
* `swap()`: Swaps the contents of two arrays.

#### Example

```cpp
#include <iostream>
#include <array>

int main() {
    std::array<int, 5> myArray = {1, 2, 3, 4, 5};

    // Print array elements
    for (const auto& element : myArray) {
        std::cout << element << " ";
    }
    std::cout << std::endl;

    // Accessing and modifying array elements
    myArray[0] = 10;
    myArray.at(1) = 20;

    // Fill array with a value
    myArray.fill(100);

    // Print array elements after modification
    for (const auto& element : myArray) {
        std::cout << element << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

This is a basic overview of using the array container in C++ STL. It provides a convenient and efficient way to work with fixed-size arrays.

### 1. Algorithms & Data Structures (C++): Array: Deleting the Last Element

Deleting the last element of an array in C++ involves reducing the size of the array by one. Since arrays in C++ are of fixed size, you typically need to create a new array with a size one less than the original array, copy all elements except the last one from the original array to the new array, and then deallocate the memory of the original array. Here's how you can achieve this:

```cpp
#include <iostream>

void deleteLastElement(int* &arr, int& size) {
    if (size <= 0) {
        std::cout << "Array is empty!" << std::endl;
        return;
    }

    // Create a new array with size one less than the original array
    int newSize = size - 1;
    int* newArr = new int[newSize];

    // Copy elements except the last one
    for (int i = 0; i < newSize; ++i) {
        newArr[i] = arr[i];
    }

    // Deallocate memory of the original array
    delete[] arr;

    // Update the pointer and size to point to the new array
    arr = newArr;
    size = newSize;
}

int main() {
    int size = 5;
    int* arr = new int[size] {1, 2, 3, 4, 5};

    std::cout << "Original Array: ";
    for (int i = 0; i < size; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    deleteLastElement(arr, size);

    std::cout << "Array after deleting the last element: ";
    for (int i = 0; i < size; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    // Don't forget to deallocate memory of the array
    delete[] arr;

    return 0;
}
```

In this code:

* The `deleteLastElement` function takes a reference to a pointer to an array (`int* &arr`) and a reference to the size of the array (`int& size`).
* It first checks if the array is empty.
* Then, it creates a new array with one less element than the original array, copies all elements except the last one from the original array to the new array, deallocates the memory of the original array, and updates the pointer and size to point to the new array.
* Finally, in the `main` function, it demonstrates how to use the `deleteLastElement` function.

### 1. Algorithms & Data Structures (C++): Array: Print Array in Reverse Order

To print an array in reverse order in C++, you can iterate through the array starting from the last element and print each element until you reach the first element. Here's a simple example:

```cpp
#include <iostream>

void printArrayReverse(int arr[], int size) {
    for (int i = size - 1; i >= 0; --i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int size = sizeof(arr) / sizeof(arr[0]);

    std::cout << "Array in reverse order: ";
    printArrayReverse(arr, size);

    return 0;
}
```

This code defines a function `printArrayReverse` that takes an array and its size as input arguments. Inside this function, a loop iterates from the last index to the first index of the array, printing each element in reverse order. Finally, in the `main` function, an array is initialized, and `printArrayReverse` is called to print the array in reverse order.

### 1. Algorithms & Data Structures (C++): Array: Segmentation Fault in Array

A segmentation fault in an array usually occurs when you're trying to access memory that you don't have permission to access, often because you're accessing an element beyond the bounds of the array. Here's a checklist to help you debug and avoid segmentation faults in arrays:

1. **Array Index Out of Bounds**: Ensure that you're not accessing elements outside the bounds of the array. In C++, arrays are zero-indexed, meaning the first element is at index 0 and the last element is at index `size - 1`.

   ```cpp
   int arr[5];  // Array of size 5
   arr[5] = 10; // Accessing arr[5] is out of bounds
   ```

2. **Null Pointers**: If you're dealing with pointers to arrays, make sure they are properly initialized and not pointing to `nullptr`.

   ```cpp
   int* arrPtr = nullptr;
   arrPtr[0] = 10; // Accessing a null pointer
   ```

3. **Uninitialized Pointers**: Ensure that pointers are initialized to point to valid memory locations.

   ```cpp
   int* arrPtr;
   *arrPtr = 10; // Using an uninitialized pointer
   ```

4. **Dynamic Memory Management**: If you're dynamically allocating memory for arrays using `new` or `malloc`, ensure that you allocate and deallocate memory properly.

   ```cpp
   int* arrPtr = new int[5];
   delete[] arrPtr; // Don't forget to free memory after use
   ```

5. **Check Input Data**: If your program relies on user input or external data, validate that the input doesn't cause out-of-bounds accesses.

6. **Debugging Tools**: Utilize debugging tools like `gdb` (GNU Debugger) to identify the exact line of code causing the segmentation fault.

Here's a simple example illustrating an array causing a segmentation fault due to an out-of-bounds access:

```cpp
#include <iostream>

int main() {
    int arr[5] = {1, 2, 3, 4, 5};

    // Accessing elements within bounds
    for (int i = 0; i < 5; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    // Accessing an element out of bounds
    std::cout << arr[5] << std::endl; // This line will cause a segmentation fault

    return 0;
}
```

To fix this, make sure to access elements within the bounds of the array. In this case, accessing `arr[5]` is causing the segmentation fault because it's trying to access the 6th element of a 5-element array.

### 1. Algorithms & Data Structures (C++): Arrays

#### Array Algorithms

C++ Standard Library provides algorithms for common array operations such as sorting, searching, etc. They are located in the `<algorithm>` header.

```cpp
#include <algorithm>
std::sort(myArray.begin(), myArray.end()); // sorts the array
```

Arrays are a cornerstone of programming and understanding how to work with them efficiently is crucial for any programmer.

### 1. Algorithms & Data Structures (C++): Arrays & Functions - Pass by Reference

Certainly! In C++, when working with arrays and functions, passing arrays by reference is a common and efficient practice. Here's a detailed explanation, along with code examples to help you understand the concept.

In C++, passing by reference means passing the reference (or address) of a variable rather than a copy of the variable. This is useful for efficiency, especially with large data structures like arrays, as it avoids the overhead of copying data.

To pass an array by reference, you need to pass the pointer to the array along with its size (if the function needs to know the size of the array).

#### Example: Function to Print Array Elements

```cpp
#include <iostream>
using namespace std;

// Function prototype
void printArray(int (&arr)[5]);

int main() {
    int myArray[5] = {1, 2, 3, 4, 5};
    printArray(myArray);
    return 0;
}

// Function definition
void printArray(int (&arr)[5]) {
    for (int i = 0; i < 5; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}
```

In this example:

* The `printArray` function takes an array of 5 integers by reference.
* The `(&arr)[5]` syntax specifies that `arr` is a reference to an array of 5 integers.

#### Benefits of Passing by Reference

1. **Efficiency**: Passing large arrays by reference avoids copying the entire array, saving time and memory.
2. **Modification**: Allows the function to modify the original array, if needed.

#### Generalizing Array Functions with Templates

To handle arrays of different sizes, you can use templates. Here's how:

```cpp
#include <iostream>
using namespace std;

template <size_t N>
void printArray(int (&arr)[N]) {
    for (size_t i = 0; i < N; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

int main() {
    int myArray1[5] = {1, 2, 3, 4, 5};
    int myArray2[3] = {10, 20, 30};
    
    printArray(myArray1);
    printArray(myArray2);
    
    return 0;
}
```

In this example:

* The `printArray` function template can handle arrays of any size.
* The `template <size_t N>` declares a template with a non-type parameter `N` representing the size of the array.

### 1. Algorithms & Data Structures (C++): Arrays & Vectors

#### Vectors

Vectors are part of the Standard Template Library (STL) in C++. They are dynamic arrays that can resize themselves automatically when needed. Vectors provide similar functionality to arrays but with additional operations such as dynamic resizing, insertion, and deletion at the beginning, middle, or end of the vector.

```cpp
#include <vector>

// Declaration and initialization of a vector
std::vector<int> vec = {1, 2, 3, 4, 5};

// Accessing elements of the vector
int firstElement = vec[0]; // Accessing the first element (index 0)
int thirdElement = vec[2]; // Accessing the third element (index 2)

// Modifying elements of the vector
vec[1] = 10; // Modifying the second element (index 1)

// Size of the vector
int size = vec.size(); // Gives the size of the vector
```

Vectors offer more flexibility compared to arrays due to their dynamic resizing capability and the range of functions provided by the STL, such as `push_back()`, `pop_back()`, `insert()`, `erase()`, etc.

Both arrays and vectors have their advantages and use cases. Arrays are more efficient in terms of memory and slightly faster for access since they are fixed in size, while vectors offer more flexibility and ease of use. The choice between them depends on the specific requirements of your program.

### 1. Algorithms & Data Structures (C++): Arrays and Functions

#### Using Arrays with Functions

```cpp
#include <iostream>

// Function to print elements of an integer array
void printArray(int arr[], int size) {
    for (int i = 0; i < size; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
}

int main() {
    int myArray[5] = {1, 2, 3, 4, 5};
    int size = sizeof(myArray) / sizeof(myArray[0]); // Calculate the size of the array

    // Call the function to print the array
    printArray(myArray, size);

    return 0;
}
```

This program will output:

```paintext
1 2 3 4 5
```

This is just a basic introduction to using arrays and functions in C++. There are many more advanced concepts and techniques you can explore! Let me know if you have any questions or if you'd like to delve deeper into any specific topic.

### 1. Algorithms & Data Structures (C++): Arrays vs Vectors

In C++, both arrays and vectors are commonly used data structures for storing sequences of elements. Each has its own characteristics, advantages, and disadvantages. Here’s a comparative overview:

#### Arrays

##### Characteristics

1. **Fixed Size**: The size of an array is determined at compile time and cannot be changed.
2. **Contiguous Memory**: Arrays store elements in contiguous memory locations, which makes them efficient in terms of accessing elements via indexing.
3. **Low-level Structure**: Arrays are a low-level data structure, offering direct access to elements and memory.
4. **Syntax**: Declaring an array is straightforward. For example:

   ```cpp
   int arr[10]; // declares an array of 10 integers
   ```

#### Advantages

1. **Performance**: Due to contiguous memory allocation, arrays provide fast element access using indices (O(1) time complexity).
2. **Memory Overhead**: Arrays do not have extra memory overhead beyond the storage for the elements themselves.
3. **Predictable Memory Use**: Since the size is fixed, memory usage is predictable.

#### Disadvantages

1. **Fixed Size**: Inflexibility in size can be a limitation if the number of elements is not known in advance.
2. **Manual Memory Management**: When using dynamic arrays (allocated with `new`), the programmer must handle memory allocation and deallocation manually.
3. **Lack of Built-in Methods**: Arrays lack built-in functions for common operations (e.g., resizing, inserting).

#### Vectors

##### Characteristics

1. **Dynamic Size**: Vectors can grow and shrink dynamically at runtime.
2. **Contiguous Memory**: Like arrays, vectors also store elements in contiguous memory locations.
3. **STL Container**: Vectors are part of the C++ Standard Template Library (STL), which provides many useful functions.
4. **Syntax**: Declaring a vector is done through the STL:

   ```cpp
   #include <vector>
   std::vector<int> vec; // declares a vector of integers
   ```

#### Advantages

1. **Dynamic Resizing**: Vectors can automatically resize themselves as elements are added or removed.
2. **Ease of Use**: Vectors come with a range of built-in functions such as `push_back`, `pop_back`, `size`, `clear`, and more.
3. **Memory Management**: Memory management is handled automatically by the vector class.
4. **Safety**: Vectors provide bounds checking with the `at` method, which throws an exception if the index is out of range.

#### Disadvantages

1. **Memory Overhead**: Vectors may allocate extra memory to manage future growth, leading to potential memory overhead.
2. **Reallocation Cost**: When a vector grows beyond its current capacity, it needs to allocate new memory and copy existing elements, which can be costly.
3. **Performance Overhead**: The automatic resizing and other additional functionalities introduce slight performance overhead compared to raw arrays.

#### When to Use Each

* **Arrays**:
  * Use arrays when the size of the data is known at compile time and does not change.
  * When you need very fast and predictable access to elements.
  * In performance-critical sections where memory overhead needs to be minimal.

* **Vectors**:
  * Use vectors when the size of the data can change at runtime.
  * When you need built-in methods for manipulating the data (inserting, removing, searching).
  * When you prefer automatic memory management to avoid manual handling of memory.

#### Example Comparison

```cpp
// Array example
#include <iostream>

int main() {
    int arr[5] = {1, 2, 3, 4, 5};
    for (int i = 0; i < 5; ++i) {
        std::cout << arr[i] << " ";
    }
    return 0;
}

// Vector example
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};
    vec.push_back(6); // Adding an element to the vector
    for (int i = 0; i < vec.size(); ++i) {
        std::cout << vec[i] << " ";
    }
    return 0;
}
```

In conclusion, the choice between arrays and vectors in C++ depends on the specific requirements of your application, including the need for dynamic sizing, performance considerations, and ease of use.

### 1. Algorithms & Data Structures (C++): Arrays in C++

#### Pointers and Arrays

In C++, arrays are closely related to pointers. The name of the array itself represents a pointer to the first element of the array. You can also perform pointer arithmetic to navigate through the array.

```cpp
int arr[] = {10, 20, 30, 40, 50};
int* ptr = arr; // ptr points to the first element of the array
cout << *ptr; // Prints 10
ptr++; // Moves to the next element
cout << *ptr; // Prints 20
```

Understanding arrays in C++ is crucial as they are the building blocks for many other data structures and algorithms.

### 1. Algorithms & Data Structures (C++): Arrays in Memory

In C++, arrays are collections of elements stored in contiguous memory locations. Understanding how arrays are laid out in memory is crucial for efficient manipulation and access of array elements. Here's a breakdown of how arrays work in memory:

1. **Contiguous Memory Allocation**: When you declare an array in C++, memory is allocated for all its elements in a contiguous block. This means that the memory addresses of successive elements are contiguous, allowing for efficient traversal and random access.

2. **Element Access**: Each element in the array can be accessed using its index. The index specifies the position of the element within the array. For example, `array[0]` refers to the first element, `array[1]` refers to the second element, and so on.

3. **Memory Layout**: Arrays are laid out in memory such that each element occupies a fixed amount of memory space, and the elements are stored one after the other without any gaps. The size of each element depends on its data type.

4. **Pointer Arithmetic**: Since arrays are laid out contiguously in memory, you can use pointer arithmetic to navigate through array elements. For example, if `arr` is an array, `arr + i` points to the memory location of the `i`-th element of the array.

5. **Memory Efficiency**: Arrays offer efficient memory usage since they store elements in a contiguous block. This allows for efficient cache utilization and enables faster access compared to other data structures like linked lists.

Here's a simple example demonstrating the concepts mentioned above:

```cpp
#include <iostream>

int main() {
    int arr[5] = {10, 20, 30, 40, 50};

    // Accessing elements using array indexing
    std::cout << "First element: " << arr[0] << std::endl;
    std::cout << "Third element: " << arr[2] << std::endl;

    // Pointer arithmetic to access elements
    int* ptr = arr; // ptr points to the first element of the array
    std::cout << "Second element using pointer: " << *(ptr + 1) << std::endl;

    return 0;
}
```

In this example, `arr` is an array of integers with five elements. We access array elements using both array indexing and pointer arithmetic, demonstrating their equivalence.

### 1. Algorithms & Data Structures (C++): Arrays Representations

In C++, arrays can be represented in several ways, each with its own advantages and use cases. Here are a few common representations:

1. **Static Arrays**: These are the simplest form of arrays where the size is fixed at compile time. They are declared using square brackets `[]` with the size specified at declaration.

    ```cpp
    int arr[5]; // Declares an array of integers with size 5
    ```

2. **Dynamic Arrays (Pointer-based)**: These arrays have a variable size and are allocated on the heap using pointers. They offer flexibility in size but require manual memory management.

    ```cpp
    int *arr = new int[5]; // Allocates an array of integers with size 5 dynamically
    delete[] arr; // Frees the dynamically allocated memory
    ```

3. **Vectors (Standard Library)**: Vectors are part of the C++ Standard Library and provide dynamic array functionality with additional features such as automatic resizing and bounds checking.

    ```cpp
    #include <vector>
    std::vector<int> vec(5); // Declares a vector of integers with size 5
    ```

4. **Arrays of Arrays (Multi-dimensional Arrays)**: Arrays can be nested within one another to create multi-dimensional arrays.

    ```cpp
    int matrix[3][3]; // Declares a 3x3 matrix
    ```

5. **Array Wrappers (std::array)**: Introduced in C++11, `std::array` provides a safer and more feature-rich alternative to traditional C-style arrays. They offer bounds checking and can be used with standard algorithms.

    ```cpp
    #include <array>
    std::array<int, 5> arr; // Declares an array of integers with size 5 using std::array
    ```

Each representation has its own strengths and weaknesses, so choosing the right one depends on factors such as performance requirements, memory management considerations, and ease of use.

### 1. Algorithms & Data Structures (C++): Arrays Static

#### Pros and Cons of Static Arrays

**Pros:**

1. Simple and efficient for small, fixed-size collections.
2. No overhead of dynamic memory allocation and deallocation.
3. Direct memory access.

**Cons:**

1. Fixed size can be a limitation if the size needs to change at runtime.
2. Memory is allocated on the stack, which can lead to stack overflow for large arrays.
3. Need to know the size at compile time, which may not always be possible or convenient.

### 1. Algorithms & Data Structures (C++): Arrays Static vs Dynamic Arrays

In C++, arrays can be static or dynamic, each with its own characteristics and use cases.

1. **Static Arrays:**
   * Static arrays have a fixed size that is determined at compile time.
   * They are declared using a fixed size within square brackets, like `int arr[100];`.
   * Once declared, the size cannot be changed during runtime.
   * Memory for static arrays is allocated on the stack, making them fast to access but limited in size.
   * Static arrays are suitable when the size of the array is known beforehand and won't change throughout the program's execution.

Example of a static array:

```cpp
#include <iostream>

int main() {
    int arr[5] = {1, 2, 3, 4, 5};
    
    for(int i = 0; i < 5; ++i) {
        std::cout << arr[i] << " ";
    }
    
    return 0;
}
```

1. **Dynamic Arrays (using pointers):**
   * Dynamic arrays are allocated memory at runtime using pointers.
   * They allow for dynamic resizing during program execution.
   * Dynamic arrays are created using the `new` keyword in C++, like `int* arr = new int[size];`.
   * Memory for dynamic arrays is allocated on the heap, making them flexible but slower in access compared to static arrays.
   * It's important to deallocate the memory using the `delete[]` operator to avoid memory leaks.

Example of a dynamic array:

```cpp
#include <iostream>

int main() {
    int size;
    std::cout << "Enter the size of the array: ";
    std::cin >> size;
    
    int* arr = new int[size];
    
    for(int i = 0; i < size; ++i) {
        arr[i] = i + 1;
    }
    
    std::cout << "Array elements: ";
    for(int i = 0; i < size; ++i) {
        std::cout << arr[i] << " ";
    }
    
    delete[] arr; // Deallocate memory
    
    return 0;
}
```

When choosing between static and dynamic arrays, consider the requirements of your program. If the size is fixed and known at compile time, static arrays are preferable for their simplicity and efficiency. However, if the size is not known until runtime or needs to change dynamically, dynamic arrays offer the flexibility required.

### 1. Algorithms & Data Structures (C++): Arrays vs Linked List

When comparing arrays and linked lists in the context of algorithms and data structures, each has its own strengths and weaknesses. Let's delve into the comparison:

1. **Memory Allocation**:
    * Arrays: Contiguous memory allocation. Once the size is defined, it's fixed.
    * Linked Lists: Dynamic memory allocation. Nodes are scattered in memory and connected via pointers.

2. **Insertion and Deletion**:
    * Arrays: Insertions and deletions can be inefficient, especially in the middle, as it may require shifting elements.
    * Linked Lists: Efficient for insertions and deletions, especially at the beginning or end, as it involves adjusting pointers.

3. **Access Time**:
    * Arrays: O(1) constant time access if the index is known.
    * Linked Lists: O(n) time for accessing an element, as you need to traverse the list from the head or tail.

4. **Memory Overhead**:
    * Arrays: Typically more memory efficient due to minimal overhead.
    * Linked Lists: Additional memory overhead due to storing pointers for each element.

5. **Size Flexibility**:
    * Arrays: Fixed size unless resized, which may be inefficient.
    * Linked Lists: Dynamic size; can grow or shrink easily without much overhead.

6. **Cache Efficiency**:
    * Arrays: Better cache locality, as elements are stored contiguously.
    * Linked Lists: Poor cache locality, as nodes are scattered in memory.

7. **Implementation Complexity**:
    * Arrays: Simpler implementation and easier to understand.
    * Linked Lists: More complex due to managing pointers and dynamic memory allocation.

8. **Usage**:
    * Arrays: Suitable for random access and when the size is known and won't change frequently.
    * Linked Lists: Ideal for scenarios where frequent insertions and deletions are expected, or when the size is not known beforehand.

Choosing between arrays and linked lists depends on the specific requirements of the problem you're solving. If fast random access is crucial and memory is not a concern, arrays might be preferable. Conversely, if dynamic size and efficient insertions/deletions are more important, linked lists might be the better choice. In some cases, hybrid data structures like dynamic arrays (e.g., `std::vector` in C++) offer a compromise between the two.

### 1. Algorithms & Data Structures (C++): Big O: Vectors

When analyzing algorithms and data structures in C++, understanding their performance characteristics, often expressed in terms of Big O notation, is crucial. Let's delve into the Big O analysis for vectors in C++.

Vectors in C++ are part of the Standard Template Library (STL) and provide dynamic array functionality. Here's a brief overview of some common operations on vectors and their corresponding Big O complexities:

1. **Accessing Elements by Index**:
   * Accessing an element by index: O(1)
   * This is because vectors provide constant-time random access, meaning accessing any element by its index takes the same amount of time regardless of the vector's size.

2. **Insertion and Deletion**:
   * Insertion or deletion at the end of the vector (push_back, pop_back): O(1) amortized
   * This is because vectors typically allocate more memory than needed, and when the vector is full and a new element is added, it reallocates memory, which has a linear cost. However, this reallocation happens infrequently, leading to an amortized constant time complexity.

   * Insertion or deletion at the beginning or in the middle of the vector: O(n)
   * When inserting or deleting elements at positions other than the end, elements need to be shifted to accommodate the change, resulting in a linear time complexity.

3. **Searching**:
   * Linear search (find): O(n)
   * This is because in the worst-case scenario, you may need to traverse the entire vector to find the element you are looking for.

   * Binary search (for sorted vectors): O(log n)
   * If the vector is sorted, binary search can be applied, which has a logarithmic time complexity.

4. **Sorting**:
   * Sorting the entire vector (sort): O(n log n)
   * The standard sort algorithm (usually implemented as an introsort, which is a hybrid sorting algorithm) has an average-case time complexity of O(n log n).

5. **Size and Capacity**:
   * Getting the size of the vector (size): O(1)
   * Getting the current size of the vector is a constant-time operation.

   * Getting the capacity of the vector (capacity): O(1)
   * Similarly, getting the current capacity of the vector is also a constant-time operation.

Overall, vectors in C++ are very efficient for random access and appending elements at the end. However, they might not be the best choice for frequent insertion or deletion operations at the beginning or middle of the vector, as those operations have a linear time complexity. For such cases, other data structures like linked lists or dequeues might be more suitable.

### 1. Algorithms & Data Structures (C++): Declarations of Array

#### Multidimensional Arrays

Arrays can have multiple dimensions:

```cpp
// Syntax: dataType arrayName[dim1Size][dim2Size]...[dimNSize];
int matrix[3][3]; // 3x3 matrix
char image[2][3][3]; // 2x3x3 image represented by characters
```

#### String Arrays

C-style strings are arrays of characters terminated by a null character ('\0').

```cpp
char greeting[] = "Hello, world!"; // Automatically sized array to fit the string and null terminator
```

#### Array Sizes

You can get the size of a static array using the `sizeof` operator:

```cpp
int size = sizeof(integers) / sizeof(integers[0]); // Size of the array
```

For dynamic arrays, you need to keep track of the size separately.

These are the basic ways to declare arrays in C++, each serving different needs based on the program's requirements.

### 1. Algorithms & Data Structures (C++): Comparison of Array with Linked List

Certainly! Comparing arrays and linked lists in terms of algorithms and data structures can help in understanding their strengths and weaknesses. Let's break down the comparison:

1. **Memory Representation**:
   * **Array**: Contiguous block of memory where elements are stored consecutively. Accessing elements is efficient using indexing.
   * **Linked List**: Elements are stored in nodes, where each node contains the data and a pointer/reference to the next node. Memory allocation for nodes may not be contiguous, allowing dynamic allocation and flexibility.

2. **Insertion and Deletion**:
   * **Array**: Insertion and deletion operations may require shifting elements to accommodate changes in size. Insertion or deletion at the beginning or middle of the array can be inefficient due to the need for shifting.
   * **Linked List**: Insertion and deletion can be efficient, especially for singly linked lists, as it only requires updating pointers. Deletion can be done in constant time if the node to be deleted is given. However, locating the node may require linear time traversal in the worst case.

3. **Access Time**:
   * **Array**: Accessing elements by index is constant time (O(1)) since arrays provide direct access to memory locations.
   * **Linked List**: Accessing elements by index requires traversing the list from the head (for singly linked list) or tail (for doubly linked list), which is O(n) time complexity in the worst case.

4. **Memory Overhead**:
   * **Array**: Generally has lower memory overhead as it only needs to store the elements and, in some cases, the length of the array.
   * **Linked List**: Requires additional memory for storing pointers/references to the next node, resulting in higher memory overhead per element.

5. **Dynamic Size**:
   * **Array**: In many programming languages, the size of an array is fixed at compile time. Resizing may involve creating a new array and copying elements, which can be inefficient.
   * **Linked List**: Can dynamically grow or shrink without the need for reallocation, making it more flexible for dynamic data structures.

6. **Cache Locality**:
   * **Array**: Provides better cache locality since elements are stored contiguously, leading to better performance in situations where accessing nearby elements is common.
   * **Linked List**: Poor cache locality due to scattered memory locations of nodes, which can lead to more cache misses, especially in large lists.

7. **Traversal**:
   * **Array**: Traversal is straightforward using loops since elements are contiguous in memory.
   * **Linked List**: Traversal requires following pointers from one node to another, which introduces additional overhead compared to array traversal.

In summary, arrays are preferable when random access and efficient traversal are required, especially for small to medium-sized collections with a known fixed size. On the other hand, linked lists are better suited for scenarios where frequent insertion/deletion operations are expected or when the size of the collection is dynamic and unpredictable.

### 1. Algorithms & Data Structures (C++): Data Structure : Vectors

Vectors in C++ are a versatile data structure provided by the Standard Template Library (STL). They are similar to arrays but with dynamic sizing and additional functionalities. Here's an overview:

#### 1. **Dynamic Sizing:**

* Vectors can dynamically resize themselves to accommodate new elements. This makes them suitable for situations where the number of elements is not known in advance.

#### 2. **Contiguous Memory:**

* Like arrays, vectors store their elements in contiguous memory, allowing for efficient random access.

#### 3. **Access and Modification:**

* Elements can be accessed using the `[]` operator or the `at()` function.
* Vectors support both reading and writing operations.

#### 4. **Iterators:**

* Vectors support iterators, which allow traversal through the elements of the vector. This enables operations like iteration, searching, and sorting.

#### 5. **Dynamic Allocation:**

* Vectors manage memory dynamically, automatically handling memory allocation and deallocation. This reduces the risk of memory leaks and buffer overflows.

#### 6. **Insertion and Deletion:**

* Elements can be inserted at the end, in the middle, or at the beginning of a vector using various functions like `push_back()`, `insert()`, `emplace_back()`, etc.
* Similarly, elements can be deleted using functions like `pop_back()`, `erase()`, etc.

#### 7. **Size and Capacity:**

* The `size()` function returns the number of elements currently stored in the vector.
* The `capacity()` function returns the number of elements that can be stored in the vector without reallocation.

#### Example

```cpp
#include <iostream>
#include <vector>

int main() {
    // Declaration
    std::vector<int> myVector;

    // Adding elements
    myVector.push_back(10);
    myVector.push_back(20);
    myVector.push_back(30);

    // Accessing elements
    std::cout << "First Element: " << myVector[0] << std::endl;
    std::cout << "Second Element: " << myVector.at(1) << std::endl;

    // Iterating through the vector
    for (int i = 0; i < myVector.size(); ++i) {
        std::cout << myVector[i] << " ";
    }
    std::cout << std::endl;

    // Deleting elements
    myVector.pop_back();

    // Size and Capacity
    std::cout << "Size: " << myVector.size() << std::endl;
    std::cout << "Capacity: " << myVector.capacity() << std::endl;

    return 0;
}
```

Vectors are incredibly useful due to their flexibility and efficiency. However, they may not be the best choice for scenarios requiring frequent insertions or deletions in the middle of large collections, as these operations can be costly due to the need for shifting elements. In such cases, other data structures like lists or deques might be more suitable.

### 1. Algorithms & Data Structures (C++): Data structures: Arrays: operations

Arrays are fundamental data structures in programming languages like C++. They store a fixed-size sequential collection of elements of the same type. Here are some common operations performed on arrays:

1. **Accessing Elements**: Arrays allow accessing elements by their index. In C++, array indices start from 0.

    ```cpp
    int arr[5] = {1, 2, 3, 4, 5};
    int firstElement = arr[0]; // Accessing the first element
    int thirdElement = arr[2]; // Accessing the third element
    ```

2. **Insertion**: Inserting an element into an array involves shifting elements to make space for the new element.

    ```cpp
    int arr[5] = {1, 2, 3, 4, 5};
    // Inserting 6 at index 2
    for(int i = 4; i > 2; i--) {
        arr[i] = arr[i - 1];
    }
    arr[2] = 6;
    ```

3. **Deletion**: Deleting an element from an array involves shifting elements to fill the gap left by the deleted element.

    ```cpp
    int arr[5] = {1, 2, 3, 4, 5};
    // Deleting element at index 2
    for(int i = 2; i < 4; i++) {
        arr[i] = arr[i + 1];
    }
    ```

4. **Traversal**: Accessing each element of the array one by one.

    ```cpp
    int arr[5] = {1, 2, 3, 4, 5};
    for(int i = 0; i < 5; i++) {
        // Do something with arr[i]
    }
    ```

5. **Searching**: Finding the index of a specific element in the array.

    ```cpp
    int arr[5] = {1, 2, 3, 4, 5};
    int key = 3; // Element to search for
    int index = -1; // Initialize with -1 indicating not found
    for(int i = 0; i < 5; i++) {
        if(arr[i] == key) {
            index = i;
            break;
        }
    }
    ```

6. **Updating**: Modifying the value of an element at a particular index.

    ```cpp
    int arr[5] = {1, 2, 3, 4, 5};
    // Updating element at index 2
    arr[2] = 10;
    ```

These are some of the basic operations you can perform on arrays in C++. Depending on your requirements, you might need more complex operations or optimizations, which could involve using different data structures.

### 1. Algorithms & Data Structures (C++): Deleting from Array

In C++, deleting an element from an array requires shifting elements to fill the gap created by the deletion. Here's a basic example of how you can delete an element from a dynamic array:

```cpp
#include <iostream>

// Function to delete an element from an array
void deleteElement(int arr[], int& size, int index) {
    if (index < 0 || index >= size) {
        std::cout << "Invalid index\n";
        return;
    }

    // Shift elements to the left to fill the gap
    for (int i = index; i < size - 1; ++i) {
        arr[i] = arr[i + 1];
    }

    // Decrement size
    size--;
}

int main() {
    const int maxSize = 100;
    int arr[maxSize] = {1, 2, 3, 4, 5};
    int size = 5; // Current size of the array

    // Index of the element to delete
    int indexToDelete = 2;

    // Delete element at indexToDelete
    deleteElement(arr, size, indexToDelete);

    // Print the array after deletion
    std::cout << "Array after deletion:\n";
    for (int i = 0; i < size; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this example, the `deleteElement` function takes the array, its size, and the index of the element to delete. It then shifts the elements after the index to the left, effectively overwriting the element at the specified index. Finally, it decrements the size of the array.

Keep in mind that deleting elements from an array in this way is not very efficient for large arrays because shifting elements has a time complexity of O(n), where n is the number of elements after the deleted element. If you need to perform frequent deletions, consider using other data structures like linked lists or vectors which provide better performance for such operations.

### 1. Algorithms & Data Structures (C++): Difference between Array of Pointers and Pointer to an Array

In C++, an array of pointers and a pointer to an array may seem similar but have different purposes and behaviors.

1. **Array of Pointers**:
   * An array of pointers is a collection of pointers where each element points to a memory location, typically to another variable or object.
   * This type of structure is useful when you need to manage a collection of dynamically allocated memory or when you want to point to different objects of varying sizes.
   * Example:

     ```cpp
     int* arr[5]; // Array of pointers to int
     ```

   * Here, `arr` is an array containing 5 elements, each of which is a pointer to an integer.

2. **Pointer to an Array**:
   * A pointer to an array points to the memory location of the first element of an array.
   * It's useful when you want to pass an entire array to a function or manipulate the array as a whole.
   * Example:

     ```cpp
     int (*ptr)[5]; // Pointer to an array of 5 ints
     ```

   * Here, `ptr` is a pointer that points to an array of 5 integers.

Here's a brief comparison:

* **Memory Allocation**:
  * Array of Pointers: Requires separate memory allocation for each pointer and the objects they point to.
  * Pointer to an Array: Points to a contiguous block of memory where the array is stored.

* **Access**:
  * Array of Pointers: Each pointer can point to different memory locations.
  * Pointer to an Array: Accesses a contiguous block of memory representing the entire array.

* **Usage**:
  * Array of Pointers: Used when dealing with an array of dynamically allocated objects or objects of varying sizes.
  * Pointer to an Array: Used when passing entire arrays to functions or when needing to manipulate arrays as a whole.

* **Example**:
  * Array of Pointers: An array of pointers might be used in a situation where you want to store pointers to strings.
  * Pointer to an Array: A pointer to an array might be used when you want to pass an array to a function without knowing its size at compile time.

In summary, the choice between an array of pointers and a pointer to an array depends on the specific requirements of your program and how you intend to manipulate or access the data.

### 1. Algorithms & Data Structures (C++): Disadvantage of standard array

One notable disadvantage of using standard arrays in C++ for algorithms and data structures is their fixed size. Once declared, the size of a standard array cannot be changed dynamically during runtime. This limitation can lead to several issues:

1. **Memory inefficiency**: If you allocate more space than needed, you waste memory. If you allocate less space, you may encounter buffer overflows or have to reallocate memory, which can be costly.

2. **Limited flexibility**: Since the size is fixed, you may need to make assumptions about the maximum size of the data you're dealing with. If these assumptions are incorrect, your program may fail unexpectedly or require extensive modifications to accommodate larger datasets.

3. **No built-in bounds checking**: Standard C++ arrays do not perform bounds checking, meaning you can easily access or modify elements outside the bounds of the array without any warnings from the compiler. This can lead to hard-to-debug runtime errors, such as segmentation faults or memory corruption.

4. **Difficulty in passing as function arguments**: When passing arrays to functions, you typically need to pass the size of the array separately, which can be error-prone and cumbersome, especially in large codebases.

To mitigate these issues, C++ offers alternatives like `std::vector`, which provides dynamic resizing, bounds checking, and a range of convenient member functions for manipulation. Other data structures like linked lists, trees, or hash tables can also offer more flexibility and functionality compared to standard arrays in many cases.

### 1. Algorithms & Data Structures (C++): Drawbacks of Arrays

Arrays in C++ offer simplicity and efficiency for storing and accessing elements in contiguous memory locations. However, they also come with several drawbacks:

1. **Fixed Size**: Arrays in C++ have a fixed size determined at compile time. Once defined, their size cannot be changed dynamically during runtime. This limitation can be problematic when the size of the data is not known in advance or needs to be adjusted based on runtime conditions.

2. **Memory Management**: Arrays require contiguous memory allocation. This can be a limitation when dealing with large datasets or when memory fragmentation becomes an issue. Additionally, dynamic memory allocation for arrays can lead to memory leaks or inefficient memory usage if not managed properly.

3. **No Built-in Bounds Checking**: C++ arrays do not perform bounds checking by default. Accessing elements outside the bounds of the array can lead to undefined behavior, such as memory corruption or segmentation faults. While this allows for faster access, it also increases the risk of runtime errors if not handled carefully.

4. **No Built-in Operations**: Arrays in C++ do not come with built-in operations for common tasks such as resizing, searching, or sorting. Developers must implement these functionalities themselves or use external libraries, which can be time-consuming and error-prone.

5. **Inflexible Data Types**: C++ arrays are homogeneous, meaning they can only store elements of the same data type. This limitation can be problematic when dealing with heterogeneous data or when different data types need to be stored within the same data structure.

6. **Passing by Value**: When passing an array to a function in C++, it is passed by value by default. This means that a copy of the entire array is made, which can be inefficient for large arrays. While passing by reference or using pointers can mitigate this issue, it adds complexity to the code.

7. **Lack of Flexibility**: Arrays lack flexibility compared to other data structures like linked lists or dynamic arrays. Operations such as insertion or deletion of elements in the middle of the array require shifting elements, resulting in inefficient time complexity, especially for large arrays.

Overall, while arrays offer simplicity and efficiency for basic data storage and retrieval, they come with inherent limitations that may make them unsuitable for certain use cases. Developers often need to carefully consider these drawbacks and choose alternative data structures when necessary to meet the requirements of their applications.

### 1. Algorithms & Data Structures (C++): Dynamic Array Class

Sure, let's create a simple dynamic array class in C++. This class will dynamically allocate memory to store elements and resize itself as needed.

```cpp
#include <iostream>

template <typename T>
class DynamicArray {
private:
    T* array; // Pointer to dynamically allocated array
    size_t capacity; // Current capacity of the array
    size_t size; // Current number of elements in the array

public:
    // Constructor
    DynamicArray() : array(nullptr), capacity(0), size(0) {}

    // Destructor
    ~DynamicArray() {
        delete[] array;
    }

    // Copy constructor
    DynamicArray(const DynamicArray& other) {
        capacity = other.capacity;
        size = other.size;
        array = new T[capacity];
        for (size_t i = 0; i < size; ++i) {
            array[i] = other.array[i];
        }
    }

    // Assignment operator
    DynamicArray& operator=(const DynamicArray& other) {
        if (this != &other) {
            delete[] array;
            capacity = other.capacity;
            size = other.size;
            array = new T[capacity];
            for (size_t i = 0; i < size; ++i) {
                array[i] = other.array[i];
            }
        }
        return *this;
    }

    // Add an element to the end of the array
    void push_back(const T& element) {
        if (size >= capacity) {
            // Double the capacity if needed
            capacity = (capacity == 0) ? 1 : capacity * 2;
            T* newArray = new T[capacity];
            for (size_t i = 0; i < size; ++i) {
                newArray[i] = array[i];
            }
            delete[] array;
            array = newArray;
        }
        array[size++] = element;
    }

    // Remove the last element from the array
    void pop_back() {
        if (size > 0) {
            --size;
        }
    }

    // Get the current number of elements in the array
    size_t getSize() const {
        return size;
    }

    // Get the element at a specific index
    T& operator[](size_t index) {
        if (index >= size) {
            throw std::out_of_range("Index out of range");
        }
        return array[index];
    }

    // Const version of operator[] for read-only access
    const T& operator[](size_t index) const {
        if (index >= size) {
            throw std::out_of_range("Index out of range");
        }
        return array[index];
    }
};

int main() {
    DynamicArray<int> arr;
    arr.push_back(1);
    arr.push_back(2);
    arr.push_back(3);

    for (size_t i = 0; i < arr.getSize(); ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

This implementation provides basic functionality for a dynamic array, including adding elements at the end, removing elements from the end, accessing elements by index, and resizing the array dynamically as needed.

### 1. Algorithms & Data Structures (C++): Dynamic Arrays

Dynamic arrays, also known as resizable arrays or vectors in C++, are a fundamental data structure that allows for efficient insertion, deletion, and retrieval of elements. Unlike static arrays, dynamic arrays can dynamically resize themselves to accommodate a varying number of elements. In C++, the standard library provides the `std::vector` container, which is a dynamic array implementation.

Here's an overview of how dynamic arrays work in C++:

#### `std::vector` in C++

```cpp
#include <vector>
#include <iostream>

int main() {
    // Declare a dynamic array of integers
    std::vector<int> dynamicArray;

    // Add elements to the dynamic array
    dynamicArray.push_back(10);
    dynamicArray.push_back(20);
    dynamicArray.push_back(30);

    // Access elements using array syntax
    std::cout << "First element: " << dynamicArray[0] << std::endl;

    // Modify elements
    dynamicArray[1] = 25;

    // Iterate through elements
    for (int i = 0; i < dynamicArray.size(); ++i) {
        std::cout << dynamicArray[i] << " ";
    }
    std::cout << std::endl;

    // Size of the dynamic array
    std::cout << "Size of dynamic array: " << dynamicArray.size() << std::endl;

    // Resize the dynamic array
    dynamicArray.resize(5, 50); // New elements initialized to 50

    return 0;
}
```

#### Key Features

1. **Dynamic Resizing**: The `std::vector` container automatically manages the storage for its elements. When elements are added beyond the current capacity, it reallocates memory to accommodate more elements efficiently.

2. **Random Access**: Elements can be accessed using the subscript (`[]`) operator just like in arrays. This allows for constant-time access to elements.

3. **Efficient Insertion and Deletion**: Unlike static arrays, inserting and deleting elements from anywhere in the dynamic array is efficient. However, insertion or deletion at the beginning or middle of the array can involve moving elements, which can be less efficient compared to adding or removing elements from the end.

4. **Automatic Memory Management**: `std::vector` manages memory automatically, handling memory allocation and deallocation. You don't need to worry about memory management.

5. **Iterators**: It supports iterators which allow traversing the elements efficiently.

6. **Various Operations**: `std::vector` provides various member functions for different operations such as resizing, clearing, swapping, etc.

Dynamic arrays are widely used in C++ for their flexibility and efficiency in managing collections of elements whose size may change over time. They are suitable for many applications ranging from simple data storage to more complex algorithms and data structures.

### 1. Algorithms & Data Structures (C++): How are resizable arrays implemented

Resizable arrays, also known as dynamic arrays or vectors in C++, are implemented using a combination of fixed-size arrays and dynamic memory allocation. The standard library in C++ provides the `std::vector` class, which is a dynamic array implementation.

Here's a simplified explanation of how resizable arrays are typically implemented:

1. **Fixed-size Array**: Initially, a resizable array is implemented using a fixed-size array. This array has a certain capacity, which is the maximum number of elements it can hold without resizing.

2. **Dynamic Memory Allocation**: When the array reaches its capacity and there's a need to add more elements, a new, larger array is allocated in memory using dynamic memory allocation functions like `new` in C++.

3. **Copying Elements**: The elements from the old array are copied to the new array. This is necessary because the new array might be at a different memory location.

4. **Deallocation**: After the elements are copied to the new array, the memory occupied by the old array is deallocated using `delete` in C++. This step is crucial to prevent memory leaks.

5. **Updating Capacity**: The capacity of the resizable array is updated to the new size of the allocated array.

6. **Adding Elements**: New elements can now be added to the resizable array.

7. **Size Management**: The resizable array keeps track of the number of elements it currently holds (size) and its total capacity.

Here's a simplified example of how this might look in C++:

```cpp
class ResizableArray {
private:
    int* array; // Pointer to the dynamically allocated array
    int size;   // Number of elements currently in the array
    int capacity; // Capacity of the array

public:
    // Constructor
    ResizableArray() {
        size = 0;
        capacity = 2; // Initial capacity
        array = new int[capacity];
    }

    // Destructor
    ~ResizableArray() {
        delete[] array;
    }

    // Method to add an element to the array
    void add(int element) {
        if (size == capacity) {
            // If array is full, double its capacity
            int* newArray = new int[capacity * 2];
            // Copy elements to the new array
            for (int i = 0; i < size; ++i) {
                newArray[i] = array[i];
            }
            // Deallocate old array
            delete[] array;
            // Update array pointer to the new array
            array = newArray;
            // Update capacity
            capacity *= 2;
        }
        // Add new element
        array[size++] = element;
    }
};
```

In this example, when the array is full (`size == capacity`), a new array with double the capacity is allocated, elements are copied over, the old array is deallocated, and the pointer is updated to point to the new array.

### 1. Algorithms & Data Structures (C++): Implementing An Array

Sure, let's implement a basic array data structure in C++. An array is a collection of elements stored in contiguous memory locations and accessed using an index. Here's a simple implementation:

```cpp
#include <iostream>
#include <stdexcept>

template <typename T>
class Array {
private:
    T* data; // Pointer to the dynamically allocated array
    size_t size; // Number of elements in the array

public:
    // Constructor
    Array(size_t size) : size(size) {
        data = new T[size];
    }

    // Destructor
    ~Array() {
        delete[] data;
    }

    // Copy constructor
    Array(const Array& other) : size(other.size) {
        data = new T[size];
        for (size_t i = 0; i < size; ++i) {
            data[i] = other.data[i];
        }
    }

    // Assignment operator
    Array& operator=(const Array& other) {
        if (this != &other) {
            delete[] data;
            size = other.size;
            data = new T[size];
            for (size_t i = 0; i < size; ++i) {
                data[i] = other.data[i];
            }
        }
        return *this;
    }

    // Access element at index
    T& operator[](size_t index) {
        if (index >= size) {
            throw std::out_of_range("Index out of range");
        }
        return data[index];
    }

    // Get size of the array
    size_t getSize() const {
        return size;
    }
};
```

This `Array` class provides basic functionality for creating an array, accessing elements by index, and getting the size of the array. Here's an example usage:

```cpp
int main() {
    Array<int> arr(5); // Creating an array of integers with size 5

    // Assigning values to the array elements
    for (size_t i = 0; i < arr.getSize(); ++i) {
        arr[i] = i * 2;
    }

    // Accessing and printing array elements
    for (size_t i = 0; i < arr.getSize(); ++i) {
        std::cout << "arr[" << i << "] = " << arr[i] << std::endl;
    }

    return 0;
}
```

This program creates an array of integers with a size of 5, assigns values to its elements, and then prints them out.

### 1. Algorithms & Data Structures (C++): indexOf() operation on Array

Sure! Implementing an `indexOf()` operation on an array in C++ is relatively straightforward. The `indexOf()` function returns the index of the first occurrence of a specified element in the array, or -1 if the element is not found. Here's a simple implementation:

```cpp
#include <iostream>

// Function to find the index of a specified element in an array
int indexOf(int arr[], int size, int target) {
    for (int i = 0; i < size; ++i) {
        if (arr[i] == target) {
            return i; // Return the index if the element is found
        }
    }
    return -1; // Return -1 if the element is not found
}

int main() {
    int arr[] = {5, 10, 15, 20, 25};
    int size = sizeof(arr) / sizeof(arr[0]);
    int target = 15;

    int index = indexOf(arr, size, target);

    if (index != -1) {
        std::cout << "Element " << target << " found at index " << index << std::endl;
    } else {
        std::cout << "Element " << target << " not found in the array" << std::endl;
    }

    return 0;
}
```

In this implementation:

* The `indexOf()` function takes three parameters: the array (`arr`), the size of the array (`size`), and the target element to search for (`target`).
* It iterates through the array elements using a `for` loop and checks if each element matches the target element.
* If a match is found, it returns the index of that element.
* If no match is found after iterating through the entire array, it returns -1 to indicate that the target element is not present in the array.

You can modify the `target` variable to search for different elements in the array.

### 1. Algorithms & Data Structures (C++): Inserting in an Array

Inserting elements into an array in C++ involves several methods depending on whether you're inserting at the beginning, middle, or end of the array. Here's a basic overview:

1. **Inserting at the Beginning**:
   * To insert an element at the beginning of an array, you need to shift all existing elements to the right and then insert the new element at index 0.

   ```cpp
   void insertAtBeginning(int arr[], int size, int element) {
       for (int i = size - 1; i >= 0; i--) {
           arr[i + 1] = arr[i];
       }
       arr[0] = element;
   }
   ```

2. **Inserting at the End**:
   * Inserting at the end is relatively simple. You just insert the element at the next available index after the last element.

   ```cpp
   void insertAtEnd(int arr[], int size, int element) {
       arr[size] = element;
   }
   ```

3. **Inserting at a Specific Position**:
   * To insert an element at a specific position, you need to shift all elements to the right from the insertion point and then insert the new element at that index.

   ```cpp
   void insertAtPosition(int arr[], int size, int element, int position) {
       for (int i = size - 1; i >= position; i--) {
           arr[i + 1] = arr[i];
       }
       arr[position] = element;
   }
   ```

Remember, these are basic implementations assuming the array has enough space to accommodate the new element. In real-world scenarios, you might need to consider dynamic resizing or use data structures like vectors in C++ to handle dynamic memory allocation more effectively.

### 1. Algorithms & Data Structures (C++): Memory Management of Arrays and Vectors

In C++, memory management for arrays and vectors is crucial for efficient and safe programming. Let's dive into how arrays and vectors handle memory management:

#### Arrays

1. **Static Arrays**: When you declare an array with a fixed size at compile-time, memory for the array is allocated on the stack or in the static memory region. For example:

    ```cpp
    int arr[10]; // Memory allocated on stack or static memory
    ```

   * **Advantages**: Fast access, no overhead for memory management.
   * **Disadvantages**: Fixed size, cannot be resized dynamically.

2. **Dynamic Arrays (Using `new` and `delete`)**: You can also allocate memory for arrays dynamically at runtime using the `new` keyword, and deallocate it using `delete`. For example:

    ```cpp
    int* arr = new int[10]; // Memory allocated on heap
    // Use arr
    delete[] arr; // Free memory
    ```

   * **Advantages**: Dynamic size, resizable.
   * **Disadvantages**: Manual memory management, risk of memory leaks if not handled properly.

#### Vectors (Dynamic Arrays)

Vectors in C++ are part of the Standard Template Library (STL) and provide dynamic array functionality with automatic memory management. Vectors automatically handle memory allocation and deallocation.

```cpp
#include <vector>

std::vector<int> vec; // Create an empty vector

vec.push_back(10); // Add elements dynamically
```

* **Advantages**:
  * Dynamic size: Vectors can grow or shrink dynamically.
  * Automatic memory management: No need to manually allocate or deallocate memory.
  * Range-checked access: Accessing elements is bounds-checked, reducing the risk of memory access errors.
  * Various utility functions: Vectors provide several member functions for common operations like sorting, searching, etc.

* **Disadvantages**:
  * Slightly more overhead compared to plain arrays due to additional functionality.
  * Insertion or deletion of elements at the beginning or middle of the vector can be inefficient as it may require shifting elements.

#### Memory Management Best Practices

1. **Prefer Vectors**: Unless you have a specific reason to use plain arrays, prefer vectors due to their safety and convenience.
2. **Use Smart Pointers**: If you still need to manage dynamic memory manually, prefer smart pointers like `std::unique_ptr` or `std::shared_ptr` over raw pointers to avoid memory leaks and dangling pointers.
3. **Avoid Manual Memory Management**: Whenever possible, use higher-level abstractions like vectors to avoid manual memory management and associated risks.

Understanding memory management in C++ is crucial for writing efficient and bug-free code, especially in scenarios where memory resources are limited or performance is critical.

### 1. Algorithms & Data Structures (C++): One Dimensional Array Practice

Sure! One-dimensional arrays are a fundamental data structure in programming. They allow you to store and manipulate a collection of elements of the same data type in a contiguous memory location. Here are some common operations and practice problems related to one-dimensional arrays in C++:

#### Common Operations

1. **Initialization**: Initialize an array with a set of values.
2. **Accessing Elements**: Access individual elements of the array using their indices.
3. **Insertion**: Insert an element into the array at a specified position.
4. **Deletion**: Delete an element from the array at a specified position.
5. **Traversal**: Iterate through all the elements of the array.
6. **Searching**: Search for a specific element within the array.
7. **Sorting**: Sort the elements of the array in ascending or descending order.
8. **Merging**: Merge two sorted arrays into a single sorted array.
9. **Reversal**: Reverse the order of elements in the array.
10. **Finding Maximum/Minimum**: Find the maximum or minimum element in the array.

#### Practice Problems

1. **Sum of Array Elements**: Calculate the sum of all elements in the array.
2. **Product of Array Elements**: Calculate the product of all elements in the array.
3. **Average of Array Elements**: Calculate the average of all elements in the array.
4. **Maximum Subarray Sum**: Find the contiguous subarray within the array that has the largest sum.
5. **Find Duplicate Element**: Find any duplicate element in the array.
6. **Remove Duplicates**: Remove all duplicate elements from the array.
7. **Check for Palindrome**: Check if the array is a palindrome (reads the same forwards and backwards).
8. **Rotate Array**: Rotate the elements of the array to the left or right by a given number of steps.
9. **Find Missing Number**: Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.
10. **Sort Array by Parity**: Sort the array such that all even elements come before odd elements.

These are just a few examples to get you started. As you practice more with arrays, you'll encounter more complex problems that require a deeper understanding of algorithms and data structures.

### 1. Algorithms & Data Structures (C++): Program for Adding Sparse Matrix

Sure, here's a C++ program for adding two sparse matrices:

```cpp
#include <iostream>
using namespace std;

const int MAX = 100;

class SparseMatrix {
    int row, col, num;
    int data[MAX][3];
public:
    SparseMatrix(int r, int c, int n) {
        row = r;
        col = c;
        num = n;
    }

    void read() {
        cout << "Enter non-zero elements (row, column, value):" << endl;
        for (int i = 0; i < num; i++) {
            cin >> data[i][0] >> data[i][1] >> data[i][2];
        }
    }

    void display() {
        int k = 0;
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                if (i == data[k][0] && j == data[k][1])
                    cout << data[k++][2] << " ";
                else
                    cout << "0 ";
            }
            cout << endl;
        }
    }

    SparseMatrix add(SparseMatrix &b) {
        if (row != b.row || col != b.col) {
            cerr << "Matrix dimensions don't match!" << endl;
            exit(1);
        }
        SparseMatrix result(row, col, 0);
        int i = 0, j = 0, k = 0;
        while (i < num && j < b.num) {
            if (data[i][0] < b.data[j][0] || (data[i][0] == b.data[j][0] && data[i][1] < b.data[j][1])) {
                result.data[k][0] = data[i][0];
                result.data[k][1] = data[i][1];
                result.data[k++][2] = data[i++][2];
            } else if (data[i][0] > b.data[j][0] || (data[i][0] == b.data[j][0] && data[i][1] > b.data[j][1])) {
                result.data[k][0] = b.data[j][0];
                result.data[k][1] = b.data[j][1];
                result.data[k++][2] = b.data[j++][2];
            } else {
                result.data[k][0] = data[i][0];
                result.data[k][1] = data[i][1];
                result.data[k++][2] = data[i++][2] + b.data[j++][2];
            }
            result.num++;
        }
        while (i < num) {
            result.data[k][0] = data[i][0];
            result.data[k][1] = data[i][1];
            result.data[k++][2] = data[i++][2];
            result.num++;
        }
        while (j < b.num) {
            result.data[k][0] = b.data[j][0];
            result.data[k][1] = b.data[j][1];
            result.data[k++][2] = b.data[j++][2];
            result.num++;
        }
        return result;
    }
};

int main() {
    int r, c, n;
    cout << "Enter the dimensions of the matrices (row column): ";
    cin >> r >> c;
    cout << "Enter the number of non-zero elements in the first matrix: ";
    cin >> n;
    SparseMatrix a(r, c, n);
    a.read();
    cout << "Enter the number of non-zero elements in the second matrix: ";
    cin >> n;
    SparseMatrix b(r, c, n);
    b.read();

    SparseMatrix result = a.add(b);

    cout << "Matrix A:" << endl;
    a.display();
    cout << "Matrix B:" << endl;
    b.display();
    cout << "Sum of Matrix A and B:" << endl;
    result.display();

    return 0;
}
```

This program allows you to input the dimensions and non-zero elements of two sparse matrices, and then adds them together, displaying the result.

### 1. Algorithms & Data Structures (C++): Representation of 2-Dim Arrays

In C++, a 2D array can be represented in multiple ways. One common approach is to use a nested array, where each element of the outer array is itself an array representing a row of the 2D array. Another approach is to use a single contiguous array and compute indices manually to simulate a 2D array.

Here's an example of both approaches:

#### Nested Array Approach

```cpp
#include <iostream>
using namespace std;

const int ROWS = 3;
const int COLS = 4;

int main() {
    // Define a 2D array using a nested array
    int arr[ROWS][COLS] = {
        {1, 2, 3, 4},
        {5, 6, 7, 8},
        {9, 10, 11, 12}
    };

    // Accessing elements
    cout << "Element at arr[1][2]: " << arr[1][2] << endl;

    return 0;
}
```

#### Single Array Approach

```cpp
#include <iostream>
using namespace std;

const int ROWS = 3;
const int COLS = 4;

int main() {
    // Define a 2D array using a single contiguous array
    int arr[ROWS * COLS] = {
        1, 2, 3, 4,
        5, 6, 7, 8,
        9, 10, 11, 12
    };

    // Accessing elements
    // Simulate 2D indexing using manual calculation
    int row = 1;
    int col = 2;
    int index = row * COLS + col;
    cout << "Element at arr[1][2]: " << arr[index] << endl;

    return 0;
}
```

In both approaches, `ROWS` and `COLS` represent the dimensions of the 2D array. The nested array approach provides more readability and convenience, while the single array approach saves memory by using a single contiguous block. However, the single array approach requires manual calculation of indices for accessing elements. Choose the approach based on your specific requirements and preferences.

### 1. Algorithms & Data Structures (C++): Representation of Arrays

In C++, arrays are a fundamental data structure used to store elements of the same data type in contiguous memory locations. Here's a basic representation of arrays in C++:

```cpp
#include <iostream>

int main() {
    // Declaration and initialization of an array
    int myArray[5] = {1, 2, 3, 4, 5};

    // Accessing elements of the array
    std::cout << "Elements of the array:" << std::endl;
    for (int i = 0; i < 5; ++i) {
        std::cout << "Element at index " << i << ": " << myArray[i] << std::endl;
    }

    return 0;
}
```

In this example:

* `int myArray[5]` declares an array named `myArray` of size 5 capable of holding integers.
* The elements of the array are initialized with values `{1, 2, 3, 4, 5}`.
* The elements of the array can be accessed using array indexing, starting from 0.
* The loop iterates through each element of the array and prints its value along with its index.

Arrays in C++ have fixed sizes determined at compile time. If you need dynamic sizing, you might consider using other data structures like vectors from the C++ Standard Template Library (STL) or dynamic memory allocation (e.g., `new` and `delete` keywords).

### 1. Algorithms & Data Structures (C++): Resizable array complexity analysis

Sure! Let's analyze the time complexity of basic operations on a resizable array (also known as a dynamic array) in C++, assuming that the array is implemented using a dynamically allocated array.

1. **Accessing an element by index (arr[i]):**
   * Time Complexity: O(1)
   * Explanation: Accessing an element by index in an array has constant time complexity because the index allows direct access to the memory location of the element.

2. **Insertion at the end (push_back()):**
   * Time Complexity: O(1) amortized
   * Explanation: When there is enough capacity in the array, adding an element to the end (push_back) takes constant time because it involves appending the element to the end of the array. However, if the array needs to be resized (when the current capacity is not enough), it will take O(n) time where n is the number of elements in the array. But since resizing doesn't happen every time an element is added, the average time taken for insertion at the end is O(1) over a series of insertions.

3. **Deletion from the end (pop_back()):**
   * Time Complexity: O(1)
   * Explanation: Removing the last element from the array takes constant time because it involves simply decrementing the size of the array. No resizing is needed in this case.

4. **Insertion/Deletion at/from the beginning or middle:**
   * Time Complexity: O(n)
   * Explanation: Inserting or deleting an element at/from the beginning or middle of the array requires shifting elements, which takes linear time proportional to the number of elements in the array.

5. **Resizing the array (when necessary):**
   * Time Complexity: O(n)
   * Explanation: Resizing the array involves allocating a new array with larger capacity, copying the existing elements into the new array, and deallocating the old array. This process takes linear time proportional to the number of elements in the array.

Overall, the resizable array provides efficient constant-time access to elements by index and amortized constant-time insertion at the end, making it a versatile data structure for many applications. However, insertion or deletion operations at the beginning or middle of the array are less efficient due to the need for shifting elements, which takes linear time. Resizing the array, when necessary, also takes linear time but occurs infrequently enough to provide overall efficient performance.

### 1. Algorithms & Data Structures (C++): Set operations on Array: Union, Intersection and Difference

Certainly! Here's how you can implement set operations like Union, Intersection, and Difference on arrays in C++:

```cpp
#include <iostream>
#include <unordered_set>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> setUnion(const vector<int>& arr1, const vector<int>& arr2) {
    unordered_set<int> unionSet;
    for (int num : arr1)
        unionSet.insert(num);
    for (int num : arr2)
        unionSet.insert(num);
    
    vector<int> result(unionSet.begin(), unionSet.end());
    return result;
}

vector<int> setIntersection(const vector<int>& arr1, const vector<int>& arr2) {
    unordered_set<int> intersectionSet(arr1.begin(), arr1.end());
    vector<int> result;
    for (int num : arr2) {
        if (intersectionSet.find(num) != intersectionSet.end())
            result.push_back(num);
    }
    return result;
}

vector<int> setDifference(const vector<int>& arr1, const vector<int>& arr2) {
    unordered_set<int> differenceSet(arr1.begin(), arr1.end());
    for (int num : arr2)
        differenceSet.erase(num);
    
    vector<int> result(differenceSet.begin(), differenceSet.end());
    return result;
}

int main() {
    vector<int> arr1 = {1, 2, 3, 4, 5};
    vector<int> arr2 = {3, 4, 5, 6, 7};
    
    // Union
    vector<int> unionResult = setUnion(arr1, arr2);
    cout << "Union: ";
    for (int num : unionResult)
        cout << num << " ";
    cout << endl;
    
    // Intersection
    vector<int> intersectionResult = setIntersection(arr1, arr2);
    cout << "Intersection: ";
    for (int num : intersectionResult)
        cout << num << " ";
    cout << endl;
    
    // Difference
    vector<int> differenceResult = setDifference(arr1, arr2);
    cout << "Difference (arr1 - arr2): ";
    for (int num : differenceResult)
        cout << num << " ";
    cout << endl;
    
    return 0;
}
```

This code defines three functions `setUnion`, `setIntersection`, and `setDifference` to compute the union, intersection, and difference of two arrays respectively. It utilizes `unordered_set` to efficiently handle set operations.

### 1. Algorithms & Data Structures (C++): Shifting the data Elements of an Array

Shifting the elements of an array in C++ can be done in various ways depending on your requirements. One common operation is shifting all elements to the left or right by a certain number of positions. Here's how you can do it:

#### Shifting Left

```cpp
#include <iostream>

void shiftLeft(int arr[], int size, int shiftBy) {
    for (int i = 0; i < shiftBy; ++i) {
        int temp = arr[0]; // Store the first element
        for (int j = 0; j < size - 1; ++j) {
            arr[j] = arr[j + 1]; // Shift each element one position to the left
        }
        arr[size - 1] = temp; // Place the first element at the end
    }
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int size = sizeof(arr) / sizeof(arr[0]);
    int shiftBy = 2; // Shift left by 2 positions

    shiftLeft(arr, size, shiftBy);

    std::cout << "Array after shifting left by " << shiftBy << " positions: ";
    for (int i = 0; i < size; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

#### Shifting Right

```cpp
#include <iostream>

void shiftRight(int arr[], int size, int shiftBy) {
    for (int i = 0; i < shiftBy; ++i) {
        int temp = arr[size - 1]; // Store the last element
        for (int j = size - 1; j > 0; --j) {
            arr[j] = arr[j - 1]; // Shift each element one position to the right
        }
        arr[0] = temp; // Place the last element at the beginning
    }
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int size = sizeof(arr) / sizeof(arr[0]);
    int shiftBy = 2; // Shift right by 2 positions

    shiftRight(arr, size, shiftBy);

    std::cout << "Array after shifting right by " << shiftBy << " positions: ";
    for (int i = 0; i < size; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

These are basic implementations. Depending on your needs, you might need to consider more efficient algorithms, especially for large arrays or if performance is critical. Also, note that these implementations modify the original array. If you need to keep the original array intact, you might want to work with a copy of the array.

### 1. Algorithms & Data Structures (C++): Sorted Array

A sorted array in C++ refers to an array where the elements are arranged in ascending or descending order. Sorting is a fundamental operation in computer science and is used extensively in various algorithms and data structures.

Here's a simple example of a sorted array implementation in C++:

```cpp
#include <iostream>

class SortedArray {
private:
    int* array;
    int size;
    int capacity;

public:
    SortedArray(int capacity) {
        this->capacity = capacity;
        array = new int[capacity];
        size = 0;
    }

    ~SortedArray() {
        delete[] array;
    }

    void insert(int element) {
        if (size == capacity) {
            std::cout << "Array is full. Cannot insert more elements." << std::endl;
            return;
        }

        int i = size - 1;
        while (i >= 0 && array[i] > element) {
            array[i + 1] = array[i];
            i--;
        }
        array[i + 1] = element;
        size++;
    }

    void display() {
        std::cout << "Sorted Array: ";
        for (int i = 0; i < size; i++) {
            std::cout << array[i] << " ";
        }
        std::cout << std::endl;
    }
};

int main() {
    SortedArray arr(10);
    arr.insert(5);
    arr.insert(3);
    arr.insert(8);
    arr.insert(1);
    arr.insert(10);
    arr.display();

    return 0;
}
```

In this example:

* The `SortedArray` class maintains a dynamically allocated array of integers.
* The `insert` method inserts an element into the array while maintaining the sorted order.
* The `display` method prints the elements of the array.

You can further extend this implementation by adding methods for searching, deleting elements, or handling duplicates, depending on your requirements. Additionally, you can explore more efficient sorting algorithms like merge sort or quicksort for sorting the array initially.

### 1. Algorithms & Data Structures (C++): Static Vs Dynamic Arrays - Memory Layout of Main Memory

In C++, static arrays and dynamic arrays (commonly implemented as `std::array` and `std::vector`, respectively) have different memory layouts in main memory.

1. **Static Arrays:**
   * Memory for static arrays is allocated at compile time.
   * The size of a static array must be known at compile time.
   * Memory for static arrays is typically allocated on the stack or in the data segment of the program.
   * Static arrays have a fixed size, which cannot be changed at runtime.
   * Accessing elements of static arrays is typically faster than dynamic arrays because the compiler can optimize memory access patterns.

2. **Dynamic Arrays (std::vector in C++):**
   * Memory for dynamic arrays is allocated at runtime.
   * Dynamic arrays can resize dynamically as elements are added or removed.
   * Dynamic arrays typically use a heap memory allocation, managed by the `new` and `delete` operators or, in modern C++, by `std::allocator`.
   * Dynamic arrays have a more complex memory layout compared to static arrays. They typically consist of a pointer to the dynamically allocated memory block and additional metadata to keep track of the array's size and capacity.
   * Accessing elements of dynamic arrays might involve an additional level of indirection through the pointer to the data, which can introduce slight overhead compared to static arrays.

In terms of memory layout, a static array's memory is contiguous, meaning all elements are stored in adjacent memory locations. On the other hand, a dynamic array's memory might not be contiguous initially, and as elements are added and the array grows beyond its capacity, it might be reallocated to a new memory block, potentially leading to fragmentation.

Overall, the choice between static and dynamic arrays depends on the specific requirements of the program. Static arrays are suitable when the size is known at compile time and won't change, offering better performance due to their simpler memory layout. Dynamic arrays are more flexible, allowing resizing and dynamic memory management, but they might incur slightly more overhead due to their dynamic nature.

### 1. Algorithms & Data Structures (C++): Subsequence Based Problems

Subsequence-based problems in algorithms and data structures often involve finding or analyzing subsequences within a given sequence. A subsequence is a sequence that can be derived from another sequence by deleting some or no elements without changing the order of the remaining elements. Here are some common subsequence-based problems in C++:

1. **Longest Increasing Subsequence (LIS)**:
   * Problem: Given an array of integers, find the length of the longest increasing subsequence.
   * Solution: This problem can be solved using dynamic programming. You can define a DP array where `dp[i]` represents the length of the longest increasing subsequence ending at index `i`.
   * Code Example:

    ```cpp
    int lengthOfLIS(vector<int>& nums) {
        int n = nums.size();
        vector<int> dp(n, 1);
        int maxLen = 1;
        
        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) {
                    dp[i] = max(dp[i], dp[j] + 1);
                    maxLen = max(maxLen, dp[i]);
                }
            }
        }
        
        return maxLen;
    }
    ```

2. **Longest Common Subsequence (LCS)**:
   * Problem: Given two sequences, find the length of the longest subsequence present in both of them.
   * Solution: This can also be solved using dynamic programming. You can define a 2D DP array where `dp[i][j]` represents the length of LCS for `text1[0...i]` and `text2[0...j]`.
   * Code Example:

    ```cpp
    int longestCommonSubsequence(string text1, string text2) {
        int m = text1.size(), n = text2.size();
        vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));
        
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (text1[i - 1] == text2[j - 1])
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                else
                    dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
            }
        }
        
        return dp[m][n];
    }
    ```

3. **Maximum Sum Increasing Subsequence**:
   * Problem: Given an array of integers, find the sum of the maximum sum subsequence such that the integers in the subsequence are sorted in increasing order.
   * Solution: This can also be solved using dynamic programming. You can define a DP array where `dp[i]` represents the maximum sum of increasing subsequence ending at index `i`.
   * Code Example:

    ```cpp
    int maxSumIncreasingSubsequence(vector<int>& nums) {
        int n = nums.size();
        vector<int> dp(n);
        int maxSum = INT_MIN;
        
        for (int i = 0; i < n; i++) {
            dp[i] = nums[i];
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) {
                    dp[i] = max(dp[i], dp[j] + nums[i]);
                }
            }
            maxSum = max(maxSum, dp[i]);
        }
        
        return maxSum;
    }
    ```

These are just a few examples of subsequence-based problems in C++. There are many more variations and complexities of these problems, and they often involve dynamic programming techniques for efficient solutions.

### 1. Algorithms & Data Structures (C++): Sum Closest

To find the sum of two numbers in an array that are closest to a given target value, you can follow these steps:

1. Sort the array.
2. Initialize two pointers, one at the beginning (left) and the other at the end (right) of the sorted array.
3. While the left pointer is less than the right pointer:
   a. Calculate the sum of the current elements pointed by the left and right pointers.
   b. Update the closest sum found so far if the absolute difference between the current sum and the target is less than the absolute difference between the closest sum and the target.
   c. If the current sum is less than the target, move the left pointer to the right (increasing the sum).
   d. If the current sum is greater than the target, move the right pointer to the left (decreasing the sum).
4. Repeat until the pointers meet.

Here's a C++ implementation of the algorithm:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <climits>

using namespace std;

pair<int, int> sumClosest(vector<int>& nums, int target) {
    sort(nums.begin(), nums.end()); // Sort the array
    int closestSum = INT_MAX;
    pair<int, int> result;

    int left = 0;
    int right = nums.size() - 1;

    while (left < right) {
        int sum = nums[left] + nums[right];
        int diff = abs(sum - target);

        if (diff < abs(closestSum - target)) {
            closestSum = sum;
            result = {nums[left], nums[right]};
        }

        if (sum < target) {
            left++;
        } else if (sum > target) {
            right--;
        } else { // If sum equals target, this is the closest possible sum
            return {nums[left], nums[right]};
        }
    }

    return result;
}

int main() {
    vector<int> nums = {1, 2, 4, 7, 11, 15};
    int target = 18;
    pair<int, int> closestPair = sumClosest(nums, target);

    cout << "Closest pair summing to " << target << ": " << closestPair.first << " and " << closestPair.second << endl;

    return 0;
}
```

This code demonstrates how to find the pair of numbers whose sum is closest to the target value in a given array. You can adjust the `nums` array and `target` value as per your requirement.

### 1. Algorithms & Data Structures (C++): Time and Space Complexity of One Dimensional Array

In computer science, analyzing algorithms and data structures involves understanding their time and space complexities. Let's discuss the time and space complexities of basic operations on a one-dimensional array in C++:

#### Time Complexity

1. **Accessing an element by index**: O(1)
   * Accessing an element in an array by index is a constant-time operation because it directly computes the memory address of the element based on its index.

2. **Searching for an element (Linear Search)**: O(n)
   * In the worst case, you might need to iterate through all n elements of the array to find the desired element.

3. **Insertion at the end of the array**: O(1) (Amortized)
   * If there's available space at the end of the array, inserting an element takes constant time. However, if resizing is required, it might take O(n) time to copy elements to a new array.

4. **Insertion at arbitrary index**: O(n)
   * Inserting an element at an arbitrary index may require shifting all subsequent elements, resulting in a time complexity proportional to the number of elements shifted.

5. **Deletion of an element**: O(n)
   * Similar to insertion, deleting an element may require shifting subsequent elements, leading to a time complexity proportional to the number of elements shifted.

6. **Sorting (e.g., using quicksort)**: O(n log n) (average case), O(n^2) (worst case)
   * Sorting algorithms typically have an average-case time complexity of O(n log n). However, some algorithms like quicksort may degrade to O(n^2) in the worst case.

#### Space Complexity

1. **Storage for elements**: O(n)
   * The space required to store n elements in an array is directly proportional to the number of elements.

2. **Additional space for variables**: O(1)
   * Except for the array itself, most operations don't require additional space that scales with the size of the array.

Understanding these complexities is crucial for designing efficient algorithms and data structures, as it helps in selecting the most appropriate solution for a given problem based on its input size and performance requirements.

### 1. Algorithms & Data Structures (C++): Time Complexity of Operations on Array

Certainly! In C++, arrays are a fundamental data structure used to store elements of the same type sequentially in memory. Understanding the time complexity of operations on arrays is crucial for designing efficient algorithms. Here's a summary of common operations and their time complexities on arrays:

1. **Accessing an element by index**: O(1)
   * Retrieving the value of an element by its index is a constant-time operation because arrays provide direct access to elements based on their memory addresses.

2. **Insertion at the end**: O(1) (amortized)
   * If there is available space in the array, inserting an element at the end (appending) is a constant-time operation because you simply need to update the value at the next available index. However, if the array needs to be resized (e.g., if it's dynamic), the operation may take longer, but still amortized O(1) on average.

3. **Insertion at the beginning or in the middle**: O(n)
   * Inserting an element at the beginning or in the middle of an array requires shifting all subsequent elements to make room, which takes linear time proportional to the number of elements already in the array.

4. **Deletion at the end**: O(1)
   * Removing the last element from an array is a constant-time operation because no shifting of elements is required.

5. **Deletion at the beginning or in the middle**: O(n)
   * Deleting an element from the beginning or in the middle of an array requires shifting all subsequent elements to fill the gap, resulting in linear time complexity.

6. **Searching for an element (unsorted array)**: O(n)
   * In the worst case, you might have to traverse the entire array to find the desired element, resulting in linear time complexity.

7. **Searching for an element (sorted array)**: O(log n) (using binary search)
   * If the array is sorted, you can utilize binary search to find an element in O(log n) time complexity.

8. **Sorting**: O(n log n) (using efficient sorting algorithms like Merge Sort, Quick Sort)
   * Sorting an array using efficient sorting algorithms typically requires O(n log n) time complexity.

These time complexities provide insights into the efficiency of various operations on arrays and help in choosing the appropriate data structure or algorithm for specific tasks.

### 1. Algorithms & Data Structures (C++): Trapping Rain Water - Arrays

Trapping Rain Water problem is a classic algorithmic problem that can be solved efficiently using arrays. The problem statement goes like this: given an elevation map represented by an array where the width of each bar is 1, calculate how much water it can trap after raining.

Here's a simple approach to solve this problem efficiently:

1. **Scan from left to right to find the maximum height of bars on the left of each bar.**
2. **Scan from right to left to find the maximum height of bars on the right of each bar.**
3. **Iterate over each bar and calculate the trapped water at that position as min(max_left, max_right) - height of the current bar.**

Here's a sample implementation in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int trap(vector<int>& height) {
    int n = height.size();
    if (n == 0) return 0;

    vector<int> max_left(n);
    vector<int> max_right(n);

    // Fill max_left array
    max_left[0] = height[0];
    for (int i = 1; i < n; ++i) {
        max_left[i] = max(max_left[i - 1], height[i]);
    }

    // Fill max_right array
    max_right[n - 1] = height[n - 1];
    for (int i = n - 2; i >= 0; --i) {
        max_right[i] = max(max_right[i + 1], height[i]);
    }

    int water = 0;
    // Calculate trapped water at each position
    for (int i = 0; i < n; ++i) {
        water += min(max_left[i], max_right[i]) - height[i];
    }

    return water;
}

int main() {
    vector<int> height = {0,1,0,2,1,0,1,3,2,1,2,1};
    cout << "Trapped water: " << trap(height) << endl;
    return 0;
}
```

This code snippet first calculates the maximum height of bars to the left and right of each bar in two separate passes. Then, it calculates the trapped water at each position by taking the minimum of the maximum heights on both sides and subtracting the height of the current bar. Finally, it sums up all the trapped water to get the total amount of trapped rainwater.

### 1. Algorithms & Data Structures (C++): Types of Array

In C++, arrays are one of the fundamental data structures, providing a contiguous block of memory to store elements of the same type. There are several types of arrays based on their dimensions, allocation methods, and usage. Here's an overview:

1. **Static Arrays**:
   * Static arrays have a fixed size determined at compile time.
   * Elements are stored in contiguous memory locations.
   * Once declared, their size cannot be changed during runtime.
   * Example:

     ```cpp
     int arr[5]; // Static array of integers with size 5
     ```

2. **Dynamic Arrays (Vector in C++)**:
   * Dynamic arrays allow resizing during runtime.
   * Memory is allocated dynamically using heap memory.
   * The `std::vector` container in C++ is a popular dynamic array implementation.
   * Provides dynamic resizing, insertion, and deletion of elements.
   * Example:

     ```cpp
     #include <vector>
     std::vector<int> dynamicArray; // Dynamic array of integers
     ```

3. **Multidimensional Arrays**:
   * Arrays having more than one dimension.
   * Can be represented as arrays of arrays or using pointers.
   * Example:

     ```cpp
     int matrix[3][3]; // Multidimensional static array
     ```

     ```cpp
     int** matrix; // Multidimensional dynamic array using pointers
     ```

4. **Jagged Arrays**:
   * Arrays of arrays where each row can have a different number of elements.
   * Often implemented using an array of pointers, where each pointer points to an array representing a row.
   * Example:

     ```cpp
     int* jaggedArray[3]; // Jagged array of integers
     ```

5. **Sparse Arrays**:
   * Arrays where most of the elements have the same value (often zero or null).
   * Storage-efficient representation techniques are used to handle such arrays.
   * Example:

     ```cpp
     // Sparse array representation using hash table or other data structures
     std::unordered_map<int, int> sparseArray;
     ```

Each type of array has its advantages and use cases. The choice depends on factors such as memory requirements, performance considerations, and the flexibility needed in the application.

### 1. Algorithms & Data Structures (C++): What are arrays and how they are stored

In C++, an array is a collection of elements of the same data type that are stored in contiguous memory locations. It provides a convenient way to store and access multiple elements of the same type under a single name.

Arrays are typically declared with a fixed size, meaning the number of elements they can hold must be specified at compile time. Here's the basic syntax for declaring an array in C++:

```cpp
dataType arrayName[arraySize];
```

For example, to declare an array of integers with a size of 5:

```cpp
int myArray[5];
```

Once declared, you can access individual elements of the array using square brackets `[]` and the index of the element (remembering that arrays in C++ are zero-indexed). For instance:

```cpp
myArray[0] = 10;  // Assigning value 10 to the first element
myArray[1] = 20;  // Assigning value 20 to the second element
// and so on...
```

Regarding how arrays are stored in memory, they are stored in contiguous memory locations, meaning that the memory addresses of successive elements are consecutive. This makes accessing elements of the array more efficient, as the compiler can calculate the memory address of any element based on the base address of the array and the index of the element.

Here's a visual representation of how an array might be stored in memory:

```bash
Index:     0       1       2       3       4
          +---+---+---+---+---+
Memory:   | 1 | 2 | 3 | 4 | 5 |
          +---+---+---+---+---+
```

In this example, assuming each integer takes up 4 bytes of memory, the array `myArray` consists of 5 integers stored consecutively in memory starting at some base address. So, `myArray[0]` is located at the base address, `myArray[1]` is at the base address + 4 bytes, `myArray[2]` is at the base address + 8 bytes, and so on.

### 1. Algorithms & Data Structures (C++): When to use/avoid array

Arrays in C++ are fundamental data structures that offer contiguous memory storage for elements of the same data type. They have several advantages, but also some limitations. Here's when to use and avoid using arrays:

#### When to Use Arrays

1. **Sequential Access**: Arrays provide constant time access to elements using their indices, which makes them efficient for sequential access scenarios.

2. **Fixed Size**: When the size of the collection is known beforehand and won't change during runtime, arrays are a good choice due to their fixed size.

3. **Efficient Random Access**: If you need fast access to elements by index and the indices are known or easily calculable, arrays provide O(1) time complexity for random access.

4. **Memory Efficiency**: Arrays use contiguous memory, which reduces memory overhead compared to some other data structures like linked lists, making them memory efficient.

5. **Efficient Iteration**: For-loops iterating over arrays are often more efficient than iterating over other data structures due to their contiguous memory layout.

#### When to Avoid Arrays

1. **Dynamic Size**: Arrays have a fixed size determined at compile-time. If you need a collection that can dynamically grow or shrink during runtime, arrays are not suitable. Consider using dynamic data structures like vectors or lists instead.

2. **Insertion and Deletion**: Insertion and deletion operations in arrays, especially in the middle or beginning, are inefficient because they require shifting elements. If your application involves frequent insertion or deletion of elements, arrays may not be the best choice.

3. **Heterogeneous Data Types**: Arrays in C++ store elements of the same data type. If you need to store elements of different data types, arrays are not suitable. Consider using structures or classes to create collections of heterogeneous data.

4. **Sparse Data**: If your data is sparse (i.e., it contains a lot of empty or null values), using arrays may waste memory, as they allocate memory for each element regardless of whether it's used or not. Sparse data structures like hash maps or trees might be more appropriate.

5. **Memory Overflows**: Arrays have a fixed size, so if you're not careful about bounds checking, you can easily run into memory overflow issues, leading to segmentation faults or undefined behavior. Consider using safer alternatives like std::array or std::vector with bounds checking enabled.

In summary, arrays are efficient for scenarios where you have a fixed-size collection with known indices and need fast access to elements. However, they are not suitable for dynamic collections, heterogeneous data types, frequent insertions/deletions, sparse data, or scenarios requiring bounds checking. In such cases, consider using more appropriate data structures provided by the C++ Standard Library.

### 1. Algorithms & Data Structures (C++): Why Arrays ? and What is Arrays ?

Arrays are fundamental data structures in computer science and programming. They provide a way to store and access a collection of elements of the same type under a single name. Here's why arrays are important and what they are:

1. **Efficient Access**: Arrays provide efficient random access to elements. This means you can access any element directly using its index, which is particularly useful in algorithms that require frequent access to elements, such as searching and sorting.

2. **Contiguous Memory Allocation**: In memory, array elements are stored in contiguous locations. This allows for efficient memory access patterns and cache utilization, leading to better performance compared to some other data structures.

3. **Simplicity**: Arrays are simple and straightforward to use. Once defined, you can easily manipulate elements using index-based operations.

4. **Versatility**: Arrays can be used to represent various data structures such as lists, queues, stacks, matrices, and strings. Many more complex data structures and algorithms are built upon or utilize arrays as their underlying representation.

However, arrays also have limitations:

1. **Fixed Size**: In most programming languages, arrays have a fixed size, meaning you need to know the maximum number of elements you'll store in advance. This can be limiting if the size needs to change dynamically during runtime.

2. **Linear Search Time**: Searching for an element in an unsorted array requires linear time complexity, meaning the time taken to search increases linearly with the size of the array.

3. **Insertion and Deletion**: Insertion and deletion operations in arrays, especially in the middle, can be inefficient as they may require shifting elements, resulting in a time complexity of O(n).

In C++, arrays are declared using the following syntax:

```cpp
dataType arrayName[arraySize];
```

Here, `dataType` specifies the type of elements the array will hold, `arrayName` is the name of the array, and `arraySize` is the number of elements in the array.

For example, to declare an array of integers with 5 elements:

```cpp
int myArray[5];
```

Arrays in C++ are zero-indexed, meaning the first element is accessed using index 0, the second using index 1, and so on.

## Problems

### 1. Algorithms & Data Structures (C++): Array Partition

Array partitioning is a common operation in computer science and involves rearranging the elements of an array in such a way that they're grouped according to some criteria. In the context of algorithms and data structures, array partitioning often refers to partitioning an array based on a pivot element, which is a central concept in many sorting algorithms like quicksort.

Here's a simple C++ implementation of array partitioning using a pivot element:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to partition the array around a pivot element
int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high]; // Choose the last element as the pivot
    int i = low - 1; // Index of the smaller element

    for (int j = low; j < high; j++) {
        // If the current element is smaller than or equal to the pivot
        if (arr[j] <= pivot) {
            i++; // Increment index of smaller element
            swap(arr[i], arr[j]); // Swap arr[i] and arr[j]
        }
    }
    swap(arr[i + 1], arr[high]); // Swap arr[i+1] and arr[high] (pivot)
    return i + 1; // Return the partitioning index
}

int main() {
    vector<int> arr = {10, 7, 8, 9, 1, 5};
    int n = arr.size();
    cout << "Original array: ";
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;

    int pivotIndex = partition(arr, 0, n - 1);

    cout << "Array after partitioning: ";
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;

    cout << "Index of pivot element after partitioning: " << pivotIndex << endl;

    return 0;
}
```

In this implementation:

* The `partition` function takes an array `arr`, along with the indices `low` and `high` representing the range of the array to partition.
* It chooses the last element of the array (`arr[high]`) as the pivot element.
* It iterates through the array from `low` to `high-1`, comparing each element to the pivot.
* If an element is smaller than or equal to the pivot, it swaps that element with the element at index `i`, where `i` is initially set to `low-1`.
* Finally, it swaps the pivot element (which is at index `high`) with the element at index `i+1`, placing the pivot in its correct sorted position.
* The function returns the index of the pivot element after partitioning.

In the `main` function, you can see an example of using this partition function on an array.

### 1. Algorithms & Data Structures (C++): Array permutations

Sure! Array permutations involve generating all possible arrangements of elements in an array. Here's a simple implementation of generating permutations of an array in C++ using recursion:

```cpp
#include <iostream>
#include <vector>
using namespace std;

// Function to generate permutations
void generatePermutations(vector<int>& nums, int start, vector<vector<int>>& result) {
    if (start == nums.size() - 1) {
        result.push_back(nums);
        return;
    }

    for (int i = start; i < nums.size(); ++i) {
        swap(nums[start], nums[i]);  // Swap current element with each element after it
        generatePermutations(nums, start + 1, result);  // Recursively generate permutations for the rest of the array
        swap(nums[start], nums[i]);  // Backtrack: restore the array to its original state
    }
}

// Function to print permutations
void printPermutations(const vector<vector<int>>& result) {
    for (const auto& perm : result) {
        for (int num : perm) {
            cout << num << " ";
        }
        cout << endl;
    }
}

int main() {
    vector<int> nums = {1, 2, 3};
    vector<vector<int>> result;
    generatePermutations(nums, 0, result);
    printPermutations(result);
    return 0;
}
```

This code defines a function `generatePermutations` which recursively generates all permutations of the array `nums`. It swaps each element with every element after it, recursively generates permutations for the rest of the array, and then swaps back to restore the array to its original state.

The `main` function demonstrates how to use this function to generate permutations of an example array `{1, 2, 3}` and then prints the generated permutations.

You can modify the array `nums` in the `main` function to generate permutations for different arrays.

### 1. Algorithms & Data Structures (C++): Array permutations: Complexity analysis

Sure, let's discuss the complexity analysis of generating permutations of an array in C++.

First, let's consider a straightforward approach to generating permutations recursively. One common method is to use backtracking. Here's a basic outline of how it works:

1. For each position in the array, swap the current element with every element after it.
2. Recursively generate permutations for the remaining elements.
3. Undo the swap to backtrack and try the next possibility.

Here's a simple implementation of this algorithm:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void generatePermutations(vector<int>& nums, int start, vector<vector<int>>& result) {
    if (start == nums.size()) {
        result.push_back(nums);
        return;
    }
    for (int i = start; i < nums.size(); ++i) {
        swap(nums[start], nums[i]);
        generatePermutations(nums, start + 1, result);
        swap(nums[start], nums[i]); // Backtrack
    }
}

vector<vector<int>> permute(vector<int>& nums) {
    vector<vector<int>> result;
    generatePermutations(nums, 0, result);
    return result;
}

int main() {
    vector<int> nums = {1, 2, 3};
    vector<vector<int>> permutations = permute(nums);
    for (const auto& perm : permutations) {
        for (int num : perm) {
            cout << num << " ";
        }
        cout << endl;
    }
    return 0;
}
```

Now let's analyze the time and space complexity of this algorithm:

1. Time Complexity:
   * There are \( n! \) permutations of an array of size \( n \), where \( n \) is the length of the array.
   * For each permutation, we perform \( O(n) \) operations to swap elements.
   * Therefore, the overall time complexity is \( O(n \cdot n!) \).

2. Space Complexity:
   * The space complexity is dominated by the recursive call stack. At any point in time, the maximum depth of the recursion is \( n \) (the number of elements in the array).
   * Additionally, the space complexity also includes the storage space for the resulting permutations, which is \( O(n \cdot n!) \) since there are \( n! \) permutations, each containing \( n \) elements.
   * So, the overall space complexity is \( O(n \cdot n!) \).

It's worth noting that while this approach generates all possible permutations, it's not the most efficient in terms of time complexity. There are more optimized algorithms like Heap's algorithm or Steinhaus�Johnson�Trotter algorithm which can generate permutations in \( O(n \cdot n!) \) time but are more complex to implement. However, for small input sizes, the straightforward backtracking approach is usually sufficient.

### 1. Algorithms & Data Structures (C++): Array Products

To implement an algorithm in C++ to find the product of all elements in an array except for the current element, you can use a simple approach leveraging prefix and suffix products. Here's how you can do it:

```cpp
#include <iostream>
#include <vector>

using namespace std;

vector<int> arrayProducts(const vector<int>& nums) {
    int n = nums.size();
    vector<int> result(n, 1); // Initialize result vector with 1s

    // Calculate prefix products
    int prefix = 1;
    for (int i = 0; i < n; ++i) {
        result[i] *= prefix;
        prefix *= nums[i];
    }

    // Calculate suffix products
    int suffix = 1;
    for (int i = n - 1; i >= 0; --i) {
        result[i] *= suffix;
        suffix *= nums[i];
    }

    return result;
}

int main() {
    // Example usage
    vector<int> nums = {1, 2, 3, 4, 5};
    vector<int> result = arrayProducts(nums);

    // Output the result
    cout << "Product of all elements except current element:\n";
    for (int num : result) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}
```

This code first initializes a result vector with 1s. Then, it calculates prefix products and stores them in the result vector, followed by calculating suffix products and updating the result vector accordingly. Finally, it returns the result vector containing products of all elements except the current element.

### 1. Algorithms & Data Structures (C++): Array Reverse

Sure, here's a simple C++ implementation to reverse an array:

```cpp
#include <iostream>

// Function to reverse the array
void reverseArray(int arr[], int start, int end) {
    while (start < end) {
        // Swapping elements at start and end indices
        int temp = arr[start];
        arr[start] = arr[end];
        arr[end] = temp;
        // Moving towards the center
        start++;
        end--;
    }
}

// Function to print the array
void printArray(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int n = sizeof(arr) / sizeof(arr[0]);

    std::cout << "Original array: ";
    printArray(arr, n);

    // Reverse the array
    reverseArray(arr, 0, n - 1);

    std::cout << "Reversed array: ";
    printArray(arr, n);

    return 0;
}
```

This code defines a function `reverseArray` that takes an array, a starting index, and an ending index. It then reverses the elements in the array between these two indices. The `main` function demonstrates how to use this function by reversing an array and printing the result.

### 1. Algorithms & Data Structures (C++): Array Stabilization

Array stabilization refers to a problem where you're given an array of integers and you want to stabilize it by minimizing the difference between the maximum and minimum elements after removing exactly one element from the array. In C++, you can solve this problem efficiently using sorting and basic array manipulation. Here's a basic outline of the algorithm:

1. Sort the array in non-decreasing order.
2. Calculate the difference between the maximum and minimum elements of the sorted array.
3. Consider two cases:
   a. Removing the first element and calculating the difference between the new maximum and minimum.
   b. Removing the last element and calculating the difference between the new maximum and minimum.
4. Return the minimum of the differences obtained in step 3.

Here's a C++ function implementing this algorithm:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int arrayStabilization(std::vector<int>& nums) {
    int n = nums.size();
    if (n <= 2) return 0; // If array has 1 or 2 elements, no need to remove any

    std::sort(nums.begin(), nums.end()); // Step 1

    // Step 2
    int originalDiff = nums[n - 1] - nums[0];

    // Step 3
    int newDiff1 = nums[n - 2] - nums[0];
    int newDiff2 = nums[n - 1] - nums[1];

    // Step 4
    return std::min(newDiff1, newDiff2);
}

int main() {
    std::vector<int> nums = {1, 5, 6, 2, 9};
    std::cout << "Minimum difference after stabilization: " << arrayStabilization(nums) << std::endl;
    return 0;
}
```

This code sorts the array and then calculates the difference for two possible scenarios after removing one element: removing the first element or removing the last element. Finally, it returns the minimum of these differences.

### 1. Algorithms & Data Structures (C++): Array: Reverse Array

Sure, here's a simple C++ implementation to reverse an array using pointers:

```cpp
#include <iostream>

void reverseArray(int arr[], int size) {
    int *start = arr; // Pointer to the first element
    int *end = arr + size - 1; // Pointer to the last element

    while (start < end) {
        // Swap the elements pointed by start and end
        int temp = *start;
        *start = *end;
        *end = temp;

        // Move the pointers towards each other
        start++;
        end--;
    }
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int size = sizeof(arr) / sizeof(arr[0]);

    std::cout << "Original array: ";
    for (int i = 0; i < size; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    reverseArray(arr, size);

    std::cout << "Reversed array: ";
    for (int i = 0; i < size; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

This code defines a function `reverseArray` that takes an array and its size as arguments and reverses the elements of the array in-place. Then, in the `main` function, an array is initialized, its original contents are printed, the array is reversed using the `reverseArray` function, and finally, the reversed array is printed.

### 1. Algorithms & Data Structures (C++): Arrays Question: Find first and last position of element in sorted Array

To find the first and last position of an element in a sorted array in C++, you can use a modified binary search algorithm. Here's a simple implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to find the first occurrence of the target element
int findFirstOccurrence(vector<int>& nums, int target) {
    int low = 0, high = nums.size() - 1;
    int result = -1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (nums[mid] == target) {
            result = mid;
            high = mid - 1; // Continue searching towards the left
        } else if (nums[mid] < target) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }

    return result;
}

// Function to find the last occurrence of the target element
int findLastOccurrence(vector<int>& nums, int target) {
    int low = 0, high = nums.size() - 1;
    int result = -1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (nums[mid] == target) {
            result = mid;
            low = mid + 1; // Continue searching towards the right
        } else if (nums[mid] < target) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }

    return result;
}

// Function to find first and last position of element in sorted Array
vector<int> searchRange(vector<int>& nums, int target) {
    vector<int> result(2, -1);

    int first = findFirstOccurrence(nums, target);
    if (first == -1) // If the element is not found, return {-1, -1}
        return result;

    int last = findLastOccurrence(nums, target);

    result[0] = first;
    result[1] = last;

    return result;
}

int main() {
    vector<int> nums = {5, 7, 7, 8, 8, 10};
    int target = 8;
    vector<int> positions = searchRange(nums, target);
    
    cout << "First occurrence: " << positions[0] << endl;
    cout << "Last occurrence: " << positions[1] << endl;

    return 0;
}
```

This code defines two functions: `findFirstOccurrence` and `findLastOccurrence`, which use modified binary search to find the first and last occurrences of the target element in the sorted array, respectively. Then, the `searchRange` function combines these two functions to return a vector containing the first and last occurrences of the target element. Finally, in the `main` function, an example usage is provided.

### 1. Algorithms & Data Structures (C++): Count of Smaller Numbers

To solve the problem of counting smaller numbers in an array, you can use a popular algorithm called Fenwick Tree or Binary Indexed Tree (BIT). This algorithm efficiently solves the problem in \( O(n\log n) \) time complexity.

Here's a brief explanation of how you can implement it in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Function to update the BIT
void update(vector<int> &bit, int index, int val) {
    while (index < bit.size()) {
        bit[index] += val;
        index += index & (-index);
    }
}

// Function to query the BIT
int query(vector<int> &bit, int index) {
    int sum = 0;
    while (index > 0) {
        sum += bit[index];
        index -= index & (-index);
    }
    return sum;
}

vector<int> countSmaller(vector<int>& nums) {
    vector<int> sorted_nums = nums; // Copy of nums
    sort(sorted_nums.begin(), sorted_nums.end());
    vector<int> bit(nums.size() + 1, 0); // Initializing BIT

    vector<int> result;
    for (int i = nums.size() - 1; i >= 0; --i) {
        int index = lower_bound(sorted_nums.begin(), sorted_nums.end(), nums[i]) - sorted_nums.begin() + 1;
        result.push_back(query(bit, index - 1));
        update(bit, index, 1);
    }

    reverse(result.begin(), result.end()); // Reversing the result
    return result;
}

int main() {
    vector<int> nums = {5, 2, 6, 1};
    vector<int> smallerCounts = countSmaller(nums);

    cout << "Counts of smaller numbers to the right of each element:" << endl;
    for (int count : smallerCounts) {
        cout << count << " ";
    }
    cout << endl;

    return 0;
}
```

This code will output the counts of smaller numbers to the right of each element in the array. You can replace the `nums` vector with your own array for testing.

### 1. Algorithms & Data Structures (C++): Divide Array in Sets of K Consecutive Numbers

To divide an array into sets of \( K \) consecutive numbers in C++, you can use a map to count the occurrences of each element and then iterate through the map while forming sets of consecutive numbers. Here's a possible implementation:

```cpp
#include <iostream>
#include <vector>
#include <map>

using namespace std;

bool isPossibleDivide(vector<int>& nums, int k) {
    map<int, int> counter;

    // Count occurrences of each number
    for (int num : nums)
        counter[num]++;

    // Iterate through the map
    for (auto it = counter.begin(); it != counter.end(); ++it) {
        if (it->second > 0) {
            int num = it->first;

            // Start forming a set of consecutive numbers
            for (int i = 0; i < k; ++i) {
                if (counter[num + i] < it->second)
                    return false; // Unable to form a set
                counter[num + i] -= it->second;
            }
        }
    }

    return true;
}

int main() {
    vector<int> nums = {1, 2, 3, 3, 4, 4, 5, 6};
    int k = 4;

    if (isPossibleDivide(nums, k))
        cout << "It is possible to divide the array into sets of " << k << " consecutive numbers." << endl;
    else
        cout << "It is not possible to divide the array into sets of " << k << " consecutive numbers." << endl;

    return 0;
}
```

This code will output whether it's possible to divide the array into sets of \( K \) consecutive numbers or not. The idea is to iterate through the array once to count the occurrences of each number, then iterate through the map formed by the counts to check if you can form sets of consecutive numbers. If at any point it's not possible to form a set, the function returns false; otherwise, it returns true.

### 1. Algorithms & Data Structures (C++): Find First And Last Position Of Element In Sorted Array

Certainly! You can implement an efficient algorithm to find the first and last position of an element in a sorted array using C++. Here's an example implementation:

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

// Function to find both the first and last occurrence of target in nums
pair<int, int> searchRange(vector<int>& nums, int target) {
    int first = findFirstOccurrence(nums, target);
    int last = findLastOccurrence(nums, target);
    return make_pair(first, last);
}

int main() {
    vector<int> nums = {5, 7, 7, 8, 8, 10};
    int target = 8;
    pair<int, int> result = searchRange(nums, target);
    
    if (result.first != -1 && result.second != -1) {
        cout << "First occurrence: " << result.first << endl;
        cout << "Last occurrence: " << result.second << endl;
    } else {
        cout << "Target not found in the array." << endl;
    }

    return 0;
}
```

This code performs a binary search to find the first occurrence of the target element and then separately finds the last occurrence of the target element. The functions `findFirstOccurrence()` and `findLastOccurrence()` implement binary search to find the first and last occurrences respectively. The `searchRange()` function combines these two searches and returns a pair containing the first and last occurrences.

### 1. Algorithms & Data Structures (C++): Find First And Last Position Of Element In Sorted Array - Binary Search

Sure, here's a C++ implementation to find the first and last position of an element in a sorted array using binary search:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int findFirstPosition(vector<int>& nums, int target) {
    int left = 0, right = nums.size() - 1;
    int result = -1;

    while (left <= right) {
        int mid = left + (right - left) / 2;
        
        if (nums[mid] >= target) {
            right = mid - 1;
            if (nums[mid] == target)
                result = mid;
        } else {
            left = mid + 1;
        }
    }

    return result;
}

int findLastPosition(vector<int>& nums, int target) {
    int left = 0, right = nums.size() - 1;
    int result = -1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (nums[mid] <= target) {
            left = mid + 1;
            if (nums[mid] == target)
                result = mid;
        } else {
            right = mid - 1;
        }
    }

    return result;
}

vector<int> searchRange(vector<int>& nums, int target) {
    int first = findFirstPosition(nums, target);
    int last = findLastPosition(nums, target);

    return {first, last};
}

int main() {
    vector<int> nums = {5, 7, 7, 8, 8, 10};
    int target = 8;

    vector<int> result = searchRange(nums, target);

    if (result[0] == -1 || result[1] == -1)
        cout << "Element not found\n";
    else
        cout << "First occurrence: " << result[0] << ", Last occurrence: " << result[1] << endl;

    return 0;
}
```

This code defines two functions `findFirstPosition` and `findLastPosition` to find the first and last positions of the target element in the sorted array using binary search. Then, a `searchRange` function combines these two to return the range. Finally, in the `main` function, it demonstrates the usage by searching for the first and last occurrences of the target element in the given array.

### 1. Algorithms & Data Structures (C++): Find K Closest Elements

To find the K closest elements to a given target value in a sorted array, you can use a two-pointer approach. Here's how you can do it in C++:

```cpp
#include <iostream>
#include <vector>
#include <cmath>

using namespace std;

vector<int> findClosestElements(vector<int>& arr, int k, int x) {
    int left = 0;
    int right = arr.size() - 1;

    // Binary search to find the closest element to 'x'
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] < x) {
            left = mid + 1;
        } else {
            right = mid;
        }
    }

    // 'right' now points to the closest element or the element itself
    int closestIndex = right;
    left = closestIndex - 1;
    right = closestIndex + 1;

    // Expand the window to find the K closest elements
    while (right - left - 1 < k) {
        if (left >= 0 && (right >= arr.size() || abs(arr[left] - x) <= abs(arr[right] - x))) {
            left--;
        } else {
            right++;
        }
    }

    // Construct the result vector
    vector<int> result(arr.begin() + left + 1, arr.begin() + right);
    return result;
}

int main() {
    vector<int> arr = {1, 2, 3, 4, 5};
    int k = 4;
    int x = 3;
    vector<int> closest = findClosestElements(arr, k, x);

    cout << "K closest elements to " << x << " are: ";
    for (int num : closest) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}
```

This code finds the closest element to the target 'x' using binary search. Then, it expands a window to include the K closest elements around that closest element. Finally, it constructs and returns the result vector containing the K closest elements.

### 1. Algorithms & Data Structures (C++): Find Pivot Index

To find the pivot index in an array using C++, you can iterate through the array and check if the sum of elements to the left of the current index is equal to the sum of elements to the right of the current index. If such an index is found, it is the pivot index. Here's a sample code to achieve this:

```cpp
#include <iostream>
#include <vector>

int findPivotIndex(const std::vector<int>& nums) {
    int totalSum = 0;
    int leftSum = 0;

    // Calculating total sum of the array
    for (int num : nums) {
        totalSum += num;
    }

    // Iterating through the array to find the pivot index
    for (int i = 0; i < nums.size(); ++i) {
        // If the sum of elements to the left is equal to the sum of elements to the right
        if (leftSum == totalSum - leftSum - nums[i]) {
            return i; // Found the pivot index
        }
        leftSum += nums[i]; // Incrementing left sum for the next iteration
    }

    // If pivot index not found, return -1
    return -1;
}

int main() {
    std::vector<int> nums = {1, 7, 3, 6, 5, 6};
    int pivotIndex = findPivotIndex(nums);
    if (pivotIndex != -1) {
        std::cout << "Pivot index: " << pivotIndex << std::endl;
    } else {
        std::cout << "No pivot index found." << std::endl;
    }
    return 0;
}
```

This code will output the index of the pivot if it exists, otherwise, it will indicate that no pivot index was found.

### 1. Algorithms & Data Structures (C++): Find Smallest missing positive number from an unsorted array

To find the smallest missing positive number from an unsorted array in C++, you can follow these steps:

1. Iterate through the array and move all positive integers to the beginning of the array.
2. Mark elements as visited by using the array indices.
3. Iterate through the positive integers again and mark elements as visited if they fall within the range of the array.
4. Finally, iterate through the positive integers again to find the first element that is not marked as visited. This will be the smallest missing positive number.

Here's a C++ code implementing this algorithm:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int firstMissingPositive(vector<int>& nums) {
    int n = nums.size();
    // Step 1: Move all positive integers to the beginning of the array
    int j = 0;
    for (int i = 0; i < n; ++i) {
        if (nums[i] > 0) {
            swap(nums[i], nums[j]);
            ++j;
        }
    }
    // Step 2: Mark elements as visited using array indices
    for (int i = 0; i < j; ++i) {
        if (abs(nums[i]) <= j) {
            nums[abs(nums[i]) - 1] = -abs(nums[abs(nums[i]) - 1]);
        }
    }
    // Step 3: Find the first positive integer that is not marked as visited
    for (int i = 0; i < j; ++i) {
        if (nums[i] > 0) {
            return i + 1;
        }
    }
    // If all positive integers are present, return the next number
    return j + 1;
}

int main() {
    vector<int> arr = {3, 4, -1, 1};
    int result = firstMissingPositive(arr);
    cout << "Smallest missing positive number: " << result << endl;
    return 0;
}
```

This code will output the smallest missing positive number from the given array.

### 1. Algorithms & Data Structures (C++): Find the duplicate

Certainly! Here's a simple algorithm in C++ to find duplicates in an array using a hash set:

```cpp
#include <iostream>
#include <unordered_set>
#include <vector>

std::vector<int> findDuplicates(const std::vector<int>& nums) {
    std::unordered_set<int> seen;
    std::vector<int> duplicates;
    
    for (int num : nums) {
        if (seen.count(num) == 0) {
            seen.insert(num);
        } else {
            duplicates.push_back(num);
        }
    }
    
    return duplicates;
}

int main() {
    std::vector<int> nums = {4, 3, 2, 7, 8, 2, 3, 1};
    std::vector<int> duplicates = findDuplicates(nums);
    
    if (duplicates.empty()) {
        std::cout << "No duplicates found." << std::endl;
    } else {
        std::cout << "Duplicates found: ";
        for (int num : duplicates) {
            std::cout << num << " ";
        }
        std::cout << std::endl;
    }
    
    return 0;
}
```

This code initializes an empty hash set to store seen elements and an empty vector to store duplicates. It iterates through the input array `nums`, for each element it checks if it's already in the hash set. If it's not, it adds it to the hash set. If it is, it adds the element to the `duplicates` vector. Finally, it returns the `duplicates` vector.

### 1. Algorithms & Data Structures (C++): Find the Duplicate Number

To find a duplicate number in an array using C++, you can employ various approaches. One common method is to utilize a set to keep track of numbers seen so far. As you iterate through the array, if you encounter a number that's already in the set, you've found the duplicate. Here's a sample implementation:

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>

int findDuplicate(const std::vector<int>& nums) {
    std::unordered_set<int> seen;

    for (int num : nums) {
        if (seen.find(num) != seen.end()) {
            // Found the duplicate
            return num;
        }
        seen.insert(num);
    }

    // No duplicate found
    return -1;
}

int main() {
    std::vector<int> nums = {1, 3, 4, 2, 2}; // Example array with duplicate
    int duplicate = findDuplicate(nums);
    if (duplicate != -1) {
        std::cout << "Duplicate number is: " << duplicate << std::endl;
    } else {
        std::cout << "No duplicate found." << std::endl;
    }
    return 0;
}
```

This code defines a function `findDuplicate` that takes a vector of integers as input and returns the duplicate number if found, otherwise -1. In the `main` function, you can see an example usage of this function with a sample array.

### 1. Algorithms & Data Structures (C++): Find the Duplicate Number - Sorting

To find a duplicate number in an array using sorting in C++, you can follow these steps:

1. Sort the array.
2. Iterate through the sorted array to find adjacent elements that are the same.

Here's how you can implement this algorithm:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int findDuplicate(std::vector<int>& nums) {
    // Sort the array
    std::sort(nums.begin(), nums.end());

    // Iterate through the sorted array to find the duplicate
    for (int i = 1; i < nums.size(); ++i) {
        if (nums[i] == nums[i - 1]) {
            return nums[i];
        }
    }

    // If no duplicate is found
    return -1; // or any appropriate indication of no duplicate
}

int main() {
    std::vector<int> nums = {1, 3, 4, 2, 2}; // Example array with a duplicate
    int duplicate = findDuplicate(nums);
    if (duplicate != -1) {
        std::cout << "Duplicate number: " << duplicate << std::endl;
    } else {
        std::cout << "No duplicate found." << std::endl;
    }
    return 0;
}
```

This code sorts the array and then iterates through it to find the duplicate number. The time complexity of this approach is O(n log n) due to the sorting step.

### 1. Algorithms & Data Structures (C++): Find the duplicate: Complexity analysis

To analyze the complexity of finding duplicates in an array using different algorithms and data structures in C++, let's consider a few common approaches:

1. **Brute Force**: Compare each element with every other element in the array. This approach has a time complexity of O(n^2), where n is the number of elements in the array.

2. **Sorting**: Sort the array first and then check for adjacent duplicates. Sorting typically takes O(n log n) time complexity (if using efficient algorithms like quicksort or mergesort), and then finding duplicates in the sorted array takes O(n) time complexity. So, the overall time complexity is O(n log n).

3. **Hash Table (unordered_set)**: Iterate through the array and insert each element into an unordered_set while checking if it already exists. If it does, then it's a duplicate. Inserting into an unordered_set has an average-case time complexity of O(1), so the overall time complexity is O(n).

4. **Bit Manipulation**: If the range of values in the array is within a certain range, you can use bit manipulation techniques to find duplicates efficiently. This approach usually has a time complexity of O(n).

Here's a summary of the time complexities for each approach:

* Brute Force: O(n^2)
* Sorting: O(n log n)
* Hash Table: O(n)
* Bit Manipulation: O(n)

In terms of space complexity:

* Brute Force: O(1)
* Sorting: O(1) if in-place sorting is used; otherwise, O(n)
* Hash Table: O(n) for storing the hash table
* Bit Manipulation: O(1)

Depending on factors like the size of the array, the range of values, and the resources available, you might choose one approach over the other. For small arrays or arrays with limited value ranges, the brute force approach or bit manipulation might be more efficient. However, for larger arrays or arrays with a wide range of values, hash tables or sorting might be preferable.

### 1. Algorithms & Data Structures (C++): Find() and search() operations on Array

In C++, the `std::find` function is used to search for an element in an array or any other container. Here's how you can use it:

```cpp
#include <iostream>
#include <algorithm> // for std::find
#include <vector>    // for std::vector

int main() {
    // Example array
    int arr[] = {1, 2, 3, 4, 5};
    int n = sizeof(arr) / sizeof(arr[0]);

    // Search for element 3 in the array
    int* result = std::find(arr, arr + n, 3);

    // Check if the element was found
    if (result != arr + n) {
        std::cout << "Element found at index: " << (result - arr) << std::endl;
    } else {
        std::cout << "Element not found" << std::endl;
    }

    return 0;
}
```

In this code:

* `std::find(arr, arr + n, value)` searches for the element `value` in the range `[arr, arr + n)`.
* It returns an iterator pointing to the first occurrence of `value` if found, otherwise, it returns the end iterator (`arr + n` in this case).
* You can then compare the result with `arr + n` to check if the element was found.

For searching in other data structures like vectors, the usage is similar. Here's an example with a `std::vector`:

```cpp
#include <iostream>
#include <algorithm> // for std::find
#include <vector>    // for std::vector

int main() {
    // Example vector
    std::vector<int> vec = {1, 2, 3, 4, 5};

    // Search for element 3 in the vector
    auto result = std::find(vec.begin(), vec.end(), 3);

    // Check if the element was found
    if (result != vec.end()) {
        std::cout << "Element found at index: " << (result - vec.begin()) << std::endl;
    } else {
        std::cout << "Element not found" << std::endl;
    }

    return 0;
}
```

The `std::search` function, on the other hand, is used to search for a sequence within another sequence. Here's how you can use it:

```cpp
#include <iostream>
#include <algorithm> // for std::search
#include <vector>    // for std::vector

int main() {
    // Example vector
    std::vector<int> haystack = {1, 2, 3, 4, 5, 6, 7, 8, 9};
    std::vector<int> needle = {4, 5, 6};

    // Search for the needle sequence in the haystack
    auto result = std::search(haystack.begin(), haystack.end(), needle.begin(), needle.end());

    // Check if the sequence was found
    if (result != haystack.end()) {
        std::cout << "Sequence found at index: " << (result - haystack.begin()) << std::endl;
    } else {
        std::cout << "Sequence not found" << std::endl;
    }

    return 0;
}
```

In this code:

* `std::search(haystack.begin(), haystack.end(), needle.begin(), needle.end())` searches for the sequence defined by the iterators `needle.begin()` and `needle.end()` within the range `[haystack.begin(), haystack.end())`.
* It returns an iterator pointing to the beginning of the found sequence if found, otherwise, it returns the end iterator (`haystack.end()` in this case).
* You can then compare the result with `haystack.end()` to check if the sequence was found.

### 1. Algorithms & Data Structures (C++): Finding a Pair of Elements with sum K

To find a pair of elements in an array that sum up to a given value \( K \), you can use a hash set to store the elements as you iterate through the array. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <unordered_set>
#include <vector>

std::pair<int, int> findPairWithSumK(const std::vector<int>& nums, int K) {
    std::unordered_set<int> complements;

    for (int num : nums) {
        int complement = K - num;
        if (complements.find(complement) != complements.end()) {
            // Found the pair
            return std::make_pair(num, complement);
        }
        complements.insert(num);
    }

    // No pair found
    return std::make_pair(-1, -1);
}

int main() {
    std::vector<int> nums = {1, 4, 6, 8, 9};
    int K = 10;
    
    std::pair<int, int> result = findPairWithSumK(nums, K);
    
    if (result.first != -1 && result.second != -1) {
        std::cout << "Pair found: " << result.first << ", " << result.second << std::endl;
    } else {
        std::cout << "No pair found with sum " << K << std::endl;
    }

    return 0;
}
```

This code defines a function `findPairWithSumK` that takes a vector of integers `nums` and an integer `K` as input and returns a pair of integers representing the pair of elements that sum up to `K`. If no such pair is found, it returns (-1, -1).

In the `main` function, you can change the values of `nums` and `K` to test different cases. This algorithm has a time complexity of O(n) since it iterates through the array only once.

### 1. Algorithms & Data Structures (C++): Finding a Pair of Elements with sum K in Sorted Array

Certainly! Finding a pair of elements with a sum K in a sorted array can be efficiently done using the two-pointer technique. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to find the pair with given sum K
bool findPairWithSumK(const vector<int>& arr, int K) {
    int left = 0; // Index of the leftmost element
    int right = arr.size() - 1; // Index of the rightmost element

    while (left < right) {
        int currentSum = arr[left] + arr[right];

        if (currentSum == K) {
            cout << "Pair found: " << arr[left] << " + " << arr[right] << " = " << K << endl;
            return true;
        } else if (currentSum < K) {
            left++; // Move the left pointer to increase the sum
        } else {
            right--; // Move the right pointer to decrease the sum
        }
    }

    // If no pair found
    cout << "No pair found with sum " << K << endl;
    return false;
}

int main() {
    vector<int> arr = {1, 3, 5, 7, 9, 11, 13};
    int K = 14;

    findPairWithSumK(arr, K);

    return 0;
}
```

This code defines a function `findPairWithSumK` that takes a sorted array `arr` and a target sum `K` as input and finds a pair of elements in the array whose sum equals `K`. It uses two pointers `left` and `right` which start at the beginning and end of the array respectively and moves them towards each other based on the current sum of elements pointed to by the pointers.

The time complexity of this solution is O(n) since in the worst case, both pointers traverse the entire array once.

### 1. Algorithms & Data Structures (C++): Finding Duplicates in a Sorted Array

To find duplicates in a sorted array efficiently, you can iterate through the array once and compare adjacent elements. Here's how you can implement this in C++:

```cpp
#include <iostream>
#include <vector>

std::vector<int> findDuplicates(const std::vector<int>& nums) {
    std::vector<int> duplicates;
    int n = nums.size();
    
    for (int i = 1; i < n; ++i) {
        if (nums[i] == nums[i - 1]) {
            duplicates.push_back(nums[i]);
        }
    }
    
    return duplicates;
}

int main() {
    // Example usage
    std::vector<int> nums = {1, 2, 2, 3, 4, 4, 4, 5, 5};
    std::vector<int> duplicates = findDuplicates(nums);
    
    if (duplicates.empty()) {
        std::cout << "No duplicates found.\n";
    } else {
        std::cout << "Duplicates found: ";
        for (int num : duplicates) {
            std::cout << num << " ";
        }
        std::cout << "\n";
    }
    
    return 0;
}
```

This code defines a function `findDuplicates` that takes a sorted vector of integers `nums` and returns a vector containing the duplicates. The main function demonstrates its usage by finding duplicates in a sorted array and printing them out.

### 1. Algorithms & Data Structures (C++): Finding Duplicates in a Unsorted Array

Certainly! One way to find duplicates in an unsorted array in C++ is by using a hash set or unordered set to keep track of elements that have been encountered before. Here's a sample implementation:

```cpp
#include <iostream>
#include <unordered_set>
#include <vector>

void findDuplicates(const std::vector<int>& arr) {
    std::unordered_set<int> seen;
    std::unordered_set<int> duplicates;

    for (int num : arr) {
        if (seen.find(num) != seen.end()) {
            // If the number is already in the seen set, it's a duplicate
            duplicates.insert(num);
        } else {
            // Otherwise, add it to the seen set
            seen.insert(num);
        }
    }

    // Print the duplicates
    if (duplicates.empty()) {
        std::cout << "No duplicates found." << std::endl;
    } else {
        std::cout << "Duplicates: ";
        for (int num : duplicates) {
            std::cout << num << " ";
        }
        std::cout << std::endl;
    }
}

int main() {
    std::vector<int> arr = {4, 2, 6, 8, 2, 7, 4, 1, 6, 2, 9};
    findDuplicates(arr);
    return 0;
}
```

This code defines a function `findDuplicates` that takes an unsorted array as input and uses an unordered set `seen` to keep track of elements encountered so far. If an element is encountered again, it's considered a duplicate and is added to another unordered set called `duplicates`. Finally, it prints out the duplicates found.

### 1. Algorithms & Data Structures (C++): Finding Duplicates in Array

Sure, finding duplicates in an array is a common problem in computer science and can be approached in several ways. Here's a simple algorithm in C++ to find duplicates in an array:

```cpp
#include <iostream>
#include <unordered_set>
#include <vector>

// Function to find duplicates in an array
void findDuplicates(const std::vector<int>& arr) {
    // Create a set to store visited elements
    std::unordered_set<int> visited;
    
    // Iterate through the array
    for (int num : arr) {
        // If the element is already in the set, it's a duplicate
        if (visited.find(num) != visited.end()) {
            std::cout << "Duplicate found: " << num << std::endl;
        } else {
            // Otherwise, add it to the set
            visited.insert(num);
        }
    }
}

int main() {
    std::vector<int> arr = {1, 2, 3, 4, 2, 7, 8, 8, 3};
    
    // Find duplicates in the array
    findDuplicates(arr);
    
    return 0;
}
```

This code snippet defines a function `findDuplicates` that takes a vector of integers as input and prints out any duplicates found within the array. It uses an `unordered_set` to store visited elements and quickly check for duplicates.

You can call the `findDuplicates` function with any array of integers to find duplicates. In the example provided in `main()`, it will output:

```bash
Duplicate found: 2
Duplicate found: 3
Duplicate found: 8
```

This indicates that the numbers 2, 3, and 8 are duplicates in the given array.

### 1. Algorithms & Data Structures (C++): Finding Duplicates in Sorted Array using Hashing

Certainly! Here's how you can find duplicates in a sorted array using hashing in C++:

```cpp
#include <iostream>
#include <unordered_set>
#include <vector>

void findDuplicates(const std::vector<int>& sortedArray) {
    std::unordered_set<int> hashSet;
    bool foundDuplicate = false;

    for (int num : sortedArray) {
        // If the number is already in the hash set, it's a duplicate
        if (hashSet.find(num) != hashSet.end()) {
            std::cout << "Duplicate found: " << num << std::endl;
            foundDuplicate = true;
        } else {
            hashSet.insert(num);
        }
    }

    if (!foundDuplicate) {
        std::cout << "No duplicates found" << std::endl;
    }
}

int main() {
    std::vector<int> sortedArray = {1, 2, 2, 3, 4, 4, 4, 5, 6, 7, 7};
    
    std::cout << "Finding duplicates in the sorted array:" << std::endl;
    findDuplicates(sortedArray);

    return 0;
}
```

In this code:

* We use an `unordered_set` from the C++ Standard Library to store unique elements encountered in the array.
* As we iterate through the sorted array, we check if the current element is already present in the hash set. If it is, we print it as a duplicate. Otherwise, we insert it into the hash set.
* Finally, if no duplicates are found, we print a message indicating that.

This approach has a time complexity of O(n) where n is the size of the sorted array, and a space complexity of O(n) as well.

### 1. Algorithms & Data Structures (C++): Finding Maximum and Minimum from an Array

Sure! Here's a simple implementation in C++ to find the maximum and minimum elements from an array using a linear scan:

```cpp
#include <iostream>
#include <climits>

using namespace std;

// Function to find maximum and minimum element in an array
void findMaxMin(int arr[], int size, int &max, int &min) {
    max = INT_MIN; // Initialize max to the smallest possible integer value
    min = INT_MAX; // Initialize min to the largest possible integer value

    for (int i = 0; i < size; ++i) {
        if (arr[i] > max) {
            max = arr[i];
        }
        if (arr[i] < min) {
            min = arr[i];
        }
    }
}

int main() {
    int arr[] = {5, 7, 2, 4, 9, 1, 6};
    int size = sizeof(arr) / sizeof(arr[0]);
    int max, min;

    findMaxMin(arr, size, max, min);

    cout << "Maximum element: " << max << endl;
    cout << "Minimum element: " << min << endl;

    return 0;
}
```

This code initializes variables `max` and `min` to the extremes of the integer range (`INT_MIN` and `INT_MAX`, respectively) and then iterates through the array, updating `max` and `min` as necessary. Finally, it prints out the found maximum and minimum elements.

### 1. Algorithms & Data Structures (C++): Finding Minimum Number of Merge operations on Arrays

To find the minimum number of merge operations required to merge \( k \) arrays into a single array, you can use a priority queue (min-heap) data structure. Here's a basic algorithm in C++:

```cpp
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

int minMergeOperations(vector<vector<int>>& arrays) {
    // Priority queue to store the smallest elements from each array
    priority_queue<int, vector<int>, greater<int>> minHeap;

    // Push the first element of each array into the minHeap
    for (auto& arr : arrays) {
        if (!arr.empty())
            minHeap.push(arr[0]);
    }

    int mergeCount = 0;

    // Merge the arrays
    while (!minHeap.empty()) {
        int smallest = minHeap.top();
        minHeap.pop();
        mergeCount++;

        // Find the array containing the next smallest element
        for (auto& arr : arrays) {
            if (!arr.empty() && arr[0] == smallest) {
                arr.erase(arr.begin()); // Remove the smallest element
                if (!arr.empty())
                    minHeap.push(arr[0]); // Push the next element of the array
                break;
            }
        }
    }

    return mergeCount - 1; // Total merges = arrays.size() - 1
}

int main() {
    vector<vector<int>> arrays = {{1, 3, 5}, {2, 4, 6}, {0, 7, 8}};
    cout << "Minimum number of merge operations: " << minMergeOperations(arrays) << endl;
    return 0;
}
```

This code snippet defines a function `minMergeOperations` that takes a vector of vectors `arrays` as input, where each inner vector represents a sorted array. The function calculates and returns the minimum number of merge operations required to merge all arrays into a single sorted array.

The approach is to use a min-heap to keep track of the smallest elements from all arrays. We start by pushing the first element of each array into the min-heap. Then, in each iteration, we pop the smallest element from the min-heap and increment the merge count. We then find the array containing the popped element and remove it from the array. If the array is not empty after removing the smallest element, we push the next element of the array into the min-heap. We continue this process until the min-heap becomes empty.

Finally, we return the merge count minus one because the total number of merges needed is one less than the number of arrays.

### 1. Algorithms & Data Structures (C++): Finding Missing Element in an Array Method 2

Method 2 for finding a missing element in an array in C++ can utilize bitwise XOR operation. Here's how it works:

```cpp
#include <iostream>
#include <vector>

int findMissingElement(const std::vector<int>& arr) {
    int n = arr.size() + 1;
    int xor_sum = 0;
    
    // XOR of all elements from 1 to n
    for (int i = 1; i <= n; ++i) {
        xor_sum ^= i;
    }
    
    // XOR of all elements in the array
    for (int num : arr) {
        xor_sum ^= num;
    }
    
    return xor_sum;
}

int main() {
    std::vector<int> arr = {1, 2, 4, 5, 6};
    int missing_element = findMissingElement(arr);
    std::cout << "Missing element is: " << missing_element << std::endl;
    return 0;
}
```

Explanation:

1. We know that the array contains numbers from 1 to n, but one element is missing.
2. We calculate the XOR of all numbers from 1 to n. This is done by XORing all the numbers from 1 to n in a loop.
3. Then, we calculate the XOR of all the elements in the array.
4. The missing element will be the XOR of the two XORs obtained in steps 2 and 3.
5. By the properties of XOR, the missing element will be left as the result.

This method has a time complexity of O(n) and a space complexity of O(1).

### 1. Algorithms & Data Structures (C++): Finding Multiple Missing Elements in an Array

To find multiple missing elements in an array using C++, you can utilize various approaches. One common method is to use a boolean array or a hash set to mark the presence of elements, then iterate through the original array to find the missing elements. Here's a basic example of how you can implement this:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to find and print multiple missing elements in an array
void findMissingElements(const vector<int>& arr) {
    int maxElement = *max_element(arr.begin(), arr.end());
    vector<bool> present(maxElement + 1, false);

    // Mark elements as present
    for (int num : arr) {
        present[num] = true;
    }

    // Find missing elements and print them
    cout << "Missing elements:";
    for (int i = 1; i <= maxElement; ++i) {
        if (!present[i]) {
            cout << " " << i;
        }
    }
    cout << endl;
}

int main() {
    vector<int> arr = {2, 5, 7, 10};
    findMissingElements(arr);

    return 0;
}
```

This code snippet defines a function `findMissingElements` that takes a vector of integers `arr` as input and prints the missing elements in the range `[1, max_element]`. You can customize the range based on your requirements.

This approach has a time complexity of O(n), where n is the number of elements in the input array. However, the space complexity is O(maxElement), where maxElement is the maximum element in the input array. If the maximum element is significantly larger than the number of elements, you might consider alternative approaches to optimize space usage.

### 1. Algorithms & Data Structures (C++): Finding Single Missing Element in an Array

Sure, finding a single missing element in an array can be approached in several ways. Here's a common method using bitwise XOR in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to find the missing element
int findMissingElement(const vector<int>& arr) {
    int n = arr.size();
    int xorSum = 0;

    // XOR of all elements in the array
    for (int i = 0; i < n; ++i) {
        xorSum ^= arr[i];
    }

    // XOR of all elements from 1 to n+1
    for (int i = 1; i <= n + 1; ++i) {
        xorSum ^= i;
    }

    return xorSum;
}

int main() {
    vector<int> arr = {1, 2, 4, 5, 6};
    int missingElement = findMissingElement(arr);
    cout << "The missing element is: " << missingElement << endl;

    return 0;
}
```

Explanation:

* We initialize `xorSum` to 0.
* We XOR all the elements of the array with `xorSum`. This will cancel out all the elements that appear twice, leaving only the missing element.
* We XOR `xorSum` with all elements from 1 to n+1 (where n is the size of the array). This will cancel out all the elements from 1 to n+1, leaving only the missing element.
* The result will be the missing element in the array.

This method has a time complexity of O(n) and a space complexity of O(1), which makes it efficient.

### 1. Algorithms & Data Structures (C++): First Index of Duplicate Numbers

To find the index of the first occurrence of a duplicate number in an array using C++, you can use a hash map to keep track of the indices of numbers as you iterate through the array. Here's a sample implementation:

```cpp
#include <iostream>
#include <unordered_map>
#include <vector>

int firstDuplicateIndex(const std::vector<int>& nums) {
    std::unordered_map<int, int> numIndices;

    for (int i = 0; i < nums.size(); ++i) {
        if (numIndices.find(nums[i]) != numIndices.end()) {
            // Found a duplicate
            return numIndices[nums[i]];
        } else {
            // Store the index of the number
            numIndices[nums[i]] = i;
        }
    }

    // No duplicates found
    return -1;
}

int main() {
    std::vector<int> nums = {2, 4, 3, 1, 3, 6, 2};
    int index = firstDuplicateIndex(nums);
    
    if (index != -1) {
        std::cout << "First duplicate found at index: " << index << std::endl;
    } else {
        std::cout << "No duplicates found." << std::endl;
    }
    
    return 0;
}
```

This code defines a function `firstDuplicateIndex` that takes a vector of integers as input and returns the index of the first occurrence of a duplicate number. The function iterates through the vector, storing each number along with its index in a hash map. If a number is encountered again during the iteration, its index is retrieved from the hash map and returned.

In the `main` function, you can test the `firstDuplicateIndex` function with a sample vector of integers. If a duplicate is found, it prints the index; otherwise, it indicates that no duplicates were found.

### 1. Algorithms & Data Structures (C++): Flip the array

Certainly! To flip an array in C++, you can simply swap elements from the beginning and end until you reach the middle of the array. Here's a function that does that:

```cpp
#include <iostream>
#include <vector>

void flipArray(std::vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n / 2; ++i) {
        // Swap elements from the beginning and end
        int temp = arr[i];
        arr[i] = arr[n - i - 1];
        arr[n - i - 1] = temp;
    }
}

int main() {
    // Example usage
    std::vector<int> arr = {1, 2, 3, 4, 5};
    
    std::cout << "Original Array: ";
    for (int num : arr) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
    
    flipArray(arr);
    
    std::cout << "Flipped Array: ";
    for (int num : arr) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
    
    return 0;
}
```

This code defines a function `flipArray` that takes a reference to a vector of integers and flips it in place. Then, in the `main` function, an example array is created, flipped, and printed before and after the flip.

### 1. Algorithms & Data Structures (C++): Flood Fill - Arrays

Certainly! Flood fill is a classic algorithm used to traverse and manipulate connected regions in a grid or an array. It's commonly used in image processing, maze-solving, and other graphical applications. The basic idea is to start from a given point in the grid and explore its neighbors, recursively applying some operation until a certain condition is met. Here's a C++ implementation of the flood fill algorithm:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Define the directions (up, down, left, right)
const int dx[] = {-1, 1, 0, 0};
const int dy[] = {0, 0, -1, 1};

// Function to perform flood fill
void floodFill(vector<vector<int>>& grid, int x, int y, int newColor, int oldColor) {
    // Boundary check
    if (x < 0 || x >= grid.size() || y < 0 || y >= grid[0].size() || grid[x][y] != oldColor)
        return;

    // Change the color of the current cell
    grid[x][y] = newColor;

    // Recursively flood fill adjacent cells
    for (int i = 0; i < 4; ++i) {
        int nx = x + dx[i];
        int ny = y + dy[i];
        floodFill(grid, nx, ny, newColor, oldColor);
    }
}

// Function to print the grid
void printGrid(const vector<vector<int>>& grid) {
    for (const auto& row : grid) {
        for (int cell : row) {
            cout << cell << " ";
        }
        cout << endl;
    }
}

int main() {
    vector<vector<int>> grid = {
        {1, 1, 1, 1, 1},
        {1, 1, 0, 0, 1},
        {1, 0, 1, 0, 1},
        {1, 1, 1, 1, 1}
    };

    cout << "Original Grid:" << endl;
    printGrid(grid);

    int x = 1, y = 2; // Starting point
    int newColor = 2; // New color to flood fill with
    int oldColor = grid[x][y]; // Old color of the starting point

    floodFill(grid, x, y, newColor, oldColor);

    cout << "\nGrid after flood fill:" << endl;
    printGrid(grid);

    return 0;
}
```

In this implementation:

* We define a 2D vector `grid` representing the array.
* `floodFill` function performs the flood fill algorithm recursively. It takes the grid, coordinates of the starting point `(x, y)`, the new color to fill, and the old color of the starting point as parameters.
* `printGrid` function simply prints the grid.
* In the `main` function, we define a sample grid, choose a starting point `(x, y)`, specify the new color, and call `floodFill` function with these parameters.
* Finally, we print the grid before and after the flood fill operation.

You can adjust the grid, starting point, and new color as needed to experiment with different scenarios.

### 1. Algorithms & Data Structures (C++): Good Array

A "Good Array" is a concept in computer science where you're given an array of integers, and the goal is to determine whether it's a "good" array or not based on certain criteria. The criteria for a "good" array can vary depending on the problem statement.

Here's an example of a problem related to determining whether an array is "good":

**Problem:** Given an array of integers, determine whether it's a "good" array or not. An array is considered "good" if the sum of all its elements is even.

**Solution (C++):**

```cpp
#include <iostream>
#include <vector>

bool isGoodArray(const std::vector<int>& arr) {
    int sum = 0;
    for (int num : arr) {
        sum += num;
    }
    return sum % 2 == 0;
}

int main() {
    std::vector<int> arr = {2, 4, 6, 8}; // Example array
    if (isGoodArray(arr)) {
        std::cout << "It's a good array." << std::endl;
    } else {
        std::cout << "It's not a good array." << std::endl;
    }
    return 0;
}
```

In this example, the function `isGoodArray` iterates through all elements of the array, calculates their sum, and then checks whether the sum is even or not. Based on this, it returns `true` if it's a good array and `false` otherwise.

This is a simple example, but the concept can be extended to more complex problems where the definition of a "good" array might involve more intricate conditions or operations on the array elements.

### 1. Algorithms & Data Structures (C++): K smallest Element

To find the K smallest elements in an array, you can use various algorithms. One commonly used approach is to use a min-heap data structure. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>

std::vector<int> kSmallestElements(const std::vector<int>& nums, int k) {
    std::priority_queue<int, std::vector<int>, std::greater<int>> minHeap;
    
    // Push first k elements into min-heap
    for (int i = 0; i < k; ++i) {
        minHeap.push(nums[i]);
    }

    // Push remaining elements into min-heap and pop the maximum element if heap size exceeds k
    for (int i = k; i < nums.size(); ++i) {
        if (nums[i] < minHeap.top()) {
            minHeap.pop();
            minHeap.push(nums[i]);
        }
    }

    // Copy the k smallest elements from min-heap into a vector
    std::vector<int> result;
    while (!minHeap.empty()) {
        result.push_back(minHeap.top());
        minHeap.pop();
    }

    return result;
}

int main() {
    std::vector<int> nums = {3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5};
    int k = 4;

    std::vector<int> smallestElements = kSmallestElements(nums, k);

    std::cout << "The " << k << " smallest elements are: ";
    for (int num : smallestElements) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

This code snippet demonstrates finding the K smallest elements in an array using a min-heap implemented with `std::priority_queue` in C++. In the `kSmallestElements` function, it iterates through the array once, maintaining a min-heap of size K. It pushes the first K elements into the heap. Then, for each subsequent element, if it's smaller than the maximum element in the heap, it replaces the maximum element with the current element. Finally, it extracts the elements from the min-heap, giving you the K smallest elements.

### 1. Algorithms & Data Structures (C++): K Sorted Array

A "k-sorted" array is an array in which each element is at most k positions away from its correct sorted position. This typically arises in scenarios where you have a large array that is partially sorted, for example, due to small random fluctuations or errors. Implementing an algorithm to sort such an array efficiently can be quite useful.

Here's a high-level approach to sort a k-sorted array efficiently:

1. **Use a Min Heap**: Create a min-heap of size k+1 and insert the first k+1 elements from the array into the heap.
2. **Extract Minimum & Insert**: Repeat the following steps until there are no elements left in the array:
   * Extract the minimum element from the heap. This will be the smallest element in the current window of size k+1.
   * Insert the next element from the array into the heap.
   * Append the extracted minimum to the sorted array.
3. **Handle Remaining Elements**: After the above loop, there might be elements left in the heap. Extract them one by one and append them to the sorted array.

Here's a simple implementation in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

vector<int> kSortedArray(vector<int>& arr, int k) {
    vector<int> sortedArr;
    priority_queue<int, vector<int>, greater<int>> minHeap;

    // Insert first k+1 elements into the heap
    for (int i = 0; i <= k && i < arr.size(); ++i) {
        minHeap.push(arr[i]);
    }

    // Process the remaining elements
    for (int i = k + 1; i < arr.size(); ++i) {
        sortedArr.push_back(minHeap.top());
        minHeap.pop();
        minHeap.push(arr[i]);
    }

    // Extract remaining elements from the heap
    while (!minHeap.empty()) {
        sortedArr.push_back(minHeap.top());
        minHeap.pop();
    }

    return sortedArr;
}

int main() {
    vector<int> arr = {6, 5, 3, 2, 8, 10, 9};
    int k = 3;

    vector<int> sortedArr = kSortedArray(arr, k);

    cout << "Sorted Array: ";
    for (int num : sortedArr) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}
```

This implementation has a time complexity of O(n log k), where n is the number of elements in the array. The space complexity is O(k) due to the size of the min-heap.

### 1. Algorithms & Data Structures (C++): Kadane's Algorithm

Kadane's Algorithm is a classic algorithm used to find the maximum subarray sum within a given array of integers. It's quite efficient with a time complexity of O(n), where n is the size of the array. Here's how it works in C++:

```cpp
#include <iostream>
#include <vector>
#include <climits>

using namespace std;

int kadane(vector<int>& nums) {
    int maxEndingHere = 0;
    int maxSoFar = INT_MIN;

    for (int i = 0; i < nums.size(); ++i) {
        maxEndingHere = max(maxEndingHere + nums[i], nums[i]);
        maxSoFar = max(maxSoFar, maxEndingHere);
    }

    return maxSoFar;
}

int main() {
    // Example usage:
    vector<int> nums = {-2, 1, -3, 4, -1, 2, 1, -5, 4};
    cout << "Maximum subarray sum: " << kadane(nums) << endl;
    return 0;
}
```

Explanation:

* `maxEndingHere` represents the maximum subarray sum ending at the current position.
* `maxSoFar` represents the maximum subarray sum seen so far.
* We iterate through the array, updating `maxEndingHere` at each step. If adding the current element to the previous subarray sum (`maxEndingHere + nums[i]`) increases the sum, we continue with the updated sum. Otherwise, we start a new subarray at the current element (`nums[i]`).
* At each step, we update `maxSoFar` with the maximum of `maxSoFar` and `maxEndingHere`.

The final `maxSoFar` will give us the maximum subarray sum.

### 1. Algorithms & Data Structures (C++): Kth Largest Element

To find the Kth largest element in an array, there are several approaches you can take. One common method is to use a priority queue (implemented as a max heap in C++).

Here's a basic implementation in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

int findKthLargest(vector<int>& nums, int k) {
    // Create a max heap
    priority_queue<int> maxHeap;

    // Push all elements of the array into the max heap
    for (int num : nums) {
        maxHeap.push(num);
    }

    // Pop k-1 elements from the heap
    for (int i = 0; i < k - 1; ++i) {
        maxHeap.pop();
    }

    // The top element of the heap is the kth largest element
    return maxHeap.top();
}

int main() {
    vector<int> nums = {3, 2, 1, 5, 6, 4};
    int k = 2; // Find the 2nd largest element

    int kthLargest = findKthLargest(nums, k);
    cout << "The " << k << "th largest element is: " << kthLargest << endl;

    return 0;
}
```

This code first creates a max heap from the given array. Then, it pops elements from the heap k-1 times, effectively getting rid of the k-1 largest elements, leaving the kth largest element at the top of the heap.

Remember to handle cases where k might be larger than the array size or negative numbers. Additionally, you can optimize this approach further using a min heap or the quickselect algorithm for better performance.

### 1. Algorithms & Data Structures (C++): Kth Largest Element In An Array

To find the \( k \)-th largest element in an array, you can use various algorithms. One of the most efficient approaches is using a max heap. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

int findKthLargest(vector<int>& nums, int k) {
    priority_queue<int, vector<int>, greater<int>> minHeap;

    for (int num : nums) {
        minHeap.push(num);
        if (minHeap.size() > k) {
            minHeap.pop(); // Ensure heap size remains k
        }
    }

    return minHeap.top(); // Top of heap will be kth largest element
}

int main() {
    vector<int> nums = {3, 2, 1, 5, 6, 4};
    int k = 2; // Find the 2nd largest element

    int result = findKthLargest(nums, k);
    cout << "The " << k << "-th largest element is: " << result << endl;

    return 0;
}
```

In this code:

1. We use a `priority_queue` as a min heap (`priority_queue<int, vector<int>, greater<int>>`), ensuring that the top element is always the smallest in the heap.
2. We iterate through the array, pushing elements into the min heap.
3. If the size of the heap exceeds \( k \), we pop the smallest element, ensuring the heap size remains \( k \).
4. Finally, the top element of the heap will be the \( k \)-th largest element in the array.

This approach has a time complexity of \( O(n \log k) \), where \( n \) is the size of the input array.

### 1. Algorithms & Data Structures (C++): Left and Right Rotate of the Elements on Array

Certainly! Rotating elements in an array left or right involves shifting the elements of the array in the desired direction. Here's how you can implement left and right rotation of elements in a C++ array:

```cpp
#include <iostream>

void leftRotate(int arr[], int n, int d) {
    // Create a temporary array to store the elements to be rotated
    int temp[d];
    
    // Copy the first d elements to the temporary array
    for (int i = 0; i < d; i++)
        temp[i] = arr[i];

    // Shift the remaining elements of the original array to the left
    for (int i = d; i < n; i++)
        arr[i - d] = arr[i];

    // Copy the elements from the temporary array to the end of the original array
    for (int i = 0; i < d; i++)
        arr[n - d + i] = temp[i];
}

void rightRotate(int arr[], int n, int d) {
    // Create a temporary array to store the elements to be rotated
    int temp[d];

    // Copy the last d elements to the temporary array
    for (int i = 0; i < d; i++)
        temp[i] = arr[n - d + i];

    // Shift the remaining elements of the original array to the right
    for (int i = n - 1; i >= d; i--)
        arr[i] = arr[i - d];

    // Copy the elements from the temporary array to the beginning of the original array
    for (int i = 0; i < d; i++)
        arr[i] = temp[i];
}

void printArray(int arr[], int n) {
    for (int i = 0; i < n; i++)
        std::cout << arr[i] << " ";
    std::cout << std::endl;
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int n = sizeof(arr) / sizeof(arr[0]);
    int d = 2; // Number of rotations

    std::cout << "Original array: ";
    printArray(arr, n);

    leftRotate(arr, n, d);
    std::cout << "Array after left rotation: ";
    printArray(arr, n);

    rightRotate(arr, n, d);
    std::cout << "Array after right rotation: ";
    printArray(arr, n);

    return 0;
}
```

This program defines two functions, `leftRotate` and `rightRotate`, which perform left and right rotation of elements in the array, respectively. The `main` function demonstrates how to use these functions by rotating an array of integers and printing the results.

### 1. Algorithms & Data Structures (C++): Max Consecutive Ones

To find the maximum number of consecutive ones in an array of 0s and 1s using C++, you can iterate through the array and keep track of the current consecutive ones count and the maximum consecutive ones count encountered so far. Here's a simple implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int findMaxConsecutiveOnes(vector<int>& nums) {
    int maxCount = 0;
    int count = 0;

    for (int num : nums) {
        if (num == 1) {
            count++;
            maxCount = max(maxCount, count);
        } else {
            count = 0;
        }
    }

    return maxCount;
}

int main() {
    vector<int> nums = {1, 1, 0, 1, 1, 1, 0, 1, 1, 1, 1};
    cout << "Maximum consecutive ones: " << findMaxConsecutiveOnes(nums) << endl;
    return 0;
}
```

This code defines a function `findMaxConsecutiveOnes` that takes a vector of integers as input and returns the maximum number of consecutive ones. In the `main` function, we create a sample array `nums`, call the function, and output the result.

This algorithm has a time complexity of O(n), where n is the length of the input array `nums`.

### 1. Algorithms & Data Structures (C++): Min Array Jumps

Sure, let's discuss an algorithm to find the minimum number of jumps required to reach the end of an array. This problem can be solved using dynamic programming.

Here's the basic idea:

1. Initialize an array `minJumps` of the same size as the input array, where `minJumps[i]` represents the minimum number of jumps required to reach the `i`-th position from the start.
2. Initialize `minJumps[0]` to 0, as it takes 0 jumps to reach the start position.
3. Iterate over each position `i` from 1 to the end of the array.
4. For each position `i`, iterate over all positions `j` from 0 to `i - 1`.
5. For each `j`, if it is reachable from `j` and `j` itself is reachable from the start, update `minJumps[i]` to the minimum of its current value and `minJumps[j] + 1`.
6. Finally, return `minJumps` at the last position, which represents the minimum number of jumps required to reach the end.

Here's a sample implementation in C++:

```cpp
#include <iostream>
#include <vector>
#include <climits>
using namespace std;

int minArrayJumps(vector<int>& nums) {
    int n = nums.size();
    vector<int> minJumps(n, INT_MAX);
    minJumps[0] = 0;

    for (int i = 1; i < n; ++i) {
        for (int j = 0; j < i; ++j) {
            if (j + nums[j] >= i && minJumps[j] != INT_MAX) {
                minJumps[i] = min(minJumps[i], minJumps[j] + 1);
            }
        }
    }

    return minJumps[n - 1];
}

int main() {
    vector<int> nums = {2, 3, 1, 1, 4};
    cout << "Minimum number of jumps: " << minArrayJumps(nums) << endl;
    return 0;
}
```

This implementation should output `Minimum number of jumps: 2` for the given input array `{2, 3, 1, 1, 4}`.

### 1. Algorithms & Data Structures (C++): MinHeap: Sink DownHeap: Kth Smallest Element in an Array

Sure, let's delve into implementing a MinHeap in C++ and then use it to find the Kth smallest element in an array.

First, let's define the MinHeap class:

```cpp
#include <vector>

class MinHeap {
private:
    std::vector<int> heap;

    void sink(int index) {
        int left = 2 * index + 1;
        int right = 2 * index + 2;
        int smallest = index;

        if (left < heap.size() && heap[left] < heap[smallest])
            smallest = left;

        if (right < heap.size() && heap[right] < heap[smallest])
            smallest = right;

        if (smallest != index) {
            std::swap(heap[index], heap[smallest]);
            sink(smallest);
        }
    }

public:
    MinHeap() {}

    void insert(int val) {
        heap.push_back(val);
        int index = heap.size() - 1;
        int parent = (index - 1) / 2;

        while (index > 0 && heap[index] < heap[parent]) {
            std::swap(heap[index], heap[parent]);
            index = parent;
            parent = (index - 1) / 2;
        }
    }

    int extractMin() {
        if (heap.empty())
            throw std::out_of_range("Heap is empty");

        int min = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        sink(0);

        return min;
    }

    int size() const {
        return heap.size();
    }
};
```

Now, let's implement a function to find the Kth smallest element in an array using this MinHeap:

```cpp
#include <iostream>
#include <vector>
#include <stdexcept>

int kthSmallestElement(const std::vector<int>& nums, int k) {
    if (k > nums.size() || k <= 0)
        throw std::invalid_argument("Invalid value of k");

    MinHeap minHeap;

    for (int num : nums) {
        minHeap.insert(num);
        if (minHeap.size() > k)
            minHeap.extractMin();
    }

    return minHeap.extractMin();
}

int main() {
    std::vector<int> nums = {7, 10, 4, 3, 20, 15};
    int k = 3;
    
    try {
        int kth_smallest = kthSmallestElement(nums, k);
        std::cout << "The " << k << "th smallest element is: " << kth_smallest << std::endl;
    } catch (const std::exception& e) {
        std::cerr << "Error: " << e.what() << std::endl;
    }

    return 0;
}
```

This implementation finds the Kth smallest element in an array using a MinHeap. The time complexity of this approach is O(nlogk), where n is the size of the input array and k is the value of k.

### 1. Algorithms & Data Structures (C++): Minimum in rotated sorted array

Finding the minimum element in a rotated sorted array is a classic problem in computer science. One efficient approach to solve this problem is using a binary search algorithm. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <vector>

int findMin(const std::vector<int>& nums) {
    int left = 0;
    int right = nums.size() - 1;

    // If the array is not rotated, the first element is the minimum
    if (nums[left] < nums[right])
        return nums[left];

    while (left < right) {
        int mid = left + (right - left) / 2;

        // If the mid element is greater than the last element, the minimum is in the right half
        if (nums[mid] > nums[right]) {
            left = mid + 1;
        }
        // If the mid element is less than or equal to the last element, the minimum is in the left half
        else {
            right = mid;
        }
    }
    // At the end of the loop, 'left' will point to the minimum element
    return nums[left];
}

int main() {
    std::vector<int> nums = {4, 5, 6, 7, 0, 1, 2};
    std::cout << "Minimum element: " << findMin(nums) << std::endl;
    return 0;
}
```

In this code:

* We initialize two pointers, `left` and `right`, which represent the start and end of the array, respectively.
* We check if the array is not rotated by comparing the first and last elements. If not rotated, the first element is the minimum.
* If the array is rotated, we perform binary search:
  * We calculate the middle index.
  * If the middle element is greater than the last element, the minimum element must be in the right half, so we update `left` to `mid + 1`.
  * Otherwise, the minimum element must be in the left half, so we update `right` to `mid`.
* We repeat this process until `left` and `right` converge, and then return the element pointed to by `left`, which is the minimum element.

### 1. Algorithms & Data Structures (C++): Minimum in rotated sorted array: Complexity analysis

To analyze the complexity of finding the minimum element in a rotated sorted array using C++, let's first discuss the algorithm. The problem can be solved using a modified binary search approach.

Here's a brief outline of the algorithm:

1. We perform a binary search on the rotated sorted array.
2. At each step, we compare the middle element (let's call it mid) with the first element of the array.
3. If mid is greater than the first element, then the minimum element must be in the right half of the array. Otherwise, it must be in the left half.
4. We adjust the search space accordingly and continue the binary search.
5. We repeat this process until we find the minimum element.

Now, let's analyze the time complexity of this algorithm:

* **Time Complexity:** O(log n)

In each step of the binary search, we reduce the search space by half. Therefore, the time complexity of the binary search is O(log n), where n is the number of elements in the array.

* **Space Complexity:** O(1)

The space complexity is constant because we are not using any extra space that scales with the input size. We are only using a few variables for indices and comparisons.

In summary, the time complexity of finding the minimum element in a rotated sorted array using the binary search approach is O(log n), where n is the number of elements in the array. The space complexity is O(1), indicating that the algorithm uses constant space regardless of the input size.

### 1. Algorithms & Data Structures (C++): Mountain

Creating a mountain algorithmically can be an interesting exercise. You can represent a mountain as a 2D grid with varying heights. Here's a simple approach in C++ using a 2D vector:

```cpp
#include <iostream>
#include <vector>
#include <cstdlib>
#include <ctime>

using namespace std;

void generateMountain(vector<vector<int>>& mountain, int width, int height, int peakHeight) {
    // Set random seed
    srand(time(NULL));

    // Initialize the mountain with zeros
    mountain.resize(height, vector<int>(width, 0));

    // Set peak position
    int peakPosition = rand() % width;
    mountain[0][peakPosition] = peakHeight;

    // Generate slopes
    for (int i = 1; i < height; ++i) {
        for (int j = 0; j < width; ++j) {
            int left = max(j - 1, 0);
            int right = min(j + 1, width - 1);
            int slope = (mountain[i - 1][left] + mountain[i - 1][j] + mountain[i - 1][right]) / 3;
            mountain[i][j] = max(0, slope + (rand() % 3 - 1)); // Add randomness to slope
        }
    }
}

void printMountain(const vector<vector<int>>& mountain) {
    for (const auto& row : mountain) {
        for (int height : row) {
            if (height == 0)
                cout << " ";
            else if (height <= 3)
                cout << ".";
            else if (height <= 6)
                cout << "^";
            else if (height <= 9)
                cout << "!";
            else
                cout << "#";
        }
        cout << endl;
    }
}

int main() {
    int width = 20;
    int height = 10;
    int peakHeight = 10;

    vector<vector<int>> mountain;
    generateMountain(mountain, width, height, peakHeight);
    printMountain(mountain);

    return 0;
}
```

This code generates a 2D mountain represented by a matrix of heights. The `generateMountain` function creates the mountain, and `printMountain` function prints it out. The mountain is generated using a simple random slope algorithm, where each point in the grid is influenced by its neighboring points in the previous row.

### 1. Algorithms & Data Structures (C++): Move Zeroes

Moving zeroes to the end of an array is a common problem in coding interviews and algorithmic practice. The task is to rearrange the elements of the array so that all zeroes appear at the end, while maintaining the relative order of non-zero elements. Here's a C++ implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void moveZeroes(vector<int>& nums) {
    int n = nums.size();
    int zeroIndex = 0; // Index to place the next non-zero element

    // Traverse the array
    for (int i = 0; i < n; i++) {
        if (nums[i] != 0) {
            // If the current element is non-zero, move it to the position of zeroIndex
            nums[zeroIndex] = nums[i];
            // Increment zeroIndex to prepare for the next non-zero element
            zeroIndex++;
        }
    }

    // After moving non-zero elements, fill the rest of the array with zeroes
    for (int i = zeroIndex; i < n; i++) {
        nums[i] = 0;
    }
}

int main() {
    vector<int> nums = {0, 1, 0, 3, 12};
    
    cout << "Original Array: ";
    for (int num : nums) {
        cout << num << " ";
    }
    cout << endl;

    moveZeroes(nums);

    cout << "Array after moving zeroes: ";
    for (int num : nums) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}
```

This code defines a function `moveZeroes` that takes a reference to a vector of integers `nums` and rearranges its elements as required. The `main` function demonstrates the usage of this function with a sample array.

### 1. Algorithms & Data Structures (C++): Move Zeroes - Array

Sure, the "Move Zeroes" problem is a classic algorithmic problem. The task is to move all the zeroes in an array to the end without changing the order of the non-zero elements. Here's a simple approach to solve this problem in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void moveZeroes(vector<int>& nums) {
    int nonZeroIndex = 0;
    int size = nums.size();

    // Move all non-zero elements to the front
    for (int i = 0; i < size; i++) {
        if (nums[i] != 0) {
            nums[nonZeroIndex++] = nums[i];
        }
    }

    // Fill the remaining positions with zeroes
    for (int i = nonZeroIndex; i < size; i++) {
        nums[i] = 0;
    }
}

int main() {
    vector<int> nums = {0, 1, 0, 3, 12};

    cout << "Original Array: ";
    for (int num : nums) {
        cout << num << " ";
    }
    cout << endl;

    moveZeroes(nums);

    cout << "Array After Moving Zeroes: ";
    for (int num : nums) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}
```

This code snippet defines a function `moveZeroes` that takes a reference to a vector of integers `nums` as input and moves all the zeroes to the end of the array while maintaining the order of non-zero elements.

The function iterates through the array, keeping track of the index where the next non-zero element should be placed. After all non-zero elements are moved to the front, the remaining positions in the array are filled with zeroes.

The `main` function demonstrates the usage of the `moveZeroes` function with a sample input array.

### 1. Algorithms & Data Structures (C++): Product Of Array Except Self

To implement the "Product of Array Except Self" algorithm in C++, you can use a simple approach that utilizes two passes through the array. In the first pass, you calculate the products of all elements to the left of each element, and in the second pass, you calculate the products of all elements to the right of each element. Finally, you multiply these two products to get the result.

Here's a sample implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

vector<int> productExceptSelf(vector<int>& nums) {
    int n = nums.size();
    vector<int> output(n, 1); // Initialize the output vector with all elements set to 1

    // Calculate the product of all elements to the left of each element
    int leftProduct = 1;
    for (int i = 0; i < n; ++i) {
        output[i] *= leftProduct;
        leftProduct *= nums[i];
    }

    // Calculate the product of all elements to the right of each element and multiply with the previous product
    int rightProduct = 1;
    for (int i = n - 1; i >= 0; --i) {
        output[i] *= rightProduct;
        rightProduct *= nums[i];
    }

    return output;
}

int main() {
    vector<int> nums = {1, 2, 3, 4};
    vector<int> result = productExceptSelf(nums);
    
    cout << "Result: ";
    for (int num : result) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}
```

This implementation has a time complexity of O(n) and a space complexity of O(n), where n is the number of elements in the input array.

### 1. Algorithms & Data Structures (C++): Product Of Array Except Self - Arrays

Sure! The "Product of Array Except Self" problem is a classic algorithmic problem where you're given an array of integers, and you need to return a new array such that each element at index `i` of the new array is the product of all the numbers in the original array except the one at `i`.

Here's how you can solve this problem in C++:

```cpp
#include <vector>

std::vector<int> productExceptSelf(std::vector<int>& nums) {
    int n = nums.size();
    std::vector<int> result(n, 1); // Initialize result array with 1s
    int left = 1, right = 1;

    // Calculate products of elements to the left of i
    for (int i = 0; i < n; i++) {
        result[i] *= left;
        left *= nums[i];
    }

    // Calculate products of elements to the right of i
    for (int i = n - 1; i >= 0; i--) {
        result[i] *= right;
        right *= nums[i];
    }

    return result;
}
```

Here's a brief explanation of the solution:

* We initialize an array `result` with all elements set to 1.
* We traverse the array from left to right, multiplying the elements encountered so far to get the product of all elements to the left of each element.
* We traverse the array from right to left, multiplying the elements encountered so far to get the product of all elements to the right of each element.
* Finally, each element of the `result` array contains the product of all elements of the original array except the one at that index.

You can use this function by passing your array of integers as an argument, and it will return the product of array except self.

### 1. Algorithms & Data Structures (C++): Product of array except self: Complexity analysis

The problem of finding the product of array except self can be solved using various approaches, but a common one involves using two extra arrays to store the product of elements to the left and right of each element in the input array. Let's analyze the time and space complexity of this approach:

#### Time Complexity

1. **Forward Pass to Calculate Left Product Array:** In this pass, we iterate through the array once and calculate the product of all elements to the left of each element. The time complexity of this pass is O(n), where n is the size of the input array.
2. **Backward Pass to Calculate Right Product Array:** Similarly, in this pass, we iterate through the array once again, calculating the product of all elements to the right of each element. The time complexity of this pass is also O(n).
3. **Combining Left and Right Products:** We combine the left and right product arrays to obtain the final result. This step involves iterating through the array once more, which contributes O(n) to the time complexity.

Overall, the time complexity of this approach is O(n), where n is the size of the input array.

#### Space Complexity

1. **Left Product Array:** We need an additional array to store the product of all elements to the left of each element. The space complexity for this array is O(n).
2. **Right Product Array:** Similarly, we need another array to store the product of all elements to the right of each element. The space complexity for this array is also O(n).
3. **Output Array:** If the output array is considered in the space complexity, it will contribute O(n) space.
4. **Total Space Complexity:** Considering all the arrays, the total space complexity is O(n).

#### Summary

* Time Complexity: O(n)
* Space Complexity: O(n)

This approach provides a linear time solution to the problem, which is quite efficient for most practical purposes.

### 1. Algorithms & Data Structures (C++): Product Of Arrays Except Self - Arrays

The "Product of Arrays Except Self" problem is a classic algorithmic problem where you're given an array of integers, and you need to return another array where each element at index `i` contains the product of all elements in the original array except the one at index `i`. Here's a C++ implementation:

```cpp
#include <vector>

std::vector<int> productExceptSelf(const std::vector<int>& nums) {
    int n = nums.size();
    std::vector<int> result(n, 1);
    
    int leftProduct = 1;
    for (int i = 0; i < n; ++i) {
        result[i] *= leftProduct;
        leftProduct *= nums[i];
    }
    
    int rightProduct = 1;
    for (int i = n - 1; i >= 0; --i) {
        result[i] *= rightProduct;
        rightProduct *= nums[i];
    }
    
    return result;
}
```

Explanation:

1. We initialize a result vector with the same size as the input array, filled with 1's initially.

2. We traverse the array from left to right, updating the result vector such that each element at index `i` contains the product of all elements to the left of `i`.

3. We traverse the array from right to left, updating the result vector such that each element at index `i` now contains the product of all elements to the left and right of `i`.

4. Finally, we return the result vector, which contains the product of arrays except self.

This algorithm runs in O(n) time complexity and O(1) space complexity (excluding the output array).

### 1. Algorithms & Data Structures (C++): Print All Sub-Arrays with zero sum

To print all sub-arrays with zero sum in C++, you can use a hashmap to keep track of the running sum and its corresponding indices. Whenever you encounter a sum that you've seen before, it indicates that the sub-array between the current index and the previous index has a sum of zero.

Here's a C++ implementation:

```cpp
#include <iostream>
#include <unordered_map>
#include <vector>

using namespace std;

void printAllSubArraysZeroSum(vector<int>& arr) {
    unordered_map<int, vector<int>> sumMap;
    int sum = 0;

    for (int i = 0; i < arr.size(); ++i) {
        sum += arr[i];

        // If sum is zero, print from beginning of array till current index
        if (sum == 0) {
            cout << "Sub-array from 0 to " << i << endl;
        }

        // If sum is already present in hash map, it indicates sub-array with zero sum
        if (sumMap.find(sum) != sumMap.end()) {
            vector<int> indices = sumMap[sum];
            for (auto index : indices) {
                cout << "Sub-array from " << index + 1 << " to " << i << endl;
            }
        }

        // Add current index to the sum's vector
        sumMap[sum].push_back(i);
    }
}

int main() {
    vector<int> arr = {4, 2, -3, 1, 6};
    cout << "Sub-arrays with zero sum are:" << endl;
    printAllSubArraysZeroSum(arr);
    return 0;
}
```

This program will print all sub-arrays with zero sum for the given array `{4, 2, -3, 1, 6}`. You can replace this array with any other array to test different inputs.

### 1. Algorithms & Data Structures (C++): Problem DIVSUB

The DIVSUB problem involves finding a non-empty contiguous subsequence of an array whose sum is divisible by a given number \( k \). Here's a way to solve it in C++:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>

using namespace std;

pair<int, int> findSubsequence(vector<int>& arr, int k) {
    unordered_map<int, int> modIndex; // Store the index of the first occurrence of each modulo
    int sum = 0;
    modIndex[0] = -1; // Required for handling the case when the whole array is divisible by k
    for (int i = 0; i < arr.size(); ++i) {
        sum = (sum + arr[i]) % k;
        if (modIndex.find(sum) != modIndex.end()) {
            return {modIndex[sum] + 1, i}; // Found a subsequence
        }
        modIndex[sum] = i;
    }
    return {-1, -1}; // No such subsequence found
}

int main() {
    int n, k;
    cin >> n >> k;
    vector<int> arr(n);
    for (int i = 0; i < n; ++i) {
        cin >> arr[i];
    }

    pair<int, int> result = findSubsequence(arr, k);
    if (result.first == -1) {
        cout << "-1\n";
    } else {
        cout << result.first + 1 << " " << result.second + 1 << endl;
    }

    return 0;
}
```

Explanation:

* We use an unordered map to store the index of the first occurrence of each modulo of the cumulative sum of the array elements.
* If at any point, the same modulo occurs again, it means that the subsequence between the two indices has a sum divisible by \( k \).
* We store the indices in the unordered map to find the length of the subsequence.
* We return the indices of the subsequence as a pair.
* If no such subsequence is found, we return {-1, -1}.

This solution has a time complexity of \( O(n) \) where \( n \) is the size of the array.

### 1. Algorithms & Data Structures (C++): Problem on Row Major Order Representation of an Array

Sure, let's dive into a problem related to representing a two-dimensional array in row-major order, which is a common concept in computer science.

Problem:
Given a two-dimensional array `arr` of size `m x n`, where `m` represents the number of rows and `n` represents the number of columns, implement two functions:

1. `toRowMajorOrder`: Convert the two-dimensional array `arr` into its row-major order representation.
2. `fromRowMajorOrder`: Convert a row-major order representation of an array back into a two-dimensional array.

You should implement these functions in C++.

Here's a possible implementation:

```cpp
#include <iostream>
#include <vector>

// Function to convert a 2D array into row-major order representation
std::vector<int> toRowMajorOrder(const std::vector<std::vector<int>>& arr) {
    std::vector<int> rowMajor;
    int rows = arr.size();
    int cols = arr[0].size();

    for (int i = 0; i < rows; ++i) {
        for (int j = 0; j < cols; ++j) {
            rowMajor.push_back(arr[i][j]);
        }
    }

    return rowMajor;
}

// Function to convert row-major order representation back into a 2D array
std::vector<std::vector<int>> fromRowMajorOrder(const std::vector<int>& rowMajor, int rows, int cols) {
    std::vector<std::vector<int>> arr(rows, std::vector<int>(cols, 0));
    int index = 0;

    for (int i = 0; i < rows; ++i) {
        for (int j = 0; j < cols; ++j) {
            arr[i][j] = rowMajor[index++];
        }
    }

    return arr;
}

int main() {
    // Example usage
    std::vector<std::vector<int>> arr = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};

    // Convert to row-major order
    std::vector<int> rowMajor = toRowMajorOrder(arr);

    // Print row-major order
    std::cout << "Row-major order representation: ";
    for (int elem : rowMajor) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    // Convert back to 2D array
    std::vector<std::vector<int>> newArr = fromRowMajorOrder(rowMajor, arr.size(), arr[0].size());

    // Print the original 2D array
    std::cout << "Original array:\n";
    for (const auto& row : newArr) {
        for (int elem : row) {
            std::cout << elem << " ";
        }
        std::cout << std::endl;
    }

    return 0;
}
```

This implementation assumes that the input array `arr` is rectangular (i.e., all rows have the same number of columns). The `toRowMajorOrder` function iterates through each element of the input array and appends them to the `rowMajor` vector. The `fromRowMajorOrder` function creates a new 2D array and fills it with elements from the `rowMajor` vector.

You can test this code with different input arrays to verify its correctness.

### 1. Algorithms & Data Structures (C++): Reversing using Sliding Pointers

In C++, reversing an array or a sequence using sliding pointers is a common technique. The idea is to use two pointers, typically starting from the two ends of the array, and swap elements iteratively until they meet in the middle. Here's a simple example of how you can implement this algorithm:

```cpp
#include <iostream>

void reverseArray(int arr[], int size) {
    // Initialize two pointers, one pointing to the beginning and
    // the other pointing to the end of the array
    int start = 0;
    int end = size - 1;

    // Swap elements until the pointers meet in the middle
    while (start < end) {
        // Swap arr[start] and arr[end]
        int temp = arr[start];
        arr[start] = arr[end];
        arr[end] = temp;

        // Move the pointers towards the middle
        start++;
        end--;
    }
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int size = sizeof(arr) / sizeof(arr[0]);

    std::cout << "Original array: ";
    for (int i = 0; i < size; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    // Reverse the array
    reverseArray(arr, size);

    std::cout << "Reversed array: ";
    for (int i = 0; i < size; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this code:

* The `reverseArray` function takes an integer array `arr` and its size `size` as parameters.
* Two pointers `start` and `end` are initialized at the beginning and end of the array, respectively.
* The function iterates over the array, swapping elements pointed to by `start` and `end` until `start` becomes greater than or equal to `end`.
* The `main` function demonstrates how to use the `reverseArray` function to reverse an array and prints the original and reversed arrays.

This technique is efficient, as it only requires a single pass through the array, resulting in a time complexity of O(n/2) or simply O(n), where n is the number of elements in the array.

### 1. Algorithms & Data Structures (C++): Rotate Array

Rotating an array in C++ can be done using a few different approaches, each with its own advantages and trade-offs. Here's one common way to rotate an array:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to reverse the elements of an array
void reverse(vector<int>& arr, int start, int end) {
    while (start < end) {
        swap(arr[start], arr[end]);
        start++;
        end--;
    }
}

// Function to rotate an array to the right by 'k' steps
void rotateArray(vector<int>& arr, int k) {
    int n = arr.size();
    
    // To handle the case when k is greater than n
    k = k % n;
    
    // If k is 0 or multiple of n, no rotation is needed
    if (k == 0 || n == 0) return;
    
    // Reverse the first n-k elements
    reverse(arr, 0, n - k - 1);
    
    // Reverse the remaining k elements
    reverse(arr, n - k, n - 1);
    
    // Reverse the entire array
    reverse(arr, 0, n - 1);
}

int main() {
    vector<int> arr = {1, 2, 3, 4, 5};
    int k = 2;
    
    cout << "Original array: ";
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;
    
    rotateArray(arr, k);
    
    cout << "Array rotated by " << k << " steps to the right: ";
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;
    
    return 0;
}
```

This code rotates an array to the right by a given number of steps `k`. It first reverses the first `n-k` elements, then reverses the next `k` elements, and finally reverses the entire array. This results in the array being rotated to the right by `k` steps.

You can adjust the value of `k` to rotate the array by a different number of steps.

### 1. Algorithms & Data Structures (C++): Search In A Rotated Sorted Array

Searching in a rotated sorted array can be a bit tricky, but it can be efficiently solved using a modified binary search algorithm. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int searchInRotatedArray(const vector<int>& nums, int target) {
    int left = 0;
    int right = nums.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (nums[mid] == target) {
            return mid;
        }

        // If left half is sorted
        if (nums[left] <= nums[mid]) {
            // If target lies in the left half
            if (nums[left] <= target && target < nums[mid]) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        // If right half is sorted
        else {
            // If target lies in the right half
            if (nums[mid] < target && target <= nums[right]) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
    }

    return -1; // Target not found
}

int main() {
    vector<int> nums = {4, 5, 6, 7, 0, 1, 2};
    int target = 0;
    int index = searchInRotatedArray(nums, target);
    if (index != -1) {
        cout << "Target found at index: " << index << endl;
    } else {
        cout << "Target not found" << endl;
    }
    return 0;
}
```

This algorithm maintains the binary search property while adjusting for the rotation. By checking whether the left or right half is sorted, it decides which half to discard in each iteration. This approach maintains a time complexity of O(log n) for the search.

### 1. Algorithms & Data Structures (C++): Search Insert Position

Sure, here's an implementation of the "Search Insert Position" problem in C++. This problem asks to find the index of a target element in a sorted array, or if the target is not found, to return the index where it would be inserted in order to maintain sorted order.

```cpp
#include <iostream>
#include <vector>

using namespace std;

int searchInsert(vector<int>& nums, int target) {
    int left = 0, right = nums.size() - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target)
            return mid;
        else if (nums[mid] < target)
            left = mid + 1;
        else
            right = mid - 1;
    }
    return left;
}

int main() {
    vector<int> nums = {1, 3, 5, 6};
    int target = 5;
    int result = searchInsert(nums, target);
    cout << "Index where " << target << " should be inserted: " << result << endl;
    return 0;
}
```

This implementation uses binary search to find the target element or the position where it should be inserted. If the target is found, the index of the target is returned. Otherwise, when the loop ends, the `left` pointer points to the position where the target should be inserted to maintain the sorted order, so `left` is returned.

### 1. Algorithms & Data Structures (C++): Search Insert Position - Binary Search

Sure! The search insert position problem is a classic problem that can be solved efficiently using binary search. Here's a C++ implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int searchInsert(vector<int>& nums, int target) {
    int low = 0, high = nums.size() - 1;
    
    while (low <= high) {
        int mid = low + (high - low) / 2;
        
        if (nums[mid] == target)
            return mid;
        else if (nums[mid] < target)
            low = mid + 1;
        else
            high = mid - 1;
    }
    
    return low; // Target not found, return the insertion position
}

int main() {
    vector<int> nums = {1, 3, 5, 6};
    int target = 5;
    
    int position = searchInsert(nums, target);
    
    cout << "The position to insert " << target << " is: " << position << endl;
    
    return 0;
}
```

In this code:

* We define a function `searchInsert` that takes a sorted vector `nums` and a target value `target`.
* We initialize `low` to 0 and `high` to the last index of the vector.
* In each iteration of the while loop, we calculate the middle index `mid`.
* If the element at `mid` is equal to the target, we return `mid`.
* If the element at `mid` is less than the target, we update `low` to `mid + 1`.
* If the element at `mid` is greater than the target, we update `high` to `mid - 1`.
* If we exit the loop, it means the target is not found in the array, so we return `low`, which represents the insertion position of the target.

In the `main` function, we create a sample vector `nums` and a target value `target`, then we call the `searchInsert` function and print the result.

### 1. Algorithms & Data Structures (C++): Search Insert Position - Sorting

Certainly! The "Search Insert Position" problem is a classic problem in computer science, often asked in interviews. Here's the problem statement:

Given a sorted array and a target value, return the index where the target would be if it were inserted in order. If the target is already present in the array, return the index of the target.

Here's a C++ implementation of the solution using binary search:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int searchInsert(vector<int>& nums, int target) {
    int low = 0, high = nums.size() - 1;
    
    while (low <= high) {
        int mid = low + (high - low) / 2;
        
        if (nums[mid] == target) {
            return mid;
        } else if (nums[mid] < target) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }
    
    return low;
}

int main() {
    vector<int> nums = {1, 3, 5, 6};
    int target = 5;
    cout << "Index to insert " << target << " is: " << searchInsert(nums, target) << endl;
    
    target = 2;
    cout << "Index to insert " << target << " is: " << searchInsert(nums, target) << endl;
    
    target = 7;
    cout << "Index to insert " << target << " is: " << searchInsert(nums, target) << endl;
    
    target = 0;
    cout << "Index to insert " << target << " is: " << searchInsert(nums, target) << endl;
    
    return 0;
}
```

In this code, `searchInsert` function takes a sorted array `nums` and a target value `target`. It performs a binary search to find the target value or its insertion position. If the target is found, it returns the index. Otherwise, it returns the index where the target should be inserted.

You can run this code snippet to see how it works with different test cases.

### 1. Algorithms & Data Structures (C++): Sort Subsequences

Sorting subsequences in C++ involves identifying subsequences within a given sequence and sorting them separately. Here's a basic approach to achieve this:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

// Function to sort a subsequence within a range [start, end]
void sortSubsequence(std::vector<int>& arr, int start, int end) {
    std::sort(arr.begin() + start, arr.begin() + end + 1);
}

// Function to sort all subsequences of length k in the array
void sortAllSubsequences(std::vector<int>& arr, int k) {
    int n = arr.size();
    for (int i = 0; i <= n - k; i += k) {
        sortSubsequence(arr, i, i + k - 1);
    }
}

int main() {
    std::vector<int> arr = {3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5};
    int k = 3; // Length of subsequences to sort
    
    std::cout << "Original Array: ";
    for (int num : arr) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    sortAllSubsequences(arr, k);

    std::cout << "Array with sorted subsequences of length " << k << ": ";
    for (int num : arr) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this code:

1. `sortSubsequence` function sorts a subsequence within the range `[start, end]` of the array.
2. `sortAllSubsequences` function iterates through the array and sorts all subsequences of length `k`.
3. In the `main` function, an example array `arr` is defined, and the length of subsequences to sort (`k`) is specified.
4. The original array is printed, then all subsequences of length `k` are sorted, and the sorted array is printed.

You can modify the array `arr` and the value of `k` according to your requirements. This code assumes that the length of the array is divisible by `k` for simplicity. You might need to add additional error handling if this assumption doesn't hold for your use case.

### 1. Algorithms & Data Structures (C++): Sorting Subarray

Sorting a subarray in C++ involves isolating a portion of an array and then applying a sorting algorithm to that portion. Here's a simple example of how you can implement this:

```cpp
#include <iostream>
#include <algorithm>

void printArray(int arr[], int size) {
    for (int i = 0; i < size; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
}

void sortSubarray(int arr[], int left, int right) {
    std::sort(arr + left, arr + right + 1);
}

int main() {
    int arr[] = {3, 7, 1, 9, 4, 6, 2, 8, 5};
    int size = sizeof(arr) / sizeof(arr[0]);
    
    std::cout << "Original array: ";
    printArray(arr, size);
    
    int left = 2; // index of the left boundary of the subarray
    int right = 6; // index of the right boundary of the subarray
    
    sortSubarray(arr, left, right);
    
    std::cout << "Array after sorting subarray: ";
    printArray(arr, size);
    
    return 0;
}
```

In this example:

* `sortSubarray` is a function that takes the array and the indices of the left and right boundaries of the subarray to be sorted.
* `std::sort` from the `<algorithm>` header is used to sort the subarray. `std::sort` is a built-in sorting function in C++ that implements a highly efficient sorting algorithm (typically introsort or a variation of quicksort).
* `printArray` is a utility function to print the elements of an array.
* In the `main` function, an array is initialized, and its original content is printed.
* `left` and `right` variables define the subarray boundaries. In this example, the subarray to be sorted starts from index 2 and ends at index 6.
* Finally, `sortSubarray` is called with the array and the boundary indices, and the sorted array is printed.

### 1. Algorithms & Data Structures (C++): Squares of a Sorted Array

Certainly! The problem "Squares of a Sorted Array" involves taking an array of integers, squaring each integer, and returning an array of squared integers in non-decreasing order. Here's a C++ implementation for this problem:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> sortedSquares(vector<int>& nums) {
    int n = nums.size();
    vector<int> result(n);
    
    int left = 0, right = n - 1;
    int index = n - 1;
    
    while (left <= right) {
        int leftSq = nums[left] * nums[left];
        int rightSq = nums[right] * nums[right];
        
        if (leftSq > rightSq) {
            result[index] = leftSq;
            left++;
        } else {
            result[index] = rightSq;
            right--;
        }
        index--;
    }
    
    return result;
}

int main() {
    vector<int> nums = {-4, -1, 0, 3, 10};
    vector<int> result = sortedSquares(nums);

    cout << "Squared sorted array: ";
    for (int num : result) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}
```

This implementation utilizes a two-pointer approach where one pointer starts at the beginning of the array and the other at the end. We square the elements pointed by these pointers and put the larger squared value into the result array, moving the pointers accordingly. Finally, we return the result array.

### 1. Algorithms & Data Structures (C++): Subarray Sort

Subarray sort is a common problem in algorithmic interviews and competitive programming. The task is to find the shortest subarray within a given array that needs to be sorted in order for the entire array to become sorted.

Here's a C++ implementation of an algorithm to solve this problem:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

pair<int, int> findUnsortedSubarray(vector<int>& nums) {
    int n = nums.size();
    int left = 0, right = n - 1;
    
    // Find the left boundary of the unsorted subarray
    while (left < n - 1 && nums[left] <= nums[left + 1]) left++;
    
    // If the array is already sorted
    if (left == n - 1) return {-1, -1};
    
    // Find the right boundary of the unsorted subarray
    while (right > 0 && nums[right] >= nums[right - 1]) right--;
    
    // Find the minimum and maximum values within the unsorted subarray
    int min_val = *min_element(nums.begin() + left, nums.begin() + right + 1);
    int max_val = *max_element(nums.begin() + left, nums.begin() + right + 1);
    
    // Expand the left boundary if necessary
    while (left >= 0 && nums[left] > min_val) left--;
    
    // Expand the right boundary if necessary
    while (right < n && nums[right] < max_val) right++;
    
    return {left + 1, right - 1};
}

int main() {
    vector<int> nums = {1, 3, 5, 4, 2, 6, 7};
    pair<int, int> result = findUnsortedSubarray(nums);
    
    if (result.first == -1 && result.second == -1)
        cout << "The array is already sorted.\n";
    else
        cout << "The unsorted subarray lies between indices " << result.first << " and " << result.second << ".\n";
    
    return 0;
}
```

This code first finds the left boundary of the unsorted subarray by iterating from the beginning of the array until it finds the first decreasing element. Then, it finds the right boundary by iterating from the end of the array until it finds the first increasing element. After that, it finds the minimum and maximum values within this subarray. Finally, it expands the left and right boundaries as necessary to include any elements that need to be sorted.

You can test this code with different arrays to see how it performs.

### 1. Algorithms & Data Structures (C++): Subarray Sum Divisible by N

To find the number of subarrays whose sum is divisible by a given number N, you can utilize the concept of prefix sums and modular arithmetic. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>

using namespace std;

int subarraysDivByK(vector<int>& A, int K) {
    unordered_map<int, int> remainderCount;
    remainderCount[0] = 1; // Initialize with one subarray whose sum is divisible by K
    int sum = 0;
    int count = 0;
    
    for (int num : A) {
        sum = (sum + num) % K; // Calculate the cumulative sum modulo K
        if (sum < 0) sum += K; // Ensure sum is positive
        
        // If there exists a subarray whose sum is divisible by K,
        // it means that the difference between two prefix sums is divisible by K.
        // So, we count how many prefix sums have the same remainder when divided by K.
        count += remainderCount[sum];
        
        // Update the count for the current remainder
        remainderCount[sum]++;
    }
    
    return count;
}

int main() {
    vector<int> A = {4, 5, 0, -2, -3, 1};
    int K = 5;
    cout << "Number of subarrays divisible by " << K << ": " << subarraysDivByK(A, K) << endl;
    return 0;
}
```

This code will output the number of subarrays whose sum is divisible by the given number `K`.

Here's a brief explanation of how it works:

1. We maintain a map `remainderCount` to store the count of remainders obtained when the cumulative sum of elements is divided by `K`.
2. We initialize `remainderCount[0]` with 1 to handle the case when the sum of elements up to the current index is divisible by `K`.
3. We iterate through the array, updating the cumulative sum modulo `K`.
4. If the current sum modulo `K` exists in `remainderCount`, it means there exists a subarray whose sum is divisible by `K`. We update the count accordingly.
5. We update `remainderCount` with the current sum modulo `K`.
6. Finally, we return the count of subarrays found.

### 1. Algorithms & Data Structures (C++): Subarray Sum: Brute Force

In C++, a brute force approach to find the subarray with the maximum sum involves iterating through all possible subarrays and calculating their sums. Here's a simple implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to find the maximum sum subarray using brute force
pair<int, int> maxSubarraySum(const vector<int>& nums) {
    int maxSum = INT_MIN;
    pair<int, int> result;

    // Iterate through all subarrays
    for (int i = 0; i < nums.size(); ++i) {
        int sum = 0;
        for (int j = i; j < nums.size(); ++j) {
            sum += nums[j];
            // Update maxSum and result if a higher sum is found
            if (sum > maxSum) {
                maxSum = sum;
                result.first = i;
                result.second = j;
            }
        }
    }
    return result;
}

int main() {
    vector<int> nums = {1, -3, 2, 1, -1};
    pair<int, int> result = maxSubarraySum(nums);
    
    cout << "Maximum sum subarray is from index " << result.first << " to " << result.second << endl;

    return 0;
}
```

This code defines a function `maxSubarraySum` that takes a vector of integers and returns a pair of integers representing the start and end indices of the subarray with the maximum sum. The main function demonstrates how to use this function with an example array.

### 1. Algorithms & Data Structures (C++): Subarray Sum: Kadane's Algorithm

Kadane's Algorithm is a well-known technique for finding the maximum sum subarray within a given array of integers. It's particularly efficient with a time complexity of O(n), where n is the size of the array. Here's how you can implement Kadane's Algorithm in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int maxSubArraySum(vector<int>& nums) {
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
    cout << "Maximum sum of subarray: " << maxSubArraySum(nums) << endl;
    return 0;
}
```

In this implementation:

1. `maxSum` keeps track of the maximum sum found so far.
2. `currentSum` keeps track of the sum of the current subarray being processed.
3. We iterate through the array, updating `currentSum` to be the maximum of the current element or the sum of the current element and the previous subarray sum.
4. We update `maxSum` to be the maximum of the current `maxSum` and `currentSum`.
5. Finally, we return `maxSum`, which represents the maximum sum of any subarray in the given array.

This algorithm is particularly useful when you only need the sum of the subarray and not the actual subarray itself. It's also very efficient, as it only requires a single pass through the array.

### 1. Algorithms & Data Structures (C++): Subarray Sum: Prefix Sums

Subarray sum problems are quite common and can be efficiently solved using prefix sums. In C++, you can implement an algorithm to find the subarray with a given sum using prefix sums. Here's a simple implementation:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>

using namespace std;

// Function to find subarray with given sum
vector<int> subarraySum(vector<int>& nums, int targetSum) {
    unordered_map<int, int> prefixSum; // Map to store prefix sums
    int currentSum = 0;
    vector<int> result;

    // Traverse through the array
    for (int i = 0; i < nums.size(); ++i) {
        currentSum += nums[i];

        // If currentSum equals targetSum, subarray starts from index 0
        if (currentSum == targetSum) {
            result.push_back(0);
            result.push_back(i);
            return result;
        }

        // If (currentSum - targetSum) is found in prefixSum, subarray exists
        if (prefixSum.find(currentSum - targetSum) != prefixSum.end()) {
            result.push_back(prefixSum[currentSum - targetSum] + 1);
            result.push_back(i);
            return result;
        }

        // Store currentSum with its index in prefixSum
        prefixSum[currentSum] = i;
    }

    // If no subarray found
    result.push_back(-1);
    return result;
}

int main() {
    vector<int> nums = {1, 4, 20, 3, 10, 5};
    int targetSum = 33;

    vector<int> result = subarraySum(nums, targetSum);

    if (result[0] == -1) {
        cout << "No subarray found with sum " << targetSum << endl;
    } else {
        cout << "Subarray found from index " << result[0] << " to " << result[1] << endl;
    }

    return 0;
}
```

In this implementation:

* We maintain a prefix sum array to store the cumulative sum of elements from index 0 to i.
* As we traverse the array, we keep updating the prefix sum.
* If the current prefix sum equals the target sum, it means the subarray starts from the beginning.
* If there exists a prefix sum such that (currentSum - targetSum), then the subarray lies between the indices of that prefix sum and the current index.
* We use an unordered_map to store the prefix sums along with their corresponding indices for efficient lookup.
* If no subarray is found, we return [-1] as the result.
