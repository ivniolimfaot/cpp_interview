### 1. Algorithms & Data Structures (C++): Stacks (Theory)

Stacks are fundamental data structures in computer science, following the Last-In-First-Out (LIFO) principle, meaning the last element inserted is the first one to be removed. This structure mimics a real-life stack of items, where you can only add or remove from the top.

#### Key Operations

1. **Push**: Add an element to the top of the stack.
2. **Pop**: Remove the top element from the stack.
3. **Peek (or Top)**: Get the top element without removing it.
4. **isEmpty**: Check if the stack is empty.
5. **Size**: Get the number of elements in the stack.

#### Characteristics

- **Dynamic Size**: Stacks can dynamically grow or shrink as elements are pushed or popped.
- **Implementation**: Can be implemented using arrays or linked lists.
- **Efficiency**: Typically, the time complexity for push, pop, peek, isEmpty, and size operations is O(1).
- **Uses**: Stacks are used in various algorithms and applications, including expression evaluation, backtracking, parsing, and implementing function calls and recursion.

#### Applications

1. **Expression Evaluation**: Stacks are used to evaluate infix, postfix, and prefix expressions.
2. **Function Call Stack**: In programming languages, stacks are used to manage function calls, local variables, and return addresses.
3. **Backtracking Algorithms**: Stacks are employed in backtracking algorithms like Depth-First Search (DFS) to store the state of exploration.
4. **Compiler Parsing**: Stacks are used in compiler design for parsing and syntax analysis.
5. **Undo Mechanisms**: Stacks are used to implement undo mechanisms in text editors and other applications.

#### Implementation

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

### 1. Algorithms & Data Structures (C++): Stack: Balanced Parentheses

To determine if a sequence of parentheses (or other types of brackets) is balanced, we can use a stack data structure. Here’s how you can implement an algorithm in C++ to check if the parentheses are balanced:

1. **Initialization**: Create an empty stack.
2. **Traversal**: Traverse the string from left to right.
   - If you encounter an opening bracket (such as '(', '[', or '{'), push it onto the stack.
   - If you encounter a closing bracket (such as ')', ']', or '}'), check if the stack is empty. If it is, the sequence is unbalanced because there is no matching opening bracket.
   - If the stack is not empty, pop the top of the stack and check if it matches the corresponding opening bracket for the current closing bracket. If it doesn't match, the sequence is unbalanced.
3. **Completion**: After traversing the string, if the stack is empty, the sequence is balanced. If not, it is unbalanced.

Here’s the C++ implementation:

```cpp
#include <iostream>
#include <stack>
#include <string>

bool isMatchingPair(char open, char close) {
    return (open == '(' && close == ')') ||
           (open == '[' && close == ']') ||
           (open == '{' && close == '}');
}

bool areParenthesesBalanced(const std::string& expression) {
    std::stack<char> stack;
    for (char ch : expression) {
        if (ch == '(' || ch == '[' || ch == '{') {
            stack.push(ch);
        } else if (ch == ')' || ch == ']' || ch == '}') {
            if (stack.empty() || !isMatchingPair(stack.top(), ch)) {
                return false;
            }
            stack.pop();
        }
    }
    return stack.empty();
}

int main() {
    std::string expression;
    std::cout << "Enter an expression: ";
    std::cin >> expression;

    if (areParenthesesBalanced(expression)) {
        std::cout << "Balanced\n";
    } else {
        std::cout << "Not Balanced\n";
    }

    return 0;
}
```

#### Explanation

1. **isMatchingPair Function**: This function checks if the opening and closing brackets match.
2. **areParenthesesBalanced Function**: This function checks the entire expression for balanced parentheses.
   - It uses a `for` loop to iterate through each character in the string.
   - It pushes opening brackets onto the stack.
   - For closing brackets, it checks for corresponding opening brackets at the top of the stack.
   - If the stack is empty at the end of the loop, all brackets were matched correctly.
3. **main Function**: This is the entry point of the program. It reads the expression from the user and calls the `areParenthesesBalanced` function to check if it is balanced.

#### Example

For the input `({[]})`, the program will output `Balanced` because every opening bracket has a corresponding closing bracket in the correct order.

For the input `({[)]}`, the program will output `Not Balanced` because the brackets do not match correctly.

This code ensures that parentheses are correctly nested and matched, making it a robust solution for the problem of checking balanced parentheses.

### 1. Algorithms & Data Structures (C++): Stack: Reverse a String

Reversing a string using a stack is a classic problem that demonstrates the Last In First Out (LIFO) property of stacks. Here's how you can implement this in C++:

1. **Push each character of the string onto the stack.**
2. **Pop each character from the stack and form the reversed string.**

Here is a step-by-step implementation:

#### Step-by-Step Implementation

1. **Include necessary headers**: We'll need the stack and string headers.
2. **Define the function**: Create a function that takes a string and returns the reversed string.
3. **Use the stack**: Push characters of the string onto the stack and then pop them to form the reversed string.

#### Code Example

```cpp
#include <iostream>
#include <stack>
#include <string>

// Function to reverse a string using a stack
std::string reverseString(const std::string &str) {
    std::stack<char> charStack;
    std::string reversedStr;

    // Push all characters of the string onto the stack
    for (char ch : str) {
        charStack.push(ch);
    }

    // Pop characters from the stack and append to the reversed string
    while (!charStack.empty()) {
        reversedStr += charStack.top();
        charStack.pop();
    }

    return reversedStr;
}

int main() {
    std::string input = "Hello, World!";
    std::string reversed = reverseString(input);

    std::cout << "Original String: " << input << std::endl;
    std::cout << "Reversed String: " << reversed << std::endl;

    return 0;
}
```

#### Explanation

1. **Headers**: `#include <iostream>` for standard I/O, `#include <stack>` for stack data structure, and `#include <string>` for string manipulation.
2. **reverseString Function**:
   - Takes a `const std::string &str` as input.
   - Uses a `std::stack<char>` to hold the characters.
   - Iterates through the input string and pushes each character onto the stack.
   - Pops characters from the stack and appends them to the `reversedStr` until the stack is empty.
3. **main Function**:
   - Defines an input string.
   - Calls `reverseString` to get the reversed string.
   - Prints the original and reversed strings.

#### Usage

- **Compile and Run**: You can compile this program using a C++ compiler like `g++`:

  ```bash
  g++ -o reverse_string reverse_string.cpp
  ./reverse_string
  ```

- **Output**:

  ```bash
  Original String: Hello, World!
  Reversed String: !dlroW ,olleH
  ```

This program effectively demonstrates the use of a stack to reverse a string by utilizing the LIFO principle.

### 1. Algorithms & Data Structures (C++): Stack: Evaluation of Postfix Expression

To evaluate a postfix expression (also known as Reverse Polish Notation), you can use a stack to keep track of operands and apply operators when they appear in the expression. Here’s how you can implement this in C++:

1. **Read the postfix expression from left to right**.
2. **Use a stack** to store operands.
3. When an operand is encountered, push it onto the stack.
4. When an operator is encountered, pop the required number of operands from the stack, apply the operator, and push the result back onto the stack.
5. The final result will be on the stack after the entire expression has been processed.

Here’s a step-by-step implementation:

#### Example Postfix Expression: `6 2 / 3 - 4 2 * +`

#### Step-by-Step Algorithm

1. Initialize an empty stack.
2. For each token in the postfix expression:
    - If the token is an operand, push it onto the stack.
    - If the token is an operator, pop the appropriate number of operands from the stack, apply the operator, and push the result back onto the stack.
3. The value left in the stack is the result of the postfix expression.

#### C++ Code Implementation

```cpp
#include <iostream>
#include <stack>
#include <sstream>
#include <string>

int evaluatePostfixExpression(const std::string& expression) {
    std::stack<int> stack;
    std::istringstream tokens(expression);
    std::string token;

    while (tokens >> token) {
        if (isdigit(token[0])) {
            stack.push(std::stoi(token));
        } else {
            int operand2 = stack.top(); stack.pop();
            int operand1 = stack.top(); stack.pop();
            int result;

            switch (token[0]) {
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
                    throw std::runtime_error("Unknown operator");
            }
            stack.push(result);
        }
    }

    return stack.top();
}

int main() {
    std::string expression = "6 2 / 3 - 4 2 * +";
    try {
        int result = evaluatePostfixExpression(expression);
        std::cout << "Result: " << result << std::endl;
    } catch (const std::exception& ex) {
        std::cerr << "Error: " << ex.what() << std::endl;
    }
    return 0;
}
```

#### Explanation

1. **Reading Input**:
   - `std::istringstream tokens(expression)` is used to tokenize the input string.
   - `tokens >> token` extracts each token from the input string.

2. **Handling Operands**:
   - `isdigit(token[0])` checks if the token is a digit.
   - `stack.push(std::stoi(token))` converts the token to an integer and pushes it onto the stack.

3. **Handling Operators**:
   - Pop the top two elements from the stack.
   - Apply the operator.
   - Push the result back onto the stack.

4. **Final Result**:
   - The result of the expression is the remaining element in the stack after processing all tokens.

#### Error Handling

- The code assumes the input expression is valid.
- Additional checks can be added to handle errors, such as insufficient operands or invalid operators.

#### Sample Output

For the given postfix expression `6 2 / 3 - 4 2 * +`, the output will be:

```
Result: 7
```

This C++ program correctly evaluates the given postfix expression using a stack.

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

### 1. Algorithms & Data Structures (C++): Stack of Plates

You need to create a data structure `SetOfStacks` that simulates a stack of plates where each sub-stack has a maximum capacity. When a sub-stack reaches this capacity, a new sub-stack is created.

#### Requirements

1. Implement a class `SetOfStacks` that contains multiple stacks.
2. Each stack has a maximum capacity.
3. Implement the following operations:
   - `void push(int value)`: Pushes a value onto the top stack.
   - `int pop()`: Pops a value from the top stack and returns it. If the stack is empty, continue to the previous stack.
   - `int popAt(int index)`: Pops a value from a specific sub-stack indicated by the index.

#### Implementation

Here's a possible C++ implementation:

```cpp
#include <iostream>
#include <vector>
#include <stack>
#include <stdexcept>

class SetOfStacks {
private:
    std::vector<std::stack<int>> stacks;
    int capacity;
    
public:
    SetOfStacks(int capacity) : capacity(capacity) {
        if (capacity <= 0) throw std::invalid_argument("Capacity must be greater than 0");
    }

    void push(int value) {
        if (stacks.empty() || stacks.back().size() == capacity) {
            std::stack<int> newStack;
            newStack.push(value);
            stacks.push_back(newStack);
        } else {
            stacks.back().push(value);
        }
    }

    int pop() {
        if (stacks.empty()) throw std::out_of_range("No plates to pop");
        int value = stacks.back().top();
        stacks.back().pop();
        if (stacks.back().empty()) {
            stacks.pop_back();
        }
        return value;
    }

    int popAt(int index) {
        if (index < 0 || index >= stacks.size()) throw std::out_of_range("Invalid stack index");
        int value = stacks[index].top();
        stacks[index].pop();
        if (stacks[index].empty()) {
            stacks.erase(stacks.begin() + index);
        }
        return value;
    }

    bool isEmpty() const {
        return stacks.empty();
    }
};

int main() {
    SetOfStacks stacks(3);

    stacks.push(1);
    stacks.push(2);
    stacks.push(3);
    stacks.push(4);
    stacks.push(5);
    stacks.push(6);
    stacks.push(7);

    std::cout << "Pop: " << stacks.pop() << std::endl;
    std::cout << "PopAt(0): " << stacks.popAt(0) << std::endl;
    std::cout << "Pop: " << stacks.pop() << std::endl;

    return 0;
}
```

#### Explanation

- **Class Members**:
  - `std::vector<std::stack<int>> stacks`: This is a vector of stacks to hold the plates.
  - `int capacity`: The maximum capacity of each sub-stack.
- **Constructor**:
  - `SetOfStacks(int capacity)`: Initializes the stack with a given capacity. Throws an exception if the capacity is less than or equal to zero.
- **Methods**:
  - `void push(int value)`: Adds a value to the top stack. If the top stack is at capacity or doesn't exist, it creates a new stack.
  - `int pop()`: Removes and returns the top value from the top stack. If the top stack is empty after popping, it removes the stack.
  - `int popAt(int index)`: Removes and returns the top value from the specific stack at the given index. If the stack at the index becomes empty after popping, it removes the stack.
  - `bool isEmpty() const`: Checks if the entire set of stacks is empty.

This implementation ensures that you can manage multiple stacks with a fixed capacity, handle edge cases such as popping from an empty stack, and provides flexibility to pop from a specific sub-stack.

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

#### Explanation

1. **Sorting:** The intervals are first sorted based on their starting points using `sort` and a custom comparator.
2. **Stack Operations:**
   - The first interval is pushed onto the stack.
   - For each interval, we check if it overlaps with the top of the stack:
     - If it does not overlap, we push it onto the stack.
     - If it overlaps, we merge the intervals by updating the end of the top interval.
3. **Result Extraction:** The intervals are extracted from the stack and reversed to maintain the original order.

#### Points to Consider

- The stack helps in keeping track of merged intervals efficiently.
- Sorting the intervals simplifies the problem significantly as it ensures that we only need to look at the top of the stack for merging.
- The time complexity is dominated by the sorting step, which is \(O(n \log n)\), where \(n\) is the number of intervals. The subsequent merging process is \(O(n)\). Thus, the overall complexity is \(O(n \log n)\).

### 1. Algorithms & Data Structures (C++): Stack practice: Next Greater Element

The "Next Greater Element" problem is a classic exercise involving stacks. The goal is to find the next greater element for each element in an array. The next greater element for an element \( x \) is the first greater element on the right side of \( x \) in the array. If no such element exists, we return -1 for that position.

Here’s a step-by-step guide and code implementation in C++ to solve this problem using a stack:

#### Problem Statement

Given an array of integers, for each element in the array, find the next greater element. If no such element exists, return -1.

#### Example

**Input:** [4, 5, 2, 25]  
**Output:** [5, 25, 25, -1]

#### Steps to Solve the Problem

1. **Initialize a stack** to keep track of elements for which we are trying to find the next greater element.
2. **Traverse the array from right to left**:
   - For each element, while the stack is not empty and the top of the stack is less than or equal to the current element, pop the stack.
   - If the stack becomes empty, it means there is no greater element on the right, so assign -1 to the result for that element.
   - If the stack is not empty, the top of the stack is the next greater element for the current element.
   - Push the current element onto the stack.
3. **Store the result** in an array and return it.

#### C++ Implementation

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

vector<int> nextGreaterElement(vector<int>& nums) {
    int n = nums.size();
    vector<int> result(n, -1); // Initialize the result array with -1
    stack<int> s; // Stack to keep track of elements
    
    for (int i = n - 1; i >= 0; --i) {
        // Maintain elements in stack in decreasing order from top to bottom
        while (!s.empty() && s.top() <= nums[i]) {
            s.pop();
        }
        
        if (!s.empty()) {
            result[i] = s.top();
        }
        
        s.push(nums[i]);
    }
    
    return result;
}

int main() {
    vector<int> nums = {4, 5, 2, 25};
    vector<int> result = nextGreaterElement(nums);
    
    cout << "Next greater elements are: ";
    for (int i : result) {
        cout << i << " ";
    }
    
    return 0;
}
```

#### Explanation

- We start by initializing a stack and a result vector filled with -1 (assuming there is no greater element initially).
- We iterate over the array from right to left to efficiently use the stack for the next greater element lookup.
- For each element, we ensure that the stack contains elements greater than the current element by popping elements that are not greater.
- If the stack is not empty after the popping process, the top of the stack is the next greater element for the current element.
- We then push the current element onto the stack for future comparisons.

This solution has a time complexity of \( O(n) \) because each element is pushed and popped from the stack at most once. The space complexity is \( O(n) \) due to the use of the stack and the result array.

### 1. Algorithms & Data Structures (C++): Stack Span Problem [RETURN]

The Stack Span Problem is a classic problem that can be efficiently solved using stacks. The problem is typically defined in the context of financial markets, where it is used to calculate the "span" of stock prices. The span of a stock's price for a given day is defined as the maximum number of consecutive days just before the given day for which the price of the stock on the current day is less than or equal to its price on those days.

Here’s a step-by-step approach to solve the Stack Span Problem using C++:

#### Problem Statement

Given an array of prices, we need to calculate the span for each price. The span of the price on the \(i^{th}\) day is defined as the maximum number of consecutive days just before the \(i^{th}\) day, for which the price of the stock is less than or equal to the price on the \(i^{th}\) day.

#### Example

For an array of stock prices: `[100, 80, 60, 70, 60, 75, 85]`

The spans are: `[1, 1, 1, 2, 1, 4, 6]`

#### Solution Using Stack

1. **Initialize a stack** that will store indices of the array elements.
2. **Traverse through the price array**.
3. For each price, **pop elements from the stack** until the stack is empty or the element at the index stored in the stack is greater than the current price.
4. The span for the current price is the difference between the current index and the index of the top element of the stack (if the stack is not empty) or the current index plus one (if the stack is empty).
5. **Push the current index** onto the stack.
6. Continue this for all elements of the price array.

#### C++ Implementation

Here’s the C++ code to implement the Stack Span Problem:

```cpp
#include <iostream>
#include <vector>
#include <stack>
using namespace std;

vector<int> calculateSpan(const vector<int>& prices) {
    vector<int> span(prices.size());
    stack<int> s;  // Stack to store indices

    for (int i = 0; i < prices.size(); ++i) {
        // Pop elements from stack while stack is not empty and top of stack is less than or equal to current price
        while (!s.empty() && prices[s.top()] <= prices[i]) {
            s.pop();
        }

        // If stack becomes empty, then price[i] is greater than all elements on left of it
        // Else price[i] is greater than elements after top of stack
        span[i] = s.empty() ? (i + 1) : (i - s.top());

        // Push this element to stack
        s.push(i);
    }
    return span;
}

int main() {
    vector<int> prices = {100, 80, 60, 70, 60, 75, 85};
    vector<int> span = calculateSpan(prices);

    cout << "Span of stock prices: ";
    for (int i = 0; i < span.size(); ++i) {
        cout << span[i] << " ";
    }
    cout << endl;
    return 0;
}
```

#### Explanation

1. **Vector Initialization**: We initialize a vector `span` of the same size as `prices` to store the span of each day.
2. **Stack Usage**: The stack `s` is used to store the indices of days. This helps in quickly accessing the previous higher price.
3. **Loop through Prices**: For each price, we pop indices from the stack until we find a day with a higher price than the current day or the stack is empty.
4. **Calculate Span**: The span for the current day is calculated based on the index of the last higher price found using the stack.
5. **Push Current Index**: After calculating the span, the current day’s index is pushed onto the stack.

This algorithm runs in O(n) time complexity, making it very efficient for large datasets.

### 1. Algorithms & Data Structures (C++): Stack using 2 Queues

Creating a stack using two queues can be done in a couple of different ways, but I'll present one common approach. In this method, we will use two queues, `queue1` and `queue2`, to simulate the stack's LIFO (Last In, First Out) behavior.

Here's the approach we'll take:

1. **Push Operation:** Always push the new element into `queue1`.
2. **Pop Operation:** Transfer all elements from `queue1` to `queue2`, except for the last element (the element to be popped). Swap the names of `queue1` and `queue2`.
3. **Top Operation:** Similar to the pop operation, but return the last element instead of removing it.

Here is the implementation in C++:

```cpp
#include <iostream>
#include <queue>

class StackUsingQueues {
private:
    std::queue<int> queue1;
    std::queue<int> queue2;
    
public:
    // Push element onto stack
    void push(int x) {
        queue1.push(x);
    }
    
    // Removes the element on top of the stack and returns that element
    int pop() {
        if (queue1.empty()) {
            std::cout << "Stack is empty!" << std::endl;
            return -1;
        }
        
        // Transfer all elements except the last one to queue2
        while (queue1.size() > 1) {
            queue2.push(queue1.front());
            queue1.pop();
        }
        
        // The last element in queue1 is the element to be popped
        int topElement = queue1.front();
        queue1.pop();
        
        // Swap the names of queue1 and queue2
        std::swap(queue1, queue2);
        
        return topElement;
    }
    
    // Get the top element
    int top() {
        if (queue1.empty()) {
            std::cout << "Stack is empty!" << std::endl;
            return -1;
        }
        
        // Transfer all elements except the last one to queue2
        while (queue1.size() > 1) {
            queue2.push(queue1.front());
            queue1.pop();
        }
        
        // The last element in queue1 is the element on the top of the stack
        int topElement = queue1.front();
        
        // Move the last element to queue2 as well
        queue2.push(topElement);
        queue1.pop();
        
        // Swap the names of queue1 and queue2
        std::swap(queue1, queue2);
        
        return topElement;
    }
    
    // Check if the stack is empty
    bool empty() {
        return queue1.empty();
    }
};

int main() {
    StackUsingQueues stack;
    
    stack.push(1);
    stack.push(2);
    stack.push(3);
    
    std::cout << "Top element is: " << stack.top() << std::endl; // Should print 3
    
    std::cout << "Popped element is: " << stack.pop() << std::endl; // Should print 3
    
    std::cout << "Top element is: " << stack.top() << std::endl; // Should print 2
    
    std::cout << "Stack is empty: " << (stack.empty() ? "Yes" : "No") << std::endl; // Should print No
    
    return 0;
}
```

#### Explanation:

- **Push Operation:** Directly push the element to `queue1`.
- **Pop Operation:** Transfer all elements except the last one from `queue1` to `queue2`. The last element is the one we need to pop. After popping, swap `queue1` and `queue2`.
- **Top Operation:** Transfer all elements except the last one from `queue1` to `queue2` to reach the last element, which is the top element. Push this element back to `queue2` after retrieving it. Swap `queue1` and `queue2`.
- **Empty Operation:** Simply check if `queue1` is empty.

By using this method, we ensure that the stack operations are simulated correctly using two queues.

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

### 1. Algorithms & Data Structures (C++): Stack: Duplicate Parentheses [RETURN] [INCORRECT]

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

### 1. Algorithms & Data Structures (C++): Stack: Infix Expression [RETURN]

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

### 1. Algorithms & Data Structures (C++): Stack: Infix to Postfix Conversion and Evaluation [RETURN]

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

### 1. Algorithms & Data Structures (C++): Stack: Maximum Rectangular Area in Histogram [RETURN]

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

### 1. Algorithms & Data Structures (C++): Stack: Sort Stack [RETURN]

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

### 1. Algorithms & Data Structures (C++): Stacks: Minimum Brackets To Remove [RETURN]

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

### 1. Algorithms & Data Structures (C++): Minimum Stack in O(1) [RETURN]

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

### 1. Algorithms & Data Structures (C++): Another Application of stack - Recursion [RETURN]

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

### 1. Algorithms & Data Structures (C++): Create Stack that returns the Smallest Element with One stack [RETURN]

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

### 1. Algorithms & Data Structures (C++): Double Stacks [RETURN]

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

### 1. Algorithms & Data Structures (C++): Exercise: Stack & Queue: Animal Shelter [RETURN]

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

### 1. Algorithms & Data Structures (C++): Program for Infix to Postfix Conversion [RETURN]

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
