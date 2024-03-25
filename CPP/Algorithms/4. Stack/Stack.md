### 1. Algorithms & Data Structures (C++): Basic Algorithm for Stack data structure

Sure! Here's a basic algorithm for implementing a stack data structure in C++ using arrays:

```cpp
#include <iostream>
using namespace std;

#define MAX_SIZE 1000

class Stack {
private:
    int top;
    int arr[MAX_SIZE];

public:
    Stack() {
        top = -1;
    }

    bool isEmpty() {
        return (top == -1);
    }

    bool isFull() {
        return (top == MAX_SIZE - 1);
    }

    void push(int val) {
        if (isFull()) {
            cout << "Stack Overflow\n";
            return;
        }
        arr[++top] = val;
        cout << val << " pushed into stack\n";
    }

    int pop() {
        if (isEmpty()) {
            cout << "Stack Underflow\n";
            return -1;
        }
        return arr[top--];
    }

    int peek() {
        if (isEmpty()) {
            cout << "Stack is empty\n";
            return -1;
        }
        return arr[top];
    }
};

int main() {
    Stack myStack;
    myStack.push(1);
    myStack.push(2);
    myStack.push(3);
    cout << "Top element is: " << myStack.peek() << endl;
    cout << myStack.pop() << " popped from stack\n";
    cout << "Top element is: " << myStack.peek() << endl;
    return 0;
}
```

This code implements a basic stack data structure using an array. The `push` function inserts an element into the stack, the `pop` function removes the top element from the stack, and the `peek` function returns the top element without removing it. Additionally, `isEmpty` and `isFull` functions are used to check if the stack is empty or full, respectively.

### 1. Algorithms & Data Structures (C++): Minimum Stack in O(1)

Implementing a minimum stack in C++ with O(1) time complexity for all operations involves using an auxiliary stack to keep track of the minimum element at the top of the main stack. Here's a basic implementation:

```cpp
#include <iostream>
#include <stack>

using namespace std;

class MinStack {
private:
    stack<int> mainStack;
    stack<int> minStack;

public:
    void push(int x) {
        mainStack.push(x);
        if (minStack.empty() || x <= minStack.top())
            minStack.push(x);
    }

    void pop() {
        if (mainStack.top() == minStack.top())
            minStack.pop();
        mainStack.pop();
    }

    int top() {
        return mainStack.top();
    }

    int getMin() {
        return minStack.top();
    }

    bool empty() {
        return mainStack.empty();
    }
};

int main() {
    MinStack minStack;
    minStack.push(5);
    minStack.push(2);
    minStack.push(4);
    minStack.push(1);

    cout << "Minimum element: " << minStack.getMin() << endl; // Output: 1

    minStack.pop();
    cout << "Top element after pop: " << minStack.top() << endl; // Output: 4

    cout << "Minimum element after pop: " << minStack.getMin() << endl; // Output: 2

    return 0;
}
```

Explanation:

- The `mainStack` holds the elements as usual.
- The `minStack` keeps track of the minimum element so far. It only pushes the new minimum onto the stack or if the element being pushed onto the main stack is smaller or equal to the current minimum.
- When popping, if the element being popped from the main stack is the minimum, we also pop it from the `minStack`.

This way, `push`, `pop`, `top`, and `getMin` operations all have O(1) time complexity.

### 1. Algorithms & Data Structures (C++): Another Application of stack - Recursion

Recursion and stacks are closely related in computer science. When a function calls itself, the computer needs to keep track of each call so it knows where to return after each function call completes. This tracking is often done using a data structure called the "call stack."

In C++, recursion can be implemented using function calls. Each time a function is called recursively, the current state of the function (including its arguments and local variables) is pushed onto the call stack. When a base case is reached, the function calls start returning, popping the call stack and allowing the program to resume execution at each previous call site.

Let's take a simple example to illustrate this concept: calculating the factorial of a number recursively.

```cpp
#include <iostream>

// Recursive function to calculate factorial
int factorial(int n) {
    // Base case: factorial of 0 is 1
    if (n == 0) {
        return 1;
    } else {
        // Recursive case: n! = n * (n-1)!
        return n * factorial(n - 1);
    }
}

int main() {
    int n = 5;
    std::cout << "Factorial of " << n << " is " << factorial(n) << std::endl;
    return 0;
}
```

When `factorial(5)` is called, the following sequence of function calls and returns occurs:

1. `factorial(5)` calls `factorial(4)`
2. `factorial(4)` calls `factorial(3)`
3. `factorial(3)` calls `factorial(2)`
4. `factorial(2)` calls `factorial(1)`
5. `factorial(1)` calls `factorial(0)`

At this point, `factorial(0)` returns 1, and the subsequent calls start returning:

1. `factorial(1)` returns 1 * 1 = 1
1. `factorial(2)` returns 2 * 1 = 2
1. `factorial(3)` returns 3 * 2 = 6
1. `factorial(4)` returns 4 * 6 = 24
1. `factorial(5)` returns 5 * 24 = 120

This process is made possible by the call stack, which keeps track of each function call and its state until the base case is reached and the returns start happening. So, recursion relies on the stack data structure to manage function calls and returns efficiently.

### 1. Algorithms & Data Structures (C++): Array Representation of Stack

In C++, you can represent a stack using an array. Here's a simple implementation:

```cpp
#include <iostream>

#define MAX_SIZE 1000 // Define the maximum size of the stack

class Stack {
private:
    int arr[MAX_SIZE]; // Array to store elements
    int top; // Index of the top element

public:
    // Constructor
    Stack() {
        top = -1; // Initialize top to -1 (empty stack)
    }

    // Push operation: add an element to the top of the stack
    void push(int x) {
        if (top >= MAX_SIZE - 1) {
            std::cout << "Stack Overflow\n";
            return;
        }
        arr[++top] = x;
        std::cout << x << " pushed into stack\n";
    }

    // Pop operation: remove and return the top element from the stack
    int pop() {
        if (top < 0) {
            std::cout << "Stack Underflow\n";
            return -1; // Return a dummy value indicating underflow
        }
        int poppedElement = arr[top--];
        return poppedElement;
    }

    // Peek operation: return the top element of the stack without removing it
    int peek() {
        if (top < 0) {
            std::cout << "Stack is Empty\n";
            return -1; // Return a dummy value indicating underflow
        }
        return arr[top];
    }

    // Utility function to check if the stack is empty
    bool isEmpty() {
        return (top < 0);
    }
};

int main() {
    Stack stack;

    stack.push(10);
    stack.push(20);
    stack.push(30);

    std::cout << stack.pop() << " popped from stack\n";

    std::cout << "Top element is: " << stack.peek() << std::endl;

    std::cout << "Is the stack empty? " << (stack.isEmpty() ? "Yes" : "No") << std::endl;

    return 0;
}
```

This implementation uses an array to store the elements of the stack and keeps track of the index of the top element. The `push` operation adds an element to the top of the stack, the `pop` operation removes and returns the top element, the `peek` operation returns the top element without removing it, and `isEmpty` checks if the stack is empty.

Keep in mind that this implementation has a fixed maximum size for the stack (`MAX_SIZE`). If you need a dynamically resizable stack, you may want to consider using a `std::vector` instead of a raw array.

### 1. Algorithms & Data Structures (C++): C++ class for Stack using Linked List

Sure, here's a simple implementation of a stack using a linked list in C++:

```cpp
#include <iostream>

// Define a structure for a node in the linked list
template <typename T>
struct Node {
    T data;
    Node<T>* next;
    Node(T val) : data(val), next(nullptr) {}
};

// Define the Stack class
template <typename T>
class Stack {
private:
    Node<T>* top; // Pointer to the top of the stack
    int size;     // Size of the stack

public:
    // Constructor
    Stack() : top(nullptr), size(0) {}

    // Destructor to deallocate memory
    ~Stack() {
        while (!isEmpty()) {
            pop();
        }
    }

    // Function to check if the stack is empty
    bool isEmpty() {
        return top == nullptr;
    }

    // Function to push an element onto the stack
    void push(T val) {
        Node<T>* newNode = new Node<T>(val);
        newNode->next = top;
        top = newNode;
        size++;
    }

    // Function to pop an element from the stack
    T pop() {
        if (isEmpty()) {
            std::cerr << "Error: Stack is empty.\n";
            exit(EXIT_FAILURE);
        }
        Node<T>* temp = top;
        T data = temp->data;
        top = top->next;
        delete temp;
        size--;
        return data;
    }

    // Function to return the top element of the stack
    T peek() {
        if (isEmpty()) {
            std::cerr << "Error: Stack is empty.\n";
            exit(EXIT_FAILURE);
        }
        return top->data;
    }

    // Function to return the size of the stack
    int getSize() {
        return size;
    }
};

// Main function for testing the stack
int main() {
    Stack<int> stack;
    stack.push(1);
    stack.push(2);
    stack.push(3);

    std::cout << "Top element: " << stack.peek() << std::endl;
    std::cout << "Size of stack: " << stack.getSize() << std::endl;

    while (!stack.isEmpty()) {
        std::cout << "Popped element: " << stack.pop() << std::endl;
    }

    return 0;
}
```

This implementation provides basic operations like push, pop, peek, and checking if the stack is empty. The stack is implemented using a singly linked list, with each element pushed onto the top of the stack.

### 1. Algorithms & Data Structures (C++): Concurrent Queue and Concurrent Stack

Certainly! Implementing concurrent data structures like a concurrent queue and concurrent stack in C++ typically involves synchronization mechanisms like mutexes or atomic operations to ensure thread safety. Let's start with a concurrent queue:

```cpp
#include <iostream>
#include <queue>
#include <mutex>
#include <condition_variable>

template<typename T>
class ConcurrentQueue {
private:
    std::queue<T> queue_;
    mutable std::mutex mutex_;
    std::condition_variable cond_;

public:
    void Push(const T& item) {
        std::lock_guard<std::mutex> lock(mutex_);
        queue_.push(item);
        cond_.notify_one();
    }

    bool Pop(T& item) {
        std::unique_lock<std::mutex> lock(mutex_);
        cond_.wait(lock, [this] { return !queue_.empty(); });
        if (queue_.empty()) {
            return false;
        }
        item = queue_.front();
        queue_.pop();
        return true;
    }

    bool Empty() const {
        std::lock_guard<std::mutex> lock(mutex_);
        return queue_.empty();
    }
};
```

Now, let's implement a concurrent stack:

```cpp
#include <iostream>
#include <stack>
#include <mutex>
#include <condition_variable>

template<typename T>
class ConcurrentStack {
private:
    std::stack<T> stack_;
    mutable std::mutex mutex_;
    std::condition_variable cond_;

public:
    void Push(const T& item) {
        std::lock_guard<std::mutex> lock(mutex_);
        stack_.push(item);
        cond_.notify_one();
    }

    bool Pop(T& item) {
        std::unique_lock<std::mutex> lock(mutex_);
        cond_.wait(lock, [this] { return !stack_.empty(); });
        if (stack_.empty()) {
            return false;
        }
        item = stack_.top();
        stack_.pop();
        return true;
    }

    bool Empty() const {
        std::lock_guard<std::mutex> lock(mutex_);
        return stack_.empty();
    }
};
```

Both implementations use a mutex to ensure that only one thread can access the data structure at a time, preventing race conditions. Additionally, a condition variable is used to handle cases where a thread needs to wait for the data structure to become non-empty before proceeding.

Remember to be cautious with concurrent data structures, as they can introduce overhead and potential for deadlock if not used carefully. Testing thoroughly with multiple threads is crucial to ensure correctness and performance.

### 1. Algorithms & Data Structures (C++): Create Stack that returns the Smallest Element in const time

To create a stack data structure that can return the smallest element in constant time, you can use an additional auxiliary stack to keep track of the minimum element at each level of the main stack. Here's how you can implement it in C++:

```cpp
#include <stack>
#include <iostream>

template<typename T>
class MinStack {
private:
    std::stack<T> mainStack;
    std::stack<T> minStack;

public:
    // Push element onto the stack
    void push(const T& value) {
        mainStack.push(value);
        if (minStack.empty() || value <= minStack.top()) {
            minStack.push(value);
        }
    }

    // Remove and return the top element from the stack
    void pop() {
        if (mainStack.empty()) {
            std::cerr << "Stack is empty. Cannot pop.\n";
            return;
        }
        if (mainStack.top() == minStack.top()) {
            minStack.pop();
        }
        mainStack.pop();
    }

    // Return the top element of the stack
    T top() const {
        if (mainStack.empty()) {
            throw std::logic_error("Stack is empty.");
        }
        return mainStack.top();
    }

    // Return the smallest element in the stack in O(1) time
    T getMin() const {
        if (minStack.empty()) {
            throw std::logic_error("Stack is empty.");
        }
        return minStack.top();
    }

    // Check if the stack is empty
    bool empty() const {
        return mainStack.empty();
    }

    // Return the size of the stack
    size_t size() const {
        return mainStack.size();
    }
};

int main() {
    MinStack<int> minStack;
    minStack.push(5);
    minStack.push(3);
    minStack.push(7);
    minStack.push(2);
    minStack.push(8);

    std::cout << "Minimum element: " << minStack.getMin() << std::endl;

    minStack.pop(); // Remove 8
    minStack.pop(); // Remove 2

    std::cout << "Minimum element after popping: " << minStack.getMin() << std::endl;

    return 0;
}
```

In this implementation, whenever a new element is pushed onto the main stack, it is also checked if it's smaller than or equal to the top element of the auxiliary stack (minStack). If it is, the element is pushed onto the minStack as well. This ensures that the minStack always contains the minimum element seen so far. When popping elements from the main stack, if the top element of the main stack is the same as the top element of the minStack, it's removed from the minStack too. This way, the minimum element is always accessible in constant time.

### 1. Algorithms & Data Structures (C++): Create Stack that returns the Smallest Element with One stack

You can create a stack data structure that returns the smallest element efficiently using a single stack and keeping track of the minimum element. Here's a basic implementation in C++:

```cpp
#include <iostream>
#include <stack>

using namespace std;

class MinStack {
private:
    stack<int> st;
    int minElem;

public:
    MinStack() {
        minElem = INT_MAX;
    }

    void push(int val) {
        if (val <= minElem) {
            st.push(minElem);
            minElem = val;
        }
        st.push(val);
    }

    void pop() {
        if (st.top() == minElem) {
            st.pop();
            minElem = st.top();
            st.pop();
        } else {
            st.pop();
        }
    }

    int top() {
        return st.top();
    }

    int getMin() {
        return minElem;
    }
};

int main() {
    MinStack stack;
    stack.push(5);
    stack.push(2);
    stack.push(3);
    stack.push(1);

    cout << "Current Minimum: " << stack.getMin() << endl;

    stack.pop();
    cout << "Current Minimum after popping: " << stack.getMin() << endl;

    return 0;
}
```

This implementation ensures that every time a new minimum element is encountered during push, it's pushed onto the stack along with the new element. When popping, if the top element is the minimum element, both the top element and the current minimum are popped out and the next minimum is updated. Otherwise, just the top element is popped. This way, you always have access to the minimum element in constant time without using any additional data structures.

### 1. Algorithms & Data Structures (C++): Create Stack using Linked List

Sure! Below is an implementation of a stack using a linked list in C++:

```cpp
#include <iostream>

// Node class for the linked list
template <typename T>
class Node {
public:
    T data;
    Node* next;

    Node(T val) {
        data = val;
        next = nullptr;
    }
};

// Stack class
template <typename T>
class Stack {
private:
    Node<T>* topNode;

public:
    Stack() {
        topNode = nullptr;
    }

    ~Stack() {
        while (!isEmpty()) {
            pop();
        }
    }

    // Check if the stack is empty
    bool isEmpty() {
        return topNode == nullptr;
    }

    // Push an element onto the stack
    void push(T val) {
        Node<T>* newNode = new Node<T>(val);
        newNode->next = topNode;
        topNode = newNode;
    }

    // Remove and return the top element from the stack
    T pop() {
        if (isEmpty()) {
            std::cerr << "Stack is empty!" << std::endl;
            exit(EXIT_FAILURE);
        }
        Node<T>* temp = topNode;
        T popped = temp->data;
        topNode = topNode->next;
        delete temp;
        return popped;
    }

    // Return the top element of the stack without removing it
    T top() {
        if (isEmpty()) {
            std::cerr << "Stack is empty!" << std::endl;
            exit(EXIT_FAILURE);
        }
        return topNode->data;
    }
};

// Example usage
int main() {
    Stack<int> stack;
    stack.push(5);
    stack.push(10);
    stack.push(15);

    std::cout << "Top element: " << stack.top() << std::endl;

    std::cout << "Popping elements: ";
    while (!stack.isEmpty()) {
        std::cout << stack.pop() << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this implementation:

- We have a `Node` class to represent each element of the linked list.
- The `Stack` class maintains a pointer to the top node of the linked list (`topNode`).
- `push` function adds an element to the top of the stack by creating a new node and updating pointers.
- `pop` function removes and returns the top element of the stack, updating pointers accordingly.
- `top` function returns the top element of the stack without removing it.
- `isEmpty` function checks if the stack is empty.
- The `main` function demonstrates how to use the stack by pushing elements onto it, printing the top element, and then popping elements from the stack.

### 1. Algorithms & Data Structures (C++): Data Structure : Stacks

Stacks are a fundamental data structure in computer science, operating on the principle of last-in, first-out (LIFO). This means that the last element added to the stack is the first one to be removed. Think of it as a stack of plates where you can only add or remove the top plate.

In C++, you can implement a stack using the standard template library (STL). The `std::stack` class provides a convenient interface for working with stacks. Here's a basic example of how to use it:

```cpp
#include <iostream>
#include <stack>

int main() {
    // Create an empty stack of integers
    std::stack<int> myStack;

    // Push elements onto the stack
    myStack.push(10);
    myStack.push(20);
    myStack.push(30);

    // Print the top element of the stack
    std::cout << "Top element: " << myStack.top() << std::endl;

    // Pop elements from the stack
    myStack.pop();
    myStack.pop();

    // Check if the stack is empty
    if (myStack.empty()) {
        std::cout << "Stack is empty!" << std::endl;
    } else {
        std::cout << "Stack is not empty." << std::endl;
    }

    return 0;
}
```

This code demonstrates basic stack operations:

1. `push(x)`: Adds element `x` to the top of the stack.
2. `pop()`: Removes the top element from the stack.
3. `top()`: Accesses the top element of the stack without removing it.
4. `empty()`: Checks if the stack is empty.

Stacks are commonly used in various algorithms and applications, such as expression evaluation, backtracking, parsing, and more. Understanding how to use stacks efficiently is essential for every programmer.

### 1. Algorithms & Data Structures (C++): Double Stacks

Double stacks refer to a data structure that is essentially two stacks combined into one. This structure allows you to perform stack operations (like push and pop) on two different stacks within the same data structure. It can be implemented using arrays, linked lists, or other underlying data structures.

Here's a basic implementation of double stacks using arrays in C++:

```cpp
#include <iostream>
using namespace std;

#define MAX_SIZE 100

class DoubleStack {
private:
    int arr[MAX_SIZE];
    int top1, top2;

public:
    DoubleStack() {
        top1 = -1; // Initialize top of stack 1
        top2 = MAX_SIZE; // Initialize top of stack 2
    }

    // Function to push an element x to stack1
    void push1(int x) {
        if (top1 < top2 - 1) {
            top1++;
            arr[top1] = x;
        } else {
            cout << "Stack Overflow\n";
        }
    }

    // Function to push an element x to stack2
    void push2(int x) {
        if (top1 < top2 - 1) {
            top2--;
            arr[top2] = x;
        } else {
            cout << "Stack Overflow\n";
        }
    }

    // Function to pop an element from stack1
    int pop1() {
        if (top1 >= 0) {
            int x = arr[top1];
            top1--;
            return x;
        } else {
            cout << "Stack 1 Underflow\n";
            return -1;
        }
    }

    // Function to pop an element from stack2
    int pop2() {
        if (top2 < MAX_SIZE) {
            int x = arr[top2];
            top2++;
            return x;
        } else {
            cout << "Stack 2 Underflow\n";
            return -1;
        }
    }

    // Function to check if stack1 is empty
    bool isEmpty1() {
        return (top1 == -1);
    }

    // Function to check if stack2 is empty
    bool isEmpty2() {
        return (top2 == MAX_SIZE);
    }
};

int main() {
    DoubleStack ds;

    // Pushing elements to stack1
    ds.push1(1);
    ds.push1(2);
    ds.push1(3);

    // Pushing elements to stack2
    ds.push2(11);
    ds.push2(12);
    ds.push2(13);

    // Popping elements from stack1
    cout << ds.pop1() << endl; // Output: 3
    cout << ds.pop1() << endl; // Output: 2

    // Popping elements from stack2
    cout << ds.pop2() << endl; // Output: 13
    cout << ds.pop2() << endl; // Output: 12

    return 0;
}
```

In this implementation, we have an array `arr` of fixed size `MAX_SIZE`, which holds elements for both stacks. We maintain two indices `top1` and `top2` to keep track of the top elements of the two stacks. Stack 1 grows from the beginning of the array (`arr[0]`), while stack 2 grows from the end of the array (`arr[MAX_SIZE - 1]`). We also define functions to perform push, pop, and check if each stack is empty.

### 1. Algorithms & Data Structures (C++): Dynamic Stack

A dynamic stack in C++ typically refers to a stack implementation that can dynamically resize itself when it runs out of capacity. Here's a basic implementation of a dynamic stack using a dynamically allocated array:

```cpp
#include <iostream>

class DynamicStack {
private:
    int *arr;
    int top;
    int capacity;

public:
    // Constructor
    DynamicStack(int size = 10) {
        capacity = size;
        arr = new int[capacity];
        top = -1;
    }

    // Destructor
    ~DynamicStack() {
        delete[] arr;
    }

    // Check if stack is empty
    bool isEmpty() {
        return top == -1;
    }

    // Check if stack is full
    bool isFull() {
        return top == capacity - 1;
    }

    // Push element onto stack
    void push(int element) {
        if (isFull()) {
            // Double the capacity
            int *temp = new int[2 * capacity];
            for (int i = 0; i < capacity; ++i) {
                temp[i] = arr[i];
            }
            delete[] arr;
            arr = temp;
            capacity *= 2;
        }
        arr[++top] = element;
    }

    // Pop element from stack
    int pop() {
        if (isEmpty()) {
            std::cerr << "Stack is empty." << std::endl;
            return -1; // or throw an exception
        }
        return arr[top--];
    }

    // Peek at the top element of the stack
    int peek() {
        if (isEmpty()) {
            std::cerr << "Stack is empty." << std::endl;
            return -1; // or throw an exception
        }
        return arr[top];
    }
};

int main() {
    DynamicStack stack;

    // Push some elements onto the stack
    stack.push(10);
    stack.push(20);
    stack.push(30);

    // Pop and print elements until stack is empty
    while (!stack.isEmpty()) {
        std::cout << stack.pop() << std::endl;
    }

    return 0;
}
```

This implementation dynamically doubles the capacity of the stack when it runs out of space. However, you can adjust the resizing strategy as per your requirements. Also, note that this is a basic implementation, and in practice, you might want to handle more edge cases and error conditions.

### 1. Algorithms & Data Structures (C++): Exercise: Stack & Queue: Animal Shelter

Sure, let's work on that!

The Animal Shelter problem involves implementing a data structure that supports two operations: `enqueue` and `dequeueAny`. `enqueue` adds an animal (either a dog or a cat) to the shelter, and `dequeueAny` removes the oldest animal from the shelter. Additionally, there are `dequeueDog` and `dequeueCat` operations to specifically remove the oldest dog or cat from the shelter.

Here's a possible implementation in C++ using queues:

```cpp
#include <iostream>
#include <queue>
#include <string>

using namespace std;

class Animal {
public:
    string name;
    int order;

    Animal(string n) : name(n), order(0) {}
};

class AnimalShelter {
private:
    queue<Animal> dogs;
    queue<Animal> cats;
    int order;

public:
    AnimalShelter() : order(0) {}

    void enqueue(string name, string type) {
        Animal newAnimal(name);
        newAnimal.order = order++;
        if (type == "dog") {
            dogs.push(newAnimal);
        } else if (type == "cat") {
            cats.push(newAnimal);
        } else {
            cout << "Invalid animal type" << endl;
        }
    }

    Animal dequeueAny() {
        if (dogs.empty() && cats.empty()) {
            throw runtime_error("Shelter is empty");
        } else if (dogs.empty()) {
            return dequeueCat();
        } else if (cats.empty()) {
            return dequeueDog();
        } else {
            if (dogs.front().order < cats.front().order) {
                return dequeueDog();
            } else {
                return dequeueCat();
            }
        }
    }

    Animal dequeueDog() {
        if (dogs.empty()) {
            throw runtime_error("No dogs available");
        }
        Animal dog = dogs.front();
        dogs.pop();
        return dog;
    }

    Animal dequeueCat() {
        if (cats.empty()) {
            throw runtime_error("No cats available");
        }
        Animal cat = cats.front();
        cats.pop();
        return cat;
    }
};

int main() {
    AnimalShelter shelter;

    shelter.enqueue("Max", "dog");
    shelter.enqueue("Bella", "dog");
    shelter.enqueue("Whiskers", "cat");
    shelter.enqueue("Leo", "cat");

    cout << "Adopted: " << shelter.dequeueAny().name << endl; // Adopt oldest animal
    cout << "Adopted: " << shelter.dequeueDog().name << endl; // Adopt oldest dog
    cout << "Adopted: " << shelter.dequeueCat().name << endl; // Adopt oldest cat

    return 0;
}
```

This code provides an implementation of an Animal Shelter using two queues, one for dogs and one for cats. Animals are enqueued with a unique order value, and when dequeueing, the oldest animal (according to order of arrival) is removed from the appropriate queue. The `dequeueAny` function determines whether to dequeue a dog or a cat based on which animal was enqueued first.

### 1. Algorithms & Data Structures (C++): Exercise: Stack & Queue: Queue via Stacks

Sure, I can help you with that! Implementing a queue using two stacks is a classic exercise in data structures. Here's a basic implementation in C++:

```cpp
#include <iostream>
#include <stack>

using namespace std;

class Queue {
private:
    stack<int> inbox;   // For enqueue operation
    stack<int> outbox;  // For dequeue operation

public:
    // Function to enqueue an element to the queue
    void enqueue(int x) {
        inbox.push(x);
    }

    // Function to dequeue an element from the queue
    int dequeue() {
        if (outbox.empty()) {
            // Transfer elements from inbox to outbox
            while (!inbox.empty()) {
                outbox.push(inbox.top());
                inbox.pop();
            }
        }

        if (outbox.empty()) {
            // If both stacks are empty, the queue is empty
            cout << "Queue is empty.\n";
            return -1; // Assuming -1 as an error value
        }

        int front = outbox.top();
        outbox.pop();
        return front;
    }

    // Function to check if the queue is empty
    bool isEmpty() {
        return inbox.empty() && outbox.empty();
    }
};

int main() {
    Queue q;

    q.enqueue(1);
    q.enqueue(2);
    q.enqueue(3);

    cout << "Dequeued: " << q.dequeue() << endl;

    q.enqueue(4);

    cout << "Dequeued: " << q.dequeue() << endl;
    cout << "Dequeued: " << q.dequeue() << endl;
    cout << "Dequeued: " << q.dequeue() << endl;

    return 0;
}
```

This code creates a queue using two stacks. The `inbox` stack is used for enqueue operations, and the `outbox` stack is used for dequeue operations. When you need to dequeue an element, if the `outbox` is empty, you transfer all elements from the `inbox` to the `outbox` to reverse their order, allowing you to simulate a queue.

Feel free to run and test this code, and let me know if you have any questions or need further clarification!

### 1. Algorithms & Data Structures (C++): Exercise: Stack & Queue: Stack Minimum

The "Stack Minimum" problem involves designing a data structure that supports standard stack operations (push, pop, and isEmpty), along with an additional operation to find the minimum element in the stack in constant time.

One approach to solve this problem efficiently is to use an additional stack to keep track of the minimum element at each state of the main stack. Let's call this additional stack `minStack`. Here's a simple implementation in C++:

```cpp
#include <stack>
#include <iostream>

using namespace std;

class MinStack {
private:
    stack<int> mainStack;
    stack<int> minStack;

public:
    // Push element onto the stack
    void push(int x) {
        mainStack.push(x);
        if (minStack.empty() || x <= minStack.top()) {
            minStack.push(x);
        }
    }

    // Remove the element on top of the stack
    void pop() {
        if (mainStack.top() == minStack.top()) {
            minStack.pop();
        }
        mainStack.pop();
    }

    // Get the top element of the stack
    int top() {
        return mainStack.top();
    }

    // Get the minimum element in the stack
    int getMin() {
        return minStack.top();
    }

    // Check if the stack is empty
    bool isEmpty() {
        return mainStack.empty();
    }
};

int main() {
    MinStack stack;
    stack.push(3);
    stack.push(5);
    stack.push(2);
    stack.push(1);

    cout << "Minimum element: " << stack.getMin() << endl; // Output: 1

    stack.pop();
    cout << "Minimum element: " << stack.getMin() << endl; // Output: 2

    return 0;
}
```

In this implementation, whenever you push an element onto the main stack, you also check if it's smaller than or equal to the top element of the `minStack`. If it is, you push it onto the `minStack` as well. When you pop an element from the main stack, you check if it's the same as the top element of the `minStack`, and if it is, you also pop from `minStack`. This way, `minStack` always contains the minimum element at the top.

### 1. Algorithms & Data Structures (C++): Exercise: Stack & Queue: Stack of Plates

The "Stack of Plates" problem is an interesting one. Here's the problem statement:

**Problem Statement:**

Imagine a (literal) stack of plates. If the stack gets too high, it might topple. Therefore, in real life, we would likely start a new stack when the previous stack exceeds some threshold. Implement a data structure `SetOfStacks` that mimics this. `SetOfStacks` should be composed of several stacks and should create a new stack once the previous one exceeds capacity. `SetOfStacks.push()` and `SetOfStacks.pop()` should behave identically to a single stack (that is, `pop()` should return the same values as it would if there were just a single stack).

**Follow-up:**

Implement a function `popAt(int index)` which performs a pop operation on a specific sub-stack.

Would you like a walkthrough of how to approach this problem or some code examples in C++?

### 1. Algorithms & Data Structures (C++): Exercise: Stack & Queue: Three in One

Sure! The "Three in One" exercise typically involves implementing three stacks using a single array in C++. Here's a basic outline of how you can achieve this:

```cpp
#include <iostream>
#include <stdexcept>

class ThreeStacks {
private:
    int* array;
    int size;
    int top1, top2, top3;
    int stackSize;

public:
    ThreeStacks(int stackSize) : size(3 * stackSize), top1(-1), top2(stackSize - 1), top3(2 * stackSize - 1), stackSize(stackSize) {
        array = new int[size];
    }

    ~ThreeStacks() {
        delete[] array;
    }

    void push(int stackNum, int data) {
        if (isFull(stackNum)) {
            std::cerr << "Stack " << stackNum << " is full." << std::endl;
            return;
        }

        switch (stackNum) {
            case 1:
                array[++top1] = data;
                break;
            case 2:
                array[++top2] = data;
                break;
            case 3:
                array[++top3] = data;
                break;
            default:
                std::cerr << "Invalid stack number." << std::endl;
                break;
        }
    }

    int pop(int stackNum) {
        if (isEmpty(stackNum)) {
            std::cerr << "Stack " << stackNum << " is empty." << std::endl;
            return INT_MIN;
        }

        switch (stackNum) {
            case 1:
                return array[top1--];
            case 2:
                return array[top2--];
            case 3:
                return array[top3--];
            default:
                std::cerr << "Invalid stack number." << std::endl;
                return INT_MIN;
        }
    }

    bool isEmpty(int stackNum) const {
        switch (stackNum) {
            case 1:
                return top1 == -1;
            case 2:
                return top2 == stackSize - 1;
            case 3:
                return top3 == 2 * stackSize - 1;
            default:
                std::cerr << "Invalid stack number." << std::endl;
                return true;
        }
    }

    bool isFull(int stackNum) const {
        switch (stackNum) {
            case 1:
                return top1 == stackSize - 1;
            case 2:
                return top2 == 2 * stackSize - 1;
            case 3:
                return top3 == size - 1;
            default:
                std::cerr << "Invalid stack number." << std::endl;
                return true;
        }
    }
};

int main() {
    ThreeStacks stacks(5); // Each stack can hold up to 5 elements

    stacks.push(1, 10);
    stacks.push(1, 20);
    stacks.push(1, 30);

    stacks.push(2, 40);
    stacks.push(2, 50);

    stacks.push(3, 60);
    stacks.push(3, 70);

    std::cout << stacks.pop(1) << std::endl; // Output: 30
    std::cout << stacks.pop(2) << std::endl; // Output: 50
    std::cout << stacks.pop(3) << std::endl; // Output: 70

    return 0;
}
```

In this implementation, we maintain three variables `top1`, `top2`, and `top3` to keep track of the tops of the three stacks. We use these variables to push and pop elements accordingly. The `isEmpty` and `isFull` functions are used to check if a particular stack is empty or full, respectively.

### 1. Algorithms & Data Structures (C++): How to push and pop onto a Stack

In C++, you can implement a stack using the standard template library (STL) `std::stack` or by implementing your own stack data structure. Here's how you can do it using `std::stack`:

```cpp
#include <iostream>
#include <stack>

int main() {
    std::stack<int> myStack;

    // Pushing elements onto the stack
    myStack.push(5);
    myStack.push(10);
    myStack.push(15);

    // Popping elements from the stack
    while (!myStack.empty()) {
        std::cout << myStack.top() << " "; // Print the top element
        myStack.pop(); // Remove the top element
    }

    return 0;
}
```

This code demonstrates how to push elements onto a stack using the `push()` method and pop elements from the stack using the `pop()` method. The `top()` method is used to access the top element of the stack without removing it.

If you want to implement your own stack data structure, you would typically use a dynamically allocated array or a linked list. Here's a simple example using an array:

```cpp
#include <iostream>

class Stack {
private:
    static const int maxSize = 100; // Maximum size of the stack
    int arr[maxSize]; // Array to store elements
    int topIndex; // Index of the top element

public:
    Stack() : topIndex(-1) {} // Constructor

    // Function to push element onto the stack
    void push(int value) {
        if (topIndex >= maxSize - 1) {
            std::cout << "Stack overflow!" << std::endl;
            return;
        }
        arr[++topIndex] = value;
    }

    // Function to pop element from the stack
    int pop() {
        if (topIndex < 0) {
            std::cout << "Stack underflow!" << std::endl;
            return -1; // Or throw an exception
        }
        return arr[topIndex--];
    }

    // Function to get the top element of the stack
    int top() {
        if (topIndex < 0) {
            std::cout << "Stack is empty!" << std::endl;
            return -1; // Or throw an exception
        }
        return arr[topIndex];
    }

    // Function to check if the stack is empty
    bool empty() {
        return topIndex < 0;
    }
};

int main() {
    Stack myStack;

    // Pushing elements onto the stack
    myStack.push(5);
    myStack.push(10);
    myStack.push(15);

    // Popping elements from the stack
    while (!myStack.empty()) {
        std::cout << myStack.top() << " "; // Print the top element
        myStack.pop(); // Remove the top element
    }

    return 0;
}
```

In this implementation, `push()` adds an element to the top of the stack, `pop()` removes the top element, `top()` returns the top element without removing it, and `empty()` checks if the stack is empty.

### 1. Algorithms & Data Structures (C++): Implementation of Stack

Certainly! Here's a simple implementation of a stack data structure in C++:

```cpp
#include <iostream>

using namespace std;

// Define the maximum size of the stack
#define MAX_SIZE 100

class Stack {
private:
    int top;
    int data[MAX_SIZE];

public:
    Stack() {
        top = -1;
    }

    // Check if the stack is empty
    bool isEmpty() {
        return top == -1;
    }

    // Check if the stack is full
    bool isFull() {
        return top == MAX_SIZE - 1;
    }

    // Push element onto the stack
    void push(int value) {
        if (isFull()) {
            cout << "Stack Overflow!" << endl;
            return;
        }
        data[++top] = value;
    }

    // Pop element from the stack
    int pop() {
        if (isEmpty()) {
            cout << "Stack Underflow!" << endl;
            return -1;
        }
        return data[top--];
    }

    // Peek the top element of the stack
    int peek() {
        if (isEmpty()) {
            cout << "Stack is empty!" << endl;
            return -1;
        }
        return data[top];
    }
};

int main() {
    Stack stack;

    // Pushing elements onto the stack
    stack.push(5);
    stack.push(10);
    stack.push(15);

    // Popping elements from the stack
    cout << stack.pop() << " popped from the stack." << endl;
    cout << stack.pop() << " popped from the stack." << endl;

    // Peek the top element of the stack
    cout << "Top element of the stack is: " << stack.peek() << endl;

    return 0;
}
```

This implementation provides the basic functionality of a stack, including push, pop, and peek operations. It also includes checks for stack overflow and underflow.

### 1. Algorithms & Data Structures (C++): Implementation of Stack using singly linked list

Certainly! Below is a simple implementation of a stack using a singly linked list in C++:

```cpp
#include <iostream>

using namespace std;

// Node class for the linked list
class Node {
public:
    int data;
    Node* next;
    Node(int data) {
        this->data = data;
        this->next = nullptr;
    }
};

// Stack class
class Stack {
private:
    Node* top;

public:
    Stack() {
        top = nullptr;
    }

    // Check if the stack is empty
    bool isEmpty() {
        return top == nullptr;
    }

    // Push operation to insert an element
    void push(int data) {
        Node* newNode = new Node(data);
        newNode->next = top;
        top = newNode;
        cout << data << " pushed to stack\n";
    }

    // Pop operation to remove an element
    int pop() {
        if (isEmpty()) {
            cout << "Stack is empty\n";
            return -1; // Assuming -1 represents an empty stack
        }
        int popped = top->data;
        Node* temp = top;
        top = top->next;
        delete temp;
        return popped;
    }

    // Function to return the top element of the stack
    int peek() {
        if (isEmpty()) {
            cout << "Stack is empty\n";
            return -1; // Assuming -1 represents an empty stack
        }
        return top->data;
    }
};

int main() {
    Stack stack;
    
    stack.push(10);
    stack.push(20);
    stack.push(30);

    cout << "Top element is: " << stack.peek() << endl;
    cout << stack.pop() << " popped from stack\n";
    cout << "Top element is: " << stack.peek() << endl;

    return 0;
}
```

This code defines a `Stack` class with basic operations such as `push()`, `pop()`, `peek()`, and `isEmpty()`, implemented using a singly linked list. The `Node` class represents the individual elements of the stack, with each node containing an integer value and a pointer to the next node.

### 1. Algorithms & Data Structures (C++): Implementing 2 STACKS using single Array

Implementing two stacks using a single array is an interesting exercise in data structure manipulation. The idea is to divide the array into two halves and allow each stack to grow in opposite directions. Here's a simple implementation in C++:

```cpp
#include <iostream>
using namespace std;

#define MAX_SIZE 100

class TwoStacks {
private:
    int arr[MAX_SIZE];
    int top1;
    int top2;

public:
    TwoStacks() {
        top1 = -1; // Initialize top of stack 1
        top2 = MAX_SIZE; // Initialize top of stack 2
    }

    // Push element x to stack 1
    void push1(int x) {
        if (top1 < top2 - 1) {
            arr[++top1] = x;
        } else {
            cout << "Stack Overflow for Stack 1\n";
        }
    }

    // Push element x to stack 2
    void push2(int x) {
        if (top1 < top2 - 1) {
            arr[--top2] = x;
        } else {
            cout << "Stack Overflow for Stack 2\n";
        }
    }

    // Pop element from stack 1
    int pop1() {
        if (top1 >= 0) {
            return arr[top1--];
        } else {
            cout << "Stack Underflow for Stack 1\n";
            return -1;
        }
    }

    // Pop element from stack 2
    int pop2() {
        if (top2 < MAX_SIZE) {
            return arr[top2++];
        } else {
            cout << "Stack Underflow for Stack 2\n";
            return -1;
        }
    }

    // Check if stack 1 is empty
    bool isEmpty1() {
        return top1 == -1;
    }

    // Check if stack 2 is empty
    bool isEmpty2() {
        return top2 == MAX_SIZE;
    }
};

int main() {
    TwoStacks ts;

    // Push some elements to stack 1
    ts.push1(1);
    ts.push1(2);
    ts.push1(3);

    // Push some elements to stack 2
    ts.push2(4);
    ts.push2(5);
    ts.push2(6);

    // Pop elements from stack 1
    cout << "Popping from Stack 1: ";
    while (!ts.isEmpty1()) {
        cout << ts.pop1() << " ";
    }
    cout << endl;

    // Pop elements from stack 2
    cout << "Popping from Stack 2: ";
    while (!ts.isEmpty2()) {
        cout << ts.pop2() << " ";
    }
    cout << endl;

    return 0;
}
```

This implementation uses two indices (`top1` and `top2`) to keep track of the top of each stack within the array. Stack 1 grows from the start of the array towards the end, while Stack 2 grows from the end of the array towards the start. The `push1()` and `pop1()` operations manipulate Stack 1, and `push2()` and `pop2()` operations manipulate Stack 2. This way, both stacks can operate independently using a single array.

### 1. Algorithms & Data Structures (C++): Implementing Linked Stack ADT

Implementing a Linked Stack ADT (Abstract Data Type) in C++ involves creating a class for the stack and another class for the nodes of the linked list. Here's a simple implementation:

```cpp
#include <iostream>

template<typename T>
class Node {
public:
    T data;
    Node<T>* next;

    Node(const T& newData) : data(newData), next(nullptr) {}
};

template<typename T>
class LinkedStack {
private:
    Node<T>* top; // Pointer to the top of the stack

public:
    LinkedStack() : top(nullptr) {}

    ~LinkedStack() {
        while (!isEmpty()) {
            pop();
        }
    }

    // Check if the stack is empty
    bool isEmpty() const {
        return top == nullptr;
    }

    // Push element to the top of the stack
    void push(const T& newData) {
        Node<T>* newNode = new Node<T>(newData);
        newNode->next = top;
        top = newNode;
    }

    // Remove and return the element from the top of the stack
    T pop() {
        if (isEmpty()) {
            std::cerr << "Error: Stack is empty." << std::endl;
            exit(EXIT_FAILURE);
        }
        Node<T>* temp = top;
        T data = temp->data;
        top = top->next;
        delete temp;
        return data;
    }

    // Return the element at the top of the stack
    T peek() const {
        if (isEmpty()) {
            std::cerr << "Error: Stack is empty." << std::endl;
            exit(EXIT_FAILURE);
        }
        return top->data;
    }
};

int main() {
    LinkedStack<int> stack;
    
    stack.push(10);
    stack.push(20);
    stack.push(30);

    std::cout << "Top element: " << stack.peek() << std::endl;

    std::cout << "Popping elements: ";
    while (!stack.isEmpty()) {
        std::cout << stack.pop() << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

This code defines a `Node` class to represent each element in the stack, and a `LinkedStack` class to manage the stack operations. The `push` function inserts an element at the top of the stack, `pop` removes and returns the top element, `peek` returns the top element without removing it, and `isEmpty` checks if the stack is empty.

In the `main` function, some elements are pushed onto the stack, then popped and printed one by one.

### 1. Algorithms & Data Structures (C++): Implementing Stack using Array : Pop, Peak, Display

Sure, here's a basic implementation of a stack using an array in C++:

```cpp
#include <iostream>
using namespace std;

#define MAX_SIZE 100 // Maximum size of the stack

class Stack {
private:
    int top;          // Index of the top element
    int arr[MAX_SIZE];// Array to store stack elements

public:
    Stack() {
        top = -1; // Initialize top as -1 to indicate empty stack
    }

    // Function to push an element onto the stack
    void push(int val) {
        if (top == MAX_SIZE - 1) {
            cout << "Stack Overflow! Cannot push element.\n";
            return;
        }
        arr[++top] = val;
    }

    // Function to pop the top element from the stack
    void pop() {
        if (top == -1) {
            cout << "Stack Underflow! Cannot pop element.\n";
            return;
        }
        top--;
    }

    // Function to return the top element of the stack
    int peek() {
        if (top == -1) {
            cout << "Stack is empty.\n";
            return -1; // Return -1 if stack is empty
        }
        return arr[top];
    }

    // Function to display the elements of the stack
    void display() {
        if (top == -1) {
            cout << "Stack is empty.\n";
            return;
        }
        cout << "Stack elements are: ";
        for (int i = top; i >= 0; i--) {
            cout << arr[i] << " ";
        }
        cout << endl;
    }
};

int main() {
    Stack myStack;

    // Pushing elements onto the stack
    myStack.push(10);
    myStack.push(20);
    myStack.push(30);

    // Displaying stack elements
    myStack.display();

    // Popping an element
    myStack.pop();

    // Displaying stack elements after popping
    myStack.display();

    // Peeking at the top element
    cout << "Top element is: " << myStack.peek() << endl;

    return 0;
}
```

This code demonstrates how to implement a stack using an array in C++. It includes functions for pushing, popping, peeking, and displaying elements in the stack. You can adjust the `MAX_SIZE` macro to change the maximum capacity of the stack.

### 1. Algorithms & Data Structures (C++): Implementing Stack using Array : Push

Sure, implementing a stack using an array in C++ is a common exercise. Here's a basic implementation of the `push` operation:

```cpp
#include <iostream>
using namespace std;

#define MAX_SIZE 100 // Maximum size of the stack

class Stack {
private:
    int arr[MAX_SIZE];
    int top;

public:
    Stack() {
        top = -1; // Initialize top of the stack
    }

    bool push(int x) {
        if (top >= MAX_SIZE - 1) {
            cout << "Stack Overflow\n";
            return false;
        }
        arr[++top] = x; // Increment top and insert element
        cout << x << " pushed into stack\n";
        return true;
    }
};

int main() {
    Stack myStack;
    myStack.push(1);
    myStack.push(2);
    myStack.push(3);
    return 0;
}
```

In this implementation:

- `MAX_SIZE` defines the maximum capacity of the stack.
- `arr` is the array used to implement the stack.
- `top` keeps track of the index of the top element in the stack.

The `push` function first checks if the stack is full (`top` is equal to `MAX_SIZE - 1`). If the stack is not full, it increments `top` and inserts the element at that index in the array.

In the `main` function, we create a `Stack` object and push some elements onto the stack.

You can compile and run this code to see the output. It should print:

```bash
1 pushed into stack
2 pushed into stack
3 pushed into stack
```

### 1. Algorithms & Data Structures (C++): Implementing Stack using Linked List

Implementing a stack using a linked list in C++ involves creating a class for the linked list nodes and another class for the stack itself. Here's a basic implementation:

```cpp
#include <iostream>

// Define a Node class for the linked list
class Node {
public:
    int data;
    Node* next;

    Node(int data) {
        this->data = data;
        this->next = nullptr;
    }
};

// Define a Stack class using linked list
class Stack {
private:
    Node* top;

public:
    Stack() {
        top = nullptr;
    }

    // Push operation to insert an element onto the stack
    void push(int data) {
        Node* newNode = new Node(data);
        if (top == nullptr) {
            top = newNode;
        } else {
            newNode->next = top;
            top = newNode;
        }
    }

    // Pop operation to remove and return the top element from the stack
    int pop() {
        if (isEmpty()) {
            std::cerr << "Stack underflow\n";
            return INT_MIN; // or throw an exception
        }
        int data = top->data;
        Node* temp = top;
        top = top->next;
        delete temp;
        return data;
    }

    // Peek operation to return the top element without removing it
    int peek() {
        if (isEmpty()) {
            std::cerr << "Stack is empty\n";
            return INT_MIN; // or throw an exception
        }
        return top->data;
    }

    // Utility function to check if the stack is empty
    bool isEmpty() {
        return top == nullptr;
    }

    // Utility function to print the stack
    void printStack() {
        if (isEmpty()) {
            std::cout << "Stack is empty\n";
            return;
        }
        Node* temp = top;
        while (temp != nullptr) {
            std::cout << temp->data << " ";
            temp = temp->next;
        }
        std::cout << std::endl;
    }
};

int main() {
    Stack stack;
    stack.push(10);
    stack.push(20);
    stack.push(30);
    
    std::cout << "Stack elements: ";
    stack.printStack();

    std::cout << "Top element: " << stack.peek() << std::endl;

    std::cout << "Popping: " << stack.pop() << std::endl;
    std::cout << "Popping: " << stack.pop() << std::endl;

    std::cout << "Stack elements after popping: ";
    stack.printStack();

    return 0;
}
```

In this code:

- The `Node` class represents individual nodes of the linked list. Each node has a data field and a pointer to the next node.
- The `Stack` class maintains a pointer to the top of the stack. It provides methods for push, pop, peek, and isEmpty operations.
- The `push` operation inserts a new element onto the stack by creating a new node and updating the top pointer.
- The `pop` operation removes and returns the top element from the stack. It also deallocates memory for the removed node.
- The `peek` operation returns the top element without removing it.
- The `isEmpty` method checks if the stack is empty.
- The `printStack` method prints the elements of the stack.

The `main` function demonstrates the usage of the stack by pushing elements onto the stack, printing the stack, peeking the top element, and popping elements from the stack.

### 1. Algorithms & Data Structures (C++): Inbuilt Stack

In C++, you can use the `std::stack` container from the Standard Template Library (STL) for implementing a stack data structure. Here's a basic overview of how to use it:

```cpp
#include <iostream>
#include <stack>

int main() {
    // Creating a stack of integers
    std::stack<int> myStack;

    // Pushing elements onto the stack
    myStack.push(10);
    myStack.push(20);
    myStack.push(30);

    // Accessing the top element of the stack
    std::cout << "Top element of the stack: " << myStack.top() << std::endl;

    // Popping elements from the stack
    myStack.pop();
    
    std::cout << "After popping, top element of the stack: " << myStack.top() << std::endl;

    // Checking if the stack is empty
    if (myStack.empty()) {
        std::cout << "Stack is empty!" << std::endl;
    } else {
        std::cout << "Stack is not empty!" << std::endl;
    }

    // Getting the size of the stack
    std::cout << "Size of the stack: " << myStack.size() << std::endl;

    return 0;
}
```

This code demonstrates basic operations such as pushing elements onto the stack, accessing the top element, popping elements, checking if the stack is empty, and getting the size of the stack. The `std::stack` provides a convenient interface for implementing a stack without having to manage memory allocation and deallocation explicitly.

### 1. Algorithms & Data Structures (C++): Invert the elements of a Stack

Certainly! To invert the elements of a stack in C++, you can use another stack to temporarily store the elements while popping them off the original stack and pushing them onto the temporary stack in reverse order. Here's a simple implementation:

```cpp
#include <iostream>
#include <stack>

using namespace std;

// Function to invert the elements of a stack
void invertStack(stack<int> &s) {
    stack<int> tempStack;

    // Transfer elements from original stack to temporary stack
    while (!s.empty()) {
        int temp = s.top();
        s.pop();
        tempStack.push(temp);
    }

    // Transfer elements back to original stack
    while (!tempStack.empty()) {
        int temp = tempStack.top();
        tempStack.pop();
        s.push(temp);
    }
}

// Function to print the stack
void printStack(stack<int> s) {
    while (!s.empty()) {
        cout << s.top() << " ";
        s.pop();
    }
    cout << endl;
}

int main() {
    stack<int> myStack;

    // Push some elements onto the stack
    myStack.push(1);
    myStack.push(2);
    myStack.push(3);
    myStack.push(4);
    myStack.push(5);

    cout << "Original Stack: ";
    printStack(myStack);

    // Invert the stack
    invertStack(myStack);

    cout << "Inverted Stack: ";
    printStack(myStack);

    return 0;
}
```

This code defines a function `invertStack` which takes a stack by reference and inverts its elements. Then, in the `main` function, it demonstrates how to use this function by creating a stack, pushing some elements onto it, inverting it, and then printing both the original and inverted stacks.

### 1. Algorithms & Data Structures (C++): Manipulating Stacks

Manipulating stacks in C++ is a fundamental aspect of working with data structures. Stacks follow the Last In, First Out (LIFO) principle, meaning the last element added to the stack is the first one to be removed. Here's a basic implementation of a stack in C++ along with some common operations:

```cpp
#include <iostream>
#include <stack>

using namespace std;

int main() {
    stack<int> s;

    // Pushing elements onto the stack
    s.push(5);
    s.push(10);
    s.push(15);

    // Displaying the top element
    cout << "Top element: " << s.top() << endl;

    // Popping elements from the stack
    s.pop();

    // Displaying the top element after popping
    cout << "Top element after popping: " << s.top() << endl;

    // Checking if the stack is empty
    if (s.empty())
        cout << "Stack is empty\n";
    else
        cout << "Stack is not empty\n";

    // Getting the size of the stack
    cout << "Size of the stack: " << s.size() << endl;

    return 0;
}
```

In this code:

- We include the necessary headers for `iostream` and `stack`.
- We create a stack of integers using `stack<int> s;`.
- Elements are pushed onto the stack using `s.push(element)`.
- The top element of the stack is accessed using `s.top()`.
- Elements are removed from the top of the stack using `s.pop()`.
- We can check if the stack is empty using `s.empty()`.
- The size of the stack can be obtained using `s.size()`.

This is a basic example, and there are more advanced operations and implementations you can explore depending on your requirements.

### 1. Algorithms & Data Structures (C++): Minimum Element In A Stack In Constant Time

To find the minimum element in a stack in constant time, you can use an auxiliary stack to keep track of the minimum elements encountered so far. Here's how you can implement it in C++:

```cpp
#include <stack>
#include <iostream>

using namespace std;

class MinStack {
    stack<int> dataStack;
    stack<int> minStack;
public:
    void push(int val) {
        dataStack.push(val);
        if (minStack.empty() || val <= minStack.top()) {
            minStack.push(val);
        }
    }
    
    void pop() {
        if (dataStack.empty()) {
            cout << "Stack is empty." << endl;
            return;
        }
        if (dataStack.top() == minStack.top()) {
            minStack.pop();
        }
        dataStack.pop();
    }
    
    int top() {
        if (dataStack.empty()) {
            cout << "Stack is empty." << endl;
            return -1;
        }
        return dataStack.top();
    }
    
    int getMin() {
        if (minStack.empty()) {
            cout << "Stack is empty." << endl;
            return -1;
        }
        return minStack.top();
    }
};

int main() {
    MinStack minStack;
    minStack.push(3);
    minStack.push(5);
    minStack.push(2);
    minStack.push(1);
    
    cout << "Minimum element: " << minStack.getMin() << endl; // Output: 1
    
    minStack.pop();
    cout << "Minimum element: " << minStack.getMin() << endl; // Output: 2
    
    minStack.pop();
    cout << "Minimum element: " << minStack.getMin() << endl; // Output: 2
    
    return 0;
}
```

In this implementation, we use two stacks: `dataStack` to store the actual elements and `minStack` to keep track of the minimum elements. When pushing a new element onto the stack, we compare it with the top element of `minStack`. If it's smaller or equal, we push it onto `minStack`. When popping an element, we check if the top element of `dataStack` is equal to the top element of `minStack`. If so, we pop from `minStack` as well.

This way, the `getMin()` function can retrieve the minimum element in constant time by just peeking at the top of `minStack`.

### 1. Algorithms & Data Structures (C++): Operations on Stack

In C++, you can implement a stack data structure using the standard library's `std::stack` or by implementing your own stack using arrays or linked lists. Here's an example of how you can perform basic operations on a stack:

```cpp
#include <iostream>
#include <stack>

using namespace std;

int main() {
    // Creating a stack
    stack<int> myStack;

    // Pushing elements onto the stack
    myStack.push(10);
    myStack.push(20);
    myStack.push(30);

    // Getting the top element of the stack
    cout << "Top element of the stack: " << myStack.top() << endl;

    // Popping elements from the stack
    myStack.pop();
    cout << "Popped one element from the stack." << endl;

    // Checking if the stack is empty
    if (myStack.empty()) {
        cout << "Stack is empty." << endl;
    } else {
        cout << "Stack is not empty." << endl;
    }

    // Getting the size of the stack
    cout << "Size of the stack: " << myStack.size() << endl;

    return 0;
}
```

This code demonstrates the basic operations on a stack:

1. **Push**: Adds an element onto the top of the stack.
2. **Pop**: Removes the top element from the stack.
3. **Top**: Retrieves the top element of the stack without removing it.
4. **Empty**: Checks if the stack is empty.
5. **Size**: Returns the number of elements in the stack.

You can run this code to see how these operations work with the stack in C++.

### 1. Algorithms & Data Structures (C++): Program for Infix to Postfix Conversion

Sure, here's a simple C++ program to convert infix expressions to postfix using the stack data structure:

```cpp
#include <iostream>
#include <stack>
#include <string>
#include <unordered_map>

using namespace std;

// Function to check if a character is an operator
bool isOperator(char c) {
    return c == '+' || c == '-' || c == '*' || c == '/';
}

// Function to get the precedence of an operator
int precedence(char op) {
    if (op == '+' || op == '-') return 1;
    if (op == '*' || op == '/') return 2;
    return 0;
}

// Function to convert infix expression to postfix
string infixToPostfix(string infix) {
    string postfix;
    stack<char> s;
    unordered_map<char, int> precedenceMap;

    precedenceMap['+'] = 1;
    precedenceMap['-'] = 1;
    precedenceMap['*'] = 2;
    precedenceMap['/'] = 2;

    for (char c : infix) {
        if (isalnum(c)) {
            postfix += c;
        } else if (c == '(') {
            s.push(c);
        } else if (c == ')') {
            while (!s.empty() && s.top() != '(') {
                postfix += s.top();
                s.pop();
            }
            if (!s.empty()) {
                s.pop(); // Discard the '('
            }
        } else if (isOperator(c)) {
            while (!s.empty() && precedenceMap[s.top()] >= precedenceMap[c]) {
                postfix += s.top();
                s.pop();
            }
            s.push(c);
        }
    }

    while (!s.empty()) {
        postfix += s.top();
        s.pop();
    }

    return postfix;
}

int main() {
    string infix_expression;
    cout << "Enter infix expression: ";
    getline(cin, infix_expression);

    string postfix_expression = infixToPostfix(infix_expression);
    cout << "Postfix expression: " << postfix_expression << endl;

    return 0;
}
```

This program takes an infix expression as input and converts it to a postfix expression using the stack data structure. It uses a map to store the precedence of operators and follows the shunting-yard algorithm to perform the conversion.

### 1. Algorithms & Data Structures (C++): Recursively Reverse a Stack

To recursively reverse a stack in C++, you can use a recursive function that pops elements from the original stack and inserts them at the bottom using recursion. Here's a sample implementation:

```cpp
#include <iostream>
#include <stack>

using namespace std;

// Function to insert an element at the bottom of a stack
void insertAtBottom(stack<int> &st, int x) {
    // Base case: If the stack is empty, push the element
    if (st.empty()) {
        st.push(x);
        return;
    }
    // Recursive call to insert at the bottom after popping all elements
    int temp = st.top();
    st.pop();
    insertAtBottom(st, x);
    // Push the popped elements back onto the stack
    st.push(temp);
}

// Function to reverse a stack recursively
void reverseStack(stack<int> &st) {
    // Base case: If the stack is not empty, pop the top element
    if (!st.empty()) {
        int x = st.top();
        st.pop();
        // Recursively reverse the remaining stack
        reverseStack(st);
        // Insert the popped element at the bottom
        insertAtBottom(st, x);
    }
}

int main() {
    stack<int> st;
    // Push some elements onto the stack
    st.push(1);
    st.push(2);
    st.push(3);
    st.push(4);

    cout << "Original Stack: ";
    while (!st.empty()) {
        cout << st.top() << " ";
        st.pop();
    }
    cout << endl;

    // Reverse the stack
    reverseStack(st);

    cout << "Reversed Stack: ";
    while (!st.empty()) {
        cout << st.top() << " ";
        st.pop();
    }
    cout << endl;

    return 0;
}
```

This code defines two functions: `insertAtBottom` and `reverseStack`. The `insertAtBottom` function is a helper function that inserts an element at the bottom of a stack using recursion. The `reverseStack` function recursively reverses the stack by repeatedly popping elements and inserting them at the bottom until the original stack is empty. Finally, the `main` function demonstrates the usage of these functions by reversing a sample stack.

### 1. Algorithms & Data Structures (C++): Representation of Stacks

In C++, you can represent a stack using various data structures. One of the most common ways is to use a dynamic array (vector) or a linked list. Here's a basic implementation of a stack using a dynamic array (vector):

```cpp
#include <iostream>
#include <vector>

template<typename T>
class Stack {
private:
    std::vector<T> elements;

public:
    // Push element onto the stack
    void push(const T& value) {
        elements.push_back(value);
    }

    // Remove and return the top element from the stack
    T pop() {
        if (empty()) {
            throw std::out_of_range("Stack is empty");
        }
        T top_element = elements.back();
        elements.pop_back();
        return top_element;
    }

    // Return the top element from the stack without removing it
    T top() const {
        if (empty()) {
            throw std::out_of_range("Stack is empty");
        }
        return elements.back();
    }

    // Check if the stack is empty
    bool empty() const {
        return elements.empty();
    }

    // Return the size of the stack
    size_t size() const {
        return elements.size();
    }
};

int main() {
    Stack<int> stack;

    // Push elements onto the stack
    stack.push(10);
    stack.push(20);
    stack.push(30);

    // Print the size of the stack
    std::cout << "Stack size: " << stack.size() << std::endl;

    // Print and remove elements from the stack until it's empty
    while (!stack.empty()) {
        std::cout << "Top element: " << stack.top() << std::endl;
        stack.pop();
    }

    return 0;
}
```

This implementation uses a vector to store elements, providing dynamic resizing capabilities. Each operation (push, pop, top, empty, size) has a time complexity of O(1), making it efficient.

You can also implement a stack using a linked list, which allows for efficient insertion and deletion at the beginning (top) of the list. Here's a basic implementation using a singly linked list:

```cpp
#include <iostream>

template<typename T>
struct Node {
    T data;
    Node* next;

    Node(const T& value) : data(value), next(nullptr) {}
};

template<typename T>
class Stack {
private:
    Node<T>* top_node;

public:
    Stack() : top_node(nullptr) {}

    // Push element onto the stack
    void push(const T& value) {
        Node<T>* new_node = new Node<T>(value);
        new_node->next = top_node;
        top_node = new_node;
    }

    // Remove and return the top element from the stack
    T pop() {
        if (empty()) {
            throw std::out_of_range("Stack is empty");
        }
        T top_value = top_node->data;
        Node<T>* temp = top_node;
        top_node = top_node->next;
        delete temp;
        return top_value;
    }

    // Return the top element from the stack without removing it
    T top() const {
        if (empty()) {
            throw std::out_of_range("Stack is empty");
        }
        return top_node->data;
    }

    // Check if the stack is empty
    bool empty() const {
        return top_node == nullptr;
    }
};

int main() {
    Stack<int> stack;

    // Push elements onto the stack
    stack.push(10);
    stack.push(20);
    stack.push(30);

    // Print the size of the stack
    std::cout << "Stack size: " << stack.size() << std::endl;

    // Print and remove elements from the stack until it's empty
    while (!stack.empty()) {
        std::cout << "Top element: " << stack.top() << std::endl;
        stack.pop();
    }

    return 0;
}
```

This implementation of a stack using a linked list also provides O(1) time complexity for each operation.

### 1. Algorithms & Data Structures (C++): Representations of Stack

In C++, a stack can be represented using various data structures. The most common representations include using arrays or linked lists. Here's how you can implement a stack using each of these representations:

### 1. Stack using Array

```cpp
#include <iostream>
#define MAX_SIZE 1000

using namespace std;

class Stack {
private:
    int arr[MAX_SIZE];
    int top;
public:
    Stack() { top = -1; }
    
    bool isEmpty() {
        return top == -1;
    }

    bool isFull() {
        return top == MAX_SIZE - 1;
    }

    void push(int val) {
        if (isFull()) {
            cout << "Stack Overflow" << endl;
            return;
        }
        arr[++top] = val;
    }

    int pop() {
        if (isEmpty()) {
            cout << "Stack Underflow" << endl;
            return -1; // or throw an exception
        }
        return arr[top--];
    }

    int peek() {
        if (isEmpty()) {
            cout << "Stack is Empty" << endl;
            return -1; // or throw an exception
        }
        return arr[top];
    }
};

int main() {
    Stack s;
    s.push(10);
    s.push(20);
    s.push(30);

    cout << s.pop() << " popped from stack" << endl;

    cout << "Top element is " << s.peek() << endl;

    return 0;
}
```

### 2. Stack using Linked List

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

class Stack {
private:
    Node* top;
public:
    Stack() { top = nullptr; }

    bool isEmpty() {
        return top == nullptr;
    }

    void push(int val) {
        Node* newNode = new Node(val);
        newNode->next = top;
        top = newNode;
    }

    int pop() {
        if (isEmpty()) {
            cout << "Stack Underflow" << endl;
            return -1; // or throw an exception
        }
        Node* temp = top;
        int popped = temp->data;
        top = top->next;
        delete temp;
        return popped;
    }

    int peek() {
        if (isEmpty()) {
            cout << "Stack is Empty" << endl;
            return -1; // or throw an exception
        }
        return top->data;
    }
};

int main() {
    Stack s;
    s.push(10);
    s.push(20);
    s.push(30);

    cout << s.pop() << " popped from stack" << endl;

    cout << "Top element is " << s.peek() << endl;

    return 0;
}
```

Both implementations offer similar functionality, but the choice between them depends on factors like memory efficiency, ease of implementation, and specific requirements of your application.

### 1. Algorithms & Data Structures (C++): Reverse a number using stack

Sure, you can reverse a number using a stack in C++. Here's a simple implementation:

```cpp
#include <iostream>
#include <stack>

using namespace std;

int reverseNumber(int number) {
    stack<int> digits;

    // Push each digit of the number onto the stack
    while (number != 0) {
        digits.push(number % 10);
        number /= 10;
    }

    int reversed = 0;
    int multiplier = 1;

    // Pop each digit from the stack and build the reversed number
    while (!digits.empty()) {
        reversed += digits.top() * multiplier;
        digits.pop();
        multiplier *= 10;
    }

    return reversed;
}

int main() {
    int number;
    cout << "Enter a number: ";
    cin >> number;

    int reversed = reverseNumber(number);
    cout << "Reversed number: " << reversed << endl;

    return 0;
}
```

This program first pushes each digit of the input number onto a stack. Then it pops each digit from the stack and constructs the reversed number. Finally, it prints the reversed number.

### 1. Algorithms & Data Structures (C++): Runtime characteristics of Stacks and Queues

Stacks and queues are fundamental data structures in computer science, each with its own set of runtime characteristics. Here's a breakdown of their runtime characteristics in terms of operations:

### Stacks

1. **Push Operation:**
   - Time Complexity: O(1)
   - Stacks typically have constant-time insertion at one end (usually called "push"). This is because the element is added to the top of the stack, and no traversal or searching is required.

2. **Pop Operation:**
   - Time Complexity: O(1)
   - Similarly, popping from a stack also has a constant-time complexity. The top element is simply removed from the stack.

3. **Peek Operation:**
   - Time Complexity: O(1)
   - Peeking at the top element of the stack is also a constant-time operation. It doesn't involve any traversal; it simply returns the top element.

4. **Space Complexity:**
   - The space complexity for a stack depends on the number of elements in the stack. It's O(n), where n is the number of elements currently in the stack.

### Queues

1. **Enqueue Operation:**
   - Time Complexity: O(1)
   - Adding an element to the rear of the queue typically takes constant time. No traversal is required; the element is simply appended to the end of the queue.

2. **Dequeue Operation:**
   - Time Complexity: O(1)
   - Removing an element from the front of the queue also typically takes constant time. Similar to the enqueue operation, no traversal is required; the first element is simply removed.

3. **Peek Operation:**
   - Time Complexity: O(1)
   - Similar to stacks, peeking at the front element of the queue is also a constant-time operation. It doesn't involve any traversal; it simply returns the front element.

4. **Space Complexity:**
   - The space complexity for a queue is also O(n), where n is the number of elements currently in the queue.

### Summary

- Both stacks and queues offer constant-time insertion and removal of elements, making them efficient for adding and removing items.
- Stacks follow the Last In, First Out (LIFO) principle, while queues follow the First In, First Out (FIFO) principle.
- Stacks and queues are often used in scenarios where the order of insertion and removal of elements is important, such as in algorithmic problems, parsing expressions, managing function calls, etc.

### 1. Algorithms & Data Structures (C++): Stack

A stack is a fundamental data structure in computer science that follows the Last In, First Out (LIFO) principle. This means that the last element added to the stack is the first one to be removed.

In C++, you can implement a stack using various methods. One common approach is to use the standard template library (STL) container `std::stack`, which provides a convenient interface for working with stacks.

Here's a simple example of how you can use `std::stack` in C++:

```cpp
#include <iostream>
#include <stack>

int main() {
    std::stack<int> myStack;

    // Push elements onto the stack
    myStack.push(10);
    myStack.push(20);
    myStack.push(30);

    // Print the top element of the stack
    std::cout << "Top element of the stack: " << myStack.top() << std::endl;

    // Pop elements from the stack
    myStack.pop();

    // Print the top element of the stack after popping
    std::cout << "Top element of the stack after popping: " << myStack.top() << std::endl;

    // Check if the stack is empty
    if (myStack.empty()) {
        std::cout << "Stack is empty\n";
    } else {
        std::cout << "Stack is not empty\n";
    }

    // Get the size of the stack
    std::cout << "Size of the stack: " << myStack.size() << std::endl;

    return 0;
}
```

Output:

```bash
Top element of the stack: 30
Top element of the stack after popping: 20
Stack is not empty
Size of the stack: 2
```

This code demonstrates basic operations with a stack: pushing elements onto the stack, accessing the top element, popping elements, checking if the stack is empty, and getting the size of the stack.

### 1. Algorithms & Data Structures (C++): Stack - Pop

In C++, the `pop()` operation in the context of a stack removes the top element from the stack. Here's a basic implementation of the `pop()` function for a stack data structure:

```cpp
#include <iostream>
#include <stack>

int main() {
    std::stack<int> myStack;

    // Push some elements onto the stack
    myStack.push(10);
    myStack.push(20);
    myStack.push(30);

    // Display the top element before popping
    std::cout << "Top element before pop: " << myStack.top() << std::endl;

    // Pop the top element
    myStack.pop();

    // Display the top element after popping
    std::cout << "Top element after pop: " << myStack.top() << std::endl;

    return 0;
}
```

In this example:

- We include the necessary header files (`iostream` for input/output and `stack` for the stack container).
- We create a stack named `myStack` to hold integer values.
- We push three elements onto the stack: 10, 20, and 30.
- We display the top element of the stack using `top()` before popping.
- We call the `pop()` function to remove the top element from the stack.
- Finally, we display the new top element of the stack.

Remember, it's important to check if the stack is empty before calling `pop()` to avoid undefined behavior.

### 1. Algorithms & Data Structures (C++): Stack - Push

In C++, the `push()` operation is used to insert an element onto the top of a stack data structure. Here's a simple implementation of the `push()` operation for a stack using C++:

```cpp
#include <iostream>
#include <stack>

int main() {
    std::stack<int> myStack;

    // Pushing elements onto the stack
    myStack.push(10);
    myStack.push(20);
    myStack.push(30);

    // Displaying the stack after pushing
    std::cout << "Stack elements after pushing: ";
    while (!myStack.empty()) {
        std::cout << myStack.top() << " ";
        myStack.pop();
    }
    std::cout << std::endl;

    return 0;
}
```

Output:

```bash
Stack elements after pushing: 30 20 10
```

In this example, the `push()` function is used to insert elements onto the stack. The elements are added onto the top of the stack. `top()` function is used to access the top element of the stack, and `pop()` function is used to remove the top element from the stack.

### 1. Algorithms & Data Structures (C++): Stack ADT

A stack is a fundamental data structure that follows the Last In, First Out (LIFO) principle. It's like a stack of plates: the last plate added is the first one to be removed. In C++, you can implement a stack using various methods, but one common approach is using a linked list.

Here's a basic implementation of a stack using a singly linked list in C++:

```cpp
#include <iostream>

template <typename T>
class Node {
public:
    T data;
    Node* next;

    Node(T data) : data(data), next(nullptr) {}
};

template <typename T>
class Stack {
private:
    Node<T>* top;

public:
    Stack() : top(nullptr) {}

    ~Stack() {
        while (!isEmpty()) {
            pop();
        }
    }

    void push(T data) {
        Node<T>* newNode = new Node<T>(data);
        newNode->next = top;
        top = newNode;
    }

    T pop() {
        if (isEmpty()) {
            throw std::out_of_range("Stack is empty");
        }
        Node<T>* temp = top;
        T data = temp->data;
        top = top->next;
        delete temp;
        return data;
    }

    T peek() {
        if (isEmpty()) {
            throw std::out_of_range("Stack is empty");
        }
        return top->data;
    }

    bool isEmpty() {
        return top == nullptr;
    }
};

int main() {
    Stack<int> stack;

    stack.push(1);
    stack.push(2);
    stack.push(3);

    std::cout << "Top element: " << stack.peek() << std::endl;

    std::cout << "Popping elements: ";
    while (!stack.isEmpty()) {
        std::cout << stack.pop() << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

This code defines a generic `Node` class to represent each element in the stack and a `Stack` class that maintains a pointer to the top element of the stack. The `push()` function adds an element to the top of the stack, `pop()` removes and returns the top element, `peek()` returns the top element without removing it, and `isEmpty()` checks if the stack is empty.

### 1. Algorithms & Data Structures (C++): Stack Algorithms

Stacks are fundamental data structures that follow the Last In, First Out (LIFO) principle, where elements are added and removed from the top of the stack. Here are some common algorithms implemented using stacks in C++:

1. **Balanced Parentheses:** This algorithm checks if a given string of parentheses is balanced or not. It uses a stack to keep track of opening parentheses and matches them with closing parentheses. If the stack becomes empty at the end of traversal and all parentheses are matched, the string is considered balanced.

```cpp
#include <iostream>
#include <stack>
#include <string>

bool isBalanced(const std::string& str) {
    std::stack<char> stack;
    for (char bracket : str) {
        if (bracket == '(' || bracket == '[' || bracket == '{') {
            stack.push(bracket);
        } else if (!stack.empty() &&
                   ((bracket == ')' && stack.top() == '(') ||
                    (bracket == ']' && stack.top() == '[') ||
                    (bracket == '}' && stack.top() == '{'))) {
            stack.pop();
        } else {
            return false; // Unmatched closing bracket or no opening bracket found
        }
    }
    return stack.empty(); // If stack is empty, all brackets were matched
}

int main() {
    std::string expression = "{[()]}";
    if (isBalanced(expression)) {
        std::cout << "Balanced\n";
    } else {
        std::cout << "Not Balanced\n";
    }
    return 0;
}
```

1. **Reverse a String:** This algorithm reverses a given string using a stack.

```cpp
#include <iostream>
#include <stack>
#include <string>

std::string reverseString(const std::string& str) {
    std::stack<char> stack;
    for (char ch : str) {
        stack.push(ch);
    }
    std::string reversedStr;
    while (!stack.empty()) {
        reversedStr += stack.top();
        stack.pop();
    }
    return reversedStr;
}

int main() {
    std::string str = "hello";
    std::cout << "Original string: " << str << std::endl;
    std::cout << "Reversed string: " << reverseString(str) << std::endl;
    return 0;
}
```

1. **Evaluation of Postfix Expression:** This algorithm evaluates a postfix expression using a stack. Postfix notation doesn't require parentheses to specify order of operations because it's unambiguous.

```cpp
#include <iostream>
#include <stack>
#include <string>
#include <sstream>

bool isOperand(char c) {
    return isdigit(c);
}

int performOperation(char operation, int operand1, int operand2) {
    switch (operation) {
        case '+': return operand1 + operand2;
        case '-': return operand1 - operand2;
        case '*': return operand1 * operand2;
        case '/': return operand1 / operand2;
        default: return 0; // Invalid operation
    }
}

int evaluatePostfix(const std::string& exp) {
    std::stack<int> stack;
    std::stringstream ss(exp);
    std::string token;
    while (ss >> token) {
        if (isOperand(token[0])) {
            stack.push(std::stoi(token));
        } else {
            int operand2 = stack.top();
            stack.pop();
            int operand1 = stack.top();
            stack.pop();
            stack.push(performOperation(token[0], operand1, operand2));
        }
    }
    return stack.top();
}

int main() {
    std::string postfixExp = "6 2 3 + - 3 8 2 / + *";
    std::cout << "Postfix expression: " << postfixExp << std::endl;
    std::cout << "Result: " << evaluatePostfix(postfixExp) << std::endl;
    return 0;
}
```

These are just a few examples of algorithms that can be implemented using stacks in C++. Stacks are versatile data structures and find applications in various areas of computer science and programming.

### 1. Algorithms & Data Structures (C++): Stack and Queue

Sure, let's dive into Stack and Queue data structures in C++.

### Stack

A stack is a Last In, First Out (LIFO) data structure. The last element added to the stack is the first one to be removed. Think of it like a stack of plates, where you can only remove the top plate.

#### Operations

1. **Push**: Adds an element to the top of the stack.
2. **Pop**: Removes the top element from the stack.
3. **Top/Peek**: Returns the top element without removing it.
4. **isEmpty**: Checks if the stack is empty.

```cpp
#include <iostream>
#include <stack>

using namespace std;

int main() {
    stack<int> s;

    s.push(5);
    s.push(10);
    s.push(15);

    cout << "Top element: " << s.top() << endl; // Output: 15

    s.pop();

    cout << "Top element after pop: " << s.top() << endl; // Output: 10

    cout << "Stack size: " << s.size() << endl; // Output: 2

    cout << "Is stack empty? " << (s.empty() ? "Yes" : "No") << endl; // Output: No

    return 0;
}
```

### Queue

A queue is a First In, First Out (FIFO) data structure. The element added first is the one that gets removed first, like people waiting in a line.

#### Operations

1. **Enqueue**: Adds an element to the rear of the queue.
2. **Dequeue**: Removes the front element from the queue.
3. **Front**: Returns the front element without removing it.
4. **isEmpty**: Checks if the queue is empty.

```cpp
#include <iostream>
#include <queue>

using namespace std;

int main() {
    queue<int> q;

    q.push(5);
    q.push(10);
    q.push(15);

    cout << "Front element: " << q.front() << endl; // Output: 5

    q.pop();

    cout << "Front element after dequeue: " << q.front() << endl; // Output: 10

    cout << "Queue size: " << q.size() << endl; // Output: 2

    cout << "Is queue empty? " << (q.empty() ? "Yes" : "No") << endl; // Output: No

    return 0;
}
```

These are basic implementations of Stack and Queue using the Standard Template Library (STL) in C++. You can also implement these data structures from scratch using arrays or linked lists if needed.

### 1. Algorithms & Data Structures (C++): Stack and Queue killer feature

One of the killer features of stacks and queues in C++ is their simplicity and versatility in solving a wide range of problems efficiently. Here's a breakdown of their key features and why they are so powerful:

1. **Stacks:**

   - **LIFO (Last In, First Out) Structure:** This property makes stacks ideal for tasks where you need to reverse or backtrack through a sequence of elements.

   - **Function Call Stack:** Stacks are extensively used in programming language implementations to manage function calls. This enables functions to execute recursively and return control back to the caller efficiently.

   - **Expression Evaluation:** Stacks are fundamental in evaluating arithmetic expressions, converting infix expressions to postfix (or prefix) notation, and then calculating the result.

   - **Undo Functionality:** Stacks are often used to implement the "undo" feature in text editors and other applications where you need to revert the most recent operation.

   - **Backtracking Algorithms:** Many backtracking algorithms, such as depth-first search (DFS) in graph traversal or solving problems like the Tower of Hanoi, rely on stacks to store the sequence of choices made.

2. **Queues:**

   - **FIFO (First In, First Out) Structure:** Queues are essential for scenarios where you need to process elements in the order they were added, such as task scheduling, printing queue management, or event handling systems.

   - **Breadth-First Search (BFS):** In graph traversal, BFS relies on queues to traverse through adjacent nodes level by level, making it a key algorithm for finding shortest paths and exploring graphs systematically.

   - **Producer-Consumer Problem:** Queues are extensively used in concurrent programming to synchronize communication between multiple threads or processes. They facilitate communication between producers (those generating data) and consumers (those processing data) efficiently.

   - **Buffering and Scheduling:** Queues are used in buffering systems to manage data flow between different components of a system, ensuring smooth and controlled data transfer.

   - **Task Management:** In operating systems, queues are used for managing processes and scheduling tasks based on priority or other criteria.

Both stacks and queues can be implemented efficiently using various data structures like arrays or linked lists, and they serve as building blocks for more complex data structures and algorithms. Their simplicity and versatility make them indispensable tools in algorithm design and software development.

### 1. Algorithms & Data Structures (C++): Stack and Queue operations

Sure, I can provide you with basic implementations of stacks and queues in C++. Let's start with the stack.

```cpp
#include <iostream>
#include <stack>

using namespace std;

int main() {
    // Creating a stack
    stack<int> myStack;

    // Pushing elements onto the stack
    myStack.push(5);
    myStack.push(10);
    myStack.push(15);

    // Accessing the top element of the stack
    cout << "Top element of the stack: " << myStack.top() << endl;

    // Popping elements from the stack
    myStack.pop();
    cout << "Top element after popping: " << myStack.top() << endl;

    // Checking if the stack is empty
    if (myStack.empty())
        cout << "Stack is empty" << endl;
    else
        cout << "Stack is not empty" << endl;

    // Getting the size of the stack
    cout << "Size of the stack: " << myStack.size() << endl;

    return 0;
}
```

Now, let's move on to the queue.

```cpp
#include <iostream>
#include <queue>

using namespace std;

int main() {
    // Creating a queue
    queue<int> myQueue;

    // Pushing elements into the queue
    myQueue.push(5);
    myQueue.push(10);
    myQueue.push(15);

    // Accessing the front element of the queue
    cout << "Front element of the queue: " << myQueue.front() << endl;

    // Popping elements from the queue
    myQueue.pop();
    cout << "Front element after popping: " << myQueue.front() << endl;

    // Checking if the queue is empty
    if (myQueue.empty())
        cout << "Queue is empty" << endl;
    else
        cout << "Queue is not empty" << endl;

    // Getting the size of the queue
    cout << "Size of the queue: " << myQueue.size() << endl;

    return 0;
}
```

These are basic implementations of stack and queue operations in C++. Feel free to modify and expand upon them based on your requirements!

### 1. Algorithms & Data Structures (C++): Stack Applications

Stacks are fundamental data structures in computer science, primarily used for managing function calls, expression evaluation, parsing, and other applications where data needs to be accessed and manipulated in a Last-In-First-Out (LIFO) manner. Here are some common applications of stacks in C++:

1. **Expression Evaluation**:
   - Stacks are widely used in evaluating expressions, such as arithmetic expressions and postfix (Reverse Polish Notation) expressions.
   - Infix to Postfix conversion and postfix evaluation both utilize stacks.

2. **Function Call Management**:
   - When a function is called, the program must remember the address to return to after the function call completes. Stacks are used to manage this return address.
   - The function's local variables and parameters are often stored in a stack frame.

3. **Undo Functionality**:
   - Many applications, such as text editors and graphic design software, offer an 'Undo' feature. Stacks can be used to implement this functionality by keeping a stack of actions performed by the user.
   - When the user chooses to undo an action, the last action is popped from the stack and reversed.

4. **Backtracking**:
   - In algorithms such as depth-first search (DFS), backtracking involves exploring all possible paths in a search space. Stacks are used to keep track of the current path being explored.
   - When a dead-end is encountered, the algorithm can backtrack by popping elements from the stack until it finds a valid path to explore.

5. **Syntax Parsing**:
   - Stacks play a crucial role in syntax parsing, particularly in parsing context-free grammars.
   - For example, in a recursive descent parser, a stack is used to track the production rules that have been matched so far.

6. **Memory Management**:
   - In some memory management systems, a stack is used to allocate and deallocate memory for function calls and local variables.
   - Each function call pushes a new stack frame onto the stack, and when the function returns, its stack frame is popped.

7. **Checking for Balanced Parentheses**:
   - Stacks are commonly used to check whether parentheses, brackets, and braces in an expression are balanced.
   - As the expression is parsed, opening symbols are pushed onto the stack, and when a closing symbol is encountered, it is compared with the top of the stack.

These are just a few examples of how stacks are used in C++ programming. Stacks are versatile data structures with numerous applications across various domains.

### 1. Algorithms & Data Structures (C++): Stack as an array

Sure, let's delve into implementing a stack using an array in C++. A stack is a data structure that follows the Last In, First Out (LIFO) principle, meaning that the most recently added element is the first one to be removed.

Here's a basic implementation of a stack using an array in C++:

```cpp
#include <iostream>
#define MAX_SIZE 100 // Define maximum size for the stack

class Stack {
private:
    int arr[MAX_SIZE];
    int top;

public:
    Stack() {
        top = -1; // Initialize top as -1 to indicate an empty stack
    }

    bool isEmpty() {
        return (top == -1);
    }

    bool isFull() {
        return (top == MAX_SIZE - 1);
    }

    void push(int x) {
        if (isFull()) {
            std::cout << "Stack Overflow\n";
            return;
        }
        arr[++top] = x; // Increment top and then insert element
        std::cout << x << " pushed into stack\n";
    }

    int pop() {
        if (isEmpty()) {
            std::cout << "Stack Underflow\n";
            return -1; // Returning a default value, you can handle underflow differently based on your need
        }
        return arr[top--]; // Return top element and then decrement top
    }

    int peek() {
        if (isEmpty()) {
            std::cout << "Stack is empty\n";
            return -1; // Returning a default value, you can handle this differently based on your need
        }
        return arr[top]; // Return top element without removing it
    }
};

int main() {
    Stack stack;

    stack.push(5);
    stack.push(10);
    stack.push(15);

    std::cout << stack.pop() << " popped from stack\n";
    std::cout << "Top element is " << stack.peek() << std::endl;

    return 0;
}
```

In this implementation:

- The array `arr` is used to store the elements of the stack.
- `top` keeps track of the index of the top element in the stack.
- `isEmpty()` checks if the stack is empty.
- `isFull()` checks if the stack is full.
- `push(int x)` adds an element to the top of the stack.
- `pop()` removes and returns the top element from the stack.
- `peek()` returns the top element without removing it from the stack.

You can adjust the `MAX_SIZE` macro according to your needs. Keep in mind that this implementation has a fixed size, but you can modify it to use dynamic memory allocation if you need a stack of arbitrary size.

### 1. Algorithms & Data Structures (C++): Stack Data Structure

A stack is a fundamental data structure in computer science that follows the Last In, First Out (LIFO) principle. It's like a stack of plates where you can only add (push) or remove (pop) from the top. Here's a basic implementation of a stack in C++:

```cpp
#include <iostream>
#include <stack>

int main() {
    // Creating a stack of integers
    std::stack<int> myStack;

    // Pushing elements onto the stack
    myStack.push(10);
    myStack.push(20);
    myStack.push(30);

    // Getting the size of the stack
    std::cout << "Size of stack: " << myStack.size() << std::endl;

    // Accessing the top element of the stack
    std::cout << "Top element: " << myStack.top() << std::endl;

    // Popping elements from the stack
    myStack.pop();

    // Checking if the stack is empty
    if (myStack.empty()) {
        std::cout << "Stack is empty." << std::endl;
    } else {
        std::cout << "Stack is not empty." << std::endl;
    }

    return 0;
}
```

In this example:

- We include the necessary header files for `iostream` and `stack`.
- We create a stack named `myStack` that stores integers.
- We push three integers onto the stack using the `push()` method.
- We retrieve the size of the stack using the `size()` method.
- We access the top element of the stack without removing it using the `top()` method.
- We pop an element from the stack using the `pop()` method.
- We check if the stack is empty using the `empty()` method.

This is just a basic example. Stacks are used in various algorithms and applications, such as function call stacks, expression evaluation, backtracking algorithms, and more.

### 1. Algorithms & Data Structures (C++): Stack Double Function

Sure, I can provide you with an example of implementing a stack data structure in C++ and a function to double its elements. Here's a basic implementation:

```cpp
#include <iostream>
#include <stack>

using namespace std;

// Function to double the elements of a stack
void doubleStack(stack<int> &s) {
    stack<int> tempStack;

    // Transfer elements from original stack to temp stack and double them
    while (!s.empty()) {
        int element = s.top();
        s.pop();
        tempStack.push(2 * element);
    }

    // Transfer elements back to original stack
    while (!tempStack.empty()) {
        int element = tempStack.top();
        tempStack.pop();
        s.push(element);
    }
}

int main() {
    stack<int> myStack;

    // Push elements onto the stack
    myStack.push(1);
    myStack.push(2);
    myStack.push(3);
    myStack.push(4);
    myStack.push(5);

    // Double the elements of the stack
    doubleStack(myStack);

    // Print the doubled elements
    cout << "Doubled stack elements: ";
    while (!myStack.empty()) {
        cout << myStack.top() << " ";
        myStack.pop();
    }
    cout << endl;

    return 0;
}
```

In this example:

1. We define a `doubleStack` function that takes a reference to a `stack<int>` as its parameter.
2. Inside the function, we create a temporary stack (`tempStack`) to store the doubled elements.
3. We iterate through the original stack (`s`), popping elements one by one, doubling them, and pushing them onto the `tempStack`.
4. After all elements are doubled and transferred to the `tempStack`, we transfer them back to the original stack (`s`).
5. In the `main` function, we create a stack `myStack`, push some elements onto it, call the `doubleStack` function to double its elements, and then print the doubled elements.

This code demonstrates a basic implementation of a stack and a function to double its elements in C++.

### 1. Algorithms & Data Structures (C++): Stack Implementation (Array)

Sure, I can guide you through implementing a stack using arrays in C++. Here's a simple implementation:

```cpp
#include <iostream>

// Define the maximum size of the stack
const int MAX_SIZE = 100;

class Stack {
private:
    int top; // Index of the top element
    int arr[MAX_SIZE]; // Array to store stack elements

public:
    Stack() {
        top = -1; // Initialize top to -1 indicating an empty stack
    }

    // Function to push an element onto the stack
    void push(int value) {
        if (top >= MAX_SIZE - 1) {
            std::cout << "Stack Overflow\n";
            return;
        }
        arr[++top] = value;
    }

    // Function to pop an element from the stack
    int pop() {
        if (top < 0) {
            std::cout << "Stack Underflow\n";
            return -1; // Returning a default value since stack is empty
        }
        return arr[top--];
    }

    // Function to check if the stack is empty
    bool isEmpty() {
        return top == -1;
    }

    // Function to get the top element of the stack
    int peek() {
        if (top < 0) {
            std::cout << "Stack is empty\n";
            return -1; // Returning a default value since stack is empty
        }
        return arr[top];
    }
};

int main() {
    Stack stack;

    stack.push(10);
    stack.push(20);
    stack.push(30);

    std::cout << "Top element: " << stack.peek() << std::endl;

    std::cout << "Popped element: " << stack.pop() << std::endl;
    std::cout << "Popped element: " << stack.pop() << std::endl;

    std::cout << "Top element: " << stack.peek() << std::endl;

    stack.push(40);

    std::cout << "Top element: " << stack.peek() << std::endl;

    return 0;
}
```

In this implementation:

- `MAX_SIZE` defines the maximum capacity of the stack.
- `Stack` class encapsulates the stack data structure and its operations.
- `push` function inserts an element onto the stack.
- `pop` function removes and returns the top element from the stack.
- `isEmpty` function checks if the stack is empty.
- `peek` function returns the top element of the stack without removing it.
- In the `main` function, we create a stack object and demonstrate its usage by pushing, popping, and peeking elements.

### 1. Algorithms & Data Structures (C++): Stack Implementation (Linked Lists)

Certainly! Implementing a stack using linked lists in C++ is a fundamental exercise in understanding both data structures and pointers. Here's a basic implementation:

```cpp
#include <iostream>

template <typename T>
class Node {
public:
    T data;
    Node<T>* next;

    Node(T data) : data(data), next(nullptr) {}
};

template <typename T>
class Stack {
private:
    Node<T>* top;

public:
    Stack() : top(nullptr) {}

    ~Stack() {
        while (!isEmpty()) {
            pop();
        }
    }

    void push(T data) {
        Node<T>* newNode = new Node<T>(data);
        if (isEmpty()) {
            top = newNode;
        } else {
            newNode->next = top;
            top = newNode;
        }
    }

    void pop() {
        if (!isEmpty()) {
            Node<T>* temp = top;
            top = top->next;
            delete temp;
        } else {
            std::cout << "Stack underflow! Cannot pop from an empty stack." << std::endl;
        }
    }

    T peek() {
        if (!isEmpty()) {
            return top->data;
        } else {
            std::cerr << "Stack is empty! No top element to peek." << std::endl;
            // Return a default value, you can change this based on your requirements
            return T();
        }
    }

    bool isEmpty() {
        return top == nullptr;
    }
};

int main() {
    Stack<int> stack;

    stack.push(5);
    stack.push(10);
    stack.push(15);

    std::cout << "Top element: " << stack.peek() << std::endl;

    stack.pop();
    std::cout << "Top element after pop: " << stack.peek() << std::endl;

    stack.pop();
    std::cout << "Top element after second pop: " << stack.peek() << std::endl;

    stack.pop(); // This will print an error message since the stack is empty

    return 0;
}
```

In this implementation:

- `Node<T>` represents each element of the stack, containing the data and a pointer to the next node.
- `Stack<T>` is the stack data structure itself, with member functions to manipulate the stack.
- `push()` adds a new element to the top of the stack.
- `pop()` removes the top element from the stack.
- `peek()` returns the top element without removing it.
- `isEmpty()` checks if the stack is empty.
- The `main()` function demonstrates basic usage of the stack.

Make sure to include error handling for edge cases, such as trying to pop from an empty stack, based on your requirements.

### 1. Algorithms & Data Structures (C++): Stack Implementation (LinkedList)

Sure, here's a basic implementation of a stack using a linked list in C++:

```cpp
#include <iostream>

// Node class to represent each element in the stack
class Node {
public:
    int data;
    Node* next;

    Node(int data) {
        this->data = data;
        this->next = nullptr;
    }
};

// Stack class
class Stack {
private:
    Node* top; // Pointer to the top of the stack

public:
    Stack() {
        top = nullptr;
    }

    // Function to push an element onto the stack
    void push(int data) {
        Node* newNode = new Node(data);
        if (top == nullptr) {
            top = newNode;
        } else {
            newNode->next = top;
            top = newNode;
        }
        std::cout << data << " pushed to stack." << std::endl;
    }

    // Function to pop an element from the stack
    int pop() {
        if (isEmpty()) {
            std::cerr << "Stack is empty. Cannot pop." << std::endl;
            return INT_MIN; // Returning INT_MIN to signify underflow
        }
        int popped = top->data;
        Node* temp = top;
        top = top->next;
        delete temp;
        return popped;
    }

    // Function to check if the stack is empty
    bool isEmpty() {
        return top == nullptr;
    }

    // Function to return the top element of the stack without popping it
    int peek() {
        if (isEmpty()) {
            std::cerr << "Stack is empty. Cannot peek." << std::endl;
            return INT_MIN; // Returning INT_MIN to signify underflow
        }
        return top->data;
    }
};

int main() {
    Stack stack;
    stack.push(5);
    stack.push(10);
    stack.push(15);

    std::cout << "Top element: " << stack.peek() << std::endl;

    std::cout << "Popped element: " << stack.pop() << std::endl;
    std::cout << "Popped element: " << stack.pop() << std::endl;

    std::cout << "Top element: " << stack.peek() << std::endl;

    stack.push(20);

    std::cout << "Top element after push: " << stack.peek() << std::endl;

    return 0;
}
```

This code implements a stack using a linked list. The `Node` class represents each element of the stack, and the `Stack` class contains the necessary functions to manipulate the stack (push, pop, isEmpty, peek). In the `main` function, some sample operations on the stack are demonstrated.

### 1. Algorithms & Data Structures (C++): Stack Implementation using Array

Sure, here's a simple implementation of a stack using an array in C++:

```cpp
#include <iostream>
using namespace std;

const int MAX_SIZE = 100; // Maximum size of the stack

class Stack {
private:
    int arr[MAX_SIZE];
    int top;

public:
    Stack() {
        top = -1; // Initialize top to -1 indicating empty stack
    }

    bool isEmpty() {
        return (top == -1);
    }

    bool isFull() {
        return (top == MAX_SIZE - 1);
    }

    void push(int value) {
        if (isFull()) {
            cout << "Stack Overflow! Cannot push element.\n";
            return;
        }
        arr[++top] = value;
    }

    void pop() {
        if (isEmpty()) {
            cout << "Stack Underflow! Cannot pop element.\n";
            return;
        }
        top--;
    }

    int peek() {
        if (isEmpty()) {
            cout << "Stack is empty.\n";
            return -1;
        }
        return arr[top];
    }
};

int main() {
    Stack stack;

    // Pushing elements onto the stack
    stack.push(10);
    stack.push(20);
    stack.push(30);
    stack.push(40);

    // Popping elements from the stack
    stack.pop();
    stack.pop();

    // Printing the top element
    cout << "Top element: " << stack.peek() << endl;

    return 0;
}
```

This implementation defines a class `Stack` with methods for basic stack operations like `push`, `pop`, `isEmpty`, `isFull`, and `peek`. The stack is implemented using an array, and the maximum size of the stack is defined by the constant `MAX_SIZE`. The stack follows the Last In First Out (LIFO) principle.

### 1. Algorithms & Data Structures (C++): Stack implementation with linked lists

Sure, implementing a stack using linked lists in C++ is a fundamental exercise in data structures. Here's a basic implementation:

```cpp
#include <iostream>

template <typename T>
class Node {
public:
    T data;
    Node<T>* next;

    Node(T data) : data(data), next(nullptr) {}
};

template <typename T>
class Stack {
private:
    Node<T>* topNode;
    int size;

public:
    Stack() : topNode(nullptr), size(0) {}

    // Push operation
    void push(T data) {
        Node<T>* newNode = new Node<T>(data);
        newNode->next = topNode;
        topNode = newNode;
        size++;
    }

    // Pop operation
    T pop() {
        if (isEmpty()) {
            std::cerr << "Stack is empty, cannot pop.\n";
            exit(EXIT_FAILURE);
        }
        T poppedData = topNode->data;
        Node<T>* temp = topNode;
        topNode = topNode->next;
        delete temp;
        size--;
        return poppedData;
    }

    // Peek operation
    T peek() {
        if (isEmpty()) {
            std::cerr << "Stack is empty, cannot peek.\n";
            exit(EXIT_FAILURE);
        }
        return topNode->data;
    }

    // Check if the stack is empty
    bool isEmpty() {
        return topNode == nullptr;
    }

    // Get the size of the stack
    int getSize() {
        return size;
    }
};

int main() {
    Stack<int> stack;

    // Push some elements onto the stack
    stack.push(10);
    stack.push(20);
    stack.push(30);

    // Print the top element of the stack
    std::cout << "Top element: " << stack.peek() << std::endl;

    // Pop an element from the stack
    std::cout << "Popped element: " << stack.pop() << std::endl;

    // Print the top element of the stack again
    std::cout << "Top element: " << stack.peek() << std::endl;

    return 0;
}
```

In this implementation, we have two classes: `Node`, which represents a single node in the linked list, and `Stack`, which implements the stack data structure using linked lists. The `Stack` class contains methods for `push`, `pop`, `peek`, `isEmpty`, and `getSize` operations.

The `push` operation adds a new element to the top of the stack, the `pop` operation removes and returns the top element of the stack, the `peek` operation returns the top element without removing it, `isEmpty` checks if the stack is empty, and `getSize` returns the current size of the stack.

In the `main` function, we create a `Stack` object, push some elements onto it, perform operations, and print the results to demonstrate the functionality.

### 1. Algorithms & Data Structures (C++): Stack Implementations

Certainly! In C++, you can implement a stack using various approaches. Here's a basic implementation using arrays and another using linked lists:

### Stack Implementation using Arrays

```cpp
#include <iostream>

#define MAX_SIZE 1000

class Stack {
private:
    int top;
    int arr[MAX_SIZE];
public:
    Stack() { top = -1; }

    bool push(int x) {
        if (top >= (MAX_SIZE - 1)) {
            std::cout << "Stack Overflow\n";
            return false;
        }
        arr[++top] = x;
        return true;
    }

    int pop() {
        if (top < 0) {
            std::cout << "Stack Underflow\n";
            return -1;
        }
        return arr[top--];
    }

    int peek() {
        if (top < 0) {
            std::cout << "Stack is Empty\n";
            return -1;
        }
        return arr[top];
    }

    bool isEmpty() { return (top < 0); }
};

int main() {
    Stack stack;
    stack.push(10);
    stack.push(20);
    stack.push(30);

    std::cout << stack.pop() << " Popped from stack\n";
    std::cout << "Top element is " << stack.peek() << std::endl;
    std::cout << "Is the stack empty? " << (stack.isEmpty() ? "Yes" : "No") << std::endl;

    return 0;
}
```

### Stack Implementation using Linked Lists

```cpp
#include <iostream>

class Node {
public:
    int data;
    Node* next;
};

class Stack {
private:
    Node* top;
public:
    Stack() { top = nullptr; }

    bool push(int x) {
        Node* newNode = new Node();
        if (newNode == nullptr) {
            std::cout << "Stack Overflow\n";
            return false;
        }
        newNode->data = x;
        newNode->next = top;
        top = newNode;
        return true;
    }

    int pop() {
        if (top == nullptr) {
            std::cout << "Stack Underflow\n";
            return -1;
        }
        int popped = top->data;
        Node* temp = top;
        top = top->next;
        delete temp;
        return popped;
    }

    int peek() {
        if (top == nullptr) {
            std::cout << "Stack is Empty\n";
            return -1;
        }
        return top->data;
    }

    bool isEmpty() { return (top == nullptr); }
};

int main() {
    Stack stack;
    stack.push(10);
    stack.push(20);
    stack.push(30);

    std::cout << stack.pop() << " Popped from stack\n";
    std::cout << "Top element is " << stack.peek() << std::endl;
    std::cout << "Is the stack empty? " << (stack.isEmpty() ? "Yes" : "No") << std::endl;

    return 0;
}
```

Both implementations provide the basic functionalities of a stack: `push`, `pop`, `peek`, and `isEmpty`. The first implementation uses a fixed-size array, while the second one uses a linked list. Choose the one that suits your needs best!

### 1. Algorithms & Data Structures (C++): Stack Insert At Bottom

To insert an element at the bottom of a stack in C++, you typically need to reverse the stack, push the new element, and then reverse it again to restore the original order. Here's a C++ implementation using recursion:

```cpp
#include <iostream>
#include <stack>

using namespace std;

// Function to insert an element at the bottom of a stack
void insertAtBottom(stack<int> &stk, int item) {
    // Base case: if the stack is empty, push the item
    if (stk.empty()) {
        stk.push(item);
    } else {
        // Recursive case: pop the top element and call insertAtBottom recursively
        int temp = stk.top();
        stk.pop();
        insertAtBottom(stk, item);
        // Push the popped item back after inserting the new item at bottom
        stk.push(temp);
    }
}

int main() {
    stack<int> stk;
    
    // Push elements onto the stack
    stk.push(1);
    stk.push(2);
    stk.push(3);
    
    // Item to be inserted at the bottom
    int newItem = 4;
    
    // Insert newItem at the bottom of the stack
    insertAtBottom(stk, newItem);
    
    // Print the stack to verify the result
    while (!stk.empty()) {
        cout << stk.top() << " ";
        stk.pop();
    }
    
    return 0;
}
```

This code will output:

```
4 3 2 1
```

Here, `insertAtBottom` function recursively pops each element from the stack until it reaches the bottom, then it pushes the new item, and finally pushes back the popped elements.

### 1. Algorithms & Data Structures (C++): Stack Member Functions

In C++, a stack is a data structure that follows the Last In, First Out (LIFO) principle. It has a variety of member functions to manipulate its elements. Here are some common member functions you might find in a stack implementation:

1. **push(element)**: Adds an element to the top of the stack.

2. **pop()**: Removes the top element from the stack. The element is not returned but removed from the stack.

3. **top()**: Returns a reference to the top element of the stack, without removing it. This function doesn't modify the stack.

4. **empty()**: Returns true if the stack is empty; otherwise, returns false.

5. **size()**: Returns the number of elements currently in the stack.

These functions are fundamental for using a stack in C++. Here's a simple example demonstrating their usage:

```cpp
#include <iostream>
#include <stack>

int main() {
    std::stack<int> myStack;

    // Pushing elements onto the stack
    myStack.push(10);
    myStack.push(20);
    myStack.push(30);

    std::cout << "Stack size: " << myStack.size() << std::endl; // Output: 3

    // Accessing the top element
    std::cout << "Top element: " << myStack.top() << std::endl; // Output: 30

    // Popping elements from the stack
    myStack.pop();
    std::cout << "Stack size after pop: " << myStack.size() << std::endl; // Output: 2

    // Checking if the stack is empty
    if (!myStack.empty()) {
        std::cout << "Stack is not empty." << std::endl;
    } else {
        std::cout << "Stack is empty." << std::endl;
    }

    return 0;
}
```

This example demonstrates the basic usage of stack member functions. You can use these functions to manipulate the stack's elements according to the LIFO principle.

### 1. Algorithms & Data Structures (C++): Stack memory visualization

Visualizing stack memory in C++ can help in understanding how local variables, function calls, and control flow interact within a program. Let's create a simple example to demonstrate this:

```cpp
#include <iostream>

void function1(int x) {
    int y = x * 2;
    std::cout << "Function 1: " << y << std::endl;
}

void function2(int a, int b) {
    int z = a + b;
    function1(z);
    std::cout << "Function 2: " << z << std::endl;
}

int main() {
    int num1 = 5;
    int num2 = 10;
    function2(num1, num2);
    return 0;
}
```

Let's break down what happens during the execution of this program:

1. **main()**: When the program starts, it calls the `main()` function. Two integer variables `num1` and `num2` are declared on the stack and initialized with values `5` and `10` respectively.

   ```bash
   Stack:
   |  num2 (10)  |
   |  num1 (5)   |
   |  main()     |
   ```

2. **function2()**: `main()` then calls `function2(num1, num2)`. Inside `function2()`, two integer variables `a` and `b` are declared on the stack and initialized with the values of `num1` and `num2` respectively. Another integer variable `z` is declared and initialized with the sum of `a` and `b`.

   ```bash
   Stack:
   |  z (15)     |
   |  b (10)     |
   |  a (5)      |
   |  num2 (10)  |
   |  num1 (5)   |
   |  main()     |
   ```

3. **function1()**: `function2()` then calls `function1(z)`. Inside `function1()`, an integer variable `y` is declared and initialized with the value of `z` multiplied by `2`.

   ```bash
   Stack:
   |  y (30)     |
   |  z (15)     |
   |  b (10)     |
   |  a (5)      |
   |  num2 (10)  |
   |  num1 (5)   |
   |  main()     |
   ```

4. **Output**: After `function1()` returns, `function2()` prints the value of `z`, and then `main()` prints a newline and returns 0.

   ```bash
   Stack:
   |  z (15)     |
   |  b (10)     |
   |  a (5)      |
   |  num2 (10)  |
   |  num1 (5)   |
   |  main()     |
   ```

Eventually, as each function completes its execution, its stack frame is removed from the stack, and control returns to the calling function. This process continues until the `main()` function completes, and the program terminates.

### 1. Algorithms & Data Structures (C++): Stack memory visualization - finding max (min) items

Visualizing how stack memory works with algorithms and data structures, like finding the maximum or minimum items, can be really helpful for understanding. Let's break it down.

In C++, a stack is a data structure that follows the Last In, First Out (LIFO) principle. It means that the last element added to the stack will be the first one to be removed. You can visualize it like a stack of plates where you can only add or remove from the top.

Now, let's talk about finding the maximum (or minimum) item in a stack.

### Finding Maximum Item in a Stack

To find the maximum item in a stack, you can iterate through all the elements in the stack and keep track of the maximum item found so far. Here's how you can do it:

```cpp
#include <iostream>
#include <stack>

int findMax(std::stack<int>& s) {
    if (s.empty()) {
        // If the stack is empty, there is no maximum element
        std::cerr << "Stack is empty!" << std::endl;
        return INT_MIN; // Return minimum integer value
    }

    int maxItem = s.top(); // Initialize maxItem with the top element

    // Iterate through the stack
    while (!s.empty()) {
        // Compare each element with maxItem
        if (s.top() > maxItem) {
            maxItem = s.top(); // Update maxItem if a larger element is found
        }
        s.pop(); // Remove the element from the stack
    }

    return maxItem;
}

int main() {
    std::stack<int> myStack;
    myStack.push(3);
    myStack.push(8);
    myStack.push(1);
    myStack.push(6);

    std::cout << "Maximum item in the stack: " << findMax(myStack) << std::endl;

    return 0;
}
```

This code snippet demonstrates how to find the maximum item in a stack. It iterates through the stack, updates `maxItem` whenever a larger element is found, and finally returns the maximum item.

You can do something similar to find the minimum item in a stack by updating the logic to find the smallest item instead of the largest.

Understanding algorithms and data structures through visualization and hands-on coding can significantly enhance your comprehension and proficiency.

### 1. Algorithms & Data Structures (C++): Stack memory visualization - tree traversal

Visualizing stack memory during tree traversal in C++ is a great way to understand how recursive algorithms work. Let's consider the depth-first traversal methods: pre-order, in-order, and post-order traversal. We'll use a simple binary tree structure for demonstration.

Here's a basic implementation in C++:

```cpp
#include <iostream>
#include <stack>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
    Node(int value) : data(value), left(nullptr), right(nullptr) {}
};

void preOrderTraversal(Node* root) {
    if (root == nullptr) return;

    stack<Node*> nodeStack;
    nodeStack.push(root);

    while (!nodeStack.empty()) {
        Node* current = nodeStack.top();
        nodeStack.pop();
        cout << current->data << " ";

        if (current->right != nullptr)
            nodeStack.push(current->right);
        if (current->left != nullptr)
            nodeStack.push(current->left);
    }
}

void inOrderTraversal(Node* root) {
    if (root == nullptr) return;

    stack<Node*> nodeStack;
    Node* current = root;

    while (current != nullptr || !nodeStack.empty()) {
        while (current != nullptr) {
            nodeStack.push(current);
            current = current->left;
        }
        current = nodeStack.top();
        nodeStack.pop();
        cout << current->data << " ";
        current = current->right;
    }
}

void postOrderTraversal(Node* root) {
    if (root == nullptr) return;

    stack<Node*> nodeStack;
    Node* current = root;
    Node* lastVisitedNode = nullptr;

    while (current != nullptr || !nodeStack.empty()) {
        if (current != nullptr) {
            nodeStack.push(current);
            current = current->left;
        } else {
            Node* peekNode = nodeStack.top();
            if (peekNode->right != nullptr && lastVisitedNode != peekNode->right)
                current = peekNode->right;
            else {
                cout << peekNode->data << " ";
                lastVisitedNode = nodeStack.top();
                nodeStack.pop();
            }
        }
    }
}

int main() {
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    root->right->left = new Node(6);
    root->right->right = new Node(7);

    cout << "Pre-order traversal: ";
    preOrderTraversal(root);
    cout << endl;

    cout << "In-order traversal: ";
    inOrderTraversal(root);
    cout << endl;

    cout << "Post-order traversal: ";
    postOrderTraversal(root);
    cout << endl;

    return 0;
}
```

This code will help you visualize how the stack is used during different tree traversal methods. You can run it and observe the order in which nodes are pushed and popped from the stack, giving you insight into the traversal process.

### 1. Algorithms & Data Structures (C++): Stack of Plates

Certainly! Let's delve into the implementation of a "Stack of Plates" using C++. This is based on the concept of a stack but extends it by creating multiple stacks when one stack exceeds a certain capacity. This is often called "Set of Stacks".

Here's a step-by-step approach to implement this:

1. **Define the Stack class**: This will be a basic stack implementation.
2. **Define the SetOfStacks class**: This will manage multiple stacks.

### Step 1: Stack Class

First, we create a basic Stack class to handle the stack operations:

```cpp
#include <vector>
#include <stdexcept>

template <typename T>
class Stack {
private:
    std::vector<T> elements;
    int capacity;

public:
    Stack(int cap) : capacity(cap) {}

    void push(T value) {
        if (elements.size() >= capacity) {
            throw std::overflow_error("Stack is full");
        }
        elements.push_back(value);
    }

    T pop() {
        if (elements.empty()) {
            throw std::underflow_error("Stack is empty");
        }
        T value = elements.back();
        elements.pop_back();
        return value;
    }

    T top() const {
        if (elements.empty()) {
            throw std::underflow_error("Stack is empty");
        }
        return elements.back();
    }

    bool isEmpty() const {
        return elements.empty();
    }

    bool isFull() const {
        return elements.size() >= capacity;
    }

    int size() const {
        return elements.size();
    }
};
```

### Step 2: SetOfStacks Class

Now, we implement the SetOfStacks class that will manage multiple stacks:

```cpp
#include <iostream>
#include <vector>
#include <stdexcept>

template <typename T>
class SetOfStacks {
private:
    std::vector<Stack<T>> stacks;
    int stackCapacity;

public:
    SetOfStacks(int capacity) : stackCapacity(capacity) {
        stacks.push_back(Stack<T>(capacity));
    }

    void push(T value) {
        if (stacks.back().isFull()) {
            stacks.push_back(Stack<T>(stackCapacity));
        }
        stacks.back().push(value);
    }

    T pop() {
        if (stacks.empty() || stacks.back().isEmpty()) {
            throw std::underflow_error("All stacks are empty");
        }
        T value = stacks.back().pop();
        if (stacks.back().isEmpty() && stacks.size() > 1) {
            stacks.pop_back();
        }
        return value;
    }

    T top() const {
        if (stacks.empty() || stacks.back().isEmpty()) {
            throw std::underflow_error("All stacks are empty");
        }
        return stacks.back().top();
    }

    bool isEmpty() const {
        return stacks.size() == 1 && stacks.back().isEmpty();
    }

    int numberOfStacks() const {
        return stacks.size();
    }
};

int main() {
    SetOfStacks<int> setOfStacks(3);

    // Test pushing
    setOfStacks.push(1);
    setOfStacks.push(2);
    setOfStacks.push(3);
    setOfStacks.push(4);  // This should create a new stack

    // Test popping
    std::cout << "Popped: " << setOfStacks.pop() << std::endl;  // Should be 4
    std::cout << "Top: " << setOfStacks.top() << std::endl;  // Should be 3
    setOfStacks.pop(); // Popping 3
    setOfStacks.pop(); // Popping 2
    setOfStacks.pop(); // Popping 1

    // Check if empty
    std::cout << "Is empty: " << setOfStacks.isEmpty() << std::endl;

    return 0;
}
```

### Explanation

1. **Stack Class**:
    - This is a generic stack class using `std::vector` to store elements.
    - It has standard stack operations: `push`, `pop`, `top`, `isEmpty`, `isFull`, and `size`.

2. **SetOfStacks Class**:
    - Manages multiple stacks where each stack has a fixed capacity.
    - `push` operation checks if the last stack is full; if so, it creates a new stack and pushes the element.
    - `pop` operation checks if the last stack is empty after popping an element; if it is, it removes the stack from the set.
    - `top` operation retrieves the top element of the last stack.
    - `isEmpty` checks if the entire set of stacks is empty.
    - `numberOfStacks` returns the number of stacks currently managed.

### Testing

The `main` function demonstrates basic operations: pushing elements to exceed the stack capacity, popping elements, and checking if the stacks are empty. Adjust the capacity and operations as needed to test various scenarios.

This implementation should give you a solid foundation to build and extend a "Set of Stacks" in C++.

### 1. Algorithms & Data Structures (C++): Stack operations

Certainly! In C++, you can implement stack operations using the `std::stack` container provided by the Standard Template Library (STL). Here's a basic overview of stack operations:

1. **Push**: Adds an element to the top of the stack.
2. **Pop**: Removes the element from the top of the stack.
3. **Top (or Peek)**: Returns the element at the top of the stack without removing it.
4. **Empty**: Checks if the stack is empty.
5. **Size**: Returns the number of elements in the stack.

Here's how you can implement these operations:

```cpp
#include <iostream>
#include <stack>

int main() {
    std::stack<int> myStack;

    // Pushing elements onto the stack
    myStack.push(10);
    myStack.push(20);
    myStack.push(30);

    // Popping an element from the stack
    myStack.pop();

    // Top element of the stack
    std::cout << "Top element: " << myStack.top() << std::endl;

    // Checking if the stack is empty
    if (myStack.empty()) {
        std::cout << "Stack is empty." << std::endl;
    } else {
        std::cout << "Stack is not empty." << std::endl;
    }

    // Size of the stack
    std::cout << "Size of stack: " << myStack.size() << std::endl;

    return 0;
}
```

This code demonstrates basic stack operations. You can add more elements using `push`, remove elements using `pop`, check the top element using `top`, check if the stack is empty using `empty`, and get the size of the stack using `size`.

### 1. Algorithms & Data Structures (C++): Stack Operations using Linked List

Certainly! Below is a simple implementation of a stack using a linked list in C++:

```cpp
#include <iostream>

// Define the structure of each node in the linked list
struct Node {
    int data;
    Node* next;
    
    Node(int val) : data(val), next(nullptr) {}
};

// Define the Stack class
class Stack {
private:
    Node* top;

public:
    Stack() : top(nullptr) {}

    // Function to push a new element onto the stack
    void push(int val) {
        Node* newNode = new Node(val);
        if (top == nullptr) {
            top = newNode;
        } else {
            newNode->next = top;
            top = newNode;
        }
    }

    // Function to pop the top element from the stack
    void pop() {
        if (top == nullptr) {
            std::cout << "Stack Underflow! The stack is empty.\n";
            return;
        }
        Node* temp = top;
        top = top->next;
        delete temp;
    }

    // Function to get the top element of the stack without removing it
    int peek() {
        if (top == nullptr) {
            std::cout << "Stack is empty.\n";
            return -1; // Or any appropriate value to indicate empty stack
        }
        return top->data;
    }

    // Function to check if the stack is empty
    bool isEmpty() {
        return top == nullptr;
    }
};

int main() {
    Stack myStack;

    // Push some elements onto the stack
    myStack.push(5);
    myStack.push(10);
    myStack.push(15);

    // Print the top element
    std::cout << "Top element: " << myStack.peek() << std::endl;

    // Pop one element from the stack
    myStack.pop();

    // Print the top element after popping
    std::cout << "Top element after pop: " << myStack.peek() << std::endl;

    // Check if the stack is empty
    std::cout << "Is the stack empty? " << (myStack.isEmpty() ? "Yes" : "No") << std::endl;

    return 0;
}
```

This code implements basic stack operations (`push`, `pop`, `peek`, and `isEmpty`) using a linked list. Each element in the stack is represented by a node in the linked list, and the top of the stack is always the first node in the list.

### 1. Algorithms & Data Structures (C++): Stack practice: Merge Intervals

Certainly! Let's go through the problem of merging intervals using a stack in C++. The problem is to merge overlapping intervals and return the list of merged intervals.

#### Problem Statement

Given a collection of intervals, merge all overlapping intervals.

#### Example

```bash
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].
```

#### Steps to Solve the Problem

1. **Sort the Intervals:** First, sort the intervals based on the starting time. This will help to easily identify overlapping intervals.
2. **Use a Stack to Merge Intervals:**
   - Push the first interval onto the stack.
   - For each subsequent interval, check if it overlaps with the interval on top of the stack.
     - If it does, merge them and update the interval on the stack.
     - If it doesn’t, push the new interval onto the stack.

#### Detailed Implementation in C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <stack>

using namespace std;

struct Interval {
    int start;
    int end;
    Interval() : start(0), end(0) {}
    Interval(int s, int e) : start(s), end(e) {}
};

bool compareInterval(Interval a, Interval b) {
    return a.start < b.start;
}

vector<Interval> merge(vector<Interval>& intervals) {
    if(intervals.empty()) return vector<Interval>();
    
    // Sort the intervals based on the starting time
    sort(intervals.begin(), intervals.end(), compareInterval);
    
    // Use a stack to help merge intervals
    stack<Interval> s;
    s.push(intervals[0]);
    
    for(int i = 1; i < intervals.size(); i++) {
        Interval top = s.top();
        
        // If the current interval does not overlap with the stack top, push it to the stack
        if(top.end < intervals[i].start) {
            s.push(intervals[i]);
        }
        // Otherwise, there is overlap, so merge the current interval with the stack top
        else if(top.end < intervals[i].end) {
            top.end = intervals[i].end;
            s.pop();
            s.push(top);
        }
    }
    
    // Extracting the merged intervals from the stack
    vector<Interval> result;
    while(!s.empty()) {
        result.push_back(s.top());
        s.pop();
    }
    
    // The stack stores the result in reverse order, so reverse it back
    reverse(result.begin(), result.end());
    
    return result;
}

int main() {
    vector<Interval> intervals = {Interval(1, 3), Interval(2, 6), Interval(8, 10), Interval(15, 18)};
    vector<Interval> mergedIntervals = merge(intervals);
    
    for(Interval interval : mergedIntervals) {
        cout << "[" << interval.start << ", " << interval.end << "] ";
    }
    return 0;
}
```

### Explanation

1. **Sorting:** The intervals are first sorted based on their starting points using `sort` and a custom comparator.
2. **Stack Operations:**
   - The first interval is pushed onto the stack.
   - For each interval, we check if it overlaps with the top of the stack:
     - If it does not overlap, we push it onto the stack.
     - If it overlaps, we merge the intervals by updating the end of the top interval.
3. **Result Extraction:** The intervals are extracted from the stack and reversed to maintain the original order.

### Points to Consider

- The stack helps in keeping track of merged intervals efficiently.
- Sorting the intervals simplifies the problem significantly as it ensures that we only need to look at the top of the stack for merging.
- The time complexity is dominated by the sorting step, which is \(O(n \log n)\), where \(n\) is the number of intervals. The subsequent merging process is \(O(n)\). Thus, the overall complexity is \(O(n \log n)\).

### 1. Algorithms & Data Structures (C++): Stack practice: Min Stack

Sure, let's implement a stack data structure in C++ that supports finding the minimum element in constant time. This is often referred to as the "Min Stack" problem.

Here's a basic implementation using two stacks:

```cpp
#include <stack>
#include <iostream>

using namespace std;

class MinStack {
private:
    stack<int> dataStack; // Stack to store actual data
    stack<int> minStack;  // Stack to keep track of minimum values

public:
    // Push element onto the stack
    void push(int x) {
        dataStack.push(x);
        if (minStack.empty() || x <= minStack.top()) {
            minStack.push(x);
        }
    }

    // Remove the top element from the stack
    void pop() {
        if (dataStack.empty()) {
            cout << "Stack is empty\n";
            return;
        }
        if (dataStack.top() == minStack.top()) {
            minStack.pop();
        }
        dataStack.pop();
    }

    // Get the top element of the stack
    int top() {
        if (dataStack.empty()) {
            cout << "Stack is empty\n";
            return -1; // or any error handling
        }
        return dataStack.top();
    }

    // Get the minimum element in the stack
    int getMin() {
        if (minStack.empty()) {
            cout << "Stack is empty\n";
            return -1; // or any error handling
        }
        return minStack.top();
    }

    // Check if the stack is empty
    bool isEmpty() {
        return dataStack.empty();
    }
};

int main() {
    MinStack minStack;

    minStack.push(5);
    minStack.push(3);
    minStack.push(2);
    minStack.push(8);

    cout << "Minimum element: " << minStack.getMin() << endl;

    minStack.pop();
    cout << "Minimum element after pop: " << minStack.getMin() << endl;

    minStack.pop();
    cout << "Minimum element after pop: " << minStack.getMin() << endl;

    return 0;
}
```

In this implementation, we use two stacks: `dataStack` to store the actual data and `minStack` to keep track of the minimum element at any point in time. Whenever we push an element onto the stack, we compare it with the top element of `minStack` and push it onto `minStack` only if it is less than or equal to the top element. This ensures that `minStack` always holds the minimum element at the top.

Similarly, when we pop an element from the stack, we check if the element being popped is also the minimum element. If it is, we pop it from `minStack` as well.

### 1. Algorithms & Data Structures (C++): Stack practice: Minimum Add To Make Parantheses Valid

To solve this problem, you can use a stack to keep track of the opening parentheses encountered so far. When you encounter a closing parenthesis, if there's a matching opening parenthesis on top of the stack, you pop it off. If there isn't, it means you need to add one more opening parenthesis to make it valid.

Here's how you can implement this in C++:

```cpp
#include <iostream>
#include <stack>
#include <string>

int minAddToMakeValid(std::string s) {
    std::stack<char> st;
    int count = 0;
    
    for (char c : s) {
        if (c == '(') {
            st.push(c);
        } else if (c == ')') {
            if (!st.empty() && st.top() == '(') {
                st.pop();
            } else {
                count++; // Need to add one more opening parenthesis
            }
        }
    }
    
    // At the end, the stack may still have some unmatched opening parentheses
    count += st.size();
    
    return count;
}

int main() {
    std::string s = "())";
    std::cout << "Minimum add to make parentheses valid: " << minAddToMakeValid(s) << std::endl;
    return 0;
}
```

In this code:

- We iterate through each character in the input string.
- If the character is an opening parenthesis, we push it onto the stack.
- If the character is a closing parenthesis, we check if there's a matching opening parenthesis on top of the stack. If there is, we pop it off; otherwise, we increment the count indicating that we need to add one more opening parenthesis to make it valid.
- Finally, we add the count of remaining unmatched opening parentheses on the stack to the total count, as each of them needs a corresponding closing parenthesis to make the string valid.

### 1. Algorithms & Data Structures (C++): Stack practice: Next Greater Element

Sure! The Next Greater Element problem is a classic algorithmic problem where you're given an array and you need to find the next greater element for every element in the array. In the context of this problem, "next greater element" for an element \( x \) is the first element to the right of \( x \) which is greater than \( x \). If there is no such element, then the output for that element is -1.

Here's the C++ code to solve the Next Greater Element problem using a stack:

```cpp
#include <iostream>
#include <stack>
#include <vector>
#include <unordered_map>

using namespace std;

vector<int> nextGreaterElement(const vector<int>& nums) {
    stack<int> s;
    unordered_map<int, int> nextGreater;

    for (int i = nums.size() - 1; i >= 0; --i) {
        while (!s.empty() && s.top() <= nums[i]) {
            s.pop();
        }
        if (!s.empty()) {
            nextGreater[nums[i]] = s.top();
        } else {
            nextGreater[nums[i]] = -1;
        }
        s.push(nums[i]);
    }

    vector<int> result;
    for (int num : nums) {
        result.push_back(nextGreater[num]);
    }

    return result;
}

int main() {
    vector<int> nums = {4, 5, 2, 10, 8};
    vector<int> result = nextGreaterElement(nums);

    cout << "Next Greater Elements:\n";
    for (int i = 0; i < nums.size(); ++i) {
        cout << nums[i] << " --> " << result[i] << endl;
    }

    return 0;
}
```

This code finds the next greater element for each element in the given array `nums`. It iterates through the array in reverse order. While iterating, it maintains a stack that stores elements in decreasing order. If the current element is greater than the top of the stack, it means it's the next greater element for all elements in the stack that are smaller than it. The result is stored in a hashmap. Finally, it creates a vector of next greater elements based on this hashmap.

### 1. Algorithms & Data Structures (C++): Stack practice: Valid Paranthesis

Sure! Implementing a solution to validate parentheses using a stack is a common algorithm problem. Here's a C++ implementation:

```cpp
#include <iostream>
#include <stack>
#include <string>

bool isValidParentheses(const std::string& s) {
    std::stack<char> stack;

    for (char c : s) {
        if (c == '(' || c == '[' || c == '{') {
            stack.push(c);
        } else {
            if (stack.empty()) {
                return false; // More closing brackets than opening brackets
            }
            char top = stack.top();
            stack.pop();
            if ((c == ')' && top != '(') ||
                (c == ']' && top != '[') ||
                (c == '}' && top != '{')) {
                return false; // Mismatched brackets
            }
        }
    }

    return stack.empty(); // Check if there are leftover opening brackets
}

int main() {
    std::string input;
    std::cout << "Enter a string containing parentheses: ";
    std::cin >> input;

    if (isValidParentheses(input)) {
        std::cout << "Valid parentheses\n";
    } else {
        std::cout << "Invalid parentheses\n";
    }

    return 0;
}
```

This code defines a function `isValidParentheses` that takes a string as input and returns `true` if the parentheses in the string are balanced, and `false` otherwise. The `main` function takes user input and checks if the provided string contains valid parentheses using the `isValidParentheses` function.

### 1. Algorithms & Data Structures (C++): Stack PUSH and POP using Linked Lists

Sure, I can provide you with a simple implementation of a stack using linked lists in C++. In a linked list-based stack, we will implement the push and pop operations to add and remove elements from the top of the stack, respectively.

Here's a basic implementation:

```cpp
#include <iostream>

// Define a structure for a node in the linked list
struct Node {
    int data;
    Node* next;
    
    Node(int value) : data(value), next(nullptr) {}
};

// Define the stack class
class Stack {
private:
    Node* top; // Pointer to the top of the stack

public:
    Stack() : top(nullptr) {}

    // Function to push an element onto the stack
    void push(int value) {
        Node* newNode = new Node(value); // Create a new node
        if (top == nullptr) {
            top = newNode; // If the stack is empty, the new node becomes the top
        } else {
            newNode->next = top; // Point the new node to the current top
            top = newNode; // Update the top to the new node
        }
    }

    // Function to pop an element from the stack
    int pop() {
        if (top == nullptr) {
            std::cerr << "Error: Stack is empty." << std::endl;
            return -1; // Return -1 indicating an error
        } else {
            int value = top->data; // Get the value of the top node
            Node* temp = top; // Store the current top node
            top = top->next; // Move the top to the next node
            delete temp; // Delete the old top node
            return value; // Return the popped value
        }
    }

    // Function to check if the stack is empty
    bool isEmpty() {
        return top == nullptr;
    }
};

int main() {
    Stack stack;

    // Pushing elements onto the stack
    stack.push(10);
    stack.push(20);
    stack.push(30);

    // Popping elements from the stack
    std::cout << stack.pop() << std::endl; // Output: 30
    std::cout << stack.pop() << std::endl; // Output: 20
    std::cout << stack.pop() << std::endl; // Output: 10

    // Trying to pop from an empty stack
    std::cout << stack.pop() << std::endl; // Output: Error: Stack is empty. -1

    return 0;
}
```

This implementation uses a singly linked list where each node has a data field and a pointer to the next node. The `top` pointer points to the top of the stack. The `push` operation adds a new node to the top of the stack, and the `pop` operation removes and returns the top element from the stack. The `isEmpty` function checks whether the stack is empty.

### 1. Algorithms & Data Structures (C++): Stack Question: Binary Tree Postorder Traversal

Sure! Implementing postorder traversal of a binary tree using a stack is a common algorithmic problem. In postorder traversal, you visit the nodes in the order of left subtree, right subtree, and then the root node.

Here's how you can implement the postorder traversal of a binary tree using a stack in C++:

```cpp
#include <iostream>
#include <stack>
#include <vector>

using namespace std;

// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

vector<int> postorderTraversal(TreeNode* root) {
    vector<int> result;
    stack<TreeNode*> s;
    TreeNode* prev = nullptr;
    TreeNode* current = root;

    while (current != nullptr || !s.empty()) {
        if (current != nullptr) {
            s.push(current);
            current = current->left;
        } else {
            TreeNode* temp = s.top()->right;
            if (temp == nullptr || temp == prev) {
                prev = s.top();
                result.push_back(prev->val);
                s.pop();
            } else {
                current = temp;
            }
        }
    }

    return result;
}

// Function to create a new TreeNode
TreeNode* createNode(int val) {
    TreeNode* newNode = new TreeNode(val);
    return newNode;
}

int main() {
    TreeNode* root = createNode(1);
    root->left = createNode(2);
    root->right = createNode(3);
    root->left->left = createNode(4);
    root->left->right = createNode(5);
    root->right->left = createNode(6);
    root->right->right = createNode(7);

    vector<int> result = postorderTraversal(root);
    cout << "Postorder Traversal: ";
    for (int val : result) {
        cout << val << " ";
    }
    cout << endl;

    return 0;
}
```

This code implements the postorder traversal iteratively using a stack. We keep track of the previously visited node to handle cases where we need to backtrack from the right subtree.

Hope this helps! Let me know if you have further questions!

### 1. Algorithms & Data Structures (C++): Stack Span Problem

The "Stack Span Problem" is a classic problem in computer science and is commonly used to understand the concepts of stacks and arrays. The problem is usually formulated as follows:

Given an array of stock prices over a series of days, the task is to find the span of stock’s price for all the days. The span of the stock's price for a particular day is defined as the maximum number of consecutive days (including the current day) before the given day, for which the stock price is less than or equal to the price on the given day.

For example, consider the array `stockPrices[] = {100, 80, 60, 70, 60, 75, 85}`. The span values for corresponding days are `{1, 1, 1, 2, 1, 4, 6}`.

Here is a C++ implementation of the solution using stacks:

```cpp
#include <iostream>
#include <stack>
#include <vector>

using namespace std;

// Function to calculate stock span values
vector<int> calculateSpan(vector<int>& prices) {
    int n = prices.size();
    vector<int> span(n, 1); // Initializing span values with 1
    stack<int> st; // Stack to store indices of elements

    // Process first element separately
    st.push(0);

    // Span of first element is always 1
    span[0] = 1;

    // Calculate span values for rest of the elements
    for (int i = 1; i < n; i++) {
        // Pop elements from stack while stack is not empty and top
        // of stack is smaller than prices[i]
        while (!st.empty() && prices[st.top()] <= prices[i])
            st.pop();

        // If stack becomes empty, then price[i] is greater than all
        // elements to its left, hence span = i + 1
        span[i] = (st.empty()) ? (i + 1) : (i - st.top());

        // Push this element to stack
        st.push(i);
    }

    return span;
}

// Utility function to print elements of vector
void printVector(const vector<int>& vec) {
    for (int i : vec)
        cout << i << " ";
    cout << endl;
}

int main() {
    vector<int> stockPrices = {100, 80, 60, 70, 60, 75, 85};
    vector<int> span = calculateSpan(stockPrices);
    
    cout << "Stock Prices: ";
    printVector(stockPrices);
    cout << "Stock Span: ";
    printVector(span);
    
    return 0;
}
```

This code snippet demonstrates how to find the span of stock prices using a stack-based approach. The `calculateSpan` function calculates the span values for the given stock prices, and the `printVector` function is a utility to print the resulting span values.

### 1. Algorithms & Data Structures (C++): Stack Span Solution

In C++, you can implement the stack span problem using a stack data structure. The stack span problem is about finding the span of stock prices, i.e., for each day, finding the number of consecutive days prior to the current day where the stock price was less than or equal to the price of the current day.

Here's a C++ implementation of the stack span problem using a stack:

```cpp
#include <iostream>
#include <stack>
#include <vector>

using namespace std;

// Function to calculate stock span
vector<int> calculateSpan(vector<int>& prices) {
    int n = prices.size();
    vector<int> span(n, 1); // Span of the first day is always 1
    stack<int> st;
    st.push(0); // Push index of the first day into the stack

    for (int i = 1; i < n; i++) {
        // Pop elements from the stack while the current price is greater than or equal to the price at the top of the stack
        while (!st.empty() && prices[i] >= prices[st.top()]) {
            st.pop();
        }
        // If the stack becomes empty, then the current day is the greatest so far
        if (st.empty()) {
            span[i] = i + 1;
        } else {
            // Otherwise, the current day is the difference between the current index and the index of the top of the stack
            span[i] = i - st.top();
        }
        // Push the current index into the stack
        st.push(i);
    }

    return span;
}

// Function to print stock span
void printSpan(vector<int>& span) {
    cout << "Stock Span: ";
    for (int i = 0; i < span.size(); i++) {
        cout << span[i] << " ";
    }
    cout << endl;
}

int main() {
    vector<int> prices = {100, 80, 60, 70, 60, 75, 85};
    vector<int> span = calculateSpan(prices);
    printSpan(span);
    return 0;
}
```

This code calculates the span for each day's stock price and prints the result. You can replace the `prices` vector with your own data.

### 1. Algorithms & Data Structures (C++): Stack STL

In C++, the Standard Template Library (STL) provides a powerful implementation of data structures, including stacks. A stack is a Last-In-First-Out (LIFO) data structure, meaning that the last element added to the stack is the first one to be removed.

Here's a basic overview of how you can use the stack data structure in C++ using the STL:

### Including the necessary header

```cpp
#include <stack>
```

### Declaration

```cpp
std::stack<T> myStack;
```

Here, `T` is the type of elements you want to store in the stack.

### Basic Operations

1. **Push**: Adds an element to the top of the stack.

   ```cpp
   myStack.push(element);
   ```

2. **Pop**: Removes the top element from the stack.

   ```cpp
   myStack.pop();
   ```

3. **Top**: Returns a reference to the top element of the stack (without removing it).

   ```cpp
   T topElement = myStack.top();
   ```

4. **Size**: Returns the number of elements in the stack.

   ```cpp
   int size = myStack.size();
   ```

5. **Empty**: Checks if the stack is empty.

   ```cpp
   bool isEmpty = myStack.empty();
   ```

### Example Usage

```cpp
#include <iostream>
#include <stack>

int main() {
    std::stack<int> myStack;

    // Pushing elements onto the stack
    myStack.push(10);
    myStack.push(20);
    myStack.push(30);

    // Popping an element from the stack
    myStack.pop();

    // Accessing the top element
    std::cout << "Top element: " << myStack.top() << std::endl;

    // Checking the size of the stack
    std::cout << "Size of stack: " << myStack.size() << std::endl;

    // Checking if the stack is empty
    if (myStack.empty()) {
        std::cout << "Stack is empty" << std::endl;
    } else {
        std::cout << "Stack is not empty" << std::endl;
    }

    return 0;
}
```

This is a basic introduction to using the stack data structure provided by the C++ STL. It's a versatile tool for managing data in a Last-In-First-Out manner.

### 1. Algorithms & Data Structures (C++): Stack using 2 Queues

Sure, implementing a stack using two queues in C++ is a classic interview question. Here's how you can do it:

```cpp
#include <iostream>
#include <queue>

using namespace std;

class Stack {
private:
    queue<int> q1, q2;
    int top_element;

public:
    Stack() {}

    void push(int x) {
        // Push element to q2
        q2.push(x);
        // Set the top element
        top_element = x;

        // Move all elements from q1 to q2
        while (!q1.empty()) {
            q2.push(q1.front());
            top_element = q1.front();
            q1.pop();
        }

        // Swap q1 and q2
        swap(q1, q2);
    }

    void pop() {
        // Pop the top element
        q1.pop();
        // If q1 is not empty, update the top element
        if (!q1.empty())
            top_element = q1.front();
    }

    int top() {
        return top_element;
    }

    bool empty() {
        return q1.empty();
    }
};

int main() {
    Stack stack;
    stack.push(1);
    stack.push(2);
    stack.push(3);

    cout << "Top element: " << stack.top() << endl;
    stack.pop();
    cout << "Top element after pop: " << stack.top() << endl;

    return 0;
}
```

This implementation uses two queues, `q1` and `q2`. When pushing an element, it pushes the element to `q2`, then moves all elements from `q1` to `q2`, effectively making the newly pushed element on top. Finally, it swaps `q1` and `q2` so that `q1` always contains the elements in the stack.

Pop operation simply involves popping from `q1`, and updating the `top_element` accordingly.

This implementation has a time complexity of O(1) for push and O(n) for pop and top operations, where n is the number of elements in the stack.

### 1. Algorithms & Data Structures (C++): Stack using Array

Sure, I can provide you with a simple implementation of a stack using an array in C++:

```cpp
#include <iostream>
using namespace std;

#define MAX_SIZE 100

class Stack {
private:
    int arr[MAX_SIZE];
    int top;

public:
    Stack() {
        top = -1; // Initialize top to -1 indicating an empty stack
    }

    // Function to push an element onto the stack
    void push(int value) {
        if (top == MAX_SIZE - 1) {
            cout << "Stack Overflow! Cannot push element " << value << endl;
            return;
        }
        arr[++top] = value;
        cout << "Pushed " << value << " onto the stack." << endl;
    }

    // Function to pop an element from the stack
    int pop() {
        if (isEmpty()) {
            cout << "Stack Underflow! Cannot pop from an empty stack." << endl;
            return -1;
        }
        int poppedValue = arr[top--];
        cout << "Popped " << poppedValue << " from the stack." << endl;
        return poppedValue;
    }

    // Function to check if the stack is empty
    bool isEmpty() {
        return (top == -1);
    }

    // Function to return the top element of the stack without removing it
    int peek() {
        if (isEmpty()) {
            cout << "Stack is empty." << endl;
            return -1;
        }
        return arr[top];
    }
};

int main() {
    Stack myStack;

    myStack.push(10);
    myStack.push(20);
    myStack.push(30);

    cout << "Top element of the stack: " << myStack.peek() << endl;

    myStack.pop();
    myStack.pop();

    cout << "Top element of the stack after popping: " << myStack.peek() << endl;

    return 0;
}
```

This implementation uses an array to store the elements of the stack. The `push()` function adds elements to the top of the stack, the `pop()` function removes elements from the top of the stack, the `isEmpty()` function checks if the stack is empty, and the `peek()` function returns the top element of the stack without removing it.

### 1. Algorithms & Data Structures (C++): Stack using linked list

Certainly! Implementing a stack using a linked list in C++ involves creating a linked list where each node holds a data element and a pointer to the next node. Here's a basic implementation:

```cpp
#include <iostream>

template <typename T>
class Node {
public:
    T data;
    Node* next;
    
    Node(T value) : data(value), next(nullptr) {}
};

template <typename T>
class Stack {
private:
    Node<T>* top; // Points to the top element of the stack

public:
    Stack() : top(nullptr) {}

    ~Stack() {
        while (!isEmpty()) {
            pop();
        }
    }

    // Check if the stack is empty
    bool isEmpty() const {
        return top == nullptr;
    }

    // Push an element onto the stack
    void push(T value) {
        Node<T>* newNode = new Node<T>(value);
        newNode->next = top;
        top = newNode;
    }

    // Remove and return the top element of the stack
    T pop() {
        if (isEmpty()) {
            std::cerr << "Error: Stack is empty!" << std::endl;
            exit(EXIT_FAILURE);
        }
        Node<T>* temp = top;
        T data = temp->data;
        top = top->next;
        delete temp;
        return data;
    }

    // Return the top element of the stack without removing it
    T peek() const {
        if (isEmpty()) {
            std::cerr << "Error: Stack is empty!" << std::endl;
            exit(EXIT_FAILURE);
        }
        return top->data;
    }
};

int main() {
    Stack<int> stack;
    
    stack.push(1);
    stack.push(2);
    stack.push(3);
    
    std::cout << "Top element: " << stack.peek() << std::endl;
    
    std::cout << "Popping elements: ";
    while (!stack.isEmpty()) {
        std::cout << stack.pop() << " ";
    }
    std::cout << std::endl;
    
    return 0;
}
```

In this implementation:

- `Node` is a class representing a node in the linked list.
- `Stack` is a class representing a stack. It has member functions to push, pop, and peek at elements, as well as to check if the stack is empty.
- `push` adds an element to the top of the stack by creating a new node and updating the `top` pointer to point to this new node.
- `pop` removes the top element from the stack and returns its value. It also deallocates the memory for the removed node.
- `peek` returns the value of the top element without removing it.
- The `main` function demonstrates the usage of the stack by pushing elements onto it, peeking at the top element, and then popping elements off the stack.

### 1. Algorithms & Data Structures (C++): Stack Using Linked Lists

Sure, I can help you with that! Implementing a stack using linked lists is a common exercise in data structures and algorithms. Here's a simple implementation of a stack using a singly linked list in C++:

```cpp
#include <iostream>

using namespace std;

// Define the Node structure for the linked list
struct Node {
    int data;
    Node* next;
    Node(int value) : data(value), next(nullptr) {}
};

class Stack {
private:
    Node* top; // Pointer to the top of the stack

public:
    Stack() : top(nullptr) {}

    // Check if the stack is empty
    bool isEmpty() {
        return top == nullptr;
    }

    // Push an element onto the stack
    void push(int value) {
        Node* newNode = new Node(value);
        if (isEmpty()) {
            top = newNode;
        } else {
            newNode->next = top;
            top = newNode;
        }
    }

    // Pop an element from the stack
    int pop() {
        if (isEmpty()) {
            cout << "Stack Underflow: The stack is empty." << endl;
            return -1; // Return a default value indicating underflow
        } else {
            int poppedValue = top->data;
            Node* temp = top;
            top = top->next;
            delete temp;
            return poppedValue;
        }
    }

    // Peek at the top element of the stack
    int peek() {
        if (isEmpty()) {
            cout << "Stack is empty." << endl;
            return -1; // Return a default value indicating underflow
        } else {
            return top->data;
        }
    }

    // Display the stack
    void display() {
        if (isEmpty()) {
            cout << "Stack is empty." << endl;
        } else {
            Node* current = top;
            cout << "Stack: ";
            while (current != nullptr) {
                cout << current->data << " ";
                current = current->next;
            }
            cout << endl;
        }
    }

    // Destructor to deallocate memory
    ~Stack() {
        while (!isEmpty()) {
            pop();
        }
    }
};

int main() {
    Stack stack;
    stack.push(5);
    stack.push(10);
    stack.push(15);
    stack.display(); // Output: Stack: 15 10 5
    cout << "Popped: " << stack.pop() << endl; // Output: Popped: 15
    cout << "Top: " << stack.peek() << endl;   // Output: Top: 10
    stack.display(); // Output: Stack: 10 5
    return 0;
}
```

This code defines a `Stack` class that uses a singly linked list internally to implement the stack operations `push`, `pop`, `peek`, and `isEmpty`. The `Node` struct represents each element in the linked list.

### 1. Algorithms & Data Structures (C++): Stack using Linked Representation

Sure, implementing a stack using linked representation in C++ is a fundamental exercise in data structures. Here's a simple implementation:

```cpp
#include <iostream>

// Define a node structure for the linked list
struct Node {
    int data;
    Node* next;
    
    // Constructor to initialize node
    Node(int value) : data(value), next(nullptr) {}
};

// Define a Stack class
class Stack {
private:
    Node* top; // Pointer to the top element of the stack

public:
    // Constructor
    Stack() : top(nullptr) {}

    // Destructor to deallocate memory
    ~Stack() {
        while (!isEmpty()) {
            pop();
        }
    }

    // Function to check if the stack is empty
    bool isEmpty() {
        return top == nullptr;
    }

    // Function to push an element onto the stack
    void push(int value) {
        Node* newNode = new Node(value);
        newNode->next = top;
        top = newNode;
    }

    // Function to pop an element from the stack
    void pop() {
        if (isEmpty()) {
            std::cout << "Stack Underflow: The stack is empty\n";
            return;
        }
        Node* temp = top;
        top = top->next;
        delete temp;
    }

    // Function to return the top element of the stack
    int peek() {
        if (isEmpty()) {
            std::cout << "Stack is empty\n";
            return -1; // Return a default value indicating stack is empty
        }
        return top->data;
    }
};

int main() {
    // Create a stack object
    Stack stack;

    // Push elements onto the stack
    stack.push(5);
    stack.push(10);
    stack.push(15);

    // Print the top element
    std::cout << "Top element: " << stack.peek() << std::endl;

    // Pop an element
    stack.pop();

    // Print the top element again
    std::cout << "Top element after popping: " << stack.peek() << std::endl;

    return 0;
}
```

This code demonstrates the basic operations of a stack using a linked list representation. It includes `push`, `pop`, `peek`, and `isEmpty` functions. The stack is implemented using a singly linked list where each node points to the next node, and the `top` pointer always points to the top element of the stack.

### 1. Algorithms & Data Structures (C++): Stack using LL

Sure! Here's an implementation of a stack using a linked list in C++:

```cpp
#include <iostream>

// Node class for the linked list
class Node {
public:
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

// Stack class using linked list
class Stack {
private:
    Node* top;

public:
    Stack() : top(nullptr) {}

    // Check if the stack is empty
    bool isEmpty() {
        return top == nullptr;
    }

    // Push an element onto the stack
    void push(int val) {
        Node* newNode = new Node(val);
        newNode->next = top;
        top = newNode;
        std::cout << val << " pushed to stack\n";
    }

    // Pop an element from the stack
    int pop() {
        if (isEmpty()) {
            std::cout << "Stack underflow\n";
            return INT_MIN; // Return minimum integer value to indicate underflow
        }
        int poppedValue = top->data;
        Node* temp = top;
        top = top->next;
        delete temp;
        return poppedValue;
    }

    // Return the top element of the stack without popping it
    int peek() {
        if (isEmpty()) {
            std::cout << "Stack is empty\n";
            return INT_MIN; // Return minimum integer value to indicate underflow
        }
        return top->data;
    }
};

int main() {
    Stack stack;
    stack.push(10);
    stack.push(20);
    stack.push(30);

    std::cout << "Top element is: " << stack.peek() << std::endl;

    std::cout << stack.pop() << " popped from stack\n";
    std::cout << stack.pop() << " popped from stack\n";

    std::cout << "Top element is: " << stack.peek() << std::endl;

    stack.push(40);
    std::cout << "Top element is: " << stack.peek() << std::endl;

    return 0;
}
```

In this implementation:

- The `Node` class represents a single node in the linked list, containing an integer data value and a pointer to the next node.
- The `Stack` class uses a pointer to the top node of the linked list.
- `push()` adds a new node to the top of the stack.
- `pop()` removes the top node from the stack and returns its value.
- `peek()` returns the value of the top node without removing it from the stack.
- `isEmpty()` checks if the stack is empty.

### 1. Algorithms & Data Structures (C++): Stack using Templates

Sure, here's an example of implementing a stack data structure using templates in C++:

```cpp
#include <iostream>
#include <vector>

template <typename T>
class Stack {
private:
    std::vector<T> elements;

public:
    // Push element onto the stack
    void push(const T& element) {
        elements.push_back(element);
    }

    // Remove and return the top element from the stack
    T pop() {
        if (elements.empty()) {
            throw std::out_of_range("Stack

is empty, cannot pop element");
        }
        T topElement = elements.back();
        elements.pop_back();
        return topElement;
    }

    // Return the top element of the stack without removing it
    T top() const {
        if (elements.empty()) {
            throw std::out_of_range("Stack is empty, cannot retrieve top element");
        }
        return elements.back();
    }

    // Check if the stack is empty
    bool empty() const {
        return elements.empty();
    }

    // Return the number of elements in the stack
    size_t size() const {
        return elements.size();
    }
};

int main() {
    // Example usage of the Stack class
    Stack<int> intStack;

    intStack.push(5);
    intStack.push(10);
    intStack.push(15);

    std::cout << "Size of stack: " << intStack.size() << std::endl;
    std::cout << "Top element: " << intStack.top() << std::endl;

    intStack.pop();
    std::cout << "Size of stack after pop: " << intStack.size() << std::endl;
    std::cout << "Top element after pop: " << intStack.top() << std::endl;

    return 0;
}
```

This code defines a generic `Stack` class using templates, allowing it to work with any data type. It uses a `std::vector` internally to store the elements of the stack. The class provides methods to push elements onto the stack, pop elements from the stack, access the top element without removing it, check if the stack is empty, and get the size of the stack.

### 1. Algorithms & Data Structures (C++): Stack using Vector

Sure, here's a basic implementation of a stack using a vector in C++:

```cpp
#include <iostream>
#include <vector>

template<typename T>
class Stack {
private:
    std::vector<T> elements;

public:
    // Push element onto the stack
    void push(const T& element) {
        elements.push_back(element);
    }

    // Remove and return the top element from the stack
    T pop() {
        if (elements.empty()) {
            throw std::out_of_range("Stack

empty, cannot pop");
        }
        T element = elements.back();
        elements.pop_back();
        return element;
    }

    // Return the top element from the stack without removing it
    T& top() {
        if (elements.empty()) {
            throw std::out_of_range("Stack empty, cannot retrieve top");
        }
        return elements.back();
    }

    // Check if the stack is empty
    bool empty() const {
        return elements.empty();
    }

    // Return the number of elements in the stack
    size_t size() const {
        return elements.size();
    }
};

int main() {
    Stack<int> stack;

    // Push elements onto the stack
    stack.push(10);
    stack.push(20);
    stack.push(30);

    // Print the top element
    std::cout << "Top element: " << stack.top() << std::endl;

    // Pop elements from the stack
    std::cout << "Popping elements: ";
    while (!stack.empty()) {
        std::cout << stack.pop() << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

This implementation uses the `std::vector` container to store the elements of the stack. The `push` function adds an element to the end of the vector, simulating pushing onto the stack. The `pop` function removes and returns the last element of the vector, simulating popping from the stack. The `top` function returns the last element of the vector without removing it. The `empty` function checks if the vector is empty, and the `size` function returns the number of elements in the vector.

### 1. Algorithms & Data Structures (C++): Stack vs Heap Memory

In C++, stack and heap are two areas of memory where objects can be stored, each with its own characteristics and use cases.

1. **Stack Memory:**
   - Stack memory is a region of memory that operates in a Last-In-First-Out (LIFO) manner.
   - It's used for storing local variables and function call information.
   - When a function is called, its local variables are pushed onto the stack, and when the function exits, those variables are popped off the stack.
   - Stack memory allocation and deallocation are handled automatically by the compiler.
   - Stack memory is limited and typically smaller in size compared to heap memory.
   - Accessing data on the stack is faster than accessing data on the heap because stack allocation and deallocation are simple pointer manipulations.
   - However, stack memory is limited in size, and allocating large objects or allocating too many objects on the stack can lead to stack overflow errors.

2. **Heap Memory:**
   - Heap memory is a region of memory that operates in a less organized manner, and it's typically larger than the stack.
   - It's used for dynamic memory allocation, where objects are allocated and deallocated explicitly by the programmer.
   - Memory on the heap is not automatically deallocated when a function exits, so it's the programmer's responsibility to manage memory allocation and deallocation to avoid memory leaks.
   - Accessing data on the heap is slightly slower than accessing data on the stack because it involves more complex memory management.
   - Heap memory is not limited in size by the compiler, but the available memory is determined by the operating system and hardware.
   - The flexibility of heap memory allows for dynamic allocation of objects whose size or lifetime is not known at compile time.

In summary, stack memory is used for static memory allocation with a well-defined lifetime, such as local variables, while heap memory is used for dynamic memory allocation with a less predictable lifetime, such as objects created with `new` and `delete` or `malloc` and `free` functions. Understanding the differences between stack and heap memory and when to use each is crucial for writing efficient and bug-free C++ programs.

### 1. Algorithms & Data Structures (C++): Stack with Two Queues

Implementing a stack using two queues is an interesting exercise. The basic idea is to simulate the behavior of a stack using two queues. One queue will serve as the primary storage for the elements, while the other will be used for temporary storage during operations like pushing and popping. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <queue>

using namespace std;

class Stack {
private:
    queue<int> q1;
    queue<int> q2;

public:
    void push(int val) {
        // Add the new element to q2
        q2.push(val);

        // Move all elements from q1 to q2
        while (!q1.empty()) {
            q2.push(q1.front());
            q1.pop();
        }

        // Swap q1 and q2
        swap(q1, q2);
    }

    void pop() {
        if (empty()) {
            cout << "Stack underflow!" << endl;
            return;
        }
        // Pop the top element from q1
        q1.pop();
    }

    int top() {
        if (empty()) {
            cout << "Stack is empty!" << endl;
            return -1;
        }
        // Return the front element of q1
        return q1.front();
    }

    bool empty() {
        // Check if q1 is empty
        return q1.empty();
    }
};

int main() {
    Stack s;

    s.push(1);
    s.push(2);
    s.push(3);

    cout << "Top element: " << s.top() << endl;
    s.pop();
    cout << "Top element after pop: " << s.top() << endl;

    return 0;
}
```

In this implementation:

- `q1` is the primary queue where elements are stored as a stack.
- `q2` is a temporary queue used during `push` operation.

Here's what happens during `push`:

1. The new element is pushed into `q2`.
2. All elements from `q1` are moved to `q2`.
3. The elements are reversed in `q2` after the new element is added.
4. `q1` and `q2` are swapped so that `q1` always contains the stack elements.

This implementation ensures that the top element of the stack is always at the front of `q1`, making the `top` and `pop` operations efficient (O(1) time complexity).

### 1. Algorithms & Data Structures (C++): Stack: Algorithm to Check for Balanced Paranthesis

To check if a given expression has balanced parentheses using a stack, you can follow these steps:

1. Iterate through each character in the expression.
2. If the character is an opening parenthesis (i.e., '(', '{', or '['), push it onto the stack.
3. If the character is a closing parenthesis (i.e., ')', '}', or ']'), pop the top element from the stack.
   - If the stack is empty, return false because there is no corresponding opening parenthesis.
   - If the popped element does not match the current closing parenthesis, return false.
4. After iterating through all characters, if the stack is empty, return true (indicating balanced parentheses); otherwise, return false.

Here's how you can implement this algorithm in C++:

```cpp
#include <iostream>
#include <stack>
#include <string>

bool isBalanced(const std::string& expression) {
    std::stack<char> st;
    for (char ch : expression) {
        if (ch == '(' || ch == '{' || ch == '[') {
            st.push(ch);
        } else if (ch == ')' || ch == '}' || ch == ']') {
            if (st.empty()) {
                return false;
            }
            char top = st.top();
            st.pop();
            if ((ch == ')' && top != '(') ||
                (ch == '}' && top != '{') ||
                (ch == ']' && top != '[')) {
                return false;
            }
        }
    }
    return st.empty();
}

int main() {
    std::string expression;
    std::cout << "Enter an expression: ";
    std::cin >> expression;

    if (isBalanced(expression)) {
        std::cout << "The expression has balanced parentheses.\n";
    } else {
        std::cout << "The expression does not have balanced parentheses.\n";
    }

    return 0;
}
```

This code reads an expression from the user and checks if it has balanced parentheses using the `isBalanced` function.

### 1. Algorithms & Data Structures (C++): Stack: Constructor

In C++, a stack can be implemented using various data structures like arrays, linked lists, or the STL container `std::stack`. Let's start with a simple implementation of a stack using an array. Below is the constructor for a stack class in C++:

```cpp
#include <iostream>

const int MAX_SIZE = 100; // Maximum size of the stack

class Stack {
private:
    int top;            // Index of the top element
    int capacity;       // Maximum capacity of the stack
    int* elements;      // Array to store stack elements

public:
    // Constructor to initialize an empty stack
    Stack(int size = MAX_SIZE) {
        capacity = size;
        elements = new int[capacity];
        top = -1;       // Initialize top as -1 to indicate an empty stack
    }

    // Destructor to free dynamically allocated memory
    ~Stack() {
        delete[] elements;
    }

    // Other member functions for stack operations (push, pop, peek, etc.) would be defined here
};

int main() {
    Stack myStack(10); // Create a stack with a capacity of 10
    // You can now perform stack operations on 'myStack'
    return 0;
}
```

In this code:

- The `Stack` class encapsulates the functionality of a stack.
- The constructor `Stack(int size = MAX_SIZE)` initializes an empty stack. It takes an optional parameter `size` to specify the maximum capacity of the stack. If no size is provided, it defaults to `MAX_SIZE`.
- Inside the constructor, dynamic memory allocation is done using `new` to allocate memory for the stack elements. The size of the array is determined by the `capacity`.
- The `top` variable is initialized to `-1` to indicate an empty stack.
- The destructor `~Stack()` is responsible for deallocating the dynamically allocated memory.

Remember to handle stack overflow scenarios when pushing elements onto the stack, and stack underflow scenarios when popping elements from the stack. These checks should be implemented in other member functions of the `Stack` class.

### 1. Algorithms & Data Structures (C++): Stack: Converting an Infix Expression to postfix Expression

Converting an infix expression to a postfix expression is a classic problem in computer science. The postfix notation, also known as Reverse Polish Notation (RPN), has operators placed after their operands. This makes it easier to evaluate expressions using a stack-based algorithm.

Here's how you can implement a C++ function to convert an infix expression to a postfix expression using a stack:

```cpp
#include <iostream>
#include <stack>
#include <string>
#include <unordered_map>

using namespace std;

// Function to check if a character is an operator
bool isOperator(char ch) {
    return (ch == '+' || ch == '-' || ch == '*' || ch == '/');
}

// Function to get the precedence of an operator
int precedence(char op) {
    if (op == '+' || op == '-') return 1;
    if (op == '*' || op == '/') return 2;
    return 0;
}

string infixToPostfix(const string& infix) {
    stack<char> operators;
    string postfix;
    unordered_map<char, int> precedenceMap;

    for (char ch : infix) {
        if (ch == ' ') continue; // Ignore spaces
        if (isalnum(ch)) {
            postfix += ch; // Append operands to the postfix expression
        } else if (ch == '(') {
            operators.push(ch); // Push opening parenthesis onto the stack
        } else if (ch == ')') {
            // Pop operators from the stack and append them to postfix until '(' is encountered
            while (!operators.empty() && operators.top() != '(') {
                postfix += operators.top();
                operators.pop();
            }
            // Pop the '(' from the stack
            operators.pop();
        } else if (isOperator(ch)) {
            // Pop operators with higher or equal precedence from the stack
            while (!operators.empty() && precedence(operators.top()) >= precedence(ch)) {
                postfix += operators.top();
                operators.pop();
            }
            // Push the current operator onto the stack
            operators.push(ch);
        }
    }

    // Append remaining operators to the postfix expression
    while (!operators.empty()) {
        postfix += operators.top();
        operators.pop();
    }

    return postfix;
}

int main() {
    string infix = "a + b * (c - d) / e";
    cout << "Infix expression: " << infix << endl;
    cout << "Postfix expression: " << infixToPostfix(infix) << endl;
    return 0;
}
```

This code snippet should give you a good starting point for converting infix expressions to postfix expressions in C++. Make sure to test it with different infix expressions to verify its correctness.

### 1. Algorithms & Data Structures (C++): Stack: Decimal to binary conversion

Sure, here's a simple C++ code to convert a decimal number to binary using a stack:

```cpp
#include <iostream>
#include <stack>
using namespace std;

// Function to convert decimal to binary
void decimalToBinary(int decimal) {
    stack<int> binaryStack;

    // Convert decimal to binary
    while (decimal > 0) {
        int remainder = decimal % 2;
        binaryStack.push(remainder);
        decimal /= 2;
    }

    // Print binary representation
    cout << "Binary representation: ";
    while (!binaryStack.empty()) {
        cout << binaryStack.top();
        binaryStack.pop();
    }
}

int main() {
    int decimal;

    // Input decimal number
    cout << "Enter a decimal number: ";
    cin >> decimal;

    // Convert decimal to binary
    decimalToBinary(decimal);

    return 0;
}
```

In this code:

1. We include necessary headers such as `<iostream>` for input-output operations and `<stack>` for using the stack data structure.
2. We define a function `decimalToBinary` that takes an integer decimal number as input and converts it to binary using a stack. Inside the function, we repeatedly divide the decimal number by 2 and push the remainders onto the stack until the decimal number becomes 0.
3. We then print the binary representation by popping elements from the stack one by one.
4. In the `main` function, we take the decimal number as input from the user, call the `decimalToBinary` function, and print the binary representation.

This code takes a decimal number as input and prints its binary representation.

### 1. Algorithms & Data Structures (C++): Stack: Duplicate Parentheses

Duplicate parentheses in an expression occur when there are redundant parentheses present. For example, "((a + b))" has duplicate parentheses because the inner parentheses "()" are redundant. In algorithms and data structures, detecting duplicate parentheses in an expression is a common problem, often tackled using a stack data structure. Here's how you might implement an algorithm in C++ to detect duplicate parentheses using a stack:

```cpp
#include <iostream>
#include <stack>
#include <string>

bool hasDuplicateParentheses(const std::string& expression) {
    std::stack<char> parenthesisStack;

    for (char c : expression) {
        if (c == '(') {
            parenthesisStack.push(c);
        } else if (c == ')') {
            // If the top of stack is '(', then duplicate parentheses detected
            if (!parenthesisStack.empty() && parenthesisStack.top() == '(') {
                return true;
            }

            // Pop all characters until matching '(' is found
            while (!parenthesisStack.empty() && parenthesisStack.top() != '(') {
                parenthesisStack.pop();
            }

            // Pop the '(' itself
            if (!parenthesisStack.empty()) {
                parenthesisStack.pop();
            } else {
                // If '(' not found, there are extra ')' which is invalid
                return true;
            }
        }
    }

    // If stack is not empty at the end, then there are extra '('
    return !parenthesisStack.empty();
}

int main() {
    std::string expression = "((a + b))";
    
    if (hasDuplicateParentheses(expression)) {
        std::cout << "Expression has duplicate parentheses\n";
    } else {
        std::cout << "Expression does not have duplicate parentheses\n";
    }

    return 0;
}
```

This code defines a function `hasDuplicateParentheses` that takes a string expression as input and returns true if duplicate parentheses are found, and false otherwise. The function iterates through the expression character by character. When it encounters an opening parenthesis '(', it pushes it onto the stack. When it encounters a closing parenthesis ')', it checks if the top of the stack contains an opening parenthesis '('. If it does, it indicates duplicate parentheses. Otherwise, it pops characters from the stack until it finds the matching opening parenthesis '('. If no opening parenthesis is found, it indicates extra closing parentheses ')' which is also invalid. At the end of the iteration, if the stack is not empty, it indicates extra opening parentheses '(' which is invalid.

### 1. Algorithms & Data Structures (C++): Stack: Evaluating a Postfix Expression

Evaluating a postfix expression using a stack is a classic problem in computer science. Postfix notation, also known as Reverse Polish Notation (RPN), is a mathematical notation in which every operator follows all of its operands. This makes it easier to evaluate using a stack. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <stack>
#include <string>

using namespace std;

bool isOperator(char c) {
    return c == '+' || c == '-' || c == '*' || c == '/';
}

int performOperation(char operation, int operand1, int operand2) {
    switch (operation) {
        case '+':
            return operand1 + operand2;
        case '-':
            return operand1 - operand2;
        case '*':
            return operand1 * operand2;
        case '/':
            return operand1 / operand2;
        default:
            return 0; // Handle invalid operation
    }
}

int evaluatePostfix(const string& expression) {
    stack<int> operandStack;

    for (char c : expression) {
        if (isdigit(c)) {
            operandStack.push(c - '0'); // Convert char to integer
        } else if (isOperator(c)) {
            int operand2 = operandStack.top();
            operandStack.pop();
            int operand1 = operandStack.top();
            operandStack.pop();
            int result = performOperation(c, operand1, operand2);
            operandStack.push(result);
        }
    }

    return operandStack.top();
}

int main() {
    string postfixExpression = "62/3-42*+";
    cout << "Postfix Expression: " << postfixExpression << endl;
    int result = evaluatePostfix(postfixExpression);
    cout << "Result: " << result << endl;

    return 0;
}
```

In this code:

- The `evaluatePostfix` function takes a postfix expression as input and returns the result after evaluating it.
- We iterate through each character of the expression.
- If the character is a digit, we push it onto the stack.
- If the character is an operator, we pop the top two elements from the stack, perform the operation, and push the result back onto the stack.
- Finally, we return the result left on the stack, which is the final result of the expression.

You can modify the `main` function to input different postfix expressions and test the implementation.

### 1. Algorithms & Data Structures (C++): Stack: Implement Stack Using a List

Sure, here's an implementation of a stack using a linked list in C++:

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
class Stack {
private:
    Node<T>* top;

public:
    Stack() : top(nullptr) {}

    ~Stack() {
        while (!isEmpty()) {
            pop();
        }
    }

    void push(T data) {
        Node<T>* newNode = new Node<T>(data);
        newNode->next = top;
        top = newNode;
    }

    void pop() {
        if (isEmpty()) {
            std::cout << "Stack underflow\n";
            return;
        }
        Node<T>* temp = top;
        top = top->next;
        delete temp;
    }

    T peek() const {
        if (isEmpty()) {
            std::cout << "Stack is empty\n";
            exit(1);
        }
        return top->data;
    }

    bool isEmpty() const {
        return top == nullptr;
    }
};

int main() {
    Stack<int> stack;
    stack.push(1);
    stack.push(2);
    stack.push(3);

    std::cout << "Top element: " << stack.peek() << std::endl;

    stack.pop();
    stack.pop();

    std::cout << "Top element after popping: " << stack.peek() << std::endl;

    return 0;
}
```

This implementation uses a linked list to store the elements of the stack. The `push()` function adds an element to the top of the stack, the `pop()` function removes the top element, and the `peek()` function returns the top element without removing it.

### 1. Algorithms & Data Structures (C++): Stack: Implementing Parenthesis Matching

Certainly! Implementing parenthesis matching using a stack in C++ is a classic problem. Here's how you can do it:

```cpp
#include <iostream>
#include <stack>
#include <string>

bool isMatchingPair(char opening, char closing) {
    return (opening == '(' && closing == ')') ||
           (opening == '{' && closing == '}') ||
           (opening == '[' && closing == ']');
}

bool isBalanced(const std::string &expression) {
    std::stack<char> s;
    for (char bracket : expression) {
        if (bracket == '(' || bracket == '{' || bracket == '[') {
            // Push opening brackets onto the stack
            s.push(bracket);
        } else if (bracket == ')' || bracket == '}' || bracket == ']') {
            // If a closing bracket is encountered
            if (s.empty() || !isMatchingPair(s.top(), bracket)) {
                return false; // Unmatched closing bracket
            } else {
                s.pop(); // Matching pair found, pop from stack
            }
        }
    }
    // If the stack is empty, all brackets are matched
    return s.empty();
}

int main() {
    std::string expression;
    std::cout << "Enter an expression: ";
    std::cin >> expression;

    if (isBalanced(expression)) {
        std::cout << "The expression is balanced." << std::endl;
    } else {
        std::cout << "The expression is not balanced." << std::endl;
    }

    return 0;
}
```

This code defines a function `isBalanced` that takes a string representing an expression and checks whether the parentheses in the expression are balanced or not using a stack. The `isMatchingPair` function checks whether two parentheses characters form a valid pair.

In the `main` function, it reads an expression from the user and prints whether the expression is balanced or not.

### 1. Algorithms & Data Structures (C++): Stack: Implementing Postfix Evaluation

Implementing postfix evaluation using a stack in C++ is a great exercise for understanding both stacks and postfix notation. Here's a basic implementation:

```cpp
#include <iostream>
#include <stack>
#include <string>
#include <cctype>

using namespace std;

// Function to evaluate postfix expression
int evaluatePostfix(const string& exp) {
    stack<int> stk;

    // Traverse through every character of input expression
    for (char ch : exp) {
        // If the character is an operand, push it onto the stack
        if (isdigit(ch)) {
            stk.push(ch - '0'); // Convert char to int
        }
        // If the character is an operator
        else {
            // Pop two operands from stack
            int operand2 = stk.top();
            stk.pop();
            int operand1 = stk.top();
            stk.pop();

            // Perform operation based on operator
            switch (ch) {
                case '+': stk.push(operand1 + operand2); break;
                case '-': stk.push(operand1 - operand2); break;
                case '*': stk.push(operand1 * operand2); break;
                case '/': stk.push(operand1 / operand2); break;
                default:  throw runtime_error("Invalid operator");
            }
        }
    }
    // Result will be at the top of the stack
    return stk.top();
}

int main() {
    string exp = "231*+9-"; // Example postfix expression: 2*3+1-9
    cout << "Postfix expression evaluation result: " << evaluatePostfix(exp) << endl;
    return 0;
}
```

In this implementation:

- We use a stack to store operands.
- We traverse the postfix expression from left to right.
- If we encounter an operand, we push it onto the stack.
- If we encounter an operator, we pop the top two operands from the stack, perform the operation, and push the result back onto the stack.
- Finally, the result will be at the top of the stack after evaluating the entire expression.

### 1. Algorithms & Data Structures (C++): Stack: Infix Expression

Certainly! A stack can be used to evaluate infix expressions, which are mathematical expressions where operators are placed between operands. To evaluate an infix expression, you typically convert it to postfix (or prefix) notation and then evaluate it using a stack. However, you can also directly evaluate infix expressions using a stack.

Here's a basic implementation of evaluating an infix expression using a stack in C++:

```cpp
#include <iostream>
#include <stack>
#include <string>
#include <cmath> // for pow() function

using namespace std;

// Function to check if a character is an operator
bool isOperator(char c) {
    return (c == '+' || c == '-' || c == '*' || c == '/' || c == '^');
}

// Function to perform arithmetic operations
int performOperation(char operation, int operand1, int operand2) {
    switch(operation) {
        case '+': return operand1 + operand2;
        case '-': return operand1 - operand2;
        case '*': return operand1 * operand2;
        case '/': return operand1 / operand2;
        case '^': return pow(operand1, operand2);
        default: return 0;
    }
}

// Function to evaluate infix expression
int evaluateInfix(string expression) {
    stack<int> operandStack;
    stack<char> operatorStack;

    for (int i = 0; i < expression.length(); i++) {
        if (expression[i] == ' ') continue; // Skip whitespace

        if (isdigit(expression[i])) {
            // Extract the operand
            int operand = 0;
            while (i < expression.length() && isdigit(expression[i])) {
                operand = operand * 10 + (expression[i] - '0');
                i++;
            }
            i--; // Move back one character
            operandStack.push(operand);
        } else if (expression[i] == '(') {
            operatorStack.push(expression[i]);
        } else if (expression[i] == ')') {
            while (!operatorStack.empty() && operatorStack.top() != '(') {
                int operand2 = operandStack.top();
                operandStack.pop();

                int operand1 = operandStack.top();
                operandStack.pop();

                char operation = operatorStack.top();
                operatorStack.pop();

                operandStack.push(performOperation(operation, operand1, operand2));
            }
            operatorStack.pop(); // Pop '('
        } else if (isOperator(expression[i])) {
            while (!operatorStack.empty() && operatorStack.top() != '(' &&
                   ((expression[i] != '^' && expression[i] != '*' && expression[i] != '/') ||
                    (expression[i] == '^' && (operatorStack.top() == '*' || operatorStack.top() == '/')) ||
                    (expression[i] == '*' && operatorStack.top() == '/') || 
                    (expression[i] != '^' && expression[i] != '*' && expression[i] != '/' && 
                     operatorStack.top() != '^'))) {
                int operand2 = operandStack.top();
                operandStack.pop();

                int operand1 = operandStack.top();
                operandStack.pop();

                char operation = operatorStack.top();
                operatorStack.pop();

                operandStack.push(performOperation(operation, operand1, operand2));
            }
            operatorStack.push(expression[i]);
        }
    }

    // Process remaining operators in the stack
    while (!operatorStack.empty()) {
        int operand2 = operandStack.top();
        operandStack.pop();

        int operand1 = operandStack.top();
        operandStack.pop();

        char operation = operatorStack.top();
        operatorStack.pop();

        operandStack.push(performOperation(operation, operand1, operand2));
    }

    // Result will be at the top of the operand stack
    return operandStack.top();
}

int main() {
    string expression;
    cout << "Enter an infix expression: ";
    getline(cin, expression);

    int result = evaluateInfix(expression);
    cout << "Result: " << result << endl;

    return 0;
}
```

This code evaluates infix expressions containing the operators `+`, `-`, `*`, `/`, and `^` (exponentiation). It also handles parentheses correctly. You can input an infix expression, and it will output the result after evaluating it.

### 1. Algorithms & Data Structures (C++): Stack: Infix Expression to Postfix/Prefix Expression Conversion

Sure, let's start with converting an infix expression to a postfix expression using the stack data structure in C++.

Here's the step-by-step process:

1. Initialize an empty stack to store operators.
2. Scan the infix expression from left to right.
3. If the scanned character is an operand, output it.
4. If the scanned character is an operator and the stack is empty, push it onto the stack.
5. If the scanned character is an operator and the stack is not empty, compare the precedence of the scanned operator with the operator at the top of the stack. If the precedence of the scanned operator is higher, push it onto the stack. If the precedence is lower, pop operators from the stack and output them until a lower precedence operator is encountered, then push the scanned operator onto the stack.
6. If the scanned character is a left parenthesis, push it onto the stack.
7. If the scanned character is a right parenthesis, pop operators from the stack and output them until a left parenthesis is encountered. Pop and discard the left parenthesis from the stack.
8. Repeat steps 3-7 until all characters are scanned.
9. Pop and output all operators from the stack.

Here's a C++ implementation of the algorithm:

```cpp
#include <iostream>
#include <stack>
#include <string>

using namespace std;

int precedence(char op) {
    if (op == '+' || op == '-')
        return 1;
    if (op == '*' || op == '/')
        return 2;
    return 0;
}

string infixToPostfix(string infix) {
    stack<char> s;
    string postfix;

    for (char& c : infix) {
        if (isalnum(c)) {
            postfix += c;
        } else if (c == '(') {
            s.push(c);
        } else if (c == ')') {
            while (!s.empty() && s.top() != '(') {
                postfix += s.top();
                s.pop();
            }
            s.pop(); // Discard '('
        } else {
            while (!s.empty() && precedence(c) <= precedence(s.top())) {
                postfix += s.top();
                s.pop();
            }
            s.push(c);
        }
    }

    while (!s.empty()) {
        postfix += s.top();
        s.pop();
    }

    return postfix;
}

int main() {
    string infix_expression = "a+b*c-(d/e+f*g*h)";
    cout << "Infix Expression: " << infix_expression << endl;
    cout << "Postfix Expression: " << infixToPostfix(infix_expression) << endl;
    return 0;
}
```

This code will convert the infix expression `"a+b*c-(d/e+f*g*h)"` to its postfix equivalent. You can replace this expression with any other infix expression you want to convert.

### 1. Algorithms & Data Structures (C++): Stack: Infix to Postfix Conversion and Evaluation

Sure, I can provide you with a basic implementation of infix to postfix conversion and evaluation using stacks in C++. Here's how you can do it:

```cpp
#include <iostream>
#include <stack>
#include <string>
#include <cctype> // for isdigit()

using namespace std;

// Function to return precedence of operators
int precedence(char op) {
    if(op == '+' || op == '-')
        return 1;
    if(op == '*' || op == '/')
        return 2;
    return 0;
}

// Function to perform arithmetic operations
int applyOp(int a, int b, char op) {
    switch(op) {
        case '+': return a + b;
        case '-': return a - b;
        case '*': return a * b;
        case '/': return a / b;
    }
    return 0;
}

// Function to convert infix expression to postfix
string infixToPostfix(string exp) {
    string postfix = "";
    stack<char> operators;

    for (char c : exp) {
        if (isspace(c))
            continue;
        if (isdigit(c)) {
            postfix += c;
        } else if (c == '(') {
            operators.push(c);
        } else if (c == ')') {
            while (!operators.empty() && operators.top() != '(') {
                postfix += operators.top();
                operators.pop();
            }
            operators.pop(); // Pop '('
        } else {
            while (!operators.empty() && precedence(operators.top()) >= precedence(c)) {
                postfix += operators.top();
                operators.pop();
            }
            operators.push(c);
        }
    }

    while (!operators.empty()) {
        postfix += operators.top();
        operators.pop();
    }

    return postfix;
}

// Function to evaluate postfix expression
int evaluatePostfix(string exp) {
    stack<int> operands;

    for (char c : exp) {
        if (isdigit(c)) {
            operands.push(c - '0');
        } else {
            int operand2 = operands.top();
            operands.pop();
            int operand1 = operands.top();
            operands.pop();
            int result = applyOp(operand1, operand2, c);
            operands.push(result);
        }
    }

    return operands.top();
}

int main() {
    string infix_exp = "5 + (3 * 2) - 8 / 4"; // Example infix expression
    string postfix_exp = infixToPostfix(infix_exp);

    cout << "Postfix expression: " << postfix_exp << endl;
    
    int result = evaluatePostfix(postfix_exp);
    cout << "Result: " << result << endl;

    return 0;
}
```

This code first converts the infix expression to postfix using the shunting-yard algorithm, and then evaluates the postfix expression using a stack. You can replace the example infix expression with your own expression.

### 1. Algorithms & Data Structures (C++): Stack: Maximum Rectangular Area in Histogram

To find the maximum rectangular area in a histogram, you can use a stack-based algorithm. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <stack>
#include <vector>

using namespace std;

int maxRectangularArea(vector<int>& heights) {
    stack<int> s;
    int maxArea = 0;
    int i = 0;
    while (i < heights.size()) {
        if (s.empty() || heights[i] >= heights[s.top()]) {
            s.push(i);
            i++;
        } else {
            int topHeightIndex = s.top();
            s.pop();
            int width = s.empty() ? i : i - s.top() - 1;
            int area = heights[topHeightIndex] * width;
            maxArea = max(maxArea, area);
        }
    }
    while (!s.empty()) {
        int topHeightIndex = s.top();
        s.pop();
        int width = s.empty() ? i : i - s.top() - 1;
        int area = heights[topHeightIndex] * width;
        maxArea = max(maxArea, area);
    }
    return maxArea;
}

int main() {
    vector<int> heights = {2, 1, 5, 6, 2, 3};
    cout << "Maximum rectangular area in the histogram: " << maxRectangularArea(heights) << endl;
    return 0;
}
```

This algorithm works as follows:

1. Iterate through each bar of the histogram.
2. If the stack is empty or the current bar's height is greater than or equal to the height of the bar at the top of the stack, push the current bar's index onto the stack.
3. If the current bar's height is less than the height of the bar at the top of the stack, pop the stack and calculate the area of the rectangle with the popped bar as the smallest bar. The width of the rectangle will be the difference between the current index and the index at the top of the stack (minus one if the stack is not empty).
4. Repeat steps 2 and 3 until all bars are processed.
5. After the loop, pop all remaining bars from the stack and calculate the area for each, updating the maximum area as necessary.
6. Return the maximum area found.

This algorithm has a time complexity of O(n), where n is the number of bars in the histogram.

### 1. Algorithms & Data Structures (C++): Stack: Next Greater Element

Certainly! The Next Greater Element problem can be solved using a stack efficiently. The problem statement is as follows:

Given an array, for each element, find the next element (to its right side) which is greater than the current element. If there is no greater element to the right, return -1.

Here's the C++ code to solve this problem using a stack:

```cpp
#include <iostream>
#include <stack>
#include <vector>
#include <unordered_map>

using namespace std;

vector<int> nextGreaterElement(vector<int>& nums) {
    stack<int> st;
    unordered_map<int, int> nextGreater;
    vector<int> result(nums.size(), -1); // Initialize result vector with -1

    for (int i = 0; i < nums.size(); ++i) {
        while (!st.empty() && nums[i] > nums[st.top()]) {
            // If current element is greater than the element at top of stack
            nextGreater[st.top()] = i; // Store the index of next greater element
            st.pop(); // Pop the element from stack
        }
        st.push(i); // Push current element's index onto the stack
    }

    // Fill the result vector using the indices stored in the map
    for (int i = 0; i < nums.size(); ++i) {
        if (nextGreater.count(i)) {
            result[i] = nums[nextGreater[i]]; // Update result with the next greater element
        }
    }

    return result;
}

int main() {
    vector<int> nums = {4, 5, 2, 10, 8};
    vector<int> result = nextGreaterElement(nums);

    cout << "Next Greater Elements: ";
    for (int num : result) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}
```

This code will find the next greater element for each element in the given array and store the results in a vector. The time complexity of this solution is O(n) because each element is pushed and popped from the stack at most once.

### 1. Algorithms & Data Structures (C++): Stack: Parentheses Balanced

Balanced parentheses are a classic problem in computer science and can be efficiently solved using a stack data structure. The task is to determine if a given string of parentheses is balanced, meaning that every opening parenthesis has a corresponding closing parenthesis and they appear in the correct order.

Here's a C++ implementation to check whether a string of parentheses is balanced or not:

```cpp
#include <iostream>
#include <stack>
#include <string>

bool isBalanced(const std::string& parentheses) {
    std::stack<char> stack;
    for (char paren : parentheses) {
        if (paren == '(' || paren == '[' || paren == '{') {
            stack.push(paren);
        } else if (paren == ')' || paren == ']' || paren == '}') {
            if (stack.empty()) {
                return false; // Unmatched closing parenthesis
            }
            char top = stack.top();
            stack.pop();
            if ((paren == ')' && top != '(') ||
                (paren == ']' && top != '[') ||
                (paren == '}' && top != '{')) {
                return false; // Mismatched parentheses
            }
        }
    }
    return stack.empty(); // True if all parentheses matched
}

int main() {
    std::string input;
    std::cout << "Enter a string of parentheses: ";
    std::cin >> input;
    if (isBalanced(input)) {
        std::cout << "The parentheses are balanced." << std::endl;
    } else {
        std::cout << "The parentheses are not balanced." << std::endl;
    }
    return 0;
}
```

This code defines a function `isBalanced` that takes a string of parentheses as input and returns true if the parentheses are balanced, and false otherwise. The function uses a stack to keep track of opening parentheses encountered so far. When a closing parenthesis is encountered, it checks if it matches the top element of the stack (i.e., the most recent opening parenthesis). If there's a match, the opening parenthesis is popped from the stack. If the stack is empty at the end, it means all parentheses have been matched, and the function returns true. Otherwise, it returns false.

### 1. Algorithms & Data Structures (C++): Stack: Parenthesis Matching

Sure, I can provide you with an example of how to implement parenthesis matching using a stack in C++. The idea is to iterate through the string containing parentheses, pushing opening parentheses onto the stack and popping when a closing parenthesis is encountered. If the stack is empty when a closing parenthesis is found or there are unmatched parentheses at the end, then the parentheses are not balanced.

Here's a simple implementation:

```cpp
#include <iostream>
#include <stack>
#include <string>

bool isMatching(char open, char close) {
    return (open == '(' && close == ')') ||
           (open == '[' && close == ']') ||
           (open == '{' && close == '}');
}

bool isBalanced(const std::string& expression) {
    std::stack<char> s;
    for (char ch : expression) {
        if (ch == '(' || ch == '[' || ch == '{') {
            s.push(ch);
        } else if (ch == ')' || ch == ']' || ch == '}') {
            if (s.empty() || !isMatching(s.top(), ch)) {
                return false;
            }
            s.pop();
        }
    }
    return s.empty(); // If stack is empty at the end, then balanced
}

int main() {
    std::string expression;
    std::cout << "Enter an expression containing parentheses: ";
    std::getline(std::cin, expression);
    if (isBalanced(expression)) {
        std::cout << "Parentheses are balanced." << std::endl;
    } else {
        std::cout << "Parentheses are not balanced." << std::endl;
    }
    return 0;
}
```

In this code:

- The `isMatching` function checks whether a given pair of parentheses matches.
- The `isBalanced` function iterates through the expression, pushing opening parentheses onto the stack and popping when encountering a closing parenthesis. If a closing parenthesis is encountered without a corresponding opening parenthesis on the stack, or if there are unmatched parentheses at the end, the function returns `false`.
- The `main` function takes an input expression from the user and calls the `isBalanced` function to determine whether the parentheses in the expression are balanced or not.

### 1. Algorithms & Data Structures (C++): Stack: Pop

In C++, popping an element from a stack involves removing the top element of the stack. The standard library provides the `pop()` function for this purpose. Here's a basic example:

```cpp
#include <iostream>
#include <stack>

int main() {
    std::stack<int> myStack;
    
    // Pushing elements onto the stack
    myStack.push(10);
    myStack.push(20);
    myStack.push(30);

    // Popping the top element
    myStack.pop();

    // Now the top element should be 20
    std::cout << "Top element after popping: " << myStack.top() << std::endl;

    return 0;
}
```

In this example, `myStack.pop()` removes the top element (which is 30), leaving 20 as the new top element.

### 1. Algorithms & Data Structures (C++): Stack: Pop for a Stack That Uses a Vector

Sure, here's an implementation of the `pop()` function for a stack that uses a vector in C++:

```cpp
#include <iostream>
#include <vector>
#include <stdexcept>

template <typename T>
class Stack {
private:
    std::vector<T> elements;

public:
    // Push element onto the stack
    void push(const T& element) {
        elements.push_back(element);
    }

    // Pop element from the stack
    void pop() {
        if (empty()) {
            throw std::out_of_range("Stack

empty, cannot pop.");
        }
        elements.pop_back();
    }

    // Return the top element of the stack
    T& top() {
        if (empty()) {
            throw std::out_of_range("Stack empty, cannot access top element.");
        }
        return elements.back();
    }

    // Check if the stack is empty
    bool empty() const {
        return elements.empty();
    }

    // Return the size of the stack
    size_t size() const {
        return elements.size();
    }
};

int main() {
    Stack<int> myStack;

    // Push some elements onto the stack
    myStack.push(10);
    myStack.push(20);
    myStack.push(30);

    // Display the top element
    std::cout << "Top element: " << myStack.top() << std::endl;

    // Pop an element
    myStack.pop();

    // Display the top element again
    std::cout << "Top element after pop: " << myStack.top() << std::endl;

    return 0;
}
```

In this implementation, the `pop()` function removes the top element from the stack by using the `pop_back()` function of the `std::vector` container. It also includes error handling to check if the stack is empty before attempting to pop an element.

### 1. Algorithms & Data Structures (C++): Stack: Pop for Stack That Uses List

In C++, if you're implementing a stack using a list, you can use the `std::list` container from the Standard Template Library (STL) along with its member functions to implement the stack operations. Here's a basic implementation of a stack using `std::list` and the `pop()` operation:

```cpp
#include <iostream>
#include <list>

template<typename T>
class Stack {
private:
    std::list<T> elements;

public:
    // Push element onto the stack
    void push(const T& element) {
        elements.push_back(element);
    }

    // Pop element from the stack
    void pop() {
        if (!elements.empty()) {
            elements.pop_back();
        } else {
            std::cerr << "Stack is empty. Cannot pop." << std::endl;
        }
    }

    // Get the top element of the stack
    T& top() {
        if (!elements.empty()) {
            return elements.back();
        } else {
            throw std::runtime_error("Stack is empty. Cannot get top element.");
        }
    }

    // Check if the stack is empty
    bool empty() const {
        return elements.empty();
    }

    // Get the size of the stack
    size_t size() const {
        return elements.size();
    }
};

int main() {
    Stack<int> stack;

    stack.push(10);
    stack.push(20);
    stack.push(30);

    std::cout << "Stack size: " << stack.size() << std::endl;

    while (!stack.empty()) {
        std::cout << "Top element: " << stack.top() << std::endl;
        stack.pop();
    }

    return 0;
}
```

In this implementation:

- We use the `std::list` container to hold the elements of the stack.
- The `push()` function appends elements to the end of the list.
- The `pop()` function removes the last element of the list if the stack is not empty.
- The `top()` function returns a reference to the last element of the list, which is the top element of the stack.
- The `empty()` function checks if the stack is empty.
- The `size()` function returns the number of elements in the stack.

This implementation demonstrates the basic functionality of a stack using a list in C++.

### 1. Algorithms & Data Structures (C++): Stack: Postfix Evaluation

Postfix evaluation using a stack is a common problem in computer science and programming interviews. In postfix notation (also known as Reverse Polish Notation), operators come after their operands. The evaluation of postfix expressions is straightforward and can be efficiently done using a stack data structure.

Here's a C++ implementation of postfix expression evaluation using a stack:

```cpp
#include <iostream>
#include <stack>
#include <string>
#include <cstdlib> // for atoi()

using namespace std;

int evaluatePostfix(const string& expression) {
    stack<int> operands;

    for (char ch : expression) {
        if (isdigit(ch)) {
            operands.push(ch - '0'); // Convert char to integer and push to stack
        } else if (ch == ' ') {
            // Ignore whitespaces
            continue;
        } else {
            // Operator encountered
            int operand2 = operands.top();
            operands.pop();
            int operand1 = operands.top();
            operands.pop();
            int result;

            switch (ch) {
                case '+':
                    result = operand1 + operand2;
                    break;
                case '-':
                    result = operand1 - operand2;
                    break;
                case '*':
                    result = operand1 * operand2;
                    break;
                case '/':
                    result = operand1 / operand2;
                    break;
                default:
                    cerr << "Invalid operator: " << ch << endl;
                    return INT_MIN; // Indicate error
            }

            operands.push(result);
        }
    }

    return operands.top();
}

int main() {
    string expression = "5 3 + 4 * 2 /"; // Postfix expression: (5+3)*4/2 = 16
    cout << "Result: " << evaluatePostfix(expression) << endl;
    return 0;
}
```

In this implementation:

- We iterate through each character of the expression.
- If the character is a digit, we convert it to an integer and push it onto the stack.
- When we encounter an operator, we pop the top two operands from the stack, perform the operation, and push the result back onto the stack.
- Finally, we return the result left on the stack.

This implementation assumes that the input expression is valid postfix notation and contains only integers, operators, and spaces between them.

### 1. Algorithms & Data Structures (C++): Stack: Push

In C++, pushing an element onto a stack involves adding an element to the top of the stack. Here's a simple example of how you can implement the `push` operation for a stack using C++:

```cpp
#include <iostream>
#include <stack>

using namespace std;

int main() {
    // Create a stack of integers
    stack<int> myStack;

    // Push elements onto the stack
    myStack.push(10);
    myStack.push(20);
    myStack.push(30);

    // Display the elements of the stack
    cout << "Stack elements after pushing: ";
    while (!myStack.empty()) {
        cout << myStack.top() << " ";
        myStack.pop(); // Removing the top element after displaying
    }
    cout << endl;

    return 0;
}
```

In this example:

- We include the necessary header files.
- Create a stack named `myStack` that stores integers.
- Push elements onto the stack using the `push` member function.
- We can access the top element of the stack using the `top()` member function, and we remove the top element using the `pop()` member function.

This code will output:

```bash
Stack elements after pushing: 30 20 10
```

This demonstrates pushing elements onto a stack in C++.

### 1. Algorithms & Data Structures (C++): Stack: Push for a Stack That Uses a Vector

Sure, here's an example implementation of the `push` operation for a stack using a vector in C++:

```cpp
#include <iostream>
#include <vector>

template <typename T>
class Stack {
private:
    std::vector<T> elements;

public:
    // Function to push an element onto the stack
    void push(const T& element) {
        elements.push_back(element);
    }

    // Function to check if the stack is empty
    bool empty() const {
        return elements.empty();
    }

    // Function to get the top element of the stack
    T& top() {
        if (empty()) {
            throw std::out_of_range("Stack

Empty");
        }
        return elements.back();
    }
};

int main() {
    Stack<int> myStack;
    
    // Push some elements onto the stack
    myStack.push(10);
    myStack.push(20);
    myStack.push(30);

    // Print the top element of the stack
    std::cout << "Top element of the stack: " << myStack.top() << std::endl;

    return 0;
}
```

In this implementation, the `push` function simply calls the `push_back` function of the vector to add an element to the end of the vector, effectively adding it to the top of the stack.

### 1. Algorithms & Data Structures (C++): Stack: Push for Stack That Uses List

Sure, here's an example of how you can implement the `push` operation for a stack using a list in C++:

```cpp
#include <iostream>
#include <list>

using namespace std;

template<typename T>
class Stack {
private:
    list<T> data;
public:
    // Push operation to add an element to the top of the stack
    void push(const T& value) {
        data.push_back(value);
    }

    // Method to check if the stack is empty
    bool isEmpty() const {
        return data.empty();
    }

    // Method to get the top element of the stack
    T& top() {
        if (isEmpty()) {
            throw out_of_range("Stack is empty");
        }
        return data.back();
    }
};

int main() {
    Stack<int> myStack;

    // Push some elements onto the stack
    myStack.push(10);
    myStack.push(20);
    myStack.push(30);

    // Print the top element of the stack
    cout << "Top element: " << myStack.top() << endl;

    return 0;
}
```

In this implementation:

- We're using the standard template library's `list` container to store the elements of the stack.
- The `push` operation simply adds an element to the end of the list.
- The `top` method returns the last element of the list, which is the top element of the stack.
- The `isEmpty` method checks if the list (and thus the stack) is empty.

This is a basic implementation, but you can expand upon it by adding more functionality like pop, peek, or even iterate over the elements of the stack.

### 1. Algorithms & Data Structures (C++): Stack: Reverse String

To reverse a string using a stack in C++, you can follow these steps:

1. Create an empty stack.
2. Push each character of the string onto the stack.
3. Pop each character from the stack and append it to a new string.
4. The new string will be the reversed version of the original string.

Here's the C++ code implementing this algorithm:

```cpp
#include <iostream>
#include <stack>
#include <string>

using namespace std;

string reverseString(const string& str) {
    stack<char> charStack;

    // Push each character onto the stack
    for (char ch : str) {
        charStack.push(ch);
    }

    string reversedStr;
    // Pop each character from the stack and append to reversedStr
    while (!charStack.empty()) {
        reversedStr += charStack.top();
        charStack.pop();
    }

    return reversedStr;
}

int main() {
    string str = "Hello, World!";
    string reversed = reverseString(str);
    cout << "Original String: " << str << endl;
    cout << "Reversed String: " << reversed << endl;
    return 0;
}
```

This code will output:

```
Original String: Hello, World!
Reversed String: !dlroW ,olleH
```

This approach reverses the string in linear time, making use of a stack data structure.

### 1. Algorithms & Data Structures (C++): Stack: Reversing the content of a text file

Certainly! You can use a stack data structure to reverse the content of a text file in C++. Here's how you can do it:

```cpp
#include <iostream>
#include <fstream>
#include <stack>
#include <string>

using namespace std;

void reverseFileContent(const string& filename) {
    // Open the input file
    ifstream input(filename);
    
    // Check if file opened successfully
    if (!input.is_open()) {
        cout << "Unable to open file: " << filename << endl;
        return;
    }
    
    // Stack to store lines of the file
    stack<string> lines;
    
    // Read the file line by line and push each line onto the stack
    string line;
    while (getline(input, line)) {
        lines.push(line);
    }
    
    // Close the input file
    input.close();
    
    // Open the same file for writing
    ofstream output(filename);
    
    // Check if file opened successfully
    if (!output.is_open()) {
        cout << "Unable to open file: " << filename << " for writing." << endl;
        return;
    }
    
    // Pop lines from the stack and write them back to the file
    while (!lines.empty()) {
        output << lines.top() << endl;
        lines.pop();
    }
    
    // Close the output file
    output.close();
    
    cout << "Content of file '" << filename << "' reversed successfully." << endl;
}

int main() {
    string filename = "input.txt"; // Change the filename as per your requirement
    reverseFileContent(filename);
    return 0;
}
```

This code reads the content of a text file line by line, pushing each line onto a stack. After reading the entire file, it pops each line from the stack and writes it back to the file, effectively reversing the order of lines. Finally, it prints a success message.

Remember to replace `"input.txt"` with the path to the file you want to reverse.

### 1. Algorithms & Data Structures (C++): Stack: Sort Stack

To implement sorting of a stack using another stack, you can follow these steps:

1. Create a temporary stack.
2. While the input stack is not empty, pop the top element.
3. Keep popping elements from the temporary stack and pushing them onto the input stack while the top of the temporary stack is greater than the popped element or until the temporary stack is empty.
4. Push the popped element onto the temporary stack.
5. Repeat steps 2-4 until the input stack is empty.
6. The temporary stack now contains the elements of the input stack in sorted order.
7. Copy the elements back to the input stack.

Here's a sample implementation in C++:

```cpp
#include <stack>
#include <iostream>

void sortStack(std::stack<int>& inputStack) {
    std::stack<int> tempStack;
    while (!inputStack.empty()) {
        // Pop the top element from the input stack
        int temp = inputStack.top();
        inputStack.pop();

        // Move elements from the temporary stack to the input stack
        while (!tempStack.empty() && tempStack.top() > temp) {
            inputStack.push(tempStack.top());
            tempStack.pop();
        }

        // Push the popped element onto the temporary stack
        tempStack.push(temp);
    }

    // Copy elements from the temporary stack back to the input stack
    while (!tempStack.empty()) {
        inputStack.push(tempStack.top());
        tempStack.pop();
    }
}

int main() {
    std::stack<int> myStack;
    myStack.push(5);
    myStack.push(2);
    myStack.push(8);
    myStack.push(1);
    myStack.push(6);

    std::cout << "Original Stack: ";
    while (!myStack.empty()) {
        std::cout << myStack.top() << " ";
        myStack.pop();
    }
    std::cout << std::endl;

    // Sorting the stack
    sortStack(myStack);

    std::cout << "Sorted Stack: ";
    while (!myStack.empty()) {
        std::cout << myStack.top() << " ";
        myStack.pop();
    }
    std::cout << std::endl;

    return 0;
}
```

This code demonstrates how to sort a stack of integers in ascending order. You can modify it according to your requirements and the data type of the stack elements.

### 1. Algorithms & Data Structures (C++): Stack: Time & Space Complexity of Algorithm Which Checks Balanced Paranthesis

The algorithm to check balanced parentheses using a stack typically has a time complexity of O(n) and a space complexity of O(n), where n is the length of the input string.

Here's a brief explanation of why:

- **Time Complexity (O(n))**: The algorithm scans the input string character by character once. For each character, it either pushes it onto the stack (if it's an opening parenthesis) or pops from the stack and checks if the popped parenthesis matches the current closing parenthesis (if it's a closing parenthesis). Since each character is processed once, the time complexity is linear with respect to the length of the input string, hence O(n).

- **Space Complexity (O(n))**: In the worst-case scenario, if all the characters in the input string are opening parentheses, they will all be pushed onto the stack. Thus, the maximum space used by the stack would be proportional to the length of the input string, leading to a space complexity of O(n).

This makes the algorithm efficient and suitable for checking balanced parentheses in practical scenarios.

### 1. Algorithms & Data Structures (C++): Stacks

Stacks are fundamental data structures in computer science and are widely used in various algorithms and applications. A stack is a linear data structure that follows the Last In, First Out (LIFO) principle, meaning that the last element added to the stack is the first one to be removed.

In C++, you can implement a stack using either arrays or linked lists. Here's a basic implementation of a stack using an array:

```cpp
#include <iostream>

const int MAX_SIZE = 100; // Maximum size of the stack

class Stack {
private:
    int top;            // Index of the top element
    int data[MAX_SIZE]; // Array to store elements

public:
    Stack() : top(-1) {}  // Constructor

    // Check if the stack is empty
    bool isEmpty() {
        return top == -1;
    }

    // Check if the stack is full
    bool isFull() {
        return top == MAX_SIZE - 1;
    }

    // Push an element onto the stack
    void push(int val) {
        if (isFull()) {
            std::cout << "Stack Overflow\n";
            return;
        }
        data[++top] = val;
    }

    // Pop an element from the stack
    int pop() {
        if (isEmpty()) {
            std::cout << "Stack Underflow\n";
            return -1;
        }
        return data[top--];
    }

    // Return the top element of the stack
    int peek() {
        if (isEmpty()) {
            std::cout << "Stack is empty\n";
            return -1;
        }
        return data[top];
    }
};

int main() {
    Stack stack;

    // Pushing elements onto the stack
    stack.push(5);
    stack.push(10);
    stack.push(15);

    // Popping elements from the stack
    std::cout << stack.pop() << std::endl; // Output: 15
    std::cout << stack.pop() << std::endl; // Output: 10
    std::cout << stack.pop() << std::endl; // Output: 5

    // Trying to pop from an empty stack
    std::cout << stack.pop() << std::endl; // Output: Stack Underflow

    return 0;
}
```

This code demonstrates a basic implementation of a stack using an array. It includes methods for pushing elements onto the stack (`push()`), popping elements from the stack (`pop()`), checking if the stack is empty (`isEmpty()`), checking if the stack is full (`isFull()`), and peeking at the top element of the stack (`peek()`).

### 1. Algorithms & Data Structures (C++): Stacks (Theory)

Stacks are fundamental data structures in computer science, following the Last-In-First-Out (LIFO) principle, meaning the last element inserted is the first one to be removed. This structure mimics a real-life stack of items, where you can only add or remove from the top.

### Key Operations

1. **Push**: Add an element to the top of the stack.
2. **Pop**: Remove the top element from the stack.
3. **Peek (or Top)**: Get the top element without removing it.
4. **isEmpty**: Check if the stack is empty.
5. **Size**: Get the number of elements in the stack.

### Characteristics

- **Dynamic Size**: Stacks can dynamically grow or shrink as elements are pushed or popped.
- **Implementation**: Can be implemented using arrays or linked lists.
- **Efficiency**: Typically, the time complexity for push, pop, peek, isEmpty, and size operations is O(1).
- **Uses**: Stacks are used in various algorithms and applications, including expression evaluation, backtracking, parsing, and implementing function calls and recursion.

### Applications

1. **Expression Evaluation**: Stacks are used to evaluate infix, postfix, and prefix expressions.
2. **Function Call Stack**: In programming languages, stacks are used to manage function calls, local variables, and return addresses.
3. **Backtracking Algorithms**: Stacks are employed in backtracking algorithms like Depth-First Search (DFS) to store the state of exploration.
4. **Compiler Parsing**: Stacks are used in compiler design for parsing and syntax analysis.
5. **Undo Mechanisms**: Stacks are used to implement undo mechanisms in text editors and other applications.

### Implementation

In C++, stacks can be implemented using arrays or linked lists. Here's a basic implementation using an array:

```cpp
#include <iostream>
#define MAX_SIZE 1000 // Maximum size of stack

class Stack {
private:
    int top;
    int arr[MAX_SIZE];

public:
    Stack() { top = -1; }

    bool isEmpty() { return (top == -1); }

    void push(int val) {
        if (top >= (MAX_SIZE - 1)) {
            std::cout << "Stack Overflow\n";
            return;
        }
        arr[++top] = val;
    }

    int pop() {
        if (isEmpty()) {
            std::cout << "Stack Underflow\n";
            return -1;
        }
        return arr[top--];
    }

    int peek() {
        if (isEmpty()) {
            std::cout << "Stack is empty\n";
            return -1;
        }
        return arr[top];
    }

    int size() { return top + 1; }
};

int main() {
    Stack s;
    s.push(10);
    s.push(20);
    s.push(30);

    std::cout << "Top element: " << s.peek() << std::endl;
    std::cout << "Stack size: " << s.size() << std::endl;

    std::cout << "Popped element: " << s.pop() << std::endl;
    std::cout << "Popped element: " << s.pop() << std::endl;

    std::cout << "Stack size after pop: " << s.size() << std::endl;

    return 0;
}
```

This code demonstrates the basic functionalities of a stack, including push, pop, peek, isEmpty, and size.

### 1. Algorithms & Data Structures (C++): Stacks & Queue Problems

Sure, I'd be happy to help with some algorithms and data structures problems involving stacks and queues in C++. What specific problems are you looking to tackle?

### 1. Algorithms & Data Structures (C++): Stacks & Queues

Stacks and queues are fundamental data structures used in computer science and programming, including in C++. Let's delve into each:

### Stacks

- **Definition:** A stack is a Last In, First Out (LIFO) data structure, where the last element added is the first one to be removed. It's like a stack of plates; you can only take the top plate off.
- **Operations:** Stacks typically support two primary operations:
  1. **Push:** Adds an element to the top of the stack.
  2. **Pop:** Removes and returns the top element from the stack.
- **Implementation in C++:** You can implement a stack using arrays or linked lists.
- **Example Use Cases:** Function call stack, undo functionality in text editors, backtracking algorithms, expression evaluation.

Here's a simple C++ implementation of a stack using an array:

```cpp
#include <iostream>
using namespace std;

const int MAX_SIZE = 100; // Maximum size of the stack

class Stack {
private:
    int arr[MAX_SIZE];
    int top;

public:
    Stack() {
        top = -1;
    }

    void push(int x) {
        if (top >= MAX_SIZE - 1) {
            cout << "Stack Overflow\n";
            return;
        }
        arr[++top] = x;
    }

    int pop() {
        if (top < 0) {
            cout << "Stack Underflow\n";
            return -1;
        }
        return arr[top--];
    }

    bool isEmpty() {
        return top == -1;
    }

    int peek() {
        if (top < 0) {
            cout << "Stack is empty\n";
            return -1;
        }
        return arr[top];
    }
};

int main() {
    Stack s;
    s.push(1);
    s.push(2);
    s.push(3);
    cout << s.pop() << endl; // Outputs: 3
    cout << s.peek() << endl; // Outputs: 2
    return 0;
}
```

### Queues

- **Definition:** A queue is a First In, First Out (FIFO) data structure, where the first element added is the first one to be removed. It's like a queue of people waiting in line; the first person who joins the line is the first to leave.
- **Operations:** Queues typically support two primary operations:
  1. **Enqueue:** Adds an element to the back of the queue.
  2. **Dequeue:** Removes and returns the front element from the queue.
- **Implementation in C++:** You can implement a queue using arrays or linked lists.
- **Example Use Cases:** Task scheduling, breadth-first search algorithm, printer queues.

Here's a simple C++ implementation of a queue using an array:

```cpp
#include <iostream>
using namespace std;

const int MAX_SIZE = 100; // Maximum size of the queue

class Queue {
private:
    int arr[MAX_SIZE];
    int front, rear;

public:
    Queue() {
        front = rear = -1;
    }

    void enqueue(int x) {
        if (rear >= MAX_SIZE - 1) {
            cout << "Queue Overflow\n";
            return;
        }
        if (front == -1) {
            front = rear = 0;
        } else {
            rear++;
        }
        arr[rear] = x;
    }

    int dequeue() {
        if (front == -1 || front > rear) {
            cout << "Queue Underflow\n";
            return -1;
        }
        int item = arr[front];
        front++;
        return item;
    }

    bool isEmpty() {
        return front == -1 || front > rear;
    }

    int peek() {
        if (front == -1 || front > rear) {
            cout << "Queue is empty\n";
            return -1;
        }
        return arr[front];
    }
};

int main() {
    Queue q;
    q.enqueue(1);
    q.enqueue(2);
    q.enqueue(3);
    cout << q.dequeue() << endl; // Outputs: 1
    cout << q.peek() << endl; // Outputs: 2
    return 0;
}
```

These implementations give you a basic idea of how stacks and queues work in C++. Feel free to expand and customize them based on your requirements!

### 1. Algorithms & Data Structures (C++): Stacks & Queues Big O

Certainly! Here's a breakdown of the typical time complexities (Big O notation) for common operations on stacks and queues implemented using arrays or linked lists in C++:

### Stacks

1. **Push Operation**:
   - Array Implementation: O(1) - Constant time complexity, as adding an element to the top of the stack requires only updating the top pointer/index.
   - Linked List Implementation: O(1) - Similarly, adding a node to the front of the linked list (representing the top of the stack) is a constant time operation.

2. **Pop Operation**:
   - Array Implementation: O(1) - Removing an element from the top of the stack also requires only updating the top pointer/index.
   - Linked List Implementation: O(1) - Removing the first node (top of the stack) is a constant time operation.

3. **Peek/Top Operation**:
   - Both Array and Linked List Implementations: O(1) - Simply returning the value of the top element without modifying the stack.

### Queues

1. **Enqueue Operation** (Adding an element):
   - Array Implementation: O(1) - Adding an element to the end of the array (tail of the queue) is a constant time operation.
   - Linked List Implementation: O(1) - Adding a node to the end of the linked list (tail of the queue) is also a constant time operation.

2. **Dequeue Operation** (Removing an element):
   - Array Implementation: O(n) - Removing the first element of an array-based queue requires shifting all remaining elements to the left.
   - Linked List Implementation: O(1) - Removing the first node (front of the queue) is a constant time operation.

3. **Front Operation** (Viewing the front element):
   - Both Array and Linked List Implementations: O(1) - Simply returning the value of the first element without modifying the queue.

### Summary

- Stacks generally offer O(1) time complexity for push, pop, and peek operations, regardless of implementation.
- Queues offer O(1) time complexity for enqueue and front operations in both array and linked list implementations. However, the dequeue operation has different complexities based on the implementation: O(n) for array-based queues and O(1) for linked list-based queues.

These complexities assume basic implementations and may vary depending on specific optimizations or additional features implemented in the data structures.

### 1. Algorithms & Data Structures (C++): Stacks and Queues

Stacks and queues are fundamental data structures in computer science used to manage data in various applications. Let's delve into each of them:

### Stacks

A stack is a Last-In-First-Out (LIFO) data structure, where the last element added to the stack is the first one to be removed. Think of it like a stack of plates, where you can only remove the top plate. Key operations on a stack typically include:

1. **Push**: Add an element to the top of the stack.
2. **Pop**: Remove the element from the top of the stack.
3. **Peek (or Top)**: Get the element at the top of the stack without removing it.
4. **isEmpty**: Check if the stack is empty.

Here's a simple implementation of a stack in C++ using an array:

```cpp
#include <iostream>
using namespace std;

const int MAX_SIZE = 100;

class Stack {
private:
    int top;
    int arr[MAX_SIZE];
public:
    Stack() {
        top = -1; // Initialize top to -1 to indicate an empty stack
    }
    
    void push(int x) {
        if (top >= MAX_SIZE - 1) {
            cout << "Stack Overflow\n";
            return;
        }
        arr[++top] = x;
    }
    
    void pop() {
        if (top < 0) {
            cout << "Stack Underflow\n";
            return;
        }
        top--;
    }
    
    int peek() {
        if (top < 0) {
            cout << "Stack is empty\n";
            return -1;
        }
        return arr[top];
    }
    
    bool isEmpty() {
        return (top < 0);
    }
};
```

### Queues

A queue is a First-In-First-Out (FIFO) data structure, where the first element added to the queue is the first one to be removed. Think of it like people waiting in a line. Key operations on a queue typically include:

1. **Enqueue**: Add an element to the back of the queue.
2. **Dequeue**: Remove the element from the front of the queue.
3. **Front**: Get the element at the front of the queue without removing it.
4. **isEmpty**: Check if the queue is empty.

Here's a simple implementation of a queue in C++ using an array:

```cpp
#include <iostream>
using namespace std;

const int MAX_SIZE = 100;

class Queue {
private:
    int front, rear;
    int arr[MAX_SIZE];
public:
    Queue() {
        front = rear = -1; // Initialize front and rear to -1 to indicate an empty queue
    }
    
    void enqueue(int x) {
        if (rear >= MAX_SIZE - 1) {
            cout << "Queue Overflow\n";
            return;
        }
        arr[++rear] = x;
        if (front == -1) front = 0; // If it's the first element, set front to 0
    }
    
    void dequeue() {
        if (front == -1 || front > rear) {
            cout << "Queue Underflow\n";
            return;
        }
        front++;
    }
    
    int Front() {
        if (front == -1 || front > rear) {
            cout << "Queue is empty\n";
            return -1;
        }
        return arr[front];
    }
    
    bool isEmpty() {
        return (front == -1 || front > rear);
    }
};
```

These are basic implementations to get you started with stacks and queues in C++. Depending on your requirements, you can customize these implementations or use built-in libraries for more advanced functionality.

### 1. Algorithms & Data Structures (C++): Stacks Implementation

Certainly! A stack is a fundamental data structure that follows the Last In, First Out (LIFO) principle. In C++, you can implement a stack using arrays or linked lists. Here's a simple implementation using arrays:

```cpp
#include <iostream>
using namespace std;

const int MAX_SIZE = 100; // Maximum size of the stack

class Stack {
private:
    int top;            // Index of the top element
    int arr[MAX_SIZE];  // Array to store elements

public:
    Stack() {
        top = -1;  // Initialize top to -1 to indicate an empty stack
    }

    bool isEmpty() {
        return top == -1;  // If top is -1, stack is empty
    }

    bool isFull() {
        return top == MAX_SIZE - 1;  // If top is at max size, stack is full
    }

    void push(int x) {
        if (isFull()) {
            cout << "Stack Overflow: Cannot push element " << x << endl;
            return;
        }
        arr[++top] = x;  // Increment top and insert the element
    }

    void pop() {
        if (isEmpty()) {
            cout << "Stack Underflow: Cannot pop from an empty stack" << endl;
            return;
        }
        top--;  // Decrement top to remove the top element
    }

    int peek() {
        if (isEmpty()) {
            cout << "Stack is empty" << endl;
            return -1;
        }
        return arr[top];  // Return the top element without removing it
    }
};

int main() {
    Stack stack;

    stack.push(5);
    stack.push(10);
    stack.push(15);

    cout << "Top element: " << stack.peek() << endl;

    stack.pop();

    cout << "Top element after pop: " << stack.peek() << endl;

    return 0;
}
```

This code defines a `Stack` class with basic stack operations such as `push()`, `pop()`, and `peek()`. It uses an array to store the elements, and `top` keeps track of the index of the top element in the stack. You can create a `Stack` object and perform operations on it as demonstrated in the `main()` function.

### 1. Algorithms & Data Structures (C++): Stacks implementation with arrays

Sure, here's a basic implementation of a stack using arrays in C++:

```cpp
#include <iostream>

#define MAX_SIZE 100 // Maximum size of the stack

class Stack {
private:
    int top;            // Index of the top element
    int array[MAX_SIZE]; // Array to store stack elements

public:
    Stack() {           // Constructor
        top = -1;       // Initialize top as -1
    }

    bool isEmpty() {    // Check if stack is empty
        return (top == -1);
    }

    bool isFull() {     // Check if stack is full
        return (top == MAX_SIZE - 1);
    }

    void push(int item) { // Push element onto the stack
        if (isFull()) {
            std::cout << "Stack Overflow\n";
            return;
        }
        array[++top] = item;
        std::cout << item << " pushed to stack\n";
    }

    int pop() {         // Remove and return the top element from the stack
        if (isEmpty()) {
            std::cout << "Stack Underflow\n";
            return -1;
        }
        return array[top--];
    }

    int peek() {        // Return the top element without removing it
        if (isEmpty()) {
            std::cout << "Stack is empty\n";
            return -1;
        }
        return array[top];
    }
};

int main() {
    Stack stack;

    stack.push(10);
    stack.push(20);
    stack.push(30);

    std::cout << stack.pop() << " popped from stack\n";

    std::cout << "Top element is " << stack.peek() << std::endl;

    return 0;
}
```

This implementation uses an array to hold the stack elements, and it provides basic operations like `push`, `pop`, and `peek`. The `MAX_SIZE` constant defines the maximum capacity of the stack. You can adjust this value according to your needs.

### 1. Algorithms & Data Structures (C++): Stacks in memory management (stacks and heaps)

In C++, memory management is crucial for efficient program execution. Stacks and heaps are two important concepts in memory management.

**Stack:**

- The stack is a region of memory that operates in a Last In, First Out (LIFO) manner.
- It's typically used for function call management, local variables, and passing function parameters.
- In C++, the stack memory management is handled automatically by the compiler. When a function is called, space for local variables and function parameters is allocated on the stack. When the function exits, the memory allocated for its variables is deallocated automatically.
- Stack memory allocation and deallocation are fast because it involves only moving the stack pointer.
- However, the size of the stack is usually limited, and if you exhaust it with deep recursion or large local variables, you'll encounter a stack overflow error.

**Heap:**

- The heap is a region of memory that operates in a less structured manner compared to the stack.
- It's used for dynamic memory allocation, where the size of the memory required is not known at compile time.
- In C++, memory allocation on the heap is managed using operators like `new` and `delete` or `new[]` and `delete[]`.
- Heap memory allocation and deallocation can be slower compared to the stack because it involves searching for a suitable block of memory and may lead to memory fragmentation.
- Unlike the stack, the size of the heap is typically much larger, limited by the available system memory.

**Stacks in Memory Management:**

In the context of memory management, stacks and heaps play distinct roles:

1. **Stack for Function Calls**: Every time a function is called, space is allocated on the stack for its local variables, parameters, and return address. When the function completes, the stack space is deallocated, making it a convenient and efficient mechanism for managing function calls.

2. **Stack for Memory Frames**: Each function call creates a new memory frame (also called activation record or stack frame) on the stack, which contains information about the function's execution, including parameters, local variables, and the return address. This allows for nested function calls and ensures that each function's variables are isolated from other functions.

3. **Stack for Data Structures**: Stacks (the abstract data structure) can also be implemented using the stack memory. For example, if you're implementing a stack using an array or a linked list, the memory for the stack elements can be allocated on the stack.

In summary, while the stack in memory management primarily handles function calls and their associated data, the heap is used for more dynamic memory needs, like allocating memory for objects whose sizes are determined at runtime. Both play crucial roles in C++ memory management, and understanding their differences and best use cases is essential for writing efficient and robust code.

### 1. Algorithms & Data Structures (C++): Stacks using Arrays

Certainly! In C++, you can implement a stack using arrays. Here's a basic implementation:

```cpp
#include <iostream>

#define MAX_SIZE 100 // Maximum size of the stack

class Stack {
private:
    int arr[MAX_SIZE];
    int top;

public:
    Stack() {
        top = -1; // Initialize top of the stack
    }

    bool isEmpty() {
        return top == -1;
    }

    bool isFull() {
        return top == MAX_SIZE - 1;
    }

    void push(int x) {
        if (isFull()) {
            std::cout << "Stack Overflow\n";
            return;
        }
        arr[++top] = x;
        std::cout << x << " pushed into stack\n";
    }

    int pop() {
        if (isEmpty()) {
            std::cout << "Stack Underflow\n";
            return -1;
        }
        return arr[top--];
    }

    int peek() {
        if (isEmpty()) {
            std::cout << "Stack is empty\n";
            return -1;
        }
        return arr[top];
    }
};

int main() {
    Stack stack;
    
    stack.push(10);
    stack.push(20);
    stack.push(30);

    std::cout << stack.pop() << " popped from stack\n";

    std::cout << "Top element is " << stack.peek() << std::endl;

    return 0;
}
```

In this implementation:

- We define a class `Stack` with private member variables `arr`, an array to hold the stack elements, and `top`, an integer representing the index of the top element of the stack.
- `isEmpty()` and `isFull()` functions check if the stack is empty or full, respectively.
- `push(int x)` function inserts an element into the stack.
- `pop()` function removes and returns the top element from the stack.
- `peek()` function returns the top element without removing it.
- In the `main()` function, we demonstrate how to use the `Stack` class by pushing elements onto the stack, popping elements, and peeking at the top element.

### 1. Algorithms & Data Structures (C++): Stacks using Linked List

Certainly! Implementing a stack using a linked list in C++ is a common exercise in data structures. Here's a basic implementation:

```cpp
#include <iostream>

// Define a Node structure for the linked list
struct Node {
    int data;
    Node* next;
    Node(int value) : data(value), next(nullptr) {}
};

// Define the Stack class
class Stack {
private:
    Node* top; // Pointer to the top of the stack

public:
    // Constructor
    Stack() : top(nullptr) {}

    // Destructor
    ~Stack() {
        // Free memory allocated for nodes
        while (top != nullptr) {
            Node* temp = top;
            top = top->next;
            delete temp;
        }
    }

    // Function to check if the stack is empty
    bool isEmpty() {
        return top == nullptr;
    }

    // Function to push an element onto the stack
    void push(int value) {
        Node* newNode = new Node(value);
        newNode->next = top;
        top = newNode;
    }

    // Function to pop an element from the stack
    int pop() {
        if (isEmpty()) {
            std::cerr << "Stack is empty\n";
            return -1; // or throw an exception
        }
        int poppedValue = top->data;
        Node* temp = top;
        top = top->next;
        delete temp;
        return poppedValue;
    }

    // Function to peek at the top element of the stack
    int peek() {
        if (isEmpty()) {
            std::cerr << "Stack is empty\n";
            return -1; // or throw an exception
        }
        return top->data;
    }
};

// Main function for testing the stack
int main() {
    Stack stack;
    stack.push(10);
    stack.push(20);
    stack.push(30);

    std::cout << "Top element: " << stack.peek() << std::endl;

    std::cout << "Popped element: " << stack.pop() << std::endl;
    std::cout << "Popped element: " << stack.pop() << std::endl;
    std::cout << "Top element after popping: " << stack.peek() << std::endl;

    return 0;
}
```

In this implementation:

- We define a `Node` struct to represent each element of the linked list.
- The `Stack` class maintains a pointer `top` to the top of the stack.
- Functions like `push`, `pop`, `peek`, and `isEmpty` are defined to manipulate the stack.
- The `main` function provides a simple test case demonstrating the usage of the stack.

### 1. Algorithms & Data Structures (C++): Stacks VS Queues

Stacks and queues are fundamental data structures in computer science, each with its unique characteristics and applications.

**Stacks:**

1. **Last In, First Out (LIFO) Structure:** The last element added to the stack is the first one to be removed.
2. **Operations:**
   - **Push:** Adds an element to the top of the stack.
   - **Pop:** Removes the top element from the stack.
   - **Peek (or Top):** Returns the top element without removing it.
3. **Implementation:**
   - Can be implemented using arrays, linked lists, or dynamic arrays.
4. **Applications:**
   - Function call stack in programming languages.
   - Reversing the order of items.
   - Undo mechanisms in applications.
   - Parentheses matching and expression evaluation.

**Queues:**

1. **First In, First Out (FIFO) Structure:** The first element added to the queue is the first one to be removed.
2. **Operations:**
   - **Enqueue:** Adds an element to the back of the queue.
   - **Dequeue:** Removes and returns the front element from the queue.
   - **Front (or Peek):** Returns the front element without removing it.
3. **Implementation:**
   - Can be implemented using arrays, linked lists, or circular buffers.
4. **Applications:**
   - Print queue management.
   - CPU scheduling algorithms.
   - Breadth-first search (BFS) algorithm in graph traversal.
   - Message passing systems.

**Comparison:**

- **Ordering:** Stacks maintain the order based on the sequence of additions and removals, whereas queues maintain the order of elements based on the principle of first-in-first-out (FIFO).
- **Access:** Stacks allow access to only the top element without removing it, while queues allow access to both the front and back elements.
- **Use Cases:** Stacks are suitable for applications where the most recently added item needs to be processed first, such as in function calls and expression evaluation. Queues are useful for scenarios where elements need to be processed in the order they were added, such as in task scheduling and message passing.

In C++, both stacks and queues are provided as part of the Standard Template Library (STL) under the `<stack>` and `<queue>` headers, respectively. They offer efficient implementations with various member functions to perform operations like push, pop, enqueue, and dequeue.

### 1. Algorithms & Data Structures (C++): Stacks: Interview Question : Valid Parentheses

The Valid Parentheses problem is a classic interview question that can be solved efficiently using a stack. Here's how you can approach it in C++:

```cpp
#include <iostream>
#include <stack>
#include <string>

bool isValid(std::string s) {
    std::stack<char> parentheses;

    for (char &c : s) {
        if (c == '(' || c == '[' || c == '{') {
            parentheses.push(c);
        } else {
            if (parentheses.empty()) {
                return false; // If stack is empty, there's no opening parenthesis to match
            } else if ((c == ')' && parentheses.top() != '(') ||
                       (c == ']' && parentheses.top() != '[') ||
                       (c == '}' && parentheses.top() != '{')) {
                return false; // If the closing parenthesis doesn't match the top of the stack, it's invalid
            } else {
                parentheses.pop(); // Valid closing parenthesis, pop the corresponding opening parenthesis
            }
        }
    }

    return parentheses.empty(); // If stack is empty, all parentheses were matched
}

int main() {
    std::string str;
    std::cout << "Enter a string with parentheses: ";
    std::cin >> str;

    if (isValid(str)) {
        std::cout << "Valid parentheses!" << std::endl;
    } else {
        std::cout << "Invalid parentheses!" << std::endl;
    }

    return 0;
}
```

This program defines a function `isValid()` that takes a string `s` as input and returns `true` if the string contains a valid arrangement of parentheses, brackets, and braces, and `false` otherwise. It uses a stack to keep track of opening parentheses encountered so far. When a closing parenthesis is encountered, it checks if it matches the top of the stack. If it does, it pops the corresponding opening parenthesis from the stack. If the stack is empty or if the closing parenthesis doesn't match the top of the stack, the string is invalid.

The `main()` function simply prompts the user to enter a string and then calls `isValid()` to check if the parentheses in the string are valid.

### 1. Algorithms & Data Structures (C++): Stacks: Minimum Brackets To Remove

To solve the problem of finding the minimum number of brackets to remove in a string to make it valid, you can use a stack data structure. The idea is to iterate through the string and keep track of opening brackets using a stack. Whenever you encounter a closing bracket, you check if it matches the top element of the stack (which should be an opening bracket). If it matches, you pop the opening bracket from the stack; otherwise, you mark the closing bracket for removal.

Here's a C++ implementation of this approach:

```cpp
#include <iostream>
#include <stack>
#include <string>

int minBracketsToRemove(const std::string& s) {
    std::stack<int> st; // Stack to store indices of opening brackets

    for (int i = 0; i < s.length(); ++i) {
        if (s[i] == '(') {
            st.push(i); // Push index of opening bracket
        } else if (s[i] == ')') {
            if (!st.empty()) {
                st.pop(); // Matching opening bracket found
            } else {
                // No matching opening bracket found, mark for removal
                s[i] = '*';
            }
        }
    }

    // Mark remaining opening brackets for removal
    while (!st.empty()) {
        s[st.top()] = '*';
        st.pop();
    }

    // Count remaining brackets marked for removal
    int count = 0;
    for (char c : s) {
        if (c == '*') {
            count++;
        }
    }

    return count;
}

int main() {
    std::string s = "())()(()))";
    std::cout << "Minimum brackets to remove: " << minBracketsToRemove(s) << std::endl;
    return 0;
}
```

This code will output the minimum number of brackets to remove to make the string valid. The time complexity of this solution is O(n), where n is the length of the string.

### 1. Algorithms & Data Structures (C++): Time and Space Complexity of Stack

In C++, a stack is typically implemented using an array or a linked list. Let's analyze the time and space complexities of both implementations:

1. **Array-based Stack:**

    - **Time Complexity:**
        - Push Operation: O(1) on average. If the array needs to be resized, it could be O(n) in the worst case, where n is the number of elements in the stack.
        - Pop Operation: O(1).
        - Peek Operation: O(1).
        - Search Operation: O(n), as you might need to traverse the entire stack.

    - **Space Complexity:** O(n), where n is the number of elements in the stack. This is because the array needs to allocate space for each element.

2. **Linked List-based Stack:**

    - **Time Complexity:**
        - Push Operation: O(1).
        - Pop Operation: O(1).
        - Peek Operation: O(1).
        - Search Operation: O(n), as you might need to traverse the entire stack.

    - **Space Complexity:** O(n), where n is the number of elements in the stack. Each node in the linked list will consume memory.

In summary, both implementations have the same time and space complexity for most operations. However, array-based implementations may have occasional O(n) time complexity for push operations when resizing is required.

### 1. Algorithms & Data Structures (C++): Using Stack

Using a stack in C++ can be incredibly useful for implementing algorithms and data structures that require last-in, first-out (LIFO) behavior. Here's a brief overview of how you can use the stack in C++:

1. **Include the necessary header file**: Start by including the `<stack>` header file.

   ```cpp
   #include <stack>
   ```

2. **Declare a stack**: Create a stack object of the desired type.

   ```cpp
   std::stack<int> myStack; // Example stack of integers
   ```

3. **Operations on the stack**:

   - **Push**: Add an element to the top of the stack.

     ```cpp
     myStack.push(5); // Pushes 5 onto the stack
     ```

   - **Pop**: Remove the element from the top of the stack.

     ```cpp
     myStack.pop(); // Removes the top element (5 in this case)
     ```

   - **Top**: Get the top element of the stack without removing it.

     ```cpp
     int topElement = myStack.top(); // Retrieves the top element (without removing it)
     ```

   - **Size**: Get the current size of the stack.

     ```cpp
     int size = myStack.size(); // Returns the number of elements in the stack
     ```

   - **Empty**: Check if the stack is empty.

     ```cpp
     if (myStack.empty()) {
         // Stack is empty
     }
     ```

4. **Iterating through the stack**: You can't iterate through a stack directly, but you can repeatedly pop elements until it's empty.

   ```cpp
   while (!myStack.empty()) {
       int element = myStack.top();
       // Do something with the element
       myStack.pop();
   }
   ```

Remember that stacks are a fundamental data structure used in various algorithms and applications such as expression evaluation, backtracking, parsing, and more. Understanding how to use stacks efficiently is crucial for mastering data structures and algorithms in C++.

### 1. Algorithms & Data Structures (C++): Valid brackets

Sure! The problem of validating brackets is a classic example of using a stack data structure. Here's a simple C++ implementation to validate brackets:

```cpp
#include <iostream>
#include <stack>
#include <string>

bool isValid(std::string s) {
    std::stack<char> stack;
    for (char c : s) {
        if (c == '(' || c == '[' || c == '{') {
            stack.push(c);
        } else {
            if (stack.empty()) {
                return false;
            }
            char top = stack.top();
            stack.pop();
            if ((c == ')' && top != '(') || (c == ']' && top != '[') || (c == '}' && top != '{')) {
                return false;
            }
        }
    }
    return stack.empty();
}

int main() {
    std::string str = "{[()]}";
    if (isValid(str)) {
        std::cout << "Valid brackets\n";
    } else {
        std::cout << "Invalid brackets\n";
    }
    return 0;
}
```

This code defines a function `isValid` that takes a string containing brackets and returns true if the brackets are balanced and false otherwise. It iterates through each character of the string, pushing opening brackets onto the stack and popping from the stack when encountering a closing bracket. If the closing bracket doesn't match the top of the stack, or if the stack is empty when encountering a closing bracket, it returns false. Finally, it checks if the stack is empty after iterating through the string to ensure all brackets are matched.

### 1. Algorithms & Data Structures (C++): Valid brackets: Complexity analysis

The problem of validating brackets using algorithms and data structures, such as a stack, can be approached with a time complexity analysis. Here's a breakdown:

1. **Input Size**: Let's denote the size of the input string as \( n \), where \( n \) is the number of characters in the string.

2. **Stack Operations**:
   - Each character in the string is iterated once. During each iteration, there are potentially two operations on the stack:
     - Push operation: If the character is an opening bracket.
     - Pop operation: If the character is a closing bracket and matches the top of the stack.
   - Both push and pop operations are \( O(1) \) operations for a stack implemented using an array or a linked list.

3. **Time Complexity**:
   - For each character in the string, there is at most one push or pop operation.
   - Hence, the time complexity is linear in terms of the input size \( n \), expressed as \( O(n) \).

4. **Space Complexity**:
   - Space complexity is determined by the additional space used by the stack.
   - In the worst case, when all opening brackets are followed by closing brackets in a valid sequence, the stack could hold all opening brackets. Hence, the space complexity is also \( O(n) \).

5. **Optimizations**:
   - If the input string has an odd number of characters, we can immediately return false as it can't be balanced.
   - If the first character is a closing bracket, we can immediately return false.
   - If we encounter a closing bracket without a matching opening bracket on the stack, we can immediately return false.
   - After iterating through the entire string, if the stack is not empty, it means there are unmatched opening brackets, so we return false.

6. **Example**: Here's a simple implementation in C++:

```cpp
#include <iostream>
#include <stack>
#include <string>

bool isValid(std::string s) {
    std::stack<char> stack;
    for (char c : s) {
        if (c == '(' || c == '[' || c == '{') {
            stack.push(c);
        } else {
            if (stack.empty()) return false;
            if ((c == ')' && stack.top() != '(') ||
                (c == ']' && stack.top() != '[') ||
                (c == '}' && stack.top() != '{')) {
                return false;
            }
            stack.pop();
        }
    }
    return stack.empty();
}

int main() {
    std::string testString = "{[()]}";
    std::cout << isValid(testString) << std::endl; // Output: 1 (true)
    return 0;
}
```

This code snippet demonstrates the linear time complexity \( O(n) \) and linear space complexity \( O(n) \) characteristics of the algorithm for validating brackets.

### 1. Algorithms & Data Structures (C++): What are stacks ?

In C++ programming, a stack is a data structure that follows the Last In, First Out (LIFO) principle, meaning the last element added to the stack will be the first one to be removed. Think of it as a stack of plates, where you can only add or remove plates from the top.

In terms of implementation, you can use arrays or linked lists to create a stack. However, the dynamic nature of linked lists often makes them a preferred choice due to their ability to grow and shrink easily.

Here are some key operations associated with stacks:

1. **Push**: Adds an element to the top of the stack.
2. **Pop**: Removes the top element from the stack.
3. **Top (or Peek)**: Returns the top element of the stack without removing it.
4. **isEmpty**: Checks if the stack is empty.
5. **Size**: Returns the number of elements in the stack.

In C++, you can implement a stack using the standard template library (STL) `std::stack` or by creating your own stack class using arrays or linked lists. Here's a simple example of using `std::stack`:

```cpp
#include <iostream>
#include <stack>

int main() {
    std::stack<int> myStack;

    // Push elements onto the stack
    myStack.push(10);
    myStack.push(20);
    myStack.push(30);

    // Pop elements from the stack
    while (!myStack.empty()) {
        std::cout << myStack.top() << " "; // Print the top element
        myStack.pop(); // Remove the top element
    }

    return 0;
}
```

This would output: `30 20 10`, demonstrating the LIFO behavior of the stack.

### 1. Algorithms & Data Structures (C++): What is a Stack?

In C++ and many other programming languages, a stack is a data structure that follows the Last In, First Out (LIFO) principle. Think of it like a stack of plates in a cafeteria—when you add a new plate, you put it on top, and when you want to remove a plate, you take the one from the top.

In terms of implementation, a stack typically supports two primary operations:

1. **Push**: This operation adds an element to the top of the stack.
2. **Pop**: This operation removes the top element from the stack.

Additionally, stacks often support another operation:

1. **Peek (or Top)**: This operation allows you to look at the top element of the stack without removing it.

These operations make stacks useful for various tasks such as parsing expressions, backtracking in algorithms, managing function calls in programming languages, and more.

In C++, you can implement a stack using various data structures such as arrays, linked lists, or the `std::stack` container provided by the Standard Template Library (STL). The `std::stack` is a wrapper around other container classes and provides a simple interface for using stacks in your programs.

### 1. Algorithms & Data Structures (C++): What is stack

In C++ programming, a stack is a linear data structure that follows the Last In, First Out (LIFO) principle. It means that the element which is added last will be the first one to be removed. Think of it like a stack of plates in a cafeteria; you can only take the top plate.

In terms of implementation, you can use either arrays or linked lists to create a stack. Common operations associated with a stack include:

1. **Push**: Adding an element onto the top of the stack.
2. **Pop**: Removing the top element from the stack.
3. **Peek (or Top)**: Viewing the top element without removing it.
4. **isEmpty**: Checking if the stack is empty.
5. **Size**: Finding out how many elements are in the stack.

Here's a simple example of a stack implemented using C++ standard library:

```cpp
#include <iostream>
#include <stack>

int main() {
    std::stack<int> myStack;

    // Pushing elements onto the stack
    myStack.push(10);
    myStack.push(20);
    myStack.push(30);

    // Printing the top element
    std::cout << "Top element: " << myStack.top() << std::endl;

    // Popping elements
    myStack.pop();
    std::cout << "Top element after pop: " << myStack.top() << std::endl;

    // Checking if the stack is empty
    if (myStack.empty()) {
        std::cout << "Stack is empty\n";
    } else {
        std::cout << "Stack is not empty\n";
    }

    // Finding the size of the stack
    std::cout << "Size of stack: " << myStack.size() << std::endl;

    return 0;
}
```

This code demonstrates basic stack operations such as pushing elements, popping elements, checking if the stack is empty, finding the top element, and determining the size of the stack.

### 1. Algorithms & Data Structures (C++): What is Stack Data Structure ?

A stack is a fundamental data structure in computer science that follows the Last In, First Out (LIFO) principle. This means that the last element added to the stack will be the first one to be removed. Think of it like a stack of plates where you can only remove the top plate.

In a stack, two main operations are performed:

1. **Push**: Adds an element to the top of the stack.
2. **Pop**: Removes the element from the top of the stack.

Additionally, there's often a third operation:

1. **Peek (or Top)**: Returns the element at the top of the stack without removing it.

These operations are typically implemented using an array or a linked list. In C++, you can implement a stack using either the `std::stack` container from the Standard Template Library (STL) or by creating your own stack class.

Here's a basic example of how you might implement a stack in C++ using an array:

```cpp
#include <iostream>
#define MAX_SIZE 100

class Stack {
private:
    int arr[MAX_SIZE];
    int top;

public:
    Stack() {
        top = -1; // Initialize top to -1 to indicate an empty stack
    }

    void push(int value) {
        if (top == MAX_SIZE - 1) {
            std::cout << "Stack Overflow! Cannot push element.\n";
            return;
        }
        arr[++top] = value;
    }

    void pop() {
        if (top == -1) {
            std::cout << "Stack Underflow! Cannot pop element.\n";
            return;
        }
        top--;
    }

    int peek() {
        if (top == -1) {
            std::cout << "Stack is empty!\n";
            return -1; // Return some default value indicating failure
        }
        return arr[top];
    }

    bool isEmpty() {
        return top == -1;
    }
};

int main() {
    Stack stack;
    
    stack.push(5);
    stack.push(10);
    stack.push(15);

    std::cout << "Top element: " << stack.peek() << std::endl;

    stack.pop();
    std::cout << "Top element after pop: " << stack.peek() << std::endl;

    return 0;
}
```

This implementation provides basic functionalities of a stack, including pushing, popping, peeking, and checking if the stack is empty or not.

### 1. Algorithms & Data Structures (C++): When there is no need of stack

In programming, particularly in C++, stacks are often used for various purposes, including implementing recursive algorithms, parsing expressions, backtracking, and managing function calls. However, there are situations where stacks are not necessary. Here are some scenarios:

1. **Linear Data Processing**: If you're simply iterating over a linear data structure like an array or a linked list without any need for backtracking or recursion, you might not need a stack.

2. **Queue Operations**: If you're implementing a First In First Out (FIFO) operation, a queue might be more suitable than a stack. For example, when processing elements in the order they were added without any need to backtrack.

3. **Tree Traversal**: Although stacks are commonly used in tree traversal algorithms (like in-order, pre-order, and post-order traversal), certain traversal methods, such as level-order traversal, can be performed without a stack.

4. **Simple Arithmetic Calculations**: For basic arithmetic calculations or expressions without nested parentheses, you might not need a stack. Simple expressions can be evaluated using straightforward algorithms without the need for stack-based evaluation.

5. **Direct Access Data Structures**: Data structures like arrays or hash tables that support direct access to elements might not require a stack. Stacks are typically used for sequential access or operations that involve a Last In First Out (LIFO) order.

6. **State Machines**: In some cases, state machines or finite automata can be implemented without using a stack. State transitions can be managed using variables and conditional statements.

7. **Memory Management**: Modern C++ provides features like smart pointers and containers that manage memory automatically. In such cases, explicit stack management for memory allocation and deallocation might not be necessary.

8. **Performance Considerations**: In performance-critical applications, avoiding unnecessary stack operations can lead to more efficient code execution. If a simpler data structure or algorithm suffices, it's often preferable to avoid the overhead associated with stack operations.

In summary, while stacks are versatile and widely used in programming, there are many scenarios where they are not needed, and simpler alternatives can be employed instead. Understanding when to use stacks and when to employ other data structures or algorithms is essential for writing efficient and maintainable code.

### 1. Algorithms & Data Structures (C++): When to use/avoid Stack

Stacks are fundamental data structures that follow the Last In, First Out (LIFO) principle. They are efficient for managing function calls, tracking state changes, and implementing algorithms like backtracking and expression evaluation. Here are scenarios where you might want to use or avoid stacks in C++:

**Use Stacks:**

1. **Function Call Management**: Stacks are used by compilers and interpreters to manage function calls, storing return addresses and local variables.

2. **Expression Evaluation**: Stacks are useful for evaluating expressions, especially infix to postfix conversion and postfix evaluation, as well as solving problems like parenthesis matching and infix expression conversion.

3. **Backtracking Algorithms**: Many backtracking algorithms, like depth-first search (DFS) in graph traversal or solving problems like the N-Queens problem, utilize stacks to track the current state and backtrack when needed.

4. **Undo Mechanism**: Stacks can be used to implement an undo mechanism in applications where users need to revert their actions.

5. **Parsing**: Stacks can be used in parsing algorithms, such as parsing XML or HTML documents, to keep track of nested structures.

**Avoid Stacks:**

1. **Random Access or Search**: Stacks are inefficient for random access or searching. If your primary operation involves accessing elements at arbitrary positions or searching for specific elements, other data structures like arrays or hash tables might be more suitable.

2. **Memory Usage**: Stacks can lead to stack overflow errors if too many items are pushed onto the stack, especially in recursive algorithms or when dealing with large datasets. In such cases, consider using dynamic memory allocation or alternative data structures.

3. **Complexity**: While stacks offer efficient insertion and deletion operations (O(1) time complexity), other data structures like queues or trees might offer better performance for specific operations, such as searching or sorting.

4. **Concurrency**: Stacks might not be the best choice for concurrent programming due to potential race conditions and synchronization issues. In concurrent environments, thread-safe data structures like concurrent queues or locks might be preferred.

In summary, use stacks when dealing with LIFO-based operations like function calls, expression evaluation, backtracking, or parsing. However, consider other data structures for scenarios requiring random access, memory efficiency, or complex operations.

### 1. Algorithms & Data Structures (C++): Where Stack is used?

Stacks are fundamental data structures used in various algorithms and applications. In C++, stacks are typically implemented using arrays or linked lists. Here are some common applications of stacks:

1. **Function Call Stack**: In languages like C++ that support function calls, a stack is used to manage function calls. When a function is called, its local variables and the return address are pushed onto the stack. When the function returns, the stack is popped, and control returns to the caller.

2. **Expression Evaluation**: Stacks are used in evaluating arithmetic expressions, converting infix expressions to postfix or prefix notation, and evaluating the postfix or prefix expressions. This is often accomplished using a stack to store operators and operands.

3. **Parsing**: Stacks are used in parsing algorithms, such as for parsing arithmetic expressions or programming language syntax. They help in keeping track of nested structures like parentheses, braces, or tags in XML/HTML.

4. **Backtracking Algorithms**: In backtracking algorithms, stacks are used to store the state of the search at each step so that it can be later restored when backtracking.

5. **Undo Functionality**: Stacks are used to implement undo functionality in applications like text editors, where each action is pushed onto a stack, allowing the user to undo operations sequentially.

6. **Expression Conversion and Evaluation**: Stacks are used in converting expressions from infix to postfix or prefix notation and then evaluating the converted expressions.

7. **Memory Management**: Stacks are used in memory management systems, such as managing memory for recursive function calls or managing dynamic memory allocation and deallocation.

8. **Depth-First Search (DFS)**: In graph algorithms, stacks are used in depth-first search (DFS) to keep track of vertices to visit. DFS typically uses recursion, and the system stack effectively acts as a stack data structure.

These are just a few examples of where stacks are commonly used. Their simplicity and efficiency in managing data make them versatile and widely applicable in various programming scenarios.

### 1. Algorithms & Data Structures (C++): Drawbacks of Array Implementation of Stack

While arrays can be used to implement a stack data structure in C++, there are several drawbacks associated with this approach:

1. **Fixed Size**: Arrays have a fixed size, meaning you need to specify the maximum number of elements the stack can hold when you declare the array. This can lead to either wasted memory if the array is larger than necessary or runtime errors if the stack exceeds its capacity.

2. **Memory Wastage**: If the size of the array is set too large, it can lead to wastage of memory, especially if the stack does not reach its maximum capacity. Conversely, if the size is set too small, it can lead to stack overflow errors if the stack exceeds its capacity.

3. **Dynamic Resize**: Unlike some other data structures like linked lists, arrays require more complex logic to resize dynamically when they run out of space. If the stack needs to grow beyond the size of the array, you'll need to allocate a new array, copy elements over, and deallocate the old array, which can be inefficient in terms of time complexity.

4. **Insertion and Deletion Overhead**: Inserting or deleting elements in the middle of an array (which can happen when pushing or popping elements in a stack) requires shifting all subsequent elements, resulting in a time complexity of O(n) for these operations, where n is the number of elements in the array.

5. **Fragmentation**: Frequent push and pop operations on the stack can lead to fragmentation of memory, especially if the stack grows and shrinks often. This fragmentation can make it difficult to find contiguous blocks of memory for resizing the array.

6. **Contiguous Memory Requirement**: Arrays require contiguous memory allocation. If a large enough contiguous block of memory is not available, the array cannot be created, which can be a limitation in systems with memory fragmentation.

7. **Not Suitable for Large Stacks**: For very large stacks, the array implementation might not be suitable due to the limitations of available memory or the overhead of resizing.

In summary, while arrays are a simple and efficient way to implement a stack with constant-time access to elements, they have limitations regarding fixed size, dynamic resizing, and memory overhead. Depending on the specific requirements of your application, you may need to consider alternative implementations such as linked lists or dynamic arrays (e.g., vectors in C++) to mitigate these drawbacks.
