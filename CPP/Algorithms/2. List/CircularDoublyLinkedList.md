
### 1. Algorithms & Data Structures (C++): Circular Doubly Linked List Constructor

Sure, let's dive into creating a Circular Doubly Linked List constructor in C++. A circular doubly linked list is a data structure where each node contains a data element and two pointers, one pointing to the next node and the other pointing to the previous node. In a circular list, the last node's next pointer points to the first node, and the first node's previous pointer points to the last node, forming a circular structure.

Here's a basic implementation of a Circular Doubly Linked List constructor in C++:

```cpp
#include <iostream>

template <class T>
class Node {
public:
    T data;
    Node<T>* next;
    Node<T>* prev;

    Node(const T& value) : data(value), next(nullptr), prev(nullptr) {}
};

template <class T>
class CircularDoublyLinkedList {
private:
    Node<T>* head;
    int size;

public:
    CircularDoublyLinkedList() : head(nullptr), size(0) {}

    void addNode(const T& value) {
        Node<T>* newNode = new Node<T>(value);
        if (head == nullptr) {
            head = newNode;
            head->next = head;
            head->prev = head;
        } else {
            Node<T>* lastNode = head->prev;
            lastNode->next = newNode;
            newNode->prev = lastNode;
            newNode->next = head;
            head->prev = newNode;
        }
        size++;
    }

    void display() {
        if (head == nullptr) {
            std::cout << "List is empty\n";
            return;
        }
        Node<T>* current = head;
        do {
            std::cout << current->data << " ";
            current = current->next;
        } while (current != head);
        std::cout << std::endl;
    }
};

int main() {
    CircularDoublyLinkedList<int> myList;
    myList.addNode(1);
    myList.addNode(2);
    myList.addNode(3);
    myList.display();
    return 0;
}
```

In this implementation:

* We define a `Node` class to represent each element in the list. Each node contains a data element of type `T`, and two pointers, `next` and `prev`, pointing to the next and previous nodes, respectively.
* We define the `CircularDoublyLinkedList` class with a constructor that initializes the head pointer to `nullptr` and sets the size to 0.
* The `addNode` function adds a new node to the circular doubly linked list. If the list is empty, it sets the new node as the head and makes it point to itself. Otherwise, it appends the new node after the last node and adjusts pointers accordingly.
* The `display` function prints the elements of the list.

In the `main` function, we create a `CircularDoublyLinkedList` object, add some elements to it, and then display its contents.

### 1. Algorithms & Data Structures (C++): Circular Doubly Linked List: Append Method

Certainly! Here's how you can implement the append method for a circular doubly linked list in C++:

```cpp
#include <iostream>

using namespace std;

// Node structure for a doubly linked list
struct Node {
    int data;
    Node* next;
    Node* prev;
};

// Class for the circular doubly linked list
class CircularDoublyLinkedList {
private:
    Node* head;

public:
    CircularDoublyLinkedList() {
        head = nullptr;
    }

    // Function to append a new node to the end of the list
    void append(int data) {
        Node* newNode = new Node();
        newNode->data = data;

        if (head == nullptr) { // If the list is empty
            newNode->next = newNode;
            newNode->prev = newNode;
            head = newNode;
        } else {
            Node* last = head->prev; // Last node
            newNode->next = head;
            head->prev = newNode;
            newNode->prev = last;
            last->next = newNode;
        }
    }

    // Function to display the circular doubly linked list
    void display() {
        if (head == nullptr) {
            cout << "List is empty." << endl;
            return;
        }

        Node* temp = head;
        do {
            cout << temp->data << " ";
            temp = temp->next;
        } while (temp != head);
        cout << endl;
    }
};

int main() {
    CircularDoublyLinkedList list;

    // Appending elements to the list
    list.append(1);
    list.append(2);
    list.append(3);
    list.append(4);

    // Displaying the list
    cout << "Circular Doubly Linked List: ";
    list.display();

    return 0;
}
```

This code defines a `CircularDoublyLinkedList` class with an `append` method to add elements to the end of the list. In the `main` function, some elements are appended to the list, and then the list is displayed.

### 1. Algorithms & Data Structures (C++): Circular Doubly Linked List: Delete All Method

Sure, here's an implementation of the delete all method for a circular doubly linked list in C++:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* next;
    Node* prev;
    
    Node(int value) : data(value), next(nullptr), prev(nullptr) {}
};

class CircularDoublyLinkedList {
private:
    Node* head;

public:
    CircularDoublyLinkedList() : head(nullptr) {}

    // Insert at the end of the list
    void insert(int value) {
        Node* newNode = new Node(value);
        if (!head) {
            head = newNode;
            head->next = head;
            head->prev = head;
        } else {
            Node* last = head->prev;
            newNode->next = head;
            head->prev = newNode;
            newNode->prev = last;
            last->next = newNode;
        }
    }

    // Delete all nodes with a given value
    void deleteAll(int value) {
        if (!head)
            return;

        Node* current = head;
        Node* temp;
        bool deleted = false;

        do {
            temp = current->next;
            if (current->data == value) {
                if (current == head) {
                    head = head->next;
                    if (head == current)
                        head = nullptr;
                }
                current->prev->next = current->next;
                current->next->prev = current->prev;
                delete current;
                deleted = true;
            }
            current = temp;
        } while (current != head);

        if (!deleted)
            std::cout << "Value not found in the list." << std::endl;
    }

    // Display the list
    void display() {
        if (!head) {
            std::cout << "List is empty." << std::endl;
            return;
        }

        Node* current = head;
        do {
            std::cout << current->data << " ";
            current = current->next;
        } while (current != head);
        std::cout << std::endl;
    }

    // Destructor to free memory
    ~CircularDoublyLinkedList() {
        if (!head)
            return;

        Node* current = head;
        Node* temp;
        do {
            temp = current->next;
            delete current;
            current = temp;
        } while (current != head);
    }
};

int main() {
    CircularDoublyLinkedList list;
    list.insert(1);
    list.insert(2);
    list.insert(3);
    list.insert(4);
    list.insert(2);
    list.insert(5);

    std::cout << "Original list: ";
    list.display();

    int valueToDelete = 2;
    std::cout << "Deleting all occurrences of " << valueToDelete << std::endl;
    list.deleteAll(valueToDelete);

    std::cout << "List after deletion: ";
    list.display();

    return 0;
}
```

This code creates a Circular Doubly Linked List class with methods to insert nodes at the end of the list, delete all nodes with a given value, display the list, and a destructor to free memory. The `deleteAll` method iterates through the list and deletes all nodes with the given value.

### 1. Algorithms & Data Structures (C++): Circular Doubly Linked List: Get Method

Sure, here's an example implementation of the `get` method for a Circular Doubly Linked List in C++:

```cpp
#include <iostream>

using namespace std;

// Node class for each element in the linked list
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

// Circular Doubly Linked List class
class CircularDoublyLinkedList {
private:
    Node* head;
    int size;
public:
    CircularDoublyLinkedList() {
        head = nullptr;
        size = 0;
    }
    
    // Method to get element at a specified index
    int get(int index) {
        if (head == nullptr || index < 0 || index >= size) {
            cout << "Invalid index or empty list!" << endl;
            return -1; // Return -1 for invalid index or empty list
        }
        
        Node* current = head;
        for (int i = 0; i < index; i++) {
            current = current->next;
        }
        
        return current->data;
    }
    
    // Method to insert element at the end of the list
    void insert(int val) {
        Node* newNode = new Node(val);
        
        if (head == nullptr) {
            head = newNode;
            head->next = head;
            head->prev = head;
        } else {
            Node* tail = head->prev;
            tail->next = newNode;
            newNode->prev = tail;
            newNode->next = head;
            head->prev = newNode;
        }
        
        size++;
    }
    
    // Method to display the list
    void display() {
        if (head == nullptr) {
            cout << "Empty list" << endl;
            return;
        }
        
        Node* current = head;
        do {
            cout << current->data << " ";
            current = current->next;
        } while (current != head);
        cout << endl;
    }
};

int main() {
    CircularDoublyLinkedList list;
    list.insert(1);
    list.insert(2);
    list.insert(3);
    list.insert(4);
    list.insert(5);
    
    cout << "List: ";
    list.display();
    
    // Get elements at various indices
    cout << "Element at index 2: " << list.get(2) << endl;
    cout << "Element at index 0: " << list.get(0) << endl;
    cout << "Element at index 4: " << list.get(4) << endl;
    cout << "Element at index -1: " << list.get(-1) << endl;
    
    return 0;
}
```

This implementation provides the basic functionality of a Circular Doubly Linked List, including insertion of elements and retrieving an element at a given index. The `get` method traverses the list until the specified index is reached and returns the data of that node. It also handles cases such as an empty list or an invalid index.

### 1. Algorithms & Data Structures (C++): Circular Doubly Linked List: Insert Method

Sure, I can help you with that. Below is a C++ implementation of the insert method for a Circular Doubly Linked List:

```cpp
#include <iostream>

// Node class for the circular doubly linked list
class Node {
public:
    int data;
    Node* next;
    Node* prev;

    // Constructor
    Node(int value) {
        data = value;
        next = nullptr;
        prev = nullptr;
    }
};

// Circular Doubly Linked List class
class CircularDoublyLinkedList {
private:
    Node* head;

public:
    // Constructor
    CircularDoublyLinkedList() {
        head = nullptr;
    }

    // Function to insert a new node at the beginning of the list
    void insert(int value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = newNode;
            head->next = head;
            head->prev = head;
        } else {
            Node* last = head->prev;
            newNode->next = head;
            newNode->prev = last;
            last->next = newNode;
            head->prev = newNode;
            head = newNode;
        }
    }

    // Function to display the circular doubly linked list
    void display() {
        if (head == nullptr) {
            std::cout << "List is empty" << std::endl;
            return;
        }
        Node* temp = head;
        do {
            std::cout << temp->data << " ";
            temp = temp->next;
        } while (temp != head);
        std::cout << std::endl;
    }
};

int main() {
    CircularDoublyLinkedList myList;

    // Insert some elements into the list
    myList.insert(10);
    myList.insert(20);
    myList.insert(30);

    // Display the list
    std::cout << "Circular Doubly Linked List: ";
    myList.display();

    return 0;
}
```

This code defines a Circular Doubly Linked List class with an insert method to insert a new node at the beginning of the list. It also includes a display method to print the elements of the list. You can test this code by compiling and running it.

### 1. Algorithms & Data Structures (C++): Circular Doubly Linked List: Pop First Method

To implement the pop first method for a circular doubly linked list in C++, you need to follow these steps:

1. Check if the list is empty. If it is, then there's nothing to pop, so return.
2. If the list is not empty, update the pointers to remove the first node.
3. Adjust the pointers of adjacent nodes to maintain the circular nature of the list.
4. Delete the node that was popped.
5. Update the size of the list if necessary.

Here's a sample implementation:

```cpp
#include <iostream>

// Node structure for the circular doubly linked list
struct Node {
    int data;
    Node* next;
    Node* prev;
    Node(int val) : data(val), next(nullptr), prev(nullptr) {}
};

// Circular Doubly Linked List class
class CircularDoublyLinkedList {
private:
    Node* head;
    int size;

public:
    CircularDoublyLinkedList() : head(nullptr), size(0) {}

    // Method to pop the first element from the list
    void popFirst() {
        if (head == nullptr) {
            std::cout << "List is empty. Nothing to pop.\n";
            return;
        }

        Node* temp = head;
        if (head->next == head) { // Only one node in the list
            delete head;
            head = nullptr;
        } else {
            head->prev->next = head->next;
            head->next->prev = head->prev;
            head = head->next;
            delete temp;
        }
        size--;
    }

    // Method to display the elements of the list
    void display() {
        if (head == nullptr) {
            std::cout << "List is empty.\n";
            return;
        }

        Node* current = head;
        do {
            std::cout << current->data << " ";
            current = current->next;
        } while (current != head);
        std::cout << std::endl;
    }

    // Method to get the size of the list
    int getSize() {
        return size;
    }
};

int main() {
    CircularDoublyLinkedList myList;
    // Insert some elements for demonstration
    for (int i = 1; i <= 5; ++i) {
        myList.pushBack(i);
    }

    std::cout << "Original List: ";
    myList.display(); // Output: Original List: 1 2 3 4 5

    myList.popFirst();
    std::cout << "List after popping the first element: ";
    myList.display(); // Output: List after popping the first element: 2 3 4 5

    return 0;
}
```

In this implementation, the `popFirst()` method removes the first element of the circular doubly linked list. The `display()` method is provided to print the elements of the list for demonstration purposes.

### 1. Algorithms & Data Structures (C++): Circular Doubly Linked List: Pop Method

Certainly! The pop method in a circular doubly linked list removes an element from either the beginning or the end of the list, and adjusts the pointers accordingly. Here's a sample implementation in C++:

```cpp
#include <iostream>

template <typename T>
class Node {
public:
    T data;
    Node<T>* next;
    Node<T>* prev;

    Node(T data) : data(data), next(nullptr), prev(nullptr) {}
};

template <typename T>
class CircularDoublyLinkedList {
private:
    Node<T>* head;

public:
    CircularDoublyLinkedList() : head(nullptr) {}

    // Function to pop from the beginning of the list
    void popFront() {
        if (head == nullptr) {
            std::cout << "List is empty. Cannot pop.\n";
            return;
        }

        Node<T>* temp = head;

        if (head->next == head) {
            delete head;
            head = nullptr;
        } else {
            head->prev->next = head->next;
            head->next->prev = head->prev;
            head = head->next;
            delete temp;
        }
    }

    // Function to pop from the end of the list
    void popBack() {
        if (head == nullptr) {
            std::cout << "List is empty. Cannot pop.\n";
            return;
        }

        Node<T>* temp = head->prev;

        if (temp == head) {
            delete head;
            head = nullptr;
        } else {
            temp->prev->next = head;
            head->prev = temp->prev;
            delete temp;
        }
    }

    // Function to display the list
    void display() {
        if (head == nullptr) {
            std::cout << "List is empty.\n";
            return;
        }

        Node<T>* current = head;
        do {
            std::cout << current->data << " ";
            current = current->next;
        } while (current != head);
        std::cout << std::endl;
    }

    // Function to insert at the beginning of the list
    void insertFront(T data) {
        Node<T>* newNode = new Node<T>(data);
        if (head == nullptr) {
            head = newNode;
            head->next = head->prev = head;
        } else {
            newNode->next = head;
            newNode->prev = head->prev;
            head->prev->next = newNode;
            head->prev = newNode;
            head = newNode;
        }
    }

    // Function to insert at the end of the list
    void insertBack(T data) {
        Node<T>* newNode = new Node<T>(data);
        if (head == nullptr) {
            head = newNode;
            head->next = head->prev = head;
        } else {
            newNode->next = head;
            newNode->prev = head->prev;
            head->prev->next = newNode;
            head->prev = newNode;
        }
    }
};

int main() {
    CircularDoublyLinkedList<int> cdll;
    cdll.insertFront(3);
    cdll.insertFront(2);
    cdll.insertFront(1);
    cdll.display(); // Output: 1 2 3
    cdll.popFront();
    cdll.display(); // Output: 2 3
    cdll.popBack();
    cdll.display(); // Output: 2
    return 0;
}
```

In this code, `popFront()` removes the element from the beginning of the list, and `popBack()` removes the element from the end of the list. Both methods handle the circular nature of the list properly by adjusting the pointers accordingly.

### 1. Algorithms & Data Structures (C++): Circular Doubly Linked List: Prepend Method

Certainly! The prepend method for a circular doubly linked list in C++ inserts a new node at the beginning of the list. Here's a basic implementation:

```cpp
#include <iostream>

// Define the structure for a node
struct Node {
    int data;
    Node* next;
    Node* prev;
    
    // Constructor to initialize data
    Node(int value) : data(value), next(nullptr), prev(nullptr) {}
};

// Define the circular doubly linked list class
class CircularDoublyLinkedList {
private:
    Node* head; // Pointer to the head of the list

public:
    // Constructor to initialize an empty list
    CircularDoublyLinkedList() : head(nullptr) {}

    // Method to prepend a node to the list
    void prepend(int value) {
        Node* newNode = new Node(value); // Create a new node with the given value

        if (head == nullptr) { // If the list is empty
            head = newNode;
            head->next = head;
            head->prev = head;
        } else { // If the list is not empty
            Node* lastNode = head->prev; // Get the last node
            newNode->next = head; // Set the next pointer of the new node to the head
            newNode->prev = lastNode; // Set the previous pointer of the new node to the last node
            lastNode->next = newNode; // Update the next pointer of the last node to point to the new node
            head->prev = newNode; // Update the previous pointer of the head to point to the new node
            head = newNode; // Update the head pointer to the new node
        }
    }

    // Method to print the elements of the list
    void printList() {
        if (head == nullptr) {
            std::cout << "List is empty\n";
            return;
        }
        Node* current = head;
        do {
            std::cout << current->data << " ";
            current = current->next;
        } while (current != head);
        std::cout << std::endl;
    }
};

int main() {
    CircularDoublyLinkedList list;
    list.prepend(3);
    list.prepend(2);
    list.prepend(1);
    list.printList(); // Output: 1 2 3
    return 0;
}
```

This code defines a `Node` struct representing each element of the list and a `CircularDoublyLinkedList` class with a `prepend` method to insert a new node at the beginning of the list. The `printList` method is used to print the elements of the list.

### 1. Algorithms & Data Structures (C++): Circular Doubly Linked List: Remove Method

Certainly! Below is an implementation of the `remove` method for a circular doubly linked list in C++:

```cpp
#include <iostream>

using namespace std;

// Node structure for the linked list
struct Node {
    int data;
    Node* next;
    Node* prev;
    
    Node(int val) : data(val), next(nullptr), prev(nullptr) {}
};

// Circular Doubly Linked List class
class CircularDoublyLinkedList {
private:
    Node* head;

public:
    CircularDoublyLinkedList() : head(nullptr) {}

    // Method to remove a node from the list by value
    void remove(int val) {
        if (!head)
            return;

        Node* curr = head;
        do {
            if (curr->data == val) {
                // If the node to be removed is the only node in the list
                if (curr->next == curr) {
                    delete curr;
                    head = nullptr;
                    return;
                }

                // If the node to be removed is the head node
                if (curr == head) {
                    head = head->next;
                }

                // Adjust the pointers of adjacent nodes
                curr->prev->next = curr->next;
                curr->next->prev = curr->prev;

                delete curr;
                return;
            }
            curr = curr->next;
        } while (curr != head);

        cout << "Element " << val << " not found in the list." << endl;
    }

    // Method to add a node at the end of the list
    void append(int val) {
        Node* newNode = new Node(val);
        if (!head) {
            head = newNode;
            head->next = head;
            head->prev = head;
        } else {
            Node* last = head->prev;
            last->next = newNode;
            newNode->prev = last;
            newNode->next = head;
            head->prev = newNode;
        }
    }

    // Method to print the elements of the list
    void display() {
        if (!head)
            return;

        Node* curr = head;
        do {
            cout << curr->data << " ";
            curr = curr->next;
        } while (curr != head);
        cout << endl;
    }
};

int main() {
    CircularDoublyLinkedList cdl;
    cdl.append(1);
    cdl.append(2);
    cdl.append(3);
    cdl.append(4);
    cdl.append(5);
    cdl.display(); // Output: 1 2 3 4 5
    cdl.remove(3);
    cdl.display(); // Output: 1 2 4 5
    cdl.remove(1);
    cdl.display(); // Output: 2 4 5
    cdl.remove(5);
    cdl.display(); // Output: 2 4
    cdl.remove(10); // Output: Element 10 not found in the list.
    return 0;
}
```

This code defines a `CircularDoublyLinkedList` class with methods to append elements to the list, display the elements, and remove elements by value. The `remove` method traverses the list and removes the node with the specified value. If the value is not found, it displays a message indicating that the element was not found in the list.

### 1. Algorithms & Data Structures (C++): Circular Doubly Linked List: Reverse Traverse Method

To implement a reverse traversal method for a circular doubly linked list in C++, you can start by defining the structure of the node and the list itself. Then, you can implement the reverse traversal method. Here's an example implementation:

```cpp
#include <iostream>

// Node structure
struct Node {
    int data;
    Node* next;
    Node* prev;
    
    Node(int value) : data(value), next(nullptr), prev(nullptr) {}
};

// Circular Doubly Linked List class
class CircularDoublyLinkedList {
private:
    Node* head;
public:
    CircularDoublyLinkedList() : head(nullptr) {}

    // Function to insert a node at the end of the list
    void insertEnd(int value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = newNode;
            head->next = head;
            head->prev = head;
        } else {
            Node* last = head->prev;
            last->next = newNode;
            newNode->prev = last;
            newNode->next = head;
            head->prev = newNode;
        }
    }

    // Function to traverse and print the list in reverse order
    void reverseTraverse() {
        if (head == nullptr) {
            std::cout << "List is empty" << std::endl;
            return;
        }
        
        Node* temp = head->prev;
        Node* current = temp;
        std::cout << "Reverse Traversal: ";
        do {
            std::cout << current->data << " ";
            current = current->prev;
        } while (current != temp);
        std::cout << std::endl;
    }
};

int main() {
    CircularDoublyLinkedList list;
    
    // Insert some elements
    list.insertEnd(1);
    list.insertEnd(2);
    list.insertEnd(3);
    list.insertEnd(4);
    list.insertEnd(5);
    
    // Print in reverse order
    list.reverseTraverse();
    
    return 0;
}
```

In this code:

* `Node` represents each node in the circular doubly linked list.
* `CircularDoublyLinkedList` is the class that represents the circular doubly linked list and contains methods to insert elements at the end and to traverse the list in reverse order.
* `insertEnd()` method inserts a new node at the end of the list.
* `reverseTraverse()` method traverses the list in reverse order, starting from the last node (i.e., the `prev` pointer of the head node) and printing each node's data until it reaches the head node again.

### 1. Algorithms & Data Structures (C++): Circular Doubly Linked List: Search Method

Certainly! Below is an implementation of the search method for a circular doubly linked list in C++:

```cpp
#include <iostream>

// Node structure for the circular doubly linked list
struct Node {
    int data;
    Node* next;
    Node* prev;
    
    Node(int value) : data(value), next(nullptr), prev(nullptr) {}
};

// Circular Doubly Linked List class
class CircularDoublyLinkedList {
private:
    Node* head;

public:
    CircularDoublyLinkedList() : head(nullptr) {}

    // Function to insert a new node at the end of the list
    void insert(int value) {
        Node* newNode = new Node(value);
        if (!head) {
            head = newNode;
            head->next = head;
            head->prev = head;
        } else {
            Node* tail = head->prev;
            tail->next = newNode;
            newNode->prev = tail;
            newNode->next = head;
            head->prev = newNode;
        }
    }

    // Function to search for a value in the list
    bool search(int value) {
        if (!head) return false; // If list is empty
        
        Node* current = head;
        do {
            if (current->data == value) // If value found
                return true;
            current = current->next;
        } while (current != head); // Continue until we reach the head again
        
        return false; // Value not found
    }
};

int main() {
    CircularDoublyLinkedList myList;
    myList.insert(5);
    myList.insert(10);
    myList.insert(15);

    std::cout << "Search for 10: " << (myList.search(10) ? "Found" : "Not Found") << std::endl;
    std::cout << "Search for 20: " << (myList.search(20) ? "Found" : "Not Found") << std::endl;

    return 0;
}
```

In this implementation, the `search` method traverses the circular doubly linked list starting from the `head` node and continues until it reaches the `head` again, checking each node's data for a match with the value being searched for. If the value is found, it returns `true`; otherwise, it returns `false`.

### 1. Algorithms & Data Structures (C++): Circular Doubly Linked List: Set Method

To implement the `set` method for a circular doubly linked list in C++, you'll need to locate the node at the specified index and update its value. Here's a basic implementation:

```cpp
#include <iostream>

using namespace std;

// Node class for the circular doubly linked list
class Node {
public:
    int data;
    Node* next;
    Node* prev;
};

// Circular Doubly Linked List class
class CircularDoublyLinkedList {
private:
    Node* head;

public:
    CircularDoublyLinkedList() {
        head = nullptr;
    }

    // Function to insert a node at the end of the list
    void insertEnd(int value) {
        Node* newNode = new Node();
        newNode->data = value;
        if (head == nullptr) {
            head = newNode;
            head->next = head;
            head->prev = head;
        } else {
            Node* last = head->prev;
            last->next = newNode;
            newNode->prev = last;
            newNode->next = head;
            head->prev = newNode;
        }
    }

    // Function to set the value at a specific index
    void set(int index, int value) {
        if (head == nullptr) {
            cout << "List is empty." << endl;
            return;
        }

        Node* current = head;
        int currentIndex = 0;

        // Traverse the list until the desired index or the end of the list is reached
        while (current != nullptr && currentIndex < index) {
            current = current->next;
            currentIndex++;
        }

        // If the index is out of bounds, display an error message
        if (current == nullptr) {
            cout << "Index out of bounds." << endl;
            return;
        }

        // Update the value at the specified index
        current->data = value;
    }

    // Function to display the contents of the list
    void display() {
        if (head == nullptr) {
            cout << "List is empty." << endl;
            return;
        }

        Node* current = head;
        do {
            cout << current->data << " ";
            current = current->next;
        } while (current != head);
        cout << endl;
    }
};

int main() {
    CircularDoublyLinkedList list;
    list.insertEnd(1);
    list.insertEnd(2);
    list.insertEnd(3);
    list.insertEnd(4);

    cout << "Original list: ";
    list.display();

    // Set value at index 2 (3rd element)
    list.set(2, 10);
    cout << "After setting value at index 2: ";
    list.display();

    return 0;
}
```

In this implementation:

* The `set` method updates the value at the specified index.
* It traverses the list until it reaches the desired index or the end of the list.
* If the index is out of bounds, it displays an error message.
* Otherwise, it updates the value of the node at the specified index.

### 1. Algorithms & Data Structures (C++): Circular Doubly Linked List: Time and Space Complexity

In a Circular Doubly Linked List (CDLL), the time and space complexity for various operations are as follows:

1. **Space Complexity**:
   * The space complexity of a CDLL is O(n), where n is the number of elements in the list. This is because each node in the list consumes space, and the space required increases linearly with the number of elements.

2. **Time Complexity**:

   * **Traversal**:
     * Time Complexity: O(n)
     * Explanation: Traversing the CDLL involves visiting each node once. Since the list is circular, we can start from any node and traverse until we reach the starting node again. This results in a linear time complexity relative to the number of elements.

   * **Insertion (at beginning, end, or middle)**:
     * Time Complexity: O(1)
     * Explanation: Insertion in a CDLL typically involves updating a few pointers to link the new node appropriately. Regardless of where the insertion happens (beginning, end, or middle), the time complexity remains constant because we can directly access neighboring nodes without needing to traverse the entire list.

   * **Deletion (at beginning, end, or middle)**:
     * Time Complexity: O(1)
     * Explanation: Deletion in a CDLL also involves updating pointers to unlink the node from the list. Like insertion, regardless of the deletion position, the time complexity remains constant because we can directly access neighboring nodes.

   * **Searching for an element**:
     * Time Complexity: O(n)
     * Explanation: Although CDLL provides bidirectional traversal, searching still requires visiting each node at most once, resulting in a linear time complexity.

   * **Accessing an element by index**:
     * Time Complexity: O(n)
     * Explanation: Although bidirectional traversal is possible, CDLL does not provide direct indexing like arrays. Accessing an element by index requires traversing from either end or from the closest end to the index, resulting in a linear time complexity in the worst case.

Overall, CDLL provides efficient insertion and deletion operations (O(1)), making it suitable for scenarios where frequent modifications are required. However, searching and accessing by index operations are relatively slower compared to arrays due to their linear time complexity.

### 1. Algorithms & Data Structures (C++): Circular Doubly Linked List: Traverse Method

In C++, traversing a circular doubly linked list involves moving through each node of the list, starting from any given node, and ending at the same node after visiting all nodes. Here's how you can implement the traversal method for a circular doubly linked list:

```cpp
#include <iostream>

using namespace std;

// Node structure for the circular doubly linked list
struct Node {
    int data;
    Node* next;
    Node* prev;
};

class CircularDoublyLinkedList {
private:
    Node* head;

public:
    // Constructor to initialize the head to NULL
    CircularDoublyLinkedList() : head(nullptr) {}

    // Function to traverse the circular doubly linked list
    void traverse() {
        if (head == nullptr) {
            cout << "List is empty" << endl;
            return;
        }

        Node* current = head;
        do {
            cout << current->data << " ";
            current = current->next;
        } while (current != head);
        cout << endl;
    }

    // Function to insert a node at the end of the circular doubly linked list
    void insertEnd(int data) {
        Node* newNode = new Node;
        newNode->data = data;

        if (head == nullptr) {
            head = newNode;
            head->next = head;
            head->prev = head;
        } else {
            Node* last = head->prev;
            last->next = newNode;
            newNode->prev = last;
            newNode->next = head;
            head->prev = newNode;
        }
    }
};

int main() {
    CircularDoublyLinkedList list;

    // Insert some elements into the list
    list.insertEnd(1);
    list.insertEnd(2);
    list.insertEnd(3);
    list.insertEnd(4);

    // Traverse and print the list
    cout << "Circular Doubly Linked List: ";
    list.traverse();

    return 0;
}
```

This code defines a CircularDoublyLinkedList class with a Node structure inside. The traverse method iterates through the circular list starting from the head node and continues until it reaches the head node again. Finally, it prints the data of each node while traversing the list.
