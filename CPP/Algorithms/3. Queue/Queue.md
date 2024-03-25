### 1. Algorithms & Data Structures (C++): Algorithm development for Double Ended Queue operations

Developing algorithms for Double Ended Queue (Deque) operations involves ensuring efficient insertion and deletion at both ends of the queue. Let's discuss the main operations typically associated with a deque:

1. **Insertion at Front (`push_front`)**: This operation adds an element to the front of the deque.
2. **Insertion at Back (`push_back`)**: This operation adds an element to the back of the deque.
3. **Deletion at Front (`pop_front`)**: This operation removes an element from the front of the deque.
4. **Deletion at Back (`pop_back`)**: This operation removes an element from the back of the deque.
5. **Accessing Front (`front`)**: This operation retrieves the element at the front of the deque.
6. **Accessing Back (`back`)**: This operation retrieves the element at the back of the deque.

Here's a basic implementation of these operations in C++:

```cpp
#include <iostream>
#include <deque>

using namespace std;

int main() {
    deque<int> dq;

    // Insertion at Front
    dq.push_front(1);
    dq.push_front(2);
    dq.push_front(3);

    // Insertion at Back
    dq.push_back(4);
    dq.push_back(5);
    dq.push_back(6);

    // Deletion at Front
    dq.pop_front();

    // Deletion at Back
    dq.pop_back();

    // Accessing Front and Back
    cout << "Front element: " << dq.front() << endl;
    cout << "Back element: " << dq.back() << endl;

    // Displaying the deque
    cout << "Deque: ";
    for (auto it = dq.begin(); it != dq.end(); ++it) {
        cout << *it << " ";
    }
    cout << endl;

    return 0;
}
```

This is a basic implementation. However, if you're interested in the algorithmic details, here's the time complexity analysis for each operation:

* **Insertion at Front (`push_front`)**: O(1)
* **Insertion at Back (`push_back`)**: O(1)
* **Deletion at Front (`pop_front`)**: O(1)
* **Deletion at Back (`pop_back`)**: O(1)
* **Accessing Front (`front`)**: O(1)
* **Accessing Back (`back`)**: O(1)

Deque provides constant time complexity for all these operations because it is implemented as a doubly-linked list or an array-based structure with dynamic resizing. Therefore, it efficiently supports insertion and deletion at both ends.

### 1. Algorithms & Data Structures (C++): Algorithm for Circular Queue operations

A circular queue is a data structure that operates much like a regular queue but with a fixed size. It avoids the wastage of space in a regular queue implementation where elements are dequeued and new elements are enqueued causing the front of the queue to shift and leave empty spaces at the front. Here's a basic algorithm for circular queue operations (enqueue and dequeue) in C++:

```cpp
#include <iostream>

#define SIZE 5

using namespace std;

class CircularQueue {
private:
    int items[SIZE], front, rear;

public:
    CircularQueue() {
        front = -1;
        rear = -1;
    }

    // Function to check if the queue is full
    bool isFull() {
        if ((front == 0 && rear == SIZE - 1) || (rear == (front - 1) % (SIZE - 1))) {
            return true;
        }
        return false;
    }

    // Function to check if the queue is empty
    bool isEmpty() {
        if (front == -1)
            return true;
        else
            return false;
    }

    // Function to add an element to the queue
    void enqueue(int element) {
        if (isFull()) {
            cout << "Queue Overflow \n";
            return;
        }

        if (front == -1) {
            front = 0;
            rear = 0;
        } else if (rear == SIZE - 1 && front != 0) {
            rear = 0;
        } else {
            rear = (rear + 1) % SIZE;
        }
        items[rear] = element;
        cout << element << " enqueued to queue\n";
    }

    // Function to remove an element from the queue
    int dequeue() {
        if (isEmpty()) {
            cout << "Queue Underflow\n";
            return -1;
        }

        int element = items[front];
        if (front == rear) {
            front = -1;
            rear = -1;
        } else {
            front = (front + 1) % SIZE;
        }
        return element;
    }

    // Function to display the queue
    void display() {
        if (isEmpty()) {
            cout << "Queue is empty\n";
            return;
        }
        cout << "Elements in Circular Queue are: ";
        if (rear >= front) {
            for (int i = front; i <= rear; i++)
                cout << items[i] << " ";
        } else {
            for (int i = front; i < SIZE; i++)
                cout << items[i] << " ";

            for (int i = 0; i <= rear; i++)
                cout << items[i] << " ";
        }
        cout << endl;
    }
};

int main() {
    CircularQueue q;

    // Adding elements to the queue
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    q.enqueue(40);
    q.enqueue(50);

    // Displaying the queue
    q.display();

    // Removing elements from the queue
    cout << q.dequeue() << " dequeued from queue\n";
    cout << q.dequeue() << " dequeued from queue\n";

    // Displaying the queue after dequeuing
    q.display();

    // Adding more elements after dequeuing
    q.enqueue(60);
    q.enqueue(70);

    // Displaying the queue after enqueuing
    q.display();

    return 0;
}
```

This code provides basic implementations of circular queue operations such as enqueue, dequeue, and display. It also includes checks for queue overflow and underflow.

### 1. Algorithms & Data Structures (C++): Algorithm for FIFO Queue

Certainly! A FIFO (First-In-First-Out) queue is a data structure that operates on the principle that the first element added to the queue will be the first one to be removed. It's analogous to a queue of people waiting in line: the person who arrived first is the one who gets served first.

In C++, you can implement a FIFO queue using various underlying data structures such as arrays, linked lists, or deques. Here's a simple implementation using a linked list:

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
class Queue {
private:
    Node<T>* front;
    Node<T>* rear;
    int size;

public:
    Queue() : front(nullptr), rear(nullptr), size(0) {}

    ~Queue() {
        while (!isEmpty()) {
            dequeue();
        }
    }

    void enqueue(T data) {
        Node<T>* newNode = new Node<T>(data);
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            rear->next = newNode;
            rear = newNode;
        }
        size++;
    }

    void dequeue() {
        if (isEmpty()) {
            std::cerr << "Queue is empty. Cannot dequeue.\n";
            return;
        }
        Node<T>* temp = front;
        front = front->next;
        delete temp;
        size--;
        if (isEmpty()) {
            rear = nullptr;
        }
    }

    T peek() const {
        if (isEmpty()) {
            std::cerr << "Queue is empty. Cannot peek.\n";
            exit(EXIT_FAILURE);
        }
        return front->data;
    }

    bool isEmpty() const {
        return size == 0;
    }

    int getSize() const {
        return size;
    }
};

int main() {
    Queue<int> q;
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);

    std::cout << "Queue size: " << q.getSize() << std::endl;
    std::cout << "Front element: " << q.peek() << std::endl;

    q.dequeue();
    std::cout << "Front element after dequeue: " << q.peek() << std::endl;

    return 0;
}
```

This code defines a simple FIFO queue using a singly linked list. It includes operations such as `enqueue` to add elements to the queue, `dequeue` to remove elements from the front of the queue, `peek` to see the front element without removing it, and `isEmpty` and `getSize` to check the state of the queue.

### 1. Algorithms & Data Structures (C++): Array representation of Queue

In C++, you can represent a queue using an array. Here's a simple implementation of a queue using an array:

```cpp
#include <iostream>

#define MAX_SIZE 100

class Queue {
private:
    int front, rear, size;
    int arr[MAX_SIZE];

public:
    Queue() {
        front = rear = -1;
        size = 0;
    }

    bool isEmpty() {
        return size == 0;
    }

    bool isFull() {
        return size == MAX_SIZE;
    }

    void enqueue(int value) {
        if (isFull()) {
            std::cout << "Queue is full. Cannot enqueue more elements." << std::endl;
            return;
        }
        if (isEmpty())
            front = 0;
        rear = (rear + 1) % MAX_SIZE;
        arr[rear] = value;
        size++;
    }

    void dequeue() {
        if (isEmpty()) {
            std::cout << "Queue is empty. Cannot dequeue." << std::endl;
            return;
        }
        front = (front + 1) % MAX_SIZE;
        size--;
        if (isEmpty())
            front = rear = -1;
    }

    int peek() {
        if (isEmpty()) {
            std::cout << "Queue is empty. No front element." << std::endl;
            return -1; // Return some default value indicating queue is empty
        }
        return arr[front];
    }
};

int main() {
    Queue q;

    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    q.enqueue(40);

    std::cout << "Front element: " << q.peek() << std::endl;

    q.dequeue();
    q.dequeue();

    std::cout << "Front element after dequeue: " << q.peek() << std::endl;

    return 0;
}
```

In this implementation, we use an array to store the elements of the queue. The front and rear indices keep track of the positions of the first and last elements, respectively. We use the modulo operator to handle wrap-around when the end of the array is reached.

This implementation has a maximum size defined by `MAX_SIZE`. When the queue is full, attempting to enqueue additional elements will result in an error message. Similarly, attempting to dequeue from an empty queue will result in an error message.

### 1. Algorithms & Data Structures (C++): Build A Queue With Two Stacks

Sure! In C++, you can implement a queue using two stacks. One stack will be used for enqueue operations (pushing elements) and the other for dequeue operations (popping elements). Here's how you can implement it:

```cpp
#include <iostream>
#include <stack>

using namespace std;

class QueueWithTwoStacks {
private:
    stack<int> inbox;   // Stack for enqueue operations
    stack<int> outbox;  // Stack for dequeue operations

public:
    // Add an element to the back of the queue
    void enqueue(int element) {
        inbox.push(element);
    }

    // Remove the front element of the queue and return it
    int dequeue() {
        if (outbox.empty()) {
            // If outbox is empty, transfer elements from inbox
            while (!inbox.empty()) {
                outbox.push(inbox.top());
                inbox.pop();
            }
        }
        
        if (outbox.empty()) {
            // Queue is empty
            cout << "Queue is empty!" << endl;
            return -1; // Or throw an exception
        }

        int frontElement = outbox.top();
        outbox.pop();
        return frontElement;
    }

    // Check if the queue is empty
    bool isEmpty() {
        return inbox.empty() && outbox.empty();
    }
};

int main() {
    QueueWithTwoStacks q;

    q.enqueue(1);
    q.enqueue(2);
    q.enqueue(3);

    cout << q.dequeue() << endl; // Should print 1
    cout << q.dequeue() << endl; // Should print 2

    q.enqueue(4);
    q.enqueue(5);

    cout << q.dequeue() << endl; // Should print 3
    cout << q.dequeue() << endl; // Should print 4
    cout << q.dequeue() << endl; // Should print 5

    cout << q.dequeue() << endl; // Should print "Queue is empty!" and -1

    return 0;
}
```

This implementation should give you a basic understanding of how to build a queue using two stacks in C++. The `enqueue` operation is straightforward as it just pushes elements onto one stack (`inbox`). The `dequeue` operation is a bit more complex; if the `outbox` stack is empty, it transfers elements from `inbox` to `outbox` first, and then pops the top element from `outbox` to simulate a dequeue operation. This way, the elements are dequeued in the same order as they were enqueued.

### 1. Algorithms & Data Structures (C++): Circular Queue

A Circular Queue is a data structure that serves as a queue where the last position is connected back to the first position to make a circle. It overcomes the limitation of a standard queue where insertion can cause overflow and deletion can cause underflow. Circular queues efficiently utilize memory and can be implemented using arrays.

Here's a simple implementation of a Circular Queue in C++:

```cpp
#include <iostream>
using namespace std;

#define SIZE 5

class CircularQueue {
private:
    int front, rear;
    int items[SIZE];

public:
    CircularQueue() {
        front = -1;
        rear = -1;
    }

    // Check if the queue is full
    bool isFull() {
        if ((front == 0 && rear == SIZE - 1) || (rear == front - 1))
            return true;
        return false;
    }

    // Check if the queue is empty
    bool isEmpty() {
        if (front == -1)
            return true;
        return false;
    }

    // Add an element to the queue
    void enqueue(int element) {
        if (isFull()) {
            cout << "Queue is full\n";
            return;
        }
        if (front == -1)
            front = 0;
        rear = (rear + 1) % SIZE;
        items[rear] = element;
        cout << element << " enqueued to queue\n";
    }

    // Remove an element from the queue
    int dequeue() {
        int element;
        if (isEmpty()) {
            cout << "Queue is empty\n";
            return -1;
        }
        element = items[front];
        if (front == rear) {
            front = -1;
            rear = -1;
        } else {
            front = (front + 1) % SIZE;
        }
        return element;
    }

    // Display the elements of the queue
    void display() {
        int i;
        if (isEmpty()) {
            cout << "Queue is empty\n";
            return;
        }
        cout << "Front -> ";
        for (i = front; i != rear; i = (i + 1) % SIZE)
            cout << items[i] << " ";
        cout << items[i] << " ";
        cout << "<- Rear\n";
    }
};

int main() {
    CircularQueue q;

    // Adding elements to Circular Queue
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    q.enqueue(40);

    // Display elements present in Circular Queue
    q.display();

    // Deleting elements from Circular Queue
    cout << "Deleted value = " << q.dequeue() << endl;
    cout << "Deleted value = " << q.dequeue() << endl;

    // Remaining elements in Circular Queue
    q.display();

    q.enqueue(50);
    q.enqueue(60);
    q.enqueue(70);

    // Display elements present in Circular Queue
    q.display();

    return 0;
}
```

This implementation includes the basic operations of a Circular Queue:

* **enqueue**: Adds an element to the rear of the queue.
* **dequeue**: Removes an element from the front of the queue.
* **isFull**: Checks if the queue is full.
* **isEmpty**: Checks if the queue is empty.
* **display**: Displays the elements of the queue.

The circular nature of the queue is handled by using the modulo operator (%) to wrap around the rear index when it reaches the end of the array.

### 1. Algorithms & Data Structures (C++): Circular Queue (Implementation)

Certainly! Implementing a circular queue in C++ involves creating a data structure that allows for efficient insertion and deletion operations from both ends of the queue. Here's a basic implementation:

```cpp
#include <iostream>

using namespace std;

class CircularQueue {
private:
    int front, rear, capacity;
    int *arr;

public:
    CircularQueue(int size) {
        capacity = size;
        arr = new int[capacity];
        front = rear = -1;
    }

    ~CircularQueue() {
        delete[] arr;
    }

    // Function to enqueue an element
    void enqueue(int element) {
        if ((rear + 1) % capacity == front) {
            cout << "Queue is full. Enqueue operation failed.\n";
            return;
        }

        if (isEmpty())
            front = 0;

        rear = (rear + 1) % capacity;
        arr[rear] = element;
        cout << element << " enqueued to the queue.\n";
    }

    // Function to dequeue an element
    int dequeue() {
        if (isEmpty()) {
            cout << "Queue is empty. Dequeue operation failed.\n";
            return -1;
        }

        int dequeuedElement = arr[front];
        if (front == rear)
            front = rear = -1;
        else
            front = (front + 1) % capacity;

        return dequeuedElement;
    }

    // Function to check if the queue is empty
    bool isEmpty() {
        return front == -1;
    }

    // Function to check if the queue is full
    bool isFull() {
        return (rear + 1) % capacity == front;
    }

    // Function to get the front element of the queue
    int peek() {
        if (isEmpty()) {
            cout << "Queue is empty. Peek operation failed.\n";
            return -1;
        }
        return arr[front];
    }

    // Function to display the elements of the queue
    void display() {
        if (isEmpty()) {
            cout << "Queue is empty.\n";
            return;
        }

        cout << "Elements in the queue are: ";
        int i = front;
        do {
            cout << arr[i] << " ";
            i = (i + 1) % capacity;
        } while (i != (rear + 1) % capacity);
        cout << endl;
    }
};

int main() {
    CircularQueue cq(5);

    cq.enqueue(1);
    cq.enqueue(2);
    cq.enqueue(3);
    cq.enqueue(4);
    cq.enqueue(5);
    cq.enqueue(6); // Should fail, as the queue is full

    cq.display();

    cout << "Dequeued: " << cq.dequeue() << endl;
    cout << "Dequeued: " << cq.dequeue() << endl;

    cq.display();

    cq.enqueue(6); // Should work, as there's space now
    cq.display();

    return 0;
}
```

This implementation uses an array to store the elements of the queue and maintains two pointers `front` and `rear` to keep track of the front and rear ends of the queue respectively. The modulo operation is used to ensure circular behavior when incrementing these pointers.

### 1. Algorithms & Data Structures (C++): Circular Queue (Theory)

A Circular Queue is a data structure that behaves like a normal queue (FIFO - First In, First Out), but with a fixed size. The main difference between a circular queue and a regular queue is that once the queue becomes full, instead of refusing to accept more elements, it starts overwriting the oldest elements in the queue.

Here's the basic theory behind implementing a Circular Queue in C++:

#### 1. Implementation

In C++, you can implement a Circular Queue using an array and two pointers, `front` and `rear`.

* `front`: points to the first element of the queue.
* `rear`: points to the last element of the queue.

Initially, both `front` and `rear` are set to `-1`.

#### 2. Operations

* **Enqueue (Insertion)**: To insert an element into the circular queue, you move the `rear` pointer to the next available position and insert the element there.

* **Dequeue (Deletion)**: To remove an element from the circular queue, you move the `front` pointer to the next available position and remove the element from there.

#### 3. Handling Circular Nature

Since the queue is circular, after reaching the end of the array, the `rear` pointer wraps around to the beginning, and similarly, after reaching the end, the `front` pointer wraps around to the beginning as well.

#### 4. Overflow and Underflow Conditions

* **Overflow**: Occurs when you try to insert an element into a full queue.
* **Underflow**: Occurs when you try to remove an element from an empty queue.

#### 5. Implementation Tips

* Always check for overflow and underflow conditions.
* Ensure to update the pointers correctly after every insertion and deletion operation.
* Handle the circular nature of the queue properly to avoid incorrect behavior.

#### Sample Code (Partial Implementation)

Here's a simplified implementation of a Circular Queue in C++:

```cpp
#include <iostream>
using namespace std;

#define SIZE 5

class CircularQueue {
private:
    int arr[SIZE];
    int front, rear;

public:
    CircularQueue() {
        front = rear = -1;
    }

    // Function to check if queue is full
    bool isFull() {
        return (front == 0 && rear == SIZE - 1) || (rear == (front - 1) % (SIZE - 1));
    }

    // Function to check if queue is empty
    bool isEmpty() {
        return front == -1;
    }

    // Function to insert an element into the queue
    void enqueue(int value) {
        if (isFull()) {
            cout << "Queue is full!" << endl;
            return;
        }
        if (front == -1)
            front = 0;
        rear = (rear + 1) % SIZE;
        arr[rear] = value;
        cout << value << " enqueued to queue." << endl;
    }

    // Function to remove an element from the queue
    int dequeue() {
        int value;
        if (isEmpty()) {
            cout << "Queue is empty!" << endl;
            return -1;
        }
        value = arr[front];
        if (front == rear)
            front = rear = -1;
        else
            front = (front + 1) % SIZE;
        return value;
    }

    // Function to display the elements of the queue
    void display() {
        if (isEmpty()) {
            cout << "Queue is empty!" << endl;
            return;
        }
        int i = front;
        do {
            cout << arr[i] << " ";
            i = (i + 1) % SIZE;
        } while (i != (rear + 1) % SIZE);
        cout << endl;
    }
};

int main() {
    CircularQueue q;
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    q.enqueue(40);
    q.enqueue(50);
    q.enqueue(60); // Queue is full
    cout << "Queue: ";
    q.display();
    cout << "Dequeued: " << q.dequeue() << endl;
    cout << "Queue: ";
    q.display();
    return 0;
}
```

This code provides a basic implementation of a Circular Queue in C++. You can extend it further by adding additional functionalities like peek, clear, etc., as per your requirements.

### 1. Algorithms & Data Structures (C++): Circular Queue Operations

Certainly! A circular queue is a data structure that operates much like a regular queue, but it wraps around itself. This means that when an element is dequeued, the space it occupied becomes available for future enqueue operations. Here's a basic implementation of circular queue operations in C++:

```cpp
#include <iostream>

using namespace std;

class CircularQueue {
private:
    int *arr;
    int front, rear, maxSize;
public:
    CircularQueue(int size) {
        maxSize = size;
        arr = new int[maxSize];
        front = rear = -1;
    }

    ~CircularQueue() {
        delete[] arr;
    }

    bool isEmpty() {
        return front == -1;
    }

    bool isFull() {
        return (front == 0 && rear == maxSize - 1) || (rear == (front - 1) % (maxSize - 1));
    }

    void enqueue(int item) {
        if (isFull()) {
            cout << "Queue is full, cannot enqueue " << item << endl;
            return;
        }

        if (isEmpty()) {
            front = rear = 0;
        } else {
            rear = (rear + 1) % maxSize;
        }
        arr[rear] = item;
        cout << item << " enqueued to queue" << endl;
    }

    int dequeue() {
        if (isEmpty()) {
            cout << "Queue is empty, cannot dequeue" << endl;
            return -1;
        }

        int item = arr[front];
        if (front == rear) {
            front = rear = -1;
        } else {
            front = (front + 1) % maxSize;
        }
        cout << item << " dequeued from queue" << endl;
        return item;
    }

    void display() {
        if (isEmpty()) {
            cout << "Queue is empty" << endl;
            return;
        }

        cout << "Elements in circular queue are:" << endl;
        if (rear >= front) {
            for (int i = front; i <= rear; i++)
                cout << arr[i] << " ";
        } else {
            for (int i = front; i < maxSize; i++)
                cout << arr[i] << " ";
            for (int i = 0; i <= rear; i++)
                cout << arr[i] << " ";
        }
        cout << endl;
    }
};

int main() {
    CircularQueue cq(5);

    cq.enqueue(10);
    cq.enqueue(20);
    cq.enqueue(30);
    cq.enqueue(40);
    cq.enqueue(50);

    cq.display();

    cout << "Dequeued item: " << cq.dequeue() << endl;
    cout << "Dequeued item: " << cq.dequeue() << endl;

    cq.display();

    cq.enqueue(60);
    cq.enqueue(70);

    cq.display();

    return 0;
}
```

This code demonstrates the basic operations of a circular queue:

1. `enqueue`: Adds an element to the rear of the queue.
2. `dequeue`: Removes and returns the element from the front of the queue.
3. `isEmpty`: Checks if the queue is empty.
4. `isFull`: Checks if the queue is full.
5. `display`: Displays the elements of the queue.

In this implementation, the circular nature of the queue is achieved by using modulo operations to wrap around the indices of the array representing the queue.

### 1. Algorithms & Data Structures (C++): Circular queue: dequeue

Certainly! A circular queue is a data structure that follows the First In First Out (FIFO) principle, where elements are inserted at the rear and removed from the front.

In C++, you can implement a circular queue using an array. Here's a basic implementation of the `dequeue` operation for a circular queue:

```cpp
#include <iostream>
using namespace std;

#define MAX_SIZE 100

class CircularQueue {
private:
    int front, rear;
    int arr[MAX_SIZE];

public:
    CircularQueue() {
        front = rear = -1;
    }

    // Function to check if the queue is empty
    bool isEmpty() {
        return (front == -1 && rear == -1);
    }

    // Function to check if the queue is full
    bool isFull() {
        return (rear + 1) % MAX_SIZE == front;
    }

    // Function to enqueue an element
    void enqueue(int value) {
        if (isFull()) {
            cout << "Queue is full. Cannot enqueue.\n";
            return;
        } else if (isEmpty()) {
            front = rear = 0;
        } else {
            rear = (rear + 1) % MAX_SIZE;
        }
        arr[rear] = value;
    }

    // Function to dequeue an element
    void dequeue() {
        if (isEmpty()) {
            cout << "Queue is empty. Cannot dequeue.\n";
            return;
        } else if (front == rear) {
            // If there's only one element in the queue
            front = rear = -1;
        } else {
            front = (front + 1) % MAX_SIZE;
        }
    }

    // Function to display the elements in the queue
    void display() {
        if (isEmpty()) {
            cout << "Queue is empty.\n";
            return;
        }

        int i = front;
        cout << "Queue elements: ";
        do {
            cout << arr[i] << " ";
            i = (i + 1) % MAX_SIZE;
        } while (i != (rear + 1) % MAX_SIZE);
        cout << endl;
    }
};

int main() {
    CircularQueue q;
    q.enqueue(1);
    q.enqueue(2);
    q.enqueue(3);
    q.display();

    q.dequeue();
    q.display();

    q.enqueue(4);
    q.display();

    q.dequeue();
    q.dequeue();
    q.dequeue();
    q.display();

    return 0;
}
```

In this implementation:

* `dequeue()` removes an element from the front of the circular queue. If the queue becomes empty after removal, it updates the front and rear pointers accordingly.
* The circular nature of the queue is handled using the modulo operator `% MAX_SIZE` to wrap around the array when it reaches the end.
* `front` and `rear` are indices pointing to the front and rear elements of the queue respectively.
* `MAX_SIZE` defines the maximum capacity of the circular queue.

### 1. Algorithms & Data Structures (C++): Circular queue: enqueue

To implement the enqueue operation for a circular queue in C++, you need to consider the following steps:

1. Check if the circular queue is full.
2. If it's not full, insert the element at the rear of the queue.
3. Update the rear pointer to the next position.
4. Handle the circular aspect of the queue by considering wrapping around the end of the array if necessary.

Here's a sample implementation:

```cpp
#include <iostream>

#define MAX_SIZE 100

class CircularQueue {
private:
    int front, rear;
    int arr[MAX_SIZE];

public:
    CircularQueue() {
        front = rear = -1;
    }

    // Function to check if the queue is full
    bool isFull() {
        return (front == 0 && rear == MAX_SIZE - 1) || (rear == (front - 1) % (MAX_SIZE - 1));
    }

    // Function to check if the queue is empty
    bool isEmpty() {
        return front == -1;
    }

    // Function to add an element to the queue
    void enqueue(int data) {
        if (isFull()) {
            std::cout << "Queue is full. Cannot enqueue.\n";
            return;
        }

        if (front == -1) {
            front = rear = 0;
        } else {
            rear = (rear + 1) % MAX_SIZE;
        }

        arr[rear] = data;
        std::cout << data << " enqueued to the queue.\n";
    }

    // Function to display elements of the queue
    void display() {
        if (isEmpty()) {
            std::cout << "Queue is empty.\n";
            return;
        }

        int i = front;
        do {
            std::cout << arr[i] << " ";
            i = (i + 1) % MAX_SIZE;
        } while (i != (rear + 1) % MAX_SIZE);
        std::cout << std::endl;
    }
};

int main() {
    CircularQueue q;

    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    q.enqueue(40);
    q.enqueue(50);

    q.display();

    return 0;
}
```

In this implementation:

* `MAX_SIZE` defines the maximum capacity of the circular queue.
* `front` and `rear` are pointers to the front and rear elements of the queue, respectively.
* The `enqueue()` function adds an element to the queue.
* The `isFull()` and `isEmpty()` functions check if the queue is full or empty, respectively.
* The `display()` function is used to display the elements of the queue.

### 1. Algorithms & Data Structures (C++): Circular queue: operations

In C++, implementing a circular queue involves managing the front and rear pointers to keep track of the elements. Circular queues are often used when you want to efficiently use memory by reusing positions once elements are dequeued. Here are the basic operations for a circular queue:

1. **Enqueue (Insertion)**: Add an element to the rear of the queue.
2. **Dequeue (Deletion)**: Remove an element from the front of the queue.
3. **isEmpty**: Check if the queue is empty.
4. **isFull**: Check if the queue is full.
5. **Front**: Get the element at the front of the queue.
6. **Rear**: Get the element at the rear of the queue.

Here's a basic implementation of a circular queue in C++:

```cpp
#include <iostream>
using namespace std;

#define SIZE 5

class CircularQueue {
private:
    int front, rear;
    int arr[SIZE];

public:
    CircularQueue() {
        front = rear = -1;
    }

    // Function to check if the queue is empty
    bool isEmpty() {
        return (front == -1 && rear == -1);
    }

    // Function to check if the queue is full
    bool isFull() {
        return (rear + 1) % SIZE == front;
    }

    // Function to add an element to the rear of the queue
    void enqueue(int value) {
        if (isFull()) {
            cout << "Queue is full. Cannot enqueue." << endl;
            return;
        } else if (isEmpty()) {
            front = rear = 0;
        } else {
            rear = (rear + 1) % SIZE;
        }
        arr[rear] = value;
        cout << value << " enqueued to the queue." << endl;
    }

    // Function to remove an element from the front of the queue
    void dequeue() {
        if (isEmpty()) {
            cout << "Queue is empty. Cannot dequeue." << endl;
            return;
        } else if (front == rear) {
            cout << arr[front] << " dequeued from the queue." << endl;
            front = rear = -1;
        } else {
            cout << arr[front] << " dequeued from the queue." << endl;
            front = (front + 1) % SIZE;
        }
    }

    // Function to get the element at the front of the queue
    int Front() {
        if (isEmpty()) {
            cout << "Queue is empty." << endl;
            return -1;
        }
        return arr[front];
    }

    // Function to get the element at the rear of the queue
    int Rear() {
        if (isEmpty()) {
            cout << "Queue is empty." << endl;
            return -1;
        }
        return arr[rear];
    }
};

int main() {
    CircularQueue q;

    // Example usage
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    q.enqueue(40);
    q.enqueue(50);

    cout << "Front element: " << q.Front() << endl;
    cout << "Rear element: " << q.Rear() << endl;

    q.dequeue();
    q.dequeue();

    cout << "Front element after two dequeues: " << q.Front() << endl;

    return 0;
}
```

This code provides a basic implementation of a circular queue in C++. You can add more operations or modify it according to your requirements.

### 1. Algorithms & Data Structures (C++): Circular Queue: Sorting and Searching

Implementing sorting and searching algorithms on a circular queue in C++ involves a few considerations due to its circular nature. Here's a basic example of how you can implement sorting and searching functionalities on a circular queue:

```cpp
#include <iostream>
using namespace std;

const int MAX_SIZE = 100;

class CircularQueue {
private:
    int arr[MAX_SIZE];
    int front, rear, size;

public:
    CircularQueue() {
        front = rear = -1;
        size = 0;
    }

    bool isEmpty() {
        return size == 0;
    }

    bool isFull() {
        return size == MAX_SIZE;
    }

    void enqueue(int value) {
        if (isFull()) {
            cout << "Queue is full. Cannot enqueue.\n";
            return;
        }
        if (front == -1)  // if queue is initially empty
            front = 0;
        rear = (rear + 1) % MAX_SIZE;
        arr[rear] = value;
        size++;
    }

    int dequeue() {
        if (isEmpty()) {
            cout << "Queue is empty. Cannot dequeue.\n";
            return -1;
        }
        int value = arr[front];
        if (front == rear)  // if only one element is present
            front = rear = -1;
        else
            front = (front + 1) % MAX_SIZE;
        size--;
        return value;
    }

    void display() {
        if (isEmpty()) {
            cout << "Queue is empty.\n";
            return;
        }
        int i = front;
        do {
            cout << arr[i] << " ";
            i = (i + 1) % MAX_SIZE;
        } while (i != (rear + 1) % MAX_SIZE);
        cout << endl;
    }

    // Sorting the circular queue using bubble sort
    void bubbleSort() {
        if (isEmpty()) {
            cout << "Queue is empty. Nothing to sort.\n";
            return;
        }
        for (int i = 0; i < size - 1; i++) {
            for (int j = 0; j < size - i - 1; j++) {
                int nextIdx = (front + j + 1) % MAX_SIZE;
                int nextNextIdx = (front + j + 2) % MAX_SIZE;
                if (arr[nextIdx] > arr[nextNextIdx]) {
                    swap(arr[nextIdx], arr[nextNextIdx]);
                }
            }
        }
    }

    // Searching for an element in the circular queue
    bool search(int key) {
        if (isEmpty()) {
            cout << "Queue is empty. Nothing to search.\n";
            return false;
        }
        int i = front;
        do {
            if (arr[i] == key)
                return true;
            i = (i + 1) % MAX_SIZE;
        } while (i != (rear + 1) % MAX_SIZE);
        return false;
    }
};

int main() {
    CircularQueue cq;
    cq.enqueue(5);
    cq.enqueue(3);
    cq.enqueue(8);
    cq.enqueue(1);
    cq.enqueue(9);

    cout << "Original Circular Queue: ";
    cq.display();

    cq.bubbleSort();
    cout << "Sorted Circular Queue: ";
    cq.display();

    int searchKey = 8;
    if (cq.search(searchKey))
        cout << searchKey << " found in the queue.\n";
    else
        cout << searchKey << " not found in the queue.\n";

    return 0;
}
```

This code provides a basic implementation of a circular queue with sorting and searching functionalities using bubble sort and linear search respectively. You can modify and optimize these functionalities as per your requirements and preferences.

### 1. Algorithms & Data Structures (C++): Circular Queue: Sorting Trade-Offs

When implementing a circular queue in C++ and considering sorting trade-offs, several factors come into play, including time complexity, space complexity, and the specific requirements of your application. Here's a breakdown:

1. **Sorting Frequency**: How often do you need to sort the elements in the circular queue? If sorting is infrequent or not required at all, you might prioritize other aspects of your data structure implementation, such as efficient enqueue and dequeue operations.

2. **Sorting Algorithm Choice**: If sorting is necessary, the choice of sorting algorithm depends on the size of the queue and the data distribution. For smaller queues or nearly sorted data, simple algorithms like insertion sort or bubble sort might be sufficient due to their low overhead. For larger queues or random data, more sophisticated algorithms like quicksort or mergesort might offer better performance on average.

3. **Space Complexity**: Some sorting algorithms have additional space complexity requirements. For example, mergesort typically requires additional space proportional to the size of the input, while in-place algorithms like quicksort have lower space overhead. Consider the memory constraints of your application when choosing a sorting algorithm.

4. **Time Complexity**: The time complexity of sorting impacts the overall performance of operations on the circular queue. While quicksort and mergesort have average-case time complexities of O(n log n), other algorithms like insertion sort have worst-case time complexities of O(n^2). Depending on the size and characteristics of your data, this trade-off might be acceptable.

5. **Stability**: If the order of elements with equal keys needs to be preserved, stability becomes an important consideration when choosing a sorting algorithm. Merge sort is inherently stable, while quicksort is not without additional modifications.

6. **Implementation Complexity**: Consider the complexity of implementing and maintaining the chosen sorting algorithm within your circular queue implementation. Some algorithms, like insertion sort, have simpler implementations compared to others like mergesort or quicksort.

In summary, when designing a circular queue in C++ with sorting capabilities, carefully weigh factors such as sorting frequency, space complexity, time complexity, stability, and implementation complexity to choose the most suitable sorting algorithm for your specific use case.

### 1. Algorithms & Data Structures (C++): Concept of Imitating a Queue using 2 Stacks

Imitating a queue using two stacks is a classic problem in computer science and is often used to demonstrate how different data structures can be combined to achieve certain functionalities. In this case, we're trying to simulate the behavior of a queue (FIFO - First In, First Out) using two stacks (LIFO - Last In, First Out).

Here's how you can implement this concept in C++:

```cpp
#include <iostream>
#include <stack>

using namespace std;

template<typename T>
class QueueWithStacks {
private:
    stack<T> inbox;    // For enqueue operation
    stack<T> outbox;   // For dequeue operation

public:
    // Add an element to the back of the queue
    void enqueue(const T& element) {
        inbox.push(element);
    }

    // Remove and return the front element of the queue
    T dequeue() {
        if (outbox.empty()) {
            // If the outbox is empty, transfer elements from inbox to outbox
            while (!inbox.empty()) {
                outbox.push(inbox.top());
                inbox.pop();
            }
        }

        if (outbox.empty()) {
            // If both stacks are empty, the queue is empty
            cerr << "Error: Queue is empty!" << endl;
            exit(1); // Or throw an exception
        }

        T frontElement = outbox.top();
        outbox.pop();
        return frontElement;
    }

    // Check if the queue is empty
    bool isEmpty() const {
        return inbox.empty() && outbox.empty();
    }

    // Get the number of elements in the queue
    size_t size() const {
        return inbox.size() + outbox.size();
    }
};

int main() {
    QueueWithStacks<int> q;

    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);

    cout << "Dequeued: " << q.dequeue() << endl;
    cout << "Dequeued: " << q.dequeue() << endl;

    q.enqueue(40);

    cout << "Dequeued: " << q.dequeue() << endl;
    cout << "Dequeued: " << q.dequeue() << endl;

    return 0;
}
```

Explanation:

* We have two stacks: `inbox` and `outbox`.
* For `enqueue` operation, we simply push elements onto the `inbox`.
* For `dequeue` operation, if `outbox` is empty, we transfer all elements from `inbox` to `outbox`, effectively reversing their order. This ensures that the oldest element is at the top of `outbox`, mimicking the behavior of a queue. Then, we pop from `outbox` to retrieve the front element.
* The `isEmpty` and `size` functions provide the corresponding functionalities to check if the queue is empty and get its size.

This implementation provides the same time complexities as a regular queue for enqueue, dequeue, isEmpty, and size operations, all O(1) amortized time complexity.

### 1. Algorithms & Data Structures (C++): Constructor and Destructor of Queue Class

Sure, I can provide you with a basic implementation of a queue class in C++ including its constructor and destructor. Here's a simple example:

```cpp
#include <iostream>

template <typename T>
class Queue {
private:
    struct Node {
        T data;
        Node* next;
        Node(T value) : data(value), next(nullptr) {}
    };

    Node* frontPtr;
    Node* rearPtr;

public:
    Queue() : frontPtr(nullptr), rearPtr(nullptr) {}

    ~Queue() {
        while (!isEmpty()) {
            dequeue();
        }
    }

    void enqueue(const T& value) {
        Node* newNode = new Node(value);
        if (isEmpty()) {
            frontPtr = rearPtr = newNode;
        } else {
            rearPtr->next = newNode;
            rearPtr = newNode;
        }
    }

    void dequeue() {
        if (isEmpty()) {
            std::cerr << "Queue is empty. Cannot dequeue.\n";
            return;
        }
        Node* temp = frontPtr;
        frontPtr = frontPtr->next;
        delete temp;
        if (frontPtr == nullptr) {
            rearPtr = nullptr;
        }
    }

    bool isEmpty() const {
        return frontPtr == nullptr;
    }

    const T& front() const {
        if (isEmpty()) {
            std::cerr << "Queue is empty. No front element.\n";
            // Return a default value or throw an exception as desired
        }
        return frontPtr->data;
    }

    const T& rear() const {
        if (isEmpty()) {
            std::cerr << "Queue is empty. No rear element.\n";
            // Return a default value or throw an exception as desired
        }
        return rearPtr->data;
    }
};

int main() {
    Queue<int> myQueue;
    myQueue.enqueue(10);
    myQueue.enqueue(20);
    myQueue.enqueue(30);

    std::cout << "Front of the queue: " << myQueue.front() << std::endl;
    std::cout << "Rear of the queue: " << myQueue.rear() << std::endl;

    myQueue.dequeue();

    std::cout << "Front of the queue after dequeue: " << myQueue.front() << std::endl;

    return 0;
}
```

In this implementation:

* The `Queue` class uses a linked list to implement the queue.
* The constructor initializes both `frontPtr` and `rearPtr` to `nullptr`.
* The destructor deallocates all memory allocated for the nodes in the queue.
* `enqueue()` adds an element to the rear of the queue.
* `dequeue()` removes an element from the front of the queue.
* `front()` returns the element at the front of the queue without removing it.
* `rear()` returns the element at the rear of the queue without removing it.
* `isEmpty()` checks whether the queue is empty or not.

This is a basic implementation. Depending on your requirements, you might need to add error handling, additional functionality, or optimize certain operations for efficiency.

### 1. Algorithms & Data Structures (C++): Creating a Queue From Stacks

Creating a queue from stacks is a classic problem in computer science. You can implement a queue using two stacks. One stack will act as the input stack, where you enqueue elements, and the other stack will act as the output stack, where you dequeue elements.

Here's a basic implementation of a queue using two stacks in C++:

```cpp
#include <iostream>
#include <stack>

template <typename T>
class QueueFromStacks {
private:
    std::stack<T> inputStack;
    std::stack<T> outputStack;

public:
    // Enqueue operation
    void enqueue(const T& value) {
        inputStack.push(value);
    }

    // Dequeue operation
    T dequeue() {
        if (outputStack.empty()) {
            // If output stack is empty, transfer elements from input stack
            while (!inputStack.empty()) {
                outputStack.push(inputStack.top());
                inputStack.pop();
            }
        }
        
        // If output stack is still empty, queue is empty
        if (outputStack.empty()) {
            throw std::out_of_range("Queue is empty");
        }

        T front = outputStack.top();
        outputStack.pop();
        return front;
    }

    // Check if the queue is empty
    bool isEmpty() const {
        return inputStack.empty() && outputStack.empty();
    }

    // Get the size of the queue
    size_t size() const {
        return inputStack.size() + outputStack.size();
    }
};

int main() {
    QueueFromStacks<int> myQueue;

    // Enqueue some elements
    myQueue.enqueue(10);
    myQueue.enqueue(20);
    myQueue.enqueue(30);

    // Dequeue and print elements
    std::cout << "Dequeued: " << myQueue.dequeue() << std::endl;
    std::cout << "Dequeued: " << myQueue.dequeue() << std::endl;

    // Enqueue more elements
    myQueue.enqueue(40);
    myQueue.enqueue(50);

    // Dequeue and print remaining elements
    while (!myQueue.isEmpty()) {
        std::cout << "Dequeued: " << myQueue.dequeue() << std::endl;
    }

    return 0;
}
```

In this implementation:

* We use two stacks, `inputStack` and `outputStack`, to simulate the queue operations.
* The `enqueue` operation simply pushes elements onto the `inputStack`.
* The `dequeue` operation pops elements from the `outputStack`. If the `outputStack` is empty, we transfer elements from the `inputStack` to the `outputStack` first.
* The `isEmpty` and `size` methods provide information about the state of the queue.

### 1. Algorithms & Data Structures (C++): Data Structure : Priority Queue

A Priority Queue is a data structure similar to a regular queue, but each element in the queue has a priority associated with it. In a priority queue, an element with high priority is served before an element with low priority. This means that elements with higher priority are dequeued before those with lower priority.

In C++, you can implement a priority queue using the `std::priority_queue` container provided by the Standard Template Library (STL). Here's a brief overview of how to use it:

```cpp
#include <iostream>
#include <queue>

int main() {
    // Declaration of a priority queue of integers
    std::priority_queue<int> pq;

    // Inserting elements into the priority queue
    pq.push(10);
    pq.push(20);
    pq.push(15);

    // Accessing the top element of the priority queue
    std::cout << "Top element of the priority queue: " << pq.top() << std::endl;

    // Removing the top element
    pq.pop();

    // Accessing the new top element
    std::cout << "Top element after popping: " << pq.top() << std::endl;

    return 0;
}
```

In this example:

* We include the necessary header files (`#include <iostream>` and `#include <queue>`).
* We declare a priority queue `pq` of integers (`std::priority_queue<int>`).
* We insert elements into the priority queue using the `push()` method.
* We access the top element of the priority queue using the `top()` method.
* We remove the top element from the priority queue using the `pop()` method.
* Finally, we access the new top element after popping.

The priority queue in C++ is implemented as a max-heap by default, meaning that the element with the highest value has the highest priority. If you want to change the priority queue to behave like a min-heap, where the element with the lowest value has the highest priority, you can specify a different comparison function as the second template parameter of `std::priority_queue`. For example:

```cpp
// Declaration of a priority queue of integers, with a custom comparison function
std::priority_queue<int, std::vector<int>, std::greater<int>> pq;
```

This declaration creates a priority queue of integers where the element with the smallest value has the highest priority.

Priority queues are commonly used in algorithms like Dijkstra's algorithm for finding the shortest path in graphs and in implementing algorithms like Prim's and Kruskal's algorithms for finding minimum spanning trees. They are also used in various scheduling algorithms and in simulating systems where tasks have different priorities.

### 1. Algorithms & Data Structures (C++): DeleteFront() and DeleteRear() from DEQueue

Sure, I can provide you with C++ implementations for `DeleteFront()` and `DeleteRear()` operations for a double-ended queue (Deque). A deque is a data structure that allows insertion and deletion of elements from both the front and the rear.

Here's a simple implementation:

```cpp
#include <iostream>
using namespace std;

#define MAX_SIZE 100

class Deque {
private:
    int arr[MAX_SIZE];
    int front, rear;
public:
    Deque() {
        front = rear = -1;
    }

    bool isEmpty() {
        return (front == -1 && rear == -1);
    }

    bool isFull() {
        return (front == 0 && rear == MAX_SIZE - 1) || (rear == (front - 1) % (MAX_SIZE - 1));
    }

    void insertFront(int key) {
        if (isFull()) {
            cout << "Deque is full. Cannot insert element.\n";
            return;
        }
        if (isEmpty()) {
            front = rear = 0;
        } else if (front == 0) {
            front = MAX_SIZE - 1;
        } else {
            front = (front - 1) % (MAX_SIZE - 1);
        }
        arr[front] = key;
        cout << "Inserted " << key << " at the front.\n";
    }

    void insertRear(int key) {
        if (isFull()) {
            cout << "Deque is full. Cannot insert element.\n";
            return;
        }
        if (isEmpty()) {
            front = rear = 0;
        } else if (rear == MAX_SIZE - 1) {
            rear = 0;
        } else {
            rear = (rear + 1) % (MAX_SIZE - 1);
        }
        arr[rear] = key;
        cout << "Inserted " << key << " at the rear.\n";
    }

    void deleteFront() {
        if (isEmpty()) {
            cout << "Deque is empty. Cannot delete.\n";
            return;
        }
        if (front == rear) {
            cout << "Deleted " << arr[front] << " from the front.\n";
            front = rear = -1;
        } else {
            cout << "Deleted " << arr[front] << " from the front.\n";
            front = (front + 1) % (MAX_SIZE - 1);
        }
    }

    void deleteRear() {
        if (isEmpty()) {
            cout << "Deque is empty. Cannot delete.\n";
            return;
        }
        if (front == rear) {
            cout << "Deleted " << arr[rear] << " from the rear.\n";
            front = rear = -1;
        } else if (rear == 0) {
            cout << "Deleted " << arr[rear] << " from the rear.\n";
            rear = MAX_SIZE - 1;
        } else {
            cout << "Deleted " << arr[rear] << " from the rear.\n";
            rear = (rear - 1) % (MAX_SIZE - 1);
        }
    }

    void display() {
        if (isEmpty()) {
            cout << "Deque is empty.\n";
            return;
        }
        cout << "Deque elements: ";
        int i = front;
        while (i != rear) {
            cout << arr[i] << " ";
            i = (i + 1) % (MAX_SIZE - 1);
        }
        cout << arr[rear] << endl;
    }
};

int main() {
    Deque dq;
    dq.insertFront(5);
    dq.insertRear(10);
    dq.insertFront(3);
    dq.display();
    dq.deleteFront();
    dq.display();
    dq.deleteRear();
    dq.display();
    return 0;
}
```

In this implementation:

* `deleteFront()`: Deletes an element from the front of the deque.
* `deleteRear()`: Deletes an element from the rear of the deque.

Both of these operations handle the cases when the deque is empty or full. They also handle the scenarios where after deletion, the deque becomes empty or only one element is left.

### 1. Algorithms & Data Structures (C++): Deque

A deque, short for double-ended queue, is a data structure that allows insertion and deletion of elements from both the front and the back. In C++, you can use the `std::deque` container provided by the Standard Template Library (STL) to implement a deque efficiently. Here's a basic overview of how to use `std::deque` in C++:

#### Including the Necessary Header File

```cpp
#include <deque>
```

#### Declaring a deque

```cpp
std::deque<int> myDeque; // Declaration of a deque of integers
```

#### Inserting Elements

You can insert elements at either end of the deque using `push_front()` and `push_back()` functions:

```cpp
myDeque.push_front(10); // Inserts 10 at the front
myDeque.push_back(20);  // Inserts 20 at the back
```

#### Accessing Elements

You can access elements using array-like indexing or iterators:

```cpp
int frontElement = myDeque.front(); // Retrieves the element at the front
int backElement = myDeque.back();   // Retrieves the element at the back
```

#### Removing Elements

You can remove elements from either end using `pop_front()` and `pop_back()` functions:

```cpp
myDeque.pop_front(); // Removes the element from the front
myDeque.pop_back();  // Removes the element from the back
```

#### Size and Empty Check

You can get the size of the deque and check if it's empty using `size()` and `empty()` functions:

```cpp
size_t dequeSize = myDeque.size(); // Returns the number of elements in the deque
bool isEmpty = myDeque.empty();    // Returns true if the deque is empty, false otherwise
```

#### Iterating Over Elements

You can use iterators to traverse through the deque:

```cpp
for (auto it = myDeque.begin(); it != myDeque.end(); ++it) {
    // Access element using *it
    std::cout << *it << " ";
}
```

#### Clearing the Deque

You can clear all elements from the deque using `clear()`:

```cpp
myDeque.clear(); // Removes all elements from the deque
```

Deques are versatile data structures, offering constant time insertion and deletion at both ends, making them suitable for various applications where elements need to be added or removed from the front and the back frequently.

### 1. Algorithms & Data Structures (C++): Deque STL

Sure! In C++, `std::deque` (pronounced "deck") stands for "double-ended queue". It's a sequence container that allows fast insertion and deletion at both its beginning and its end. Here's how you can use it:

#### Including the necessary header file

```cpp
#include <deque>
```

#### Declaring a deque

```cpp
std::deque<int> myDeque; // Creates an empty deque of integers
```

#### Operations on deque

1. **Insertion and Removal**:
    * `push_back(value)`: Adds an element to the end of the deque.
    * `push_front(value)`: Adds an element to the beginning of the deque.
    * `pop_back()`: Removes the last element from the deque.
    * `pop_front()`: Removes the first element from the deque.

    ```cpp
    myDeque.push_back(10);
    myDeque.push_front(20);
    myDeque.pop_back();
    myDeque.pop_front();
    ```

2. **Accessing Elements**:
    * `front()`: Accesses the first element.
    * `back()`: Accesses the last element.

    ```cpp
    int firstElement = myDeque.front();
    int lastElement = myDeque.back();
    ```

3. **Size and Capacity**:
    * `size()`: Returns the number of elements in the deque.
    * `empty()`: Checks whether the deque is empty or not.

    ```cpp
    int size = myDeque.size();
    bool isEmpty = myDeque.empty();
    ```

4. **Iterating through the deque**:
    You can use iterators to traverse the deque. Here's an example of iterating through a deque:

    ```cpp
    for (auto it = myDeque.begin(); it != myDeque.end(); ++it) {
        // Do something with *it
    }
    ```

#### Advantages of `std::deque`

* **Fast insertion and removal**: Unlike vectors, deques have efficient insertion and deletion at both ends.
* **Dynamic resizing**: Deques grow and shrink dynamically to accommodate elements efficiently.

#### When to use `std::deque`

* When you need fast insertion and deletion at both ends of the sequence.
* When you need dynamic resizing and don't want to pay the cost of reallocation like in vectors.

#### Example

```cpp
#include <iostream>
#include <deque>

int main() {
    std::deque<int> myDeque;

    // Inserting elements
    myDeque.push_back(10);
    myDeque.push_front(20);

    // Accessing elements
    std::cout << "First element: " << myDeque.front() << std::endl;
    std::cout << "Last element: " << myDeque.back() << std::endl;

    // Removing elements
    myDeque.pop_back();
    myDeque.pop_front();

    // Checking size
    std::cout << "Size: " << myDeque.size() << std::endl;

    return 0;
}
```

That's a basic rundown of using `std::deque` in C++! Let me know if you have any specific questions or need further clarification.

### 1. Algorithms & Data Structures (C++): DEQueue ( Double-Ended-Queue )

A double-ended queue, often abbreviated as deque (pronounced "deck"), is a data structure that supports insertion and deletion at both the front and the back of the queue. Implementing a deque in C++ involves various methods to manipulate its contents efficiently. Below is a simple implementation of a deque in C++ using arrays:

```cpp
#include <iostream>

template <typename T>
class Deque {
private:
    T* arr;
    int capacity;
    int front;
    int rear;
    int size;

public:
    Deque(int capacity) : capacity(capacity), front(0), rear(-1), size(0) {
        arr = new T[capacity];
    }

    ~Deque() {
        delete[] arr;
    }

    bool isEmpty() {
        return size == 0;
    }

    bool isFull() {
        return size == capacity;
    }

    void insertFront(T element) {
        if (isFull()) {
            std::cout << "Deque is full. Cannot insert.\n";
            return;
        }
        front = (front - 1 + capacity) % capacity;
        arr[front] = element;
        size++;
    }

    void insertRear(T element) {
        if (isFull()) {
            std::cout << "Deque is full. Cannot insert.\n";
            return;
        }
        rear = (rear + 1) % capacity;
        arr[rear] = element;
        size++;
    }

    T deleteFront() {
        if (isEmpty()) {
            std::cout << "Deque is empty. Cannot delete.\n";
            return T();
        }
        T deleted = arr[front];
        front = (front + 1) % capacity;
        size--;
        return deleted;
    }

    T deleteRear() {
        if (isEmpty()) {
            std::cout << "Deque is empty. Cannot delete.\n";
            return T();
        }
        T deleted = arr[rear];
        rear = (rear - 1 + capacity) % capacity;
        size--;
        return deleted;
    }

    T getFront() {
        if (isEmpty()) {
            std::cout << "Deque is empty. No front element.\n";
            return T();
        }
        return arr[front];
    }

    T getRear() {
        if (isEmpty()) {
            std::cout << "Deque is empty. No rear element.\n";
            return T();
        }
        return arr[rear];
    }
};

int main() {
    Deque<int> deque(5);

    deque.insertFront(10);
    deque.insertRear(20);
    deque.insertFront(30);
    deque.insertRear(40);

    std::cout << "Front element: " << deque.getFront() << std::endl;
    std::cout << "Rear element: " << deque.getRear() << std::endl;

    deque.deleteFront();
    deque.deleteRear();

    std::cout << "Front element after deletion: " << deque.getFront() << std::endl;
    std::cout << "Rear element after deletion: " << deque.getRear() << std::endl;

    return 0;
}
```

This code defines a `Deque` class with methods to insert and delete elements from both ends of the deque. It uses circular arrays to efficiently utilize memory. The main function demonstrates the usage of the deque by inserting elements at both ends, retrieving front and rear elements, and deleting elements from both ends.

### 1. Algorithms & Data Structures (C++): DEQueue (Double-Ended-Queue)

A Double-Ended Queue (DEQueue) is a data structure that allows insertion and deletion of elements from both the front and the rear ends. In C++, you can implement a DEQueue using various approaches, such as using doubly linked lists or arrays. Here's a simple implementation using a doubly linked list:

```cpp
#include <iostream>

// Node structure for the doubly linked list
template <typename T>
struct Node {
    T data;
    Node* prev;
    Node* next;
    
    Node(const T& d) : data(d), prev(nullptr), next(nullptr) {}
};

// DEQueue class
template <typename T>
class DEQueue {
private:
    Node<T>* front;
    Node<T>* rear;
    int size;

public:
    DEQueue() : front(nullptr), rear(nullptr), size(0) {}

    // Function to check if the DEQueue is empty
    bool isEmpty() const {
        return size == 0;
    }

    // Function to get the size of the DEQueue
    int getSize() const {
        return size;
    }

    // Function to insert an element at the front of the DEQueue
    void insertFront(const T& value) {
        Node<T>* newNode = new Node<T>(value);
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            newNode->next = front;
            front->prev = newNode;
            front = newNode;
        }
        size++;
    }

    // Function to insert an element at the rear of the DEQueue
    void insertRear(const T& value) {
        Node<T>* newNode = new Node<T>(value);
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            rear->next = newNode;
            newNode->prev = rear;
            rear = newNode;
        }
        size++;
    }

    // Function to remove an element from the front of the DEQueue
    T removeFront() {
        if (isEmpty()) {
            std::cerr << "DEQueue is empty. Cannot remove from front.\n";
            exit(EXIT_FAILURE);
        }
        T value = front->data;
        Node<T>* temp = front;
        if (front == rear) {
            front = rear = nullptr;
        } else {
            front = front->next;
            front->prev = nullptr;
        }
        delete temp;
        size--;
        return value;
    }

    // Function to remove an element from the rear of the DEQueue
    T removeRear() {
        if (isEmpty()) {
            std::cerr << "DEQueue is empty. Cannot remove from rear.\n";
            exit(EXIT_FAILURE);
        }
        T value = rear->data;
        Node<T>* temp = rear;
        if (front == rear) {
            front = rear = nullptr;
        } else {
            rear = rear->prev;
            rear->next = nullptr;
        }
        delete temp;
        size--;
        return value;
    }

    // Function to display the elements of the DEQueue
    void display() const {
        if (isEmpty()) {
            std::cout << "DEQueue is empty.\n";
            return;
        }
        Node<T>* current = front;
        while (current != nullptr) {
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }

    // Destructor to free memory
    ~DEQueue() {
        while (!isEmpty()) {
            removeFront();
        }
    }
};

int main() {
    DEQueue<int> dq;
    
    dq.insertFront(10);
    dq.insertFront(20);
    dq.insertRear(30);
    dq.insertRear(40);
    
    std::cout << "DEQueue elements: ";
    dq.display();
    
    std::cout << "Removed from front: " << dq.removeFront() << std::endl;
    std::cout << "Removed from rear: " << dq.removeRear() << std::endl;
    
    std::cout << "DEQueue elements after removal: ";
    dq.display();
    
    return 0;
}
```

This code provides a basic implementation of a DEQueue using a doubly linked list in C++. You can perform operations like insertion at both ends (`insertFront()` and `insertRear()`), removal from both ends (`removeFront()` and `removeRear()`), check if the DEQueue is empty (`isEmpty()`), get the size of the DEQueue (`getSize()`), and display the elements (`display()`).

### 1. Algorithms & Data Structures (C++): Dequeue in Linked List

Certainly! A deque, short for "double-ended queue," is a data structure that allows insertion and deletion of elements from both the front and the back. Implementing a deque using a linked list involves creating a node structure and managing pointers to maintain the connections between nodes.

Here's a basic implementation of a deque using a doubly linked list in C++:

```cpp
#include <iostream>

template <typename T>
class Node {
public:
    T data;
    Node<T>* next;
    Node<T>* prev;

    Node(const T& newData) : data(newData), next(nullptr), prev(nullptr) {}
};

template <typename T>
class Deque {
private:
    Node<T>* front;
    Node<T>* rear;
    int size;

public:
    Deque() : front(nullptr), rear(nullptr), size(0) {}

    ~Deque() {
        clear();
    }

    void push_front(const T& value) {
        Node<T>* newNode = new Node<T>(value);
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            newNode->next = front;
            front->prev = newNode;
            front = newNode;
        }
        size++;
    }

    void push_back(const T& value) {
        Node<T>* newNode = new Node<T>(value);
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            rear->next = newNode;
            newNode->prev = rear;
            rear = newNode;
        }
        size++;
    }

    void pop_front() {
        if (!isEmpty()) {
            Node<T>* temp = front;
            front = front->next;
            if (front)
                front->prev = nullptr;
            delete temp;
            size--;
            if (isEmpty())
                rear = nullptr;
        }
    }

    void pop_back() {
        if (!isEmpty()) {
            Node<T>* temp = rear;
            rear = rear->prev;
            if (rear)
                rear->next = nullptr;
            delete temp;
            size--;
            if (isEmpty())
                front = nullptr;
        }
    }

    T& front_element() {
        if (!isEmpty())
            return front->data;
        else
            throw std::out_of_range("Deque is empty");
    }

    T& back_element() {
        if (!isEmpty())
            return rear->data;
        else
            throw std::out_of_range("Deque is empty");
    }

    bool isEmpty() {
        return size == 0;
    }

    int getSize() {
        return size;
    }

    void clear() {
        while (!isEmpty())
            pop_front();
    }
};

int main() {
    Deque<int> deque;

    deque.push_front(1);
    deque.push_front(2);
    deque.push_back(3);
    deque.push_back(4);

    std::cout << "Front element: " << deque.front_element() << std::endl;
    std::cout << "Back element: " << deque.back_element() << std::endl;

    deque.pop_front();
    deque.pop_back();

    std::cout << "Front element after pop_front: " << deque.front_element() << std::endl;
    std::cout << "Back element after pop_back: " << deque.back_element() << std::endl;

    return 0;
}
```

This code defines a deque using a doubly linked list. It provides methods to push and pop elements from both the front and the back of the deque, as well as methods to access the front and back elements. Finally, there's a simple demonstration of how to use the deque in the `main` function.

### 1. Algorithms & Data Structures (C++): DeQueue() in Circular Queue

In C++, implementing a `DeQueue()` operation (also known as `pop_front()` in some implementations) in a circular queue involves removing an element from the front of the queue. A circular queue has the property that when an element is dequeued from the front, the next element becomes the new front element, considering the circular nature of the underlying array.

Here's a basic implementation of a circular queue in C++ with a `DeQueue()` operation:

```cpp
#include <iostream>
using namespace std;

const int MAX_SIZE = 100;

class CircularQueue {
private:
    int front, rear, size;
    int arr[MAX_SIZE];

public:
    CircularQueue() {
        front = rear = -1;
        size = 0;
    }

    bool isEmpty() {
        return size == 0;
    }

    bool isFull() {
        return size == MAX_SIZE;
    }

    void enQueue(int value) {
        if (isFull()) {
            cout << "Queue is full. Cannot enqueue." << endl;
            return;
        }

        if (isEmpty()) {
            front = rear = 0;
        } else {
            rear = (rear + 1) % MAX_SIZE;
        }
        arr[rear] = value;
        size++;
    }

    void deQueue() {
        if (isEmpty()) {
            cout << "Queue is empty. Cannot dequeue." << endl;
            return;
        }

        if (front == rear) {
            // Reset front and rear as the queue becomes empty after dequeue
            front = rear = -1;
        } else {
            front = (front + 1) % MAX_SIZE;
        }
        size--;
    }

    void display() {
        if (isEmpty()) {
            cout << "Queue is empty." << endl;
            return;
        }

        int i = front;
        while (i != rear) {
            cout << arr[i] << " ";
            i = (i + 1) % MAX_SIZE;
        }
        cout << arr[rear] << endl;
    }
};

int main() {
    CircularQueue queue;

    queue.enQueue(10);
    queue.enQueue(20);
    queue.enQueue(30);

    cout << "Queue elements: ";
    queue.display();

    queue.deQueue();

    cout << "Queue elements after dequeue: ";
    queue.display();

    return 0;
}
```

In this implementation, `front` and `rear` indices are maintained to represent the front and rear of the queue respectively. When an element is dequeued, `front` is moved one step forward, considering the circular nature of the queue. If `front` becomes equal to `rear`, it means the queue is empty, and both indices are reset accordingly.

### 1. Algorithms & Data Structures (C++): Double Ended Queue

A Double Ended Queue (Deque) is a data structure that allows insertion and deletion of elements from both the front and the back. It's like a combination of a stack and a queue. In C++, you can implement a deque using the `std::deque` container provided by the Standard Template Library (STL). Here's a basic example:

```cpp
#include <iostream>
#include <deque>

int main() {
    // Declare a deque
    std::deque<int> myDeque;

    // Insert elements at the back
    myDeque.push_back(10);
    myDeque.push_back(20);
    myDeque.push_back(30);

    // Insert elements at the front
    myDeque.push_front(5);
    myDeque.push_front(2);

    // Print elements
    std::cout << "Deque elements: ";
    for (int num : myDeque) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    // Remove elements from the back
    myDeque.pop_back();
    myDeque.pop_back();

    // Remove elements from the front
    myDeque.pop_front();

    // Print elements after removal
    std::cout << "Deque elements after removal: ";
    for (int num : myDeque) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

This code demonstrates basic operations on a deque, such as insertion at both ends (`push_back` and `push_front`), removal from both ends (`pop_back` and `pop_front`), and iteration over the elements.

Deques offer constant time insertion and deletion at both ends, making them a versatile data structure for many scenarios.

### 1. Algorithms & Data Structures (C++): Double Ended Queue DEQUEUE

A double-ended queue (deque) is a data structure that allows insertion and deletion of elements from both the front and the back. In C++, you can implement a deque using the `std::deque` container provided by the Standard Template Library (STL). Here's a basic overview of how you can use `std::deque`:

```cpp
#include <iostream>
#include <deque>

int main() {
    // Declaration of deque
    std::deque<int> myDeque;

    // Insert elements at the back
    myDeque.push_back(10);
    myDeque.push_back(20);
    myDeque.push_back(30);

    // Insert elements at the front
    myDeque.push_front(5);
    myDeque.push_front(2);

    // Access elements
    std::cout << "Elements in deque: ";
    for (int elem : myDeque) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    // Remove elements from the front
    myDeque.pop_front();
    myDeque.pop_front();

    // Remove elements from the back
    myDeque.pop_back();

    // Access updated elements
    std::cout << "Updated deque: ";
    for (int elem : myDeque) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

This code demonstrates basic operations on a deque, such as insertion at both ends (`push_back` and `push_front`), removal from both ends (`pop_back` and `pop_front`), and traversal of elements using a range-based for loop.

Remember, `std::deque` provides constant time insertion and deletion at both the beginning and the end of the deque. However, accessing elements at arbitrary positions within the deque is less efficient compared to vectors (`std::vector`), as deque does not provide contiguous storage.

### 1. Algorithms & Data Structures (C++): Double Ended Queue using doubly linked list

Creating a double-ended queue (deque) using a doubly linked list in C++ involves implementing the necessary functionalities such as insertion and deletion from both ends of the deque. Here's a simple implementation:

```cpp
#include <iostream>

template <typename T>
class Node {
public:
    T data;
    Node<T>* next;
    Node<T>* prev;

    Node(T val) : data(val), next(nullptr), prev(nullptr) {}
};

template <typename T>
class Deque {
private:
    Node<T>* front;
    Node<T>* rear;

public:
    Deque() : front(nullptr), rear(nullptr) {}

    bool isEmpty() {
        return front == nullptr;
    }

    void insertFront(T val) {
        Node<T>* newNode = new Node<T>(val);
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            newNode->next = front;
            front->prev = newNode;
            front = newNode;
        }
    }

    void insertRear(T val) {
        Node<T>* newNode = new Node<T>(val);
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            rear->next = newNode;
            newNode->prev = rear;
            rear = newNode;
        }
    }

    T deleteFront() {
        if (isEmpty()) {
            std::cerr << "Deque is empty!" << std::endl;
            exit(1);
        }

        T deletedData = front->data;
        Node<T>* temp = front;
        if (front == rear) {
            front = rear = nullptr;
        } else {
            front = front->next;
            front->prev = nullptr;
        }
        delete temp;
        return deletedData;
    }

    T deleteRear() {
        if (isEmpty()) {
            std::cerr << "Deque is empty!" << std::endl;
            exit(1);
        }

        T deletedData = rear->data;
        Node<T>* temp = rear;
        if (front == rear) {
            front = rear = nullptr;
        } else {
            rear = rear->prev;
            rear->next = nullptr;
        }
        delete temp;
        return deletedData;
    }

    void display() {
        if (isEmpty()) {
            std::cout << "Deque is empty!" << std::endl;
            return;
        }

        Node<T>* current = front;
        while (current != nullptr) {
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }
};

int main() {
    Deque<int> deque;
    
    deque.insertFront(10);
    deque.insertRear(20);
    deque.insertFront(5);
    deque.insertRear(30);
    
    deque.display(); // Output: 5 10 20 30
    
    std::cout << "Deleted front element: " << deque.deleteFront() << std::endl;
    std::cout << "Deleted rear element: " << deque.deleteRear() << std::endl;
    
    deque.display(); // Output: 10 20
    
    return 0;
}
```

This code defines a `Deque` class using a doubly linked list. It provides methods to insert elements at both the front and rear, delete elements from both ends, and display the contents of the deque.

### 1. Algorithms & Data Structures (C++): Double Ended Queues using Arrays

Certainly! A double-ended queue (deque) implemented using arrays in C++ allows for efficient insertion and deletion operations at both ends of the deque. Here's a basic implementation:

```cpp
#include <iostream>
using namespace std;

#define MAX_SIZE 100

class Deque {
private:
    int arr[MAX_SIZE];
    int front, rear;
public:
    Deque() {
        front = -1;
        rear = -1;
    }

    bool isEmpty() {
        return (front == -1 && rear == -1);
    }

    bool isFull() {
        return (rear + 1) % MAX_SIZE == front;
    }

    void insertFront(int x) {
        if (isFull()) {
            cout << "Deque is full. Overflow!" << endl;
            return;
        }
        if (isEmpty()) {
            front = rear = 0;
        } else {
            front = (front - 1 + MAX_SIZE) % MAX_SIZE;
        }
        arr[front] = x;
    }

    void insertRear(int x) {
        if (isFull()) {
            cout << "Deque is full. Overflow!" << endl;
            return;
        }
        if (isEmpty()) {
            front = rear = 0;
        } else {
            rear = (rear + 1) % MAX_SIZE;
        }
        arr[rear] = x;
    }

    void deleteFront() {
        if (isEmpty()) {
            cout << "Deque is empty. Underflow!" << endl;
            return;
        }
        if (front == rear) {
            front = rear = -1;
        } else {
            front = (front + 1) % MAX_SIZE;
        }
    }

    void deleteRear() {
        if (isEmpty()) {
            cout << "Deque is empty. Underflow!" << endl;
            return;
        }
        if (front == rear) {
            front = rear = -1;
        } else {
            rear = (rear - 1 + MAX_SIZE) % MAX_SIZE;
        }
    }

    int getFront() {
        if (isEmpty()) {
            cout << "Deque is empty." << endl;
            return -1;
        }
        return arr[front];
    }

    int getRear() {
        if (isEmpty()) {
            cout << "Deque is empty." << endl;
            return -1;
        }
        return arr[rear];
    }
};

int main() {
    Deque dq;
    dq.insertFront(5);
    dq.insertRear(10);
    dq.insertFront(3);
    dq.insertRear(15);
    cout << "Front element: " << dq.getFront() << endl;
    cout << "Rear element: " << dq.getRear() << endl;
    dq.deleteFront();
    dq.deleteRear();
    cout << "Front element after deletion: " << dq.getFront() << endl;
    cout << "Rear element after deletion: " << dq.getRear() << endl;
    return 0;
}
```

This implementation maintains a circular array to efficiently utilize the available space. The `insertFront`, `insertRear`, `deleteFront`, and `deleteRear` operations have a time complexity of O(1) on average. However, be aware that this implementation has a fixed maximum size (`MAX_SIZE`), and it doesn't dynamically resize itself.

### 1. Algorithms & Data Structures (C++): Double Ended Queues using Linked List

Sure, implementing a Double Ended Queue (Deque) using a linked list in C++ involves creating a structure for the nodes of the linked list and then implementing the necessary methods to manipulate the deque. Here's a basic implementation:

```cpp
#include <iostream>

using namespace std;

// Node structure for the linked list
struct Node {
    int data;
    Node* next;
    Node* prev;
    
    Node(int value) : data(value), next(nullptr), prev(nullptr) {}
};

class Deque {
private:
    Node* front;
    Node* rear;
    int size;
    
public:
    Deque() : front(nullptr), rear(nullptr), size(0) {}

    bool isEmpty() {
        return size == 0;
    }

    // Insert at the front of the deque
    void insertFront(int value) {
        Node* newNode = new Node(value);
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            newNode->next = front;
            front->prev = newNode;
            front = newNode;
        }
        size++;
    }

    // Insert at the rear of the deque
    void insertRear(int value) {
        Node* newNode = new Node(value);
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            rear->next = newNode;
            newNode->prev = rear;
            rear = newNode;
        }
        size++;
    }

    // Delete from the front of the deque
    void deleteFront() {
        if (isEmpty()) {
            cout << "Deque is empty." << endl;
            return;
        }
        Node* temp = front;
        if (front == rear) {
            front = rear = nullptr;
        } else {
            front = front->next;
            front->prev = nullptr;
        }
        delete temp;
        size--;
    }

    // Delete from the rear of the deque
    void deleteRear() {
        if (isEmpty()) {
            cout << "Deque is empty." << endl;
            return;
        }
        Node* temp = rear;
        if (front == rear) {
            front = rear = nullptr;
        } else {
            rear = rear->prev;
            rear->next = nullptr;
        }
        delete temp;
        size--;
    }

    // Display the elements of the deque
    void display() {
        if (isEmpty()) {
            cout << "Deque is empty." << endl;
            return;
        }
        Node* current = front;
        while (current != nullptr) {
            cout << current->data << " ";
            current = current->next;
        }
        cout << endl;
    }
};

int main() {
    Deque deque;
    deque.insertFront(5);
    deque.insertFront(10);
    deque.insertRear(15);
    deque.display(); // Output: 10 5 15
    deque.deleteFront();
    deque.display(); // Output: 5 15
    deque.deleteRear();
    deque.display(); // Output: 5
    return 0;
}
```

This implementation provides basic functionalities like inserting and deleting elements from both the front and rear ends of the deque, as well as checking if the deque is empty and displaying its contents.

### 1. Algorithms & Data Structures (C++): DQUERY SPOJ using Mo's Algorithm

Solving the DQUERY problem on SPOJ using Mo's Algorithm can be an interesting challenge. Mo's Algorithm is an offline algorithm used to process range queries offline, meaning that it's suitable when you have all the queries in advance and can process them in any order.

Here's a general outline of how you can implement Mo's Algorithm to solve the DQUERY problem:

1. **Input**: Read the input, which consists of an array of N integers and M queries. Each query is represented by two integers L and R, denoting the range for which you need to find distinct elements.

2. **Preprocessing**: Sort the queries based on the block to which they belong. Each query's block is determined by the value L / block_size, where block_size is some appropriate value. Additionally, sort the array elements if they are not already sorted.

3. **Initialize**: Initialize data structures and variables needed for processing queries.

4. **Mo's Algorithm Processing**: Iterate through each query. For each query, move the left and right pointers to accommodate the current query. As you move from one query to the next, update your data structures to reflect the changes in the range.

5. **Output**: For each query, output the number of distinct elements in the range.

Here's a sample implementation in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <cmath>
#include <unordered_map>

using namespace std;

#define MAXN 30005
#define MAXQ 200005
#define BLOCK_SIZE 175 // Experiment with block size

struct Query {
    int id, l, r;
};

int freq[MAXN]; // frequency array to count occurrences of elements
int ans[MAXQ]; // to store the answer of each query
int arr[MAXN]; // input array
Query queries[MAXQ];

bool compare(Query a, Query b) {
    // Comparator function to sort queries based on the block
    if (a.l / BLOCK_SIZE != b.l / BLOCK_SIZE)
        return a.l / BLOCK_SIZE < b.l / BLOCK_SIZE;
    return a.r < b.r;
}

void add(int idx, int& cnt) {
    // Update data structures when including a new element at idx
    if (freq[arr[idx]] == 0)
        cnt++;
    freq[arr[idx]]++;
}

void remove(int idx, int& cnt) {
    // Update data structures when excluding an element at idx
    freq[arr[idx]]--;
    if (freq[arr[idx]] == 0)
        cnt--;
}

void processQueries(int n, int m) {
    sort(queries, queries + m, compare);
    
    int currL = 0, currR = -1;
    int distinctCount = 0;

    for (int i = 0; i < m; i++) {
        int L = queries[i].l;
        int R = queries[i].r;

        while (currL > L) {
            currL--;
            add(currL, distinctCount);
        }
        while (currR < R) {
            currR++;
            add(currR, distinctCount);
        }
        while (currL < L) {
            remove(currL, distinctCount);
            currL++;
        }
        while (currR > R) {
            remove(currR, distinctCount);
            currR--;
        }

        ans[queries[i].id] = distinctCount;
    }
}

int main() {
    int n, m;
    cin >> n;

    for (int i = 0; i < n; i++)
        cin >> arr[i];

    cin >> m;

    for (int i = 0; i < m; i++) {
        cin >> queries[i].l >> queries[i].r;
        queries[i].id = i;
    }

    processQueries(n, m);

    for (int i = 0; i < m; i++)
        cout << ans[i] << endl;

    return 0;
}
```

This code assumes that the maximum array size is 30005 and the maximum number of queries is 200005. Adjust these constants according to the constraints given in the problem statement. Additionally, you may need to modify the BLOCK_SIZE constant based on experimentation for optimal performance.

Remember to thoroughly test your implementation with various test cases to ensure correctness and efficiency.

### 1. Algorithms & Data Structures (C++): DQUERY using Fenwick Tree

Sure, let's discuss how to solve the "DQUERY" problem using Fenwick Tree (also known as Binary Indexed Tree or BIT) in C++.

The "DQUERY" problem is a classic problem on online judges like SPOJ. Here's a brief overview of the problem:

You are given an array of \( N \) integers. You have to answer \( Q \) queries. Each query is defined by two integers \( l \) and \( r \), and you need to find the number of distinct elements in the subarray \( A[l, r] \).

Here's how you can solve this problem efficiently using a Fenwick Tree:

1. Create a Fenwick Tree of size \( N \) to store the frequencies of elements in the array.
2. Initialize another array to keep track of the last occurrence of each element.
3. Process each query:
   * For each query \( l, r \), iterate from \( l \) to \( r \) and update the Fenwick Tree and the last occurrence array.
   * Count the distinct elements by subtracting the cumulative frequency at the last occurrence of each element before \( l \) from the cumulative frequency at \( r \).

Here's a sample implementation in C++:

```cpp
#include <iostream>
#include <vector>
#include <map>
using namespace std;

// Fenwick Tree class
class FenwickTree {
private:
    vector<int> tree;
public:
    FenwickTree(int size) : tree(size + 1, 0) {}

    void update(int index, int val) {
        for (; index < tree.size(); index += index & -index)
            tree[index] += val;
    }

    int query(int index) {
        int sum = 0;
        for (; index > 0; index -= index & -index)
            sum += tree[index];
        return sum;
    }
};

int main() {
    int n;
    cin >> n;

    vector<int> a(n + 1); // 1-indexed array
    map<int, int> last_occurrence;

    for (int i = 1; i <= n; ++i) {
        cin >> a[i];
        last_occurrence[a[i]] = 0; // Initialize last occurrence for each element
    }

    int q;
    cin >> q;

    vector<pair<int, pair<int, int>>> queries(q); // (index, (l, r))
    vector<int> result(q);

    for (int i = 0; i < q; ++i) {
        cin >> queries[i].second.first >> queries[i].second.second;
        queries[i].first = i;
    }

    sort(queries.begin(), queries.end());

    FenwickTree fenwick(n);
    int curr_index = 1;

    for (int i = 0; i < q; ++i) {
        auto [index, lr] = queries[i];
        int l = lr.first, r = lr.second;

        while (curr_index <= r) {
            if (last_occurrence[a[curr_index]] != 0) {
                fenwick.update(last_occurrence[a[curr_index]], -1);
            }
            last_occurrence[a[curr_index]] = curr_index;
            fenwick.update(curr_index, 1);
            curr_index++;
        }

        result[index] = fenwick.query(r) - fenwick.query(l - 1);
    }

    for (int i = 0; i < q; ++i) {
        cout << result[i] << endl;
    }

    return 0;
}
```

This code first reads the input array, then processes the queries one by one using Fenwick Tree to efficiently compute the number of distinct elements in each subarray. Finally, it prints the results of all queries.

Hope this helps! Let me know if you have further questions!

### 1. Algorithms & Data Structures (C++): Drawback of Queue using Array

One drawback of implementing a queue using an array in C++ is the fixed size limitation. When you allocate an array for the queue, you have to specify its maximum size. This fixed size can lead to inefficiencies or errors in certain situations:

1. **Fixed Capacity**: Arrays have a fixed capacity, meaning you must allocate a certain amount of memory upfront. If the queue reaches its maximum capacity and you try to enqueue more elements, you'll encounter overflow, which can lead to data loss or program termination.

2. **Memory Waste**: If you allocate a large array to accommodate potential future growth of the queue, but the queue rarely reaches that size, you're wasting memory. This is inefficient, especially if memory is limited or expensive.

3. **Dynamic Behavior**: Queues often need to grow and shrink dynamically based on the number of elements they contain. With an array-based implementation, resizing the array dynamically (e.g., using `realloc` in C++) can be complex and inefficient.

4. **Fragmentation**: If you frequently enqueue and dequeue elements from the queue, the array might become fragmented over time, with unused spaces scattered throughout the array. This fragmentation can lead to wasted memory and reduced performance.

To overcome these limitations, you might consider using dynamic memory allocation (e.g., linked list-based implementation) or a circular buffer approach, which allows the queue to wrap around to the beginning of the array when it reaches the end, effectively reusing space. Each approach has its own trade-offs in terms of time complexity, memory usage, and ease of implementation.

### 1. Algorithms & Data Structures (C++): Drawbacks of Implementing a Queue using Normal Array

Implementing a queue using a normal array in C++ has some drawbacks, primarily related to efficiency and flexibility:

1. **Fixed Size**: Arrays have a fixed size, meaning you have to preallocate memory for a certain number of elements. If the queue reaches its maximum capacity, adding more elements becomes problematic. You'd need to resize the array, which involves allocating a new array, copying elements, and deallocating the old array, resulting in a time-consuming operation.

2. **Dynamic Memory Management Overhead**: Resizing the array dynamically involves dynamic memory management, which can lead to fragmentation and overhead. It can also introduce issues like memory leaks or dangling pointers if not managed properly.

3. **Inefficient Dequeue Operation**: Removing an element from the front of the queue (dequeuing) requires shifting all the other elements to the front, which has a time complexity of O(n), where n is the number of elements in the queue. This operation can be inefficient, especially for large queues.

4. **Wasted Space**: If you preallocate a large array to accommodate potential growth, but the queue remains small, you'll waste memory.

5. **Insertion Overhead**: While inserting an element at the end of the queue (enqueueing) is efficient (O(1)), if the array needs resizing, it can lead to occasional performance overhead.

6. **Cache Inefficiency**: Arrays are contiguous blocks of memory, so if the array size is large and the queue only occupies a small portion of it, cache efficiency decreases because of potential cache misses.

7. **Not Suitable for Real-time Systems**: In real-time systems where predictable performance is crucial, the dynamic resizing of arrays can introduce unpredictable delays, making them unsuitable.

To overcome these drawbacks, you might consider using other data structures like linked lists or dynamic arrays (vectors in C++) which can dynamically resize without much overhead, or circular buffers which can efficiently manage space and avoid shifting elements.

### 1. Algorithms & Data Structures (C++): Dry run Circular Queue operations using the algorithm

Sure! Let's go through a dry run of Circular Queue operations using C++.

A Circular Queue is a data structure that operates in a similar way to a regular queue, but with a fixed size. When elements are dequeued, the space they occupied becomes available for further enqueuing.

Here's a simple implementation of a Circular Queue in C++:

```cpp
#include <iostream>
using namespace std;

#define SIZE 5

class CircularQueue {
private:
    int items[SIZE], front, rear;

public:
    CircularQueue() {
        front = -1;
        rear = -1;
    }

    // Check if the queue is full
    bool isFull() {
        if ((front == 0 && rear == SIZE - 1) || (front == rear + 1))
            return true;
        return false;
    }

    // Check if the queue is empty
    bool isEmpty() {
        if (front == -1)
            return true;
        return false;
    }

    // Add an element to the queue
    void enqueue(int element) {
        if (isFull()) {
            cout << "Queue is full" << endl;
        } else {
            if (front == -1)
                front = 0;
            rear = (rear + 1) % SIZE;
            items[rear] = element;
            cout << "Inserted " << element << endl;
        }
    }

    // Remove an element from the queue
    int dequeue() {
        int element;
        if (isEmpty()) {
            cout << "Queue is empty" << endl;
            return -1;
        } else {
            element = items[front];
            if (front == rear) {
                front = -1;
                rear = -1;
            } else {
                front = (front + 1) % SIZE;
            }
            return element;
        }
    }

    // Display the queue elements
    void display() {
        int i;
        if (isEmpty()) {
            cout << "Queue is empty" << endl;
        } else {
            cout << "Front -> " << front << endl;
            cout << "Items -> ";
            for (i = front; i != rear; i = (i + 1) % SIZE)
                cout << items[i] << " ";
            cout << items[i];
            cout << endl;
            cout << "Rear -> " << rear << endl;
        }
    }
};

int main() {
    CircularQueue q;

    // Inserting elements into Circular Queue
    q.enqueue(1);
    q.enqueue(2);
    q.enqueue(3);
    q.enqueue(4);
    q.enqueue(5);

    // Displaying elements present in Circular Queue 
    q.display();

    // Deleting elements from Circular Queue
    cout << "Deleted element = " << q.dequeue() << endl;
    cout << "Deleted element = " << q.dequeue() << endl;

    q.display();

    q.enqueue(6);
    q.enqueue(7);

    q.display();

    // Inserting another element will make queue full
    q.enqueue(8);

    return 0;
}
```

Let's run through this code step by step:

1. We start with an empty Circular Queue. `front` and `rear` are initialized to -1 to indicate an empty queue.
2. We enqueue elements 1, 2, 3, 4, and 5 into the queue. Since the queue is not full, we add elements accordingly.
3. We display the elements in the queue. The `front` points to the first element and the `rear` points to the last element.
4. We dequeue two elements. This removes the elements from the queue. We display the updated queue after each dequeue operation.
5. We enqueue elements 6 and 7 into the queue. Since the queue is circular, it wraps around to the beginning when reaching the end.
6. We try to enqueue another element (8), but the queue is full, so we cannot insert it.

This is a basic dry run of Circular Queue operations using C++. Let me know if you need further clarification or assistance!

### 1. Algorithms & Data Structures (C++): Dry run of the DEQ algorithm

The DEQ algorithm, also known as the Double Ended Queue algorithm, is commonly implemented using a doubly linked list. It allows insertion and deletion of elements from both ends of the queue. Let's dry run a simple DEQ algorithm implemented in C++:

```cpp
#include <iostream>

using namespace std;

// Node structure for doubly linked list
struct Node {
    int data;
    Node* next;
    Node* prev;
};

class DEQueue {
private:
    Node* front;
    Node* rear;
public:
    DEQueue() {
        front = nullptr;
        rear = nullptr;
    }

    // Function to check if the queue is empty
    bool isEmpty() {
        return front == nullptr;
    }

    // Function to insert element at the front of the queue
    void insertFront(int data) {
        Node* newNode = new Node();
        newNode->data = data;
        newNode->next = front;
        newNode->prev = nullptr;
        if (isEmpty()) {
            rear = newNode;
        } else {
            front->prev = newNode;
        }
        front = newNode;
    }

    // Function to insert element at the rear of the queue
    void insertRear(int data) {
        Node* newNode = new Node();
        newNode->data = data;
        newNode->next = nullptr;
        newNode->prev = rear;
        if (isEmpty()) {
            front = newNode;
        } else {
            rear->next = newNode;
        }
        rear = newNode;
    }

    // Function to delete element from the front of the queue
    void deleteFront() {
        if (isEmpty()) {
            cout << "Queue is empty\n";
            return;
        }
        Node* temp = front;
        front = front->next;
        if (front != nullptr) {
            front->prev = nullptr;
        } else {
            rear = nullptr;
        }
        delete temp;
    }

    // Function to delete element from the rear of the queue
    void deleteRear() {
        if (isEmpty()) {
            cout << "Queue is empty\n";
            return;
        }
        Node* temp = rear;
        rear = rear->prev;
        if (rear != nullptr) {
            rear->next = nullptr;
        } else {
            front = nullptr;
        }
        delete temp;
    }

    // Function to display the elements of the queue
    void display() {
        if (isEmpty()) {
            cout << "Queue is empty\n";
            return;
        }
        Node* temp = front;
        while (temp != nullptr) {
            cout << temp->data << " ";
            temp = temp->next;
        }
        cout << endl;
    }
};

int main() {
    DEQueue deq;

    // Insert elements at the front
    deq.insertFront(10);
    deq.insertFront(20);
    deq.insertFront(30);

    // Insert elements at the rear
    deq.insertRear(40);
    deq.insertRear(50);
    deq.insertRear(60);

    // Display the queue
    cout << "Queue elements: ";
    deq.display();

    // Delete elements from the front and rear
    deq.deleteFront();
    deq.deleteRear();

    // Display the queue after deletion
    cout << "Queue elements after deletion: ";
    deq.display();

    return 0;
}
```

Now, let's dry run this code step by step:

1. Initially, both the front and rear pointers are set to nullptr, indicating an empty queue.
2. Three elements (30, 20, 10) are inserted at the front of the queue.
3. Three elements (40, 50, 60) are inserted at the rear of the queue.
4. The queue elements are displayed: 30 20 10 40 50 60
5. One element is deleted from the front and one from the rear.
6. The queue elements after deletion are displayed: 20 10 40 50

### 1. Algorithms & Data Structures (C++): Dry run the FIFO queue algorithm

Sure, let's dry run the FIFO (First-In-First-Out) queue algorithm in C++. Here's a basic implementation:

```cpp
#include <iostream>
#include <queue>

int main() {
    // Creating a queue
    std::queue<int> myQueue;

    // Enqueue elements
    myQueue.push(10);
    myQueue.push(20);
    myQueue.push(30);
    myQueue.push(40);

    // Displaying the elements of the queue
    std::cout << "Queue elements: ";
    while (!myQueue.empty()) {
        std::cout << myQueue.front() << " ";
        myQueue.pop();
    }
    std::cout << std::endl;

    return 0;
}
```

Now, let's dry run this code step by step:

1. **Initialization**: We create a queue named `myQueue` of type `int`.

2. **Enqueue Elements**: We add elements to the queue using the `push()` function:
   * `myQueue.push(10)` adds 10 to the queue.
   * `myQueue.push(20)` adds 20 to the queue.
   * `myQueue.push(30)` adds 30 to the queue.
   * `myQueue.push(40)` adds 40 to the queue.

   Now the queue looks like this: `[10, 20, 30, 40]`.

3. **Dequeue and Display**: We iterate through the queue using a while loop until the queue is empty:
   * In the first iteration: `myQueue.front()` returns the front element of the queue, which is 10. We print 10 and then remove it from the queue using `myQueue.pop()`.
   * In the second iteration: `myQueue.front()` returns the front element of the queue, which is now 20. We print 20 and then remove it from the queue.
   * In the third iteration: `myQueue.front()` returns the front element of the queue, which is now 30. We print 30 and then remove it from the queue.
   * In the fourth iteration: `myQueue.front()` returns the front element of the queue, which is now 40. We print 40 and then remove it from the queue.

4. **Empty Check**: After all elements are dequeued, the queue becomes empty (`myQueue.empty()` returns `true`).

5. **Output**: The program prints:

   ```bash
   Queue elements: 10 20 30 40
   ```

And that's the dry run of the FIFO queue algorithm in C++. It follows the principle of First-In-First-Out, meaning the element added first is the one to be removed first.

### 1. Algorithms & Data Structures (C++): Dynamic Queue

A dynamic queue in C++ is a queue data structure that dynamically adjusts its size as elements are added or removed. Unlike a static queue, which has a fixed size, a dynamic queue can grow or shrink as needed to accommodate the number of elements it holds. This is achieved using dynamic memory allocation, typically with pointers.

Here's a basic implementation of a dynamic queue in C++:

```cpp
#include <iostream>

using namespace std;

// Node structure for each element in the queue
struct Node {
    int data;
    Node* next;
};

class DynamicQueue {
private:
    Node* front; // Points to the front of the queue
    Node* rear;  // Points to the rear of the queue

public:
    DynamicQueue() : front(nullptr), rear(nullptr) {}

    // Function to check if the queue is empty
    bool isEmpty() {
        return front == nullptr;
    }

    // Function to enqueue (insert) an element into the queue
    void enqueue(int value) {
        Node* newNode = new Node;
        newNode->data = value;
        newNode->next = nullptr;

        // If the queue is empty, set both front and rear to the new node
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            // Otherwise, add the new node to the rear and update rear
            rear->next = newNode;
            rear = newNode;
        }
    }

    // Function to dequeue (remove) an element from the queue
    int dequeue() {
        if (isEmpty()) {
            cout << "Queue is empty. Cannot dequeue." << endl;
            return -1; // Return some default value indicating failure
        }

        int value = front->data;
        Node* temp = front;

        // Move front to the next node
        front = front->next;

        // If after dequeue the queue becomes empty, update rear as well
        if (front == nullptr) {
            rear = nullptr;
        }

        delete temp; // Free memory of the dequeued node
        return value;
    }

    // Function to display the elements of the queue
    void display() {
        if (isEmpty()) {
            cout << "Queue is empty." << endl;
            return;
        }

        cout << "Queue elements: ";
        Node* temp = front;
        while (temp != nullptr) {
            cout << temp->data << " ";
            temp = temp->next;
        }
        cout << endl;
    }

    // Destructor to free memory allocated for nodes
    ~DynamicQueue() {
        while (!isEmpty()) {
            dequeue();
        }
    }
};

int main() {
    DynamicQueue queue;

    queue.enqueue(10);
    queue.enqueue(20);
    queue.enqueue(30);
    queue.display();

    cout << "Dequeue: " << queue.dequeue() << endl;
    cout << "Dequeue: " << queue.dequeue() << endl;

    queue.display();

    return 0;
}
```

This code defines a `DynamicQueue` class with basic operations such as `enqueue`, `dequeue`, `isEmpty`, and `display`. It dynamically allocates memory for nodes using `new` when elements are added and deallocates it using `delete` when elements are removed. The `display` function is used to print the elements of the queue. The destructor ensures that memory allocated for nodes is properly deallocated when the queue object is destroyed.

### 1. Algorithms & Data Structures (C++): Enqueue and Dequeue using Push1, Pop1, Push2 and Pop2

Sure, implementing a queue using two stacks (often called the two-stack method) involves using two stacks to simulate the behavior of a queue. Here's how you can implement enqueue and dequeue operations using two stacks in C++:

```cpp
#include <iostream>
#include <stack>

using namespace std;

class Queue {
private:
    stack<int> stack1;
    stack<int> stack2;

public:
    // Function to enqueue an element to the queue
    void enqueue(int value) {
        // Push the element onto stack1
        stack1.push(value);
    }

    // Function to dequeue an element from the queue
    int dequeue() {
        // If both stacks are empty, the queue is empty
        if (stack1.empty() && stack2.empty()) {
            cout << "Queue is empty." << endl;
            return -1; // Return some default value or throw an exception
        }

        // If stack2 is empty, transfer all elements from stack1 to stack2
        if (stack2.empty()) {
            while (!stack1.empty()) {
                stack2.push(stack1.top());
                stack1.pop();
            }
        }

        // Pop the top element from stack2 (which is the front of the queue)
        int front_element = stack2.top();
        stack2.pop();

        return front_element;
    }
};

int main() {
    Queue q;
    q.enqueue(1);
    q.enqueue(2);
    q.enqueue(3);

    cout << q.dequeue() << endl; // Output: 1
    cout << q.dequeue() << endl; // Output: 2

    q.enqueue(4);
    cout << q.dequeue() << endl; // Output: 3
    cout << q.dequeue() << endl; // Output: 4

    cout << q.dequeue() << endl; // Output: Queue is empty.

    return 0;
}
```

In this implementation, `stack1` is used to simulate the back of the queue (where elements are enqueued), and `stack2` is used to simulate the front of the queue (where elements are dequeued). When we need to dequeue an element, we first check if `stack2` is empty. If it is, we transfer all elements from `stack1` to `stack2`, effectively reversing the order of elements. Then we can pop the top element from `stack2`, which is the oldest element in the queue. If both stacks are empty when a dequeue operation is requested, it indicates that the queue is empty.

### 1. Algorithms & Data Structures (C++): Enqueue in Linked List

To enqueue an element in a linked list using C++, you typically perform the following steps:

1. Create a new node with the given data.
2. If the linked list is empty, make the new node the head of the list.
3. Otherwise, traverse the list to the last node and make the last node point to the new node.

Here's a simple implementation:

```cpp
#include <iostream>

// Define the structure of a node
struct Node {
    int data;
    Node* next;
    
    Node(int val) : data(val), next(nullptr) {}
};

// Define the class for the linked list
class LinkedList {
private:
    Node* head;

public:
    LinkedList() : head(nullptr) {}

    // Function to enqueue (insert at the end) an element
    void enqueue(int val) {
        Node* newNode = new Node(val); // Create a new node with the given data
        
        if (head == nullptr) { // If the list is empty
            head = newNode; // Make the new node the head of the list
        } else {
            Node* temp = head;
            while (temp->next != nullptr) { // Traverse to the last node
                temp = temp->next;
            }
            temp->next = newNode; // Make the last node point to the new node
        }
    }

    // Function to print the elements of the linked list
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

    // Enqueue some elements
    list.enqueue(1);
    list.enqueue(2);
    list.enqueue(3);
    list.enqueue(4);

    // Display the elements of the linked list
    std::cout << "Linked List: ";
    list.display();

    return 0;
}
```

This implementation defines a `Node` struct to represent each element in the linked list and a `LinkedList` class to manage the list. The `enqueue` function inserts elements at the end of the list, and the `display` function prints the elements of the list.

### 1. Algorithms & Data Structures (C++): EnQueue() and DeQueue() functions in Queue

Certainly! In C++, a queue is a data structure that follows the First-In-First-Out (FIFO) principle. It supports two main operations: `EnQueue()` to add elements to the back of the queue, and `DeQueue()` to remove elements from the front of the queue.

Here's a simple implementation of these functions:

```cpp
#include <iostream>

using namespace std;

// Define the structure of a QueueNode
struct QueueNode {
    int data;
    QueueNode* next;
    QueueNode(int val) : data(val), next(nullptr) {}
};

// Define the structure of the Queue
class Queue {
private:
    QueueNode* front;
    QueueNode* rear;

public:
    Queue() : front(nullptr), rear(nullptr) {}

    // Function to add an element to the back of the queue
    void EnQueue(int val) {
        QueueNode* newNode = new QueueNode(val);
        
        // If the queue is empty
        if (rear == nullptr) {
            front = rear = newNode;
            return;
        }

        // Otherwise, add the new node to the rear and update the rear pointer
        rear->next = newNode;
        rear = newNode;
    }

    // Function to remove an element from the front of the queue
    void DeQueue() {
        // If the queue is empty
        if (front == nullptr) {
            cout << "Queue is empty. Cannot dequeue.\n";
            return;
        }

        // Store the front node and move the front pointer to the next node
        QueueNode* temp = front;
        front = front->next;

        // If after dequeuing, the queue becomes empty, update the rear pointer to null
        if (front == nullptr) {
            rear = nullptr;
        }

        // Delete the dequeued node to avoid memory leaks
        delete temp;
    }
};

int main() {
    Queue queue;
    
    // Enqueue some elements
    queue.EnQueue(10);
    queue.EnQueue(20);
    queue.EnQueue(30);

    // Dequeue an element
    queue.DeQueue();

    // Enqueue another element
    queue.EnQueue(40);

    // Dequeue remaining elements
    while (queue.front != nullptr) {
        cout << "Dequeued: " << queue.front->data << endl;
        queue.DeQueue();
    }

    return 0;
}
```

This code defines a simple queue data structure using a linked list. The `EnQueue()` function adds elements to the rear of the queue, and the `DeQueue()` function removes elements from the front of the queue.

### 1. Algorithms & Data Structures (C++): EnQueue() and DeQueue() using Linked Representations

Certainly! In C++, you can implement a Queue data structure using linked representations. Here's a simple implementation of EnQueue() and DeQueue() operations:

```cpp
#include <iostream>

// Node structure for a linked list
struct Node {
    int data;
    Node* next;
    
    Node(int value) : data(value), next(nullptr) {}
};

// Queue class using linked list
class Queue {
private:
    Node* front; // Pointer to the front of the queue
    Node* rear;  // Pointer to the rear of the queue

public:
    Queue() : front(nullptr), rear(nullptr) {}

    // EnQueue operation to add an element to the rear of the queue
    void EnQueue(int value) {
        Node* newNode = new Node(value);
        if (rear == nullptr) {
            front = rear = newNode;
        } else {
            rear->next = newNode;
            rear = newNode;
        }
        std::cout << value << " enqueued to the queue.\n";
    }

    // DeQueue operation to remove an element from the front of the queue
    void DeQueue() {
        if (front == nullptr) {
            std::cout << "Queue is empty, cannot dequeue.\n";
            return;
        }
        
        Node* temp = front;
        front = front->next;
        
        if (front == nullptr) {
            rear = nullptr; // Queue becomes empty
        }
        
        std::cout << temp->data << " dequeued from the queue.\n";
        delete temp;
    }
};

int main() {
    Queue queue;

    // Enqueue some elements
    queue.EnQueue(10);
    queue.EnQueue(20);
    queue.EnQueue(30);

    // Dequeue elements
    queue.DeQueue();
    queue.DeQueue();
    queue.DeQueue();

    // Trying to dequeue from an empty queue
    queue.DeQueue();

    return 0;
}
```

This code defines a `Node` struct representing each element in the queue and a `Queue` class implementing EnQueue() and DeQueue() operations. The EnQueue() operation adds elements to the rear of the queue, while the DeQueue() operation removes elements from the front of the queue.

### 1. Algorithms & Data Structures (C++): EnQueue() in Circular Queue

Certainly! EnQueue operation in a circular queue is used to insert an element at the rear end of the queue. Here's how you can implement it in C++:

```cpp
#include <iostream>
using namespace std;

#define SIZE 5

class CircularQueue {
private:
    int front, rear;
    int queue[SIZE];

public:
    CircularQueue() {
        front = rear = -1;
    }

    // Function to check if the queue is full
    bool isFull() {
        if ((front == 0 && rear == SIZE - 1) || (rear == (front - 1) % (SIZE - 1))) {
            return true;
        }
        return false;
    }

    // Function to check if the queue is empty
    bool isEmpty() {
        if (front == -1) {
            return true;
        }
        return false;
    }

    // Function to insert an element into the queue
    void enQueue(int value) {
        if (isFull()) {
            cout << "Queue is full. EnQueue operation failed." << endl;
            return;
        }

        if (front == -1) {
            front = rear = 0;
            queue[rear] = value;
        } else if (rear == SIZE - 1 && front != 0) {
            rear = 0;
            queue[rear] = value;
        } else {
            rear++;
            queue[rear] = value;
        }
        cout << value << " enQueued into the circular queue." << endl;
    }

    // Function to display the elements of the queue
    void displayQueue() {
        if (isEmpty()) {
            cout << "Queue is empty." << endl;
            return;
        }
        cout << "Elements in the circular queue are: ";
        if (rear >= front) {
            for (int i = front; i <= rear; i++)
                cout << queue[i] << " ";
        } else {
            for (int i = front; i < SIZE; i++)
                cout << queue[i] << " ";
            for (int i = 0; i <= rear; i++)
                cout << queue[i] << " ";
        }
        cout << endl;
    }
};

int main() {
    CircularQueue cq;

    // Inserting elements into Circular Queue
    cq.enQueue(10);
    cq.enQueue(20);
    cq.enQueue(30);
    cq.enQueue(40);
    cq.enQueue(50);
    cq.enQueue(60); // This will fail as the queue is full

    // Displaying the Circular Queue
    cq.displayQueue();

    return 0;
}
```

This code implements a circular queue of fixed size `SIZE`. The `enQueue` function inserts elements into the circular queue. It first checks whether the queue is full or not using the `isFull` function. If the queue is not full, it checks different conditions to correctly insert the element at the rear end of the queue, considering both forward and wrapping cases.

Finally, the `displayQueue` function is used to display the elements of the circular queue.

### 1. Algorithms & Data Structures (C++): FIFO Queue Algorithm understanding

A FIFO (First In, First Out) queue is a fundamental data structure in computer science that operates on the principle that the first element added to the queue will be the first one to be removed. It follows the same principle as standing in a line: the first person to arrive at the line is the first one to leave.

In C++, you can implement a FIFO queue using various data structures such as arrays, linked lists, or the standard library's `std::queue`. Let's see how you can implement a FIFO queue using a simple array-based approach:

```cpp
#include <iostream>

const int MAX_SIZE = 100; // Maximum size of the queue

class Queue {
private:
    int arr[MAX_SIZE];
    int front, rear;

public:
    Queue() {
        front = -1; // Initialize front and rear
        rear = -1;
    }

    // Function to check if the queue is empty
    bool isEmpty() {
        return front == -1 && rear == -1;
    }

    // Function to check if the queue is full
    bool isFull() {
        return rear == MAX_SIZE - 1;
    }

    // Function to add an element to the queue
    void enqueue(int x) {
        if (isFull()) {
            std::cout << "Queue is full. Cannot enqueue element.\n";
            return;
        }
        if (isEmpty()) {
            front = rear = 0; // If queue is empty, set front and rear to 0
        } else {
            rear++;
        }
        arr[rear] = x;
    }

    // Function to remove an element from the queue
    void dequeue() {
        if (isEmpty()) {
            std::cout << "Queue is empty. Cannot dequeue element.\n";
            return;
        }
        if (front == rear) {
            // If only one element is present, reset front and rear to -1
            front = rear = -1;
        } else {
            front++;
        }
    }

    // Function to get the front element of the queue
    int frontElement() {
        if (isEmpty()) {
            std::cout << "Queue is empty. No front element.\n";
            return -1;
        }
        return arr[front];
    }
};

int main() {
    Queue q;
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);

    std::cout << "Front element: " << q.frontElement() << std::endl;

    q.dequeue();
    std::cout << "Front element after dequeue: " << q.frontElement() << std::endl;

    return 0;
}
```

In this implementation:

* We use an array `arr` to store the elements of the queue.
* `front` and `rear` are indices to keep track of the front and rear of the queue.
* `enqueue()` adds an element to the rear of the queue.
* `dequeue()` removes an element from the front of the queue.
* `frontElement()` returns the element at the front of the queue without removing it.
* `isEmpty()` and `isFull()` are helper functions to check if the queue is empty or full, respectively.

This implementation provides a basic understanding of how a FIFO queue works in C++. It's important to note that this is a simple implementation; in real-world scenarios, you might want to use the `std::queue` from the C++ standard library for more robust and efficient FIFO queue operations.

### 1. Algorithms & Data Structures (C++): How Dequeue is performed using Front Variable

In C++, a deque (double-ended queue) is a data structure that allows insertion and deletion at both ends, i.e., the front and the back. You can implement a deque using various data structures, such as arrays or linked lists. If you're using a linked list implementation, you'd typically have nodes, each containing a value and pointers to the previous and next nodes.

Here's a basic example of how you could implement a deque using a linked list and a `front` variable to facilitate dequeue operations from the front:

```cpp
#include <iostream>

// Define a Node structure for the linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
};

class Deque {
private:
    Node* front; // Pointer to the front of the deque
    Node* back;  // Pointer to the back of the deque

public:
    Deque() : front(nullptr), back(nullptr) {}

    // Function to insert element at the front of the deque
    void push_front(int value) {
        Node* newNode = new Node{value, nullptr, front};
        if (front == nullptr) {
            front = back = newNode;
        } else {
            front->prev = newNode;
            front = newNode;
        }
    }

    // Function to remove and return element from the front of the deque
    int pop_front() {
        if (front == nullptr) {
            std::cerr << "Deque is empty!\n";
            return -1; // Or throw an exception
        }
        int value = front->data;
        Node* temp = front;
        if (front == back) {
            front = back = nullptr;
        } else {
            front = front->next;
            front->prev = nullptr;
        }
        delete temp;
        return value;
    }

    // Function to check if the deque is empty
    bool empty() const {
        return front == nullptr;
    }
};

int main() {
    Deque dq;

    dq.push_front(5);
    dq.push_front(10);
    dq.push_front(15);

    std::cout << "Deque elements: ";
    while (!dq.empty()) {
        std::cout << dq.pop_front() << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this implementation:

* We have a `Node` struct to represent each element of the deque.
* The `Deque` class manages the deque operations.
* `push_front()` inserts an element at the front of the deque.
* `pop_front()` removes and returns the element from the front of the deque.
* The `front` variable points to the first element of the deque, facilitating dequeue operations from the front.
* The `back` variable could be used in a similar manner for operations at the back of the deque if needed.

### 1. Algorithms & Data Structures (C++): How Enqueue is performed using Rear Variable

In a typical queue implementation in C++, when you enqueue an element, you're adding it to the back of the queue. This involves updating the "rear" variable to point to the new element if it's the first element, or simply moving the rear pointer one position forward if the queue already contains elements.

Here's a simple implementation of a queue using a linked list in C++:

```cpp
#include <iostream>

// Define a structure for the node
struct Node {
    int data;
    Node* next;
};

// Define the Queue class
class Queue {
private:
    Node* front;
    Node* rear;

public:
    Queue() : front(nullptr), rear(nullptr) {}

    // Enqueue operation to add elements to the back of the queue
    void enqueue(int value) {
        Node* newNode = new Node;
        newNode->data = value;
        newNode->next = nullptr;

        // If the queue is empty, update both front and rear
        if (rear == nullptr) {
            front = rear = newNode;
        } else {
            // Otherwise, update the rear pointer
            rear->next = newNode;
            rear = newNode;
        }
    }

    // Function to display the queue
    void display() {
        if (front == nullptr) {
            std::cout << "Queue is empty" << std::endl;
            return;
        }
        Node* temp = front;
        while (temp != nullptr) {
            std::cout << temp->data << " ";
            temp = temp->next;
        }
        std::cout << std::endl;
    }
};

int main() {
    Queue q;
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    q.display();
    return 0;
}
```

In this code:

* `Node` is a simple structure defining a node of the linked list.
* The `Queue` class maintains pointers to the front and rear of the queue.
* The `enqueue` function adds elements to the queue by creating a new node and updating the rear pointer accordingly.
* The `display` function is included to visualize the queue's contents.

In the `enqueue` function:

* If the queue is empty (rear is nullptr), the front and rear pointers are updated to point to the new node.
* If the queue is not empty, the new node is appended to the end of the queue by updating the rear pointer to point to it and then moving the rear pointer forward.

### 1. Algorithms & Data Structures (C++): How Queue is Implemented using Linked List

Implementing a queue using a linked list in C++ is quite straightforward. In a linked list-based queue, you use a linked list to store the elements of the queue, and you maintain pointers to the front and rear of the queue to efficiently enqueue and dequeue elements. Here's a basic implementation:

```cpp
#include <iostream>

// Node class for creating nodes of the linked list
class Node {
public:
    int data;
    Node* next;
    
    Node(int value) : data(value), next(nullptr) {}
};

// Queue class implemented using a linked list
class Queue {
private:
    Node* front; // Pointer to the front of the queue
    Node* rear;  // Pointer to the rear of the queue

public:
    // Constructor
    Queue() : front(nullptr), rear(nullptr) {}

    // Destructor
    ~Queue() {
        // Deallocate memory for all nodes in the queue
        while (front != nullptr) {
            Node* temp = front;
            front = front->next;
            delete temp;
        }
        rear = nullptr;
    }

    // Function to check if the queue is empty
    bool isEmpty() {
        return front == nullptr;
    }

    // Function to enqueue an element into the queue
    void enqueue(int value) {
        // Create a new node with the given value
        Node* newNode = new Node(value);

        // If the queue is empty, set both front and rear to the new node
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            // Otherwise, add the new node to the rear and update the rear pointer
            rear->next = newNode;
            rear = newNode;
        }
    }

    // Function to dequeue an element from the queue
    int dequeue() {
        if (isEmpty()) {
            std::cerr << "Queue is empty. Cannot dequeue.\n";
            return -1; // Assuming -1 is used as an error indicator
        } else {
            // Store the data of the front node and move front to the next node
            int data = front->data;
            Node* temp = front;
            front = front->next;
            delete temp;
            
            // If front becomes nullptr, set rear to nullptr as well
            if (front == nullptr) {
                rear = nullptr;
            }
            
            return data;
        }
    }

    // Function to peek at the front element of the queue without removing it
    int peek() {
        if (isEmpty()) {
            std::cerr << "Queue is empty. Cannot peek.\n";
            return -1; // Assuming -1 is used as an error indicator
        } else {
            return front->data;
        }
    }
};

// Sample usage
int main() {
    Queue q;
    
    // Enqueue elements
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);

    // Dequeue and print elements
    std::cout << "Dequeued: " << q.dequeue() << std::endl;
    std::cout << "Dequeued: " << q.dequeue() << std::endl;

    // Enqueue more elements
    q.enqueue(40);
    q.enqueue(50);

    // Peek at the front element
    std::cout << "Front element: " << q.peek() << std::endl;

    return 0;
}
```

This implementation uses a singly linked list. Each node holds the data and a pointer to the next node. The `Queue` class maintains pointers to the front and rear nodes of the queue. Enqueueing is done by adding a new node at the rear, and dequeueing is done by removing the node at the front.

### 1. Algorithms & Data Structures (C++): How to add and remove from a Queue

Adding and removing elements from a queue in C++ is quite straightforward using the standard library's `queue` container, which is part of the `<queue>` header. Here's how you can do it:

```cpp
#include <iostream>
#include <queue>

int main() {
    // Create a queue of integers
    std::queue<int> myQueue;

    // Adding elements to the queue
    myQueue.push(10);
    myQueue.push(20);
    myQueue.push(30);

    // Removing elements from the queue
    std::cout << "Removing elements from the queue:" << std::endl;
    while (!myQueue.empty()) {
        std::cout << myQueue.front() << " ";
        myQueue.pop();
    }
    std::cout << std::endl;

    return 0;
}
```

In this example:

* `push(value)` is used to add elements to the back of the queue.
* `front()` returns the front element of the queue (the oldest element).
* `pop()` removes the front element from the queue.

Remember to include the necessary headers `<iostream>` for input and output and `<queue>` for the queue container. This example demonstrates a basic usage scenario, but you can use the `queue` container for any type of data, not just integers.

### 1. Algorithms & Data Structures (C++): Immutable Stack and Queue

Creating immutable versions of stack and queue data structures in C++ requires some careful design. Here's a basic implementation of immutable stack and queue:

```cpp
#include <iostream>
#include <memory>

template <typename T>
class ImmutableStack {
private:
    const std::shared_ptr<const ImmutableStack<T>> previous;
    const T value;
public:
    ImmutableStack() : previous(nullptr), value(T()) {}
    ImmutableStack(const std::shared_ptr<const ImmutableStack<T>>& prev, const T& val) : previous(prev), value(val) {}

    bool isEmpty() const {
        return !previous;
    }

    T top() const {
        return value;
    }

    std::shared_ptr<const ImmutableStack<T>> pop() const {
        if (isEmpty()) {
            throw std::out_of_range("Stack is empty");
        }
        return previous;
    }

    std::shared_ptr<const ImmutableStack<T>> push(const T& val) const {
        return std::make_shared<const ImmutableStack<T>>(this->shared_from_this(), val);
    }
};

template <typename T>
class ImmutableQueue {
private:
    const std::shared_ptr<const ImmutableStack<T>> frontStack;
    const std::shared_ptr<const ImmutableStack<T>> rearStack;
public:
    ImmutableQueue() : frontStack(nullptr), rearStack(nullptr) {}
    ImmutableQueue(const std::shared_ptr<const ImmutableStack<T>>& front, const std::shared_ptr<const ImmutableStack<T>>& rear)
        : frontStack(front), rearStack(rear) {}

    bool isEmpty() const {
        return !frontStack && !rearStack;
    }

    T front() const {
        if (isEmpty()) {
            throw std::out_of_range("Queue is empty");
        }
        if (frontStack) {
            return frontStack->top();
        } else {
            return rearStack->top();
        }
    }

    std::shared_ptr<const ImmutableQueue<T>> pop() const {
        if (isEmpty()) {
            throw std::out_of_range("Queue is empty");
        }
        if (frontStack) {
            return std::make_shared<const ImmutableQueue<T>>(frontStack->pop(), rearStack);
        } else {
            return std::make_shared<const ImmutableQueue<T>>(nullptr, rearStack->pop());
        }
    }

    std::shared_ptr<const ImmutableQueue<T>> push(const T& val) const {
        if (isEmpty()) {
            return std::make_shared<const ImmutableQueue<T>>(
                std::make_shared<const ImmutableStack<T>>()->push(val), nullptr);
        } else {
            return std::make_shared<const ImmutableQueue<T>>(frontStack, rearStack->push(val));
        }
    }
};

int main() {
    auto queue = std::make_shared<const ImmutableQueue<int>>();
    auto queue1 = queue->push(1)->push(2)->push(3);
    auto front = queue1->front();
    std::cout << "Front element: " << front << std::endl;

    auto queue2 = queue1->pop();
    front = queue2->front();
    std::cout << "Front element after pop: " << front << std::endl;

    return 0;
}
```

In this implementation:

* `ImmutableStack` is a simple immutable stack with methods `push`, `pop`, `top`, and `isEmpty`.
* `ImmutableQueue` is implemented using two stacks, where elements are enqueued to one stack and dequeued from another. This approach ensures that dequeue operations are performed in constant time.

Please note that this is a basic implementation and may not cover all edge cases or be the most efficient solution for all scenarios.

### 1. Algorithms & Data Structures (C++): Implement Queue using Front and Rear Variables

Certainly! Implementing a queue using front and rear variables in C++ is a fundamental exercise in understanding how queues work. Here's a simple implementation:

```cpp
#include <iostream>
using namespace std;

#define MAX_SIZE 100 // Maximum size of the queue

class Queue {
private:
    int arr[MAX_SIZE];
    int front, rear;

public:
    Queue() {
        front = -1;
        rear = -1;
    }

    bool isEmpty() {
        return (front == -1 && rear == -1);
    }

    bool isFull() {
        return (rear + 1) % MAX_SIZE == front ? true : false;
    }

    void enqueue(int value) {
        if (isFull()) {
            cout << "Queue is full. Cannot enqueue." << endl;
            return;
        } else if (isEmpty()) {
            front = rear = 0;
        } else {
            rear = (rear + 1) % MAX_SIZE;
        }
        arr[rear] = value;
    }

    void dequeue() {
        if (isEmpty()) {
            cout << "Queue is empty. Cannot dequeue." << endl;
            return;
        } else if (front == rear) {
            front = rear = -1;
        } else {
            front = (front + 1) % MAX_SIZE;
        }
    }

    int peek() {
        if (isEmpty()) {
            cout << "Queue is empty. No front element." << endl;
            return -1; // Return some default value or throw an exception
        }
        return arr[front];
    }

    void display() {
        if (isEmpty()) {
            cout << "Queue is empty." << endl;
            return;
        }
        int i = front;
        while (i != rear) {
            cout << arr[i] << " ";
            i = (i + 1) % MAX_SIZE;
        }
        cout << arr[rear] << endl;
    }
};

int main() {
    Queue q;
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    q.enqueue(40);
    q.enqueue(50);

    cout << "Queue elements: ";
    q.display();

    cout << "Front element: " << q.peek() << endl;

    q.dequeue();
    cout << "Queue after dequeue: ";
    q.display();

    return 0;
}
```

In this implementation:

* `front` and `rear` variables keep track of the front and rear of the queue, respectively.
* `isEmpty()` and `isFull()` functions are used to check if the queue is empty or full, respectively.
* `enqueue()` function adds an element to the rear of the queue.
* `dequeue()` function removes an element from the front of the queue.
* `peek()` function returns the front element without removing it.
* `display()` function displays all the elements of the queue.

### 1. Algorithms & Data Structures (C++): Implement Queue Using ONE stack

Implementing a queue using only one stack in C++ involves a clever manipulation of the stack operations. The idea is to simulate the behavior of a queue using just one stack. Here's a simple implementation:

```cpp
#include <iostream>
#include <stack>

using namespace std;

class Queue {
private:
    stack<int> s1;

public:
    void enqueue(int x) {
        s1.push(x); // Push element to stack
    }

    int dequeue() {
        if (s1.empty()) {
            cout << "Queue is empty!" << endl;
            return -1; // Or throw an exception
        }

        int x = s1.top();
        s1.pop();

        if (s1.empty()) // If this was the last element, return
            return x;
        
        int item = dequeue(); // Recursively dequeue until the last element
        s1.push(x); // Push back elements after recursion
        
        return item;
    }

    bool isEmpty() {
        return s1.empty();
    }
};

int main() {
    Queue q;
    q.enqueue(1);
    q.enqueue(2);
    q.enqueue(3);

    cout << q.dequeue() << endl; // Output: 1
    cout << q.dequeue() << endl; // Output: 2
    cout << q.dequeue() << endl; // Output: 3
    cout << q.dequeue() << endl; // Output: Queue is empty!

    return 0;
}
```

In this implementation:

* The `enqueue()` operation simply pushes the element onto the stack.
* The `dequeue()` operation is a bit tricky. It recursively dequeues elements until the last element of the stack is reached. Then, it pops that last element and returns it. During the recursion, elements are popped and pushed back onto the stack, effectively reversing their order.
* `isEmpty()` checks if the stack is empty.

Keep in mind that this implementation has some limitations and may not be as efficient as using two stacks or other queue implementations, especially when dealing with large amounts of data. However, it demonstrates the concept of implementing a queue using one stack.

### 1. Algorithms & Data Structures (C++): Implementation of Circular Queue

Sure, here's a basic implementation of a circular queue in C++:

```cpp
#include <iostream>

#define MAX_SIZE 100

using namespace std;

class CircularQueue {
private:
    int front, rear;
    int arr[MAX_SIZE];
public:
    CircularQueue() {
        front = -1;
        rear = -1;
    }

    bool isEmpty() {
        return (front == -1 && rear == -1);
    }

    bool isFull() {
        return ((rear + 1) % MAX_SIZE == front);
    }

    void enqueue(int val) {
        if (isFull()) {
            cout << "Queue is full." << endl;
            return;
        } else if (isEmpty()) {
            front = rear = 0;
        } else {
            rear = (rear + 1) % MAX_SIZE;
        }
        arr[rear] = val;
    }

    void dequeue() {
        if (isEmpty()) {
            cout << "Queue is empty." << endl;
            return;
        } else if (front == rear) {
            front = rear = -1;
        } else {
            front = (front + 1) % MAX_SIZE;
        }
    }

    int peek() {
        if (isEmpty()) {
            cout << "Queue is empty." << endl;
            return -1;
        }
        return arr[front];
    }

    void display() {
        if (isEmpty()) {
            cout << "Queue is empty." << endl;
            return;
        }
        cout << "Elements in the queue are: ";
        int i = front;
        while (i != rear) {
            cout << arr[i] << " ";
            i = (i + 1) % MAX_SIZE;
        }
        cout << arr[rear] << endl;
    }
};

int main() {
    CircularQueue q;
    q.enqueue(1);
    q.enqueue(2);
    q.enqueue(3);
    q.enqueue(4);
    q.display();
    q.dequeue();
    q.dequeue();
    q.display();
    q.enqueue(5);
    q.enqueue(6);
    q.display();
    return 0;
}
```

This implementation defines a class `CircularQueue` with methods for `enqueue`, `dequeue`, `isEmpty`, `isFull`, `peek`, and `display`. It uses an array to store the elements of the queue, and it keeps track of the `front` and `rear` indices to implement the circular nature of the queue.

### 1. Algorithms & Data Structures (C++): Implementation of Double Ended Queue

Sure! Below is a simple implementation of a Double Ended Queue (Deque) in C++:

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

class Deque {
private:
    Node* front;
    Node* rear;
    int size;
    
public:
    Deque() : front(nullptr), rear(nullptr), size(0) {}
    
    // Check if deque is empty
    bool isEmpty() {
        return size == 0;
    }
    
    // Get the size of the deque
    int getSize() {
        return size;
    }
    
    // Insert element at the front of the deque
    void insertFront(int val) {
        Node* newNode = new Node(val);
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            newNode->next = front;
            front->prev = newNode;
            front = newNode;
        }
        size++;
    }
    
    // Insert element at the rear of the deque
    void insertRear(int val) {
        Node* newNode = new Node(val);
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            rear->next = newNode;
            newNode->prev = rear;
            rear = newNode;
        }
        size++;
    }
    
    // Remove element from the front of the deque
    void deleteFront() {
        if (isEmpty()) {
            cout << "Deque is empty\n";
        } else {
            Node* temp = front;
            if (front == rear) {
                front = rear = nullptr;
            } else {
                front = front->next;
                front->prev = nullptr;
            }
            delete temp;
            size--;
        }
    }
    
    // Remove element from the rear of the deque
    void deleteRear() {
        if (isEmpty()) {
            cout << "Deque is empty\n";
        } else {
            Node* temp = rear;
            if (front == rear) {
                front = rear = nullptr;
            } else {
                rear = rear->prev;
                rear->next = nullptr;
            }
            delete temp;
            size--;
        }
    }
    
    // Display the deque
    void display() {
        if (isEmpty()) {
            cout << "Deque is empty\n";
            return;
        }
        Node* curr = front;
        while (curr != nullptr) {
            cout << curr->data << " ";
            curr = curr->next;
        }
        cout << endl;
    }
};

int main() {
    Deque dq;
    
    dq.insertFront(1);
    dq.insertRear(2);
    dq.insertFront(3);
    dq.insertRear(4);
    
    cout << "Deque: ";
    dq.display(); // Output: Deque: 3 1 2 4
    
    dq.deleteFront();
    dq.deleteRear();
    
    cout << "Deque after deletion: ";
    dq.display(); // Output: Deque after deletion: 1 2
    
    return 0;
}
```

This implementation uses a doubly linked list to represent the deque. It supports insertion and deletion operations at both ends of the deque and provides methods to check if the deque is empty and to get its size.

### 1. Algorithms & Data Structures (C++): Implementation of FIFO Queue

Certainly! Below is a simple implementation of a FIFO (First-In-First-Out) queue using C++:

```cpp
#include <iostream>

template <typename T>
class Queue {
private:
    struct Node {
        T data;
        Node* next;
        Node(const T& data) : data(data), next(nullptr) {}
    };

    Node* frontPtr;
    Node* rearPtr;
    int size;

public:
    Queue() : frontPtr(nullptr), rearPtr(nullptr), size(0) {}

    ~Queue() {
        while (!isEmpty()) {
            dequeue();
        }
    }

    void enqueue(const T& data) {
        Node* newNode = new Node(data);
        if (isEmpty()) {
            frontPtr = rearPtr = newNode;
        } else {
            rearPtr->next = newNode;
            rearPtr = newNode;
        }
        size++;
    }

    void dequeue() {
        if (!isEmpty()) {
            Node* temp = frontPtr;
            frontPtr = frontPtr->next;
            delete temp;
            size--;
            if (isEmpty()) {
                rearPtr = nullptr;
            }
        } else {
            std::cerr << "Error: Queue is empty. Cannot dequeue.\n";
        }
    }

    T front() const {
        if (!isEmpty()) {
            return frontPtr->data;
        } else {
            throw std::runtime_error("Error: Queue is empty. Cannot retrieve front element.");
        }
    }

    bool isEmpty() const {
        return size == 0;
    }

    int getSize() const {
        return size;
    }
};

int main() {
    Queue<int> myQueue;

    myQueue.enqueue(10);
    myQueue.enqueue(20);
    myQueue.enqueue(30);

    std::cout << "Front element: " << myQueue.front() << std::endl;
    std::cout << "Queue size: " << myQueue.getSize() << std::endl;

    myQueue.dequeue();

    std::cout << "Front element after dequeue: " << myQueue.front() << std::endl;
    std::cout << "Queue size after dequeue: " << myQueue.getSize() << std::endl;

    return 0;
}
```

This implementation defines a `Queue` class using a linked list. Each element in the queue is represented by a node containing the data and a pointer to the next node. The `enqueue()` function adds elements to the rear of the queue, while `dequeue()` removes elements from the front of the queue. The `front()` function returns the element at the front of the queue without removing it.

### 1. Algorithms & Data Structures (C++): Implementation of Priority Queue

Sure, I can provide you with a simple implementation of a priority queue in C++ using a binary heap. Here's a basic example:

```cpp
#include <iostream>
#include <vector>

using namespace std;

template<typename T>
class PriorityQueue {
private:
    vector<T> heap;

    // Helper functions
    int parent(int i) { return (i - 1) / 2; }
    int left(int i) { return 2 * i + 1; }
    int right(int i) { return 2 * i + 2; }

    // Maintains heap property by moving the element up
    void heapifyUp(int i) {
        while (i > 0 && heap[parent(i)] < heap[i]) {
            swap(heap[i], heap[parent(i)]);
            i = parent(i);
        }
    }

    // Maintains heap property by moving the element down
    void heapifyDown(int i) {
        int maxIndex = i;
        int l = left(i);
        int r = right(i);

        if (l < heap.size() && heap[l] > heap[maxIndex])
            maxIndex = l;
        if (r < heap.size() && heap[r] > heap[maxIndex])
            maxIndex = r;

        if (i != maxIndex) {
            swap(heap[i], heap[maxIndex]);
            heapifyDown(maxIndex);
        }
    }

public:
    // Insert element into the priority queue
    void insert(T element) {
        heap.push_back(element);
        heapifyUp(heap.size() - 1);
    }

    // Remove the highest priority element from the queue
    T extractMax() {
        if (heap.empty()) {
            throw out_of_range("Priority queue is empty");
        }

        T max = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        heapifyDown(0);

        return max;
    }

    // Get the highest priority element without removing it
    T getMax() {
        if (heap.empty()) {
            throw out_of_range("Priority queue is empty");
        }
        return heap[0];
    }

    // Check if the priority queue is empty
    bool isEmpty() {
        return heap.empty();
    }
};

int main() {
    PriorityQueue<int> pq;

    // Insert elements into the priority queue
    pq.insert(5);
    pq.insert(10);
    pq.insert(3);
    pq.insert(7);

    // Print and remove elements from the priority queue
    while (!pq.isEmpty()) {
        cout << pq.extractMax() << " ";
    }
    cout << endl;

    return 0;
}
```

This implementation uses a max-heap to implement the priority queue. The `insert` function inserts an element into the priority queue, the `extractMax` function removes and returns the highest priority element, the `getMax` function returns the highest priority element without removing it, and the `isEmpty` function checks if the priority queue is empty.

### 1. Algorithms & Data Structures (C++): Implementation of Queue using Linked List

Certainly! Here's a basic implementation of a Queue using a linked list in C++:

```cpp
#include <iostream>

// Node class to represent each element of the linked list
class Node {
public:
    int data;
    Node* next;
    Node(int value) : data(value), next(nullptr) {}
};

// Queue class implementing the Queue using linked list
class Queue {
private:
    Node* front; // Pointer to the front of the queue
    Node* rear;  // Pointer to the rear of the queue
public:
    Queue() : front(nullptr), rear(nullptr) {}

    // Function to check if the queue is empty
    bool isEmpty() {
        return front == nullptr;
    }

    // Function to enqueue an element to the rear of the queue
    void enqueue(int value) {
        Node* newNode = new Node(value);
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            rear->next = newNode;
            rear = newNode;
        }
    }

    // Function to dequeue an element from the front of the queue
    void dequeue() {
        if (isEmpty()) {
            std::cout << "Queue is empty. Cannot dequeue.\n";
        } else {
            Node* temp = front;
            front = front->next;
            delete temp;
            if (front == nullptr) {
                rear = nullptr; // Reset rear when the last element is dequeued
            }
        }
    }

    // Function to get the front element of the queue
    int peek() {
        if (isEmpty()) {
            std::cerr << "Queue is empty. No front element.\n";
            return -1; // Returning -1 indicating an invalid value
        }
        return front->data;
    }

    // Function to display the elements of the queue
    void display() {
        if (isEmpty()) {
            std::cout << "Queue is empty.\n";
        } else {
            Node* current = front;
            std::cout << "Queue elements: ";
            while (current != nullptr) {
                std::cout << current->data << " ";
                current = current->next;
            }
            std::cout << std::endl;
        }
    }

    // Destructor to free memory
    ~Queue() {
        while (!isEmpty()) {
            dequeue();
        }
    }
};

// Main function to test the implementation
int main() {
    Queue queue;

    queue.enqueue(10);
    queue.enqueue(20);
    queue.enqueue(30);
    queue.enqueue(40);

    queue.display(); // Output should be: 10 20 30 40

    std::cout << "Front element: " << queue.peek() << std::endl; // Output should be: 10

    queue.dequeue();
    queue.dequeue();

    queue.display(); // Output should be: 30 40

    std::cout << "Front element: " << queue.peek() << std::endl; // Output should be: 30

    return 0;
}
```

This code provides a basic implementation of a queue using a linked list in C++. The `Queue` class provides methods for enqueueing, dequeueing, checking if the queue is empty, peeking at the front element, and displaying the elements of the queue.

### 1. Algorithms & Data Structures (C++): Implementing Linked Representation of Queue

Certainly! Implementing a queue using a linked representation involves creating a linked list where each node represents an element in the queue. Here's a basic implementation of a queue using a linked list in C++:

```cpp
#include <iostream>

// Define the structure of a node
struct Node {
    int data;
    Node* next;
    
    Node(int value) : data(value), next(nullptr) {}
};

// Define the Queue class
class Queue {
private:
    Node* front;
    Node* rear;
    
public:
    Queue() : front(nullptr), rear(nullptr) {}
    
    // Function to check if the queue is empty
    bool isEmpty() {
        return front == nullptr;
    }
    
    // Function to enqueue an element to the queue
    void enqueue(int value) {
        Node* newNode = new Node(value);
        
        // If queue is empty, both front and rear point to the new node
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            // Else, append the new node to the rear of the queue
            rear->next = newNode;
            rear = newNode;
        }
        
        std::cout << value << " enqueued to queue." << std::endl;
    }
    
    // Function to dequeue an element from the queue
    void dequeue() {
        // Check if queue is empty
        if (isEmpty()) {
            std::cout << "Queue is empty. Cannot dequeue." << std::endl;
            return;
        }
        
        // Store the node to be dequeued
        Node* temp = front;
        
        // Move front pointer to the next node
        front = front->next;
        
        // If front becomes null, then set rear to null as well
        if (front == nullptr) {
            rear = nullptr;
        }
        
        std::cout << temp->data << " dequeued from queue." << std::endl;
        
        // Free memory
        delete temp;
    }
    
    // Function to display the elements of the queue
    void display() {
        // Check if queue is empty
        if (isEmpty()) {
            std::cout << "Queue is empty." << std::endl;
            return;
        }
        
        std::cout << "Elements in the queue: ";
        Node* current = front;
        
        // Traverse the queue and print elements
        while (current != nullptr) {
            std::cout << current->data << " ";
            current = current->next;
        }
        
        std::cout << std::endl;
    }
    
    // Function to get the front element of the queue
    int getFront() {
        // Check if queue is empty
        if (isEmpty()) {
            std::cerr << "Queue is empty." << std::endl;
            return -1; // Error code or throw exception
        }
        return front->data;
    }
};

// Main function for testing the Queue implementation
int main() {
    Queue queue;
    
    queue.enqueue(10);
    queue.enqueue(20);
    queue.enqueue(30);
    
    queue.display(); // Output: Elements in the queue: 10 20 30
    
    std::cout << "Front element: " << queue.getFront() << std::endl; // Output: Front element: 10
    
    queue.dequeue();
    
    queue.display(); // Output: Elements in the queue: 20 30
    
    return 0;
}
```

This code creates a basic implementation of a queue using a linked list. It provides functions to enqueue, dequeue, display the elements of the queue, and get the front element of the queue.

### 1. Algorithms & Data Structures (C++): Implementing QEUEUE using STACK Data Structure

Implementing a queue using stacks in C++ can be done by using two stacks. One stack is used for enqueue operations, and the other stack is used for dequeue operations. Here's a simple implementation:

```cpp
#include <iostream>
#include <stack>

using namespace std;

class QueueUsingStack {
private:
    stack<int> enqueueStack;
    stack<int> dequeueStack;

public:
    void enqueue(int x) {
        // Simply push the element onto the enqueue stack
        enqueueStack.push(x);
    }

    int dequeue() {
        // Check if dequeue stack is empty
        if (dequeueStack.empty()) {
            // Transfer all elements from enqueue stack to dequeue stack
            while (!enqueueStack.empty()) {
                dequeueStack.push(enqueueStack.top());
                enqueueStack.pop();
            }
        }

        // If dequeue stack is still empty, the queue is empty
        if (dequeueStack.empty()) {
            cerr << "Error: Queue is empty." << endl;
            return -1; // Return a sentinel value indicating error
        }

        // Pop from dequeue stack to perform dequeue operation
        int front = dequeueStack.top();
        dequeueStack.pop();
        return front;
    }

    bool isEmpty() {
        // Queue is empty if both stacks are empty
        return enqueueStack.empty() && dequeueStack.empty();
    }
};

int main() {
    QueueUsingStack q;

    q.enqueue(1);
    q.enqueue(2);
    q.enqueue(3);

    cout << q.dequeue() << endl; // Should print 1
    cout << q.dequeue() << endl; // Should print 2

    q.enqueue(4);
    q.enqueue(5);

    cout << q.dequeue() << endl; // Should print 3
    cout << q.dequeue() << endl; // Should print 4
    cout << q.dequeue() << endl; // Should print 5

    cout << (q.isEmpty() ? "Queue is empty" : "Queue is not empty") << endl; // Should print "Queue is empty"

    return 0;
}
```

In this implementation, the `enqueueStack` is used for enqueue operations. When a dequeue operation is requested, elements are transferred from the `enqueueStack` to the `dequeueStack` (if it's empty). Then, the top element of the `dequeueStack` is popped to perform the dequeue operation.

This implementation ensures that enqueue and dequeue operations take \(O(1)\) amortized time complexity, with \(O(n)\) time complexity for transferring elements between stacks when needed.

### 1. Algorithms & Data Structures (C++): Inbuilt Min Priority Queue

In C++, you can use the Standard Template Library (STL) to work with a min priority queue. The `std::priority_queue` container in C++ STL is by default a max heap, but you can make it behave like a min heap by providing a custom comparator. Here's how you can use it:

```cpp
#include <iostream>
#include <queue>

int main() {
    // Declaration of min priority queue of integers
    std::priority_queue<int, std::vector<int>, std::greater<int>> minHeap;

    // Inserting elements into the min heap
    minHeap.push(5);
    minHeap.push(2);
    minHeap.push(8);
    minHeap.push(1);
    minHeap.push(3);

    // Accessing the top element of the min heap
    std::cout << "Top element of min heap: " << minHeap.top() << std::endl;

    // Removing the top element from the min heap
    minHeap.pop();
    std::cout << "Top element after removal: " << minHeap.top() << std::endl;

    return 0;
}
```

In the code above:

* `std::priority_queue<int, std::vector<int>, std::greater<int>>` declares a min priority queue of integers. The third template argument `std::greater<int>` specifies the comparison function, making it a min heap. `std::greater<int>` is a functor that returns true if the first argument is greater than the second, thus making the priority queue behave like a min heap.

* `push()` is used to insert elements into the priority queue.

* `top()` returns a reference to the top (minimum) element of the priority queue.

* `pop()` removes the top element from the priority queue.

This is a simple example of using a min priority queue in C++ using the STL. You can customize it based on your specific requirements.

### 1. Algorithms & Data Structures (C++): Inbuilt Priority Queue

In C++, you can use the Standard Template Library (STL) to implement a priority queue efficiently. Priority queues are a type of container adapters, which are specifically designed to operate in a way that the elements with the highest priority are served before elements with lower priority. Here's a brief overview of how to use the inbuilt priority queue in C++:

```cpp
#include <iostream>
#include <queue>

int main() {
    // Declaration of a priority queue of integers
    std::priority_queue<int> pq;

    // Inserting elements into the priority queue
    pq.push(10);
    pq.push(30);
    pq.push(20);

    // Accessing the top element (highest priority element) of the priority queue
    std::cout << "Top element: " << pq.top() << std::endl;

    // Removing the top element from the priority queue
    pq.pop();

    // Accessing the top element after removal
    std::cout << "Top element after removal: " << pq.top() << std::endl;

    // Checking if the priority queue is empty
    std::cout << "Is priority queue empty? " << (pq.empty() ? "Yes" : "No") << std::endl;

    // Size of the priority queue
    std::cout << "Size of priority queue: " << pq.size() << std::endl;

    return 0;
}
```

In this code:

* We include the `<queue>` header, which provides the priority queue functionality.
* We create a priority queue `pq` of integers using `std::priority_queue<int>`.
* We can push elements into the priority queue using the `push()` method.
* To access the top element (the element with the highest priority), we use the `top()` method.
* To remove the top element, we use the `pop()` method.
* We can check if the priority queue is empty using the `empty()` method.
* The `size()` method returns the number of elements in the priority queue.

The elements are arranged in the priority queue in such a way that the element with the highest priority (maximum value by default for integers) is at the top. You can also define your custom comparison function to change the priority order based on your requirements.

### 1. Algorithms & Data Structures (C++): Inbuilt queue

In C++, the Standard Template Library (STL) provides a versatile set of containers and algorithms, including queues, which are implemented as part of the `<queue>` header. The `queue` container is a First-In-First-Out (FIFO) data structure, meaning that elements are inserted at the back and removed from the front. Here's a basic example of how to use the inbuilt `queue` in C++:

```cpp
#include <iostream>
#include <queue>

int main() {
    // Creating a queue of integers
    std::queue<int> myQueue;

    // Inserting elements into the queue
    myQueue.push(10);
    myQueue.push(20);
    myQueue.push(30);

    // Accessing the front element
    std::cout << "Front element: " << myQueue.front() << std::endl;

    // Accessing the back element
    std::cout << "Back element: " << myQueue.back() << std::endl;

    // Removing elements from the queue
    myQueue.pop();

    // Displaying the size of the queue
    std::cout << "Size of the queue: " << myQueue.size() << std::endl;

    // Checking if the queue is empty
    if (myQueue.empty()) {
        std::cout << "Queue is empty." << std::endl;
    } else {
        std::cout << "Queue is not empty." << std::endl;
    }

    return 0;
}
```

This code demonstrates basic operations with a queue:

1. `push`: Inserts an element at the back of the queue.
2. `front`: Accesses the element at the front of the queue.
3. `back`: Accesses the element at the back of the queue.
4. `pop`: Removes the element from the front of the queue.
5. `size`: Returns the number of elements in the queue.
6. `empty`: Checks if the queue is empty.

Remember to include the `<queue>` header at the beginning of your code to use the `queue` container.

### 1. Algorithms & Data Structures (C++): InsertFront() and InsertRear() in DEQueue

In C++, you can implement a double-ended queue (deque) and its `InsertFront()` and `InsertRear()` operations using a doubly linked list. Here's a basic implementation:

```cpp
#include <iostream>

// Node structure for the doubly linked list
struct Node {
    int data;
    Node* next;
    Node* prev;
    
    Node(int val) : data(val), next(nullptr), prev(nullptr) {}
};

// Double-ended queue class
class Deque {
private:
    Node* front;
    Node* rear;
    
public:
    Deque() : front(nullptr), rear(nullptr) {}
    
    // Function to insert an element at the front of the deque
    void InsertFront(int val) {
        Node* newNode = new Node(val);
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            newNode->next = front;
            front->prev = newNode;
            front = newNode;
        }
    }
    
    // Function to insert an element at the rear of the deque
    void InsertRear(int val) {
        Node* newNode = new Node(val);
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            rear->next = newNode;
            newNode->prev = rear;
            rear = newNode;
        }
    }
    
    // Function to check if the deque is empty
    bool isEmpty() {
        return front == nullptr;
    }
    
    // Function to display the deque from front to rear
    void display() {
        Node* temp = front;
        while (temp != nullptr) {
            std::cout << temp->data << " ";
            temp = temp->next;
        }
        std::cout << std::endl;
    }
};

int main() {
    Deque dq;
    
    dq.InsertFront(10);
    dq.InsertFront(20);
    dq.InsertRear(30);
    dq.InsertRear(40);
    
    std::cout << "Deque: ";
    dq.display(); // Output: Deque: 20 10 30 40
    
    return 0;
}
```

In this implementation:

* We define a `Node` structure to represent each element in the doubly linked list.
* The `Deque` class contains two pointers: `front` points to the first node, and `rear` points to the last node.
* `InsertFront()` inserts a new node at the beginning of the deque.
* `InsertRear()` inserts a new node at the end of the deque.
* `isEmpty()` checks if the deque is empty.
* `display()` traverses the deque from front to rear and prints its elements.

You can extend this implementation by adding other operations such as deleting elements from the front and rear, accessing elements, and so on.

### 1. Algorithms & Data Structures (C++): Interleave two halves of a queue

To interleave two halves of a queue in C++, you can follow these steps:

1. Split the queue into two halves.
2. Interleave the elements of the two halves.
3. Merge the interleaved halves back into the original queue.

Here's a C++ implementation of this algorithm:

```cpp
#include <iostream>
#include <queue>

using namespace std;

// Function to interleave two halves of a queue
void interleave(queue<int>& q) {
    // Step 1: Split the queue into two halves
    int size = q.size();
    int half_size = size / 2;

    queue<int> first_half, second_half;
    for (int i = 0; i < half_size; ++i) {
        first_half.push(q.front());
        q.pop();
    }
    while (!q.empty()) {
        second_half.push(q.front());
        q.pop();
    }

    // Step 2: Interleave the elements of the two halves
    while (!first_half.empty()) {
        q.push(second_half.front());
        second_half.pop();
        q.push(first_half.front());
        first_half.pop();
    }

    // Step 3: Merge the interleaved halves back into the original queue
    while (!second_half.empty()) {
        q.push(second_half.front());
        second_half.pop();
    }
}

// Function to print the elements of a queue
void printQueue(queue<int> q) {
    while (!q.empty()) {
        cout << q.front() << " ";
        q.pop();
    }
    cout << endl;
}

int main() {
    queue<int> q;
    // Push elements into the queue
    for (int i = 1; i <= 10; ++i) {
        q.push(i);
    }

    cout << "Original Queue: ";
    printQueue(q);

    interleave(q);

    cout << "Interleaved Queue: ";
    printQueue(q);

    return 0;
}
```

This code first splits the queue into two halves, then interleave the elements of the two halves, and finally merges the interleaved halves back into the original queue. You can test it by running the `main` function.

### 1. Algorithms & Data Structures (C++): Linked Representation of Queue

Sure, here's a basic implementation of a queue using linked representation in C++:

```cpp
#include <iostream>

using namespace std;

// Node class to represent individual elements in the queue
class Node {
public:
    int data;
    Node* next;

    // Constructor to initialize a node with given data
    Node(int value) {
        data = value;
        next = nullptr;
    }
};

// Queue class
class Queue {
private:
    Node* front; // Pointer to the front of the queue
    Node* rear;  // Pointer to the rear of the queue

public:
    // Constructor to initialize an empty queue
    Queue() {
        front = nullptr;
        rear = nullptr;
    }

    // Function to check if the queue is empty
    bool isEmpty() {
        return (front == nullptr);
    }

    // Function to enqueue an element into the queue
    void enqueue(int value) {
        // Create a new node with the given value
        Node* newNode = new Node(value);

        // If the queue is empty, set both front and rear to the new node
        if (isEmpty()) {
            front = newNode;
            rear = newNode;
        } else {
            // Otherwise, link the current rear node to the new node
            rear->next = newNode;
            // Update the rear pointer to the new node
            rear = newNode;
        }
    }

    // Function to dequeue an element from the queue
    int dequeue() {
        // If the queue is empty, return -1 (assuming -1 is not a valid queue element)
        if (isEmpty()) {
            cout << "Queue is empty. Cannot dequeue.\n";
            return -1;
        } else {
            // Store the data of the front node
            int data = front->data;
            // Move the front pointer to the next node
            Node* temp = front;
            front = front->next;
            // If the front becomes nullptr (queue becomes empty), also update rear to nullptr
            if (front == nullptr) {
                rear = nullptr;
            }
            // Delete the previous front node
            delete temp;
            // Return the data of the dequeued node
            return data;
        }
    }

    // Function to return the front element of the queue without dequeueing it
    int peek() {
        // If the queue is empty, return -1
        if (isEmpty()) {
            cout << "Queue is empty. Cannot peek.\n";
            return -1;
        } else {
            // Return the data of the front node
            return front->data;
        }
    }
};

int main() {
    Queue q;

    // Enqueue elements into the queue
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);

    // Print the front element of the queue
    cout << "Front element: " << q.peek() << endl;

    // Dequeue an element
    cout << "Dequeued element: " << q.dequeue() << endl;

    // Print the front element again
    cout << "Front element after dequeue: " << q.peek() << endl;

    return 0;
}
```

This implementation uses a singly linked list to represent the queue. Each node contains an integer value (`data`) and a pointer to the next node (`next`). The `Queue` class manages the front and rear pointers of the queue and provides methods for enqueueing, dequeueing, and peeking elements.

### 1. Algorithms & Data Structures (C++): Manipulating Queues

Certainly! Manipulating queues in C++ is a fundamental operation in many programming tasks. Queues follow the First-In-First-Out (FIFO) principle, where elements are added at the back and removed from the front. C++ provides a standard library `queue` container adapter that makes it easy to work with queues.

Here's a basic overview of how to manipulate queues in C++:

#### Creating a Queue

You can create a queue in C++ using the `std::queue` container adapter provided by the Standard Template Library (STL). You need to include the `<queue>` header to use it.

```cpp
#include <iostream>
#include <queue>

int main() {
    std::queue<int> myQueue;
    return 0;
}
```

#### Adding Elements to the Queue

You can add elements to the back of the queue using the `push()` method.

```cpp
myQueue.push(10);
myQueue.push(20);
myQueue.push(30);
```

#### Removing Elements from the Queue

You can remove elements from the front of the queue using the `pop()` method.

```cpp
myQueue.pop();
```

#### Accessing the Front Element

You can access the front element of the queue using the `front()` method.

```cpp
std::cout << "Front element: " << myQueue.front() << std::endl;
```

#### Checking if the Queue is Empty

You can check if the queue is empty using the `empty()` method.

```cpp
if (!myQueue.empty()) {
    // Queue is not empty
}
```

#### Getting the Size of the Queue

You can get the size of the queue using the `size()` method.

```cpp
std::cout << "Queue size: " << myQueue.size() << std::endl;
```

#### Iterating Over the Queue

You can't directly iterate over the queue like a standard container, but you can copy it to another container and then iterate over it.

```cpp
std::queue<int> tempQueue = myQueue;
while (!tempQueue.empty()) {
    std::cout << tempQueue.front() << " ";
    tempQueue.pop();
}
std::cout << std::endl;
```

#### Clearing the Queue

You can clear the queue using the `queue.swap(queue())` trick.

```cpp
std::queue<int>().swap(myQueue);
```

#### Full Example

```cpp
#include <iostream>
#include <queue>

int main() {
    std::queue<int> myQueue;

    myQueue.push(10);
    myQueue.push(20);
    myQueue.push(30);

    std::cout << "Front element: " << myQueue.front() << std::endl;

    myQueue.pop();

    if (!myQueue.empty()) {
        std::cout << "Queue size: " << myQueue.size() << std::endl;

        std::queue<int> tempQueue = myQueue;
        while (!tempQueue.empty()) {
            std::cout << tempQueue.front() << " ";
            tempQueue.pop();
        }
        std::cout << std::endl;
    }

    std::queue<int>().swap(myQueue); // Clearing the queue

    return 0;
}
```

This is just a basic overview. There are more advanced operations and use cases for queues in C++, but these are the fundamental operations you'll commonly use.

### 1. Algorithms & Data Structures (C++): Max Subarray (Sliding Window + Deque)

Certainly! Implementing the maximum subarray problem using the sliding window technique along with a deque (double-ended queue) in C++ can be an efficient approach. Here's a sample implementation:

```cpp
#include <iostream>
#include <vector>
#include <deque>

using namespace std;

vector<int> maxSubarray(vector<int>& nums, int k) {
    vector<int> result;
    if (nums.empty() || k <= 0 || k > nums.size()) return result;

    deque<int> dq;
    for (int i = 0; i < nums.size(); ++i) {
        // Remove elements from the front of the deque if they are out of the current window
        if (!dq.empty() && dq.front() == i - k)
            dq.pop_front();

        // Remove elements from the back of the deque if they are smaller than the current element
        while (!dq.empty() && nums[i] >= nums[dq.back()])
            dq.pop_back();

        dq.push_back(i);

        // Add the maximum element of the current window to the result vector
        if (i >= k - 1)
            result.push_back(nums[dq.front()]);
    }
    return result;
}

int main() {
    vector<int> nums = {1, 3, -1, -3, 5, 3, 6, 7};
    int k = 3;

    vector<int> result = maxSubarray(nums, k);

    cout << "Maximum subarray elements for each window of size " << k << ":" << endl;
    for (int num : result)
        cout << num << " ";
    cout << endl;

    return 0;
}
```

This code finds the maximum subarray elements for each window of size `k` using a deque. It iterates through the array, maintaining a sliding window of size `k`. At each step, it updates the deque to contain only elements within the current window that might be the maximum. The maximum element of each window is then pushed into the result vector.

You can adjust the input array `nums` and the window size `k` in the `main` function to test different scenarios.

### 1. Algorithms & Data Structures (C++): Member functions of Queue

In C++, when implementing a queue data structure, you typically have member functions that allow you to manipulate the queue, such as enqueueing elements, dequeueing elements, checking if the queue is empty, and accessing the front element without dequeuing it. Here's a basic example of what these member functions might look like:

```cpp
#include <iostream>
#include <queue>

using namespace std;

class Queue {
private:
    queue<int> q;

public:
    // Function to add an element to the queue
    void enqueue(int value) {
        q.push(value);
    }

    // Function to remove an element from the queue
    void dequeue() {
        if (!q.empty()) {
            q.pop();
        } else {
            cout << "Queue is empty. Cannot dequeue." << endl;
        }
    }

    // Function to check if the queue is empty
    bool isEmpty() {
        return q.empty();
    }

    // Function to get the front element of the queue without removing it
    int front() {
        if (!q.empty()) {
            return q.front();
        } else {
            cout << "Queue is empty. No front element." << endl;
            return -1; // Return a default value indicating empty queue
        }
    }

    // Function to get the size of the queue
    int size() {
        return q.size();
    }
};

int main() {
    Queue myQueue;

    myQueue.enqueue(10);
    myQueue.enqueue(20);
    myQueue.enqueue(30);

    cout << "Front element: " << myQueue.front() << endl;
    cout << "Queue size: " << myQueue.size() << endl;

    myQueue.dequeue();
    cout << "Front element after dequeue: " << myQueue.front() << endl;
    cout << "Queue size after dequeue: " << myQueue.size() << endl;

    myQueue.dequeue();
    myQueue.dequeue();

    cout << "Is the queue empty? " << (myQueue.isEmpty() ? "Yes" : "No") << endl;

    return 0;
}
```

This code demonstrates the basic functionalities of a queue: enqueue, dequeue, isEmpty, front, and size. You can build upon this by adding more functionalities or modifying it as per your requirements.

### 1. Algorithms & Data Structures (C++): More on Queue From Stack

Certainly! Implementing a queue using stacks is a classic exercise in data structures. In C++, you can achieve this by using two stacks. Here's how you can do it:

```cpp
#include <iostream>
#include <stack>

using namespace std;

class Queue {
private:
    stack<int> inbox;  // For enqueue operation
    stack<int> outbox; // For dequeue operation

public:
    // Function to enqueue an element to the queue
    void enqueue(int element) {
        inbox.push(element);
    }

    // Function to dequeue an element from the queue
    int dequeue() {
        if (outbox.empty()) {
            // If outbox is empty, transfer elements from inbox to outbox
            while (!inbox.empty()) {
                outbox.push(inbox.top());
                inbox.pop();
            }
        }

        // Pop the top element from outbox
        if (!outbox.empty()) {
            int front = outbox.top();
            outbox.pop();
            return front;
        } else {
            // If both stacks are empty, queue is empty
            cout << "Queue is empty!" << endl;
            return -1; // You can handle this situation differently based on your needs
        }
    }

    // Function to check if the queue is empty
    bool isEmpty() {
        return inbox.empty() && outbox.empty();
    }
};

int main() {
    Queue q;

    // Enqueue some elements
    q.enqueue(1);
    q.enqueue(2);
    q.enqueue(3);

    // Dequeue elements
    cout << q.dequeue() << endl; // Should print 1
    cout << q.dequeue() << endl; // Should print 2

    // Enqueue more elements
    q.enqueue(4);
    q.enqueue(5);

    // Dequeue remaining elements
    cout << q.dequeue() << endl; // Should print 3
    cout << q.dequeue() << endl; // Should print 4
    cout << q.dequeue() << endl; // Should print 5

    // Try to dequeue when queue is empty
    cout << q.dequeue() << endl; // Should print "Queue is empty!"

    return 0;
}
```

In this implementation:

* We have two stacks: `inbox` and `outbox`.
* `inbox` is used for the enqueue operation, and `outbox` is used for the dequeue operation.
* When we dequeue an element, if the `outbox` is empty, we transfer all elements from `inbox` to `outbox`. This way, the oldest element enqueued in the queue becomes the top element in the `outbox`.
* We keep dequeuing from the `outbox` until it's empty. If both `inbox` and `outbox` are empty, we consider the queue empty.

### 1. Algorithms & Data Structures (C++): Moving rear and front in Circular Queue

In C++, implementing a circular queue involves managing the front and rear pointers appropriately. Here's a basic implementation that demonstrates how to move the rear and front pointers in a circular queue:

```cpp
#include <iostream>
using namespace std;

#define SIZE 5

class CircularQueue {
private:
    int items[SIZE], front, rear;

public:
    CircularQueue() {
        front = -1;
        rear = -1;
    }

    // Check if the queue is full
    bool isFull() {
        if ((front == 0 && rear == SIZE - 1) || (rear == (front - 1) % (SIZE - 1)))
            return true;
        return false;
    }

    // Check if the queue is empty
    bool isEmpty() {
        if (front == -1)
            return true;
        return false;
    }

    // Add an element to the queue
    void enQueue(int element) {
        if (isFull()) {
            cout << "Queue is full" << endl;
        } else {
            if (front == -1)
                front = 0;
            rear = (rear + 1) % SIZE;
            items[rear] = element;
            cout << element << " enqueued to the queue." << endl;
        }
    }

    // Remove an element from the queue
    int deQueue() {
        int element;
        if (isEmpty()) {
            cout << "Queue is empty." << endl;
            return -1;
        } else {
            element = items[front];
            if (front == rear) {
                front = -1;
                rear = -1;
            } else {
                front = (front + 1) % SIZE;
            }
            return element;
        }
    }

    // Display the queue
    void display() {
        int i;
        if (isEmpty()) {
            cout << "Queue is empty." << endl;
        } else {
            cout << "Front: " << front << endl;
            cout << "Items: ";
            for (i = front; i != rear; i = (i + 1) % SIZE)
                cout << items[i] << " ";
            cout << items[i] << endl;
            cout << "Rear: " << rear << endl;
        }
    }
};

int main() {
    CircularQueue q;

    // Adding elements to the queue
    q.enQueue(1);
    q.enQueue(2);
    q.enQueue(3);
    q.enQueue(4);
    q.enQueue(5);

    // Display the queue
    q.display();

    // Removing elements from the queue
    cout << "Dequeued item: " << q.deQueue() << endl;
    cout << "Dequeued item: " << q.deQueue() << endl;

    // Display the queue
    q.display();

    // Adding more elements after dequeuing
    q.enQueue(6);
    q.enQueue(7);

    // Display the queue
    q.display();

    return 0;
}
```

This code creates a circular queue with a fixed size of 5. The `enQueue` function adds elements to the queue, and the `deQueue` function removes elements. The front and rear pointers are adjusted accordingly to make the queue circular.

### 1. Algorithms & Data Structures (C++): Printing all the Elements of a Queue

Certainly! In C++, you can print all the elements of a queue by dequeuing each element until the queue becomes empty. Here's a simple example:

```cpp
#include <iostream>
#include <queue>

using namespace std;

// Function to print all elements of a queue
void printQueue(queue<int> q) {
    while (!q.empty()) {
        cout << q.front() << " ";
        q.pop();
    }
    cout << endl;
}

int main() {
    // Create a queue
    queue<int> myQueue;

    // Push some elements into the queue
    myQueue.push(10);
    myQueue.push(20);
    myQueue.push(30);
    myQueue.push(40);
    myQueue.push(50);

    // Print all elements of the queue
    cout << "Elements of the queue: ";
    printQueue(myQueue);

    return 0;
}
```

In this example, the `printQueue` function takes a queue as a parameter and prints all its elements. It does so by repeatedly dequeuing elements until the queue becomes empty, printing each element as it goes. Finally, in the `main` function, we create a queue, push some elements into it, and then call `printQueue` to print all the elements.

### 1. Algorithms & Data Structures (C++): Priority Queue

A priority queue is a fundamental data structure in computer science that manages a set of elements each associated with a priority. It allows for efficient access to the element with the highest (or lowest) priority. In C++, the `std::priority_queue` is available in the Standard Template Library (STL) to implement a priority queue.

Here's a basic example of how to use `std::priority_queue` in C++:

```cpp
#include <iostream>
#include <queue>

int main() {
    // Create a priority queue of integers
    std::priority_queue<int> pq;

    // Insert elements into the priority queue
    pq.push(10);
    pq.push(30);
    pq.push(20);

    // Access the top element (highest priority)
    std::cout << "Top element: " << pq.top() << std::endl;

    // Remove the top element
    pq.pop();

    // Access the new top element
    std::cout << "Top element after pop: " << pq.top() << std::endl;

    // Check if the priority queue is empty
    if (pq.empty())
        std::cout << "Priority queue is empty\n";
    else
        std::cout << "Priority queue is not empty\n";

    // Get the size of the priority queue
    std::cout << "Size of priority queue: " << pq.size() << std::endl;

    return 0;
}
```

In this example:

* `std::priority_queue<int>` creates a priority queue of integers. You can specify the type of the elements inside the angle brackets (`<>`).
* `pq.push(value)` inserts an element into the priority queue.
* `pq.top()` returns the top element (element with the highest priority) without removing it.
* `pq.pop()` removes the top element from the priority queue.
* `pq.empty()` checks if the priority queue is empty.
* `pq.size()` returns the number of elements in the priority queue.

You can also define your own comparison function for custom priorities or use a custom data type with its own comparison function. For example:

```cpp
#include <iostream>
#include <queue>

struct CustomType {
    int value;
    // Define a comparison function for CustomType
    bool operator<(const CustomType& other) const {
        return value < other.value; // Change < to > for min priority queue
    }
};

int main() {
    // Create a priority queue of CustomType
    std::priority_queue

```cpp


```cpp
    <CustomType> pq;

    // Insert elements into the priority queue
    pq.push({10});
    pq.push({30});
    pq.push({20});

    // Access the top element (highest priority)
    std::cout << "Top element: " << pq.top().value << std::endl;

    // Remove the top element
    pq.pop();

    // Access the new top element
    std::cout << "Top element after pop: " << pq.top().value << std::endl;

    return 0;
}
```

In this example, `CustomType` is a custom data type with an integer value. We overload the `<` operator to define the comparison based on the `value` member variable. This allows us to use `CustomType` with `std::priority_queue`, and the priority queue will be ordered based on the `value` of each element.

### 1. Algorithms & Data Structures (C++): Priority Queue Problems

Sure, priority queues are an essential data structure in computer science, often implemented using heaps. They are commonly used in algorithms like Dijkstra's shortest path algorithm and Prim's minimum spanning tree algorithm, among others. Here are a few classic problems that you can solve using priority queues in C++:

1. **Merge K Sorted Lists**:
   Given K sorted lists, merge them into one sorted list. You can use a priority queue to efficiently merge them.

2. **Top K Frequent Elements**:
   Given an array of integers, return the K most frequent elements. You can use a priority queue to keep track of the frequency of elements.

3. **Kth Largest Element in an Array**:
   Given an unsorted array of integers, find the Kth largest element. You can use a min-heap to efficiently find the Kth largest element.

4. **Find Median from Data Stream**:
   Design a data structure that supports adding integers to the data structure and finding the median of the elements currently present. You can use two priority queues, one for the smaller half of the elements (max-heap) and one for the larger half (min-heap).

5. **Task Scheduler**:
   Given a sequence of tasks represented by characters, each task could be done in one interval. You need to find the minimum time to finish all the tasks, given a non-negative integer n, which represents the cooldown interval between two same tasks. You can use a priority queue to schedule the tasks efficiently.

6. **Huffman Coding**:
   Huffman coding is a method used for lossless data compression. Given a set of characters and their frequencies, build a Huffman tree and generate the Huffman codes for each character. Priority queues are used to build the Huffman tree efficiently.

7. **Super Ugly Number**:
   Write a program to find the nth super ugly number. Super ugly numbers are positive numbers whose all prime factors are in the given prime list primes of size k. You can use a priority queue to generate super ugly numbers efficiently.

These are just a few examples of problems that can be solved using priority queues in C++. Each of these problems requires understanding the priority queue operations like insertion, deletion, and accessing the top element efficiently.

### 1. Algorithms & Data Structures (C++): Priority Queue STL

A priority queue is a data structure that maintains a set of elements, each associated with a priority. Its primary operations are inserting an element with a priority, and extracting the element with the highest priority. In C++, you can use the Standard Template Library (STL) `priority_queue` to implement a priority queue efficiently. Here's how you can use it:

```cpp
#include <iostream>
#include <queue>

using namespace std;

int main() {
    // Define a priority queue of integers
    priority_queue<int> pq;

    // Insert elements into the priority queue
    pq.push(30);
    pq.push(10);
    pq.push(50);
    pq.push(20);

    // Print the elements of the priority queue
    cout << "Priority Queue elements: ";
    while (!pq.empty()) {
        cout << pq.top() << " ";
        pq.pop();
    }
    cout << endl;

    return 0;
}
```

Output:

```bash
Priority Queue elements: 50 30 20 10
```

By default, `priority_queue` is implemented as a max heap, where the element with the highest value is at the top. If you want to use a min heap instead, where the element with the lowest value is at the top, you can define your priority queue like this:

```cpp
priority_queue<int, vector<int>, greater<int>> pq;
```

Here's a breakdown of the template parameters:

* `int`: The data type of the elements.
* `vector<int>`: The underlying container used to store the elements. In this case, a vector is used, but you can also use other containers like `deque`.
* `greater<int>`: The comparison function used to determine the priority. `greater<int>` creates a min heap, while the default `less<int>` creates a max heap.

You can also customize the priority queue by providing your own comparison function.

### 1. Algorithms & Data Structures (C++): Priority Queue: Different Algorithms

Certainly! Priority queues are a fundamental data structure in computer science, used to manage a collection of elements with associated priorities. They are particularly useful when you need to retrieve elements in order of priority rather than in the order they were inserted. In C++, you typically implement priority queues using the `std::priority_queue` container from the Standard Template Library (STL).

Here are some common algorithms and operations involving priority queues:

1. **Insertion**: Adding an element with a priority to the priority queue. This operation typically has a time complexity of O(log n), where n is the number of elements in the priority queue.

2. **Extraction**: Removing and returning the element with the highest priority (or lowest priority, depending on the implementation). This operation also has a time complexity of O(log n).

3. **Heapify**: Converting an array of elements into a heap structure. This operation can be done in linear time, O(n), using algorithms such as heapify or build_heap.

4. **Merging**: Combining two priority queues into one. This operation generally requires merging the underlying heaps, which can be done in O(n) time.

5. **Changing Priority**: Modifying the priority of an element already in the priority queue. This operation can be tricky and often involves removing the element and re-inserting it with the new priority, which can take O(n) time in the worst case.

6. **Top k Elements**: Retrieving the top k elements with the highest (or lowest) priority. This can be done by extracting elements one by one until you have the desired number.

7. **Heap Sort**: Using a priority queue to sort elements. You can insert all elements into the priority queue and then extract them one by one, which sorts them in the desired order. This approach has a time complexity of O(n log n).

8. **Dijkstra's Algorithm**: A famous graph traversal algorithm that uses a priority queue to greedily select the next vertex to explore based on the shortest known distance. This algorithm is commonly used to find the shortest path between nodes in a graph with non-negative edge weights.

9. **Prim's Algorithm**: Another graph algorithm similar to Dijkstra's, but used for finding the minimum spanning tree of a graph. It also utilizes a priority queue to greedily select the next edge to include in the tree.

These are just a few examples of algorithms and operations involving priority queues. They are incredibly versatile and have applications in various fields, including operating systems, networking, and computational biology, among others.

### 1. Algorithms & Data Structures (C++): Priority Queue: Immutable and Concurrent Collections

In C++, implementing immutable and concurrent priority queues can be a bit challenging due to the language's lack of built-in support for immutability and concurrency. However, it's definitely achievable with some effort and careful design.

### Immutable Priority Queue

An immutable data structure doesn't allow modification of its contents after creation. You can implement an immutable priority queue by ensuring that all operations return a new priority queue object instead of modifying the existing one. You can do this by using copy-on-write techniques or persistent data structures.

Here's a basic outline of how you might implement an immutable priority queue in C++:

```cpp
template<typename T, typename Compare = std::less<T>>
class ImmutablePriorityQueue {
private:
    std::priority_queue<T, std::vector<T>, Compare> data;

public:
    ImmutablePriorityQueue() = default;

    ImmutablePriorityQueue(std::initializer_list<T> init) : data(init) {}

    ImmutablePriorityQueue push(const T& value) const {
        ImmutablePriorityQueue<T, Compare> newQueue(*this);
        newQueue.data.push(value);
        return newQueue;
    }

    ImmutablePriorityQueue pop() const {
        ImmutablePriorityQueue<T, Compare> newQueue(*this);
        newQueue.data.pop();
        return newQueue;
    }

    const T& top() const {
        return data.top();
    }

    bool empty() const {
        return data.empty();
    }

    // Other methods like size(), clear(), etc.
};
```

### Concurrent Priority Queue

Implementing a concurrent priority queue requires synchronization mechanisms to ensure thread safety. You can use mutexes or atomic operations to achieve this. Here's a basic example using mutexes:

```cpp
#include <queue>
#include <mutex>
#include <condition_variable>

template<typename T, typename Compare = std::less<T>>
class ConcurrentPriorityQueue {
private:
    std::priority_queue<T, std::vector<T>, Compare> data;
    mutable std::mutex mutex;
    std::condition_variable cv;

public:
    ConcurrentPriorityQueue() = default;

    void push(const T& value) {
        std::lock_guard<std::mutex> lock(mutex);
        data.push(value);
        cv.notify_one();
    }

    T pop() {
        std::unique_lock<std::mutex> lock(mutex);
        cv.wait(lock, [this] { return !data.empty(); });
        T value = data.top();
        data.pop();
        return value;
    }

    const T& top() const {
        std::lock_guard<std::mutex> lock(mutex);
        return data.top();
    }

    bool empty() const {
        std::lock_guard<std::mutex> lock(mutex);
        return data.empty();
    }

    // Other methods like size(), clear(), etc.
};
```

This implementation uses a mutex to guard access to the underlying data structure, ensuring that only one thread can modify it at a time. The condition variable (`cv`) is used to signal waiting threads when the queue is not empty, allowing them to proceed.

Keep in mind that these implementations are basic and may need enhancements depending on your specific requirements, especially for concurrent data structures where correctness and performance are critical. Also, consider using existing libraries like Intel TBB or Boost for more robust concurrent data structures if they fit your project requirements.

### 1. Algorithms & Data Structures (C++): Priority Queue: Implementation - Insert

Certainly! A priority queue is a data structure similar to a regular queue or stack data structure, but with each element assigned a priority. In C++, you can implement a priority queue using a variety of underlying data structures, such as a heap. Here's a basic implementation of a priority queue using a binary heap:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class PriorityQueue {
private:
    vector<int> heap;

    // Helper function to maintain heap property after insertion
    void heapifyUp(int index) {
        int parent = (index - 1) / 2;
        while (index > 0 && heap[index] > heap[parent]) {
            swap(heap[index], heap[parent]);
            index = parent;
            parent = (index - 1) / 2;
        }
    }

public:
    // Constructor
    PriorityQueue() {}

    // Insert element into the priority queue
    void insert(int value) {
        heap.push_back(value);
        heapifyUp(heap.size() - 1);
    }

    // Utility function to print the priority queue
    void print() {
        for (int i = 0; i < heap.size(); ++i) {
            cout << heap[i] << " ";
        }
        cout << endl;
    }
};

int main() {
    PriorityQueue pq;

    // Insert elements into the priority queue
    pq.insert(10);
    pq.insert(20);
    pq.insert(15);
    pq.insert(30);
    pq.insert(5);

    // Print the priority queue
    pq.print();

    return 0;
}
```

In this implementation:

* We use a `vector` to store the elements of the priority queue. This allows us to easily resize the underlying array as needed.
* The `heapifyUp` function is used to maintain the heap property after inserting an element into the priority queue. It compares the inserted element with its parent and swaps them if necessary to restore the heap property.
* The `insert` function inserts a new element into the priority queue by appending it to the end of the `vector` and then calling `heapifyUp` to restore the heap property.
* The `print` function is a utility function to print the elements of the priority queue.

You can run this code to see how elements are inserted into the priority queue and how the heap property is maintained.

### 1. Algorithms & Data Structures (C++): Priority Queue: Insert

Certainly! In C++, you can use the `priority_queue` container provided by the Standard Template Library (STL) to implement a priority queue. To insert elements into a priority queue, you typically use the `push()` member function.

Here's a basic example demonstrating how to insert elements into a `priority_queue`:

```cpp
#include <iostream>
#include <queue>

int main() {
    // Define a priority queue of integers
    std::priority_queue<int> pq;

    // Insert elements into the priority queue
    pq.push(10);
    pq.push(30);
    pq.push(20);

    // Display the elements of the priority queue
    std::cout << "Priority Queue elements: ";
    while (!pq.empty()) {
        std::cout << pq.top() << " ";
        pq.pop();
    }
    std::cout << std::endl;

    return 0;
}
```

In this example:

* We include the necessary headers (`iostream` and `queue`).
* We declare a priority queue `pq` of integers.
* We insert elements into the priority queue using the `push()` member function.
* Finally, we display the elements of the priority queue by repeatedly popping elements using `top()` to get the highest priority element and `pop()` to remove it.

This code will output:

```bash
Priority Queue elements: 30 20 10
```

This demonstrates that the priority queue maintains the elements in descending order based on their priority.

### 1. Algorithms & Data Structures (C++): Priority Queue: Insert Function

In C++, you can implement a priority queue using the `priority_queue` container provided by the Standard Template Library (STL). The `priority_queue` is implemented as a heap, which allows for efficient insertion, removal, and retrieval of the maximum (or minimum) element.

Here's how you can implement the insert function for a priority queue in C++:

```cpp
#include <iostream>
#include <queue>

using namespace std;

// Function to insert an element into the priority queue
template<typename T>
void insertIntoPriorityQueue(priority_queue<T>& pq, const T& element) {
    pq.push(element);
}

int main() {
    // Example usage
    priority_queue<int> pq; // Creating a priority queue of integers

    // Inserting elements into the priority queue
    insertIntoPriorityQueue(pq, 10);
    insertIntoPriorityQueue(pq, 5);
    insertIntoPriorityQueue(pq, 20);
    insertIntoPriorityQueue(pq, 15);

    // Printing elements of the priority queue
    cout << "Priority Queue elements: ";
    while (!pq.empty()) {
        cout << pq.top() << " ";
        pq.pop();
    }
    cout << endl;

    return 0;
}
```

In this example:

* We define a function `insertIntoPriorityQueue` that takes a reference to a `priority_queue` and the element to be inserted.
* Inside the function, we simply use the `push` function of the `priority_queue` to insert the element.
* In the `main` function, we create a `priority_queue` of integers and insert some elements into it using the `insertIntoPriorityQueue` function.
* Finally, we print the elements of the priority queue by repeatedly popping elements from it.

This demonstrates the basic usage of inserting elements into a priority queue in C++.

### 1. Algorithms & Data Structures (C++): Priority Queue: Nearby Cars

Using a priority queue in C++ for managing nearby cars is a common scenario, especially in applications like ride-sharing services or autonomous vehicle navigation systems. The priority queue can be used to efficiently retrieve the nearest cars based on their distance from a given location. Here's a basic implementation:

```cpp
#include <iostream>
#include <queue>
#include <cmath>

using namespace std;

// Define a structure to represent a car
struct Car {
    int id;
    double x, y; // Coordinates of the car
    // Constructor
    Car(int _id, double _x, double _y) : id(_id), x(_x), y(_y) {}
    // Function to calculate distance between two cars
    double distance(const Car& other) const {
        return sqrt(pow(x - other.x, 2) + pow(y - other.y, 2));
    }
};

// Custom comparator for comparing cars based on their distance from a given location
struct CompareCars {
    Car reference_point;
    CompareCars(const Car& ref) : reference_point(ref) {}
    bool operator()(const Car& a, const Car& b) const {
        return a.distance(reference_point) > b.distance(reference_point);
    }
};

int main() {
    // Define the reference point
    Car reference_point(0, 0, 0); // Assuming reference point is at (0, 0)

    // Priority queue of cars, ordered by distance from the reference point
    priority_queue<Car, vector<Car>, CompareCars> nearby_cars(CompareCars(reference_point));

    // Adding some cars to the priority queue
    nearby_cars.push(Car(1, 3, 4));
    nearby_cars.push(Car(2, -1, 2));
    nearby_cars.push(Car(3, 5, 1));
    nearby_cars.push(Car(4, -2, -3));
    nearby_cars.push(Car(5, 0, 0));

    // Retrieve the nearest car
    Car nearest_car = nearby_cars.top();
    cout << "Nearest car ID: " << nearest_car.id << ", Distance: " << nearest_car.distance(reference_point) << endl;

    return 0;
}
```

In this implementation:

* We define a `Car` structure to represent each car, storing its ID and coordinates (x, y).
* We define a custom comparator `CompareCars` to compare cars based on their distance from a reference point.
* We use a priority queue of cars, with the custom comparator `CompareCars`, to store nearby cars ordered by their distance from the reference point.
* We add some cars to the priority queue and retrieve the nearest car using the `top()` function of the priority queue.

You can adapt this code to your specific requirements, such as using real-time location updates for cars or integrating it into a larger application.

### 1. Algorithms & Data Structures (C++): Priority Queue: Reduced array size to half

Reducing the size of a priority queue (or any dynamic array-based data structure) to half its capacity typically involves creating a new array with half the size and copying elements from the old array to the new one. In C++, you can achieve this by using dynamic memory allocation and the `std::copy` algorithm. Here's a basic example of how you might implement this operation for a priority queue:

```cpp
#include <iostream>
#include <algorithm> // for std::copy

template <typename T>
class PriorityQueue {
private:
    T* array;
    size_t capacity;
    size_t size;

    void resize(size_t newCapacity) {
        T* newArray = new T[newCapacity];
        std::copy(array, array + size, newArray);
        delete[] array;
        array = newArray;
        capacity = newCapacity;
    }

public:
    PriorityQueue() : array(nullptr), capacity(0), size(0) {}

    void push(const T& value) {
        // Check if resize is needed before pushing
        if (size + 1 > capacity) {
            resize(capacity == 0 ? 1 : capacity * 2);
        }
        // Push value into the priority queue
        // (not implemented in this example)
    }

    void pop() {
        // Pop the top element from the priority queue
        // (not implemented in this example)
    }

    // Other member functions...

    ~PriorityQueue() {
        delete[] array;
    }
};

int main() {
    // Example usage
    PriorityQueue<int> pq;
    pq.push(5);
    pq.push(10);
    pq.push(3);
    pq.push(8);
    // Perform some operations...

    return 0;
}
```

In this example:

* The `resize` function doubles the capacity of the array when needed.
* The `push` function checks if the array needs resizing before adding an element.
* `std::copy` is used to copy elements from the old array to the new array during resizing.
* The destructor deallocates the dynamically allocated memory.

This is a basic implementation. Depending on your requirements, you might need additional functionalities like popping elements, peeking at the top element, or comparing elements for ordering.

### 1. Algorithms & Data Structures (C++): Priority Queue: Relative Ranks

Sure, I can help you with that! A priority queue is a data structure that stores elements in a way that allows for efficient retrieval of the highest (or lowest) priority element. In C++, you can implement a priority queue using the `std::priority_queue` container from the `<queue>` header.

To assign relative ranks to elements in a priority queue, you typically need to perform some operations when inserting elements or when retrieving them. Here's how you could implement a priority queue with relative ranks in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <unordered_map>
#include <algorithm>

using namespace std;

// Function to assign relative ranks to elements
vector<string> findRelativeRanks(vector<int>& nums) {
    // Create a copy of nums to keep track of original positions
    vector<int> sorted_nums = nums;
    sort(sorted_nums.rbegin(), sorted_nums.rend()); // Sort in descending order

    // Map to store the original position of each number
    unordered_map<int, int> position_map;
    for (int i = 0; i < sorted_nums.size(); ++i) {
        position_map[sorted_nums[i]] = i + 1;
    }

    // Vector to store result ranks
    vector<string> result(nums.size());

    // Assign ranks
    for (int i = 0; i < nums.size(); ++i) {
        int rank = position_map[nums[i]];
        if (rank == 1)
            result[i] = "Gold Medal";
        else if (rank == 2)
            result[i] = "Silver Medal";
        else if (rank == 3)
            result[i] = "Bronze Medal";
        else
            result[i] = to_string(rank);
    }

    return result;
}

int main() {
    vector<int> nums = {10, 3, 8, 9, 4};
    vector<string> ranks = findRelativeRanks(nums);
    
    cout << "Relative Ranks:" << endl;
    for (int i = 0; i < nums.size(); ++i) {
        cout << nums[i] << ": " << ranks[i] << endl;
    }
    
    return 0;
}
```

In this example, `findRelativeRanks` function takes a vector of integers `nums` as input and returns a vector of strings representing the relative ranks of the numbers. The ranks are assigned based on the sorted order of the numbers. The function first creates a sorted copy of the input vector and then creates a map to store the original position of each number in the sorted order. Then, it iterates through the input vector, looks up the rank of each number in the map, and assigns the appropriate rank string to the result vector. Finally, the main function demonstrates the usage of this function.

### 1. Algorithms & Data Structures (C++): Priority Queue: Remove Min & Complexity Analysis

In C++, removing the minimum element from a priority queue can be achieved using the `pop()` method. The `pop()` method removes the top element from the priority queue, which is the minimum (or maximum, depending on how you've configured the priority queue).

Here's a simple example of how you can remove the minimum element from a priority queue in C++:

```cpp
#include <iostream>
#include <queue>

int main() {
    std::priority_queue<int> pq;

    // Insert some elements into the priority queue
    pq.push(10);
    pq.push(20);
    pq.push(5);
    pq.push(15);

    // Remove the minimum element
    pq.pop();

    // Now the top element should be the next minimum
    std::cout << "Minimum element after removal: " << pq.top() << std::endl;

    return 0;
}
```

In terms of complexity analysis:

* Removing the minimum element from a priority queue implemented with a binary heap (the most common implementation) has a time complexity of O(log n), where n is the number of elements in the priority queue. This is because removing the minimum element involves rearranging the heap to maintain its heap property, which requires logarithmic time relative to the number of elements.

* The space complexity of removing the minimum element from a priority queue is O(1) because the operation doesn't require additional space proportional to the input size. The space complexity of the priority queue itself depends on its implementation, but typically it's O(n), where n is the number of elements in the priority queue.

### 1. Algorithms & Data Structures (C++): Priority Queue: Remove Min Solution & Complexity Analysis

Certainly! In C++, the `priority_queue` container from the Standard Template Library (STL) can be utilized to implement a priority queue. However, it doesn't provide a direct method to remove the minimum element. Instead, we typically simulate removal by accessing the top element (minimum element), popping it, and then reconstructing the priority queue without that element. Let's write a function to remove the minimum element from a `priority_queue` and analyze its complexity.

```cpp
#include <iostream>
#include <queue>
using namespace std;

// Function to remove the minimum element from a priority queue
template <typename T>
void removeMin(priority_queue<T>& pq) {
    // Create a temporary priority queue to hold elements
    priority_queue<T> temp;
    
    // Pop the top element (minimum element)
    pq.pop();
    
    // Transfer elements from original pq to temp, excluding the removed element
    while (!pq.empty()) {
        temp.push(pq.top());
        pq.pop();
    }
    
    // Transfer elements back to original pq from temp
    while (!temp.empty()) {
        pq.push(temp.top());
        temp.pop();
    }
}

int main() {
    // Example usage
    priority_queue<int> pq;
    pq.push(5);
    pq.push(2);
    pq.push(7);
    pq.push(1);
    
    cout << "Before removal: ";
    while (!pq.empty()) {
        cout << pq.top() << " ";
        pq.pop();
    }
    cout << endl;
    
    // Restore elements and remove minimum
    pq.push(5);
    pq.push(2);
    pq.push(7);
    pq.push(1);
    removeMin(pq);
    
    cout << "After removal: ";
    while (!pq.empty()) {
        cout << pq.top() << " ";
        pq.pop();
    }
    cout << endl;
    
    return 0;
}
```

This function `removeMin()` works as follows:

1. It pops the top (minimum) element from the priority queue.
2. It then transfers the remaining elements from the original priority queue to a temporary one, effectively excluding the removed minimum element.
3. After that, it transfers the elements back to the original priority queue from the temporary one.

Let's analyze the time complexity of this `removeMin()` function:

* Popping the top element from a priority queue takes O(log n) time complexity.
* Transferring elements from one priority queue to another takes O(n log n) time, where n is the number of elements in the priority queue.

So, the overall time complexity of the `removeMin()` function is O(n log n), where n is the number of elements in the priority queue.

### 1. Algorithms & Data Structures (C++): Priority Queue: Remove Minimum

In C++, you can implement a priority queue using the `priority_queue` container provided by the Standard Template Library (STL). However, `priority_queue` doesn't have a direct method to remove the minimum element. Typically, you would remove the top element, which is the minimum by default.

Here's a basic example demonstrating how to use `priority_queue` and remove the minimum element:

```cpp
#include <iostream>
#include <queue>

int main() {
    // Creating a priority queue of integers
    std::priority_queue<int> pq;

    // Inserting elements into the priority queue
    pq.push(10);
    pq.push(20);
    pq.push(15);
    pq.push(5);

    // Printing the elements of the priority queue
    std::cout << "Priority Queue elements: ";
    while (!pq.empty()) {
        std::cout << pq.top() << " ";
        pq.pop(); // Removing the top element (minimum)
    }
    std::cout << std::endl;

    return 0;
}
```

This code will output:

```bash
Priority Queue elements: 20 15 10 5
```

As you can see, the elements are printed in descending order because `priority_queue` is a max-heap by default. If you want to use a min-heap, you can specify the comparison function.

If you need to remove a specific minimum element, you might consider using a different data structure such as a set or a multiset, where you can iterate through and remove specific elements based on your criteria.

### 1. Algorithms & Data Structures (C++): Priority Queue: Sieve of Eratosthenes

The Sieve of Eratosthenes is a classic algorithm used to generate all prime numbers up to a given limit. It's an efficient way to find primes and is based on the principle of iteratively marking the multiples of each prime number starting from 2. Here's how you can implement the Sieve of Eratosthenes using C++ with a priority queue:

```cpp
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

void sieveOfEratosthenes(int n) {
    // Create a boolean vector "prime[0..n]" and initialize
    // all entries as true.
    vector<bool> prime(n + 1, true);

    // Create a priority queue to store the primes.
    priority_queue<int, vector<int>, greater<int>> pq;

    for (int p = 2; p * p <= n; ++p) {
        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {
            // Update all multiples of p
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Store primes in the priority queue
    for (int p = 2; p <= n; ++p)
        if (prime[p])
            pq.push(p);

    // Print the primes in ascending order
    while (!pq.empty()) {
        cout << pq.top() << " ";
        pq.pop();
    }
    cout << endl;
}

int main() {
    int n;
    cout << "Enter the upper limit for prime numbers: ";
    cin >> n;

    cout << "Prime numbers up to " << n << " are:\n";
    sieveOfEratosthenes(n);

    return 0;
}
```

This C++ code uses a boolean vector `prime` to mark whether a number is prime or not. It iterates through the numbers, marking multiples of each prime number as not prime. Finally, it stores the primes found in a priority queue and prints them out in ascending order.

### 1. Algorithms & Data Structures (C++): Priority Queue: Weakest Rows

To implement a priority queue for the "Weakest Rows" problem, you'll need a way to prioritize rows based on their strength. In this problem, the strength of a row is defined as the number of soldiers in it. We can use a min-heap to store pairs of (strength, index), where strength is the number of soldiers and index is the row index. This way, when we pop from the priority queue, we'll get the row with the weakest soldiers first.

Here's a basic outline of how you can implement this in C++:

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <utility>

using namespace std;

vector<int> kWeakestRows(vector<vector<int>>& mat, int k) {
    // Priority queue to store pairs of (strength, index)
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    
    // Iterate through each row, calculate strength and push into the priority queue
    for (int i = 0; i < mat.size(); ++i) {
        int strength = 0;
        for (int j = 0; j < mat[i].size(); ++j) {
            strength += mat[i][j];
        }
        pq.push({strength, i});
    }
    
    // Extract the k weakest rows from the priority queue
    vector<int> result;
    while (k-- > 0 && !pq.empty()) {
        result.push_back(pq.top().second);
        pq.pop();
    }
    
    return result;
}

int main() {
    vector<vector<int>> mat = {
        {1, 1, 0, 0, 0},
        {1, 1, 1, 1, 0},
        {1, 0, 0, 0, 0},
        {1, 1, 0, 0, 0},
        {1, 1, 1, 1, 1}
    };
    int k = 3;
    
    vector<int> weakest = kWeakestRows(mat, k);
    
    cout << "The indices of the k weakest rows are: ";
    for (int idx : weakest) {
        cout << idx << " ";
    }
    cout << endl;
    
    return 0;
}
```

In this implementation, we first iterate through each row of the matrix, calculate its strength (i.e., the sum of elements), and push a pair of (strength, index) into the priority queue. Then, we pop the k weakest rows from the priority queue and return their indices.

### 1. Algorithms & Data Structures (C++): Priority Queues

Priority queues are a fundamental data structure in computer science, used to maintain a set of elements with associated priorities. They are often implemented as heaps due to their efficient insertion and removal operations.

In C++, you can use the `std::priority_queue` container provided by the Standard Template Library (STL) to implement a priority queue. Here's a basic overview of how to use it:

```cpp
#include <iostream>
#include <queue>

int main() {
    // Declaration of priority queue
    std::priority_queue<int> pq;

    // Inserting elements into the priority queue
    pq.push(30);
    pq.push(10);
    pq.push(50);
    pq.push(20);

    // Printing the top element (highest priority)
    std::cout << "Top element: " << pq.top() << std::endl;

    // Removing the top element
    pq.pop();

    // Printing the top element after removal
    std::cout << "Top element after removal: " << pq.top() << std::endl;

    // Checking if the priority queue is empty
    if (pq.empty()) {
        std::cout << "Priority queue is empty.\n";
    } else {
        std::cout << "Priority queue is not empty.\n";
    }

    // Size of the priority queue
    std::cout << "Size of priority queue: " << pq.size() << std::endl;

    return 0;
}
```

In this example, `std::priority_queue<int>` creates a priority queue of integers. You can change `int` to any other data type or define your own custom comparison function if you need to prioritize elements differently.

Key operations include:

* `push(value)`: Inserts an element into the priority queue.
* `pop()`: Removes the top element from the priority queue.
* `top()`: Accesses the top (highest priority) element in the priority queue.
* `empty()`: Checks if the priority queue is empty.
* `size()`: Returns the number of elements in the priority queue.

Priority queues are often used in algorithms like Dijkstra's shortest path algorithm, Prim's minimum spanning tree algorithm, and Huffman coding. They provide efficient access to the element with the highest priority, making them indispensable in many applications.

### 1. Algorithms & Data Structures (C++): Priority Queues (Heaps)

Priority queues are essential data structures in computer science, particularly for scenarios where elements need to be processed based on their priority. Heaps are commonly used to implement priority queues efficiently. Here's a brief overview of priority queues and heaps in the context of C++:

### Priority Queues

* **Definition**: A priority queue is an abstract data type similar to a regular queue or stack, but each element has an associated priority. Elements with higher priority are served before elements with lower priority.
  
* **Operations**:
  * **Insertion**: Adds an element with a priority to the queue.
  * **Deletion**: Removes the element with the highest priority from the queue.
  * **Peek**: Returns the element with the highest priority without removing it from the queue.
  
* **Implementation**: Priority queues can be implemented using various data structures, such as arrays, linked lists, binary heaps, or balanced binary search trees. Binary heaps are one of the most common implementations due to their efficiency.

### Heaps

* **Definition**: A heap is a binary tree-based data structure that satisfies the heap property. In a max heap, for any given node, the value of the node is greater than or equal to the values of its children. In a min heap, the value of the node is less than or equal to the values of its children.
  
* **Operations**:
  * **Insertion**: Adds a new element to the heap while maintaining the heap property.
  * **Deletion**: Removes the root node (the maximum or minimum value) from the heap and restores the heap property.
  * **Heapify**: Converts an array of elements into a heap.
  
* **Implementation**: Heaps are commonly implemented using arrays due to their compact representation. In a binary heap, the parent of the node at index \(i\) is at index \((i-1)/2\), and its children are at indices \(2i+1\) and \(2i+2\).

### C++ Implementation

C++ provides the `priority_queue` container adapter in the `<queue>` header, which implements a priority queue using a heap by default. You can also implement heaps from scratch using arrays or dynamic memory allocation.

Here's an example of using `priority_queue` in C++:

```cpp
#include <iostream>
#include <queue>

int main() {
    std::priority_queue<int> pq;
    
    pq.push(10);
    pq.push(30);
    pq.push(20);
    
    while (!pq.empty()) {
        std::cout << pq.top() << " ";
        pq.pop();
    }
    
    return 0;
}
```

This would output: `30 20 10`.

For more control or specific requirements, you may need to implement your heap or priority queue from scratch, especially if you need to customize the behavior or performance characteristics.

### 1. Algorithms & Data Structures (C++): Priority Queues & Heaps

Priority queues and heaps are fundamental data structures used in computer science and algorithm design, particularly for tasks that require efficient prioritization or ordering of elements. In C++, you can implement priority queues using the standard library's `priority_queue` container, which internally uses a heap data structure.

Here's an overview of priority queues and heaps in C++:

### Priority Queues

A priority queue is a type of container in which elements are popped based on their priority. Elements with higher priority are popped before elements with lower priority. Priority queues typically support operations like insertion and deletion of elements, as well as retrieval of the highest-priority element without removing it.

In C++, you can use the `priority_queue` container provided by the `<queue>` header.

**Example:**

```cpp
#include <queue>
#include <iostream>

int main() {
    std::priority_queue<int> pq;

    pq.push(10);
    pq.push(20);
    pq.push(5);

    std::cout << "Top element: " << pq.top() << std::endl;

    pq.pop();
    std::cout << "Top element after popping: " << pq.top() << std::endl;

    return 0;
}
```

### Heaps

A heap is a binary tree-based data structure that satisfies the heap property. In a max heap, the parent node is always greater than or equal to its children, and in a min heap, the parent node is always less than or equal to its children. Heaps are often implemented as arrays, where the parent-child relationships are determined by the indices of the array elements.

In C++, the `priority_queue` container typically uses a max heap, but you can implement your own heap data structure if you need more control.

**Example of a Max Heap:**

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

void heapify(std::vector<int>& arr, int n, int i) {
    int largest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;

    if (left < n && arr[left] > arr[largest])
        largest = left;

    if (right < n && arr[right] > arr[largest])
        largest = right;

    if (largest != i) {
        std::swap(arr[i], arr[largest]);
        heapify(arr, n, largest);
    }
}

void buildMaxHeap(std::vector<int>& arr) {
    int n = arr.size();
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);
}

int main() {
    std::vector<int> arr = {12, 11, 13, 5, 6, 7};
    buildMaxHeap(arr);

    std::cout << "Max Heap: ";
    for (int num : arr)
        std::cout << num << " ";
    std::cout << std::endl;

    return 0;
}
```

This code demonstrates building a max heap from an array. You can modify it for a min heap by changing the comparison logic.

Understanding priority queues and heaps is essential for various algorithms like Dijkstra's shortest path algorithm, Prim's minimum spanning tree algorithm, and efficient sorting algorithms like heap sort. They offer efficient insertion and removal of elements based on their priority, making them invaluable tools in algorithm design and optimization.

### 1. Algorithms & Data Structures (C++): priority queues: array representation

In C++, priority queues are typically implemented using heaps, particularly binary heaps. Binary heaps can be easily represented using arrays. Here's a basic explanation of how to represent a priority queue using an array in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class PriorityQueue {
private:
    vector<int> heap;

    // Helper functions
    int parent(int i) { return (i - 1) / 2; }
    int leftChild(int i) { return (2 * i) + 1; }
    int rightChild(int i) { return (2 * i) + 2; }

    // Rearranges elements to maintain heap property
    void heapifyUp(int i) {
        while (i > 0 && heap[parent(i)] < heap[i]) {
            swap(heap[parent(i)], heap[i]);
            i = parent(i);
        }
    }

    // Rearranges elements to maintain heap property
    void heapifyDown(int i) {
        int maxIndex = i;
        int left = leftChild(i);
        int right = rightChild(i);

        if (left < heap.size() && heap[left] > heap[maxIndex]) {
            maxIndex = left;
        }

        if (right < heap.size() && heap[right] > heap[maxIndex]) {
            maxIndex = right;
        }

        if (i != maxIndex) {
            swap(heap[i], heap[maxIndex]);
            heapifyDown(maxIndex);
        }
    }

public:
    // Inserts a new element into the priority queue
    void insert(int value) {
        heap.push_back(value);
        heapifyUp(heap.size() - 1);
    }

    // Removes and returns the maximum element (root) from the priority queue
    int extractMax() {
        if (heap.empty()) {
            throw out_of_range("Priority queue is empty");
        }

        int maxElement = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        heapifyDown(0);
        return maxElement;
    }

    // Returns the maximum element (root) from the priority queue without removing it
    int getMax() {
        if (heap.empty()) {
            throw out_of_range("Priority queue is empty");
        }
        return heap[0];
    }

    // Returns true if the priority queue is empty, false otherwise
    bool isEmpty() {
        return heap.empty();
    }
};

int main() {
    PriorityQueue pq;
    pq.insert(10);
    pq.insert(20);
    pq.insert(15);
    pq.insert(30);

    while (!pq.isEmpty()) {
        cout << pq.extractMax() << " ";
    }
    cout << endl;

    return 0;
}
```

This code demonstrates a basic implementation of a priority queue using a max-heap. The `PriorityQueue` class uses a vector to store elements, where each element is inserted into the appropriate position in the heap according to its priority. The `insert()` function inserts a new element into the heap while maintaining the heap property, the `extractMax()` function removes and returns the maximum element from the heap, and the `getMax()` function returns the maximum element without removing it.

### 1. Algorithms & Data Structures (C++): priority queues: basics

Sure, let's dive into the basics of priority queues in C++.

A priority queue is a data structure that manages a set of elements with priorities. The elements are stored in such a way that the element with the highest (or lowest) priority can be accessed quickly. Priority queues are commonly implemented using heaps, which are specialized binary trees.

In C++, the standard library provides the `priority_queue` class, which is a part of the `<queue>` header file. Here's how you can use it:

```cpp
#include <iostream>
#include <queue>

int main() {
    // Creating a priority queue of integers
    std::priority_queue<int> pq;

    // Inserting elements into the priority queue
    pq.push(30);
    pq.push(10);
    pq.push(50);
    pq.push(20);

    // Accessing the top element (highest priority)
    std::cout << "Top element: " << pq.top() << std::endl;

    // Removing the top element
    pq.pop();

    // Accessing the new top element
    std::cout << "Top element after pop: " << pq.top() << std::endl;

    return 0;
}
```

This code creates a priority queue of integers, inserts some elements into it, accesses the top element, removes the top element, and then accesses the new top element.

By default, the `priority_queue` is a max heap, which means the element with the highest value will be at the top. If you want to create a min heap (where the smallest element is at the top), you can specify a custom comparator function:

```cpp
#include <iostream>
#include <queue>

// Custom comparator function for min heap
struct Compare {
    bool operator()(int a, int b) {
        return a > b; // Returns true if a should go before b in the priority queue
    }
};

int main() {
    // Creating a priority queue of integers with custom comparator
    std::priority_queue<int, std::vector<int>, Compare> pq;

    // Inserting elements into the priority queue
    pq.push(30);
    pq.push(10);
    pq.push(50);
    pq.push(20);

    // Accessing the top element (highest priority)
    std::cout << "Top element: " << pq.top() << std::endl;

    // Removing the top element
    pq.pop();

    // Accessing the new top element
    std::cout << "Top element after pop: " << pq.top() << std::endl;

    return 0;
}
```

In this code, `Compare` is a struct defining the custom comparator function. The function returns true if `a` should go before `b` in the priority queue, effectively creating a min heap.

That's the basics of priority queues in C++ using the standard library. They are quite handy for tasks where you need to process elements in order of priority.

### 1. Algorithms & Data Structures (C++): priority queues: remove operation

In C++, priority queues don't typically support a direct remove operation like standard containers such as vectors or sets. However, you can achieve similar functionality by using other data structures in combination with the priority queue.

One common approach is to use an additional data structure, like a map or a set, to keep track of the elements' positions in the priority queue. Here's a simple example using a map:

```cpp
#include <iostream>
#include <queue>
#include <unordered_map>

using namespace std;

template<typename T>
class PriorityQueueWithRemove {
private:
    priority_queue<T> pq;
    unordered_map<T, int> index; // Maps element to its index in the priority queue

public:
    void push(const T& val) {
        pq.push(val);
        index[val] = pq.size(); // Index is 1-based
    }

    void remove(const T& val) {
        if (index.find(val) == index.end()) return; // Element not found

        int idx = index[val];
        index.erase(val);

        // Swap with the last element and pop
        if (idx != pq.size()) {
            T last = pq.top();
            pq.pop();
            pq.push(last);
            index[last] = idx;
        }
        pq.pop(); // Remove the duplicated last element
    }

    T top() const {
        return pq.top();
    }

    bool empty() const {
        return pq.empty();
    }

    size_t size() const {
        return pq.size();
    }
};

int main() {
    PriorityQueueWithRemove<int> pq;
    pq.push(3);
    pq.push(5);
    pq.push(1);
    pq.push(7);

    cout << "Current top: " << pq.top() << endl; // Should print 7

    pq.remove(5); // Remove element 5

    cout << "After removal, new top: " << pq.top() << endl; // Should print 7

    return 0;
}
```

In this implementation, the `index` map keeps track of the index of each element in the priority queue. When removing an element, it swaps the element with the last one in the queue and then pops it. This approach allows for a pseudo-removal operation with logarithmic complexity. Keep in mind that the actual removal might not be very efficient compared to direct removal in other data structures.

### 1. Algorithms & Data Structures (C++): Queue

A queue is a fundamental data structure in computer science that follows the First In, First Out (FIFO) principle. This means that the first element added to the queue will be the first one to be removed. Think of it like a queue at a ticket counter; the person who arrives first is served first.

In C++, you can implement a queue using various methods. One common approach is to use the Standard Template Library (STL) `queue` container. Here's a simple example:

```cpp
#include <iostream>
#include <queue>

int main() {
    // Creating a queue of integers
    std::queue<int> myQueue;

    // Adding elements to the queue
    myQueue.push(10);
    myQueue.push(20);
    myQueue.push(30);

    // Accessing the front element of the queue
    std::cout << "Front element of the queue: " << myQueue.front() << std::endl;

    // Removing elements from the queue
    myQueue.pop();

    // Size of the queue
    std::cout << "Size of the queue: " << myQueue.size() << std::endl;

    // Checking if the queue is empty
    if (myQueue.empty()) {
        std::cout << "Queue is empty" << std::endl;
    } else {
        std::cout << "Queue is not empty" << std::endl;
    }

    return 0;
}
```

In this example:

* We include the necessary headers for `iostream` and `queue`.
* We create a queue called `myQueue` to store integers.
* We add elements to the queue using the `push()` method.
* We access the front element of the queue using the `front()` method.
* We remove an element from the front of the queue using the `pop()` method.
* We check the size of the queue using the `size()` method.
* We check if the queue is empty using the `empty()` method.

The `queue` container in C++ provides a convenient way to implement queues without having to manually manage memory allocation and deallocation.

### 1. Algorithms & Data Structures (C++): Queue - Enqueue

In C++, implementing the enqueue operation for a queue involves adding an element to the back of the queue. You can use various data structures like arrays, linked lists, or even doubly-linked lists to implement a queue. Here's a simple implementation of a queue using an array:

```cpp
#include <iostream>

#define MAX_SIZE 100

class Queue {
private:
    int arr[MAX_SIZE];
    int front;
    int rear;

public:
    Queue() {
        front = -1;
        rear = -1;
    }

    bool isEmpty() {
        return (front == -1 && rear == -1);
    }

    bool isFull() {
        return (rear + 1) % MAX_SIZE == front;
    }

    void enqueue(int value) {
        if (isFull()) {
            std::cout << "Queue is full. Cannot enqueue.\n";
            return;
        } else if (isEmpty()) {
            front = rear = 0;
        } else {
            rear = (rear + 1) % MAX_SIZE;
        }
        arr[rear] = value;
        std::cout << value << " enqueued to the queue.\n";
    }
};

int main() {
    Queue q;
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    q.enqueue(40);
    q.enqueue(50);
    q.enqueue(60); // Queue is full at this point
    return 0;
}
```

In this implementation, we maintain two pointers, `front` and `rear`, to keep track of the front and back of the queue respectively. We use an array to store the elements of the queue. The `enqueue` function first checks whether the queue is full, and if not, it adds the element at the rear position and updates the rear pointer accordingly.

Remember to handle the case when the queue is empty as well, as it requires special handling when enqueuing the first element. In this implementation, I used a circular array to handle the wrapping around of the rear pointer when it reaches the end of the array.

### 1. Algorithms & Data Structures (C++): Queue (Theory)

A queue is a fundamental data structure in computer science that follows the First In, First Out (FIFO) principle. It operates much like a line of people waiting for a service, where the person who arrives first is served first. In a queue, elements are added at the back (called enqueue operation) and removed from the front (called dequeue operation).

### Properties of a Queue

1. **FIFO (First In, First Out)**: The element that is added first is the one to be removed first.

2. **Linear Data Structure**: A queue is a linear data structure, meaning its elements are arranged in a sequence.

3. **Dynamic Size**: A queue can dynamically grow or shrink to accommodate the elements being enqueued or dequeued.

4. **Two Primary Operations**:
   * **Enqueue**: Adds an element to the back of the queue.
   * **Dequeue**: Removes the element from the front of the queue.

5. **Supports Peek Operation**: Peek operation retrieves the element at the front of the queue without removing it.

### Queue Applications

1. **Breadth-First Search (BFS)**: Used in graph algorithms like BFS to traverse a graph level by level.

2. **Job Scheduling**: Queues are used in job scheduling algorithms where tasks are executed in the order they arrive.

3. **Print Queue**: Used in printers to queue up documents for printing.

4. **Bounded Buffer**: Queues are used in scenarios where there's a need for a buffer of fixed size.

### Implementation

Queues can be implemented using various underlying data structures, such as arrays or linked lists. Here's a basic implementation of a queue using a linked list:

```cpp
#include <iostream>

using namespace std;

// Node structure for linked list
struct Node {
    int data;
    Node* next;
};

// Queue class
class Queue {
private:
    Node* front;
    Node* rear;
public:
    Queue() {
        front = nullptr;
        rear = nullptr;
    }

    // Enqueue operation
    void enqueue(int value) {
        Node* newNode = new Node;
        newNode->data = value;
        newNode->next = nullptr;
        if (rear == nullptr) {
            front = rear = newNode;
        } else {
            rear->next = newNode;
            rear = newNode;
        }
    }

    // Dequeue operation
    void dequeue() {
        if (front == nullptr) {
            cout << "Queue is empty" << endl;
            return;
        }
        Node* temp = front;
        front = front->next;
        delete temp;
        if (front == nullptr) {
            rear = nullptr;
        }
    }

    // Peek operation
    int peek() {
        if (front == nullptr) {
            cout << "Queue is empty" << endl;
            return -1;
        }
        return front->data;
    }

    // Utility function to check if the queue is empty
    bool isEmpty() {
        return front == nullptr;
    }
};
```

### Time Complexity

* Enqueue operation: O(1)
* Dequeue operation: O(1)
* Peek operation: O(1)
* Space complexity: O(n), where n is the number of elements in the queue.

This is a basic overview of the queue data structure, its properties, applications, and a simple implementation in C++.

### 1. Algorithms & Data Structures (C++): Queue ADT

A Queue ADT (Abstract Data Type) is a fundamental data structure in computer science that follows the First In, First Out (FIFO) principle. In C++, you can implement a Queue using various methods, but one common approach is to use a linked list or an array.

Here's a simple implementation of a Queue ADT using a linked list in C++:

```cpp
#include <iostream>

template <typename T>
class Queue {
private:
    struct Node {
        T data;
        Node* next;
        Node(const T& item) : data(item), next(nullptr) {}
    };
    Node* frontPtr;
    Node* rearPtr;
public:
    Queue() : frontPtr(nullptr), rearPtr(nullptr) {}

    ~Queue() {
        while (!isEmpty())
            dequeue();
    }

    bool isEmpty() const {
        return frontPtr == nullptr;
    }

    void enqueue(const T& item) {
        Node* newNode = new Node(item);
        if (isEmpty()) {
            frontPtr = rearPtr = newNode;
        } else {
            rearPtr->next = newNode;
            rearPtr = newNode;
        }
    }

    void dequeue() {
        if (!isEmpty()) {
            Node* temp = frontPtr;
            if (frontPtr == rearPtr) {
                frontPtr = rearPtr = nullptr;
            } else {
                frontPtr = frontPtr->next;
            }
            delete temp;
        }
    }

    const T& front() const {
        if (!isEmpty()) {
            return frontPtr->data;
        }
        throw std::runtime_error("Queue is empty");
    }
};

int main() {
    Queue<int> q;
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);

    std::cout << "Front of the queue: " << q.front() << std::endl;

    q.dequeue();

    std::cout << "Front of the queue after dequeue: " << q.front() << std::endl;

    return 0;
}
```

This implementation provides basic functionalities like `enqueue`, `dequeue`, `isEmpty`, and `front`. You can further extend it to include additional features like `size`, `clear`, etc., based on your requirements.

In this implementation:

* `enqueue`: Adds an element to the rear of the queue.
* `dequeue`: Removes the element from the front of the queue.
* `isEmpty`: Checks if the queue is empty.
* `front`: Returns the element at the front of the queue without removing it.

Remember to handle memory deallocation properly in your application to avoid memory leaks.

### 1. Algorithms & Data Structures (C++): Queue Applications

Queues, a fundamental data structure in computer science, are commonly used to manage tasks, data, or events in a FIFO (First In, First Out) manner. Here are several common applications of queues in C++:

1. **Breadth-First Search (BFS)**: BFS explores nodes in a graph level by level. Queues are used to keep track of the nodes to be visited, ensuring that nodes at the current level are processed before moving to the next level.

2. **Simulation**: Queues are often used in simulations to model real-world scenarios. For example, in a bank simulation, the queue represents the line of customers waiting to be served.

3. **Task Scheduling**: Queues are used to schedule tasks or jobs in various applications such as operating systems, where tasks are executed in the order they were received.

4. **Printer Queue**: In a printing system, documents are printed in the order they were sent to the printer, making queues a natural choice for managing print jobs.

5. **CPU Scheduling**: Queues are used in CPU scheduling algorithms like Round Robin, where processes are queued and executed in a cyclic manner.

6. **Call Center Management**: Queues are used in call centers to manage incoming calls. Callers are placed in a queue and served by available agents in the order they called.

7. **Buffering**: Queues are used as buffers in networking and I/O operations. Incoming data is stored in a queue until it can be processed.

8. **Bounded Buffer Problem**: In producer-consumer scenarios, where producers produce data and consumers consume it, queues can be used as a bounded buffer to coordinate between producers and consumers.

9. **Caching**: Queues can be used in caching mechanisms, such as the LRU (Least Recently Used) cache eviction policy, where the least recently accessed item is evicted from the cache.

10. **Event Handling**: Queues are used in event-driven programming to handle events such as user inputs, network events, or timer expirations. Events are queued and processed in the order they occur.

In C++, the Standard Template Library (STL) provides a ready-to-use queue container in the `<queue>` header, making it easy to implement these applications. Additionally, C++ allows you to create your own queue data structure using arrays, linked lists, or other underlying data structures. Depending on the specific application and requirements, you can choose the most suitable implementation.

### 1. Algorithms & Data Structures (C++): Queue Data Structure

Certainly! A queue is a fundamental data structure in computer science that follows the First In, First Out (FIFO) principle. This means that the element added first is the one to be removed first. In C++, you can implement a queue using various methods, but one common approach is to use the Standard Template Library (STL) `queue` container.

Here's a basic implementation of a queue using the `queue` container in C++:

```cpp
#include <iostream>
#include <queue>

int main() {
    // Declare a queue of integers
    std::queue<int> myQueue;

    // Push elements into the queue
    myQueue.push(10);
    myQueue.push(20);
    myQueue.push(30);
    myQueue.push(40);

    // Display the elements of the queue
    std::cout << "Queue elements: ";
    while (!myQueue.empty()) {
        std::cout << myQueue.front() << " ";
        myQueue.pop();
    }
    std::cout << std::endl;

    return 0;
}
```

In this example:

* We include the necessary headers: `<iostream>` for input/output operations and `<queue>` for using the queue container.
* We declare a queue `myQueue` of integer type using `std::queue<int>`.
* We push some elements into the queue using the `push()` member function.
* We then traverse the queue using a `while` loop and `front()` to access the front element of the queue, and `pop()` to remove that element.
* Finally, we print out the elements of the queue.

This is just a basic example. Queues can be used in various applications like breadth-first search (BFS) in graph algorithms, implementing task scheduling algorithms, and many more.

### 1. Algorithms & Data Structures (C++): Queue From Stacks

Creating a queue using stacks in C++ involves simulating the behavior of a queue using two stacks. One stack is used for enqueue operations, and the other stack is used for dequeue operations. Here's a basic implementation:

```cpp
#include <iostream>
#include <stack>

using namespace std;

class Queue {
private:
    stack<int> s1; // Stack for enqueue
    stack<int> s2; // Stack for dequeue

public:
    // Function to enqueue an element
    void enqueue(int x) {
        // Move all elements from s2 to s1
        while (!s2.empty()) {
            s1.push(s2.top());
            s2.pop();
        }
        // Push the new element onto s1
        s1.push(x);
    }

    // Function to dequeue an element
    int dequeue() {
        // If both stacks are empty, queue is empty
        if (s1.empty() && s2.empty()) {
            cout << "Queue is empty" << endl;
            return -1;
        }

        // If s2 is empty, move all elements from s1 to s2
        if (s2.empty()) {
            while (!s1.empty()) {
                s2.push(s1.top());
                s1.pop();
            }
        }
        // Pop and return the top element of s2
        int front = s2.top();
        s2.pop();
        return front;
    }

    // Function to check if the queue is empty
    bool isEmpty() {
        return s1.empty() && s2.empty();
    }
};

int main() {
    Queue q;

    q.enqueue(1);
    q.enqueue(2);
    q.enqueue(3);

    cout << "Dequeued element: " << q.dequeue() << endl;

    q.enqueue(4);
    q.enqueue(5);

    while (!q.isEmpty()) {
        cout << "Dequeued element: " << q.dequeue() << endl;
    }

    return 0;
}
```

This implementation ensures that dequeue operations are efficient (amortized O(1) time complexity) by transferring elements between the two stacks when necessary. The enqueue operation has a worst-case time complexity of O(n) because transferring elements between stacks may be required.

### 1. Algorithms & Data Structures (C++): Queue Implementation

Certainly! A queue is a fundamental data structure that follows the First In, First Out (FIFO) principle. Here's a simple implementation of a queue in C++:

```cpp
#include <iostream>

template <typename T>
class Queue {
private:
    struct Node {
        T data;
        Node* next;
        Node(T val) : data(val), next(nullptr) {}
    };

    Node* frontPtr;
    Node* rearPtr;
    int size;

public:
    Queue() : frontPtr(nullptr), rearPtr(nullptr), size(0) {}

    // Destructor to deallocate memory
    ~Queue() {
        while (!isEmpty()) {
            dequeue();
        }
    }

    // Check if the queue is empty
    bool isEmpty() {
        return frontPtr == nullptr;
    }

    // Enqueue operation to add an element to the rear of the queue
    void enqueue(const T& value) {
        Node* newNode = new Node(value);
        if (isEmpty()) {
            frontPtr = rearPtr = newNode;
        } else {
            rearPtr->next = newNode;
            rearPtr = newNode;
        }
        size++;
    }

    // Dequeue operation to remove an element from the front of the queue
    void dequeue() {
        if (!isEmpty()) {
            Node* temp = frontPtr;
            frontPtr = frontPtr->next;
            delete temp;
            size--;
            if (frontPtr == nullptr) {
                rearPtr = nullptr;
            }
        } else {
            std::cerr << "Queue is empty. Cannot dequeue.\n";
        }
    }

    // Return the element at the front of the queue
    T& front() {
        if (!isEmpty()) {
            return frontPtr->data;
        } else {
            throw std::runtime_error("Queue is empty. Cannot access front element.");
        }
    }

    // Return the current size of the queue
    int getSize() const {
        return size;
    }
};

int main() {
    Queue<int> q;
    
    // Enqueue some elements
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);

    // Print front element and queue size
    std::cout << "Front element: " << q.front() << std::endl;
    std::cout << "Queue size: " << q.getSize() << std::endl;

    // Dequeue an element
    q.dequeue();
    std::cout << "Front element after dequeue: " << q.front() << std::endl;
    std::cout << "Queue size after dequeue: " << q.getSize() << std::endl;

    return 0;
}
```

This implementation uses a singly linked list to store the elements of the queue. The `enqueue()` function adds elements to the rear of the queue, the `dequeue()` function removes elements from the front, and the `front()` function returns the element at the front without removing it.

### 1. Algorithms & Data Structures (C++): Queue Implementation (Array)

Sure, here's a basic implementation of a queue using an array in C++:

```cpp
#include <iostream>

#define MAX_SIZE 100 // Maximum size of the queue

class Queue {
private:
    int front, rear;
    int arr[MAX_SIZE];

public:
    Queue() {
        front = -1;
        rear = -1;
    }

    bool isEmpty() {
        return front == -1 && rear == -1;
    }

    bool isFull() {
        return (rear + 1) % MAX_SIZE == front;
    }

    void enqueue(int x) {
        if (isFull()) {
            std::cout << "Queue is full. Cannot enqueue element.\n";
            return;
        }
        if (isEmpty()) {
            front = rear = 0;
        } else {
            rear = (rear + 1) % MAX_SIZE;
        }
        arr[rear] = x;
        std::cout << x << " enqueued to the queue.\n";
    }

    void dequeue() {
        if (isEmpty()) {
            std::cout << "Queue is empty. Cannot dequeue element.\n";
            return;
        }
        std::cout << arr[front] << " dequeued from the queue.\n";
        if (front == rear) {
            front = rear = -1;
        } else {
            front = (front + 1) % MAX_SIZE;
        }
    }

    int peek() {
        if (isEmpty()) {
            std::cout << "Queue is empty. No elements to peek.\n";
            return -1; // Assuming -1 as an indicator for an empty queue
        }
        return arr[front];
    }
};

int main() {
    Queue q;
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    std::cout << "Front element: " << q.peek() << std::endl;
    q.dequeue();
    std::cout << "Front element after dequeue: " << q.peek() << std::endl;
    q.dequeue();
    q.dequeue();
    q.dequeue(); // Trying to dequeue from an empty queue
    return 0;
}
```

This code defines a `Queue` class with member functions `enqueue`, `dequeue`, `isEmpty`, `isFull`, and `peek`. It uses an array to implement the queue, with `front` and `rear` pointers to keep track of the elements in the queue. The `MAX_SIZE` macro defines the maximum size of the queue.

### 1. Algorithms & Data Structures (C++): Queue Implementation (LinkedList)

Sure, I can provide you with a simple implementation of a queue using a linked list in C++. Here's a basic example:

```cpp
#include <iostream>

// Define a structure for a node in the linked list
struct Node {
    int data;
    Node* next;
    
    // Constructor
    Node(int value) : data(value), next(nullptr) {}
};

// Define the Queue class
class Queue {
private:
    Node* front; // Points to the front of the queue
    Node* rear;  // Points to the rear of the queue
    
public:
    // Constructor
    Queue() : front(nullptr), rear(nullptr) {}
    
    // Destructor
    ~Queue() {
        // Delete all nodes in the queue
        while (front != nullptr) {
            Node* temp = front;
            front = front->next;
            delete temp;
        }
    }
    
    // Function to check if the queue is empty
    bool isEmpty() {
        return front == nullptr;
    }
    
    // Function to enqueue an element
    void enqueue(int value) {
        Node* newNode = new Node(value);
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            rear->next = newNode;
            rear = newNode;
        }
    }
    
    // Function to dequeue an element
    void dequeue() {
        if (isEmpty()) {
            std::cout << "Queue is empty. Cannot dequeue.\n";
        } else {
            Node* temp = front;
            front = front->next;
            if (front == nullptr) {
                rear = nullptr;
            }
            delete temp;
        }
    }
    
    // Function to get the front element of the queue
    int peek() {
        if (isEmpty()) {
            std::cout << "Queue is empty. No front element.\n";
            return -1; // Return a default value
        }
        return front->data;
    }
};

// Main function to test the queue implementation
int main() {
    Queue q;
    
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    
    std::cout << "Front element: " << q.peek() << std::endl;
    
    q.dequeue();
    
    std::cout << "Front element after dequeue: " << q.peek() << std::endl;
    
    return 0;
}
```

In this implementation:

* We define a `Node` struct to represent each element in the queue.
* The `Queue` class contains two private member variables: `front` and `rear`, which point to the front and rear of the queue, respectively.
* The `enqueue()` function adds an element to the rear of the queue.
* The `dequeue()` function removes an element from the front of the queue.
* The `peek()` function returns the front element of the queue without removing it.
* The `isEmpty()` function checks if the queue is empty.
* In the `main()` function, we test the queue implementation by enqueueing elements, peeking at the front element, and dequeueing an element.

### 1. Algorithms & Data Structures (C++): Queue implementation with linked list

Sure, here's a basic implementation of a queue using a linked list in C++:

```cpp
#include <iostream>

// Node structure for the linked list
struct Node {
    int data;
    Node* next;
    Node(int value) : data(value), next(nullptr) {}
};

// Queue class
class Queue {
private:
    Node* front; // Points to the front of the queue
    Node* rear;  // Points to the rear of the queue

public:
    Queue() : front(nullptr), rear(nullptr) {}

    // Check if the queue is empty
    bool isEmpty() {
        return front == nullptr;
    }

    // Enqueue (add element to the rear of the queue)
    void enqueue(int value) {
        Node* newNode = new Node(value);
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            rear->next = newNode;
            rear = newNode;
        }
    }

    // Dequeue (remove element from the front of the queue)
    void dequeue() {
        if (isEmpty()) {
            std::cout << "Queue is empty. Cannot dequeue.\n";
        } else {
            Node* temp = front;
            front = front->next;
            delete temp;
            if (front == nullptr) {
                rear = nullptr; // If the queue becomes empty after dequeue
            }
        }
    }

    // Get the element at the front of the queue
    int peek() {
        if (isEmpty()) {
            std::cout << "Queue is empty. Cannot peek.\n";
            return -1; // Return -1 to indicate error
        } else {
            return front->data;
        }
    }

    // Display the elements of the queue
    void display() {
        if (isEmpty()) {
            std::cout << "Queue is empty.\n";
        } else {
            Node* temp = front;
            while (temp != nullptr) {
                std::cout << temp->data << " ";
                temp = temp->next;
            }
            std::cout << std::endl;
        }
    }

    // Destructor to free memory
    ~Queue() {
        while (!isEmpty()) {
            dequeue();
        }
    }
};

// Main function to test the Queue implementation
int main() {
    Queue q;

    // Enqueue elements
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    q.enqueue(40);

    // Display the queue
    std::cout << "Queue elements: ";
    q.display();

    // Peek
    std::cout << "Front element: " << q.peek() << std::endl;

    // Dequeue elements
    q.dequeue();
    q.dequeue();

    // Display the queue after dequeue
    std::cout << "Queue elements after dequeue: ";
    q.display();

    return 0;
}
```

This implementation defines a `Queue` class with basic operations such as `enqueue`, `dequeue`, `peek`, and `display`. Each element of the queue is represented by a `Node` structure containing an integer value and a pointer to the next node in the queue. The `front` pointer points to the front of the queue, and the `rear` pointer points to the rear of the queue.

### 1. Algorithms & Data Structures (C++): Queue in C++

Sure, here's an implementation of a queue data structure in C++:

```cpp
#include <iostream>

template <typename T>
class Queue {
private:
    struct Node {
        T data;
        Node* next;
        Node(const T& data) : data(data), next(nullptr) {}
    };

    Node* front;
    Node* rear;

public:
    Queue() : front(nullptr), rear(nullptr) {}

    ~Queue() {
        while (!isEmpty()) {
            dequeue();
        }
    }

    void enqueue(const T& data) {
        Node* newNode = new Node(data);
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            rear->next = newNode;
            rear = newNode;
        }
    }

    void dequeue() {
        if (isEmpty()) {
            std::cerr << "Queue is empty. Cannot dequeue.\n";
            return;
        }
        Node* temp = front;
        front = front->next;
        delete temp;
        if (front == nullptr) {
            rear = nullptr;
        }
    }

    T peek() const {
        if (isEmpty()) {
            std::cerr << "Queue is empty. Cannot peek.\n";
            exit(1);
        }
        return front->data;
    }

    bool isEmpty() const {
        return front == nullptr;
    }
};

int main() {
    Queue<int> myQueue;
    
    myQueue.enqueue(10);
    myQueue.enqueue(20);
    myQueue.enqueue(30);

    std::cout << "Front element: " << myQueue.peek() << std::endl;
    
    myQueue.dequeue();
    std::cout << "Front element after dequeue: " << myQueue.peek() << std::endl;
    
    return 0;
}
```

This code implements a simple queue using a singly linked list. The `enqueue` function adds an element to the rear of the queue, the `dequeue` function removes an element from the front of the queue, the `peek` function returns the element at the front of the queue without removing it, and the `isEmpty` function checks if the queue is empty.

### 1. Algorithms & Data Structures (C++): Queue operations

Sure, I can help with that! In C++, you can implement queue operations using the standard library's `queue` container, or you can implement your own queue using arrays or linked lists. Here's an example of how you can perform basic queue operations using the standard library's `queue` container:

```cpp
#include <iostream>
#include <queue>

using namespace std;

int main() {
    // Creating a queue
    queue<int> q;

    // Enqueue elements into the queue
    q.push(10);
    q.push(20);
    q.push(30);

    // Displaying the elements in the queue
    cout << "Queue elements: ";
    while (!q.empty()) {
        cout << q.front() << " ";
        q.pop();
    }
    cout << endl;

    return 0;
}
```

This code demonstrates how to enqueue elements into a queue using `push()`, and dequeue elements from the queue using `pop()`. The `front()` function is used to access the front element of the queue, and `empty()` checks whether the queue is empty.

If you prefer to implement your own queue using arrays or linked lists, let me know, and I can provide examples for that as well.

### 1. Algorithms & Data Structures (C++): Queue STL

Sure! In C++, the Standard Template Library (STL) provides a versatile implementation of queues through the `queue` container adapter. This adapter is a part of the `<queue>` header file. Here's a basic overview and example usage:

### Overview

* **Queue**: A queue is a First-In-First-Out (FIFO) data structure, where elements are added to the back (also called rear or tail) and removed from the front (also called head). It follows the principle of "first come, first served."
* **Container Adapter**: `queue` in C++ is a container adapter, meaning it's implemented using other data structures underneath (typically deque or list).

### Operations Supported

1. **Push**: Adds an element to the back of the queue.
2. **Pop**: Removes the element from the front of the queue.
3. **Front**: Accesses the element at the front of the queue.
4. **Back**: Accesses the element at the back of the queue.
5. **Empty**: Checks if the queue is empty.
6. **Size**: Returns the number of elements in the queue.

### Example Usage

```cpp
#include <iostream>
#include <queue>

int main() {
    // Declaring a queue of integers
    std::queue<int> myQueue;

    // Pushing elements into the queue
    myQueue.push(10);
    myQueue.push(20);
    myQueue.push(30);

    // Accessing the front and back elements
    std::cout << "Front element: " << myQueue.front() << std::endl; // Outputs: 10
    std::cout << "Back element: " << myQueue.back() << std::endl;   // Outputs: 30

    // Popping an element
    myQueue.pop();

    // Checking if the queue is empty and its size
    std::cout << "Is queue empty? " << (myQueue.empty() ? "Yes" : "No") << std::endl; // Outputs: No
    std::cout << "Queue size: " << myQueue.size() << std::endl;                        // Outputs: 2

    return 0;
}
```

### Notes

* The `push` function adds elements to the back of the queue.
* The `pop` function removes the front element from the queue.
* Accessing front or back elements of an empty queue is undefined behavior, so it's always a good practice to check if the queue is empty before doing so.
* Queues are particularly useful in scenarios where you want to process elements in the order they were added, such as task scheduling, breadth-first search, etc.

### 1. Algorithms & Data Structures (C++): Queue using 2 Stacks

Certainly! Implementing a queue using two stacks is a classic problem in data structures. You can use two stacks to simulate the behavior of a queue. One stack is used for enqueue operations, and the other is used for dequeue operations. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <stack>

using namespace std;

class Queue {
private:
    stack<int> s1; // For enqueue operation
    stack<int> s2; // For dequeue operation

public:
    void enqueue(int x) {
        // Push all elements from s2 to s1
        while (!s2.empty()) {
            s1.push(s2.top());
            s2.pop();
        }

        // Push the new element onto s1
        s1.push(x);
    }

    int dequeue() {
        // If both stacks are empty, the queue is empty
        if (s1.empty() && s2.empty()) {
            cout << "Queue is empty\n";
            return -1;
        }

        // If s2 is empty, move elements from s1 to s2
        if (s2.empty()) {
            while (!s1.empty()) {
                s2.push(s1.top());
                s1.pop();
            }
        }

        // Pop and return the top element of s2
        int front = s2.top();
        s2.pop();
        return front;
    }

    bool isEmpty() {
        return (s1.empty() && s2.empty());
    }
};

int main() {
    Queue q;

    q.enqueue(1);
    q.enqueue(2);
    q.enqueue(3);

    cout << q.dequeue() << endl; // Output: 1
    cout << q.dequeue() << endl; // Output: 2

    q.enqueue(4);

    cout << q.dequeue() << endl; // Output: 3
    cout << q.dequeue() << endl; // Output: 4

    cout << q.dequeue() << endl; // Output: Queue is empty, -1

    return 0;
}
```

In this implementation:

* `enqueue(int x)`: To enqueue an element, we push it onto `s1`.
* `dequeue()`: To dequeue an element, we check if `s2` is empty. If it is, we move all elements from `s1` to `s2`. Then, we pop the top element of `s2`, which is the front of the queue.
* `isEmpty()`: Checks if both stacks are empty.

This implementation ensures that the elements are dequeued in the same order as they were enqueued, maintaining the FIFO (First In, First Out) property of a queue.

### 1. Algorithms & Data Structures (C++): Queue using Array

Sure! Below is a simple implementation of a queue using an array in C++:

```cpp
#include <iostream>

#define MAX_SIZE 100

class Queue {
private:
    int front, rear;
    int arr[MAX_SIZE];

public:
    Queue() {
        front = -1;
        rear = -1;
    }

    bool isEmpty() {
        return front == -1 && rear == -1;
    }

    bool isFull() {
        return rear == MAX_SIZE - 1;
    }

    void enqueue(int x) {
        if (isFull()) {
            std::cout << "Queue is full. Cannot enqueue element.\n";
            return;
        } else if (isEmpty()) {
            front = rear = 0;
        } else {
            rear++;
        }
        arr[rear] = x;
        std::cout << x << " enqueued to the queue.\n";
    }

    void dequeue() {
        if (isEmpty()) {
            std::cout << "Queue is empty. Cannot dequeue element.\n";
            return;
        } else if (front == rear) {
            front = rear = -1;
        } else {
            front++;
        }
    }

    int peek() {
        if (isEmpty()) {
            std::cout << "Queue is empty. No element to peek.\n";
            return -1;
        }
        return arr[front];
    }

    void display() {
        if (isEmpty()) {
            std::cout << "Queue is empty.\n";
            return;
        }
        std::cout << "Queue elements: ";
        for (int i = front; i <= rear; ++i) {
            std::cout << arr[i] << " ";
        }
        std::cout << std::endl;
    }
};

int main() {
    Queue q;

    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);

    q.display();

    std::cout << "Front element: " << q.peek() << std::endl;

    q.dequeue();
    q.dequeue();

    q.display();

    std::cout << "Front element: " << q.peek() << std::endl;

    return 0;
}
```

In this implementation:

* The `Queue` class contains member functions for common queue operations like `enqueue`, `dequeue`, `peek`, and `display`.
* It uses an array `arr` to store the elements of the queue.
* `front` and `rear` are indices to keep track of the front and rear of the queue respectively.
* The `enqueue` function adds an element to the rear of the queue.
* The `dequeue` function removes an element from the front of the queue.
* The `peek` function returns the front element of the queue without removing it.
* The `display` function prints all the elements of the queue.

### 1. Algorithms & Data Structures (C++): Queue using array: Double Property

Sure! Implementing a queue using an array in C++ is a common task. Adding a double property to each element in the queue could be useful for certain applications. Here's how you can implement it:

```cpp
#include <iostream>
using namespace std;

// Define the maximum size of the queue
#define MAX_SIZE 100

// Define the structure of each element in the queue
struct QueueElement {
    int data;
    double property;
};

// Define the Queue class
class Queue {
private:
    QueueElement elements[MAX_SIZE];
    int front, rear;

public:
    Queue() {
        front = -1;
        rear = -1;
    }

    // Function to check if the queue is empty
    bool isEmpty() {
        return (front == -1 && rear == -1);
    }

    // Function to check if the queue is full
    bool isFull() {
        return (rear + 1) % MAX_SIZE == front;
    }

    // Function to add an element to the queue
    void enqueue(int data, double property) {
        if (isFull()) {
            cout << "Queue Overflow\n";
            return;
        } else if (isEmpty()) {
            front = rear = 0;
        } else {
            rear = (rear + 1) % MAX_SIZE;
        }

        elements[rear].data = data;
        elements[rear].property = property;
    }

    // Function to remove an element from the queue
    void dequeue() {
        if (isEmpty()) {
            cout << "Queue Underflow\n";
            return;
        } else if (front == rear) {
            front = rear = -1;
        } else {
            front = (front + 1) % MAX_SIZE;
        }
    }

    // Function to get the front element of the queue
    QueueElement frontElement() {
        if (isEmpty()) {
            cout << "Queue is empty\n";
            // Returning a default element when the queue is empty
            return {0, 0.0};
        }
        return elements[front];
    }
};

// Main function to test the queue
int main() {
    Queue q;
    q.enqueue(10, 3.14);
    q.enqueue(20, 6.28);
    q.enqueue(30, 9.42);

    cout << "Front element: " << q.frontElement().data << " " << q.frontElement().property << endl;

    q.dequeue();

    cout << "Front element after dequeue: " << q.frontElement().data << " " << q.frontElement().property << endl;

    return 0;
}
```

In this implementation, each element in the queue is represented by a structure `QueueElement` containing an integer `data` and a double `property`. The queue itself is implemented using a circular array, with `front` and `rear` indices to keep track of the front and rear elements. The `enqueue()` function adds elements to the rear of the queue, while the `dequeue()` function removes elements from the front. The `frontElement()` function returns the front element of the queue without removing it.

### 1. Algorithms & Data Structures (C++): Queue using Circular Array

Sure, I can provide you with a C++ implementation of a queue using a circular array. Here's a basic implementation:

```cpp
#include <iostream>

#define MAX_SIZE 100

class Queue {
private:
    int arr[MAX_SIZE];
    int front, rear;

public:
    Queue() {
        front = rear = -1;
    }

    bool isEmpty() {
        return (front == -1 && rear == -1);
    }

    bool isFull() {
        return ((rear + 1) % MAX_SIZE == front);
    }

    void enqueue(int value) {
        if (isFull()) {
            std::cout << "Queue is full. Cannot enqueue more elements.\n";
            return;
        }
        if (isEmpty()) {
            front = rear = 0;
        } else {
            rear = (rear + 1) % MAX_SIZE;
        }
        arr[rear] = value;
    }

    void dequeue() {
        if (isEmpty()) {
            std::cout << "Queue is empty. Cannot dequeue.\n";
            return;
        }
        if (front == rear) {
            front = rear = -1;
        } else {
            front = (front + 1) % MAX_SIZE;
        }
    }

    int peek() {
        if (isEmpty()) {
            std::cout << "Queue is empty. Cannot peek.\n";
            return -1; // Assuming -1 is not a valid value in the queue
        }
        return arr[front];
    }
};

int main() {
    Queue q;
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    q.enqueue(40);

    std::cout << "Front element: " << q.peek() << std::endl;

    q.dequeue();
    q.dequeue();

    std::cout << "Front element after dequeuing twice: " << q.peek() << std::endl;

    q.enqueue(50);
    q.enqueue(60);

    std::cout << "Front element after enqueuing twice: " << q.peek() << std::endl;

    return 0;
}
```

This implementation defines a class `Queue` with member functions for `enqueue`, `dequeue`, `isEmpty`, `isFull`, and `peek`. It uses a circular array `arr` with a maximum size of `MAX_SIZE` to store the elements of the queue. The `front` and `rear` indices keep track of the front and rear elements of the queue respectively.

### 1. Algorithms & Data Structures (C++): Queue using Circular Array instead of Normal Array

Using a circular array to implement a queue in C++ is quite efficient, especially in scenarios where memory allocation and deallocation are costly operations. Here's how you can implement a queue using a circular array:

```cpp
#include <iostream>

#define MAX_SIZE 100 // Maximum size of the circular array

class Queue {
private:
    int front, rear;
    int arr[MAX_SIZE];

public:
    Queue() {
        front = -1;
        rear = -1;
    }

    bool isEmpty() {
        return front == -1;
    }

    bool isFull() {
        return (front == 0 && rear == MAX_SIZE - 1) || (rear == (front - 1) % (MAX_SIZE - 1));
    }

    void enqueue(int value) {
        if (isFull()) {
            std::cout << "Queue Overflow\n";
            return;
        }
        if (isEmpty()) {
            front = rear = 0;
        } else {
            rear = (rear + 1) % MAX_SIZE;
        }
        arr[rear] = value;
    }

    void dequeue() {
        if (isEmpty()) {
            std::cout << "Queue Underflow\n";
            return;
        }
        if (front == rear) {
            front = rear = -1;
        } else {
            front = (front + 1) % MAX_SIZE;
        }
    }

    int peek() {
        if (isEmpty()) {
            std::cout << "Queue is empty\n";
            return -1;
        }
        return arr[front];
    }
};

int main() {
    Queue q;
    
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    q.enqueue(40);
    
    std::cout << "Front element: " << q.peek() << std::endl;
    
    q.dequeue();
    std::cout << "Front element after dequeue: " << q.peek() << std::endl;

    return 0;
}
```

In this implementation:

* We maintain two indices, `front` and `rear`, to keep track of the front and rear elements of the queue.
* The circular nature of the array allows us to reuse the space freed up after dequeuing elements.
* We have defined `MAX_SIZE` to limit the size of the circular array to avoid overflow.
* Enqueue operation checks if the queue is full, and if not, it inserts the element at the rear and updates the rear index accordingly.
* Dequeue operation checks if the queue is empty, and if not, it removes the element at the front and updates the front index accordingly.
* Peek operation returns the element at the front without removing it from the queue.

### 1. Algorithms & Data Structures (C++): Queue using linked list

Sure, here's an implementation of a queue using a linked list in C++:

```cpp
#include <iostream>

// Define a node structure for the linked list
struct Node {
    int data;
    Node* next;
    
    Node(int value) : data(value), next(nullptr) {}
};

// Define the Queue class
class Queue {
private:
    Node* front; // Pointer to the front of the queue
    Node* rear;  // Pointer to the rear of the queue
    
public:
    Queue() : front(nullptr), rear(nullptr) {}
    
    // Function to check if the queue is empty
    bool isEmpty() {
        return front == nullptr;
    }
    
    // Function to enqueue an element to the rear of the queue
    void enqueue(int value) {
        Node* newNode = new Node(value);
        
        // If the queue is empty, both front and rear will point to the new node
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            // Otherwise, append the new node to the rear and update rear pointer
            rear->next = newNode;
            rear = newNode;
        }
        
        std::cout << value << " enqueued to the queue." << std::endl;
    }
    
    // Function to dequeue an element from the front of the queue
    void dequeue() {
        // If the queue is empty, do nothing
        if (isEmpty()) {
            std::cout << "Queue is empty. Cannot dequeue." << std::endl;
            return;
        }
        
        // Store the front node and move front pointer to the next node
        Node* temp = front;
        front = front->next;
        
        // If after dequeuing, the queue becomes empty, also update rear pointer
        if (front == nullptr) {
            rear = nullptr;
        }
        
        std::cout << temp->data << " dequeued from the queue." << std::endl;
        delete temp; // Free memory
    }
    
    // Function to get the front element of the queue
    int getFront() {
        // If the queue is empty, return -1 (assuming -1 is not a valid element in the queue)
        if (isEmpty()) {
            std::cout << "Queue is empty." << std::endl;
            return -1;
        }
        return front->data;
    }
    
    // Function to get the rear element of the queue
    int getRear() {
        // If the queue is empty, return -1 (assuming -1 is not a valid element in the queue)
        if (isEmpty()) {
            std::cout << "Queue is empty." << std::endl;
            return -1;
        }
        return rear->data;
    }
};

int main() {
    Queue q;
    
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    
    std::cout << "Front element: " << q.getFront() << std::endl;
    std::cout << "Rear element: " << q.getRear() << std::endl;
    
    q.dequeue();
    q.dequeue();
    q.dequeue();
    q.dequeue(); // Trying to dequeue from an empty queue
    
    return 0;
}
```

This code implements a basic queue using a singly linked list. It defines a `Node` struct to represent elements of the linked list, and a `Queue` class to encapsulate the queue operations. The queue supports enqueueing, dequeueing, and retrieving the front and rear elements.

### 1. Algorithms & Data Structures (C++): Queue using Linked Lists

Sure! Below is a simple implementation of a queue using linked lists in C++:

```cpp
#include <iostream>

// Node class to represent each element in the linked list
class Node {
public:
    int data;
    Node* next;

    // Constructor to initialize data and next pointer
    Node(int data) : data(data), next(nullptr) {}
};

// Queue class implemented using a linked list
class Queue {
private:
    Node* front; // Pointer to the front of the queue
    Node* rear; // Pointer to the rear of the queue

public:
    // Constructor to initialize front and rear pointers
    Queue() : front(nullptr), rear(nullptr) {}

    // Function to check if the queue is empty
    bool isEmpty() {
        return front == nullptr;
    }

    // Function to enqueue an element to the rear of the queue
    void enqueue(int data) {
        Node* newNode = new Node(data);
        // If the queue is empty, both front and rear point to the new node
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            // Otherwise, add the new node to the rear and update rear pointer
            rear->next = newNode;
            rear = newNode;
        }
        std::cout << data << " enqueued to queue.\n";
    }

    // Function to dequeue an element from the front of the queue
    int dequeue() {
        // If the queue is empty, return -1 indicating underflow
        if (isEmpty()) {
            std::cout << "Queue is empty. Cannot dequeue.\n";
            return -1;
        } else {
            int data = front->data;
            Node* temp = front;
            // Move front pointer to the next node
            front = front->next;
            // If the front becomes nullptr, the queue becomes empty, update rear accordingly
            if (front == nullptr) {
                rear = nullptr;
            }
            delete temp; // Delete the dequeued node
            std::cout << data << " dequeued from queue.\n";
            return data;
        }
    }

    // Function to display the elements of the queue
    void display() {
        if (isEmpty()) {
            std::cout << "Queue is empty.\n";
            return;
        }
        std::cout << "Elements of queue are: ";
        Node* temp = front;
        while (temp != nullptr) {
            std::cout << temp->data << " ";
            temp = temp->next;
        }
        std::cout << std::endl;
    }

    // Destructor to deallocate memory
    ~Queue() {
        Node* temp;
        while (front != nullptr) {
            temp = front;
            front = front->next;
            delete temp;
        }
        rear = nullptr;
    }
};

int main() {
    Queue q;

    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);

    q.display();

    q.dequeue();
    q.dequeue();

    q.display();

    q.dequeue();
    q.dequeue(); // Dequeue from empty queue

    return 0;
}
```

This code implements a queue using a linked list. It has the basic operations of a queue: `enqueue`, `dequeue`, and `display`. The `enqueue` operation adds an element to the rear of the queue, the `dequeue` operation removes an element from the front of the queue, and `display` operation prints the elements of the queue.

### 1. Algorithms & Data Structures (C++): Queue using LinkedList

Certainly! Below is a simple implementation of a queue using a linked list in C++:

```cpp
#include <iostream>

// Node class to represent each element in the linked list
class Node {
public:
    int data;
    Node* next;

    Node(int val) : data(val), next(nullptr) {}
};

// Queue class
class Queue {
private:
    Node* front; // Points to the front of the queue
    Node* rear;  // Points to the rear of the queue

public:
    Queue() : front(nullptr), rear(nullptr) {}

    // Function to check if the queue is empty
    bool isEmpty() {
        return front == nullptr;
    }

    // Function to enqueue an element to the rear of the queue
    void enqueue(int val) {
        Node* newNode = new Node(val);
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            rear->next = newNode;
            rear = newNode;
        }
        std::cout << val << " enqueued to the queue.\n";
    }

    // Function to dequeue an element from the front of the queue
    void dequeue() {
        if (isEmpty()) {
            std::cout << "Queue is empty. Cannot dequeue.\n";
            return;
        }
        Node* temp = front;
        front = front->next;
        if (front == nullptr) {
            rear = nullptr; // Reset rear if queue becomes empty
        }
        std::cout << temp->data << " dequeued from the queue.\n";
        delete temp;
    }

    // Function to get the front element of the queue
    int peek() {
        if (isEmpty()) {
            std::cout << "Queue is empty.\n";
            return -1; // Return a default value indicating queue is empty
        }
        return front->data;
    }

    // Function to display the elements of the queue
    void display() {
        if (isEmpty()) {
            std::cout << "Queue is empty.\n";
            return;
        }
        Node* temp = front;
        std::cout << "Elements of the queue are: ";
        while (temp != nullptr) {
            std::cout << temp->data << " ";
            temp = temp->next;
        }
        std::cout << std::endl;
    }
};

int main() {
    Queue q;

    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);

    q.display();

    std::cout << "Front element: " << q.peek() << std::endl;

    q.dequeue();
    q.dequeue();

    q.display();

    std::cout << "Front element: " << q.peek() << std::endl;

    q.dequeue();

    q.display();

    std::cout << "Front element: " << q.peek() << std::endl;

    q.dequeue(); // Trying to dequeue from empty queue

    return 0;
}
```

This code defines a Queue class that internally uses a linked list to store elements. It provides enqueue, dequeue, peek, isEmpty, and display operations. The main function demonstrates how to use these operations.

### 1. Algorithms & Data Structures (C++): Queue using LL

Sure! Below is an implementation of a Queue using a linked list in C++:

```cpp
#include <iostream>

using namespace std;

// Node class to represent individual elements in the linked list
class Node {
public:
    int data;
    Node* next;

    Node(int value) {
        data = value;
        next = nullptr;
    }
};

// Queue class
class Queue {
private:
    Node* front; // Points to the front of the queue
    Node* rear; // Points to the rear of the queue

public:
    Queue() {
        front = nullptr;
        rear = nullptr;
    }

    // Function to check if the queue is empty
    bool isEmpty() {
        return front == nullptr;
    }

    // Function to add an element to the rear of the queue
    void enqueue(int value) {
        Node* newNode = new Node(value);
        if (isEmpty()) {
            front = newNode;
            rear = newNode;
        } else {
            rear->next = newNode;
            rear = newNode;
        }
    }

    // Function to remove an element from the front of the queue
    void dequeue() {
        if (isEmpty()) {
            cout << "Queue is empty. Cannot dequeue.\n";
        } else {
            Node* temp = front;
            front = front->next;
            delete temp;
        }
    }

    // Function to get the front element of the queue
    int peek() {
        if (isEmpty()) {
            cout << "Queue is empty. No front element.\n";
            return -1;
        } else {
            return front->data;
        }
    }

    // Function to display the queue
    void display() {
        if (isEmpty()) {
            cout << "Queue is empty.\n";
        } else {
            Node* current = front;
            cout << "Queue: ";
            while (current != nullptr) {
                cout << current->data << " ";
                current = current->next;
            }
            cout << endl;
        }
    }
};

int main() {
    Queue queue;

    queue.enqueue(10);
    queue.enqueue(20);
    queue.enqueue(30);

    queue.display(); // Output: Queue: 10 20 30

    cout << "Front element: " << queue.peek() << endl; // Output: Front element: 10

    queue.dequeue();
    queue.display(); // Output: Queue: 20 30

    return 0;
}
```

This code implements a Queue using a linked list. The `Queue` class maintains pointers to the front and rear of the queue. The `enqueue()` function adds elements to the rear, the `dequeue()` function removes elements from the front, and the `peek()` function returns the element at the front without removing it. The `display()` function is provided to print the elements of the queue.

### 1. Algorithms & Data Structures (C++): Queue using Single Pointer

To implement a queue using a single pointer in C++, you can use a circular linked list. In this implementation, each node in the linked list contains data and a pointer to the next node. The rear pointer always points to the last node in the queue, and the next pointer of the last node points to the first node, creating a circular structure.

Here's a basic implementation:

```cpp
#include <iostream>

using namespace std;

// Node structure
struct Node {
    int data;
    Node* next;
};

// Queue class
class Queue {
private:
    Node* rear; // Rear pointer pointing to the last node

public:
    // Constructor
    Queue() {
        rear = nullptr; // Initialize rear to null
    }

    // Destructor to free memory
    ~Queue() {
        // Traverse and delete all nodes
        while (rear != nullptr) {
            Node* temp = rear->next;
            if (temp == rear) { // Only one node left
                delete rear;
                rear = nullptr;
            } else {
                rear->next = temp->next;
                delete temp;
            }
        }
    }

    // Function to check if the queue is empty
    bool isEmpty() {
        return rear == nullptr;
    }

    // Function to enqueue a new element
    void enqueue(int data) {
        Node* newNode = new Node; // Create a new node
        newNode->data = data; // Assign data to the new node

        if (isEmpty()) { // If the queue is empty
            rear = newNode;
            newNode->next = rear; // Circular linking
        } else {
            newNode->next = rear->next; // Connect the new node to the front
            rear->next = newNode; // Update the rear's next pointer
            rear = newNode; // Update rear to the new node
        }
    }

    // Function to dequeue an element
    void dequeue() {
        if (isEmpty()) {
            cout << "Queue is empty. Cannot dequeue.\n";
            return;
        }

        if (rear->next == rear) { // Only one element in the queue
            delete rear;
            rear = nullptr;
        } else {
            Node* temp = rear->next; // Node to be dequeued
            rear->next = temp->next; // Rear skips the front node
            delete temp; // Delete the front node
        }
    }

    // Function to display the queue
    void display() {
        if (isEmpty()) {
            cout << "Queue is empty.\n";
            return;
        }

        Node* temp = rear->next; // Start from the front
        do {
            cout << temp->data << " "; // Display current node's data
            temp = temp->next; // Move to the next node
        } while (temp != rear->next); // Stop when back to the front
        cout << endl;
    }
};

// Main function for testing
int main() {
    Queue q;

    // Enqueue some elements
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);

    // Display the queue
    cout << "Queue: ";
    q.display();

    // Dequeue an element
    q.dequeue();

    // Display the queue after dequeue
    cout << "Queue after dequeue: ";
    q.display();

    return 0;
}
```

This implementation provides the basic operations of a queue: enqueue, dequeue, checking if the queue is empty, and displaying the elements of the queue. It uses a circular linked list to efficiently implement these operations with a single pointer (`rear`).

### 1. Algorithms & Data Structures (C++): Queue Using Stack Data Structure

Creating a queue using a stack data structure in C++ is a classic exercise that helps you understand how stacks and queues work internally. You can implement a queue using two stacks. Here's how you can do it:

```cpp
#include <iostream>
#include <stack>

using namespace std;

template<typename T>
class QueueUsingStack {
private:
    stack<T> inbox; // Used for enqueue operation
    stack<T> outbox; // Used for dequeue operation

public:
    // Enqueue operation
    void enqueue(const T& value) {
        inbox.push(value);
    }

    // Dequeue operation
    T dequeue() {
        // If outbox is empty, transfer elements from inbox to outbox
        if (outbox.empty()) {
            while (!inbox.empty()) {
                outbox.push(inbox.top());
                inbox.pop();
            }
        }

        // If outbox is still empty, the queue is empty
        if (outbox.empty()) {
            throw out_of_range("Queue is empty");
        }

        // Pop and return the front element from outbox
        T front = outbox.top();
        outbox.pop();
        return front;
    }

    // Check if the queue is empty
    bool empty() const {
        return inbox.empty() && outbox.empty();
    }

    // Return the size of the queue
    size_t size() const {
        return inbox.size() + outbox.size();
    }
};

int main() {
    QueueUsingStack<int> q;

    // Enqueue elements
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);

    // Dequeue and print elements
    cout << "Dequeued: " << q.dequeue() << endl;
    cout << "Dequeued: " << q.dequeue() << endl;
    cout << "Dequeued: " << q.dequeue() << endl;

    // Check if the queue is empty
    if (q.empty()) {
        cout << "Queue is empty" << endl;
    } else {
        cout << "Queue is not empty" << endl;
    }

    return 0;
}
```

In this implementation, the `enqueue` operation is straightforward; it just pushes elements onto the `inbox` stack. The `dequeue` operation is a bit more complicated. It transfers elements from the `inbox` stack to the `outbox` stack if the `outbox` is empty. Then it pops the top element from the `outbox` to dequeue an element. This way, the oldest element in the queue will always be at the top of the `outbox` stack, simulating a queue's behavior.

This implementation ensures that both enqueue and dequeue operations have an amortized time complexity of O(1).

### 1. Algorithms & Data Structures (C++): Queue Using Stacks: Dequeue

Sure, implementing a queue using stacks in C++ involves simulating the FIFO (First In, First Out) behavior of a queue using two stacks. One stack will be used for enqueue operations, and the other will be used for dequeue operations.

Here's a simple implementation:

```cpp
#include <iostream>
#include <stack>

using namespace std;

class Queue {
private:
    stack<int> enqStack; // For enqueue operations
    stack<int> deqStack; // For dequeue operations

    // Move elements from enqStack to deqStack
    void moveElements() {
        while (!enqStack.empty()) {
            deqStack.push(enqStack.top());
            enqStack.pop();
        }
    }

public:
    // Enqueue operation
    void enqueue(int value) {
        enqStack.push(value);
    }

    // Dequeue operation
    int dequeue() {
        // If deqStack is empty, move elements from enqStack
        if (deqStack.empty()) {
            moveElements();
        }
        // If deqStack is still empty, the queue is empty
        if (deqStack.empty()) {
            cout << "Queue is empty!" << endl;
            return -1; // Assuming -1 represents an empty queue
        }
        // Pop from deqStack
        int front = deqStack.top();
        deqStack.pop();
        return front;
    }
};

int main() {
    Queue q;

    q.enqueue(1);
    q.enqueue(2);
    q.enqueue(3);

    cout << q.dequeue() << endl; // Should print 1
    cout << q.dequeue() << endl; // Should print 2

    q.enqueue(4);

    cout << q.dequeue() << endl; // Should print 3
    cout << q.dequeue() << endl; // Should print 4

    cout << q.dequeue() << endl; // Should print "Queue is empty!"

    return 0;
}
```

This code demonstrates the basic functionality of a queue using stacks. The `enqueue` operation is straightforward, as it simply pushes elements onto the `enqStack`. The `dequeue` operation is a bit more involved. It first checks if the `deqStack` is empty, and if so, it moves elements from the `enqStack` to the `deqStack`. Then it pops the top element from the `deqStack` to simulate the dequeue operation. If both stacks are empty, it prints a message indicating that the queue is empty.

### 1. Algorithms & Data Structures (C++): Queue Using Stacks: Enqueue

To implement a queue using stacks in C++, you typically use two stacks. One stack is used for enqueue operations, and the other one is used for dequeue operations. Here's how you can implement the `enqueue` operation:

```cpp
#include <iostream>
#include <stack>

using namespace std;

class Queue {
private:
    stack<int> s1; // Stack for enqueue
    stack<int> s2; // Stack for dequeue

public:
    // Function to enqueue an element
    void enqueue(int x) {
        // Move all elements from s2 to s1
        while (!s2.empty()) {
            s1.push(s2.top());
            s2.pop();
        }

        // Push the new element into s1
        s1.push(x);
    }

    // Function to dequeue an element
    int dequeue() {
        // Move all elements from s1 to s2
        while (!s1.empty()) {
            s2.push(s1.top());
            s1.pop();
        }

        // If s2 is empty, queue is empty
        if (s2.empty()) {
            cout << "Queue is empty." << endl;
            return -1; // Return some default value indicating empty queue
        }

        // Pop the front element from s2 (which was originally at the front of the queue)
        int frontElement = s2.top();
        s2.pop();
        return frontElement;
    }
};

int main() {
    Queue q;
    q.enqueue(1);
    q.enqueue(2);
    q.enqueue(3);

    cout << q.dequeue() << endl; // Output: 1
    cout << q.dequeue() << endl; // Output: 2
    cout << q.dequeue() << endl; // Output: 3
    cout << q.dequeue() << endl; // Output: Queue is empty, -1

    return 0;
}
```

This code implements a basic queue using two stacks. The `enqueue` operation is implemented by pushing elements onto `s1`, while the `dequeue` operation is implemented by first moving all elements to `s2` and then popping from `s2`.

### 1. Algorithms & Data Structures (C++): Queue using Two Pointers

Certainly! Implementing a queue using two pointers in C++ typically involves having one pointer to the front of the queue and another pointer to the rear. Here's a basic implementation:

```cpp
#include <iostream>

using namespace std;

const int MAX_SIZE = 100;

class Queue {
private:
    int arr[MAX_SIZE];
    int front, rear;

public:
    Queue() {
        front = -1; // Initialize front and rear pointers
        rear = -1;
    }

    bool isEmpty() {
        return (front == -1 && rear == -1);
    }

    bool isFull() {
        return (rear + 1) % MAX_SIZE == front; // Check if rear is one position ahead of front
    }

    void enqueue(int x) {
        if (isFull()) {
            cout << "Queue is full. Cannot enqueue." << endl;
            return;
        } else if (isEmpty()) {
            front = rear = 0; // If queue is empty, set front and rear to 0
        } else {
            rear = (rear + 1) % MAX_SIZE; // Move rear circularly
        }
        arr[rear] = x;
        cout << x << " enqueued into the queue." << endl;
    }

    void dequeue() {
        if (isEmpty()) {
            cout << "Queue is empty. Cannot dequeue." << endl;
            return;
        } else if (front == rear) {
            cout << arr[front] << " dequeued from the queue." << endl;
            front = rear = -1; // If only one element in the queue, reset front and rear
        } else {
            cout << arr[front] << " dequeued from the queue." << endl;
            front = (front + 1) % MAX_SIZE; // Move front circularly
        }
    }

    int peek() {
        if (isEmpty()) {
            cout << "Queue is empty." << endl;
            return -1;
        }
        return arr[front];
    }
};

int main() {
    Queue q;
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    q.dequeue();
    cout << "Front element: " << q.peek() << endl;
    return 0;
}
```

In this implementation:

* We use an array `arr` to store the elements of the queue.
* `front` and `rear` are pointers to the front and rear of the queue respectively. They are initialized to `-1` when the queue is empty.
* `isFull()` checks if the queue is full, and `isEmpty()` checks if the queue is empty.
* `enqueue()` adds an element to the rear of the queue, and `dequeue()` removes an element from the front of the queue.
* We use modulo operator `%` to implement the circular queue behavior, allowing the queue to wrap around when it reaches the end of the array.
* `peek()` returns the element at the front of the queue without removing it.
  
You can further modify or extend this implementation based on your requirements.

### 1. Algorithms & Data Structures (C++): Queue: Constructor

In C++, the constructor for a queue typically initializes the queue object. If you're implementing a queue from scratch, you'd typically define a class for the queue, and its constructor would allocate any necessary memory or initialize internal variables.

Here's an example of how you might define a simple queue class in C++ with a constructor:

```cpp
#include <iostream>
using namespace std;

const int MAX_SIZE = 100; // Maximum size of the queue

class Queue {
private:
    int front, rear;
    int arr[MAX_SIZE];

public:
    Queue() { // Constructor
        front = rear = -1; // Initialize front and rear indices
    }

    // Other member functions like enqueue, dequeue, isEmpty, isFull, etc.
};

int main() {
    Queue q; // Creating a queue object

    // Perform operations on the queue
    // Example:
    // q.enqueue(10);
    // q.enqueue(20);
    // q.dequeue();

    return 0;
}
```

In this example, the constructor `Queue()` initializes the `front` and `rear` indices to -1, indicating that the queue is empty. You can add other member functions like `enqueue`, `dequeue`, `isEmpty`, `isFull`, etc., depending on the functionality you need for your queue.

### 1. Algorithms & Data Structures (C++): Queue: Dequeue

In C++, dequeuing from a queue typically involves removing an element from the front of the queue. Here's how you can dequeue from a queue using the `std::queue` container from the C++ Standard Library:

```cpp
#include <iostream>
#include <queue>

int main() {
    std::queue<int> myQueue;

    // Enqueue some elements
    myQueue.push(10);
    myQueue.push(20);
    myQueue.push(30);

    // Dequeue the front element
    if (!myQueue.empty()) {
        std::cout << "Dequeued element: " << myQueue.front() << std::endl;
        myQueue.pop();
    } else {
        std::cout << "Queue is empty. Cannot dequeue." << std::endl;
    }

    return 0;
}
```

In this example, `myQueue.front()` returns a reference to the front element of the queue, and `myQueue.pop()` removes that element from the queue. Always make sure to check if the queue is empty before dequeuing to avoid undefined behavior.

### 1. Algorithms & Data Structures (C++): Queue: Enqueue

Certainly! In C++, the enqueue operation adds an element to the rear end of the queue. Here's a simple implementation of the enqueue operation for a queue using a linked list:

```cpp
#include <iostream>

// Define the structure of a node
struct Node {
    int data;
    Node* next;
    
    Node(int val) : data(val), next(nullptr) {}
};

// Define the Queue class
class Queue {
private:
    Node* front;
    Node* rear;
    
public:
    Queue() : front(nullptr), rear(nullptr) {}
    
    // Enqueue operation to add an element to the rear end of the queue
    void enqueue(int val) {
        Node* newNode = new Node(val);
        
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            rear->next = newNode;
            rear = newNode;
        }
    }
    
    // Utility function to check if the queue is empty
    bool isEmpty() {
        return front == nullptr;
    }
    
    // Function to display the queue
    void display() {
        if (isEmpty()) {
            std::cout << "Queue is empty." << std::endl;
            return;
        }
        
        Node* temp = front;
        while (temp != nullptr) {
            std::cout << temp->data << " ";
            temp = temp->next;
        }
        std::cout << std::endl;
    }
};

int main() {
    Queue q;
    
    // Enqueue some elements
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    
    // Display the queue
    std::cout << "Queue after enqueue operations: ";
    q.display();
    
    return 0;
}
```

In this code:

* We define a structure `Node` to represent the elements of the queue.
* We define the `Queue` class with two private pointers `front` and `rear` pointing to the front and rear of the queue, respectively.
* The `enqueue` function inserts a new node with the given value at the rear end of the queue.
* The `isEmpty` function checks if the queue is empty.
* The `display` function prints the elements of the queue.

### 1. Algorithms & Data Structures (C++): Queue: First Non-Repeating Letter

To solve this problem efficiently, you can use a queue and a hash map (unordered_map in C++) to keep track of the frequency of each character as well as their order of appearance. Here's how you can implement the solution in C++:

```cpp
#include <iostream>
#include <queue>
#include <unordered_map>

char firstNonRepeatingLetter(const std::string& str) {
    std::unordered_map<char, int> frequency;
    std::queue<char> nonRepeatingChars;

    for (char c : str) {
        frequency[c]++;
        if (frequency[c] == 1) {
            // First occurrence of c
            nonRepeatingChars.push(c);
        } else {
            // If it's a repeating character, we remove it from the queue
            while (!nonRepeatingChars.empty() && frequency[nonRepeatingChars.front()] > 1) {
                nonRepeatingChars.pop();
            }
        }
    }

    if (nonRepeatingChars.empty()) {
        // If there are no non-repeating characters, return a special value like '\0'
        return '\0';
    } else {
        // Otherwise, return the first non-repeating character
        return nonRepeatingChars.front();
    }
}

int main() {
    std::string str = "abaccdeff";
    char result = firstNonRepeatingLetter(str);
    if (result != '\0') {
        std::cout << "First non-repeating letter: " << result << std::endl;
    } else {
        std::cout << "No non-repeating letters found." << std::endl;
    }
    return 0;
}
```

This code iterates through the given string, maintaining a frequency count of each character encountered so far. It also maintains a queue of characters that have appeared exactly once. Whenever a character is encountered, it checks if it's the first occurrence or not. If it's the first occurrence, it pushes it into the queue. If it's not the first occurrence, it removes it from the queue if it's present, as it's no longer a candidate for the first non-repeating character.

Finally, it returns the front element of the queue, which represents the first non-repeating character, or a special value (like '\0') if no such character exists.

### 1. Algorithms & Data Structures (C++): Queue: How to Weave

Weaving queues is a common operation in computer science where you interleave the elements of two queues into a single queue. This operation is often used in multithreading, scheduling, and various other applications.

Here's a basic approach to weave two queues in C++:

```cpp
#include <iostream>
#include <queue>

using namespace std;

// Function to weave two queues
queue<int> weave(queue<int>& q1, queue<int>& q2) {
    queue<int> result;

    while (!q1.empty() || !q2.empty()) {
        if (!q1.empty()) {
            result.push(q1.front());
            q1.pop();
        }
        if (!q2.empty()) {
            result.push(q2.front());
            q2.pop();
        }
    }

    return result;
}

int main() {
    queue<int> q1, q2;
    q1.push(1);
    q1.push(2);
    q1.push(3);

    q2.push(4);
    q2.push(5);
    q2.push(6);

    queue<int> wovenQueue = weave(q1, q2);

    cout << "Woven Queue: ";
    while (!wovenQueue.empty()) {
        cout << wovenQueue.front() << " ";
        wovenQueue.pop();
    }
    cout << endl;

    return 0;
}
```

In this example, we have two queues `q1` and `q2` with elements `[1, 2, 3]` and `[4, 5, 6]` respectively. The `weave` function takes these two queues, iterates through them, and interleaves their elements into the `result` queue. Finally, in the `main` function, we call `weave` with `q1` and `q2`, and then print the resulting woven queue.

This code outputs:

```bash
Woven Queue: 1 4 2 5 3 6
```

This demonstrates how the elements of both queues are interleaved into a single queue.

### 1. Algorithms & Data Structures (C++): Queue: Peek

In C++, the "peek" operation on a queue refers to examining the element at the front of the queue without removing it. Here's how you can implement a peek operation on a queue using the standard library `std::queue`:

```cpp
#include <iostream>
#include <queue>

template <typename T>
T peekQueue(std::queue<T>& q) {
    if (!q.empty()) {
        return q.front(); // Return the element at the front of the queue
    } else {
        std::cerr << "Error: Queue is empty. Peek operation cannot be performed.\n";
        // You might want to handle this error condition differently based on your needs
        exit(1); // Exiting the program due to error
    }
}

int main() {
    std::queue<int> myQueue;

    // Insert some elements into the queue
    myQueue.push(10);
    myQueue.push(20);
    myQueue.push(30);

    // Peeking at the front element of the queue
    int frontElement = peekQueue(myQueue);
    std::cout << "Front element of the queue: " << frontElement << std::endl;

    return 0;
}
```

In this example, `peekQueue()` is a function template that takes a reference to a queue and returns the front element of the queue. It checks if the queue is empty before performing the operation to avoid errors. In the `main()` function, we demonstrate how to use `peekQueue()` to peek at the front element of a queue of integers.

### 1. Algorithms & Data Structures (C++): Queue: Weave

The "weave" operation on queues is a common problem in computer science and is often used to combine two queues into one by alternating elements from each. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <queue>

// Function to weave two queues
std::queue<int> weave(std::queue<int>& q1, std::queue<int>& q2) {
    std::queue<int> result;

    while (!q1.empty() || !q2.empty()) {
        if (!q1.empty()) {
            result.push(q1.front());
            q1.pop();
        }
        if (!q2.empty()) {
            result.push(q2.front());
            q2.pop();
        }
    }

    return result;
}

int main() {
    std::queue<int> q1, q2;
    q1.push(1);
    q1.push(3);
    q1.push(5);

    q2.push(2);
    q2.push(4);
    q2.push(6);

    std::queue<int> wovenQueue = weave(q1, q2);

    std::cout << "Woven Queue: ";
    while (!wovenQueue.empty()) {
        std::cout << wovenQueue.front() << " ";
        wovenQueue.pop();
    }
    std::cout << std::endl;

    return 0;
}
```

In this implementation, the `weave` function takes two queues (`q1` and `q2`) as input and returns a new queue that contains elements from both queues, alternately. The implementation uses a `while` loop to iterate until both queues are empty. In each iteration, it checks if `q1` or `q2` is not empty, then pushes the front element of that queue into the `result` queue and pops the front element from the respective queue. Finally, it returns the `result` queue containing the woven elements.

### 1. Algorithms & Data Structures (C++): Queue: What's a Weave?

In the context of algorithms and data structures, a "weave" operation typically refers to combining two queues into one, by alternating elements from each queue. This operation is commonly used in scenarios where you need to interleave or merge elements from two separate queues while maintaining their order.

Here's how the weave operation works:

1. You have two separate queues, let's call them `q1` and `q2`.
2. You create a new empty queue, let's call it `resultQueue`, where you'll store the weaved elements.
3. While both `q1` and `q2` are not empty:
   * Dequeue an element from `q1` and enqueue it into `resultQueue`.
   * Dequeue an element from `q2` and enqueue it into `resultQueue`.
4. If there are any remaining elements in `q1` or `q2`, enqueue them into `resultQueue`.
5. Now, `resultQueue` contains the elements of both `q1` and `q2` interleaved in the order they were originally in the input queues.

This operation is particularly useful in scenarios where you have tasks or events from two different sources (represented by the queues) that you want to process alternately or in a specific order. It's commonly used in various algorithms and applications involving parallel processing, scheduling, and more.

### 1. Algorithms & Data Structures (C++): Queues

Queues are fundamental data structures in computer science that follow the First-In-First-Out (FIFO) principle, akin to a line in a supermarket. In C++, queues are typically implemented using the Standard Template Library (STL) `queue` container, which provides all the necessary functionalities. Here's a basic overview and example usage:

### Overview

* **Queue**: A linear data structure where elements are inserted from one end called the rear (also known as tail) and deleted from the other end called the front (also known as head). Thus, it follows the FIFO order.

* **Operations** typically supported:
  * `enqueue()` or `push()`: Adds an element to the rear of the queue.
  * `dequeue()` or `pop()`: Removes an element from the front of the queue.
  * `front()`: Returns the element at the front without removing it.
  * `back()`: Returns the element at the rear without removing it.
  * `empty()`: Checks if the queue is empty.
  * `size()`: Returns the number of elements in the queue.

### Example Usage

```cpp
#include <iostream>
#include <queue>

int main() {
    // Creating a queue of integers
    std::queue<int> myQueue;

    // Enqueue elements
    myQueue.push(10);
    myQueue.push(20);
    myQueue.push(30);

    // Displaying the front and rear elements
    std::cout << "Front element: " << myQueue.front() << std::endl; // Output: 10
    std::cout << "Rear element: " << myQueue.back() << std::endl;   // Output: 30

    // Dequeue elements
    myQueue.pop();

    // Displaying the front element after dequeue
    std::cout << "Front element after dequeue: " << myQueue.front() << std::endl; // Output: 20

    // Checking if the queue is empty
    if (myQueue.empty()) {
        std::cout << "Queue is empty." << std::endl;
    } else {
        std::cout << "Queue is not empty." << std::endl;
    }

    // Getting the size of the queue
    std::cout << "Size of the queue: " << myQueue.size() << std::endl; // Output: 2

    return 0;
}
```

### Complexity Analysis

* Enqueue (`push`) and dequeue (`pop`) operations take O(1) time complexity.
* Accessing the front or back element (`front` and `back`) takes O(1) time complexity.
* Checking whether the queue is empty (`empty`) also takes O(1) time complexity.
* Getting the size of the queue (`size`) takes O(1) time complexity.

In summary, queues are efficient data structures for scenarios where you need to maintain order and process elements in a FIFO manner, such as in job scheduling, breadth-first search algorithms, and more.

### 1. Algorithms & Data Structures (C++): Queues and DEque

Queues and deque (double-ended queue) are fundamental data structures in computer science. Let's delve into each of them:

### Queues

* **Definition**: A queue is a linear data structure that follows the First In, First Out (FIFO) principle, i.e., the element that is inserted first is the one that is removed first.
* **Operations**:
  * **Enqueue**: Adds an element to the end of the queue.
  * **Dequeue**: Removes an element from the front of the queue.
  * **Peek/Front**: Retrieves the element at the front of the queue without removing it.
  * **isEmpty**: Checks if the queue is empty.
* **Implementation**: Queues can be implemented using arrays or linked lists. In C++, you can use the `std::queue` container from the Standard Template Library (STL) to implement a queue efficiently.

Example C++ code:

```cpp
#include <iostream>
#include <queue>

int main() {
    std::queue<int> myQueue;
    
    myQueue.push(10);
    myQueue.push(20);
    myQueue.push(30);
    
    std::cout << "Front element: " << myQueue.front() << std::endl;
    
    myQueue.pop();
    
    std::cout << "Front element after dequeue: " << myQueue.front() << std::endl;
    
    return 0;
}
```

### Deque (Double-ended Queue)

* **Definition**: A deque, pronounced as "deck", is a generalized queue that allows insertion and deletion at both ends.
* **Operations**:
  * **push_front**: Adds an element to the front of the deque.
  * **push_back**: Adds an element to the back of the deque.
  * **pop_front**: Removes an element from the front of the deque.
  * **pop_back**: Removes an element from the back of the deque.
  * **front**: Retrieves the element at the front of the deque.
  * **back**: Retrieves the element at the back of the deque.
  * **isEmpty**: Checks if the deque is empty.
* **Implementation**: Deques can also be implemented using arrays or linked lists. In C++, you can use the `std::deque` container from the Standard Template Library (STL) to implement a deque efficiently.

Example C++ code:

```cpp
#include <iostream>
#include <deque>

int main() {
    std::deque<int> myDeque;
    
    myDeque.push_front(10);
    myDeque.push_back(20);
    myDeque.push_back(30);
    
    std::cout << "Front element: " << myDeque.front() << std::endl;
    std::cout << "Back element: " << myDeque.back() << std::endl;
    
    myDeque.pop_front();
    
    std::cout << "Front element after pop_front: " << myDeque.front() << std::endl;
    
    return 0;
}
```

Both queues and deques are used extensively in algorithms and real-world applications for tasks such as job scheduling, managing tasks, and implementing various algorithms like breadth-first search (BFS).

### 1. Algorithms & Data Structures (C++): Queues Implementation

Certainly! Implementing a queue in C++ is quite straightforward. A queue is a linear data structure that follows the First In, First Out (FIFO) principle, meaning that the element that is inserted first will be the one to be removed first. Here's a basic implementation of a queue in C++:

```cpp
#include <iostream>

template<typename T>
class Queue {
private:
    struct Node {
        T data;
        Node* next;
        Node(const T& item) : data(item), next(nullptr) {}
    };

    Node* frontNode;
    Node* rearNode;
    int size;

public:
    Queue() : frontNode(nullptr), rearNode(nullptr), size(0) {}

    ~Queue() {
        while (!isEmpty()) {
            dequeue();
        }
    }

    bool isEmpty() const {
        return size == 0;
    }

    int getSize() const {
        return size;
    }

    void enqueue(const T& item) {
        Node* newNode = new Node(item);
        if (isEmpty()) {
            frontNode = newNode;
            rearNode = newNode;
        } else {
            rearNode->next = newNode;
            rearNode = newNode;
        }
        size++;
    }

    void dequeue() {
        if (!isEmpty()) {
            Node* temp = frontNode;
            frontNode = frontNode->next;
            delete temp;
            size--;
            if (isEmpty()) {
                rearNode = nullptr;
            }
        } else {
            std::cerr << "Error: Queue is empty, cannot dequeue.\n";
        }
    }

    T& peek() const {
        if (!isEmpty()) {
            return frontNode->data;
        } else {
            std::cerr << "Error: Queue is empty, cannot peek.\n";
            // Return a default value if needed
            T* defaultValue = new T();
            return *defaultValue;
        }
    }
};
```

In this implementation:

* The `Queue` class is a template class, allowing you to create queues of any data type.
* The `Node` struct represents each element in the queue. It contains the data and a pointer to the next node.
* `frontNode` points to the front of the queue, and `rearNode` points to the rear.
* Operations like `enqueue`, `dequeue`, and `peek` are defined to add, remove, and view elements from the queue, respectively.
* The destructor `~Queue()` is implemented to ensure memory deallocation when the queue is destroyed.

You can use this implementation as follows:

```cpp
int main() {
    Queue<int> myQueue;
    myQueue.enqueue(10);
    myQueue.enqueue(20);
    myQueue.enqueue(30);

    std::cout << "Queue size: " << myQueue.getSize() << std::endl;
    std::cout << "Front element: " << myQueue.peek() << std::endl;

    myQueue.dequeue();

    std::cout << "Queue size after dequeue: " << myQueue.getSize() << std::endl;
    std::cout << "Front element after dequeue: " << myQueue.peek() << std::endl;

    return 0;
}
```

This will output:

```bash
Queue size: 3
Front element: 10
Queue size after dequeue: 2
Front element after dequeue: 20
```

### 1. Algorithms & Data Structures (C++): Queues using Arrays

Sure! Implementing a queue using arrays in C++ is a fundamental exercise in understanding data structures. Here's a basic implementation:

```cpp
#include <iostream>
using namespace std;

#define MAX_SIZE 100

class Queue {
private:
    int arr[MAX_SIZE];
    int front, rear;

public:
    Queue() {
        front = rear = -1; // Initializing front and rear to -1 indicates an empty queue
    }

    bool isEmpty() {
        return front == -1 && rear == -1;
    }

    bool isFull() {
        return rear == MAX_SIZE - 1;
    }

    void enqueue(int x) {
        if (isFull()) {
            cout << "Queue is full. Cannot enqueue element.\n";
            return;
        } else if (isEmpty()) {
            front = rear = 0; // For the first element, set both front and rear to 0
        } else {
            rear++;
        }
        arr[rear] = x;
    }

    void dequeue() {
        if (isEmpty()) {
            cout << "Queue is empty. Cannot dequeue element.\n";
            return;
        } else if (front == rear) {
            // If there's only one element in the queue, reset front and rear to -1
            front = rear = -1;
        } else {
            front++;
        }
    }

    int peek() {
        if (isEmpty()) {
            cout << "Queue is empty. No element to peek.\n";
            return -1; // Return a default value or throw an exception
        }
        return arr[front];
    }

    void display() {
        if (isEmpty()) {
            cout << "Queue is empty.\n";
            return;
        }
        cout << "Queue elements: ";
        for (int i = front; i <= rear; i++) {
            cout << arr[i] << " ";
        }
        cout << endl;
    }
};

int main() {
    Queue q;

    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    q.enqueue(40);
    q.display();

    cout << "Element at front: " << q.peek() << endl;

    q.dequeue();
    q.display();

    return 0;
}
```

This code defines a `Queue` class with methods for enqueue, dequeue, peek, and display operations. The queue is implemented using an array of fixed size. Make sure to handle edge cases such as full queue, empty queue, etc., appropriately.

### 1. Algorithms & Data Structures (C++): Queues using Linked List

Certainly! Implementing a queue using a linked list involves creating a linked list where elements are added at one end (rear) and removed from the other end (front). Here's a basic implementation of a queue using a singly linked list in C++:

```cpp
#include <iostream>

// Node structure for the linked list
template <typename T>
struct Node {
    T data;
    Node<T>* next;
    
    Node(const T& val) : data(val), next(nullptr) {}
};

// Queue class
template <typename T>
class Queue {
private:
    Node<T>* front; // Pointer to the front of the queue
    Node<T>* rear;  // Pointer to the rear of the queue

public:
    Queue() : front(nullptr), rear(nullptr) {}

    ~Queue() {
        while (!isEmpty()) {
            dequeue();
        }
    }

    // Function to check if the queue is empty
    bool isEmpty() {
        return front == nullptr;
    }

    // Function to enqueue an element
    void enqueue(const T& value) {
        Node<T>* newNode = new Node<T>(value);
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            rear->next = newNode;
            rear = newNode;
        }
    }

    // Function to dequeue an element
    void dequeue() {
        if (isEmpty()) {
            std::cout << "Queue is empty. Cannot dequeue.\n";
            return;
        }
        Node<T>* temp = front;
        front = front->next;
        delete temp;
        if (front == nullptr) {
            rear = nullptr; // Reset rear when the last element is dequeued
        }
    }

    // Function to get the front element of the queue
    T& peek() {
        if (isEmpty()) {
            throw std::runtime_error("Queue is empty. Cannot peek.");
        }
        return front->data;
    }

    // Function to display the queue
    void display() {
        if (isEmpty()) {
            std::cout << "Queue is empty.\n";
            return;
        }
        Node<T>* temp = front;
        while (temp != nullptr) {
            std::cout << temp->data << " ";
            temp = temp->next;
        }
        std::cout << std::endl;
    }
};

int main() {
    Queue<int> q;
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);
    q.enqueue(40);
    
    q.display(); // Output: 10 20 30 40
    
    std::cout << "Front element: " << q.peek() << std::endl; // Output: Front element: 10
    
    q.dequeue();
    q.display(); // Output: 20 30 40
    
    std::cout << "Front element: " << q.peek() << std::endl; // Output: Front element: 20
    
    return 0;
}
```

In this implementation:

* The `Queue` class contains private member variables `front` and `rear` to keep track of the front and rear of the queue.
* The `enqueue()` function adds elements to the rear of the queue, while the `dequeue()` function removes elements from the front of the queue.
* The `peek()` function returns the front element without removing it.
* The `isEmpty()` function checks if the queue is empty.
* The `display()` function is used to display the elements of the queue.

### 1. Algorithms & Data Structures (C++): Queues Using Stacks

Implementing a queue using stacks is a classic problem in data structures and algorithms. Here's a basic implementation of a queue using two stacks in C++:

```cpp
#include <iostream>
#include <stack>

using namespace std;

class QueueUsingStacks {
private:
    stack<int> inputStack;
    stack<int> outputStack;

public:
    // Add element to the back of the queue
    void enqueue(int x) {
        // Push the element onto the input stack
        inputStack.push(x);
    }

    // Remove element from the front of the queue
    int dequeue() {
        // If output stack is empty, transfer elements from input stack to output stack
        if (outputStack.empty()) {
            while (!inputStack.empty()) {
                outputStack.push(inputStack.top());
                inputStack.pop();
            }
        }

        // If output stack is still empty, the queue is empty
        if (outputStack.empty()) {
            cout << "Queue is empty" << endl;
            return -1; // or throw an exception
        }

        // Pop the front element from the output stack
        int frontElement = outputStack.top();
        outputStack.pop();
        return frontElement;
    }

    // Check if the queue is empty
    bool isEmpty() {
        return inputStack.empty() && outputStack.empty();
    }
};

int main() {
    QueueUsingStacks q;

    // Enqueue some elements
    q.enqueue(1);
    q.enqueue(2);
    q.enqueue(3);

    // Dequeue elements
    cout << q.dequeue() << endl; // Output: 1
    cout << q.dequeue() << endl; // Output: 2

    // Enqueue more elements
    q.enqueue(4);
    q.enqueue(5);

    // Dequeue remaining elements
    cout << q.dequeue() << endl; // Output: 3
    cout << q.dequeue() << endl; // Output: 4
    cout << q.dequeue() << endl; // Output: 5

    // Try dequeueing from an empty queue
    cout << q.dequeue() << endl; // Output: Queue is empty, -1

    return 0;
}
```

In this implementation, we maintain two stacks: `inputStack` and `outputStack`. The `enqueue()` function simply pushes elements onto the `inputStack`. When we want to dequeue an element, if the `outputStack` is empty, we transfer all elements from the `inputStack` to the `outputStack`. Then, we can simply pop from the `outputStack` to get the front element of the queue.

This implementation ensures that the amortized time complexity of both enqueue and dequeue operations is O(1).

### 1. Algorithms & Data Structures (C++): Queues: Implement Queue With Stacks

Sure! Implementing a queue using two stacks is a classic problem in data structures. Here's a simple implementation in C++:

```cpp
#include <iostream>
#include <stack>

using namespace std;

class Queue {
private:
    stack<int> inbox;  // For enqueue operation
    stack<int> outbox; // For dequeue operation

public:
    // Add element to the queue
    void enqueue(int value) {
        inbox.push(value);
    }

    // Remove element from the queue
    int dequeue() {
        if (outbox.empty()) {
            // If outbox is empty, transfer elements from inbox to outbox
            while (!inbox.empty()) {
                outbox.push(inbox.top());
                inbox.pop();
            }
        }

        // Pop the front element from outbox
        if (!outbox.empty()) {
            int frontElement = outbox.top();
            outbox.pop();
            return frontElement;
        }

        // If both stacks are empty, queue is empty
        throw runtime_error("Queue is empty");
    }

    // Check if the queue is empty
    bool isEmpty() {
        return inbox.empty() && outbox.empty();
    }
};

int main() {
    Queue q;

    // Enqueue elements
    q.enqueue(1);
    q.enqueue(2);
    q.enqueue(3);

    // Dequeue elements
    cout << q.dequeue() << endl; // Output: 1
    cout << q.dequeue() << endl; // Output: 2

    // Enqueue more elements
    q.enqueue(4);
    q.enqueue(5);

    // Dequeue remaining elements
    cout << q.dequeue() << endl; // Output: 3
    cout << q.dequeue() << endl; // Output: 4
    cout << q.dequeue() << endl; // Output: 5

    // Trying to dequeue from an empty queue
    // cout << q.dequeue() << endl; // This will throw a runtime_error

    return 0;
}
```

In this implementation, the `enqueue()` operation is straightforward; it simply pushes the element onto the `inbox` stack.

For the `dequeue()` operation, we need to ensure that the oldest element in the queue is at the top of the `outbox` stack. If the `outbox` is empty, we transfer all elements from `inbox` to `outbox`, effectively reversing their order. Then we pop the top element from `outbox`, which corresponds to the oldest element in the queue.

The `isEmpty()` function checks if both stacks are empty, indicating that the queue is empty.

This implementation ensures that both enqueue and dequeue operations have an amortized O(1) time complexity.

### 1. Algorithms & Data Structures (C++): Representation of Queues

In C++, queues can be represented using various data structures, with the most common being arrays and linked lists. Here, I'll provide you with basic implementations of queues using both arrays and linked lists.

### Using Arrays

```cpp
#include <iostream>
#define SIZE 10

using namespace std;

class Queue {
private:
    int front, rear, capacity;
    int* array;

public:
    Queue(int size = SIZE);  // Constructor
    ~Queue();  // Destructor

    void enqueue(int item);  // Add an item to the queue
    int dequeue();  // Remove an item from the queue
    bool isEmpty();  // Check if the queue is empty
    bool isFull();  // Check if the queue is full
};

Queue::Queue(int size) {
    capacity = size;
    front = rear = -1;
    array = new int[capacity];
}

Queue::~Queue() {
    delete[] array;
}

void Queue::enqueue(int item) {
    if (isFull()) {
        cout << "Queue is full\n";
        return;
    }
    rear = (rear + 1) % capacity;
    array[rear] = item;
    if (front == -1)
        front = rear;
}

int Queue::dequeue() {
    if (isEmpty()) {
        cout << "Queue is empty\n";
        return -1;
    }
    int item = array[front];
    if (front == rear)
        front = rear = -1;
    else
        front = (front + 1) % capacity;
    return item;
}

bool Queue::isEmpty() {
    return front == -1;
}

bool Queue::isFull() {
    return (rear + 1) % capacity == front;
}

int main() {
    Queue queue(5);

    queue.enqueue(1);
    queue.enqueue(2);
    queue.enqueue(3);
    queue.enqueue(4);
    queue.enqueue(5);

    cout << "Dequeued item: " << queue.dequeue() << endl;
    cout << "Dequeued item: " << queue.dequeue() << endl;

    queue.enqueue(6);

    cout << "Dequeued item: " << queue.dequeue() << endl;
    cout << "Dequeued item: " << queue.dequeue() << endl;
    cout << "Dequeued item: " << queue.dequeue() << endl;
    cout << "Dequeued item: " << queue.dequeue() << endl;

    return 0;
}
```

### Using Linked Lists

```cpp
#include <iostream>

using namespace std;

struct Node {
    int data;
    Node* next;
};

class Queue {
private:
    Node *front, *rear;

public:
    Queue();  // Constructor
    ~Queue();  // Destructor

    void enqueue(int item);  // Add an item to the queue
    int dequeue();  // Remove an item from the queue
    bool isEmpty();  // Check if the queue is empty
};

Queue::Queue() {
    front = rear = nullptr;
}

Queue::~Queue() {
    while (!isEmpty()) {
        dequeue();
    }
}

void Queue::enqueue(int item) {
    Node* newNode = new Node;
    newNode->data = item;
    newNode->next = nullptr;
    if (isEmpty()) {
        front = rear = newNode;
    } else {
        rear->next = newNode;
        rear = newNode;
    }
}

int Queue::dequeue() {
    if (isEmpty()) {
        cout << "Queue is empty\n";
        return -1;
    }
    int item = front->data;
    Node* temp = front;
    if (front == rear) {
        front = rear = nullptr;
    } else {
        front = front->next;
    }
    delete temp;
    return item;
}

bool Queue::isEmpty() {
    return front == nullptr;
}

int main() {
    Queue queue;

    queue.enqueue(1);
    queue.enqueue(2);
    queue.enqueue(3);
    queue.enqueue(4);
    queue.enqueue(5);

    cout << "Dequeued item: " << queue.dequeue() << endl;
    cout << "Dequeued item: " << queue.dequeue() << endl;

    queue.enqueue(6);

    cout << "Dequeued item: " << queue.dequeue() << endl;
    cout << "Dequeued item: " << queue.dequeue() << endl;
    cout << "Dequeued item: " << queue.dequeue() << endl;
    cout << "Dequeued item: " << queue.dequeue() << endl;

    return 0;
}
```

Both implementations provide basic functionality for a queue. The array-based implementation has a fixed size, while the linked list implementation can grow dynamically as needed. Choose the appropriate one based on your requirements.

### 1. Algorithms & Data Structures (C++): Representations of Queue

In C++, you can represent a queue using various data structures, but the most common implementations involve arrays or linked lists. Here's how you can implement a queue using both:

1. **Queue using Array:**

```cpp
#include <iostream>
#define MAX_SIZE 100 // Maximum size of the queue

using namespace std;

class Queue {
private:
    int arr[MAX_SIZE];
    int front, rear;

public:
    Queue() {
        front = -1;
        rear = -1;
    }

    bool isEmpty() {
        return (front == -1 && rear == -1);
    }

    bool isFull() {
        return (rear == MAX_SIZE - 1);
    }

    void enqueue(int value) {
        if (isFull()) {
            cout << "Queue is full. Cannot enqueue." << endl;
            return;
        }
        if (isEmpty()) {
            front = rear = 0;
        } else {
            rear++;
        }
        arr[rear] = value;
    }

    void dequeue() {
        if (isEmpty()) {
            cout << "Queue is empty. Cannot dequeue." << endl;
            return;
        }
        if (front == rear) {
            front = rear = -1;
        } else {
            front++;
        }
    }

    int peek() {
        if (isEmpty()) {
            cout << "Queue is empty. No elements to peek." << endl;
            return -1;
        }
        return arr[front];
    }
};

int main() {
    Queue q;
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);

    cout << "Front element: " << q.peek() << endl;

    q.dequeue();
    cout << "Front element after dequeue: " << q.peek() << endl;

    return 0;
}
```

1. **Queue using Linked List:**

```cpp
#include <iostream>

using namespace std;

class Node {
public:
    int data;
    Node* next;

    Node(int value) {
        data = value;
        next = nullptr;
    }
};

class Queue {
private:
    Node* front;
    Node* rear;

public:
    Queue() {
        front = rear = nullptr;
    }

    bool isEmpty() {
        return (front == nullptr && rear == nullptr);
    }

    void enqueue(int value) {
        Node* newNode = new Node(value);
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            rear->next = newNode;
            rear = newNode;
        }
    }

    void dequeue() {
        if (isEmpty()) {
            cout << "Queue is empty. Cannot dequeue." << endl;
            return;
        }
        Node* temp = front;
        if (front == rear) {
            front = rear = nullptr;
        } else {
            front = front->next;
        }
        delete temp;
    }

    int peek() {
        if (isEmpty()) {
            cout << "Queue is empty. No elements to peek." << endl;
            return -1;
        }
        return front->data;
    }
};

int main() {
    Queue q;
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);

    cout << "Front element: " << q.peek() << endl;

    q.dequeue();
    cout << "Front element after dequeue: " << q.peek() << endl;

    return 0;
}
```

Both implementations provide the basic functionalities of a queue: enqueue, dequeue, and peek. Choose the one that suits your needs based on factors like performance, memory usage, and ease of use.

### 1. Algorithms & Data Structures (C++): Reverse a queue

To reverse a queue in C++, you can use another auxiliary data structure, like a stack, to temporarily store the elements of the queue in reverse order. Here's how you can implement this:

```cpp
#include <iostream>
#include <queue>
#include <stack>

using namespace std;

// Function to reverse a queue
void reverseQueue(queue<int> &q) {
    stack<int> s;
    
    // Push elements of queue into stack
    while (!q.empty()) {
        s.push(q.front());
        q.pop();
    }
    
    // Pop elements from stack and push them back into the queue
    while (!s.empty()) {
        q.push(s.top());
        s.pop();
    }
}

// Function to print a queue
void printQueue(queue<int> q) {
    while (!q.empty()) {
        cout << q.front() << " ";
        q.pop();
    }
    cout << endl;
}

int main() {
    // Create a queue
    queue<int> q;
    
    // Push elements into the queue
    q.push(1);
    q.push(2);
    q.push(3);
    q.push(4);
    q.push(5);
    
    cout << "Original queue: ";
    printQueue(q);
    
    // Reverse the queue
    reverseQueue(q);
    
    cout << "Reversed queue: ";
    printQueue(q);
    
    return 0;
}
```

In this code:

1. We use a stack to reverse the order of elements in the queue. We first push all elements of the queue into the stack.
2. Then, we pop elements from the stack and push them back into the queue. Since stacks follow a last in, first out (LIFO) order, this effectively reverses the order of elements.
3. Finally, we have helper functions `printQueue()` to print the elements of the queue before and after the reversal.

This code will output:

```bash
Original queue: 1 2 3 4 5 
Reversed queue: 5 4 3 2 1 
```

And the queue is successfully reversed.

### 1. Algorithms & Data Structures (C++): Reversing a Queue

Sure, here's a C++ implementation of a function to reverse a queue using a stack:

```cpp
#include <iostream>
#include <queue>
#include <stack>

using namespace std;

void reverseQueue(queue<int> &q) {
    stack<int> s;

    // Push all elements of the queue into a stack
    while (!q.empty()) {
        s.push(q.front());
        q.pop();
    }

    // Pop all elements from the stack and enqueue them back into the queue
    while (!s.empty()) {
        q.push(s.top());
        s.pop();
    }
}

int main() {
    // Sample queue
    queue<int> q;
    q.push(1);
    q.push(2);
    q.push(3);
    q.push(4);
    q.push(5);

    // Display original queue
    cout << "Original queue: ";
    while (!q.empty()) {
        cout << q.front() << " ";
        q.pop();
    }
    cout << endl;

    // Restore original queue
    q.push(1);
    q.push(2);
    q.push(3);
    q.push(4);
    q.push(5);

    // Reverse the queue
    reverseQueue(q);

    // Display reversed queue
    cout << "Reversed queue: ";
    while (!q.empty()) {
        cout << q.front() << " ";
        q.pop();
    }
    cout << endl;

    return 0;
}
```

This program defines a `reverseQueue` function that takes a reference to a `queue` of integers as input, and reverses the elements of the queue using a `stack`. Then, in the `main` function, a sample queue is created, displayed, reversed, and displayed again to demonstrate the reversal.

### 1. Algorithms & Data Structures (C++): The FIFO queue implementation idea using Array

Sure! Implementing a FIFO (First-In-First-Out) queue using an array in C++ is a fundamental exercise in data structures. Here's a basic implementation:

```cpp
#include <iostream>

class Queue {
private:
    int capacity; // Maximum capacity of the queue
    int front;    // Index of the front element
    int rear;     // Index of the rear element
    int* array;   // Array to store queue elements

public:
    // Constructor to initialize queue
    Queue(int size) {
        capacity = size;
        front = 0;
        rear = -1;
        array = new int[capacity];
    }

    // Destructor to free allocated memory
    ~Queue() {
        delete[] array;
    }

    // Function to check if the queue is empty
    bool isEmpty() {
        return (rear == -1);
    }

    // Function to check if the queue is full
    bool isFull() {
        return (rear == capacity - 1);
    }

    // Function to add an element to the rear of the queue
    void enqueue(int item) {
        if (isFull()) {
            std::cout << "Queue is full. Cannot enqueue.\n";
            return;
        }
        rear++;
        array[rear] = item;
    }

    // Function to remove an element from the front of the queue
    int dequeue() {
        if (isEmpty()) {
            std::cout << "Queue is empty. Cannot dequeue.\n";
            return -1; // or throw an exception
        }
        int item = array[front];
        front++;
        if (front > rear) {
            // Reset front and rear if queue becomes empty
            front = 0;
            rear = -1;
        }
        return item;
    }

    // Function to get the front element of the queue without removing it
    int peek() {
        if (isEmpty()) {
            std::cout << "Queue is empty. No front element.\n";
            return -1; // or throw an exception
        }
        return array[front];
    }
};

int main() {
    Queue queue(5); // Create a queue of capacity 5

    // Enqueue some elements
    queue.enqueue(10);
    queue.enqueue(20);
    queue.enqueue(30);

    // Print and dequeue elements until the queue is empty
    while (!queue.isEmpty()) {
        std::cout << "Front element: " << queue.peek() << std::endl;
        std::cout << "Dequeued: " << queue.dequeue() << std::endl;
    }

    return 0;
}
```

In this implementation:

* We maintain two indices, `front` and `rear`, to keep track of the front and rear elements respectively.
* The `enqueue` function adds elements to the rear of the queue, and the `dequeue` function removes elements from the front of the queue.
* We also have functions `isEmpty` and `isFull` to check whether the queue is empty or full.
* Memory for the array is dynamically allocated in the constructor and deallocated in the destructor to prevent memory leaks.

This is a basic implementation; you can extend it by adding additional functionality or error handling as needed.

### 1. Algorithms & Data Structures (C++): The Queue Data Structure

Sure! Let's dive into the Queue data structure in C++. A queue is a linear data structure that follows the FIFO (First In First Out) principle, meaning that the element inserted first will be the one to be removed first. This makes it a suitable choice for applications such as task scheduling, breadth-first search algorithms, and more.

In C++, you can implement a queue using various methods, but one of the most common approaches is using the Standard Template Library (STL) `queue` container.

Here's a simple example demonstrating how to use the `queue` container in C++:

```cpp
#include <iostream>
#include <queue>

int main() {
    // Declare a queue of integers
    std::queue<int> myQueue;

    // Insert elements into the queue
    myQueue.push(10);
    myQueue.push(20);
    myQueue.push(30);

    // Display the front element of the queue
    std::cout << "Front element of the queue: " << myQueue.front() << std::endl;

    // Display the size of the queue
    std::cout << "Size of the queue: " << myQueue.size() << std::endl;

    // Remove elements from the queue
    myQueue.pop();
    std::cout << "Size of the queue after popping one element: " << myQueue.size() << std::endl;

    // Check if the queue is empty
    if (myQueue.empty()) {
        std::cout << "The queue is empty." << std::endl;
    } else {
        std::cout << "The queue is not empty." << std::endl;
    }

    return 0;
}
```

Output:

```bash
Front element of the queue: 10
Size of the queue: 3
Size of the queue after popping one element: 2
The queue is not empty.
```

In this example:

* We first include the necessary headers (`iostream` for input/output and `queue` for the queue container).
* Then, we declare a queue of integers using `std::queue<int> myQueue`.
* Elements are inserted into the queue using the `push` method.
* We retrieve the front element of the queue using the `front` method.
* The `size` method returns the number of elements in the queue.
* The `pop` method removes the front element from the queue.
* We use the `empty` method to check if the queue is empty.

This is a basic example, but the `queue` container provides a range of methods for queue manipulation, making it very versatile for various applications.

### 1. Algorithms & Data Structures (C++): Time & Space Complexity : Array Implementation of Queue

In C++, implementing a queue using an array involves maintaining two pointers, one for the front of the queue and the other for the rear. Here's a basic implementation along with the time and space complexity analysis:

```cpp
#include <iostream>

using namespace std;

class Queue {
private:
    int front, rear, capacity;
    int* array;

public:
    Queue(int size) {
        capacity = size;
        front = rear = -1;
        array = new int[capacity];
    }

    ~Queue() {
        delete[] array;
    }

    // Function to enqueue an element to the queue
    void enqueue(int item) {
        if (isFull()) {
            cout << "Queue is full!" << endl;
            return;
        }

        if (isEmpty())
            front = 0;

        array[++rear] = item;
        cout << item << " enqueued to the queue." << endl;
    }

    // Function to dequeue an element from the queue
    int dequeue() {
        if (isEmpty()) {
            cout << "Queue is empty!" << endl;
            return -1;
        }

        int item = array[front++];
        if (front > rear)
            front = rear = -1;

        return item;
    }

    // Function to check if the queue is empty
    bool isEmpty() {
        return front == -1;
    }

    // Function to check if the queue is full
    bool isFull() {
        return rear == capacity - 1;
    }
};

int main() {
    Queue queue(5); // Creating a queue of capacity 5

    queue.enqueue(10);
    queue.enqueue(20);
    queue.enqueue(30);
    queue.enqueue(40);
    queue.enqueue(50);

    cout << "Dequeued item: " << queue.dequeue() << endl;
    cout << "Dequeued item: " << queue.dequeue() << endl;

    queue.enqueue(60);
    queue.enqueue(70);

    return 0;
}
```

#### Time Complexity Analysis

* Enqueue Operation: O(1)
* Dequeue Operation: O(1)
* Accessing any element: O(1)

#### Space Complexity Analysis

* The space complexity is O(n), where n is the capacity of the queue, due to the array used to store the elements.

This implementation has constant time complexity for both enqueue and dequeue operations as they involve simple array manipulations. However, the drawback of this implementation is that it has a fixed capacity, and once that capacity is reached, further enqueue operations will fail.

### 1. Algorithms & Data Structures (C++): Time and Space complexity of Queue

In C++, a queue is a data structure that follows the First-In-First-Out (FIFO) principle, meaning that the element that is inserted first is the one that is removed first. The time and space complexity of various operations on a queue implemented using different data structures can vary.

Let's discuss the time and space complexity of a queue implemented using a linked list and an array:

1. **Queue Implemented using Linked List**:
   * Time Complexity:
     * Enqueue (insertion at the rear): O(1)
     * Dequeue (removal from the front): O(1)
     * Peek (accessing the front element): O(1)
   * Space Complexity: O(n) for storing n elements, where n is the number of elements in the queue.

2. **Queue Implemented using Array**:
   * Time Complexity:
     * Enqueue (insertion at the rear): O(1) on average, but O(n) in the worst case when resizing the array.
     * Dequeue (removal from the front): O(n) due to shifting elements to maintain the queue's order.
     * Peek (accessing the front element): O(1)
   * Space Complexity: O(n) for storing n elements, where n is the size of the array.

It's important to note that while the array-based implementation may have a time complexity of O(1) for enqueue in average case, the worst-case time complexity is O(n) due to resizing the array. Additionally, dequeuing from an array-based queue requires shifting elements, resulting in O(n) time complexity in the worst case.

So, for most practical purposes, both implementations provide constant time complexity for the basic operations. However, the choice between them depends on factors such as the specific use case, the expected size of the queue, and the importance of memory efficiency.

### 1. Algorithms & Data Structures (C++): Ways to implement Priority Queue

In C++, there are several ways to implement a priority queue, each with its own advantages and disadvantages. Here are a few common methods:

1. **Using Standard Template Library (STL)**:
   The simplest way to implement a priority queue in C++ is to use the `std::priority_queue` class provided by the Standard Template Library (STL). It internally uses a heap data structure to maintain the elements in priority order. Here's a basic example:

   ```cpp
   #include <queue>

   int main() {
       std::priority_queue<int> pq;

       pq.push(5);
       pq.push(2);
       pq.push(10);

       while (!pq.empty()) {
           std::cout << pq.top() << " ";
           pq.pop();
       }

       return 0;
   }
   ```

   This would output: `10 5 2`

2. **Using Heap Operations**:
   You can also implement a priority queue using heap operations directly, without relying on the `std::priority_queue` class. This gives you more control over the underlying data structure. You can implement your own heap or use functions like `std::make_heap`, `std::push_heap`, and `std::pop_heap`. Here's a simple example:

   ```cpp
   #include <iostream>
   #include <vector>
   #include <algorithm>

   int main() {
       std::vector<int> heap = {5, 2, 10};

       std::make_heap(heap.begin(), heap.end());

       while (!heap.empty()) {
           std::cout << heap.front() << " ";
           std::pop_heap(heap.begin(), heap.end());
           heap.pop_back();
       }

       return 0;
   }
   ```

   This would also output: `10 5 2`

3. **Using Binary Search Trees (BST)**:
   Another approach is to use a binary search tree (BST) to implement a priority queue. You can use a self-balancing BST like AVL tree or Red-Black tree to maintain the elements in sorted order. This approach allows for efficient insertion and deletion of elements while maintaining sorted order. However, it may not provide the same performance guarantees as using a heap-based approach.

4. **Using an Array or Linked List**:
   While less efficient, you can implement a priority queue using an array or linked list and manually maintain the sorted order of elements. However, this approach typically has worse time complexity for operations like insertion and deletion compared to heap-based implementations.

The choice of implementation depends on factors such as the specific requirements of your application, expected performance characteristics, and ease of implementation. Typically, for most use cases, the `std::priority_queue` from the STL suffices due to its simplicity and good performance characteristics.

### 1. Algorithms & Data Structures (C++): What are Double Ended Queues (DEQue) ?

Double Ended Queues, often abbreviated as DEQue or deque (pronounced "deck"), are a versatile data structure that allows insertion and deletion of elements from both ends. It combines the properties of stacks (Last-In-First-Out, or LIFO) and queues (First-In-First-Out, or FIFO).

In C++, the standard template library (STL) provides a deque container in the `<deque>` header, which implements a double-ended queue efficiently. It allows fast insertions and deletions at both the beginning and the end, as well as random access to elements.

Here are some key characteristics and operations of a deque:

1. **Double-ended**: Elements can be added or removed from both the front and the back of the deque.

2. **Dynamic resizing**: The underlying memory structure of a deque typically dynamically resizes itself to accommodate a varying number of elements efficiently.

3. **Random access**: Unlike some other data structures like linked lists, deques allow for constant-time random access to elements, meaning you can directly access any element with an index.

4. **Efficient insertion and deletion**: Both insertion and deletion operations at either end of the deque have a time complexity of O(1) on average.

5. **Not strictly sequential**: While elements are stored in a sequential manner in memory, they are not necessarily contiguous like arrays, due to the dynamic resizing nature of the deque.

Here are some common operations associated with deques:

* `push_front()`: Adds an element to the front of the deque.
* `pop_front()`: Removes the element from the front of the deque.
* `push_back()`: Adds an element to the back of the deque.
* `pop_back()`: Removes the element from the back of the deque.
* `front()`: Accesses the element at the front of the deque.
* `back()`: Accesses the element at the back of the deque.
* `size()`: Returns the number of elements in the deque.
* `empty()`: Checks if the deque is empty.

Double-ended queues are widely used in various applications where fast insertion and deletion operations are required at both ends of the data structure. They provide a flexible and efficient alternative to other linear data structures like stacks and queues.

### 1. Algorithms & Data Structures (C++): What are Priority Queues ?

Priority queues are abstract data types similar to regular queues but with an added priority associated with each element. In a priority queue, elements are removed based on their priority rather than the order in which they were added.

In a priority queue, each element has an associated priority value, and elements with higher priority values are dequeued before elements with lower priority values. Priority queues are typically implemented using heaps, which allow for efficient insertion, deletion, and retrieval of the highest (or lowest, depending on the implementation) priority element.

In C++, priority queues are provided as part of the Standard Template Library (STL) and can be found in the `<queue>` header. They are implemented as container adaptors, meaning they internally use a container such as a vector or a deque to manage the elements, and provide a high-level interface for operations like insertion and deletion based on priority.

Here's a simple example demonstrating the usage of priority queues in C++:

```cpp
#include <iostream>
#include <queue>

int main() {
    // Create a priority queue of integers
    std::priority_queue<int> pq;

    // Insert elements into the priority queue
    pq.push(30);
    pq.push(10);
    pq.push(50);
    pq.push(20);

    // Print elements of the priority queue
    while (!pq.empty()) {
        std::cout << pq.top() << " ";
        pq.pop();
    }
    std::cout << std::endl;

    return 0;
}
```

In this example, elements (integers) are inserted into the priority queue using the `push()` method, and then they are printed in sorted order (highest to lowest) using the `top()` method to access the highest priority element and `pop()` method to remove it from the queue.

### 1. Algorithms & Data Structures (C++): What are priority queues?

Priority queues are a type of data structure used in computer science to store elements in a way that allows for efficient retrieval of the highest (or lowest) priority element. In a priority queue, each element has an associated priority, and elements with higher priorities are dequeued before those with lower priorities.

In C++, priority queues are typically implemented using binary heaps, although other data structures like Fibonacci heaps can also be used. Binary heaps are complete binary trees where each node satisfies the heap property, meaning that the priority of a parent node is either greater than or equal to (in a max heap) or less than or equal to (in a min heap) the priorities of its children.

C++ provides a `std::priority_queue` container adapter in the `<queue>` header that implements a priority queue using a binary heap. It allows elements to be inserted with a specified priority and supports operations like insertion, extraction of the top element, and checking whether the priority queue is empty.

Here's a basic example of how to use `std::priority_queue` in C++:

```cpp
#include <iostream>
#include <queue>

int main() {
    // Creating a max priority queue of integers
    std::priority_queue<int> maxPriorityQueue;

    // Inserting elements into the priority queue
    maxPriorityQueue.push(30);
    maxPriorityQueue.push(10);
    maxPriorityQueue.push(50);
    maxPriorityQueue.push(20);

    // Printing the top element (highest priority)
    std::cout << "Top element: " << maxPriorityQueue.top() << std::endl;

    // Removing the top element
    maxPriorityQueue.pop();

    // Printing the top element again
    std::cout << "Top element after removal: " << maxPriorityQueue.top() << std::endl;

    return 0;
}
```

In this example, `maxPriorityQueue` is a priority queue that stores integers in a max heap, so the element with the highest value will have the highest priority. The `push()` function is used to insert elements, `top()` retrieves the highest priority element without removing it, and `pop()` removes the highest priority element from the priority queue.

### 1. Algorithms & Data Structures (C++): What are Queues

In the realm of computer science and programming, a queue is a linear data structure that follows the First In, First Out (FIFO) principle. Imagine it as a line of people waiting for something; the person who arrives first is served first, and so on. Similarly, in a queue data structure, the element that is inserted first will be the first one to be removed.

In C++, queues are usually implemented as an adapter on top of other data structures, typically a deque (double-ended queue) or a list. The Standard Template Library (STL) provides a convenient implementation of queues through the `std::queue` class, which is included in the `<queue>` header.

Here's a basic overview of some key operations associated with queues:

1. **Enqueue (Push)**: Adds an element to the back of the queue.
2. **Dequeue (Pop)**: Removes the element from the front of the queue.
3. **Front**: Retrieves the element at the front of the queue without removing it.
4. **Empty**: Checks if the queue is empty.
5. **Size**: Returns the number of elements in the queue.

Here's a simple example of how you might use a queue in C++:

```cpp
#include <iostream>
#include <queue>

int main() {
    std::queue<int> myQueue;

    // Enqueue some elements
    myQueue.push(10);
    myQueue.push(20);
    myQueue.push(30);

    // Dequeue elements and print them
    while (!myQueue.empty()) {
        std::cout << myQueue.front() << " "; // Print the front element
        myQueue.pop(); // Remove the front element
    }
    std::cout << std::endl;

    return 0;
}
```

This program creates a queue of integers, enqueues three elements, and then dequeues them, printing them out in the order they were enqueued (10, 20, 30).

### 1. Algorithms & Data Structures (C++): What are Priority Queues ?

Priority queues are abstract data types similar to regular queues but with an added priority associated with each element. In a priority queue, elements are removed based on their priority rather than the order in which they were added.

In a priority queue, each element has an associated priority value, and elements with higher priority values are dequeued before elements with lower priority values. Priority queues are typically implemented using heaps, which allow for efficient insertion, deletion, and retrieval of the highest (or lowest, depending on the implementation) priority element.

In C++, priority queues are provided as part of the Standard Template Library (STL) and can be found in the `<queue>` header. They are implemented as container adaptors, meaning they internally use a container such as a vector or a deque to manage the elements, and provide a high-level interface for operations like insertion and deletion based on priority.

Here's a simple example demonstrating the usage of priority queues in C++:

```cpp
#include <iostream>
#include <queue>

int main() {
    // Create a priority queue of integers
    std::priority_queue<int> pq;

    // Insert elements into the priority queue
    pq.push(30);
    pq.push(10);
    pq.push(50);
    pq.push(20);

    // Print elements of the priority queue
    while (!pq.empty()) {
        std::cout << pq.top() << " ";
        pq.pop();
    }
    std::cout << std::endl;

    return 0;
}
```

In this example, elements (integers) are inserted into the priority queue using the `push()` method, and then they are printed in sorted order (highest to lowest) using the `top()` method to access the highest priority element and `pop()` method to remove it from the queue.

### 1. Algorithms & Data Structures (C++): What are priority queues?

Priority queues are a type of data structure used in computer science to store elements in a way that allows for efficient retrieval of the highest (or lowest) priority element. In a priority queue, each element has an associated priority, and elements with higher priorities are dequeued before those with lower priorities.

In C++, priority queues are typically implemented using binary heaps, although other data structures like Fibonacci heaps can also be used. Binary heaps are complete binary trees where each node satisfies the heap property, meaning that the priority of a parent node is either greater than or equal to (in a max heap) or less than or equal to (in a min heap) the priorities of its children.

C++ provides a `std::priority_queue` container adapter in the `<queue>` header that implements a priority queue using a binary heap. It allows elements to be inserted with a specified priority and supports operations like insertion, extraction of the top element, and checking whether the priority queue is empty.

Here's a basic example of how to use `std::priority_queue` in C++:

```cpp
#include <iostream>
#include <queue>

int main() {
    // Creating a max priority queue of integers
    std::priority_queue<int> maxPriorityQueue;

    // Inserting elements into the priority queue
    maxPriorityQueue.push(30);
    maxPriorityQueue.push(10);
    maxPriorityQueue.push(50);
    maxPriorityQueue.push(20);

    // Printing the top element (highest priority)
    std::cout << "Top element: " << maxPriorityQueue.top() << std::endl;

    // Removing the top element
    maxPriorityQueue.pop();

    // Printing the top element again
    std::cout << "Top element after removal: " << maxPriorityQueue.top() << std::endl;

    return 0;
}
```

In this example, `maxPriorityQueue` is a priority queue that stores integers in a max heap, so the element with the highest value will have the highest priority. The `push()` function is used to insert elements, `top()` retrieves the highest priority element without removing it, and `pop()` removes the highest priority element from the priority queue.

### 1. Algorithms & Data Structures (C++): What are Queues

In the realm of computer science and programming, a queue is a linear data structure that follows the First In, First Out (FIFO) principle. Imagine it as a line of people waiting for something; the person who arrives first is served first, and so on. Similarly, in a queue data structure, the element that is inserted first will be the first one to be removed.

In C++, queues are usually implemented as an adapter on top of other data structures, typically a deque (double-ended queue) or a list. The Standard Template Library (STL) provides a convenient implementation of queues through the `std::queue` class, which is included in the `<queue>` header.

Here's a basic overview of some key operations associated with queues:

1. **Enqueue (Push)**: Adds an element to the back of the queue.
2. **Dequeue (Pop)**: Removes the element from the front of the queue.
3. **Front**: Retrieves the element at the front of the queue without removing it.
4. **Empty**: Checks if the queue is empty.
5. **Size**: Returns the number of elements in the queue.

Here's a simple example of how you might use a queue in C++:

```cpp
#include <iostream>
#include <queue>

int main() {
    std::queue<int> myQueue;

    // Enqueue some elements
    myQueue.push(10);
    myQueue.push(20);
    myQueue.push(30);

    // Dequeue elements and print them
    while (!myQueue.empty()) {
        std::cout << myQueue.front() << " "; // Print the front element
        myQueue.pop(); // Remove the front element
    }
    std::cout << std::endl;

    return 0;
}
```

This program creates a queue of integers, enqueues three elements, and then dequeues them, printing them out in the order they were enqueued (10, 20, 30).

### 1. Algorithms & Data Structures (C++): What is Queue Data Structure ?

A queue is a fundamental data structure in computer science that follows the First-In-First-Out (FIFO) principle, meaning that the first element added to the queue will be the first one to be removed. It operates much like a queue of people waiting in line; the person who arrived first will be the first one to leave the line.

In a queue, elements are added at the rear (also known as "enqueue") and removed from the front (also known as "dequeue"). This ensures that the oldest element in the queue is always at the front, and the newest element is always at the rear.

Additionally, queues often support other operations such as peek (to view the front element without removing it), isEmpty (to check if the queue is empty), and size (to get the number of elements in the queue).

Queues are commonly used in scenarios such as task scheduling, breadth-first search algorithms, and managing resources in computer systems where the order of processing is important. In C++, you can implement a queue using the `std::queue` container from the Standard Template Library (STL).

### 1. Algorithms & Data Structures (C++): What is Queue?

In C++ programming, a queue is a data structure that follows the First-In-First-Out (FIFO) principle. It's similar to a queue of people waiting in line; the first person to join the line is the first one to be served.

A queue supports two primary operations:

1. **Enqueue**: This operation adds an element to the end of the queue.
2. **Dequeue**: This operation removes an element from the front of the queue.

Other common operations on a queue include:

1. **Front**: Returns the element at the front of the queue without removing it.
1. **Empty**: Checks if the queue is empty.
1. **Size**: Returns the number of elements currently in the queue.

In C++, you can implement a queue using various data structures like arrays, linked lists, or even with the help of the standard library's `std::queue` container. Here's a simple example of implementing a queue using a linked list:

```cpp
#include <iostream>

// Node structure for the linked list
struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

// Queue class using linked list
class Queue {
private:
    Node* front;
    Node* rear;
    int size;

public:
    Queue() : front(nullptr), rear(nullptr), size(0) {}

    void enqueue(int val) {
        Node* newNode = new Node(val);
        if (isEmpty()) {
            front = rear = newNode;
        } else {
            rear->next = newNode;
            rear = newNode;
        }
        size++;
    }

    void dequeue() {
        if (isEmpty()) {
            std::cout << "Queue is empty. Cannot dequeue.\n";
            return;
        }
        Node* temp = front;
        front = front->next;
        delete temp;
        size--;
        if (front == nullptr) {
            rear = nullptr; // if queue becomes empty, reset rear
        }
    }

    int getFront() {
        if (isEmpty()) {
            std::cout << "Queue is empty. No front element.\n";
            return -1; // or throw an exception
        }
        return front->data;
    }

    bool isEmpty() {
        return size == 0;
    }

    int getSize() {
        return size;
    }
};

int main() {
    Queue q;
    q.enqueue(10);
    q.enqueue(20);
    q.enqueue(30);

    std::cout << "Front element: " << q.getFront() << std::endl; // Output: 10

    q.dequeue();
    std::cout << "Front element after dequeue: " << q.getFront() << std::endl; // Output: 20

    return 0;
}
```

This code defines a basic queue using a linked list. It supports enqueue, dequeue, getFront, isEmpty, and getSize operations.
