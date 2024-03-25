# Linked List (Single, Simple)

## Theory

### 1. Algorithms & Data Structures (C++): What are Linked Lists

A linked list is a fundamental data structure in computer science used to store a sequence of elements. In a linked list, each element is stored in a node, and each node contains two parts: the data itself, and a reference (or pointer) to the next node in the sequence. This arrangement allows for dynamic memory allocation, making linked lists a flexible data structure.

In a singly linked list, each node only has a reference to the next node in the sequence, forming a unidirectional chain. Meanwhile, in a doubly linked list, each node has references to both the next and the previous nodes, creating a bidirectional chain.

Advantages:

1. Dynamic Size: Linked lists can easily grow or shrink in size at runtime since memory allocation is not required to be contiguous.
2. Insertions and Deletions: Insertions and deletions at any position in the list can be done efficiently by adjusting pointers, whereas in arrays, these operations may require shifting elements.
3. Memory Efficiency: Linked lists can use memory more efficiently than arrays, especially when the size of the data structure is not known in advance.

Disadvantages:

1. Random Access: Unlike arrays, linked lists do not support constant-time random access to elements. Traversing a linked list requires sequential access from the beginning.
2. Extra Memory: Linked lists require additional memory for storing pointers to the next (and possibly previous) nodes, which can increase memory overhead compared to arrays.
3. Cache Performance: Arrays often have better cache performance since they store elements contiguously in memory, leading to fewer cache misses during traversal.

Overall, linked lists are particularly useful when frequent insertions and deletions are required, or when the size of the data structure needs to be dynamic. They are commonly used as building blocks for more complex data structures such as stacks, queues, and hash tables.

#### Types of Linked List

In C++, linked lists are a fundamental data structure consisting of a sequence of elements, each containing a reference (or pointer) to the next element in the sequence. There are several types of linked lists, each with its own characteristics and use cases. Here are the most common types:

1. **Singly Linked List**:
   * In a singly linked list, each element, or node, contains data and a reference to the next node in the sequence.
   * It has a forward direction only, meaning you can only traverse the list from the head to the tail.
   * Singly linked lists are relatively simple to implement and use less memory compared to other types of linked lists.

2. **Doubly Linked List**:
   * In a doubly linked list, each node contains a reference to both the next and the previous nodes in the sequence.
   * This bidirectional linking allows traversal in both forward and backward directions, which can be useful in certain situations.
   * Doubly linked lists require more memory per node due to the additional pointer to the previous node.

3. **Circular Linked List**:
   * In a circular linked list, the last node points back to the first node, forming a circular structure.
   * This can simplify certain operations, such as traversal or rotation, since there is no "end" to the list.
   * Circular linked lists can be either singly or doubly linked.

4. **Sorted Linked List**:
   * A sorted linked list maintains its elements in sorted order, typically ascending or descending.
   * Insertions in a sorted linked list require maintaining the sorted order, which may involve traversing the list to find the correct position for insertion.
   * Sorted linked lists are useful when you frequently need to insert elements in sorted order and maintain that order without the need for sorting the entire list.

5. **Sparse Linked List**:
   * A sparse linked list is a variation that optimizes storage for lists with many null or default values.
   * Instead of storing every element, it only stores elements that differ from the default value.
   * This can save memory in situations where the majority of elements have default values.

6. **Unrolled Linked List**:
    * Unrolled linked lists store multiple elements in each node, allowing for better cache performance and reduced memory overhead compared to traditional linked lists.
    * Each node in an unrolled linked list contains an array or vector to hold multiple elements along with pointers to the next node.

Each type of linked list has its advantages and disadvantages, and the choice depends on the specific requirements of the application you are working on.

#### Why do we use Linked List

Linked lists are fundamental data structures in computer science and are commonly used for various reasons:

1. **Dynamic Size**: Linked lists can dynamically grow and shrink in size. Unlike arrays, where the size is fixed once allocated, linked lists can easily accommodate changes in size by simply adding or removing nodes.

2. **Memory Allocation**: Linked lists provide flexibility in memory allocation. Each node can be allocated independently in memory, allowing for efficient usage of memory and easy expansion without the need for contiguous memory blocks like arrays.

3. **Insertions and Deletions**: Linked lists excel in insertions and deletions, especially in scenarios where frequent modifications are expected. Adding or removing elements in a linked list typically involves adjusting pointers, which can be done in constant time (O(1)) for insertions and deletions at the beginning or end of the list, and linear time (O(n)) for insertions and deletions at arbitrary positions.

4. **No Pre-allocation**: Linked lists do not require pre-allocation of memory for a fixed number of elements, unlike arrays. This can be advantageous when the number of elements is unknown or varies widely.

5. **Ease of Implementation**: Linked lists are relatively easy to implement and understand compared to some other data structures like trees or graphs. They involve simple pointer manipulation, making them suitable for educational purposes and as building blocks for more complex data structures.

6. **Versatility**: Linked lists come in various forms such as singly linked lists, doubly linked lists, and circular linked lists. Each type offers different trade-offs in terms of memory usage, traversal speed, and ease of manipulation, allowing developers to choose the most appropriate type based on their specific requirements.

However, it's worth noting that linked lists also have some drawbacks, such as inefficient random access (O(n) time complexity) and increased memory overhead due to storing pointers. Therefore, their usage should be carefully considered based on the specific requirements of the problem at hand.

#### Conception of Node

In C++ programming, when dealing with linked lists, a fundamental concept is the notion of a "Node." A Node represents an individual element within the linked list. Each Node contains two primary components:

1. **Data**: This is the actual value or payload that the Node holds. It could be of any data type depending on the requirements of your linked list. For instance, if you're creating a linked list of integers, the data part of the Node would be an integer. If it's a linked list of strings, the data part would be a string, and so on.

2. **Pointer(s)**: These are references or pointers to other Nodes. In a singly linked list, each Node typically contains a single pointer, called the "next" pointer, which points to the next Node in the sequence. In a doubly linked list, each Node contains two pointers: one pointing to the next Node (often called "next"), and one pointing to the previous Node (often called "prev").

Here's a simple example of what a Node might look like in C++:

```cpp
template <typename T>
struct Node {
    T data;           // Data part of the Node
    Node<T>* next;    // Pointer to the next Node
};
```

In this example, `T` is a template parameter representing the data type of the Node's payload. This allows you to create Nodes containing data of any type without having to define multiple versions of the Node structure.

Once you have defined the Node structure, you can create instances of Node to build your linked list. Here's a basic example of how you might create a Node:

```cpp
Node<int>* newNode = new Node<int>(); // Creating a Node with integer data
newNode->data = 10;                    // Assigning a value to the data part
newNode->next = nullptr;               // Initializing the next pointer (typically to nullptr initially)
```

This creates a Node with an integer data part (value 10) and initializes its next pointer to `nullptr`, indicating that it currently doesn't point to any other Node.

### Linked List: Implementation

Here's a basic implementation of a singly linked list in C++:

```cpp
#include <iostream>

using namespace std;

// Node class represents each node in the linked list
class Node {
public:
    int data;
    Node* next;
    Node(int d) : data(d), next(nullptr) {}
};

// LinkedList class represents the linked list
class LinkedList {
private:
    Node* head;
public:
    // Constructor to initialize an empty linked list
    LinkedList() : head(nullptr) {}

    // Constructor to initialize linked list with an array
    LinkedList(int arr[], int n) {
        head = nullptr;
        for (int i = 0; i < n; i++)
            append(arr[i]);
    }

    int length() {
        int length = 0;
        Node* current = head;
        
        // Traverse the list and count nodes
        while (current != nullptr) {
            length++;
            current = current->next;
        }
        return length;
    }

    // Function to add a node to the front of the list
    void push_front(int val) {
        Node* newNode = new Node(val); // Create a new node with the given value
        newNode->next = head; // Set the new node's next pointer to the current head
        head = newNode; // Update the head pointer to point to the new node
    }

    // Function to add a node at the end of the linked list
    void push_back(int data) {
        Node* newNode = new Node(data);
        if (head == nullptr) {
            head = newNode;
            return;
        }
        Node* temp = head;
        while (temp->next != nullptr)
            temp = temp->next;
        temp->next = newNode;
    }

    void pop_front() {
        if (head == nullptr) {
            std::cout << "List is empty. Nothing to delete.\n";
            return;
        }
        Node* temp = head;
        head = head->next;
        delete temp;
    }

        // Function to delete the last node of the linked list
    void pop_back() {
        if (!head) {
            std::cout << "List is empty. Nothing to delete.\n";
            return;
        }
        if (!head->next) {
            delete head;
            head = nullptr;
            return;
        }
        Node* temp = head;
        while (temp->next->next) {
            temp = temp->next;
        }
        delete temp->next;
        temp->next = nullptr;
    }


    // Function to delete a node from any position in the list
    void deleteNode(int position) {
        if (head == nullptr) {
            cout << "List is empty" << endl;
            return;
        }
        Node* temp = head;
        if (position == 0) {
            head = head->next;
            delete temp;
            return;
        }
        for (int i = 0; temp != nullptr && i < position - 1; i++) {
            temp = temp->next;
        }
        if (temp == nullptr || temp->next == nullptr) {
            cout << "Position is out of bounds" << endl;
            return;
        }
        Node* nodeToDelete = temp->next;
        temp->next = nodeToDelete->next;
        delete nodeToDelete;
    }
    // Function to display the linked list
    void display() {
        Node* temp = head;
        while (temp != nullptr) {
            cout << temp->data << "->";
            temp = temp->next;
        }
        cout << endl;
    }

    void clear() {
        while (head != nullptr) {
            Node* temp = head;
            head = head->next;
            delete temp;
        }
    }

    // Method to get the last element of the list
    Node* getLast() {
        if (head) {
            Node* temp = head;
            while (temp->next) {
                temp = temp->next;
            }
            return temp-;
        }
        return head;
    }

    // Method to get the first element of the list
    Node* getFirst() {
        return head;
    }

    // Function to get data at a specific position
    int GetAt(int position) {
        Node* current = head;
        int currentPosition = 0;

        // Traverse the list until either reaching the end or the desired position
        while (current != nullptr && currentPosition < position) {
            current = current->next;
            currentPosition++;
        }

        // If current is nullptr, it means position is out of bounds
        if (current == nullptr) {
            std::cerr << "Error: Position out of bounds\n";
            return -1; // Return a sentinel value to indicate error
        }

        // Otherwise, return the data at the desired position
        return current->data;
    }

        // Function to insert a node after a given position
    void insertAfter(int position, int data) {
        // Create a new node
        Node* newNode = new Node(data);

        // If list is empty, insert at the beginning
        if (head == nullptr) {
            head = newNode;
            return;
        }

        // Traverse the list to find the position
        Node* current = head;
        for (int i = 1; i < position && current != nullptr; ++i) {
            current = current->next;
        }

        // If the position is beyond the end of the list, insert at the end
        if (current == nullptr) {
            std::cerr << "Position out of range. Inserting at the end." << std::endl;
            Node* tail = head;
            while (tail->next != nullptr) {
                tail = tail->next;
            }
            tail->next = newNode;
        } else {
            // Insert the new node after the current position
            newNode->next = current->next;
            current->next = newNode;
        }
    }
};

int main() {
    // Creating a linked list using the constructor with an array
    int arr[] = {1, 2, 3, 4, 5};
    int n = sizeof(arr) / sizeof(arr[0]);
    LinkedList ll(arr, n);

    // Displaying the linked list
    ll.display();

    return 0;
}
```

In this example:

* We have a `Node` class representing each node in the linked list.
* We have a `LinkedList` class representing the linked list itself.
* The `LinkedList` class has two constructors:
  1. A default constructor that initializes an empty linked list.
  2. A constructor that takes an array and its size as parameters to initialize the linked list with the elements of the array.
* The `push_back` function is used to add elements to the end of the linked list.
* The `push_front` function is used to add elements to the begining of the linked list.
* The `display` function is used to print the elements of the linked list.

### Complexity analysis

1. **Access/Search (by index or value):**
   * Time Complexity: O(n)
   * Explanation: In a singly linked list, accessing or searching for an element typically requires traversing the list from the head (or possibly the tail) until the desired element is found. Since there is no direct access to elements by index, you may need to iterate through all or part of the list.

2. **Insertion (at the beginning):**
   * Time Complexity: O(1)
   * Explanation: Inserting a node at the beginning of a singly linked list involves updating the head pointer to point to the new node. This operation can be done in constant time regardless of the size of the list.

3. **Insertion (at the end, if tail pointer is available):**
   * Time Complexity: O(1)
   * Explanation: If the linked list maintains a tail pointer, inserting a node at the end involves updating the tail pointer to point to the new node, which can be done in constant time.

4. **Insertion (at the end, without tail pointer):**
   * Time Complexity: O(n)
   * Explanation: Without a tail pointer, inserting a node at the end requires traversing the entire list to find the last node, then updating its next pointer to point to the new node.

5. **Insertion (in the middle):**
   * Time Complexity: O(n)
   * Explanation: Inserting a node in the middle of a singly linked list requires traversing the list to find the node at the desired position. This operation may involve traversing approximately half of the list on average.

6. **Deletion (from the beginning):**
   * Time Complexity: O(1)
   * Explanation: Deleting the first node of a singly linked list involves updating the head pointer to point to the second node, which can be done in constant time.

7. **Deletion (from the end, if tail pointer is available):**
   * Time Complexity: O(n)
   * Explanation: Without a tail pointer, deleting the last node of a singly linked list requires traversing the entire list to find the second-to-last node, then updating its next pointer to nullptr. If a tail pointer is available, this operation can be done in constant time.

8. **Deletion (from the end, without tail pointer):**
   * Time Complexity: O(n)
   * Explanation: Deleting the last node of a singly linked list without a tail pointer involves traversing the entire list to find the last node and the second-to-last node, then updating the second-to-last node's next pointer to nullptr.

9. **Deletion (from the middle):**
   * Time Complexity: O(n)
   * Explanation: Deleting a node from the middle of a singly linked list requires traversing the list to find the node to be deleted and its predecessor node. This operation may involve traversing approximately half of the list on average.

10. **Traversal (length):**

* Time Complexity: O(n)
* Explanation: To traverse the entire linked list, you need to visit each node once, resulting in a time complexity of O(n).

1. **Concatenation (Joining two lists):**

* Time Complexity: O(1)
* Explanation: Concatenating two linked lists involves updating the next pointer of the last node of the first list to point to the head of the second list. This operation has a constant time complexity.

1. **Reversal:**

* Time Complexity: O(n)
* Explanation: Reversing a linked list requires iterating through the list once and updating the pointers of each node to reverse the direction. This operation has a time complexity of O(n).

These complexities describe the upper bounds on the performance of the corresponding operations. Depending on the specific implementation and optimizations, actual performance may vary.

### Linked List in the Memory

In C++, a linked list is a data structure consisting of a sequence of elements, each of which points to the next element in the sequence. Unlike arrays, linked lists do not have a predetermined fixed size, and elements can be easily inserted or removed without reallocation or reorganization of the entire structure.

In memory, a linked list is typically represented as a series of nodes. Each node contains two components: the data, which holds the value of the element, and a pointer/reference to the next node in the sequence.

Here's a simple example of a singly linked list node in C++:

```cpp
template <typename T>
struct Node {
    T data;
    Node* next;

    // Constructor
    Node(const T& data) : data(data), next(nullptr) {}
};
```

In this example:

* `data`: holds the value of the element.
* `next`: a pointer to the next node in the sequence.

To form a linked list, you would create instances of these nodes and link them together. The last node's `next` pointer would typically be set to `nullptr` to indicate the end of the list.

Here's an example of how you might construct a linked list:

```cpp
Node<int>* head = new Node<int>(10); // Create the first node
head->next = new Node<int>(20);       // Create the second node and link it
head->next->next = new Node<int>(30); // Create the third node and link it
// Continue adding nodes as needed...
```

In memory, this would look like:

```bash
Node 1: [data: 10][next: ] --> Node 2: [data: 20][next: ] --> Node 3: [data: 30][next: nullptr]
```

Each node is allocated memory dynamically (using `new` in C++), and they are linked together via the `next` pointers.

Remember, when using linked lists, it's important to properly manage memory allocation and deallocation to prevent memory leaks. When done using the list, make sure to deallocate the memory for each node to avoid memory leaks.

### 1. Algorithms & Data Structures (C++): Linked List: Why Linked Lists?

Linked lists are a fundamental data structure in computer science and are used for various reasons. Here are some key advantages of using linked lists:

1. **Dynamic Memory Allocation**: Unlike arrays, linked lists do not require a fixed amount of memory allocation at the outset. They can grow or shrink dynamically as needed, which makes them more flexible for managing memory efficiently.

2. **Insertions and Deletions**: Linked lists excel at insertions and deletions, especially when compared to arrays. In arrays, inserting or deleting an element requires shifting all subsequent elements, which can be time-consuming, especially for large arrays. In linked lists, insertions and deletions can be done in constant time \( O(1) \), assuming you have a reference to the node where the operation needs to occur.

3. **No Contiguous Memory Requirement**: Linked lists do not require contiguous memory allocation like arrays. This means that memory fragmentation is less of an issue with linked lists, and it's easier to allocate memory for them, especially in environments where contiguous blocks of memory may be scarce.

4. **Dynamic Data Structures**: Linked lists can easily handle data structures of varying sizes and shapes. For example, you can create a singly linked list, a doubly linked list, or even a circular linked list depending on your requirements.

5. **Efficient for Sequential Access**: While arrays offer \( O(1) \) time complexity for accessing elements by index, linked lists are more efficient for sequential access. Traversing a linked list from start to end or end to start is straightforward and typically done in linear time \( O(n) \).

6. **Ease of Implementation**: Linked lists are relatively simple to implement compared to some other data structures like trees or graphs. This simplicity makes them an excellent choice for learning purposes or for situations where a simpler solution is sufficient.

Despite these advantages, linked lists also have some drawbacks. They have higher memory overhead compared to arrays due to the additional memory required for storing pointers/references. Additionally, random access to elements (i.e., accessing elements by index) is less efficient in linked lists compared to arrays. However, the benefits they offer in terms of flexibility and efficiency for certain operations make them a valuable tool in a programmer's toolkit.

### 1. Algorithms & Data Structures (C++): Linked Lists vs Arrays

Linked lists and arrays are two fundamental data structures in computer science, each with its own strengths and weaknesses. Let's compare them in terms of various aspects:

1. **Memory Allocation:**
   * **Arrays:** Contiguous block of memory is allocated for elements, ensuring efficient access but may lead to memory fragmentation.
   * **Linked Lists:** Elements are scattered in memory, connected via pointers, which can lead to less efficient memory access but avoids fragmentation and allows dynamic memory allocation.

2. **Insertion and Deletion:**
   * **Arrays:** Insertion and deletion can be costly, especially in the middle, as elements may need to be shifted.
   * **Linked Lists:** Insertion and deletion are generally faster, especially for singly linked lists when inserting/deleting at the beginning or end. However, accessing arbitrary elements requires traversal from the head, which can be slower.

3. **Access Time:**
   * **Arrays:** Constant-time access to elements given the index (O(1)).
   * **Linked Lists:** Access time is O(n) as it requires traversing from the head (for singly linked lists) or both directions (for doubly linked lists) to find the desired element.

4. **Memory Overhead:**
   * **Arrays:** Fixed memory overhead for storing the elements and possibly some additional memory for bookkeeping.
   * **Linked Lists:** Additional memory overhead for storing pointers/references to the next (and possibly previous) nodes.

5. **Dynamic Size:**
   * **Arrays:** Often have a fixed size, though dynamic arrays (like `std::vector` in C++) can resize dynamically.
   * **Linked Lists:** Can dynamically grow or shrink without the need for resizing.

6. **Cache Performance:**
   * **Arrays:** Better cache performance due to contiguous memory access, leading to fewer cache misses.
   * **Linked Lists:** Poor cache performance due to scattered memory access, leading to more cache misses.

7. **Implementation Complexity:**
   * **Arrays:** Generally simpler to implement and understand.
   * **Linked Lists:** More complex due to the need to manage pointers and dynamic memory allocation.

Choose arrays when:

* You need fast random access.
* Memory is a concern and the size of the data is known in advance.
* You are dealing with small or fixed-size collections.

Choose linked lists when:

* You frequently insert or delete elements, especially at the beginning or end of the list.
* Memory usage is dynamic and unpredictable.
* You can tolerate slower access times for fast insertion and deletion.

In C++, the standard library provides both array-like (`std::array`, `std::vector`) and linked list-like (`std::list`) containers, allowing you to choose based on your specific requirements.

### 1. Algorithms & Data Structures (C++): Linked Lists: Linked Lists with Iterators

Certainly! Implementing a linked list with iterators in C++ can be quite useful for efficient traversal and manipulation of the list elements. Here's an example implementation:

```cpp
#include <iostream>

// Node class representing each element in the linked list
template <typename T>
class Node {
public:
    T data;
    Node* next;

    Node(const T& newData) : data(newData), next(nullptr) {}
};

// Iterator class to traverse the linked list
template <typename T>
class LinkedListIterator {
    Node<T>* current;

public:
    LinkedListIterator(Node<T>* node) : current(node) {}

    T& operator*() const {
        return current->data;
    }

    LinkedListIterator<T>& operator++() {
        current = current->next;
        return *this;
    }

    LinkedListIterator<T> operator++(int) {
        LinkedListIterator<T> old = *this;
        ++(*this);
        return old;
    }

    bool operator==(const LinkedListIterator<T>& other) const {
        return current == other.current;
    }

    bool operator!=(const LinkedListIterator<T>& other) const {
        return !(*this == other);
    }
};

// Linked list class
template <typename T>
class LinkedList {
private:
    Node<T>* head;

public:
    LinkedList() : head(nullptr) {}

    ~LinkedList() {
        while (head) {
            Node<T>* temp = head;
            head = head->next;
            delete temp;
        }
    }

    // Function to insert a new element at the beginning of the list
    void insert(const T& data) {
        Node<T>* newNode = new Node<T>(data);
        newNode->next = head;
        head = newNode;
    }

    // Function to return an iterator pointing to the first element of the list
    LinkedListIterator<T> begin() const {
        return LinkedListIterator<T>(head);
    }

    // Function to return an iterator pointing to the end of the list
    LinkedListIterator<T> end() const {
        return LinkedListIterator<T>(nullptr);
    }
};

int main() {
    LinkedList<int> myList;
    myList.insert(10);
    myList.insert(20);
    myList.insert(30);

    // Iterating through the list using iterators
    for (LinkedListIterator<int> it = myList.begin(); it != myList.end(); ++it) {
        std::cout << *it << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this code:

* The `Node` class represents each element in the linked list. It contains data and a pointer to the next node.
* The `LinkedListIterator` class provides the iterator interface for traversing the linked list.
* The `LinkedList` class manages the linked list and provides functions like `insert`, `begin`, and `end`.
* In the `main` function, we demonstrate the usage of the linked list by inserting elements and iterating through them using iterators.

### 1. Algorithms & Data Structures (C++): Linked list question: Odd Even linked list

Sure! The "Odd Even Linked List" problem involves reorganizing a linked list so that all the odd-indexed nodes come before the even-indexed nodes. Here's how you can implement this in C++:

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
    ListNode* oddEvenList(ListNode* head) {
        if (head == nullptr || head->next == nullptr) {
            return head; // No need to modify the list if it's empty or has only one node
        }
        
        ListNode *odd = head;
        ListNode *even = head->next;
        ListNode *evenHead = even; // Save the head of even list
        
        while (even != nullptr && even->next != nullptr) {
            odd->next = even->next; // Link odd nodes
            odd = odd->next; // Move odd pointer
            
            even->next = odd->next; // Link even nodes
            even = even->next; // Move even pointer
        }
        
        odd->next = evenHead; // Connect the end of odd list to the head of even list
        
        return head;
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
    ListNode* head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);

    Solution sol;
    cout << "Original List: ";
    printList(head);

    ListNode* newHead = sol.oddEvenList(head);

    cout << "List after rearranging odd and even nodes: ";
    printList(newHead);

    return 0;
}
```

This code defines a `ListNode` structure representing a node in a singly-linked list. The `Solution` class contains the `oddEvenList` function, which rearranges the list as required. The `main` function demonstrates its usage by creating a sample linked list and calling the `oddEvenList` function on it.

### 1. Algorithms & Data Structures (C++): Linked list question: Remove Nth node from end of list

To remove the nth node from the end of a linked list in C++, you can use a two-pointer approach. Here's a step-by-step solution:

1. Use two pointers, `first` and `second`, both initially pointing to the head of the list.
2. Move the `second` pointer to the nth node from the beginning of the list.
3. Move both pointers (`first` and `second`) simultaneously until the `second` pointer reaches the end of the list.
4. The `first` pointer will now be pointing to the nth node from the end.
5. Remove the nth node by adjusting the `next` pointer of the node before it.

Here's the C++ code to implement the above logic:

```cpp
#include <iostream>

struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

ListNode* removeNthFromEnd(ListNode* head, int n) {
    ListNode *dummy = new ListNode(0);
    dummy->next = head;
    ListNode *first = dummy;
    ListNode *second = dummy;

    // Move the second pointer to the nth node from the beginning
    for (int i = 0; i <= n; ++i) {
        if (second == nullptr)
            return nullptr; // Error: n is greater than the number of nodes
        second = second->next;
    }

    // Move both pointers simultaneously until second reaches the end
    while (second != nullptr) {
        first = first->next;
        second = second->next;
    }

    // Remove the nth node by adjusting the next pointer of the node before it
    first->next = first->next->next;

    ListNode *result = dummy->next;
    delete dummy;
    return result;
}

// Utility function to print the linked list
void printList(ListNode* head) {
    while (head != nullptr) {
        std::cout << head->val << " ";
        head = head->next;
    }
    std::cout << std::endl;
}

int main() {
    // Example usage
    ListNode *head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);

    std::cout << "Original List: ";
    printList(head);

    int n = 2; // Remove the 2nd node from the end
    head = removeNthFromEnd(head, n);

    std::cout << "List after removing " << n << " node from the end: ";
    printList(head);

    return 0;
}
```

This code should correctly remove the nth node from the end of the linked list and handle edge cases like when the value of n exceeds the number of nodes in the list.

### 1. Algorithms & Data Structures (C++): Linked List Remove Duplicates

Certainly! Below is a C++ implementation of removing duplicates from a singly linked list:

```cpp
#include <iostream>
#include <unordered_set>

using namespace std;

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

void removeDuplicates(ListNode *head) {
    if (head == nullptr)
        return;

    unordered_set<int> seen;
    ListNode *curr = head;
    ListNode *prev = nullptr;

    while (curr != nullptr) {
        if (seen.find(curr->val) != seen.end()) {
            // Duplicate found, remove the node
            prev->next = curr->next;
            delete curr;
            curr = prev->next;
        } else {
            // No duplicate, add to set and move to next node
            seen.insert(curr->val);
            prev = curr;
            curr = curr->next;
        }
    }
}

// Utility function to print the linked list
void printList(ListNode *head) {
    ListNode *temp = head;
    while (temp != nullptr) {
        cout << temp->val << " ";
        temp = temp->next;
    }
    cout << endl;
}

// Test the implementation
int main() {
    // Create a linked list: 1->2->3->3->4->4->5
    ListNode *head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(3);
    head->next->next->next->next = new ListNode(4);
    head->next->next->next->next->next = new ListNode(4);
    head->next->next->next->next->next->next = new ListNode(5);

    cout << "Original List: ";
    printList(head);

    removeDuplicates(head);

    cout << "List after removing duplicates: ";
    printList(head);

    // Free the memory
    while (head != nullptr) {
        ListNode *temp = head;
        head = head->next;
        delete temp;
    }

    return 0;
}
```

This code defines a `ListNode` structure for the linked list, provides a function `removeDuplicates()` to remove duplicates from the list, and a `printList()` function to print the list. The `main()` function creates a linked list with duplicates, removes duplicates, and prints the modified list.

### 1. Algorithms & Data Structures (C++): Linked List: Concept of Short Circuiting

In the context of algorithms and data structures, particularly when dealing with linked lists in C++, the concept of short-circuiting doesn't directly apply as it does in languages like C or in boolean expressions. However, we can discuss a similar concept that is relevant when traversing or manipulating linked lists: early termination.

In C and languages with boolean expressions, short-circuiting refers to the behavior where an expression stops evaluating as soon as the outcome is determined. For example, in the expression `A && B`, if `A` evaluates to false, there's no need to evaluate `B` because the result will always be false. Similarly, in `A || B`, if `A` evaluates to true, there's no need to evaluate `B`.

In the context of linked lists, early termination can be thought of as a similar optimization concept. For example, consider a function that searches for a specific value in a linked list:

```cpp
bool search(Node* head, int target) {
    Node* current = head;
    while (current != nullptr) {
        if (current->data == target) {
            return true; // Early termination if target is found
        }
        current = current->next;
    }
    return false; // Target not found in the list
}
```

In this function, as soon as the target value is found (`current->data == target` evaluates to true), the loop terminates early and the function returns true. This is analogous to short-circuiting because further iterations are unnecessary once the condition is met.

Similarly, in other operations such as deletion or insertion, you might encounter scenarios where you can stop traversing the list once a certain condition is met, avoiding unnecessary iterations and improving efficiency.

While the terminology might not directly match, the concept of early termination in linked list operations serves a similar purpose to short-circuiting in boolean expressions—it optimizes the execution by avoiding unnecessary computations.

### 1. Algorithms & Data Structures (C++): Linked List: Find Kth Node From End

To find the Kth node from the end of a linked list in C++, you can use a two-pointer approach. Here's a simple implementation:

```cpp
#include <iostream>

using namespace std;

// Define the structure of a node
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

// Function to find the Kth node from the end of a linked list
ListNode* findKthFromEnd(ListNode* head, int k) {
    if (head == nullptr || k <= 0) // If head is null or k is invalid, return nullptr
        return nullptr;

    ListNode *slow = head; // Slow pointer initially points to the head
    ListNode *fast = head; // Fast pointer initially points to the head

    // Move fast pointer ahead by k steps
    for (int i = 0; i < k; ++i) {
        if (fast == nullptr) // If k is greater than the length of the list, return nullptr
            return nullptr;
        fast = fast->next;
    }

    // Move both pointers until fast reaches the end
    while (fast != nullptr) {
        slow = slow->next;
        fast = fast->next;
    }

    return slow; // Slow pointer now points to the Kth node from the end
}

// Function to print the linked list
void printList(ListNode* head) {
    while (head != nullptr) {
        cout << head->val << " ";
        head = head->next;
    }
    cout << endl;
}

// Function to delete the linked list to avoid memory leaks
void deleteList(ListNode* head) {
    while (head != nullptr) {
        ListNode* temp = head;
        head = head->next;
        delete temp;
    }
}

int main() {
    // Create a sample linked list: 1 -> 2 -> 3 -> 4 -> 5
    ListNode* head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);

    int k = 2; // Find the second node from the end
    ListNode* result = findKthFromEnd(head, k);
    if (result != nullptr)
        cout << "The " << k << "th node from the end is: " << result->val << endl;
    else
        cout << "Invalid k value or list is empty." << endl;

    // Clean up memory by deleting the linked list
    deleteList(head);

    return 0;
}
```

This code defines a `ListNode` structure and provides a function `findKthFromEnd()` to find the Kth node from the end of a linked list. The main function demonstrates its usage with a sample linked list.

### 1. Algorithms & Data Structures (C++): Linked List: Kth Last Element

To find the Kth last element in a singly linked list, you can use a two-pointer approach. One pointer will be ahead of the other by K nodes. When the first pointer reaches the end of the list, the second pointer will be pointing to the Kth last element. Here's a C++ implementation for this:

```cpp
#include <iostream>

using namespace std;

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* kthLastElement(ListNode* head, int k) {
    if (!head || k <= 0) return nullptr;

    ListNode *slow = head, *fast = head;

    // Move the fast pointer K nodes ahead
    for (int i = 0; i < k; ++i) {
        if (fast == nullptr) return nullptr; // List has fewer than k nodes
        fast = fast->next;
    }

    // Move both pointers until the fast pointer reaches the end
    while (fast != nullptr) {
        slow = slow->next;
        fast = fast->next;
    }

    // Now, slow points to the Kth last node
    return slow;
}

// Helper function to create a linked list
ListNode* createLinkedList(vector<int>& elements) {
    ListNode* head = nullptr;
    ListNode* prev = nullptr;
    for (int val : elements) {
        ListNode* newNode = new ListNode(val);
        if (!head) {
            head = newNode;
        } else {
            prev->next = newNode;
        }
        prev = newNode;
    }
    return head;
}

// Helper function to delete the linked list to prevent memory leaks
void deleteLinkedList(ListNode* head) {
    while (head) {
        ListNode* temp = head;
        head = head->next;
        delete temp;
    }
}

// Helper function to print the linked list
void printLinkedList(ListNode* head) {
    while (head) {
        cout << head->val << " -> ";
        head = head->next;
    }
    cout << "NULL" << endl;
}

int main() {
    vector<int> elements = {1, 2, 3, 4, 5, 6, 7, 8, 9};
    ListNode* head = createLinkedList(elements);
    cout << "Original linked list: ";
    printLinkedList(head);

    int k = 3; // Find the 3rd last element
    ListNode* kthLast = kthLastElement(head, k);
    if (kthLast)
        cout << "The " << k << "th last element is: " << kthLast->val << endl;
    else
        cout << "List has fewer than " << k << " elements" << endl;

    // Clean up memory
    deleteLinkedList(head);

    return 0;
}
```

This code defines a `ListNode` struct representing a node in the linked list and provides functions to create, delete, and print a linked list. The `kthLastElement` function finds the Kth last element using the two-pointer technique, and the `main` function demonstrates its usage.

### 1. Algorithms & Data Structures (C++): Linked List: Partition List

Partitioning a linked list around a given value involves rearranging the elements in such a way that all nodes with values less than the given value appear before all nodes with values greater than or equal to the given value. One way to accomplish this is by creating two separate linked lists: one for nodes with values less than the given value and another for nodes with values greater than or equal to the given value. Then, you can merge these two lists to form the final partitioned list.

Here's a C++ implementation of the partition function for a singly linked list:

```cpp
#include <iostream>

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* partition(ListNode* head, int x) {
    ListNode less_head(0); // Dummy node for the list of nodes with values less than x
    ListNode greater_head(0); // Dummy node for the list of nodes with values greater than or equal to x
    ListNode *less_ptr = &less_head; // Pointer to the end of the list of nodes with values less than x
    ListNode *greater_ptr = &greater_head; // Pointer to the end of the list of nodes with values greater than or equal to x
    
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
    
    // Connect the two partitions
    less_ptr->next = greater_head.next;
    greater_ptr->next = nullptr; // Terminate the end of the list of nodes with values greater than or equal to x
    
    return less_head.next; // Return the head of the partitioned list
}

// Utility function to print a linked list
void printList(ListNode* head) {
    while (head != nullptr) {
        std::cout << head->val << " ";
        head = head->next;
    }
    std::cout << std::endl;
}

int main() {
    // Example usage
    ListNode *head = new ListNode(1);
    head->next = new ListNode(4);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(2);
    head->next->next->next->next = new ListNode(5);
    head->next->next->next->next->next = new ListNode(2);

    std::cout << "Original list: ";
    printList(head);

    int x = 3;
    ListNode *partitioned = partition(head, x);

    std::cout << "Partitioned list (around " << x << "): ";
    printList(partitioned);

    return 0;
}
```

In this implementation, we maintain two pointers `less_ptr` and `greater_ptr` to keep track of the end of the partitions with values less than `x` and values greater than or equal to `x`, respectively. We traverse the original list, appending nodes to the appropriate partition. Finally, we connect the two partitions and return the head of the list with nodes less than `x`.

### 1. Algorithms & Data Structures (C++): Linked List: Rearranging Only Even Numbers

To rearrange only even numbers in a linked list, you'll need to traverse the list, extract the even numbers, and then rearrange them accordingly while maintaining their relative order. Here's a sample implementation in C++:

```cpp
#include <iostream>

using namespace std;

// Node structure for the linked list
struct Node {
    int data;
    Node* next;
    
    Node(int val) : data(val), next(nullptr) {}
};

// Function to insert a node at the end of the linked list
void insert(Node*& head, int data) {
    Node* newNode = new Node(data);
    if (head == nullptr) {
        head = newNode;
    } else {
        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = newNode;
    }
}

// Function to rearrange even numbers in the linked list
Node* rearrangeEvenNumbers(Node* head) {
    if (head == nullptr || head->next == nullptr) {
        return head; // No need to rearrange if list is empty or has only one node
    }

    Node* evenHead = nullptr;
    Node* evenTail = nullptr;
    Node* oddHead = nullptr;
    Node* oddTail = nullptr;

    Node* current = head;

    while (current != nullptr) {
        if (current->data % 2 == 0) {
            // Even number
            if (evenHead == nullptr) {
                evenHead = evenTail = current;
            } else {
                evenTail->next = current;
                evenTail = current;
            }
        } else {
            // Odd number
            if (oddHead == nullptr) {
                oddHead = oddTail = current;
            } else {
                oddTail->next = current;
                oddTail = current;
            }
        }
        current = current->next;
    }

    // Joining odd and even lists
    if (oddHead == nullptr) {
        return evenHead;
    } else {
        oddTail->next = evenHead;
        if (evenTail != nullptr) {
            evenTail->next = nullptr;
        }
        return oddHead;
    }
}

// Function to print the linked list
void printList(Node* head) {
    while (head != nullptr) {
        cout << head->data << " ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    Node* head = nullptr;

    // Inserting elements into the linked list
    insert(head, 1);
    insert(head, 2);
    insert(head, 3);
    insert(head, 4);
    insert(head, 5);
    insert(head, 6);

    cout << "Original list: ";
    printList(head);

    // Rearranging even numbers
    head = rearrangeEvenNumbers(head);

    cout << "Rearranged list: ";
    printList(head);

    return 0;
}
```

This code will rearrange the even numbers in the linked list while maintaining their relative order.

### 1. Algorithms & Data Structures (C++): Linked List: Remove Duplicates

Sure, I can help you with that! Below is a C++ implementation of removing duplicates from a singly linked list:

```cpp
#include <iostream>
#include <unordered_set>

using namespace std;

// Node definition for the linked list
struct Node {
    int data;
    Node* next;
    Node(int value) : data(value), next(nullptr) {}
};

// Function to remove duplicates from a singly linked list
void removeDuplicates(Node* head) {
    if (head == nullptr)
        return;

    unordered_set<int> seen;
    Node* current = head;
    Node* prev = nullptr;

    while (current != nullptr) {
        if (seen.find(current->data) != seen.end()) {
            prev->next = current->next;
            delete current;
            current = prev->next;
        } else {
            seen.insert(current->data);
            prev = current;
            current = current->next;
        }
    }
}

// Function to print the linked list
void printList(Node* head) {
    Node* temp = head;
    while (temp != nullptr) {
        cout << temp->data << " ";
        temp = temp->next;
    }
    cout << endl;
}

// Function to delete the linked list
void deleteList(Node*& head) {
    Node* current = head;
    while (current != nullptr) {
        Node* next = current->next;
        delete current;
        current = next;
    }
    head = nullptr;
}

// Main function to test the code
int main() {
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->next = new Node(3);
    head->next->next->next = new Node(2);
    head->next->next->next->next = new Node(4);
    head->next->next->next->next->next = new Node(1);

    cout << "Original List: ";
    printList(head);

    removeDuplicates(head);

    cout << "List after removing duplicates: ";
    printList(head);

    deleteList(head);

    return 0;
}
```

This code defines a simple linked list with a function `removeDuplicates()` to remove duplicates. The function uses a hash set to keep track of unique elements while traversing the list. If it encounters a duplicate, it removes the duplicate node from the list. Finally, there are utility functions to print and delete the list for testing purposes.

### 1. Algorithms & Data Structures (C++): Linked List: Remove nth Node from end of list

To remove the nth node from the end of a linked list in C++, you can use a two-pointer approach. Here's the algorithm:

1. Use two pointers, `fast` and `slow`, both initially pointing to the head of the list.
2. Move the `fast` pointer forward by `n` steps.
3. Move both `fast` and `slow` pointers simultaneously until `fast` reaches the end of the list.
4. At this point, `slow` will be pointing to the node just before the node to be deleted.
5. Adjust the pointers to remove the nth node from the end.

Here's the C++ implementation:

```cpp
#include <iostream>

struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* removeNthFromEnd(ListNode* head, int n) {
    ListNode* dummy = new ListNode(0);
    dummy->next = head;
    ListNode* fast = dummy;
    ListNode* slow = dummy;

    // Move fast pointer n steps ahead
    for (int i = 0; i <= n; ++i) {
        if (fast == nullptr) return nullptr; // List length < n
        fast = fast->next;
    }

    // Move fast to the end, maintaining the gap of n between fast and slow
    while (fast != nullptr) {
        fast = fast->next;
        slow = slow->next;
    }

    // Remove the nth node from the end
    ListNode* toDelete = slow->next;
    slow->next = slow->next->next;
    delete toDelete;

    return dummy->next;
}

// Utility function to print the linked list
void printList(ListNode* head) {
    ListNode* curr = head;
    while (curr != nullptr) {
        std::cout << curr->val << " ";
        curr = curr->next;
    }
    std::cout << std::endl;
}

int main() {
    // Create a sample linked list: 1->2->3->4->5
    ListNode* head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);

    std::cout << "Original list: ";
    printList(head);

    int n = 2; // Remove the 2nd node from the end
    head = removeNthFromEnd(head, n);

    std::cout << "List after removing " << n << "th node from end: ";
    printList(head);

    // Cleanup
    ListNode* curr = head;
    while (curr != nullptr) {
        ListNode* next = curr->next;
        delete curr;
        curr = next;
    }

    return 0;
}
```

This code demonstrates the removal of the nth node from the end of a linked list and includes a simple test case.

### 1. Algorithms & Data Structures (C++): Add two linked lists

To add two linked lists in C++, you'll need to traverse both lists simultaneously, adding corresponding elements and keeping track of any carry generated during the addition. Here's a basic implementation:

```cpp
#include <iostream>

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
    ListNode* dummyHead = new ListNode(0);
    ListNode* p = l1;
    ListNode* q = l2;
    ListNode* curr = dummyHead;
    int carry = 0;

    while (p != nullptr || q != nullptr) {
        int x = (p != nullptr) ? p->val : 0;
        int y = (q != nullptr) ? q->val : 0;
        int sum = x + y + carry;
        carry = sum / 10;
        curr->next = new ListNode(sum % 10);
        curr = curr->next;
        if (p != nullptr) p = p->next;
        if (q != nullptr) q = q->next;
    }

    if (carry > 0) {
        curr->next = new ListNode(carry);
    }

    return dummyHead->next;
}

// Function to print a linked list
void printList(ListNode* head) {
    ListNode* temp = head;
    while (temp != nullptr) {
        std::cout << temp->val << " ";
        temp = temp->next;
    }
    std::cout << std::endl;
}

// Function to delete a linked list to avoid memory leaks
void deleteList(ListNode* head) {
    ListNode* temp;
    while (head) {
        temp = head;
        head = head->next;
        delete temp;
    }
}

int main() {
    // Example usage
    ListNode* l1 = new ListNode(2);
    l1->next = new ListNode(4);
    l1->next->next = new ListNode(3);

    ListNode* l2 = new ListNode(5);
    l2->next = new ListNode(6);
    l2->next->next = new ListNode(4);

    std::cout << "List 1: ";
    printList(l1);
    std::cout << "List 2: ";
    printList(l2);

    ListNode* sum = addTwoNumbers(l1, l2);
    std::cout << "Sum: ";
    printList(sum);

    // Clean up memory
    deleteList(l1);
    deleteList(l2);
    deleteList(sum);

    return 0;
}
```

This program defines a simple linked list structure, a function to add two numbers represented as linked lists, and functions to print and delete a linked list. In the main function, two example linked lists are created, their sum is calculated using the `addTwoNumbers` function, and then the memory is cleaned up to avoid memory leaks.

### 1. Algorithms & Data Structures (C++): Add two linked lists: Complexity analysis

1. **Time Complexity**:
   * The algorithm iterates through both linked lists once, which gives it a time complexity of O(max(m, n)), where m and n are the lengths of the two linked lists.
   * Each iteration involves constant time operations (additions, comparisons, assignments).
   * Constructing the result linked list also takes linear time.

2. **Space Complexity**:
   * The algorithm utilizes a constant amount of extra space besides the input and output, regardless of the size of the inputs. So, the space complexity is O(1).

Overall, the algorithm is efficient in terms of both time and space complexities.

### 1. Algorithms & Data Structures (C++): Add Two Numbers - Linked List

Sure! Adding two numbers represented by linked lists is a common problem in programming interviews. Here's how you can solve it in C++:

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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* dummy = new ListNode(0);
        ListNode* current = dummy;
        int carry = 0;

        while (l1 != nullptr || l2 != nullptr) {
            int x = (l1 != nullptr) ? l1->val : 0;
            int y = (l2 != nullptr) ? l2->val : 0;
            int sum = x + y + carry;
            carry = sum / 10;
            current->next = new ListNode(sum % 10);
            current = current->next;
            if (l1 != nullptr) l1 = l1->next;
            if (l2 != nullptr) l2 = l2->next;
        }

        if (carry > 0) {
            current->next = new ListNode(carry);
        }

        return dummy->next;
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
    ListNode* l1 = new ListNode(2);
    l1->next = new ListNode(4);
    l1->next->next = new ListNode(3);

    ListNode* l2 = new ListNode(5);
    l2->next = new ListNode(6);
    l2->next->next = new ListNode(4);

    Solution solution;
    ListNode* result = solution.addTwoNumbers(l1, l2);

    cout << "Sum of the two numbers: ";
    printList(result);

    // Free memory
    delete l1;
    delete l2;
    while (result != nullptr) {
        ListNode* temp = result;
        result = result->next;
        delete temp;
    }

    return 0;
}
```

This code defines a `ListNode` struct to represent nodes in the linked list and a `Solution` class with a method `addTwoNumbers` that takes two linked lists representing non-negative integers and returns their sum as a linked list. The main function demonstrates how to use this method with an example.

Let me know if you need further clarification or assistance with anything!

### 1. Algorithms & Data Structures (C++): Comparison of Linked List

Certainly! When comparing linked lists, several factors come into play, such as memory usage, insertion and deletion efficiency, and access time complexity. Let's compare the most common types: singly linked list, doubly linked list, and circular linked list.

1. **Singly Linked List**:
   * **Memory Usage**: Each node in a singly linked list contains a data field and a pointer to the next node. Hence, it consumes less memory compared to doubly linked lists.
   * **Insertion and Deletion Efficiency**: Insertion and deletion at the beginning take O(1) time complexity as they involve only changing pointers. However, insertion and deletion at arbitrary positions require traversal, taking O(n) time complexity.
   * **Access Time Complexity**: Accessing an element by index takes O(n) time since you must traverse from the head to the desired index.

2. **Doubly Linked List**:
   * **Memory Usage**: Each node in a doubly linked list contains a data field and two pointers (to the next and previous nodes). Hence, it consumes more memory compared to singly linked lists.
   * **Insertion and Deletion Efficiency**: Insertion and deletion at the beginning and end take O(1) time complexity as they involve only changing pointers. Insertion and deletion at arbitrary positions still require traversal but involve fewer pointer adjustments than in singly linked lists, hence taking O(n/2) or O(n) time complexity in the worst case.
   * **Access Time Complexity**: Accessing an element by index still takes O(n) time since you might need to traverse from either the head or the tail to the desired index.

3. **Circular Linked List**:
   * **Memory Usage**: Similar to singly linked lists, it consumes memory comparable to them.
   * **Insertion and Deletion Efficiency**: Similar to singly linked lists, insertion and deletion at the beginning take O(1) time complexity. However, deletion of the last element requires traversal to update the pointer of the second-last element, which takes O(n) time. Insertion and deletion at arbitrary positions also require traversal, hence O(n) time complexity.
   * **Access Time Complexity**: Similar to singly linked lists, accessing an element by index takes O(n) time complexity.

In summary, choosing the appropriate linked list type depends on the specific requirements of your application. If memory efficiency is crucial and frequent insertion/deletion at the beginning is required, a singly linked list might be suitable. If bidirectional traversal or insertion/deletion at both ends is common, a doubly linked list would be better. Circular linked lists are useful when you need continuous access to elements without worrying about the end of the list.

### 1. Algorithms & Data Structures (C++): Concatenating 2 Linked Lists

To concatenate two linked lists in C++, you essentially need to attach the second list to the end of the first list. Here's a basic implementation assuming you have a linked list structure defined:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* next;
    
    Node(int value) : data(value), next(nullptr) {}
};

class LinkedList {
private:
    Node* head;

public:
    LinkedList() : head(nullptr) {}

    // Function to insert a node at the end of the linked list
    void insert(int value) {
        Node* newNode = new Node(value);
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

    // Function to concatenate another linked list at the end of this list
    void concatenate(LinkedList& otherList) {
        if (!otherList.head) return; // If the other list is empty, nothing to concatenate
        
        if (!head) {
            head = otherList.head;
            return;
        }
        
        Node* temp = head;
        while (temp->next) {
            temp = temp->next;
        }
        temp->next = otherList.head;
    }

    // Function to display the linked list
    void display() {
        Node* temp = head;
        while (temp) {
            std::cout << temp->data << " ";
            temp = temp->next;
        }
        std::cout << std::endl;
    }
};

int main() {
    LinkedList list1;
    list1.insert(1);
    list1.insert(2);
    list1.insert(3);

    LinkedList list2;
    list2.insert(4);
    list2.insert(5);

    std::cout << "List 1: ";
    list1.display();
    std::cout << "List 2: ";
    list2.display();

    list1.concatenate(list2);

    std::cout << "Concatenated List: ";
    list1.display();

    return 0;
}
```

This code defines a `LinkedList` class with basic operations like insertion and display. The `concatenate` function concatenates another linked list at the end of the current list. Finally, in the `main` function, we create two linked lists, concatenate the second list to the first, and then display the concatenated list.

### 1. Algorithms & Data Structures (C++): Data structures: Linked Lists: Comparing linked lists and arrays

Linked lists and arrays are fundamental data structures in computer science, each with its own advantages and disadvantages. Let's compare them in terms of various aspects:

1. **Memory Allocation**

Linked List:
    - Linked lists use dynamic memory allocation, which means memory is allocated at runtime as nodes are added.
Array:
    - Arrays use static memory allocation, meaning memory is allocated at compile time and the size of the array must be known beforehand.

1. **Insertion and Deletion**:
    * Linked List:
        * Insertions and deletions are generally faster in linked lists, especially for operations involving adding or removing elements at the beginning or middle of the list. This is because no shifting of elements is required; only the links need to be adjusted.
    * Array:
        * Insertions and deletions in arrays, especially in the middle or beginning, can be slower since elements may need to be shifted to accommodate the change, which can be \(O(n)\) in the worst case.

1. **Random Access**:
    * Linked List:
        * Random access to elements in a linked list is inefficient. To access an element at a particular index, you need to traverse the list from the beginning or end, which takes \(O(n)\) time on average.
    * Array:
        * Arrays support constant-time access to elements using their indices (\(O(1)\) time complexity).

1. **Memory Efficiency**:
    * Linked List:
        * Linked lists use additional memory for storing pointers/references, which can increase memory overhead compared to arrays.
    * Array:
        * Arrays are more memory-efficient since they store only the elements themselves without any additional pointers/references.

1. **Contiguous vs. Non-contiguous Memory**:
    * Linked List:
        * Linked lists use non-contiguous memory allocation as each node can be located anywhere in memory.
    * Array:
        * Arrays use contiguous memory allocation where elements are stored in adjacent memory locations.

1. **Dynamic Size**:
    * Linked List:
        * Linked lists can easily accommodate dynamic resizing since memory allocation is dynamic.
    * Array:
        * Resizing arrays can be inefficient since it may involve allocating a new larger array, copying elements, and deallocating the old array.

1. **Cache Performance**:
    * Linked List:
        * Linked lists may exhibit poorer cache performance compared to arrays, especially in scenarios where elements are accessed sequentially.
    * Array:
        * Arrays can have better cache performance, especially for sequential access, due to the contiguous memory layout.

1. **Implementation Complexity**:
    * Linked List:
        * Implementing a linked list typically involves managing pointers and memory allocation, which can be more complex compared to arrays.
    * Array:
        * Arrays have simpler implementations since they are a basic feature of most programming languages.

In summary, linked lists are often preferred for scenarios requiring frequent insertions and deletions, while arrays are preferred when fast random access or memory efficiency is important. The choice between them depends on the specific requirements and constraints of the problem at hand.

### 1. Algorithms & Data Structures (C++): Data structures: Linked Lists: Linked list theory - operations

Certainly! Linked lists are fundamental data structures in computer science and are often used to implement other data structures like stacks, queues, and graphs. A linked list consists of nodes where each node contains a data field and a reference (or pointer) to the next node in the sequence.

Here's a brief overview of the basic operations on linked lists:

1. **Insertion:**
   * **Insertion at the beginning:** Create a new node with the given data, point its next pointer to the current head of the list, then update the head to point to the new node.
   * **Insertion at the end:** Traverse the list until you reach the last node, then create a new node with the given data and set its next pointer to NULL. Update the next pointer of the current last node to point to the new node.
   * **Insertion at a specific position:** Traverse the list until you reach the node just before the desired position, then adjust the pointers to insert the new node in between.

2. **Deletion:**
   * **Deletion at the beginning:** Update the head pointer to point to the next node of the current head, then delete the old head node.
   * **Deletion at the end:** Traverse the list until you reach the second-to-last node, update its next pointer to NULL, then delete the last node.
   * **Deletion of a specific node:** Traverse the list until you find the node to be deleted, update the next pointer of the previous node to skip the node to be deleted, then delete the node.

3. **Traversal:**
   * Start from the head node and repeatedly follow the next pointers until you reach the end of the list, while processing each node as necessary.

4. **Searching:**
   * Start from the head node and compare the data of each node with the target value until you find a match or reach the end of the list.

5. **Other Operations:**
   * **Size:** Traverse the list and count the number of nodes encountered.
   * **Reverse:** Change the next pointers of each node to reverse the order of the list.
   * **Concatenation:** Link the last node of one list to the head of another list.

It's worth noting that linked lists have advantages such as dynamic memory allocation and efficient insertion and deletion operations compared to arrays, especially when dealing with large amounts of data. However, they also have disadvantages such as the lack of random access and the overhead of storing pointers. Therefore, the choice of data structure depends on the specific requirements of the application.

### 1. Algorithms & Data Structures (C++): Data structures: Linked Lists: Practical (real-world) applications of linked lists

Linked lists have a variety of practical applications across different domains due to their flexibility and efficiency in certain scenarios. Here are some real-world applications where linked lists shine:

1. **Operating Systems**: Linked lists are frequently used in operating systems for managing various system resources such as processes, files, and memory. For example, in process management, a linked list can be used to maintain a list of running processes, where each node contains information about a process (like its ID, state, and pointers to other processes).

2. **File Systems**: In file systems, linked lists can be used to maintain the directory structure. Each node in the linked list can represent a file or a directory, containing metadata such as name, size, and pointers to other files or directories.

3. **Networking**: Linked lists can be used in networking applications for managing data packets in a network buffer. Each node in the linked list can represent a packet, and pointers can be used to link packets together in the order they are received or need to be transmitted.

4. **Graphics and Game Development**: Linked lists are commonly used in graphics and game development for implementing data structures such as scene graphs or linked lists of objects. Each node can represent an object in the scene, and pointers can be used to link objects together based on their relationships (e.g., parent-child relationships in a scene graph).

5. **Undo Functionality**: Linked lists are often used to implement undo functionality in text editors or other applications where users can perform undo operations. Each node in the linked list represents a state change, and pointers are used to navigate between different states.

6. **Polynomial Manipulation**: Linked lists can be used to represent polynomials in mathematics. Each node in the linked list can represent a term in the polynomial (e.g., coefficient and exponent), and pointers can be used to link terms together to form the polynomial.

7. **Symbol Tables**: Linked lists are used in compilers and interpreters for implementing symbol tables, which store information about variables, functions, and other symbols in a program. Each node in the linked list represents a symbol, and pointers are used to link symbols together.

8. **Cache Management**: Linked lists are used in cache management algorithms such as LRU (Least Recently Used) or LFU (Least Frequently Used). In these algorithms, linked lists are used to maintain the order of cache entries based on their access frequency or recency.

These are just a few examples, but linked lists find applications in many other areas of computer science and software engineering due to their simplicity and versatility.

### 1. Algorithms & Data Structures (C++): Data structures: Linked Lists: Pros and cons of linked lists

Linked lists are fundamental data structures in computer science, offering certain advantages and drawbacks compared to other data structures like arrays. Here's an overview of the pros and cons of linked lists:

#### Pros

1. **Dynamic Size**: Linked lists can dynamically grow and shrink in size, as memory allocation for each element is done individually. This makes them suitable for situations where the size of the data structure is unpredictable or needs to change frequently.

2. **Insertions and Deletions**: Insertions and deletions in a linked list are generally fast operations, especially when performed at the beginning or the middle of the list. Unlike arrays, where inserting or deleting elements might require shifting elements, linked lists only require changing pointers, which can be done in constant time.

3. **Memory Efficiency**: Linked lists only utilize memory for the elements they contain and the pointers to connect them, making them memory-efficient compared to fixed-size arrays which may have unused space or need to allocate more space than required.

4. **Flexibility**: There are different types of linked lists like singly linked lists, doubly linked lists, and circular linked lists, each offering specific advantages. This flexibility allows for the selection of the most appropriate type based on the requirements of the application.

#### Cons

1. **Random Access**: Unlike arrays, linked lists do not support constant-time random access to elements. Accessing an element in a linked list typically requires traversing the list from the beginning or end, which can result in linear time complexity, making them inefficient for random access scenarios.

2. **Memory Overhead**: Each element in a linked list requires additional memory for storing the pointer to the next (and previous, in the case of doubly linked lists) element. This overhead can be significant, especially for small data types, leading to higher memory consumption compared to arrays.

3. **Cache Locality**: Linked lists often suffer from poor cache locality due to the scattered memory locations of their elements. This can result in more cache misses and slower performance, especially in applications that heavily rely on data caching.

4. **Traversal Overhead**: Traversing a linked list requires following pointers from one node to another, which can introduce overhead compared to arrays where elements are stored contiguously in memory. This overhead can impact performance, especially in situations where frequent traversal is required.

In summary, linked lists are efficient for dynamic data structures where frequent insertions and deletions are performed, but they may not be suitable for scenarios requiring random access or where memory efficiency and cache locality are critical. The choice of data structure depends on the specific requirements and characteristics of the application.

### 1. Algorithms & Data Structures (C++): Duplicates removal in Linked List

Removing duplicates from a linked list is a common task in programming interviews and real-world scenarios. Here's how you can do it in C++:

```cpp
#include <iostream>
#include <unordered_set>

using namespace std;

// Node definition for the linked list
struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

// Function to remove duplicates from a linked list
void removeDuplicates(Node* head) {
    if (head == nullptr || head->next == nullptr) // Check if the list is empty or has only one element
        return;

    unordered_set<int> seen;
    Node* prev = nullptr;
    Node* current = head;

    while (current != nullptr) {
        if (seen.find(current->data) != seen.end()) {
            // Duplicate found, remove current node
            prev->next = current->next;
            delete current;
            current = prev->next;
        } else {
            // No duplicate found, move to the next node
            seen.insert(current->data);
            prev = current;
            current = current->next;
        }
    }
}

// Function to print the linked list
void printList(Node* head) {
    while (head != nullptr) {
        cout << head->data << " ";
        head = head->next;
    }
    cout << endl;
}

// Test the implementation
int main() {
    // Create a sample linked list with duplicates
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->next = new Node(3);
    head->next->next->next = new Node(2);
    head->next->next->next->next = new Node(4);
    head->next->next->next->next->next = new Node(1);

    cout << "Original linked list: ";
    printList(head);

    // Remove duplicates
    removeDuplicates(head);

    cout << "Linked list after removing duplicates: ";
    printList(head);

    return 0;
}
```

In this code:

1. We traverse the linked list while keeping track of the elements seen so far using an `unordered_set`.
2. If we encounter a duplicate, we remove the node containing the duplicate by adjusting pointers.
3. The `printList` function is provided to display the linked list before and after removing duplicates.
4. Finally, in the `main` function, we create a sample linked list with duplicates, remove the duplicates, and print the result.

### 1. Algorithms & Data Structures (C++): Exercise: Linked List Cycle

Sure, here's an exercise on detecting a cycle in a linked list in C++:

```cpp
#include <iostream>

struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

bool hasCycle(ListNode *head) {
    if (!head || !head->next)
        return false;
    
    ListNode *slow = head;
    ListNode *fast = head->next;
    
    while (fast && fast->next) {
        if (slow == fast)
            return true;
        slow = slow->next;
        fast = fast->next->next;
    }
    
    return false;
}

int main() {
    // Example usage:
    ListNode *head = new ListNode(3);
    head->next = new ListNode(2);
    head->next->next = new ListNode(0);
    head->next->next->next = new ListNode(-4);
    head->next->next->next->next = head->next; // Cycle formed
    
    if (hasCycle(head))
        std::cout << "The linked list has a cycle." << std::endl;
    else
        std::cout << "The linked list does not have a cycle." << std::endl;
    
    return 0;
}
```

This code defines a `ListNode` struct and a function `hasCycle` that detects if a linked list contains a cycle. It uses the slow and fast pointer approach, where the slow pointer moves one step at a time while the fast pointer moves two steps at a time. If there's a cycle, the fast pointer will eventually catch up with the slow pointer.

### 1. Algorithms & Data Structures (C++): Exercise: Linked List: Exersice Return Kth to Last

Sure, let's work on an exercise to return the kth to last element of a singly linked list in C++. Here's how you can implement it:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* next;
    Node(int d) : data(d), next(nullptr) {}
};

class LinkedList {
private:
    Node* head;
public:
    LinkedList() : head(nullptr) {}

    // Function to add a node at the end of the list
    void append(int data) {
        Node* newNode = new Node(data);
        if (head == nullptr) {
            head = newNode;
            return;
        }
        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = newNode;
    }

    // Function to return the kth to last element of the list
    Node* kthToLast(int k) {
        if (head == nullptr || k < 1) return nullptr;

        Node* p1 = head;
        Node* p2 = head;

        // Move p2 k nodes into the list
        for (int i = 0; i < k; ++i) {
            if (p2 == nullptr) return nullptr; // Out of bounds
            p2 = p2->next;
        }

        // Move them at the same pace. When p2 hits the end, p1 will be at the right element.
        while (p2 != nullptr) {
            p1 = p1->next;
            p2 = p2->next;
        }
        return p1;
    }

    // Function to display the list
    void display() {
        Node* temp = head;
        while (temp != nullptr) {
            std::cout << temp->data << " ";
            temp = temp->next;
        }
        std::cout << std::endl;
    }
};

int main() {
    LinkedList list;
    list.append(1);
    list.append(2);
    list.append(3);
    list.append(4);
    list.append(5);

    std::cout << "Original list: ";
    list.display();

    int k = 2; // Change k to any desired value
    Node* kthNode = list.kthToLast(k);
    if (kthNode != nullptr)
        std::cout << "The " << k << "th to last element is: " << kthNode->data << std::endl;
    else
        std::cout << "Invalid value of k or list is too short." << std::endl;

    return 0;
}
```

In this code, `LinkedList` is a simple implementation of a singly linked list, and `kthToLast` is the function that returns the kth to last element. It uses two pointers, `p1` and `p2`, where `p2` is k nodes ahead of `p1`. Then, it moves both pointers until `p2` reaches the end of the list. At that point, `p1` will be pointing to the kth to last element.

### 1. Algorithms & Data Structures (C++): Exercise: Linked List: Intersection

Sure, let's dive into it. For finding the intersection of two linked lists in C++, you can follow these steps:

1. Traverse both linked lists and find their lengths.
2. Calculate the difference in lengths between the two lists.
3. Traverse the longer list by the difference calculated in step 2.
4. Now, both lists have the same number of nodes remaining.
5. Traverse both lists in parallel until you find a common node (intersection point) or reach the end of one of the lists.

Here's a C++ implementation of the intersection of two linked lists:

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
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        int lenA = getLength(headA);
        int lenB = getLength(headB);

        // Move head of longer list to make both lists equal in length
        while (lenA > lenB) {
            headA = headA->next;
            lenA--;
        }

        while (lenB > lenA) {
            headB = headB->next;
            lenB--;
        }

        // Traverse both lists until intersection point is found
        while (headA != headB) {
            headA = headA->next;
            headB = headB->next;
        }

        return headA; // Return intersection point, or NULL if no intersection
    }

private:
    int getLength(ListNode *head) {
        int length = 0;
        while (head != nullptr) {
            length++;
            head = head->next;
        }
        return length;
    }
};

// Helper function to print the linked list
void printList(ListNode *head) {
    while (head) {
        cout << head->val << " ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    // Example usage
    ListNode *headA = new ListNode(4);
    headA->next = new ListNode(1);
    headA->next->next = new ListNode(8);
    headA->next->next->next = new ListNode(4);
    headA->next->next->next->next = new ListNode(5);

    ListNode *headB = new ListNode(5);
    headB->next = new ListNode(0);
    headB->next->next = headA->next->next;

    cout << "List A: ";
    printList(headA);
    cout << "List B: ";
    printList(headB);

    Solution solution;
    ListNode *intersectionNode = solution.getIntersectionNode(headA, headB);

    if (intersectionNode)
        cout << "Intersection at node with value: " << intersectionNode->val << endl;
    else
        cout << "No intersection found" << endl;

    return 0;
}
```

This code defines a `ListNode` structure and a `Solution` class with a method `getIntersectionNode` to find the intersection point of two linked lists. In the `main` function, it demonstrates how to use this method with two example linked lists.

### 1. Algorithms & Data Structures (C++): Exercise: Linked List: Partition

Sure, let's work on the partitioning of a linked list. In this exercise, you'll partition a linked list around a value `x`, such that all nodes less than `x` come before all nodes greater than or equal to `x`. Here's a sample approach in C++:

```cpp
#include <iostream>

using namespace std;

// Node structure for the linked list
struct Node {
    int data;
    Node* next;
    Node(int d) : data(d), next(nullptr) {}
};

// Function to partition the linked list
Node* partition(Node* head, int x) {
    Node* before_head = nullptr;
    Node* before_tail = nullptr;
    Node* after_head = nullptr;
    Node* after_tail = nullptr;

    while (head != nullptr) {
        Node* next_node = head->next;
        head->next = nullptr;
        if (head->data < x) {
            if (before_head == nullptr) {
                before_head = head;
                before_tail = head;
            } else {
                before_tail->next = head;
                before_tail = head;
            }
        } else {
            if (after_head == nullptr) {
                after_head = head;
                after_tail = head;
            } else {
                after_tail->next = head;
                after_tail = head;
            }
        }
        head = next_node;
    }

    if (before_head == nullptr) {
        return after_head;
    }

    before_tail->next = after_head;
    return before_head;
}

// Function to print the linked list
void printList(Node* node) {
    while (node != nullptr) {
        cout << node->data << " ";
        node = node->next;
    }
    cout << endl;
}

// Test the partition function
int main() {
    // Creating the linked list: 1 -> 4 -> 3 -> 2 -> 5 -> 2
    Node* head = new Node(1);
    head->next = new Node(4);
    head->next->next = new Node(3);
    head->next->next->next = new Node(2);
    head->next->next->next->next = new Node(5);
    head->next->next->next->next->next = new Node(2);

    cout << "Original linked list: ";
    printList(head);

    int x = 3; // Partition value
    head = partition(head, x);

    cout << "Linked list after partitioning around " << x << ": ";
    printList(head);

    return 0;
}
```

In this code:

* We define a `Node` struct to represent each node in the linked list.
* The `partition` function takes the head of the linked list and the partition value `x` as input.
* We traverse the list once, moving nodes to two separate lists (`before_head` and `after_head`) based on whether their values are less than `x` or greater than or equal to `x`.
* Finally, we concatenate the two lists and return the head of the partitioned list.

You can adjust the test case and the partition value `x` to see how the function behaves with different inputs.

### 1. Algorithms & Data Structures (C++): Exercise: Linked List: Remove Duplicates

Sure, let's work on an exercise to remove duplicates from a singly linked list in C++. Here's a simple implementation:

```cpp
#include <iostream>
#include <unordered_set>

using namespace std;

// Node definition for the linked list
struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

// Function to remove duplicates from a linked list
void removeDuplicates(Node* head) {
    if (head == nullptr || head->next == nullptr)
        return;

    unordered_set<int> seen;
    Node* curr = head;
    Node* prev = nullptr;

    while (curr != nullptr) {
        if (seen.find(curr->data) != seen.end()) {
            prev->next = curr->next;
            delete curr;
            curr = prev->next;
        } else {
            seen.insert(curr->data);
            prev = curr;
            curr = curr->next;
        }
    }
}

// Function to print the linked list
void printList(Node* head) {
    Node* temp = head;
    while (temp != nullptr) {
        cout << temp->data << " ";
        temp = temp->next;
    }
    cout << endl;
}

int main() {
    // Creating the linked list: 1 -> 2 -> 2 -> 3 -> 4 -> 4 -> 5
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->next = new Node(2);
    head->next->next->next = new Node(3);
    head->next->next->next->next = new Node(4);
    head->next->next->next->next->next = new Node(4);
    head->next->next->next->next->next->next = new Node(5);

    cout << "Original Linked List: ";
    printList(head);

    removeDuplicates(head);

    cout << "Linked List after removing duplicates: ";
    printList(head);

    return 0;
}
```

This code defines a `Node` structure for the linked list and implements a function `removeDuplicates` to remove duplicate elements from the list. The `printList` function is for printing the elements of the list. In the `main` function, a sample linked list is created, and then duplicates are removed using the `removeDuplicates` function. Finally, the resulting list is printed.

### 1. Algorithms & Data Structures (C++): Exercise: Linked List: Sum Linked Lists

To solve the exercise of summing two linked lists in C++, you can follow these steps:

1. Define a linked list node structure with a value and a pointer to the next node.
2. Implement a function to add a new node to the end of a linked list.
3. Implement a function to print a linked list for debugging purposes.
4. Implement a function to sum two linked lists.
5. Test your implementation with different cases.

Here's a sample implementation:

```cpp
#include <iostream>

struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

void insertNode(ListNode *&head, int val) {
    if (!head) {
        head = new ListNode(val);
    } else {
        ListNode *temp = head;
        while (temp->next) {
            temp = temp->next;
        }
        temp->next = new ListNode(val);
    }
}

void printList(ListNode *head) {
    while (head) {
        std::cout << head->val << " ";
        head = head->next;
    }
    std::cout << std::endl;
}

ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
    ListNode *dummy = new ListNode(0);
    ListNode *current = dummy;
    int carry = 0;

    while (l1 || l2 || carry) {
        int sum = (l1 ? l1->val : 0) + (l2 ? l2->val : 0) + carry;
        carry = sum / 10;
        current->next = new ListNode(sum % 10);
        current = current->next;
        l1 = l1 ? l1->next : nullptr;
        l2 = l2 ? l2->next : nullptr;
    }

    return dummy->next;
}

int main() {
    // Creating linked lists
    ListNode *l1 = nullptr;
    ListNode *l2 = nullptr;

    // Adding elements to the linked lists
    insertNode(l1, 2);
    insertNode(l1, 4);
    insertNode(l1, 3);

    insertNode(l2, 5);
    insertNode(l2, 6);
    insertNode(l2, 4);

    std::cout << "Input Lists:" << std::endl;
    std::cout << "List 1: ";
    printList(l1);
    std::cout << "List 2: ";
    printList(l2);

    // Summing the lists
    ListNode *sumList = addTwoNumbers(l1, l2);

    std::cout << "Summed List: ";
    printList(sumList);

    // Freeing memory
    while (sumList) {
        ListNode *temp = sumList;
        sumList = sumList->next;
        delete temp;
    }
    return 0;
}
```

This code defines a `ListNode` structure, along with functions to insert nodes into a linked list, print a linked list, and sum two linked lists. Finally, it demonstrates the usage of these functions in the `main` function.

### 1. Algorithms & Data Structures (C++): Exercise: Intersection Of Two Linked Lists

Sure, I can provide you with a C++ implementation for finding the intersection of two linked lists. Here's a simple approach using hash sets to store visited nodes:

```cpp
#include <iostream>
#include <unordered_set>

using namespace std;

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        unordered_set<ListNode*> visited;

        // Traverse the first list and store its nodes in the set
        ListNode* temp = headA;
        while (temp != nullptr) {
            visited.insert(temp);
            temp = temp->next;
        }

        // Traverse the second list and check for intersection
        temp = headB;
        while (temp != nullptr) {
            // If current node is found in the set, it's the intersection point
            if (visited.find(temp) != visited.end())
                return temp;
            temp = temp->next;
        }

        // No intersection found
        return nullptr;
    }
};

// Helper function to print the linked list
void printList(ListNode* head) {
    ListNode* temp = head;
    while (temp != nullptr) {
        cout << temp->val << " ";
        temp = temp->next;
    }
    cout << endl;
}

int main() {
    // Creating sample linked lists
    ListNode* intersect = new ListNode(8);
    intersect->next = new ListNode(4);
    intersect->next->next = new ListNode(5);

    ListNode* listA = new ListNode(4);
    listA->next = new ListNode(1);
    listA->next->next = intersect;

    ListNode* listB = new ListNode(5);
    listB->next = new ListNode(6);
    listB->next->next = new ListNode(1);
    listB->next->next->next = intersect;

    Solution solution;
    ListNode* intersectionNode = solution.getIntersectionNode(listA, listB);

    if (intersectionNode)
        cout << "Intersection node value: " << intersectionNode->val << endl;
    else
        cout << "No intersection found" << endl;

    // Freeing memory
    delete listA;
    delete listB;
    delete intersect;

    return 0;
}
```

This code defines a `ListNode` structure for the linked list nodes and a `Solution` class containing the `getIntersectionNode` method, which finds the intersection node of two linked lists. The `main` function demonstrates the usage of this method with sample linked lists.

### 1. Algorithms & Data Structures (C++): Exercise: Palindrome Linked List

Sure! The exercise involves writing a C++ function to determine whether a singly linked list is a palindrome or not. A palindrome is a sequence of characters that reads the same forwards and backwards.

Here's an approach using C++:

```cpp
#include <iostream>

struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

// Function to reverse a linked list
ListNode* reverseList(ListNode* head) {
    ListNode* prev = nullptr;
    ListNode* curr = head;
    while (curr != nullptr) {
        ListNode* next = curr->next;
        curr->next = prev;
        prev = curr;
        curr = next;
    }
    return prev;
}

// Function to check if a linked list is a palindrome
bool isPalindrome(ListNode* head) {
    if (head == nullptr || head->next == nullptr)
        return true;

    // Find the middle of the linked list
    ListNode* slow = head;
    ListNode* fast = head;
    while (fast->next != nullptr && fast->next->next != nullptr) {
        slow = slow->next;
        fast = fast->next->next;
    }

    // Reverse the second half of the linked list
    ListNode* secondHalf = reverseList(slow->next);

    // Compare the first half and the reversed second half
    ListNode* p1 = head;
    ListNode* p2 = secondHalf;
    while (p2 != nullptr) {
        if (p1->val != p2->val)
            return false;
        p1 = p1->next;
        p2 = p2->next;
    }

    // Restore the original list (not necessary in this case)
    // slow->next = reverseList(secondHalf);

    return true;
}

int main() {
    // Example usage
    ListNode* head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(2);
    head->next->next->next->next = new ListNode(1);

    if (isPalindrome(head))
        std::cout << "Linked list is a palindrome." << std::endl;
    else
        std::cout << "Linked list is not a palindrome." << std::endl;

    // Free memory
    ListNode* current = head;
    while (current != nullptr) {
        ListNode* temp = current;
        current = current->next;
        delete temp;
    }

    return 0;
}
```

This code defines a `ListNode` struct representing a node in a singly linked list, and two functions: `reverseList` to reverse a linked list and `isPalindrome` to check if a linked list is a palindrome.

In the `isPalindrome` function:

1. We find the middle of the linked list using the slow and fast pointers technique.
2. We reverse the second half of the linked list.
3. We compare the first half with the reversed second half to check if the linked list is a palindrome.

Finally, in the `main` function, an example usage of the `isPalindrome` function is provided.

### 1. Algorithms & Data Structures (C++): Find Middle Of Linked List - Linked List

To find the middle of a linked list in C++, you can use the fast-slow pointer approach. Here's how it works:

1. Initialize two pointers, `slow` and `fast`, both pointing to the head of the linked list.
2. Move `slow` one step at a time while moving `fast` two steps at a time.
3. When `fast` reaches the end of the list (i.e., `fast->next` or `fast->next->next` is `nullptr`), `slow` will be at the middle of the list.

Here's the C++ code implementation:

```cpp
#include <iostream>

struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* findMiddle(ListNode* head) {
    if (head == nullptr || head->next == nullptr)
        return head; // Empty list or single node list
    
    ListNode* slow = head;
    ListNode* fast = head;
    
    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;
        fast = fast->next->next;
    }
    
    return slow;
}

// Utility function to print the linked list
void printList(ListNode* head) {
    while (head != nullptr) {
        std::cout << head->val << " ";
        head = head->next;
    }
    std::cout << std::endl;
}

int main() {
    // Create a sample linked list: 1 -> 2 -> 3 -> 4 -> 5 -> nullptr
    ListNode* head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);
    
    std::cout << "Original List: ";
    printList(head);
    
    ListNode* middle = findMiddle(head);
    std::cout << "Middle of the List: " << middle->val << std::endl;
    
    return 0;
}
```

This code will output:

```bash
Original List: 1 2 3 4 5 
Middle of the List: 3
```

This approach has a time complexity of O(N) where N is the number of nodes in the linked list and requires only a constant amount of extra space.

### 1. Algorithms & Data Structures (C++): Find data in Linked List

Sure, finding data in a linked list involves traversing the list and comparing each node's data with the data you're searching for. Here's a simple example in C++:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* next;
    
    Node(int value) : data(value), next(nullptr) {}
};

class LinkedList {
private:
    Node* head;

public:
    LinkedList() : head(nullptr) {}

    // Function to insert data at the end of the linked list
    void insert(int data) {
        Node* newNode = new Node(data);
        if (head == nullptr) {
            head = newNode;
        } else {
            Node* temp = head;
            while (temp->next != nullptr) {
                temp = temp->next;
            }
            temp->next = newNode;
        }
    }

    // Function to find data in the linked list
    bool find(int data) {
        Node* temp = head;
        while (temp != nullptr) {
            if (temp->data == data) {
                return true; // Found the data
            }
            temp = temp->next;
        }
        return false; // Data not found
    }
};

int main() {
    LinkedList list;
    list.insert(5);
    list.insert(10);
    list.insert(15);
    
    // Search for data in the linked list
    int searchData = 10;
    if (list.find(searchData)) {
        std::cout << "Data " << searchData << " found in the linked list." << std::endl;
    } else {
        std::cout << "Data " << searchData << " not found in the linked list." << std::endl;
    }
    
    return 0;
}
```

In this example, we have a `Node` struct to represent each element of the linked list, and a `LinkedList` class to manage the list. The `insert` function adds elements to the end of the list, and the `find` function searches for a specific value within the list. Finally, in the `main` function, we create a linked list, populate it with some data, and then search for a specific value.

### 1. Algorithms & Data Structures (C++): Find the Intersection Point in Linked Lists

Finding the intersection point of two linked lists is a common algorithmic problem. Here's a C++ implementation using the two-pointer approach, which is efficient and has a time complexity of O(m + n), where m and n are the lengths of the two linked lists.

```cpp
#include <iostream>

using namespace std;

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

int length(ListNode *head) {
    int len = 0;
    while (head != NULL) {
        len++;
        head = head->next;
    }
    return len;
}

ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
    // Get the lengths of the two linked lists
    int lenA = length(headA);
    int lenB = length(headB);
    
    // Set two pointers at the heads of the linked lists
    ListNode *ptrA = headA;
    ListNode *ptrB = headB;
    
    // Advance the longer list's pointer by the difference in lengths
    if (lenA > lenB) {
        for (int i = 0; i < lenA - lenB; ++i) {
            ptrA = ptrA->next;
        }
    } else {
        for (int i = 0; i < lenB - lenA; ++i) {
            ptrB = ptrB->next;
        }
    }
    
    // Move both pointers until they meet or reach the end
    while (ptrA != NULL && ptrB != NULL && ptrA != ptrB) {
        ptrA = ptrA->next;
        ptrB = ptrB->next;
    }
    
    // Return the intersection point (or NULL if no intersection)
    return ptrA;
}

// Function to print the linked list
void printList(ListNode *head) {
    while (head != NULL) {
        cout << head->val << " ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    // Example usage
    // Create two intersecting linked lists
    ListNode *intersection = new ListNode(8);
    intersection->next = new ListNode(4);
    intersection->next->next = new ListNode(5);
    
    ListNode *headA = new ListNode(4);
    headA->next = new ListNode(1);
    headA->next->next = intersection;
    
    ListNode *headB = new ListNode(5);
    headB->next = new ListNode(0);
    headB->next->next = new ListNode(1);
    headB->next->next->next = intersection;
    
    // Find and print the intersection point
    ListNode *intersectionNode = getIntersectionNode(headA, headB);
    if (intersectionNode)
        cout << "Intersection Point Value: " << intersectionNode->val << endl;
    else
        cout << "No intersection point found." << endl;
    
    // Clean up memory
    delete headA;
    delete headB;
    delete intersection;
    
    return 0;
}
```

This code first calculates the lengths of both linked lists. Then, it adjusts the pointers so that they start at the same relative position from the end of each list. Finally, it iterates through both lists until it finds the intersection point or reaches the end of either list.

### 1. Algorithms & Data Structures (C++): Finding Intersecting point of Two Linked List

To find the intersecting point of two linked lists in C++, you can use the following approach:

1. Traverse both linked lists to find their lengths and the tail nodes.
2. If the tail nodes are not the same, then the lists do not intersect, and you can return nullptr.
3. If they do intersect, reset the pointers to the heads of both lists and advance the pointer of the longer list by the difference in lengths.
4. Now, traverse both lists in parallel until you find the common node, which is the intersection point.

Here's the C++ code implementing this approach:

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
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        if (!headA || !headB) return nullptr;

        // Function to get the length of a linked list
        auto getLength = [](ListNode *head) {
            int len = 0;
            while (head) {
                len++;
                head = head->next;
            }
            return len;
        };

        int lenA = getLength(headA);
        int lenB = getLength(headB);

        // Reset pointers to the beginning of each list
        ListNode *ptrA = headA;
        ListNode *ptrB = headB;

        // Move the pointer of the longer list ahead by the difference in lengths
        while (lenA > lenB) {
            ptrA = ptrA->next;
            lenA--;
        }
        while (lenB > lenA) {
            ptrB = ptrB->next;
            lenB--;
        }

        // Traverse both lists in parallel until intersection point is found
        while (ptrA != ptrB) {
            ptrA = ptrA->next;
            ptrB = ptrB->next;
        }

        // Return the intersection point (or nullptr if no intersection)
        return ptrA;
    }
};

// Helper function to print the linked list for testing
void printList(ListNode *head) {
    while (head) {
        cout << head->val << " ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    // Example usage
    ListNode *common = new ListNode(8);
    common->next = new ListNode(4);
    common->next->next = new ListNode(5);

    ListNode *headA = new ListNode(4);
    headA->next = new ListNode(1);
    headA->next->next = common;

    ListNode *headB = new ListNode(5);
    headB->next = new ListNode(6);
    headB->next->next = new ListNode(1);
    headB->next->next->next = common;

    Solution solution;
    ListNode *intersectionNode = solution.getIntersectionNode(headA, headB);
    if (intersectionNode)
        cout << "Intersecting node value: " << intersectionNode->val << endl;
    else
        cout << "Lists do not intersect." << endl;

    return 0;
}
```

This code creates two linked lists `headA` and `headB` and finds their intersecting node, if any. You can modify the `main` function to create different linked lists and test the function with your own examples.

### 1. Algorithms & Data Structures (C++): Finding Middle Element of a Linked List

To find the middle element of a linked list in C++, you can use the slow and fast pointer approach. Here's a simple implementation:

```cpp
#include <iostream>

// Node structure for the linked list
struct Node {
    int data;
    Node* next;
    
    Node(int val) : data(val), next(nullptr) {}
};

// Function to find the middle element of a linked list
Node* findMiddleElement(Node* head) {
    if (head == nullptr || head->next == nullptr) {
        return head;
    }
    
    Node* slow = head;
    Node* fast = head;
    
    // Move slow pointer one step at a time and fast pointer two steps at a time
    // When the fast pointer reaches the end, the slow pointer will be at the middle
    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;
        fast = fast->next->next;
    }
    
    return slow;
}

// Function to print the linked list
void printLinkedList(Node* head) {
    while (head != nullptr) {
        std::cout << head->data << " ";
        head = head->next;
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
    
    std::cout << "Linked List: ";
    printLinkedList(head);
    
    Node* middle = findMiddleElement(head);
    if (middle != nullptr) {
        std::cout << "Middle Element: " << middle->data << std::endl;
    } else {
        std::cout << "List is empty!" << std::endl;
    }
    
    return 0;
}
```

This code defines a `Node` structure representing each element of the linked list. The `findMiddleElement` function implements the slow and fast pointer approach to locate the middle element of the list. Finally, `printLinkedList` is a utility function to print the linked list, and the `main` function demonstrates the usage of these functions.

### 1. Algorithms & Data Structures (C++): Immutable List

Sure! An immutable list in C++ can be implemented using various approaches. One common approach is to use a linked list structure where each node contains a value and a pointer to the next node. However, instead of allowing modification of the list, operations return a new list with the desired changes while keeping the original list unchanged.

Here's a simple implementation of an immutable linked list in C++:

```cpp
#include <iostream>

template <typename T>
class ImmutableList {
private:
    T value;
    const ImmutableList<T>* next;

public:
    ImmutableList(const T& value, const ImmutableList<T>* next = nullptr)
        : value(value), next(next) {}

    // Function to prepend a value to the list
    ImmutableList<T> prepend(const T& value) const {
        return ImmutableList(value, this);
    }

    // Function to get the value at the head of the list
    T head() const {
        return value;
    }

    // Function to get the tail of the list
    ImmutableList<T> tail() const {
        return *next;
    }

    // Function to check if the list is empty
    bool isEmpty() const {
        return next == nullptr;
    }
};

int main() {
    // Create an empty list
    ImmutableList<int> emptyList(0);

    // Add some elements
    ImmutableList<int> list = emptyList.prepend(3).prepend(2).prepend(1);

    // Print the elements of the list
    while (!list.isEmpty()) {
        std::cout << list.head() << " ";
        list = list.tail();
    }
    std::cout << std::endl;

    return 0;
}
```

In this implementation:

* The `ImmutableList` class represents a node in the linked list. It contains a `value` and a pointer to the next node, which is a `const` pointer to ensure immutability.
* The `prepend` function is used to add a new element to the beginning of the list, returning a new list with the new element added.
* The `head` function returns the value at the head of the list.
* The `tail` function returns a new list containing all elements except the head.
* The `isEmpty` function checks if the list is empty.

This implementation demonstrates how you can create and manipulate an immutable list in C++.

### 1. Algorithms & Data Structures (C++): Insert in Sorted Linked List

Inserting an element into a sorted linked list in C++ involves finding the correct position to insert the new element while maintaining the sorted order of the list. Here's a basic implementation:

```cpp
#include <iostream>

using namespace std;

// Define the structure of a node in the linked list
struct Node {
    int data;
    Node* next;
};

// Function to create a new node
Node* createNode(int data) {
    Node* newNode = new Node;
    newNode->data = data;
    newNode->next = nullptr;
    return newNode;
}

// Function to insert a new node into a sorted linked list
void insertSorted(Node*& head, int data) {
    Node* newNode = createNode(data);
    
    // If the list is empty or the new data is less than the first element
    if (head == nullptr || data < head->data) {
        newNode->next = head;
        head = newNode;
        return;
    }
    
    Node* current = head;
    while (current->next != nullptr && current->next->data < data) {
        current = current->next;
    }
    
    newNode->next = current->next;
    current->next = newNode;
}

// Function to print the linked list
void printList(Node* head) {
    while (head != nullptr) {
        cout << head->data << " ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    Node* head = nullptr;
    insertSorted(head, 5);
    insertSorted(head, 3);
    insertSorted(head, 8);
    insertSorted(head, 1);
    insertSorted(head, 6);
    
    cout << "Sorted Linked List: ";
    printList(head);
    
    return 0;
}
```

In this code:

* We define a `Node` structure to represent each element in the linked list.
* `createNode` function creates a new node with the given data.
* `insertSorted` function inserts a new node into the sorted linked list while maintaining the sorted order.
* `printList` function is used to print the elements of the linked list.
* In the `main` function, we create a sorted linked list by inserting elements in a sorted order and then print the list.

### 1. Algorithms & Data Structures (C++): Inserting in a Sorted Linked List

Inserting a new node into a sorted linked list in C++ involves traversing the list to find the correct position for insertion while maintaining the sorted order. Here's a simple implementation:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* next;
    Node(int value) : data(value), next(nullptr) {}
};

void insertSorted(Node*& head, int value) {
    Node* newNode = new Node(value);
    
    // If the list is empty or the new node's value is less than the head's value
    // Insert the new node at the beginning
    if (head == nullptr || value < head->data) {
        newNode->next = head;
        head = newNode;
        return;
    }

    // Traverse the list to find the correct position to insert the new node
    Node* current = head;
    while (current->next != nullptr && current->next->data < value) {
        current = current->next;
    }

    // Insert the new node after the current node
    newNode->next = current->next;
    current->next = newNode;
}

void printList(Node* head) {
    while (head != nullptr) {
        std::cout << head->data << " ";
        head = head->next;
    }
    std::cout << std::endl;
}

int main() {
    Node* head = nullptr;
    
    // Inserting elements into the sorted linked list
    insertSorted(head, 5);
    insertSorted(head, 10);
    insertSorted(head, 7);
    insertSorted(head, 3);
    insertSorted(head, 12);

    // Print the sorted linked list
    std::cout << "Sorted Linked List: ";
    printList(head);

    return 0;
}
```

This code defines a `Node` structure representing each element in the linked list. The `insertSorted` function inserts a new node into the sorted linked list while maintaining the sorted order. Finally, the `printList` function prints the elements of the linked list.

When you run this program, it will output:

```bash
Sorted Linked List: 3 5 7 10 12 
```

This demonstrates the sorted insertion of elements into the linked list.

### 1. Algorithms & Data Structures (C++): Intersection Of Two Linked List - Linked List

Certainly! Finding the intersection of two linked lists involves determining if there are any common nodes between them. Here's a basic implementation in C++:

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
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        if (!headA || !headB)
            return nullptr;

        ListNode *a = headA;
        ListNode *b = headB;

        // Traverse both lists until they meet or reach the end
        while (a != b) {
            // If a has reached the end, move it to the head of B
            if (!a)
                a = headB;
            else
                a = a->next;
            
            // If b has reached the end, move it to the head of A
            if (!b)
                b = headA;
            else
                b = b->next;
        }

        // a (or b) will be either nullptr (no intersection) or the intersection point
        return a;
    }
};

int main() {
    // Example usage
    ListNode *intersection = new ListNode(8);
    
    ListNode *headA = new ListNode(4);
    headA->next = new ListNode(1);
    headA->next->next = intersection;
    headA->next->next->next = new ListNode(4);
    headA->next->next->next->next = new ListNode(5);

    ListNode *headB = new ListNode(5);
    headB->next = new ListNode(6);
    headB->next->next = new ListNode(1);
    headB->next->next->next = intersection;

    Solution solution;
    ListNode *result = solution.getIntersectionNode(headA, headB);

    if (result)
        cout << "Intersection node value: " << result->val << endl;
    else
        cout << "No intersection found." << endl;

    return 0;
}
```

In this implementation, we have a class `Solution` that contains the method `getIntersectionNode`, which takes in the heads of two linked lists `headA` and `headB`. The method iterates through both lists simultaneously until they meet at the intersection point or reach the end. If there's no intersection, it returns `nullptr`. Otherwise, it returns the node where they intersect.

In the `main` function, I've provided an example usage with two linked lists that intersect at node with value `8`. You can modify it to test with your own linked lists.

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

* Use lists (std::list) when you need efficient insertion and deletion operations at arbitrary positions and don't require frequent random access.
* Use linked lists when you need flexibility in memory allocation, such as when you expect frequent insertions or deletions at the beginning or middle of the list, or when contiguous memory allocation is not feasible.

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

* The function `findLongestString` takes a vector of strings as input and returns the longest string found in the list.
* Inside the function, it first checks if the list is empty. If it is, it returns an empty string.
* Otherwise, it assumes the first string in the list is the longest.
* It then iterates through the remaining strings in the list and updates the `longest` variable if it encounters a longer string.
* Finally, it returns the longest string found.
* In the `main` function, a sample list of strings is created, and the `findLongestString` function is called to find the longest string.

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
   * **Vector**: The `std::vector` in C++ is a dynamic array that can resize itself automatically when needed. It provides constant time access to elements and amortized constant time insertion at the end.

   ```cpp
   #include <vector>
   std::vector<int> myVector;
   ```

2. **Linked Lists:**
   * **Singly Linked List**: Each element in the list contains a reference to the next element in the sequence.

   ```cpp
   struct Node {
       int data;
       Node* next;
   };
   ```

   * **Doubly Linked List**: Each element contains references to both the next and previous elements.

   ```cpp
   struct Node {
       int data;
       Node* prev;
       Node* next;
   };
   ```

3. **Forward List**:
   * `std::forward_list` is a singly linked list provided by the C++ standard library. It allows forward traversal only (from beginning to end) and does not support bidirectional traversal like the doubly linked list.

   ```cpp
   #include <forward_list>
   std::forward_list<int> myForwardList;
   ```

4. **Circular Linked List**:
   * In this list, the last node points back to the first node, forming a circle.

   ```cpp
   struct Node {
       int data;
       Node* next;
   };
   ```

5. **Other Implementations**:
   * Apart from the standard implementations, you can create your own custom implementations of lists based on the specific requirements of your application.

Each type of list has its own advantages and use cases. For example, arrays (like vectors) provide fast access to elements through indexing but may be inefficient for insertions and deletions at arbitrary positions. Linked lists, on the other hand, allow efficient insertions and deletions anywhere in the list but may have slower access times.

When choosing a list implementation, it's essential to consider the operations you'll perform most frequently and the performance characteristics of each implementation with respect to those operations.

### 1. Algorithms & Data Structures (C++): Loop detection

In the context of algorithms and data structures, loop detection typically refers to finding whether a linked list contains a cycle or loop. This problem is often encountered in computer science interviews and is crucial for understanding and implementing various algorithms involving linked lists.

Here's a common approach to detect loops in a linked list using C++:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* next;
    
    Node(int data) : data(data), next(nullptr) {}
};

bool hasCycle(Node* head) {
    if (head == nullptr || head->next == nullptr)
        return false; // No loop if list is empty or has only one node
    
    Node* slow = head;
    Node* fast = head->next;

    while (fast != nullptr && fast->next != nullptr) {
        if (slow == fast) {
            return true; // Loop detected
        }
        slow = slow->next;
        fast = fast->next->next;
    }

    return false; // No loop detected
}

int main() {
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->next = new Node(3);
    head->next->next->next = new Node(4);
    head->next->next->next->next = head; // Creating a cycle

    if (hasCycle(head)) {
        std::cout << "The linked list contains a cycle." << std::endl;
    } else {
        std::cout << "The linked list does not contain a cycle." << std::endl;
    }

    // Clean up memory (not necessary for demonstrating the algorithm)
    Node* current = head;
    while (current != nullptr) {
        Node* temp = current;
        current = current->next;
        delete temp;
    }

    return 0;
}
```

In this code:

* We use two pointers, `slow` and `fast`, to traverse the list. `slow` moves one step at a time, while `fast` moves two steps at a time.
* If there's a loop in the list, `slow` and `fast` pointers will eventually meet at some point.
* If there's no loop, `fast` will reach the end of the list (i.e., become `nullptr`) before `slow` reaches it.

This algorithm has a time complexity of O(n) and a space complexity of O(1), where n is the number of nodes in the linked list.

### 1. Algorithms & Data Structures (C++): Middle Element

To find the middle element of a singly linked list, you typically use two pointers: one slow pointer and one fast pointer. The slow pointer moves one step at a time, while the fast pointer moves two steps at a time. When the fast pointer reaches the end of the list, the slow pointer will be at the middle element.

Here's how you can implement this in C++:

```cpp
#include <iostream>

using namespace std;

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* findMiddle(ListNode* head) {
    if (head == nullptr) return nullptr; // Empty list
    ListNode* slow = head;
    ListNode* fast = head;
    
    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;
        fast = fast->next->next;
    }
    
    return slow;
}

int main() {
    // Example usage
    ListNode* head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);

    ListNode* middle = findMiddle(head);
    if (middle != nullptr)
        cout << "Middle element: " << middle->val << endl;
    else
        cout << "List is empty!" << endl;

    // Freeing memory
    while (head != nullptr) {
        ListNode* temp = head;
        head = head->next;
        delete temp;
    }
    
    return 0;
}
```

This code defines a `ListNode` struct representing nodes in the linked list, and a `findMiddle` function to find the middle element. The `main` function demonstrates how to use this function with an example linked list. Finally, it deallocates the memory allocated for the linked list to prevent memory leaks.

### 1. Algorithms & Data Structures (C++): Middle Node of List - Slow and Fast Pointer Approach

Certainly! The slow and fast pointer approach, also known as the tortoise and hare algorithm, is a widely used technique to find the middle node of a linked list. Here's how it works:

```cpp
#include <iostream>

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* middleNode(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;
    
    // Move 'fast' pointer two steps ahead and 'slow' pointer one step ahead
    // When 'fast' reaches the end, 'slow' will be at the middle.
    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;
        fast = fast->next->next;
    }
    
    return slow;
}

// Utility function to print the linked list
void printList(ListNode* head) {
    while (head != nullptr) {
        std::cout << head->val << " ";
        head = head->next;
    }
    std::cout << std::endl;
}

int main() {
    // Example usage
    ListNode* head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);

    std::cout << "Original list: ";
    printList(head);

    ListNode* middle = middleNode(head);
    std::cout << "Middle node value: " << middle->val << std::endl;

    return 0;
}
```

In this approach, we use two pointers, `slow` and `fast`, initially pointing to the head of the list. In each iteration of the loop, the `slow` pointer moves one step forward, while the `fast` pointer moves two steps forward. This way, when the `fast` pointer reaches the end of the list, the `slow` pointer will be at the middle node.

### 1. Algorithms & Data Structures (C++): Midpoint Linked List

Sure! Implementing a function to find the midpoint of a linked list in C++ involves using the slow and fast pointer approach. Here's how you can do it:

```cpp
#include <iostream>

using namespace std;

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

ListNode* findMidpoint(ListNode* head) {
    if (head == nullptr || head->next == nullptr) {
        return head; // If the list is empty or has only one node, return head
    }

    ListNode *slow = head;
    ListNode *fast = head;

    // Move fast pointer two steps at a time and slow pointer one step at a time
    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;
        fast = fast->next->next;
    }

    return slow; // Slow pointer will be at the midpoint when fast pointer reaches the end
}

// Utility function to print the linked list
void printList(ListNode *head) {
    while (head != nullptr) {
        cout << head->val << " ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    // Creating a sample linked list: 1->2->3->4->5
    ListNode *head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);

    cout << "Original Linked List: ";
    printList(head);

    ListNode *midpoint = findMidpoint(head);
    cout << "Midpoint of the Linked List: " << midpoint->val << endl;

    return 0;
}
```

In this code:

* We define a `ListNode` struct to represent each node of the linked list.
* The `findMidpoint` function takes the head of the linked list as input and returns a pointer to the midpoint node.
* We use the slow and fast pointer approach where the slow pointer moves one step at a time and the fast pointer moves two steps at a time. When the fast pointer reaches the end of the list, the slow pointer will be at the midpoint.
* The `printList` function is a utility function to print the linked list.
* In the `main` function, we create a sample linked list, print it, find the midpoint, and print the value of the midpoint node.

### 1. Algorithms & Data Structures (C++): Odd Even Linked List

An odd-even linked list problem involves rearranging a linked list such that all nodes with odd indices appear before nodes with even indices. Here's how you can implement this in C++:

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
    ListNode* oddEvenList(ListNode* head) {
        if (!head || !head->next)
            return head;

        ListNode* odd = head;
        ListNode* even = head->next;
        ListNode* evenHead = even;

        while (even && even->next) {
            odd->next = even->next;
            odd = odd->next;
            even->next = odd->next;
            even = even->next;
        }

        odd->next = evenHead;
        return head;
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
    // Create a sample linked list: 1->2->3->4->5
    ListNode* head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);

    Solution sol;
    ListNode* result = sol.oddEvenList(head);

    cout << "Original List: ";
    printList(head);

    cout << "Odd-Even List: ";
    printList(result);

    return 0;
}
```

In this solution:

* We iterate through the linked list, starting with the head.
* At each iteration, we move the odd-indexed nodes to the front and even-indexed nodes to the back.
* Finally, we connect the last odd node with the head of the even list to form a single list.

### 1. Algorithms & Data Structures (C++): Pairwise Swap of Adjacent Nodes using Links

Sure, here's an implementation in C++ for pairwise swapping of adjacent nodes in a linked list:

```cpp
#include <iostream>

// Define the structure for a node in the linked list
struct Node {
    int data;
    Node* next;
    
    Node(int value) : data(value), next(nullptr) {}
};

// Function to add a node at the end of the linked list
void append(Node* &head, int value) {
    Node* newNode = new Node(value);
    if (head == nullptr) {
        head = newNode;
        return;
    }
    Node* temp = head;
    while (temp->next != nullptr) {
        temp = temp->next;
    }
    temp->next = newNode;
}

// Function to swap nodes pairwise in a linked list
void pairwiseSwap(Node* &head) {
    if (head == nullptr || head->next == nullptr)
        return;
    
    Node* prev = head;
    Node* current = head->next;
    
    head = current; // New head of the list
    
    while (true) {
        Node* nextNode = current->next;
        current->next = prev;
        
        if (nextNode == nullptr || nextNode->next == nullptr) {
            prev->next = nextNode;
            break;
        }
        
        prev->next = nextNode->next;
        prev = nextNode;
        current = prev->next;
    }
}

// Function to print the linked list
void printList(Node* head) {
    while (head != nullptr) {
        std::cout << head->data << " ";
        head = head->next;
    }
    std::cout << std::endl;
}

// Function to delete the linked list to prevent memory leaks
void deleteList(Node* &head) {
    while (head != nullptr) {
        Node* temp = head;
        head = head->next;
        delete temp;
    }
}

int main() {
    // Example usage
    Node* head = nullptr;
    append(head, 1);
    append(head, 2);
    append(head, 3);
    append(head, 4);
    append(head, 5);
    
    std::cout << "Original list: ";
    printList(head);
    
    pairwiseSwap(head);
    
    std::cout << "List after pairwise swapping: ";
    printList(head);
    
    // Delete the list to free memory
    deleteList(head);
    
    return 0;
}
```

This code defines a basic singly linked list with nodes having integer data. The `pairwiseSwap` function swaps adjacent nodes pairwise in the list. The `append` function adds nodes to the end of the list, and the `printList` function prints the elements of the list. Finally, the `deleteList` function deletes the list to prevent memory leaks.

### 1. Algorithms & Data Structures (C++): Palindrome linked list

Sure! Implementing a palindrome checker for a linked list involves traversing the list efficiently while simultaneously checking if the elements form a palindrome. Here's a C++ implementation:

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
    bool isPalindrome(ListNode* head) {
        if (!head || !head->next)
            return true;
        
        // Find the middle of the linked list
        ListNode* slow = head;
        ListNode* fast = head;
        while (fast->next && fast->next->next) {
            slow = slow->next;
            fast = fast->next->next;
        }
        
        // Reverse the second half of the linked list
        ListNode* prev = nullptr;
        ListNode* curr = slow->next;
        while (curr) {
            ListNode* nextTemp = curr->next;
            curr->next = prev;
            prev = curr;
            curr = nextTemp;
        }
        
        // Compare the first half and reversed second half
        ListNode* p1 = head;
        ListNode* p2 = prev;
        while (p2) {
            if (p1->val != p2->val)
                return false;
            p1 = p1->next;
            p2 = p2->next;
        }
        return true;
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
    // Example usage
    ListNode* head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(2);
    head->next->next->next->next = new ListNode(1);

    Solution solution;
    cout << "Original List: ";
    printList(head);
    if (solution.isPalindrome(head))
        cout << "The list is a palindrome.\n";
    else
        cout << "The list is not a palindrome.\n";

    // Free memory
    while (head) {
        ListNode* temp = head;
        head = head->next;
        delete temp;
    }
    
    return 0;
}
```

This code first finds the middle of the linked list using the slow and fast pointer technique. Then, it reverses the second half of the list. Finally, it compares the first half with the reversed second half to determine if the linked list is a palindrome or not.

### 1. Algorithms & Data Structures (C++): Palindrome linked list: Complexity analysis

To analyze the complexity of checking whether a linked list is a palindrome in C++, let's break down the process into steps:

1. **Reverse the second half of the linked list**: To check if a linked list is a palindrome, we need to compare the first half of the list with the reversed second half. So, first, we need to find the midpoint of the list and then reverse the second half of the list.

2. **Compare the first half with the reversed second half**: Once we have the reversed second half of the list, we can start comparing it with the first half. If every element matches, the list is a palindrome.

Let's analyze the complexity of each step:

1. **Finding the midpoint and reversing the second half**:
   * Finding the midpoint: To find the midpoint, we need to traverse the list once, which takes O(n) time, where n is the number of elements in the list.
   * Reversing the second half: Reversing a linked list requires traversing the second half once, which also takes O(n/2) time.
   * So, the total time complexity for this step is O(n/2) + O(n) ≈ O(n).

2. **Comparing the first half with the reversed second half**:
   * To compare the first half with the reversed second half, we need to traverse both halves once, which takes O(n/2) + O(n/2) = O(n) time.

Therefore, the overall time complexity of checking whether a linked list is a palindrome using this approach is O(n).

In terms of space complexity, we are not using any additional data structures apart from a few pointers, so the space complexity is O(1).

This analysis assumes a singly linked list. If it's a doubly linked list, the reversal step would be simpler, but the overall complexity would still remain O(n).

### 1. Algorithms & Data Structures (C++): Palindrome Linked Lists - Linked List

Sure, implementing a function to check if a linked list is a palindrome in C++ is an interesting problem. Here's how you could approach it:

```cpp
#include <iostream>
#include <stack>

using namespace std;

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

bool isPalindrome(ListNode* head) {
    if (!head || !head->next)
        return true;
    
    // Find the middle of the linked list
    ListNode* slow = head;
    ListNode* fast = head;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
    }
    
    // Reverse the second half of the linked list
    ListNode* prev = nullptr;
    ListNode* curr = slow;
    ListNode* next = nullptr;
    while (curr) {
        next = curr->next;
        curr->next = prev;
        prev = curr;
        curr = next;
    }
    
    // Compare the first and second halves
    ListNode* firstHalf = head;
    ListNode* secondHalf = prev;
    while (secondHalf) {
        if (firstHalf->val != secondHalf->val)
            return false;
        firstHalf = firstHalf->next;
        secondHalf = secondHalf->next;
    }
    
    return true;
}

// Function to print the linked list
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
    head->next->next->next = new ListNode(2);
    head->next->next->next->next = new ListNode(1);
    
    cout << "Original list: ";
    printList(head);
    
    if (isPalindrome(head))
        cout << "The linked list is a palindrome." << endl;
    else
        cout << "The linked list is not a palindrome." << endl;
    
    // Free memory
    while (head != nullptr) {
        ListNode* temp = head;
        head = head->next;
        delete temp;
    }
    
    return 0;
}
```

This code defines a linked list structure (`ListNode`) and implements a function `isPalindrome` to check if the given linked list is a palindrome. It uses the approach of reversing the second half of the linked list and then comparing it with the first half. The function `printList` is just a utility function to print the linked list elements, and the `main` function demonstrates its usage with an example.

### 1. Algorithms & Data Structures (C++): Recursive Display for Linked List

Sure! In C++, you can implement a recursive function to display the elements of a linked list. Here's an example implementation:

```cpp
#include <iostream>

// Node structure for the linked list
struct Node {
    int data;
    Node* next;
    
    Node(int val) : data(val), next(nullptr) {}
};

// Function to recursively display the linked list
void displayList(Node* head) {
    // Base case: If the current node is null, return
    if (head == nullptr)
        return;

    // Display the data of the current node
    std::cout << head->data << " ";

    // Recursively call the function for the next node
    displayList(head->next);
}

int main() {
    // Create a sample linked list: 1 -> 2 -> 3 -> 4 -> 5
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->next = new Node(3);
    head->next->next->next = new Node(4);
    head->next->next->next->next = new Node(5);

    // Display the linked list
    std::cout << "Linked List: ";
    displayList(head);
    std::cout << std::endl;

    // Clean up memory (deallocation)
    Node* current = head;
    while (current != nullptr) {
        Node* temp = current;
        current = current->next;
        delete temp;
    }

    return 0;
}
```

In this example, the `displayList()` function takes the head of the linked list as an argument and recursively displays each node's data. The function stops when it reaches the end of the list (when the current node is `nullptr`). Finally, in the `main()` function, a sample linked list is created and displayed using the `displayList()` function, followed by memory deallocation to prevent memory leaks.

### 1. Algorithms & Data Structures (C++): Recursive Display of Linked List

Sure! Below is an example of how you can recursively display the elements of a linked list in C++:

```cpp
#include <iostream>

// Define the structure of a node in the linked list
struct Node {
    int data;
    Node* next;
    
    Node(int val) : data(val), next(nullptr) {}
};

// Function to recursively display the linked list
void displayLinkedList(Node* head) {
    if (head == nullptr) {
        // Base case: if the current node is nullptr, return
        return;
    }
    
    // Display the data of the current node
    std::cout << head->data << " ";
    
    // Recursively call the function for the next node
    displayLinkedList(head->next);
}

int main() {
    // Create a sample linked list: 1 -> 2 -> 3 -> 4 -> 5
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->next = new Node(3);
    head->next->next->next = new Node(4);
    head->next->next->next->next = new Node(5);
    
    // Display the linked list recursively
    std::cout << "Linked List: ";
    displayLinkedList(head);
    
    // Cleanup: delete the allocated memory
    Node* current = head;
    while (current != nullptr) {
        Node* temp = current;
        current = current->next;
        delete temp;
    }
    
    return 0;
}
```

This code defines a basic linked list structure and a function `displayLinkedList` that recursively displays the elements of the linked list. The `main` function creates a sample linked list and calls the display function. Finally, it cleans up the memory by deleting the allocated nodes.

### 1. Algorithms & Data Structures (C++): Remove Loop (Cycle) from Linked List

Removing a loop or cycle from a linked list involves detecting the loop and then breaking the cycle at some point. One common algorithm to achieve this is called Floyd's Cycle Detection Algorithm, also known as the "tortoise and hare" algorithm. Here's how it works:

1. Use two pointers, often referred to as slow and fast pointers, initially pointing to the head of the linked list.
2. Move the slow pointer one step at a time and the fast pointer two steps at a time.
3. If the slow pointer and fast pointer meet at some point, it indicates the presence of a cycle.
4. Once the cycle is detected, reset one of the pointers to the head of the list and move both pointers one step at a time until they meet again. The meeting point is the start of the cycle.
5. Break the cycle by setting the next pointer of the node before the meeting point to null.

Here's the C++ implementation:

```cpp
#include <iostream>

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

class Solution {
public:
    void removeCycle(ListNode *head) {
        if (!head || !head->next)
            return;

        // Detect cycle using Floyd's Cycle Detection Algorithm
        ListNode *slow = head, *fast = head;
        while (fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
            if (slow == fast)
                break;
        }

        // If no cycle found
        if (slow != fast)
            return;

        // Move one pointer back to the head
        slow = head;

        // Find the start of the cycle
        while (slow != fast) {
            slow = slow->next;
            fast = fast->next;
        }

        // Break the cycle
        ListNode *prev = nullptr;
        while (head != slow) {
            prev = slow;
            slow = slow->next;
            head = head->next;
        }
        // prev now points to the node before the start of the cycle
        prev->next = nullptr;
    }
};

// Utility function to print the linked list
void printList(ListNode *head) {
    while (head) {
        std::cout << head->val << " -> ";
        head = head->next;
    }
    std::cout << "nullptr" << std::endl;
}

int main() {
    // Creating a sample linked list with a cycle
    ListNode *head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = head->next; // Creating a cycle

    Solution sol;
    sol.removeCycle(head);

    std::cout << "Linked list after removing the cycle:" << std::endl;
    printList(head);

    // Clean up memory
    while (head) {
        ListNode *temp = head;
        head = head->next;
        delete temp;
    }

    return 0;
}
```

This implementation first detects the cycle using Floyd's algorithm, then finds the start of the cycle, and finally breaks the cycle.

### 1. Algorithms & Data Structures (C++): Sort linked list

Certainly! Here's an implementation of sorting a linked list using the Merge Sort algorithm in C++:

```cpp
#include <iostream>

using namespace std;

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

// Function to merge two sorted linked lists
ListNode* merge(ListNode* l1, ListNode* l2) {
    if (!l1) return l2;
    if (!l2) return l1;

    if (l1->val < l2->val) {
        l1->next = merge(l1->next, l2);
        return l1;
    } else {
        l2->next = merge(l1, l2->next);
        return l2;
    }
}

// Function to perform merge sort on a linked list
ListNode* sortList(ListNode* head) {
    // Base case: if the list is empty or has only one element
    if (!head || !head->next) return head;

    // Find the middle of the list
    ListNode *slow = head, *fast = head->next;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
    }

    ListNode* secondHalf = slow->next;
    slow->next = nullptr;

    // Recursively sort the two halves
    ListNode* firstHalf = sortList(head);
    secondHalf = sortList(secondHalf);

    // Merge the sorted halves
    return merge(firstHalf, secondHalf);
}

// Function to print a linked list
void printList(ListNode* head) {
    while (head) {
        cout << head->val << " ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    // Example usage
    ListNode* head = new ListNode(4);
    head->next = new ListNode(2);
    head->next->next = new ListNode(1);
    head->next->next->next = new ListNode(3);

    cout << "Original list: ";
    printList(head);

    head = sortList(head);

    cout << "Sorted list: ";
    printList(head);

    return 0;
}
```

This code defines a linked list structure `ListNode` and implements the Merge Sort algorithm to sort the linked list. The `sortList` function recursively divides the list into halves, sorts them individually, and then merges them back together. Finally, the `printList` function is used to print the sorted list.

### 1. Algorithms & Data Structures (C++): Sort linked list: Complexity analysis

Sorting a linked list involves rearranging its elements so that they are in a specific order, typically non-decreasing or non-increasing. Several sorting algorithms can be applied to linked lists, each with its own time and space complexities. Let's analyze the complexity of sorting a linked list using various sorting algorithms:

1. **Insertion Sort**:
   * Time Complexity: \(O(n^2)\) in the worst-case scenario. Since insertion sort iterates over each element in the list and potentially swaps it with preceding elements, the time complexity is quadratic.
   * Space Complexity: \(O(1)\). Insertion sort typically performs sorting in place without requiring additional space.

2. **Selection Sort**:
   * Time Complexity: \(O(n^2)\) in all cases. Selection sort also iterates over the list, but in each iteration, it finds the minimum element and places it at the beginning, which requires \(O(n)\) comparisons for each element.
   * Space Complexity: \(O(1)\). Similar to insertion sort, selection sort operates in place.

3. **Merge Sort**:
   * Time Complexity: \(O(n \log n)\). Merge sort consistently exhibits this time complexity, even for linked lists. It recursively divides the list into halves until each sublist contains only one element, then merges the sorted sublists.
   * Space Complexity: \(O(\log n)\). Merge sort typically requires additional space for recursion stack due to its divide-and-conquer approach.

4. **Quick Sort**:
   * Time Complexity: \(O(n \log n)\) on average case, but \(O(n^2)\) in the worst case. Quick sort's time complexity depends on the choice of the pivot element. In the worst-case scenario, the pivot is either the smallest or largest element, resulting in unbalanced partitioning.
   * Space Complexity: \(O(\log n)\) on average. Similar to merge sort, quick sort also requires additional space for recursion stack.

5. **Heap Sort**:
   * Time Complexity: \(O(n \log n)\) in all cases. Heap sort first builds a max-heap from the elements and then repeatedly extracts the maximum element from the heap, resulting in sorted order.
   * Space Complexity: \(O(1)\). Unlike merge sort and quick sort, heap sort doesn't require additional space proportional to the input size.

Among these algorithms, merge sort and heap sort are more efficient for linked lists due to their consistent \(O(n \log n)\) time complexity and space efficiency. However, merge sort is preferred over heap sort for linked lists because it's stable and doesn't rely on random access, which is not a natural operation for linked lists.

### 1. Algorithms & Data Structures (C++): Sorted Linked Lists

Sorted linked lists are a fundamental data structure in computer science, especially for maintaining a sorted collection of elements efficiently. In C++, you can implement a sorted linked list by ensuring that elements are inserted into the list in a sorted order.

Here's a basic implementation of a sorted linked list in C++:

```cpp
#include <iostream>

// Node class represents each element in the linked list
class Node {
public:
    int data;
    Node* next;

    Node(int value) {
        data = value;
        next = nullptr;
    }
};

// SortedLinkedList class represents the sorted linked list
class SortedLinkedList {
private:
    Node* head;

public:
    SortedLinkedList() {
        head = nullptr;
    }

    // Function to insert a new node with given value into the sorted linked list
    void insert(int value) {
        Node* newNode = new Node(value);
        
        // If the list is empty or the new node's value is less than the head's value
        if (head == nullptr || value < head->data) {
            newNode->next = head;
            head = newNode;
        } else {
            Node* current = head;
            while (current->next != nullptr && current->next->data < value) {
                current = current->next;
            }
            newNode->next = current->next;
            current->next = newNode;
        }
    }

    // Function to display the sorted linked list
    void display() {
        Node* current = head;
        while (current != nullptr) {
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }
};

int main() {
    SortedLinkedList list;

    // Insert elements into the sorted linked list
    list.insert(5);
    list.insert(10);
    list.insert(2);
    list.insert(8);

    // Display the sorted linked list
    std::cout << "Sorted Linked List: ";
    list.display();

    return 0;
}
```

In this implementation:

* The `Node` class represents each element in the linked list.
* The `SortedLinkedList` class manages the linked list and provides functions to insert elements into the list while maintaining the sorted order.
* The `insert` function inserts a new node with the given value into the sorted linked list.
* The `display` function prints the elements of the sorted linked list.

This implementation ensures that elements are inserted into the list in such a way that the list remains sorted at all times.

## Cycle Detection

### 1. Algorithms & Data Structures (C++): Detect Cycle in a Linked List

Detecting a cycle in a linked list is a classic problem that can be efficiently solved using Floyd’s Cycle-Finding Algorithm, also known as the Tortoise and Hare algorithm. This algorithm uses two pointers moving at different speeds to detect a cycle.

Here’s a step-by-step guide and a C++ implementation to detect a cycle in a singly linked list:

### Steps

1. **Initialize Two Pointers:** Start with two pointers, both at the head of the linked list. Let’s call them `slow` and `fast`.
2. **Move the Pointers:** Move `slow` one step at a time and `fast` two steps at a time.
3. **Check for Cycle:**
   * If `fast` or `fast->next` becomes `NULL`, it means there is no cycle (since the end of the list is reached).
   * If `slow` and `fast` meet at some point, then there is a cycle in the list.
4. **Return Result:** If the pointers meet, return `true`. If `fast` reaches the end, return `false`.

### C++ Implementation

```cpp
#include <iostream>

struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

bool hasCycle(ListNode *head) {
    if (!head) return false;
    
    ListNode *slow = head;
    ListNode *fast = head;
    
    while (fast && fast->next) {
        slow = slow->next;           // Move slow pointer by 1
        fast = fast->next->next;     // Move fast pointer by 2
        
        if (slow == fast) {
            return true;             // Cycle detected
        }
    }
    
    return false;                    // No cycle
}

int main() {
    // Example usage:
    ListNode *head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = head->next; // Creates a cycle

    if (hasCycle(head)) {
        std::cout << "Cycle detected in the linked list." << std::endl;
    } else {
        std::cout << "No cycle in the linked list." << std::endl;
    }
    
    // Remember to free the allocated memory in a real application to avoid memory leaks
    // For this example, we are assuming the program ends here and OS cleans up the memory
    return 0;
}
```

### Explanation

* **ListNode Structure:** A simple structure representing a node in the linked list.
* **hasCycle Function:** Implements the Tortoise and Hare algorithm.
  * **Edge Case Check:** If the list is empty (`head == nullptr`), return `false`.
  * **Pointer Initialization:** Both `slow` and `fast` are initialized to the head of the list.
  * **Cycle Detection Loop:** `slow` moves one step, `fast` moves two steps in each iteration. If they meet, a cycle is detected.
  * **End of List Check:** If `fast` or `fast->next` becomes `NULL`, it means there’s no cycle.

### Usage

In the `main` function, we create a linked list with a cycle and check if the `hasCycle` function correctly identifies it. If a cycle is detected, it prints a message indicating so; otherwise, it indicates no cycle is present.

This approach ensures O(n) time complexity with O(1) space complexity, making it efficient and suitable for large linked lists.

## Problems

### 1. Algorithms & Data Structures (C++): Linked List Problems

Certainly! Linked lists are a fundamental data structure in computer science, and there are several common problems and exercises associated with them. Here are a few typical linked list problems along with their solutions in C++:

1. **Reverse a Linked List:**
2. **Detect a Cycle in a Linked List:**
3. **Find the Middle of a Linked List:**
4. **Merge Two Sorted Lists:**
5. **Remove Nth Node From End of List:**
6. **Removing Duplicates**
7. **Intersection Point**

## Reversing

### 1. Algorithms & Data Structures (C++): Linked List: Reversing a Linked List : Recursive Approach

Reversing a linked list using a recursive approach in C++ involves changing the direction of the links between nodes. Here is a step-by-step explanation and implementation of the recursive approach:

#### Step-by-Step Explanation

1. **Base Case**: If the list is empty (head is `nullptr`) or it has only one node (head's next is `nullptr`), return the head. This is the termination condition for the recursion.

2. **Recursive Step**: Reverse the rest of the list beyond the head. To do this, call the reverse function on the next node of the head.

3. **Re-linking**: Once the rest of the list is reversed, the next node (head->next) should point back to the head. Adjust the links to achieve this.

4. **Final Adjustment**: Make sure to set the head's next pointer to `nullptr` to finalize the reversal for the original head node.

#### Implementation in C++

Here is a C++ implementation of reversing a linked list recursively:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

class LinkedList {
public:
    Node* head;

    LinkedList() : head(nullptr) {}

    void append(int data) {
        if (head == nullptr) {
            head = new Node(data);
            return;
        }
        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = new Node(data);
    }

    void printList() {
        Node* temp = head;
        while (temp != nullptr) {
            std::cout << temp->data << " -> ";
            temp = temp->next;
        }
        std::cout << "nullptr" << std::endl;
    }

    Node* reverseList(Node* node) {
        // Base case: if head is empty or has reached the list end
        if (node == nullptr || node->next == nullptr) {
            return node;
        }

        // Recursively reverse the rest of the list
        Node* newHead = reverseList(node->next);

        // Adjust the next pointers
        node->next->next = node;
        node->next = nullptr;

        return newHead;
    }

    void reverse() {
        head = reverseList(head);
    }
};

int main() {
    LinkedList list;
    list.append(1);
    list.append(2);
    list.append(3);
    list.append(4);
    list.append(5);

    std::cout << "Original List: ";
    list.printList();

    list.reverse();

    std::cout << "Reversed List: ";
    list.printList();

    return 0;
}
```

#### Explanation of the Code

1. **Node Structure**: The `Node` structure holds the data and a pointer to the next node.

2. **LinkedList Class**:
    * `append(int data)`: Adds a new node with the given data at the end of the list.
    * `printList()`: Prints the linked list.
    * `reverseList(Node* node)`: Recursively reverses the linked list starting from the given node.
    * `reverse()`: A wrapper function that calls `reverseList` starting from the head of the list.

3. **Main Function**:
    * Creates a linked list and appends some nodes.
    * Prints the original list.
    * Calls the `reverse` function to reverse the list.
    * Prints the reversed list.

This approach leverages recursion to reverse the linked list by reversing the smaller sublists until the entire list is reversed. The use of recursion simplifies the code by handling the state through recursive calls rather than explicit loops and stack management.

#### Time Complexity

The time complexity of the recursive approach to reverse a linked list is \( O(n) \), where \( n \) is the number of nodes in the linked list. This is because:

1. **Traversal**: Each node is visited exactly once. During the recursion, we traverse each node from the head to the last node.
2. **Link Adjustments**: Each node has its link adjusted exactly once.

Thus, the total number of operations is proportional to the number of nodes, leading to a time complexity of \( O(n) \).

#### Space Complexity

The space complexity of this approach is \( O(n) \) due to the recursion stack. Here’s why:

1. **Recursive Calls**: For each node in the list, a recursive call is made. This results in a call stack that grows linearly with the number of nodes.
2. **Stack Frames**: Each recursive call consumes a stack frame. Since the maximum depth of the recursion is \( n \), the total space used by the recursion stack is \( O(n) \).

#### Summary

* **Time Complexity**: \( O(n) \)
* **Space Complexity**: \( O(n) \)

This space complexity is a key characteristic of the recursive approach, as it uses additional space on the call stack. In contrast, an iterative approach to reverse the linked list would have a space complexity of \( O(1) \), as it doesn't require additional stack frames.

### 1. Algorithms & Data Structures (C++): Linked List: Reversing a Linked List : Iterative Approach

Reversing a linked list is a common problem that can be solved using an iterative approach. Below is a step-by-step explanation and implementation of how to reverse a singly linked list in C++.

#### Steps to Reverse a Linked List Iteratively

1. **Initialize Pointers**: You need three pointers to keep track of nodes during the reversal process.
   * `prev` to store the previous node, initialized to `nullptr`.
   * `current` to store the current node, initialized to the head of the list.
   * `next` to store the next node, initialized to `nullptr`.

2. **Iterate Through the List**: Loop through the list until `current` becomes `nullptr`.
   * Inside the loop, perform the following steps:
     1. Save the next node: `next = current->next`.
     2. Reverse the link: `current->next = prev`.
     3. Move `prev` and `current` one step forward:
        * `prev = current`
        * `current = next`

3. **Update Head**: After the loop, `prev` will be pointing to the new head of the reversed list. Update the head of the list to `prev`.

#### Implementation in C++

Here's how you can implement this:

```cpp
#include <iostream>

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
};

class LinkedList {
public:
    // Function to reverse the linked list
    ListNode* reverseList(ListNode* head) {
        ListNode* prev = nullptr;
        ListNode* current = head;
        ListNode* next = nullptr;

        while (current != nullptr) {
            // Save the next node
            next = current->next;
            // Reverse the link
            current->next = prev;
            // Move forward in the list
            prev = current;
            current = next;
        }

        // Update head to the new front of the list
        return prev;
    }

    // Function to print the linked list
    void printList(ListNode* head) {
        ListNode* temp = head;
        while (temp != nullptr) {
            std::cout << temp->val << " ";
            temp = temp->next;
        }
        std::cout << std::endl;
    }
};

int main() {
    // Create a sample list: 1 -> 2 -> 3 -> 4 -> 5
    ListNode* head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);

    LinkedList ll;
    std::cout << "Original List: ";
    ll.printList(head);

    head = ll.reverseList(head);

    std::cout << "Reversed List: ";
    ll.printList(head);

    // Clean up the memory
    ListNode* current = head;
    while (current != nullptr) {
        ListNode* next = current->next;
        delete current;
        current = next;
    }

    return 0;
}
```

#### Explanation

1. **ListNode Struct**: Defines the structure of a node in the linked list.
2. **LinkedList Class**: Contains the `reverseList` method which performs the iterative reversal of the list and a `printList` method to print the list.
3. **reverseList Function**:
   * `prev`, `current`, and `next` pointers are used for the reversal.
   * The while loop continues until `current` becomes `nullptr`.
   * In each iteration, the link of the `current` node is reversed, and the pointers are updated to move forward.
4. **printList Function**: Iterates through the list and prints each node's value.
5. **main Function**: Demonstrates the creation of a linked list, reversing it, and then printing both the original and reversed lists. It also ensures that the dynamically allocated memory is freed at the end.

This code provides a complete example of how to reverse a singly linked list using an iterative approach in C++.

#### Time Complexity

1. **Traversal**: The algorithm iterates through each node of the linked list exactly once. Therefore, the time complexity for traversal is O(n), where n is the number of nodes in the linked list.
2. **Reversal**: Within the traversal, for each node, the algorithm performs constant-time operations like updating pointers. Hence, the time complexity for reversal is also O(n).

Thus, the overall time complexity of the iterative approach to reverse a linked list is O(n).

#### Space Complexity

The iterative approach doesn't use any additional data structures proportional to the size of the input. It only requires a constant amount of extra space for storing pointers. So, the space complexity is O(1), indicating that it's constant space complexity regardless of the size of the linked list.

In summary, the time complexity is O(n) and the space complexity is O(1) for the iterative approach to reverse a linked list.

### 1. Algorithms & Data Structures (C++): Linked List: M, N Reversals

Reversing parts of a linked list, sometimes referred to as "M, N reversals," involves dividing the list into segments of length M and reversing each segment separately. This process is then repeated for segments of length N, until the end of the list is reached. Here's a C++ implementation to achieve this:

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
    ListNode* reverseBetween(ListNode* head, int m, int n) {
        if (head == nullptr || m >= n) return head;

        // Dummy node to simplify edge cases
        ListNode *dummy = new ListNode(0);
        dummy->next = head;
        ListNode *prev = dummy;

        // Move prev to the node before the segment to reverse
        for (int i = 0; i < m - 1; ++i) {
            if (prev == nullptr) return head;
            prev = prev->next;
        }

        // Initialize pointers for reversing the segment
        ListNode *start = prev->next;
        ListNode *then = start->next;

        // Reverse the segment
        for (int i = 0; i < n - m; ++i) {
            if (then == nullptr) break;
            start->next = then->next;
            then->next = prev->next;
            prev->next = then;
            then = start->next;
        }

        return dummy->next;
    }
};

// Utility function to print the linked list
void printList(ListNode *head) {
    while (head != nullptr) {
        cout << head->val << " ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    // Example usage
    ListNode *head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);

    cout << "Original list: ";
    printList(head);

    Solution sol;
    int m = 2, n = 4;
    head = sol.reverseBetween(head, m, n);

    cout << "List after reversing from position " << m << " to " << n << ": ";
    printList(head);

    return 0;
}
```

In this implementation:

* We iterate through the list to find the node before the segment to be reversed.
* Then, we reverse the segment of the list defined by the indices `m` and `n`.
* We update the pointers accordingly to perform the reversal.
* Finally, we return the modified list.

You can customize `m` and `n` in the `main` function to reverse different segments of the list.

### 1. Algorithms & Data Structures (C++): K-Reverse a Linked List

Certainly! Reversing a linked list in groups of K is a common problem in data structures. Here's how you can implement it in C++:

```cpp
#include <iostream>

using namespace std;

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* reverseKGroup(ListNode* head, int k) {
    ListNode* curr = head;
    int count = 0;
    while (curr != nullptr && count < k) {
        curr = curr->next;
        count++;
    }
    if (count == k) {
        // Reverse the first K nodes of the linked list
        curr = reverseKGroup(curr, k);
        while (count-- > 0) {
            ListNode* temp = head->next;
            head->next = curr;
            curr = head;
            head = temp;
        }
        head = curr;
    }
    return head;
}

// Utility function to print the linked list
void printList(ListNode* node) {
    while (node != nullptr) {
        cout << node->val << " ";
        node = node->next;
    }
    cout << endl;
}

int main() {
    // Create a linked list: 1->2->3->4->5->6->7->8->9
    ListNode* head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);
    head->next->next->next->next->next = new ListNode(6);
    head->next->next->next->next->next->next = new ListNode(7);
    head->next->next->next->next->next->next->next = new ListNode(8);
    head->next->next->next->next->next->next->next->next = new ListNode(9);

    int k = 3; // K value for reversing

    cout << "Original Linked List: ";
    printList(head);

    head = reverseKGroup(head, k);

    cout << "Reversed Linked List in groups of " << k << ": ";
    printList(head);

    return 0;
}
```

This code defines a `ListNode` struct for creating a singly-linked list and implements the `reverseKGroup` function to reverse the list in groups of size K. The `main` function demonstrates its usage by creating a linked list and then reversing it in groups of 3.

### 1. Algorithms & Data Structures (C++): Linked List: Reverse Between

Certainly! Implementing a function to reverse a linked list between two specified positions involves a few steps:

1. Traverse the list to reach the node just before the starting position.
2. Reverse the sublist between the given positions.
3. Update the pointers of the surrounding nodes to maintain the integrity of the list.

Here's a C++ implementation:

```cpp
#include <iostream>

struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* reverseBetween(ListNode* head, int m, int n) {
    if (head == nullptr || m == n) return head;

    ListNode* dummy = new ListNode(0);
    dummy->next = head;
    ListNode* preStart = dummy;

    // Move preStart to the node just before the sublist to be reversed
    for (int i = 0; i < m - 1; ++i)
        preStart = preStart->next;

    ListNode* start = preStart->next;
    ListNode* then = start->next;

    // Reverse the sublist from m to n
    for (int i = 0; i < n - m; ++i) {
        start->next = then->next;
        then->next = preStart->next;
        preStart->next = then;
        then = start->next;
    }

    return dummy->next;
}

void printList(ListNode* head) {
    while (head != nullptr) {
        std::cout << head->val << " ";
        head = head->next;
    }
    std::cout << std::endl;
}

int main() {
    // Example usage
    ListNode* head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);

    std::cout << "Original list: ";
    printList(head);

    int m = 2, n = 4;
    head = reverseBetween(head, m, n);

    std::cout << "List after reversing from position " << m << " to " << n << ": ";
    printList(head);

    return 0;
}
```

This code snippet demonstrates the implementation of the `reverseBetween` function, which takes a linked list `head` and two integers `m` and `n` representing the positions to reverse between. It returns the head of the modified list after reversing the sublist between positions `m` and `n`.

## Interview qustions

### 1. Algorithms & Data Structures (C++): Linked Lists: From Last

In C++, to find the kth element from the end of a singly linked list efficiently, you can use a two-pointer technique. Here's a simple approach:

1. Maintain two pointers, let's call them `fast` and `slow`, initialized to the head of the linked list.
2. Move the `fast` pointer k steps ahead.
3. Then move both `fast` and `slow` pointers simultaneously until `fast` reaches the end of the list.
4. At this point, `slow` will be pointing to the kth element from the end.

Here's how you can implement it:

```cpp
#include <iostream>

using namespace std;

// Node structure
struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

// Function to find the kth element from the end of a linked list
Node* kthFromEnd(Node* head, int k) {
    if (head == nullptr || k <= 0) return nullptr;

    Node* fast = head;
    Node* slow = head;

    // Move fast k steps ahead
    for (int i = 0; i < k; ++i) {
        if (fast == nullptr) return nullptr; // If k is greater than the length of the list
        fast = fast->next;
    }

    // Move both fast and slow pointers simultaneously until fast reaches the end
    while (fast != nullptr) {
        fast = fast->next;
        slow = slow->next;
    }

    return slow;
}

// Function to print the linked list
void printList(Node* head) {
    while (head != nullptr) {
        cout << head->data << " ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    // Creating a sample linked list: 1 -> 2 -> 3 -> 4 -> 5
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->next = new Node(3);
    head->next->next->next = new Node(4);
    head->next->next->next->next = new Node(5);

    cout << "Original linked list: ";
    printList(head);

    int k = 2;
    Node* kth = kthFromEnd(head, k);
    if (kth != nullptr) {
        cout << "The " << k << "th element from the end is: " << kth->data << endl;
    } else {
        cout << "The linked list is too short or invalid value of k." << endl;
    }

    return 0;
}
```

In this example, `k` is set to 2, so it will find the second element from the end of the linked list. You can adjust `k` to find any kth element from the end.

## Merge Sorted

### 1. Algorithms & Data Structures (C++): Merge Sorted Linked Lists

Certainly! Merging two sorted linked lists in C++ involves creating a new sorted list by iterating through both input lists simultaneously, comparing elements, and appending the smaller one to the new list. Here's an implementation:

```cpp
#include <iostream>

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
        ListNode* current = dummy;

        // Merge the lists until one of them is exhausted
        while (l1 != nullptr && l2 != nullptr) {
            if (l1->val < l2->val) {
                current->next = l1;
                l1 = l1->next;
            } else {
                current->next = l2;
                l2 = l2->next;
            }
            current = current->next;
        }

        // Append the remaining nodes of the non-empty list
        current->next = (l1 != nullptr) ? l1 : l2;

        // Store the head of the merged list
        ListNode* result = dummy->next;

        // Clean up dummy node
        delete dummy;

        return result;
    }
};

// Helper function to print a linked list
void printList(ListNode* head) {
    while (head != nullptr) {
        std::cout << head->val << " ";
        head = head->next;
    }
    std::cout << std::endl;
}

int main() {
    // Create two sorted linked lists
    ListNode* l1 = new ListNode(1);
    l1->next = new ListNode(3);
    l1->next->next = new ListNode(5);

    ListNode* l2 = new ListNode(2);
    l2->next = new ListNode(4);
    l2->next->next = new ListNode(6);

    // Merge the lists
    Solution solution;
    ListNode* mergedList = solution.mergeTwoLists(l1, l2);

    // Print the merged list
    std::cout << "Merged List: ";
    printList(mergedList);

    // Clean up memory
    while (mergedList != nullptr) {
        ListNode* temp = mergedList;
        mergedList = mergedList->next;
        delete temp;
    }

    return 0;
}
```

This code creates two sorted linked lists `l1` and `l2`, merges them using the `mergeTwoLists` function, and then prints the merged list. Finally, it deallocates the memory allocated for the linked lists.

### 1. Algorithms & Data Structures (C++): Linked List: Alternate Merge

To merge two linked lists alternately in C++, you'll need to iterate through both lists, taking one element from each list alternately and appending it to the result list. If one list is longer than the other, append the remaining elements of the longer list to the result list.

Here's a basic implementation:

```cpp
#include <iostream>

using namespace std;

// Node structure for a linked list
struct Node {
    int data;
    Node* next;
    
    Node(int val) : data(val), next(nullptr) {}
};

// Function to insert a new node at the end of a linked list
void insert(Node*& head, int val) {
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

// Function to merge two linked lists alternately
Node* alternateMerge(Node* head1, Node* head2) {
    if (!head1) return head2;
    if (!head2) return head1;
    
    Node* merged = nullptr;
    Node* tail = nullptr;
    while (head1 && head2) {
        if (!merged) {
            merged = head1;
            tail = merged;
            head1 = head1->next;
        } else {
            tail->next = head2;
            tail = tail->next;
            head2 = head2->next;
            tail->next = head1;
            tail = tail->next;
            head1 = head1->next;
        }
    }
    
    if (head1) tail->next = head1;
    if (head2) tail->next = head2;
    
    return merged;
}

// Function to print a linked list
void printList(Node* head) {
    while (head) {
        cout << head->data << " ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    Node* head1 = nullptr;
    Node* head2 = nullptr;
    
    // Insert elements into the first linked list
    insert(head1, 1);
    insert(head1, 3);
    insert(head1, 5);
    
    // Insert elements into the second linked list
    insert(head2, 2);
    insert(head2, 4);
    insert(head2, 6);
    insert(head2, 8);
    
    cout << "First List: ";
    printList(head1);
    cout << "Second List: ";
    printList(head2);
    
    Node* merged = alternateMerge(head1, head2);
    
    cout << "Merged List: ";
    printList(merged);
    
    return 0;
}
```

In this implementation, `alternateMerge` takes two linked lists as input and returns a new linked list that contains elements alternately merged from both input lists. The `printList` function is just a utility function to print the contents of a linked list.

## Middle point

### 1. Algorithms & Data Structures (C++): Linked List: Find Middle Node

To find the middle node of a linked list in C++, you can use the slow and fast pointer technique. Here's how it works:

1. Initialize two pointers, `slow` and `fast`, both pointing to the head of the linked list.
2. Move the `fast` pointer twice as fast as the `slow` pointer. When the `fast` pointer reaches the end of the list, the `slow` pointer will be at the middle node.
3. Return the node pointed to by the `slow` pointer.

Here's a sample implementation:

```cpp
#include <iostream>

struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* findMiddleNode(ListNode* head) {
    if (head == nullptr)
        return nullptr;

    ListNode* slow = head;
    ListNode* fast = head;

    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;
        fast = fast->next->next;
    }

    return slow;
}

int main() {
    // Example usage
    ListNode* head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);

    ListNode* middleNode = findMiddleNode(head);
    if (middleNode != nullptr)
        std::cout << "Middle Node: " << middleNode->val << std::endl;
    else
        std::cout << "List is empty." << std::endl;

    return 0;
}
```

In this example, the `findMiddleNode` function returns the middle node of the linked list. You can adjust the logic according to your specific requirements.

### 1. Algorithms & Data Structures (C++): Linked List: Middle Node of List - Slow and Fast Pointer Approach

In C++, finding the middle node of a linked list using the slow and fast pointer approach is a common algorithmic technique. This approach involves using two pointers: one that moves one node at a time (slow pointer) and another that moves two nodes at a time (fast pointer). By the time the fast pointer reaches the end of the list, the slow pointer will be at the middle node.

Here's the implementation:

```cpp
#include <iostream>

// Define the structure for a node in the linked list
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

// Function to find the middle node of a linked list
ListNode* middleNode(ListNode* head) {
    if (head == nullptr || head->next == nullptr) {
        return head;
    }

    ListNode *slow = head;
    ListNode *fast = head;

    // Move the fast pointer two nodes at a time and the slow pointer one node at a time
    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;
        fast = fast->next->next;
    }

    // At this point, slow pointer is at the middle node
    return slow;
}

// Utility function to print the linked list
void printList(ListNode *head) {
    while (head != nullptr) {
        std::cout << head->val << " ";
        head = head->next;
    }
    std::cout << std::endl;
}

int main() {
    // Example usage
    ListNode *head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);

    std::cout << "Original List: ";
    printList(head);

    ListNode *middle = middleNode(head);
    std::cout << "Middle Node: " << middle->val << std::endl;

    return 0;
}
```

This code defines a simple linked list structure, implements the `middleNode` function using the slow and fast pointer approach, and provides a `printList` function to print the elements of the linked list for demonstration purposes. Finally, it demonstrates the usage of the `middleNode` function in the `main` function with an example linked list.

### 1. Algorithms & Data Structures (C++): Exercise: Find Middle Of The Linked List

To find the middle of a linked list, you can use the slow and fast pointer technique. Here's how it works:

1. Initialize two pointers, slow and fast, both pointing to the head of the linked list.
2. Move the fast pointer twice as fast as the slow pointer. When the fast pointer reaches the end of the list, the slow pointer will be at the middle.
3. Return the node pointed to by the slow pointer.

Here's the C++ code for the function:

```cpp
#include <iostream>

// Define the structure of a node in the linked list
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* findMiddle(ListNode* head) {
    if (head == nullptr || head->next == nullptr) {
        return head; // Empty list or single node
    }

    ListNode* slow = head;
    ListNode* fast = head;

    // Move slow pointer by one and fast pointer by two
    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;
        fast = fast->next->next;
    }

    // Now slow points to the middle node
    return slow;
}

// Function to print the elements of the linked list
void printList(ListNode* head) {
    while (head != nullptr) {
        std::cout << head->val << " ";
        head = head->next;
    }
    std::cout << std::endl;
}

// Test the findMiddle function
int main() {
    // Create a sample linked list: 1->2->3->4->5
    ListNode* head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);

    std::cout << "Original List: ";
    printList(head);

    ListNode* middle = findMiddle(head);
    std::cout << "Middle Element: " << middle->val << std::endl;

    return 0;
}
```

This code defines a linked list node structure, implements the findMiddle function, and provides a main function to test the findMiddle function with a sample linked list.

### 1. Algorithms & Data Structures (C++): Singly Linked Lists: Sentinels

Using sentinels in singly linked lists can simplify certain operations and edge cases. Sentinels are special nodes that do not hold any actual data but are used as placeholders at the beginning and/or end of the list. They provide several advantages:

1. **Simplifying edge cases**: Sentinels eliminate the need to handle special cases for an empty list or operations at the beginning or end of the list.

2. **Uniform operations**: With sentinels, all operations (insertion, deletion, traversal) can be performed uniformly throughout the list without extra conditionals to check for special cases.

Here's a basic implementation of a singly linked list with sentinels in C++:

```cpp
#include <iostream>

template<typename T>
class Node {
public:
    T data;
    Node* next;
    Node(T data) : data(data), next(nullptr) {}
};

template<typename T>
class SinglyLinkedList {
private:
    Node<T>* head;
    Node<T>* tail;

public:
    SinglyLinkedList() {
        // Create sentinel nodes
        head = new Node<T>(T());
        tail = new Node<T>(T());
        head->next = tail;
    }

    ~SinglyLinkedList() {
        Node<T>* current = head;
        while (current) {
            Node<T>* next = current->next;
            delete current;
            current = next;
        }
    }

    // Insert at the end of the list
    void insert(T data) {
        Node<T>* newNode = new Node<T>(data);
        newNode->next = tail;
        Node<T>* current = head;
        while (current->next != tail) {
            current = current->next;
        }
        current->next = newNode;
    }

    // Display the list
    void display() {
        Node<T>* current = head->next;
        while (current != tail) {
  
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }
};

int main() {
    SinglyLinkedList<int> list;
    list.insert(1);
    list.insert(2);
    list.insert(3);
    list.display(); // Output: 1 2 3
    return 0;
}
```

In this implementation, `head` points to the sentinel node before the first actual node, and `tail` points to the sentinel node after the last actual node. This way, even if the list is empty, `head` and `tail` will always exist, simplifying operations.

### 1. Algorithms & Data Structures (C++): Loop removal in Singly Linked Lists: Floyd's Algorithm Explained

Floyd's Algorithm, also known as the Tortoise and Hare algorithm, is a popular technique used for various tasks in linked lists, including loop detection and removal. Let's delve into how it works and how it can be applied to detect and remove loops in a singly linked list using C++.

**1. Loop Detection using Floyd's Algorithm:**

In Floyd's Algorithm, we use two pointers, often referred to as the "slow" and "fast" pointers. The slow pointer moves one step at a time, while the fast pointer moves two steps at a time. If there is a loop in the linked list, these pointers will eventually meet.

Here's how it works in code:

```cpp
bool detectLoop(Node* head) {
    Node* slow = head;
    Node* fast = head;
    
    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;
        fast = fast->next->next;
        
        // If they meet, it means there's a loop
        if (slow == fast)
            return true;
    }
    
    // If fast reaches the end, no loop exists
    return false;
}
```

**2. Removing the Loop:**

Once we've detected the loop, we need to find the starting point of the loop. Afterward, we can simply set the next pointer of the last node in the loop to null to break the loop.

Here's how it can be implemented:

```cpp
void removeLoop(Node* head) {
    Node* slow = head;
    Node* fast = head;

    // Detect the loop and find the meeting point
    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;
        fast = fast->next->next;
        if (slow == fast)
            break;
    }

    // If no loop exists, simply return
    if (fast == nullptr || fast->next == nullptr)
        return;

    // Move slow to the beginning of the list, keeping fast at the meeting point
    slow = head;
    while (slow->next != fast->next) {
        slow = slow->next;
        fast = fast->next;
    }

    // Set the next pointer of the last node in the loop to null
    fast->next = nullptr;
}
```

**3. Example:**

Let's illustrate this with an example:

```bash
1 -> 2 -> 3 -> 4 -> 5 -> 6
          ^         |    |
          |_________|____|
```

In this list, nodes 5 and 6 create a loop. After detecting the loop, we can set the next pointer of node 6 to null to remove the loop:

```bash
1 -> 2 -> 3 -> 4 -> 5 -> 6
```

This code effectively removes the loop from the linked list while preserving the rest of the list's structure. Floyd's Algorithm provides a simple and efficient way to both detect and remove loops in linked lists.

### 1. Algorithms & Data Structures (C++): Loop removal in Singly Linked Lists: Floyd's Algorithm Implemented

Sure, I can guide you through implementing Floyd's algorithm for loop detection and removal in a singly linked list in C++. Floyd's algorithm, also known as the Tortoise and Hare algorithm, is a two-pointer technique used to detect cycles in a linked list.

Here's a step-by-step explanation of how you can implement it:

1. **Node Definition**: Define the structure for a node in the linked list.

2. **Loop Detection**: Implement Floyd's algorithm to detect if there's a loop in the linked list. This involves using two pointers - one slow pointer that moves one step at a time and a fast pointer that moves two steps at a time. If there's a loop, these pointers will meet at some point.

3. **Loop Removal**: After detecting the loop, find the start of the loop. This can be done by moving one pointer to the head of the list and then moving both pointers (slow and fast) one step at a time until they meet again. The meeting point will be the start of the loop. Then, break the loop by setting the next pointer of the node before the start of the loop to null.

Here's a sample implementation in C++:

```cpp
#include <iostream>

using namespace std;

// Node definition
struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

// Function to detect and remove loop
void detectAndRemoveLoop(Node* head) {
    if (head == nullptr || head->next == nullptr)
        return;

    Node* slow = head;
    Node* fast = head;

    // Detect loop
    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;
        fast = fast->next->next;

        if (slow == fast)
            break;
    }

    // If loop exists, find the start of the loop
    if (slow == fast) {
        slow = head;
        while (slow->next != fast->next) {
            slow = slow->next;
            fast = fast->next;
        }

        // Break the loop
        fast->next = nullptr;
    }
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
    // Creating a linked list with a loop
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->next = new Node(3);
    head->next->next->next = new Node(4);
    head->next->next->next->next = new Node(5);

    // Creating a loop for testing
    head->next->next->next->next->next = head->next->next;

    // Detect and remove loop
    detectAndRemoveLoop(head);

    // Print the linked list
    cout << "Linked List after removing loop: ";
    printList(head);

    return 0;
}
```

This code will create a linked list with a loop, detect the loop using Floyd's algorithm, and then remove the loop if it exists. Finally, it will print the linked list after loop removal.

### 1. Algorithms & Data Structures (C++): Singly Linked List - Rotate

Sure, I can help you with that! Rotating a singly linked list involves shifting its elements to the right or left by a certain number of positions. Here's a C++ implementation for rotating a singly linked list:

```cpp
#include <iostream>

// Definition for singly-linked list node
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

// Function to print the linked list
void printList(ListNode *head) {
    ListNode *curr = head;
    while (curr) {
        std::cout << curr->val << " ";
        curr = curr->next;
    }
    std::cout << std::endl;
}

// Function to rotate a singly linked list to the right by k positions
ListNode* rotateRight(ListNode* head, int k) {
    if (!head || k == 0) return head;

    // Find the length of the list and locate the new head
    int len = 1;
    ListNode *tail = head;
    while (tail->next) {
        tail = tail->next;
        len++;
    }
    k = k % len; // Adjust k if it's greater than the length of the list
    if (k == 0) return head; // No rotation needed

    // Move the tail to the (n-k)th node
    ListNode *newTail = head;
    for (int i = 1; i < len - k; ++i) {
        newTail = newTail->next;
    }

    // Adjust pointers to rotate the list
    tail->next = head;
    head = newTail->next;
    newTail->next = nullptr;

    return head;
}

// Test
int main() {
    // Create a sample linked list: 1 -> 2 -> 3 -> 4 -> 5
    ListNode *head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);

    std::cout << "Original list: ";
    printList(head);

    int k = 2; // Rotate right by 2 positions
    head = rotateRight(head, k);

    std::cout << "Rotated list: ";
    printList(head);

    return 0;
}
```

This code defines a `ListNode` struct for the nodes of the singly linked list and provides a function `rotateRight` to rotate the list to the right by `k` positions. The `printList` function is used to print the list for demonstration purposes. Finally, the `main` function demonstrates how to use the `rotateRight` function with a sample linked list.
