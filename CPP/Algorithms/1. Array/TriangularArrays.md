### 1. Algorithms & Data Structures (C++): Triangular Arrays

Triangular arrays in the context of algorithms and data structures typically refer to arrays that are shaped like triangles, where each row has one fewer element than the previous row. They are commonly used to represent symmetric matrices or to store data in a triangular pattern to save memory space.

In C++, you can implement triangular arrays using various approaches. One common approach is to use a one-dimensional array and calculate the index of the element based on its row and column. Here's a simple implementation:

```cpp
#include <iostream>
using namespace std;

class TriangularArray {
private:
    int size;
    int* array;

    // Calculate the index of the triangular array
    int calculateIndex(int row, int col) {
        if (row >= col) {
            return (row * (row - 1) / 2) + col;
        } else {
            return (col * (col - 1) / 2) + row;
        }
    }

public:
    TriangularArray(int n) {
        size = n * (n + 1) / 2;
        array = new int[size];
        for (int i = 0; i < size; ++i) {
            array[i] = 0; // Initialize all elements to 0
        }
    }

    ~TriangularArray() {
        delete[] array;
    }

    // Set value at given row and column
    void setValue(int row, int col, int value) {
        if (row < 0 || col < 0 || row >= size || col >= size) {
            cout << "Invalid row or column index\n";
            return;
        }
        array[calculateIndex(row, col)] = value;
    }

    // Get value at given row and column
    int getValue(int row, int col) {
        if (row < 0 || col < 0 || row >= size || col >= size) {
            cout << "Invalid row or column index\n";
            return -1; // Or throw an exception
        }
        return array[calculateIndex(row, col)];
    }
};

int main() {
    TriangularArray arr(5); // Create a 5x5 triangular array

    arr.setValue(0, 0, 1);
    arr.setValue(1, 0, 2);
    arr.setValue(1, 1, 3);
    arr.setValue(2, 0, 4);
    arr.setValue(2, 1, 5);
    arr.setValue(2, 2, 6);

    cout << arr.getValue(1, 1) << endl; // Output: 3

    return 0;
}
```

This implementation uses a one-dimensional array to represent the triangular array, and it calculates the index of each element based on its row and column. It provides methods to set and get values at specific positions in the triangular array.

### 1. Algorithms & Data Structures (C++): Triangular Arrays: How to Build This Array

A triangular array is a two-dimensional array where the values are only stored in the upper or lower triangle of the matrix, rather than in the entire matrix. Let's focus on building a triangular array in C++.

One way to implement a triangular array in C++ is to use a one-dimensional array and calculate the index based on the row and column of the triangular matrix.

Here's an example of how you can implement it:

```cpp
#include <iostream>
using namespace std;

class TriangularArray {
private:
    int* array;
    int size;

public:
    // Constructor
    TriangularArray(int n) {
        size = n * (n + 1) / 2; // Number of elements in a triangular array of size n
        array = new int[size];
        // Initialize array elements to zero
        for (int i = 0; i < size; i++) {
            array[i] = 0;
        }
    }

    // Destructor
    ~TriangularArray() {
        delete[] array;
    }

    // Set value at row i and column j
    void setValue(int i, int j, int value) {
        if (i >= 0 && j >= 0 && i <= j) {
            int index = (i * (i + 1) / 2) + j; // Calculate index in 1D array
            array[index] = value;
        } else {
            cout << "Invalid indices." << endl;
        }
    }

    // Get value at row i and column j
    int getValue(int i, int j) {
        if (i >= 0 && j >= 0 && i <= j) {
            int index = (i * (i + 1) / 2) + j; // Calculate index in 1D array
            return array[index];
        } else {
            cout << "Invalid indices." << endl;
            return -1; // Return some default value indicating error
        }
    }
};

int main() {
    int size = 5; // Size of the triangular array
    TriangularArray triangularArray(size);

    // Set values
    triangularArray.setValue(0, 0, 1);
    triangularArray.setValue(1, 0, 2);
    triangularArray.setValue(1, 1, 3);
    triangularArray.setValue(2, 0, 4);
    triangularArray.setValue(2, 1, 5);
    triangularArray.setValue(2, 2, 6);

    // Get and print values
    for (int i = 0; i < size; i++) {
        for (int j = 0; j <= i; j++) {
            cout << triangularArray.getValue(i, j) << " ";
        }
        cout << endl;
    }

    return 0;
}
```

In this implementation:

* We define a class `TriangularArray` to encapsulate the functionality.
* The constructor takes the size of the triangular array as an argument and allocates memory for the one-dimensional array based on the size.
* `setValue` and `getValue` methods are used to set and get values respectively at a given row and column.
* The indices of the triangular array are calculated using a formula to map them to the corresponding indices of the one-dimensional array.
* In the `main` function, we demonstrate how to use the `TriangularArray` class to set and get values.

You can adjust the `size` variable in the `main` function to create triangular arrays of different sizes.
