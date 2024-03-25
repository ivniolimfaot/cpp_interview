
### 1. Algorithms & Data Structures (C++): Applying Heap to Compute the Top N Value

Using a heap is a great approach for finding the top N values efficiently. Here's a basic implementation in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

vector<int> findTopN(const vector<int>& nums, int N) {
    priority_queue<int, vector<int>, greater<int>> minHeap; // Min heap

    // Push first N elements into the heap
    for (int i = 0; i < N; ++i) {
        minHeap.push(nums[i]);
    }

    // Iterate through the remaining elements
    for (int i = N; i < nums.size(); ++i) {
        if (nums[i] > minHeap.top()) {
            minHeap.pop();
            minHeap.push(nums[i]);
        }
    }

    // Extract top N elements from the heap
    vector<int> topN;
    while (!minHeap.empty()) {
        topN.push_back(minHeap.top());
        minHeap.pop();
    }
    return topN;
}

int main() {
    vector<int> nums = {10, 7, 2, 14, 3, 8, 5, 11};
    int N = 3; // Find top 3 values
    vector<int> topN = findTopN(nums, N);

    cout << "Top " << N << " values: ";
    for (int num : topN) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}
```

In this code:

* We use a `priority_queue`, which is implemented as a heap, to maintain the top N elements.
* We push the first N elements into the heap.
* Then, we iterate through the remaining elements. If an element is greater than the smallest element in the heap (i.e., the top element), we remove the smallest element and insert the current element into the heap.
* Finally, we extract the top N elements from the heap.

You can adjust the value of N to find the top N values you're interested in.

### 1. Algorithms & Data Structures (C++): Applying Search() operation on Singly Linked List

In C++, implementing a search operation on a singly linked list involves traversing the list from the head node until the target value is found or the end of the list is reached. Here's a basic example of how you can implement the `search()` operation:

```cpp
#include <iostream>

// Define a Node structure for the linked list
struct Node {
    int data;
    Node* next;
    
    Node(int value) : data(value), next(nullptr) {}
};

// Define a LinkedList class
class LinkedList {
private:
    Node* head; // Pointer to the head of the list
    
public:
    LinkedList() : head(nullptr) {}
    
    // Function to insert a new node at the beginning of the list
    void insert(int value) {
        Node* newNode = new Node(value);
        newNode->next = head;
        head = newNode;
    }
    
    // Function to search for a value in the list
    bool search(int value) {
        Node* current = head;
        while (current != nullptr) {
            if (current->data == value)
                return true; // Value found
            current = current->next;
        }
        return false; // Value not found
    }
    
    // Function to display the elements of the list
    void display() {
        Node* current = head;
        while (current != nullptr) {
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }
    
    // Destructor to free memory allocated to the list
    ~LinkedList() {
        Node* current = head;
        while (current != nullptr) {
            Node* temp = current;
            current = current->next;
            delete temp;
        }
    }
};

int main() {
    LinkedList list;
    
    // Insert some elements into the list
    list.insert(5);
    list.insert(10);
    list.insert(15);
    list.insert(20);
    
    // Display the elements of the list
    std::cout << "List elements: ";
    list.display();
    
    // Search for elements in the list
    int valueToSearch = 10;
    if (list.search(valueToSearch))
        std::cout << valueToSearch << " found in the list." << std::endl;
    else
        std::cout << valueToSearch << " not found in the list." << std::endl;
    
    valueToSearch = 25;
    if (list.search(valueToSearch))
        std::cout << valueToSearch << " found in the list." << std::endl;
    else
        std::cout << valueToSearch << " not found in the list." << std::endl;
    
    return 0;
}
```

This code defines a basic singly linked list with operations to insert elements at the beginning and search for a value within the list. You can modify and extend this code as needed for your application.

### 1. Algorithms & Data Structures (C++): Array Implementation of heaps

Implementing a heap using an array is a common approach. In a binary heap, each node has at most two children, and in a max heap, the value of each node is greater than or equal to the values of its children. Conversely, in a min heap, each node is smaller than or equal to its children.

Here's a basic implementation of a max heap using an array in C++:

```cpp
#include <iostream>
#include <vector>

class MaxHeap {
private:
    std::vector<int> heap;

    // Helper function to heapify up (used in insert)
    void heapifyUp(int index) {
        int parent = (index - 1) / 2;
        while (index > 0 && heap[index] > heap[parent]) {
            std::swap(heap[index], heap[parent]);
            index = parent;
            parent = (index - 1) / 2;
        }
    }

    // Helper function to heapify down (used in extractMax)
    void heapifyDown(int index) {
        int left = 2 * index + 1;
        int right = 2 * index + 2;
        int largest = index;

        if (left < heap.size() && heap[left] > heap[largest])
            largest = left;
        if (right < heap.size() && heap[right] > heap[largest])
            largest = right;

        if (largest != index) {
            std::swap(heap[index], heap[largest]);
            heapifyDown(largest);
        }
    }

public:
    // Constructor
    MaxHeap() {}

    // Insert element into the heap
    void insert(int value) {
        heap.push_back(value);
        heapifyUp(heap.size() - 1);
    }

    // Extract the maximum element from the heap
    int extractMax() {
        if (heap.empty())
            throw std::out_of_range("Heap is empty");
        
        int max = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        heapifyDown(0);
        return max;
    }

    // Get the maximum element without removing it
    int getMax() {
        if (heap.empty())
            throw std::out_of_range("Heap is empty");
        
        return heap[0];
    }

    // Check if the heap is empty
    bool isEmpty() {
        return heap.empty();
    }
};

int main() {
    MaxHeap heap;

    heap.insert(10);
    heap.insert(20);
    heap.insert(15);
    heap.insert(30);

    std::cout << "Max element: " << heap.getMax() << std::endl;
    std::cout << "Extracted max element: " << heap.extractMax() << std::endl;
    std::cout << "Max element after extraction: " << heap.getMax() << std::endl;

    return 0;
}
```

In this implementation, the heap is stored in a vector (`std::vector<int> heap`). The `heapifyUp` function is used when inserting an element to maintain the heap property, and `heapifyDown` is used when extracting the maximum element. These functions ensure that the heap remains valid after each operation.

### 1. Algorithms & Data Structures (C++): Binary Heap

A binary heap is a fundamental data structure used to implement priority queues, which are data structures that allow efficient retrieval of the maximum or minimum element. It's a complete binary tree where each node satisfies the heap property, which is often defined as either the max-heap property or the min-heap property.

In a max-heap, the value of each node is greater than or equal to the values of its children. In a min-heap, the value of each node is less than or equal to the values of its children.

Here's a basic implementation of a binary heap in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class BinaryHeap {
private:
    vector<int> heap;

    // Helper functions to maintain heap property
    void heapifyUp(int index) {
        int parent = (index - 1) / 2;
        while (index > 0 && heap[index] > heap[parent]) {
            swap(heap[index], heap[parent]);
            index = parent;
            parent = (index - 1) / 2;
        }
    }

    void heapifyDown(int index) {
        int leftChild = 2 * index + 1;
        int rightChild = 2 * index + 2;
        int largest = index;

        if (leftChild < heap.size() && heap[leftChild] > heap[largest])
            largest = leftChild;

        if (rightChild < heap.size() && heap[rightChild] > heap[largest])
            largest = rightChild;

        if (largest != index) {
            swap(heap[index], heap[largest]);
            heapifyDown(largest);
        }
    }

public:
    void insert(int value) {
        heap.push_back(value);
        heapifyUp(heap.size() - 1);
    }

    int extractMax() {
        if (heap.empty()) {
            cerr << "Heap is empty!" << endl;
            return -1; // or throw an exception
        }

        int root = heap.front();
        swap(heap.front(), heap.back());
        heap.pop_back();
        heapifyDown(0);
        return root;
    }

    void printHeap() {
        for (int i : heap)
            cout << i << " ";
        cout << endl;
    }
};

int main() {
    BinaryHeap maxHeap;
    maxHeap.insert(5);
    maxHeap.insert(10);
    maxHeap.insert(3);
    maxHeap.insert(8);
    maxHeap.insert(1);

    cout << "Max heap: ";
    maxHeap.printHeap();

    cout << "Extracted max element: " << maxHeap.extractMax() << endl;
    cout << "Max heap after extraction: ";
    maxHeap.printHeap();

    return 0;
}
```

This code demonstrates the basic operations of a binary heap: insertion and extraction of the maximum element. The `heapifyUp` and `heapifyDown` functions ensure that the heap property is maintained after each insertion and extraction operation.

### 1. Algorithms & Data Structures (C++): Binary Heaps

Binary heaps are a fundamental data structure used to implement priority queues efficiently. They are a type of binary tree with two main variants: min-heap and max-heap. In a min-heap, the parent node's value is smaller than or equal to the values of its children, while in a max-heap, the parent node's value is greater than or equal to the values of its children.

Here's a basic overview of binary heaps in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class BinaryHeap {
private:
    vector<int> heap;

    // Helper functions
    int parent(int i) { return (i - 1) / 2; }
    int leftChild(int i) { return 2 * i + 1; }
    int rightChild(int i) { return 2 * i + 2; }

    void heapifyUp(int index) {
        while (index > 0 && heap[parent(index)] > heap[index]) {
            swap(heap[index], heap[parent(index)]);
            index = parent(index);
        }
    }

    void heapifyDown(int index) {
        int minIndex = index;
        int left = leftChild(index);
        int right = rightChild(index);

        if (left < heap.size() && heap[left] < heap[minIndex])
            minIndex = left;
        if (right < heap.size() && heap[right] < heap[minIndex])
            minIndex = right;

        if (index != minIndex) {
            swap(heap[index], heap[minIndex]);
            heapifyDown(minIndex);
        }
    }

public:
    // Constructor
    BinaryHeap() {}

    // Insertion
    void insert(int value) {
        heap.push_back(value);
        heapifyUp(heap.size() - 1);
    }

    // Extract min (for min-heap) or max (for max-heap)
    int extractRoot() {
        if (heap.empty())
            throw runtime_error("Heap is empty");

        int root = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        heapifyDown(0);

        return root;
    }

    // Get the root element without removing it
    int peek() {
        if (heap.empty())
            throw runtime_error("Heap is empty");

        return heap[0];
    }

    // Check if the heap is empty
    bool isEmpty() {
        return heap.empty();
    }
};

int main() {
    BinaryHeap minHeap;

    minHeap.insert(3);
    minHeap.insert(2);
    minHeap.insert(1);
    minHeap.insert(4);
    minHeap.insert(5);

    while (!minHeap.isEmpty()) {
        cout << minHeap.extractRoot() << " ";
    }

    return 0;
}
```

This code demonstrates the basic operations of a binary heap, including insertion and extraction. You can further extend this implementation by adding functionalities like deleting a specific element, changing the value of a node, building a heap from an array, and more.

### 1. Algorithms & Data Structures (C++): Binary Heaps: How do you extract the max?

To extract the maximum element from a binary heap, which is typically implemented as a max-heap, you follow these steps:

1. Replace the root node, which contains the maximum element, with the last node of the heap.
2. Restore the heap property by "bubbling down" the new root node to its correct position in the heap.

Here's a step-by-step guide on how to extract the maximum element from a binary heap implemented in C++:

```cpp
#include <iostream>
#include <vector>
using namespace std;

// Function to maintain the heap property after removing the root
void heapifyDown(vector<int>& heap, int index) {
    int largest = index; // Initialize largest as root
    int left = 2 * index + 1; // Left child
    int right = 2 * index + 2; // Right child

    // If left child is larger than root
    if (left < heap.size() && heap[left] > heap[largest])
        largest = left;

    // If right child is larger than largest so far
    if (right < heap.size() && heap[right] > heap[largest])
        largest = right;

    // If largest is not root
    if (largest != index) {
        swap(heap[index], heap[largest]);
        // Recursively heapify the affected subtree
        heapifyDown(heap, largest);
    }
}

// Function to extract the maximum element from the heap
int extractMax(vector<int>& heap) {
    if (heap.empty()) {
        cout << "Heap is empty!" << endl;
        return -1; // or throw an exception
    }

    // Extracting the maximum element from the root
    int maxElement = heap[0];

    // Replace the root with the last element
    heap[0] = heap.back();
    heap.pop_back(); // Remove the last element

    // Restore heap property by heapifying down the root
    heapifyDown(heap, 0);

    return maxElement;
}

int main() {
    vector<int> heap = {30, 20, 10, 5, 15, 25}; // Example heap
    cout << "Heap before extraction: ";
    for (int num : heap)
        cout << num << " ";
    cout << endl;

    int maxElement = extractMax(heap);
    cout << "Max element extracted: " << maxElement << endl;

    cout << "Heap after extraction: ";
    for (int num : heap)
        cout << num << " ";
    cout << endl;

    return 0;
}
```

In this code:

* `heapifyDown()` function is used to maintain the heap property while moving down the tree from the root.
* `extractMax()` function extracts the maximum element by swapping the root with the last element and then restoring the heap property using `heapifyDown()`.
* The `main()` function demonstrates how to use these functions.

This approach ensures that the heap remains valid after extraction, with the next maximum element ready to be extracted efficiently.

### 1. Algorithms & Data Structures (C++): Binary Heaps: Larger Nodes Near the Bottom

In a binary heap, larger nodes are typically nearer to the bottom. This property is a result of the heap's structure and the way elements are inserted and removed.

Binary heaps are complete binary trees, meaning every level of the tree is fully filled, except possibly for the last level, which is filled from left to right. When elements are inserted into a binary heap, they are added at the next available position at the lowest level from left to right, maintaining the complete tree structure.

To maintain the heap property (either max-heap or min-heap), where each node is greater (or smaller) than its children, the element is then "bubbled up" or "percolated up" as necessary. This means that if the newly inserted element violates the heap property, it is swapped with its parent until the heap property is restored.

Since larger elements are repeatedly moved upwards in the heap during insertion, they tend to end up closer to the bottom as smaller elements are pushed down by the larger ones. This results in larger elements being concentrated towards the bottom of the heap.

Conversely, during deletion (assuming we are deleting the root element), the last element in the heap, which is at the bottom level and typically smaller, is moved to the root position. Then, it is "bubbled down" or "percolated down" by swapping it with its larger child until the heap property is restored. This process may result in smaller elements being moved towards the top.

So, the combination of insertion and deletion operations in a binary heap leads to larger nodes being positioned closer to the bottom. This property is often exploited in algorithms that use heaps for efficient sorting, priority queue operations, and more.

### 1. Algorithms & Data Structures (C++): Binomial and Fibonacci heaps

Binomial and Fibonacci heaps are two types of heap data structures used in computer science, particularly in the realm of priority queues. They both offer efficient implementations for various operations like insertion, deletion, and merging of heaps. Here's a brief overview of each:

#### Binomial Heap

Binomial heaps are a collection of binomial trees. A binomial tree of order k can be defined recursively as follows:

1. A binomial tree of order 0 is a single node.
2. A binomial tree of order k is formed by linking two binomial trees of order k-1 together, such that one becomes the leftmost child of the other.

Properties of binomial heaps:

* Each binomial tree in the heap follows the heap property (the key of each node is greater than or equal to the key of its parent).
* In a binomial heap, there can be at most one tree of any order.
* The number of nodes in a binomial tree of order k is \( 2^k \).
* Binomial heaps support insertion, union (merging), and extraction of the minimum element efficiently (in logarithmic time).

#### Fibonacci Heap

Fibonacci heaps are a more relaxed form of heap compared to binomial heaps. They consist of a collection of trees that are not necessarily binomial trees. Each tree follows the min-heap property, but the sibling relationship among trees is more flexible compared to binomial heaps.

Properties of Fibonacci heaps:

* Fibonacci heaps have a set of properties that make them very efficient for certain operations, although they can be more complex to implement.
* They have a constant time complexity for insertion and constant amortized time complexity for decrease key and delete min operations.
* The union (merge) operation is particularly efficient, taking constant time.
* However, Fibonacci heaps may not have strictly logarithmic time complexity for extract min operation. It's amortized logarithmic but in the worst case, it can approach O(n).

Both heap types have their strengths and weaknesses and are suitable for different use cases. Binomial heaps are often used when you need strict bounds on the time complexity of operations, while Fibonacci heaps are used when amortized bounds are acceptable and when you need fast merging of heaps.

### 1. Algorithms & Data Structures (C++): Common operations (Creation, Peek, sizeofheap) on Binary Heap

A binary heap is a complete binary tree that satisfies the heap property. In a min-heap, for every node \( i \) other than the root, the value of the parent node is less than or equal to the value of node \( i \). In a max-heap, it's the opposite: the value of the parent node is greater than or equal to the value of node \( i \). Here are common operations on a binary heap in C++:

#### Creation of a Binary Heap

```cpp
#include <vector>

// For a min-heap
void heapify(std::vector<int>& heap, int idx) {
    int smallest = idx;
    int left = 2 * idx + 1;
    int right = 2 * idx + 2;

    if (left < heap.size() && heap[left] < heap[smallest])
        smallest = left;

    if (right < heap.size() && heap[right] < heap[smallest])
        smallest = right;

    if (smallest != idx) {
        std::swap(heap[idx], heap[smallest]);
        heapify(heap, smallest);
    }
}

void buildHeap(std::vector<int>& heap) {
    for (int i = heap.size() / 2 - 1; i >= 0; --i) {
        heapify(heap, i);
    }
}
```

#### Peek Operation

```cpp
// For a min-heap
int peek(const std::vector<int>& heap) {
    if (!heap.empty()) {
        return heap[0];
    } else {
        // Handle empty heap case
        return INT_MIN; // or throw an exception
    }
}
```

#### Size of Heap

```cpp
int sizeofHeap(const std::vector<int>& heap) {
    return heap.size();
}
```

These functions assume a min-heap. For a max-heap, you just need to adjust the comparison operators accordingly.

### 1. Algorithms & Data Structures (C++): Creating a Heap

Creating a heap in C++ typically involves using the standard library's `priority_queue` or manually implementing a heap data structure. Here's how you can do it manually:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class MinHeap {
private:
    vector<int> heap;

    // Helper function to maintain the heap property after inserting an element
    void heapifyUp(int index) {
        int parent = (index - 1) / 2;
        while (index > 0 && heap[index] < heap[parent]) {
            swap(heap[index], heap[parent]);
            index = parent;
            parent = (index - 1) / 2;
        }
    }

    // Helper function to maintain the heap property after removing an element
    void heapifyDown(int index) {
        int left = 2 * index + 1;
        int right = 2 * index + 2;
        int smallest = index;

        if (left < heap.size() && heap[left] < heap[index])
            smallest = left;
        if (right < heap.size() && heap[right] < heap[smallest])
            smallest = right;

        if (smallest != index) {
            swap(heap[index], heap[smallest]);
            heapifyDown(smallest);
        }
    }

public:
    // Constructor
    MinHeap() {}

    // Insert an element into the heap
    void insert(int value) {
        heap.push_back(value);
        heapifyUp(heap.size() - 1);
    }

    // Remove the minimum element from the heap
    int extractMin() {
        if (heap.empty()) {
            cerr << "Heap is empty!" << endl;
            return -1; // or throw an exception
        }

        int minVal = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        heapifyDown(0);
        return minVal;
    }

    // Get the minimum element without removing it
    int getMin() {
        if (heap.empty()) {
            cerr << "Heap is empty!" << endl;
            return -1; // or throw an exception
        }
        return heap[0];
    }

    // Check if the heap is empty
    bool isEmpty() {
        return heap.empty();
    }
};

int main() {
    MinHeap minHeap;

    minHeap.insert(5);
    minHeap.insert(3);
    minHeap.insert(8);
    minHeap.insert(2);

    cout << "Minimum element: " << minHeap.extractMin() << endl;
    cout << "Minimum element: " << minHeap.getMin() << endl;

    return 0;
}
```

This code creates a MinHeap class that implements the heap data structure. You can modify it to create a MaxHeap by changing the comparison operators in the `heapifyUp` and `heapifyDown` functions.

### 1. Algorithms & Data Structures (C++): Creating Heaps using Insert function

Sure, creating a heap using the insert function in C++ is a common task in implementing data structures. Let's walk through how you can implement a max heap using the insert function.

First, you need a class to represent the max heap. Here's a simple implementation:

```cpp
#include <vector>

class MaxHeap {
private:
    std::vector<int> heap;

    // Helper function to move a node up the tree if it violates the heap property
    void heapifyUp(int index) {
        int parentIndex = (index - 1) / 2;
        while (index > 0 && heap[index] > heap[parentIndex]) {
            std::swap(heap[index], heap[parentIndex]);
            index = parentIndex;
            parentIndex = (index - 1) / 2;
        }
    }

public:
    // Function to insert a new element into the heap
    void insert(int value) {
        heap.push_back(value);
        heapifyUp(heap.size() - 1);
    }

    // Function to get the maximum element from the heap
    int getMax() {
        if (heap.empty()) {
            throw std::out_of_range("Heap is empty");
        }
        return heap[0];
    }

    // Function to check if the heap is empty
    bool isEmpty() {
        return heap.empty();
    }
};
```

Here's a brief explanation of the code:

* We have a private member variable `std::vector<int> heap;` to store the elements of the heap.
* The `heapifyUp` function is a helper function that moves a node up the tree if it violates the heap property (i.e., if the child is greater than its parent).
* The `insert` function adds a new element to the heap and then calls `heapifyUp` to maintain the heap property.
* The `getMax` function returns the maximum element from the heap (which is always at the root).
* The `isEmpty` function checks if the heap is empty.

You can use this `MaxHeap` class to create a max heap and insert elements into it like this:

```cpp
#include <iostream>

int main() {
    MaxHeap maxHeap;
    maxHeap.insert(5);
    maxHeap.insert(10);
    maxHeap.insert(3);
    maxHeap.insert(8);
    maxHeap.insert(1);

    std::cout << "Max element: " << maxHeap.getMax() << std::endl;

    return 0;
}
```

This will output:

```bash
Max element: 10
```

This is because 10 is the maximum element in the max heap we've created.

### 1. Algorithms & Data Structures (C++): Delete an element from Heap

Deleting an element from a heap in C++ typically involves two steps: finding the element to delete and then rearranging the heap to maintain its properties. If you're using a max-heap, you'll delete the maximum element, and if you're using a min-heap, you'll delete the minimum element.

Here's a basic outline of how you might implement this:

```cpp
#include <iostream>
#include <vector>

// Function to delete an element from a max-heap
void deleteFromMaxHeap(std::vector<int>& heap, int element) {
    // Find the index of the element to delete
    auto it = std::find(heap.begin(), heap.end(), element);
    if (it == heap.end()) {
        std::cout << "Element not found in the heap\n";
        return;
    }

    // Replace the element to delete with the last element
    *it = heap.back();
    heap.pop_back();

    // Heapify down from the element's position
    int index = it - heap.begin();
    int size = heap.size();
    while (true) {
        int left = 2 * index + 1;
        int right = 2 * index + 2;
        int largest = index;

        if (left < size && heap[left] > heap[largest])
            largest = left;

        if (right < size && heap[right] > heap[largest])
            largest = right;

        if (largest != index) {
            std::swap(heap[index], heap[largest]);
            index = largest;
        } else {
            break;
        }
    }
}

int main() {
    std::vector<int> maxHeap = {10, 8, 7, 6, 5, 3, 2};
    int elementToDelete = 7;

    std::cout << "Max Heap before deletion: ";
    for (int num : maxHeap)
        std::cout << num << " ";
    std::cout << std::endl;

    deleteFromMaxHeap(maxHeap, elementToDelete);

    std::cout << "Max Heap after deletion: ";
    for (int num : maxHeap)
        std::cout << num << " ";
    std::cout << std::endl;

    return 0;
}
```

This code defines a function `deleteFromMaxHeap` to delete an element from a max-heap. It finds the element, replaces it with the last element, and then heapifies down from the position of the replaced element to maintain the heap property. You can adjust it for a min-heap accordingly.

### 1. Algorithms & Data Structures (C++): Delete and Heapify

In C++, deleting elements from a data structure such as a heap typically involves two steps:

1. Deleting the element.
2. Re-organizing the data structure to maintain its properties, like the heap property in a heap data structure.

Here's how you can implement deletion and heapification for a max heap:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to perform heapify after deletion
void heapify(vector<int>& heap, int i, int n) {
    int largest = i; // Initialize largest as root
    int left = 2 * i + 1; // Left child
    int right = 2 * i + 2; // Right child

    // If left child is larger than root
    if (left < n && heap[left] > heap[largest])
        largest = left;

    // If right child is larger than largest so far
    if (right < n && heap[right] > heap[largest])
        largest = right;

    // If largest is not root
    if (largest != i) {
        swap(heap[i], heap[largest]);

        // Recursively heapify the affected sub-tree
        heapify(heap, largest, n);
    }
}

// Function to delete an element from the heap
void deleteElement(vector<int>& heap, int key) {
    // Find the index of key in heap
    auto it = find(heap.begin(), heap.end(), key);
    if (it == heap.end()) {
        cout << "Element not found in heap!" << endl;
        return;
    }

    // Get the index of the element
    int index = distance(heap.begin(), it);

    // Replace the key to be deleted with the last element
    heap[index] = heap.back();
    heap.pop_back();

    // Heapify the heap after deletion
    heapify(heap, index, heap.size());
}

int main() {
    vector<int> maxHeap = {10, 20, 15, 40, 50, 100, 25, 45};

    cout << "Max Heap before deletion: ";
    for (int num : maxHeap)
        cout << num << " ";
    cout << endl;

    int keyToDelete = 20;
    deleteElement(maxHeap, keyToDelete);

    cout << "Max Heap after deletion of " << keyToDelete << ": ";
    for (int num : maxHeap)
        cout << num << " ";
    cout << endl;

    return 0;
}
```

This code demonstrates how to delete an element from a max heap and then heapify the remaining elements to maintain the max heap property. You can modify it according to your needs, such as for a min heap or any other data structure.

### 1. Algorithms & Data Structures (C++): Delete entire Binary Heap

Deleting an entire binary heap typically involves deallocating memory for all nodes in the heap and resetting any necessary metadata. Here's how you can delete an entire binary heap implemented in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class BinaryHeap {
private:
    vector<int> heap;

    // Helper function to heapify down
    void heapifyDown(int index) {
        int left = 2 * index + 1;
        int right = 2 * index + 2;
        int smallest = index;

        if (left < heap.size() && heap[left] < heap[index]) {
            smallest = left;
        }

        if (right < heap.size() && heap[right] < heap[smallest]) {
            smallest = right;
        }

        if (smallest != index) {
            swap(heap[index], heap[smallest]);
            heapifyDown(smallest);
        }
    }

public:
    // Constructor
    BinaryHeap() {}

    // Destructor
    ~BinaryHeap() {
        heap.clear();
    }

    // Function to delete entire heap
    void deleteHeap() {
        heap.clear();
    }

    // Other heap operations...
};

int main() {
    BinaryHeap heap;

    // Insert elements into heap...

    // Delete the entire heap
    heap.deleteHeap();

    return 0;
}
```

In this implementation:

1. The `deleteHeap()` function simply clears the vector that stores the heap elements, effectively deallocating the memory used by the heap.
2. The destructor (`~BinaryHeap()`) also clears the vector, ensuring that memory is deallocated when the `BinaryHeap` object goes out of scope.

Remember, if there are any dynamically allocated resources within the heap nodes (like pointers to objects), you'll need to properly deallocate them before clearing the heap to avoid memory leaks.

### 1. Algorithms & Data Structures (C++): Deleting from Heap

In C++, deleting from a heap typically involves removing an element and then restoring the heap property by rearranging the elements as necessary. Here's a basic outline of how you can delete from a heap in C++:

```cpp
#include <iostream>
#include <vector>

// Function to restore heap property after removing an element
void heapify(std::vector<int>& heap, int index) {
    int largest = index; // Initialize largest as root
    int left = 2 * index + 1; // Left child
    int right = 2 * index + 2; // Right child

    // If left child is larger than root
    if (left < heap.size() && heap[left] > heap[largest])
        largest = left;

    // If right child is larger than largest so far
    if (right < heap.size() && heap[right] > heap[largest])
        largest = right;

    // If largest is not root
    if (largest != index) {
        std::swap(heap[index], heap[largest]);
        // Recursively heapify the affected sub-tree
        heapify(heap, largest);
    }
}

// Function to delete an element from the heap
void deleteFromHeap(std::vector<int>& heap, int value) {
    // Find the index of the element to be deleted
    auto it = std::find(heap.begin(), heap.end(), value);
    if (it == heap.end()) {
        std::cout << "Element not found in heap." << std::endl;
        return;
    }

    // Replace the element to be deleted with the last element
    *it = heap.back();
    heap.pop_back();

    // Restore heap property
    int index = std::distance(heap.begin(), it);
    heapify(heap, index);
}

int main() {
    std::vector<int> heap = {10, 20, 15, 30, 40}; // Example heap
    int elementToDelete = 20;

    std::cout << "Heap before deletion: ";
    for (int num : heap)
        std::cout << num << " ";
    std::cout << std::endl;

    // Deleting element from heap
    deleteFromHeap(heap, elementToDelete);

    std::cout << "Heap after deletion: ";
    for (int num : heap)
        std::cout << num << " ";
    std::cout << std::endl;

    return 0;
}
```

In this code:

* The `heapify()` function is used to restore the heap property after removing an element.
* The `deleteFromHeap()` function takes the heap and the value to be deleted as arguments.
* It first finds the index of the value in the heap.
* Then, it replaces the value with the last element of the heap and removes the last element.
* Finally, it calls `heapify()` to restore the heap property.

### 1. Algorithms & Data Structures (C++): Deletion from Heaps

Sure, I can explain how deletion from heaps works in C++.

In a heap, elements are stored in a way that allows for efficient retrieval of the maximum (in a max-heap) or minimum (in a min-heap) element. When you delete an element from a heap, you typically remove the root node (for a max-heap) or the minimum element (for a min-heap) and then adjust the heap structure to maintain the heap property.

Here's a basic overview of how deletion from a max-heap works in C++:

1. Swap the root node (maximum element) with the last node in the heap.
2. Remove the last node (previously the root node) from the heap.
3. Heapify the heap to restore the heap property. This involves moving the swapped element down the heap, swapping it with its largest child until the heap property is satisfied.

Here's a C++ implementation of deletion from a max-heap:

```cpp
#include <iostream>
#include <vector>
using namespace std;

// Function to perform heapify operation
void heapify(vector<int>& heap, int i, int heapSize) {
    int largest = i; // Initialize largest as root
    int leftChild = 2 * i + 1;
    int rightChild = 2 * i + 2;

    // If left child is larger than root
    if (leftChild < heapSize && heap[leftChild] > heap[largest])
        largest = leftChild;

    // If right child is larger than largest so far
    if (rightChild < heapSize && heap[rightChild] > heap[largest])
        largest = rightChild;

    // If largest is not root
    if (largest != i) {
        swap(heap[i], heap[largest]);

        // Recursively heapify the affected sub-tree
        heapify(heap, largest, heapSize);
    }
}

// Function to delete an element from the heap
void deleteFromHeap(vector<int>& heap, int value) {
    // Find the index of the element to be deleted
    int i;
    for (i = 0; i < heap.size(); i++) {
        if (heap[i] == value)
            break;
    }

    // If the element is not found
    if (i == heap.size()) {
        cout << "Element not found in heap." << endl;
        return;
    }

    // Swap the element with the last element
    swap(heap[i], heap[heap.size() - 1]);

    // Reduce the size of the heap
    heap.pop_back();

    // Heapify the heap
    for (int j = heap.size() / 2 - 1; j >= 0; j--)
        heapify(heap, j, heap.size());
}

int main() {
    vector<int> heap = {30, 20, 10, 5, 15, 25};

    cout << "Original Heap: ";
    for (int i : heap)
        cout << i << " ";
    cout << endl;

    deleteFromHeap(heap, 20);

    cout << "Heap after deletion: ";
    for (int i : heap)
        cout << i << " ";
    cout << endl;

    return 0;
}
```

This code demonstrates how to delete an element from a max-heap in C++. The `deleteFromHeap` function takes the heap and the value to be deleted as parameters, finds the index of the element to be deleted, swaps it with the last element, reduces the size of the heap, and then performs heapify operation to maintain the heap property.

### 1. Algorithms & Data Structures (C++): Deletion In Heaps - Sift Down

In the context of heaps, specifically binary heaps, deletion typically refers to removing the root element (the maximum or minimum depending on whether it's a max-heap or min-heap) and maintaining the heap property. Sift down, also known as heapify-down or trickle-down, is one of the techniques used to restore the heap property after deletion.

Here's how you can implement deletion using sift down in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to perform sift down operation to restore heap property
void siftDown(vector<int> &heap, int index) {
    int n = heap.size();
    int leftChild, rightChild, largest;

    while (true) {
        leftChild = 2 * index + 1;
        rightChild = 2 * index + 2;
        largest = index;

        // Compare with left child
        if (leftChild < n && heap[leftChild] > heap[largest])
            largest = leftChild;

        // Compare with right child
        if (rightChild < n && heap[rightChild] > heap[largest])
            largest = rightChild;

        // If the largest is not the current node, swap and continue
        if (largest != index) {
            swap(heap[index], heap[largest]);
            index = largest; // Update index for the next iteration
        } else {
            break; // If the heap property is satisfied, exit
        }
    }
}

// Function to delete the root element of the heap
void deleteRoot(vector<int> &heap) {
    int n = heap.size();
    if (n == 0)
        return; // Empty heap

    // Swap root with the last element
    swap(heap[0], heap[n - 1]);

    // Remove the last element
    heap.pop_back();

    // Restore heap property by sifting down from the root
    siftDown(heap, 0);
}

int main() {
    vector<int> maxHeap = {10, 5, 3, 6, 2, 8};
    
    cout << "Max Heap before deletion: ";
    for (int num : maxHeap) {
        cout << num << " ";
    }
    cout << endl;
    
    deleteRoot(maxHeap);
    
    cout << "Max Heap after deletion: ";
    for (int num : maxHeap) {
        cout << num << " ";
    }
    cout << endl;
    
    return 0;
}
```

In this code:

* `siftDown` function is used to restore the heap property starting from a given index.
* `deleteRoot` function removes the root element of the heap and then restores the heap property by performing a sift down operation starting from the root.

This implementation assumes a max-heap, but it can be easily modified for a min-heap by changing the comparison operators appropriately.

### 1. Algorithms & Data Structures (C++): Extract a node from Binary Heap

To extract a node from a binary heap in C++, you typically perform the following steps:

1. Remove the root node.
2. Replace the root with the last node of the heap.
3. Heapify the heap to maintain the heap property.

Here's a C++ implementation of these steps:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class BinaryHeap {
private:
    vector<int> heap;

    // Helper functions for heap operations
    void heapifyDown(int index) {
        int left = 2 * index + 1;
        int right = 2 * index + 2;
        int smallest = index;

        if (left < heap.size() && heap[left] < heap[index]) {
            smallest = left;
        }

        if (right < heap.size() && heap[right] < heap[smallest]) {
            smallest = right;
        }

        if (smallest != index) {
            swap(heap[index], heap[smallest]);
            heapifyDown(smallest);
        }
    }

public:
    // Constructor
    BinaryHeap() {}

    // Extract the minimum element from the heap
    int extractMin() {
        if (heap.empty()) {
            cerr << "Heap is empty!" << endl;
            return -1; // or any appropriate value indicating error
        }

        int minElement = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        heapifyDown(0);
        
        return minElement;
    }

    // Utility function to insert a new element into the heap
    void insert(int value) {
        heap.push_back(value);
        int index = heap.size() - 1;
        int parent = (index - 1) / 2;

        while (index > 0 && heap[parent] > heap[index]) {
            swap(heap[parent], heap[index]);
            index = parent;
            parent = (index - 1) / 2;
        }
    }

    // Display the heap elements
    void displayHeap() {
        for (int i = 0; i < heap.size(); ++i) {
            cout << heap[i] << " ";
        }
        cout << endl;
    }
};

int main() {
    BinaryHeap minHeap;
    minHeap.insert(10);
    minHeap.insert(20);
    minHeap.insert(15);
    minHeap.insert(40);
    minHeap.insert(50);

    cout << "Min Heap: ";
    minHeap.displayHeap();

    int extracted = minHeap.extractMin();
    cout << "Extracted element: " << extracted << endl;

    cout << "Min Heap after extraction: ";
    minHeap.displayHeap();

    return 0;
}
```

This code demonstrates a binary heap implemented as a min heap. The `extractMin()` function is responsible for extracting the minimum element from the heap and maintaining the heap property by heapifying down.

### 1. Algorithms & Data Structures (C++): Find Median from Data Stream - Heaps

To find the median from a data stream efficiently, you can use two heaps: a max heap to store the smaller half of the elements, and a min heap to store the larger half. This allows us to access the median in constant time.

Here's how you can implement this in C++:

```cpp
#include <iostream>
#include <queue>
#include <vector>
using namespace std;

class MedianFinder {
    priority_queue<int> maxHeap; // Max heap for the smaller half
    priority_queue<int, vector<int>, greater<int>> minHeap; // Min heap for the larger half

public:
    void addNum(int num) {
        // Add the number to the appropriate heap
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
    
    double findMedian() {
        if (maxHeap.size() == minHeap.size()) {
            return (maxHeap.top() + minHeap.top()) / 2.0;
        } else {
            return maxHeap.top();
        }
    }
};

int main() {
    MedianFinder mf;
    mf.addNum(1);
    mf.addNum(2);
    cout << "Median: " << mf.findMedian() << endl; // Output: 1.5
    mf.addNum(3); 
    cout << "Median: " << mf.findMedian() << endl; // Output: 2
    return 0;
}
```

In this implementation, we maintain two heaps. The max heap contains the smaller half of the elements, while the min heap contains the larger half. We ensure that the size of the max heap is always equal to or one greater than the size of the min heap. This ensures that the median can be found in constant time. When the total number of elements is odd, the median is the top element of the max heap. When it's even, the median is the average of the top elements of both heaps.

### 1. Algorithms & Data Structures (C++): Formal Definition of Heap

In computer science, a heap is a specialized tree-based data structure that satisfies the heap property. The heap property varies depending on whether it's a min-heap or a max-heap.

A min-heap is a binary tree where for every node \( i \), the value of \( i \) is less than or equal to the values of its children (if any). This means that the smallest element is at the root.

A max-heap is a binary tree where for every node \( i \), the value of \( i \) is greater than or equal to the values of its children (if any). This means that the largest element is at the root.

Formally, a heap \( H \) can be defined as a binary tree with the following properties:

1. **Shape Property**: A heap is a complete binary tree. This means that all levels of the tree are fully filled except possibly for the last level, which is filled from left to right.

2. **Heap Property**: The key stored in each node is either greater than or equal to (in a max-heap) or less than or equal to (in a min-heap) the keys in the node's children, according to some total order.

In a heap implemented as an array, if a node is at index \( i \), its left child is at index \( 2i + 1 \) and its right child is at index \( 2i + 2 \).

In C++, heaps are often implemented using arrays or as binary trees. The STL (Standard Template Library) provides a heap data structure in the form of `std::priority_queue`. This is typically implemented as a max-heap but can be customized to behave as a min-heap.

### 1. Algorithms & Data Structures (C++): Heap

A heap is a specialized tree-based data structure that satisfies the heap property. There are two common types of heaps: binary heaps and d-ary heaps. In this response, I'll focus on binary heaps, which are the most commonly used.

### Binary Heap

A binary heap is a complete binary tree where each node has a value greater than or equal to (in a max heap) or less than or equal to (in a min heap) the values of its children.

#### Operations

1. **Insertion (Push)**: Add a new element to the heap.
2. **Extraction (Pop)**: Remove the root element from the heap.
3. **Peek**: View the top element of the heap without removing it.
4. **Heapify**: Reorganize the heap to satisfy the heap property.

#### Implementation (C++)

Here's a basic implementation of a max heap:

```cpp
#include <iostream>
#include <vector>

class MaxHeap {
private:
    std::vector<int> heap;

    void heapifyUp(int index) {
        int parent = (index - 1) / 2;
        while (index > 0 && heap[index] > heap[parent]) {
            std::swap(heap[index], heap[parent]);
            index = parent;
            parent = (index - 1) / 2;
        }
    }

    void heapifyDown(int index) {
        int left = 2 * index + 1;
        int right = 2 * index + 2;
        int largest = index;

        if (left < heap.size() && heap[left] > heap[largest])
            largest = left;
        if (right < heap.size() && heap[right] > heap[largest])
            largest = right;

        if (largest != index) {
            std::swap(heap[index], heap[largest]);
            heapifyDown(largest);
        }
    }

public:
    void push(int value) {
        heap.push_back(value);
        heapifyUp(heap.size() - 1);
    }

    int pop() {
        if (heap.empty()) {
            std::cerr << "Heap is empty\n";
            return -1; // or throw an exception
        }

        int top = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        heapifyDown(0);
        return top;
    }

    int peek() const {
        if (heap.empty()) {
            std::cerr << "Heap is empty\n";
            return -1; // or throw an exception
        }
        return heap[0];
    }

    bool isEmpty() const {
        return heap.empty();
    }
};

int main() {
    MaxHeap maxHeap;
    maxHeap.push(10);
    maxHeap.push(30);
    maxHeap.push(20);
    maxHeap.push(5);

    std::cout << "Max element: " << maxHeap.pop() << std::endl; // Output: 30

    return 0;
}
```

This implementation demonstrates the basic operations of a max heap: insertion (push), extraction (pop), peek, and checking if the heap is empty.

Remember, heaps are often used in algorithms like heap sort, priority queues, and graph algorithms like Dijkstra's algorithm. They offer efficient insertion and extraction of the maximum (or minimum) element.

### 1. Algorithms & Data Structures (C++): Heap / Priority Queue

Heap and priority queue are fundamental data structures used in computer science, particularly in algorithms for efficient sorting, searching, and graph algorithms like Dijkstra's algorithm.

**Heap:**

A heap is a complete binary tree where each node satisfies the heap property. In a max heap, the value of each node is greater than or equal to the values of its children. In a min heap, the value of each node is less than or equal to the values of its children.

In C++, heaps are commonly implemented using arrays. The parent-child relationship can be defined by simple arithmetic operations. For any node at index `i`:

* Its left child is at index `2*i + 1`
* Its right child is at index `2*i + 2`
* Its parent is at index `(i - 1) / 2`

Basic operations on a heap include insertion, deletion (removing the maximum or minimum element), and heapify (adjusting the heap to maintain the heap property after insertion or deletion).

**Priority Queue:**

A priority queue is an abstract data type similar to a regular queue or stack, but each element has a "priority" associated with it. In a priority queue, an element with higher priority is served before an element with lower priority.

In C++, the standard library provides a `std::priority_queue` which is implemented using heaps. You can use `std::priority_queue` to create max heaps or min heaps by specifying the comparator.

Here's a basic example of using `std::priority_queue` in C++:

```cpp
#include <iostream>
#include <queue>

int main() {
    // Creating a max heap
    std::priority_queue<int> maxHeap;

    // Inserting elements
    maxHeap.push(10);
    maxHeap.push(20);
    maxHeap.push(5);

    // Accessing the top element (maximum element)
    std::cout << "Top element of max heap: " << maxHeap.top() << std::endl;

    // Removing the top element
    maxHeap.pop();

    // Accessing the new top element
    std::cout << "Top element after pop: " << maxHeap.top() << std::endl;

    return 0;
}
```

This example demonstrates basic operations on a max heap implemented using `std::priority_queue`. You can similarly create a min heap by defining a custom comparator.

### 1. Algorithms & Data Structures (C++): Heap Adjust Operation

The "heap adjust" operation is a fundamental step in maintaining the heap property of a binary heap data structure, especially when performing heap operations like insertion, deletion, or heapifying an array. In the context of a binary heap, the adjust operation is often used to correct the heap structure when it has been violated due to an element being inserted or removed.

In a max-heap, the adjust operation ensures that the parent nodes have values greater than or equal to their children, and in a min-heap, it ensures that parent nodes have values less than or equal to their children.

Here's a brief overview of how the adjust operation typically works:

1. **Heapify Up (for Insertion):** When inserting a new element into a heap, the element is initially placed at the bottom of the heap (at the end of the array representation of the heap). The adjust operation then involves "bubbling up" the newly inserted element by swapping it with its parent node until the heap property is restored.

2. **Heapify Down (for Deletion):** When removing the root element from a heap, the last element in the array is moved to the root position, and then the adjust operation, known as "heapify down," is performed. This involves comparing the value of the new root with its children and swapping it with the larger (in a max-heap) or smaller (in a min-heap) child until the heap property is restored.

Here's a simple example of heapify up and heapify down operations in C++ for a max-heap:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Heapify Up (For Insertion)
void heapifyUp(vector<int>& heap, int index) {
    int parent = (index - 1) / 2;
    while (index > 0 && heap[index] > heap[parent]) {
        swap(heap[index], heap[parent]);
        index = parent;
        parent = (index - 1) / 2;
    }
}

// Heapify Down (For Deletion)
void heapifyDown(vector<int>& heap, int index, int heapSize) {
    int leftChild = 2 * index + 1;
    int rightChild = 2 * index + 2;
    int largest = index;

    if (leftChild < heapSize && heap[leftChild] > heap[largest]) {
        largest = leftChild;
    }

    if (rightChild < heapSize && heap[rightChild] > heap[largest]) {
        largest = rightChild;
    }

    if (largest != index) {
        swap(heap[index], heap[largest]);
        heapifyDown(heap, largest, heapSize);
    }
}

// Example usage
int main() {
    vector<int> heap = {40, 30, 25, 20, 15, 10, 5};

    // Insert 35 into the heap
    heap.push_back(35);
    heapifyUp(heap, heap.size() - 1);

    // Output the heap after insertion
    cout << "Heap after insertion: ";
    for (int num : heap) {
        cout << num << " ";
    }
    cout << endl;

    // Remove the root element
    swap(heap[0], heap.back());
    heap.pop_back();
    heapifyDown(heap, 0, heap.size());

    // Output the heap after deletion
    cout << "Heap after deletion: ";
    for (int num : heap) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}
```

In this example, `heapifyUp` and `heapifyDown` functions perform the adjust operations needed after insertion and deletion, respectively, to maintain the max-heap property.

### 1. Algorithms & Data Structures (C++): Heap as Array

In C++, you can implement a heap data structure using an array. A heap is a binary tree-based data structure where the parent node's value is always greater than or equal to (max heap) or less than or equal to (min heap) the values of its children. Here's a basic implementation of a max heap using an array:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class MaxHeap {
private:
    vector<int> heap;

    int parent(int i) { return (i - 1) / 2; }
    int leftChild(int i) { return 2 * i + 1; }
    int rightChild(int i) { return 2 * i + 2; }

    void heapifyUp(int i) {
        while (i > 0 && heap[parent(i)] < heap[i]) {
            swap(heap[parent(i)], heap[i]);
            i = parent(i);
        }
    }

    void heapifyDown(int i) {
        int maxIndex = i;
        int left = leftChild(i);
        int right = rightChild(i);

        if (left < heap.size() && heap[left] > heap[maxIndex])
            maxIndex = left;

        if (right < heap.size() && heap[right] > heap[maxIndex])
            maxIndex = right;

        if (i != maxIndex) {
            swap(heap[i], heap[maxIndex]);
            heapifyDown(maxIndex);
        }
    }

public:
    void insert(int value) {
        heap.push_back(value);
        heapifyUp(heap.size() - 1);
    }

    int extractMax() {
        if (heap.empty()) {
            cout << "Heap is empty\n";
            return -1; // or throw an exception
        }

        int max = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        heapifyDown(0);
        return max;
    }

    void printHeap() {
        cout << "Heap: ";
        for (int i = 0; i < heap.size(); ++i)
            cout << heap[i] << " ";
        cout << endl;
    }
};

int main() {
    MaxHeap maxHeap;
    maxHeap.insert(5);
    maxHeap.insert(3);
    maxHeap.insert(17);
    maxHeap.insert(10);
    maxHeap.insert(84);
    maxHeap.insert(19);
    maxHeap.insert(6);
    maxHeap.insert(22);
    maxHeap.insert(9);

    maxHeap.printHeap();

    cout << "Extracting max: " << maxHeap.extractMax() << endl;
    maxHeap.printHeap();

    return 0;
}
```

In this implementation:

* The `heap` vector holds the elements of the heap.
* The `heapifyUp` function is used when a new element is inserted into the heap.
* The `heapifyDown` function is used when an element is removed from the heap (extract operation).
* `insert` function inserts an element into the heap and maintains the heap property.
* `extractMax` function removes the maximum element (the root of the max heap) from the heap and returns it.
* `printHeap` function is used to print the elements of the heap.

### 1. Algorithms & Data Structures (C++): Heap as CBT

Sure, let's delve into how you can implement a heap as a complete binary tree (CBT) in C++.

A complete binary tree is a binary tree in which every level, except possibly the last, is completely filled, and all nodes are as far left as possible. This property makes it very suitable for implementing a heap.

Here's a basic implementation of a max heap using a complete binary tree structure in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class MaxHeap {
private:
    vector<int> heap;

    // Helper function to maintain the heap property by swapping elements up
    void heapifyUp(int index) {
        while (index > 0 && heap[parent(index)] < heap[index]) {
            swap(heap[parent(index)], heap[index]);
            index = parent(index);
        }
    }

    // Helper function to maintain the heap property by swapping elements down
    void heapifyDown(int index) {
        int maxIndex = index;
        int left = leftChild(index);
        int right = rightChild(index);

        if (left < heap.size() && heap[left] > heap[maxIndex]) {
            maxIndex = left;
        }

        if (right < heap.size() && heap[right] > heap[maxIndex]) {
            maxIndex = right;
        }

        if (index != maxIndex) {
            swap(heap[index], heap[maxIndex]);
            heapifyDown(maxIndex);
        }
    }

public:
    // Constructor
    MaxHeap() {}

    // Helper functions to get parent, left child, and right child indices
    int parent(int index) { return (index - 1) / 2; }
    int leftChild(int index) { return 2 * index + 1; }
    int rightChild(int index) { return 2 * index + 2; }

    // Function to insert a new element into the heap
    void insert(int value) {
        heap.push_back(value);
        heapifyUp(heap.size() - 1);
    }

    // Function to remove the maximum element from the heap
    int extractMax() {
        if (heap.empty()) {
            cout << "Heap is empty!" << endl;
            return -1; // or throw an exception
        }

        int max = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        heapifyDown(0);
        return max;
    }

    // Function to get the maximum element from the heap
    int getMax() {
        if (heap.empty()) {
            cout << "Heap is empty!" << endl;
            return -1; // or throw an exception
        }
        return heap[0];
    }

    // Function to check if the heap is empty
    bool isEmpty() {
        return heap.empty();
    }
};

int main() {
    MaxHeap maxHeap;
    
    maxHeap.insert(5);
    maxHeap.insert(10);
    maxHeap.insert(3);
    maxHeap.insert(7);
    maxHeap.insert(1);
    
    cout << "Max element: " << maxHeap.getMax() << endl;
    
    maxHeap.extractMax();
    
    cout << "Max element after extraction: " << maxHeap.getMax() << endl;

    return 0;
}
```

In this implementation:

* The heap is stored in a vector.
* The `heapifyUp()` function is used to maintain the max heap property by swapping elements upwards after insertion.
* The `heapifyDown()` function is used to maintain the max heap property by swapping elements downwards after extraction.
* The `insert()` function inserts a new element into the heap and maintains the heap property.
* The `extractMax()` function removes the maximum element from the heap and maintains the heap property.
* The `getMax()` function returns the maximum element from the heap without removing it.
* The `isEmpty()` function checks whether the heap is empty or not.

This is a basic implementation of a max heap using a complete binary tree structure in C++. You can extend and customize it further based on your requirements.

### 1. Algorithms & Data Structures (C++): Heap as Priority Queue

Sure, I'd be happy to explain!

In C++, a heap can be implemented as a priority queue. A heap is a specialized tree-based data structure that satisfies the heap property. The heap property states that in a max heap, for every node 'i' other than the root, the value of the node is at most the value of its parent. Conversely, in a min heap, for every node 'i' other than the root, the value of the node is at least the value of its parent.

A priority queue is an abstract data type similar to a regular queue or stack, but each element has a priority associated with it. In a priority queue, an element with higher priority is served before an element with lower priority. Priority queues are typically implemented using heaps because heaps provide efficient operations for maintaining the highest (or lowest) priority element.

Here's a simple implementation of a priority queue using a max heap in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

class MaxHeap {
private:
    vector<int> heap;

    void heapifyUp(int index) {
        int parent = (index - 1) / 2;
        while (index > 0 && heap[index] > heap[parent]) {
            swap(heap[index], heap[parent]);
            index = parent;
            parent = (index - 1) / 2;
        }
    }

    void heapifyDown(int index) {
        int left = 2 * index + 1;
        int right = 2 * index + 2;
        int largest = index;

        if (left < heap.size() && heap[left] > heap[largest])
            largest = left;
        if (right < heap.size() && heap[right] > heap[largest])
            largest = right;

        if (largest != index) {
            swap(heap[index], heap[largest]);
            heapifyDown(largest);
        }
    }

public:
    void insert(int val) {
        heap.push_back(val);
        heapifyUp(heap.size() - 1);
    }

    int extractMax() {
        if (heap.empty()) {
            cerr << "Heap is empty!" << endl;
            return -1; // or throw an exception
        }

        int maxVal = heap.front();
        heap[0] = heap.back();
        heap.pop_back();
        heapifyDown(0);

        return maxVal;
    }

    bool isEmpty() {
        return heap.empty();
    }
};

int main() {
    MaxHeap pq;
    pq.insert(10);
    pq.insert(30);
    pq.insert(20);
    pq.insert(5);

    while (!pq.isEmpty()) {
        cout << pq.extractMax() << " ";
    }
    cout << endl;

    return 0;
}
```

In this implementation:

* `heap` is represented as a vector, where each element represents a node in the heap.
* `heapifyUp` and `heapifyDown` functions maintain the heap property by fixing violations during insertions and extractions.
* `insert` inserts a new element into the heap and maintains the heap property by performing a heapify-up operation.
* `extractMax` removes and returns the maximum element (the root) from the heap and maintains the heap property by performing a heapify-down operation.
* `isEmpty` checks if the priority queue is empty.

This implementation demonstrates how you can use a max heap to implement a priority queue, where elements with higher values (higher priority) are served before elements with lower values.

### 1. Algorithms & Data Structures (C++): Heap Build

In C++, you can implement a heap data structure using an array representation. To build a heap from an array, you typically start from the last non-leaf node and heapify down to the root. Here's a basic implementation of building a max heap:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to heapify a subtree rooted at index i
// n is the size of heap
void heapify(vector<int>& arr, int n, int i) {
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

// Function to build a max heap
void buildHeap(vector<int>& arr) {
    int n = arr.size();

    // Index of the last non-leaf node
    int startIdx = (n / 2) - 1;

    // Perform reverse level order traversal
    // from the last non-leaf node and heapify each node
    for (int i = startIdx; i >= 0; i--) {
        heapify(arr, n, i);
    }
}

// Utility function to print an array
void printArray(vector<int>& arr) {
    for (int i : arr) {
        cout << i << " ";
    }
    cout << endl;
}

// Driver code
int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    cout << "Original array: ";
    printArray(arr);

    // Build heap
    buildHeap(arr);

    cout << "Max Heap: ";
    printArray(arr);

    return 0;
}
```

This code first defines a function `heapify` to maintain the heap property. Then, `buildHeap` uses `heapify` to build the heap from an array by starting from the last non-leaf node and calling `heapify` on each node in reverse level order traversal. Finally, in the `main` function, it demonstrates how to use `buildHeap` to convert an array into a max heap.

### 1. Algorithms & Data Structures (C++): Heap CBT and its

In computer science, a Complete Binary Tree (CBT) is a binary tree in which every level, except possibly the last, is completely filled, and all nodes are as far left as possible. This structure has some interesting properties and applications, particularly in the realm of heap data structures.

A heap is a specialized tree-based data structure that satisfies the heap property. The heap property can be of two types: the max-heap property and the min-heap property. In a max-heap, for any given node \( i \), the value of \( i \)'s parent is greater than or equal to the value of \( i \). In a min-heap, the value of \( i \)'s parent is less than or equal to the value of \( i \).

A heap can be represented efficiently using a CBT. Storing a heap in a CBT ensures that the structure remains balanced, with the benefit of being able to store the tree in a flat array representation.

Here's a brief overview of how to represent a heap using a CBT in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class MinHeap {
private:
    vector<int> heap;

    // Helper function to heapify the subtree rooted at index i
    void heapify(int i) {
        int smallest = i;
        int left = 2 * i + 1;
        int right = 2 * i + 2;

        if (left < heap.size() && heap[left] < heap[smallest])
            smallest = left;
        if (right < heap.size() && heap[right] < heap[smallest])
            smallest = right;

        if (smallest != i) {
            swap(heap[i], heap[smallest]);
            heapify(smallest);
        }
    }

public:
    // Constructor to initialize an empty heap
    MinHeap() {}

    // Function to insert a new element into the heap
    void insert(int key) {
        heap.push_back(key);
        int i = heap.size() - 1;
        while (i > 0 && heap[(i - 1) / 2] > heap[i]) {
            swap(heap[i], heap[(i - 1) / 2]);
            i = (i - 1) / 2;
        }
    }

    // Function to get the minimum element from the heap
    int getMin() {
        if (heap.empty()) {
            cerr << "Heap is empty!" << endl;
            return -1; // or throw an exception
        }
        return heap[0];
    }

    // Function to extract the minimum element from the heap
    int extractMin() {
        if (heap.empty()) {
            cerr << "Heap is empty!" << endl;
            return -1; // or throw an exception
        }

        int root = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        heapify(0);

        return root;
    }

    // Function to check if the heap is empty
    bool isEmpty() {
        return heap.empty();
    }
};

int main() {
    MinHeap heap;

    heap.insert(3);
    heap.insert(2);
    heap.insert(1);
    heap.insert(15);
    heap.insert(5);
    heap.insert(4);
    heap.insert(45);

    cout << "Minimum element extracted: " << heap.extractMin() << endl;
    cout << "Minimum element extracted: " << heap.extractMin() << endl;

    cout << "Minimum element: " << heap.getMin() << endl;

    return 0;
}
```

In this implementation, we use a vector to represent the CBT. The heap property is maintained through the `insert`, `extractMin`, and `heapify` operations. The `heapify` function is crucial for maintaining the heap property after insertions and deletions.

### 1. Algorithms & Data Structures (C++): Heap Definition

In C++, a heap is a complete binary tree (or binary heap) that satisfies the heap property. The heap property states that for every node \( i \) other than the root:

* If it's a max-heap: The value of the parent node is greater than or equal to the values of its children.
* If it's a min-heap: The value of the parent node is less than or equal to the values of its children.

A heap can be implemented using an array, where the children of the node at index \( i \) are located at indices \( 2i + 1 \) (left child) and \( 2i + 2 \) (right child). Conversely, the parent of a node at index \( j \) is located at index \( \lfloor(j-1)/2 \rfloor \).

Here's a basic definition of a heap in C++:

```cpp
#include <vector>

// Define the Heap class
template<typename T>
class Heap {
private:
    std::vector<T> heapArray;
    bool isMaxHeap;

    // Helper functions for heapify operations
    void heapifyUp(int index);
    void heapifyDown(int index);

public:
    // Constructor
    Heap(bool isMaxHeap = true) : isMaxHeap(isMaxHeap) {}

    // Insert a new element into the heap
    void insert(T value);

    // Remove the top element from the heap
    void removeTop();

    // Get the top element of the heap
    T getTop() const;

    // Check if the heap is empty
    bool isEmpty() const;

    // Get the size of the heap
    int size() const;
};

// Implementation of member functions
template<typename T>
void Heap<T>::insert(T value) {
    heapArray.push_back(value);
    heapifyUp(heapArray.size() - 1);
}

template<typename T>
void Heap<T>::removeTop() {
    if (isEmpty()) {
        // Handle empty heap
        return;
    }
    // Swap top element with last element
    std::swap(heapArray[0], heapArray.back());
    // Remove last element
    heapArray.pop_back();
    // Heapify down from root
    heapifyDown(0);
}

template<typename T>
T Heap<T>::getTop() const {
    if (isEmpty()) {
        // Handle empty heap
        throw std::out_of_range("Heap is empty");
    }
    return heapArray[0];
}

template<typename T>
bool Heap<T>::isEmpty() const {
    return heapArray.empty();
}

template<typename T>
int Heap<T>::size() const {
    return heapArray.size();
}

template<typename T>
void Heap<T>::heapifyUp(int index) {
    // Implement heapify up operation
    // ...
}

template<typename T>
void Heap<T>::heapifyDown(int index) {
    // Implement heapify down operation
    // ...
}
```

You would need to implement the `heapifyUp` and `heapifyDown` functions to maintain the heap property after insertion and deletion operations. Depending on whether it's a max-heap or a min-heap, you would implement these functions accordingly.

### 1. Algorithms & Data Structures (C++): Heap Deletion

In C++, when you delete an element from a heap (typically implemented as a binary heap), you usually remove the root element. This operation maintains the heap property by reorganizing the heap after deletion. Here's how you can delete an element from a heap in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to heapify a subtree rooted with the given index
// This function assumes that the subtrees are already heapified
void heapify(vector<int>& heap, int index) {
    int size = heap.size();
    int largest = index; // Initialize largest as root
    int left = 2 * index + 1; // left child
    int right = 2 * index + 2; // right child

    // If left child is larger than root
    if (left < size && heap[left] > heap[largest])
        largest = left;

    // If right child is larger than largest so far
    if (right < size && heap[right] > heap[largest])
        largest = right;

    // If largest is not root
    if (largest != index) {
        swap(heap[index], heap[largest]);
        // Recursively heapify the affected sub-tree
        heapify(heap, largest);
    }
}

// Function to delete the root of the heap
void deleteRoot(vector<int>& heap) {
    int size = heap.size();
    if (size == 0) {
        cout << "Heap is empty." << endl;
        return;
    }

    // Replace the root with the last element
    heap[0] = heap[size - 1];
    // Remove the last element
    heap.pop_back();
    // Heapify the root
    heapify(heap, 0);
}

// Function to print the heap
void printHeap(const vector<int>& heap) {
    for (int i = 0; i < heap.size(); ++i) {
        cout << heap[i] << " ";
    }
    cout << endl;
}

int main() {
    vector<int> heap = {10, 20, 15, 40, 50, 100, 25, 45};
    
    cout << "Heap before deletion: ";
    printHeap(heap);

    deleteRoot(heap);

    cout << "Heap after deletion: ";
    printHeap(heap);

    return 0;
}
```

In this code:

* `heapify()` function is used to maintain the heap property after deletion. It compares the root with its children and swaps with the larger child if necessary, recursively fixing any violations of the heap property.
* `deleteRoot()` function deletes the root of the heap by replacing it with the last element, removing the last element, and then heapifying the root.
* `printHeap()` function is a utility function to print the heap.

This code assumes that the heap is represented using a vector, where the root is at index 0.

### 1. Algorithms & Data Structures (C++): Heap Insertion

In C++, heap insertion typically involves adding a new element to a heap and then adjusting the heap structure to maintain its properties, usually ensuring that it remains a valid max-heap or min-heap.

Here's a general outline of how you can implement heap insertion in C++ for a max-heap (where the highest value is at the root):

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to adjust the max-heap after insertion
void maxHeapify(vector<int>& heap, int index) {
    int parent = (index - 1) / 2; // Calculate the parent index

    // Keep swapping with parent until the heap property is satisfied
    while (index > 0 && heap[index] > heap[parent]) {
        swap(heap[index], heap[parent]);
        index = parent;
        parent = (index - 1) / 2;
    }
}

// Function to insert an element into the max-heap
void insertIntoMaxHeap(vector<int>& heap, int value) {
    heap.push_back(value); // Add the new element to the end of the heap
    maxHeapify(heap, heap.size() - 1); // Adjust the heap to maintain its properties
}

int main() {
    vector<int> maxHeap = {30, 20, 10, 7, 9, 5}; // Example max-heap

    cout << "Original Max-Heap: ";
    for (int num : maxHeap)
        cout << num << " ";
    cout << endl;

    int newValue = 25;
    insertIntoMaxHeap(maxHeap, newValue);

    cout << "Max-Heap after insertion of " << newValue << ": ";
    for (int num : maxHeap)
        cout << num << " ";
    cout << endl;

    return 0;
}
```

In this code:

* `maxHeapify` function maintains the max-heap property by repeatedly swapping the newly inserted element with its parent until the heap property is satisfied.
* `insertIntoMaxHeap` function adds the new element to the end of the heap and then calls `maxHeapify` to adjust the heap.
* The `main` function demonstrates the insertion of a new element into the max-heap.

This code assumes a max-heap, where the parent node is always greater than or equal to its children. If you're working with a min-heap, where the parent is smaller than or equal to its children, you would adjust the comparisons accordingly.

### 1. Algorithms & Data Structures (C++): Heap Maximum Product

To find the maximum product of three integers in an array using a heap, you can follow these steps:

1. Construct a max heap using the given array.
2. Extract the top three elements from the heap, which will give you the three largest elements.
3. Return the product of these three elements.

Here's the implementation in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

// Comparator for max heap
struct MaxHeapComparator {
    bool operator()(const int& a, const int& b) {
        return a < b; // Change to a > b for max heap
    }
};

int maxProductOfThree(vector<int>& nums) {
    priority_queue<int, vector<int>, MaxHeapComparator> maxHeap;

    // Construct max heap
    for (int num : nums) {
        maxHeap.push(num);
    }

    // Extract top three elements
    int max1 = maxHeap.top();
    maxHeap.pop();
    int max2 = maxHeap.top();
    maxHeap.pop();
    int max3 = maxHeap.top();
    maxHeap.pop();

    // Return product of top three elements
    return max1 * max2 * max3;
}

int main() {
    vector<int> nums = {1, 5, 3, 9, 8, 7};
    cout << "Maximum product of three integers: " << maxProductOfThree(nums) << endl;
    return 0;
}
```

This code defines a custom comparator `MaxHeapComparator` for the priority queue to create a max heap. Then, it constructs the max heap using the given array and extracts the top three elements to calculate their product, which is returned as the maximum product of three integers.

### 1. Algorithms & Data Structures (C++): Heap Order Property

In the context of algorithms and data structures, the Heap Order Property refers to a fundamental characteristic of heaps, particularly in the context of binary heaps.

A binary heap is a complete binary tree where each node satisfies the heap property. There are two variations of heap properties:

1. **Max-Heap Property**: In a max-heap, for every node \( i \) other than the root, the value of the node is at most the value of its parent. In other words, the key of a node is always greater than or equal to the keys of its children. The highest key is in the root node.

2. **Min-Heap Property**: In a min-heap, for every node \( i \) other than the root, the value of the node is at least the value of its parent. In other words, the key of a node is always less than or equal to the keys of its children. The lowest key is in the root node.

In C++, you can implement a heap data structure using an array, where each element in the array corresponds to a node in the heap. The parent-child relationships can be defined based on the indices of elements in the array. For a node at index \( i \), its left child is at index \( 2i + 1 \) and its right child is at index \( 2i + 2 \).

Here's a simple example of checking the max-heap property for a node at index \( i \):

```cpp
bool isMaxHeap(int arr[], int n, int i) {
    // If node is a leaf node
    if (i >= n / 2)
        return true;

    // Check if the current node is greater than its children
    if (arr[i] >= arr[2*i + 1] && arr[i] >= arr[2*i + 2] &&
        isMaxHeap(arr, n, 2*i + 1) && isMaxHeap(arr, n, 2*i + 2))
        return true;
    
    return false;
}
```

This function recursively checks if the given array satisfies the max-heap property starting from the given index \( i \).

Similarly, you can define a function to check the min-heap property by comparing the current node with its children appropriately.

### 1. Algorithms & Data Structures (C++): Heap Problems

Heap problems are a staple of algorithmic coding interviews and are commonly encountered in competitive programming as well. Here are a few classic heap-related problems along with brief explanations:

1. **Heap Sort**: Although not a problem per se, implementing heap sort is a good exercise to understand how heaps work. It involves building a max heap from the array and repeatedly extracting the maximum element to sort the array.

2. **Kth Largest Element in an Array**: Given an array of integers, find the kth largest element. This can be efficiently solved using a min-heap of size k.

3. **Top K Frequent Elements**: Given a non-empty array of integers, return the k most frequent elements. This can be solved by using a max-heap where the elements are sorted based on their frequencies.

4. **Merge K Sorted Lists**: Given k sorted linked lists, merge them into one sorted linked list. This can be efficiently solved using a min-heap where each node of the heap stores the value and the pointer to the next element in the linked list.

5. **Sort Nearly Sorted Array**: Given a k-sorted array (each element is at most k positions away from its sorted position), efficiently sort the array. This can be solved using a min-heap of size k+1.

6. **Connect Ropes to Minimize Cost**: Given n ropes of different lengths, connect them into one rope with minimum cost. At each step, merge the two shortest ropes. This can be solved using a min-heap.

7. **Median of Stream**: Design a data structure that supports the following two operations:
    * void addNum(int num): Add a new integer num to the data structure.
    * double findMedian(): Return the median of all elements so far. This can be solved using two heaps, one max-heap to store the lower half of the elements and one min-heap to store the upper half.

These are just a few examples, but there are many other interesting problems that involve heaps. Understanding heaps and their operations is crucial for efficiently solving these problems.

### 1. Algorithms & Data Structures (C++): Heap Remove Min/ Max

In C++, removing the minimum or maximum element from a heap involves deleting the root node, which is typically the minimum or maximum element depending on whether it's a min-heap or a max-heap. Here's an example of how you can remove the minimum or maximum element from a heap in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

// Heapify down operation to maintain heap property after removal
void heapifyDown(std::vector<int>& heap, int index, int heapSize, bool isMinHeap) {
    int smallestOrLargest = index;
    int left = 2 * index + 1;
    int right = 2 * index + 2;

    if (left < heapSize && ((isMinHeap && heap[left] < heap[smallestOrLargest]) || (!isMinHeap && heap[left] > heap[smallestOrLargest]))) {
        smallestOrLargest = left;
    }
    if (right < heapSize && ((isMinHeap && heap[right] < heap[smallestOrLargest]) || (!isMinHeap && heap[right] > heap[smallestOrLargest]]))) {
        smallestOrLargest = right;
    }

    if (smallestOrLargest != index) {
        std::swap(heap[index], heap[smallestOrLargest]);
        heapifyDown(heap, smallestOrLargest, heapSize, isMinHeap);
    }
}

// Function to remove the minimum or maximum element from a heap
void removeRoot(std::vector<int>& heap, bool isMinHeap) {
    if (heap.empty()) {
        std::cout << "Heap is empty!" << std::endl;
        return;
    }

    int heapSize = heap.size();
    std::swap(heap[0], heap[heapSize - 1]);
    heap.pop_back();
    heapifyDown(heap, 0, heapSize - 1, isMinHeap);
}

int main() {
    // Example of using removeRoot function with a min-heap
    std::vector<int> minHeap = {3, 5, 8, 10, 4, 9, 7};
    removeRoot(minHeap, true); // Removing minimum element
    for (int num : minHeap) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    // Example of using removeRoot function with a max-heap
    std::vector<int> maxHeap = {10, 8, 7, 5, 4, 3, 1};
    removeRoot(maxHeap, false); // Removing maximum element
    for (int num : maxHeap) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

This code includes a `heapifyDown` function to maintain the heap property after removing the root element and a `removeRoot` function to remove the minimum or maximum element depending on whether it's a min-heap or a max-heap. Finally, it demonstrates how to use these functions with examples of both min-heap and max-heap.

### 1. Algorithms & Data Structures (C++): Heap vs other Data Structure

Heap data structure is particularly useful for implementing priority queues, where the highest (or lowest) priority element is always at the root. The key advantages of a heap compared to other data structures include:

1. **Efficient Priority Queue Operations**: Heaps support efficient insertion, deletion, and retrieval of the maximum (or minimum) element in logarithmic time complexity (\(O(\log n)\)).

2. **Space Efficiency**: Heaps can be implemented using arrays, providing good space efficiency compared to some other priority queue implementations.

3. **Versatility**: Heaps are versatile and can be used to solve various problems such as finding the \(k\) largest (or smallest) elements in a dataset efficiently.

However, heaps also have some limitations and may not be the best choice in all scenarios:

1. **No Efficient Search Operation**: While heaps excel at priority queue operations, searching for arbitrary elements within a heap is inefficient (\(O(n)\)) compared to other data structures like binary search trees (\(O(\log n)\)).

2. **No Support for Key-based Operations**: In a heap, elements are ordered based on their priority value and not by a key. If you need to access elements by a key rather than by priority, other data structures like hash tables or binary search trees might be more suitable.

3. **Not Suitable for All Types of Priority Queues**: While heaps are great for priority queues where the highest (or lowest) priority element is always at the root, they might not be the best choice for priority queues with complex priority rules or dynamic priority changes.

In summary, heaps are powerful data structures for implementing priority queues efficiently, especially when the highest (or lowest) priority element needs to be quickly accessible. However, the choice of data structure depends on the specific requirements of the problem at hand, and other data structures may be more suitable in certain scenarios.

### 1. Algorithms & Data Structures (C++): Heap: Helper Functions

Sure, heap data structures are fundamental in computer science, particularly for implementing priority queues and heap sort algorithms. In C++, you can implement a heap using arrays or using C++ Standard Library's `std::priority_queue`. Here's an example of some helper functions for managing heaps:

```cpp
#include <iostream>
#include <vector>

class Heap {
private:
    std::vector<int> heapArray;

    // Helper functions to maintain heap property
    void heapifyUp(int index) {
        int parentIndex = (index - 1) / 2;
        while (index > 0 && heapArray[index] > heapArray[parentIndex]) {
            std::swap(heapArray[index], heapArray[parentIndex]);
            index = parentIndex;
            parentIndex = (index - 1) / 2;
        }
    }

    void heapifyDown(int index) {
        int leftChildIndex = 2 * index + 1;
        int rightChildIndex = 2 * index + 2;
        int largestIndex = index;

        if (leftChildIndex < heapArray.size() && heapArray[leftChildIndex] > heapArray[largestIndex])
            largestIndex = leftChildIndex;
        if (rightChildIndex < heapArray.size() && heapArray[rightChildIndex] > heapArray[largestIndex])
            largestIndex = rightChildIndex;

        if (largestIndex != index) {
            std::swap(heapArray[index], heapArray[largestIndex]);
            heapifyDown(largestIndex);
        }
    }

public:
    // Constructor
    Heap() {}

    // Insertion operation
    void insert(int value) {
        heapArray.push_back(value);
        heapifyUp(heapArray.size() - 1);
    }

    // Removal operation
    int extractMax() {
        if (heapArray.empty()) {
            std::cerr << "Heap is empty!" << std::endl;
            return -1; // or throw an exception
        }

        int max = heapArray[0];
        heapArray[0] = heapArray.back();
        heapArray.pop_back();
        heapifyDown(0);
        return max;
    }

    // Utility function to check if the heap is empty
    bool isEmpty() const {
        return heapArray.empty();
    }

    // Utility function to get the size of the heap
    size_t size() const {
        return heapArray.size();
    }
};

int main() {
    Heap maxHeap;

    maxHeap.insert(10);
    maxHeap.insert(20);
    maxHeap.insert(15);
    maxHeap.insert(30);
    maxHeap.insert(25);

    std::cout << "Max Heap: ";
    while (!maxHeap.isEmpty()) {
        std::cout << maxHeap.extractMax() << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this code:

* `heapifyUp` ensures that when a new element is added, it is "bubbled up" to its correct position to maintain the heap property.
* `heapifyDown` ensures that when the root (max in this case) is removed, the last element is placed at the root and "bubbled down" to its correct position.
* `insert` inserts an element into the heap and maintains the heap property.
* `extractMax` removes and returns the maximum element from the heap while maintaining the heap property.
* `isEmpty` and `size` are utility functions to check if the heap is empty and to get its size, respectively.

This code implements a max heap. If you want to implement a min heap, you just need to adjust the comparison operators in `heapifyUp` and `heapifyDown`.

### 1. Algorithms & Data Structures (C++): Heap: Helper Methods

In C++, heaps are often implemented as binary trees where each node satisfies the heap property (for max heaps, each node is greater than or equal to its children; for min heaps, each node is less than or equal to its children). Here are some helper methods commonly used when working with heaps:

1. **getParentIndex(index)**: This function returns the index of the parent node given the index of a child node.

```cpp
int getParentIndex(int index) {
    return (index - 1) / 2;
}
```

1. **getLeftChildIndex(index)**: This function returns the index of the left child node given the index of a parent node.

```cpp
int getLeftChildIndex(int index) {
    return (2 * index) + 1;
}
```

1. **getRightChildIndex(index)**: This function returns the index of the right child node given the index of a parent node.

```cpp
int getRightChildIndex(int index) {
    return (2 * index) + 2;
}
```

1. **heapifyUp(arr, index)**: This function is used to maintain the heap property by moving a node up the heap if necessary. It's typically used after inserting a new element into the heap.

```cpp
void heapifyUp(vector<int>& arr, int index) {
    while (index > 0 && arr[getParentIndex(index)] < arr[index]) {
        swap(arr[getParentIndex(index)], arr[index]);
        index = getParentIndex(index);
    }
}
```

1. **heapifyDown(arr, index, size)**: This function is used to maintain the heap property by moving a node down the heap if necessary. It's typically used after removing the root element from the heap.

```cpp
void heapifyDown(vector<int>& arr, int index, int size) {
    int leftChildIndex = getLeftChildIndex(index);
    int rightChildIndex = getRightChildIndex(index);
    int largest = index;

    if (leftChildIndex < size && arr[leftChildIndex] > arr[index]) {
        largest = leftChildIndex;
    }

    if (rightChildIndex < size && arr[rightChildIndex] > arr[largest]) {
        largest = rightChildIndex;
    }

    if (largest != index) {
        swap(arr[index], arr[largest]);
        heapifyDown(arr, largest, size);
    }
}
```

These helper methods are essential for implementing and maintaining the heap data structure efficiently.

### 1. Algorithms & Data Structures (C++): Heap: Insert

Inserting an element into a heap involves two key steps:

1. **Appending**: Add the new element to the end of the array representing the heap.
2. **Heapify Up**: Restore the heap property by moving the newly inserted element up the tree until it satisfies the heap property (usually that the parent node is greater than or equal to its children, for a max-heap).

Here's a simple implementation of heap insertion in C++:

```cpp
#include <iostream>
#include <vector>

class MaxHeap {
private:
    std::vector<int> heap;

    // Helper function to swap two elements in the heap
    void swap(int& a, int& b) {
        int temp = a;
        a = b;
        b = temp;
    }

    // Helper function to move a newly inserted element up the heap
    void heapifyUp(int index) {
        int parent = (index - 1) / 2;
        // Continue moving up as long as the current element is greater than its parent
        while (index > 0 && heap[index] > heap[parent]) {
            swap(heap[index], heap[parent]);
            index = parent;
            parent = (index - 1) / 2;
        }
    }

public:
    // Insert a new element into the heap
    void insert(int key) {
        heap.push_back(key); // Append the new element to the end
        heapifyUp(heap.size() - 1); // Restore heap property
    }

    // Function to print the heap
    void printHeap() {
        for (int i = 0; i < heap.size(); ++i)
            std::cout << heap[i] << " ";
        std::cout << std::endl;
    }
};

int main() {
    MaxHeap heap;
    heap.insert(10);
    heap.insert(20);
    heap.insert(15);
    heap.insert(30);
    heap.insert(40);
    heap.insert(5);

    std::cout << "Heap after insertion: ";
    heap.printHeap();

    return 0;
}
```

In this code:

* `insert()` inserts the new element into the heap.
* `heapifyUp()` restores the heap property by moving the newly inserted element up the heap until it satisfies the heap property.
* `printHeap()` simply prints out the elements of the heap for visualization.

This implementation assumes a max-heap (where the parent is greater than or equal to its children). If you want to create a min-heap (where the parent is less than or equal to its children), you just need to reverse the comparison in the `heapifyUp()` function.

### 1. Algorithms & Data Structures (C++): Heap: Maximum Element in a Stream

To find the maximum element in a stream of numbers using a heap in C++, you can use the `priority_queue` container from the Standard Template Library (STL). Here's how you can implement it:

```cpp
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

int main() {
    // Define a priority queue to store elements in descending order
    priority_queue<int> maxHeap;

    // Stream of numbers
    vector<int> stream = {4, 8, 2, 5, 9, 1, 6};

    // Process the stream
    for (int i = 0; i < stream.size(); ++i) {
        // Insert current element into the max heap
        maxHeap.push(stream[i]);

        // Get the maximum element in the stream
        cout << "Maximum element in the stream after " << i + 1 << " elements: " << maxHeap.top() << endl;
    }

    return 0;
}
```

In this code:

* We use `priority_queue<int> maxHeap;` to create a max heap. By default, `priority_queue` orders elements in descending order, so it will give us the maximum element at the top.
* We iterate through the stream of numbers and insert each element into the max heap using `maxHeap.push(stream[i]);`.
* After inserting each element, we print the maximum element in the stream using `maxHeap.top()`.

This code will output the maximum element in the stream after each element is inserted. You can modify it according to your requirements or integrate it into a larger program as needed.

### 1. Algorithms & Data Structures (C++): Heap: MinHeap Insert

Sure, I can guide you through implementing the insertion operation for a MinHeap in C++. First, let's briefly discuss what a MinHeap is.

A MinHeap is a complete binary tree where each node has a value less than or equal to the values of its children. The root node contains the minimum value in the heap.

To insert a new element into a MinHeap, we typically add it at the bottom-most, right-most position to maintain the complete binary tree property. Then, we compare the new element with its parent node and swap them if the parent's value is greater, ensuring the MinHeap property is maintained.

Here's a basic implementation of the MinHeap and its insertion operation in C++:

```cpp
#include <vector>
#include <iostream>

using namespace std;

class MinHeap {
private:
    vector<int> heap;

    // Helper function to swap two elements in the heap
    void swap(int& a, int& b) {
        int temp = a;
        a = b;
        b = temp;
    }

    // Helper function to maintain the MinHeap property after insertion
    void heapifyUp(int index) {
        int parentIndex = (index - 1) / 2;
        while (index > 0 && heap[index] < heap[parentIndex]) {
            swap(heap[index], heap[parentIndex]);
            index = parentIndex;
            parentIndex = (index - 1) / 2;
        }
    }

public:
    // Constructor
    MinHeap() {}

    // Function to insert a new element into the heap
    void insert(int value) {
        heap.push_back(value);
        heapifyUp(heap.size() - 1);
    }

    // Function to print the heap
    void printHeap() {
        for (int i = 0; i < heap.size(); ++i) {
            cout << heap[i] << " ";
        }
        cout << endl;
    }
};

int main() {
    MinHeap minHeap;
    minHeap.insert(5);
    minHeap.insert(3);
    minHeap.insert(8);
    minHeap.insert(2);
    minHeap.insert(6);

    cout << "MinHeap after insertions: ";
    minHeap.printHeap();

    return 0;
}
```

In this implementation:

* The `insert()` function inserts a new element at the end of the heap and then calls `heapifyUp()` to maintain the MinHeap property.
* The `heapifyUp()` function compares the newly inserted element with its parent and swaps them if necessary until the MinHeap property is satisfied.

You can run this code to see how the MinHeap is constructed and maintained after insertions.

### 1. Algorithms & Data Structures (C++): Heap: MinHeap Remove

To remove an element from a MinHeap in C++, you typically follow these steps:

1. Identify the index of the element you want to remove.
2. Swap the element with the last element in the heap.
3. Remove the last element (which is now the one you want to remove).
4. Perform heapify-down operation to maintain the heap property.

Here's a sample implementation:

```cpp
#include <iostream>
#include <vector>

class MinHeap {
private:
    std::vector<int> heap;

    void heapifyDown(int index) {
        int left = 2 * index + 1;
        int right = 2 * index + 2;
        int smallest = index;

        if (left < heap.size() && heap[left] < heap[index])
            smallest = left;
        if (right < heap.size() && heap[right] < heap[smallest])
            smallest = right;

        if (smallest != index) {
            std::swap(heap[index], heap[smallest]);
            heapifyDown(smallest);
        }
    }

public:
    void remove(int value) {
        for (int i = 0; i < heap.size(); ++i) {
            if (heap[i] == value) {
                heap[i] = heap.back();
                heap.pop_back();
                heapifyDown(i);
                break;
            }
        }
    }

    void print() {
        for (int i = 0; i < heap.size(); ++i)
            std::cout << heap[i] << " ";
        std::cout << std::endl;
    }
};

int main() {
    MinHeap minHeap;
    minHeap.insert(3);
    minHeap.insert(2);
    minHeap.insert(1);
    minHeap.insert(5);
    minHeap.insert(4);

    std::cout << "MinHeap before removal: ";
    minHeap.print();

    minHeap.remove(2); // Remove value 2

    std::cout << "MinHeap after removal: ";
    minHeap.print();

    return 0;
}
```

In this implementation, the `remove` function takes the value you want to remove as an argument and searches for it in the heap. Once found, it replaces that element with the last element in the heap and then removes the last element. Finally, it calls `heapifyDown` to maintain the heap property.

### 1. Algorithms & Data Structures (C++): Heap: MinHeap Sink Down

In C++, implementing a MinHeap and its "sink down" operation is a fundamental concept in data structures. The "sink down" operation, also known as "heapify down" or "percolate down," is crucial for maintaining the heap property after a removal operation or when initializing a heap from an unsorted array.

Here's an example implementation of a MinHeap and its sink down operation:

```cpp
#include <iostream>
#include <vector>

class MinHeap {
private:
    std::vector<int> heap;

    // Helper function to swap two elements in the heap
    void swap(int& a, int& b) {
        int temp = a;
        a = b;
        b = temp;
    }

    // Helper function to get the index of the left child
    int leftChild(int parentIndex) {
        return 2 * parentIndex + 1;
    }

    // Helper function to get the index of the right child
    int rightChild(int parentIndex) {
        return 2 * parentIndex + 2;
    }

    // Helper function to get the index of the parent
    int parent(int childIndex) {
        return (childIndex - 1) / 2;
    }

    // Helper function to perform the sink down operation
    void sinkDown(int index) {
        int smallest = index;
        int left = leftChild(index);
        int right = rightChild(index);
        
        // Check if left child is smaller than current node
        if (left < heap.size() && heap[left] < heap[smallest]) {
            smallest = left;
        }

        // Check if right child is smaller than current node and left child
        if (right < heap.size() && heap[right] < heap[smallest]) {
            smallest = right;
        }

        // If smallest is not the current index, swap and recursively call sinkDown
        if (smallest != index) {
            swap(heap[index], heap[smallest]);
            sinkDown(smallest);
        }
    }

public:
    // Constructor to initialize an empty heap
    MinHeap() {}

    // Function to insert a new element into the heap
    void insert(int value) {
        heap.push_back(value);
        int index = heap.size() - 1;
        int parentIndex = parent(index);
        while (index > 0 && heap[parentIndex] > heap[index]) {
            swap(heap[index], heap[parentIndex]);
            index = parentIndex;
            parentIndex = parent(index);
        }
    }

    // Function to remove the minimum element from the heap
    int removeMin() {
        if (heap.empty()) {
            throw std::out_of_range("Heap is empty");
        }
        int minValue = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        sinkDown(0);
        return minValue;
    }

    // Function to check if the heap is empty
    bool isEmpty() {
        return heap.empty();
    }
};

int main() {
    MinHeap minHeap;
    minHeap.insert(5);
    minHeap.insert(3);
    minHeap.insert(8);
    minHeap.insert(1);
    minHeap.insert(6);

    while (!minHeap.isEmpty()) {
        std::cout << minHeap.removeMin() << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this implementation, the `sinkDown` function is called after removing the minimum element from the heap to restore the heap property. This function compares the element at the current index with its children and swaps it with the smallest child if necessary, recursively calling itself until the heap property is satisfied.

You can test this implementation with sample inputs to ensure its correctness and efficiency.

### 1. Algorithms & Data Structures (C++): Heap: Priority Queues & Big O

In C++, a heap is often implemented as a binary heap, which is a complete binary tree where each node's value is greater than or equal to (or less than or equal to, depending on whether it's a max heap or min heap) the values of its children. Priority queues are often implemented using heaps, where the highest (or lowest) priority element can be efficiently accessed.

Here's an overview of priority queues and their big O complexities:

1. **Insertion (enqueue)**:
   * To insert an element into a priority queue implemented with a heap, you typically add the element at the bottom level of the heap (the last position) and then perform a "heapify up" operation to maintain the heap property.
   * Time complexity: O(log n) where n is the number of elements in the priority queue. This is because the height of the heap is logarithmic with respect to the number of elements.

2. **Deletion (dequeue)**:
   * Removing the element with the highest (or lowest) priority from the priority queue. For heaps, this typically means removing the root element, replacing it with the last element, and then performing a "heapify down" operation to maintain the heap property.
   * Time complexity: O(log n) for the same reason as insertion.

3. **Peek**:
   * To access the element with the highest (or lowest) priority without removing it from the priority queue.
   * Time complexity: O(1). This is because the highest (or lowest) priority element is always at the root of the heap.

4. **Heapify**:
   * This operation is used to convert an array into a heap.
   * Time complexity: O(n). This is a linear time operation. Although it may seem contradictory to the O(log n) complexity of insertion and deletion, heapifying doesn't involve as many comparisons as insertion and deletion operations.

5. **Overall**:
   * Overall, the time complexity of most operations on a priority queue implemented with a heap is O(log n), where n is the number of elements in the priority queue.
   * However, building a priority queue from an array (heapify) takes O(n) time.
   * Priority queues are efficient for operations requiring accessing the highest (or lowest) priority element, such as task scheduling, event-driven simulation, and graph algorithms like Dijkstra's algorithm and Prim's algorithm.

In C++, you can use the `priority_queue` container in the `<queue>` header to implement a priority queue using heaps.

### 1. Algorithms & Data Structures (C++): Heap: Remove

In C++, removing an element from a heap typically involves two steps:

1. First, you need to find the element you want to remove. Since heaps are commonly implemented using arrays, you'll usually find the element in constant time, as it's typically the root of the heap.

2. After removing the element, you need to restore the heap property by adjusting the heap structure, usually by performing a "heapify" operation.

Here's a basic example of how you might implement the removal of an element from a heap in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to heapify a subtree rooted with node i which is an index in arr[]. 
// n is the size of the heap. 
void heapify(vector<int>& arr, int n, int i) {
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

// Function to delete an element from heap
void deleteNode(vector<int>& arr, int& n, int key) {
    // Find the position of the element to be deleted
    int i;
    for (i = 0; i < n; ++i) {
        if (arr[i] == key)
            break;
    }

    // If key is not found
    if (i == n) {
        cout << "Element not found in the heap" << endl;
        return;
    }

    // Move the last element to the position of the element to be deleted
    arr[i] = arr[n - 1];
    n--;

    // Heapify the array from root to downward
    for (int j = (n - 1) / 2; j >= 0; --j)
        heapify(arr, n, j);
}

// Function to print the heap
void printHeap(vector<int>& arr, int n) {
    cout << "Heap: ";
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";
    cout << endl;
}

int main() {
    vector<int> heap = {10, 20, 15, 40, 50, 100, 25, 45};
    int n = heap.size();

    cout << "Original ";
    printHeap(heap, n);

    // Remove an element (e.g., 40) from the heap
    int key = 40;
    deleteNode(heap, n, key);

    cout << "After deletion of " << key << " ";
    printHeap(heap, n);

    return 0;
}
```

This code demonstrates how to remove an element from a max heap implemented as a vector. After removal, it ensures that the heap property is maintained by performing heapify operations.

### 1. Algorithms & Data Structures (C++): Heap: Sink Down

In the context of heaps, "sink down" usually refers to the operation of restoring the heap property after removing the root element (typically the maximum in a max-heap or the minimum in a min-heap). The idea is to move the element at the top (root) of the heap down to its correct position to maintain the heap property.

Here's a basic implementation of sinking down in a max-heap:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void sinkDown(vector<int>& heap, int index) {
    int size = heap.size();
    int parent = index;

    while (true) {
        int leftChild = 2 * parent + 1;
        int rightChild = 2 * parent + 2;
        int largest = parent;

        // Compare with left child
        if (leftChild < size && heap[leftChild] > heap[largest])
            largest = leftChild;

        // Compare with right child
        if (rightChild < size && heap[rightChild] > heap[largest])
            largest = rightChild;

        // If parent is already larger than its children, stop
        if (largest == parent)
            break;

        // Swap parent with the largest child
        swap(heap[parent], heap[largest]);

        // Update parent index for next iteration
        parent = largest;
    }
}

int main() {
    vector<int> heap = {9, 8, 7, 6, 5, 4, 3, 2, 1};
    sinkDown(heap, 0);

    // Print the heap after sinking down
    for (int num : heap)
        cout << num << " ";
    cout << endl;

    return 0;
}
```

In this implementation:

* `sinkDown` takes the heap vector and the index of the element that needs to be sunk down.
* It continuously compares the element at the given index with its children and swaps it with the larger child if necessary, ensuring that the largest element "sinks down" to its correct position.
* The loop terminates when the element reaches its correct position or when it becomes a leaf node (has no children larger than itself).

This process maintains the heap property, which is crucial for efficient operations on heaps like insertion and deletion.

### 1. Algorithms & Data Structures (C++): Heapify

Heapify is a fundamental operation in heap data structures, which are commonly used to implement priority queues. The process of heapifying an array converts it into a heap, ensuring that the heap property is satisfied.

In a max heap, for any node \( i \), the value of the node is greater than or equal to the values of its children. In a min heap, the value of the node is less than or equal to the values of its children.

Heapify can be performed in two ways:

1. **Bottom-up (Iterative) Approach**: Starting from the last non-leaf node and moving up to the root, each node is heapified by comparing it with its children and swapping if necessary to maintain the heap property.

2. **Top-down (Recursive) Approach**: Starting from the root node, heapify recursively ensures that each subtree rooted at the node satisfies the heap property.

Here's an example of heapify implemented in C++ for a max heap:

```cpp
#include <iostream>
#include <vector>
using namespace std;

// Heapify a subtree rooted with node i which is an index in vector arr[]
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

// Build heap (rearrange vector)
void buildHeap(vector<int>& arr) {
    int n = arr.size();

    // Index of the last non-leaf node
    int startIdx = (n / 2) - 1;

    // Perform reverse level order traversal
    // from last non-leaf node and heapify each node
    for (int i = startIdx; i >= 0; i--) {
        heapify(arr, n, i);
    }
}

// Function to print an array
void printArray(const vector<int>& arr) {
    for (int i : arr) {
        cout << i << " ";
    }
    cout << endl;
}

int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    int n = arr.size();

    cout << "Original array: ";
    printArray(arr);

    buildHeap(arr);

    cout << "Heapified array: ";
    printArray(arr);

    return 0;
}
```

In this example, `heapify` function is used to heapify a subtree rooted at index `i` in the vector `arr`, and `buildHeap` function is used to build a heap from an array by heapifying each subtree in bottom-up manner.

### 1. Algorithms & Data Structures (C++): Heapify - Faster Method for creating Heap

Heapify is a fundamental operation in heap data structures, particularly in the context of binary heaps. It's used to maintain the heap property after inserting an element or deleting the root element from the heap. The heap property ensures that for a max heap, the parent node is always greater than or equal to its child nodes, and for a min heap, the parent node is always less than or equal to its child nodes.

The usual method to heapify involves starting from the last non-leaf node and moving upwards, repeatedly comparing the node with its children and swapping if necessary until the heap property is satisfied. This method typically has a time complexity of O(n), where n is the number of elements in the heap.

However, there's a faster method for heapifying an array called Floyd's heap construction algorithm, also known as "bottom-up heap construction." This method has a time complexity of O(n), making it more efficient than the traditional approach.

Here's a high-level overview of Floyd's heap construction algorithm:

1. Start from the last non-leaf node in the array (i.e., the parent of the last element).
2. Move upwards towards the root of the heap.
3. For each node, compare it with its children and swap it with the larger (in the case of a max heap) or smaller (in the case of a min heap) child if necessary.
4. Continue this process until the entire array satisfies the heap property.

Here's a sample implementation of heapify using Floyd's algorithm in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to heapify a subtree rooted at index i
// This function assumes that the subtrees are already heapified
// Note: This function is called heapifyDown in the context of heap sort
void heapify(vector<int>& arr, int n, int i) {
    int largest = i;  // Initialize largest as root
    int left = 2 * i + 1;  // left child
    int right = 2 * i + 2;  // right child

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

// Function to build a heap
void buildHeap(vector<int>& arr) {
    int n = arr.size();

    // Index of the last non-leaf node
    int startIdx = (n / 2) - 1;

    // Perform reverse level order traversal
    // from the last non-leaf node and heapify each node
    for (int i = startIdx; i >= 0; i--) {
        heapify(arr, n, i);
    }
}

int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    int n = arr.size();

    cout << "Original array is \n";
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";
    cout << endl;

    buildHeap(arr);

    cout << "Heapified array is \n";
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";
    cout << endl;

    return 0;
}
```

This implementation uses the `heapify` function to maintain the heap property while traversing from the bottom up. The `buildHeap` function initializes the heap using Floyd's algorithm, and then we print the heapified array.

### 1. Algorithms & Data Structures (C++): Heapify function

Heapify is a fundamental operation used in heap data structures, like binary heaps, to maintain the heap property. The heap property can be defined differently for min-heaps and max-heaps. In a min-heap, for any given node \( i \), the value of \( \text{parent}(i) \) is less than or equal to the value of \( i \), and similarly for a max-heap, the parent's value is greater than or equal to the value of \( i \). Heapify ensures that if there is any violation of the heap property at a particular node, it is fixed by properly arranging the elements.

Here's a simple implementation of heapify for a max-heap in C++:

```cpp
#include <iostream>
#include <vector>
using namespace std;

// Function to heapify a subtree rooted at index i
// n is the size of heap
void maxHeapify(vector<int>& arr, int n, int i) {
    int largest = i;    // Initialize largest as root
    int left = 2 * i + 1;  // left = 2*i + 1
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
        maxHeapify(arr, n, largest);
    }
}

// Utility function to print array
void printArray(vector<int>& arr, int n) {
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";
    cout << "\n";
}

int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    int n = arr.size();

    cout << "Original array: \n";
    printArray(arr, n);

    // Build max heap
    for (int i = n / 2 - 1; i >= 0; --i)
        maxHeapify(arr, n, i);

    cout << "Max heap: \n";
    printArray(arr, n);

    return 0;
}
```

In this implementation:

* `maxHeapify` is the main function that ensures the max-heap property.
* `left` and `right` represent the indices of the left and right child nodes of a given node, respectively.
* If either of the child nodes is greater than the current node, `largest` is updated to the index of the larger child.
* If the largest is not the current node, a swap is performed, and the function is recursively called on the affected sub-tree.
* `printArray` is a utility function to print the elements of an array.
* In the `main` function, an array is heapified to form a max-heap.

### 1. Algorithms & Data Structures (C++): Heapify operation: Constructing heap from an arbitrary one dimensional array

Heapify is a fundamental operation in heap data structures. It's commonly used to build a heap from an arbitrary array. A heap is a specialized tree-based data structure in which the parent node is either greater than or equal to its children (max heap), or less than or equal to its children (min heap).

In the context of constructing a heap from an array, heapify is typically used in a bottom-up manner. Here's how you can implement heapify in C++:

```cpp
#include <iostream>
#include <vector>
using namespace std;

void maxHeapify(vector<int>& arr, int n, int i) {
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
        maxHeapify(arr, n, largest);
    }
}

void buildMaxHeap(vector<int>& arr) {
    int n = arr.size();

    // Index of last non-leaf node
    int startIdx = (n / 2) - 1;

    // Perform reverse level order traversal from last non-leaf node and heapify each node
    for (int i = startIdx; i >= 0; i--) {
        maxHeapify(arr, n, i);
    }
}

int main() {
    vector<int> arr = {12, 11, 13, 5, 6, 7};
    int n = arr.size();

    cout << "Original array: ";
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";
    cout << endl;

    buildMaxHeap(arr);

    cout << "Max Heap: ";
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";
    cout << endl;

    return 0;
}
```

In this code:

* `maxHeapify` function ensures that the subtree rooted at index `i` follows the max heap property.
* `buildMaxHeap` function constructs a max heap from the given array by starting from the last non-leaf node and calling `maxHeapify` for each node.
* In the `main` function, you can see an example of how to use these functions to build a max heap from an arbitrary array.

This implementation assumes a max heap. For a min heap, you would modify the comparisons accordingly.

### 1. Algorithms & Data Structures (C++): Heapify process

Heapify is a crucial operation in the realm of algorithms and data structures, particularly for implementing heap data structures like binary heaps. It's primarily used to maintain the heap property, which is essential for efficient heap operations such as insertions, deletions, and heap sort.

In the context of binary heaps, heapify refers to the process of ensuring that a given binary tree satisfies the heap property. Specifically, for a max-heap, the heap property states that for any node \(i\), the value of \(i\) must be greater than or equal to the values of its children. For a min-heap, it's the opposite: the value of \(i\) must be less than or equal to the values of its children.

There are two types of heapify operations:

1. **Bottom-up (also known as "heapify up" or "sift-up"):** This is typically used during insertion. It starts from the newly inserted node and moves upwards, swapping the node with its parent if necessary to maintain the heap property.

2. **Top-down (also known as "heapify down" or "sift-down"):** This is commonly used during deletion (particularly when removing the root). It starts from the root and moves downwards, swapping the root with one of its children if necessary to maintain the heap property.

Here's an example of how heapify down (for a max-heap) would work in C++:

```cpp
void heapifyDown(vector<int>& heap, int index, int heapSize) {
    int largest = index;
    int leftChild = 2 * index + 1;
    int rightChild = 2 * index + 2;

    // Check if left child exists and is greater than the current node
    if (leftChild < heapSize && heap[leftChild] > heap[largest])
        largest = leftChild;

    // Check if right child exists and is greater than the current node and left child
    if (rightChild < heapSize && heap[rightChild] > heap[largest])
        largest = rightChild;

    // If the largest element is not the current node, swap it with the largest child
    if (largest != index) {
        swap(heap[index], heap[largest]);
        // Recursively heapify the affected subtree
        heapifyDown(heap, largest, heapSize);
    }
}

// Example usage:
// Assuming 'heap' is a vector representing a max-heap and 'heapSize' is the size of the heap
// Perform heapify down starting from index 0
heapifyDown(heap, 0, heapSize);
```

In this example, `heapifyDown` function takes the heap vector, the index of the node to heapify, and the size of the heap. It then compares the node with its children, finds the largest among them, and swaps if necessary. Finally, it recursively calls itself on the affected subtree until the heap property is satisfied.

### 1. Algorithms & Data Structures (C++): Heaps

Heaps are fundamental data structures in computer science, extensively used for implementing priority queues and in various sorting algorithms like heap sort. They're essentially binary trees that satisfy the heap property.

In C++, heaps are typically implemented using arrays because of their efficient use of memory. There are two main types of heaps:

1. **Max Heap**: In a max heap, the value of each node is greater than or equal to the values of its children. Thus, the largest element is always at the root.

2. **Min Heap**: In a min heap, the value of each node is less than or equal to the values of its children. Thus, the smallest element is always at the root.

Here's a basic overview of how heaps work in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm> // For make_heap, push_heap, pop_heap

using namespace std;

int main() {
    // Creating a max heap
    vector<int> maxHeap = {10, 20, 15, 40, 50, 100, 25};

    // Convert the vector into a max heap
    make_heap(maxHeap.begin(), maxHeap.end());

    // Print the elements of the max heap
    cout << "Max Heap elements: ";
    for (int i : maxHeap)
        cout << i << " ";
    cout << endl;

    // Inserting a new element into the max heap
    maxHeap.push_back(35);
    push_heap(maxHeap.begin(), maxHeap.end()); // Re-establish the heap property

    // Print the elements of the max heap after insertion
    cout << "Max Heap elements after insertion: ";
    for (int i : maxHeap)
        cout << i << " ";
    cout << endl;

    // Removing the largest element from the max heap
    pop_heap(maxHeap.begin(), maxHeap.end()); // Move the largest element to the end
    maxHeap.pop_back(); // Remove the largest element

    // Print the elements of the max heap after removal
    cout << "Max Heap elements after removal: ";
    for (int i : maxHeap)
        cout << i << " ";
    cout << endl;

    return 0;
}
```

This code demonstrates the basic operations on a max heap using the `<algorithm>` library functions `make_heap`, `push_heap`, and `pop_heap`.

Understanding heap operations is crucial because they are often used as underlying data structures for more complex algorithms, like Dijkstra's algorithm for shortest paths and Huffman coding for data compression.

### 1. Algorithms & Data Structures (C++): Heaps - Delete Function

In C++, deleting an element from a heap typically involves two steps: first, finding the element to be deleted, and second, restoring the heap property after deletion. Here's a basic outline of how you can implement the delete operation for a max heap:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to heapify a subtree rooted with node i which is an index in heap[]
void heapify(vector<int>& heap, int n, int i) {
    int largest = i;  // Initialize largest as root
    int left = 2 * i + 1;  // left = 2*i + 1
    int right = 2 * i + 2;  // right = 2*i + 2

    // If left child is larger than root
    if (left < n && heap[left] > heap[largest])
        largest = left;

    // If right child is larger than largest so far
    if (right < n && heap[right] > heap[largest])
        largest = right;

    // If largest is not root
    if (largest != i) {
        swap(heap[i], heap[largest]);

        // Recursively heapify the affected sub-tree
        heapify(heap, n, largest);
    }
}

// Function to delete an element from heap
void deleteNode(vector<int>& heap, int& n, int key) {
    // Find the index of key in heap
    int i;
    for (i = 0; i < n; i++) {
        if (heap[i] == key)
            break;
    }

    // If key was not found
    if (i == n) {
        cout << "Key not found in heap" << endl;
        return;
    }

    // Swap the found element with the last element
    heap[i] = heap[n - 1];
    n--;

    // Heapify the root
    heapify(heap, n, i);
}

// Function to print the heap
void printHeap(const vector<int>& heap) {
    for (int i = 0; i < heap.size(); i++)
        cout << heap[i] << " ";
    cout << endl;
}

int main() {
    vector<int> heap = {10, 20, 15, 40, 50, 100, 25, 45};
    int n = heap.size();

    cout << "Heap before deletion: ";
    printHeap(heap);

    int key = 50;
    deleteNode(heap, n, key);

    cout << "Heap after deletion of " << key << ": ";
    printHeap(heap);

    return 0;
}
```

In this code:

* `heapify()` is a recursive function to heapify a subtree with root at the given index `i`.
* `deleteNode()` takes the heap, its size `n`, and the key to be deleted as arguments. It finds the index of the key in the heap, swaps it with the last element, reduces the heap size by 1, and then heapifies the root.

This code assumes a max heap. If you're working with a min heap, you'll need to adjust the comparisons accordingly.

### 1. Algorithms & Data Structures (C++): Heaps - Deletion

In C++, deletion in heaps typically involves removing the root element and then maintaining the heap property by adjusting the heap accordingly. There are two main types of heaps: max heaps and min heaps.

### Max Heap Deletion

1. **Remove Root:** In a max heap, the root contains the maximum value. To delete it, you replace the root with the last element in the heap.

    ```cpp
    void deleteMax(int heap[], int& n) {
        if (n == 0) {
            cout << "Heap is empty";
            return;
        }
        int maxValue = heap[0];
        heap[0] = heap[n - 1];
        n--;
        maxHeapify(heap, 0, n);
        cout << "Deleted element: " << maxValue << endl;
    }
    ```

2. **Max Heapify:** After replacing the root, you need to maintain the max heap property. This is done by performing a max heapify operation starting from the root.

    ```cpp
    void maxHeapify(int heap[], int i, int n) {
        int largest = i;
        int left = 2 * i + 1;
        int right = 2 * i + 2;
        
        if (left < n && heap[left] > heap[largest])
            largest = left;
        
        if (right < n && heap[right] > heap[largest])
            largest = right;
        
        if (largest != i) {
            swap(heap[i], heap[largest]);
            maxHeapify(heap, largest, n);
        }
    }
    ```

### Min Heap Deletion

1. **Remove Root:** In a min heap, the root contains the minimum value. To delete it, you replace the root with the last element in the heap.

    ```cpp
    void deleteMin(int heap[], int& n) {
        if (n == 0) {
            cout << "Heap is empty";
            return;
        }
        int minValue = heap[0];
        heap[0] = heap[n - 1];
        n--;
        minHeapify(heap, 0, n);
        cout << "Deleted element: " << minValue << endl;
    }
    ```

2. **Min Heapify:** After replacing the root, you need to maintain the min heap property. This is done by performing a min heapify operation starting from the root.

    ```cpp
    void minHeapify(int heap[], int i, int n) {
        int smallest = i;
        int left = 2 * i + 1;
        int right = 2 * i + 2;
        
        if (left < n && heap[left] < heap[smallest])
            smallest = left;
        
        if (right < n && heap[right] < heap[smallest])
            smallest = right;
        
        if (smallest != i) {
            swap(heap[i], heap[smallest]);
            minHeapify(heap, smallest, n);
        }
    }
    ```

Remember to adjust the heap size `n` accordingly after deletion. These functions assume that the heap is stored in an array representation.

### 1. Algorithms & Data Structures (C++): Heaps - Insert Function

Sure, I can provide you with a C++ implementation of the insert function for a binary min-heap. Here's how you can implement it:

```cpp
#include <vector>

class MinHeap {
private:
    std::vector<int> heap;

    // Helper function to swap two elements in the heap
    void swap(int& a, int& b) {
        int temp = a;
        a = b;
        b = temp;
    }

    // Helper function to maintain the heap property after insertion
    void heapifyUp(int index) {
        while (index > 0 && heap[parent(index)] > heap[index]) {
            swap(heap[parent(index)], heap[index]);
            index = parent(index);
        }
    }

    // Helper function to get the index of the parent of a node
    int parent(int index) {
        return (index - 1) / 2;
    }

public:
    // Constructor to create an empty heap
    MinHeap() {}

    // Function to insert a new element into the heap
    void insert(int value) {
        heap.push_back(value);
        int lastIndex = heap.size() - 1;
        heapifyUp(lastIndex);
    }
};
```

In this implementation:

* We maintain the heap property by using the `heapifyUp` function after inserting an element. This function compares the newly inserted element with its parent and swaps them if necessary to maintain the min-heap property.
* The `insert` function inserts a new element into the heap and then calls `heapifyUp` to ensure that the heap property is preserved.
* The `parent` function calculates the index of the parent node of a given index in the heap.

You can use this `MinHeap` class to create a binary min-heap and insert elements into it. For example:

```cpp
int main() {
    MinHeap minHeap;
    minHeap.insert(3);
    minHeap.insert(2);
    minHeap.insert(1);
    minHeap.insert(5);
    minHeap.insert(4);

    // Now the min heap contains: 1, 2, 3, 5, 4
    return 0;
}
```

This is a basic implementation of the insert function for a binary min-heap in C++. You can further extend it to include other operations like extracting the minimum element or deleting elements.

### 1. Algorithms & Data Structures (C++): Heaps - Insertion

Sure, let's dive into the basics of inserting elements into a heap data structure in C++.

A heap is a specialized tree-based data structure that satisfies the heap property. In a max heap, for any given node \( i \), the value of the node is greater than or equal to the values of its children. In a min heap, for any given node \( i \), the value of the node is less than or equal to the values of its children.

Here's a basic implementation of inserting elements into a max heap in C++:

```cpp
#include <iostream>
#include <vector>

class MaxHeap {
private:
    std::vector<int> heap;

    // Helper function to maintain the max heap property
    void heapifyUp(int index) {
        int parentIndex = (index - 1) / 2;
        while (index > 0 && heap[index] > heap[parentIndex]) {
            std::swap(heap[index], heap[parentIndex]);
            index = parentIndex;
            parentIndex = (index - 1) / 2;
        }
    }

public:
    // Function to insert an element into the max heap
    void insert(int value) {
        heap.push_back(value); // Add the element to the end of the heap
        heapifyUp(heap.size() - 1); // Restore heap property
    }

    // Function to print the elements of the heap
    void printHeap() {
        for (int i = 0; i < heap.size(); ++i) {
            std::cout << heap[i] << " ";
        }
        std::cout << std::endl;
    }
};

int main() {
    MaxHeap maxHeap;

    // Insert elements into the max heap
    maxHeap.insert(10);
    maxHeap.insert(5);
    maxHeap.insert(20);
    maxHeap.insert(8);
    maxHeap.insert(15);

    // Print the max heap
    std::cout << "Max Heap: ";
    maxHeap.printHeap();

    return 0;
}
```

In this implementation:

* We use a `std::vector<int>` to store the elements of the heap.
* The `insert` function adds a new element to the end of the vector and then calls `heapifyUp` to restore the heap property by comparing the element with its parent and swapping if necessary.
* The `heapifyUp` function moves the newly inserted element up the tree until the heap property is satisfied.
* Finally, in the `main` function, we create a `MaxHeap` object, insert some elements into it, and then print the heap.

You can modify this implementation for a min heap by changing the comparison operator in the `heapifyUp` function.

### 1. Algorithms & Data Structures (C++): Heaps and Arrays

Heaps and arrays are fundamental in computer science and play vital roles in implementing various algorithms and data structures efficiently. Let's delve into each of them:

### Arrays

Arrays are a contiguous collection of elements stored in memory, each accessible by an index. In C++, arrays have a fixed size that's determined at compile time. Here are some key points:

1. **Random Access:** Elements in an array can be accessed randomly by their index in constant time.
  
2. **Memory Efficiency:** Arrays have excellent memory locality, making them efficient in terms of memory access.

3. **Static Size:** The size of an array is fixed at compile time and cannot be changed during runtime.

4. **Declaration:** Arrays in C++ can be declared using square brackets, like `int myArray[5];`, where `5` represents the size of the array.

5. **Initialization:** Arrays can be initialized during declaration, like `int myArray[5] = {1, 2, 3, 4, 5};`.

6. **Access:** Elements of an array are accessed using indices, starting from 0. For example, `myArray[0]` refers to the first element, `myArray[1]` to the second, and so on.

### Heaps

Heaps are specialized binary trees that satisfy the heap property. In a max heap, for any node `i`, the value of the node is greater than or equal to the values of its children. In a min heap, the value of the node is less than or equal to the values of its children. Here are some key points:

1. **Complete Binary Tree:** Heaps are typically implemented as complete binary trees, where all levels are filled except possibly the last level, which is filled from left to right.

2. **Efficient Priority Queue:** Heaps are commonly used to implement priority queues, where elements with higher priorities are served before elements with lower priorities.

3. **Operations:** Heaps usually support operations like insertion, deletion, and retrieval of the maximum or minimum element, all in logarithmic time complexity.

4. **Heapify:** This operation involves creating a heap from a given array of elements. It can be done in linear time complexity.

5. **Implementation:** Heaps can be implemented using arrays. The children of the node at index `i` are at indices `2*i + 1` and `2*i + 2`.

6. **Heap Sort:** Heapsort is a comparison-based sorting algorithm that uses a heap data structure to sort elements in ascending or descending order.

Understanding both arrays and heaps is crucial for designing and implementing efficient algorithms and data structures in C++ and other programming languages. They serve as foundational building blocks for many advanced data structures and algorithms.

### 1. Algorithms & Data Structures (C++): Heaps and Heap Sort

Heaps are fundamental data structures used in algorithm design. They're particularly handy for maintaining a maximum or minimum value efficiently. In C++, heaps are often implemented using arrays due to their compactness and cache-friendliness. Heap sort, on the other hand, is a comparison-based sorting algorithm that leverages the heap data structure.

Let's break down the concepts:

### Heaps

* **Binary Heap:** A binary heap is a complete binary tree where every level, except possibly the last, is completely filled, and the nodes are filled from left to right. It has two main variations:
  * **Max Heap:** In a max heap, the value of each node is greater than or equal to the values of its children. The highest value is at the root.
  * **Min Heap:** In a min heap, the value of each node is less than or equal to the values of its children. The lowest value is at the root.

* **Operations on Heap:**
  * **Insert:** Adds a new element to the heap while maintaining the heap property.
  * **Extract Max/Min:** Removes and returns the root element (max in a max heap, min in a min heap) while maintaining the heap property.
  * **Heapify:** Builds a heap from an array, usually used in heap sort.

### Heap Sort

Heap sort is a comparison-based sorting algorithm that works by first building a heap from the input data and then repeatedly extracting the maximum (in a max heap) and placing it at the end of the array. The heap is then reduced in size, and the process is repeated until the heap is empty. The elements end up sorted in ascending order.

Here's a basic outline of the Heap Sort algorithm:

1. **Build Max Heap:** Build a max heap from the input array.
2. **Swap and Heapify Down:** Swap the first element (maximum) with the last element of the heap, reduce the heap size by one, and heapify the root.
3. **Repeat:** Repeat step 2 until the heap size is 1.
4. **Sorted Array:** The array now contains the sorted elements.

### Implementation in C++

```cpp
#include <iostream>
#include <algorithm>

void heapify(int arr[], int n, int i) {
    int largest = i; // Initialize largest as root
    int left = 2 * i + 1;
    int right = 2 * i + 2;

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

void heapSort(int arr[], int n) {
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

int main() {
    int arr[] = {12, 11, 13, 5, 6, 7};
    int n = sizeof(arr) / sizeof(arr[0]);

    heapSort(arr, n);

    std::cout << "Sorted array is \n";
    for (int i = 0; i < n; i++)
        std::cout << arr[i] << " ";
    std::cout << std::endl;
    return 0;
}
```

This C++ code demonstrates heap sort implementation along with the heapify function for building the heap.

### 1. Algorithms & Data Structures (C++): Heaps CBT

A Complete Binary Tree (CBT) is a binary tree in which every level, except possibly the last, is completely filled, and all nodes are as far left as possible. Heaps are often implemented using Complete Binary Trees because of their efficient structure for heap operations like insertion and deletion.

In C++, you can implement a Heap using a Complete Binary Tree quite effectively. Here's a basic implementation of a max-heap using a Complete Binary Tree:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class MaxHeap {
private:
    vector<int> heap;

    // Helper function to maintain the heap property by swapping with parent if necessary
    void heapifyUp(int index) {
        int parentIndex = (index - 1) / 2;
        while (index > 0 && heap[index] > heap[parentIndex]) {
            swap(heap[index], heap[parentIndex]);
            index = parentIndex;
            parentIndex = (index - 1) / 2;
        }
    }

    // Helper function to maintain the heap property by swapping with child if necessary
    void heapifyDown(int index) {
        int leftChild = 2 * index + 1;
        int rightChild = 2 * index + 2;
        int largest = index;

        if (leftChild < heap.size() && heap[leftChild] > heap[largest])
            largest = leftChild;

        if (rightChild < heap.size() && heap[rightChild] > heap[largest])
            largest = rightChild;

        if (largest != index) {
            swap(heap[index], heap[largest]);
            heapifyDown(largest);
        }
    }

public:
    // Constructor
    MaxHeap() {}

    // Function to insert a new element into the heap
    void insert(int value) {
        heap.push_back(value);
        heapifyUp(heap.size() - 1);
    }

    // Function to get the maximum element from the heap
    int getMax() {
        if (!heap.empty())
            return heap[0];
        else
            throw runtime_error("Heap is empty!");
    }

    // Function to remove and return the maximum element from the heap
    int extractMax() {
        if (heap.empty())
            throw runtime_error("Heap is empty!");

        int max = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        heapifyDown(0);
        return max;
    }

    // Function to check if the heap is empty
    bool isEmpty() {
        return heap.empty();
    }
};

int main() {
    MaxHeap heap;
    heap.insert(10);
    heap.insert(20);
    heap.insert(15);
    heap.insert(30);

    cout << "Max element: " << heap.getMax() << endl;

    heap.extractMax();
    cout << "Max element after extraction: " << heap.getMax() << endl;

    return 0;
}
```

This code provides a basic implementation of a max-heap using a Complete Binary Tree. You can extend it with additional functionalities like deleting specific elements, heap sort, etc., depending on your requirements.

### 1. Algorithms & Data Structures (C++): Heaps Data Structure

Heaps are a fundamental data structure used in many algorithms and applications, particularly in priority queue implementations. They provide efficient access to the maximum or minimum element in a collection.

In C++, heaps are commonly implemented using arrays, where each element satisfies the heap property: for a max heap, each parent node is greater than or equal to its children; for a min heap, each parent node is less than or equal to its children.

Here's a basic overview of heap operations and implementation in C++:

### Operations

1. **Insertion**: To insert a new element into the heap, it is placed at the end of the array and then the heap property is restored by performing a "heapify up" operation.

2. **Deletion (Extract maximum or minimum)**: The maximum (for a max heap) or minimum (for a min heap) element is removed from the root of the heap. To maintain the heap property, the last element in the array replaces the root, and a "heapify down" operation is performed.

3. **Peek**: Retrieve the maximum or minimum element without removing it from the heap.

### Implementation (Max Heap)

```cpp
#include <vector>
#include <iostream>

class MaxHeap {
private:
    std::vector<int> heap;

    // Helper function to heapify up
    void heapifyUp(int index) {
        while (index > 0 && heap[parent(index)] < heap[index]) {
            std::swap(heap[parent(index)], heap[index]);
            index = parent(index);
        }
    }

    // Helper function to heapify down
    void heapifyDown(int index) {
        int left = leftChild(index);
        int right = rightChild(index);
        int largest = index;

        if (left < heap.size() && heap[left] > heap[index])
            largest = left;

        if (right < heap.size() && heap[right] > heap[largest])
            largest = right;

        if (largest != index) {
            std::swap(heap[index], heap[largest]);
            heapifyDown(largest);
        }
    }

public:
    // Get parent, left child, and right child indices
    int parent(int i) { return (i - 1) / 2; }
    int leftChild(int i) { return 2 * i + 1; }
    int rightChild(int i) { return 2 * i + 2; }

    // Insert element into the heap
    void insert(int key) {
        heap.push_back(key);
        int index = heap.size() - 1;
        heapifyUp(index);
    }

    // Extract maximum element (root) from the heap
    int extractMax() {
        if (heap.empty())
            throw std::out_of_range("Heap is empty");

        int max = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        heapifyDown(0);
        return max;
    }

    // Get the maximum element (root) without removing it
    int getMax() {
        if (heap.empty())
            throw std::out_of_range("Heap is empty");

        return heap[0];
    }

    // Check if heap is empty
    bool isEmpty() {
        return heap.empty();
    }
};
```

This code provides a basic implementation of a max heap in C++. You can modify it for a min heap by changing the comparison operators appropriately.

Remember, heaps are often used as part of more complex algorithms, such as heap sort, priority queues, and various graph algorithms like Dijkstra's algorithm. Understanding their operations and implementations is crucial for efficient algorithm design and optimization.

### 1. Algorithms & Data Structures (C++): Heaps implementation

Sure, let's delve into implementing heaps in C++.

A heap is a binary tree where every parent node has a value less than or equal to any of its children (in a max heap), or greater than or equal to any of its children (in a min heap). It's typically implemented as an array. The parent-child relationship can be established by calculating indices. Specifically, for a node at index `i`:

* Its left child is at index `2*i + 1`.
* Its right child is at index `2*i + 2`.
* Its parent is at index `(i-1)/2`.

Here's a basic implementation of a max heap in C++:

```cpp
#include <iostream>
#include <vector>

class MaxHeap {
private:
    std::vector<int> heap;

    void heapifyUp(int index) {
        while (index > 0) {
            int parentIndex = (index - 1) / 2;
            if (heap[index] > heap[parentIndex]) {
                std::swap(heap[index], heap[parentIndex]);
                index = parentIndex;
            } else {
                break;
            }
        }
    }

    void heapifyDown(int index) {
        int size = heap.size();
        while (2 * index + 1 < size) {
            int leftChild = 2 * index + 1;
            int rightChild = 2 * index + 2;
            int largest = index;
            if (leftChild < size && heap[leftChild] > heap[largest]) {
                largest = leftChild;
            }
            if (rightChild < size && heap[rightChild] > heap[largest]) {
                largest = rightChild;
            }
            if (largest != index) {
                std::swap(heap[index], heap[largest]);
                index = largest;
            } else {
                break;
            }
        }
    }

public:
    MaxHeap() {}

    void insert(int value) {
        heap.push_back(value);
        heapifyUp(heap.size() - 1);
    }

    int extractMax() {
        if (heap.empty()) {
            throw std::out_of_range("Heap is empty");
        }
        int max = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        heapifyDown(0);
        return max;
    }

    int getMax() {
        if (heap.empty()) {
            throw std::out_of_range("Heap is empty");
        }
        return heap[0];
    }

    bool empty() {
        return heap.empty();
    }
};

int main() {
    MaxHeap maxHeap;
    maxHeap.insert(5);
    maxHeap.insert(3);
    maxHeap.insert(8);
    maxHeap.insert(1);

    std::cout << "Max element: " << maxHeap.getMax() << std::endl;

    std::cout << "Extracted max element: " << maxHeap.extractMax() << std::endl;
    std::cout << "Max element after extraction: " << maxHeap.getMax() << std::endl;

    return 0;
}
```

This implementation provides basic functionalities like insertion, extraction of the maximum element, and getting the maximum element without removing it. It uses vector to store the heap elements and performs heapify operations to maintain the heap property. You can extend it further by adding more operations or making it a template class to support different types of elements.

### 1. Algorithms & Data Structures (C++): Heaps: Implementing Peek and Remove

Certainly! A heap is a data structure that satisfies the heap property. Typically, in a min-heap, for any node \( i \), the value of \( i \)'th node is less than or equal to the values of its children. In a max-heap, it's the opposite, where the parent node is greater than or equal to its children.

Here's how you can implement peek (getting the minimum or maximum element without removing it) and remove (removing the minimum or maximum element) functions for a min-heap in C++:

```cpp
#include <iostream>
#include <vector>
using namespace std;

class MinHeap {
private:
    vector<int> heap;

    // Helper function to maintain the heap property
    void heapifyUp(int index) {
        int parent = (index - 1) / 2;
        while (index > 0 && heap[index] < heap[parent]) {
            swap(heap[index], heap[parent]);
            index = parent;
            parent = (index - 1) / 2;
        }
    }

    void heapifyDown(int index) {
        int smallest = index;
        int leftChild = 2 * index + 1;
        int rightChild = 2 * index + 2;
        if (leftChild < heap.size() && heap[leftChild] < heap[smallest]) {
            smallest = leftChild;
        }
        if (rightChild < heap.size() && heap[rightChild] < heap[smallest]) {
            smallest = rightChild;
        }
        if (smallest != index) {
            swap(heap[index], heap[smallest]);
            heapifyDown(smallest);
        }
    }

public:
    void insert(int value) {
        heap.push_back(value);
        heapifyUp(heap.size() - 1);
    }

    int peek() {
        if (!heap.empty()) {
            return heap[0];
        }
        throw runtime_error("Heap is empty");
    }

    void remove() {
        if (!heap.empty()) {
            heap[0] = heap.back();
            heap.pop_back();
            heapifyDown(0);
        } else {
            throw runtime_error("Heap is empty");
        }
    }

    void printHeap() {
        for (int i = 0; i < heap.size(); ++i) {
            cout << heap[i] << " ";
        }
        cout << endl;
    }
};

int main() {
    MinHeap minHeap;
    minHeap.insert(4);
    minHeap.insert(2);
    minHeap.insert(6);
    minHeap.insert(1);
    minHeap.insert(5);

    cout << "Heap: ";
    minHeap.printHeap();

    cout << "Peek: " << minHeap.peek() << endl;
    minHeap.remove();
    cout << "After removing min element: ";
    minHeap.printHeap();

    return 0;
}
```

This code implements a min-heap, where the `insert` function adds elements to the heap, `peek` function returns the minimum element without removing it, and `remove` function removes the minimum element from the heap. `heapifyUp` and `heapifyDown` are helper functions to maintain the heap property during insertion and removal.

### 1. Algorithms & Data Structures (C++): Heaps: Insertion

Sure! In C++, you can implement a heap data structure for insertion using an array-based approach. Here's a basic implementation of the insertion operation for a max-heap:

```cpp
#include <iostream>
#include <vector>

class MaxHeap {
private:
    std::vector<int> heap;

    void heapifyUp(int index) {
        int parent = (index - 1) / 2;
        while (index > 0 && heap[index] > heap[parent]) {
            std::swap(heap[index], heap[parent]);
            index = parent;
            parent = (index - 1) / 2;
        }
    }

public:
    void insert(int value) {
        heap.push_back(value);
        heapifyUp(heap.size() - 1);
    }

    void print() {
        for (int i : heap) {
            std::cout << i << " ";
        }
        std::cout << std::endl;
    }
};

int main() {
    MaxHeap maxHeap;
    maxHeap.insert(5);
    maxHeap.insert(3);
    maxHeap.insert(8);
    maxHeap.insert(1);
    maxHeap.insert(10);

    maxHeap.print(); // Output: 10 5 8 1 3

    return 0;
}
```

In this implementation:

* We use a `std::vector<int>` to represent the heap.
* The `insert` function adds an element to the end of the vector and then calls `heapifyUp` to maintain the heap property.
* The `heapifyUp` function moves the newly inserted element up in the heap until it satisfies the heap property.
* In the `main` function, we demonstrate inserting elements into the max-heap and printing the heap after each insertion to show that the max-heap property is maintained.

### 1. Algorithms & Data Structures (C++): Heaps: Insertion: Theory

Sure, let's delve into the theory of inserting elements into a heap data structure, particularly in the context of a binary heap, which is one of the most common implementations.

### Binary Heap Overview

A binary heap is a complete binary tree, meaning all levels of the tree are fully filled except for possibly the last level, which is filled from left to right. It can be represented as an array, where the parent's index is always less than its children's indices. There are two types of binary heaps: min heap and max heap.

* In a **min heap**, the parent node is smaller than or equal to its children nodes.
* In a **max heap**, the parent node is greater than or equal to its children nodes.

### Insertion Algorithm

When inserting a new element into a heap, the typical approach involves the following steps:

1. **Insertion at the Bottom**: First, the new element is added to the bottom level, maintaining the complete binary tree property. This means the new element is placed in the first available slot from left to right at the deepest level.

2. **Percolate Up (Heapify Up)**: After adding the element at the bottom, it's compared with its parent node. If the heap property is violated (for min heap: the parent is greater than the new element, for max heap: the parent is smaller than the new element), the elements are swapped. This process continues recursively until the heap property is satisfied.

### Insertion Procedure

Let's say we are inserting a new element `x` into a heap.

1. Add `x` to the end of the array (bottom level, rightmost position).
2. Compare the newly added element with its parent.
3. If `x` is less (for min heap) or greater (for max heap) than its parent, swap `x` with its parent.
4. Repeat steps 2-3 until the heap property is restored.

### Time Complexity

The time complexity of inserting an element into a heap is O(log n), where n is the number of elements in the heap. This complexity arises from the fact that, in the worst case, the height of the binary heap is logarithmic to the number of elements.

### Example

Let's illustrate the insertion of an element `7` into a min heap:

Initial heap:

```
      5
     / \
    8   12
   / \
  11  14
```

After inserting `7`:

```
      5
     / \
    7   12
   / \  /
  11  14 8
```

7 is placed at the bottom-right position and then percolated up to its correct position to maintain the min heap property.

That's the theory behind inserting elements into a heap! Let me know if you need further clarification or examples.

### 1. Algorithms & Data Structures (C++): Heaps: Performance of Operations in a Heap

In a heap data structure, the performance of operations depends on the type of operation being performed. The main operations on a heap are insertion, deletion, and heapification (which includes building a heap from an array). Here's a breakdown of the performance of these operations in a binary heap, which is the most common type of heap:

1. **Insertion**:
   * When inserting a new element into a heap, you typically add it at the bottom level, maintaining the heap property, and then "bubble up" the element until the heap property is restored.
   * The worst-case time complexity of insertion in a binary heap is O(log n), where n is the number of elements in the heap. This is because the height of a binary heap is logarithmic with respect to the number of elements.

2. **Deletion (Extraction of the Minimum/Maximum)**:
   * In a binary heap, the minimum (or maximum) element is always at the root of the heap. When you delete this element, you replace it with the last element in the heap and then "bubble down" the new root until the heap property is restored.
   * The worst-case time complexity of deletion in a binary heap is also O(log n), where n is the number of elements in the heap. Like insertion, this is because the height of a binary heap is logarithmic with respect to the number of elements.

3. **Heapification (Building a Heap)**:
   * Heapification is the process of converting an array of elements into a heap. This involves adjusting the elements of the array to satisfy the heap property.
   * The worst-case time complexity of building a heap from an array is O(n), where n is the number of elements in the array. This is because you can start from the middle of the array and perform "bubble down" operations on each element, effectively building the heap bottom-up.

Overall, binary heaps provide efficient operations for insertion, deletion, and heapification, with worst-case time complexities of O(log n) for insertion and deletion, and O(n) for building a heap from an array. These properties make heaps suitable for priority queues and implementing algorithms like heap sort.

### 1. Algorithms & Data Structures (C++): Heaps: Remove: Theory

In the context of algorithms and data structures, heaps are tree-based data structures that satisfy the heap property. A heap is typically implemented as a binary tree, where each node in the tree satisfies the heap property, which depends on whether it's a min-heap or a max-heap.

In a min-heap, for every node \( i \) other than the root, the value of the node is greater than or equal to the value of its parent. In other words, the smallest element is at the root. Conversely, in a max-heap, the value of each node is less than or equal to the value of its parent, making the largest element at the root.

Heaps are commonly used to implement priority queues and for heap sort algorithms due to their efficient operations for inserting and removing elements.

To remove an element from a heap, the general procedure involves:

1. **Find the Element to Remove**: Locate the element you want to remove. In a priority queue, this is often the element with the highest (for a max-heap) or lowest (for a min-heap) priority.

2. **Swap with Last Element**: Swap the element to be removed with the last element in the heap. This ensures that the heap remains complete.

3. **Remove the Last Element**: After swapping, remove the last element (which now contains the element to be removed).

4. **Heapify**: After removal, the heap property may be violated at the root. To restore the heap property, perform heapify operation, which means moving the root element down the heap to its appropriate position based on its value and the heap property (either min-heap or max-heap).

The complexity of removing an element from a heap is \( O(\log n) \), where \( n \) is the number of elements in the heap. This is because heapify operations are required, which have logarithmic complexity.

In C++, heaps are commonly implemented using arrays. The index of a parent and its children can be easily calculated using simple arithmetic operations. This allows for efficient removal and insertion operations on heaps.

### 1. Algorithms & Data Structures (C++): How to build a Binary Heap

To build a binary heap in C++, you can follow these steps:

1. **Define the BinaryHeap class**: Begin by defining a class for the binary heap. This class will hold the necessary data members and member functions to implement the heap operations.

2. **Data Members**: The main data member will be an array to store the elements of the heap. You can also include other variables like the size of the heap.

3. **Constructor**: Implement a constructor to initialize the heap with an empty array and set the size to zero.

4. **Heapify Up**: Implement a function to maintain the heap property while inserting elements into the heap. This function, often called heapify-up or bubble-up, compares the newly inserted element with its parent and swaps them if necessary until the heap property is satisfied.

5. **Heapify Down**: Implement a function to maintain the heap property while removing elements from the heap. This function, often called heapify-down or bubble-down, compares the element being removed with its children and swaps it with the smaller (for a min-heap) or larger (for a max-heap) child until the heap property is satisfied.

6. **Insertion**: Implement a function to insert elements into the heap. This function will add the new element to the end of the array and then call heapify-up to maintain the heap property.

7. **Extraction**: Implement a function to extract the root element of the heap. This function will remove the root element, move the last element to the root position, and then call heapify-down to maintain the heap property.

Here's a basic example implementation of a min-heap in C++:

```cpp
#include <vector>
#include <iostream>

using namespace std;

class BinaryHeap {
private:
    vector<int> heap;

    // Helper functions for heap operations
    void heapifyUp(int index) {
        while (index > 0) {
            int parent = (index - 1) / 2;
            if (heap[index] < heap[parent]) {
                swap(heap[index], heap[parent]);
                index = parent;
            } else {
                break;
            }
        }
    }

    void heapifyDown(int index) {
        int size = heap.size();
        while (index < size) {
            int leftChild = 2 * index + 1;
            int rightChild = 2 * index + 2;
            int smallest = index;

            if (leftChild < size && heap[leftChild] < heap[smallest])
                smallest = leftChild;

            if (rightChild < size && heap[rightChild] < heap[smallest])
                smallest = rightChild;

            if (smallest != index) {
                swap(heap[index], heap[smallest]);
                index = smallest;
            } else {
                break;
            }
        }
    }

public:
    // Constructor
    BinaryHeap() {}

    // Insertion
    void insert(int value) {
        heap.push_back(value);
        heapifyUp(heap.size() - 1);
    }

    // Extraction
    int extractMin() {
        if (heap.empty()) {
            cerr << "Heap is empty\n";
            return -1; // Or throw an exception
        }

        int min = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        heapifyDown(0);
        return min;
    }
};

int main() {
    BinaryHeap minHeap;

    minHeap.insert(10);
    minHeap.insert(20);
    minHeap.insert(15);
    minHeap.insert(30);
    minHeap.insert(5);

    cout << "Extracted Min: " << minHeap.extractMin() << endl; // Should print 5

    return 0;
}
```

This code provides a basic implementation of a binary min-heap in C++. You can modify it as needed for your specific requirements or to implement a max-heap instead.

### 1. Algorithms & Data Structures (C++): Implementation of Heap

Sure! Here's a basic implementation of a max-heap in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class MaxHeap {
private:
    vector<int> heap;

    // Helper function to maintain heap property by swapping elements upward
    void heapifyUp(int index) {
        int parentIndex = (index - 1) / 2;
        while (index > 0 && heap[index] > heap[parentIndex]) {
            swap(heap[index], heap[parentIndex]);
            index = parentIndex;
            parentIndex = (index - 1) / 2;
        }
    }

    // Helper function to maintain heap property by swapping elements downward
    void heapifyDown(int index) {
        int leftChild, rightChild, largestChild;
        while (true) {
            leftChild = 2 * index + 1;
            rightChild = 2 * index + 2;
            largestChild = index;
            if (leftChild < heap.size() && heap[leftChild] > heap[largestChild]) {
                largestChild = leftChild;
            }
            if (rightChild < heap.size() && heap[rightChild] > heap[largestChild]) {
                largestChild = rightChild;
            }
            if (largestChild != index) {
                swap(heap[index], heap[largestChild]);
                index = largestChild;
            } else {
                break;
            }
        }
    }

public:
    // Constructor
    MaxHeap() {}

    // Insertion operation
    void insert(int key) {
        heap.push_back(key);
        heapifyUp(heap.size() - 1);
    }

    // Get the maximum element (root of the heap)
    int getMax() {
        if (heap.empty()) {
            throw out_of_range("Heap is empty");
        }
        return heap[0];
    }

    // Extract the maximum element (root of the heap)
    int extractMax() {
        if (heap.empty()) {
            throw out_of_range("Heap is empty");
        }
        int maxElement = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        heapifyDown(0);
        return maxElement;
    }

    // Check if the heap is empty
    bool isEmpty() {
        return heap.empty();
    }

    // Get the size of the heap
    int size() {
        return heap.size();
    }
};

int main() {
    MaxHeap maxHeap;
    maxHeap.insert(10);
    maxHeap.insert(20);
    maxHeap.insert(15);
    cout << "Max Element: " << maxHeap.getMax() << endl;
    cout << "Extract Max Element: " << maxHeap.extractMax() << endl;
    cout << "Max Element: " << maxHeap.getMax() << endl;

    return 0;
}
```

This code provides a basic implementation of a max-heap, which is a binary tree where the value of each node is greater than or equal to the values of its children. It includes functions for insertion, extracting the maximum element, checking if the heap is empty, and getting the size of the heap.

### 1. Algorithms & Data Structures (C++): Inplace Heap Sort

In-place heap sort is a sorting algorithm that sorts an array in ascending order by first building a max heap from the array and then repeatedly removing the maximum element from the heap and placing it at the end of the array. Here's how it works in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to heapify a subtree rooted at index i in an array of size n
void heapify(vector<int>& arr, int n, int i) {
    int largest = i;  // Initialize largest as root
    int left = 2 * i + 1;  // left child = 2*i + 1
    int right = 2 * i + 2;  // right child = 2*i + 2

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

// Main function to perform heap sort
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

This C++ code defines functions for heapifying a subtree and for performing heap sort. In the `heapify` function, the largest element is placed at the root position, and the function is recursively applied to the affected subtree. In the `heapSort` function, the array is first converted into a max heap, and then elements are extracted from the heap one by one to obtain the sorted array.

### 1. Algorithms & Data Structures (C++): Insert & Delete in Heaps

Sure, I can explain how to insert and delete elements in a heap using C++.

**Heap Insertion (Push):**

When you insert a new element into a heap, you typically add it at the end of the heap and then adjust the heap to maintain its properties. Here's how you can insert an element into a heap:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to restore the heap property after inserting an element
void heapify_up(vector<int>& heap, int idx) {
    while (idx > 0) {
        int parent_idx = (idx - 1) / 2;
        if (heap[idx] <= heap[parent_idx]) {
            break;  // Heap property is satisfied
        }
        swap(heap[idx], heap[parent_idx]);
        idx = parent_idx;
    }
}

// Function to insert an element into the heap
void push_heap(vector<int>& heap, int val) {
    heap.push_back(val); // Add the element at the end
    heapify_up(heap, heap.size() - 1); // Restore the heap property
}

int main() {
    vector<int> heap = {10, 7, 6, 5, 3, 8};
    push_heap(heap, 9);
    cout << "Heap after insertion: ";
    for (int val : heap) {
        cout << val << " ";
    }
    cout << endl;
    return 0;
}
```

**Heap Deletion (Pop):**

When you delete an element from a heap (usually the root), you replace it with the last element in the heap and then adjust the heap to maintain its properties. Here's how you can delete the root element from a heap:

```cpp
// Function to restore the heap property after deleting the root element
void heapify_down(vector<int>& heap, int idx) {
    int n = heap.size();
    while (2 * idx + 1 < n) {
        int left_child_idx = 2 * idx + 1;
        int right_child_idx = 2 * idx + 2;
        int max_child_idx = left_child_idx;
        if (right_child_idx < n && heap[right_child_idx] > heap[left_child_idx]) {
            max_child_idx = right_child_idx;
        }
        if (heap[idx] >= heap[max_child_idx]) {
            break;  // Heap property is satisfied
        }
        swap(heap[idx], heap[max_child_idx]);
        idx = max_child_idx;
    }
}

// Function to delete the root element from the heap
void pop_heap(vector<int>& heap) {
    if (heap.empty()) {
        return;
    }
    heap[0] = heap.back(); // Replace the root with the last element
    heap.pop_back(); // Remove the last element
    heapify_down(heap, 0); // Restore the heap property
}

int main() {
    vector<int> heap = {10, 9, 8, 5, 3, 7, 6};
    pop_heap(heap);
    cout << "Heap after deletion: ";
    for (int val : heap) {
        cout << val << " ";
    }
    cout << endl;
    return 0;
}
```

These functions implement the insertion and deletion operations for a max heap. For a min heap, you would need to modify the comparison conditions accordingly.

### 1. Algorithms & Data Structures (C++): Insert a node in Binary Heap

Sure! A binary heap is a complete binary tree where each node has a value less than or equal to (for a max heap) or greater than or equal to (for a min heap) the values of its children. To insert a node into a binary heap, you typically follow these steps:

1. Add the new node at the end of the heap (i.e., the bottom-rightmost position).
2. Compare the value of the new node with its parent.
3. If the heap property is violated (i.e., the parent's value is less than for a max heap, or greater than for a min heap, than the new node's value), swap the new node with its parent.
4. Repeat step 3 until the heap property is satisfied.

Here's a C++ implementation of inserting a node into a binary heap:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to swap two elements in the heap
void swap(vector<int> &heap, int i, int j) {
    int temp = heap[i];
    heap[i] = heap[j];
    heap[j] = temp;
}

// Function to insert a node into the binary heap
void insertNode(vector<int> &heap, int value) {
    heap.push_back(value); // Step 1: Add the new node at the end
    
    int currentIndex = heap.size() - 1;
    int parentIndex = (currentIndex - 1) / 2;

    // Steps 2 and 3: Compare with parent and swap if necessary
    while (currentIndex > 0 && heap[currentIndex] > heap[parentIndex]) {
        swap(heap, currentIndex, parentIndex);
        currentIndex = parentIndex;
        parentIndex = (currentIndex - 1) / 2;
    }
}

// Function to print the heap
void printHeap(const vector<int> &heap) {
    for (int i = 0; i < heap.size(); ++i) {
        cout << heap[i] << " ";
    }
    cout << endl;
}

int main() {
    vector<int> maxHeap; // Example of max heap
    insertNode(maxHeap, 10);
    insertNode(maxHeap, 20);
    insertNode(maxHeap, 15);
    insertNode(maxHeap, 30);
    insertNode(maxHeap, 25);

    cout << "Max Heap after insertion: ";
    printHeap(maxHeap);

    return 0;
}
```

This code defines functions to swap elements in the heap, insert a node into the heap, and print the heap. Then, it demonstrates inserting nodes into a max heap and printing the heap after each insertion.

### 1. Algorithms & Data Structures (C++): Insert And Remove From A Heap

Sure, let's dive into implementing insertion and removal operations in a heap data structure using C++.

A heap is a specialized binary tree-based data structure that satisfies the heap property. In a min-heap, for any given node \( i \), the value of the parent node is less than or equal to the value of its children nodes. In a max-heap, it's the opposite; the value of the parent node is greater than or equal to the value of its children nodes.

Here's a basic implementation of a min-heap in C++ along with insertion and removal operations:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class MinHeap {
private:
    vector<int> heap;

    // Helper function to maintain heap property after insertion
    void heapifyUp(int index) {
        int parent = (index - 1) / 2;
        while (index > 0 && heap[index] < heap[parent]) {
            swap(heap[index], heap[parent]);
            index = parent;
            parent = (index - 1) / 2;
        }
    }

    // Helper function to maintain heap property after removal
    void heapifyDown(int index) {
        int leftChild = 2 * index + 1;
        int rightChild = 2 * index + 2;
        int smallest = index;

        if (leftChild < heap.size() && heap[leftChild] < heap[smallest])
            smallest = leftChild;
        if (rightChild < heap.size() && heap[rightChild] < heap[smallest])
            smallest = rightChild;

        if (smallest != index) {
            swap(heap[index], heap[smallest]);
            heapifyDown(smallest);
        }
    }

public:
    // Function to insert a new element into the heap
    void insert(int value) {
        heap.push_back(value);
        heapifyUp(heap.size() - 1);
    }

    // Function to remove the minimum element from the heap
    void removeMin() {
        if (heap.empty()) {
            cout << "Heap is empty!" << endl;
            return;
        }
        heap[0] = heap.back();
        heap.pop_back();
        heapifyDown(0);
    }

    // Function to get the minimum element from the heap
    int getMin() {
        if (heap.empty()) {
            cout << "Heap is empty!" << endl;
            return -1; // or throw an exception
        }
        return heap[0];
    }

    // Function to check if the heap is empty
    bool isEmpty() {
        return heap.empty();
    }
};

int main() {
    MinHeap minHeap;
    minHeap.insert(3);
    minHeap.insert(2);
    minHeap.insert(1);
    minHeap.insert(4);

    cout << "Minimum element: " << minHeap.getMin() << endl;

    minHeap.removeMin();
    cout << "Minimum element after removal: " << minHeap.getMin() << endl;

    return 0;
}
```

This implementation provides methods to insert elements into the heap, remove the minimum element, get the minimum element, and check if the heap is empty. The `heapifyUp` and `heapifyDown` functions ensure that the heap property is maintained after insertion and removal operations, respectively.

Feel free to ask if you have any questions or need further clarification!

### 1. Algorithms & Data Structures (C++): Insert in a Heap

In C++, you can insert elements into a heap data structure using the `push_heap()` function provided by the `<algorithm>` header. Here's a simple example demonstrating how to insert an element into a max heap:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main() {
    // Create a vector to represent a heap
    vector<int> heap = {10, 7, 9, 5, 3, 8};

    // Display the original heap
    cout << "Original heap: ";
    for (int num : heap) {
        cout << num << " ";
    }
    cout << endl;

    // Insert a new element into the heap
    int new_element = 12;
    heap.push_back(new_element);
    push_heap(heap.begin(), heap.end());

    // Display the heap after insertion
    cout << "Heap after insertion: ";
    for (int num : heap) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}
```

In this example, `push_heap()` is used to maintain the heap property after inserting an element into the heap. The new element is first added to the end of the vector representing the heap, and then `push_heap()` is called to re-establish the heap property. After insertion, the heap will be restructured to maintain the heap property.

### 1. Algorithms & Data Structures (C++): Insertion In Heaps - Sift Up

In C++, when implementing insertion in heaps, the "sift up" operation is commonly used to maintain the heap property after inserting an element into the heap. This operation ensures that the newly inserted element moves up the heap to its correct position, so that the heap maintains its structure (e.g., max-heap or min-heap).

Here's a basic implementation of the sift up operation for inserting elements into a max-heap:

```cpp
#include <vector>

using namespace std;

class MaxHeap {
private:
    vector<int> heap;

    // Helper function to swap two elements in the heap
    void swap(int& a, int& b) {
        int temp = a;
        a = b;
        b = temp;
    }

    // Sift up operation to maintain max-heap property after insertion
    void siftUp(int index) {
        while (index > 0 && heap[index] > heap[parent(index)]) {
            swap(heap[index], heap[parent(index)]);
            index = parent(index);
        }
    }

    // Helper function to get the index of the parent of a node
    int parent(int i) {
        return (i - 1) / 2;
    }

public:
    // Constructor
    MaxHeap() {}

    // Insertion operation
    void insert(int value) {
        heap.push_back(value); // Add the new element at the end
        siftUp(heap.size() - 1); // Perform sift up operation from the last element
    }
};
```

This `MaxHeap` class provides a basic implementation of a max-heap data structure, including the `insert` method that inserts a new element into the heap and ensures that the heap property is maintained using the sift up operation.

You can similarly implement a min-heap by modifying the comparison condition in the `siftUp` method and changing the parent index calculation if necessary.

### 1. Algorithms & Data Structures (C++): Insertion into Heap

Insertion into a heap, particularly a binary heap, follows a specific algorithm to maintain the heap property. In a binary heap, every node has a value greater than or equal to (or less than or equal to, depending on whether it's a max heap or a min heap) its children.

Here's how you can insert an element into a binary heap in C++:

```cpp
#include <vector>

// Function to maintain the heap property after inserting an element
void heapifyUp(std::vector<int>& heap, int index) {
    // Index 0 is considered as the root, so no need to heapify further
    if (index == 0)
        return;

    int parentIndex = (index - 1) / 2; // Calculate the index of the parent node

    // If the current node is greater than its parent (for max heap),
    // or less than its parent (for min heap), swap them
    if (heap[index] > heap[parentIndex]) {
        std::swap(heap[index], heap[parentIndex]);
        // Recursively heapify the parent node
        heapifyUp(heap, parentIndex);
    }
}

// Function to insert an element into the heap
void insertIntoHeap(std::vector<int>& heap, int value) {
    // Add the new element at the end of the heap
    heap.push_back(value);
    // Heapify the heap upwards starting from the last index
    heapifyUp(heap, heap.size() - 1);
}
```

You can use these functions as follows:

```cpp
int main() {
    std::vector<int> maxHeap = {30, 20, 10, 5, 15};
    
    // Insert a new element into the heap
    insertIntoHeap(maxHeap, 25);
    
    // Display the heap after insertion
    for (int num : maxHeap)
        std::cout << num << " ";
    std::cout << std::endl;
    
    return 0;
}
```

This will output the elements of the heap after insertion, maintaining the heap property.

### 1. Algorithms & Data Structures (C++): Kth Largest Element In An Array - Heaps

Certainly! Implementing the algorithm to find the Kth largest element in an array using heaps, specifically a max-heap, is an efficient approach. Here's how you can do it in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

int findKthLargest(vector<int>& nums, int k) {
    priority_queue<int> maxHeap;

    // Push all elements into the max heap
    for (int num : nums) {
        maxHeap.push(num);
    }

    // Pop k-1 elements from the heap
    for (int i = 0; i < k - 1; ++i) {
        maxHeap.pop();
    }

    // Return the top element which is the kth largest
    return maxHeap.top();
}

int main() {
    vector<int> nums = {3, 2, 1, 5, 6, 4}; // Example array
    int k = 2; // Finding the 2nd largest element

    int kthLargest = findKthLargest(nums, k);
    cout << "The " << k << "th largest element is: " << kthLargest << endl;

    return 0;
}
```

In this code:

* We use `priority_queue` from the Standard Template Library (STL) of C++, which by default is a max-heap.
* We push all elements from the array into the max heap.
* We pop `k-1` elements from the heap because we are interested in the `k`th largest element.
* Finally, we return the top element of the heap, which is the `k`th largest element in the array.

This implementation has a time complexity of O(N log N), where N is the number of elements in the array, due to the construction of the heap.

### 1. Algorithms & Data Structures (C++): Max Binary Heap - Extract Max

To implement the `Extract Max` operation in a Max Binary Heap in C++, you typically follow these steps:

1. Save the root node's value (the maximum element).
2. Swap the root node with the last node of the heap.
3. Remove the last node (previously the root).
4. Restore the heap property by 'sinking down' the new root node to its correct position.

Here's a sample implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class MaxHeap {
private:
    vector<int> heap;

    // Helper function to maintain heap property by shifting a node down
    void heapifyDown(int index) {
        int leftChild = 2 * index + 1;
        int rightChild = 2 * index + 2;
        int largest = index;

        if (leftChild < heap.size() && heap[leftChild] > heap[largest])
            largest = leftChild;

        if (rightChild < heap.size() && heap[rightChild] > heap[largest])
            largest = rightChild;

        if (largest != index) {
            swap(heap[index], heap[largest]);
            heapifyDown(largest); // Recursively heapify the affected subtree
        }
    }

public:
    // Extract the maximum element from the heap
    int extractMax() {
        if (heap.empty())
            throw runtime_error("Heap is empty");

        int maxElement = heap[0]; // Save the maximum element
        heap[0] = heap.back();    // Replace root with last element
        heap.pop_back();           // Remove the last element
        heapifyDown(0);           // Restore heap property
        return maxElement;        // Return the extracted maximum element
    }

    // Other methods (e.g., insert, print, etc.) can be implemented here
};

int main() {
    MaxHeap maxHeap;
    // Insert elements into the heap
    maxHeap.insert(10);
    maxHeap.insert(20);
    maxHeap.insert(15);
    maxHeap.insert(30);
    maxHeap.insert(5);

    cout << "Max Heap: ";
    maxHeap.print();

    // Extract the maximum element
    cout << "Extracted Max Element: " << maxHeap.extractMax() << endl;

    cout << "Max Heap after extraction: ";
    maxHeap.print();

    return 0;
}
```

In this implementation, `heapifyDown()` is used to restore the heap property after extracting the maximum element. It compares the current node with its children and swaps it with the larger child if necessary, continuing the process recursively until the heap property is restored.

### 1. Algorithms & Data Structures (C++): Max Binary Heap - Insert

Sure! In C++, you can implement a max binary heap and its insertion operation as follows:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class MaxHeap {
private:
    vector<int> heap;

    // Helper function to maintain heap property after insertion
    void heapifyUp(int index) {
        int parent = (index - 1) / 2;
        while (index > 0 && heap[index] > heap[parent]) {
            // Swap the current node with its parent
            swap(heap[index], heap[parent]);
            index = parent;
            parent = (index - 1) / 2;
        }
    }

public:
    // Insert an element into the max heap
    void insert(int value) {
        // Insert the new element at the end
        heap.push_back(value);
        
        // Maintain heap property
        heapifyUp(heap.size() - 1);
    }

    // Function to print the elements of the heap
    void printHeap() {
        cout << "Max Heap: ";
        for (int i = 0; i < heap.size(); ++i) {
            cout << heap[i] << " ";
        }
        cout << endl;
    }
};

int main() {
    MaxHeap maxHeap;

    // Insert elements into the max heap
    maxHeap.insert(5);
    maxHeap.insert(3);
    maxHeap.insert(10);
    maxHeap.insert(8);
    maxHeap.insert(1);

    // Print the max heap
    maxHeap.printHeap();

    return 0;
}
```

In this implementation, the `MaxHeap` class maintains a vector `heap` to store the elements of the max heap. The `insert` function adds a new element to the heap and then calls the `heapifyUp` function to maintain the heap property by moving the newly inserted element up the tree as necessary.

You can test the insertion operation by creating a `MaxHeap` object, inserting elements into it, and then printing the heap to verify that the elements are stored in the correct order.

### 1. Algorithms & Data Structures (C++): Maximum Element In A Minimum Heap and K Largest Elements In A Stream

Sure! Let's tackle these one by one.

#### Maximum Element in a Minimum Heap

In a minimum heap, the smallest element is always at the root. So, the maximum element in a minimum heap will always be one of the leaf nodes. To find the maximum element in a minimum heap, you need to traverse the leaf nodes and find the maximum among them. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Function to find the maximum element in a minimum heap
int findMaxInMinHeap(const vector<int>& heap) {
    if (heap.empty()) {
        cout << "Heap is empty!" << endl;
        return -1; // return a sentinel value or throw an exception
    }
    
    int maxElement = heap[0]; // Initialize maxElement with the root element
    
    // Traverse leaf nodes and find the maximum element
    for (int i = (heap.size() - 1) / 2 + 1; i < heap.size(); ++i) {
        maxElement = max(maxElement, heap[i]);
    }
    
    return maxElement;
}

int main() {
    // Example usage
    vector<int> heap = {1, 3, 6, 9, 5, 8, 7};
    cout << "Maximum element in the minimum heap: " << findMaxInMinHeap(heap) << endl;
    
    return 0;
}
```

#### K Largest Elements in a Stream

To find the K largest elements in a stream, you can use a min-heap of size K. As you read elements from the stream, maintain the K largest elements in the min-heap. When the size of the heap exceeds K, remove the smallest element from the heap. This way, you'll always have the K largest elements in the heap. Here's a simple implementation in C++:

```cpp
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

// Function to find the K largest elements in a stream
vector<int> findKLargestInStream(const vector<int>& stream, int k) {
    priority_queue<int, vector<int>, greater<int>> minHeap; // Min-heap to store K largest elements
    vector<int> result;

    for (int num : stream) {
        minHeap.push(num);
        if (minHeap.size() > k) {
            minHeap.pop(); // Remove the smallest element if heap size exceeds K
        }
    }

    // Store the K largest elements from the heap into the result vector
    while (!minHeap.empty()) {
        result.push_back(minHeap.top());
        minHeap.pop();
    }

    return result;
}

int main() {
    // Example usage
    vector<int> stream = {5, 3, 8, 2, 7, 1, 9, 4, 6};
    int k = 3;
    vector<int> kLargest = findKLargestInStream(stream, k);

    cout << "K largest elements in the stream: ";
    for (int num : kLargest) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}
```

This program will print the K largest elements in the stream. In this example, with K set to 3 and the given stream, the output would be `9 8 7`.

### 1. Algorithms & Data Structures (C++): Min Binary Heap - Insert

Sure, I can guide you through the implementation of inserting an element into a minimum binary heap in C++. Here's a basic outline:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class MinHeap {
private:
    vector<int> heap;

    // Helper function to swap two elements in the heap
    void swap(int& a, int& b) {
        int temp = a;
        a = b;
        b = temp;
    }

    // Helper function to maintain heap property after insertion
    void heapifyUp(int index) {
        if (index <= 0) return; // Reached the root

        int parentIndex = (index - 1) / 2;

        // If the current node is smaller than its parent, swap and continue heapifying up
        if (heap[index] < heap[parentIndex]) {
            swap(heap[index], heap[parentIndex]);
            heapifyUp(parentIndex);
        }
    }

public:
    // Function to insert a new element into the heap
    void insert(int value) {
        heap.push_back(value); // Insert the new element at the end
        heapifyUp(heap.size() - 1); // Maintain heap property
    }

    // Function to print the heap
    void printHeap() {
        for (int i = 0; i < heap.size(); ++i) {
            cout << heap[i] << " ";
        }
        cout << endl;
    }
};

int main() {
    MinHeap heap;
    
    // Insert elements into the heap
    heap.insert(3);
    heap.insert(2);
    heap.insert(1);
    heap.insert(15);
    heap.insert(5);
    heap.insert(4);
    heap.insert(45);
    
    // Print the heap
    heap.printHeap();
    
    return 0;
}
```

In this implementation, the `MinHeap` class has a private member `heap` which is a vector used to store the elements of the heap. The `insert` function inserts a new element into the heap and then calls `heapifyUp` to maintain the heap property. The `heapifyUp` function compares the newly inserted element with its parent and swaps them if necessary until the heap property is satisfied.

Finally, in the `main` function, we create a `MinHeap` object and insert some elements into it to demonstrate the functionality.

### 1. Algorithms & Data Structures (C++): MinHeap: Insert

To implement the insertion operation for a MinHeap in C++, you typically follow these steps:

1. Add the new element at the end of the heap array.
2. Perform a "heapify-up" operation to maintain the heap property, ensuring that the newly added element is in the correct position relative to its parent(s).

Here's a C++ implementation of the insert operation for a MinHeap:

```cpp
#include <iostream>
#include <vector>

class MinHeap {
private:
    std::vector<int> heap;

    // Helper function to maintain heap property by moving the newly added element up the heap
    void heapifyUp(int index) {
        int parentIndex = (index - 1) / 2;
        while (index > 0 && heap[index] < heap[parentIndex]) {
            std::swap(heap[index], heap[parentIndex]);
            index = parentIndex;
            parentIndex = (index - 1) / 2;
        }
    }

public:
    // Function to insert a new element into the MinHeap
    void insert(int value) {
        heap.push_back(value); // Step 1: Add the new element at the end
        heapifyUp(heap.size() - 1); // Step 2: Perform heapify-up operation
    }

    // Function to print the MinHeap
    void print() {
        for (int i = 0; i < heap.size(); ++i) {
            std::cout << heap[i] << " ";
        }
        std::cout << std::endl;
    }
};

int main() {
    MinHeap minHeap;
    minHeap.insert(5);
    minHeap.insert(3);
    minHeap.insert(8);
    minHeap.insert(1);
    minHeap.insert(9);

    std::cout << "MinHeap: ";
    minHeap.print();

    return 0;
}
```

This code defines a `MinHeap` class with a `heap` vector to store the elements. The `insert` function adds a new element to the heap and then calls the `heapifyUp` function to maintain the heap property. Finally, the `print` function is provided to visualize the heap.

### 1. Algorithms & Data Structures (C++): MinHeap: Remove

In C++, removing an element from a min-heap involves a few steps to maintain the heap property. Here's how you can implement the `remove` operation for a min-heap:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class MinHeap {
private:
    vector<int> heap;

    // Helper function to swap two elements in the heap
    void swap(int& a, int& b) {
        int temp = a;
        a = b;
        b = temp;
    }

    // Helper function to heapify a subtree with the given index
    void heapifyDown(int index) {
        int left = 2 * index + 1;
        int right = 2 * index + 2;
        int smallest = index;

        if (left < heap.size() && heap[left] < heap[smallest]) {
            smallest = left;
        }

        if (right < heap.size() && heap[right] < heap[smallest]) {
            smallest = right;
        }

        if (smallest != index) {
            swap(heap[index], heap[smallest]);
            heapifyDown(smallest);
        }
    }

public:
    // Constructor
    MinHeap() {}

    // Function to remove the minimum element from the heap
    void removeMin() {
        if (heap.empty()) {
            cout << "Heap is empty. Cannot remove." << endl;
            return;
        }

        // Move the last element to the root
        heap[0] = heap.back();
        heap.pop_back();

        // Heapify down from the root
        heapifyDown(0);
    }

    // Function to insert a new element into the heap
    void insert(int val) {
        heap.push_back(val);
        int index = heap.size() - 1;

        // Heapify up
        while (index > 0 && heap[index] < heap[(index - 1) / 2]) {
            swap(heap[index], heap[(index - 1) / 2]);
            index = (index - 1) / 2;
        }
    }

    // Function to print the heap
    void printHeap() {
        cout << "Heap: ";
        for (int i = 0; i < heap.size(); i++) {
            cout << heap[i] << " ";
        }
        cout << endl;
    }
};

int main() {
    MinHeap heap;
    heap.insert(5);
    heap.insert(3);
    heap.insert(8);
    heap.insert(1);
    heap.insert(10);

    cout << "Initial ";
    heap.printHeap();

    heap.removeMin();
    cout << "After removing minimum: ";
    heap.printHeap();

    return 0;
}
```

In this implementation:

* `removeMin()` removes the minimum element from the heap.
* It replaces the root (minimum element) with the last element of the heap.
* Then it removes the last element from the heap.
* After replacing the root, it performs heapify-down operation to maintain the heap property.
* `heapifyDown()` function ensures that the heap property is maintained starting from the root.

You can test this code by running the `main()` function.



### 1. Algorithms & Data Structures (C++): Operations on Heap (Deleting an Element from a Heap)

Deleting an element from a heap in C++ involves removing an element and maintaining the heap property, which ensures that the heap remains valid. In a max heap, the maximum element is at the root, and in a min heap, the minimum element is at the root.

Here's how you can delete an element from a max heap:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to heapify down after deleting an element
void heapifyDown(vector<int>& heap, int index) {
    int size = heap.size();
    int leftChild = 2 * index + 1;
    int rightChild = 2 * index + 2;
    int largest = index;

    // Compare with left child
    if (leftChild < size && heap[leftChild] > heap[largest]) {
        largest = leftChild;
    }

    // Compare with right child
    if (rightChild < size && heap[rightChild] > heap[largest]) {
        largest = rightChild;
    }

    // If the largest element is not the current node, swap and heapify down recursively
    if (largest != index) {
        swap(heap[index], heap[largest]);
        heapifyDown(heap, largest);
    }
}

// Function to delete an element from the heap
void deleteElement(vector<int>& heap, int element) {
    int size = heap.size();
    // Find the element to be deleted
    int index = -1;
    for (int i = 0; i < size; ++i) {
        if (heap[i] == element) {
            index = i;
            break;
        }
    }

    if (index == -1) {
        cout << "Element not found in the heap\n";
        return;
    }

    // Replace the element with the last element in the heap
    heap[index] = heap[size - 1];
    // Resize the heap
    heap.resize(size - 1);
    // Heapify down from the index where the element was replaced
    heapifyDown(heap, index);
}

// Function to print the heap
void printHeap(const vector<int>& heap) {
    for (int i : heap) {
        cout << i << " ";
    }
    cout << endl;
}

int main() {
    vector<int> maxHeap = {70, 60, 50, 40, 30, 20, 10};

    cout << "Original max heap: ";
    printHeap(maxHeap);

    // Delete element 40 from the max heap
    deleteElement(maxHeap, 40);

    cout << "Max heap after deleting 40: ";
    printHeap(maxHeap);

    return 0;
}
```

This code demonstrates how to delete an element from a max heap in C++. You can adapt it for a min heap by changing the comparisons accordingly. The `heapifyDown` function is used to restore the heap property after deleting an element.


### 1. Algorithms & Data Structures (C++): Runtime characteristics of Binary Heap

A binary heap is a fundamental data structure commonly used to implement priority queues. It provides efficient operations for insertion, deletion, and finding the minimum (or maximum) element. Here are the runtime characteristics of binary heaps in terms of various operations:

1. **Insertion (HeapifyUp)**:
   - Time Complexity: O(log n)
   - Explanation: When inserting a new element into a binary heap, it is added at the next available leaf node, and then it may need to be "bubbled up" to restore the heap property (i.e., parent nodes are smaller than their children in a min-heap or larger in a max-heap). This bubbling process involves comparing the new element with its parent and swapping if necessary, repeating until the heap property is satisfied.

2. **Deletion (HeapifyDown)**:
   - Time Complexity: O(log n)
   - Explanation: When deleting the minimum (or maximum) element from a binary heap, the last leaf node is moved to the root position, and then it may need to be "bubbled down" to restore the heap property. This involves comparing the element with its children and swapping it with the smaller (or larger) child until the heap property is satisfied.

3. **Finding Minimum (or Maximum)**:
   - Time Complexity: O(1)
   - Explanation: In a binary min-heap (or max-heap), the minimum (or maximum) element is always at the root, so it can be directly accessed in constant time.

4. **Building a Heap (Heapify)**:
   - Time Complexity: O(n)
   - Explanation: Given an array of elements, building a binary heap can be done by repeatedly inserting elements into the heap. However, a more efficient method is to perform a "heapify" operation on the array, which rearranges the elements to satisfy the heap property bottom-up. The overall time complexity of heapifying the array is linear in the number of elements.

5. **Extracting Minimum (or Maximum)**:
   - Time Complexity: O(log n)
   - Explanation: Extracting the minimum (or maximum) element from a binary heap involves deleting the root element, which takes O(log n) time due to the heapify-down operation.

6. **Heapify Complexity**:
   - Space Complexity: O(1) - Heapify can be performed in-place.
   - Explanation: Heapify operations generally don't require additional space proportional to the input size; they can be done in-place, modifying the existing array or data structure.

These runtime characteristics make binary heaps efficient for priority queue operations, particularly in scenarios where elements are frequently inserted, deleted, or accessed based on their priority.

### 1. Algorithms & Data Structures (C++): Sort Operations on Heap (Inserting an Element in a Heap)

In C++, you can implement heap sort operations like inserting an element into a heap using the standard library's `priority_queue` or by implementing your own heap data structure. Here's how you can insert an element into a heap using both methods:

### Using `priority_queue`:

```cpp
#include <iostream>
#include <queue>

int main() {
    std::priority_queue<int> max_heap; // Max heap
    // std::priority_queue<int, std::vector<int>, std::greater<int>> min_heap; // Min heap

    // Inserting elements into the heap
    max_heap.push(10);
    max_heap.push(30);
    max_heap.push(20);

    // Inserting a new element into the heap
    max_heap.push(15);

    // Printing elements of the heap
    while (!max_heap.empty()) {
        std::cout << max_heap.top() << " ";
        max_heap.pop();
    }

    return 0;
}
```

### Implementing Heap from Scratch:

```cpp
#include <iostream>
#include <vector>

class MinHeap {
private:
    std::vector<int> heap;

    void heapifyUp(int index) {
        int parentIndex = (index - 1) / 2;
        while (index > 0 && heap[index] < heap[parentIndex]) {
            std::swap(heap[index], heap[parentIndex]);
            index = parentIndex;
            parentIndex = (index - 1) / 2;
        }
    }

public:
    void insert(int val) {
        heap.push_back(val);
        heapifyUp(heap.size() - 1);
    }

    void print() {
        for (int i = 0; i < heap.size(); ++i) {
            std::cout << heap[i] << " ";
        }
    }
};

int main() {
    MinHeap minHeap;
    minHeap.insert(10);
    minHeap.insert(30);
    minHeap.insert(20);
    minHeap.insert(15);

    minHeap.print(); // Output: 10 15 20 30

    return 0;
}
```

In both cases, we insert an element into the heap by pushing it into the data structure and then perform any necessary adjustments to maintain the heap property (e.g., heapify operations).



### 1. Algorithms & Data Structures (C++): The Binary Heap - Logically A Tree Really An Array

Indeed, binary heaps are often represented as arrays, making them seem like a tree logically, but implemented using an array under the hood. This representation offers several advantages in terms of memory usage and access efficiency.

Here's a brief overview of how it works:

1. **Binary Heap Structure**: Binary heaps are complete binary trees, meaning every level of the tree is fully filled except possibly for the last level, which is filled from left to right. This structure lends itself well to array representation.

2. **Array Representation**: In the array representation of a binary heap, if a node is at index `i`, its left child is at index `2*i + 1` and its right child is at index `2*i + 2`. Conversely, if a node is at index `i`, its parent is at index `(i - 1) / 2`. This mapping allows efficient navigation within the array.

3. **Heap Property**: Binary heaps maintain the heap property, which states that for a max heap, each parent node must be greater than or equal to its children, and for a min heap, each parent node must be less than or equal to its children.

4. **Operations**: The array representation simplifies heap operations such as insertion and deletion. For example, to insert a new element, it's added at the end of the array and then "bubbled up" by swapping it with its parent until the heap property is restored. Similarly, for deletion, the root element (either minimum or maximum depending on the heap type) is removed, and the last element is placed at the root and "bubbled down" to its correct position.

5. **Efficiency**: Array representation allows for better cache locality, as elements are stored sequentially in memory. This can lead to faster access times compared to tree-based structures.

So, while conceptually, binary heaps are viewed as trees due to their hierarchical nature, their array implementation offers practical advantages in terms of implementation simplicity and efficiency.


### 1. Algorithms & Data Structures (C++): Time and space complexity of Binary Heap

In algorithms and data structures, analyzing the time and space complexity of data structures like a Binary Heap, specifically in the context of C++, involves understanding its operations and their efficiency.

1. **Time Complexity:**
   - **Insertion (push):** O(log n)
     - When inserting an element into a binary heap, it needs to be placed at the next available position and then possibly bubbled up (heapify-up) to maintain the heap property. The height of the binary heap is logarithmic with respect to the number of elements (n), so the insertion operation has a time complexity of O(log n).
   - **Extraction (pop):** O(log n)
     - When extracting the minimum (or maximum) element from a binary heap, the root element is removed, and the last element of the heap replaces it. Then, the element may need to be bubbled down (heapify-down) to maintain the heap property. Again, this operation has a time complexity of O(log n) due to the logarithmic height of the binary heap.
   - **Finding minimum/maximum (top):** O(1)
     - Unlike extracting the minimum or maximum element, finding the minimum or maximum element (depending on whether it's a min-heap or a max-heap) is a constant-time operation because the root of the heap always holds the minimum or maximum value.

2. **Space Complexity:**
   - The space complexity of a binary heap is O(n), where n is the number of elements in the heap. This space is required to store the elements themselves.

Binary heaps are commonly used in algorithms like heap sort, priority queues, and graph algorithms for efficient operations on priority-based data. Understanding their time and space complexity helps in evaluating their suitability for different applications and scenarios.


### 1. Algorithms & Data Structures (C++): Using heap data structure to sort (heapsort)

Heap sort is a comparison-based sorting algorithm that uses a binary heap data structure to sort elements. It has a time complexity of O(n log n) in the worst-case scenario.

Here's how you can implement heap sort in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to heapify a subtree rooted at index i
void heapify(vector<int>& arr, int n, int i) {
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
    int n = arr.size();
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";
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

This code first builds a max heap out of the input array. Then, it repeatedly extracts the maximum element from the heap and rebuilds the heap until the entire array is sorted.


### 1. Algorithms & Data Structures (C++): What are Binary Heaps and what are they good for?

Binary heaps are a fundamental data structure commonly used in algorithm design and optimization. They are a specialized form of binary tree with two key properties:

1. **Shape Property**: Binary heaps are complete binary trees, meaning every level of the tree is fully filled except possibly for the last level, which is filled from left to right.
2. **Heap Property**: In a max heap, for every node `i` other than the root, the value of `A[parent(i)]` is at most the value of `A[i]`, meaning the value of each node is at least as large as the values of its children. Conversely, in a min heap, the value of each node is at most as large as the values of its children.

Binary heaps are commonly implemented using arrays, where the children of the node at index `i` are located at indices `2*i` (left child) and `2*i + 1` (right child). This representation allows efficient memory usage and traversal.

Binary heaps are particularly useful for priority queue implementations due to their efficient insertion, deletion, and retrieval of the maximum (or minimum) element. They offer the following time complexities:

- **Insertion**: O(log n)
- **Deletion of maximum (or minimum) element**: O(log n)
- **Peek (access the maximum or minimum element without removal)**: O(1)

Applications of binary heaps include:

1. **Priority Queues**: Binary heaps efficiently support priority queues, where elements with higher priority (or lower priority) are removed before elements with lower priority.
  
2. **Heap Sort**: Heap sort is an in-place sorting algorithm that uses binary heaps to sort elements in ascending or descending order.

3. **Graph Algorithms**: Binary heaps are used in various graph algorithms such as Dijkstra's algorithm for finding shortest paths and Prim's algorithm for minimum spanning trees.

4. **Job Scheduling**: Binary heaps are used in scheduling algorithms where jobs with higher priority need to be processed first.

Overall, binary heaps provide a simple yet powerful tool for implementing priority queues and solving various algorithmic problems efficiently.


### 1. Algorithms & Data Structures (C++): What are heaps and why they are used

In computer science, a heap is a specialized tree-based data structure that satisfies the heap property. This property depends on the type of heap (min-heap or max-heap). In a min-heap, for example, the key of a parent node is less than or equal to the keys of its children, while in a max-heap, the key of a parent node is greater than or equal to the keys of its children.

Heaps are primarily used to implement priority queues and to efficiently find the maximum or minimum element in a dataset. Here are some key features and use cases of heaps:

1. **Priority Queue Implementation**: Heaps are commonly used to implement priority queues, where elements with higher priority are served before elements with lower priority. The heap property ensures that the highest (or lowest, depending on the type of heap) priority element is always at the root, allowing for efficient retrieval.

2. **Efficient Insertion and Removal**: Heaps support efficient insertion and removal of elements. When inserting an element into a heap, it is placed at the next available position (usually at the bottom level of the tree) and then "heapified" by adjusting its position upwards until the heap property is restored. Similarly, when removing the root element (the maximum or minimum), the last element in the heap replaces the root, and then the heap is adjusted downwards to maintain the heap property.

3. **Heap Sort**: Heaps can be used to implement an efficient sorting algorithm known as heap sort. In heap sort, the input array is first converted into a max-heap (for ascending order) or a min-heap (for descending order). Then, the root element (maximum or minimum) is repeatedly removed from the heap, resulting in a sorted array.

4. **Memory Allocation**: Heaps are also used in memory allocation algorithms, such as the binary buddy system, where memory blocks of varying sizes are allocated and deallocated from a heap.

5. **Graph Algorithms**: Heaps are used in various graph algorithms, such as Dijkstra's shortest path algorithm and Prim's minimum spanning tree algorithm, to efficiently select the next vertex or edge based on their weights or costs.

Overall, heaps are versatile data structures that offer efficient operations for managing priority-based data and are widely used in various algorithms and applications across computer science and software engineering.


### 1. Algorithms & Data Structures (C++): What is Binary Heap? Why do we need it?

A binary heap is a specialized tree-based data structure that satisfies the heap property. In a binary heap, for every node \( i \) other than the root, the value stored at \( i \) is greater than or equal to the value stored at its parent. Binary heaps are typically implemented as arrays.

There are two main types of binary heaps:

1. **Min Heap**: In a min heap, the value of each node is less than or equal to the values of its children.
2. **Max Heap**: In a max heap, the value of each node is greater than or equal to the values of its children.

Binary heaps are commonly used for implementing priority queues and for efficiently finding the minimum or maximum element in a collection. They offer efficient insertion, deletion, and retrieval of the minimum or maximum element, all with logarithmic time complexity (\( O(\log n) \)). This makes binary heaps suitable for applications where fast access to the minimum or maximum element is crucial, such as in Dijkstra's algorithm for finding shortest paths in graphs and in implementing heapsort, a comparison-based sorting algorithm.

In addition to their efficiency, binary heaps are simple to implement and use minimal memory overhead compared to other tree-based structures like binary search trees. This combination of efficiency and simplicity makes binary heaps a valuable tool in algorithm design and optimization.


### 1. Algorithms & Data Structures (C++): What is Heap?

In computer science, a heap is a specialized tree-based data structure that satisfies the heap property. This property depends on whether it's a min-heap or a max-heap.

1. **Min-Heap**: In a min-heap, for any given node \( i \), the value of \( i \) is less than or equal to the values of its children. This means the root node contains the minimum element in the heap.

2. **Max-Heap**: Conversely, in a max-heap, for any given node \( i \), the value of \( i \) is greater than or equal to the values of its children. This means the root node contains the maximum element in the heap.

Heaps are commonly implemented as binary trees, where each node has up to two children. Typically, heaps are implemented using arrays rather than explicit tree structures due to their efficient use of memory.

Heaps are often used in priority queue implementations and heap sort algorithms due to their efficient retrieval of the maximum or minimum element. Insertion and deletion operations in heaps usually take \( O(\log n) \) time complexity, making them very efficient for many applications.
