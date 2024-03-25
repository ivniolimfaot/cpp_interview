# Data Structures

## Ganaeral Info

### What is a Sparse Matrix? How do you implement sparse array using STL map?

A sparse matrix is a matrix in which most of the elements are zero. These matrices are common in various applications like scientific computing, finite element analysis, and data compression. Storing all elements of a sparse matrix as a regular 2D array can be inefficient in terms of memory usage and computation. Therefore, sparse matrices are often stored in a more efficient manner to save space and optimize operations.

One way to implement a sparse matrix is by using an STL map in C++. Here's a basic outline of how you can implement a sparse matrix using `std::map`:

```cpp
#include <iostream>
#include <map>

template <typename T>
class SparseMatrix {
private:
    std::map<std::pair<int, int>, T> data; // Map to store non-zero elements

public:
    // Function to set value at a particular row and column
    void setValue(int row, int col, T value) {
        if (value != 0)
            data[{row, col}] = value; // Only store non-zero elements
        else
            data.erase({row, col}); // Remove the element if the value is 0
    }

    // Function to get value at a particular row and column
    T getValue(int row, int col) {
        auto it = data.find({row, col});
        if (it != data.end())
            return it->second;
        else
            return 0; // Return 0 if the element is not found
    }
};

int main() {
    SparseMatrix<int> matrix;
    
    // Setting values
    matrix.setValue(0, 1, 5);
    matrix.setValue(1, 2, 7);
    matrix.setValue(2, 0, 3);
    matrix.setValue(2, 2, 9);
    
    // Getting values
    std::cout << "Value at (0, 1): " << matrix.getValue(0, 1) << std::endl;
    std::cout << "Value at (1, 1): " << matrix.getValue(1, 1) << std::endl;
    std::cout << "Value at (2, 0): " << matrix.getValue(2, 0) << std::endl;
    
    return 0;
}
```

In this implementation:

- The `SparseMatrix` class holds a `std::map` where the keys are pairs of integers representing the row and column indices, and the values are the elements of the matrix.
- The `setValue` function sets the value at a given row and column, storing it in the map if it's non-zero. If the value is zero, it removes the element from the map.
- The `getValue` function retrieves the value at a given row and column. If the element is not found in the map, it returns 0.

This implementation efficiently handles sparse matrices by only storing non-zero elements.

### What is the sparse matrix?

A sparse matrix is a matrix in which most of the elements are zero. There are various ways to represent sparse matrices efficiently in C++. One common representation is using the compressed sparse row (CSR) format. In CSR format, we store only the non-zero elements of the matrix along with their corresponding row and column indices.

Here's a basic implementation of a sparse matrix using CSR format in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

class SparseMatrix {
private:
    int rows, cols;
    vector<int> values;
    vector<int> row_indices;
    vector<int> col_indices;

public:
    SparseMatrix(int rows, int cols) : rows(rows), cols(cols) {}

    void insert(int row, int col, int value) {
        if (row >= rows || col >= cols || row < 0 || col < 0) {
            cerr << "Invalid indices\n";
            return;
        }

        if (value != 0) {
            values.push_back(value);
            row_indices.push_back(row);
            col_indices.push_back(col);
        }
    }

    int get(int row, int col) const {
        if (row >= rows || col >= cols || row < 0 || col < 0) {
            cerr << "Invalid indices\n";
            return -1; // Assuming -1 as a default value for non-existing elements
        }

        for (size_t i = 0; i < values.size(); ++i) {
            if (row_indices[i] == row && col_indices[i] == col) {
                return values[i];
            }
        }

        return 0; // Default value for non-existing elements
    }
};

int main() {
    SparseMatrix mat(3, 3);

    mat.insert(0, 0, 3);
    mat.insert(1, 1, 5);
    mat.insert(2, 2, 7);

    cout << "Value at (0, 0): " << mat.get(0, 0) << endl;
    cout << "Value at (1, 1): " << mat.get(1, 1) << endl;
    cout << "Value at (2, 2): " << mat.get(2, 2) << endl;

    cout << "Value at (1, 0): " << mat.get(1, 0) << endl; // This should return 0

    return 0;
}
```

This implementation defines a `SparseMatrix` class that stores the non-zero elements, along with their row and column indices. The `insert` function is used to insert elements into the sparse matrix, while the `get` function retrieves the value at a specified row and column.

### Linked list C++

Certainly! Here's a basic implementation of a singly linked list in C++:

```cpp
#include <iostream>

template <typename T>
class Node {
public:
    T data;
    Node<T>* next;

    Node(T val) : data(val), next(nullptr) {}
};

template <typename T>
class LinkedList {
private:
    Node<T>* head;
public:
    LinkedList() : head(nullptr) {}

    void insert(T val) {
        Node<T>* newNode = new Node<T>(val);
        if (!head) {
            head = newNode;
        } else {
            Node<T>* temp = head;
            while (temp->next) {
                temp = temp->next;
            }
            temp->next = newNode;
        }
    }

    void display() {
        Node<T>* temp = head;
        while (temp) {
            std::cout << temp->data << " -> ";
            temp = temp->next;
        }
        std::cout << "nullptr" << std::endl;
    }

    ~LinkedList() {
        Node<T>* temp;
        while (head) {
            temp = head;
            head = head->next;
            delete temp;
        }
    }
};

int main() {
    LinkedList<int> list;
    list.insert(1);
    list.insert(2);
    list.insert(3);
    list.display();

    return 0;
}
```

This code defines a simple singly linked list with basic operations like insertion and display. You can create a linked list object, insert elements into it, and display the elements. The implementation includes a `Node` class representing individual nodes in the list and a `LinkedList` class for managing the list as a whole.
