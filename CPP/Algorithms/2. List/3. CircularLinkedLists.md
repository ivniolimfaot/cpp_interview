### 1. Algorithms & Data Structures (C++): Circular Linked List

A circular linked list is a variation of a linked list where the last node points back to the first node, forming a circular structure. This can be useful in certain situations, such as representing a circular buffer or for implementing certain algorithms like round-robin scheduling. Here's a simple implementation of a circular linked list in C++:

```cpp
#include <iostream>

using namespace std;

// Define a node for the circular linked list
class Node {
public:
    int data;
    Node* next;

    Node(int value) {
        data = value;
        next = nullptr;
    }
};

// Define the circular linked list class
class CircularLinkedList {
private:
    Node* head;

public:
    CircularLinkedList() {
        head = nullptr;
    }

    // Insert at the beginning of the list
    void insert(int value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = newNode;
            head->next = head; // point to itself
        } else {
            Node* temp = head;
            while (temp->next != head) {
                temp = temp->next;
            }
            temp->next = newNode;
            newNode->next = head;
            head = newNode;
        }
    }

    // Display the contents of the list
    void display() {
        if (head == nullptr) {
            cout << "List is empty" << endl;
            return;
        }

        Node* temp = head;
        do {
            cout << temp->data << " ";
            temp = temp->next;
        } while (temp != head);
        cout << endl;
    }

    // Delete a node with given value
    void deleteNode(int value) {
        if (head == nullptr) {
            cout << "List is empty" << endl;
            return;
        }

        Node* temp = head;
        Node* prev = nullptr;
        // Find the node to delete
        while (temp->data != value && temp->next != head) {
            prev = temp;
            temp = temp->next;
        }

        if (temp->data != value) {
            cout << "Node with value " << value << " not found" << endl;
            return;
        }

        // If the node to delete is head
        if (temp == head) {
            prev = head;
            while (prev->next != head)
                prev = prev->next;
            if (head == head->next)
                head = nullptr;
            else {
                prev->next = head->next;
                head = head->next;
            }
        } else {
            prev->next = temp->next;
        }

        delete temp;
        cout << "Node with value " << value << " deleted" << endl;
    }
};

int main() {
    CircularLinkedList list;
    list.insert(1);
    list.insert(2);
    list.insert(3);
    list.insert(4);
    list.insert(5);

    cout << "Circular Linked List: ";
    list.display();

    list.deleteNode(3);
    cout << "After deleting node with value 3: ";
    list.display();

    return 0;
}
```

This code creates a basic circular linked list class with functionality to insert elements at the beginning, delete nodes by value, and display the contents of the list.

### 1. Algorithms & Data Structures (C++): Circular Linked List: Delete Node

In C++, deleting a node from a circular linked list involves a few steps. Here's a basic implementation:

```cpp
#include <iostream>

using namespace std;

// Node structure
struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

// Function to delete a node from a circular linked list
void deleteNode(Node* head, int key) {
    if (head == nullptr)
        return;

    Node* curr = head;
    Node* prev = nullptr;

    // Traverse the list to find the node to be deleted
    do {
        if (curr->data == key) {
            // If the node to be deleted is the head node
            if (curr == head && curr->next != head) {
                Node* temp = head;
                while (temp->next != head)
                    temp = temp->next;
                temp->next = head->next;
                head = head->next;
                delete curr;
                return;
            }
            // If the node to be deleted is the only node in the list
            else if (curr == head && curr->next == head) {
                head = nullptr;
                delete curr;
                return;
            }
            // If the node to be deleted is any other node
            else {
                prev->next = curr->next;
                delete curr;
                return;
            }
        }
        prev = curr;
        curr = curr->next;
    } while (curr != head);

    cout << "Node with key " << key << " not found in the list." << endl;
}

// Function to print the circular linked list
void printList(Node* head) {
    if (head == nullptr)
        return;

    Node* temp = head;
    do {
        cout << temp->data << " ";
        temp = temp->next;
    } while (temp != head);
    cout << endl;
}

int main() {
    // Creating a sample circular linked list: 1 -> 2 -> 3 -> 4 -> 1
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->next = new Node(3);
    head->next->next->next = new Node(4);
    head->next->next->next->next = head; // Making it circular

    cout << "Original List: ";
    printList(head);

    // Deleting node with key 3
    deleteNode(head, 3);
    cout << "List after deleting node with key 3: ";
    printList(head);

    // Deleting node with key 1 (head node)
    deleteNode(head, 1);
    cout << "List after deleting node with key 1: ";
    printList(head);

    // Deleting node with key 5 (not present in the list)
    deleteNode(head, 5);

    return 0;
}
```

In this implementation, the `deleteNode` function takes the head of the circular linked list and the key of the node to be deleted. It then traverses the list and deletes the node with the given key. If the node to be deleted is the head node, it updates the head accordingly.

### 1. Algorithms & Data Structures (C++): Circular Linked List: find

In a circular linked list, the `find` operation searches for a given value within the list. Since it's circular, you can start traversing from any node until you reach the starting point again.

Here's a sample implementation in C++:

```cpp
#include <iostream>

using namespace std;

// Node structure for the circular linked list
struct Node {
    int data;
    Node* next;
};

// Function to insert a new node at the end of the circular linked list
void insert(Node*& head, int value) {
    Node* newNode = new Node;
    newNode->data = value;
    newNode->next = head;

    if (head == nullptr) {
        head = newNode;
        newNode->next = head;
    } else {
        Node* temp = head;
        while (temp->next != head)
            temp = temp->next;
        temp->next = newNode;
    }
}

// Function to search for a value in the circular linked list
Node* find(Node* head, int value) {
    if (head == nullptr)
        return nullptr;

    Node* current = head;
    do {
        if (current->data == value)
            return current;
        current = current->next;
    } while (current != head);

    return nullptr; // Value not found
}

// Function to display the circular linked list
void display(Node* head) {
    if (head == nullptr)
        return;

    Node* current = head;
    do {
        cout << current->data << " ";
        current = current->next;
    } while (current != head);
    cout << endl;
}

int main() {
    Node* head = nullptr;
    
    // Inserting elements into the circular linked list
    insert(head, 1);
    insert(head, 2);
    insert(head, 3);
    insert(head, 4);
    insert(head, 5);

    // Displaying the circular linked list
    cout << "Circular Linked List: ";
    display(head);

    // Searching for a value in the circular linked list
    int searchValue = 3;
    Node* result = find(head, searchValue);
    if (result != nullptr)
        cout << "Value " << searchValue << " found!" << endl;
    else
        cout << "Value " << searchValue << " not found!" << endl;

    return 0;
}
```

This code defines a basic circular linked list structure with `insert`, `find`, and `display` functions. In the `find` function, it traverses through the list until it finds the desired value or reaches the starting point again.

### 1. Algorithms & Data Structures (C++): Circular Linked List: Print

To print out the elements of a Circular Linked List in C++, you typically start from the head node and traverse through each node until you reach the head node again. Here's a sample implementation:

```cpp
#include <iostream>

using namespace std;

// Define the structure for a node in the Circular Linked List
struct Node {
    int data;
    Node* next;
};

// Function to print the elements of the Circular Linked List
void printCircularList(Node* head) {
    if (head == nullptr) {
        cout << "Circular Linked List is empty." << endl;
        return;
    }

    Node* current = head;

    do {
        cout << current->data << " ";
        current = current->next;
    } while (current != head);

    cout << endl;
}

// Example usage
int main() {
    // Create some nodes for demonstration
    Node* head = new Node();
    Node* second = new Node();
    Node* third = new Node();

    head->data = 1;
    head->next = second;

    second->data = 2;
    second->next = third;

    third->data = 3;
    third->next = head; // Making it circular

    // Print the Circular Linked List
    cout << "Circular Linked List: ";
    printCircularList(head);

    // Free allocated memory
    delete head;
    delete second;
    delete third;

    return 0;
}
```

This code defines a simple structure for a node in the Circular Linked List, provides a function `printCircularList` to print its elements, and demonstrates the usage with a simple example in the `main` function.

### 1. Algorithms & Data Structures (C++): Circular Linked Lists

Circular linked lists are a type of linked list where the last node points back to the first node, forming a circle. They can be singly or doubly linked. In C++, you can implement a circular linked list using classes to represent nodes and a separate class to manage the list itself. Here's a basic implementation of a singly circular linked list:

```cpp
#include <iostream>

// Node class representing each element in the list
class Node {
public:
    int data;
    Node* next;

    Node(int data) : data(data), next(nullptr) {}
};

// Circular linked list class
class CircularLinkedList {
private:
    Node* head; // Pointer to the first node in the list
public:
    CircularLinkedList() : head(nullptr) {}

    // Function to insert a node at the beginning of the list
    void insertAtBeginning(int data) {
        Node* newNode = ne'w Node(data);
        if (head == nullptr) {
            newNode->next = newNode; // Point to itself
        } else {
            newNode->next = head;
            Node* temp = head;
            while (temp->next != head) {
                temp = temp->next;
            }
            temp->next = newNode;
        }
        head = newNode;
    }

    // Function to display the circular linked list
    void display() {
        if (head == nullptr) {
            std::cout << "List is empty\n";
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
    CircularLinkedList cll;
    cll.insertAtBeginning(1);
    cll.insertAtBeginning(2);
    cll.insertAtBeginning(3);
    cll.display(); // Output: 3 2 1
    return 0;
}
```

In this implementation:

* `Node` class represents each element of the circular linked list.
* `CircularLinkedList` class manages the list itself, with functions for insertion, deletion, searching, etc.
* The `insertAtBeginning` function inserts a new node at the beginning of the list, maintaining circularity.
* The `display` function traverses the list from the head to print its elements.

You can expand upon this implementation by adding more functionality such as insertion at the end, deletion, searching, etc., depending on your requirements. Additionally, you may want to implement error handling for scenarios like out-of-memory conditions when dynamically allocating memory for nodes.

### 1. Algorithms & Data Structures (C++): Class ADT for Circular Linked Lists

Sure, let's define a class for a circular linked list in C++. In a circular linked list, each node has a reference to the next node in the list, and the last node points back to the first node forming a circle. Here's a basic implementation:

```cpp
#include <iostream>

template <class T>
class Node {
public:
    T data;
    Node<T>* next;

    Node(T val) : data(val), next(nullptr) {}
};

template <class T>
class CircularLinkedList {
private:
    Node<T>* head;

public:
    CircularLinkedList() : head(nullptr) {}

    ~CircularLinkedList() {
        if (head != nullptr) {
            Node<T>* current = head;
            do {
                Node<T>* temp = current;
                current = current->next;
                delete temp;
            } while (current != head);
        }
    }

    void insert(T val) {
        Node<T>* newNode = new Node<T>(val);
        if (head == nullptr) {
            head = newNode;
            head->next = head;
        } else {
            Node<T>* current = head;
            while (current->next != head) {
                current = current->next;
            }
            current->next = newNode;
            newNode->next = head;
        }
    }

    void display() {
        if (head == nullptr) {
            std::cout << "List is empty" << std::endl;
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
```

Here's a quick overview of the code:

* `Node`: Represents each element in the list. It contains data and a pointer to the next node.
* `CircularLinkedList`: Manages the circular linked list. It has methods for insertion and display.
* `insert`: Inserts a new node at the end of the list.
* `display`: Displays the elements of the list.

You can use this class like this:

```cpp
int main() {
    CircularLinkedList<int> myList;
    myList.insert(1);
    myList.insert(2);
    myList.insert(3);
    myList.display(); // Output: 1 2 3
    return 0;
}
```

This is a basic implementation. You can extend it further by adding other operations like deletion, searching, etc., as per your requirements.

### 1. Algorithms & Data Structures (C++): Delete Element at End of Circular Linked List

Deleting an element at the end of a circular linked list in C++ involves traversing the list until you reach the last node, updating pointers accordingly, and deleting the last node. Here's a basic implementation:

```cpp
#include <iostream>

// Define the structure of a node
struct Node {
    int data;
    Node* next;
    
    Node(int val) : data(val), next(nullptr) {}
};

// Class for Circular Linked List
class CircularLinkedList {
private:
    Node* head; // Head pointer to the list

public:
    // Constructor
    CircularLinkedList() : head(nullptr) {}

    // Function to insert a new node at the end
    void insert(int val) {
        Node* newNode = new Node(val);
        if (!head) {
            head = newNode;
            newNode->next = head; // Point to itself to form a circular list
        } else {
            Node* temp = head;
            while (temp->next != head) {
                temp = temp->next;
            }
            temp->next = newNode;
            newNode->next = head; // Point back to head to maintain circularity
        }
    }

    // Function to delete the last node
    void deleteLast() {
        if (!head) {
            std::cout << "List is empty. Cannot delete.\n";
            return;
        }
        Node* prev = nullptr;
        Node* temp = head;
        while (temp->next != head) {
            prev = temp;
            temp = temp->next;
        }
        if (prev) {
            prev->next = head; // Point the second last node to the head
            delete temp; // Delete the last node
        } else {
            delete head; // If there's only one node, delete it
            head = nullptr; // Set head to null
        }
    }

    // Function to display the circular linked list
    void display() {
        if (!head) {
            std::cout << "List is empty.\n";
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
    CircularLinkedList list;
    list.insert(1);
    list.insert(2);
    list.insert(3);
    list.insert(4);
    list.display(); // Output: 1 2 3 4
    list.deleteLast();
    list.display(); // Output: 1 2 3
    list.deleteLast();
    list.display(); // Output: 1 2
    return 0;
}
```

In this implementation:

* `insert(int val)` inserts a new node with the given value at the end of the circular linked list.
* `deleteLast()` deletes the last node of the circular linked list.
* `display()` prints the elements of the circular linked list.

Ensure proper handling of edge cases like deleting from an empty list, and also consider memory management for deleting nodes.

### 1. Algorithms & Data Structures (C++): Deleting an Element from Circular Linked Lists

Deleting an element from a circular linked list in C++ involves several steps, but it's not too complicated. Here's a basic algorithm:

1. Traverse the list to find the node to delete.
2. Adjust the pointers to bypass the node to be deleted.
3. If the node to delete is the only node in the list, set the head pointer to null.
4. If the node to delete is the head node, update the head pointer.
5. Delete the node from memory.

Let's implement this algorithm:

```cpp
#include <iostream>

using namespace std;

// Define the structure of a node
struct Node {
    int data;
    Node* next;
};

// Function to delete a node from the circular linked list
void deleteNode(Node* &head, int key) {
    if (head == nullptr)
        return;

    Node* current = head;
    Node* prev = nullptr;

    // Traverse the list to find the node to delete
    do {
        if (current->data == key)
            break;

        prev = current;
        current = current->next;
    } while (current != head);

    // If the node to delete is not found
    if (current == head && current->data != key) {
        cout << "Key not found in the list." << endl;
        return;
    }

    // If the node to delete is the only node in the list
    if (current->next == head && prev == nullptr) {
        head = nullptr;
    }
    // If the node to delete is the head node
    else if (current == head) {
        prev = head;
        while (prev->next != head)
            prev = prev->next;
        head = head->next;
        prev->next = head;
    }
    // If the node to delete is in the middle or end
    else {
        prev->next = current->next;
    }

    // Delete the node from memory
    delete current;
}

// Function to print the circular linked list
void printList(Node* head) {
    if (head == nullptr)
        return;

    Node* temp = head;
    do {
        cout << temp->data << " ";
        temp = temp->next;
    } while (temp != head);
    cout << endl;
}

// Function to insert a node at the end of the circular linked list
void insertEnd(Node* &head, int data) {
    Node* newNode = new Node;
    newNode->data = data;
    newNode->next = nullptr;

    if (head == nullptr) {
        head = newNode;
        head->next = head;
    } else {
        Node* temp = head;
        while (temp->next != head)
            temp = temp->next;
        temp->next = newNode;
        newNode->next = head;
    }
}

int main() {
    Node* head = nullptr;

    // Insert elements into the circular linked list
    insertEnd(head, 1);
    insertEnd(head, 2);
    insertEnd(head, 3);
    insertEnd(head, 4);
    insertEnd(head, 5);

    cout << "Original List: ";
    printList(head);

    // Delete a node
    deleteNode(head, 3);
    cout << "List after deleting 3: ";
    printList(head);

    return 0;
}
```

In this implementation:

* We define a `Node` struct representing each element in the circular linked list.
* The `deleteNode()` function deletes a node with the specified key from the list.
* The `printList()` function prints the elements of the circular linked list.
* The `insertEnd()` function inserts a new node at the end of the circular

linked list.

* In the `main()` function, we create a circular linked list with some initial elements, print the list, delete a node, and print the list again to show the effect of deletion.

This implementation handles various scenarios like deleting the only node, deleting the head node, and deleting a node from the middle or end of the list.

### 1. Algorithms & Data Structures (C++): Displaying Elements in Circular Linked lists

Sure! In C++, you can display elements in a circular linked list by traversing the list starting from any node and stopping when you reach the starting node again. Here's a simple example:

```cpp
#include <iostream>

// Node structure
struct Node {
    int data;
    Node* next;
    
    // Constructor
    Node(int value) : data(value), next(nullptr) {}
};

// Circular Linked List class
class CircularLinkedList {
private:
    Node* head;

public:
    // Constructor
    CircularLinkedList() : head(nullptr) {}

    // Insert a node at the end of the list
    void insert(int value) {
        Node* newNode = new Node(value);
        if (!head) {
            head = newNode;
            newNode->next = head; // Circular reference to itself
        } else {
            Node* temp = head;
            while (temp->next != head) {
                temp = temp->next;
            }
            temp->next = newNode;
            newNode->next = head; // Circular reference
        }
    }

    // Display all elements in the list
    void display() {
        if (!head) {
            std::cout << "List is empty." << std::endl;
            return;
        }

        Node* temp = head;
        std::cout << "Circular Linked List: ";
        do {
            std::cout << temp->data << " ";
            temp = temp->next;
        } while (temp != head);
        std::cout << std::endl;
    }
};

int main() {
    CircularLinkedList list;
    list.insert(1);
    list.insert(2);
    list.insert(3);
    list.display(); // Output: 1 2 3

    return 0;
}
```

In this code:

* We have a `Node` struct to represent each node in the list.
* The `CircularLinkedList` class manages the circular linked list operations.
* The `insert` function inserts a new node at the end of the list.
* The `display` function traverses the list from the head node and prints each element until it reaches the head node again. It uses a do-while loop to ensure that even for an empty list, at least one iteration is performed.

This code should give you a basic understanding of how to display elements in a circular linked list in C++.

### 1. Algorithms & Data Structures (C++): Displaying Elements Recursively in Circular Linked Lists

Displaying elements recursively in a circular linked list involves traversing the list starting from any given node until you reach the starting point again. Here's how you can implement this in C++:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* next;
    
    Node(int value) : data(value), next(nullptr) {}
};

class CircularLinkedList {
private:
    Node* head;

    // Helper function to display elements recursively
    void displayRecursive(Node* current, Node* start) {
        if (current == start) {
            std::cout << current->data << " ";
            return;
        }
        std::cout << current->data << " ";
        displayRecursive(current->next, start);
    }

public:
    CircularLinkedList() : head(nullptr) {}

    // Function to insert elements into the circular linked list
    void insert(int value) {
        Node* newNode = new Node(value);
        if (!head) {
            head = newNode;
            head->next = head; // Circular
        } else {
            Node* temp = head;
            while (temp->next != head) {
                temp = temp->next;
            }
            temp->next = newNode;
            newNode->next = head;
        }
    }

    // Function to display elements of the circular linked list recursively
    void display() {
        if (!head) {
            std::cout << "List is empty" << std::endl;
            return;
        }
        std::cout << "Circular Linked List (Recursive): ";
        displayRecursive(head, head);
        std::cout << std::endl;
    }
};

int main() {
    CircularLinkedList list;
    list.insert(1);
    list.insert(2);
    list.insert(3);
    list.insert(4);
    list.insert(5);

    list.display();

    return 0;
}
```

In this implementation, the `Node` struct represents each element in the linked list. The `CircularLinkedList` class contains a pointer to the head of the list. The `insert` function inserts elements into the circular linked list, maintaining the circular property. The `displayRecursive` function is a helper function that recursively displays the elements of the circular linked list starting from a given node until it reaches the starting point again. Finally, the `display` function initiates the recursive display from the head of the list.

### 1. Algorithms & Data Structures (C++): Insert at the End of a Circular Linked List

Inserting an element at the end of a circular linked list in C++ involves a few steps:

1. Create a new node with the given data.
2. If the list is empty, make the new node the head and point it to itself.
3. Traverse the list until you reach the last node.
4. Make the last node point to the new node, and the new node's next pointer should point to the head.
5. Update the head pointer to the new node if necessary.

Here's a C++ implementation of inserting at the end of a circular linked list:

```cpp
#include <iostream>

// Define the structure for a node
struct Node {
    int data;
    Node* next;
};

// Function to insert a new node at the end of the circular linked list
void insertAtEnd(Node*& head, int newData) {
    // Create a new node
    Node* newNode = new Node;
    newNode->data = newData;
    newNode->next = nullptr;

    // If the list is empty, make the new node the head
    if (head == nullptr) {
        head = newNode;
        head->next = head; // Point to itself since it's the only node
    } else {
        // Traverse to the last node
        Node* temp = head;
        while (temp->next != head) {
            temp = temp->next;
        }
        // Make the last node point to the new node
        temp->next = newNode;
        // Make the new node point to the head
        newNode->next = head;
    }
}

// Function to print the circular linked list
void printList(Node* head) {
    if (head == nullptr) {
        std::cout << "List is empty." << std::endl;
        return;
    }

    Node* temp = head;
    do {
        std::cout << temp->data << " ";
        temp = temp->next;
    } while (temp != head);
    std::cout << std::endl;
}

// Main function
int main() {
    Node* head = nullptr;

    // Inserting elements at the end
    insertAtEnd(head, 10);
    insertAtEnd(head, 20);
    insertAtEnd(head, 30);
    
    // Printing the list
    std::cout << "Circular Linked List: ";
    printList(head);

    return 0;
}
```

This code defines a `Node` struct representing a node in the circular linked list. The `insertAtEnd` function inserts a new node with the given data at the end of the list, and the `printList` function prints the elements of the circular linked list. In the `main` function, we create a circular linked list and insert some elements at the end, then print the list.

### 1. Algorithms & Data Structures (C++): Insert Element at the Beginning of Circular Linked List

To insert an element at the beginning of a circular linked list in C++, you need to follow these steps:

1. Create a new node with the given value.
2. If the list is empty, make the new node point to itself and update the head pointer.
3. If the list is not empty, traverse to the last node and make it point to the new node.
4. Update the head pointer to point to the new node.

Here's the implementation:

```cpp
#include <iostream>

struct Node {
    int data;
    Node* next;
};

class CircularLinkedList {
private:
    Node* head;

public:
    CircularLinkedList() : head(nullptr) {}

    // Function to insert element at the beginning of the circular linked list
    void insertAtBeginning(int value) {
        Node* newNode = new Node();
        newNode->data = value;

        if (head == nullptr) {
            // If the list is empty
            head = newNode;
            newNode->next = head; // Point to itself
        } else {
            // If the list is not empty
            Node* temp = head;
            // Traverse to the last node
            while (temp->next != head) {
                temp = temp->next;
            }
            // Make the last node point to the new node
            temp->next = newNode;
            // Make the new node point to the head
            newNode->next = head;
            // Update the head pointer
            head = newNode;
        }
    }

    // Function to display the circular linked list
    void display() {
        if (head == nullptr) {
            std::cout << "List is empty." << std::endl;
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
    CircularLinkedList list;
    list.insertAtBeginning(5);
    list.insertAtBeginning(10);
    list.insertAtBeginning(15);

    std::cout << "Circular Linked List: ";
    list.display();

    return 0;
}
```

This code will create a circular linked list and insert elements at the beginning. You can customize it further as per your requirements.

### 1. Algorithms & Data Structures (C++): Inserting an Element in Circular Linked Lists

Inserting an element into a circular linked list involves a few steps:

1. **Create a new node** with the given value.
2. **Traverse the list** to find the position where you want to insert the new node.
3. **Adjust the pointers** to insert the new node in the desired position.

Here's a C++ implementation to insert a new node at the beginning, end, or any position in a circular linked list:

```cpp
#include <iostream>

using namespace std;

// Node structure
struct Node {
    int data;
    Node* next;
    
    Node(int val) : data(val), next(nullptr) {}
};

// Circular Linked List class
class CircularLinkedList {
private:
    Node* head;
public:
    CircularLinkedList() : head(nullptr) {}

    // Function to insert at the beginning
    void insertAtBeginning(int val) {
        Node* newNode = new Node(val);
        if (head == nullptr) {
            head = newNode;
            head->next = head; // Circular linking
        } else {
            Node* temp = head;
            while (temp->next != head) {
                temp = temp->next;
            }
            temp->next = newNode;
            newNode->next = head;
            head = newNode;
        }
    }

    // Function to insert at the end
    void insertAtEnd(int val) {
        Node* newNode = new Node(val);
        if (head == nullptr) {
            head = newNode;
            head->next = head; // Circular linking
        } else {
            Node* temp = head;
            while (temp->next != head) {
                temp = temp->next;
            }
            temp->next = newNode;
            newNode->next = head;
        }
    }

    // Function to insert at a specific position
    void insertAtPosition(int val, int pos) {
        if (pos <= 0) {
            cout << "Invalid position." << endl;
            return;
        }
        if (pos == 1) {
            insertAtBeginning(val);
            return;
        }
        Node* newNode = new Node(val);
        Node* temp = head;
        for (int i = 1; i < pos - 1 && temp != nullptr; ++i) {
            temp = temp->next;
        }
        if (temp == nullptr) {
            cout << "Position out of range." << endl;
            return;
        }
        newNode->next = temp->next;
        temp->next = newNode;
    }

    // Function to display the list
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

// Main function
int main() {
    CircularLinkedList list;
    list.insertAtEnd(1);
    list.insertAtEnd(2);
    list.insertAtEnd(4);
    list.insertAtBeginning(0);
    list.insertAtPosition(3, 3);

    cout << "Circular Linked List: ";
    list.display();

    return 0;
}
```

In this implementation:

* `insertAtBeginning` inserts a new node at the beginning of the circular linked list.
* `insertAtEnd` inserts a new node at the end of the circular linked list.
* `insertAtPosition` inserts a new node at a specified position in the circular linked list.
* `display` is used to print the circular linked list.

Remember to handle edge cases such as an empty list or invalid positions.

### 1. Algorithms & Data Structures (C++): Difference between Circular and Normal linked list

Circular and normal linked lists are two variations of linked list data structures, differing mainly in their structure and behavior. Here are the key differences between them:

1. **Termination Condition**:
   * In a normal linked list, the last node points to nullptr (or NULL in C/C++), indicating the end of the list.
   * In a circular linked list, the last node points back to the first node, creating a circular structure.

2. **Traversal**:
   * In a normal linked list, traversal typically stops when reaching the nullptr at the end of the list.
   * In a circular linked list, traversal can continue indefinitely by following the pointers until returning to the starting point.

3. **Usage**:
   * Normal linked lists are often used when a linear collection of data with a definite end is needed, such as maintaining a sequence of items.
   * Circular linked lists are useful in applications where operations involve continuous looping through the list, like round-robin scheduling or implementing circular buffers.

4. **Insertion and Deletion**:
   * Insertion and deletion operations in normal linked lists require updating the pointers of adjacent nodes to maintain the list's integrity.
   * In circular linked lists, insertion and deletion can be slightly more complex, as special care must be taken to ensure that the circular structure is preserved.

5. **End Condition Check**:
   * In a normal linked list, checking for the end of the list involves comparing the next pointer to nullptr.
   * In a circular linked list, reaching the start node again indicates that all nodes have been traversed.

6. **Memory Management**:
   * Both types of linked lists require dynamic memory allocation, as nodes are typically created and destroyed dynamically.
   * Circular linked lists may require additional care in memory management to prevent memory leaks, especially when deleting nodes.

7. **Applications**:
   * Normal linked lists are commonly used in various applications like implementing stacks, queues, and dynamic memory allocation.
   * Circular linked lists find applications in tasks like representing a round-robin scheduling algorithm, implementing a circular buffer, or creating a circular list of players in a game.

In summary, while both normal and circular linked lists are based on similar principles, their differences lie in how they handle termination conditions, traversal, insertion/deletion operations, and their specific applications. The choice between them depends on the specific requirements of the problem being solved.

### 1. Algorithms & Data Structures (C++): Circular Singly Linked List: Check if a Circular Linked List is Sorted

To check if a circular singly linked list is sorted in ascending order, you can traverse the list and compare each node's value with the next node's value. If at any point you find that the current node's value is greater than the next node's value, then the list is not sorted. Here's a C++ implementation for this:

```cpp
#include <iostream>

// Define the structure of a node
struct Node {
    int data;
    Node* next;
    
    Node(int value) : data(value), next(nullptr) {}
};

// Function to check if a circular linked list is sorted
bool isCircularListSorted(Node* head) {
    if (head == nullptr)
        return true;

    Node* current = head;

    do {
        if (current->data > current->next->data)
            return false;
        
        current = current->next;
    } while (current != head);

    return true;
}

int main() {
    // Create a circular linked list
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->next = new Node(3);
    head->next->next->next = new Node(4);
    head->next->next->next->next = head; // Making it circular
    
    // Check if the circular linked list is sorted
    if (isCircularListSorted(head))
        std::cout << "Circular Linked List is sorted.\n";
    else
        std::cout << "Circular Linked List is not sorted.\n";
    
    // Free the memory
    delete head->next->next->next->next;
    delete head->next->next->next;
    delete head->next->next;
    delete head->next;
    delete head;
    
    return 0;
}
```

In this implementation, we define a `Node` struct to represent each node in the circular linked list. The `isCircularListSorted` function takes the head of the circular linked list as input and iterates through the list to check if it is sorted. The `main` function creates a circular linked list and then checks if it's sorted using the `isCircularListSorted` function.

### 1. Algorithms & Data Structures (C++): Circular Singly Linked List: Count the Number of Nodes

Certainly! Below is a C++ implementation of counting the number of nodes in a circular singly linked list:

```cpp
#include <iostream>

// Define the structure for a node
struct Node {
    int data;
    Node* next;
    
    // Constructor
    Node(int value) : data(value), next(nullptr) {}
};

// Class for Circular Singly Linked List
class CircularSinglyLinkedList {
private:
    Node* head;
public:
    // Constructor
    CircularSinglyLinkedList() : head(nullptr) {}
    
    // Destructor
    ~CircularSinglyLinkedList() {
        if (head == nullptr) return;
        Node* current = head->next;
        while (current != head) {
            Node* next = current->next;
            delete current;
            current = next;
        }
        delete head;
    }
    
    // Function to insert a node at the end of the list
    void insert(int value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = newNode;
            head->next = head;
        } else {
            Node* temp = head;
            while (temp->next != head) {
                temp = temp->next;
            }
            temp->next = newNode;
            newNode->next = head;
        }
    }
    
    // Function to count the number of nodes in the list
    int countNodes() {
        int count = 0;
        if (head == nullptr) return count;
        
        Node* temp = head;
        do {
            count++;
            temp = temp->next;
        } while (temp != head);
        
        return count;
    }
};

int main() {
    CircularSinglyLinkedList list;
    
    // Insert some elements into the list
    list.insert(1);
    list.insert(2);
    list.insert(3);
    list.insert(4);
    
    // Count the number of nodes and print the result
    std::cout << "Number of nodes in the list: " << list.countNodes() << std::endl;
    
    return 0;
}
```

This code defines a Circular Singly Linked List class with methods to insert nodes at the end and count the number of nodes in the list. In the `countNodes` method, it traverses the list starting from the head until it reaches the head again, incrementing the count for each node encountered. Finally, it returns the count.

### 1. Algorithms & Data Structures (C++): Circular Singly Linked List: Delete All Nodes

To delete all nodes in a circular singly linked list implemented in C++, you can traverse the list and delete each node one by one until the list is empty. Here's a sample implementation:

```cpp
#include <iostream>

// Node structure
struct Node {
    int data;
    Node* next;
    
    Node(int value) : data(value), next(nullptr) {}
};

// Circular Singly Linked List class
class CircularSinglyLinkedList {
private:
    Node* head;

public:
    CircularSinglyLinkedList() : head(nullptr) {}

    // Function to insert a node at the end of the list
    void insert(int value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = newNode;
            head->next = head; // Circular link
        } else {
            Node* temp = head;
            while (temp->next != head) {
                temp = temp->next;
            }
            temp->next = newNode;
            newNode->next = head; // Circular link
        }
    }

    // Function to delete all nodes in the list
    void deleteAllNodes() {
        if (head == nullptr) return; // List is already empty

        Node* current = head;
        Node* nextNode;

        // Traverse the list and delete each node
        do {
            nextNode = current->next;
            delete current;
            current = nextNode;
        } while (current != head);

        head = nullptr; // Reset head to nullptr
    }

    // Function to display the elements of the list
    void display() {
        if (head == nullptr) {
            std::cout << "List is empty\n";
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
    CircularSinglyLinkedList list;

    // Insert some elements into the list
    list.insert(1);
    list.insert(2);
    list.insert(3);
    list.insert(4);
    list.insert(5);

    std::cout << "Original List: ";
    list.display();

    // Delete all nodes
    list.deleteAllNodes();

    std::cout << "List after deletion: ";
    list.display();

    return 0;
}
```

In this implementation:

* The `Node` struct represents each element of the list.
* The `CircularSinglyLinkedList` class maintains a pointer to the head of the list.
* The `insert` function inserts a new node at the end of the list.
* The `deleteAllNodes` function traverses the list and deletes each node.
* The `display` function displays the elements of the list.

### 1. Algorithms & Data Structures (C++): Circular Singly Linked List: Get Method

To implement the `get` method for a circular singly linked list in C++, you'll need to traverse the list starting from the head until you reach the desired index. Here's a sample implementation:

```cpp
#include <iostream>

using namespace std;

// Node class to represent each element in the linked list
class Node {
public:
    int data;
    Node* next;

    Node(int val) : data(val), next(nullptr) {}
};

// Circular Singly Linked List class
class CircularSinglyLinkedList {
private:
    Node* head;

public:
    CircularSinglyLinkedList() : head(nullptr) {}

    // Function to add a new node to the end of the list
    void add(int val) {
        Node* newNode = new Node(val);
        if (head == nullptr) {
            head = newNode;
            newNode->next = head;
        } else {
            Node* temp = head;
            while (temp->next != head) {
                temp = temp->next;
            }
            temp->next = newNode;
            newNode->next = head;
        }
    }

    // Function to retrieve the value at a given index
    int get(int index) {
        if (head == nullptr) {
            cout << "List is empty" << endl;
            return -1; // Return -1 to indicate failure
        }

        Node* current = head;
        int count = 0;
        do {
            if (count == index) {
                return current->data;
            }
            current = current->next;
            count++;
        } while (current != head);

        // If index is out of bounds
        cout << "Index out of bounds" << endl;
        return -1; // Return -1 to indicate failure
    }
};

int main() {
    CircularSinglyLinkedList list;
    list.add(1);
    list.add(2);
    list.add(3);
    list.add(4);
    list.add(5);

    cout << "Element at index 2: " << list.get(2) << endl;
    cout << "Element at index 6: " << list.get(6) << endl;

    return 0;
}
```

In this implementation, we define a `Node` class to represent each element in the linked list. Then, we have a `CircularSinglyLinkedList` class that includes methods to add elements to the list (`add` method) and retrieve an element at a given index (`get` method).

The `get` method traverses the circular list starting from the head until it reaches the desired index, returning the value at that index. If the list is empty or the index is out of bounds, appropriate error messages are displayed, and `-1` is returned.

### 1. Algorithms & Data Structures (C++): Circular Singly Linked List: Insert into a Sorted Circular Linked List

Certainly! Inserting into a sorted circular singly linked list in C++ involves finding the correct position to insert the new node while maintaining the sorted order. Here's a step-by-step guide on how to do it:

1. **Create a Node Structure**: Define a structure for the node of the linked list.

2. **Implement the Circular Linked List Class**: Define a class for the circular linked list and include methods for insertion, deletion, traversal, etc.

3. **Implement the Insertion Function**: Write a function to insert a new node into the sorted circular linked list while maintaining the sorted order.

Here's a sample implementation:

```cpp
#include <iostream>

using namespace std;

// Node structure
struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

// Circular singly linked list class
class CircularSinglyLinkedList {
private:
    Node* head;

public:
    // Constructor
    CircularSinglyLinkedList() : head(nullptr) {}

    // Function to insert a new node into the sorted circular linked list
    void insertSorted(int val) {
        Node* newNode = new Node(val);
        if (!head) { // If the list is empty
            head = newNode;
            head->next = head;
        } else if (val <= head->data) { // If the new node should be the new head
            newNode->next = head;
            Node* temp = head;
            while (temp->next != head)
                temp = temp->next;
            temp->next = newNode;
            head = newNode;
        } else { // Inserting in between or at the end
            Node* temp = head;
            while (temp->next != head && temp->next->data < val)
                temp = temp->next;
            newNode->next = temp->next;
            temp->next = newNode;
        }
    }

    // Function to display the circular linked list
    void display() {
        if (!head) {
            cout << "List is empty" << endl;
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
    CircularSinglyLinkedList list;

    // Inserting elements into the sorted circular linked list
    list.insertSorted(5);
    list.insertSorted(2);
    list.insertSorted(8);
    list.insertSorted(3);
    list.insertSorted(1);

    // Displaying the circular linked list
    list.display();

    return 0;
}
```

This code defines a circular singly linked list class and provides a method `insertSorted()` to insert elements into the list in sorted order. The `main()` function demonstrates how to use this class to create a sorted circular linked list and display its contents.

### 1. Algorithms & Data Structures (C++): Circular Singly Linked List: Josephus Circle using Circular Linked List

Certainly! The Josephus problem is a classic problem in computer science and mathematics. It involves a group of people arranged in a circle, and they are eliminated in a specific pattern until only one person remains. We can solve this problem efficiently using a circular linked list. Here's how you can implement it in C++:

```cpp
#include <iostream>

using namespace std;

// Node structure for the circular linked list
struct Node {
    int data;
    Node* next;

    Node(int value) : data(value), next(nullptr) {}
};

// Class for the circular linked list
class CircularLinkedList {
private:
    Node* head;

public:
    CircularLinkedList() : head(nullptr) {}

    // Function to insert a node at the end of the circular linked list
    void insert(int value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = newNode;
            head->next = head; // Point to itself for circularity
        } else {
            Node* temp = head;
            while (temp->next != head) {
                temp = temp->next;
            }
            temp->next = newNode;
            newNode->next = head;
        }
    }

    // Function to delete a node from the circular linked list
    void remove(Node* prev, Node* current) {
        if (prev == current) {
            head = nullptr;
        } else {
            prev->next = current->next;
            if (current == head) {
                head = head->next;
            }
        }
        delete current;
    }

    // Function to solve the Josephus problem
    void josephus(int m) {
        Node* current = head;
        Node* prev = nullptr;
        while (current->next != current) {
            // Move m-1 steps
            for (int i = 0; i < m - 1; ++i) {
                prev = current;
                current = current->next;
            }
            // Eliminate the current node
            remove(prev, current);
            // Move to the next survivor
            current = prev->next;
        }
        // Print the survivor
        cout << "Last person standing: " << current->data << endl;
    }

    // Function to display the circular linked list
    void display() {
        if (head == nullptr) {
            cout << "Circular Linked List is empty." << endl;
            return;
        }
        Node* temp = head;
        do {
            cout << temp->data << " ";
            temp = temp->next;
        } while (temp != head);
        cout << endl;
    }

    // Destructor to free allocated memory
    ~CircularLinkedList() {
        if (head != nullptr) {
            Node* temp = head;
            while (temp->next != head) {
                Node* nextNode = temp->next;
                delete temp;
                temp = nextNode;
            }
            delete temp;
        }
    }
};

int main() {
    CircularLinkedList list;
    int n, m;
    cout << "Enter the number of people: ";
    cin >> n;
    cout << "Enter the elimination count: ";
    cin >> m;

    // Insert people into the circular linked list
    for (int i = 1; i <= n; ++i) {
        list.insert(i);
    }

    cout << "Initial circle of people: ";
    list.display();

    // Solve the Josephus problem
    list.josephus(m);

    return 0;
}
```

This C++ code implements a circular linked list and solves the Josephus problem using that circular linked list. You can run this code, and it will prompt you to enter the number of people and the elimination count (m). Then it will display the last person standing according to the Josephus problem.

### 1. Algorithms & Data Structures (C++): Circular Singly Linked List: LEETCODE Questions

Circular singly linked lists can be a bit trickier to handle than regular singly linked lists due to the cyclic nature of their structure. However, they're useful in various scenarios, such as representing tasks that need to cycle indefinitely or implementing certain kinds of data structures like circular buffers.

When it comes to LeetCode questions involving circular singly linked lists, you might encounter problems that require you to manipulate the list in various ways, such as insertion, deletion, finding cycles, or determining the starting point of a cycle (if any).

Here are a few common LeetCode problems related to circular singly linked lists:

1. **Detect Cycle in a Linked List (Easy):** Given a linked list, return true if the list has a cycle. LeetCode Problem: [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

2. **Find the Start of the Loop (Medium):** Given a linked list, return the node where the cycle begins. If there is no cycle, return null. LeetCode Problem: [Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/)

3. **Insert into a Cyclic Sorted List (Medium):** Given a node from a cyclic sorted list, insert a new node into the list such that the list remains sorted. LeetCode Problem: [Insert into a Sorted Circular Linked List](https://leetcode.com/problems/insert-into-a-sorted-circular-linked-list/)

4. **Rearrange List (Medium):** Given a singly linked list, rearrange it in-place into a sorted circular list. LeetCode Problem: [Reorder List](https://leetcode.com/problems/reorder-list/)

5. **Flatten a Multilevel Doubly Linked List (Medium):** Given a circular doubly linked list, flatten it to a singly linked list in-place. LeetCode Problem: [Flatten a Multilevel Doubly Linked List](https://leetcode.com/problems/flatten-a-multilevel-doubly-linked-list/)

These problems often require you to manipulate pointers carefully, keeping track of the nodes you've visited and considering edge cases such as empty lists or lists with only one or two nodes.

Would you like to discuss the implementation of any specific problem, or do you have any other questions about circular singly linked lists in C++?

### 1. Algorithms & Data Structures (C++): Circular Singly Linked List: Pop First Method

To implement the "Pop First" method for a circular singly linked list in C++, you need to remove the first node from the list. Here's a sample implementation:

```cpp
#include <iostream>

// Define Node structure
struct Node {
    int data;
    Node* next;
    
    Node(int value) : data(value), next(nullptr) {}
};

// Define Circular Singly Linked List class
class CircularSinglyLinkedList {
private:
    Node* head;

public:
    CircularSinglyLinkedList() : head(nullptr) {}

    // Insert a node at the end of the list
    void insert(int value) {
        Node* newNode = new Node(value);
        if (!head) {
            head = newNode;
            newNode->next = head;
        } else {
            Node* temp = head;
            while (temp->next != head) {
                temp = temp->next;
            }
            temp->next = newNode;
            newNode->next = head;
        }
    }

    // Pop the first node from the list
    void popFirst() {
        if (!head) {
            std::cout << "List is empty. Cannot pop.\n";
            return;
        }

        Node* temp = head;
        Node* lastNode = head;
        while (lastNode->next != head) {
            lastNode = lastNode->next;
        }

        head = head->next;
        lastNode->next = head;
        delete temp;
    }

    // Display the contents of the list
    void display() {
        if (!head) {
            std::cout << "List is empty.\n";
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

// Main function to test the implementation
int main() {
    CircularSinglyLinkedList myList;
    myList.insert(1);
    myList.insert(2);
    myList.insert(3);
    myList.insert(4);

    std::cout << "Original list: ";
    myList.display();

    myList.popFirst();

    std::cout << "List after popping first element: ";
    myList.display();

    return 0;
}
```

In this implementation:

* We define a `Node` struct to represent each element of the linked list.
* We define a `CircularSinglyLinkedList` class to encapsulate the functionality of the circular singly linked list.
* The `insert` method is used to add elements to the list.
* The `popFirst` method removes the first node from the list.
* The `display` method is used to print the elements of the list.

The `popFirst` method works by updating the `head` pointer to the next node in the list and deleting the original head node. Additionally, it adjusts the `next` pointer of the last node to point to the new head node.

### 1. Algorithms & Data Structures (C++): Circular Singly Linked List: Pop Method

To implement the pop operation for a circular singly linked list in C++, you'll need to consider a few cases:

1. If the list is empty, there's nothing to pop.
2. If the list has only one element, popping that element would result in an empty list.
3. If the list has more than one element, you'll need to update the pointers to maintain the circular structure.

Here's a sample implementation:

```cpp
#include <iostream>

// Node structure
struct Node {
    int data;
    Node* next;
    
    Node(int val) : data(val), next(nullptr) {}
};

// Circular Singly Linked List class
class CircularSinglyLinkedList {
private:
    Node* head;

public:
    CircularSinglyLinkedList() : head(nullptr) {}

    // Function to pop an element from the list
    void pop() {
        if (!head) {
            std::cout << "List is empty. Cannot pop.\n";
            return;
        }

        Node* temp = head;

        // If the list has only one element
        if (head->next == head) {
            delete head;
            head = nullptr;
        } else {
            // Find the second-to-last node
            Node* prev = nullptr;
            while (temp->next != head) {
                prev = temp;
                temp = temp->next;
            }

            // Update pointers
            prev->next = head;
            delete temp;
        }
    }

    // Function to print the list
    void display() {
        if (!head) {
            std::cout << "List is empty.\n";
            return;
        }

        Node* temp = head;
        do {
            std::cout << temp->data << " ";
            temp = temp->next;
        } while (temp != head);
        std::cout << std::endl;
    }

    // Function to push elements into the list (for testing)
    void push(int val) {
        Node* newNode = new Node(val);
        if (!head) {
            head = newNode;
            head->next = head; // Circular reference
        } else {
            Node* temp = head;
            while (temp->next != head) {
                temp = temp->next;
            }
            temp->next = newNode;
            newNode->next = head; // Circular reference
        }
    }
};

int main() {
    CircularSinglyLinkedList list;

    // Pushing elements for testing
    list.push(1);
    list.push(2);
    list.push(3);
    list.push(4);

    std::cout << "Original List: ";
    list.display();

    // Pop an element
    list.pop();
    std::cout << "After popping an element: ";
    list.display();

    return 0;
}
```

This implementation covers the cases where the list is empty, has only one element, or has more than one element. Make sure to test it thoroughly to ensure its correctness.

### 1. Algorithms & Data Structures (C++): Circular Singly Linked List: Prepend Method

Sure, I can help you with that! Below is an implementation of the prepend method for a Circular Singly Linked List in C++:

```cpp
#include <iostream>

using namespace std;

// Node class representing each node in the circular linked list
class Node {
public:
    int data;
    Node* next;

    // Constructor to initialize node with data and next pointer
    Node(int data) {
        this->data = data;
        this->next = nullptr;
    }
};

// Circular Singly Linked List class
class CircularSinglyLinkedList {
private:
    Node* head;

public:
    // Constructor to initialize an empty list
    CircularSinglyLinkedList() {
        head = nullptr;
    }

    // Function to prepend a node with given data to the list
    void prepend(int data) {
        Node* newNode = new Node(data);

        // If the list is empty, make the new node as head and point it to itself
        if (head == nullptr) {
            head = newNode;
            newNode->next = head;
        } else {
            // Traverse to the last node
            Node* last = head;
            while (last->next != head) {
                last = last->next;
            }

            // Set the next of new node to head and last node's next to new node
            newNode->next = head;
            last->next = newNode;

            // Update head to new node
            head = newNode;
        }
    }

    // Function to display the circular linked list
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
    CircularSinglyLinkedList list;

    // Adding elements to the list
    list.prepend(3);
    list.prepend(2);
    list.prepend(1);

    // Displaying the list
    list.display();

    return 0;
}
```

In this implementation:

* The `Node` class represents each node in the circular linked list. It has two attributes: `data` to store the value of the node, and `next` to point to the next node in the list.
* The `CircularSinglyLinkedList` class represents the circular singly linked list. It has a private attribute `head` which points to the first node of the list.
* The `prepend` method inserts a new node with the given data at the beginning of the list. If the list is empty, it sets the new node as the head and makes it point to itself. If the list is not empty, it traverses to the last node, updates pointers accordingly, and sets the head to the new node.
* The `display` method prints the elements of the list. It traverses the list starting from the head until it reaches the head again.

### 1. Algorithms & Data Structures (C++): Circular Singly Linked List: Print

Certainly! Below is a simple implementation in C++ to print out elements of a Circular Singly Linked List:

```cpp
#include <iostream>

// Node class for the linked list
class Node {
public:
    int data;
    Node* next;

    Node(int val) {
        data = val;
        next = nullptr;
    }
};

// Circular Singly Linked List class
class CircularSinglyLinkedList {
private:
    Node* head;

public:
    CircularSinglyLinkedList() {
        head = nullptr;
    }

    // Function to add a new node to the list
    void addNode(int val) {
        Node* newNode = new Node(val);
        if (head == nullptr) {
            head = newNode;
            head->next = head; // Point to itself in circular fashion
        } else {
            Node* temp = head;
            while (temp->next != head) {
                temp = temp->next;
            }
            temp->next = newNode;
            newNode->next = head;
        }
    }

    // Function to print the elements of the list
    void printList() {
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
    CircularSinglyLinkedList myList;

    // Adding elements to the list
    myList.addNode(1);
    myList.addNode(2);
    myList.addNode(3);
    myList.addNode(4);
    myList.addNode(5);

    // Printing the list
    std::cout << "Circular Singly Linked List: ";
    myList.printList();

    return 0;
}
```

This code defines a Circular Singly Linked List class with functions to add elements to the list and print out its elements. The `Node` class represents individual nodes of the linked list, and the `CircularSinglyLinkedList` class manages the list operations. In the `printList()` function, it traverses the list starting from the `head` node and prints each element until it reaches the head again, indicating the end of the circular list.

### 1. Algorithms & Data Structures (C++): Circular Singly Linked List: Remove Method

Sure, here's how you can implement the remove method for a Circular Singly Linked List in C++:

```cpp
#include <iostream>

using namespace std;

// Define the structure of a node
struct Node {
    int data;
    Node* next;
};

// Define the Circular Singly Linked List class
class CircularSinglyLinkedList {
private:
    Node* head;

public:
    // Constructor
    CircularSinglyLinkedList() : head(nullptr) {}

    // Destructor to free memory
    ~CircularSinglyLinkedList() {
        if (head == nullptr)
            return;
        Node* current = head->next;
        while (current != head) {
            Node* next = current->next;
            delete current;
            current = next;
        }
        delete head;
    }

    // Function to insert a new node at the end of the list
    void insert(int value) {
        Node* newNode = new Node;
        newNode->data = value;
        if (head == nullptr) {
            head = newNode;
            head->next = head;
        } else {
            Node* temp = head;
            while (temp->next != head)
                temp = temp->next;
            temp->next = newNode;
            newNode->next = head;
        }
    }

    // Function to remove a node with given value from the list
    void remove(int value) {
        if (head == nullptr)
            return;

        Node* temp = head;
        Node* prev = nullptr;

        // If the node to be deleted is head
        if (temp->data == value) {
            Node* last = head;
            while (last->next != head)
                last = last->next;
            last->next = head->next;
            head = head->next;
            delete temp;
            return;
        }

        // Find the node to be deleted
        while (temp->next != head && temp->data != value) {
            prev = temp;
            temp = temp->next;
        }

        // If the node with value was not found
        if (temp->data != value) {
            cout << "Node with value " << value << " not found." << endl;
            return;
        }

        // Remove the node
        prev->next = temp->next;
        delete temp;
    }

    // Function to display the list
    void display() {
        if (head == nullptr)
            return;
        Node* temp = head;
        do {
            cout << temp->data << " ";
            temp = temp->next;
        } while (temp != head);
        cout << endl;
    }
};

// Main function
int main() {
    CircularSinglyLinkedList myList;
    myList.insert(1);
    myList.insert(2);
    myList.insert(3);
    myList.insert(4);
    myList.insert(5);

    cout << "Original List: ";
    myList.display();

    myList.remove(3);
    cout << "After removing 3: ";
    myList.display();

    myList.remove(1);
    cout << "After removing 1: ";
    myList.display();

    myList.remove(5);
    cout << "After removing 5: ";
    myList.display();

    return 0;
}
```

This implementation provides the `remove` method, which removes a node with the specified value from the Circular Singly Linked List. The method handles various cases such as removing the head node, removing a node in the middle, and removing a node at the end of the list.

### 1. Algorithms & Data Structures (C++): Circular Singly Linked List: Search Method

Certainly! Below is an example implementation of a search method for a Circular Singly Linked List in C++:

```cpp
#include <iostream>

// Node structure for the Circular Singly Linked List
struct Node {
    int data;
    Node* next;
    
    Node(int value) : data(value), next(nullptr) {}
};

// Class for Circular Singly Linked List
class CircularSinglyLinkedList {
private:
    Node* head;
public:
    CircularSinglyLinkedList() : head(nullptr) {}
    
    // Method to insert a new node at the end of the list
    void insert(int value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = newNode;
            newNode->next = head;
        } else {
            Node* temp = head;
            while (temp->next != head) {
                temp = temp->next;
            }
            temp->next = newNode;
            newNode->next = head;
        }
    }
    
    // Method to search for a value in the list
    bool search(int value) {
        if (head == nullptr) {
            return false;
        }
        Node* current = head;
        do {
            if (current->data == value) {
                return true;
            }
            current = current->next;
        } while (current != head);
        return false;
    }
};

int main() {
    CircularSinglyLinkedList list;
    
    // Inserting elements into the list
    list.insert(10);
    list.insert(20);
    list.insert(30);
    list.insert(40);
    
    // Searching for elements in the list
    std::cout << "Is 20 in the list? " << (list.search(20) ? "Yes" : "No") << std::endl;
    std::cout << "Is 50 in the list? " << (list.search(50) ? "Yes" : "No") << std::endl;
    
    return 0;
}
```

In this implementation:

* We define a `Node` struct to represent each element in the linked list.
* The `CircularSinglyLinkedList` class contains a `head` pointer that points to the first node of the circular linked list.
* The `insert` method is used to insert a new node at the end of the list.
* The `search` method is used to search for a value in the list. It traverses the list starting from the `head` in a loop until it reaches the `head` again, checking each node's data against the value being searched for.

You can use the `main` function to test the implementation by inserting elements into the list and then searching for certain values.

### 1. Algorithms & Data Structures (C++): Circular Singly Linked List: Set Method

Certainly! Below is an implementation of the `set` method for a circular singly linked list in C++:

```cpp
#include <iostream>

// Define Node structure
struct Node {
    int data;
    Node* next;
    explicit Node(int val) : data(val), next(nullptr) {}
};

// Define Circular Singly Linked List class
class CircularSinglyLinkedList {
private:
    Node* head;

public:
    CircularSinglyLinkedList() : head(nullptr) {}

    // Insert at the end
    void insert(int val) {
        Node* newNode = new Node(val);
        if (!head) {
            head = newNode;
            head->next = head;
        } else {
            Node* temp = head;
            while (temp->next != head) {
                temp = temp->next;
            }
            temp->next = newNode;
            newNode->next = head;
        }
    }

    // Set data at a given index
    void set(int index, int val) {
        if (head == nullptr) {
            std::cout << "List is empty. Cannot set value.\n";
            return;
        }

        Node* current = head;
        int count = 0;

        // Traverse the list to find the node at the given index
        do {
            if (count == index) {
                current->data = val;
                std::cout << "Value at index " << index << " updated to " << val << ".\n";
                return;
            }
            current = current->next;
            count++;
        } while (current != head && count <= index);

        // If index is out of range
        std::cout << "Index out of range. Cannot set value.\n";
    }

    // Display the list
    void display() {
        if (head == nullptr) {
            std::cout << "List is empty.\n";
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
    CircularSinglyLinkedList myList;
    myList.insert(1);
    myList.insert(2);
    myList.insert(3);
    myList.insert(4);

    std::cout << "Original list: ";
    myList.display();

    // Set value at index 2 (zero-based index)
    myList.set(2, 10);

    std::cout << "Updated list: ";
    myList.display();

    return 0;
}
```

In this implementation:

* The `set` method allows you to update the value at a specified index in the circular singly linked list.
* If the list is empty or the given index is out of range, appropriate messages are displayed.
* The `display` method is provided to visualize the contents of the list before and after updating.

You can modify the `main` function to test different scenarios and verify the functionality of the `set` method.

### 1. Algorithms & Data Structures (C++): Circular Singly Linked List: Split a Circular Linked List into Two Equal Halves

To split a circular singly linked list into two equal halves, you can follow these steps:

1. Find the midpoint of the list using the slow and fast pointer technique.
2. Break the link between the midpoint and the previous node to split the list into two halves.
3. Adjust the pointers to maintain circularity.

Here's a C++ implementation to achieve this:

```cpp
#include <iostream>

using namespace std;

// Node structure for the circular singly linked list
struct Node {
    int data;
    Node* next;
};

// Function to insert a new node at the end of the circular linked list
void insert(Node*& head, int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = head;

    if (head != nullptr) {
        Node* temp = head;
        while (temp->next != head)
            temp = temp->next;
        temp->next = newNode;
    } else {
        newNode->next = newNode;
    }

    head = newNode;
}

// Function to split the circular linked list into two halves
void splitCircularList(Node* head, Node*& head1, Node*& head2) {
    if (head == nullptr)
        return;

    Node *slow = head, *fast = head;

    // Move 'fast' by two steps and 'slow' by one step
    while (fast->next != head && fast->next->next != head) {
        fast = fast->next->next;
        slow = slow->next;
    }

    // If even nodes in the list, move 'fast' one more step
    if (fast->next->next == head)
        fast = fast->next;

    // Set the head of the first half
    head1 = head;

    // Set the head of the second half
    if (head->next != head) {
        head2 = slow->next;
    }

    // Make the second half circular
    fast->next = slow->next;

    // Make the first half circular
    slow->next = head;
}

// Function to print the circular linked list
void printCircularList(Node* head) {
    if (head == nullptr)
        return;

    Node* temp = head;
    do {
        cout << temp->data << " ";
        temp = temp->next;
    } while (temp != head);
    cout << endl;
}

int main() {
    Node* head = nullptr;
    insert(head, 5);
    insert(head, 4);
    insert(head, 3);
    insert(head, 2);
    insert(head, 1);

    cout << "Original Circular Linked List: ";
    printCircularList(head);

    Node* head1 = nullptr;
    Node* head2 = nullptr;
    splitCircularList(head, head1, head2);

    cout << "First Half: ";
    printCircularList(head1);

    cout << "Second Half: ";
    printCircularList(head2);

    return 0;
}
```

This implementation finds the midpoint of the circular linked list using slow and fast pointers. Then, it splits the list into two halves and adjusts pointers to maintain the circularity of the lists. Finally, it prints both halves of the split circular linked list.

### 1. Algorithms & Data Structures (C++): Circular Singly Linked List: Split a Circular Linked List into Two Halves

To split a circular singly linked list into two halves in C++, you can follow these steps:

1. Find the middle of the list using the slow and fast pointer technique.
2. Break the circular link by assigning NULL to the next pointer of the node before the middle node.
3. Set the head pointers of the two halves accordingly.

Here's a C++ implementation for splitting a circular singly linked list into two halves:

```cpp
#include <iostream>

using namespace std;

// Node structure
struct Node {
    int data;
    Node* next;
    
    Node(int value) : data(value), next(nullptr) {}
};

// Function to split circular linked list into two halves
void splitCircularList(Node* head, Node** firstHalf, Node** secondHalf) {
    if (head == nullptr)
        return;
    
    Node* slow = head;
    Node* fast = head->next;
    
    // Move fast pointer two steps and slow pointer one step at a time
    while (fast != head && fast->next != head) {
        slow = slow->next;
        fast = fast->next->next;
    }
    
    // If the number of elements is even, move fast one more step
    if (fast->next == head)
        fast = fast->next;
    
    // Split the list into two halves
    *firstHalf = head;
    
    if (head->next != head)
        *secondHalf = slow->next;
    
    // Break the circular link
    fast->next = slow->next;
    slow->next = head;
}

// Function to print a circular linked list
void printCircularList(Node* head) {
    if (head == nullptr)
        return;
    
    Node* temp = head;
    do {
        cout << temp->data << " ";
        temp = temp->next;
    } while (temp != head);
}

int main() {
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->next = new Node(3);
    head->next->next->next = new Node(4);
    head->next->next->next->next = new Node(5);
    head->next->next->next->next->next = head; // Making it circular
    
    Node* firstHalf = nullptr;
    Node* secondHalf = nullptr;
    
    // Split the circular list into two halves
    splitCircularList(head, &firstHalf, &secondHalf);
    
    cout << "First half: ";
    printCircularList(firstHalf);
    cout << endl;
    
    cout << "Second half: ";
    printCircularList(secondHalf);
    cout << endl;
    
    return 0;
}
```

In this implementation, `splitCircularList` function takes the head of the circular linked list and two pointers to pointers (`firstHalf` and `secondHalf`). It uses the slow and fast pointer technique to find the middle of the list and then splits the list into two halves. Finally, it updates the pointers `firstHalf` and `secondHalf` accordingly.

### 1. Algorithms & Data Structures (C++): Circular Singly Linked List: Time and Space Complexity

In a circular singly linked list implemented in C++, the time and space complexities for various operations are as follows:

1. **Time Complexity:**
   * **Insertion at the beginning:** O(1)
   * **Insertion at the end:** O(n)
   * **Insertion at a given position:** O(n)
   * **Deletion at the beginning:** O(1)
   * **Deletion at the end:** O(n)
   * **Deletion at a given position:** O(n)
   * **Searching for an element:** O(n)
   * **Traversal:** O(n)

2. **Space Complexity:**
   * The space complexity of a circular singly linked list mainly depends on the number of elements it contains.
   * It requires O(n) space to store 'n' elements in the list.

The main difference between a circular singly linked list and a regular singly linked list in terms of time complexity is that in a circular singly linked list, operations like insertion and deletion at the end of the list have a time complexity of O(n) because you need to traverse the list to reach the end. In a regular singly linked list, you can optimize these operations to have a time complexity of O(1) by maintaining a pointer to the tail node. However, in a circular list, every node technically can act as both the start and end, so you must traverse the list to ensure proper connections.

### 1. Algorithms & Data Structures (C++): Circular Singly Linked List: Traversal

To traverse a circular singly linked list in C++, you can start from any node and keep traversing until you reach the starting node again. Here's an example implementation:

```cpp
#include <iostream>

// Node structure for the circular singly linked list
struct Node {
    int data;
    Node* next;
    
    Node(int val) : data(val), next(nullptr) {}
};

// Function to traverse and print the circular singly linked list
void traverseCircularLinkedList(Node* head) {
    if (head == nullptr) {
        std::cout << "List is empty" << std::endl;
        return;
    }
    
    Node* current = head;  // Start from the head node
    
    // Traverse the list until we reach the head node again
    do {
        std::cout << current->data << " ";
        current = current->next;
    } while (current != head);
    
    std::cout << std::endl;
}

int main() {
    // Creating a sample circular singly linked list: 1 -> 2 -> 3 -> 1
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->next = new Node(3);
    head->next->next->next = head;  // Making it circular
    
    // Traversing and printing the circular singly linked list
    std::cout << "Circular Singly Linked List: ";
    traverseCircularLinkedList(head);

    // Freeing allocated memory
    delete head->next->next;
    delete head->next;
    delete head;

    return 0;
}
```

This code defines a `Node` structure representing each element of the circular singly linked list and a function `traverseCircularLinkedList` to traverse and print the list. In the `main` function, a sample circular singly linked list is created, and then it's traversed and printed using the `traverseCircularLinkedList` function. Finally, memory allocated for the list is freed to prevent memory leaks.
