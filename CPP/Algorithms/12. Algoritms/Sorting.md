### 1. Algorithms & Data Structures (C++): Basic Sort

Sure! Sorting algorithms are fundamental in computer science and are used to rearrange elements of a list or an array into a particular order. One of the simplest sorting algorithms is the Bubble Sort. Here's a basic implementation of Bubble Sort in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to perform Bubble Sort
void bubbleSort(vector<int> &arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                // Swapping elements if they are in the wrong order
                swap(arr[j], arr[j + 1]);
            }
        }
    }
}

// Function to print an array
void printArray(const vector<int> &arr) {
    for (int i = 0; i < arr.size(); i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

int main() {
    vector<int> arr = {64, 34, 25, 12, 22, 11, 90};
    
    cout << "Original array: ";
    printArray(arr);

    bubbleSort(arr);

    cout << "Sorted array: ";
    printArray(arr);

    return 0;
}
```

This program demonstrates the basic implementation of Bubble Sort in C++. The `bubbleSort` function sorts the array passed to it in ascending order. The `printArray` function is used to print the elements of the array before and after sorting.

Bubble Sort works by repeatedly stepping through the list of elements, comparing adjacent items, and swapping them if they are in the wrong order. This process continues until the list is sorted.

While Bubble Sort is simple to implement, it is not very efficient, especially for large lists, because it has a worst-case and average-case time complexity of O(n^2). There are more efficient sorting algorithms available, such as Merge Sort, Quick Sort, and Heap Sort, which have better time complexities for large datasets.

### 1. Algorithms & Data Structures (C++): Basic Sorting Algorithm

Sure, let's start with one of the most fundamental sorting algorithms: **Bubble Sort**. Bubble Sort is simple to understand but not very efficient, especially for large datasets. However, it's a good starting point to grasp the concept of sorting algorithms.

Here's a basic implementation of Bubble Sort in C++:

```cpp
#include <iostream>
#include <vector>

void bubbleSort(std::vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; ++i) {
        for (int j = 0; j < n - i - 1; ++j) {
            if (arr[j] > arr[j + 1]) {
                // Swap arr[j] and arr[j+1]
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

int main() {
    std::vector<int> arr = {64, 25, 12, 22, 11};
    bubbleSort(arr);
    std::cout << "Sorted array: ";
    for (int i = 0; i < arr.size(); ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
    return 0;
}
```

This code defines a function `bubbleSort` that takes a vector of integers and sorts it using the Bubble Sort algorithm. Then, in the `main` function, it initializes an array with some values, sorts it using `bubbleSort`, and prints the sorted array.

The basic idea behind Bubble Sort is to repeatedly step through the list, compare adjacent elements, and swap them if they are in the wrong order. The pass through the list is repeated until the list is sorted.

While Bubble Sort is not very efficient compared to more advanced algorithms like Quick Sort or Merge Sort, it's useful for educational purposes and small datasets.

### 1. Algorithms & Data Structures (C++): Basic Sorting Algorithms

Sure! Sorting algorithms are essential in computer science and are used to rearrange data in a specific order. Here are some basic sorting algorithms implemented in C++:

1. **Bubble Sort:**
   Bubble Sort repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order.

```cpp
void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n-1; i++) {
        for (int j = 0; j < n-i-1; j++) {
            if (arr[j] > arr[j+1]) {
                // Swap arr[j] and arr[j+1]
                int temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }
}
```

1. **Selection Sort:**
   Selection Sort repeatedly finds the minimum element from the unsorted part of the array and puts it at the beginning.

```cpp
void selectionSort(int arr[], int n) {
    int minIndex;
    for (int i = 0; i < n-1; i++) {
        minIndex = i;
        for (int j = i+1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        // Swap the found minimum element with the first element
        int temp = arr[minIndex];
        arr[minIndex] = arr[i];
        arr[i] = temp;
    }
}
```

1. **Insertion Sort:**
   Insertion Sort builds the final sorted array one item at a time by taking elements from the unsorted part and inserting them into their correct position in the sorted part.

```cpp
void insertionSort(int arr[], int n) {
    int key, j;
    for (int i = 1; i < n; i++) {
        key = arr[i];
        j = i - 1;

        /* Move elements of arr[0..i-1], that are greater than key,
           to one position ahead of their current position */
        while (j >= 0 && arr[j] > key) {
            arr[j+1] = arr[j];
            j--;
        }
        arr[j+1] = key;
    }
}
```

These are the basic sorting algorithms in C++. Each has its advantages and disadvantages depending on the size and nature of the data to be sorted.

### 1. Algorithms & Data Structures (C++): Basic Sorts

Sure! Let's start with some basic sorting algorithms in C++. We'll cover three commonly used sorting algorithms: Bubble Sort, Selection Sort, and Insertion Sort.

1. **Bubble Sort**:
   - Bubble Sort is one of the simplest sorting algorithms. It repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. The pass through the list is repeated until the list is sorted.

```cpp
#include <iostream>
using namespace std;

void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                // Swap arr[j] and arr[j+1]
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

int main() {
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr) / sizeof(arr[0]);
    bubbleSort(arr, n);
    cout << "Sorted array: \n";
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
    return 0;
}
```

1. **Selection Sort**:
   - Selection Sort sorts an array by repeatedly finding the minimum element (considering ascending order) from the unsorted part and putting it at the beginning. The algorithm maintains two subarrays: the subarray which is already sorted and the remaining subarray which is unsorted.

```cpp
#include <iostream>
using namespace std;

void selectionSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        // Swap the found minimum element with the first element
        int temp = arr[i];
        arr[i] = arr[minIndex];
        arr[minIndex] = temp;
    }
}

int main() {
    int arr[] = {64, 25, 12, 22, 11};
    int n = sizeof(arr) / sizeof(arr[0]);
    selectionSort(arr, n);
    cout << "Sorted array: \n";
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
    return 0;
}
```

1. **Insertion Sort**:
   - Insertion Sort builds the final sorted array one item at a time. It takes each element from the array and places it in its correct position in the sorted part of the array.

```cpp
#include <iostream>
using namespace std;

void insertionSort(int arr[], int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}

int main() {
    int arr[] = {12, 11, 13, 5, 6};
    int n = sizeof(arr) / sizeof(arr[0]);
    insertionSort(arr, n);
    cout << "Sorted array: \n";
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
    return 0;
}
```

These are the basic sorting algorithms in C++. Each has its own time complexity and usage scenarios.

### 1. Algorithms & Data Structures (C++): Minimum Swaps

In C++, you can implement an algorithm to find the minimum number of swaps required to sort an array. Here's a basic approach using an unordered map to store the original indices of elements and then iterating through the array to find the cycles in the permutation:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>

using namespace std;

int minSwaps(vector<int>& arr) {
    int n = arr.size();
    unordered_map<int, int> indices;
    for (int i = 0; i < n; ++i) {
        indices[arr[i]] = i;
    }

    vector<bool> visited(n, false);
    int swaps = 0;
    for (int i = 0; i < n; ++i) {
        if (visited[i] || indices[arr[i]] == i) // Already visited or in the correct position
            continue;

        int cycle_size = 0;
        int j = i;
        while (!visited[j]) {
            visited[j] = true;
            j = indices[arr[j]];
            cycle_size++;
        }
        swaps += (cycle_size - 1);
    }
    return swaps;
}

int main() {
    vector<int> arr = {4, 3, 2, 1};
    cout << "Minimum swaps needed: " << minSwaps(arr) << endl;
    return 0;
}
```

This code snippet defines a function `minSwaps` that takes a vector of integers `arr` as input and returns the minimum number of swaps required to sort the array. In the main function, an example array `{4, 3, 2, 1}` is provided, and the minimum swaps needed to sort it are printed.

This approach has a time complexity of O(n) and a space complexity of O(n), where n is the size of the array.

### 1. Algorithms & Data Structures (C++): Algorithms: Sorting

Sorting algorithms are fundamental in computer science and are used to arrange elements of a list or an array in a particular order, such as numerical or lexicographical. In C++, you have a variety of sorting algorithms available in the Standard Template Library (STL), such as:

1. **std::sort**: This is the most commonly used sorting algorithm in C++. It typically implements a variation of quicksort or introsort, which is a hybrid of quicksort and heapsort. It has an average time complexity of O(n log n).

   ```cpp
   #include <algorithm>
   #include <vector>

   int main() {
       std::vector<int> v = {3, 1, 4, 1, 5, 9, 2, 6, 5};
       std::sort(v.begin(), v.end());
       // v is now sorted: {1, 1, 2, 3, 4, 5, 5, 6, 9}
       return 0;
   }
   ```

2. **std::stable_sort**: This is similar to std::sort, but it guarantees stability, meaning equal elements will retain their relative order. It is typically implemented using merge sort and has an average time complexity of O(n log n).

   ```cpp
   #include <algorithm>
   #include <vector>

   int main() {
       std::vector<int> v = {3, 1, 4, 1, 5, 9, 2, 6, 5};
       std::stable_sort(v.begin(), v.end());
       // v is now sorted: {1, 1, 2, 3, 4, 5, 5, 6, 9}
       return 0;
   }
   ```

3. **std::partial_sort**: This sorts the first n elements of a range, leaving the rest of the elements unsorted. It is typically implemented using a partial heap sort algorithm and has a time complexity of O(n log k), where k is the number of elements to sort.

   ```cpp
   #include <algorithm>
   #include <vector>

   int main() {
       std::vector<int> v = {3, 1, 4, 1, 5, 9, 2, 6, 5};
       int n = 4; // Sort the first 4 elements
       std::partial_sort(v.begin(), v.begin() + n, v.end());
       // First 4 elements are sorted: {1, 1, 2, 3}, rest are unsorted
       return 0;
   }
   ```

4. **std::nth_element**: This rearranges elements in a range such that the nth element is in its sorted position and the elements before it are less than or equal to it, while the elements after it are greater than or equal to it. It is typically implemented using a variation of quicksort and has an average time complexity of O(n).

   ```cpp
   #include <algorithm>
   #include <vector>

   int main() {
       std::vector<int> v = {3, 1, 4, 1, 5, 9, 2, 6, 5};
       int n = 4; // Find the 4th smallest element
       std::nth_element(v.begin(), v.begin() + n, v.end());
       // v is partitioned such that the 4th element is sorted: {1, 1, 2, 3, 5, 9, 6, 5, 4}
       return 0;
   }
   ```

These are just a few examples of sorting algorithms available in C++. Depending on your specific needs, you might choose one over the other based on factors like stability, memory usage, or performance characteristics.

### 1. Algorithms & Data Structures (C++): Analysing Selection Sort

Selection sort is a simple sorting algorithm that sorts an array by repeatedly finding the minimum element (considering ascending order) from the unsorted part and putting it at the beginning. Here's a basic analysis of the selection sort algorithm in terms of time complexity, space complexity, and its efficiency:

#### Time Complexity

- **Best Case:** O(n^2)
- **Average Case:** O(n^2)
- **Worst Case:** O(n^2)

In selection sort, regardless of the input distribution, there are always two nested loops. The outer loop runs for n-1 iterations (where n is the number of elements in the array), and the inner loop runs for (n-i) iterations for the i-th iteration of the outer loop. This results in n(n-1)/2 = O(n^2) comparisons and swaps in the worst and average cases, making it inefficient for large datasets.

#### Space Complexity

- O(1)

Selection sort is an in-place sorting algorithm, meaning it doesn't require additional space proportional to the size of the input array. It only needs a constant amount of extra space for variables like loop counters and temporary variables, hence its space complexity is O(1).

#### Stability

Selection sort is not stable. A sorting algorithm is said to be stable if two objects with equal keys appear in the same order in the sorted output as they appear in the input array. In selection sort, swapping might change the relative order of equal elements, making it unstable.

#### Performance

- Selection sort is generally not recommended for large datasets due to its quadratic time complexity.
- It's efficient for small datasets or nearly sorted arrays due to its simplicity and the fact that it always performs a fixed number of comparisons and swaps.

#### Advantages

- Simple implementation.
- No extra space is needed other than a few variables.
- Performs well on small datasets or datasets where swapping elements is expensive.

#### Disadvantages

- Inefficient for large datasets due to its quadratic time complexity.
- Not stable.
- Not adaptive; its time complexity remains the same regardless of whether the list is partially sorted.

#### Conclusion

Selection sort is a straightforward sorting algorithm suitable for small datasets or situations where simplicity is preferred over efficiency. However, for large datasets, more efficient algorithms like quicksort, mergesort, or heapsort are generally preferred.

### 1. Algorithms & Data Structures (C++): Analysis of Bubble Sort

Bubble Sort is a simple comparison-based sorting algorithm. It works by repeatedly stepping through the list, comparing each pair of adjacent items and swapping them if they are in the wrong order. The pass through the list is repeated until no swaps are needed, which indicates that the list is sorted.

Here's a basic implementation of the Bubble Sort algorithm in C++:

```cpp
void bubbleSort(int arr[], int n) {
    bool swapped;
    for (int i = 0; i < n - 1; ++i) {
        swapped = false;
        for (int j = 0; j < n - i - 1; ++j) {
            if (arr[j] > arr[j + 1]) {
                std::swap(arr[j], arr[j + 1]);
                swapped = true;
            }
        }
        // If no two elements were swapped in the inner loop, then the array is already sorted.
        if (!swapped) 
            break;
    }
}
```

#### Time Complexity

- **Worst-case time complexity**: O(n^2)
  - This occurs when the array is in reverse order, and in each pass, the largest element is bubbled to the end of the array.
- **Best-case time complexity**: O(n)
  - This occurs when the array is already sorted. However, even in the best case, Bubble Sort requires at least one pass through the array to check that it is sorted.
- **Average-case time complexity**: O(n^2)
  - On average, Bubble Sort will require approximately n^2/2 comparisons and swaps.

#### Space Complexity

- Bubble Sort is an in-place sorting algorithm, meaning it doesn't require additional space proportional to the size of the input array. Hence, its space complexity is O(1), indicating constant space usage.

#### Stability

- Bubble Sort is a stable sorting algorithm, meaning it preserves the relative order of equal elements in the sorted array. If two elements have the same value, their relative order will remain unchanged after sorting.

#### Efficiency

- Bubble Sort is generally not considered efficient, especially for large datasets, due to its quadratic time complexity. It tends to be outperformed by more efficient algorithms like Quick Sort, Merge Sort, or Heap Sort for larger datasets.
- However, it can be suitable for small datasets or nearly sorted arrays due to its simplicity and ease of implementation.

#### Conclusion

While Bubble Sort is simple to understand and implement, it's not the most efficient sorting algorithm, especially for large datasets. Its quadratic time complexity makes it impractical for sorting large arrays. However, its simplicity and easy implementation make it a good choice for educational purposes or sorting small datasets.

### 1. Algorithms & Data Structures (C++): Analysis of Insertion Sort

Insertion Sort is a simple sorting algorithm that builds the final sorted array (or list) one item at a time. It is much less efficient on large lists than more advanced algorithms such as quicksort, heapsort, or merge sort. However, it has some advantages like simplicity and low overhead, making it useful in certain situations, especially for small datasets or nearly sorted datasets.

Here's a brief analysis of the Insertion Sort algorithm in terms of its time complexity, space complexity, and best, worst, and average-case scenarios:

1. **Time Complexity**:
   - Best Case: O(n)
   - Worst Case: O(n^2)
   - Average Case: O(n^2)

   In the best-case scenario, when the array is already sorted, Insertion Sort only needs to compare each element once, resulting in linear time complexity.

   However, in the worst and average cases, where the array is in reverse order or randomly shuffled, Insertion Sort has a time complexity of O(n^2). This is because for each element, it needs to traverse through the already sorted portion of the array to find the correct position to insert the element.

2. **Space Complexity**:
   - Insertion Sort is an in-place sorting algorithm, meaning it doesn't require any extra space apart from the input array itself. Therefore, its space complexity is O(1), indicating constant space usage.

3. **Stability**:
   - Insertion Sort is stable, meaning that it maintains the relative order of equal elements.

4. **Adaptive**:
   - Insertion Sort is adaptive. If the array is almost sorted, it performs better as it requires fewer comparisons and swaps. In such cases, it can approach linear time complexity.

5. **Performance**:
   - Insertion Sort performs well on small datasets or nearly sorted datasets. It's often used as a building block in more advanced sorting algorithms like Timsort and introsort.

6. **Implementation**:
   - Insertion Sort is straightforward to implement and doesn't require recursion or additional data structures, making it suitable for scenarios where simplicity is preferred over high performance.

Overall, while Insertion Sort is not the most efficient sorting algorithm for large datasets, its simplicity and ease of implementation make it a valuable tool in certain situations, especially for sorting small or nearly sorted arrays.

### 1. Algorithms & Data Structures (C++): Analysis of Merge Sort

Merge Sort is a popular sorting algorithm known for its efficiency and effectiveness in sorting large datasets. Here's an analysis of Merge Sort:

#### Time Complexity

- **Best Case:** O(n log n)
- **Average Case:** O(n log n)
- **Worst Case:** O(n log n)

#### Space Complexity

- Merge Sort typically requires additional space proportional to the size of the input array. It needs space for the temporary arrays used during the merge step. The space complexity is O(n) for the additional arrays.

#### Key Characteristics

1. **Divide and Conquer:** Merge Sort follows the Divide and Conquer approach. It breaks down the array into smaller, more manageable subarrays until they are trivially sorted.
  
2. **Recursive:** It is implemented using recursion. The main function calls itself recursively to sort subarrays.
  
3. **Stable:** Merge Sort is stable, meaning it preserves the relative order of equal elements in the sorted output.

#### Algorithm Steps

1. **Divide:** The array is divided into two halves recursively until each subarray contains only one element.

2. **Conquer:** The subarrays are sorted individually.

3. **Merge:** The sorted subarrays are merged to produce the final sorted array. This is where the "merge" operation happens, which combines two sorted arrays into one sorted array.

#### Analysis

- Merge Sort divides the array into two halves repeatedly until each subarray has only one element. This process takes log(n) steps, where n is the number of elements in the array.
  
- At each step, the merge operation takes linear time, O(n), to merge two sorted arrays of size n/2 each.
  
- Hence, the overall time complexity is O(n log n) since the merge step is executed log(n) times and each merge step takes O(n) time.
  
- Merge Sort's worst-case time complexity is also O(n log n), making it efficient for sorting large datasets.

#### Advantages

- Merge Sort is stable.
- It guarantees O(n log n) performance.
- It performs well on large datasets.
- It's suitable for sorting linked lists as well.

#### Disadvantages

- Merge Sort requires additional memory space for the temporary arrays, which may not be feasible for large arrays.
- While its time complexity is good, it may not be as fast in practice as algorithms with similar time complexities, like Quick Sort, due to its additional memory usage and recursive nature.

In summary, Merge Sort is a reliable sorting algorithm with excellent time complexity and stability, making it a popular choice for sorting large datasets where stability is required and the additional memory usage is acceptable.

### 1. Algorithms & Data Structures (C++): Analysis of Quick Sort

Quick Sort is one of the most efficient and widely used sorting algorithms due to its average-case time complexity of O(n log n) and its in-place sorting nature. It belongs to the class of comparison-based sorting algorithms, where elements are compared pairwise and then swapped if they are in the wrong order.

Here's a breakdown of the analysis of Quick Sort:

1. **Partitioning:**
   - The key operation in Quick Sort is partitioning. It selects a pivot element and partitions the array around the pivot, such that all elements less than the pivot are placed before it and all elements greater than the pivot are placed after it. This partitioning process takes linear time, O(n), where n is the number of elements in the array.

2. **Recurrence Relation:**
   - After partitioning, the array is divided into two sub-arrays. Quick Sort recursively sorts these sub-arrays. The recurrence relation for the time complexity of Quick Sort can be expressed as:
     T(n) = T(k) + T(n-k-1) + O(n)
     where,
     - T(n) is the time taken to sort an array of size n.
     - k is the position of the pivot element after partitioning.
     - O(n) is the time taken for partitioning.

3. **Worst-case Time Complexity:**
   - In the worst-case scenario, Quick Sort might select the smallest or largest element as the pivot, resulting in unbalanced partitions. This leads to one sub-array with n-1 elements and another with 0 elements. Therefore, the worst-case time complexity of Quick Sort is O(n^2). However, this is rare in practice and occurs when the pivot selection is not optimal.
  
4. **Average-case Time Complexity:**
   - On average, Quick Sort performs very well. With good pivot selection, it divides the array into roughly equal halves, leading to a balanced partitioning. Therefore, the average-case time complexity of Quick Sort is O(n log n).

5. **Best-case Time Complexity:**
   - The best-case scenario for Quick Sort is when the pivot divides the array into two sub-arrays of roughly equal size. In this case, the partitioning process divides the array into two halves recursively until each sub-array contains only one element, which is already sorted. Thus, the best-case time complexity of Quick Sort is O(n log n).

6. **Space Complexity:**
   - Quick Sort generally has a space complexity of O(log n) due to its recursive nature. This space is required for maintaining the call stack during the recursive calls. However, in the worst-case scenario, it can require O(n) extra space due to deeply nested recursive calls, though this is uncommon.

7. **Stability:**
   - Quick Sort is not a stable sorting algorithm, meaning it does not necessarily preserve the order of equal elements. However, with proper implementation, stability can be achieved, but usually at the cost of additional overhead.

In summary, Quick Sort is a highly efficient sorting algorithm with an average-case time complexity of O(n log n). While it can degrade to O(n^2) in the worst-case scenario, this is rare in practice, and with proper pivot selection techniques, Quick Sort can consistently perform well.

### 1. Algorithms & Data Structures (C++): Analysis of Selection Sort

Selection sort is a simple sorting algorithm that works by repeatedly selecting the minimum element from the unsorted portion of the array and placing it at the beginning of the array. The algorithm maintains two subarrays: one that is already sorted and another one that is unsorted. In each iteration, it finds the minimum element from the unsorted subarray and swaps it with the first unsorted element, thus expanding the sorted subarray.

Here's a brief analysis of selection sort in terms of time and space complexity:

1. **Time Complexity**:
   - In the worst case, selection sort requires scanning the entire unsorted portion of the array for each element in the array. For an array of size \(n\), this results in approximately \(n + (n - 1) + (n - 2) + ... + 2 + 1 = \frac{n(n + 1)}{2}\) comparisons.
   - Since each comparison takes constant time, the time complexity of selection sort is \(O(n^2)\) in the worst case.
   - Even in the best case, where the array is already sorted, selection sort still needs to perform \(n - 1\) comparisons to check if the current element is the smallest. Therefore, the best-case time complexity is also \(O(n^2)\).
   - The average case time complexity is also \(O(n^2)\).

2. **Space Complexity**:
   - Selection sort is an in-place sorting algorithm, meaning it doesn't require any extra space apart from the input array.
   - The space complexity of selection sort is therefore \(O(1)\), as it only uses a constant amount of extra space for temporary variables.

3. **Stability**:
   - Selection sort is not a stable sorting algorithm. Stable sorting algorithms maintain the relative order of equal elements. In selection sort, the swapping operation can change the relative order of equal elements.

4. **Adaptiveness**:
   - Selection sort is not an adaptive sorting algorithm. An adaptive sorting algorithm is one that takes advantage of existing order in its input. Selection sort always scans the entire unsorted portion of the array to find the minimum element, regardless of the input order.

5. **Use Cases**:
   - Selection sort is not efficient for large datasets due to its \(O(n^2)\) time complexity. However, it can be useful for small datasets or when the memory usage needs to be minimized, as it has a space complexity of \(O(1)\).
   - It's often used for educational purposes due to its simplicity and ease of understanding.

Overall, while selection sort is straightforward to implement, it's not an efficient algorithm for sorting large datasets compared to more advanced algorithms like quicksort or mergesort.

### 1. Algorithms & Data Structures (C++): Bubble sort

Sure, I can provide you with a simple implementation of the bubble sort algorithm in C++:

```cpp
#include <iostream>
#include <vector>

// Bubble sort function
void bubbleSort(std::vector<int> &arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; ++i) {
        for (int j = 0; j < n - i - 1; ++j) {
            if (arr[j] > arr[j + 1]) {
                // Swap arr[j] and arr[j+1]
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

// Function to print an array
void printArray(const std::vector<int> &arr) {
    for (int num : arr) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
}

int main() {
    std::vector<int> arr = {64, 25, 12, 22, 11};
    
    std::cout << "Original array: ";
    printArray(arr);
    
    bubbleSort(arr);
    
    std::cout << "Sorted array: ";
    printArray(arr);
    
    return 0;
}
```

This implementation defines a function `bubbleSort` which takes a reference to a vector of integers as input and sorts the elements using the bubble sort algorithm. The `printArray` function is used to print the elements of an array, and the `main` function demonstrates how to use the `bubbleSort` function to sort an array of integers.

### 1. Algorithms & Data Structures (C++): Bubble Sort (Theory)

Bubble Sort is a simple sorting algorithm that works by repeatedly stepping through the list, comparing each pair of adjacent items and swapping them if they are in the wrong order. The pass through the list is repeated until no swaps are needed, which indicates that the list is sorted. It gets its name because smaller elements gradually "bubble" to the top of the list.

Here's a basic outline of how Bubble Sort works:

1. Start at the beginning of the list.
2. Compare the first two elements.
3. If the first element is greater than the second element, swap them.
4. Move to the next pair of elements and repeat steps 2-3 until the end of the list is reached.
5. Repeat steps 1-4 until no swaps are made during a pass through the list.

The algorithm is simple to understand and implement, but it's not very efficient, especially for large lists, because it has a worst-case and average-case time complexity of O(n^2), where 'n' is the number of elements in the list. This means that its performance degrades quickly as the size of the list increases.

Despite its inefficiency, Bubble Sort can be useful for educational purposes or for sorting small lists where code simplicity is more important than sorting speed. However, for most practical applications, more efficient sorting algorithms like Quick Sort, Merge Sort, or Heap Sort are preferred.

### 1. Algorithms & Data Structures (C++): Bubble Sort Algorithm

Bubble Sort is a simple sorting algorithm that repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. The pass through the list is repeated until the list is sorted. It's called "Bubble Sort" because smaller elements gradually "bubble" to the top of the list.

Here's a basic implementation of Bubble Sort in C++:

```cpp
#include <iostream>
#include <vector>

void bubbleSort(std::vector<int>& arr) {
    int n = arr.size();
    bool swapped;
    for (int i = 0; i < n - 1; i++) {
        swapped = false;
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                // Swap arr[j] and arr[j+1]
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                swapped = true;
            }
        }
        // If no two elements were swapped in the inner loop, the array is already sorted
        if (!swapped)
            break;
    }
}

int main() {
    std::vector<int> arr = {64, 25, 12, 22, 11};
    bubbleSort(arr);
    std::cout << "Sorted array: \n";
    for (int i = 0; i < arr.size(); i++)
        std::cout << arr[i] << " ";
    std::cout << std::endl;
    return 0;
}
```

This code first defines a function `bubbleSort` that takes a reference to a vector of integers. It iterates through the vector, comparing adjacent elements, and swapping them if they are in the wrong order. The process is repeated until the vector is sorted. The main function initializes a vector, calls the `bubbleSort` function to sort it, and then prints the sorted array.

### 1. Algorithms & Data Structures (C++): Bubble Sort Time Complexity

Bubble sort is a simple sorting algorithm that repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. The pass through the list is repeated until the list is sorted.

The time complexity of the bubble sort algorithm is O(n^2), where n is the number of elements in the array. This is because in the worst-case scenario, where the array is in reverse order, bubble sort will need to perform approximately n*(n-1)/2 comparisons and swaps.

Even though bubble sort is easy to understand and implement, it is not efficient for large lists due to its quadratic time complexity. However, it can be useful for educational purposes or for sorting small lists where simplicity is more important than efficiency.

### 1. Algorithms & Data Structures (C++): Bucket Sort

Bucket sort is a comparison sort algorithm that works by distributing the elements of an array into a number of buckets and then sorting each bucket individually. It's particularly useful when the input is uniformly distributed over a range. Here's a simple implementation of bucket sort in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Function to sort an array using bucket sort
void bucketSort(float arr[], int n) {
    // Create empty buckets
    vector<float> buckets[n];

    // Put array elements in different buckets
    for (int i = 0; i < n; i++) {
        int bi = n * arr[i]; // Index in bucket
        buckets[bi].push_back(arr[i]);
    }

    // Sort individual buckets
    for (int i = 0; i < n; i++) {
        sort(buckets[i].begin(), buckets[i].end());
    }

    // Concatenate all buckets into arr[]
    int index = 0;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < buckets[i].size(); j++) {
            arr[index++] = buckets[i][j];
        }
    }
}

// Function to print an array
void printArray(float arr[], int n) {
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

// Driver code
int main() {
    float arr[] = {0.42, 0.32, 0.33, 0.52, 0.37, 0.47, 0.51};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Original array: ";
    printArray(arr, n);

    bucketSort(arr, n);

    cout << "Sorted array: ";
    printArray(arr, n);
    return 0;
}
```

In this implementation:

- We create an array of vectors to represent the buckets.
- We distribute the elements of the input array into the buckets based on a calculated index.
- We sort each individual bucket. In this implementation, `std::sort` from the `<algorithm>` header is used.
- Finally, we concatenate all the buckets into the original array.

The time complexity of bucket sort depends on the sorting algorithm used to sort the individual buckets. If a good sorting algorithm like quicksort or mergesort is used to sort the buckets, the average-case time complexity is O(n + k), where n is the number of elements and k is the number of buckets. However, the worst-case time complexity can be worse if all elements are placed in a single bucket.

### 1. Algorithms & Data Structures (C++): Bucket Sort - Explanation, Algorithm and Analysis

Bucket sort is a sorting algorithm that divides the input array into a finite number of buckets, each of which is then sorted individually, typically with another sorting algorithm like insertion sort or quicksort, and then the sorted buckets are concatenated to obtain the final sorted array.

Here's a step-by-step explanation of the bucket sort algorithm:

1. **Determine the range of input**: Find the minimum and maximum elements in the input array. This helps in determining the range of values that need to be sorted.

2. **Create buckets**: Create an array of buckets, where each bucket represents a range of values. The number of buckets can vary depending on the range of input values and the distribution of data.

3. **Distribute elements into buckets**: Iterate through the input array and distribute each element into the appropriate bucket based on its value. For example, if the input array contains values between 0 and 1, and there are 10 buckets, then elements between 0 and 0.1 will go into the first bucket, elements between 0.1 and 0.2 will go into the second bucket, and so on.

4. **Sort each bucket**: Apply a sorting algorithm (such as insertion sort or quicksort) to sort each individual bucket. Since the elements in each bucket typically have a smaller range, sorting them is more efficient compared to sorting the entire input array.

5. **Concatenate the sorted buckets**: After sorting each bucket individually, concatenate the sorted buckets to obtain the final sorted array.

Now, let's discuss the analysis of bucket sort:

- **Time complexity**: The time complexity of bucket sort depends on the sorting algorithm used to sort the individual buckets and the distribution of elements into buckets. If the elements are evenly distributed across buckets and each bucket is sorted efficiently (e.g., using insertion sort), then the time complexity can be linear O(n + k), where n is the number of elements in the input array and k is the number of buckets. However, if the elements are not evenly distributed, the worst-case time complexity may be worse.

- **Space complexity**: The space complexity of bucket sort depends on the number of buckets created. If the number of buckets is proportional to the size of the input array, then the space complexity is O(n). However, if the number of buckets is fixed regardless of the input size, then the space complexity is O(k), where k is the number of buckets.

- **Stability**: Bucket sort can be stable or unstable depending on the stability of the sorting algorithm used to sort the individual buckets. For example, if a stable sorting algorithm like insertion sort is used, then bucket sort will be stable.

Overall, bucket sort is efficient for sorting a large number of elements with a uniform distribution and a known range, but its performance can degrade if the distribution is uneven or if the range of values is very large.

### 1. Algorithms & Data Structures (C++): Bucket Sort with Negative Numbers

Bucket sort is typically used for sorting elements when the range of the data is known and small. However, bucket sort as it's traditionally implemented doesn't handle negative numbers well because it usually relies on array indices, which can't be negative.

To handle negative numbers with bucket sort, you can use an offset to map the negative numbers to non-negative numbers before sorting. Here's how you can implement bucket sort in C++ to handle negative numbers:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Function to perform bucket sort
void bucketSort(vector<int>& arr) {
    int n = arr.size();
    
    // Find minimum and maximum values in the array
    int min_val = *min_element(arr.begin(), arr.end());
    int max_val = *max_element(arr.begin(), arr.end());
    
    // Calculate the range and number of buckets
    int range = max_val - min_val + 1;
    int num_buckets = range;
    
    // Create buckets
    vector<vector<int>> buckets(num_buckets);
    
    // Distribute elements into buckets
    for (int i = 0; i < n; ++i) {
        buckets[arr[i] - min_val].push_back(arr[i]);
    }
    
    // Sort individual buckets
    for (int i = 0; i < num_buckets; ++i) {
        sort(buckets[i].begin(), buckets[i].end());
    }
    
    // Concatenate the sorted buckets
    int index = 0;
    for (int i = 0; i < num_buckets; ++i) {
        for (int j = 0; j < buckets[i].size(); ++j) {
            arr[index++] = buckets[i][j];
        }
    }
}

int main() {
    // Example usage
    vector<int> arr = {4, -2, -10, 5, 0, -5, 7, -1};
    
    cout << "Original array: ";
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;
    
    bucketSort(arr);
    
    cout << "Sorted array: ";
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;
    
    return 0;
}
```

This implementation first finds the minimum and maximum values in the array to determine the range. Then it creates a bucket for each possible value in the range. Negative numbers are mapped to non-negative numbers using the minimum value as an offset. Finally, it distributes the elements into their respective buckets, sorts each bucket individually, and then concatenates the sorted buckets to get the final sorted array.

### 1. Algorithms & Data Structures (C++): Bin / Bucket Sort

Bin sort, also known as bucket sort, is a sorting algorithm that divides a list of elements into several groups called bins or buckets, and then sorts each bucket individually, either using another sorting algorithm or recursively applying bucket sort itself. Once each bucket is sorted, the sorted buckets are concatenated to obtain the sorted list. This sorting algorithm is particularly efficient when the input is uniformly distributed over a range.

Here's a basic implementation of bucket sort in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Function to perform bucket sort
void bucketSort(vector<float>& arr) {
    int n = arr.size();
    
    // Create empty buckets
    vector<vector<float>> buckets(n);
    
    // Put elements into respective buckets
    for (int i = 0; i < n; ++i) {
        int bucketIndex = n * arr[i];
        buckets[bucketIndex].push_back(arr[i]);
    }
    
    // Sort each bucket
    for (int i = 0; i < n; ++i) {
        sort(buckets[i].begin(), buckets[i].end());
    }
    
    // Concatenate sorted buckets
    int index = 0;
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < buckets[i].size(); ++j) {
            arr[index++] = buckets[i][j];
        }
    }
}

// Function to print an array
void printArray(const vector<float>& arr) {
    for (float x : arr) {
        cout << x << " ";
    }
    cout << endl;
}

int main() {
    vector<float> arr = {0.42, 0.32, 0.33, 0.52, 0.37, 0.47, 0.51};
    
    cout << "Original array: ";
    printArray(arr);
    
    bucketSort(arr);
    
    cout << "Sorted array: ";
    printArray(arr);
    
    return 0;
}
```

This code first divides the range [0,1) into equal-sized intervals, each representing a bucket. Then it iterates through the input array, placing each element into its corresponding bucket. After that, it sorts each bucket individually using an auxiliary sorting algorithm (in this case, `std::sort` from the C++ Standard Library). Finally, it concatenates all the sorted buckets to obtain the sorted array.

### 1. Algorithms & Data Structures (C++): Bin Sort

It seems like you're referring to a "Bin Sort" algorithm. However, "Bin Sort" isn't a standard sorting algorithm like Quick Sort or Merge Sort. It might be a term used in a specific context or it could be a variation or abbreviation of another sorting algorithm.

Could you provide more context or details about what you mean by "Bin Sort" so I can assist you better?

### 1. Algorithms & Data Structures (C++): Bogo Sort

Bogo Sort is an incredibly inefficient and impractical sorting algorithm. It works by shuffling the elements of the array randomly until they happen to be in sorted order. The name "Bogo" comes from the word "bogus," which accurately describes the method's lack of efficiency and reliability.

Here's a simple implementation of Bogo Sort in C++:

```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>
#include <algorithm>

// Function to check if the array is sorted
bool isSorted(int arr[], int n) {
    for (int i = 1; i < n; ++i) {
        if (arr[i - 1] > arr[i]) {
            return false;
        }
    }
    return true;
}

// Function to shuffle the array randomly
void shuffle(int arr[], int n) {
    for (int i = 0; i < n; ++i) {
        int j = rand() % n;
        std::swap(arr[i], arr[j]);
    }
}

// Bogo Sort function
void bogoSort(int arr[], int n) {
    // Keep shuffling until the array is sorted
    while (!isSorted(arr, n)) {
        shuffle(arr, n);
    }
}

int main() {
    srand(time(nullptr)); // Seed the random number generator
    
    int arr[] = {5, 2, 9, 1, 5, 6};
    int n = sizeof(arr) / sizeof(arr[0]);

    std::cout << "Original array: ";
    for (int i = 0; i < n; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    bogoSort(arr, n);

    std::cout << "Sorted array: ";
    for (int i = 0; i < n; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this implementation:

- `isSorted()` checks if the array is sorted.
- `shuffle()` randomly shuffles the array.
- `bogoSort()` repeatedly shuffles the array until it is sorted.

Keep in mind that Bogo Sort is extremely inefficient and its time complexity is unbounded. The worst-case time complexity is technically infinite because it's not guaranteed to ever terminate. It's only really useful for educational purposes or as a joke, and should never be used in practical applications.

### 1. Algorithms & Data Structures (C++): Cocktail Sort

Cocktail Sort, also known as Bidirectional Bubble Sort, is a variation of Bubble Sort. It sorts the array in both directions - from left to right (ascending) and from right to left (descending). This sorting algorithm works by repeatedly traversing the array in both directions, exchanging elements if they are in the wrong order.

Here's a C++ implementation of Cocktail Sort:

```cpp
#include <iostream>
using namespace std;

void cocktailSort(int arr[], int n) {
    bool swapped = true;
    int start = 0;
    int end = n - 1;

    while (swapped) {
        // reset the swapped flag
        swapped = false;

        // traverse from left to right
        for (int i = start; i < end; ++i) {
            if (arr[i] > arr[i + 1]) {
                swap(arr[i], arr[i + 1]);
                swapped = true;
            }
        }

        // if no swapping occurred, array is already sorted
        if (!swapped)
            break;

        // decrease end as the last element is already in place
        end--;

        // traverse from right to left
        for (int i = end - 1; i >= start; --i) {
            if (arr[i] > arr[i + 1]) {
                swap(arr[i], arr[i + 1]);
                swapped = true;
            }
        }

        // increase start as the first element is already in place
        start++;
    }
}

// Function to print an array
void printArray(int arr[], int size) {
    for (int i = 0; i < size; i++)
        cout << arr[i] << " ";
    cout << endl;
}

int main() {
    int arr[] = {5, 2, 6, 1, 3, 7, 4};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Original array: ";
    printArray(arr, n);

    cocktailSort(arr, n);

    cout << "Sorted array: ";
    printArray(arr, n);
    return 0;
}
```

In this implementation:

- `cocktailSort` function sorts the array using the Cocktail Sort algorithm.
- `start` and `end` are used to keep track of the portion of the array that is being sorted.
- The outer `while` loop continues until no swaps are made in a pass.
- The first inner loop moves from left to right, bubbling up the largest element to its correct position.
- The second inner loop moves from right to left, pushing down the smallest element to its correct position.
- The process continues until the array is sorted.

### 1. Algorithms & Data Structures (C++): Comb Sort

Comb Sort is an algorithm for sorting data. It is an improvement over Bubble Sort, designed to eliminate the "turtles" problem (small values at the end of the list) by comparing elements that are far apart. This makes Comb Sort more efficient than Bubble Sort for large datasets.

Here's how the Comb Sort algorithm works:

1. Choose a gap factor, typically a value greater than 1 (usually around 1.3). This gap factor determines the size of the gap between compared elements.
2. Initialize the gap size as the length of the array being sorted.
3. Repeat until the gap size becomes 1:
   - Set a flag to check if any swap occurs in the iteration.
   - Update the gap size by dividing it by the gap factor and taking the integer part.
   - Compare elements that are 'gap' distance apart and swap them if necessary.
   - If a swap occurs, set the flag to true.
4. Continue this process with a reduced gap size until the gap becomes 1 and no swaps occur in an iteration.

Here's a simple implementation of the Comb Sort algorithm in C++:

```cpp
#include <iostream>
#include <vector>

void combSort(std::vector<int>& arr) {
    int n = arr.size();
    int gap = n;
    float shrink = 1.3; // Gap shrink factor
    bool swapped = true;

    while (gap > 1 || swapped) {
        gap = gap / shrink;
        if (gap < 1) gap = 1;

        swapped = false;

        for (int i = 0; i + gap < n; i++) {
            if (arr[i] > arr[i + gap]) {
                std::swap(arr[i], arr[i + gap]);
                swapped = true;
            }
        }
    }
}

int main() {
    std::vector<int> arr = {8, 4, 1, 7, 3, 9, 2, 5, 6};
    std::cout << "Original array: ";
    for (int num : arr) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    combSort(arr);

    std::cout << "Sorted array: ";
    for (int num : arr) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

This implementation demonstrates the Comb Sort algorithm in C++, sorting a vector of integers in ascending order.

### 1. Algorithms & Data Structures (C++): Comparing Bubble and Insertion Sort

Both bubble sort and insertion sort are simple sorting algorithms commonly taught in introductory computer science courses. They have different approaches and efficiencies, making them suitable for different scenarios. Let's compare them:

1. **Bubble Sort**:
   - **Overview**: Bubble sort repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. This process is repeated until the list is sorted.
   - **Time Complexity**:
     - Worst-case: O(n^2)
     - Best-case (with optimization): O(n) - This occurs when the list is already sorted, and the algorithm makes only one pass.
     - Average-case: O(n^2)
   - **Space Complexity**: O(1) - Bubble sort is an in-place sorting algorithm as it only requires a constant amount of extra space.
   - **Stability**: Bubble sort is stable, meaning it preserves the relative order of equal elements.
   - **Suitability**: Bubble sort is suitable for small lists or nearly sorted lists due to its simplicity. However, it's inefficient for large lists due to its quadratic time complexity.

2. **Insertion Sort**:
   - **Overview**: Insertion sort builds the final sorted array (or list) one item at a time. It takes each element from the input list and inserts it into its correct position within the sorted portion of the list.
   - **Time Complexity**:
     - Worst-case: O(n^2)
     - Best-case: O(n) - This occurs when the list is already sorted, and insertion sort makes only one pass.
     - Average-case: O(n^2)
   - **Space Complexity**: O(1) - Insertion sort, like bubble sort, is an in-place sorting algorithm.
   - **Stability**: Insertion sort is also stable, preserving the relative order of equal elements.
   - **Suitability**: Insertion sort is efficient for small lists or nearly sorted lists. It's often used in practice for sorting small datasets or as a subroutine in more complex algorithms (like quicksort or mergesort) for sorting small subarrays.

**Comparison**:

- **Efficiency**: In terms of time complexity, both algorithms have the same worst-case and average-case complexities. However, insertion sort tends to be more efficient in practice, especially for small datasets or lists that are already partially sorted.
- **Space Complexity**: Both algorithms have the same space complexity as they are in-place sorting algorithms.
- **Stability**: Both algorithms are stable, so they preserve the relative order of equal elements.
- **Use Cases**: Bubble sort is rarely used in practice due to its inefficiency for larger datasets. Insertion sort, while still not as efficient as more advanced algorithms like quicksort or mergesort, has practical applications for small datasets or as a building block in more complex algorithms.

In summary, while both bubble sort and insertion sort are simple sorting algorithms, insertion sort tends to be more efficient in practice and is preferred over bubble sort for sorting small or partially sorted datasets.

### 1. Algorithms & Data Structures (C++): Comparison of Sorting Algorithms

Certainly! Sorting algorithms are fundamental in computer science, and each algorithm has its strengths and weaknesses depending on factors like input size, data distribution, and memory constraints. Here's a comparison of some common sorting algorithms in C++:

1. **Bubble Sort**:
   - Simple and easy to implement.
   - Poor performance for large datasets (O(n^2)).
   - Stable and in-place.

2. **Selection Sort**:
   - Simple to implement.
   - Poor performance for large datasets (O(n^2)).
   - Not stable but in-place.

3. **Insertion Sort**:
   - Efficient for small datasets and nearly sorted arrays.
   - Moderate performance for large datasets (O(n^2)).
   - Stable and in-place.

4. **Merge Sort**:
   - Efficient for large datasets (O(n log n)).
   - Stable but not in-place (requires extra memory).
   - Good for linked lists.

5. **Quick Sort**:
   - Efficient for large datasets (average case O(n log n)).
   - Unstable but in-place.
   - Worst-case performance can degrade to O(n^2), but this is rare.

6. **Heap Sort**:
   - Efficient for large datasets (O(n log n)).
   - Unstable but in-place.
   - Good for finding the maximum (or minimum) element repeatedly.

7. **Counting Sort**:
   - Efficient for a range of integers (O(n + k), where k is the range of input).
   - Requires extra space proportional to the range of the input.
   - Not suitable for floating-point numbers or objects.

8. **Radix Sort**:
   - Efficient for integers represented in binary, decimal, or hexadecimal (O(nk), where k is the average number of digits).
   - Stable and can be in-place.
   - Good for sorting strings with fixed-length keys.

9. **Bucket Sort**:
   - Efficient for uniformly distributed data (average case O(n + k), where k is the number of buckets).
   - Requires prior knowledge of the data distribution.
   - Not stable but can be made stable.

Choosing the right sorting algorithm depends on various factors such as the size of the dataset, the range of values, memory constraints, and whether stability or in-place sorting is required.

### 1. Algorithms & Data Structures (C++): Count Sort

Counting Sort is an efficient sorting algorithm that sorts elements in a specific range. It works by counting the number of occurrences of each unique element in the input array and then using arithmetic to calculate the position of each element in the sorted output array.

Here's how Counting Sort works:

1. Find the range of the input elements. Determine the minimum and maximum values in the array.
2. Create a count array to store the count of each element. The size of this array is determined by the range of elements.
3. Traverse the input array and increment the count of each element in the count array.
4. Modify the count array to store the cumulative count of each element. This step helps determine the position of each element in the sorted array.
5. Create a temporary array to store the sorted output.
6. Traverse the input array again, use the count array to determine the position of each element in the output array, and place the elements accordingly.
7. Finally, copy the elements from the temporary array back to the original array to get the sorted result.

Here's a simple implementation of Counting Sort in C++:

```cpp
#include <iostream>
#include <vector>

void countingSort(std::vector<int>& arr) {
    // Find the range of input elements
    int max_val = *std::max_element(arr.begin(), arr.end());
    int min_val = *std::min_element(arr.begin(), arr.end());
    int range = max_val - min_val + 1;

    // Create a count array and initialize all elements to 0
    std::vector<int> count(range, 0);

    // Count the occurrences of each element
    for (int i = 0; i < arr.size(); ++i) {
        count[arr[i] - min_val]++;
    }

    // Modify the count array to store the cumulative count
    for (int i = 1; i < range; ++i) {
        count[i] += count[i - 1];
    }

    // Create a temporary array to store the sorted output
    std::vector<int> output(arr.size());

    // Place the elements in the output array using the count array
    for (int i = arr.size() - 1; i >= 0; --i) {
        output[count[arr[i] - min_val] - 1] = arr[i];
        count[arr[i] - min_val]--;
    }

    // Copy the sorted elements back to the original array
    for (int i = 0; i < arr.size(); ++i) {
        arr[i] = output[i];
    }
}

int main() {
    std::vector<int> arr = {4, 2, 2, 8, 3, 3, 1};
    countingSort(arr);
    std::cout << "Sorted array: ";
    for (int x : arr) {
        std::cout << x << " ";
    }
    std::cout << std::endl;
    return 0;
}
```

This implementation sorts the input array `arr` in non-decreasing order. The time complexity of Counting Sort is O(n + k), where n is the number of elements in the input array and k is the range of input. However, Counting Sort is not suitable for sorting large arrays with a large range of values because it requires extra space proportional to the range of the input elements.

### 1. Algorithms & Data Structures (C++): Count Sort - Explanation, Algorithm and Analysis

Certainly! Counting Sort is a non-comparison based sorting algorithm that sorts elements in linear time. It works by counting the number of occurrences of each unique element in the input array and then using those counts to determine the final sorted order.

Here's a step-by-step explanation of the Counting Sort algorithm:

1. **Counting Phase**:
   - First, determine the range of input elements. Find the minimum and maximum values in the input array.
   - Create a counting array (also called an auxiliary array) of size `(max - min + 1)` where each index represents a unique element in the input array.
   - Traverse the input array and count the occurrences of each unique element by incrementing the corresponding index in the counting array.

2. **Cumulative Counting Phase** (Optional, for stability):
   - Modify the counting array to store the cumulative count of elements. This step ensures that if there are multiple occurrences of the same element, they retain their relative order in the sorted output.

3. **Sorting Phase**:
   - Iterate through the counting array, and for each element, output the corresponding number of occurrences to the sorted array.
   - Decrement the count of the element in the counting array if multiple occurrences are allowed.

Here's a simple implementation of Counting Sort in C++:

```cpp
#include <iostream>
#include <vector>

void countingSort(std::vector<int>& arr) {
    int maxVal = *std::max_element(arr.begin(), arr.end());
    int minVal = *std::min_element(arr.begin(), arr.end());
    int range = maxVal - minVal + 1;

    std::vector<int> count(range), output(arr.size());
    
    for (int i = 0; i < arr.size(); ++i)
        ++count[arr[i] - minVal];

    for (int i = 1; i < range; ++i)
        count[i] += count[i - 1];

    for (int i = arr.size() - 1; i >= 0; --i) {
        output[count[arr[i] - minVal] - 1] = arr[i];
        --count[arr[i] - minVal];
    }

    for (int i = 0; i < arr.size(); ++i)
        arr[i] = output[i];
}

int main() {
    std::vector<int> arr = {4, 2, 2, 8, 3, 3, 1};
    countingSort(arr);

    std::cout << "Sorted array: ";
    for (int num : arr)
        std::cout << num << " ";
    std::cout << std::endl;

    return 0;
}
```

**Analysis**:

- Time Complexity: O(n + k), where n is the number of elements in the input array and k is the range of input.
- Space Complexity: O(n + k) for the counting array and the output array.

Counting Sort is efficient for sorting integers within a small and known range. However, its space complexity can be a drawback for large ranges or when the range is significantly larger than the number of elements. Additionally, it's not a comparison-based sorting algorithm, which makes it faster in certain scenarios.

### 1. Algorithms & Data Structures (C++): Counting Sort

Counting Sort is an efficient sorting algorithm that sorts elements of an array by counting the number of occurrences of each unique element and then placing them in order. It works particularly well when the range of elements is known and relatively small compared to the number of elements in the array.

Here's a simple implementation of Counting Sort in C++:

```cpp
#include <iostream>
#include <vector>

void countingSort(std::vector<int>& arr) {
    // Find the maximum element in the array
    int maxElement = *max_element(arr.begin(), arr.end());

    // Create a count array to store the count of each element
    std::vector<int> count(maxElement + 1, 0);

    // Store the count of each element in the count array
    for (int i = 0; i < arr.size(); ++i)
        count[arr[i]]++;

    // Modify the count array to store the actual position of each element in the sorted array
    for (int i = 1; i <= maxElement; ++i)
        count[i] += count[i - 1];

    // Create a temporary array to store the sorted result
    std::vector<int> result(arr.size());

    // Build the sorted array
    for (int i = arr.size() - 1; i >= 0; --i) {
        result[count[arr[i]] - 1] = arr[i];
        count[arr[i]]--;
    }

    // Copy the sorted result back to the original array
    for (int i = 0; i < arr.size(); ++i)
        arr[i] = result[i];
}

int main() {
    std::vector<int> arr = {4, 2, 2, 8, 3, 3, 1};
    std::cout << "Original array: ";
    for (int num : arr)
        std::cout << num << " ";
    std::cout << std::endl;

    countingSort(arr);

    std::cout << "Sorted array: ";
    for (int num : arr)
        std::cout << num << " ";
    std::cout << std::endl;

    return 0;
}
```

This code sorts an array of integers using Counting Sort. It first determines the maximum element in the array to create a count array of appropriate size. Then, it counts the occurrences of each element and modifies the count array to represent the actual positions of elements in the sorted array. Finally, it builds the sorted array using the count array and copies the result back to the original array.

### 1. Algorithms & Data Structures (C++): Gnome Sort

Gnome Sort, also known as Stupid Sort, is a sorting algorithm inspired by the way garden gnomes sort a line of flower pots. It's a simple and inefficient sorting algorithm, primarily used for educational purposes or when simplicity is more important than efficiency.

Here's how the Gnome Sort algorithm works:

1. Start at the beginning of the array.
2. If the current element is greater than or equal to the previous element, move to the next element.
3. If the current element is smaller than the previous element, swap them and move one step back.
4. Repeat steps 2 and 3 until the current element is greater than or equal to the previous element and you reach the end of the array.
5. Once you reach the end of the array, the array is sorted.

Here's a simple implementation of Gnome Sort in C++:

```cpp
#include <iostream>
#include <vector>

void gnomeSort(std::vector<int>& arr) {
    int index = 0;
    int size = arr.size();
    
    while (index < size) {
        if (index == 0 || arr[index] >= arr[index - 1]) {
            index++;
        } else {
            std::swap(arr[index], arr[index - 1]);
            index--;
        }
    }
}

int main() {
    std::vector<int> arr = {5, 2, 9, 1, 5, 6};
    
    std::cout << "Before sorting: ";
    for (int num : arr) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
    
    gnomeSort(arr);
    
    std::cout << "After sorting: ";
    for (int num : arr) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
    
    return 0;
}
```

This implementation sorts an array of integers using the Gnome Sort algorithm. You can replace the vector with any other container or array type if needed. Remember that Gnome Sort is not efficient for large datasets and should generally be avoided in favor of more efficient sorting algorithms like Quick Sort or Merge Sort.

### 1. Algorithms & Data Structures (C++): Heap and Heap Sort

Sure, let's dive into the concepts of heaps and heap sort in C++.

#### Heaps

A heap is a binary tree data structure where each node satisfies the heap property. In a max heap, for any given node, the value of the node is greater than or equal to the values of its children. In a min heap, it's the opposite: the value of each node is less than or equal to the values of its children.

In C++, heaps are commonly implemented using arrays. In a binary heap, the children of the node at index `i` are located at indices `2*i + 1` (left child) and `2*i + 2` (right child). Conversely, the parent of a node at index `i` is located at index `(i - 1) / 2`.

#### Heap Sort

Heap sort is a comparison-based sorting algorithm that leverages the heap data structure. It consists of two main steps: heap construction and heap extraction.

1. **Heap Construction**: Given an unsorted array, we construct a max heap from it. This is done by repeatedly heapifying the array from the bottom up, starting from the last non-leaf node to the root. This ensures that every parent node is greater than or equal to its children, fulfilling the max heap property.

2. **Heap Extraction**: After constructing the max heap, the maximum element (at the root) is swapped with the last element of the array, reducing the size of the heap by 1. Then, the heap property is restored by heapifying the root node. This process is repeated until all elements are sorted.

Let's implement heap sort in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to heapify a subtree rooted at index i
// n is the size of the heap
void heapify(vector<int>& arr, int n, int i) {
    int largest = i; // Initialize largest as root
    int left = 2 * i + 1; // left child
    int right = 2 * i + 2; // right child

    // If left child is larger than root
    if (left < n && arr[left] > arr[largest])
        largest = left;

    // If right child is larger than largest so far
    if (right < n && arr[right] > arr[largest])
        largest = right;

    // If largest is not root
    if (largest != i) {
        swap(arr[i], arr[largest]);

        // Recursively heapify the affected sub-tree
        heapify(arr, n, largest);
    }
}

// Main function to do heap sort
void heapSort(vector<int>& arr) {
    int n = arr.size();

    // Build heap (rearrange array)
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);

    // One by one extract an element from heap
    for (int i = n - 1; i > 0; i--) {
        // Move current root to end
        swap(arr[0], arr[i]);

        // call max heapify on the reduced heap
        heapify(arr, i, 0);
    }
}

int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    int n = arr.size();

    cout << "Original array: ";
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;

    heapSort(arr);

    cout << "Sorted array: ";
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;

    return 0;
}
```

This C++ code demonstrates the implementation of heap sort using the heapify function for constructing and maintaining the heap property. The `heapSort` function first constructs a max heap and then repeatedly extracts the maximum element to sort the array in ascending order.

### 1. Algorithms & Data Structures (C++): Heap sort

Heap sort is a comparison-based sorting algorithm that builds a binary heap from the input array and repeatedly extracts the maximum (for max-heap) or minimum (for min-heap) element from the heap and rebuilds the heap until the array is sorted.

Here's how the heap sort algorithm works:

1. **Build Heap**: Build a max-heap from the array. This step rearranges the elements of the array so that they satisfy the heap property (the parent node is greater than its children for a max-heap, or less than its children for a min-heap).

2. **Heapify**: Repeatedly remove the maximum element from the heap (swap it with the last element in the heap so that the maximum element is at the end of the array), and decrease the size of the heap by one. Then, heapify the root of the heap (restore the heap property).

3. **Repeat**: Repeat step 2 until the heap is empty.

4. **Sorted Array**: After all iterations, the array will be sorted in ascending order (for max-heap) or descending order (for min-heap).

Here's a C++ implementation of heap sort:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to heapify a subtree rooted at index i in vector arr[]
// n is the size of the heap
template<typename T>
void heapify(vector<T>& arr, int n, int i) {
    int largest = i; // Initialize largest as root
    int left = 2 * i + 1; // left child
    int right = 2 * i + 2; // right child

    // If left child is larger than root
    if (left < n && arr[left] > arr[largest])
        largest = left;

    // If right child is larger than largest so far
    if (right < n && arr[right] > arr[largest])
        largest = right;

    // If largest is not root
    if (largest != i) {
        swap(arr[i], arr[largest]);

        // Recursively heapify the affected sub-tree
        heapify(arr, n, largest);
    }
}

// Main function to do heap sort
template<typename T>
void heapSort(vector<T>& arr) {
    int n = arr.size();

    // Build heap (rearrange array)
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);

    // One by one extract an element from heap
    for (int i = n - 1; i >= 0; i--) {
        // Move current root to end
        swap(arr[0], arr[i]);

        // call max heapify on the reduced heap
        heapify(arr, i, 0);
    }
}

// Function to print an array
template<typename T>
void printArray(vector<T>& arr) {
    for (const auto &element : arr)
        cout << element << " ";
    cout << endl;
}

// Driver code
int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    cout << "Original array: ";
    printArray(arr);

    heapSort(arr);

    cout << "Sorted array: ";
    printArray(arr);

    return 0;
}
```

This implementation demonstrates heap sort on an integer array, but it can be easily modified to work with other data types as well.

### 1. Algorithms & Data Structures (C++): Heap Sort - Explanation, Algorithm and Analysis

Heap Sort is a comparison-based sorting algorithm that falls under the category of selection sort algorithms. It works by transforming the input array into a binary heap data structure, then repeatedly removing the maximum (for a max-heap) or minimum (for a min-heap) element from the heap and rebuilding the heap until the array is sorted.

Here's a step-by-step explanation of the Heap Sort algorithm along with its implementation in C++:

#### Algorithm

1. **Build Heap**: Build a max heap from the input array. This can be done by starting from the last non-leaf node and repeatedly heapifying each subtree until the entire array is transformed into a heap. The last non-leaf node can be found at index `(n/2) - 1`, where `n` is the number of elements in the array.

2. **Heapify**: Heapify the heap. Swap the root (maximum element for max-heap) with the last element in the heap, reduce the size of the heap by 1, and heapify the root to maintain the heap property. Repeat this process until the heap size becomes 1.

#### Implementation in C++

```cpp
// Heapify a subtree rooted at index i, n is the size of the heap
void heapify(int arr[], int n, int i) {
    int largest = i;  // Initialize largest as root
    int l = 2 * i + 1;  // Left child
    int r = 2 * i + 2;  // Right child

    // If left child is larger than root
    if (l < n && arr[l] > arr[largest])
        largest = l;

    // If right child is larger than largest so far
    if (r < n && arr[r] > arr[largest])
        largest = r;

    // If largest is not root
    if (largest != i) {
        swap(arr[i], arr[largest]);
        // Recursively heapify the affected subtree
        heapify(arr, n, largest);
    }
}

// Main function to do heap sort
void heapSort(int arr[], int n) {
    // Build heap (rearrange array)
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);

    // Extract elements from heap one by one
    for (int i = n - 1; i >= 0; i--) {
        // Move current root to end
        swap(arr[0], arr[i]);

        // call max heapify on the reduced heap
        heapify(arr, i, 0);
    }
}
```

#### Analysis

- **Time Complexity**: The time complexity of Heap Sort is O(n log n) in the worst-case scenario, where 'n' is the number of elements in the array. This complexity arises because each heapify operation takes O(log n) time, and there are 'n' such operations.
  
- **Space Complexity**: The space complexity of Heap Sort is O(1) since the sorting is done in-place without requiring any extra space beyond the input array.

Heap Sort is not a stable sort, meaning that the relative order of equal elements may not be preserved. However, it has efficient average and worst-case time complexities and is widely used in practice for its simplicity and efficiency.

### 1. Algorithms & Data Structures (C++): Heap Sort Algorithm

Heap Sort is a comparison-based sorting algorithm that uses a binary heap data structure. It sorts the elements by first building a max heap (or min heap, depending on whether you're sorting in ascending or descending order) from the input array and then repeatedly removing the maximum (or minimum) element from the heap and placing it at the end of the array. Here's a basic implementation of Heap Sort in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to heapify a subtree rooted at node i
// n is the size of heap
template<typename T>
void heapify(vector<T>& arr, int n, int i) {
    int largest = i; // Initialize largest as root
    int left = 2 * i + 1; // Left child
    int right = 2 * i + 2; // Right child

    // If left child is larger than root
    if (left < n && arr[left] > arr[largest])
        largest = left;

    // If right child is larger than largest so far
    if (right < n && arr[right] > arr[largest])
        largest = right;

    // If largest is not root
    if (largest != i) {
        swap(arr[i], arr[largest]);

        // Recursively heapify the affected sub-tree
        heapify(arr, n, largest);
    }
}

// Main function to do heap sort
template<typename T>
void heapSort(vector<T>& arr) {
    int n = arr.size();

    // Build heap (rearrange array)
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);

    // One by one extract an element from heap
    for (int i = n - 1; i > 0; i--) {
        // Move current root to end
        swap(arr[0], arr[i]);

        // Call max heapify on the reduced heap
        heapify(arr, i, 0);
    }
}

// Utility function to print an array
template<typename T>
void printArray(const vector<T>& arr) {
    for (const auto& elem : arr)
        cout << elem << " ";
    cout << endl;
}

int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    cout << "Original array: ";
    printArray(arr);

    heapSort(arr);

    cout << "Sorted array: ";
    printArray(arr);
    return 0;
}
```

This code defines functions for heapify, heap sort, and printing the array. In the main function, you can see an example of how to use heap sort to sort an array of integers.

### 1. Algorithms & Data Structures (C++): Heap Sort function(Source Code)

Sure, here's a simple implementation of Heap Sort in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to heapify a subtree rooted at index 'root'
void heapify(vector<int>& arr, int n, int root) {
    int largest = root; // Initialize largest as root
    int left = 2 * root + 1; // Left child
    int right = 2 * root + 2; // Right child

    // If left child is larger than root
    if (left < n && arr[left] > arr[largest])
        largest = left;

    // If right child is larger than largest so far
    if (right < n && arr[right] > arr[largest])
        largest = right;

    // If largest is not root
    if (largest != root) {
        swap(arr[root], arr[largest]);
        // Recursively heapify the affected sub-tree
        heapify(arr, n, largest);
    }
}

// Heap sort function
void heapSort(vector<int>& arr) {
    int n = arr.size();

    // Build heap (rearrange array)
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);

    // One by one extract an element from heap
    for (int i = n - 1; i > 0; i--) {
        // Move current root to end
        swap(arr[0], arr[i]);
        // Call max heapify on the reduced heap
        heapify(arr, i, 0);
    }
}

// Function to print an array
void printArray(const vector<int>& arr) {
    for (int i : arr)
        cout << i << " ";
    cout << endl;
}

int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    cout << "Original array: ";
    printArray(arr);

    heapSort(arr);

    cout << "Sorted array: ";
    printArray(arr);
    
    return 0;
}
```

This code defines the `heapify`, `heapSort`, `printArray`, and `main` functions. The `heapify` function is used to maintain the heap property of a subtree, `heapSort` sorts the array using heap sort algorithm, and `printArray` is a utility function to print the elements of the array. Finally, `main` function initializes an array, sorts it using heap sort, and prints the sorted array.

### 1. Algorithms & Data Structures (C++): Heap Sort Usng Heapify Process

Heap sort is a comparison-based sorting algorithm that leverages the properties of a binary heap data structure. The process involves two main steps: heapify and sorting. Here's how you can implement heap sort in C++ using the heapify process:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Heapify a subtree rooted with node i which is an index in arr[]
void heapify(vector<int>& arr, int n, int i) {
    int largest = i; // Initialize largest as root
    int left = 2 * i + 1; // left child = 2*i + 1
    int right = 2 * i + 2; // right child = 2*i + 2

    // If left child is larger than root
    if (left < n && arr[left] > arr[largest])
        largest = left;

    // If right child is larger than largest so far
    if (right < n && arr[right] > arr[largest])
        largest = right;

    // If largest is not root
    if (largest != i) {
        swap(arr[i], arr[largest]);

        // Recursively heapify the affected sub-tree
        heapify(arr, n, largest);
    }
}

// Main function to do heap sort
void heapSort(vector<int>& arr) {
    int n = arr.size();

    // Build heap (rearrange array)
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);

    // One by one extract an element from heap
    for (int i = n - 1; i > 0; i--) {
        // Move current root to end
        swap(arr[0], arr[i]);

        // call max heapify on the reduced heap
        heapify(arr, i, 0);
    }
}

// Function to print an array
void printArray(vector<int>& arr) {
    for (const int& elem : arr)
        cout << elem << " ";
    cout << endl;
}

int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    cout << "Original array: ";
    printArray(arr);

    heapSort(arr);

    cout << "Sorted array: ";
    printArray(arr);
    return 0;
}
```

In this implementation, `heapify()` is a recursive function to heapify a subtree rooted with the node `i` which is an index in `arr[]`. `heapSort()` builds a heap, then repeatedly extracts the maximum element from the heap and puts it at the end of the array. Finally, `printArray()` function is used to print the elements of the array.

### 1. Algorithms & Data Structures (C++): Heap Sort: Theory

Heap Sort is a comparison-based sorting algorithm that operates by first constructing a heap from the input array and then repeatedly extracting the maximum (for a max-heap) or minimum (for a min-heap) element from the heap and rebuilding the heap with the remaining elements. The process continues until the heap is empty, resulting in a sorted array.

### Theory

1. **Heap Construction**:
   - The first step of Heap Sort is to build a heap from the input array. This heap can be constructed in-place within the array itself.
   - The heap construction process involves rearranging the elements in the array to satisfy the heap property, which states that each parent node must be greater (for max-heap) or smaller (for min-heap) than or equal to its children.
   - Starting from the last non-leaf node (index n/2 - 1), the algorithm performs heapify operation to ensure that each subtree rooted at that node is a heap.

2. **Heapify Operation**:
   - The heapify operation is crucial for maintaining the heap property. It sifts down a node to its correct position in the heap, assuming that the subtrees rooted at its children already satisfy the heap property.
   - In each iteration, the node compares itself with its children and swaps places with the larger (for max-heap) or smaller (for min-heap) child if necessary. This process continues recursively until the node is in its proper place.

3. **Sorting**:
   - Once the heap is constructed, the maximum (or minimum) element, which is always the root of the heap, is extracted and placed at the end of the array.
   - After extraction, the heap property might be violated, so the heap is reconstructed using the remaining elements.
   - This process is repeated until all elements have been extracted from the heap, resulting in a sorted array.

### Algorithm Steps

1. Build a heap from the input array.
2. Repeatedly extract the maximum (or minimum) element from the heap and rebuild the heap with the remaining elements.
3. Continue until the heap is empty.

### Time Complexity

- The time complexity of Heap Sort is O(n log n) in all cases, where n is the number of elements in the input array.
- The heap construction phase takes O(n) time.
- Each call to heapify operation takes O(log n) time.
- Since heapify is called n times, the total time complexity is O(n log n).

### Space Complexity

- Heap Sort has a space complexity of O(1) since it operates in-place, using only a constant amount of extra space regardless of the input size.

### 1. Algorithms & Data Structures (C++): Heap Sort/Tim Sort

Heap Sort and Tim Sort are two popular sorting algorithms, each with its own characteristics and advantages.

**Heap Sort:**
Heap Sort is a comparison-based sorting technique that builds a heap from the input data and repeatedly extracts the maximum (for a max-heap) and places it at the end of the array. It then reduces the size of the heap and continues the process until the heap is empty. The main steps of Heap Sort are:

1. Build a max heap from the input data.
2. Swap the root (maximum element) of the heap with the last element of the heap.
3. Reduce the size of the heap by one.
4. Heapify the root of the heap to maintain the heap property.
5. Repeat steps 2-4 until the heap is empty.

Heap Sort has a time complexity of O(n log n) in the worst case, making it efficient for large datasets. However, it is not stable, meaning that the relative order of equal elements may not be preserved.

Here's a basic implementation of Heap Sort in C++:

```cpp
#include <iostream>
#include <algorithm>

void heapify(int arr[], int n, int i) {
    int largest = i; 
    int l = 2 * i + 1; 
    int r = 2 * i + 2; 

    if (l < n && arr[l] > arr[largest])
        largest = l;

    if (r < n && arr[r] > arr[largest])
        largest = r;

    if (largest != i) {
        std::swap(arr[i], arr[largest]);
        heapify(arr, n, largest);
    }
}

void heapSort(int arr[], int n) {
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);

    for (int i = n - 1; i > 0; i--) {
        std::swap(arr[0], arr[i]);
        heapify(arr, i, 0);
    }
}

int main() {
    int arr[] = {12, 11, 13, 5, 6, 7};
    int n = sizeof(arr) / sizeof(arr[0]);

    heapSort(arr, n);

    std::cout << "Sorted array: ";
    for (int i = 0; i < n; i++)
        std::cout << arr[i] << " ";
    std::cout << std::endl;

    return 0;
}
```

**Tim Sort:**
Tim Sort is a hybrid sorting algorithm derived from merge sort and insertion sort. It divides the array into small blocks, known as runs, sorts them using insertion sort, and then merges the runs using merge sort. Tim Sort is efficient for both small and large datasets and has a time complexity of O(n log n) in the worst case. It is stable, meaning that the relative order of equal elements is preserved.

Tim Sort is the default sorting algorithm in Python's built-in sort() function and Java's Arrays.sort() method.

Here's a basic overview of how Tim Sort works:

1. Divide the array into small runs using insertion sort.
2. Merge the runs using merge sort to produce new sorted runs.
3. Repeat steps 1 and 2 until the entire array is sorted.

Unfortunately, a concise implementation of Tim Sort in C++ is quite complex due to its intricate nature. It involves a lot of details such as run detection, merge operations, and optimizations to handle various edge cases efficiently. However, you can find full implementations of Tim Sort available in various libraries and online resources.

### 1. Algorithms & Data Structures (C++): Idea behind Quick Sort

Quick Sort is a highly efficient sorting algorithm that follows the Divide and Conquer strategy. Here's a breakdown of its main idea:

1. **Divide**: The first step in Quick Sort is to select a "pivot" element from the array. This pivot can be chosen in various ways, such as the first element, the last element, the middle element, or a randomly selected element. The choice of pivot influences the performance of the algorithm.

2. **Partition**: Once the pivot is selected, the array is partitioned into two sub-arrays. Elements smaller than the pivot are placed to its left, and elements greater than the pivot are placed to its right. At the end of this step, the pivot is in its final sorted position.

3. **Conquer**: Recursively apply the above steps to the sub-arrays on the left and right of the pivot until the entire array is sorted.

4. **Combine**: No combining step is needed in Quick Sort as the sorting is done in place.

Here's a high-level overview of the Quick Sort algorithm in pseudocode:

```bash
function quickSort(arr, low, high):
    if low < high:
        pivotIndex = partition(arr, low, high)
        quickSort(arr, low, pivotIndex - 1)  // Recursively sort elements before pivot
        quickSort(arr, pivotIndex + 1, high) // Recursively sort elements after pivot

function partition(arr, low, high):
    pivot = arr[high]  // Choose the last element as the pivot
    i = low - 1        // Index of smaller element
    for j = low to high - 1:
        if arr[j] <= pivot:
            i = i + 1
            swap arr[i] and arr[j]
    swap arr[i + 1] and arr[high] // Place the pivot element in its correct position
    return i + 1
```

Quick Sort has an average-case time complexity of O(n log n), which makes it one of the fastest sorting algorithms. However, in the worst-case scenario (when the pivot selection is poor), it can degrade to O(n^2). To mitigate this, various techniques like choosing a random pivot or using the "median-of-three" pivot selection can be employed. Despite this drawback, Quick Sort is widely used in practice due to its simplicity and high average-case performance.

### 1. Algorithms & Data Structures (C++): Implementation of Heap Sort

Sure, I can provide you with a simple implementation of Heap Sort in C++. Heap Sort is a comparison-based sorting algorithm that builds a max heap (for ascending order sorting) or a min heap (for descending order sorting) from the array and then repeatedly extracts the maximum (or minimum) element from the heap and rebuilds the heap until the array is sorted.

Here's a C++ implementation of Heap Sort:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to heapify a subtree rooted with node i which is an index in vector arr[]
// n is size of heap
template<typename T>
void heapify(vector<T>& arr, int n, int i) {
    int largest = i; // Initialize largest as root
    int left = 2 * i + 1; // left = 2*i + 1
    int right = 2 * i + 2; // right = 2*i + 2

    // If left child is larger than root
    if (left < n && arr[left] > arr[largest])
        largest = left;

    // If right child is larger than largest so far
    if (right < n && arr[right] > arr[largest])
        largest = right;

    // If largest is not root
    if (largest != i) {
        swap(arr[i], arr[largest]);

        // Recursively heapify the affected sub-tree
        heapify(arr, n, largest);
    }
}

// main function to do heap sort
template<typename T>
void heapSort(vector<T>& arr) {
    int n = arr.size();

    // Build heap (rearrange array)
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);

    // One by one extract an element from heap
    for (int i = n - 1; i > 0; i--) {
        // Move current root to end
        swap(arr[0], arr[i]);

        // call max heapify on the reduced heap
        heapify(arr, i, 0);
    }
}

// Function to print an array
template<typename T>
void printArray(const vector<T>& arr) {
    for (const auto& element : arr) {
        cout << element << " ";
    }
    cout << endl;
}

int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    cout << "Original array: ";
    printArray(arr);

    heapSort(arr);

    cout << "Sorted array: ";
    printArray(arr);

    return 0;
}
```

This code defines the `heapify` function which maintains the heap property and the `heapSort` function which builds a heap and repeatedly extracts the maximum element from the heap to get a sorted array. The `printArray` function is just a utility to print the elements of the array. Finally, in the `main` function, an array is initialized, sorted using Heap Sort, and then printed.

### 1. Algorithms & Data Structures (C++): Implementation Of Topological Sort

Certainly! Topological sorting is a way of arranging the vertices of a directed graph such that for every directed edge from vertex u to vertex v, u comes before v in the ordering. This ordering is not unique, but any valid topological ordering is suitable.

Here's a basic implementation of topological sort in C++ using depth-first search (DFS) algorithm:

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

// Class representing a directed graph using adjacency list representation
class Graph {
    int V; // Number of vertices

    // Pointer to an array containing adjacency lists
    vector<int> *adj;

    // A recursive function used by topologicalSort
    void topologicalSortUtil(int v, vector<bool> &visited, stack<int> &Stack);

public:
    Graph(int V); // Constructor

    // Function to add an edge to the graph
    void addEdge(int v, int w);

    // Prints a topological sort of the complete graph
    void topologicalSort();
};

Graph::Graph(int V) {
    this->V = V;
    adj = new vector<int>[V];
}

void Graph::addEdge(int v, int w) {
    adj[v].push_back(w); // Add w to v’s list
}

void Graph::topologicalSortUtil(int v, vector<bool> &visited, stack<int> &Stack) {
    // Mark the current node as visited
    visited[v] = true;

    // Recur for all the vertices adjacent to this vertex
    for (auto i = adj[v].begin(); i != adj[v].end(); ++i)
        if (!visited[*i])
            topologicalSortUtil(*i, visited, Stack);

    // Push current vertex to stack which stores result
    Stack.push(v);
}

// The function to do Topological Sort. It uses recursive topologicalSortUtil()
void Graph::topologicalSort() {
    stack<int> Stack;

    // Mark all the vertices as not visited
    vector<bool> visited(V, false);

    // Call the recursive helper function to store Topological Sort starting from all vertices one by one
    for (int i = 0; i < V; i++)
        if (visited[i] == false)
            topologicalSortUtil(i, visited, Stack);

    // Print contents of stack
    while (!Stack.empty()) {
        cout << Stack.top() << " ";
        Stack.pop();
    }
}

// Main function
int main() {
    // Create a graph given in the above diagram
    Graph g(6);
    g.addEdge(5, 2);
    g.addEdge(5, 0);
    g.addEdge(4, 0);
    g.addEdge(4, 1);
    g.addEdge(2, 3);
    g.addEdge(3, 1);

    cout << "Topological Sort of the given graph: ";
    g.topologicalSort();
    cout << endl;

    return 0;
}
```

This program demonstrates the topological sorting for a given directed graph using adjacency list representation. You can create a `Graph` object, add edges using `addEdge()` function, and then call `topologicalSort()` function to get the topological ordering of the vertices.

### 1. Algorithms & Data Structures (C++): Inbuilt Sort : Standard Template Library (STL)

In C++, the Standard Template Library (STL) provides efficient implementations of various algorithms and data structures. One commonly used algorithm is sorting, and it's implemented in the `<algorithm>` header. The most commonly used sorting algorithm in the STL is the introsort, which is a hybrid sorting algorithm that combines quicksort, heapsort, and insertion sort.

Here's a simple example of how to use the inbuilt sort function from the STL to sort a vector of integers:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> numbers = {5, 2, 8, 1, 9, 3};

    // Sorting the vector using inbuilt sort function
    std::sort(numbers.begin(), numbers.end());

    // Printing the sorted vector
    std::cout << "Sorted numbers: ";
    for (int num : numbers) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this example:

- We include the necessary headers: `<iostream>` for input and output, `<vector>` for the vector container, and `<algorithm>` for the sort function.
- We define a vector of integers `numbers`.
- We use `std::sort()` function to sort the vector. It takes two iterators denoting the range to be sorted, which in this case are `numbers.begin()` (iterator pointing to the beginning of the vector) and `numbers.end()` (iterator pointing to the end of the vector).
- Finally, we print the sorted vector.

The `std::sort()` function is very versatile and can be used to sort various types of containers (arrays, vectors, lists, etc.) and even user-defined types if the comparison operator (`operator`) is properly defined. It's highly efficient and generally performs well in most situations. However, it's worth noting that for specific scenarios or data distributions, other sorting algorithms might be more suitable.

### 1. Algorithms & Data Structures (C++): Inbuilt Sort & Comparators

In C++, the standard library provides powerful tools for sorting data structures efficiently. The `sort()` function from the `<algorithm>` header is commonly used for this purpose. When sorting custom data types or sorting based on specific criteria, you can use comparators.

Here's a basic example of using `sort()` with custom comparators:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Define a custom data type
struct Person {
    string name;
    int age;
};

// Comparator function to sort persons by age
bool compareByAge(const Person &a, const Person &b) {
    return a.age < b.age;
}

int main() {
    vector<Person> people = {{"Alice", 25}, {"Bob", 20}, {"Charlie", 30}};

    // Sort people by age using the compareByAge function
    sort(people.begin(), people.end(), compareByAge);

    // Output sorted list
    for (const auto &person : people) {
        cout << person.name << " " << person.age << endl;
    }

    return 0;
}
```

In this example, we define a custom data type `Person` with attributes `name` and `age`. We also define a comparator function `compareByAge` which compares two `Person` objects based on their age. Then, in the `main()` function, we sort a vector of `Person` objects using `sort()` and providing `compareByAge` as the comparator function.

You can define comparators for various sorting criteria based on your requirements. For example, you might want to sort objects in descending order, based on a different attribute, or according to some custom logic. Just define the appropriate comparator function and pass it to the `sort()` function.

### 1. Algorithms & Data Structures (C++): Insertion sort

Sure! Insertion sort is a simple sorting algorithm that builds the final sorted array (or list) one item at a time. It iterates through the input data, removing one element each time and then finding the location where that element belongs within the already-sorted part of the array and inserting it there. Here's a simple implementation of insertion sort in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void insertionSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 1; i < n; ++i) {
        int key = arr[i];
        int j = i - 1;

        // Move elements of arr[0..i-1], that are greater than key,
        // to one position ahead of their current position
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}

int main() {
    vector<int> arr = {12, 11, 13, 5, 6};
    insertionSort(arr);
    cout << "Sorted array: ";
    for (int i = 0; i < arr.size(); ++i)
        cout << arr[i] << " ";
    cout << endl;
    return 0;
}
```

This C++ code snippet defines the `insertionSort` function that takes a reference to a vector of integers and sorts it using the insertion sort algorithm. The `main` function demonstrates how to use this function by sorting a sample array and printing the sorted result.

In each iteration of the outer loop (from `i = 1` to `n-1`), the algorithm selects the current element (`key`) and compares it with the elements before it in the sorted subarray. It then shifts the larger elements one position to the right to make space for inserting the `key` at the correct position.

Insertion sort has an average and worst-case time complexity of O(n^2), making it inefficient on large lists, but it's often used for small data sets or as a component in more complex algorithms.

### 1. Algorithms & Data Structures (C++): Insertion Sort (Implementation)

Sure! Here's a simple implementation of the Insertion Sort algorithm in C++:

```cpp
#include <iostream>
#include <vector>

void insertionSort(std::vector<int>& arr) {
    int n = arr.size();
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

int main() {
    std::vector<int> arr = {12, 11, 13, 5, 6};
    
    std::cout << "Original array: ";
    for (int num : arr) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
    
    insertionSort(arr);
    
    std::cout << "Sorted array: ";
    for (int num : arr) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
    
    return 0;
}
```

This code defines the `insertionSort` function which takes a reference to a vector of integers and sorts it using the Insertion Sort algorithm. Then, in the `main` function, an example array is declared, sorted using the `insertionSort` function, and then printed out to demonstrate the sorting.

### 1. Algorithms & Data Structures (C++): Insertion Sort (Theory)

Insertion Sort is a simple sorting algorithm that builds the final sorted array (or list) one item at a time. It is efficient for sorting small data sets or nearly sorted data sets. Insertion Sort works by iteratively moving elements from unsorted part to sorted part of the array until the whole array is sorted.

Here's a brief overview of how Insertion Sort works:

1. **Start with the second element**: The first element in the array is considered to be sorted. So, we start the iteration from the second element.

2. **Compare with previous elements**: Take the next unsorted element and compare it with the elements in the sorted sub-array, starting from the rightmost element of the sorted sub-array.

3. **Insert the element in the correct position**: Move all the elements in the sorted sub-array that are greater than the value of the current unsorted element one position to the right. This creates space for the current element to be inserted in its correct position.

4. **Repeat until all elements are sorted**: Repeat steps 2 and 3 until all elements in the array are sorted.

The time complexity of Insertion Sort is O(n^2) in the worst-case scenario and O(n) in the best-case scenario when the array is already sorted. However, its simplicity and low overhead make it a good choice for sorting small arrays or arrays where the elements are almost sorted.

Here's a simple implementation of Insertion Sort in C++:

```cpp
#include <iostream>
using namespace std;

void insertionSort(int arr[], int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        
        // Move elements of arr[0..i-1], that are greater than key, to one position ahead of their current position
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}

// Function to print an array
void printArray(int arr[], int n) {
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
}

int main() {
    int arr[] = {12, 11, 13, 5, 6};
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Original array: ";
    printArray(arr, n);

    insertionSort(arr, n);

    cout << "Sorted array: ";
    printArray(arr, n);

    return 0;
}
```

This implementation sorts an array of integers using Insertion Sort. You can replace the array `arr` with any other array you want to sort.

### 1. Algorithms & Data Structures (C++): Insertion Sort Function Code and it's tracing

Sure, here's a C++ implementation of the Insertion Sort algorithm along with tracing comments to help you understand how the algorithm works step by step:

```cpp
#include <iostream>
#include <vector>

void insertionSort(std::vector<int> &arr) {
    int n = arr.size();
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;

        // Move elements of arr[0..i-1], that are greater than key,
        // to one position ahead of their current position
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;

        // Trace the current state of the array after each iteration
        std::cout << "Pass " << i << ": ";
        for (int k = 0; k < n; k++) {
            std::cout << arr[k] << " ";
        }
        std::cout << std::endl;
    }
}

int main() {
    std::vector<int> arr = {12, 11, 13, 5, 6};
    std::cout << "Original array: ";
    for (int i = 0; i < arr.size(); i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    insertionSort(arr);

    std::cout << "Sorted array: ";
    for (int i = 0; i < arr.size(); i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

This code sorts an array of integers using the Insertion Sort algorithm. The `insertionSort` function takes a vector of integers as input and sorts it in ascending order.

Here's how the tracing works:

- After each iteration of the outer loop, the function prints the current state of the array.
- For example, after the first iteration, it prints the array after the first element has been inserted in its correct position. After the second iteration, it prints the array after the first two elements have been inserted in their correct positions, and so on.

You can run this code to see the sorting process step by step.

### 1. Algorithms & Data Structures (C++): Insertion Sort of Linked List

Sure! Here's a simple implementation of insertion sort for a singly linked list in C++:

```cpp
#include <iostream>

// Node structure for a singly linked list
struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

// Function to insert a new node at the beginning of a linked list
void insertAtBeginning(Node*& head, int val) {
    Node* newNode = new Node(val);
    newNode->next = head;
    head = newNode;
}

// Function to print the linked list
void printList(Node* head) {
    while (head != nullptr) {
        std::cout << head->data << " ";
        head = head->next;
    }
    std::cout << std::endl;
}

// Function to perform insertion sort on a linked list
void insertionSortLinkedList(Node*& head) {
    if (head == nullptr || head->next == nullptr)
        return;

    Node* sorted = nullptr;
    Node* current = head;

    while (current != nullptr) {
        Node* nextNode = current->next;
        
        // Insert current node into sorted list
        if (sorted == nullptr || sorted->data >= current->data) {
            current->next = sorted;
            sorted = current;
        } else {
            Node* temp = sorted;
            while (temp->next != nullptr && temp->next->data < current->data) {
                temp = temp->next;
            }
            current->next = temp->next;
            temp->next = current;
        }

        current = nextNode;
    }

    head = sorted;
}

// Function to delete the linked list to avoid memory leaks
void deleteList(Node*& head) {
    while (head != nullptr) {
        Node* temp = head;
        head = head->next;
        delete temp;
    }
}

int main() {
    Node* head = nullptr;

    // Example usage
    insertAtBeginning(head, 5);
    insertAtBeginning(head, 3);
    insertAtBeginning(head, 7);
    insertAtBeginning(head, 1);
    insertAtBeginning(head, 9);

    std::cout << "Original list: ";
    printList(head);

    insertionSortLinkedList(head);

    std::cout << "Sorted list: ";
    printList(head);

    // Clean up memory
    deleteList(head);

    return 0;
}
```

This implementation inserts each element from the input list into the sorted part of the list, moving from left to right. It maintains a 'sorted' pointer that points to the beginning of the sorted list and a 'current' pointer that iterates through the unsorted part of the list.

### 1. Algorithms & Data Structures (C++): Insertion Sort Time Complexity

Insertion Sort is a simple sorting algorithm that builds the final sorted array (or list) one item at a time. It iterates over each element in the array, and for each element, it finds the correct position in the already sorted part of the array and inserts it there.

The time complexity of Insertion Sort can be analyzed in terms of the number of comparisons and the number of swaps it performs.

1. **Comparisons**: In the worst-case scenario, when the input array is in reverse sorted order, Insertion Sort will make \(1 + 2 + 3 + \ldots + (n-1)\) comparisons, which sums up to \(\frac{n(n-1)}{2}\). Therefore, the worst-case time complexity for comparisons is \(O(n^2)\).

2. **Swaps (or Shifts)**: In the worst-case scenario, when the input array is in reverse sorted order, each element will need to be shifted to its correct position in every step. In this case, Insertion Sort performs \(1 + 2 + 3 + \ldots + (n-1)\) swaps, which also sums up to \(\frac{n(n-1)}{2}\). Thus, the worst-case time complexity for swaps is also \(O(n^2)\).

Overall, the time complexity of Insertion Sort is \(O(n^2)\) in the worst case, where \(n\) is the number of elements in the array.

However, in the best-case scenario, when the input array is already sorted, the time complexity reduces to \(O(n)\) because it only needs to iterate through the array once to check that each element is in the correct position.

In terms of space complexity, Insertion Sort is an in-place sorting algorithm, meaning it doesn't require any extra space other than a constant amount of additional memory for variables. So, its space complexity is \(O(1)\).

### 1. Algorithms & Data Structures (C++): Insertion Sort: Big O

The time complexity of insertion sort, expressed in Big O notation, is O(n^2) in the worst-case scenario, O(n) in the best-case scenario, and O(n^2) in the average case.

- **Worst-case scenario**: In the worst case, where the input array is in reverse sorted order, insertion sort needs to perform maximum comparisons and swaps for each element. This results in a quadratic time complexity, O(n^2).

- **Best-case scenario**: In the best case, when the input array is already sorted, insertion sort requires only one comparison per element but still needs to iterate through each element. Hence, it has a linear time complexity, O(n).

- **Average-case scenario**: In the average case, insertion sort requires roughly O(n^2) operations, similar to the worst-case scenario, as it's not making any assumptions about the input data distribution.

Insertion sort is generally considered efficient for small data sets or nearly sorted data due to its simplicity and low overhead. However, it becomes inefficient for large data sets due to its quadratic time complexity.

### 1. Algorithms & Data Structures (C++): Iterative Merge Sort

Iterative Merge Sort is an alternative implementation of the classic Merge Sort algorithm that avoids recursion by using an iterative approach. Here's a basic implementation of Iterative Merge Sort in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Merge function to merge two sorted subarrays arr[l..m] and arr[m+1..r]
void merge(vector<int>& arr, int l, int m, int r) {
    int n1 = m - l + 1;
    int n2 = r - m;

    // Create temporary arrays
    vector<int> L(n1), R(n2);

    // Copy data to temporary arrays L[] and R[]
    for (int i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[m + 1 + j];

    // Merge the temporary arrays back into arr[l..r]
    int i = 0, j = 0, k = l;
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

    // Copy the remaining elements of L[], if any
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    // Copy the remaining elements of R[], if any
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

// Iterative Merge Sort function to sort an array using mergeSort
void iterativeMergeSort(vector<int>& arr) {
    int n = arr.size();
    int curr_size;  // For current size of subarrays to be merged
    int left_start; // For picking starting index of left subarray to be merged

    // Merge subarrays in bottom up manner
    for (curr_size = 1; curr_size <= n-1; curr_size *= 2) {
        // Pick starting point of different subarrays of current size
        for (left_start = 0; left_start < n-1; left_start += 2*curr_size) {
            // Find ending point of left subarray. mid+1 is starting point of right
            int mid = min(left_start + curr_size - 1, n-1);
            int right_end = min(left_start + 2*curr_size - 1, n-1);
            // Merge subarrays arr[left_start...mid] & arr[mid+1...right_end]
            merge(arr, left_start, mid, right_end);
        }
    }
}

// Function to print an array
void printArray(const vector<int>& arr) {
    for (int i = 0; i < arr.size(); i++)
        cout << arr[i] << " ";
    cout << endl;
}

int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    cout << "Given array is \n";
    printArray(arr);

    iterativeMergeSort(arr);

    cout << "\nSorted array is \n";
    printArray(arr);
    return 0;
}
```

In this implementation, the `merge()` function is responsible for merging two sorted subarrays. The `iterativeMergeSort()` function sorts the array by iteratively dividing it into smaller subarrays and merging them. Finally, the `main()` function demonstrates how to use the Iterative Merge Sort algorithm by sorting a sample array.

### 1. Algorithms & Data Structures (C++): Merge sort

Merge sort is a classic divide-and-conquer algorithm used for sorting arrays or lists. It works by dividing the input array into two halves, sorting each half recursively, and then merging the sorted halves. Here's a simple implementation of merge sort in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Merge two sorted subarrays into one sorted array
void merge(vector<int>& arr, int left, int middle, int right) {
    int n1 = middle - left + 1;
    int n2 = right - middle;

    // Create temporary arrays
    vector<int> L(n1), R(n2);

    // Copy data to temporary arrays L[] and R[]
    for (int i = 0; i < n1; i++)
        L[i] = arr[left + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[middle + 1 + j];

    // Merge the temporary arrays back into arr[left..right]
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

    // Copy the remaining elements of L[], if any
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    // Copy the remaining elements of R[], if any
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

// Main function to implement merge sort
void mergeSort(vector<int>& arr, int left, int right) {
    if (left < right) {
        // Same as (left+right)/2, but avoids overflow for large left and right
        int middle = left + (right - left) / 2;

        // Sort first and second halves
        mergeSort(arr, left, middle);
        mergeSort(arr, middle + 1, right);

        // Merge the sorted halves
        merge(arr, left, middle, right);
    }
}

// Utility function to print an array
void printArray(const vector<int>& arr) {
    for (int i = 0; i < arr.size(); i++)
        cout << arr[i] << " ";
    cout << endl;
}

// Driver code
int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    int n = arr.size();

    cout << "Given array is \n";
    printArray(arr);

    mergeSort(arr, 0, n - 1);

    cout << "Sorted array is \n";
    printArray(arr);
    return 0;
}
```

This implementation defines three main functions:

1. `merge()`: This function merges two sorted subarrays into one sorted array.
2. `mergeSort()`: This function recursively divides the array into halves until each subarray contains only one element, and then merges them back together using the `merge()` function.
3. `printArray()`: This utility function prints the elements of the array.

The `main()` function demonstrates how to use `mergeSort()` to sort an array.

### 1. Algorithms & Data Structures (C++): Merge Sort - Complexity Analysis

Merge Sort is a popular sorting algorithm known for its efficiency and stability. It follows the divide-and-conquer paradigm, breaking down the problem into smaller subproblems, sorting them, and then merging them back together.

Here's a complexity analysis of Merge Sort:

1. **Time Complexity**:
    - Best Case: O(n log n)
    - Average Case: O(n log n)
    - Worst Case: O(n log n)

    Explanation:
    - In Merge Sort, the array is repeatedly divided into halves until individual elements are isolated. This process requires log n recursive calls, where n is the number of elements in the array.
    - At each level of recursion, all n elements are iterated over once for merging. Thus, the time complexity for merging at each level is O(n).
    - As there are log n levels of recursion, the total time complexity is O(n log n) in all cases.

2. **Space Complexity**:
    - Merge Sort is not an in-place sorting algorithm. It requires additional space for the temporary arrays used during the merging process.
    - The space complexity of Merge Sort is O(n) due to the need for auxiliary space for merging.

3. **Stability**:
    - Merge Sort is a stable sorting algorithm, meaning that the relative order of equal elements is preserved after sorting.

4. **Adaptability**:
    - Merge Sort is not adaptive. The time complexity remains the same regardless of the input sequence.

5. **Applications**:
    - Merge Sort is suitable for sorting large datasets efficiently due to its O(n log n) time complexity. It's often used in scenarios where stability is required, such as in external sorting where data is too large to fit into memory.

Overall, Merge Sort's efficient time complexity makes it a popular choice for sorting large datasets, especially when stability and predictability are important factors. However, its space complexity can be a limitation in memory-constrained environments.

### 1. Algorithms & Data Structures (C++): Merge Sort (Implementation)

Sure! Here's a simple implementation of the Merge Sort algorithm in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Merge function to merge two sorted subarrays arr[l..m] and arr[m+1..r]
void merge(vector<int>& arr, int l, int m, int r) {
    int n1 = m - l + 1;
    int n2 = r - m;

    // Create temporary arrays
    vector<int> L(n1), R(n2);

    // Copy data to temporary arrays L[] and R[]
    for (int i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[m + 1 + j];

    // Merge the temporary arrays back into arr[l..r]
    int i = 0, j = 0, k = l;
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

    // Copy the remaining elements of L[], if any
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    // Copy the remaining elements of R[], if any
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

// MergeSort function to sort subarray arr[l..r] using merge()
void mergeSort(vector<int>& arr, int l, int r) {
    if (l < r) {
        // Same as (l+r)/2, but avoids overflow for large l and h
        int m = l + (r - l) / 2;

        // Sort first and second halves
        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);

        // Merge the sorted halves
        merge(arr, l, m, r);
    }
}

// Utility function to print an array
void printArray(const vector<int>& arr) {
    for (int i : arr)
        cout << i << " ";
    cout << endl;
}

int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    int arr_size = arr.size();

    cout << "Given array is \n";
    printArray(arr);

    mergeSort(arr, 0, arr_size - 1);

    cout << "\nSorted array is \n";
    printArray(arr);
    return 0;
}
```

This code defines the merge sort algorithm along with auxiliary functions to merge and print arrays. The `mergeSort` function recursively divides the array into halves until it reaches single-element subarrays, then merges them in sorted order using the `merge` function. Finally, the `main` function demonstrates the usage of the merge sort algorithm by sorting a sample array.

### 1. Algorithms & Data Structures (C++): Merge Sort (Theory)

Merge Sort is a popular sorting algorithm that follows the divide-and-conquer paradigm. It's efficient for sorting large datasets and has a time complexity of O(n log n) in the average and worst cases.

Here's how Merge Sort works:

1. **Divide**: The original array is divided recursively into smaller subarrays until each subarray contains only one element. This process continues until no further division can be made.

2. **Conquer**: After the array is divided into single-element subarrays, these subarrays are merged back together in a sorted manner.

3. **Merge**: During the merge phase, adjacent subarrays are merged together to form larger sorted subarrays. This process continues until the entire array is merged back together, and the final result is a sorted array.

Here's a high-level overview of the Merge Sort algorithm:

```plaintext
mergeSort(arr[], l, r)
1. If l < r
     a. Find the middle point to divide the array into two halves:  
            middle = l + (r-l)/2
     b. Call mergeSort for the first half:   
            mergeSort(arr, l, middle)
     c. Call mergeSort for the second half:
            mergeSort(arr, middle+1, r)
     d. Merge the two halves sorted in step 2b and 2c:
            merge(arr, l, middle, r)

merge(arr[], l, m, r)
1. Create temporary arrays L[] and R[] to hold the left and right subarrays.
2. Copy data to temporary arrays L[] and R[].
3. Merge the temporary arrays back into arr[l..r]:
     a. Initialize indexes i, j, and k to 0.
     b. Until one of the subarrays is exhausted, compare the elements at indexes i and j in L[] and R[] respectively, and place the smaller one in arr[k].
     c. Copy any remaining elements from the temporary arrays back into arr[].
```

The key operation is the merging step, where the two sorted subarrays are combined into a single sorted array. This step is what gives Merge Sort its efficiency, as it's done in linear time.

In C++, the implementation might look like this:

```cpp
#include <iostream>
using namespace std;

void merge(int arr[], int l, int m, int r) {
    int n1 = m - l + 1;
    int n2 = r - m;

    int L[n1], R[n2];

    for (int i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[m + 1 + j];

    int i = 0, j = 0, k = l;
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

    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

void mergeSort(int arr[], int l, int r) {
    if (l < r) {
        int m = l + (r - l) / 2;

        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);

        merge(arr, l, m, r);
    }
}

int main() {
    int arr[] = {12, 11, 13, 5, 6, 7};
    int arr_size = sizeof(arr) / sizeof(arr[0]);

    cout << "Given array is \n";
    for (int i = 0; i < arr_size; i++)
        cout << arr[i] << " ";
    cout << endl;

    mergeSort(arr, 0, arr_size - 1);

    cout << "Sorted array is \n";
    for (int i = 0; i < arr_size; i++)
        cout << arr[i] << " ";
    cout << endl;
    return 0;
}
```

This code demonstrates how to implement Merge Sort in C++ and use it to sort an array.

### 1. Algorithms & Data Structures (C++): Merge Sort Analysis

Merge sort is a classic divide-and-conquer algorithm for sorting arrays or lists. It works by recursively dividing the input array into smaller subarrays, sorting each subarray, and then merging the sorted subarrays to produce the final sorted array. Here's a brief analysis of the merge sort algorithm:

#### Time Complexity

- **Best Case:** O(n log n)
- **Average Case:** O(n log n)
- **Worst Case:** O(n log n)

The time complexity of merge sort is consistent across all cases because it always divides the array in half and merges the subarrays in linear time. Even in the worst-case scenario, merge sort performs at O(n log n) time complexity.

#### Space Complexity

- **O(n)**

Merge sort requires additional space to store temporary arrays during the merging process. The space complexity is O(n) because it needs space proportional to the size of the input array for storing temporary data.

#### Stability

Merge sort is stable. This means that it preserves the relative order of equal elements in the sorted output as they appeared in the original unsorted input.

#### Divide-and-Conquer

Merge sort follows the divide-and-conquer paradigm. It recursively divides the input array into smaller subarrays until each subarray contains only one element (which is already sorted by definition), and then merges these sorted subarrays to produce a sorted array.

#### Parallelization

Merge sort can be easily parallelized because its divide-and-conquer approach lends itself well to parallel processing. The divide step can be distributed across multiple processors, and the merging step can be performed concurrently once the subarrays are sorted.

#### Adaptive

Merge sort is not adaptive in the sense that it doesn't take advantage of existing order in the input array. It always divides the array into halves regardless of the input. However, its performance is consistent and efficient regardless of the input distribution.

Overall, merge sort is a highly efficient sorting algorithm with a stable performance profile, making it suitable for a wide range of applications where sorting large datasets is required.

### 1. Algorithms & Data Structures (C++): Merge Sort and O(n log n)

Merge Sort is a popular sorting algorithm that follows the divide and conquer strategy. It has a time complexity of O(n log n) in the average and worst-case scenarios, making it efficient for sorting large datasets. Here's how Merge Sort works in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Merge two sorted subarrays into one sorted array
void merge(vector<int>& arr, int left, int middle, int right) {
    int n1 = middle - left + 1;
    int n2 = right - middle;

    // Create temporary arrays
    vector<int> L(n1), R(n2);

    // Copy data to temporary arrays L[] and R[]
    for (int i = 0; i < n1; i++)
        L[i] = arr[left + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[middle + 1 + j];

    // Merge the temporary arrays back into arr[left..right]
    int i = 0, j = 0, k = left;
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

    // Copy the remaining elements of L[], if any
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    // Copy the remaining elements of R[], if any
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

// Merge Sort function
void mergeSort(vector<int>& arr, int left, int right) {
    if (left < right) {
        // Same as (left + right) / 2, but avoids overflow for large left and right
        int middle = left + (right - left) / 2;

        // Sort first and second halves
        mergeSort(arr, left, middle);
        mergeSort(arr, middle + 1, right);

        // Merge the sorted halves
        merge(arr, left, middle, right);
    }
}

// Utility function to print an array
void printArray(const vector<int>& arr) {
    for (int i = 0; i < arr.size(); i++)
        cout << arr[i] << " ";
    cout << endl;
}

// Driver code
int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    int n = arr.size();

    cout << "Given array is \n";
    printArray(arr);

    mergeSort(arr, 0, n - 1);

    cout << "Sorted array is \n";
    printArray(arr);

    return 0;
}
```

In this implementation:

1. The `merge()` function merges two sorted subarrays into one sorted array.
2. The `mergeSort()` function recursively divides the array into two halves until the base case (single element) is reached and then merges the sorted halves.
3. The `printArray()` function is a utility function to print the elements of an array.
4. In the `main()` function, you can see an example of how to use Merge Sort to sort an array of integers.

This implementation sorts the given array `[12, 11, 13, 5, 6, 7]` using Merge Sort and prints the sorted array.

### 1. Algorithms & Data Structures (C++): Merge Sort Complexity Analysis

Sure! Let's break down the complexity analysis of the merge sort algorithm.

Merge sort is a divide-and-conquer algorithm that works as follows:

1. **Divide**: The array to be sorted is divided into two halves.
2. **Conquer**: Recursively sort the two halves.
3. **Combine**: Merge the sorted halves back together into a single sorted array.

Here's the complexity analysis:

#### Time Complexity

1. **Divide Step**: This step involves dividing the array into two halves. This step has a time complexity of O(1) because it only involves some pointer manipulation.

2. **Conquer Step**: This step involves recursively sorting the two halves of the array. Since the array is divided into two halves each time, the time complexity of this step can be expressed by the recurrence relation T(n) = 2T(n/2), where n is the size of the array. This step has a time complexity of O(n log n) because the array size is halved at each recursive step.

3. **Combine Step**: This step involves merging the two sorted halves of the array. The time complexity of this step is O(n) because each element of the array is visited once during the merging process.

Overall, the time complexity of merge sort is O(n log n).

#### Space Complexity

Merge sort is not an in-place sorting algorithm, meaning it requires additional space proportional to the size of the input array. This additional space is required for the temporary arrays used during the merging process. The space complexity of merge sort is O(n) where n is the size of the input array.

In summary, merge sort has a time complexity of O(n log n) and a space complexity of O(n).

### 1. Algorithms & Data Structures (C++): Merge Sort on Linked List

Sure, I can guide you through implementing Merge Sort on a Linked List in C++. Here's a step-by-step explanation along with the code:

1. **Define the Node Structure**: First, define the structure of a node in the linked list. Each node will contain the data and a pointer to the next node.

```cpp
struct Node {
    int data;
    Node* next;
};
```

1. **Split the List**: Write a function to split the linked list into two halves. You can use the fast and slow pointer technique to find the middle of the list.

1. **Merge Function**: Write a function to merge two sorted linked lists into one sorted list.

1. **Merge Sort Function**: Write a recursive function to implement merge sort on the linked list. This function will recursively split the list into halves and then merge them back in sorted order.

Here's the C++ code implementing these steps:

```cpp
#include <iostream>

using namespace std;

struct Node {
    int data;
    Node* next;
};

Node* merge(Node* left, Node* right) {
    if (left == nullptr)
        return right;
    if (right == nullptr)
        return left;
    
    Node* result = nullptr;
    if (left->data <= right->data) {
        result = left;
        result->next = merge(left->next, right);
    } else {
        result = right;
        result->next = merge(left, right->next);
    }
    return result;
}

void splitList(Node* head, Node** left, Node** right) {
    Node* slow = head;
    Node* fast = head->next;

    while (fast != nullptr) {
        fast = fast->next;
        if (fast != nullptr) {
            slow = slow->next;
            fast = fast->next;
        }
    }

    *left = head;
    *right = slow->next;
    slow->next = nullptr;
}

void mergeSort(Node** headRef) {
    Node* head = *headRef;
    Node* left;
    Node* right;

    if (head == nullptr || head->next == nullptr) {
        return;
    }

    splitList(head, &left, &right);

    mergeSort(&left);
    mergeSort(&right);

    *headRef = merge(left, right);
}

void push(Node** headRef, int newData) {
    Node* newNode = new Node();
    newNode->data = newData;
    newNode->next = (*headRef);
    (*headRef) = newNode;
}

void printList(Node* node) {
    while (node != nullptr) {
        cout << node->data << " ";
        node = node->next;
    }
    cout << endl;
}

int main() {
    Node* head = nullptr;
    push(&head, 15);
    push(&head, 10);
    push(&head, 5);
    push(&head, 20);
    push(&head, 3);
    push(&head, 2);

    cout << "Linked List before sorting \n";
    printList(head);

    mergeSort(&head);

    cout << "Linked List after sorting \n";
    printList(head);

    return 0;
}
```

This code demonstrates the Merge Sort algorithm on a Linked List. You can create a linked list, push elements into it, then call the `mergeSort` function to sort the list, and finally print the sorted list.

### 1. Algorithms & Data Structures (C++): Merge Sort Space Complexity

The space complexity of merge sort in C++ is O(n) where n is the number of elements in the array being sorted.

In merge sort, additional space is required for the temporary arrays used during the merging phase. These temporary arrays are typically of the same size as the original array being sorted.

During the merge phase of the algorithm, the space complexity increases due to the need for auxiliary arrays to merge the sorted sub-arrays. However, the space required does not increase with the input size beyond a constant factor, which makes the space complexity of merge sort O(n).

This makes merge sort efficient in terms of space usage compared to some other sorting algorithms like quicksort, which may have a space complexity of O(log n) in the worst-case scenario due to the recursive call stack.

### 1. Algorithms & Data Structures (C++): Merge Sort Theory

Merge Sort is a popular sorting algorithm that follows the divide-and-conquer strategy. It efficiently sorts arrays or lists of elements by recursively dividing them into smaller subarrays, sorting those subarrays, and then merging them back together.

Here's a breakdown of how Merge Sort works:

1. **Divide**: The array to be sorted is divided into two halves.
2. **Conquer**: Recursively sort the two halves.
3. **Merge**: Merge the sorted halves to produce a single sorted array.

Let's delve into each step in more detail:

#### Divide

Merge Sort starts by dividing the array into two halves until each subarray contains only one element, as an array with one element is inherently sorted.

#### Conquer

After dividing the array, the sorting process begins. This involves recursively sorting each half of the array until each subarray contains only one element. This process is continued until all subarrays are sorted.

#### Merge

The merge step is where the sorted subarrays are merged back together to form a single sorted array. This is done by comparing the elements from each subarray and placing them in the correct order into a temporary array. Once all elements are merged, the temporary array becomes the sorted array.

#### Pseudocode

Here's a basic pseudocode representation of the Merge Sort algorithm:

```plaintext
MergeSort(array)
    if length of array <= 1
        return array
    else
        middle = length of array / 2
        left_half = MergeSort(first half of array)
        right_half = MergeSort(second half of array)
        return Merge(left_half, right_half)

Merge(left_half, right_half)
    result = empty array
    while left_half is not empty and right_half is not empty
        if first element of left_half <= first element of right_half
            append first element of left_half to result
            remove first element from left_half
        else
            append first element of right_half to result
            remove first element from right_half
    append remaining elements of left_half to result
    append remaining elements of right_half to result
    return result
```

#### Complexity

Merge Sort has a time complexity of O(n log n) in all cases, where n is the number of elements in the array. This is because the array is always divided into two halves, and merging two sorted halves takes linear time. Additionally, Merge Sort is stable, meaning that it preserves the relative order of equal elements in the sorted output.

Overall, Merge Sort is a highly efficient and reliable sorting algorithm, especially for large datasets. However, it does require additional space for the temporary arrays used in the merge step, which can be a drawback for very large arrays.

### 1. Algorithms & Data Structures (C++): Merge Sort Time Complexity

Merge Sort is a popular sorting algorithm known for its efficiency and stability. It follows the divide-and-conquer approach to sort elements. Here's a brief overview of how it works:

1. **Divide**: The unsorted list is divided into two equal halves recursively until there is only one element in each half.
2. **Conquer**: The divided lists are then merged back together in a sorted manner.
3. **Combine**: During the merging process, the elements are compared and arranged in the correct order.

The time complexity of Merge Sort is O(n log n), where 'n' is the number of elements in the array.

Here's why:

1. **Divide Step**: In each division step, the array is halved, which takes O(log n) time because the array is divided into halves until there is only one element in each half.

2. **Merge Step**: Merging two sorted arrays of size 'n/2' each takes O(n) time. Since there are O(log n) levels of recursion and each level takes O(n) time to merge, the total time complexity for the merging step is O(n log n).

Hence, the overall time complexity of Merge Sort is O(n log n). This makes it efficient for sorting large datasets, and it's one of the most widely used sorting algorithms in practice.

### 1. Algorithms & Data Structures (C++): Merge Sort: Big O

Merge Sort is a popular sorting algorithm known for its stable and efficient performance. Its time complexity, often represented using Big O notation, is O(n log n), where 'n' is the number of elements in the array to be sorted.

Here's a brief explanation of why Merge Sort has this time complexity:

1. **Divide**: The array is divided into halves recursively until each sub-array contains only one element. This step takes O(log n) time because the array is divided in half at each level of recursion.

2. **Conquer**: Once the array is divided into single-element sub-arrays, they are merged back together in a sorted manner. Merging two sorted arrays of size 'n/2' each takes O(n) time.

3. **Combine**: As the recursion unfolds, the merging process combines increasingly larger sorted sub-arrays. Since the merging time is proportional to the total number of elements being merged, it takes O(n log n) time overall.

Hence, the overall time complexity of Merge Sort is O(n log n), making it efficient for large datasets. Additionally, Merge Sort is a stable sorting algorithm, meaning it preserves the relative order of equal elements.

### 1. Algorithms & Data Structures (C++): Merge Sort: Merge

In the merge step of the merge sort algorithm, two sorted arrays are merged into a single sorted array. Here's how you can implement the merge function in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void merge(vector<int>& arr, int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;

    // Create temporary arrays
    vector<int> L(n1), R(n2);

    // Copy data to temporary arrays L[] and R[]
    for (int i = 0; i < n1; i++)
        L[i] = arr[left + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[mid + 1 + j];

    // Merge the temporary arrays back into arr[left..right]
    int i = 0, j = 0, k = left;
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

    // Copy the remaining elements of L[], if any
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    // Copy the remaining elements of R[], if any
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    int left = 0;
    int right = arr.size() - 1;
    int mid = left + (right - left) / 2;

    merge(arr, left, mid, right);

    // Print the sorted array
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}
```

This function takes an array `arr` and three indices: `left`, `mid`, and `right`. The array is divided into two parts: `arr[left...mid]` and `arr[mid+1...right]`, and these two parts are merged into a single sorted array. The merging process is done by comparing elements from both arrays and putting the smaller one into the result array until one of the arrays is exhausted. Finally, any remaining elements are copied to the result array.

### 1. Algorithms & Data Structures (C++): Merge Sort: Merge Process

In Merge Sort, the merge process is a crucial step where two sorted arrays are combined into a single sorted array. Here's how it typically works:

1. **Setup**: You have two sorted arrays, often referred to as the left and right arrays. These arrays could be contiguous portions of a larger array being sorted.

2. **Merge Step**: Start with two pointers, one for each array, initialized to the first element of their respective arrays. Compare the elements at these pointers.

3. **Comparison**: Choose the smaller (or larger, depending on the sorting order) of the two elements and place it into the next position of the merged array. Move the pointer of the array from which the element was chosen to the next element.

4. **Repeat**: Continue this process of comparing elements from both arrays and placing the smaller (or larger) one into the merged array until one of the arrays is exhausted.

5. **Final Step**: If any elements are remaining in either of the arrays, simply append them to the end of the merged array, as they are already sorted.

Here's a simplified version of the merge process in C++:

```cpp
void merge(int arr[], int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;

    // Create temporary arrays
    int L[n1], R[n2];

    // Copy data to temporary arrays L[] and R[]
    for (int i = 0; i < n1; i++)
        L[i] = arr[left + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[mid + 1 + j];

    // Merge the temporary arrays back into arr[left..right]
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
```

This function can be called recursively during the merge sort algorithm to merge smaller sorted arrays into larger ones until the entire array is sorted.

### 1. Algorithms & Data Structures (C++): Merge Sorted Arrays

To merge two sorted arrays in C++, you can use a simple approach where you start with empty result array and then iterate through both arrays, comparing elements and inserting them into the result array in sorted order. Here's a basic implementation:

```cpp
#include <iostream>
#include <vector>

std::vector<int> mergeSortedArrays(const std::vector<int>& arr1, const std::vector<int>& arr2) {
    std::vector<int> merged;
    size_t i = 0, j = 0;

    // Merge elements into merged array until one of the arrays is exhausted
    while (i < arr1.size() && j < arr2.size()) {
        if (arr1[i] <= arr2[j]) {
            merged.push_back(arr1[i]);
            ++i;
        } else {
            merged.push_back(arr2[j]);
            ++j;
        }
    }

    // If any elements remain in either array, append them to merged array
    while (i < arr1.size()) {
        merged.push_back(arr1[i]);
        ++i;
    }

    while (j < arr2.size()) {
        merged.push_back(arr2[j]);
        ++j;
    }

    return merged;
}

int main() {
    std::vector<int> arr1 = {1, 3, 5, 7, 9};
    std::vector<int> arr2 = {2, 4, 6, 8, 10};

    std::vector<int> merged = mergeSortedArrays(arr1, arr2);

    std::cout << "Merged array:";
    for (int num : merged) {
        std::cout << " " << num;
    }
    std::cout << std::endl;

    return 0;
}
```

This code snippet defines a function `mergeSortedArrays` that takes two sorted arrays as input and returns a single sorted array by merging the two. In the `main` function, two sorted arrays `arr1` and `arr2` are merged using this function, and the merged array is printed.

### 1. Algorithms & Data Structures (C++): Merge Two Sorted Arrays

Certainly! Merging two sorted arrays efficiently is a fundamental operation in programming. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <vector>

std::vector<int> mergeSortedArrays(const std::vector<int>& arr1, const std::vector<int>& arr2) {
    std::vector<int> mergedArray;
    int i = 0, j = 0;
    
    // Merge arrays until one of them is exhausted
    while (i < arr1.size() && j < arr2.size()) {
        if (arr1[i] <= arr2[j]) {
            mergedArray.push_back(arr1[i]);
            i++;
        } else {
            mergedArray.push_back(arr2[j]);
            j++;
        }
    }
    
    // Add remaining elements from the first array
    while (i < arr1.size()) {
        mergedArray.push_back(arr1[i]);
        i++;
    }
    
    // Add remaining elements from the second array
    while (j < arr2.size()) {
        mergedArray.push_back(arr2[j]);
        j++;
    }
    
    return mergedArray;
}

int main() {
    std::vector<int> arr1 = {1, 3, 5, 7, 9};
    std::vector<int> arr2 = {2, 4, 6, 8, 10};

    std::vector<int> mergedArray = mergeSortedArrays(arr1, arr2);

    std::cout << "Merged Array: ";
    for (int num : mergedArray) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this code:

- We define a function `mergeSortedArrays` that takes two sorted arrays `arr1` and `arr2` as input.
- We initialize an empty vector `mergedArray` to store the merged result.
- We use two pointers `i` and `j` to iterate through `arr1` and `arr2` respectively.
- We compare elements at indices `i` and `j` in both arrays and insert the smaller one into `mergedArray`.
- We then move the pointer of the array from which the element was inserted.
- Finally, we append any remaining elements from both arrays.
- In the `main` function, we demonstrate the usage of the `mergeSortedArrays` function with two example arrays and print the merged array.

### 1. Algorithms & Data Structures (C++): Merge Two Sorted Arrays Theory

Merging two sorted arrays is a fundamental operation in computer science and is commonly used in various algorithms and applications. When you merge two sorted arrays, you combine them into a single sorted array.

Here's the theory behind merging two sorted arrays in C++:

#### Approach

1. **Initialize Indices:** Start with two pointers (or indices) pointing to the beginning of each array.

2. **Compare Elements:** Compare the elements at the current positions of the pointers.

3. **Merge:** Take the smaller (or larger, depending on sorting order) element among the two and add it to the merged array. Move the pointer of the array from which the element is selected to the next position.

4. **Repeat:** Repeat steps 2 and 3 until all elements from both arrays are processed.

5. **Handle Remaining Elements:** If one array becomes empty before the other, simply append the remaining elements of the non-empty array to the merged array.

#### Implementation

Here's a basic implementation of merging two sorted arrays in C++:

```cpp
#include <iostream>
#include <vector>

std::vector<int> mergeSortedArrays(const std::vector<int>& arr1, const std::vector<int>& arr2) {
    std::vector<int> merged;
    int i = 0, j = 0;

    while (i < arr1.size() && j < arr2.size()) {
        if (arr1[i] < arr2[j]) {
            merged.push_back(arr1[i]);
            i++;
        } else {
            merged.push_back(arr2[j]);
            j++;
        }
    }

    // Append remaining elements from arr1
    while (i < arr1.size()) {
        merged.push_back(arr1[i]);
        i++;
    }

    // Append remaining elements from arr2
    while (j < arr2.size()) {
        merged.push_back(arr2[j]);
        j++;
    }

    return merged;
}

int main() {
    std::vector<int> arr1 = {1, 3, 5, 7, 9};
    std::vector<int> arr2 = {2, 4, 6, 8, 10};

    std::vector<int> merged = mergeSortedArrays(arr1, arr2);

    // Print the merged array
    for (int num : merged) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

#### Time Complexity

- The time complexity of merging two sorted arrays is O(n), where n is the total number of elements in the two arrays.

#### Space Complexity

- The space complexity of the above implementation is O(n), where n is the total number of elements in the two arrays. This is because we are creating a new vector to store the merged array.

### 1. Algorithms & Data Structures (C++): Merge Two Sorted Linked List

Sure! Merging two sorted linked lists is a common operation in programming. Here's a C++ implementation of a function to merge two sorted linked lists:

```cpp
#include <iostream>

// Define the structure of a node in the linked list
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

// Function to merge two sorted linked lists
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    // Create a dummy node to start the merged list
    ListNode* dummy = new ListNode(0);
    // Pointer to the current node in the merged list
    ListNode* current = dummy;

    // Traverse both lists until one of them becomes empty
    while (l1 != NULL && l2 != NULL) {
        if (l1->val <= l2->val) {
            current->next = l1;
            l1 = l1->next;
        } else {
            current->next = l2;
            l2 = l2->next;
        }
        current = current->next;
    }

    // Add the remaining nodes from the non-empty list
    current->next = (l1 != NULL) ? l1 : l2;

    // Store the head of the merged list
    ListNode* mergedList = dummy->next;
    // Delete the dummy node
    delete dummy;

    return mergedList;
}

// Function to print a linked list
void printList(ListNode* head) {
    while (head != NULL) {
        std::cout << head->val << " ";
        head = head->next;
    }
    std::cout << std::endl;
}

int main() {
    // Example lists
    ListNode* list1 = new ListNode(1);
    list1->next = new ListNode(3);
    list1->next->next = new ListNode(5);

    ListNode* list2 = new ListNode(2);
    list2->next = new ListNode(4);
    list2->next->next = new ListNode(6);

    std::cout << "List 1: ";
    printList(list1);
    std::cout << "List 2: ";
    printList(list2);

    // Merge the lists
    ListNode* mergedList = mergeTwoLists(list1, list2);

    std::cout << "Merged List: ";
    printList(mergedList);

    return 0;
}
```

In this code:

1. `ListNode` represents a single node in the linked list.
2. `mergeTwoLists` is the function that merges two sorted linked lists. It iterates through both lists and compares the values of the nodes, appending the smaller one to the merged list.
3. `printList` is a utility function to print the elements of a linked list.
4. In the `main` function, two example linked lists `list1` and `list2` are created and merged using the `mergeTwoLists` function. Finally, the merged list is printed.

You can customize the input lists in the `main` function to test with different inputs.

### 1. Algorithms & Data Structures (C++): Merge Two Sorted Linked Lists

Certainly! Merging two sorted linked lists in C++ can be efficiently achieved by iteratively comparing the nodes of both lists and appending them to a new merged list in sorted order. Here's a simple implementation:

```cpp
#include <iostream>

using namespace std;

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        // Dummy node for the result list
        ListNode* dummy = new ListNode(0);
        ListNode* curr = dummy;
        
        // Traverse both lists and merge
        while (l1 != nullptr && l2 != nullptr) {
            if (l1->val < l2->val) {
                curr->next = l1;
                l1 = l1->next;
            } else {
                curr->next = l2;
                l2 = l2->next;
            }
            curr = curr->next;
        }
        
        // Attach remaining nodes
        if (l1 != nullptr)
            curr->next = l1;
        else if (l2 != nullptr)
            curr->next = l2;
        
        // Store the head of the merged list
        ListNode* result = dummy->next;
        delete dummy; // free dummy node
        return result;
    }
};

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
    ListNode* l1 = new ListNode(1);
    l1->next = new ListNode(3);
    l1->next->next = new ListNode(5);

    ListNode* l2 = new ListNode(2);
    l2->next = new ListNode(4);
    l2->next->next = new ListNode(6);

    Solution solution;
    ListNode* mergedList = solution.mergeTwoLists(l1, l2);

    cout << "Merged List: ";
    printList(mergedList);

    // Free memory
    delete l1;
    delete l2;
    // Free memory occupied by the merged list
    while (mergedList != nullptr) {
        ListNode* temp = mergedList;
        mergedList = mergedList->next;
        delete temp;
    }

    return 0;
}
```

This code defines a `ListNode` struct to represent each node of the linked list and a `Solution` class that contains the `mergeTwoLists` function to merge two sorted linked lists. The `printList` function is a utility to print the merged list.

In the `main` function, two sorted linked lists `l1` and `l2` are created and merged using the `mergeTwoLists` function. Finally, the merged list is printed, and memory is properly deallocated.

### 1. Algorithms & Data Structures (C++): Merge Two Sorted Lists

Certainly! Merging two sorted lists is a common operation in computer science, often used in sorting and searching algorithms. Here's a simple implementation in C++:

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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        // Create a dummy node to serve as the head of the merged list
        ListNode* dummy = new ListNode(0);
        // Pointer to the current node of the merged list
        ListNode* current = dummy;

        // Traverse both lists until one of them reaches the end
        while (l1 != nullptr && l2 != nullptr) {
            if (l1->val < l2->val) {
                current->next = l1;
                l1 = l1->next;
            } else {
                current->next = l2;
                l2 = l2->next;
            }
            // Move the current pointer forward
            current = current->next;
        }

        // If any list still has remaining elements, append them to the merged list
        if (l1 != nullptr) {
            current->next = l1;
        } else {
            current->next = l2;
        }

        // Return the merged list, skipping the dummy node
        return dummy->next;
    }
};

// Function to print a linked list
void printList(ListNode* head) {
    while (head != nullptr) {
        cout << head->val << " ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    // Example usage
    ListNode* l1 = new ListNode(1);
    l1->next = new ListNode(3);
    l1->next->next = new ListNode(5);

    ListNode* l2 = new ListNode(2);
    l2->next = new ListNode(4);
    l2->next->next = new ListNode(6);

    Solution sol;
    ListNode* mergedList = sol.mergeTwoLists(l1, l2);

    cout << "Merged List: ";
    printList(mergedList);

    return 0;
}
```

This code defines a `ListNode` struct to represent each element in the linked list, and a `Solution` class with a method `mergeTwoLists` that takes two sorted linked lists as input and merges them into a single sorted linked list. Finally, in the `main()` function, we create two sorted lists, merge them using the `mergeTwoLists` method, and print the merged list.

### 1. Algorithms & Data Structures (C++): Merge Two Sorted Lists - Linked List

Certainly! Merging two sorted linked lists in C++ involves iterating through both lists simultaneously, comparing the elements, and constructing a new sorted list. Here's a basic implementation:

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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* dummy = new ListNode(0);
        ListNode* tail = dummy;

        while (l1 && l2) {
            if (l1->val < l2->val) {
                tail->next = l1;
                l1 = l1->next;
            } else {
                tail->next = l2;
                l2 = l2->next;
            }
            tail = tail->next;
        }

        if (l1)
            tail->next = l1;
        else
            tail->next = l2;

        ListNode* mergedList = dummy->next;
        delete dummy;
        return mergedList;
    }
};

// Utility function to print a linked list
void printList(ListNode* head) {
    while (head) {
        cout << head->val << " ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    // Example lists
    ListNode* l1 = new ListNode(1);
    l1->next = new ListNode(3);
    l1->next->next = new ListNode(5);

    ListNode* l2 = new ListNode(2);
    l2->next = new ListNode(4);
    l2->next->next = new ListNode(6);

    Solution sol;
    ListNode* mergedList = sol.mergeTwoLists(l1, l2);
    cout << "Merged List: ";
    printList(mergedList);

    // Clean up
    while (mergedList) {
        ListNode* temp = mergedList;
        mergedList = mergedList->next;
        delete temp;
    }

    delete l1;
    delete l2;

    return 0;
}
```

This code defines a `ListNode` structure representing each element in the linked list, and a `Solution` class with a `mergeTwoLists` function that merges two sorted linked lists. The `main` function demonstrates how to use this class.

### 1. Algorithms & Data Structures (C++): Merge: Interview / LeetCode Exercise

Certainly! Merging algorithms are fundamental in computer science and are frequently encountered in interviews and coding exercises on platforms like LeetCode. The merge algorithm is commonly used in sorting algorithms like Merge Sort but also has various other applications in tasks like merging sorted arrays or lists efficiently.

Here's a basic implementation of the merge function in C++:

```cpp
#include <vector>
using namespace std;

void merge(vector<int>& nums, int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;

    // Create temporary arrays
    vector<int> L(n1), R(n2);

    // Copy data to temporary arrays L[] and R[]
    for (int i = 0; i < n1; i++)
        L[i] = nums[left + i];
    for (int j = 0; j < n2; j++)
        R[j] = nums[mid + 1 + j];

    // Merge the temporary arrays back into nums[left..right]
    int i = 0, j = 0, k = left;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            nums[k] = L[i];
            i++;
        } else {
            nums[k] = R[j];
            j++;
        }
        k++;
    }

    // Copy the remaining elements of L[], if any
    while (i < n1) {
        nums[k] = L[i];
        i++;
        k++;
    }

    // Copy the remaining elements of R[], if any
    while (j < n2) {
        nums[k] = R[j];
        j++;
        k++;
    }
}

void mergeSort(vector<int>& nums, int left, int right) {
    if (left < right) {
        // Same as (left+right)/2, but avoids overflow for large left and right
        int mid = left + (right - left) / 2;

        // Sort first and second halves
        mergeSort(nums, left, mid);
        mergeSort(nums, mid + 1, right);

        // Merge the sorted halves
        merge(nums, left, mid, right);
    }
}
```

In this implementation:

- The `merge` function merges two sorted subarrays `nums[left..mid]` and `nums[mid+1..right]`.
- The `mergeSort` function recursively divides the array into halves until it reaches a base case of a single element or an empty array, then merges the sorted halves.

You can use this implementation to solve problems involving merging two sorted arrays or sorting an array using the merge sort algorithm. LeetCode often has exercises related to this, such as merging sorted arrays or implementing sorting algorithms.

### 1. Algorithms & Data Structures (C++): MergeSort

Certainly! Merge sort is a popular sorting algorithm that follows the divide-and-conquer strategy. It recursively divides the input array into smaller halves, sorts them individually, and then merges them back together in a sorted manner. Here's how it works:

1. **Divide**: Divide the unsorted array into two halves.
2. **Conquer**: Recursively sort each half.
3. **Combine**: Merge the sorted halves to produce the final sorted array.

Here's a C++ implementation of Merge Sort:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Merge two sorted subarrays [left...mid] and [mid+1...right]
void merge(vector<int>& arr, int left, int mid, int right) {
    int n1 = mid - left + 1;    // Size of left subarray
    int n2 = right - mid;        // Size of right subarray

    // Create temporary arrays
    vector<int> L(n1), R(n2);

    // Copy data to temporary arrays L[] and R[]
    for (int i = 0; i < n1; i++)
        L[i] = arr[left + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[mid + 1 + j];

    // Merge the temporary arrays back into arr[left...right]
    int i = 0, j = 0, k = left;
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

    // Copy the remaining elements of L[], if any
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    // Copy the remaining elements of R[], if any
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

// Main function to perform merge sort on array arr[]
void mergeSort(vector<int>& arr, int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2; // Calculate mid index

        // Sort first and second halves
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);

        // Merge the sorted halves
        merge(arr, left, mid, right);
    }
}

// Utility function to print an array
void printArray(const vector<int>& arr) {
    for (int i = 0; i < arr.size(); i++)
        cout << arr[i] << " ";
    cout << endl;
}

int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    int n = arr.size();

    cout << "Given array is \n";
    printArray(arr);

    mergeSort(arr, 0, n - 1);

    cout << "\nSorted array is \n";
    printArray(arr);
    return 0;
}
```

This code implements the Merge Sort algorithm in C++. The `mergeSort` function is the main function that sorts the array, and `merge` is the function responsible for merging two sorted arrays. Finally, the `printArray` function is a utility to print the elements of an array.

### 1. Algorithms & Data Structures (C++): MergeSort: The Merge Function

In the MergeSort algorithm, the merge function is crucial as it combines two sorted arrays into a single sorted array. Here's a typical implementation of the merge function in C++:

```cpp
#include <vector>
#include <iostream>

using namespace std;

// Merge two sorted subarrays arr[l..m] and arr[m+1..r]
void merge(vector<int>& arr, int l, int m, int r) {
    int n1 = m - l + 1; // Size of left subarray
    int n2 = r - m;     // Size of right subarray

    // Create temporary arrays
    vector<int> L(n1);
    vector<int> R(n2);

    // Copy data to temporary arrays L[] and R[]
    for (int i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[m + 1 + j];

    // Merge the temporary arrays back into arr[l..r]
    int i = 0; // Initial index of left subarray
    int j = 0; // Initial index of right subarray
    int k = l; // Initial index of merged subarray

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

    // Copy the remaining elements of L[], if any
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    // Copy the remaining elements of R[], if any
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

// Main function to test the merge function
int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    int l = 0;
    int r = arr.size() - 1;
    int m = l + (r - l) / 2;
    merge(arr, l, m, r);

    // Print the sorted array
    for (int i = 0; i < arr.size(); i++)
        cout << arr[i] << " ";
    cout << endl;

    return 0;
}
```

This function takes four arguments:

- `arr`: The vector to be sorted.
- `l`: The left index of the subarray to be merged.
- `m`: The middle index of the subarray to be merged.
- `r`: The right index of the subarray to be merged.

The function first calculates the sizes of the two subarrays to be merged (`n1` and `n2`). Then, it creates temporary arrays `L` and `R` to store the elements of the two subarrays. After that, it merges the elements of `L` and `R` back into the original array `arr`. Finally, it copies any remaining elements from `L` or `R` back into `arr` if there are any.

### 1. Algorithms & Data Structures (C++): Merging

Sure, merging is a fundamental operation in algorithms and data structures, especially in sorting and searching algorithms. In C++, you can merge two sorted arrays or lists efficiently using various approaches. Here's a basic outline of how you can merge two sorted arrays:

```cpp
#include <iostream>
#include <vector>

std::vector<int> mergeSortedArrays(const std::vector<int>& arr1, const std::vector<int>& arr2) {
    std::vector<int> mergedArray;
    int i = 0; // Index for arr1
    int j = 0; // Index for arr2
    
    // Traverse both arrays
    while (i < arr1.size() && j < arr2.size()) {
        if (arr1[i] <= arr2[j]) {
            mergedArray.push_back(arr1[i]);
            i++;
        } else {
            mergedArray.push_back(arr2[j]);
            j++;
        }
    }
    
    // Copy the remaining elements of arr1, if any
    while (i < arr1.size()) {
        mergedArray.push_back(arr1[i]);
        i++;
    }
    
    // Copy the remaining elements of arr2, if any
    while (j < arr2.size()) {
        mergedArray.push_back(arr2[j]);
        j++;
    }
    
    return mergedArray;
}

int main() {
    std::vector<int> arr1 = {1, 3, 5, 7, 9};
    std::vector<int> arr2 = {2, 4, 6, 8, 10};
    
    std::vector<int> merged = mergeSortedArrays(arr1, arr2);
    
    std::cout << "Merged Array: ";
    for (int num : merged) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
    
    return 0;
}
```

This code defines a function `mergeSortedArrays` that takes two sorted vectors (`arr1` and `arr2`) and merges them into a single sorted vector. It uses two pointers (`i` and `j`) to traverse both arrays simultaneously and compares elements at each position to determine which one to insert into the merged array. Finally, any remaining elements in either array are appended to the merged array.

This implementation has a time complexity of O(n), where n is the total number of elements in both arrays.

### 1. Algorithms & Data Structures (C++): Merging - Algorithm

In the context of algorithms and data structures, merging generally refers to combining two or more sorted sequences into a single sorted sequence. This operation is often encountered in various scenarios, such as merging sorted arrays or merging sorted linked lists.

Here's a simple algorithm for merging two sorted arrays in C++:

```cpp
#include <iostream>
#include <vector>

std::vector<int> mergeSortedArrays(const std::vector<int>& arr1, const std::vector<int>& arr2) {
    std::vector<int> mergedArray;
    int i = 0, j = 0;

    while (i < arr1.size() && j < arr2.size()) {
        if (arr1[i] < arr2[j]) {
            mergedArray.push_back(arr1[i]);
            i++;
        } else {
            mergedArray.push_back(arr2[j]);
            j++;
        }
    }

    // Append remaining elements from arr1, if any
    while (i < arr1.size()) {
        mergedArray.push_back(arr1[i]);
        i++;
    }

    // Append remaining elements from arr2, if any
    while (j < arr2.size()) {
        mergedArray.push_back(arr2[j]);
        j++;
    }

    return mergedArray;
}

int main() {
    std::vector<int> arr1 = {1, 3, 5, 7, 9};
    std::vector<int> arr2 = {2, 4, 6, 8, 10};

    std::vector<int> mergedArray = mergeSortedArrays(arr1, arr2);

    std::cout << "Merged Array:";
    for (int num : mergedArray) {
        std::cout << " " << num;
    }
    std::cout << std::endl;

    return 0;
}
```

This code defines a function `mergeSortedArrays` that takes two sorted vectors (`arr1` and `arr2`) and merges them into a single sorted vector (`mergedArray`). The `while` loops iterate through both arrays, comparing elements and appending the smaller one to `mergedArray`. After one of the arrays is exhausted, the remaining elements from the other array are appended to `mergedArray`.

The time complexity of this merging algorithm is O(n), where n is the total number of elements in both input arrays. This is because each element of both arrays is visited exactly once.

### 1. Algorithms & Data Structures (C++): Merging 2 Linked Lists

Merging two linked lists in C++ involves combining elements from both lists into a single list while maintaining the order. Here's a simple implementation of merging two sorted linked lists:

```cpp
#include <iostream>

using namespace std;

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

// Function to merge two sorted linked lists
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    // Create a dummy node to serve as the head of the merged list
    ListNode* dummy = new ListNode(0);
    ListNode* current = dummy;

    // Traverse both lists and compare the nodes, adding the smaller one to the merged list
    while (l1 != NULL && l2 != NULL) {
        if (l1->val < l2->val) {
            current->next = l1;
            l1 = l1->next;
        } else {
            current->next = l2;
            l2 = l2->next;
        }
        current = current->next;
    }

    // Add any remaining nodes from l1 or l2
    if (l1 != NULL) {
        current->next = l1;
    } else {
        current->next = l2;
    }

    // Return the merged list, omitting the dummy node
    return dummy->next;
}

// Function to print a linked list
void printList(ListNode* head) {
    ListNode* current = head;
    while (current != NULL) {
        cout << current->val << " ";
        current = current->next;
    }
    cout << endl;
}

int main() {
    // Example usage
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

    ListNode* mergedList = mergeTwoLists(l1, l2);
    cout << "Merged List: ";
    printList(mergedList);

    return 0;
}
```

This program defines a `ListNode` structure representing nodes in the linked list, a function `mergeTwoLists` to merge two sorted linked lists, and a `printList` function to print the elements of a linked list. The `main` function demonstrates how to use these functions to merge two sorted linked lists and print the result.

### 1. Algorithms & Data Structures (C++): Merging Arrays

In C++, merging two arrays is a fundamental operation that involves combining two sorted arrays into a single sorted array. Here's a simple implementation:

```cpp
#include <iostream>
#include <vector>

std::vector<int> mergeArrays(const std::vector<int>& arr1, const std::vector<int>& arr2) {
    std::vector<int> mergedArr;
    int i = 0, j = 0;

    // Merge until one of the arrays is exhausted
    while (i < arr1.size() && j < arr2.size()) {
        if (arr1[i] <= arr2[j]) {
            mergedArr.push_back(arr1[i]);
            i++;
        } else {
            mergedArr.push_back(arr2[j]);
            j++;
        }
    }

    // Copy the remaining elements of arr1
    while (i < arr1.size()) {
        mergedArr.push_back(arr1[i]);
        i++;
    }

    // Copy the remaining elements of arr2
    while (j < arr2.size()) {
        mergedArr.push_back(arr2[j]);
        j++;
    }

    return mergedArr;
}

int main() {
    std::vector<int> arr1 = {1, 3, 5, 7, 9};
    std::vector<int> arr2 = {2, 4, 6, 8, 10};

    std::vector<int> mergedArr = mergeArrays(arr1, arr2);

    std::cout << "Merged Array: ";
    for (int num : mergedArr) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this implementation:

- We use two pointers, one for each array (`i` for `arr1` and `j` for `arr2`).
- We compare the elements at the current positions of the two pointers and push the smaller one into the `mergedArr`.
- We continue this process until one of the arrays is exhausted.
- Finally, we copy the remaining elements from both arrays into `mergedArr`.

This implementation assumes that both input arrays are sorted. If not, you'll need to sort them first before merging.

### 1. Algorithms & Data Structures (C++): Merging Two Linked Lists

Merging two linked lists in C++ can be done efficiently by traversing both lists simultaneously and merging them into one. Below is a basic implementation of merging two sorted linked lists:

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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        // Create a dummy node to hold the merged list
        ListNode* dummy = new ListNode(0);
        ListNode* tail = dummy;
        
        while (l1 && l2) {
            if (l1->val < l2->val) {
                tail->next = l1;
                l1 = l1->next;
            } else {
                tail->next = l2;
                l2 = l2->next;
            }
            tail = tail->next;
        }
        
        // Append the remaining nodes from either list
        tail->next = (l1) ? l1 : l2;
        
        return dummy->next;
    }
};

// Function to print a linked list
void printList(ListNode* head) {
    ListNode* curr = head;
    while (curr) {
        cout << curr->val << " ";
        curr = curr->next;
    }
    cout << endl;
}

int main() {
    // Create two sorted linked lists
    ListNode* l1 = new ListNode(1);
    l1->next = new ListNode(3);
    l1->next->next = new ListNode(5);

    ListNode* l2 = new ListNode(2);
    l2->next = new ListNode(4);
    l2->next->next = new ListNode(6);

    Solution solution;
    ListNode* mergedList = solution.mergeTwoLists(l1, l2);

    cout << "Merged List: ";
    printList(mergedList);

    return 0;
}
```

In this implementation:

- We traverse both lists simultaneously, comparing the values of the current nodes.
- We create a new list, linking nodes from both lists in sorted order.
- Finally, we append any remaining nodes from either list to the merged list.

This code assumes that the input lists are already sorted. If not, you might need to sort them first or modify the algorithm accordingly.

### 1. Algorithms & Data Structures (C++): Merging Two Linked Lists by Rearranging pointers

Certainly! Merging two linked lists by rearranging pointers involves manipulating the pointers of the nodes in both lists to form a single merged list. Here's how you can do it in C++:

```cpp
#include <iostream>

// Define the structure of a node in the linked list
struct Node {
    int data;
    Node* next;
    
    Node(int val) : data(val), next(nullptr) {}
};

// Function to merge two sorted linked lists
Node* mergeLinkedLists(Node* l1, Node* l2) {
    // Create a dummy node to start the merged list
    Node dummy(0);
    Node* tail = &dummy;

    // Loop until one of the lists becomes empty
    while (l1 && l2) {
        if (l1->data < l2->data) {
            tail->next = l1;
            l1 = l1->next;
        } else {
            tail->next = l2;
            l2 = l2->next;
        }
        tail = tail->next;
    }

    // Attach the remaining nodes of the non-empty list
    if (l1) {
        tail->next = l1;
    } else {
        tail->next = l2;
    }

    // Return the merged list starting from the next of the dummy node
    return dummy.next;
}

// Utility function to print a linked list
void printLinkedList(Node* head) {
    while (head) {
        std::cout << head->data << " ";
        head = head->next;
    }
    std::cout << std::endl;
}

int main() {
    // Create two sorted linked lists
    Node* list1 = new Node(1);
    list1->next = new Node(3);
    list1->next->next = new Node(5);

    Node* list2 = new Node(2);
    list2->next = new Node(4);
    list2->next->next = new Node(6);

    // Print the original lists
    std::cout << "List 1: ";
    printLinkedList(list1);
    std::cout << "List 2: ";
    printLinkedList(list2);

    // Merge the lists and print the merged list
    Node* mergedList = mergeLinkedLists(list1, list2);
    std::cout << "Merged List: ";
    printLinkedList(mergedList);

    // Clean up memory
    while (mergedList) {
        Node* temp = mergedList;
        mergedList = mergedList->next;
        delete temp;
    }

    return 0;
}
```

This code defines a `Node` structure for the linked list, a function `mergeLinkedLists` to merge two sorted linked lists, and a utility function `printLinkedList` to print the elements of a linked list. Finally, in the `main` function, it creates two sorted linked lists, merges them, and prints the merged list.

### 1. Algorithms & Data Structures (C++): Odd Even

Sure! The "Odd-Even Sort" algorithm is a parallel sorting algorithm that sorts pairs of elements in a parallel manner. It repeatedly compares adjacent pairs of elements in the array and swaps them if they are in the wrong order. It has two phases: the odd phase and the even phase. In the odd phase, it compares and swaps elements at odd indices with their adjacent even-indexed elements if they are in the wrong order. Similarly, in the even phase, it compares and swaps elements at even indices with their adjacent odd-indexed elements if they are in the wrong order. This process is repeated until the array is sorted.

Here's a simple implementation of the Odd-Even Sort algorithm in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void oddEvenSort(vector<int>& arr) {
    int n = arr.size();
    bool sorted = false; // Flag to track if the array is sorted

    while (!sorted) {
        sorted = true;

        // Odd phase
        for (int i = 1; i < n - 1; i += 2) {
            if (arr[i] > arr[i + 1]) {
                swap(arr[i], arr[i + 1]);
                sorted = false; // If any swap occurs, the array is not yet fully sorted
            }
        }

        // Even phase
        for (int i = 0; i < n - 1; i += 2) {
            if (arr[i] > arr[i + 1]) {
                swap(arr[i], arr[i + 1]);
                sorted = false; // If any swap occurs, the array is not yet fully sorted
            }
        }
    }
}

int main() {
    vector<int> arr = {5, 2, 9, 1, 5, 6};
    
    cout << "Original array: ";
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;

    oddEvenSort(arr);

    cout << "Sorted array: ";
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}
```

This implementation sorts an array of integers using the Odd-Even Sort algorithm. You can modify the `main` function to use different input arrays for sorting.

### 1. Algorithms & Data Structures (C++): Optimized Bubble Sort

Optimizing Bubble Sort involves reducing the number of comparisons and swaps. Although Bubble Sort is not the most efficient sorting algorithm, it can be optimized to some extent. Here's an optimized version of Bubble Sort in C++:

```cpp
#include <iostream>
using namespace std;

void optimizedBubbleSort(int arr[], int n) {
    bool swapped;
    for (int i = 0; i < n-1; ++i) {
        swapped = false;
        for (int j = 0; j < n-i-1; ++j) {
            if (arr[j] > arr[j+1]) {
                // Swap elements
                swap(arr[j], arr[j+1]);
                swapped = true;
            }
        }
        // If no two elements were swapped, array is sorted
        if (!swapped) 
            break;
    }
}

int main() {
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr) / sizeof(arr[0]);
    optimizedBubbleSort(arr, n);
    cout << "Sorted array: \n";
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";
    cout << endl;
    return 0;
}
```

This optimized version includes a boolean variable `swapped`. If no swapping occurs in an iteration, it means the array is already sorted, and the algorithm can terminate early. This reduces the time complexity from O(n^2) to O(n) in the best-case scenario (when the array is already sorted).

Although this optimization improves the performance of Bubble Sort, it's still not as efficient as many other sorting algorithms like Quick Sort or Merge Sort. It's often used for educational purposes or for sorting small arrays where its simplicity can be advantageous.

### 1. Algorithms & Data Structures (C++): Program for Selection Sort

Sure, here's a simple implementation of the Selection Sort algorithm in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to perform selection sort
void selectionSort(vector<int>& arr) {
    int n = arr.size();

    // Traverse the array
    for (int i = 0; i < n - 1; ++i) {
        // Find the index of the minimum element in the unsorted part
        int min_index = i;
        for (int j = i + 1; j < n; ++j) {
            if (arr[j] < arr[min_index]) {
                min_index = j;
            }
        }

        // Swap the found minimum element with the first element
        swap(arr[i], arr[min_index]);
    }
}

// Function to print an array
void printArray(const vector<int>& arr) {
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;
}

int main() {
    vector<int> arr = {64, 25, 12, 22, 11};
    cout << "Original array: ";
    printArray(arr);

    selectionSort(arr);

    cout << "Sorted array: ";
    printArray(arr);

    return 0;
}
```

This code defines a function `selectionSort` that takes a vector of integers and sorts it using the Selection Sort algorithm. The `main` function demonstrates how to use this function by sorting a sample array and printing the result.

### 1. Algorithms & Data Structures (C++): Quick Sort

Quick Sort is a highly efficient sorting algorithm based on the divide-and-conquer strategy. It works by selecting a 'pivot' element from the array and partitioning the other elements into two sub-arrays according to whether they are less than or greater than the pivot. The sub-arrays are then recursively sorted.

Here's a simple implementation of Quick Sort in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to partition the array and return the pivot index
int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high]; // Choose the last element as the pivot
    int i = low - 1; // Index of smaller element

    for (int j = low; j < high; j++) {
        // If current element is smaller than or equal to pivot
        if (arr[j] <= pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return i + 1;
}

// Function to implement Quick Sort
void quickSort(vector<int>& arr, int low, int high) {
    if (low < high) {
        // Partitioning index
        int pi = partition(arr, low, high);

        // Recursively sort elements before and after partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

// Function to print the array
void printArray(const vector<int>& arr) {
    for (int i = 0; i < arr.size(); i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

int main() {
    vector<int> arr = {12, 5, 7, 3, 8, 10, 1, 4};
    int n = arr.size();

    cout << "Original array: ";
    printArray(arr);

    quickSort(arr, 0, n - 1);

    cout << "Sorted array: ";
    printArray(arr);

    return 0;
}
```

In this implementation:

- `partition()` function selects the last element of the array as the pivot, places the pivot element at its correct position in the sorted array, and places all smaller (smaller than pivot) elements to the left of the pivot and all greater elements to the right.
- `quickSort()` function recursively sorts the sub-arrays before and after the pivot.

This implementation sorts the array in ascending order. You can modify it to sort in descending order by changing the comparison operators in the `partition()` function.

### 1. Algorithms & Data Structures (C++): Quick Sort - Algorithm

Quick Sort is a popular sorting algorithm known for its efficiency and simplicity. It follows the divide-and-conquer approach, where it divides the array into smaller sub-arrays, sorts those sub-arrays, and then combines them to obtain the sorted array. Here's how the Quick Sort algorithm works in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to partition the array and return the pivot index
int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high]; // Choosing the last element as pivot
    int i = low - 1; // Index of smaller element

    for (int j = low; j < high; j++) {
        // If current element is smaller than or equal to pivot
        if (arr[j] <= pivot) {
            i++; // Increment index of smaller element
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return (i + 1); // Return the partitioning index
}

// Function to implement Quick Sort
void quickSort(vector<int>& arr, int low, int high) {
    if (low < high) {
        // Partitioning index
        int pi = partition(arr, low, high);

        // Separately sort elements before and after partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

// Utility function to print an array
void printArray(const vector<int>& arr) {
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;
}

// Driver code
int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    int n = arr.size();

    cout << "Original array: ";
    printArray(arr);

    quickSort(arr, 0, n - 1);

    cout << "Sorted array: ";
    printArray(arr);

    return 0;
}
```

Explanation:

1. `partition()` function selects the pivot (here we choose the last element), rearranges the array so that all elements smaller than the pivot are moved to its left, and all elements greater are moved to its right. It returns the index of the pivot element after partitioning.

2. `quickSort()` is the main function that implements the Quick Sort algorithm. It recursively calls itself for the sub-arrays before and after the partition index obtained from `partition()`.

3. In the `main()` function, an array is initialized and passed to `quickSort()` to sort it.

This implementation sorts the array in ascending order. You can modify the code according to your requirement to sort in descending order or for other data types.

### 1. Algorithms & Data Structures (C++): Quick Sort - Complexity Analysis

Quick Sort is a widely used sorting algorithm due to its efficiency and simplicity. Let's break down its complexity analysis:

1. **Best Case Complexity**:
   - In the best-case scenario, Quick Sort divides the array into two nearly equal partitions at each step. The partitioning process takes O(n) time.
   - After each partitioning, the algorithm recursively sorts two subarrays.
   - The best-case time complexity occurs when the pivot divides the array into two equal halves. In this case, the recurrence relation becomes T(n) = 2T(n/2) + Θ(n).
   - By solving this recurrence relation, we get a time complexity of O(n log n).

2. **Worst Case Complexity**:
   - The worst-case time complexity of Quick Sort occurs when the pivot element chosen at each step is either the smallest or largest element in the array. This leads to highly unbalanced partitioning, where one partition has n-1 elements and the other partition is empty.
   - In the worst-case scenario, the recurrence relation becomes T(n) = T(n-1) + Θ(n), as one partition has only one less element than the original array, and the other partition is empty.
   - Solving this recurrence relation yields a time complexity of O(n^2).

3. **Average Case Complexity**:
   - The average-case time complexity of Quick Sort is O(n log n).
   - This is because, on average, the partitioning process divides the array into two roughly equal halves, leading to balanced partitioning.
   - Even though Quick Sort has a worst-case time complexity of O(n^2), it's rarely encountered in practice due to the random or median-of-three pivot selection methods.

4. **Space Complexity**:
   - Quick Sort is an in-place sorting algorithm, meaning it doesn't require additional storage proportional to the input size.
   - However, Quick Sort has a recursive nature, and the stack space used by recursion can be significant, especially for large input sizes.
   - The worst-case space complexity of Quick Sort is O(n) due to the recursion stack.

5. **Stability**:
   - Quick Sort is not stable because it may change the relative order of equal elements.

In summary, Quick Sort has an average-case time complexity of O(n log n), making it one of the fastest sorting algorithms in practice. However, it's important to be aware of its worst-case time complexity of O(n^2) and take measures to mitigate it, such as using randomized pivot selection or median-of-three partitioning.

### 1. Algorithms & Data Structures (C++): Quick Sort (Implementation)

Sure, here's a simple implementation of the Quick Sort algorithm in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to partition the array
int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high]; // Choose the last element as the pivot
    int i = low - 1; // Index of the smaller element

    for (int j = low; j < high; j++) {
        // If current element is smaller than or equal to pivot
        if (arr[j] <= pivot) {
            i++; // Increment index of smaller element
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return (i + 1); // Return the partitioning index
}

// Function to perform Quick Sort
void quickSort(vector<int>& arr, int low, int high) {
    if (low < high) {
        // Partitioning index
        int pi = partition(arr, low, high);

        // Sort elements before and after partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

// Utility function to print an array
void printArray(const vector<int>& arr) {
    for (int i : arr) {
        cout << i << " ";
    }
    cout << endl;
}

int main() {
    vector<int> arr = {12, 7, 11, 13, 5, 6};
    int n = arr.size();

    cout << "Original array: ";
    printArray(arr);

    quickSort(arr, 0, n - 1);

    cout << "Sorted array: ";
    printArray(arr);

    return 0;
}
```

This code defines the `partition` function, which takes the last element of the array as the pivot, places the pivot element at its correct position in the sorted array, and places all smaller (smaller than pivot) to the left of the pivot and all greater elements to the right of the pivot.

The `quickSort` function recursively sorts the subarrays before and after the partitioning index. Finally, the `main` function initializes an array, calls the `quickSort` function to sort it, and prints the sorted array.

### 1. Algorithms & Data Structures (C++): Quick Sort (Theory)

Quick sort is a widely used sorting algorithm that follows the divide-and-conquer strategy. It efficiently sorts arrays or lists by partitioning the elements into smaller sub-arrays or sub-lists based on a pivot element. Here's how it works:

1. **Partitioning**: Choose a pivot element from the array. Typically, the pivot is chosen as the last element in the array, but other strategies are also possible, such as choosing the first, middle, or a random element. The elements of the array are then rearranged such that all elements less than the pivot are moved to its left, and all elements greater than the pivot are moved to its right. At this point, the pivot element is in its final sorted position. This operation is sometimes called the partition operation.

2. **Recursion**: After the partitioning step, the array is divided into two sub-arrays based on the pivot's final position. The partitioning step ensures that all elements to the left of the pivot are smaller, and all elements to the right are larger. The quick sort algorithm is then recursively applied to the sub-arrays on the left and right of the pivot until the entire array is sorted.

3. **Base Case**: The recursion stops when the sub-array size becomes zero or one because a single element array is already sorted by definition.

4. **Combine**: Since the elements are rearranged in place, no additional combining step is required. Once all recursive calls are completed, the entire array is sorted.

Here's a basic implementation of the Quick Sort algorithm in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to partition the array and return the pivot index
int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high]; // Choosing the last element as pivot
    int i = low - 1; // Index of smaller element

    for (int j = low; j < high; j++) {
        // If current element is smaller than or equal to pivot
        if (arr[j] <= pivot) {
            i++; // Increment index of smaller element
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return i + 1;
}

// Recursive function to perform quick sort
void quickSort(vector<int>& arr, int low, int high) {
    if (low < high) {
        // Partitioning index
        int pi = partition(arr, low, high);

        // Separately sort elements before and after partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

// Helper function to print the array
void printArray(const vector<int>& arr) {
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;
}

// Main function to test the quick sort implementation
int main() {
    vector<int> arr = {10, 7, 8, 9, 1, 5};
    int n = arr.size();

    cout << "Original array: ";
    printArray(arr);

    quickSort(arr, 0, n - 1);

    cout << "Sorted array: ";
    printArray(arr);

    return 0;
}
```

This implementation demonstrates the core concepts of quick sort: partitioning, recursion, and combining. It's a fundamental sorting algorithm and is efficient in practice, often outperforming other sorting algorithms like merge sort and heap sort, especially for small arrays or lists. However, its worst-case time complexity is \(O(n^2)\), which occurs when the pivot selection consistently results in unbalanced partitions, but on average, its time complexity is \(O(n \log n)\).

### 1. Algorithms & Data Structures (C++): Quick Sort Theory

Quick sort is a highly efficient sorting algorithm that falls under the category of comparison-based sorting algorithms. It's known for its speed and effectiveness in practice, often outperforming other popular sorting algorithms like merge sort and heap sort.

Here's the theory behind Quick Sort:

### Overview

Quick sort follows the "divide and conquer" strategy to sort a list of elements. It works by selecting a pivot element from the array and partitioning the other elements into two sub-arrays according to whether they are less than or greater than the pivot. The sub-arrays are then recursively sorted.

### Steps

1. **Choose a Pivot**: Select a pivot element from the array. This element can be chosen in various ways, such as picking the first element, the last element, a random element, or even the median of the array.

2. **Partitioning**: Rearrange the array in such a way that all elements less than the pivot are moved to its left and all elements greater than the pivot are moved to its right. After this partitioning, the pivot element is in its final sorted position.

3. **Recursively Sort Sub-arrays**: Apply the above steps recursively to the sub-arrays on the left and right of the pivot until the entire array is sorted.

### Partitioning Algorithm

The partitioning process is crucial to the quick sort algorithm. One common implementation is the Lomuto partition scheme:

- Initialize a pointer `i` to the first element of the array.
- Iterate through the array from the second element to the last.
- If the current element is less than or equal to the pivot, swap it with the element at index `i` and increment `i`.
- Finally, swap the pivot element with the element at index `i`.
- The pivot is now in its final sorted position, with elements less than it to its left and elements greater than it to its right.

### Time Complexity

The time complexity of quick sort depends on the choice of the pivot and the partitioning strategy. On average, it has a time complexity of O(n log n), making it significantly faster than other O(n log n) algorithms in practice. However, in the worst case (such as when the pivot is consistently the smallest or largest element), it can degrade to O(n^2). Choosing a good pivot strategy, like selecting the median element as the pivot, can minimize the chance of worst-case behavior.

### Space Complexity

The space complexity of quick sort is O(log n) for the recursive function calls on the stack.

### In-place Sorting

Quick sort can be implemented in-place, meaning it does not require additional memory proportional to the size of the input array.

### Stability

Quick sort is not a stable sorting algorithm, meaning that the relative order of equal elements might not be preserved.

### Practical Considerations

While quick sort has excellent average-case performance, it might not be the best choice for all scenarios. In cases where stability is crucial or where worst-case performance is unacceptable, other sorting algorithms might be preferred. However, for general-purpose sorting, quick sort is often a top choice due to its efficiency and simplicity.

### 1. Algorithms & Data Structures (C++): Quick Sort: Big O

Quick sort is a popular sorting algorithm known for its efficiency and effectiveness in most scenarios. Its average and best-case time complexity is O(n log n), making it one of the fastest sorting algorithms available. However, its worst-case time complexity is O(n^2), which occurs when the pivot selection consistently results in highly unbalanced partitions.

Here's a breakdown of its complexities:

1. **Time Complexity:**
   - **Best Case:** O(n log n) - This occurs when the pivot selection results in evenly balanced partitions, leading to efficient division and conquering.
   - **Average Case:** O(n log n) - On average, quick sort performs very efficiently due to its randomized nature or clever pivot selection strategies (like selecting the median of the array as the pivot).
   - **Worst Case:** O(n^2) - This happens when the pivot selection consistently results in highly unbalanced partitions, leading to a partition with one element and another with n-1 elements. This typically occurs when the pivot is either the smallest or largest element in the partition. However, various optimizations can mitigate this worst-case scenario, such as randomizing the pivot selection or using techniques like the median-of-three method.
  
2. **Space Complexity:**
   - Quick sort generally has a space complexity of O(log n) for the recursive call stack. This is because, in the worst case, quick sort can have O(n) nested recursive calls on the stack due to unbalanced partitions. However, in the average and best cases, the recursion tree is more balanced, leading to a space complexity of O(log n).

3. **Stability:**
   - Quick sort is not a stable sorting algorithm, meaning that the relative order of equal elements may not be preserved after sorting.

Despite its potential worst-case scenario, quick sort is often preferred in practice due to its average-case performance and simplicity of implementation. Additionally, its in-place nature (requiring only a small additional stack space for recursion) makes it memory efficient compared to algorithms like merge sort.

### 1. Algorithms & Data Structures (C++): Quick Sort: Implementation

Sure, here's a simple implementation of the Quick Sort algorithm in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to partition the array and return the pivot index
int partition(vector<int> &arr, int low, int high) {
    int pivot = arr[high]; // Choosing the last element as the pivot
    int i = low - 1; // Index of smaller element

    for (int j = low; j < high; j++) {
        // If current element is smaller than or equal to pivot
        if (arr[j] <= pivot) {
            i++; // Increment index of smaller element
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return i + 1;
}

// Function to perform Quick Sort
void quickSort(vector<int> &arr, int low, int high) {
    if (low < high) {
        // Partitioning index
        int pi = partition(arr, low, high);

        // Recursively sort elements before and after partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

// Utility function to print an array
void printArray(const vector<int> &arr) {
    for (int i = 0; i < arr.size(); i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

int main() {
    vector<int> arr = {10, 7, 8, 9, 1, 5};
    int n = arr.size();
    
    cout << "Original array: ";
    printArray(arr);

    quickSort(arr, 0, n - 1);

    cout << "Sorted array: ";
    printArray(arr);

    return 0;
}
```

This code defines the `partition` function to place the pivot element in its correct position in the sorted array. Then, the `quickSort` function recursively calls itself to sort the sub-arrays before and after the partition. Finally, the `printArray` function is used to print the contents of the array.

### 1. Algorithms & Data Structures (C++): Quick Sort: Pivot

In Quick Sort, the choice of the pivot is crucial for the efficiency of the algorithm. The basic idea behind Quick Sort is to select a pivot element from the array and partition the other elements into two sub-arrays according to whether they are less than or greater than the pivot. The sub-arrays are then sorted recursively.

There are several strategies for choosing the pivot:

1. **First element as pivot:** This is a simple approach where the first element of the array is chosen as the pivot. However, if the array is already sorted or nearly sorted, this can lead to poor performance.

2. **Last element as pivot:** Similar to the first element approach, but the last element of the array is chosen as the pivot. This also suffers from the same issue as the first element approach.

3. **Random element as pivot:** Choosing a random element from the array as the pivot helps to mitigate the issue of poor performance on sorted or nearly sorted arrays. This approach usually yields good performance on average.

4. **Median-of-three:** This approach selects the pivot as the median of the first, middle, and last elements of the array. It provides better performance compared to choosing a single pivot element, especially for arrays that are nearly sorted.

5. **Median-of-medians:** This is a more advanced method that guarantees a good pivot choice by recursively selecting a median-of-three from subgroups of elements. While it ensures a more balanced partitioning, it involves more computation and may not always be the best choice for small arrays.

The choice of pivot strategy depends on the specific characteristics of the data being sorted and the desired trade-offs between simplicity and performance. In practice, many implementations use the median-of-three approach as it provides a good balance between simplicity and efficiency.

### 1. Algorithms & Data Structures (C++): QuickSort

QuickSort is a widely used sorting algorithm known for its efficiency and simplicity. It belongs to the class of comparison-based sorting algorithms and follows the "divide and conquer" strategy. Here's a basic implementation of QuickSort in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to partition the array
int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high]; // Choose the last element as pivot
    int i = low - 1; // Index of smaller element

    for (int j = low; j < high; j++) {
        // If current element is smaller than or equal to pivot
        if (arr[j] <= pivot) {
            i++; // Increment index of smaller element
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return i + 1;
}

// Function to implement QuickSort
void quickSort(vector<int>& arr, int low, int high) {
    if (low < high) {
        // Partitioning index
        int pi = partition(arr, low, high);

        // Recursively sort elements before partition and after partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

// Utility function to print an array
void printArray(const vector<int>& arr) {
    for (int i : arr) {
        cout << i << " ";
    }
    cout << endl;
}

int main() {
    vector<int> arr = {10, 7, 8, 9, 1, 5};
    int n = arr.size();
    cout << "Original array: ";
    printArray(arr);

    quickSort(arr, 0, n - 1);

    cout << "Sorted array: ";
    printArray(arr);

    return 0;
}
```

In this implementation:

1. `partition()` function takes the last element as pivot, places the pivot element at its correct position in the sorted array, and places all smaller elements to the left of the pivot and all greater elements to the right of the pivot.
2. `quickSort()` function recursively sorts the elements before and after the partition.
3. `printArray()` is a utility function to print the elements of an array.

This implementation sorts the input array in ascending order. You can modify it as per your requirements, such as sorting in descending order or sorting arrays of different data types.

### 1. Algorithms & Data Structures (C++): QuickSort Function

Sure! Here's an implementation of the QuickSort algorithm in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to partition the array and return the pivot index
int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high];  // Choose the last element as pivot
    int i = low - 1;  // Index of the smaller element

    for (int j = low; j < high; j++) {
        // If current element is smaller than or equal to pivot
        if (arr[j] <= pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return i + 1;
}

// Function to perform QuickSort
void quickSort(vector<int>& arr, int low, int high) {
    if (low < high) {
        // Partitioning index
        int pivotIndex = partition(arr, low, high);

        // Recursively sort elements before partition and after partition
        quickSort(arr, low, pivotIndex - 1);
        quickSort(arr, pivotIndex + 1, high);
    }
}

// Utility function to print an array
void printArray(const vector<int>& arr) {
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;
}

int main() {
    vector<int> arr = {12, 7, 11, 13, 5, 6};
    int n = arr.size();
    cout << "Original array: ";
    printArray(arr);

    quickSort(arr, 0, n - 1);

    cout << "Sorted array: ";
    printArray(arr);

    return 0;
}
```

This code defines the `partition` function, which partitions the array around a pivot element, and the `quickSort` function, which recursively sorts the partitions. The `main` function demonstrates how to use these functions to sort an array.

### 1. Algorithms & Data Structures (C++): Quicksort: Algorithm Runtime Behaviour

Quicksort is a highly efficient sorting algorithm that follows the divide-and-conquer strategy. Here's an overview of its runtime behavior:

1. **Average-case performance**: Quicksort's average-case time complexity is O(n log n), where n is the number of elements in the array to be sorted. This makes it one of the fastest sorting algorithms available.

2. **Best-case performance**: In the best-case scenario, where the pivot selection consistently divides the array into approximately equal halves, Quicksort can achieve a time complexity of O(n log n).

3. **Worst-case performance**: The worst-case time complexity of Quicksort is O(n^2). This occurs when the pivot selection consistently picks either the smallest or largest element in the array, resulting in highly unbalanced partitions. However, with good pivot selection strategies, such as choosing the median of the first, middle, and last elements, the likelihood of encountering the worst-case scenario is minimized.

4. **Space complexity**: Quicksort typically operates in-place, requiring only O(log n) additional space for recursive function calls on the stack. This space is used for maintaining the recursion stack during the sorting process. However, in the worst-case scenario where the recursion depth equals the size of the input array, the space complexity can degrade to O(n).

5. **Stability**: Quicksort is not stable by default, meaning that the relative order of equal elements may change after sorting. However, stable versions of Quicksort can be implemented by modifying the partitioning step to preserve the relative order of equal elements.

6. **Adaptive behavior**: Quicksort exhibits adaptive behavior, meaning that its performance can vary depending on the initial ordering of elements. If the array is nearly sorted or partially sorted, Quicksort can perform better than its average-case time complexity suggests.

7. **Cache efficiency**: Quicksort's cache efficiency is generally good due to its localized nature of operations. However, in large arrays, the recursion and partitioning process may cause cache misses, affecting performance.

Overall, Quicksort is a versatile and efficient sorting algorithm that is widely used in practice, especially for large datasets where its average-case time complexity of O(n log n) shines. However, careful consideration of pivot selection and potential worst-case scenarios is important for achieving optimal performance.

### 1. Algorithms & Data Structures (C++): Quicksort: Fast Sorting Alogorithm

Quicksort is indeed a fast sorting algorithm commonly used in computer science due to its efficiency, especially for large datasets. It follows the "divide and conquer" strategy, where it breaks down the sorting problem into smaller sub-problems, sorts each sub-problem independently, and then combines the solutions to the sub-problems to obtain the final sorted array.

Here's a high-level overview of how Quicksort works:

1. **Partitioning**: Choose a pivot element from the array. Partition the array into two sub-arrays such that elements less than the pivot are on the left side, and elements greater than the pivot are on the right side. The pivot element is now in its correct sorted position.

2. **Recursively sort sub-arrays**: Recursively apply the same process to the sub-arrays on the left and right of the pivot until the entire array is sorted.

3. **Combine**: As the recursive calls return, the sub-arrays become sorted, and you combine them to get the final sorted array.

Here's a simple implementation of Quicksort in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to partition the array and return the index of the pivot element
int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high]; // Choosing the last element as the pivot
    int i = low - 1; // Index of the smaller element

    for (int j = low; j < high; j++) {
        // If current element is smaller than the pivot
        if (arr[j] < pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return i + 1;
}

// Recursive function to perform quicksort
void quicksort(vector<int>& arr, int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high); // Partitioning index

        // Recursively sort elements before and after partition
        quicksort(arr, low, pi - 1);
        quicksort(arr, pi + 1, high);
    }
}

// Function to print an array
void printArray(const vector<int>& arr) {
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;
}

int main() {
    vector<int> arr = {12, 7, 14, 9, 10, 11};
    int n = arr.size();
    
    cout << "Original array: ";
    printArray(arr);

    quicksort(arr, 0, n - 1);

    cout << "Sorted array: ";
    printArray(arr);

    return 0;
}
```

This implementation sorts integers, but you can adapt it to sort other data types or objects by modifying the comparison logic. Remember, Quicksort has an average-case time complexity of O(n log n), making it very efficient for large datasets. However, its worst-case time complexity is O(n^2) if the pivot selection is poorly done, which can happen if the pivot is always chosen as the smallest or largest element. Various techniques exist to mitigate this issue, such as selecting the pivot randomly or using median-of-three pivot selection.

### 1. Algorithms & Data Structures (C++): QuickSort: Pivot Function

In C++, the pivot function for the QuickSort algorithm selects a pivot element from the array to be sorted. A common approach is to choose the pivot as the last element of the array, but other strategies like choosing the first element or a random element can also be effective. Here's a simple implementation of the pivot function in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to swap two elements in the array
void swap(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}

// Function to choose the pivot element
int choosePivot(vector<int>& arr, int low, int high) {
    // For simplicity, let's choose the last element as the pivot
    return arr[high];
}

int main() {
    vector<int> arr = {10, 7, 8, 9, 1, 5};
    int n = arr.size();
    
    // Choosing the pivot element
    int pivot = choosePivot(arr, 0, n - 1);
    
    cout << "Pivot Element: " << pivot << endl;
    
    return 0;
}
```

In this code:

- The `choosePivot` function takes a vector `arr`, and the indices `low` and `high` indicating the range of the array from which to choose the pivot.
- For simplicity, this implementation chooses the last element of the array as the pivot.
- You can modify the `choosePivot` function to implement other pivot selection strategies such as choosing the first element, median-of-three, or random selection. These strategies may affect the efficiency of the QuickSort algorithm in different scenarios.

Remember, the choice of the pivot can significantly impact the performance of the QuickSort algorithm, especially in edge cases.

### 1. Algorithms & Data Structures (C++): QuickSort: Pivot Function Implementation

Sure, let's dive into implementing the pivot function for the QuickSort algorithm in C++. The pivot function is responsible for selecting a pivot element around which the array will be partitioned.

Here's a simple implementation of the pivot function:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to swap two elements in an array
void swap(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}

// Function to choose the pivot element for QuickSort
int choosePivot(vector<int>& arr, int low, int high) {
    // Here, we choose the middle element as the pivot
    int mid = low + (high - low) / 2;
    return arr[mid];
}

int main() {
    vector<int> arr = {3, 6, 8, 10, 1, 2, 1};

    // Choose pivot element
    int pivot = choosePivot(arr, 0, arr.size() - 1);

    cout << "Pivot element: " << pivot << endl;

    return 0;
}
```

In this implementation, the `choosePivot` function selects the middle element of the array as the pivot. You can customize this function to choose the pivot element in different ways, such as selecting the first element, the last element, or using a random element.

This is a basic implementation, and you can extend it further according to your specific requirements or preferences.

### 1. Algorithms & Data Structures (C++): QuickSort: QuickSort Algorithm Implementation

Sure, here's a simple implementation of the QuickSort algorithm in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to partition the array
int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high]; // Choosing the last element as the pivot
    int i = low - 1; // Index of smaller element

    for (int j = low; j < high; j++) {
        // If current element is smaller than the pivot
        if (arr[j] < pivot) {
            i++; // Increment index of smaller element
            swap(arr[i], arr[j]);
        }
    }

    // Swap pivot element with the element at position (i + 1)
    swap(arr[i + 1], arr[high]);
    return (i + 1);
}

// Recursive function to perform QuickSort
void quickSort(vector<int>& arr, int low, int high) {
    if (low < high) {
        // Partition the array and get the index of the pivot element
        int pi = partition(arr, low, high);

        // Recursively sort elements before partition and after partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

// Function to print the array
void printArray(const vector<int>& arr) {
    for (int i = 0; i < arr.size(); i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

int main() {
    vector<int> arr = {12, 7, 11, 5, 6, 13, 6};
    int n = arr.size();

    cout << "Original array: ";
    printArray(arr);

    quickSort(arr, 0, n - 1);

    cout << "Sorted array: ";
    printArray(arr);

    return 0;
}
```

This code defines the `partition` function which chooses a pivot and places all elements smaller than the pivot to its left and larger elements to its right. The `quickSort` function recursively sorts subarrays before and after the partitioning. Finally, the `main` function demonstrates the usage of the QuickSort algorithm on an example array.

### 1. Algorithms & Data Structures (C++): Radix Sort

Radix Sort is a non-comparative sorting algorithm that sorts numbers by processing individual digits of the numbers being sorted. It's particularly efficient for sorting integers, but it can also be extended to other data types with some modifications.

Here's a basic implementation of Radix Sort in C++ for sorting integers:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to find the maximum element in the array
int getMax(vector<int>& arr) {
    int max = arr[0];
    for (int i = 1; i < arr.size(); i++) {
        if (arr[i] > max)
            max = arr[i];
    }
    return max;
}

// Counting Sort function to perform sorting based on digit at significant place
void countingSort(vector<int>& arr, int exp) {
    vector<int> output(arr.size());
    vector<int> count(10, 0);

    // Store count of occurrences in count[]
    for (int i = 0; i < arr.size(); i++)
        count[(arr[i] / exp) % 10]++;

    // Change count[i] so that count[i] now contains
    // actual position of this digit in output[]
    for (int i = 1; i < 10; i++)
        count[i] += count[i - 1];

    // Build the output array
    for (int i = arr.size() - 1; i >= 0; i--) {
        output[count[(arr[i] / exp) % 10] - 1] = arr[i];
        count[(arr[i] / exp) % 10]--;
    }

    // Copy the output array to arr[], so that arr[] now
    // contains sorted numbers according to current digit
    for (int i = 0; i < arr.size(); i++)
        arr[i] = output[i];
}

// Radix Sort function
void radixSort(vector<int>& arr) {
    // Find the maximum number to know the number of digits
    int max = getMax(arr);

    // Do counting sort for every digit.
    // Instead of passing digit number, exp is passed.
    // exp is 10^i where i is the current digit number
    for (int exp = 1; max / exp > 0; exp *= 10)
        countingSort(arr, exp);
}

// Utility function to print an array
void printArray(vector<int>& arr) {
    for (int i = 0; i < arr.size(); i++)
        cout << arr[i] << " ";
    cout << endl;
}

int main() {
    vector<int> arr = {170, 45, 75, 90, 802, 24, 2, 66};
    cout << "Original array: ";
    printArray(arr);

    radixSort(arr);

    cout << "Sorted array: ";
    printArray(arr);
    return 0;
}
```

This implementation sorts integers by their digits, starting from the least significant digit (rightmost) to the most significant digit (leftmost). It uses counting sort as a subroutine to do the sorting at each digit position.

Feel free to modify this code or ask any questions if you need further clarification!

### 1. Algorithms & Data Structures (C++): Radix Sort - Explanation, Algorithm and Analysis

Radix Sort is a non-comparative sorting algorithm that sorts elements by processing individual digits of the numbers or strings to be sorted. It's based on the idea of sorting keys in a radix-dependent manner. The basic idea behind Radix Sort is to sort numbers digit by digit, from the least significant digit (rightmost) to the most significant digit (leftmost) or vice versa, depending on the implementation. This process continues until all digits have been considered.

Here's a step-by-step explanation of the Radix Sort algorithm:

1. **Find the maximum element**: First, find the maximum element in the array to determine the number of digits in the maximum number. This helps in deciding the number of iterations needed for sorting.

2. **Initialize the buckets**: Create a set of empty buckets, one for each digit (0 to 9) if sorting integers, or one for each character if sorting strings.

3. **Iterate through each digit position**: Starting from the least significant digit (rightmost), perform the following steps:
   - Place each element into the appropriate bucket based on the value of the current digit being considered.
   - After all elements are placed into buckets according to the current digit, concatenate all the buckets back into a single array.

4. **Repeat the above step for each digit position**: Continue this process for each subsequent digit position until all digits have been considered.

5. **End**: After sorting through all the digits, the array will be sorted.

Here's a basic implementation of Radix Sort in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

void countingSort(std::vector<int>& arr, int exp) {
    const int base = 10; // Base 10 for digits
    std::vector<int> count(base, 0);
    std::vector<int> output(arr.size());

    // Count occurrences of each digit
    for (int i = 0; i < arr.size(); i++)
        count[(arr[i] / exp) % base]++;

    // Cumulative count
    for (int i = 1; i < base; i++)
        count[i] += count[i - 1];

    // Build the output array
    for (int i = arr.size() - 1; i >= 0; i--) {
        output[count[(arr[i] / exp) % base] - 1] = arr[i];
        count[(arr[i] / exp) % base]--;
    }

    // Copy the output array to arr, so arr now contains sorted numbers
    for (int i = 0; i < arr.size(); i++)
        arr[i] = output[i];
}

void radixSort(std::vector<int>& arr) {
    int max_element = *std::max_element(arr.begin(), arr.end());

    // Perform counting sort for each digit place (1s, 10s, 100s, ...)
    for (int exp = 1; max_element / exp > 0; exp *= 10)
        countingSort(arr, exp);
}

int main() {
    std::vector<int> arr = {170, 45, 75, 90, 802, 24, 2, 66};
    radixSort(arr);
    std::cout << "Sorted array: ";
    for (int num : arr)
        std::cout << num << " ";
    std::cout << std::endl;
    return 0;
}
```

**Analysis:**

- Time Complexity:
  - The time complexity of Radix Sort is \(O(d * (n + k))\), where \(n\) is the number of elements to be sorted, \(k\) is the maximum value, and \(d\) is the number of digits in the maximum number.
  - In the worst case, the number of digits \(d\) is \(\log_{10} k\), making the time complexity \(O((n + k) * \log_{10} k)\).
- Space Complexity:
  - The space complexity is \(O(n + k)\), where \(n\) is the number of elements to be sorted and \(k\) is the range of input.
- Stability:
  - Radix Sort is a stable sorting algorithm, meaning that it preserves the relative order of equal elements.

Radix Sort is efficient for sorting large lists of numbers, particularly when the numbers have a bounded number of digits. However, its performance can degrade when the number of digits becomes significantly large compared to the number of elements being sorted.

### 1. Algorithms & Data Structures (C++): Rearranging in the Order Specified in the Index

In C++, you can rearrange elements in an array according to a specified index using a variety of methods. One common approach is to use a combination of arrays and sorting algorithms. Here's a step-by-step guide:

1. **Create two arrays**: One to store the elements, and the other to store the corresponding indices.
2. **Sort the index array**: This sorting is based on the values in the elements array.
3. **Rearrange the elements array**: After sorting the index array, rearrange the elements array according to the sorted index.

Here's a sample implementation:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

// Function to rearrange elements based on the specified index
template<typename T>
void rearrange(std::vector<T>& elements, std::vector<int>& index) {
    int n = elements.size();
    std::vector<T> temp_elements(n);

    for (int i = 0; i < n; ++i) {
        temp_elements[index[i]] = elements[i];
    }

    // Copy rearranged elements back to the original array
    elements = std::move(temp_elements);
}

int main() {
    std::vector<int> elements = {10, 20, 30, 40, 50};
    std::vector<int> index = {3, 0, 4, 1, 2};

    rearrange(elements, index);

    // Output the rearranged array
    for (int elem : elements) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this example, the `elements` vector contains the original elements, and the `index` vector contains the indices specifying the desired order. The `rearrange` function rearranges the elements according to the specified index. Finally, the rearranged array is outputted.

Keep in mind that this is a basic example, and depending on your specific requirements and constraints, you may need to adjust or optimize the implementation. Additionally, you may want to handle error cases, such as when the input arrays have different sizes.

### 1. Algorithms & Data Structures (C++): Recursive Merge Sort

Sure, here's a simple implementation of the Merge Sort algorithm in C++ using recursion:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Merge two sorted subarrays [left..mid] and [mid+1..right]
void merge(vector<int>& arr, int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;

    // Create temporary arrays
    vector<int> L(n1), R(n2);

    // Copy data to temporary arrays L[] and R[]
    for (int i = 0; i < n1; i++)
        L[i] = arr[left + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[mid + 1 + j];

    // Merge the temporary arrays back into arr[left..right]
    int i = 0, j = 0, k = left;
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

    // Copy the remaining elements of L[], if any
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    // Copy the remaining elements of R[], if any
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

// Utility function to print an array
void printArray(const vector<int>& arr) {
    for (int num : arr)
        cout << num << " ";
    cout << endl;
}

int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    int arr_size = arr.size();

    cout << "Given array is \n";
    printArray(arr);

    mergeSort(arr, 0, arr_size - 1);

    cout << "\nSorted array is \n";
    printArray(arr);
    return 0;
}
```

This code first defines a `merge` function to merge two sorted halves of an array, and then a `mergeSort` function that recursively divides the array into halves until it reaches individual elements and then merges them back together in sorted order. Finally, in the `main` function, an array is initialized, sorted using `mergeSort`, and then printed.

### 1. Algorithms & Data Structures (C++): Revisiting Sorting - The Heap Sort

Heap sort is a comparison-based sorting algorithm that transforms an array into a heap data structure. It then repeatedly removes the maximum (for a max heap) and places it at the end of the array. The heap is maintained after each removal to ensure the next maximum is efficiently obtained. This process continues until the heap is empty and the array is sorted.

Here's a basic implementation of heap sort in C++:

```cpp
#include <iostream>
#include <vector>

// To heapify a subtree rooted with node i which is
// an index in arr[]. n is the size of the heap
void heapify(std::vector<int>& arr, int n, int i) {
    int largest = i;    // Initialize largest as root
    int left = 2 * i + 1; // left = 2*i + 1
    int right = 2 * i + 2; // right = 2*i + 2

    // If left child is larger than root
    if (left < n && arr[left] > arr[largest])
        largest = left;

    // If right child is larger than largest so far
    if (right < n && arr[right] > arr[largest])
        largest = right;

    // If largest is not root
    if (largest != i) {
        std::swap(arr[i], arr[largest]);

        // Recursively heapify the affected sub-tree
        heapify(arr, n, largest);
    }
}

// main function to do heap sort
void heapSort(std::vector<int>& arr) {
    int n = arr.size();

    // Build heap (rearrange array)
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);

    // One by one extract an element from heap
    for (int i = n - 1; i > 0; i--) {
        // Move current root to end
        std::swap(arr[0], arr[i]);

        // call max heapify on the reduced heap
        heapify(arr, i, 0);
    }
}

// A utility function to print array of size n
void printArray(const std::vector<int>& arr) {
    for (int i = 0; i < arr.size(); ++i)
        std::cout << arr[i] << " ";
    std::cout << "\n";
}

int main() {
    std::vector<int> arr = {12, 11, 13, 5, 6, 7};
    int n = arr.size();

    heapSort(arr);

    std::cout << "Sorted array is \n";
    printArray(arr);
}
```

This implementation uses the heapify function to maintain the heap property. The heap is built using heapify, then the maximum element is moved to the end of the array and heapify is called again to maintain the heap property. This process is repeated until the array is sorted.

### 1. Algorithms & Data Structures (C++): Runtime characteristic of Bubble Sort

Bubble Sort is a simple sorting algorithm that repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. The pass through the list is repeated until the list is sorted. Here's a brief overview of its runtime characteristics:

1. **Worst-case time complexity**: O(n^2) - This occurs when the input array is in reverse sorted order, causing the maximum number of comparisons and swaps.

2. **Best-case time complexity**: O(n) - This occurs when the input array is already sorted. However, even in the best case, Bubble Sort requires a full pass through the array to ensure it's sorted, so it's still linear time.

3. **Average-case time complexity**: O(n^2) - On average, Bubble Sort performs O(n^2) comparisons and swaps.

4. **Space complexity**: O(1) - Bubble Sort is an in-place sorting algorithm, meaning it doesn't require any additional space other than what's already occupied by the input array.

5. **Stability**: Bubble Sort is stable, meaning it preserves the relative order of equal elements. If two elements have the same value, they won't be swapped unless they're out of order with respect to other elements.

Bubble Sort is straightforward to implement but inefficient for large lists, especially compared to more advanced sorting algorithms like Quick Sort or Merge Sort. It's mainly used for educational purposes or when simplicity is more important than efficiency.

### 1. Algorithms & Data Structures (C++): Runtime characteristic of Merge Sort

Merge Sort is a classic divide-and-conquer sorting algorithm that offers both stable sorting and guaranteed O(n log n) time complexity. Here's a breakdown of its runtime characteristics:

1. **Time Complexity**: The time complexity of Merge Sort is O(n log n) in all cases, where 'n' is the number of elements in the array to be sorted. This is true for the worst-case, average-case, and best-case scenarios. The key to understanding this time complexity lies in its divide-and-conquer approach, where the array is divided into halves recursively until each sub-array contains only one element (the base case), and then merges them back together while sorting.

2. **Space Complexity**: Merge Sort typically requires additional memory proportional to the size of the input array for temporary storage during the merging phase. This gives it a space complexity of O(n). However, it can be implemented to sort an array in-place, reducing the space complexity to O(1), but this may affect its stability.

3. **Stability**: Merge Sort is a stable sorting algorithm, meaning that the relative order of equal elements is preserved after sorting. This property is particularly useful in scenarios where there are multiple keys associated with each record.

4. **Adaptability**: Merge Sort does not have an adaptive characteristic. The time complexity remains O(n log n) regardless of the input distribution or initial order of elements.

5. **Performance**: Merge Sort performs consistently well across different types of input data, making it a popular choice for general-purpose sorting. It is often preferred over other O(n log n) sorting algorithms like Quick Sort when stability is desired or when sorting linked lists.

In summary, Merge Sort is known for its stable O(n log n) time complexity, making it suitable for sorting large datasets efficiently. Its space complexity of O(n) can be a concern for memory-constrained environments, but it provides a balance between time and space efficiency.

### 1. Algorithms & Data Structures (C++): Runtime characteristic of Quicksort

Quicksort is a highly efficient sorting algorithm known for its average-case performance. Its runtime characteristic depends on various factors such as the choice of pivot element, input data distribution, and implementation details. Here's a breakdown of its runtime characteristic:

1. **Average Case Time Complexity**: Quicksort typically exhibits an average-case time complexity of O(n log n), where n is the number of elements to be sorted. This makes it one of the fastest sorting algorithms on average.

2. **Best Case Time Complexity**: The best-case time complexity of Quicksort occurs when the partitioning routine consistently divides the array into roughly equal parts. In this case, the time complexity is O(n log n).

3. **Worst Case Time Complexity**: The worst-case time complexity of Quicksort occurs when the partitioning routine consistently divides the array into highly uneven partitions, such as when the smallest or largest element is always chosen as the pivot. In this scenario, the time complexity can degrade to O(n^2). However, this worst-case scenario is rare in practice and can be mitigated through various techniques like choosing a random pivot or using the median-of-three method.

4. **Space Complexity**: Quicksort typically has an in-place partitioning scheme, meaning it doesn't require additional memory proportional to the input size. However, it does require space for the call stack during recursive calls, which can lead to a space complexity of O(log n) on average and O(n) in the worst case if not implemented carefully to avoid excessive recursion depth.

5. **Stability**: Quicksort is not a stable sorting algorithm, meaning it may change the relative order of equal elements. This is due to the swapping operations that occur during the partitioning phase.

Overall, Quicksort is favored for its excellent average-case performance and low memory overhead, but careful consideration should be given to its worst-case behavior, especially in scenarios where the input data distribution is unknown or potentially adversarial.

### 1. Algorithms & Data Structures (C++): Shell Sort

Shell Sort is an efficient sorting algorithm that's an extension of insertion sort. It sorts elements by comparing distant elements first, rather than adjacent pairs, and then gradually reducing the gap between elements to be compared. Here's a basic implementation of Shell Sort in C++:

```cpp
#include <iostream>
#include <vector>

void shellSort(std::vector<int>& arr) {
    int n = arr.size();
    for (int gap = n / 2; gap > 0; gap /= 2) {
        for (int i = gap; i < n; ++i) {
            int temp = arr[i];
            int j;
            for (j = i; j >= gap && arr[j - gap] > temp; j -= gap) {
                arr[j] = arr[j - gap];
            }
            arr[j] = temp;
        }
    }
}

void printArray(const std::vector<int>& arr) {
    for (int elem : arr) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;
}

int main() {
    std::vector<int> arr = {12, 34, 54, 2, 3};
    std::cout << "Original array: ";
    printArray(arr);

    shellSort(arr);

    std::cout << "Sorted array: ";
    printArray(arr);

    return 0;
}
```

This implementation first sorts elements that are far apart from each other and then sorts the elements with a smaller gap between them. The key to the shell sort algorithm is the choice of gap sequence. There are several known gap sequences, such as Knuth's sequence (1, 4, 13, 40, ...), Sedgewick's sequence (1, 5, 19, 41, 109, ...), and many others. The choice of gap sequence can affect the performance of the algorithm.

Shell Sort is an in-place comparison-based sorting algorithm with a time complexity of O(n log n) in its best case, but it's generally considered to have an average-case time complexity of O(n log^2 n). However, it can perform much better than other O(n log n) algorithms, such as Merge Sort or Quick Sort, for small or medium-sized arrays.

### 1. Algorithms & Data Structures (C++): Shell Sort (Implementation)

Sure, here's a simple implementation of the Shell Sort algorithm in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void shellSort(vector<int>& arr) {
    int n = arr.size();
    
    // Start with a large gap, then reduce the gap
    for (int gap = n/2; gap > 0; gap /= 2) {
        // Do a gapped insertion sort for this gap size.
        // The first gap elements arr[0..gap-1] are already in gapped order.
        // Keep adding one more element until the entire array is gap sorted
        for (int i = gap; i < n; i++) {
            // Add arr[i] to the elements that have been gap sorted
            // Save arr[i] in temp and make a hole at position i
            int temp = arr[i];
            
            // Shift earlier gap-sorted elements up until the correct
            // location for arr[i] is found
            int j;
            for (j = i; j >= gap && arr[j - gap] > temp; j -= gap) {
                arr[j] = arr[j - gap];
            }
            
            // Put temp (the original arr[i]) in its correct location
            arr[j] = temp;
        }
    }
}

int main() {
    vector<int> arr = {12, 34, 54, 2, 3};
    
    cout << "Original array: ";
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;
    
    shellSort(arr);
    
    cout << "Sorted array: ";
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;
    
    return 0;
}
```

This code defines a `shellSort` function that takes a vector of integers and sorts it using the Shell Sort algorithm. Then, in the `main` function, it demonstrates how to use the `shellSort` function by sorting a sample array and printing the original and sorted arrays.

### 1. Algorithms & Data Structures (C++): Shell Sort (Theory)

Shell sort is an in-place comparison-based sorting algorithm that is a generalization of insertion sort. It was proposed by Donald Shell in 1959. The algorithm starts by sorting pairs of elements far apart from each other, then progressively reducing the gap between elements to be compared. This makes the array partially sorted, which makes subsequent passes of the algorithm faster.

Here's how the Shell sort algorithm works:

1. **Gap Sequence Selection**: Choose a sequence of gaps (also known as increments) to determine the gap between elements to be compared. Commonly used sequences include the Knuth sequence (3x + 1), Sedgewick sequence, or any other decreasing sequence ending in 1.

2. **Gap-based Insertion Sort**: Perform an insertion sort on subarrays separated by the chosen gap. The gap divides the array into several subarrays, and elements in each subarray are compared and swapped if necessary. The goal is to partially sort the array by moving smaller elements towards the beginning and larger elements towards the end.

3. **Reduce Gap**: After sorting with the initial gap, reduce the gap and repeat the insertion sort process. This step continues until the gap becomes 1, at which point the algorithm performs a regular insertion sort to finalize the sorting process.

The performance of Shell sort depends on the chosen sequence of gaps. While it's not as efficient as some advanced sorting algorithms like quicksort or merge sort, Shell sort has better performance than simple quadratic algorithms like bubble sort or insertion sort, especially for larger datasets.

Here's a basic implementation of Shell sort in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to perform Shell sort
void shellSort(vector<int>& arr) {
    int n = arr.size();

    // Start with a large gap, then reduce the gap
    for (int gap = n / 2; gap > 0; gap /= 2) {
        // Perform insertion sort for elements at each gap
        for (int i = gap; i < n; i++) {
            int temp = arr[i];
            int j;
            for (j = i; j >= gap && arr[j - gap] > temp; j -= gap) {
                arr[j] = arr[j - gap];
            }
            arr[j] = temp;
        }
    }
}

int main() {
    vector<int> arr = {12, 34, 54, 2, 3};
    shellSort(arr);
    cout << "Sorted array: ";
    for (int i = 0; i < arr.size(); i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
    return 0;
}
```

This implementation uses the Knuth sequence for gap selection (gap = n / 2, then gap /= 2 in each iteration). You can modify the gap sequence according to your preference or experiment with different sequences for potentially better performance.

### 1. Algorithms & Data Structures (C++): Sort a queue with constant space

Sorting a queue with constant space complexity can be done using only the operations allowed on a queue, which typically include enqueue, dequeue, front, and isEmpty. One approach is to use a variation of selection sort algorithm. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <queue>

using namespace std;

// Function to sort the queue
void sortQueue(queue<int>& q) {
    int n = q.size();
    
    for (int i = 0; i < n; ++i) {
        // Find the minimum element in remaining unsorted part
        int min_index = 0;
        int min_val = q.front();
        q.pop();
        
        for (int j = 0; j < n - i - 1; ++j) {
            int curr = q.front();
            q.pop();
            
            if (curr < min_val) {
                q.push(min_val);
                min_val = curr;
                min_index = j + 1;
            } else {
                q.push(curr);
            }
        }
        
        // Move minimum element to the end
        for (int j = 0; j < n - i; ++j) {
            if (j != min_index) {
                q.push(q.front());
            }
            q.pop();
        }
        q.push(min_val);
    }
}

// Function to print the queue
void printQueue(queue<int> q) {
    while (!q.empty()) {
        cout << q.front() << " ";
        q.pop();
    }
    cout << endl;
}

int main() {
    queue<int> q;
    q.push(5);
    q.push(1);
    q.push(4);
    q.push(2);
    q.push(3);

    cout << "Original queue: ";
    printQueue(q);

    sortQueue(q);

    cout << "Sorted queue: ";
    printQueue(q);

    return 0;
}
```

In this implementation, we iterate over the queue `n` times, where `n` is the size of the queue. In each iteration, we find the minimum element in the unsorted part of the queue, move it to the end of the queue, and repeat the process. Since we only use the operations allowed on a queue and do not use any additional space proportional to the size of the queue, the space complexity remains constant.

### 1. Algorithms & Data Structures (C++): Sort Algorithms

Certainly! Sorting algorithms are fundamental in computer science and play a crucial role in various applications. Here are some commonly used sorting algorithms implemented in C++:

1. **Bubble Sort**:

```cpp
void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n-1; i++) {
        for (int j = 0; j < n-i-1; j++) {
            if (arr[j] > arr[j+1]) {
                // Swap arr[j] and arr[j+1]
                int temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }
}
```

1. **Selection Sort**:

```cpp
void selectionSort(int arr[], int n) {
    int minIndex;
    for (int i = 0; i < n-1; i++) {
        minIndex = i;
        for (int j = i+1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        // Swap arr[i] and arr[minIndex]
        int temp = arr[i];
        arr[i] = arr[minIndex];
        arr[minIndex] = temp;
    }
}
```

1. **Insertion Sort**:

```cpp
void insertionSort(int arr[], int n) {
    int key, j;
    for (int i = 1; i < n; i++) {
        key = arr[i];
        j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}
```

1. **Merge Sort**:

```cpp
void merge(int arr[], int l, int m, int r) {
    int n1 = m - l + 1;
    int n2 = r - m;

    int L[n1], R[n2];

    for (int i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[m + 1 + j];

    int i = 0, j = 0, k = l;

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

    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

void mergeSort(int arr[], int l, int r) {
    if (l < r) {
        int m = l + (r - l) / 2;
        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);
        merge(arr, l, m, r);
    }
}
```

1. **Quick Sort**:

```cpp
int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = (low - 1);

    for (int j = low; j <= high - 1; j++) {
        if (arr[j] < pivot) {
            i++;
            std::swap(arr[i], arr[j]);
        }
    }
    std::swap(arr[i + 1], arr[high]);
    return (i + 1);
}

void quickSort(int arr[], int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}
```

These are just a few examples of sorting algorithms. Each has its own advantages and disadvantages in terms of performance and use cases.

### 1. Algorithms & Data Structures (C++): Sort Array By Parity

To sort an array by parity in C++, you can use a simple approach where you maintain two pointers, one at the beginning and one at the end of the array. Move the left pointer towards the right until you find an odd number, and move the right pointer towards the left until you find an even number. Swap these numbers, and repeat the process until the left pointer crosses the right pointer. Here's a C++ implementation of this approach:

```cpp
#include <iostream>
#include <vector>

using namespace std;

vector<int> sortArrayByParity(vector<int>& A) {
    int left = 0, right = A.size() - 1;
    
    while (left < right) {
        // Move left pointer to find an odd number
        while (left < right && A[left] % 2 == 0) {
            left++;
        }
        // Move right pointer to find an even number
        while (left < right && A[right] % 2 != 0) {
            right--;
        }
        // Swap the numbers
        if (left < right) {
            swap(A[left], A[right]);
            left++;
            right--;
        }
    }
    
    return A;
}

int main() {
    vector<int> nums = {3, 1, 2, 4, 6, 7, 8};
    
    cout << "Original Array: ";
    for (int num : nums) {
        cout << num << " ";
    }
    cout << endl;
    
    nums = sortArrayByParity(nums);
    
    cout << "Sorted Array by Parity: ";
    for (int num : nums) {
        cout << num << " ";
    }
    cout << endl;
    
    return 0;
}
```

This code will sort the array `nums` by moving even numbers to the left side and odd numbers to the right side.

### 1. Algorithms & Data Structures (C++): Sort Colors

Certainly! The problem you're referring to is often known as the "Sort Colors" problem, also referred to as the Dutch National Flag problem. Here's the problem statement:

Given an array with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue. We will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

Here's a C++ implementation of a solution using the Dutch National Flag algorithm, which sorts the array in a single pass:

```cpp
#include <vector>

void sortColors(std::vector<int>& nums) {
    int n = nums.size();
    int low = 0, mid = 0, high = n - 1;

    while (mid <= high) {
        if (nums[mid] == 0) {
            std::swap(nums[low], nums[mid]);
            low++;
            mid++;
        } else if (nums[mid] == 1) {
            mid++;
        } else { // nums[mid] == 2
            std::swap(nums[mid], nums[high]);
            high--;
        }
    }
}
```

Explanation:

- We initialize three pointers: `low`, `mid`, and `high`, representing the regions of elements with colors 0, 1, and 2 respectively.
- We iterate over the array using the `mid` pointer.
- If `nums[mid]` is 0, we swap it with the element at `low` and increment both `low` and `mid`, because we know the element at `low` is 0 and correctly placed.
- If `nums[mid]` is 1, we simply move to the next element.
- If `nums[mid]` is 2, we swap it with the element at `high` and decrement `high`, because we know the element at `high` is 2 and correctly placed.
- We continue this process until `mid` crosses `high`, ensuring that all elements have been properly placed.

This algorithm runs in O(n) time complexity and requires only a constant amount of extra space.

### 1. Algorithms & Data Structures (C++): Sort Colors - Sorting

To implement the "Sort Colors" problem in C++, you can use various sorting algorithms. One of the most efficient algorithms for this task is the Dutch National Flag algorithm, also known as 3-way partitioning. This algorithm sorts an array of 0s, 1s, and 2s in linear time complexity without using any extra space.

Here's a C++ implementation of the Dutch National Flag algorithm to solve the "Sort Colors" problem:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void sortColors(vector<int>& nums) {
    int low = 0;    // index for 0
    int high = nums.size() - 1;  // index for 2
    int mid = 0;    // current index

    while (mid <= high) {
        switch (nums[mid]) {
            case 0:
                swap(nums[low++], nums[mid++]); // swap with element at low and move both pointers
                break;
            case 1:
                mid++;  // no need to swap, just move mid
                break;
            case 2:
                swap(nums[mid], nums[high--]);  // swap with element at high and move high pointer
                break;
        }
    }
}

int main() {
    vector<int> nums = {2, 0, 2, 1, 1, 0};
    
    cout << "Original Array: ";
    for (int num : nums) {
        cout << num << " ";
    }
    cout << endl;
    
    sortColors(nums);
    
    cout << "Sorted Array: ";
    for (int num : nums) {
        cout << num << " ";
    }
    cout << endl;
    
    return 0;
}
```

This implementation sorts an array containing 0, 1, and 2 in-place. It maintains three pointers: low, mid, and high. The low pointer keeps track of the position to place the next 0, the high pointer keeps track of the position to place the next 2, and the mid pointer scans the array. The elements between low and mid are 1s, and those between mid and high are yet to be scanned. The algorithm continues until mid surpasses high, ensuring the entire array is sorted.

### 1. Algorithms & Data Structures (C++): Sort Fruits

Sure, sorting fruits can be a fun exercise! Here's an example of how you might sort a list of fruits alphabetically using C++ and the standard library:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

// Comparator function to sort fruits alphabetically
bool compareFruits(const std::string& fruit1, const std::string& fruit2) {
    return fruit1 < fruit2;
}

int main() {
    // List of fruits
    std::vector<std::string> fruits = {"apple", "banana", "orange", "grape", "pineapple"};

    // Sorting the fruits using the compareFruits function
    std::sort(fruits.begin(), fruits.end(), compareFruits);

    // Printing the sorted list of fruits
    std::cout << "Sorted list of fruits:" << std::endl;
    for (const auto& fruit : fruits) {
        std::cout << fruit << std::endl;
    }

    return 0;
}
```

In this code:

- We define a vector `fruits` containing strings representing different fruits.
- We define a comparator function `compareFruits` which compares two fruits alphabetically.
- We use the `std::sort` function from the `<algorithm>` header to sort the `fruits` vector using the `compareFruits` function.
- Finally, we print out the sorted list of fruits.

This code will output:

```bash
Sorted list of fruits:
apple
banana
grape
orange
pineapple
```

You can modify the comparator function `compareFruits` to implement different sorting criteria, such as sorting by length or sorting in reverse alphabetical order.

### 1. Algorithms & Data Structures (C++): Sort Integers by The Number of 1 Bits

To sort integers by the number of 1 bits in their binary representation, you can follow these steps in C++:

1. Define a custom comparator function that compares the number of set bits (1s) in the binary representations of two integers.
2. Use this comparator function with a sorting algorithm like `std::sort`.

Here's a sample implementation:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

// Function to count the number of set bits (1s) in an integer
int countSetBits(int num) {
    int count = 0;
    while (num) {
        count += num & 1;
        num >>= 1;
    }
    return count;
}

// Custom comparator function for sorting by number of set bits
bool sortBySetBits(int a, int b) {
    int countA = countSetBits(a);
    int countB = countSetBits(b);
    // If the number of set bits is the same, sort by the actual values
    if (countA == countB) {
        return a < b;
    }
    return countA < countB;
}

int main() {
    // Sample input
    std::vector<int> nums = {5, 2, 3, 9, 7, 6};

    // Sorting using custom comparator
    std::sort(nums.begin(), nums.end(), sortBySetBits);

    // Output sorted array
    std::cout << "Sorted by number of set bits:\n";
    for (int num : nums) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

This code first defines a function `countSetBits` to count the number of set bits in an integer. Then, it defines a custom comparator function `sortBySetBits` which compares two integers based on the count of set bits in their binary representations. Finally, it sorts a vector of integers using `std::sort` with the custom comparator.

### 1. Algorithms & Data Structures (C++): Sorting

Sorting algorithms are fundamental to computer science and play a crucial role in various applications. In C++, you have a variety of sorting algorithms to choose from, each with its advantages and disadvantages in terms of performance, space complexity, and stability. Here's an overview of some common sorting algorithms:

1. **Bubble Sort**: Bubble Sort repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. The pass through the list is repeated until the list is sorted.

2. **Selection Sort**: Selection Sort divides the input list into two parts: the sublist of items already sorted and the sublist of items remaining to be sorted. It repeatedly selects the minimum element from the unsorted sublist and swaps it with the leftmost unsorted element.

3. **Insertion Sort**: Insertion Sort builds the final sorted array one item at a time. It takes each element from the input array and places it in its correct position within the sorted array.

4. **Merge Sort**: Merge Sort is a divide-and-conquer algorithm that divides the input array into two halves, recursively sorts each half, and then merges the sorted halves to produce the final sorted array.

5. **Quick Sort**: Quick Sort is another divide-and-conquer algorithm that selects a 'pivot' element from the array and partitions the other elements into two sub-arrays according to whether they are less than or greater than the pivot. It then recursively sorts the sub-arrays.

6. **Heap Sort**: Heap Sort uses the properties of a binary heap to sort the input array. It first builds a max-heap from the input array, repeatedly extracts the maximum element from the heap, and rebuilds the heap until the array is sorted.

7. **Radix Sort**: Radix Sort sorts numbers by processing individual digits of the numbers from the least significant digit to the most significant digit or vice versa. It can be applied to numbers represented in any positional numeral system.

Each of these sorting algorithms has its own time complexity, which affects its efficiency for different input sizes and types. For instance, Bubble Sort and Selection Sort have a time complexity of O(n^2), making them inefficient for large input sizes, while Merge Sort and Quick Sort have a time complexity of O(n log n), making them more suitable for larger datasets.

Choosing the right sorting algorithm depends on various factors such as the size of the input, the nature of the data, and the desired performance characteristics.

### 1. Algorithms & Data Structures (C++): Sorting & Searching

Certainly! Sorting and searching are fundamental operations in computer science and are crucial for solving many problems efficiently. Let's dive into some common algorithms for sorting and searching in C++.

#### Sorting Algorithms

1. **Bubble Sort:**
   - It repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order.
   - Not efficient for large lists but easy to implement.
   - Time Complexity: O(n^2) in the worst and average case.

2. **Selection Sort:**
   - It repeatedly finds the minimum element from the unsorted part and puts it at the beginning.
   - Not efficient for large lists but simpler than bubble sort.
   - Time Complexity: O(n^2) in the worst and average case.

3. **Insertion Sort:**
   - It builds the final sorted array one item at a time, by iteratively inserting each element into its correct position.
   - Efficient for small data sets or nearly sorted arrays.
   - Time Complexity: O(n^2) in the worst and average case.

4. **Merge Sort:**
   - It divides the array into two halves, sorts the two halves separately, and then merges them.
   - Efficient for large data sets and has a stable performance.
   - Time Complexity: O(n log n) in all cases.

5. **Quick Sort:**
   - It picks an element as pivot and partitions the array around the pivot.
   - Efficient for large data sets and usually faster than merge sort.
   - Time Complexity: O(n log n) in the average case, O(n^2) in the worst case (rare).

#### Searching Algorithms

1. **Linear Search:**
   - It sequentially checks each element in the list until the desired element is found or the end of the list is reached.
   - Simple but not efficient for large lists.
   - Time Complexity: O(n) in the worst case.

2. **Binary Search:**
   - It works on sorted arrays by repeatedly dividing the search interval in half until the element is found.
   - Very efficient for large sorted arrays.
   - Time Complexity: O(log n).

Here's a simple implementation of Binary Search in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int binarySearch(vector<int>& arr, int target) {
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
    
    return -1; // element not found
}

int main() {
    vector<int> arr = {2, 4, 6, 8, 10, 12, 14, 16, 18, 20};
    int target = 12;
    int index = binarySearch(arr, target);
    if (index != -1)
        cout << "Element found at index " << index << endl;
    else
        cout << "Element not found" << endl;
    return 0;
}
```

This code demonstrates a binary search on a sorted array. You can modify it as needed for your application.

Feel free to ask if you need more explanations or want to see implementations of other sorting or searching algorithms!

### 1. Algorithms & Data Structures (C++): Sorting a Complex Vector

Sorting a complex vector in C++ can be done using custom comparison functions. Assuming you have a vector of complex numbers, where each element has a real and an imaginary part, you can define a custom comparison function based on your sorting criteria.

Here's an example of how you can sort a vector of complex numbers based on their magnitude:

```cpp
#include <iostream>
#include <vector>
#include <complex>
#include <algorithm>

// Custom comparison function for sorting based on magnitude
bool compareMagnitude(const std::complex<double> &a, const std::complex<double> &b) {
    return std::abs(a) < std::abs(b);
}

int main() {
    std::vector<std::complex<double>> complexVector = {{3, 4}, {1, 2}, {5, 1}, {2, -2}};

    // Print original vector
    std::cout << "Original vector:" << std::endl;
    for (const auto &c : complexVector) {
        std::cout << c << " ";
    }
    std::cout << std::endl;

    // Sort the vector based on magnitude
    std::sort(complexVector.begin(), complexVector.end(), compareMagnitude);

    // Print sorted vector
    std::cout << "Sorted vector by magnitude:" << std::endl;
    for (const auto &c : complexVector) {
        std::cout << c << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

This code defines a custom comparison function `compareMagnitude` which compares the magnitudes of two complex numbers. Then, it sorts the vector of complex numbers using `std::sort` and the custom comparison function.

You can define different comparison functions based on other criteria such as real part, imaginary part, or phase angle, depending on your sorting requirements.

### 1. Algorithms & Data Structures (C++): Sorting Algorithms

Sorting algorithms are fundamental in computer science and are used to rearrange data in a specific order, typically numerical or lexicographical. Here are some commonly used sorting algorithms implemented in C++:

#### 1. Bubble Sort

- Compare adjacent elements and swap them if they are in the wrong order. Repeat until no swaps are needed.

   ```cpp
   void bubbleSort(int arr[], int n) {
       for (int i = 0; i < n - 1; ++i) {
           for (int j = 0; j < n - i - 1; ++j) {
               if (arr[j] > arr[j + 1]) {
                   std::swap(arr[j], arr[j + 1]);
               }
           }
       }
   }
   ```

#### 2. Selection Sort

- Find the minimum element in the unsorted part and swap it with the first element of the unsorted part.

   ```cpp
   void selectionSort(int arr[], int n) {
       for (int i = 0; i < n - 1; ++i) {
           int min_index = i;
           for (int j = i + 1; j < n; ++j) {
               if (arr[j] < arr[min_index]) {
                   min_index = j;
               }
           }
           std::swap(arr[i], arr[min_index]);
       }
   }
   ```

#### 3. Insertion Sort

- Build the sorted array one element at a time by inserting each unsorted element into its correct position in the sorted part.

   ```cpp
   void insertionSort(int arr[], int n) {
       for (int i = 1; i < n; ++i) {
           int key = arr[i];
           int j = i - 1;
           while (j >= 0 && arr[j] > key) {
               arr[j + 1] = arr[j];
               --j;
           }
           arr[j + 1] = key;
       }
   }
   ```

#### 4. Merge Sort

- Divide the array into two halves, recursively sort each half, and then merge the sorted halves.

   ```cpp
   void merge(int arr[], int left, int mid, int right) {
       int n1 = mid - left + 1;
       int n2 = right - mid;
       int L[n1], R[n2];
       for (int i = 0; i < n1; ++i) {
           L[i] = arr[left + i];
       }
       for (int j = 0; j < n2; ++j) {
           R[j] = arr[mid + 1 + j];
       }
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
   
   void mergeSort(int arr[], int left, int right) {
       if (left < right) {
           int mid = left + (right - left) / 2;
           mergeSort(arr, left, mid);
           mergeSort(arr, mid + 1, right);
           merge(arr, left, mid, right);
       }
   }
   ```

#### 5. Quick Sort

- Choose a pivot and partition the array around the pivot such that elements smaller than the pivot are on the left and elements greater are on the right. Recursively apply the same process to the left and right partitions.

   ```cpp
   int partition(int arr[], int low, int high) {
       int pivot = arr[high];
       int i = low - 1;
       for (int j = low; j < high; ++j) {
           if (arr[j] < pivot) {
               ++i;
               std::swap(arr[i], arr[j]);
           }
       }
       std::swap(arr[i + 1], arr[high]);
       return i + 1;
   }
   
   void quickSort(int arr[], int low, int high) {
       if (low < high) {
           int pi = partition(arr, low, high);
           quickSort(arr, low, pi - 1);
           quickSort(arr, pi + 1, high);
       }
   }
   ```

These are just basic implementations. There are optimizations and variations for each algorithm to improve efficiency in specific cases.

### 1. Algorithms & Data Structures (C++): Sorting Algorithms - Summary of Complexities

Sure! Here's a summary of the complexities of some common sorting algorithms in C++:

1. **Bubble Sort**:
   - Time Complexity:
     - Best Case: O(n) (when the array is already sorted)
     - Worst Case: O(n^2)
     - Average Case: O(n^2)
   - Space Complexity: O(1)
   - Bubble sort is not recommended for large datasets due to its poor performance.

2. **Selection Sort**:
   - Time Complexity:
     - Best Case: O(n^2)
     - Worst Case: O(n^2)
     - Average Case: O(n^2)
   - Space Complexity: O(1)
   - Similar to Bubble Sort, Selection Sort is not efficient for large datasets.

3. **Insertion Sort**:
   - Time Complexity:
     - Best Case: O(n) (when the array is already sorted)
     - Worst Case: O(n^2)
     - Average Case: O(n^2)
   - Space Complexity: O(1)
   - Insertion Sort performs well for small datasets or nearly sorted arrays.

4. **Merge Sort**:
   - Time Complexity:
     - Best Case: O(n log n)
     - Worst Case: O(n log n)
     - Average Case: O(n log n)
   - Space Complexity: O(n)
   - Merge Sort is a stable sorting algorithm and is efficient for large datasets.

5. **Quick Sort**:
   - Time Complexity:
     - Best Case: O(n log n)
     - Worst Case: O(n^2) (rare, occurs when the pivot selection is poor)
     - Average Case: O(n log n)
   - Space Complexity: O(log n) to O(n)
   - Quick Sort is widely used due to its efficiency and in-place sorting nature.

6. **Heap Sort**:
   - Time Complexity:
     - Best Case: O(n log n)
     - Worst Case: O(n log n)
     - Average Case: O(n log n)
   - Space Complexity: O(1)
   - Heap Sort is an efficient sorting algorithm and is often used for sorting large datasets.

These complexities give a general idea of how efficient each sorting algorithm is in terms of time and space. The choice of which algorithm to use depends on factors like the size of the dataset, whether the data is partially sorted, and memory constraints.

### 1. Algorithms & Data Structures (C++): Sorting and Seaching Algorithms

Sure! Sorting and searching algorithms are fundamental concepts in computer science and are essential for efficiently organizing and retrieving data. Let's start with sorting algorithms:

#### Sorting Algorithms

1. **Bubble Sort**: This algorithm repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. The pass through the list is repeated until the list is sorted.

2. **Selection Sort**: It sorts an array by repeatedly finding the minimum element from the unsorted part and putting it at the beginning.

3. **Insertion Sort**: It builds the final sorted array (or list) one item at a time. It iterates through the list, removing one element from the input data, finds the location it belongs to in the sorted list, and inserts it there.

4. **Merge Sort**: This is a divide and conquer algorithm. It divides the input array into two halves, recursively sorts each half, and then merges them to produce a sorted array.

5. **Quick Sort**: Another divide and conquer algorithm, it picks an element as pivot and partitions the given array around the chosen pivot.

6. **Heap Sort**: It is based on the heap data structure. It first builds a heap from the input data and then repeatedly extracts the maximum element from the heap and rebuilds the heap until the array is sorted.

7. **Radix Sort**: It sorts the elements by first grouping the individual digits of the same place value. Then, the elements are sorted according to their radix (the base of the number system) digit by digit.

#### Searching Algorithms

1. **Linear Search**: It sequentially checks each element of the list until a match is found or the whole list has been searched.

2. **Binary Search**: It requires the array to be sorted beforehand. It compares the target value to the middle element of the array. If they are unequal, the half in which the target cannot lie is eliminated and the search continues on the remaining half.

3. **Depth-First Search (DFS)**: It explores as far as possible along each branch before backtracking. It's often used for traversal in graphs.

4. **Breadth-First Search (BFS)**: It explores all neighbor nodes at the present depth before moving on to the nodes at the next depth level. Also commonly used in graph traversal.

5. **Hashing**: It maps keys of a certain type to values of a certain type, usually implemented with hash tables. It allows for very fast retrieval of data.

6. **Interpolation Search**: An improvement over binary search, particularly for large and uniformly distributed arrays. It calculates the probable position of the desired element.

Each of these algorithms has its strengths and weaknesses, and the choice of algorithm depends on various factors such as the size of the dataset, the nature of the data, and the specific requirements of the problem at hand.

### 1. Algorithms & Data Structures (C++): Sorting Cabs

Sorting cabs could involve organizing them based on various criteria like distance, availability, or even customer ratings. One common algorithm to sort objects in programming is the **Merge Sort** algorithm. It's efficient and works well for large datasets. Let's imagine sorting cabs based on their distance from a pickup point:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Structure to represent a cab
struct Cab {
    int id;
    float distance;

    Cab(int i, float d) : id(i), distance(d) {}
};

// Merge function for merge sort
void merge(vector<Cab>& cabs, int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;

    // Create temporary arrays
    vector<Cab> L, R;
    for (int i = 0; i < n1; i++)
        L.push_back(cabs[left + i]);
    for (int j = 0; j < n2; j++)
        R.push_back(cabs[mid + 1 + j]);

    // Merge the temporary arrays back into cabs
    int i = 0, j = 0, k = left;
    while (i < n1 && j < n2) {
        if (L[i].distance <= R[j].distance) {
            cabs[k] = L[i];
            i++;
        } else {
            cabs[k] = R[j];
            j++;
        }
        k++;
    }

    // Copy the remaining elements of L[] and R[], if any
    while (i < n1) {
        cabs[k] = L[i];
        i++;
        k++;
    }
    while (j < n2) {
        cabs[k] = R[j];
        j++;
        k++;
    }
}

// Merge sort function
void mergeSort(vector<Cab>& cabs, int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;

        // Sort first and second halves
        mergeSort(cabs, left, mid);
        mergeSort(cabs, mid + 1, right);

        // Merge the sorted halves
        merge(cabs, left, mid, right);
    }
}

// Function to print cabs
void printCabs(const vector<Cab>& cabs) {
    cout << "Cab ID\tDistance\n";
    for (const auto& cab : cabs)
        cout << cab.id << "\t" << cab.distance << "\n";
}

int main() {
    // Example cabs
    vector<Cab> cabs = {
        Cab(1, 5.3),
        Cab(2, 2.1),
        Cab(3, 3.8),
        Cab(4, 1.5),
        Cab(5, 4.6)
    };

    // Sort cabs based on distance
    mergeSort(cabs, 0, cabs.size() - 1);

    // Print sorted cabs
    cout << "Sorted Cabs:\n";
    printCabs(cabs);

    return 0;
}
```

This code uses the merge sort algorithm to sort cabs based on their distance from a pickup point. You can adjust the sorting criteria and the cab data structure according to your requirements.

### 1. Algorithms & Data Structures (C++): Sorting Cartesian Points

Sorting Cartesian points in C++ can be achieved using various sorting algorithms, such as merge sort, quick sort, or even the standard library's `std::sort`. The Cartesian points are typically represented as pairs of `(x, y)` coordinates. Here's an example of how you can sort Cartesian points based on their x-coordinate:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Define a structure to represent Cartesian points
struct Point {
    int x, y;
};

// Comparator function to compare points based on their x-coordinate
bool comparePoints(const Point& p1, const Point& p2) {
    return p1.x < p2.x;
}

// Function to print Cartesian points
void printPoints(const vector<Point>& points) {
    for (const auto& point : points) {
        cout << "(" << point.x << ", " << point.y << ") ";
    }
    cout << endl;
}

int main() {
    // Sample points
    vector<Point> points = {{3, 5}, {1, 8}, {4, 2}, {2, 10}};

    cout << "Original Points: ";
    printPoints(points);

    // Sorting the points based on x-coordinate
    sort(points.begin(), points.end(), comparePoints);

    cout << "Sorted Points based on x-coordinate: ";
    printPoints(points);

    return 0;
}
```

This code sorts the Cartesian points based on their x-coordinates. You can modify the comparator function `comparePoints` to sort based on y-coordinate or any other criteria as needed.

### 1. Algorithms & Data Structures (C++): Sorting Stable and Unstable Sorting

In C++, sorting algorithms can be categorized into stable and unstable based on how they handle elements with equal keys. Here's a brief overview:

### Stable Sorting Algorithms

Stable sorting algorithms maintain the relative order of equal elements. In other words, if two elements have the same key, the element which appeared first in the original sequence will appear first in the sorted sequence.

#### Examples of Stable Sorting Algorithms

1. **Merge Sort**: It is a stable sorting algorithm that uses the divide-and-conquer strategy.
2. **Bubble Sort**: Although not efficient, it's stable. It repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order.
3. **Insertion Sort**: It's also stable. It builds the final sorted array (or list) one item at a time.

### Unstable Sorting Algorithms

Unstable sorting algorithms do not necessarily maintain the relative order of equal elements. After sorting, the order of elements with equal keys might change.

#### Examples of Unstable Sorting Algorithms

1. **Quick Sort**: A commonly used unstable sorting algorithm that uses the divide-and-conquer approach. It's often faster than stable alternatives for large datasets.
2. **Heap Sort**: Another unstable sorting algorithm that uses a binary heap data structure.

### Implementation in C++

Here's a simple example of sorting an array of integers using stable and unstable sorting algorithms in C++:

```cpp
#include <iostream>
#include <algorithm>

int main() {
    int arr[] = {4, 2, 1, 3, 5, 2};
    int n = sizeof(arr) / sizeof(arr[0]);

    // Stable sorting using merge sort
    std::stable_sort(arr, arr + n);
    std::cout << "Stable Sorted array: ";
    for (int i = 0; i < n; ++i)
        std::cout << arr[i] << " ";
    std::cout << std::endl;

    // Unstable sorting using quick sort
    std::sort(arr, arr + n);
    std::cout << "Unstable Sorted array: ";
    for (int i = 0; i < n; ++i)
        std::cout << arr[i] << " ";
    std::cout << std::endl;

    return 0;
}
```

In this code, `std::stable_sort` is used for stable sorting and `std::sort` for unstable sorting. Both functions are part of the C++ Standard Library's `<algorithm>` header.

### 1. Algorithms & Data Structures (C++): Sorting Techniques

Sorting techniques are fundamental in computer science and are crucial for various applications. Here's an overview of some common sorting algorithms implemented in C++:

1. **Bubble Sort**:
   - Bubble Sort repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. The pass through the list is repeated until the list is sorted.

   ```cpp
   void bubbleSort(int arr[], int n) {
       for (int i = 0; i < n - 1; i++) {
           for (int j = 0; j < n - i - 1; j++) {
               if (arr[j] > arr[j + 1]) {
                   swap(arr[j], arr[j + 1]);
               }
           }
       }
   }
   ```

2. **Selection Sort**:
   - Selection Sort divides the input list into two parts: a sorted sublist and an unsorted sublist. It repeatedly finds the minimum element from the unsorted sublist and moves it to the beginning of the sorted sublist.

   ```cpp
   void selectionSort(int arr[], int n) {
       for (int i = 0; i < n - 1; i++) {
           int minIndex = i;
           for (int j = i + 1; j < n; j++) {
               if (arr[j] < arr[minIndex]) {
                   minIndex = j;
               }
           }
           swap(arr[i], arr[minIndex]);
       }
   }
   ```

3. **Insertion Sort**:
   - Insertion Sort builds the final sorted array one item at a time. It takes one element from the input data and inserts it into the correct position in the already sorted part of the array.

   ```cpp
   void insertionSort(int arr[], int n) {
       for (int i = 1; i < n; i++) {
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

4. **Merge Sort**:
   - Merge Sort is a divide and conquer algorithm. It divides the input array into two halves, sorts each half recursively, and then merges the sorted halves.

   ```cpp
   void merge(int arr[], int l, int m, int r) {
       // Merge two subarrays arr[l..m] and arr[m+1..r]
       // ...
   }

   void mergeSort(int arr[], int l, int r) {
       if (l < r) {
           int m = l + (r - l) / 2;
           mergeSort(arr, l, m);
           mergeSort(arr, m + 1, r);
           merge(arr, l, m, r);
       }
   }
   ```

5. **Quick Sort**:
   - Quick Sort is also a divide and conquer algorithm. It picks an element as a pivot and partitions the given array around the pivot. It then recursively sorts the partitions.

   ```cpp
   int partition(int arr[], int low, int high) {
       // Partition the array around a pivot
       // ...
   }

   void quickSort(int arr[], int low, int high) {
       if (low < high) {
           int pi = partition(arr, low, high);
           quickSort(arr, low, pi - 1);
           quickSort(arr, pi + 1, high);
       }
   }
   ```

Each of these sorting algorithms has its advantages and disadvantages in terms of time complexity, space complexity, and stability. The choice of sorting algorithm depends on various factors such as the size of the data, the nature of the data, and the resources available.

### 1. Algorithms & Data Structures (C++): Sorting Terminologies

Sure, let's delve into sorting terminologies in the context of algorithms and data structures in C++.

1. **Sorting Algorithm**: A sorting algorithm is an algorithm that puts elements of a list or array in a certain order. There are various sorting algorithms, each with its own set of advantages and disadvantages in terms of efficiency, stability, and space complexity.

2. **Comparison-based Sorting**: Sorting algorithms that make decisions based only on comparisons between elements are called comparison-based sorting algorithms. Common examples include Bubble Sort, Selection Sort, Insertion Sort, Merge Sort, Quick Sort, Heap Sort, etc.

3. **Non-comparison Sorting**: Some sorting algorithms don't rely solely on comparisons between elements. Instead, they exploit properties of the data being sorted. Examples include Counting Sort, Radix Sort, and Bucket Sort. These algorithms often have linear time complexity but may have limitations on the types of data they can sort.

4. **Stable Sorting**: A sorting algorithm is said to be stable if the relative order of equal elements remains unchanged after sorting. For example, if there are two equal elements A and B, and A appears before B in the original list, then A will still appear before B in the sorted list. Merge Sort and Insertion Sort are stable, while Quick Sort is not inherently stable but can be implemented to be stable.

5. **In-place Sorting**: An in-place sorting algorithm is one that doesn't require any additional space and sorts the elements within the array itself. This means the sorting is performed in memory locations of the given array without requiring extra space proportional to the size of the array. Examples of in-place sorting algorithms include Bubble Sort, Selection Sort, Insertion Sort, and Quick Sort.

6. **Out-of-place Sorting**: Out-of-place sorting algorithms require extra space proportional to the size of the input. The sorted elements are placed in a different array or data structure than the original unsorted array. Merge Sort, for instance, typically requires extra space proportional to the size of the input array.

7. **Adaptive Sorting**: An adaptive sorting algorithm is one that takes advantage of preexisting order in its input. For example, if the input array is partially sorted, an adaptive sorting algorithm can perform better than when the array is completely unsorted. Insertion Sort and Bubble Sort are examples of adaptive sorting algorithms.

8. **External Sorting**: External sorting algorithms are designed for sorting data that is too large to fit into memory all at once. These algorithms use a combination of internal memory (RAM) and external storage (such as disk) to sort the data efficiently. External Merge Sort is a popular example of an external sorting algorithm.

Understanding these terminologies can help in selecting the most appropriate sorting algorithm based on the specific requirements and constraints of a given problem or application.

### 1. Algorithms & Data Structures (C++): Sorting The Issue With sort()

Sorting is a fundamental operation in computer science, and C++ provides a convenient way to perform sorting using the `std::sort()` function, which is part of the Standard Template Library (STL). However, there might be situations where you encounter issues or need to customize the sorting behavior. Let's explore some common issues and solutions related to sorting in C++.

### 1. Custom Sorting Order

Sometimes, you might need to sort elements based on criteria other than their natural order. For example, sorting custom objects based on a specific member variable or sorting strings in a case-insensitive manner.

**Solution**: You can achieve this by providing a custom comparison function or lambda expression to the `std::sort()` function.

```cpp
#include <algorithm>
#include <iostream>
#include <vector>

struct Person {
    std::string name;
    int age;
};

// Custom comparison function for sorting Persons by age
bool sortByAge(const Person &a, const Person &b) {
    return a.age < b.age;
}

int main() {
    std::vector<Person> people = {{"Alice", 30}, {"Bob", 25}, {"Charlie", 35}};

    // Sort by age using custom comparison function
    std::sort(people.begin(), people.end(), sortByAge);

    // Display sorted people
    for (const auto &person : people) {
        std::cout << person.name << " " << person.age << std::endl;
    }

    return 0;
}
```

### 2. Stability

The stability of a sorting algorithm refers to whether it maintains the relative order of equal elements. For some applications, maintaining the relative order of equal elements is important.

**Solution**: If you need a stable sort, you can use `std::stable_sort()` instead of `std::sort()`.

```cpp
#include <algorithm>
#include <iostream>
#include <vector>

int main() {
    std::vector<std::pair<int, std::string>> data = {{3, "Alice"}, {2, "Bob"}, {3, "Charlie"}};

    // Sort by the first element of the pair (integer)
    std::stable_sort(data.begin(), data.end());

    // Display sorted data
    for (const auto &pair : data) {
        std::cout << pair.first << " " << pair.second << std::endl;
    }

    return 0;
}
```

### 3. Performance Considerations

Different sorting algorithms have different performance characteristics. The choice of sorting algorithm can significantly impact the performance of your program, especially for large datasets.

**Solution**: Choose the appropriate sorting algorithm based on the size and characteristics of your data. For general purposes, `std::sort()` is often a good choice, as it typically uses an efficient algorithm like introsort (a hybrid sorting algorithm).

```cpp
#include <algorithm>
#include <iostream>
#include <vector>

int main() {
    std::vector<int> numbers = {5, 2, 8, 1, 9, 3};

    // Sort using std::sort (often efficient for general purposes)
    std::sort(numbers.begin(), numbers.end());

    // Display sorted numbers
    for (const auto &num : numbers) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

By understanding these issues and solutions, you can effectively utilize sorting in C++ to suit your specific requirements.

### 1. Algorithms & Data Structures (C++): Sorting the queries according to MO's comparator

MO's Algorithm is a popular technique used to answer range queries efficiently on static arrays. The core idea is to use a specific sorting strategy for the queries, leveraging the sqrt decomposition technique to minimize the number of changes in the array when processing the queries. Here’s a detailed explanation on how to sort the queries using MO's comparator and implement MO's algorithm in C++:

### Steps to Sort Queries Using MO's Comparator

1. **Divide the array into blocks:**
   The array is divided into blocks of size √N, where N is the size of the array.

2. **Sort the queries:**
   Queries are sorted based on two criteria:
   - The block number of the left endpoint of the query.
   - If two queries belong to the same block, then sort them by their right endpoint.

   The idea is to minimize the movement of the right endpoint of the queries because moving the right endpoint typically involves adding/removing elements from the current range, which is less costly than moving the left endpoint.

### C++ Implementation

Below is a C++ implementation of MO's Algorithm to sort and process range queries efficiently:

```cpp
#include <bits/stdc++.h>
using namespace std;

const int MAXN = 100000; // Adjust as needed
const int SQRT = 316; // sqrt(MAXN), adjust if MAXN is different

struct Query {
    int l, r, idx;
};

// Comparison function for sorting queries according to MO's order
bool mo_compare(const Query& a, const Query& b) {
    if (a.l / SQRT != b.l / SQRT)
        return a.l / SQRT < b.l / SQRT;
    return a.r < b.r;
}

int arr[MAXN];
Query queries[MAXN];
int answers[MAXN];
int freq[MAXN];

void add(int index) {
    // Add arr[index] to the current range
    // Update frequency array or other necessary structures
}

void remove(int index) {
    // Remove arr[index] from the current range
    // Update frequency array or other necessary structures
}

void process_queries(int n, int q) {
    sort(queries, queries + q, mo_compare);

    int currentL = 0, currentR = -1;
    for (int i = 0; i < q; i++) {
        int L = queries[i].l;
        int R = queries[i].r;
        
        while (currentL < L) {
            remove(currentL);
            currentL++;
        }
        while (currentL > L) {
            currentL--;
            add(currentL);
        }
        while (currentR < R) {
            currentR++;
            add(currentR);
        }
        while (currentR > R) {
            remove(currentR);
            currentR--;
        }
        
        // Store the answer for this query
        answers[queries[i].idx] = /* result for this query */;
    }
}

int main() {
    int n, q;
    cin >> n >> q;
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }
    for (int i = 0; i < q; i++) {
        cin >> queries[i].l >> queries[i].r;
        queries[i].l--; // Convert to 0-based index
        queries[i].r--; // Convert to 0-based index
        queries[i].idx = i;
    }

    process_queries(n, q);

    for (int i = 0; i < q; i++) {
        cout << answers[i] << endl;
    }

    return 0;
}
```

### Explanation

1. **Define the Query structure:**
   The `Query` structure stores the left and right endpoints of a query and its index.

2. **MO's Comparator:**
   The `mo_compare` function sorts the queries by their block number and then by the right endpoint within the same block.

3. **Add and Remove Functions:**
   `add(int index)` and `remove(int index)` manage the addition and removal of elements from the current range. You should implement these functions based on the specific problem you are solving.

4. **Processing Queries:**
   The `process_queries` function sorts the queries and processes them. It maintains the current range `[currentL, currentR]` and adjusts it to match the range of each query while updating the data structure accordingly.

5. **Main Function:**
   The `main` function reads input, processes the queries, and outputs the results.

This implementation can be adjusted based on the specific details and requirements of the problem you are working on.

### 1. Algorithms & Data Structures (C++): Sorting using Heap

Sorting using a heap is a technique that utilizes the heap data structure to efficiently sort elements in an array. In C++, you can implement heap sort using the `priority_queue` container from the Standard Template Library (STL), or you can implement your own heap data structure.

Here's a basic implementation of heap sort using the `priority_queue` container:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

// Function to perform heap sort
void heapSort(vector<int>& arr) {
    // Create a max heap
    priority_queue<int, vector<int>, less<int>> maxHeap(arr.begin(), arr.end());
    
    // Pop elements from the heap and put them back into the array
    for (int i = arr.size() - 1; i >= 0; i--) {
        arr[i] = maxHeap.top();
        maxHeap.pop();
    }
}

int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    
    cout << "Original array: ";
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;
    
    // Perform heap sort
    heapSort(arr);
    
    cout << "Sorted array: ";
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;
    
    return 0;
}
```

This code first creates a max heap from the input array using `priority_queue` with the `less` comparator, which ensures that the maximum element is always at the top of the heap. Then, it pops elements from the heap and puts them back into the array, effectively sorting the array in non-decreasing order.

If you want to implement your own heap data structure, you can use arrays or vectors and manually implement heap operations such as heapify, buildHeap, and extractMax. This approach provides more flexibility and control over the heap operations. Let me know if you'd like to see an implementation of heap sort using a custom heap data structure!

### 1. Algorithms & Data Structures (C++): Sorting with Comparator

Sorting with a comparator in C++ allows you to sort elements based on a custom ordering defined by a comparison function. This is particularly useful when you want to sort elements based on criteria other than their natural order. Here's how you can do it:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

// Define a custom comparison function
bool customComparator(int a, int b) {
    // Example: Sort integers in descending order
    return a > b;
}

int main() {
    std::vector<int> numbers = {5, 2, 7, 1, 9};

    // Sort using the custom comparator
    std::sort(numbers.begin(), numbers.end(), customComparator);

    // Print the sorted numbers
    for (int num : numbers) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this example, `std::sort()` is used to sort a vector of integers (`numbers`) using the custom comparator function `customComparator`. The `customComparator` function defines the custom ordering, in this case, sorting the numbers in descending order.

You can define custom comparators for sorting based on any criteria you want. For example, sorting strings based on their lengths, sorting custom objects based on certain attributes, etc. Just make sure your comparator function adheres to the requirements of the comparator used by the sorting algorithm (in this case, `std::sort()`).

### 1. Algorithms & Data Structures (C++): Sorting With Linked Lists

Sorting with linked lists involves arranging the elements in ascending or descending order within the list. Here's an example of how you can implement sorting algorithms like Merge Sort or Insertion Sort with linked lists in C++:

```cpp
#include <iostream>

using namespace std;

// Node structure for linked list
struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

// Function to merge two sorted linked lists
Node* merge(Node* left, Node* right) {
    if (!left) return right;
    if (!right) return left;

    Node* result = nullptr;

    if (left->data <= right->data) {
        result = left;
        result->next = merge(left->next, right);
    } else {
        result = right;
        result->next = merge(left, right->next);
    }

    return result;
}

// Function to split the linked list into two halves
void split(Node* head, Node** left, Node** right) {
    if (!head || !head->next) {
        *left = head;
        *right = nullptr;
        return;
    }

    Node* slow = head;
    Node* fast = head->next;

    while (fast) {
        fast = fast->next;
        if (fast) {
            slow = slow->next;
            fast = fast->next;
        }
    }

    *left = head;
    *right = slow->next;
    slow->next = nullptr;
}

// Merge Sort for linked list
void mergeSort(Node** headRef) {
    Node* head = *headRef;
    Node* left;
    Node* right;

    if (!head || !head->next) return;

    split(head, &left, &right);
    mergeSort(&left);
    mergeSort(&right);

    *headRef = merge(left, right);
}

// Function to insert a new node at the beginning of the linked list
void push(Node** headRef, int newData) {
    Node* newNode = new Node(newData);
    newNode->next = *headRef;
    *headRef = newNode;
}

// Function to print the linked list
void printList(Node* node) {
    while (node != nullptr) {
        cout << node->data << " ";
        node = node->next;
    }
    cout << endl;
}

int main() {
    Node* head = nullptr;

    // Example usage
    push(&head, 3);
    push(&head, 7);
    push(&head, 1);
    push(&head, 9);
    push(&head, 5);

    cout << "Original list: ";
    printList(head);

    mergeSort(&head);

    cout << "Sorted list: ";
    printList(head);

    return 0;
}
```

This code demonstrates how to implement Merge Sort for sorting a linked list. You can also implement other sorting algorithms like Insertion Sort or Bubble Sort for linked lists similarly by adjusting the logic of sorting.

### 1. Algorithms & Data Structures (C++): Sorting with Pivot : Quicksort

Quicksort is a popular sorting algorithm known for its efficiency, particularly for large datasets. It follows the "divide and conquer" strategy, where it partitions the array into smaller segments based on a chosen pivot element, and then recursively sorts each segment.

Here's a basic implementation of Quicksort in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to partition the array and return the index of the pivot element
int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high]; // Choosing the last element as the pivot
    int i = low - 1; // Index of the smaller element

    for (int j = low; j < high; j++) {
        // If the current element is smaller than or equal to the pivot
        if (arr[j] <= pivot) {
            i++;
            // Swap arr[i] and arr[j]
            swap(arr[i], arr[j]);
        }
    }
    // Swap arr[i + 1] and arr[high] (pivot)
    swap(arr[i + 1], arr[high]);
    return i + 1;
}

// Function to perform Quicksort recursively
void quicksort(vector<int>& arr, int low, int high) {
    if (low < high) {
        // Partitioning index
        int pi = partition(arr, low, high);

        // Recursively sort elements before and after partition
        quicksort(arr, low, pi - 1);
        quicksort(arr, pi + 1, high);
    }
}

// Function to print the array
void printArray(const vector<int>& arr) {
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;
}

int main() {
    vector<int> arr = {10, 7, 8, 9, 1, 5};
    int n = arr.size();
    cout << "Original array: ";
    printArray(arr);
    
    quicksort(arr, 0, n - 1);

    cout << "Sorted array: ";
    printArray(arr);

    return 0;
}
```

This implementation chooses the last element of the array as the pivot. It partitions the array into two segments, one containing elements smaller than the pivot, and the other containing elements greater than the pivot. Then it recursively applies the same process to each segment until the entire array is sorted.

### 1. Algorithms & Data Structures (C++): Sorting: Adaptive sorting algorithms

Adaptive sorting algorithms are those that can adjust their behavior based on the initial order of the input elements. They are particularly efficient when dealing with partially sorted data. Here are a few adaptive sorting algorithms commonly used in C++:

1. **Bubble Sort**:
   - Although not very efficient for large datasets, bubble sort is adaptive because it can detect when the input is already sorted. If no swaps are made during a pass through the array, the algorithm terminates early.
   - In the best-case scenario, when the array is already sorted, its time complexity reduces to O(n).

2. **Insertion Sort**:
   - Similar to bubble sort, insertion sort is adaptive because it efficiently handles nearly sorted arrays. It scans through the array and inserts each element into its correct position relative to the already sorted elements.
   - Its best-case time complexity is O(n) when the input array is already sorted.

3. **Merge Sort**:
   - Merge sort is not inherently adaptive in its traditional form because it always divides the array into halves regardless of the initial order. However, some adaptations can make it adaptive, like using insertion sort for small subarrays.
   - The adaptive version of merge sort switches to insertion sort for small subarrays, improving performance for nearly sorted arrays.

4. **Quick Sort**:
   - Quick sort can be adaptive to some extent, especially when using a good pivot selection strategy. If the pivot is chosen wisely, the partitioning process can lead to more balanced partitions, reducing the chances of worst-case behavior.
   - Randomized quick sort, which selects a random pivot, tends to be more adaptive because it reduces the probability of encountering worst-case scenarios.

5. **Intro Sort**:
   - Also known as introspective sort, this algorithm is a hybrid of quick sort, heap sort, and insertion sort. It begins with quick sort and switches to heap sort if the recursion depth exceeds a certain limit, and then switches to insertion sort for small subarrays.
   - The use of different sorting algorithms based on the characteristics of the input data makes intro sort highly adaptive.

These adaptive sorting algorithms are commonly used in practice because they can efficiently handle various input scenarios, including partially sorted data, without sacrificing overall performance.

### 1. Algorithms & Data Structures (C++): Sorting: Counting sort implementation

Certainly! Counting Sort is an efficient sorting algorithm for sorting elements in a given range. Here's a basic implementation of Counting Sort in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void countingSort(vector<int>& arr, int range) {
    int n = arr.size();
    vector<int> count(range + 1, 0); // Array to store count of individual elements

    // Store count of each element
    for (int i = 0; i < n; i++)
        count[arr[i]]++;

    // Change count[i] so that count[i] now contains actual position of this element in output array
    for (int i = 1; i <= range; i++)
        count[i] += count[i - 1];

    // Build the output array
    vector<int> output(n);
    for (int i = n - 1; i >= 0; i--) {
        output[count[arr[i]] - 1] = arr[i];
        count[arr[i]]--;
    }

    // Copy the output array to arr, so that arr now contains sorted numbers
    for (int i = 0; i < n; i++)
        arr[i] = output[i];
}

int main() {
    vector<int> arr = {4, 2, 2, 8, 3, 3, 1};
    int range = 8; // Range of input elements
    countingSort(arr, range);

    cout << "Sorted array is \n";
    for (int i = 0; i < arr.size(); i++)
        cout << arr[i] << " ";
    cout << endl;

    return 0;
}
```

This implementation assumes that the input array consists of non-negative integers and the range of input elements is known. The time complexity of Counting Sort is O(n+k), where n is the number of elements in the input array and k is the range of input.

### 1. Algorithms & Data Structures (C++): Sorting: Hoare's partitioning and Lomuto's partitioning

Hoare's partition scheme and Lomuto's partition scheme are two popular methods used in quicksort algorithms for partitioning arrays.

### Hoare's Partition Scheme

Hoare's partitioning scheme was proposed by Sir Charles Antony Richard Hoare, the inventor of the Quicksort algorithm. In this scheme, the array is partitioned based on a pivot element. Here's how it works:

1. Choose a pivot element from the array.
2. Initialize two pointers, one starting from the left (i) and the other from the right (j) of the array.
3. Move the left pointer towards the right until an element greater than or equal to the pivot is found.
4. Move the right pointer towards the left until an element less than or equal to the pivot is found.
5. Swap the elements at positions pointed by the left and right pointers.
6. Repeat steps 3-5 until the left pointer crosses the right pointer.
7. Swap the pivot element with the element at the position of the right pointer.

Here's a basic implementation of Hoare's partitioning scheme in C++:

```cpp
int hoarePartition(int arr[], int low, int high) {
    int pivot = arr[low];
    int i = low - 1, j = high + 1;
    while (true) {
        do {
            i++;
        } while (arr[i] < pivot);

        do {
            j--;
        } while (arr[j] > pivot);

        if (i >= j)
            return j;

        std::swap(arr[i], arr[j]);
    }
}
```

### Lomuto's Partition Scheme

Lomuto's partitioning scheme is simpler to implement compared to Hoare's. It was proposed by Nico Lomuto. Here's how it works:

1. Choose the last element of the array as the pivot element.
2. Initialize a pointer 'i' at the beginning of the array.
3. Iterate through the array from the beginning.
4. If an element is less than or equal to the pivot, swap it with the element at position 'i' and increment 'i'.
5. After iterating through the array, swap the pivot element with the element at position 'i'.
6. Now, all elements to the left of 'i' are less than or equal to the pivot, and all elements to the right are greater.

Here's a basic implementation of Lomuto's partitioning scheme in C++:

```cpp
int lomutoPartition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = low - 1;
    for (int j = low; j < high; j++) {
        if (arr[j] <= pivot) {
            i++;
            std::swap(arr[i], arr[j]);
        }
    }
    std::swap(arr[i + 1], arr[high]);
    return i + 1;
}
```

Both partitioning schemes are commonly used in the Quicksort algorithm, with Lomuto's being more intuitive for implementation and Hoare's generally being more efficient due to fewer swaps. However, both have their advantages and disadvantages depending on the scenario.

### 1. Algorithms & Data Structures (C++): Sorting: Hybrid algorithms Non-comparison based algorithms

Hybrid algorithms and non-comparison based algorithms in sorting offer different strategies for optimizing performance or handling specific data characteristics. Let's delve into each:

### Hybrid Algorithms

Hybrid sorting algorithms combine different sorting techniques to leverage the strengths of each. Commonly, they mix a comparison-based algorithm with a non-comparison based one to balance the trade-offs between time and space complexity. Here are some examples:

1. **Introsort**: Introsort is a hybrid sorting algorithm that starts with quicksort and switches to heapsort if the recursion depth exceeds a certain threshold. This prevents quicksort from degrading to its worst-case time complexity due to its vulnerability to certain types of inputs.

2. **TimSort**: TimSort is another hybrid sorting algorithm used in Python's `sorted()` function and Java's `Arrays.sort()`. It combines merge sort and insertion sort. It exploits the efficiency of merge sort on partially sorted arrays (common in real-world data) and the low overhead of insertion sort on small arrays.

3. **Merge Insertion Sort**: This hybrid combines merge sort with insertion sort. It uses merge sort for larger subarrays and switches to insertion sort for smaller subarrays, taking advantage of insertion sort's efficiency on small data sets.

### Non-comparison Based Algorithms

Non-comparison based sorting algorithms don't rely on comparing elements to determine their order. Instead, they exploit specific properties of the data to achieve sorting. These algorithms are often used when the comparison-based algorithms are not efficient due to large data sizes or unique data characteristics. Some examples include:

1. **Counting Sort**: Counting sort assumes that the input elements are integers within a known range. It counts the occurrences of each element and uses this information to place each element directly into its sorted position without comparisons. Counting sort has linear time complexity but requires additional space proportional to the range of input values.

2. **Radix Sort**: Radix sort sorts elements by processing individual digits or characters of the keys. It sorts from the least significant digit to the most significant digit using a stable sort algorithm such as counting sort or bucket sort. Radix sort is often used for sorting strings, integers, or other data with multiple keys.

3. **Bucket Sort**: Bucket sort divides the input into a finite number of buckets, each containing a subset of the input elements. It then sorts each bucket individually, typically using another sorting algorithm or recursively applying bucket sort. Bucket sort is efficient when the input is uniformly distributed over a range.

These hybrid and non-comparison based sorting algorithms offer alternative strategies for sorting data efficiently, depending on the characteristics of the input and the performance requirements. Choosing the right algorithm involves considering factors like the size of the data set, the distribution of values, and the desired time and space complexity.

### 1. Algorithms & Data Structures (C++): Sorting: Merge sort and stack memory visualization

Certainly! Let's start with a brief explanation of the merge sort algorithm and then visualize its process with stack memory.

### Merge Sort Algorithm

Merge sort is a popular sorting algorithm known for its efficiency and stability. It follows the divide-and-conquer strategy:

1. **Divide:** The unsorted list is divided into two sublists of roughly equal size.
2. **Conquer:** Each sublist is recursively sorted.
3. **Merge:** The sorted sublists are then merged to produce a single sorted list.

Here's a basic implementation of the merge sort algorithm in C++:

```cpp
#include <iostream>
#include <vector>

void merge(std::vector<int>& arr, int left, int middle, int right) {
    int n1 = middle - left + 1;
    int n2 = right - middle;
    
    std::vector<int> L(n1), R(n2);
    
    for (int i = 0; i < n1; ++i)
        L[i] = arr[left + i];
    for (int j = 0; j < n2; ++j)
        R[j] = arr[middle + 1 + j];
    
    int i = 0, j = 0, k = left;
    
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k++] = L[i++];
        } else {
            arr[k++] = R[j++];
        }
    }
    
    while (i < n1)
        arr[k++] = L[i++];
    while (j < n2)
        arr[k++] = R[j++];
}

void mergeSort(std::vector<int>& arr, int left, int right) {
    if (left < right) {
        int middle = left + (right - left) / 2;
        
        mergeSort(arr, left, middle);
        mergeSort(arr, middle + 1, right);
        
        merge(arr, left, middle, right);
    }
}

int main() {
    std::vector<int> arr = {12, 11, 13, 5, 6, 7};
    int arr_size = arr.size();

    std::cout << "Given array is \n";
    for (int i = 0; i < arr_size; i++)
        std::cout << arr[i] << " ";
    
    mergeSort(arr, 0, arr_size - 1);
    
    std::cout << "\nSorted array is \n";
    for (int i = 0; i < arr_size; i++)
        std::cout << arr[i] << " ";
    std::cout << std::endl;

    return 0;
}
```

### Stack Memory Visualization

Now, let's visualize the process of merge sort using stack memory. We'll consider each recursive call to `mergeSort()` as a new stack frame.

```plaintext
mergeSort(arr, 0, 5)   // Initial call

    mergeSort(arr, 0, 2)   // Left half
        mergeSort(arr, 0, 1)   // Left half
            mergeSort(arr, 0, 0)   // Left half
                Base case: Single element, return
            mergeSort(arr, 1, 1)   // Right half
                Base case: Single element, return
            merge(arr, 0, 0, 1)   // Merge sorted halves [0, 1]
        mergeSort(arr, 2, 2)   // Right half
            Base case: Single element, return
        merge(arr, 0, 1, 2)   // Merge sorted halves [0, 1, 2]
    mergeSort(arr, 3, 5)   // Right half
        mergeSort(arr, 3, 4)   // Left half
            Base case: Single element, return
        mergeSort(arr, 5, 5)   // Right half
            Base case: Single element, return
        merge(arr, 3, 4, 5)   // Merge sorted halves [3, 4, 5]
    merge(arr, 0, 2, 5)   // Merge sorted halves [0, 1, 2, 3, 4, 5]
```

This visualization shows how the merge sort algorithm recursively divides the array into smaller subarrays until reaching single-element subarrays, and then merges them back together in sorted order. Each recursive call is represented by a stack frame, and the merging process occurs during the stack unwinding phase.

### 1. Algorithms & Data Structures (C++): Sorting: Merge sort implementation

Sure, here's a simple implementation of the Merge Sort algorithm in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Merge function to merge two sorted subarrays [left...mid] and [mid+1...right]
void merge(vector<int>& arr, int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;

    // Create temporary arrays
    vector<int> L(n1), R(n2);

    // Copy data to temporary arrays L[] and R[]
    for (int i = 0; i < n1; i++)
        L[i] = arr[left + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[mid + 1 + j];

    // Merge the temporary arrays back into arr[left...right]
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

    // Copy the remaining elements of L[], if any
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    // Copy the remaining elements of R[], if any
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

// Merge sort function
void mergeSort(vector<int>& arr, int left, int right) {
    if (left < right) {
        // Same as (left+right)/2, but avoids overflow for large left and right
        int mid = left + (right - left) / 2;

        // Sort first and second halves
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);

        // Merge the sorted halves
        merge(arr, left, mid, right);
    }
}

// Utility function to print an array
void printArray(const vector<int>& arr) {
    for (int i = 0; i < arr.size(); i++)
        cout << arr[i] << " ";
    cout << endl;
}

// Driver code
int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    int arr_size = arr.size();

    cout << "Given array is \n";
    printArray(arr);

    mergeSort(arr, 0, arr_size - 1);

    cout << "\nSorted array is \n";
    printArray(arr);
    return 0;
}
```

This implementation includes the `mergeSort` function, which recursively divides the array into halves until each subarray has only one element, and then merges them back together in sorted order using the `merge` function. The `printArray` function is used to print the elements of the array. Finally, the `main` function demonstrates the usage of the Merge Sort algorithm by sorting a sample array and printing the sorted result.

### 1. Algorithms & Data Structures (C++): Sorting: Non-Comparison Based Sorting

Non-comparison based sorting algorithms are fascinating because they sort elements without directly comparing them. Here are a few notable non-comparison based sorting algorithms in C++:

1. **Counting Sort**: This algorithm works well when the range of numbers in the input array is not significantly greater than the number of elements to be sorted. It counts the occurrences of each element and uses this information to place elements directly into their sorted position.

   ```cpp
   void countingSort(int arr[], int n, int range) {
       int count[range+1] = {0};
       int output[n];

       // Count occurrences of each element
       for (int i = 0; i < n; i++)
           count[arr[i]]++;

       // Modify count array such that count[i] now contains actual position of this digit in output array
       for (int i = 1; i <= range; i++)
           count[i] += count[i - 1];

       // Build the output array
       for (int i = n - 1; i >= 0; i--) {
           output[count[arr[i]] - 1] = arr[i];
           count[arr[i]]--;
       }

       // Copy the output array to arr, so that arr now contains sorted numbers
       for (int i = 0; i < n; i++)
           arr[i] = output[i];
   }
   ```

2. **Radix Sort**: It sorts the elements by first sorting the digits of the numbers. It can be implemented using counting sort or bucket sort as a subroutine.

   ```cpp
   // A utility function to get maximum value in arr[]
   int getMax(int arr[], int n) {
       int mx = arr[0];
       for (int i = 1; i < n; i++)
           if (arr[i] > mx)
               mx = arr[i];
       return mx;
   }

   void countSort(int arr[], int n, int exp) {
       int output[n];
       int count[10] = {0};

       // Store count of occurrences in count[]
       for (int i = 0; i < n; i++)
           count[(arr[i] / exp) % 10]++;

       // Change count[i] so that count[i] now contains actual position of this digit in output[]
       for (int i = 1; i < 10; i++)
           count[i] += count[i - 1];

       // Build the output array
       for (int i = n - 1; i >= 0; i--) {
           output[count[(arr[i] / exp) % 10] - 1] = arr[i];
           count[(arr[i] / exp) % 10]--;
       }

       // Copy the output array to arr[] so that arr[] now contains sorted numbers
       for (int i = 0; i < n; i++)
           arr[i] = output[i];
   }

   void radixSort(int arr[], int n) {
       int m = getMax(arr, n);
       for (int exp = 1; m / exp > 0; exp *= 10)
           countSort(arr, n, exp);
   }
   ```

3. **Bucket Sort**: It divides the range of array elements into a number of buckets. Each bucket is then sorted individually, either using a different sorting algorithm or by recursively applying the bucket sort.

   ```cpp
   void bucketSort(float arr[], int n) {
       vector<float> buckets[n];

       // Put array elements into different buckets
       for (int i = 0; i < n; i++) {
           int bi = n * arr[i]; // Index in bucket
           buckets[bi].push_back(arr[i]);
       }

       // Sort individual buckets
       for (int i = 0; i < n; i++)
           sort(buckets[i].begin(), buckets[i].end());

       // Concatenate all buckets into arr[]
       int index = 0;
       for (int i = 0; i < n; i++)
           for (int j = 0; j < buckets[i].size(); j++)
               arr[index++] = buckets[i][j];
   }
   ```

These algorithms have different characteristics and are suitable for different scenarios based on the characteristics of the input data.

### 1. Algorithms & Data Structures (C++): Sorting: Quicksort implementation

Sure! Here's a simple implementation of the Quicksort algorithm in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to partition the array
int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high]; // Choose the last element as the pivot
    int i = low - 1; // Index of the smaller element

    for (int j = low; j < high; j++) {
        // If current element is smaller than or equal to pivot
        if (arr[j] <= pivot) {
            i++;
            // Swap arr[i] and arr[j]
            swap(arr[i], arr[j]);
        }
    }
    // Swap arr[i + 1] and arr[high] (or pivot)
    swap(arr[i + 1], arr[high]);
    return i + 1;
}

// Quicksort function
void quickSort(vector<int>& arr, int low, int high) {
    if (low < high) {
        // Partitioning index
        int pi = partition(arr, low, high);

        // Recursively sort elements before partition and after partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

// Function to print an array
void printArray(const vector<int>& arr) {
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;
}

int main() {
    vector<int> arr = {10, 7, 8, 9, 1, 5};
    int n = arr.size();
    cout << "Original array: ";
    printArray(arr);
    quickSort(arr, 0, n - 1);
    cout << "Sorted array: ";
    printArray(arr);
    return 0;
}
```

This implementation includes the `partition()` function which partitions the array and returns the partitioning index, and the `quickSort()` function which recursively applies the partitioning and sorting. Finally, there's a `printArray()` function to display the elements of the array.

### 1. Algorithms & Data Structures (C++): Sorting: Radix sort Radix sort implementation

Radix sort is a non-comparative integer sorting algorithm that sorts data with integer keys by grouping keys by individual digits. Here's a simple implementation of radix sort in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to get the maximum element from an array
int getMax(vector<int>& arr) {
    int max = arr[0];
    for (int i = 1; i < arr.size(); ++i) {
        if (arr[i] > max) {
            max = arr[i];
        }
    }
    return max;
}

// Counting sort for radix sort
void countingSort(vector<int>& arr, int exp) {
    int n = arr.size();
    vector<int> output(n);
    vector<int> count(10, 0);

    // Store count of occurrences in count[]
    for (int i = 0; i < n; i++) {
        count[(arr[i] / exp) % 10]++;
    }

    // Change count[i] so that count[i] contains
    // the actual position of this digit in output[]
    for (int i = 1; i < 10; i++) {
        count[i] += count[i - 1];
    }

    // Build the output array
    for (int i = n - 1; i >= 0; i--) {
        output[count[(arr[i] / exp) % 10] - 1] = arr[i];
        count[(arr[i] / exp) % 10]--;
    }

    // Copy the output array to arr[]
    for (int i = 0; i < n; i++) {
        arr[i] = output[i];
    }
}

// Radix Sort
void radixSort(vector<int>& arr) {
    // Find the maximum number to know the number of digits
    int max = getMax(arr);

    // Do counting sort for every digit. Note that
    // instead of passing digit number, exp is passed.
    // exp is 10^i where i is the current digit number
    for (int exp = 1; max / exp > 0; exp *= 10) {
        countingSort(arr, exp);
    }
}

// Function to print an array
void printArray(const vector<int>& arr) {
    for (int i = 0; i < arr.size(); i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

// Main function
int main() {
    vector<int> arr = {170, 45, 75, 90, 802, 24, 2, 66};
    cout << "Original array: ";
    printArray(arr);

    radixSort(arr);

    cout << "Sorted array: ";
    printArray(arr);

    return 0;
}
```

This implementation sorts an array of integers using radix sort. It first finds the maximum number to determine the number of digits, then performs counting sort for each digit from the least significant to the most significant digit. Finally, it returns the sorted array.

### 1. Algorithms & Data Structures (C++): Sorting: Sorting Algorithms Basics

Sorting algorithms are essential tools in computer science for rearranging elements in a specific order. Here's a brief overview of some fundamental sorting algorithms in C++:

1. **Bubble Sort**:
   - Bubble Sort repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order.
   - It has a time complexity of O(n^2) in the worst and average cases, making it inefficient for large lists.

2. **Selection Sort**:
   - Selection Sort divides the input list into two parts: the sublist of sorted elements and the sublist of unsorted elements.
   - It repeatedly selects the smallest (or largest) element from the unsorted sublist and moves it to the sorted sublist.
   - Selection Sort also has a time complexity of O(n^2).

3. **Insertion Sort**:
   - Insertion Sort builds the final sorted list one item at a time.
   - It iterates over the input list, shifting elements one position to the right to make room for the next element to be inserted in the correct position.
   - While it also has a time complexity of O(n^2), it performs well on small datasets and is efficient for nearly sorted lists.

4. **Merge Sort**:
   - Merge Sort is a divide-and-conquer algorithm that divides the input list into smaller sublists, sorts them recursively, and then merges them back together.
   - It has a time complexity of O(n log n) in all cases, making it more efficient than the previous algorithms for large datasets.
   - However, it requires additional space for the merging process.

5. **Quick Sort**:
   - Quick Sort also uses a divide-and-conquer strategy but works by selecting a "pivot" element from the list and partitioning the other elements into two sublists according to whether they are less than or greater than the pivot.
   - It then recursively sorts the sublists.
   - Quick Sort has an average-case time complexity of O(n log n) and is often faster in practice than Merge Sort due to its lower constant factors.
   - However, its worst-case time complexity is O(n^2) when the pivot selection is poor.

When choosing a sorting algorithm, consider factors such as the size of the dataset, the nature of the data (e.g., nearly sorted or completely random), and the desired performance characteristics.

### 1. Algorithms & Data Structures (C++): Sorting: Sorting What is stability in sorting?

In the context of sorting algorithms, "stability" refers to the property of maintaining the relative order of equal elements in the sorted output as they were in the original input. In other words, if two elements have the same key (value), a stable sorting algorithm will ensure that their order in the sorted sequence is the same as their order in the original sequence.

For example, suppose you have an array of objects representing students, and you want to sort them primarily by their age and then by their names. If two students have the same age, a stable sorting algorithm will ensure that their original order by name is preserved in the sorted array.

Stability is important in scenarios where you need to maintain the initial ordering of equivalent elements, as it can affect the correctness and predictability of your algorithm's behavior. Some sorting algorithms like merge sort and insertion sort are inherently stable, while others like quicksort and heapsort are not stable by default, though stable versions can be implemented.

### 1. Algorithms & Data Structures (C++): Sorting: What is the worst-case scenario for quicksort?

The worst-case scenario for quicksort occurs when the pivot selection consistently results in poorly balanced partitions, causing the algorithm to degrade into a quadratic time complexity. This typically happens when the chosen pivot is either the smallest or largest element in the array, leading to highly unbalanced partitions.

For instance, if the pivot chosen is always the smallest or largest element in the array, and the array is already sorted or nearly sorted, quicksort may exhibit its worst-case behavior. In this scenario, each partitioning step only reduces the size of the partition by one element, resulting in O(n^2) time complexity.

However, it's important to note that the worst-case scenario is relatively rare in practice, especially when using randomized pivot selection strategies or median-of-three pivot selection. In most cases, quicksort performs very efficiently with an average-case time complexity of O(n log n).

### 1. Algorithms & Data Structures (C++): Stability of Sort Algorithms

In computer science, the stability of a sorting algorithm refers to whether the algorithm maintains the relative order of equal elements in the sorted output as they were in the input. In other words, if two elements have the same key (value being used for sorting), a stable sorting algorithm will ensure that their relative order remains the same after sorting as it was in the original input.

Here's a rundown of the stability of some common sorting algorithms in C++:

1. **Bubble Sort**: Bubble sort is a stable sorting algorithm. It repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. Equal elements will not be swapped, so their relative order will remain unchanged.

2. **Insertion Sort**: Like bubble sort, insertion sort is stable. It builds the final sorted array one element at a time by repeatedly inserting the next element into the sorted portion of the array. When encountering equal elements, it places the new element after the existing equal elements, preserving their original order.

3. **Merge Sort**: Merge sort is also stable. It divides the input array into two halves, recursively sorts each half, and then merges them back together. During the merge step, when encountering equal elements, merge sort will pick elements from the left subarray first, preserving their relative order.

4. **Quick Sort**: Quick sort is not inherently stable. It works by selecting a 'pivot' element from the array and partitioning the other elements into two sub-arrays according to whether they are less than or greater than the pivot. Equal elements may end up on either side of the pivot, so the relative order may not be preserved.

5. **Heap Sort**: Heap sort is not stable. It first builds a heap from the input data and then repeatedly extracts the maximum element from the heap and rebuilds the heap. During the extraction process, the relative order of equal elements may change.

6. **Selection Sort**: Selection sort is not stable. It repeatedly selects the minimum element from the unsorted portion of the array and swaps it with the element at the beginning of the unsorted portion. Equal elements may get swapped, potentially changing their relative order.

When stability is a concern, stable sorting algorithms like bubble sort, insertion sort, and merge sort are preferred. However, for many applications, stability may not be a significant consideration, and other factors like time complexity or space complexity may be more important.

### 1. Algorithms & Data Structures (C++): Types of Sorting

In C++, there are various types of sorting algorithms, each with its own advantages and best use cases. Here's an overview of some commonly used sorting algorithms:

1. **Bubble Sort**:
   - Simplest sorting algorithm.
   - Iteratively compares adjacent elements and swaps them if they are in the wrong order.
   - Not efficient for large datasets due to its \(O(n^2)\) time complexity.

2. **Selection Sort**:
   - Finds the minimum element from the unsorted part and moves it to the beginning.
   - Repeats this process for the remaining elements.
   - Also inefficient for large datasets, with a time complexity of \(O(n^2)\).

3. **Insertion Sort**:
   - Builds the final sorted array one item at a time.
   - Efficient for small datasets or nearly sorted arrays.
   - Time complexity is \(O(n^2)\) but performs well in practice for small datasets.

4. **Merge Sort**:
   - A divide-and-conquer algorithm that divides the input array into two halves, sorts each half, and then merges them.
   - Efficient and stable sorting algorithm with a time complexity of \(O(n \log n)\).
   - Requires additional memory space for the merging process.

5. **Quick Sort**:
   - Another divide-and-conquer algorithm that picks an element as a pivot and partitions the array around the pivot.
   - It has an average-case time complexity of \(O(n \log n)\), but worst-case time complexity of \(O(n^2)\) can occur if the pivot selection is poor.
   - Widely used due to its efficiency and in-place sorting.

6. **Heap Sort**:
   - Builds a heap data structure from the input array and repeatedly extracts the maximum element from the heap, which results in a sorted array.
   - Time complexity is \(O(n \log n)\) and is not stable.
   - Useful when a stable sorting algorithm is not required and memory usage is a concern.

7. **Radix Sort**:
   - Sorts integers by grouping numbers by their individual digits.
   - It can be efficient for sorting integers within a specific range but may not be suitable for general-purpose sorting.
   - Time complexity depends on the number of digits or the range of the input integers.

Each sorting algorithm has its strengths and weaknesses, and the choice of algorithm depends on factors such as the size of the dataset, the distribution of elements, memory constraints, and stability requirements.

### 1. Algorithms & Data Structures (C++): Understanding Merge Sort

Merge sort is a popular sorting algorithm that follows the divide-and-conquer approach. It's efficient for sorting large datasets due to its stable \( O(n \log n) \) time complexity. Here's a breakdown of how it works:

1. **Divide**: The unsorted array is divided into two halves until each half contains only one element. This is done recursively until the base case is reached (i.e., an array with one or zero elements).

2. **Conquer**: Once the array is divided into single-element subarrays, the merge process begins. During this step, adjacent subarrays are merged in a sorted order.

3. **Merge**: The merge step combines the smaller sorted arrays into a single larger sorted array. This process involves comparing elements from the two subarrays and placing them in the correct order into a temporary array. Once all elements are merged, the temporary array becomes the sorted array.

Here's a basic implementation of merge sort in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Merge two subarrays of arr[]
void merge(vector<int>& arr, int left, int middle, int right) {
    int n1 = middle - left + 1;
    int n2 = right - middle;

    // Create temporary arrays
    vector<int> L(n1), R(n2);

    // Copy data to temporary arrays L[] and R[]
    for (int i = 0; i < n1; i++)
        L[i] = arr[left + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[middle + 1 + j];

    // Merge the temporary arrays back into arr[left..right]
    int i = 0, j = 0, k = left;
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

    // Copy the remaining elements of L[], if any
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    // Copy the remaining elements of R[], if any
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

// Main function to implement merge sort
void mergeSort(vector<int>& arr, int left, int right) {
    if (left < right) {
        // Find the middle point
        int middle = left + (right - left) / 2;

        // Sort first and second halves
        mergeSort(arr, left, middle);
        mergeSort(arr, middle + 1, right);

        // Merge the sorted halves
        merge(arr, left, middle, right);
    }
}

// Function to print an array
void printArray(const vector<int>& arr) {
    for (int i = 0; i < arr.size(); i++)
        cout << arr[i] << " ";
    cout << endl;
}

// Driver program to test the above functions
int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    int arrSize = arr.size();

    cout << "Given array is \n";
    printArray(arr);

    mergeSort(arr, 0, arrSize - 1);

    cout << "\nSorted array is \n";
    printArray(arr);
    return 0;
}
```

In this implementation:

- The `merge()` function merges two sorted subarrays.
- The `mergeSort()` function recursively divides the array into halves and sorts them.
- The `printArray()` function is a utility to print the elements of an array.
- In the `main()` function, we initialize an array, call `mergeSort()` to sort it, and then print the sorted array.

Merge sort's key advantage is its stable \( O(n \log n) \) time complexity, making it efficient for sorting large datasets.

### 1. Algorithms & Data Structures (C++): What is Sorting?

Sorting is the process of arranging elements in a specific order, typically in ascending or descending order, based on some defined criteria. In computer science, sorting is a fundamental operation used in various applications, such as searching, indexing, and data analysis.

The efficiency of sorting algorithms is often measured in terms of time complexity and space complexity. Time complexity refers to the amount of time an algorithm takes to execute as a function of the size of the input data. Space complexity refers to the amount of memory an algorithm requires to execute.

There are numerous sorting algorithms, each with its own advantages and disadvantages in terms of time and space complexity, stability, and adaptability to different types of data. Some common sorting algorithms include:

1. **Bubble Sort:** This algorithm repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. It continues iterating until the list is sorted.

2. **Insertion Sort:** This algorithm builds the final sorted array (or list) one item at a time by repeatedly taking the next item from the unsorted part of the array and inserting it into its correct position in the sorted part.

3. **Selection Sort:** Selection sort divides the input list into two parts: the sublist of items already sorted and the sublist of items remaining to be sorted. It repeatedly selects the smallest (or largest) element from the unsorted sublist and moves it to the end of the sorted sublist.

4. **Merge Sort:** Merge sort is a divide-and-conquer algorithm that divides the input array into two halves, sorts each half independently, and then merges the sorted halves to produce the final sorted array.

5. **Quick Sort:** Quick sort is another divide-and-conquer algorithm that selects a 'pivot' element from the array and partitions the other elements into two sub-arrays according to whether they are less than or greater than the pivot. It then recursively sorts the sub-arrays.

6. **Heap Sort:** Heap sort uses a binary heap data structure to represent the input array and repeatedly extracts the maximum (or minimum) element from the heap and reconstructs the heap until the array is sorted.

These are just a few examples, and there are many other sorting algorithms, each suitable for different scenarios and data characteristics. The choice of sorting algorithm depends on factors such as the size of the data, the distribution of the data, memory constraints, and the need for stability or adaptability.

### 1. Algorithms & Data Structures (C++): Which Sort Is Best?

Determining the "best" sorting algorithm depends on various factors such as the size of the data, the distribution of the data, memory constraints, and whether the data is partially sorted or nearly sorted. Here's a quick rundown of some common sorting algorithms in C++ and their typical use cases:

1. **Quicksort**:
   - Average Time Complexity: O(n log n)
   - Best Case: O(n log n)
   - Worst Case: O(n^2)
   - Space Complexity: O(log n) - O(n)
   - Quicksort is often the fastest general-purpose sorting algorithm and is widely used in practice. However, its worst-case time complexity makes it less favorable for certain scenarios.

2. **Merge Sort**:
   - Time Complexity: O(n log n)
   - Space Complexity: O(n)
   - Merge sort has a consistent O(n log n) time complexity and is stable. It's useful when stability is important or when the data is stored in linked lists.

3. **Heapsort**:
   - Time Complexity: O(n log n)
   - Space Complexity: O(1)
   - Heapsort has a consistent O(n log n) time complexity and is in-place. It's useful when space is limited as it requires no additional space beyond the array being sorted.

4. **Insertion Sort**:
   - Time Complexity: O(n^2)
   - Best Case: O(n)
   - Space Complexity: O(1)
   - Insertion sort is efficient for small datasets or nearly sorted data due to its simplicity and low overhead.

5. **Selection Sort**:
   - Time Complexity: O(n^2)
   - Space Complexity: O(1)
   - Selection sort is straightforward and easy to implement but generally less efficient than other sorting algorithms for large datasets.

6. **Bubble Sort**:
   - Time Complexity: O(n^2)
   - Best Case: O(n)
   - Space Complexity: O(1)
   - Bubble sort is rarely used in practice due to its poor performance, especially for large datasets. It's mainly used for educational purposes.

7. **Radix Sort**:
   - Time Complexity: O(nk)
   - Space Complexity: O(n + k)
   - Radix sort is efficient for sorting integers with a limited range of values. It's particularly useful when sorting numbers with fixed-length representations like integers or strings.

The "best" sorting algorithm depends on the specific requirements of the problem at hand. For general-purpose sorting, Quicksort, Merge Sort, and Heapsort are often preferred due to their efficiency. However, the choice may vary based on factors like input size, data distribution, stability, memory constraints, and whether the data is already partially sorted.

### 1. Algorithms & Data Structures (C++): Linked List: Bubble Sort on Linked List

Sure, implementing bubble sort on a linked list involves traversing the list while comparing adjacent elements and swapping them if they are in the wrong order. This process is repeated until the list is sorted. Here's how you can implement bubble sort on a linked list in C++:

```cpp
#include <iostream>

using namespace std;

// Node structure
struct Node {
    int data;
    Node* next;
    
    Node(int val) : data(val), next(nullptr) {}
};

// Linked list class
class LinkedList {
private:
    Node* head;

public:
    LinkedList() : head(nullptr) {}

    // Function to add a node at the end of the list
    void append(int val) {
        Node* newNode = new Node(val);
        if (!head) {
            head = newNode;
            return;
        }
        Node* temp = head;
        while (temp->next) {
            temp = temp->next;
        }
        temp->next = newNode;
    }

    // Function to print the linked list
    void display() {
        Node* temp = head;
        while (temp) {
            cout << temp->data << " ";
            temp = temp->next;
        }
        cout << endl;
    }

    // Function to perform bubble sort on the linked list
    void bubbleSort() {
        if (!head || !head->next)
            return; // Empty list or single element, no sorting needed

        bool swapped;
        Node* current;
        Node* lastSorted = nullptr;

        do {
            swapped = false;
            current = head;
            
            while (current->next != lastSorted) {
                if (current->data > current->next->data) {
                    swap(current->data, current->next->data);
                    swapped = true;
                }
                current = current->next;
            }
            lastSorted = current;
        } while (swapped);
    }
};

// Main function
int main() {
    LinkedList list;
    list.append(5);
    list.append(3);
    list.append(8);
    list.append(1);
    list.append(9);

    cout << "Original list: ";
    list.display();

    // Sorting the list
    list.bubbleSort();

    cout << "Sorted list: ";
    list.display();

    return 0;
}
```

In this code:

- `Node` represents each element in the linked list.
- `LinkedList` is the class representing the linked list and contains methods to append elements, display the list, and perform bubble sort.
- The `bubbleSort()` method implements the bubble sort algorithm on the linked list.
- In the `main()` function, a sample linked list is created and sorted using the `bubbleSort()` method.