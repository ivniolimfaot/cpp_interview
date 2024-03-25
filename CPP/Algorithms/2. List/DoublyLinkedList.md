### 1. Algorithms & Data Structures (C++): Doubly Linked List

A doubly linked list is a data structure that consists of a sequence of elements, called nodes, where each node stores a reference to the previous and next nodes in the sequence. This allows for efficient insertion, deletion, and traversal operations compared to other data structures like arrays, especially when elements need to be added or removed frequently from the middle of the list.

Here's a basic implementation of a doubly linked list in C++:

```cpp
#include <iostream>

// Node class for a doubly linked list
class Node {
public:
    int data;
    Node* prev;
    Node* next;

    // Constructor
    Node(int value) {
        data = value;
        prev = nullptr;
        next = nullptr;
    }
};

// Doubly linked list class
class DoublyLinkedList {
private:
    Node* head;
    Node* tail;

public:
    // Constructor
    DoublyLinkedList() {
        head = nullptr;
        tail = nullptr;
    }

    // Method to insert a new node at the end of the list
    void insertEnd(int value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = newNode;
            tail = newNode;
        } else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
    }

    // Method to display the list from head to tail
    void displayForward() {
        Node* temp = head;
        while (temp != nullptr) {
            std::cout << temp->data << " ";
            temp = temp->next;
        }
        std::cout << std::endl;
    }

    // Method to display the list from tail to head
    void displayBackward() {
        Node* temp = tail;
        while (temp != nullptr) {
            std::cout << temp->data << " ";
            temp = temp->prev;
        }
        std::cout << std::endl;
    }

    // Method to delete a node from the list
    void deleteNode(int value) {
        Node* current = head;
        while (current != nullptr) {
            if (current->data == value) {
                if (current == head && current == tail) {
                    head = nullptr;
                    tail = nullptr;
                } else if (current == head) {
                    head = head->next;
                    head->prev = nullptr;
                } else if (current == tail) {
                    tail = tail->prev;
                    tail->next = nullptr;
                } else {
                    current->prev->next = current->next;
                    current->next->prev = current->prev;
                }
                delete current;
                return;
            }
            current = current->next;
        }
        std::cout << "Element not found in the list." << std::endl;
    }
};

// Main function to test the doubly linked list implementation
int main() {
    DoublyLinkedList dll;
    dll.insertEnd(1);
    dll.insertEnd(2);
    dll.insertEnd(3);
    dll.insertEnd(4);

    std::cout << "Forward traversal: ";
    dll.displayForward(); // Output: 1 2 3 4

    std::cout << "Backward traversal: ";
    dll.displayBackward(); // Output: 4 3 2 1

    dll.deleteNode(2);
    std::cout << "List after deleting 2: ";
    dll.displayForward(); // Output: 1 3 4

    return 0;
}
```

This code provides a basic implementation of a doubly linked list in C++. It includes methods for inserting elements at the end of the list, displaying the list in forward and backward directions, and deleting a node from the list by its value.

### 1. Algorithms & Data Structures (C++): Doubly linked list deletion

In C++, deleting a node from a doubly linked list involves several steps:

1. Find the node to delete.
2. Adjust the pointers of the previous and next nodes to bypass the node to be deleted.
3. Delete the node.

Here's a basic implementation:

```cpp
#include <iostream>

using namespace std;

// Node structure for doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
    Node(int value) : data(value), prev(nullptr), next(nullptr) {}
};

// Function to delete a node from doubly linked list
void deleteNode(Node** head_ref, Node* del_node) {
    // If the node to be deleted is the head node
    if (*head_ref == del_node)
        *head_ref = del_node->next;

    // Adjust next if the node to be deleted is NOT the last node
    if (del_node->next != nullptr)
        del_node->next->prev = del_node->prev;

    // Adjust prev if the node to be deleted is NOT the first node
    if (del_node->prev != nullptr)
        del_node->prev->next = del_node->next;

    // Free memory
    delete del_node;
}

// Function to print the doubly linked list
void printList(Node* node) {
    while (node != nullptr) {
        cout << node->data << " ";
        node = node->next;
    }
    cout << endl;
}

int main() {
    // Create a doubly linked list: 1 <-> 2 <-> 3 <-> 4 <-> 5
    Node* head = new Node(1);
    Node* second = new Node(2);
    Node* third = new Node(3);
    Node* fourth = new Node(4);
    Node* fifth = new Node(5);

    head->next = second;
    second->prev = head;
    second->next = third;
    third->prev = second;
    third->next = fourth;
    fourth->prev = third;
    fourth->next = fifth;
    fifth->prev = fourth;

    cout << "Original list: ";
    printList(head);

    // Delete node with value 3
    deleteNode(&head, third);

    cout << "List after deletion: ";
    printList(head);

    return 0;
}
```

This code creates a doubly linked list with five nodes, deletes the node with value 3, and prints the list before and after deletion.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: AddFirst

To implement adding a node to the beginning of a doubly linked list in C++, you'll need to create a new node, adjust pointers, and handle special cases such as an empty list. Here's how you can do it:

```cpp
#include <iostream>

// Define the structure of a node
struct Node {
    int data;
    Node* prev;
    Node* next;
    
    // Constructor
    Node(int value) : data(value), prev(nullptr), next(nullptr) {}
};

// Define the doubly linked list class
class DoublyLinkedList {
private:
    Node* head;
public:
    DoublyLinkedList() : head(nullptr) {}

    // Function to add a node to the beginning of the list
    void addFirst(int value) {
        // Create a new node
        Node* newNode = new Node(value);
        
        // If the list is empty
        if (head == nullptr) {
            head = newNode;
        } else {
            // Adjust pointers
            newNode->next = head;
            head->prev = newNode;
            head = newNode;
        }
    }

    // Function to print the list
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
    DoublyLinkedList myList;

    // Add elements to the beginning of the list
    myList.addFirst(3);
    myList.addFirst(7);
    myList.addFirst(10);

    // Display the list
    myList.display();

    return 0;
}
```

In this code:

* We define a `Node` struct to represent each element of the doubly linked list.
* We define a `DoublyLinkedList` class to manage the list operations.
* The `addFirst` method adds a new node to the beginning of the list.
* The `display` method prints the elements of the list.
* In the `main` function, we create a `DoublyLinkedList` object, add elements to it using `addFirst`, and then display the list.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: AddLast implementation

Sure, implementing the `AddLast` operation for a doubly linked list in C++ involves adding a new node at the end of the list. Here's a basic implementation:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* next;
    Node* prev;
    
    Node(int val) : data(val), next(nullptr), prev(nullptr) {}
};

class DoublyLinkedList {
private:
    Node* head;
    Node* tail;
    
public:
    DoublyLinkedList() : head(nullptr), tail(nullptr) {}
    
    // Function to add a new node at the end of the list
    void AddLast(int data) {
        Node* newNode = new Node(data);
        if (head == nullptr) {
            // If the list is empty, set both head and tail to the new node
            head = tail = newNode;
        } else {
            // Otherwise, update the next pointer of the current tail node
            tail->next = newNode;
            // Update the prev pointer of the new node to point to the current tail
            newNode->prev = tail;
            // Update the tail pointer to the new node
            tail = newNode;
        }
    }
    
    // Function to print the elements of the list
    void PrintList() {
        Node* temp = head;
        while (temp != nullptr) {
            std::cout << temp->data << " ";
            temp = temp->next;
        }
        std::cout << std::endl;
    }
};

int main() {
    DoublyLinkedList list;
    
    // Adding elements to the list
    list.AddLast(1);
    list.AddLast(2);
    list.AddLast(3);
    
    // Printing the elements of the list
    list.PrintList();
    
    return 0;
}
```

This code defines a `Node` struct representing each element in the doubly linked list and a `DoublyLinkedList` class that contains the `AddLast` method to add elements at the end of the list. In the `AddLast` method, a new node is created with the given data. If the list is empty, the head and tail pointers are set to the new node. Otherwise, the new node is appended after the current tail, and the tail pointer is updated to point to the new node. Finally, a `PrintList` method is provided to print the elements of the list for testing.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Append Method

Certainly! The append method in a doubly linked list adds a new node to the end of the list. Here's a basic implementation in C++:

```cpp
#include <iostream>

// Node structure for doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
    Node(int val) : data(val), prev(nullptr), next(nullptr) {}
};

// Doubly linked list class
class DoublyLinkedList {
private:
    Node* head;
    Node* tail;

public:
    DoublyLinkedList() : head(nullptr), tail(nullptr) {}

    // Method to append a new node to the end of the list
    void append(int val) {
        Node* newNode = new Node(val);
        if (!head) {
            head = newNode;
            tail = newNode;
        } else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
    }

    // Method to print the list
    void display() {
        Node* temp = head;
        while (temp) {
            std::cout << temp->data << " ";
            temp = temp->next;
        }
        std::cout << std::endl;
    }
};

// Main function for testing
int main() {
    DoublyLinkedList dll;
    dll.append(1);
    dll.append(2);
    dll.append(3);
    dll.display(); // Output: 1 2 3
    return 0;
}
```

In this implementation:

1. We have a `Node` struct which represents each node of the doubly linked list. It contains data, a pointer to the previous node (`prev`), and a pointer to the next node (`next`).
2. The `DoublyLinkedList` class maintains pointers to the head and tail of the list.
3. The `append` method creates a new node with the given value and adds it to the end of the list. If the list is empty, it sets both `head` and `tail` to the new node. Otherwise, it updates the `next` pointer of the current tail to point to the new node, sets the `prev` pointer of the new node to the current tail, and updates the `tail` pointer to the new node.
4. The `display` method traverses the list from head to tail and prints the data of each node.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Delete First

Certainly! Here's how you can delete the first node in a doubly linked list using C++:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* next;
    Node* prev;
    
    Node(int val) : data(val), next(nullptr), prev(nullptr) {}
};

class DoublyLinkedList {
private:
    Node* head;
public:
    DoublyLinkedList() : head(nullptr) {}

    // Function to insert a node at the beginning of the list
    void insertAtBeginning(int val) {
        Node* newNode = new Node(val);
        if (!head) {
            head = newNode;
        } else {
            newNode->next = head;
            head->prev = newNode;
            head = newNode;
        }
    }

    // Function to delete the first node of the list
    void deleteFirst() {
        if (!head) {
            std::cout << "List is empty. Nothing to delete." << std::endl;
            return;
        }
        Node* temp = head;
        head = head->next;
        if (head)
            head->prev = nullptr;
        delete temp;
    }

    // Function to display the elements of the list
    void display() {
        Node* current = head;
        while (current) {
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }
};

int main() {
    DoublyLinkedList dll;
    dll.insertAtBeginning(3);
    dll.insertAtBeginning(5);
    dll.insertAtBeginning(7);
    
    std::cout << "Original List: ";
    dll.display(); // Output: 7 5 3
    
    dll.deleteFirst();
    
    std::cout << "After deleting first node: ";
    dll.display(); // Output: 5 3
    
    return 0;
}
```

In this code:

* We define a `Node` struct representing a node in the doubly linked list.
* We define a `DoublyLinkedList` class to encapsulate the functionality of the doubly linked list.
* The `deleteFirst()` function deletes the first node of the list.
* The `display()` function prints the elements of the list.
* In the `main()` function, we demonstrate the usage of the `DoublyLinkedList` class by creating a list, inserting elements, deleting the first node, and displaying the list before and after the deletion.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Delete Last

Deleting the last node in a doubly linked list involves a few steps. Here's how you can implement it in C++:

```cpp
#include <iostream>

using namespace std;

// Node structure for the doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
    Node(int val) : data(val), prev(nullptr), next(nullptr) {}
};

// Doubly linked list class
class DoublyLinkedList {
private:
    Node* head;
public:
    DoublyLinkedList() : head(nullptr) {}

    // Function to delete the last node
    void deleteLast() {
        if (head == nullptr) {
            cout << "List is empty. Nothing to delete.\n";
            return;
        }

        if (head->next == nullptr) {
            delete head;
            head = nullptr;
            return;
        }

        Node* temp = head;
        while (temp->next->next != nullptr) {
            temp = temp->next;
        }

        delete temp->next;
        temp->next = nullptr;
    }

    // Function to insert a node at the end
    void insertEnd(int val) {
        Node* newNode = new Node(val);
        if (head == nullptr) {
            head = newNode;
            return;
        }

        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }

        temp->next = newNode;
        newNode->prev = temp;
    }

    // Function to display the list
    void display() {
        Node* temp = head;
        while (temp != nullptr) {
            cout << temp->data << " ";
            temp = temp->next;
        }
        cout << endl;
    }
};

int main() {
    DoublyLinkedList dll;
    dll.insertEnd(1);
    dll.insertEnd(2);
    dll.insertEnd(3);
    dll.insertEnd(4);
    cout << "Original List: ";
    dll.display();

    dll.deleteLast();
    cout << "After deleting last node: ";
    dll.display();

    return 0;
}
```

This code defines a doubly linked list and implements the `deleteLast()` function to remove the last node from the list. The `insertEnd()` function is also provided to insert elements at the end of the list, and the `display()` function is used to print the list.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Delete Node

Certainly! Deleting a node from a doubly linked list in C++ involves a few steps:

1. Find the node to be deleted.
2. Adjust the pointers of the adjacent nodes to bypass the node to be deleted.
3. Delete the node and deallocate memory.

Here's a basic implementation:

```cpp
#include <iostream>

// Node structure for doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
    Node(int val) : data(val), prev(nullptr), next(nullptr) {}
};

// Function to delete a node from doubly linked list
void deleteNode(Node* &head, Node* delNode) {
    if (head == nullptr || delNode == nullptr)
        return;

    // If the node to be deleted is the head
    if (head == delNode)
        head = delNode->next;

    // Adjust pointers of previous and next nodes
    if (delNode->prev != nullptr)
        delNode->prev->next = delNode->next;
    if (delNode->next != nullptr)
        delNode->next->prev = delNode->prev;

    // Delete the node
    delete delNode;
}

// Function to print the doubly linked list
void printList(Node* node) {
    while (node != nullptr) {
        std::cout << node->data << " ";
        node = node->next;
    }
    std::cout << std::endl;
}

int main() {
    // Create a sample doubly linked list: 1 <-> 2 <-> 3 <-> 4 <-> 5
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->prev = head;
    head->next->next = new Node(3);
    head->next->next->prev = head->next;
    head->next->next->next = new Node(4);
    head->next->next->next->prev = head->next->next;
    head->next->next->next->next = new Node(5);
    head->next->next->next->next->prev = head->next->next->next;

    std::cout << "Original List: ";
    printList(head);

    // Deleting node with value 3
    Node* delNode = head->next->next;
    deleteNode(head, delNode);

    std::cout << "List after deleting node with value 3: ";
    printList(head);

    // Free memory
    Node* current = head;
    while (current != nullptr) {
        Node* temp = current;
        current = current->next;
        delete temp;
    }

    return 0;
}
```

This code demonstrates how to delete a node from a doubly linked list in C++. You can modify it as needed for your specific use case.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Find and Insert After and Insert Before

Certainly! Below is a simple implementation of a doubly linked list in C++ along with functions to find a node and to insert a new node after and before a given node:

```cpp
#include <iostream>

using namespace std;

// Node class for the doubly linked list
class Node {
public:
    int data;
    Node* prev;
    Node* next;

    Node(int val) {
        data = val;
        prev = nullptr;
        next = nullptr;
    }
};

// Doubly linked list class
class DoublyLinkedList {
private:
    Node* head;
    Node* tail;

public:
    DoublyLinkedList() {
        head = nullptr;
        tail = nullptr;
    }

    // Function to insert a new node at the end of the list
    void append(int val) {
        Node* newNode = new Node(val);
        if (!head) {
            head = tail = newNode;
        } else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
    }

    // Function to find a node with given value
    Node* find(int val) {
        Node* current = head;
        while (current) {
            if (current->data == val)
                return current;
            current = current->next;
        }
        return nullptr;
    }

    // Function to insert a new node after a given node
    void insertAfter(Node* prevNode, int val) {
        if (!prevNode) {
            cout << "Previous node cannot be NULL.\n";
            return;
        }
        Node* newNode = new Node(val);
        newNode->next = prevNode->next;
        newNode->prev = prevNode;
        if (prevNode->next)
            prevNode->next->prev = newNode;
        prevNode->next = newNode;
        if (prevNode == tail)
            tail = newNode;
    }

    // Function to insert a new node before a given node
    void insertBefore(Node* nextNode, int val) {
        if (!nextNode) {
            cout << "Next node cannot be NULL.\n";
            return;
        }
        Node* newNode = new Node(val);
        newNode->next = nextNode;
        newNode->prev = nextNode->prev;
        if (nextNode->prev)
            nextNode->prev->next = newNode;
        else
            head = newNode;
        nextNode->prev = newNode;
    }

    // Function to display the elements of the list
    void display() {
        Node* current = head;
        while (current) {
            cout << current->data << " ";
            current = current->next;
        }
        cout << endl;
    }
};

int main() {
    DoublyLinkedList dll;

    dll.append(1);
    dll.append(2);
    dll.append(3);
    dll.append(4);
    dll.append(5);

    cout << "Original list: ";
    dll.display();

    Node* nodeToFind = dll.find(3);
    if (nodeToFind) {
        cout << "Node found: " << nodeToFind->data << endl;
    } else {
        cout << "Node not found.\n";
    }

    dll.insertAfter(nodeToFind, 6);
    cout << "List after insertion after node 3: ";
    dll.display();

    dll.insertBefore(nodeToFind, 0);
    cout << "List after insertion before node 3: ";
    dll.display();

    return 0;
}
```

This code defines a `Node` class to represent individual nodes of the doubly linked list and a `DoublyLinkedList` class to manage the list. It includes functions to append new nodes, find a node with a given value, insert a new node after a given node, and insert a new node before a given node. Finally, the `main` function demonstrates the usage of these functions.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Get

In C++, a doubly linked list is a linear data structure where each element is a node containing a data field and two pointers, one pointing to the previous node and the other pointing to the next node. Here's a basic implementation of the `get` operation for a doubly linked list:

```cpp
#include <iostream>

// Define the structure of a node
struct Node {
    int data;
    Node* prev;
    Node* next;
    
    // Constructor
    Node(int val) : data(val), prev(nullptr), next(nullptr) {}
};

// Define the doubly linked list class
class DoublyLinkedList {
private:
    Node* head;
    Node* tail;
    int size;

public:
    // Constructor
    DoublyLinkedList() : head(nullptr), tail(nullptr), size(0) {}

    // Function to get the element at a specific index
    int get(int index) {
        if (index < 0 || index >= size)
            return -1; // Invalid index

        Node* current = head;
        for (int i = 0; i < index; ++i)
            current = current->next;

        return current->data;
    }

    // Function to add a new node to the end of the list
    void append(int val) {
        Node* newNode = new Node(val);
        if (size == 0) {
            head = tail = newNode;
        } else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
        size++;
    }
};

int main() {
    DoublyLinkedList dll;
    dll.append(1);
    dll.append(2);
    dll.append(3);

    // Get elements at various indexes
    std::cout << "Element at index 0: " << dll.get(0) << std::endl; // Should print 1
    std::cout << "Element at index 1: " << dll.get(1) << std::endl; // Should print 2
    std::cout << "Element at index 2: " << dll.get(2) << std::endl; // Should print 3

    // Trying an invalid index
    std::cout << "Element at index 3: " << dll.get(3) << std::endl; // Should print -1

    return 0;
}
```

This code defines a `DoublyLinkedList` class with a `get` function that retrieves the element at a specified index. The `main` function demonstrates how to use this function by creating a doubly linked list, adding elements to it, and then retrieving elements at different indexes.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Get Method

Sure, here's an example implementation of the `get` method for a doubly linked list in C++:

```cpp
#include <iostream>

template<typename T>
class Node {
public:
    T data;
    Node<T>* next;
    Node<T>* prev;

    Node(T data) {
        this->data = data;
        this->next = nullptr;
        this->prev = nullptr;
    }
};

template<typename T>
class DoublyLinkedList {
private:
    Node<T>* head;
    int size;

public:
    DoublyLinkedList() {
        head = nullptr;
        size = 0;
    }

    void add(T data) {
        Node<T>* newNode = new Node<T>(data);
        if (head == nullptr) {
            head = newNode;
        } else {
            Node<T>* current = head;
            while (current->next != nullptr) {
                current = current->next;
            }
            current->next = newNode;
            newNode->prev = current;
        }
        size++;
    }

    T get(int index) {
        if (index < 0 || index >= size) {
            throw std::out_of_range("Index out of bounds");
        }

        Node<T>* current = head;
        for (int i = 0; i < index; i++) {
            current = current->next;
        }
        return current->data;
    }

    int getSize() {
        return size;
    }
};

int main() {
    DoublyLinkedList<int> dll;
    dll.add(1);
    dll.add(2);
    dll.add(3);

    // Get element at index 1
    std::cout << "Element at index 1: " << dll.get(1) << std::endl;

    return 0;
}
```

This code defines a doubly linked list where each node contains a data element and pointers to the next and previous nodes. The `get` method retrieves the element at a specified index in the list.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Insert

Sure! Here's an example of how you can implement the insertion operation for a doubly linked list in C++:

```cpp
#include <iostream>

using namespace std;

// Node class to represent each element in the doubly linked list
class Node {
public:
    int data;
    Node* prev;
    Node* next;

    Node(int value) {
        data = value;
        prev = nullptr;
        next = nullptr;
    }
};

// Doubly linked list class
class DoublyLinkedList {
private:
    Node* head;
public:
    DoublyLinkedList() {
        head = nullptr;
    }

    // Function to insert a new node at the beginning of the list
    void insertAtBeginning(int value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = newNode;
        } else {
            newNode->next = head;
            head->prev = newNode;
            head = newNode;
        }
    }

    // Function to insert a new node at the end of the list
    void insertAtEnd(int value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = newNode;
        } else {
            Node* temp = head;
            while (temp->next != nullptr) {
                temp = temp->next;
            }
            temp->next = newNode;
            newNode->prev = temp;
        }
    }

    // Function to display the elements of the list
    void display() {
        Node* temp = head;
        while (temp != nullptr) {
            cout << temp->data << " ";
            temp = temp->next;
        }
        cout << endl;
    }
};

int main() {
    DoublyLinkedList dll;
    dll.insertAtBeginning(1);
    dll.insertAtEnd(2);
    dll.insertAtBeginning(0);
    dll.insertAtEnd(3);

    cout << "Doubly linked list elements: ";
    dll.display();

    return 0;
}
```

In this code:

* We have a `Node` class to represent each element of the doubly linked list, containing the data and pointers to the previous and next nodes.
* The `DoublyLinkedList` class manages the list. It has functions to insert nodes at the beginning (`insertAtBeginning`) and end (`insertAtEnd`) of the list, and a function to display the elements of the list (`display`).
* In the `main` function, we demonstrate how to use the doubly linked list by inserting elements at the beginning and end of the list and then displaying the list.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Palindrome Checker

To create a palindrome checker using a doubly linked list in C++, you can follow these steps:

1. Define the structure for a doubly linked list node.
2. Implement functions to insert nodes, create the linked list, and traverse it.
3. Implement a function to check if the linked list is a palindrome.

Here's a sample implementation:

```cpp
#include <iostream>
#include <string>

using namespace std;

// Doubly Linked List Node
struct Node {
    char data;
    Node* next;
    Node* prev;
};

// Function to insert a node at the end of the list
void insertNode(Node*& head, char data) {
    Node* newNode = new Node;
    newNode->data = data;
    newNode->next = nullptr;

    if (head == nullptr) {
        newNode->prev = nullptr;
        head = newNode;
    } else {
        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = newNode;
        newNode->prev = temp;
    }
}

// Function to create a doubly linked list from a string
Node* createLinkedList(const string& str) {
    Node* head = nullptr;
    for (char ch : str) {
        insertNode(head, ch);
    }
    return head;
}

// Function to check if a doubly linked list is a palindrome
bool isPalindrome(Node* head) {
    if (head == nullptr || head->next == nullptr)
        return true;

    // Move 'end' pointer to the last node
    Node* end = head;
    while (end->next != nullptr) {
        end = end->next;
    }

    // Check if the characters match from start and end
    while (head != end && head->prev != end) {
        if (head->data != end->data)
            return false;
        head = head->next;
        end = end->prev;
    }

    return true;
}

int main() {
    string str = "racecar";
    Node* head = createLinkedList(str);

    if (isPalindrome(head))
        cout << "The string is a palindrome." << endl;
    else
        cout << "The string is not a palindrome." << endl;

    return 0;
}
```

This implementation includes functions to create a doubly linked list from a string and to check if the list is a palindrome. It traverses the list from both ends simultaneously, comparing characters until either they meet (in case of odd-length palindrome) or one reaches the other (in case of even-length palindrome).

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Pop

To implement the "pop" operation for a doubly linked list in C++, you would remove an element from either the beginning (front) or end (back) of the list. Here's a basic implementation for both scenarios:

```cpp
#include <iostream>

using namespace std;

// Node structure for doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
    Node(int val) : data(val), prev(nullptr), next(nullptr) {}
};

// Doubly Linked List class
class DoublyLinkedList {
private:
    Node* head;
    Node* tail;
public:
    DoublyLinkedList() : head(nullptr), tail(nullptr) {}

    // Function to pop from the front of the list
    void popFront() {
        if (head == nullptr) {
            cout << "List is empty, cannot pop!" << endl;
            return;
        }
        if (head == tail) { // Only one element in the list
            delete head;
            head = tail = nullptr;
        } else {
            Node* temp = head;
            head = head->next;
            head->prev = nullptr;
            delete temp;
        }
    }

    // Function to pop from the back of the list
    void popBack() {
        if (tail == nullptr) {
            cout << "List is empty, cannot pop!" << endl;
            return;
        }
        if (head == tail) { // Only one element in the list
            delete tail;
            head = tail = nullptr;
        } else {
            Node* temp = tail;
            tail = tail->prev;
            tail->next = nullptr;
            delete temp;
        }
    }

    // Function to display the list
    void display() {
        Node* current = head;
        while (current != nullptr) {
            cout << current->data << " ";
            current = current->next;
        }
        cout << endl;
    }

    // Function to add a node at the end of the list
    void pushBack(int val) {
        Node* newNode = new Node(val);
        if (head == nullptr) {
            head = tail = newNode;
        } else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
    }
};

int main() {
    DoublyLinkedList dll;
    dll.pushBack(1);
    dll.pushBack(2);
    dll.pushBack(3);
    dll.pushBack(4);

    cout << "Original list: ";
    dll.display();

    dll.popFront();
    cout << "List after popping from front: ";
    dll.display();

    dll.popBack();
    cout << "List after popping from back: ";
    dll.display();

    return 0;
}
```

This code defines a doubly linked list with operations to pop elements from the front (`popFront`) and back (`popBack`). Additionally, it includes a `pushBack` operation to add elements at the end of the list and a `display` operation to print the contents of the list.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Pop First

To implement the "pop first" operation for a doubly linked list in C++, you need to remove the first node from the list. Here's a basic implementation:

```cpp
#include <iostream>

using namespace std;

// Node structure for doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
    
    Node(int val) : data(val), prev(nullptr), next(nullptr) {}
};

// Doubly linked list class
class DoublyLinkedList {
private:
    Node* head;
public:
    DoublyLinkedList() : head(nullptr) {}
    
    // Function to add a node at the front of the list
    void pushFront(int val) {
        Node* newNode = new Node(val);
        if (!head) {
            head = newNode;
        } else {
            newNode->next = head;
            head->prev = newNode;
            head = newNode;
        }
    }
    
    // Function to remove the first node from the list
    void popFront() {
        if (!head) {
            cout << "The list is already empty." << endl;
            return;
        }
        Node* temp = head;
        head = head->next;
        if (head)
            head->prev = nullptr;
        delete temp;
    }
    
    // Function to print the list
    void display() {
        Node* temp = head;
        while (temp) {
            cout << temp->data << " ";
            temp = temp->next;
        }
        cout << endl;
    }
};

int main() {
    DoublyLinkedList myList;
    
    // Adding elements to the list
    myList.pushFront(3);
    myList.pushFront(5);
    myList.pushFront(7);
    
    // Displaying the list
    cout << "Original list: ";
    myList.display();
    
    // Removing the first node
    myList.popFront();
    
    // Displaying the list after popping the first node
    cout << "List after popping the first node: ";
    myList.display();
    
    return 0;
}
```

In this implementation:

* The `Node` struct represents each node of the doubly linked list, containing the data and pointers to the previous and next nodes.
* The `DoublyLinkedList` class manages the list and provides methods for adding nodes at the front (`pushFront`), removing the first node (`popFront`), and displaying the list (`display`).
* In the `popFront` method, if the list is empty, it prints a message indicating that the list is already empty. Otherwise, it removes the first node from the list by updating the head pointer and adjusting the pointers of the neighboring nodes accordingly.
* In the `main` function, a few elements are added to the list, and then the first node is popped using the `popFront` method.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Pop First Method

In C++, a doubly linked list's "pop first" method removes the first element from the list. Here's how you can implement it:

```cpp
#include <iostream>

// Define a node structure for the doubly linked list
struct Node {
    int data;
    Node* next;
    Node* prev;
    
    Node(int val) : data(val), next(nullptr), prev(nullptr) {}
};

class DoublyLinkedList {
private:
    Node* head;
    Node* tail;
    int size;

public:
    DoublyLinkedList() : head(nullptr), tail(nullptr), size(0) {}

    // Method to pop the first element from the list
    void popFirst() {
        if (head == nullptr) {
            std::cout << "The list is empty. Nothing to pop.\n";
            return;
        }
        
        Node* temp = head;
        head = head->next;
        
        if (head != nullptr) {
            head->prev = nullptr;
        } else {
            tail = nullptr; // If there was only one element, update tail as well
        }
        
        delete temp;
        size--;
    }

    // Method to add a new node at the end of the list
    void pushBack(int val) {
        Node* newNode = new Node(val);
        if (tail == nullptr) {
            head = tail = newNode;
        } else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
        size++;
    }

    // Method to display the elements of the list
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
    DoublyLinkedList dll;
    
    // Add some elements to the list
    dll.pushBack(1);
    dll.pushBack(2);
    dll.pushBack(3);

    std::cout << "Original list: ";
    dll.display();

    // Pop the first element
    dll.popFirst();
    std::cout << "List after popping first element: ";
    dll.display();

    return 0;
}
```

This code defines a doubly linked list and implements the `popFirst()` method to remove the first element of the list. The `pushBack()` method is also included to add elements at the end of the list for demonstration purposes, and a `display()` method is provided to print the list elements.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Pop Method

In C++, the pop operation in a doubly linked list removes an element from either the front (head) or the back (tail) of the list. Here's an implementation for both scenarios:

```cpp
#include <iostream>

using namespace std;

// Node structure for the doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
    
    Node(int value) : data(value), prev(nullptr), next(nullptr) {}
};

// Doubly linked list class
class DoublyLinkedList {
private:
    Node* head;
    Node* tail;

public:
    // Constructor
    DoublyLinkedList() : head(nullptr), tail(nullptr) {}

    // Function to remove the front element (head) of the list
    void popFront() {
        if (!head) {
            cout << "List is empty. Nothing to pop." << endl;
            return;
        }

        Node* temp = head;
        head = head->next;
        if (head)
            head->prev = nullptr;
        else
            tail = nullptr;
        
        delete temp;
    }

    // Function to remove the back element (tail) of the list
    void popBack() {
        if (!tail) {
            cout << "List is empty. Nothing to pop." << endl;
            return;
        }

        Node* temp = tail;
        tail = tail->prev;
        if (tail)
            tail->next = nullptr;
        else
            head = nullptr;
        
        delete temp;
    }

    // Function to display the elements of the list
    void display() {
        Node* current = head;
        while (current) {
            cout << current->data << " ";
            current = current->next;
        }
        cout << endl;
    }

    // Function to add a node to the front of the list
    void pushFront(int value) {
        Node* newNode = new Node(value);
        if (!head) {
            head = newNode;
            tail = newNode;
        } else {
            newNode->next = head;
            head->prev = newNode;
            head = newNode;
        }
    }

    // Function to add a node to the back of the list
    void pushBack(int value) {
        Node* newNode = new Node(value);
        if (!tail) {
            head = newNode;
            tail = newNode;
        } else {
            newNode->prev = tail;
            tail->next = newNode;
            tail = newNode;
        }
    }
};

int main() {
    DoublyLinkedList dll;

    // Adding elements to the list
    dll.pushBack(1);
    dll.pushBack(2);
    dll.pushBack(3);
    dll.pushBack(4);

    cout << "Original list: ";
    dll.display();

    // Pop front and back elements
    dll.popFront();
    dll.popBack();

    cout << "List after popping front and back: ";
    dll.display();

    return 0;
}
```

This code defines a `DoublyLinkedList` class with methods to push elements to the front and back, as well as pop elements from the front and back. The `Node` struct represents each element of the list.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Prepend

Sure, here's an implementation of the `prepend` operation for a doubly linked list in C++:

```cpp
#include <iostream>

// Node class for the doubly linked list
class Node {
public:
    int data;
    Node* next;
    Node* prev;

    Node(int val) {
        data = val;
        next = nullptr;
        prev = nullptr;
    }
};

// Doubly linked list class
class DoublyLinkedList {
private:
    Node* head;
public:
    DoublyLinkedList() {
        head = nullptr;
    }

    // Function to prepend a new node with given data to the beginning of the list
    void prepend(int val) {
        Node* newNode = new Node(val);
        if (head == nullptr) {
            head = newNode;
        } else {
            newNode->next = head;
            head->prev = newNode;
            head = newNode;
        }
    }

    // Function to print the elements of the list
    void display() {
        Node* temp = head;
        while (temp != nullptr) {
            std::cout << temp->data << " ";
            temp = temp->next;
        }
        std::cout << std::endl;
    }
};

// Main function to test the implementation
int main() {
    DoublyLinkedList dll;
    dll.prepend(5);
    dll.prepend(10);
    dll.prepend(15);
    dll.display(); // Output should be: 15 10 5
    return 0;
}
```

In this implementation:

* We have a `Node` class representing each node of the doubly linked list.
* The `DoublyLinkedList` class manages the list and contains a pointer to the head of the list.
* The `prepend` function adds a new node with the given value at the beginning of the list.
* The `display` function is just for testing purposes, to print the elements of the list.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Prepend Method

Certainly! The prepend method in a doubly linked list adds a new node at the beginning of the list. Here's how you can implement it in C++:

```cpp
#include <iostream>

// Define the structure of a node
struct Node {
    int data;
    Node* prev;
    Node* next;
};

// Define the doubly linked list class
class DoublyLinkedList {
private:
    Node* head;

public:
    // Constructor
    DoublyLinkedList() : head(nullptr) {}

    // Method to prepend a node to the list
    void prepend(int value) {
        // Create a new node
        Node* newNode = new Node;
        newNode->data = value;
        newNode->prev = nullptr;
        newNode->next = head;

        // Update the previous pointer of the current head
        if (head != nullptr)
            head->prev = newNode;

        // Update the head to point to the new node
        head = newNode;
    }

    // Method to print the list
    void printList() {
        Node* current = head;
        while (current != nullptr) {
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }
};

int main() {
    // Create a doubly linked list object
    DoublyLinkedList dll;

    // Prepend some elements to the list
    dll.prepend(3);
    dll.prepend(2);
    dll.prepend(1);

    // Print the list
    std::cout << "Doubly Linked List after prepending: ";
    dll.printList();

    return 0;
}
```

In this code:

* We define a `Node` struct which represents a node in the doubly linked list. It contains the data (`int` in this case), a pointer to the previous node (`prev`), and a pointer to the next node (`next`).
* We define the `DoublyLinkedList` class with a private member `head`, which points to the first node of the list.
* The `prepend` method creates a new node, sets its data and pointers accordingly, and updates the head to point to the new node.
* The `printList` method traverses the list from head to end, printing each node's data.
* In the `main` function, we create a doubly linked list object, prepend some elements to it, and print the list to verify the prepend operation.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Remove Method

In C++, removing a node from a doubly linked list involves updating pointers to maintain the integrity of the list. Here's a basic implementation of the `remove` method for a doubly linked list:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* prev;
    Node* next;
    Node(int val) : data(val), prev(nullptr), next(nullptr) {}
};

class DoublyLinkedList {
private:
    Node* head;
public:
    DoublyLinkedList() : head(nullptr) {}

    // Function to remove a node from the doubly linked list
    void remove(int key) {
        if (head == nullptr) return; // List is empty

        Node* current = head;
        while (current != nullptr) {
            if (current->data == key) {
                if (current->prev != nullptr) {
                    current->prev->next = current->next;
                } else {
                    head = current->next;
                }
                
                if (current->next != nullptr) {
                    current->next->prev = current->prev;
                }
                
                delete current;
                return; // Node found and removed
            }
            current = current->next;
        }
    }

    // Function to print the doubly linked list
    void printList() {
        Node* temp = head;
        while (temp != nullptr) {
            std::cout << temp->data << " ";
            temp = temp->next;
        }
        std::cout << std::endl;
    }

    // Function to insert a node at the beginning of the doubly linked list
    void insertBegin(int val) {
        Node* newNode = new Node(val);
        newNode->next = head;
        if (head != nullptr) {
            head->prev = newNode;
        }
        head = newNode;
    }
};

int main() {
    DoublyLinkedList dll;
    dll.insertBegin(3);
    dll.insertBegin(2);
    dll.insertBegin(1);
    dll.insertBegin(4);

    std::cout << "Original list: ";
    dll.printList();

    dll.remove(2); // Remove node with value 2

    std::cout << "List after removing 2: ";
    dll.printList();

    return 0;
}
```

In this implementation:

* The `remove` method takes an integer key as input and removes the node with that key from the list.
* It traverses the list to find the node with the given key.
* If the node is found, it updates the `next` and `prev` pointers of the surrounding nodes to bypass the node to be removed.
* It then deallocates the memory of the removed node.
* The `printList` method is provided to print the contents of the list for verification purposes.
* A `main` function demonstrates the usage of the `DoublyLinkedList` class by inserting some nodes, removing one of them, and printing the resulting list.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Reverse

Sure, I can guide you through implementing a function to reverse a doubly linked list in C++.

First, let's define the structure for a doubly linked list node:

```cpp
struct Node {
    int data;
    Node* next;
    Node* prev;
};
```

Now, let's create a function to reverse the doubly linked list:

```cpp
void reverseList(Node** head_ref) {
    Node* current = *head_ref;
    Node* temp = nullptr;

    // Swap next and prev for all nodes of doubly linked list
    while (current != nullptr) {
        temp = current->prev;
        current->prev = current->next;
        current->next = temp;
        current = current->prev;
    }

    // Check if the list is not empty and if the last node is not nullptr
    if (temp != nullptr) {
        *head_ref = temp->prev;
    }
}
```

You can use this function to reverse a doubly linked list. Here's a simple example of how you can use it:

```cpp
#include <iostream>

void reverseList(Node** head_ref);

int main() {
    // Example usage
    Node* head = new Node{1, nullptr, nullptr};
    head->next = new Node{2, nullptr, head};
    head->next->next = new Node{3, nullptr, head->next};

    // Before reversing
    std::cout << "Original list: ";
    for (Node* current = head; current != nullptr; current = current->next) {
        std::cout << current->data << " ";
    }
    std::cout << std::endl;

    // Reverse the list
    reverseList(&head);

    // After reversing
    std::cout << "Reversed list: ";
    for (Node* current = head; current != nullptr; current = current->next) {
        std::cout << current->data << " ";
    }
    std::cout << std::endl;

    // Clean up memory
    while (head != nullptr) {
        Node* temp = head;
        head = head->next;
        delete temp;
    }

    return 0;
}
```

This will output:

```bash
Original list: 1 2 3 
Reversed list: 3 2 1 
```

This implementation reverses the doubly linked list in place, without using any extra data structures.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Reverse Traverse Method

To implement a reverse traversal method for a doubly linked list in C++, you can start by defining a doubly linked list node structure with pointers to the previous and next nodes. Then, you can implement a class for the doubly linked list, including methods to insert nodes, delete nodes, and traverse the list in reverse. Here's a basic example:

```cpp
#include <iostream>

// Define the structure for a node in the doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
    
    Node(int value) : data(value), prev(nullptr), next(nullptr) {}
};

// Define the doubly linked list class
class DoublyLinkedList {
private:
    Node* head;
    Node* tail;

public:
    DoublyLinkedList() : head(nullptr), tail(nullptr) {}

    // Method to insert a node at the end of the list
    void insert(int value) {
        Node* newNode = new Node(value);
        if (!head) {
            head = tail = newNode;
        } else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
    }

    // Method to traverse the list in reverse and print its elements
    void reverseTraverse() {
        Node* current = tail;
        while (current != nullptr) {
            std::cout << current->data << " ";
            current = current->prev;
        }
        std::cout << std::endl;
    }
};

int main() {
    DoublyLinkedList dll;

    // Insert some elements into the list
    dll.insert(1);
    dll.insert(2);
    dll.insert(3);
    dll.insert(4);
    dll.insert(5);

    // Traverse the list in reverse order
    std::cout << "Reverse traversal of the list: ";
    dll.reverseTraverse();

    return 0;
}
```

In this example, we define a `Node` structure to represent each element in the doubly linked list. Then, we define a `DoublyLinkedList` class with methods to insert elements into the list and traverse the list in reverse order. The `reverseTraverse()` method starts from the `tail` of the list and iterates backward through the list, printing each element. Finally, in the `main()` function, we create a doubly linked list, insert some elements into it, and then perform a reverse traversal to print the elements in reverse order.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Search Method

To implement a search method for a doubly linked list in C++, you need to traverse the list from either end (beginning or end) and check each node's value until you find the desired element or reach the end of the list. Here's a sample implementation:

```cpp
#include <iostream>

// Node structure for doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
    
    Node(int value) : data(value), prev(nullptr), next(nullptr) {}
};

// Doubly linked list class
class DoublyLinkedList {
private:
    Node* head;
    Node* tail;

public:
    DoublyLinkedList() : head(nullptr), tail(nullptr) {}

    // Method to add a node at the end of the list
    void append(int value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = tail = newNode;
        } else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
    }

    // Method to search for a value in the list
    Node* search(int value) {
        Node* current = head;
        while (current != nullptr) {
            if (current->data == value) {
                return current; // Found the value, return the node
            }
            current = current->next;
        }
        return nullptr; // Value not found
    }

    // Method to print the list (for testing purposes)
    void print() {
        Node* current = head;
        while (current != nullptr) {
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }
};

int main() {
    DoublyLinkedList dll;
    dll.append(1);
    dll.append(2);
    dll.append(3);
    dll.append(4);
    dll.append(5);

    std::cout << "Original list: ";
    dll.print();

    int searchValue = 3;
    Node* result = dll.search(searchValue);
    if (result != nullptr) {
        std::cout << "Value " << searchValue << " found." << std::endl;
    } else {
        std::cout << "Value " << searchValue << " not found." << std::endl;
    }

    return 0;
}
```

In this implementation:

* We define a `Node` structure representing each element of the doubly linked list.
* The `DoublyLinkedList` class manages the list, with methods for appending nodes to the end and searching for a value.
* The `search` method traverses the list from the head to find the desired value.
* The `print` method is provided for testing purposes to print the elements of the list.
* In the `main` function, we demonstrate how to use the `DoublyLinkedList` class, including adding elements and searching for a specific value.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Set

A Doubly Linked List (DLL) is a linear data structure consisting of a sequence of elements called nodes. Each node contains two pointers, one pointing to the previous node and the other pointing to the next node in the sequence. The first node's previous pointer and the last node's next pointer are typically null, indicating the start and end of the list, respectively.

Here's a simple implementation of a Doubly Linked List in C++:

```cpp
#include <iostream>

template <typename T>
class DoublyLinkedList {
private:
    struct Node {
        T data;
        Node* prev;
        Node* next;
        Node(const T& value) : data(value), prev(nullptr), next(nullptr) {}
    };

    Node* head;
    Node* tail;
    size_t size;

public:
    DoublyLinkedList() : head(nullptr), tail(nullptr), size(0) {}

    void push_back(const T& value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = tail = newNode;
        } else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
        size++;
    }

    void display() const {
        Node* current = head;
        while (current != nullptr) {
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }

    size_t getSize() const {
        return size;
    }

    ~DoublyLinkedList() {
        Node* current = head;
        while (current != nullptr) {
            Node* next = current->next;
            delete current;
            current = next;
        }
    }
};
```

This implementation provides basic functionality for a Doubly Linked List, including:

* `push_back`: Inserts a new element at the end of the list.
* `display`: Displays the contents of the list.
* `getSize`: Returns the number of elements in the list.
* Destructor: Deallocates memory occupied by the list when it goes out of scope.

You can further extend this implementation by adding other operations like `push_front`, `pop_back`, `pop_front`, `insert`, `erase`, etc., depending on your requirements.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Set Method

Certainly! In a doubly linked list, the set method typically updates the value of a node at a given index. Here's how you can implement the set method in C++:

```cpp
#include <iostream>

using namespace std;

// Node structure for doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
    
    Node(int val) : data(val), prev(nullptr), next(nullptr) {}
};

// Doubly linked list class
class DoublyLinkedList {
private:
    Node* head;
    
public:
    DoublyLinkedList() : head(nullptr) {}
    
    // Method to set the value of a node at a given index
    bool set(int index, int val) {
        if (index < 0)
            return false;
        
        Node* current = head;
        int currentIndex = 0;
        
        // Traverse the list to find the node at the specified index
        while (current && currentIndex != index) {
            current = current->next;
            currentIndex++;
        }
        
        // If index is out of bounds or list is empty
        if (!current)
            return false;
        
        // Update the value of the node
        current->data = val;
        return true;
    }
    
    // Method to print the list
    void printList() {
        Node* current = head;
        while (current) {
            cout << current->data << " ";
            current = current->next;
        }
        cout << endl;
    }
    
    // Method to insert a node at the beginning of the list
    void insertAtBeginning(int val) {
        Node* newNode = new Node(val);
        if (!head) {
            head = newNode;
        } else {
            newNode->next = head;
            head->prev = newNode;
            head = newNode;
        }
    }
    
    // Method to insert a node at the end of the list
    void insertAtEnd(int val) {
        Node* newNode = new Node(val);
        if (!head) {
            head = newNode;
        } else {
            Node* current = head;
            while (current->next) {
                current = current->next;
            }
            current->next = newNode;
            newNode->prev = current;
        }
    }
};

int main() {
    DoublyLinkedList dll;
    
    dll.insertAtEnd(1);
    dll.insertAtEnd(2);
    dll.insertAtEnd(3);
    dll.insertAtEnd(4);
    dll.printList(); // Output: 1 2 3 4
    
    dll.set(2, 5); // Set value at index 2 to 5
    dll.printList(); // Output: 1 2 5 4
    
    return 0;
}
```

This code defines a doubly linked list with a `set` method to update the value of a node at a given index. The `printList` method is used to print the list for verification, and `insertAtBeginning` and `insertAtEnd` methods are used to insert nodes at the beginning and end of the list, respectively.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Swap First and Last

To swap the first and last nodes in a doubly linked list in C++, you can follow these steps:

1. Check if the list is empty or has only one node. If so, there's no need to swap.
2. Otherwise, find the first and last nodes.
3. Swap the data of the first and last nodes.
4. Adjust the pointers accordingly.

Here's a C++ implementation:

```cpp
#include <iostream>

using namespace std;

// Node structure for the doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
    Node(int value) : data(value), prev(nullptr), next(nullptr) {}
};

// Doubly linked list class
class DoublyLinkedList {
private:
    Node* head;
    Node* tail;

public:
    DoublyLinkedList() : head(nullptr), tail(nullptr) {}

    // Function to add a new node at the end of the list
    void append(int value) {
        Node* newNode = new Node(value);
        if (!head) {
            head = tail = newNode;
        } else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
    }

    // Function to swap the first and last nodes
    void swapFirstAndLast() {
        if (!head || head == tail) {
            // If the list is empty or has only one node, no need to swap
            return;
        }

        // Find the first and last nodes
        Node* first = head;
        Node* last = tail;

        // Swap data of first and last nodes
        int temp = first->data;
        first->data = last->data;
        last->data = temp;
    }

    // Function to print the elements of the list
    void display() {
        Node* current = head;
        while (current) {
            cout << current->data << " ";
            current = current->next;
        }
        cout << endl;
    }
};

int main() {
    DoublyLinkedList dll;

    // Adding some elements to the list
    dll.append(1);
    dll.append(2);
    dll.append(3);
    dll.append(4);
    dll.append(5);

    cout << "Original list: ";
    dll.display();

    // Swap the first and last nodes
    dll.swapFirstAndLast();

    cout << "List after swapping first and last nodes: ";
    dll.display();

    return 0;
}
```

This code defines a `DoublyLinkedList` class with methods for appending nodes, swapping the first and last nodes, and displaying the list. In the `main()` function, some elements are added to the list, and then the first and last nodes are swapped, followed by displaying the updated list.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Swap Nodes in Pairs

Certainly! Below is a C++ implementation of swapping nodes in pairs in a doubly linked list:

```cpp
#include <iostream>

using namespace std;

// Node structure for doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
    Node(int val) : data(val), prev(nullptr), next(nullptr) {}
};

// Function to swap nodes in pairs
Node* swapPairs(Node* head) {
    if (!head || !head->next) // If the list is empty or has only one node
        return head;

    Node* dummy = new Node(0); // Dummy node to handle edge cases
    dummy->next = head;
    Node* prev = dummy;

    while (prev->next && prev->next->next) {
        Node* first = prev->next;
        Node* second = first->next;

        // Swapping nodes
        prev->next = second;
        first->next = second->next;
        second->prev = prev;
        if (first->next)
            first->next->prev = first;
        second->next = first;
        first->prev = second;

        prev = first;
    }

    Node* newHead = dummy->next;
    delete dummy;
    return newHead;
}

// Function to print the doubly linked list
void printList(Node* head) {
    while (head) {
        cout << head->data << " ";
        head = head->next;
    }
    cout << endl;
}

// Function to delete the doubly linked list
void deleteList(Node* head) {
    Node* temp;
    while (head) {
        temp = head;
        head = head->next;
        delete temp;
    }
}

int main() {
    // Creating a sample doubly linked list: 1 <-> 2 <-> 3 <-> 4 <-> 5
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->prev = head;
    head->next->next = new Node(3);
    head->next->next->prev = head->next;
    head->next->next->next = new Node(4);
    head->next->next->next->prev = head->next->next;
    head->next->next->next->next = new Node(5);
    head->next->next->next->next->prev = head->next->next->next;

    cout << "Original List: ";
    printList(head);

    // Swapping nodes in pairs
    head = swapPairs(head);

    cout << "List after swapping nodes in pairs: ";
    printList(head);

    // Deleting the list to free memory
    deleteList(head);

    return 0;
}
```

This code defines a doubly linked list node structure and provides a function `swapPairs` to swap nodes in pairs. It also includes helper functions to print and delete the doubly linked list. The `main` function demonstrates the usage of the `swapPairs` function with a sample doubly linked list.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Time and Space

A doubly linked list is a data structure consisting of a sequence of elements, where each element contains a reference (or pointer) to the previous and the next elements in the sequence. Here's a breakdown of the time and space complexities associated with common operations on a doubly linked list implemented in C++:

1. **Time Complexities:**

* **Access/Search (by index):** O(n)
  * Accessing or searching for an element by index requires traversing the list from either the head or the tail, which takes linear time.

* **Insertion (at beginning or end):** O(1)
  * Inserting an element at either end (head or tail) of the list can be done in constant time since we have direct access to these points.

* **Insertion (at arbitrary position):** O(n)
  * Inserting an element at an arbitrary position requires traversing the list to find the insertion point, which takes linear time in the worst case.

* **Deletion (at beginning or end):** O(1)
  * Deleting an element from either end (head or tail) of the list can be done in constant time since we have direct access to these points.

* **Deletion (at arbitrary position):** O(n)
  * Deleting an element from an arbitrary position requires traversing the list to find the deletion point, which takes linear time in the worst case.

1. **Space Complexity:**

* **Space Complexity for elements:** O(n)
  * The space complexity for the elements themselves is linear since each element consumes a fixed amount of memory.

* **Space Complexity for pointers:** O(n)
  * In addition to the elements themselves, the pointers (previous and next) associated with each element also consume space, contributing to the linear space complexity.

In summary, doubly linked lists offer efficient insertion and deletion at the beginning and end of the list but require linear time for operations involving traversal or manipulation at arbitrary positions. Additionally, the space complexity is linear due to both the elements and the pointers associated with them.

### 1. Algorithms & Data Structures (C++): Doubly Linked List: Traverse Method

Traversing a doubly linked list involves visiting each node of the list in sequence, starting from the head (or tail) and moving through each node until the end of the list is reached. Here's a C++ implementation of the traverse method for a doubly linked list:

```cpp
#include <iostream>

// Node structure for doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
};

class DoublyLinkedList {
private:
    Node* head;
    Node* tail;

public:
    // Constructor
    DoublyLinkedList() : head(nullptr), tail(nullptr) {}

    // Function to traverse the list from head to tail
    void traverseForward() {
        Node* current = head;
        while (current != nullptr) {
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }

    // Function to traverse the list from tail to head
    void traverseBackward() {
        Node* current = tail;
        while (current != nullptr) {
            std::cout << current->data << " ";
            current = current->prev;
        }
        std::cout << std::endl;
    }

    // Other methods such as insertion, deletion, etc. can be implemented here
};

// Example usage
int main() {
    DoublyLinkedList myList;

    // Insert some elements into the list
    myList.insertAtEnd(1);
    myList.insertAtEnd(2);
    myList.insertAtEnd(3);
    myList.insertAtEnd(4);

    // Traverse the list forward
    std::cout << "Traversing forward: ";
    myList.traverseForward();

    // Traverse the list backward
    std::cout << "Traversing backward: ";
    myList.traverseBackward();

    return 0;
}
```

In this code:

* We define a `Node` structure that represents a node in the doubly linked list, containing data and pointers to the previous and next nodes.
* The `DoublyLinkedList` class maintains pointers to the head and tail of the list.
* The `traverseForward()` method iterates through the list from head to tail, printing each node's data.
* The `traverseBackward()` method iterates through the list from tail to head, printing each node's data.
* In the `main()` function, we demonstrate the usage of these traversal methods after inserting some elements into the list.

### 1. Algorithms & Data Structures (C++): Doubly Linked Lists

Certainly! A doubly linked list is a data structure consisting of a collection of nodes where each node contains a reference to the next node and the previous node in the sequence. It allows traversal in both forward and backward directions. Here's an implementation of a doubly linked list in C++:

```cpp
#include <iostream>

using namespace std;

// Node class representing each element in the doubly linked list
class Node {
public:
    int data;
    Node* next;
    Node* prev;
    
    Node(int val) : data(val), next(nullptr), prev(nullptr) {}
};

// Doubly Linked List class
class DoublyLinkedList {
private:
    Node* head;
    Node* tail;
    int size;

public:
    DoublyLinkedList() : head(nullptr), tail(nullptr), size(0) {}

    // Function to insert a new node at the end of the list
    void insertEnd(int val) {
        Node* newNode = new Node(val);
        if (head == nullptr) {
            head = tail = newNode;
        } else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
        size++;
    }

    // Function to display the list in forward direction
    void displayForward() {
        Node* current = head;
        while (current != nullptr) {
            cout << current->data << " ";
            current = current->next;
        }
        cout << endl;
    }

    // Function to display the list in backward direction
    void displayBackward() {
        Node* current = tail;
        while (current != nullptr) {
            cout << current->data << " ";
            current = current->prev;
        }
        cout << endl;
    }

    // Function to get the size of the list
    int getSize() {
        return size;
    }

    // Destructor to free the memory
    ~DoublyLinkedList() {
        Node* current = head;
        while (current != nullptr) {
            Node* next = current->next;
            delete current;
            current = next;
        }
        head = tail = nullptr;
        size = 0;
    }
};

int main() {
    DoublyLinkedList dll;

    dll.insertEnd(1);
    dll.insertEnd(2);
    dll.insertEnd(3);
    dll.insertEnd(4);
    dll.insertEnd(5);

    cout << "Doubly linked list in forward direction:" << endl;
    dll.displayForward();

    cout << "Doubly linked list in backward direction:" << endl;
    dll.displayBackward();

    cout << "Size of the list: " << dll.getSize() << endl;

    return 0;
}
```

In this implementation, `Node` represents each element in the doubly linked list, containing the data and pointers to the next and previous nodes. The `DoublyLinkedList` class manages the list, including functions to insert nodes at the end, display the list in both forward and backward directions, and get the size of the list. The `main` function demonstrates the usage of the doubly linked list.

### 1. Algorithms & Data Structures (C++): Doubly linked lists creation

Creating a doubly linked list in C++ involves defining a structure for the nodes and implementing functions to perform operations such as insertion, deletion, traversal, and searching. Here's a basic implementation:

```cpp
#include <iostream>

using namespace std;

// Node structure for the doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
    
    // Constructor
    Node(int val) : data(val), prev(nullptr), next(nullptr) {}
};

// Doubly linked list class
class DoublyLinkedList {
private:
    Node* head;
    Node* tail;

public:
    // Constructor
    DoublyLinkedList() : head(nullptr), tail(nullptr) {}

    // Destructor to free allocated memory
    ~DoublyLinkedList() {
        Node* current = head;
        while (current != nullptr) {
            Node* next = current->next;
            delete current;
            current = next;
        }
    }

    // Function to insert a node at the end of the list
    void insertEnd(int val) {
        Node* newNode = new Node(val);
        if (head == nullptr) {
            head = newNode;
            tail = newNode;
        } else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
    }

    // Function to display the list from head to tail
    void displayForward() {
        Node* current = head;
        while (current != nullptr) {
            cout << current->data << " ";
            current = current->next;
        }
        cout << endl;
    }

    // Function to display the list from tail to head
    void displayBackward() {
        Node* current = tail;
        while (current != nullptr) {
            cout << current->data << " ";
            current = current->prev;
        }
        cout << endl;
    }
};

int main() {
    DoublyLinkedList dll;

    // Insert some elements
    dll.insertEnd(1);
    dll.insertEnd(2);
    dll.insertEnd(3);
    dll.insertEnd(4);
    dll.insertEnd(5);

    // Display the list forward and backward
    cout << "Forward: ";
    dll.displayForward();
    cout << "Backward: ";
    dll.displayBackward();

    return 0;
}
```

This implementation defines a `Node` structure with integer data and pointers to the previous and next nodes. The `DoublyLinkedList` class manages the list operations like insertion and display. The `main` function demonstrates how to use this class by inserting elements and displaying the list in both forward and backward directions.

### 1. Algorithms & Data Structures (C++): Doubly linked lists insertion

Certainly! Implementing insertion operations in a doubly linked list involves managing pointers to link nodes both forward and backward. Here's a basic implementation in C++:

```cpp
#include <iostream>

// Node class representing each element in the doubly linked list
class Node {
public:
    int data;
    Node* prev;
    Node* next;
    Node(int val) : data(val), prev(nullptr), next(nullptr) {}
};

// Doubly linked list class
class DoublyLinkedList {
private:
    Node* head;
public:
    DoublyLinkedList() : head(nullptr) {}

    // Function to insert a node at the beginning of the list
    void insertAtBeginning(int val) {
        Node* newNode = new Node(val);
        if (head == nullptr) {
            head = newNode;
        } else {
            newNode->next = head;
            head->prev = newNode;
            head = newNode;
        }
    }

    // Function to insert a node at the end of the list
    void insertAtEnd(int val) {
        Node* newNode = new Node(val);
        if (head == nullptr) {
            head = newNode;
        } else {
            Node* temp = head;
            while (temp->next != nullptr) {
                temp = temp->next;
            }
            temp->next = newNode;
            newNode->prev = temp;
        }
    }

    // Function to display the elements of the list
    void display() {
        Node* temp = head;
        while (temp != nullptr) {
            std::cout << temp->data << " ";
            temp = temp->next;
        }
        std::cout << std::endl;
    }
};

// Main function to test the doubly linked list implementation
int main() {
    DoublyLinkedList dll;
    dll.insertAtBeginning(5);
    dll.insertAtBeginning(3);
    dll.insertAtEnd(7);
    dll.insertAtEnd(9);
    dll.display(); // Output: 3 5 7 9
    return 0;
}
```

This implementation includes insertion at the beginning and end of the doubly linked list. You can extend it to include other operations like insertion at a specific position, deletion, searching, etc., as per your requirements.

### 1. Algorithms & Data Structures (C++): Doubly-Linked List (Implementation)

Sure, here's a basic implementation of a doubly-linked list in C++:

```cpp
#include <iostream>

template <typename T>
class DoublyLinkedList {
private:
    struct Node {
        T data;
        Node* prev;
        Node* next;

        Node(const T& data) : data(data), prev(nullptr), next(nullptr) {}
    };

    Node* head;
    Node* tail;
    size_t size;

public:
    DoublyLinkedList() : head(nullptr), tail(nullptr), size(0) {}

    ~DoublyLinkedList() {
        clear();
    }

    void push_front(const T& value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = newNode;
            tail = newNode;
        } else {
            newNode->next = head;
            head->prev = newNode;
            head = newNode;
        }
        size++;
    }

    void push_back(const T& value) {
        Node* newNode = new Node(value);
        if (tail == nullptr) {
            head = newNode;
            tail = newNode;
        } else {
            newNode->prev = tail;
            tail->next = newNode;
            tail = newNode;
        }
        size++;
    }

    void pop_front() {
        if (head == nullptr) {
            return;
        }
        Node* temp = head;
        head = head->next;
        if (head != nullptr) {
            head->prev = nullptr;
        } else {
            tail = nullptr;
        }
        delete temp;
        size--;
    }

    void pop_back() {
        if (tail == nullptr) {
            return;
        }
        Node* temp = tail;
        tail = tail->prev;
        if (tail != nullptr) {
            tail->next = nullptr;
        } else {
            head = nullptr;
        }
        delete temp;
        size--;
    }

    void clear() {
        while (head != nullptr) {
            Node* temp = head;
            head = head->next;
            delete temp;
        }
        tail = nullptr;
        size = 0;
    }

    size_t getSize() const {
        return size;
    }

    bool empty() const {
        return size == 0;
    }

    void print() const {
        Node* current = head;
        while (current != nullptr) {
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }
};

int main() {
    DoublyLinkedList<int> myList;

    myList.push_back(10);
    myList.push_front(5);
    myList.push_back(20);
    myList.push_front(2);

    std::cout << "List size: " << myList.getSize() << std::endl;
    std::cout << "List contents: ";
    myList.print();

    myList.pop_front();
    myList.pop_back();

    std::cout << "List size after pop operations: " << myList.getSize() << std::endl;
    std::cout << "List contents after pop operations: ";
    myList.print();

    return 0;
}
```

This code defines a `DoublyLinkedList` class template with basic operations like `push_front`, `push_back`, `pop_front`, `pop_back`, `clear`, `getSize`, `empty`, and `print`. It maintains pointers to the head and tail nodes and updates them accordingly during insertion and deletion. Finally, there's a simple `main` function to demonstrate the usage of this doubly-linked list.

### 1. Algorithms & Data Structures (C++): Doubly-Linked List (Theory)

A doubly-linked list is a data structure that consists of a sequence of elements, called nodes, where each node contains a piece of data and two pointers/references to the previous and next nodes in the sequence. Unlike a singly-linked list, which only has a reference to the next node, a doubly-linked list allows traversal in both forward and backward directions.

Here's a theoretical overview of the main components and operations associated with a doubly-linked list in C++:

#### Node Structure

In C++, a node in a doubly-linked list can be defined using a structure or a class. Each node typically contains the following components:

```cpp
struct Node {
    int data;            // Data stored in the node
    Node* prev;          // Pointer to the previous node
    Node* next;          // Pointer to the next node
};
```

#### Operations

1. **Insertion**:
   * **Insertion at the Beginning**: Insert a new node at the beginning of the list.
   * **Insertion at the End**: Insert a new node at the end of the list.
   * **Insertion at a Given Position**: Insert a new node at a specific position in the list.

2. **Deletion**:
   * **Deletion from the Beginning**: Remove the first node from the list.
   * **Deletion from the End**: Remove the last node from the list.
   * **Deletion from a Given Position**: Remove a node from a specific position in the list.

3. **Traversal**: Traverse the list from the beginning to the end or from the end to the beginning.

4. **Searching**: Search for a specific element/data within the list.

5. **Updating**: Update the data stored in a specific node.

#### Advantages

* Allows traversal in both forward and backward directions.
* Supports efficient insertion and deletion operations at both ends of the list.

#### Disadvantages

* Requires extra memory for storing the previous pointers, increasing memory overhead compared to singly-linked lists.
* Increased complexity in terms of implementation due to managing both forward and backward pointers.

#### Implementation Notes

* Care must be taken to properly update the pointers when performing insertion and deletion operations to maintain the integrity of the list.
* Special cases such as inserting into an empty list or deleting the only node in the list should be handled appropriately.

In C++, it's common to encapsulate the functionality of a doubly-linked list into a class, providing member functions to perform various operations on the list while abstracting the details of node manipulation.

### 1. Algorithms & Data Structures (C++): Creating Doubly Linked List

Sure, I can guide you through creating a doubly linked list in C++. A doubly linked list is a data structure where each node contains a data element and two pointers: one pointing to the previous node and one pointing to the next node.

Here's a simple implementation:

```cpp
#include <iostream>

template <typename T>
class Node {
public:
    T data;
    Node* prev;
    Node* next;

    Node(T data) : data(data), prev(nullptr), next(nullptr) {}
};

template <typename T>
class DoublyLinkedList {
private:
    Node<T>* head;
    Node<T>* tail;
    int size;

public:
    DoublyLinkedList() : head(nullptr), tail(nullptr), size(0) {}

    // Function to add a new node to the end of the list
    void append(T data) {
        Node<T>* newNode = new Node<T>(data);
        if (!head) {
            head = tail = newNode;
        } else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
        size++;
    }

    // Function to display the list
    void display() {
        Node<T>* current = head;
        while (current) {
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }

    // Function to display the list in reverse
    void displayReverse() {
        Node<T>* current = tail;
        while (current) {
            std::cout << current->data << " ";
            current = current->prev;
        }
        std::cout << std::endl;
    }

    // Function to get the size of the list
    int getSize() {
        return size;
    }

    // Destructor to free memory
    ~DoublyLinkedList() {
        Node<T>* current = head;
        while (current) {
            Node<T>* temp = current;
            current = current->next;
            delete temp;
        }
    }
};

int main() {
    DoublyLinkedList<int> myList;

    // Appending elements to the list
    myList.append(5);
    myList.append(10);
    myList.append(15);
    myList.append(20);

    // Displaying the list
    std::cout << "List: ";
    myList.display();

    // Displaying the list in reverse
    std::cout << "List in reverse: ";
    myList.displayReverse();

    // Displaying the size of the list
    std::cout << "Size of list: " << myList.getSize() << std::endl;

    return 0;
}
```

This code creates a doubly linked list template class along with a node template class. You can create a list of any data type by instantiating the `DoublyLinkedList` class with the desired data type. The `append()` function adds elements to the end of the list, `display()` function prints the list from head to tail, `displayReverse()` function prints the list from tail to head, and `getSize()` function returns the size of the list. Finally, the destructor is implemented to free the dynamically allocated memory when the list goes out of scope.

### 1. Algorithms & Data Structures (C++): Creating Node of Doubly Linked List

Sure! Here's an example of how you can create a node for a doubly linked list in C++:

```cpp
#include <iostream>

// Define the structure of a node
struct Node {
    int data;       // Data stored in the node
    Node* prev;     // Pointer to the previous node
    Node* next;     // Pointer to the next node

    // Constructor to initialize node with data and null pointers
    Node(int value) : data(value), prev(nullptr), next(nullptr) {}
};

int main() {
    // Creating nodes
    Node* node1 = new Node(10);  // Creating a node with data 10
    Node* node2 = new Node(20);  // Creating a node with data 20
    Node* node3 = new Node(30);  // Creating a node with data 30

    // Linking nodes
    node1->next = node2;  // Linking node1 to node2
    node2->prev = node1;  // Linking node2 to node1
    node2->next = node3;  // Linking node2 to node3
    node3->prev = node2;  // Linking node3 to node2

    // Traversing the list
    Node* current = node1;  // Start from the head node
    while (current != nullptr) {
        std::cout << current->data << " ";
        current = current->next;  // Move to the next node
    }
    std::cout << std::endl;

    // Deallocating memory
    delete node1;
    delete node2;
    delete node3;

    return 0;
}
```

In this code:

* The `Node` structure represents a node in the doubly linked list. It contains three members: `data` to store the data in the node, `prev` to point to the previous node, and `next` to point to the next node.
* The constructor of the `Node` initializes the node with the given data and sets the `prev` and `next` pointers to `nullptr`.
* In the `main()` function, we create three nodes with data values 10, 20, and 30 respectively.
* We then link these nodes together to form a doubly linked list.
* Finally, we traverse the list starting from the head node (`node1`) and print the data stored in each node.

### 1. Algorithms & Data Structures (C++): Delete for Doubly Linked List

Deleting a node from a doubly linked list in C++ involves a few steps:

1. Identify the node to be deleted.
2. Update the pointers of the previous and next nodes to bypass the node to be deleted.
3. Free the memory allocated to the node to be deleted.

Here's a basic implementation:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* prev;
    Node* next;
    Node(int value) : data(value), prev(nullptr), next(nullptr) {}
};

class DoublyLinkedList {
private:
    Node* head;
public:
    DoublyLinkedList() : head(nullptr) {}

    // Function to delete a node from the doubly linked list
    void deleteNode(Node* nodeToDelete) {
        if (head == nullptr || nodeToDelete == nullptr)
            return;

        // If the node to be deleted is head
        if (head == nodeToDelete)
            head = nodeToDelete->next;

        // Change next only if the node to be deleted is NOT the last node
        if (nodeToDelete->next != nullptr)
            nodeToDelete->next->prev = nodeToDelete->prev;

        // Change prev only if the node to be deleted is NOT the first node
        if (nodeToDelete->prev != nullptr)
            nodeToDelete->prev->next = nodeToDelete->next;

        // Free the memory allocated to the node
        delete nodeToDelete;
    }

    // Function to print the doubly linked list
    void printList() {
        Node* temp = head;
        while (temp != nullptr) {
            std::cout << temp->data << " ";
            temp = temp->next;
        }
        std::cout << std::endl;
    }

    // Function to add a node at the end of the doubly linked list
    void append(int data) {
        Node* newNode = new Node(data);
        if (head == nullptr) {
            head = newNode;
            return;
        }

        Node* temp = head;
        while (temp->next != nullptr)
            temp = temp->next;
        
        temp->next = newNode;
        newNode->prev = temp;
    }
};

int main() {
    DoublyLinkedList dll;
    dll.append(1);
    dll.append(2);
    dll.append(3);
    dll.append(4);
    dll.append(5);

    std::cout << "Original list: ";
    dll.printList();

    // Deleting node with data value 3
    Node* nodeToDelete = dll.head->next->next;
    dll.deleteNode(nodeToDelete);

    std::cout << "List after deleting node with data value 3: ";
    dll.printList();

    return 0;
}
```

This code defines a doubly linked list, provides a function to delete a node given its pointer, and demonstrates how to use it. In the `main` function, a doubly linked list is created, and a node with the value 3 is deleted.

### 1. Algorithms & Data Structures (C++): Implementing Doubly Linked Lists Class

Sure, I can guide you through implementing a Doubly Linked List class in C++. A doubly linked list is a data structure that consists of a sequence of elements, where each element points to both the next and the previous element in the sequence.

Here's a basic implementation of a doubly linked list class in C++:

```cpp
#include <iostream>

template<typename T>
class Node {
public:
    T data;
    Node* next;
    Node* prev;

    Node(T val) : data(val), next(nullptr), prev(nullptr) {}
};

template<typename T>
class DoublyLinkedList {
private:
    Node<T>* head;
    Node<T>* tail;
    int size;

public:
    DoublyLinkedList() : head(nullptr), tail(nullptr), size(0) {}

    // Destructor to delete all nodes
    ~DoublyLinkedList() {
        while (head) {
            Node<T>* temp = head;
            head = head->next;
            delete temp;
        }
    }

    // Function to add a new node at the end of the list
    void push_back(T val) {
        Node<T>* newNode = new Node<T>(val);
        if (!head) {
            head = tail = newNode;
        } else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
        size++;
    }

    // Function to add a new node at the beginning of the list
    void push_front(T val) {
        Node<T>* newNode = new Node<T>(val);
        if (!head) {
            head = tail = newNode;
        } else {
            newNode->next = head;
            head->prev = newNode;
            head = newNode;
        }
        size++;
    }

    // Function to remove the last node from the list
    void pop_back() {
        if (!head) return;
        if (head == tail) {
            delete head;
            head = tail = nullptr;
        } else {
            Node<T>* temp = tail;
            tail = tail->prev;
            tail->next = nullptr;
            delete temp;
        }
        size--;
    }

    // Function to remove the first node from the list
    void pop_front() {
        if (!head) return;
        if (head == tail) {
            delete head;
            head = tail = nullptr;
        } else {
            Node<T>* temp = head;
            head = head->next;
            head->prev = nullptr;
            delete temp;
        }
        size--;
    }

    // Function to print the elements of the list
    void print() {
        Node<T>* current = head;
        while (current) {
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }

    // Function to get the size of the list
    int getSize() const {
        return size;
    }

    // Function to check if the list is empty
    bool isEmpty() const {
        return size == 0;
    }
};

int main() {
    DoublyLinkedList<int> dll;

    dll.push_back(1);
    dll.push_back(2);
    dll.push_back(3);
    dll.push_front(0);

    dll.print(); // Output: 0 1 2 3

    dll.pop_back();
    dll.pop_front();

    dll.print(); // Output: 1 2

    std::cout << "Size: " << dll.getSize() << std::endl; // Output: Size: 2

    return 0;
}
```

This code provides a basic implementation of a doubly linked list in C++. It includes functionalities to add nodes at the front and back, remove nodes from the front and back, print the list, get the size of the list, and check if the list is empty. You can expand this implementation by adding more functionality as per your requirements.

### 1. Algorithms & Data Structures (C++): Insert at a Position of a Doubly Linked List

Certainly! Below is a C++ implementation to insert a node at a specific position in a doubly linked list:

```cpp
#include <iostream>

// Node structure for a doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
};

// Function to insert a new node at a given position in a doubly linked list
void insertAtPosition(Node** head_ref, int pos, int data) {
    Node* new_node = new Node();
    new_node->data = data;
    new_node->prev = nullptr;
    new_node->next = nullptr;

    if (*head_ref == nullptr) { // If the list is empty
        *head_ref = new_node;
        return;
    }

    if (pos == 0) { // Insert at the beginning
        new_node->next = *head_ref;
        (*head_ref)->prev = new_node;
        *head_ref = new_node;
        return;
    }

    Node* temp = *head_ref;
    int count = 0;

    // Traverse to the position before the desired position
    while (temp->next != nullptr && count < pos - 1) {
        temp = temp->next;
        count++;
    }

    // If the position is greater than the number of nodes, insert at the end
    if (temp->next == nullptr) {
        temp->next = new_node;
        new_node->prev = temp;
        return;
    }

    // Insert at the desired position
    new_node->next = temp->next;
    new_node->prev = temp;
    temp->next->prev = new_node;
    temp->next = new_node;
}

// Function to print a doubly linked list
void printList(Node* node) {
    while (node != nullptr) {
        std::cout << node->data << " ";
        node = node->next;
    }
    std::cout << std::endl;
}

// Main function
int main() {
    Node* head = nullptr;
    
    // Inserting elements into the doubly linked list
    insertAtPosition(&head, 0, 1);
    insertAtPosition(&head, 1, 2);
    insertAtPosition(&head, 2, 4);
    insertAtPosition(&head, 1, 3);

    // Printing the doubly linked list
    std::cout << "Doubly linked list: ";
    printList(head);

    return 0;
}
```

This code defines a `Node` structure representing a node in a doubly linked list and provides functions to insert a node at a specific position and to print the list. You can customize the insertion logic according to your requirements.

### 1. Algorithms & Data Structures (C++): Insert at the End of a Doubly Linked List

To insert a node at the end of a doubly linked list in C++, you can follow these steps:

1. Create a new node with the given data.
2. Traverse the list to find the last node.
3. Adjust the pointers to link the new node to the last node and the last node to the new node.

Here's the implementation:

```cpp
#include <iostream>

// Node structure for doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
    
    Node(int value) : data(value), prev(nullptr), next(nullptr) {}
};

// Doubly linked list class
class DoublyLinkedList {
private:
    Node* head;
public:
    DoublyLinkedList() : head(nullptr) {}
    
    // Function to insert a node at the end of the list
    void insertAtEnd(int data) {
        Node* newNode = new Node(data);
        if (head == nullptr) {
            head = newNode;
        } else {
            Node* temp = head;
            while (temp->next != nullptr) {
                temp = temp->next;
            }
            temp->next = newNode;
            newNode->prev = temp;
        }
    }
    
    // Function to display the elements of the list
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
    DoublyLinkedList list;
    list.insertAtEnd(1);
    list.insertAtEnd(2);
    list.insertAtEnd(3);
    list.display(); // Output: 1 2 3
    return 0;
}
```

This code creates a doubly linked list and provides a method `insertAtEnd()` to insert a node at the end of the list. The `display()` function is used to print the elements of the list.

### 1. Algorithms & Data Structures (C++): Insert at the Front of a Doubly Linked List

Sure, here's a simple C++ implementation to insert a node at the front of a doubly linked list:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* prev;
    Node* next;
    
    Node(int val) : data(val), prev(nullptr), next(nullptr) {}
};

class DoublyLinkedList {
private:
    Node* head;
public:
    DoublyLinkedList() : head(nullptr) {}
    
    // Function to insert a node at the front of the list
    void insertFront(int val) {
        Node* newNode = new Node(val);
        if (head == nullptr) {
            head = newNode;
        } else {
            newNode->next = head;
            head->prev = newNode;
            head = newNode;
        }
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
    DoublyLinkedList list;
    
    // Insert some elements at the front
    list.insertFront(3);
    list.insertFront(5);
    list.insertFront(7);
    
    // Display the list
    list.display();
    
    return 0;
}
```

In this code:

* `Node` represents each node of the doubly linked list, storing data and pointers to the previous and next nodes.
* `DoublyLinkedList` is the class implementing the doubly linked list.
* `insertFront` inserts a new node at the beginning of the list.
* `display` method is used to display the contents of the list.

In the `main` function, we create a `DoublyLinkedList` object, insert some elements at the front, and then display the list.

### 1. Algorithms & Data Structures (C++): Insert Element Anywhere in between the Doubly Linked List

To insert an element anywhere in between a doubly linked list in C++, you'll need to perform the following steps:

1. Create a new node with the given data.
2. Traverse the list to find the position after which you want to insert the new node.
3. Adjust the pointers of the neighboring nodes to accommodate the new node.

Here's the C++ code to achieve this:

```cpp
#include <iostream>

// Define the structure of a doubly linked list node
struct Node {
    int data;
    Node* prev;
    Node* next;
    Node(int val) : data(val), prev(nullptr), next(nullptr) {}
};

// Function to insert a new node after a given node
void insertAfter(Node* prevNode, int data) {
    if (prevNode == nullptr) {
        std::cout << "Previous node cannot be null.\n";
        return;
    }
    
    Node* newNode = new Node(data);
    newNode->next = prevNode->next;
    newNode->prev = prevNode;
    
    if (prevNode->next != nullptr)
        prevNode->next->prev = newNode;
    
    prevNode->next = newNode;
}

// Function to print the doubly linked list
void printList(Node* head) {
    while (head != nullptr) {
        std::cout << head->data << " ";
        head = head->next;
    }
    std::cout << std::endl;
}

int main() {
    // Create the initial doubly linked list: 1 <-> 2 <-> 3
    Node* head = new Node(1);
    Node* second = new Node(2);
    Node* third = new Node(3);
    
    head->next = second;
    second->prev = head;
    second->next = third;
    third->prev = second;
    
    std::cout << "Initial list: ";
    printList(head);
    
    // Insert 4 after the second node
    insertAfter(second, 4);
    std::cout << "List after insertion: ";
    printList(head);
    
    return 0;
}
```

This code demonstrates how to insert a new node with value `4` after the node containing value `2`. You can modify it according to your requirements to insert a new node at any desired position in the doubly linked list.

### 1. Algorithms & Data Structures (C++): Insert Element at the Beginning of Doubly Linked List

To insert an element at the beginning of a doubly linked list in C++, you would follow these steps:

1. Create a new node with the given value.
2. If the list is empty, set the new node as both the head and tail of the list.
3. If the list is not empty, set the previous pointer of the current head to point to the new node, set the next pointer of the new node to point to the current head, and update the head pointer to point to the new node.

Here's a C++ implementation of the insertion at the beginning of a doubly linked list:

```cpp
#include <iostream>

// Define the structure of a node in the doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
    
    Node(int val) : data(val), prev(nullptr), next(nullptr) {}
};

class DoublyLinkedList {
private:
    Node* head;
    Node* tail;

public:
    DoublyLinkedList() : head(nullptr), tail(nullptr) {}

    // Function to insert a new node at the beginning of the list
    void insertAtBeginning(int value) {
        Node* newNode = new Node(value);
        if (!head) {
            head = tail = newNode;
        } else {
            newNode->next = head;
            head->prev = newNode;
            head = newNode;
        }
    }

    // Function to display the elements of the list
    void display() {
        Node* current = head;
        while (current) {
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }
};

int main() {
    DoublyLinkedList dll;
    
    // Insert elements at the beginning of the list
    dll.insertAtBeginning(3);
    dll.insertAtBeginning(5);
    dll.insertAtBeginning(7);
    
    // Display the list
    dll.display();
    
    return 0;
}
```

This code demonstrates inserting elements 3, 5, and 7 at the beginning of the doubly linked list and then displays the list to confirm the insertion.

### 1. Algorithms & Data Structures (C++): Insert for Doubly Linked List

Sure, here's a simple implementation of the `insert` function for a doubly linked list in C++:

```cpp
#include <iostream>

// Node structure for doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
    
    Node(int value) : data(value), prev(nullptr), next(nullptr) {}
};

// Doubly linked list class
class DoublyLinkedList {
private:
    Node* head;
    Node* tail;
    
public:
    DoublyLinkedList() : head(nullptr), tail(nullptr) {}
    
    // Function to insert a node at the beginning of the list
    void insertAtBeginning(int value) {
        Node* newNode = new Node(value);
        if (!head) {
            head = tail = newNode;
        } else {
            newNode->next = head;
            head->prev = newNode;
            head = newNode;
        }
    }
    
    // Function to insert a node at the end of the list
    void insertAtEnd(int value) {
        Node* newNode = new Node(value);
        if (!tail) {
            head = tail = newNode;
        } else {
            newNode->prev = tail;
            tail->next = newNode;
            tail = newNode;
        }
    }
    
    // Function to insert a node after a given node
    void insertAfter(Node* prevNode, int value) {
        if (!prevNode) {
            std::cout << "Previous node cannot be null.\n";
            return;
        }
        Node* newNode = new Node(value);
        newNode->next = prevNode->next;
        newNode->prev = prevNode;
        if (prevNode->next)
            prevNode->next->prev = newNode;
        else
            tail = newNode;
        prevNode->next = newNode;
    }
    
    // Function to print the list
    void printList() {
        Node* temp = head;
        while (temp != nullptr) {
            std::cout << temp->data << " ";
            temp = temp->next;
        }
        std::cout << std::endl;
    }
};

int main() {
    DoublyLinkedList dll;
    dll.insertAtBeginning(1);
    dll.insertAtEnd(3);
    dll.insertAfter(dll.head, 2);
    dll.printList(); // Output: 1 2 3
    return 0;
}
```

This code defines a doubly linked list with three operations: `insertAtBeginning`, `insertAtEnd`, and `insertAfter`. You can use these functions to insert nodes at the beginning, end, or after a specified node in the list.

### 1. Algorithms & Data Structures (C++): Insert in a Doubly Linked List

Certainly! Below is a simple implementation of inserting a node in a doubly linked list in C++:

```cpp
#include <iostream>

// Node structure for a doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
    Node(int value) : data(value), prev(nullptr), next(nullptr) {}
};

// Function to insert a new node at the beginning of a doubly linked list
void insertAtBeginning(Node*& head, int value) {
    Node* newNode = new Node(value);
    if (head == nullptr) {
        head = newNode;
    } else {
        newNode->next = head;
        head->prev = newNode;
        head = newNode;
    }
}

// Function to display the doubly linked list
void displayList(Node* head) {
    Node* temp = head;
    while (temp != nullptr) {
        std::cout << temp->data << " ";
        temp = temp->next;
    }
    std::cout << std::endl;
}

int main() {
    // Initialize an empty doubly linked list
    Node* head = nullptr;

    // Insert nodes at the beginning
    insertAtBeginning(head, 5);
    insertAtBeginning(head, 10);
    insertAtBeginning(head, 15);

    // Display the doubly linked list
    std::cout << "Doubly linked list: ";
    displayList(head);

    return 0;
}
```

In this implementation, the `insertAtBeginning` function inserts a new node with the given value at the beginning of the doubly linked list. The `displayList` function is used to print the contents of the doubly linked list.

You can extend this code to include other operations like insertion at the end, insertion at a specific position, deletion, etc., depending on your requirements.

### 1. Algorithms & Data Structures (C++): Inserting in Doubly Linked Lists

Inserting elements into a doubly linked list involves updating the pointers of the nodes appropriately to maintain the correct sequence. There are three main cases to consider when inserting a new node:

1. **Inserting at the beginning**: Update the pointers of the new node, the current head, and the old head (if any).
2. **Inserting at the end**: Update the pointers of the new node, the current tail, and the old tail (if any).
3. **Inserting at a specific position (in between)**: Traverse the list to find the appropriate position, then update the pointers of the new node, the node before it, and the node after it.

Here's a basic implementation of a doubly linked list in C++ with insertion functions:

```cpp
#include <iostream>

// Node structure for doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
    
    Node(int value) : data(value), prev(nullptr), next(nullptr) {}
};

class DoublyLinkedList {
private:
    Node* head;
    Node* tail;

public:
    DoublyLinkedList() : head(nullptr), tail(nullptr) {}

    // Function to insert a node at the beginning
    void insertAtBeginning(int value) {
        Node* newNode = new Node(value);
        if (!head) {
            head = newNode;
            tail = newNode;
        } else {
            newNode->next = head;
            head->prev = newNode;
            head = newNode;
        }
    }

    // Function to insert a node at the end
    void insertAtEnd(int value) {
        Node* newNode = new Node(value);
        if (!tail) {
            head = newNode;
            tail = newNode;
        } else {
            newNode->prev = tail;
            tail->next = newNode;
            tail = newNode;
        }
    }

    // Function to insert a node at a specific position
    void insertAtPosition(int value, int position) {
        if (position <= 0) {
            std::cout << "Invalid position.\n";
            return;
        }
        Node* newNode = new Node(value);
        if (position == 1) {
            insertAtBeginning(value);
        } else {
            Node* current = head;
            int currentPosition = 1;
            while (current && currentPosition < position - 1) {
                current = current->next;
                currentPosition++;
            }
            if (!current) {
                std::cout << "Position out of bounds.\n";
                return;
            }
            newNode->next = current->next;
            newNode->prev = current;
            if (current->next)
                current->next->prev = newNode;
            current->next = newNode;
        }
    }

    // Function to display the list
    void display() {
        Node* current = head;
        while (current) {
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }
};

int main() {
    DoublyLinkedList dll;
    dll.insertAtEnd(1);
    dll.insertAtEnd(2);
    dll.insertAtBeginning(0);
    dll.insertAtPosition(3, 3);
    dll.display(); // Output: 0 1 2 3
    return 0;
}
```

This is a basic implementation. You can further optimize and enhance it, for example by adding error handling, destructor for memory deallocation, or additional functionalities like deletion and searching.

### 1. Algorithms & Data Structures (C++): Linked List: Merge Multi-Level Doubly Linked List

To merge multi-level doubly linked lists in C++, you can follow these steps:

1. Define the structure for the doubly linked list node.
2. Implement a function to merge two doubly linked lists.
3. Implement a function to merge multi-level doubly linked lists recursively or iteratively.

Here's a sample implementation:

```cpp
#include <iostream>

using namespace std;

// Structure for the doubly linked list node
struct Node {
    int data;
    Node* prev;
    Node* next;
    Node* child;

    Node(int val) : data(val), prev(nullptr), next(nullptr), child(nullptr) {}
};

// Function to merge two sorted doubly linked lists
Node* merge(Node* first, Node* second) {
    if (!first) return second;
    if (!second) return first;

    if (first->data < second->data) {
        first->next = merge(first->next, second);
        first->next->prev = first;
        first->prev = nullptr;
        return first;
    } else {
        second->next = merge(first, second->next);
        second->next->prev = second;
        second->prev = nullptr;
        return second;
    }
}

// Function to flatten multi-level doubly linked list
Node* flatten(Node* head) {
    if (!head) return head;

    Node* current = head;
    while (current) {
        if (current->child) {
            Node* next = current->next;
            Node* childTail = current->child;
            while (childTail->next) {
                childTail = childTail->next;
            }
            current->next = current->child;
            current->child->prev = current;
            current->child = nullptr;
            childTail->next = next;
            if (next) next->prev = childTail;
        }
        current = current->next;
    }

    return head;
}

// Function to print the doubly linked list
void printList(Node* head) {
    while (head) {
        cout << head->data << " ";
        head = head->next;
    }
    cout << endl;
}

// Sample usage
int main() {
    // Example multi-level doubly linked list
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->prev = head;
    head->next->next = new Node(3);
    head->next->next->prev = head->next;
    head->next->child = new Node(4);
    head->next->child->next = new Node(5);
    head->next->child->next->prev = head->next->child;
    head->next->child->next->next = new Node(6);
    head->next->child->next->next->prev = head->next->child->next;
    head->next->next->child = new Node(7);
    head->next->next->child->next = new Node(8);
    head->next->next->child->next->prev = head->next->next->child;
    head->next->next->child->next->next = new Node(9);
    head->next->next->child->next->next->prev = head->next->next->child->next;

    cout << "Original multi-level doubly linked list:" << endl;
    printList(head);

    head = flatten(head);

    cout << "Flattened doubly linked list:" << endl;
    printList(head);

    return 0;
}
```

This code defines a `Node` structure representing a node in the doubly linked list. The `merge` function merges two sorted doubly linked lists. The `flatten` function flattens a multi-level doubly linked list. Finally, the `printList` function is used to print the contents of the doubly linked list.

You can modify this code according to your requirements and integrate it into your project.

### 1. Algorithms & Data Structures (C++): Playing with links of Doubly Linked List

Doubly linked lists are a fundamental data structure in computer science, offering efficient insertion, deletion, and traversal operations. In C++, you can manipulate doubly linked lists using pointers and structs. Here's a basic implementation to get you started:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* prev;
    Node* next;
    
    Node(int value) : data(value), prev(nullptr), next(nullptr) {}
};

class DoublyLinkedList {
private:
    Node* head;
    Node* tail;

public:
    DoublyLinkedList() : head(nullptr), tail(nullptr) {}

    // Function to insert a node at the end of the list
    void insertEnd(int value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = tail = newNode;
        } else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
    }

    // Function to display the list from head to tail
    void displayForward() {
        Node* current = head;
        while (current != nullptr) {
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }

    // Function to display the list from tail to head
    void displayBackward() {
        Node* current = tail;
        while (current != nullptr) {
            std::cout << current->data << " ";
            current = current->prev;
        }
        std::cout << std::endl;
    }

    // Function to delete a node by its value
    void deleteNode(int value) {
        Node* current = head;
        while (current != nullptr) {
            if (current->data == value) {
                if (current == head) {
                    head = head->next;
                    if (head != nullptr)
                        head->prev = nullptr;
                } else if (current == tail) {
                    tail = tail->prev;
                    if (tail != nullptr)
                        tail->next = nullptr;
                } else {
                    current->prev->next = current->next;
                    current->next->prev = current->prev;
                }
                delete current;
                return;
            }
            current = current->next;
        }
    }

    // Destructor to free memory
    ~DoublyLinkedList() {
        Node* current = head;
        while (current != nullptr) {
            Node* temp = current;
            current = current->next;
            delete temp;
        }
    }
};

int main() {
    DoublyLinkedList dll;

    dll.insertEnd(1);
    dll.insertEnd(2);
    dll.insertEnd(3);
    dll.insertEnd(4);

    std::cout << "Forward: ";
    dll.displayForward();

    std::cout << "Backward: ";
    dll.displayBackward();

    dll.deleteNode(3);

    std::cout << "Forward after deletion: ";
    dll.displayForward();

    return 0;
}
```

This code provides a basic implementation of a doubly linked list in C++. It allows you to insert nodes at the end of the list, display the list both forward and backward, and delete nodes by their values. You can build upon this foundation to implement additional functionality or optimize it further as needed.

### 1. Algorithms & Data Structures (C++): Reverse a Doubly Linked List

To reverse a doubly linked list in C++, you need to swap the next and previous pointers of each node in the list. Here's a sample implementation:

```cpp
#include <iostream>

// Node structure for doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
};

// Function to reverse a doubly linked list
Node* reverseDoublyLinkedList(Node* head) {
    Node* current = head;
    Node* temp = nullptr;

    // Swap next and prev pointers for all nodes of doubly linked list
    while (current != nullptr) {
        temp = current->prev;
        current->prev = current->next;
        current->next = temp;
        current = current->prev; // Move to the next node
    }

    // Check if list is empty or has only one node
    if (temp != nullptr) {
        head = temp->prev; // Update head to the last node
    }

    return head;
}

// Function to insert a node at the beginning of a doubly linked list
Node* insertNode(Node* head, int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->prev = nullptr;
    newNode->next = head;

    if (head != nullptr) {
        head->prev = newNode;
    }

    return newNode;
}

// Function to display a doubly linked list
void displayList(Node* head) {
    while (head != nullptr) {
        std::cout << head->data << " ";
        head = head->next;
    }
    std::cout << std::endl;
}

int main() {
    Node* head = nullptr;

    // Inserting nodes into the doubly linked list
    head = insertNode(head, 1);
    head = insertNode(head, 2);
    head = insertNode(head, 3);
    head = insertNode(head, 4);
    head = insertNode(head, 5);

    std::cout << "Original list: ";
    displayList(head);

    // Reversing the doubly linked list
    head = reverseDoublyLinkedList(head);

    std::cout << "Reversed list: ";
    displayList(head);

    return 0;
}
```

This code defines a `Node` structure for doubly linked list elements and provides functions to insert nodes, display the list, and reverse it. In the `reverseDoublyLinkedList` function, it iterates through the list, swapping the `prev` and `next` pointers for each node. Finally, it updates the `head` pointer to point to the new first node after reversal.

### 1. Algorithms & Data Structures (C++): Reversing Doubly Linked List

Sure, reversing a doubly linked list in C++ involves swapping the pointers of each node to reverse the direction of the list. Here's how you can implement it:

```cpp
#include <iostream>

// Node structure for doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
    Node(int val) : data(val), prev(nullptr), next(nullptr) {}
};

// Function to reverse a doubly linked list
Node* reverseDoublyLinkedList(Node* head) {
    Node* current = head;
    Node* temp = nullptr;

    // Swap next and prev pointers for all nodes of the doubly linked list
    while (current != nullptr) {
        temp = current->prev;
        current->prev = current->next;
        current->next = temp;
        current = current->prev; // Move to the next node
    }

    // Check if the list is empty or has only one node
    if (temp != nullptr) {
        head = temp->prev; // Update the new head
    }

    return head;
}

// Function to print the doubly linked list
void printDoublyLinkedList(Node* head) {
    while (head != nullptr) {
        std::cout << head->data << " ";
        head = head->next;
    }
    std::cout << std::endl;
}

// Test the implementation
int main() {
    // Create a sample doubly linked list: 1 <-> 2 <-> 3 <-> 4 <-> 5
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->prev = head;
    head->next->next = new Node(3);
    head->next->next->prev = head->next;
    head->next->next->next = new Node(4);
    head->next->next->next->prev = head->next->next;
    head->next->next->next->next = new Node(5);
    head->next->next->next->next->prev = head->next->next->next;

    std::cout << "Original doubly linked list: ";
    printDoublyLinkedList(head);

    // Reverse the doubly linked list
    head = reverseDoublyLinkedList(head);

    std::cout << "Reversed doubly linked list: ";
    printDoublyLinkedList(head);

    return 0;
}
```

This code defines a `Node` struct to represent each node of the doubly linked list. The `reverseDoublyLinkedList` function reverses the list by swapping the `prev` and `next` pointers of each node iteratively. Finally, `printDoublyLinkedList` is used to print the doubly linked list.

### 1. Algorithms & Data Structures (C++): Singly VS Doubly Linked Lists

Singly and doubly linked lists are fundamental data structures in computer science and are used to store collections of data. Here's a comparison between the two:

1. **Memory Usage:**
   * Singly Linked List: Each node in a singly linked list contains a reference to the next node in the sequence. Hence, it uses less memory compared to a doubly linked list.
   * Doubly Linked List: Each node in a doubly linked list contains references to both the next and the previous nodes. This additional reference increases memory usage compared to a singly linked list.

2. **Traversal:**
   * Singly Linked List: Traversal in a singly linked list can only be done in one direction, starting from the head (the first node) and progressing through each subsequent node.
   * Doubly Linked List: Traversal can be done in both directions: forward (from the head to the tail) and backward (from the tail to the head), as each node has references to both its previous and next nodes.

3. **Insertion and Deletion:**
   * Singly Linked List: Insertion and deletion at the beginning of the list can be done efficiently by updating the head pointer. However, for insertion and deletion at arbitrary positions or at the end of the list, traversal from the head to the desired position is necessary, which can take linear time.
   * Doubly Linked List: Similar to a singly linked list, insertion and deletion at the beginning and end of the list can be done efficiently by updating the head and tail pointers. Additionally, insertion and deletion at arbitrary positions can be more efficient since traversal can be done in both directions.

4. **Implementation Complexity:**
   * Singly Linked List: Implementing a singly linked list is generally simpler compared to a doubly linked list due to the lack of backward pointers.
   * Doubly Linked List: Implementing a doubly linked list requires handling both forward and backward pointers, which adds complexity to the implementation.

5. **Memory Management:**
   * Singly Linked List: In memory management systems like C or C++, singly linked lists are generally preferred due to their simpler structure and lower memory overhead.
   * Doubly Linked List: While offering more flexibility, doubly linked lists consume more memory due to the additional pointers per node.

The choice between singly and doubly linked lists depends on the specific requirements of the application. If memory usage needs to be minimized or operations mostly involve traversal from the head, a singly linked list might be preferred. However, if frequent insertion, deletion, or traversal in both directions is required, a doubly linked list might be a better choice despite its slightly higher memory overhead and implementation complexity.

### 1. Algorithms & Data Structures (C++): Sorting Doubly Linked List

Sorting a doubly linked list involves rearranging its elements in a specific order, typically in non-decreasing (ascending) or non-increasing (descending) order. Here's how you can implement sorting algorithms like Bubble Sort, Selection Sort, Insertion Sort, or Merge Sort for a doubly linked list in C++:

```cpp
#include <iostream>

using namespace std;

// Node structure for doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
    Node(int val) : data(val), prev(nullptr), next(nullptr) {}
};

// Function to insert a node at the end of a doubly linked list
void insertEnd(Node*& head, int data) {
    Node* newNode = new Node(data);
    if (!head) {
        head = newNode;
        return;
    }
    Node* temp = head;
    while (temp->next) {
        temp = temp->next;
    }
    temp->next = newNode;
    newNode->prev = temp;
}

// Function to swap data of two nodes
void swapData(Node* a, Node* b) {
    int temp = a->data;
    a->data = b->data;
    b->data = temp;
}

// Bubble sort for doubly linked list
void bubbleSort(Node* head) {
    if (!head || !head->next)
        return;

    Node* end = nullptr;
    bool swapped;
    do {
        swapped = false;
        Node* current = head;
        while (current->next != end) {
            if (current->data > current->next->data) {
                swapData(current, current->next);
                swapped = true;
            }
            current = current->next;
        }
        end = current;
    } while (swapped);
}

// Function to print the doubly linked list
void printList(Node* head) {
    while (head) {
        cout << head->data << " ";
        head = head->next;
    }
    cout << endl;
}

// Driver code
int main() {
    Node* head = nullptr;
    insertEnd(head, 5);
    insertEnd(head, 2);
    insertEnd(head, 10);
    insertEnd(head, 1);
    insertEnd(head, 7);

    cout << "Original list: ";
    printList(head);

    bubbleSort(head);

    cout << "Sorted list: ";
    printList(head);

    return 0;
}
```

This example includes the implementation of Bubble Sort for sorting a doubly linked list in C++. The `Node` struct defines the structure of a doubly linked list node. The `insertEnd` function inserts a node at the end of the list. `swapData` swaps the data of two nodes. `bubbleSort` implements the Bubble Sort algorithm for the doubly linked list. Finally, `printList` prints the elements of the list, and `main` function serves as the driver code.

### 1. Algorithms & Data Structures (C++): Traversing Doubly Linked List

Traversing a doubly linked list in C++ involves moving through each node from the beginning to the end or vice versa, accessing or modifying the data stored in each node. Here's a basic example:

```cpp
#include <iostream>

// Node structure for a doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
    
    // Constructor to initialize node
    Node(int value) : data(value), prev(nullptr), next(nullptr) {}
};

// Function to traverse and print the elements of the doubly linked list forwards
void traverseForward(Node* head) {
    std::cout << "Forward Traversal: ";
    while (head != nullptr) {
        std::cout << head->data << " ";
        head = head->next;
    }
    std::cout << std::endl;
}

// Function to traverse and print the elements of the doubly linked list backwards
void traverseBackward(Node* tail) {
    std::cout << "Backward Traversal: ";
    while (tail != nullptr) {
        std::cout << tail->data << " ";
        tail = tail->prev;
    }
    std::cout << std::endl;
}

int main() {
    // Creating nodes
    Node* head = new Node(1);
    Node* second = new Node(2);
    Node* third = new Node(3);
    Node* fourth = new Node(4);
    
    // Connecting nodes
    head->next = second;
    second->prev = head;
    second->next = third;
    third->prev = second;
    third->next = fourth;
    fourth->prev = third;
    
    // Traversing and printing doubly linked list forwards
    traverseForward(head);
    
    // Traversing and printing doubly linked list backwards
    traverseBackward(fourth);
    
    // Deleting nodes to free memory
    delete head;
    delete second;
    delete third;
    delete fourth;
    
    return 0;
}
```

This code creates a doubly linked list with four nodes, traverses it forwards and backwards, and then deletes the nodes to avoid memory leaks.

### 1. Algorithms & Data Structures (C++): What is Doubly Linked List? Node Class Constructor

A doubly linked list is a type of linked list where each node contains a data field and two pointers, one pointing to the next node in the sequence and the other pointing to the previous node. This allows traversal of the list in both forward and backward directions.

Here's a basic implementation of a node class for a doubly linked list in C++ along with its constructor:

```cpp
#include <iostream>

template <typename T>
class Node {
public:
    T data;
    Node<T>* next;
    Node<T>* prev;

    // Constructor
    Node(const T& value, Node<T>* nextNode = nullptr, Node<T>* prevNode = nullptr) : 
        data(value), next(nextNode), prev(prevNode) {}
};

int main() {
    // Example usage
    Node<int>* node1 = new Node<int>(1);
    Node<int>* node2 = new Node<int>(2);
    Node<int>* node3 = new Node<int>(3);

    // Linking nodes
    node1->next = node2;
    node2->prev = node1;
    node2->next = node3;
    node3->prev = node2;

    // Traversing forward
    Node<int>* current = node1;
    while (current != nullptr) {
        std::cout << current->data << " ";
        current = current->next;
    }
    std::cout << std::endl;

    // Traversing backward
    current = node3;
    while (current != nullptr) {
        std::cout << current->data << " ";
        current = current->prev;
    }
    std::cout << std::endl;

    // Clean up
    delete node1;
    delete node2;
    delete node3;

    return 0;
}
```

In this code:

* The `Node` class template takes a template parameter `T` representing the type of data the node will store.
* It has three member variables: `data` to store the value of the node, `next` to point to the next node, and `prev` to point to the previous node.
* The constructor initializes the `data` member with the given value and sets the `next` and `prev` pointers to the provided nodes or `nullptr` if not provided.
* In the `main()` function, we create three nodes and link them together to form a doubly linked list.
* We then traverse the list both forward and backward to demonstrate the bidirectional traversal capability of the doubly linked list.
* Finally, we delete the dynamically allocated nodes to avoid memory leaks.

### 1. Algorithms & Data Structures (C++): Class ADT for Doubly Linked lists

Certainly! Below is a basic implementation of a doubly linked list in C++:

```cpp
#include <iostream>

template <typename T>
class Node {
public:
    T data;
    Node* prev;
    Node* next;
    Node(T data) : data(data), prev(nullptr), next(nullptr) {}
};

template <typename T>
class DoublyLinkedList {
private:
    Node<T>* head;
    Node<T>* tail;
    int size;

public:
    DoublyLinkedList() : head(nullptr), tail(nullptr), size(0) {}

    ~DoublyLinkedList() {
        Node<T>* current = head;
        while (current != nullptr) {
            Node<T>* next = current->next;
            delete current;
            current = next;
        }
    }

    // Method to add a new node to the end of the list
    void append(T data) {
        Node<T>* newNode = new Node<T>(data);
        if (head == nullptr) {
            head = tail = newNode;
        } else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
        size++;
    }

    // Method to print the elements of the list
    void print() {
        Node<T>* current = head;
        while (current != nullptr) {
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }

    // Method to get the size of the list
    int getSize() const {
        return size;
    }

    // Method to check if the list is empty
    bool isEmpty() const {
        return size == 0;
    }
};

int main() {
    DoublyLinkedList<int> list;
    list.append(1);
    list.append(2);
    list.append(3);

    std::cout << "List elements: ";
    list.print();
    std::cout << "List size: " << list.getSize() << std::endl;

    return 0;
}
```

In this implementation:

* `Node` class represents each node in the doubly linked list. It contains the data and pointers to the previous and next nodes.
* `DoublyLinkedList` class represents the doubly linked list. It contains a pointer to the head node, a pointer to the tail node, and the size of the list.
* Methods include `append()` to add a new node to the end of the list, `print()` to print the elements of the list, `getSize()` to get the size of the list, and `isEmpty()` to check if the list is empty.
* In the `main()` function, a test of the implementation is shown by creating a `DoublyLinkedList<int>`, adding elements to it, and printing its contents and size.

### 1. Algorithms & Data Structures (C++): Delete Element Anywhere in between Doubly Linked List

Deleting an element from a doubly linked list involves finding the node containing the value to delete and then adjusting the pointers of its adjacent nodes to bypass the node to be deleted. Here's a C++ implementation:

```cpp
#include <iostream>

// Node structure for doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
    
    Node(int value) : data(value), prev(nullptr), next(nullptr) {}
};

// Doubly linked list class
class DoublyLinkedList {
private:
    Node* head;
    Node* tail;
    
public:
    DoublyLinkedList() : head(nullptr), tail(nullptr) {}
    
    // Function to insert a node at the end of the list
    void append(int value) {
        Node* newNode = new Node(value);
        if (tail == nullptr) {
            head = tail = newNode;
        } else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
    }
    
    // Function to delete a node with given value
    void deleteNode(int value) {
        Node* current = head;
        
        // Traverse the list to find the node with the given value
        while (current != nullptr && current->data != value) {
            current = current->next;
        }
        
        // If node not found
        if (current == nullptr) {
            std::cout << "Node with value " << value << " not found." << std::endl;
            return;
        }
        
        // Adjust pointers of adjacent nodes to bypass the node to be deleted
        if (current->prev != nullptr) {
            current->prev->next = current->next;
        } else {
            head = current->next;
        }
        
        if (current->next != nullptr) {
            current->next->prev = current->prev;
        } else {
            tail = current->prev;
        }
        
        delete current; // Free memory
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
};

int main() {
    DoublyLinkedList dll;
    dll.append(1);
    dll.append(2);
    dll.append(3);
    dll.append(4);
    dll.append(5);
    
    std::cout << "Original List: ";
    dll.display();
    
    // Delete element 3
    dll.deleteNode(3);
    std::cout << "List after deleting 3: ";
    dll.display();
    
    // Delete element 1
    dll.deleteNode(1);
    std::cout << "List after deleting 1: ";
    dll.display();
    
    // Delete element 5
    dll.deleteNode(5);
    std::cout << "List after deleting 5: ";
    dll.display();
    
    return 0;
}
```

This implementation allows you to delete elements from anywhere in the doubly linked list.

### 1. Algorithms & Data Structures (C++): Delete Element at Beginning of Doubly Linked List

Deleting an element at the beginning of a doubly linked list in C++ involves adjusting pointers to remove the first node. Here's how you can implement it:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* prev;
    Node* next;
    Node(int val) : data(val), prev(nullptr), next(nullptr) {}
};

class DoublyLinkedList {
private:
    Node* head;
public:
    DoublyLinkedList() : head(nullptr) {}

    // Function to delete the first node
    void deleteFirst() {
        if (head == nullptr) {
            std::cout << "List is empty. Nothing to delete.\n";
            return;
        }
        
        Node* temp = head;
        head = head->next;
        if (head != nullptr) {
            head->prev = nullptr;
        }
        delete temp;
    }

    // Function to display the list
    void display() {
        Node* current = head;
        while (current != nullptr) {
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }

    // Function to insert a node at the beginning
    void insertFirst(int val) {
        Node* newNode = new Node(val);
        newNode->next = head;
        if (head != nullptr) {
            head->prev = newNode;
        }
        head = newNode;
    }
};

int main() {
    DoublyLinkedList list;
    list.insertFirst(3);
    list.insertFirst(7);
    list.insertFirst(10);
    list.display(); // Output: 10 7 3
    list.deleteFirst();
    list.display(); // Output: 7 3
    list.deleteFirst();
    list.display(); // Output: 3
    list.deleteFirst();
    list.display(); // Output: List is empty. Nothing to delete.

    return 0;
}
```

In this code:

* The `Node` struct represents each element of the doubly linked list, containing data and pointers to the previous and next nodes.
* The `DoublyLinkedList` class manages the operations on the list.
* `deleteFirst()` function removes the first node from the list.
* `display()` function prints the elements of the list.
* `insertFirst()` function inserts a new node at the beginning of the list.

### 1. Algorithms & Data Structures (C++): Deleting from Doubly Linked List

Deleting from a doubly linked list in C++ involves a few steps, primarily identifying the node to delete and then updating the pointers of the adjacent nodes to bypass the node being deleted. Here's a basic example of how you can delete a node from a doubly linked list:

```cpp
#include <iostream>

// Node structure for the doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
    
    Node(int val) : data(val), prev(nullptr), next(nullptr) {}
};

// Function to delete a node from the doubly linked list
void deleteNode(Node* &head, Node* target) {
    // Check if the list is empty or target node is null
    if (head == nullptr || target == nullptr)
        return;
    
    // If the node to be deleted is the head node
    if (head == target) {
        head = target->next; // Update head to the next node
        if (head != nullptr)
            head->prev = nullptr; // Update the new head's previous pointer
        delete target; // Delete the target node
        return;
    }
    
    // Adjust the pointers of the surrounding nodes
    if (target->prev != nullptr)
        target->prev->next = target->next;
    if (target->next != nullptr)
        target->next->prev = target->prev;
    
    // Delete the target node
    delete target;
}

// Function to print the doubly linked list
void printList(Node* head) {
    while (head != nullptr) {
        std::cout << head->data << " ";
        head = head->next;
    }
    std::cout << std::endl;
}

int main() {
    // Creating a sample doubly linked list: 1 <-> 2 <-> 3 <-> 4
    Node* head = new Node(1);
    Node* second = new Node(2);
    Node* third = new Node(3);
    Node* fourth = new Node(4);
    
    head->next = second;
    second->prev = head;
    second->next = third;
    third->prev = second;
    third->next = fourth;
    fourth->prev = third;
    
    std::cout << "Original list: ";
    printList(head);
    
    // Deleting the node containing data 2
    deleteNode(head, second);
    
    std::cout << "List after deletion: ";
    printList(head);
    
    return 0;
}
```

This code demonstrates deleting a node from a doubly linked list in C++. The `deleteNode` function takes the head of the list and the target node to delete. It adjusts the pointers of the previous and next nodes of the target node to bypass it, and then deletes the target node.

### 1. Algorithms & Data Structures (C++): Deleting from Doubly Linked Lists

Deleting from a doubly linked list in C++ involves several steps to ensure proper removal of the node while maintaining the integrity of the list. Here's how you can implement the deletion of a node from a doubly linked list:

```cpp
#include <iostream>

// Define the structure of a node
struct Node {
    int data;
    Node* prev;
    Node* next;
    
    // Constructor to initialize a node
    Node(int value) : data(value), prev(nullptr), next(nullptr) {}
};

// Function to delete a node from a doubly linked list
void deleteNode(Node** head_ref, Node* del_node) {
    // Base case: If the list is empty or del_node is nullptr, return
    if (*head_ref == nullptr || del_node == nullptr)
        return;
    
    // If the node to be deleted is the head node
    if (*head_ref == del_node)
        *head_ref = del_node->next;
    
    // If the node to be deleted is not the last node
    if (del_node->next != nullptr)
        del_node->next->prev = del_node->prev;
    
    // If the node to be deleted is not the first node
    if (del_node->prev != nullptr)
        del_node->prev->next = del_node->next;
    
    // Free the memory occupied by the del_node
    delete del_node;
}

// Function to print the elements of the doubly linked list
void printList(Node* node) {
    while (node != nullptr) {
        std::cout << node->data << " ";
        node = node->next;
    }
    std::cout << std::endl;
}

// Main function
int main() {
    // Create a doubly linked list: 1 <-> 2 <-> 3 <-> 4 <-> 5
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->prev = head;
    head->next->next = new Node(3);
    head->next->next->prev = head->next;
    head->next->next->next = new Node(4);
    head->next->next->next->prev = head->next->next;
    head->next->next->next->next = new Node(5);
    head->next->next->next->next->prev = head->next->next->next;

    std::cout << "Original list: ";
    printList(head);

    // Delete node with value 3
    deleteNode(&head, head->next->next);
    std::cout << "List after deleting node with value 3: ";
    printList(head);

    // Delete node with value 1
    deleteNode(&head, head);
    std::cout << "List after deleting node with value 1: ";
    printList(head);

    // Delete node with value 5
    deleteNode(&head, head->next->next->next->next);
    std::cout << "List after deleting node with value 5: ";
    printList(head);

    return 0;
}
```

This code defines a `Node` struct representing each element of the doubly linked list. The `deleteNode` function is responsible for removing a specific node from the list. Finally, the `printList` function is used to print the elements of the list before and after deletion for demonstration purposes.

### 1. Algorithms & Data Structures (C++): Deletion at the End of the Doubly Linked List

Deleting a node at the end of a doubly linked list in C++ involves a few steps. Here's how you can implement it:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* prev;
    Node* next;
    
    Node(int val) : data(val), prev(nullptr), next(nullptr) {}
};

class DoublyLinkedList {
private:
    Node* head;
    Node* tail;
public:
    DoublyLinkedList() : head(nullptr), tail(nullptr) {}
    
    // Function to delete a node at the end of the doubly linked list
    void deleteEnd() {
        if (tail == nullptr) {
            std::cout << "List is empty. Nothing to delete." << std::endl;
            return;
        }
        
        Node* temp = tail;
        
        if (tail->prev != nullptr) {
            tail = tail->prev;
            tail->next = nullptr;
        } else {
            // If there is only one node in the list
            head = tail = nullptr;
        }
        
        delete temp;
    }
    
    // Function to insert a node at the end of the doubly linked list
    void insertEnd(int val) {
        Node* newNode = new Node(val);
        
        if (tail == nullptr) {
            head = tail = newNode;
        } else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
    }
    
    // Function to display the doubly linked list
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
    DoublyLinkedList dll;
    
    dll.insertEnd(1);
    dll.insertEnd(2);
    dll.insertEnd(3);
    
    std::cout << "Original Doubly Linked List: ";
    dll.display();
    
    dll.deleteEnd();
    
    std::cout << "Doubly Linked List after deletion at the end: ";
    dll.display();
    
    return 0;
}
```

This code defines a doubly linked list with nodes having integer data. The `deleteEnd()` function deletes the last node in the list, adjusting pointers accordingly. The `insertEnd()` function inserts a new node at the end of the list. The `display()` function is used to print the elements of the list.

In the `main()` function, we demonstrate the usage of these functions by inserting elements into the list and then deleting the last element.

### 1. Algorithms & Data Structures (C++): Deletion at the Front of the Doubly Linked List

Deleting a node at the front of a doubly linked list in C++ involves a few steps:

1. Check if the list is empty. If it is, there's nothing to delete.
2. If the list is not empty, update the `head` pointer to point to the next node.
3. Free the memory occupied by the node being deleted.
4. If the list is now empty, update the `tail` pointer as well.

Here's a sample C++ code to demonstrate this:

```cpp
#include <iostream>

// Define the structure for a node in the doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
    
    Node(int val) : data(val), prev(nullptr), next(nullptr) {}
};

class DoublyLinkedList {
private:
    Node* head;
    Node* tail;
public:
    DoublyLinkedList() : head(nullptr), tail(nullptr) {}

    // Function to delete a node at the front of the doubly linked list
    void deleteFront() {
        // Check if the list is empty
        if (head == nullptr) {
            std::cout << "List is empty. Nothing to delete." << std::endl;
            return;
        }

        // Save the reference to the node to be deleted
        Node* toDelete = head;

        // Update the head to point to the next node
        head = head->next;

        // If the list is not empty, update the previous pointer of the new head to nullptr
        if (head != nullptr) {
            head->prev = nullptr;
        } else {
            // If the list becomes empty after deletion, update the tail pointer as well
            tail = nullptr;
        }

        // Delete the node
        delete toDelete;
    }

    // Function to display the doubly linked list
    void display() {
        Node* current = head;
        while (current != nullptr) {
            std::cout << current->data << " <-> ";
            current = current->next;
        }
        std::cout << "nullptr" << std::endl;
    }

    // Function to insert a node at the end of the doubly linked list
    void insertEnd(int data) {
        Node* newNode = new Node(data);
        if (tail == nullptr) {
            head = tail = newNode;
        } else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
    }
};

int main() {
    DoublyLinkedList dll;
    dll.insertEnd(1);
    dll.insertEnd(2);
    dll.insertEnd(3);
    dll.insertEnd(4);
    dll.display(); // Output: 1 <-> 2 <-> 3 <-> 4 <-> nullptr

    dll.deleteFront();
    dll.display(); // Output: 2 <-> 3 <-> 4 <-> nullptr

    dll.deleteFront();
    dll.display(); // Output: 3 <-> 4 <-> nullptr

    dll.deleteFront();
    dll.display(); // Output: 4 <-> nullptr

    dll.deleteFront();
    dll.display(); // Output: List is empty. Nothing to delete.

    return 0;
}
```

This code demonstrates the deletion of nodes at the front of a doubly linked list in C++.

### 1. Algorithms & Data Structures (C++): Time Complexity : Insert at a Position of a Doubly Linked Lis

In a doubly linked list, inserting an element at a specific position involves traversing the list to find the position where insertion is required and then performing the insertion operation. Here's a brief explanation of the time complexity:

1. **Traversing to the insertion point**: In the worst case, you might need to traverse the list from either the head or the tail to reach the insertion point. This traversal takes O(n) time, where n is the number of elements in the list.

2. **Insertion operation**: After finding the insertion point, the insertion operation itself is generally constant time since we have direct access to the nodes in a doubly linked list. This operation typically involves creating a new node, adjusting the pointers of adjacent nodes, and updating pointers in the new node. So, it's O(1).

Therefore, the time complexity of inserting an element at a specific position in a doubly linked list is O(n) due to the traversal to find the insertion point, where n is the number of elements in the list.

In C++, the implementation might look something like this:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* prev;
    Node* next;
};

// Function to insert a new node at a given position
void insertAtPosition(Node** head_ref, int position, int new_data) {
    // Check if position is valid
    if (position < 1) {
        std::cerr << "Invalid position\n";
        return;
    }

    Node* new_node = new Node();
    new_node->data = new_data;

    if (position == 1) {
        // Insert at the beginning
        new_node->next = *head_ref;
        new_node->prev = nullptr;
        if (*head_ref != nullptr)
            (*head_ref)->prev = new_node;
        *head_ref = new_node;
    } else {
        Node* temp = *head_ref;
        // Traverse to the position
        for (int i = 1; i < position - 1 && temp != nullptr; ++i)
            temp = temp->next;

        if (temp == nullptr) {
            std::cerr << "Position out of range\n";
            return;
        }

        // Insert after temp
        new_node->next = temp->next;
        new_node->prev = temp;
        if (temp->next != nullptr)
            temp->next->prev = new_node;
        temp->next = new_node;
    }
}

// Function to print the doubly linked list
void printList(Node* node) {
    while (node != nullptr) {
        std::cout << node->data << " ";
        node = node->next;
    }
    std::cout << "\n";
}

// Main function
int main() {
    Node* head = nullptr;

    // Inserting elements at different positions
    insertAtPosition(&head, 1, 10);
    insertAtPosition(&head, 2, 20);
    insertAtPosition(&head, 2, 30);
    insertAtPosition(&head, 1, 5);

    // Print the list
    printList(head);

    return 0;
}
```

This code demonstrates how to insert elements at different positions in a doubly linked list in C++.
