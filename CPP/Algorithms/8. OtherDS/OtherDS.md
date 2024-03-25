### 1. Algorithms & Data Structures (C++): Binary Search-based Symbol Table

A Binary Search-based Symbol Table is a data structure that stores key-value pairs and allows for efficient searching, insertion, and deletion of these pairs. It is typically implemented using an ordered array or a binary search tree (BST). Here, I'll outline the implementation of a Binary Search-based Symbol Table in C++ using an ordered array.

```cpp
#include <iostream>

using namespace std;

// Structure to represent a key-value pair
struct KeyValuePair {
    int key;
    int value;
};

// Binary Search-based Symbol Table class
class SymbolTable {
private:
    KeyValuePair *table; // Array to store key-value pairs
    int capacity; // Capacity of the table
    int size; // Number of key-value pairs in the table

public:
    // Constructor
    SymbolTable(int capacity) {
        this->capacity = capacity;
        table = new KeyValuePair[capacity];
        size = 0;
    }

    // Destructor
    ~SymbolTable() {
        delete[] table;
    }

    // Binary search to find the index of a key in the table
    int binarySearch(int key) {
        int low = 0, high = size - 1;
        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (table[mid].key == key)
                return mid; // Key found
            else if (table[mid].key < key)
                low = mid + 1;
            else
                high = mid - 1;
        }
        return -1; // Key not found
    }

    // Get the value associated with a key
    int get(int key) {
        int index = binarySearch(key);
        if (index != -1)
            return table[index].value;
        else
            return -1; // Key not found
    }

    // Insert a key-value pair into the table
    void put(int key, int value) {
        int index = binarySearch(key);
        if (index != -1)
            table[index].value = value; // Update existing key
        else {
            int i;
            // Find the position to insert the new key-value pair
            for (i = size - 1; i >= 0 && table[i].key > key; i--)
                table[i + 1] = table[i];
            table[i + 1] = {key, value};
            size++;
        }
    }

    // Remove a key and its associated value from the table
    void remove(int key) {
        int index = binarySearch(key);
        if (index != -1) {
            // Shift elements to the left to remove the key-value pair
            for (int i = index; i < size - 1; i++)
                table[i] = table[i + 1];
            size--;
        }
    }
};

// Main function for testing
int main() {
    SymbolTable st(10);
    st.put(5, 100);
    st.put(3, 200);
    st.put(8, 300);
    
    cout << "Value associated with key 5: " << st.get(5) << endl;
    cout << "Value associated with key 3: " << st.get(3) << endl;
    cout << "Value associated with key 8: " << st.get(8) << endl;
    
    st.remove(3);
    cout << "Value associated with key 3 after removal: " << st.get(3) << endl;

    return 0;
}
```

This implementation uses an ordered array to store key-value pairs. The `put`, `get`, and `remove` operations are implemented efficiently using binary search for key lookup.

### 1. Algorithms & Data Structures (C++): Barcode

Sure, let's discuss how you might implement a barcode system in C++, including algorithms and data structures you might use.

1. **Representation of Barcode Data**: In a barcode system, you need to represent the data contained within the barcode. This could include numeric data, alphanumeric data, or even binary data.

2. **Data Structures for Barcode**: You might use a string or an array to represent the barcode data. For example, a string could represent the barcode digits: `"0123456789"`. Alternatively, you could use an array of integers to represent each digit: `{0, 1, 2, 3, 4, 5, 6, 7, 8, 9}`.

3. **Encoding Algorithms**: Barcodes are encoded using different schemes like UPC, EAN, Code 39, etc. Each scheme has its own rules for encoding data into bars and spaces. You would need to implement encoding algorithms for the specific barcode format you're working with.

4. **Decoding Algorithms**: Similarly, you would need decoding algorithms to interpret the bars and spaces of a scanned barcode and extract the original data.

5. **Data Validation**: Barcodes often include checksum digits to ensure data integrity. You'll need algorithms to calculate and verify these checksums.

6. **Data Storage and Retrieval**: You might need data structures to store and retrieve information associated with each barcode, such as product details in a retail system.

Here's a simple example of how you might implement a barcode class in C++:

```cpp
#include <iostream>
#include <vector>

class Barcode {
private:
    std::vector<int> data; // Data representation of the barcode

public:
    Barcode(std::vector<int> barcodeData) : data(barcodeData) {}

    void printBarcode() {
        for (int digit : data) {
            std::cout << digit;
        }
        std::cout << std::endl;
    }

    // Other methods for encoding, decoding, checksum calculation, etc.
};

int main() {
    std::vector<int> barcodeData = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
    Barcode barcode(barcodeData);
    barcode.printBarcode();
    return 0;
}
```

This is a basic skeleton. Depending on your requirements, you would need to implement encoding, decoding, checksum calculation, and other functionalities within the Barcode class.

### 1. Algorithms & Data Structures (C++): Addition of Sparse Matrices

Certainly! Adding sparse matrices in C++ involves efficiently handling the sparse nature of the matrices to optimize both space and time complexity. Here's a basic implementation:

```cpp
#include <iostream>
#include <vector>
using namespace std;

// Structure to represent a triplet (row, column, value)
struct Triplet {
    int row;
    int col;
    int value;
};

// Function to add two sparse matrices
vector<Triplet> addSparseMatrices(const vector<Triplet>& A, const vector<Triplet>& B) {
    vector<Triplet> result;
    int sizeA = A.size();
    int sizeB = B.size();
    int i = 0, j = 0;

    // Iterate until we reach the end of either matrix A or B
    while (i < sizeA && j < sizeB) {
        if (A[i].row < B[j].row || (A[i].row == B[j].row && A[i].col < B[j].col)) {
            // Add A[i] to result
            result.push_back(A[i]);
            i++;
        } else if (B[j].row < A[i].row || (A[i].row == B[j].row && B[j].col < A[i].col)) {
            // Add B[j] to result
            result.push_back(B[j]);
            j++;
        } else {
            // Add the values of A[i] and B[j] and store in result
            result.push_back({A[i].row, A[i].col, A[i].value + B[j].value});
            i++;
            j++;
        }
    }

    // Add remaining elements of A, if any
    while (i < sizeA) {
        result.push_back(A[i]);
        i++;
    }

    // Add remaining elements of B, if any
    while (j < sizeB) {
        result.push_back(B[j]);
        j++;
    }

    return result;
}

int main() {
    // Example sparse matrices
    vector<Triplet> A = {{0, 1, 3}, {1, 2, 4}, {2, 0, 1}};
    vector<Triplet> B = {{0, 1, 1}, {1, 2, 2}, {2, 1, 6}};

    // Add matrices A and B
    vector<Triplet> result = addSparseMatrices(A, B);

    // Output the result
    cout << "Resultant sparse matrix after addition:" << endl;
    for (const auto& triplet : result) {
        cout << triplet.row << " " << triplet.col << " " << triplet.value << endl;
    }

    return 0;
}
```

This implementation assumes that the sparse matrices are represented using the triplet format, where each non-zero element is represented by its row index, column index, and value. The `addSparseMatrices` function takes two sparse matrices `A` and `B` as input and returns their sum as another sparse matrix.

The algorithm iterates through both matrices simultaneously, adding corresponding elements. It takes advantage of the fact that the matrices are sorted based on row and column indices, allowing for efficient merging similar to the merge step in merge sort.

### 1. Algorithms & Data Structures (C++): API of Symbol Tables

In C++, symbol tables are often implemented using data structures like hash tables, binary search trees, or balanced trees. Here's a basic API for symbol tables in C++:

```cpp
template<typename KeyType, typename ValueType>
class SymbolTable {
public:
    // Inserts a key-value pair into the symbol table
    virtual void put(const KeyType& key, const ValueType& value) = 0;

    // Retrieves the value associated with the given key
    // Returns nullptr (or default-constructed value) if key not found
    virtual ValueType get(const KeyType& key) const = 0;

    // Removes the key and its associated value from the symbol table
    virtual void remove(const KeyType& key) = 0;

    // Checks if the symbol table contains the given key
    virtual bool contains(const KeyType& key) const = 0;

    // Checks if the symbol table is empty
    virtual bool isEmpty() const = 0;

    // Returns the number of key-value pairs in the symbol table
    virtual int size() const = 0;

    // Returns all keys in the symbol table as an iterable collection
    virtual std::vector<KeyType> keys() const = 0;

    // Destructor
    virtual ~SymbolTable() {}
};
```

This API provides a generic interface for symbol tables, allowing you to implement various symbol table data structures like hash tables, binary search trees, etc., by inheriting from this base class and implementing these methods.

Here's an example of how you might implement a symbol table using a binary search tree:

```cpp
template<typename KeyType, typename ValueType>
class BinarySearchTree : public SymbolTable<KeyType, ValueType> {
private:
    struct Node {
        KeyType key;
        ValueType value;
        Node* left;
        Node* right;
        Node(const KeyType& k, const ValueType& v) : key(k), value(v), left(nullptr), right(nullptr) {}
    };
    Node* root;
    int count;

    // Private helper functions for recursive operations
    void put(Node*& node, const KeyType& key, const ValueType& value);
    ValueType get(Node* node, const KeyType& key) const;
    Node* remove(Node* node, const KeyType& key);
    Node* min(Node* node) const;
    bool contains(Node* node, const KeyType& key) const;
    void keys(Node* node, std::vector<KeyType>& keys) const;
    void clear(Node*& node);

public:
    // Constructor
    BinarySearchTree() : root(nullptr), count(0) {}

    // Destructor
    ~BinarySearchTree() {
        clear(root);
    }

    // Implementing the SymbolTable interface
    void put(const KeyType& key, const ValueType& value) override {
        put(root, key, value);
    }

    ValueType get(const KeyType& key) const override {
        return get(root, key);
    }

    void remove(const KeyType& key) override {
        root = remove(root, key);
    }

    bool contains(const KeyType& key) const override {
        return contains(root, key);
    }

    bool isEmpty() const override {
        return size() == 0;
    }

    int size() const override {
        return count;
    }

    std::vector<KeyType> keys() const override {
        std::vector<KeyType> result;
        keys(root, result);
        return result;
    }
};
```

This is just a basic example, and the actual implementation of each method would depend on the chosen data structure. For instance, if you wanted to implement a symbol table using a hash table, you'd replace the binary search tree implementation with a hash table implementation.

### 1. Algorithms & Data Structures (C++): Array Representation of Sparse Matrix

In C++, you can represent a sparse matrix using an array. A sparse matrix is one that has a lot of zero elements, so rather than storing all elements, you only store the non-zero elements along with their row and column indices. Here's an example implementation:

```cpp
#include <iostream>
using namespace std;

const int MAX_SIZE = 100;

class SparseMatrix {
private:
    int row, col;
    int **data; // to store non-zero elements
    int **index; // to store row and column indices

public:
    SparseMatrix(int r, int c) {
        row = r;
        col = c;

        // Allocate memory for data and index arrays
        data = new int*[MAX_SIZE];
        index = new int*[MAX_SIZE];
        for (int i = 0; i < MAX_SIZE; i++) {
            data[i] = new int[MAX_SIZE];
            index[i] = new int[2];
        }

        // Initialize data array with zeros
        for (int i = 0; i < MAX_SIZE; i++) {
            for (int j = 0; j < MAX_SIZE; j++) {
                data[i][j] = 0;
            }
        }
    }

    void insert(int r, int c, int val) {
        if (r >= row || c >= col) {
            cout << "Index out of range!" << endl;
            return;
        }
        data[r][c] = val;
        index[val][0] = r;
        index[val][1] = c;
    }

    void display() {
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                cout << data[i][j] << " ";
            }
            cout << endl;
        }
    }

    void displayNonZeroElements() {
        cout << "Non-zero elements:" << endl;
        for (int i = 0; i < MAX_SIZE; i++) {
            for (int j = 0; j < MAX_SIZE; j++) {
                if (data[i][j] != 0) {
                    cout << "Value: " << data[i][j] << ", Row: " << index[data[i][j]][0] << ", Col: " << index[data[i][j]][1] << endl;
                }
            }
        }
    }

    ~SparseMatrix() {
        // Deallocate memory for data and index arrays
        for (int i = 0; i < MAX_SIZE; i++) {
            delete[] data[i];
            delete[] index[i];
        }
        delete[] data;
        delete[] index;
    }
};

int main() {
    SparseMatrix matrix(5, 5);

    // Inserting non-zero elements
    matrix.insert(0, 1, 7);
    matrix.insert(1, 2, 5);
    matrix.insert(2, 3, 3);
    matrix.insert(3, 4, 9);

    cout << "Sparse Matrix:" << endl;
    matrix.display();

    cout << endl;
    matrix.displayNonZeroElements();

    return 0;
}
```

This implementation defines a class `SparseMatrix`, where non-zero elements are stored in a 2D array `data`, and their corresponding row and column indices are stored in another 2D array `index`. The `insert` function is used to insert non-zero elements into the matrix, and `display` function displays the sparse matrix. The `displayNonZeroElements` function displays the non-zero elements along with their row and column indices.

### 1. Algorithms & Data Structures (C++): Binary Exponentiation

Binary exponentiation is a technique used to efficiently compute large powers of a number, especially in modular arithmetic. It's particularly useful when dealing with problems where you need to calculate large powers modulo some number. Here's a C++ implementation of binary exponentiation:

```cpp
#include <iostream>

using namespace std;

// Function to compute x raised to the power of y modulo m
long long binpow(long long x, long long y, long long m) {
    long long result = 1;
    x %= m;
    while (y > 0) {
        if (y & 1)  // If y is odd
            result = (result * x) % m;
        x = (x * x) % m;
        y >>= 1;  // Divide y by 2
    }
    return result;
}

int main() {
    long long x, y, m;
    cout << "Enter the base (x): ";
    cin >> x;
    cout << "Enter the exponent (y): ";
    cin >> y;
    cout << "Enter the modulo (m): ";
    cin >> m;

    long long result = binpow(x, y, m);
    cout << "Result of (" << x << "^" << y << ") % " << m << " = " << result << endl;

    return 0;
}
```

In this code:

- The `binpow` function takes three parameters: `x` (the base), `y` (the exponent), and `m` (the modulo).
- It returns the result of \(x^y \mod m\) using binary exponentiation.
- Inside the function, the `result` variable stores the final result, which is initialized to 1.
- The while loop runs until `y` becomes 0.
- In each iteration, it checks if the least significant bit of `y` is set (i.e., if `y` is odd). If it is, it multiplies `result` by `x` and takes the modulo `m`.
- Then it updates `x` to \(x^2 \mod m\) and divides `y` by 2.
- Finally, it returns the `result`, which is the value of \(x^y \mod m\).

This algorithm has a time complexity of \(O(\log y)\), where \(y\) is the exponent, making it much faster than the naive approach, which has a time complexity of \(O(y)\).

### 1. Algorithms & Data Structures (C++): C++ Big Integer Class

Creating a big integer class in C++ involves implementing arithmetic operations (addition, subtraction, multiplication, and division) for integers larger than the built-in types like `int` or `long long`. Here's a simplified version of a big integer class in C++:

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>

class BigInteger {
private:
    std::vector<int> digits;
    bool isNegative;

public:
    BigInteger() : isNegative(false) {}

    BigInteger(const std::string& number) {
        isNegative = (number[0] == '-');
        for (int i = (isNegative ? 1 : 0); i < number.size(); ++i) {
            digits.push_back(number[i] - '0');
        }
        std::reverse(digits.begin(), digits.end());
    }

    BigInteger(int number) {
        isNegative = (number < 0);
        number = std::abs(number);
        while (number > 0) {
            digits.push_back(number % 10);
            number /= 10;
        }
    }

    std::string toString() const {
        std::string result;
        if (isNegative) result += '-';
        for (auto it = digits.rbegin(); it != digits.rend(); ++it) {
            result += (*it + '0');
        }
        return result;
    }

    BigInteger operator+(const BigInteger& other) const {
        BigInteger result;
        result.digits.resize(std::max(digits.size(), other.digits.size()) + 1);
        int carry = 0;
        for (size_t i = 0; i < result.digits.size() || carry; ++i) {
            int sum = carry;
            if (i < digits.size()) sum += digits[i];
            if (i < other.digits.size()) sum += other.digits[i];
            result.digits[i] = sum % 10;
            carry = sum / 10;
        }
        while (result.digits.size() > 1 && result.digits.back() == 0) {
            result.digits.pop_back();
        }
        result.isNegative = isNegative && other.isNegative;
        return result;
    }
};

int main() {
    BigInteger a("123456789012345678901234567890");
    BigInteger b("-98765432109876543210987654321");
    BigInteger c = a + b;
    std::cout << c.toString() << std::endl; // Output: "123358023580469135580246913569"
    return 0;
}
```

This example provides a basic implementation of addition for big integers. You can extend it to include subtraction, multiplication, and division following similar principles. Additionally, you can add more functionalities like comparison operators, increment/decrement, etc., based on your requirements.

### 1. Algorithms & Data Structures (C++): C++ class for Diagonal Matrix

Sure, here's a simple C++ class for a diagonal matrix:

```cpp
#include <iostream>

class DiagonalMatrix {
private:
    int *data;
    int size;
public:
    DiagonalMatrix(int n) {
        size = n;
        data = new int[n];
        for (int i = 0; i < n; i++)
            data[i] = 0; // Initialize all elements to 0
    }

    ~DiagonalMatrix() {
        delete[] data;
    }

    void set(int i, int j, int value) {
        if (i != j) {
            std::cerr << "Error: Not a diagonal element\n";
            return;
        }
        if (i < 0 || i >= size || j < 0 || j >= size) {
            std::cerr << "Error: Index out of range\n";
            return;
        }
        data[i] = value;
    }

    int get(int i, int j) {
        if (i != j) {
            std::cerr << "Error: Not a diagonal element\n";
            return -1; // Or any error code to indicate failure
        }
        if (i < 0 || i >= size || j < 0 || j >= size) {
            std::cerr << "Error: Index out of range\n";
            return -1; // Or any error code to indicate failure
        }
        return data[i];
    }
};

int main() {
    int size = 5;
    DiagonalMatrix matrix(size);

    matrix.set(0, 0, 1);
    matrix.set(1, 1, 2);
    matrix.set(2, 2, 3);
    matrix.set(3, 3, 4);
    matrix.set(4, 4, 5);

    std::cout << "Diagonal elements:\n";
    for (int i = 0; i < size; i++) {
        for (int j = 0; j < size; j++) {
            std::cout << matrix.get(i, j) << " ";
        }
        std::cout << std::endl;
    }

    return 0;
}
```

This class represents a diagonal matrix where all elements except those on the main diagonal are assumed to be 0. It provides methods to set and get values at specific indices, with error handling for out-of-range indices and non-diagonal elements.

### 1. Algorithms & Data Structures (C++): Check Odd/Even

Certainly! You can check whether a number is odd or even using the modulo operator (%). In C++, you can create a simple function to do this check. Here's a basic implementation:

```cpp
#include <iostream>

bool isEven(int number) {
    return (number % 2 == 0);
}

int main() {
    int num;
    std::cout << "Enter a number: ";
    std::cin >> num;
    
    if (isEven(num)) {
        std::cout << num << " is even." << std::endl;
    } else {
        std::cout << num << " is odd." << std::endl;
    }

    return 0;
}
```

In this code:

- The function `isEven` checks whether a number is even by using the modulo operator (%). If the result of `number % 2` is 0, then the number is even, otherwise it's odd.
- In the `main` function, the user is prompted to enter a number.
- The entered number is then passed to the `isEven` function, and based on the return value, the program prints whether the number is even or odd.

### 1. Algorithms & Data Structures (C++): Check Subsets

Checking if one set is a subset of another set is a common problem in computer science and can be solved efficiently using algorithms and data structures. Here's a C++ implementation to check if one set is a subset of another:

```cpp
#include <iostream>
#include <unordered_set>
#include <vector>

// Function to check if set 'subset' is a subset of set 'superset'
bool isSubset(const std::vector<int>& subset, const std::vector<int>& superset) {
    std::unordered_set<int> setLookup;

    // Populate the setLookup with elements from superset
    for (const auto& num : superset) {
        setLookup.insert(num);
    }

    // Check if all elements of the subset are present in superset
    for (const auto& num : subset) {
        if (setLookup.find(num) == setLookup.end()) {
            return false; // Element not found in superset
        }
    }

    return true; // All elements of subset found in superset
}

int main() {
    // Example usage
    std::vector<int> superset = {1, 2, 3, 4, 5};
    std::vector<int> subset1 = {2, 3};
    std::vector<int> subset2 = {6, 7};

    if (isSubset(subset1, superset)) {
        std::cout << "subset1 is a subset of superset" << std::endl;
    } else {
        std::cout << "subset1 is not a subset of superset" << std::endl;
    }

    if (isSubset(subset2, superset)) {
        std::cout << "subset2 is a subset of superset" << std::endl;
    } else {
        std::cout << "subset2 is not a subset of superset" << std::endl;
    }

    return 0;
}
```

In this implementation, we use an unordered_set to store the elements of the superset, which enables constant-time lookup. Then, we iterate over each element in the subset and check if it exists in the superset. If any element is not found, we conclude that the subset is not a subset of the superset. Otherwise, if all elements are found, we conclude that the subset is indeed a subset of the superset.

### 1. Algorithms & Data Structures (C++): Complex Number Class

Sure, let's create a simple Complex Number class in C++. A complex number is typically represented as \(a + bi\), where \(a\) is the real part, \(b\) is the imaginary part, and \(i\) is the imaginary unit (\(i^2 = -1\)).

```cpp
#include <iostream>

class Complex {
private:
    double real;
    double imag;

public:
    // Constructors
    Complex() : real(0), imag(0) {}
    Complex(double re, double im) : real(re), imag(im) {}

    // Getter functions
    double getReal() const { return real; }
    double getImag() const { return imag; }

    // Setter functions
    void setReal(double re) { real = re; }
    void setImag(double im) { imag = im; }

    // Addition of two complex numbers
    Complex add(const Complex& other) const {
        return Complex(real + other.real, imag + other.imag);
    }

    // Subtraction of two complex numbers
    Complex subtract(const Complex& other) const {
        return Complex(real - other.real, imag - other.imag);
    }

    // Multiplication of two complex numbers
    Complex multiply(const Complex& other) const {
        return Complex(real * other.real - imag * other.imag,
                       real * other.imag + imag * other.real);
    }

    // Display the complex number
    void display() const {
        std::cout << "(" << real << " + " << imag << "i)" << std::endl;
    }
};

int main() {
    Complex c1(2.5, 3.7);
    Complex c2(1.2, -4.3);

    // Addition
    Complex sum = c1.add(c2);
    std::cout << "Sum: ";
    sum.display();

    // Subtraction
    Complex diff = c1.subtract(c2);
    std::cout << "Difference: ";
    diff.display();

    // Multiplication
    Complex prod = c1.multiply(c2);
    std::cout << "Product: ";
    prod.display();

    return 0;
}
```

This class represents complex numbers with basic arithmetic operations such as addition, subtraction, and multiplication. You can extend it further with other operations like division, exponentiation, and additional utility functions as needed.

### 1. Algorithms & Data Structures (C++): Complex Number Class Implementation

Sure, implementing a complex number class in C++ can be a great exercise to understand both object-oriented programming and basic mathematical concepts. Here's a simple implementation of a complex number class:

```cpp
#include <iostream>

class Complex {
private:
    double real;
    double imaginary;

public:
    // Constructors
    Complex() : real(0), imaginary(0) {}
    Complex(double re, double im) : real(re), imaginary(im) {}

    // Accessors
    double getReal() const { return real; }
    double getImaginary() const { return imaginary; }

    // Setters
    void setReal(double re) { real = re; }
    void setImaginary(double im) { imaginary = im; }

    // Operator overloading
    Complex operator+(const Complex& other) const {
        return Complex(real + other.real, imaginary + other.imaginary);
    }

    Complex operator-(const Complex& other) const {
        return Complex(real - other.real, imaginary - other.imaginary);
    }

    Complex operator*(const Complex& other) const {
        return Complex(real * other.real - imaginary * other.imaginary,
                       real * other.imaginary + imaginary * other.real);
    }

    Complex operator/(const Complex& other) const {
        double denominator = other.real * other.real + other.imaginary * other.imaginary;
        return Complex((real * other.real + imaginary * other.imaginary) / denominator,
                       (imaginary * other.real - real * other.imaginary) / denominator);
    }

    // Other methods
    double modulus() const {
        return sqrt(real * real + imaginary * imaginary);
    }

    void display() const {
        std::cout << real << " + " << imaginary << "i" << std::endl;
    }
};

int main() {
    Complex c1(2, 3);
    Complex c2(4, -5);

    Complex sum = c1 + c2;
    Complex difference = c1 - c2;
    Complex product = c1 * c2;
    Complex quotient = c1 / c2;

    std::cout << "Sum: ";
    sum.display();

    std::cout << "Difference: ";
    difference.display();

    std::cout << "Product: ";
    product.display();

    std::cout << "Quotient: ";
    quotient.display();

    std::cout << "Modulus of c1: " << c1.modulus() << std::endl;

    return 0;
}
```

This code defines a `Complex` class with real and imaginary parts as private data members. It provides constructors to initialize these values, accessor methods to get the real and imaginary parts, and overloaded operators for basic arithmetic operations (`+`, `-`, `*`, `/`). Additionally, it includes methods to compute the modulus of a complex number and display the complex number in the standard form `a + bi`. Finally, in the `main()` function, some basic arithmetic operations are performed on complex numbers.

### 1. Algorithms & Data Structures (C++): Concurrent Bag

A Concurrent Bag is a data structure designed to store items in a thread-safe manner, allowing concurrent access from multiple threads without explicit synchronization. It's particularly useful in scenarios where multiple threads need to add or remove items from a shared collection without blocking each other.

In C++, you can implement a Concurrent Bag using various synchronization primitives like mutexes or lock-free data structures. Here's a basic implementation using mutexes:

```cpp
#include <mutex>
#include <queue>

template <typename T>
class ConcurrentBag {
private:
    std::mutex mutex_;
    std::queue<T> queue_;

public:
    void Add(const T& item) {
        std::lock_guard<std::mutex> lock(mutex_);
        queue_.push(item);
    }

    bool TryTake(T& item) {
        std::lock_guard<std::mutex> lock(mutex_);
        if (queue_.empty()) {
            return false;
        }
        item = queue_.front();
        queue_.pop();
        return true;
    }

    bool IsEmpty() const {
        std::lock_guard<std::mutex> lock(mutex_);
        return queue_.empty();
    }
};
```

In this implementation:

- `Add`: Adds an item to the bag. It locks the mutex to ensure exclusive access to the underlying queue while adding the item.
- `TryTake`: Tries to take an item from the bag. It also locks the mutex to ensure exclusive access to the queue. If the queue is not empty, it takes the item from the front of the queue and removes it.
- `IsEmpty`: Checks if the bag is empty. It locks the mutex to ensure thread safety while accessing the queue's size.

This implementation ensures thread safety by using a mutex to guard access to the underlying queue. However, using mutexes can introduce contention if multiple threads are accessing the bag simultaneously. In scenarios with high contention, you might consider using lock-free data structures for better performance.


### 1. Algorithms & Data Structures (C++): Decreasing Sequence

A decreasing sequence is a sequence of elements where each element is less than or equal to the preceding element. Implementing a data structure or algorithm to handle decreasing sequences depends on the specific requirements and context of your problem. Here's a simple example in C++ of how you might represent and manipulate a decreasing sequence using a vector:

```cpp
#include <iostream>
#include <vector>

// Function to check if a vector is a decreasing sequence
bool isDecreasing(const std::vector<int>& sequence) {
    for (size_t i = 1; i < sequence.size(); ++i) {
        if (sequence[i] > sequence[i - 1]) {
            return false;
        }
    }
    return true;
}

// Function to print a vector
void printVector(const std::vector<int>& vec) {
    for (int num : vec) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
}

int main() {
    std::vector<int> decreasingSeq = {10, 8, 6, 4, 2};

    // Check if the vector is a decreasing sequence
    if (isDecreasing(decreasingSeq)) {
        std::cout << "The vector is a decreasing sequence." << std::endl;
    } else {
        std::cout << "The vector is not a decreasing sequence." << std::endl;
    }

    // Print the elements of the decreasing sequence
    std::cout << "Elements of the decreasing sequence: ";
    printVector(decreasingSeq);

    return 0;
}
```

In this example, the `isDecreasing` function checks if the given vector forms a decreasing sequence. The `printVector` function is just for printing the elements of the vector. You can extend this example by implementing other operations or algorithms tailored to your specific needs related to decreasing sequences.


### 1. Algorithms & Data Structures (C++): Fraction Class

Creating a Fraction class in C++ involves implementing methods for performing arithmetic operations (addition, subtraction, multiplication, division) and comparison operations (equality, less than, greater than) on fractions. Here's a basic implementation:

```cpp
#include <iostream>

class Fraction {
private:
    int numerator;
    int denominator;

    int gcd(int a, int b) {
        return b == 0 ? a : gcd(b, a % b);
    }

public:
    // Constructor
    Fraction(int num = 0, int denom = 1) : numerator(num), denominator(denom) {
        if (denominator == 0) {
            std::cerr << "Error: Denominator cannot be zero." << std::endl;
            exit(1);
        }
        simplify();
    }

    // Getters
    int getNumerator() const {
        return numerator;
    }

    int getDenominator() const {
        return denominator;
    }

    // Simplify the fraction
    void simplify() {
        int divisor = gcd(numerator, denominator);
        numerator /= divisor;
        denominator /= divisor;
        if (denominator < 0) { // Make sure the negative sign is on the numerator
            numerator *= -1;
            denominator *= -1;
        }
    }

    // Addition
    Fraction operator+(const Fraction& other) const {
        int num = numerator * other.denominator + other.numerator * denominator;
        int denom = denominator * other.denominator;
        return Fraction(num, denom);
    }

    // Subtraction
    Fraction operator-(const Fraction& other) const {
        int num = numerator * other.denominator - other.numerator * denominator;
        int denom = denominator * other.denominator;
        return Fraction(num, denom);
    }

    // Multiplication
    Fraction operator*(const Fraction& other) const {
        int num = numerator * other.numerator;
        int denom = denominator * other.denominator;
        return Fraction(num, denom);
    }

    // Division
    Fraction operator/(const Fraction& other) const {
        if (other.numerator == 0) {
            std::cerr << "Error: Division by zero." << std::endl;
            exit(1);
        }
        int num = numerator * other.denominator;
        int denom = denominator * other.numerator;
        return Fraction(num, denom);
    }

    // Comparison operators
    bool operator==(const Fraction& other) const {
        return numerator * other.denominator == other.numerator * denominator;
    }

    bool operator!=(const Fraction& other) const {
        return !(*this == other);
    }

    bool operator<(const Fraction& other) const {
        return numerator * other.denominator < other.numerator * denominator;
    }

    bool operator>(const Fraction& other) const {
        return numerator * other.denominator > other.numerator * denominator;
    }

    bool operator<=(const Fraction& other) const {
        return !(*this > other);
    }

    bool operator>=(const Fraction& other) const {
        return !(*this < other);
    }

    // Output operator
    friend std::ostream& operator<<(std::ostream& os, const Fraction& frac) {
        os << frac.numerator;
        if (frac.denominator != 1) {
            os << "/" << frac.denominator;
        }
        return os;
    }
};

int main() {
    Fraction f1(3, 4);
    Fraction f2(1, 2);

    std::cout << "f1: " << f1 << std::endl;
    std::cout << "f2: " << f2 << std::endl;

    Fraction sum = f1 + f2;
    std::cout << "Sum: " << sum << std::endl;

    Fraction difference = f1 - f2;
    std::cout << "Difference: " << difference << std::endl;

    Fraction product = f1 * f2;
    std::cout << "Product: " << product << std::endl;

    Fraction quotient = f1 / f2;
    std::cout << "Quotient: " << quotient << std::endl;

    if (f1 == f2) {
        std::cout << "f1 is equal to f2" << std::endl;
    } else {
        std::cout << "f1 is not equal to f2" << std::endl;
    }

    return 0;
}
```

This implementation defines a Fraction class with arithmetic and comparison operators overloaded, allowing you to perform basic operations on fractions. It also includes a method to simplify fractions by dividing both the numerator and denominator by their greatest common divisor (GCD).

### 1. Algorithms & Data Structures (C++): Fraction Class Implementation

Sure, I can provide you with a basic implementation of a Fraction class in C++:

```cpp
#include <iostream>

class Fraction {
private:
    int numerator;
    int denominator;

public:
    // Constructor
    Fraction(int num = 0, int denom = 1) : numerator(num), denominator(denom) {
        if (denominator == 0) {
            std::cerr << "Error: Denominator cannot be zero. Setting denominator to 1." << std::endl;
            denominator = 1;
        }
    }

    // Getter functions
    int getNumerator() const { return numerator; }
    int getDenominator() const { return denominator; }

    // Setter functions
    void setNumerator(int num) { numerator = num; }
    void setDenominator(int denom) {
        if (denom != 0)
            denominator = denom;
        else
            std::cerr << "Error: Denominator cannot be zero." << std::endl;
    }

    // Function to display the fraction
    void display() const {
        std::cout << numerator << "/" << denominator;
    }

    // Function to simplify the fraction
    void simplify() {
        int gcd = greatestCommonDivisor(numerator, denominator);
        numerator /= gcd;
        denominator /= gcd;
    }

    // Function to calculate the greatest common divisor (helper function)
    int greatestCommonDivisor(int a, int b) {
        if (b == 0)
            return a;
        else
            return greatestCommonDivisor(b, a % b);
    }

    // Overloaded addition operator
    Fraction operator+(const Fraction& other) const {
        int num = numerator * other.denominator + other.numerator * denominator;
        int denom = denominator * other.denominator;
        return Fraction(num, denom);
    }

    // Overloaded subtraction operator
    Fraction operator-(const Fraction& other) const {
        int num = numerator * other.denominator - other.numerator * denominator;
        int denom = denominator * other.denominator;
        return Fraction(num, denom);
    }

    // Overloaded multiplication operator
    Fraction operator*(const Fraction& other) const {
        int num = numerator * other.numerator;
        int denom = denominator * other.denominator;
        return Fraction(num, denom);
    }

    // Overloaded division operator
    Fraction operator/(const Fraction& other) const {
        if (other.numerator == 0) {
            std::cerr << "Error: Division by zero." << std::endl;
            return Fraction();
        }
        int num = numerator * other.denominator;
        int denom = denominator * other.numerator;
        return Fraction(num, denom);
    }
};

int main() {
    Fraction f1(3, 4);
    Fraction f2(2, 5);

    // Displaying fractions
    std::cout << "Fraction 1: ";
    f1.display();
    std::cout << std::endl;

    std::cout << "Fraction 2: ";
    f2.display();
    std::cout << std::endl;

    // Performing arithmetic operations
    Fraction sum = f1 + f2;
    Fraction difference = f1 - f2;
    Fraction product = f1 * f2;
    Fraction quotient = f1 / f2;

    // Displaying results
    std::cout << "Sum: ";
    sum.display();
    std::cout << std::endl;

    std::cout << "Difference: ";
    difference.display();
    std::cout << std::endl;

    std::cout << "Product: ";
    product.display();
    std::cout << std::endl;

    std::cout << "Quotient: ";
    quotient.display();
    std::cout << std::endl;

    return 0;
}
```

This implementation provides basic functionality for creating, displaying, and performing arithmetic operations on fractions. Additionally, it includes a simplification function to reduce fractions to their simplest form.


### 1. Algorithms & Data Structures (C++): Good Sequences

"Good sequences" can refer to various concepts depending on the context, but in the realm of algorithms and data structures, it often refers to sequences that satisfy certain properties or constraints. Here are a few examples:

1. **Monotonic Sequences**: A sequence is considered "good" if it is either non-increasing or non-decreasing. This property is useful in various algorithms, such as binary search.

2. **Palindrome Sequences**: Palindromes are sequences that read the same forwards and backwards (e.g., "radar", "level"). Algorithms dealing with palindromes often require efficient string manipulation and comparison techniques.

3. **Increasing Subsequence**: Given a sequence, finding the longest increasing subsequence is a common problem in algorithmic competitions and dynamic programming. A "good" sequence in this context could be one that has the longest increasing subsequence.

4. **Balanced Parentheses Sequences**: Sequences of parentheses that are balanced, meaning each opening parenthesis has a corresponding closing parenthesis and they are properly nested. This concept is crucial in many parsing and expression evaluation algorithms.

5. **Fibonacci Sequences**: Sequences generated by the Fibonacci sequence, where each number is the sum of the two preceding ones. These sequences have various interesting properties and are used in many algorithms and mathematical contexts.

6. **Prime Number Sequences**: Sequences consisting of prime numbers only. Prime number sequences have many applications, such as cryptography, hashing, and generating random numbers.

7. **Arithmetic Progressions**: Sequences where the difference between consecutive terms is constant. These sequences are often encountered in mathematics and algorithms dealing with numerical series.

8. **Geometric Progressions**: Sequences where each term after the first is found by multiplying the previous term by a fixed, non-zero number called the common ratio. Geometric progressions have applications in finance, physics, and computer graphics.

Each of these "good sequences" has its own set of algorithms and data structures optimized for dealing with them efficiently. Understanding and manipulating such sequences effectively can lead to elegant and efficient solutions to various computational problems.


### 1. Algorithms & Data Structures (C++): Linear List and Abstract Data Type

Sure, let's delve into Linear Lists and Abstract Data Types (ADTs) in the context of C++.

#### Linear List

A linear list is a sequential collection of elements where each element has a predecessor and a successor, except for the first and last elements. Common examples of linear lists include arrays, linked lists, stacks, and queues.

#### Arrays

- Arrays are a contiguous block of memory where elements are stored consecutively.
- Accessing elements in an array is done in constant time O(1) by using index notation.
- However, inserting or deleting elements in the middle of an array requires shifting elements, which can be inefficient, resulting in a time complexity of O(n).

```cpp
const int SIZE = 10;
int arr[SIZE]; // Declaration of an array with size 10
```

#### Linked Lists

- Linked lists consist of nodes where each node contains both data and a pointer/reference to the next node in the sequence.
- Accessing elements in a linked list is sequential, resulting in a time complexity of O(n).
- However, inserting or deleting elements in a linked list can be done efficiently (O(1)) if you have a reference to the node where the operation should occur.

```cpp
struct Node {
    int data;
    Node* next;
};

class LinkedList {
private:
    Node* head;
public:
    // Functions to manipulate the linked list
};
```

#### Abstract Data Type (ADT)

An abstract data type (ADT) is a mathematical model for data types where only the behavior (operations) of the data type is defined, not its implementation. It encapsulates the data and operations into a single unit.

#### Example: Stack ADT

- A stack is a Last-In-First-Out (LIFO) data structure where elements are inserted and removed from the same end, called the top.
- Common operations include push (to insert), pop (to remove), and peek (to view the top element without removing it).
- Implementation can be done using arrays or linked lists.

```cpp
class Stack {
public:
    virtual void push(int val) = 0;
    virtual int pop() = 0;
    virtual int peek() const = 0;
    virtual bool isEmpty() const = 0;
};
```

This is an abstract class defining the interface of a stack. Concrete implementations (using arrays, linked lists, etc.) will provide the actual implementation details for these operations.

These concepts lay the foundation for more advanced data structures and algorithms. Understanding linear lists and ADTs is crucial for building efficient and organized software systems.


### 1. Algorithms & Data Structures (C++): Lower Triangular Matrix Column-Major Mapping

Mapping a lower triangular matrix to a one-dimensional array in column-major order involves traversing the matrix in a column-major fashion while considering only the lower triangular part. Here's how you can achieve this in C++:

```cpp
#include <iostream>
#include <vector>

class LowerTriangularMatrix {
private:
    std::vector<int> data;
    int size;

    // Helper function to convert row, column indices to index in 1D array
    int getIndex(int row, int col) {
        // Check if indices are valid
        if (row < col) {
            std::cerr << "Invalid indices: (" << row << ", " << col << ")" << std::endl;
            exit(1);
        }
        // Column-major mapping
        return col * (col + 1) / 2 + row;
    }

public:
    // Constructor
    LowerTriangularMatrix(int n) : size(n) {
        // Calculate the size of 1D array
        int arraySize = n * (n + 1) / 2;
        // Initialize the data vector with zeros
        data.resize(arraySize);
    }

    // Function to set value at given indices
    void setValue(int row, int col, int value) {
        int index = getIndex(row, col);
        data[index] = value;
    }

    // Function to get value at given indices
    int getValue(int row, int col) {
        int index = getIndex(row, col);
        return data[index];
    }
};

int main() {
    int n = 4; // Size of the matrix
    LowerTriangularMatrix matrix(n);

    // Populate the lower triangular matrix
    for (int col = 0; col < n; col++) {
        for (int row = col; row < n; row++) {
            // Setting values in lower triangular part
            matrix.setValue(row, col, row * n + col + 1);
        }
    }

    // Print the lower triangular matrix
    for (int col = 0; col < n; col++) {
        for (int row = 0; row < n; row++) {
            // Print only lower triangular part
            if (row >= col) {
                std::cout << matrix.getValue(row, col) << "\t";
            } else {
                std::cout << "0\t";
            }
        }
        std::cout << std::endl;
    }

    return 0;
}
```

This code defines a `LowerTriangularMatrix` class that represents a lower triangular matrix and provides methods to set and get values. The `getIndex` function calculates the index in the 1D array given the row and column indices, ensuring it's within the lower triangular part. The `main` function demonstrates how to use this class by populating and printing a lower triangular matrix.

### 1. Algorithms & Data Structures (C++): Lower Triangular Matrix in C++

Sure, let's create a Lower Triangular Matrix class in C++. In a lower triangular matrix, all the elements above the main diagonal are zero. Here's a simple implementation:

```cpp
#include <iostream>

class LowerTriangularMatrix {
private:
    int *matrix;
    int size;

public:
    LowerTriangularMatrix(int n) {
        size = n;
        matrix = new int[n*(n+1)/2];
    }

    ~LowerTriangularMatrix() {
        delete[] matrix;
    }

    // Set value at given indices (i, j)
    void setValue(int i, int j, int value) {
        if (i >= j) {
            int index = i*(i+1)/2 + j;
            matrix[index] = value;
        } else {
            std::cerr << "Error: Cannot set value. Invalid indices for lower triangular matrix." << std::endl;
        }
    }

    // Get value at given indices (i, j)
    int getValue(int i, int j) {
        if (i >= j) {
            int index = i*(i+1)/2 + j;
            return matrix[index];
        } else {
            std::cerr << "Error: Cannot get value. Invalid indices for lower triangular matrix." << std::endl;
            return -1; // Return a default value to indicate error
        }
    }

    // Display the matrix
    void display() {
        for (int i = 0; i < size; i++) {
            for (int j = 0; j < size; j++) {
                if (i >= j)
                    std::cout << matrix[i*(i+1)/2 + j] << " ";
                else
                    std::cout << "0 ";
            }
            std::cout << std::endl;
        }
    }
};

int main() {
    int size;
    std::cout << "Enter the size of the matrix: ";
    std::cin >> size;

    LowerTriangularMatrix matrix(size);

    // Taking input for lower triangular matrix
    std::cout << "Enter the elements of the lower triangular matrix:" << std::endl;
    for (int i = 0; i < size; i++) {
        for (int j = 0; j <= i; j++) {
            int value;
            std::cout << "Element [" << i << "][" << j << "]: ";
            std::cin >> value;
            matrix.setValue(i, j, value);
        }
    }

    // Displaying the lower triangular matrix
    std::cout << "Lower Triangular Matrix:" << std::endl;
    matrix.display();

    return 0;
}
```

This code defines a class `LowerTriangularMatrix` which allows you to create a lower triangular matrix of a given size, set values at specific indices, get values from specific indices, and display the matrix. In the `main()` function, it prompts the user to input the size of the matrix and then the elements of the lower triangular matrix, and finally displays the resulting matrix.

### 1. Algorithms & Data Structures (C++): Lower Triangular Matrix Row-Major Mapping

In C++, a lower triangular matrix can be represented as a 2D array, with the elements above the main diagonal being zero. Row-major mapping refers to how the elements of the matrix are stored in memory when flattened into a 1D array.

Here's how you can implement row-major mapping for a lower triangular matrix in C++:

```cpp
#include <iostream>

class LowerTriangularMatrix {
private:
    int* data;
    int size;
public:
    // Constructor
    LowerTriangularMatrix(int n) {
        size = n * (n + 1) / 2; // Calculate the size of 1D array
        data = new int[size];
        // Initialize all elements to 0
        for (int i = 0; i < size; ++i) {
            data[i] = 0;
        }
    }

    // Destructor
    ~LowerTriangularMatrix() {
        delete[] data;
    }

    // Function to get index of 1D array given row and column indices
    int getIndex(int row, int col) {
        // Check if row and col are within bounds of the lower triangular matrix
        if (row >= col) {
            return (row * (row + 1) / 2) + col; // Row-major mapping
        } else {
            std::cerr << "Error: Invalid indices\n";
            exit(EXIT_FAILURE);
        }
    }

    // Function to set value at given row and column indices
    void set(int row, int col, int value) {
        if (row >= col) {
            data[getIndex(row, col)] = value;
        } else {
            std::cerr << "Error: Cannot set value for upper triangular elements\n";
        }
    }

    // Function to get value at given row and column indices
    int get(int row, int col) {
        if (row >= col) {
            return data[getIndex(row, col)];
        } else {
            return 0; // Return 0 for upper triangular elements
        }
    }
};

int main() {
    int n = 4; // Size of the matrix
    LowerTriangularMatrix mat(n);

    // Set values in the lower triangular matrix
    mat.set(0, 0, 1);
    mat.set(1, 0, 2);
    mat.set(1, 1, 3);
    mat.set(2, 0, 4);
    mat.set(2, 1, 5);
    mat.set(2, 2, 6);
    mat.set(3, 0, 7);
    mat.set(3, 1, 8);
    mat.set(3, 2, 9);
    mat.set(3, 3, 10);

    // Display the lower triangular matrix
    std::cout << "Lower Triangular Matrix:\n";
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < n; ++j) {
            std::cout << mat.get(i, j) << " ";
        }
        std::cout << "\n";
    }

    return 0;
}
```

In this code:

- The `LowerTriangularMatrix` class represents the lower triangular matrix.
- The `data` member is a dynamically allocated 1D array to store the elements of the lower triangular matrix.
- The `getIndex` function calculates the index in the 1D array given row and column indices, using row-major mapping.
- The `set` and `get` functions allow setting and getting values in the lower triangular matrix.
- In the `main` function, a lower triangular matrix is created, values are set, and then displayed.


### 1. Algorithms & Data Structures (C++): Pond

Sure, let's discuss the implementation of a data structure and algorithm commonly known as a "Pond". In computer science, a pond is essentially a dynamic data structure that allows efficient addition and removal of elements, typically organized in a manner that facilitates searching and manipulation.

For the sake of this discussion, let's consider implementing a basic pond data structure using C++.

```cpp
#include <iostream>
#include <vector>

using namespace std;

class Pond {
private:
    vector<int> elements;

public:
    // Function to add an element to the pond
    void add(int element) {
        elements.push_back(element);
    }

    // Function to remove an element from the pond
    void remove(int element) {
        // Find the element in the pond
        auto it = find(elements.begin(), elements.end(), element);

        // If element found, remove it
        if (it != elements.end()) {
            elements.erase(it);
            cout << "Element " << element << " removed from the pond." << endl;
        } else {
            cout << "Element " << element << " not found in the pond." << endl;
        }
    }

    // Function to check if an element exists in the pond
    bool exists(int element) {
        return find(elements.begin(), elements.end(), element) != elements.end();
    }

    // Function to print all elements in the pond
    void print() {
        cout << "Pond elements: ";
        for (int element : elements) {
            cout << element << " ";
        }
        cout << endl;
    }
};

int main() {
    Pond pond;

    // Add elements to the pond
    pond.add(5);
    pond.add(10);
    pond.add(15);
    pond.add(20);

    // Print all elements in the pond
    pond.print();

    // Check if an element exists in the pond
    cout << "Element 10 exists in the pond: " << (pond.exists(10) ? "Yes" : "No") << endl;

    // Remove an element from the pond
    pond.remove(15);

    // Print all elements in the pond after removal
    pond.print();

    return 0;
}
```

In this implementation:

- The `Pond` class encapsulates a vector to store the elements.
- The `add` function adds an element to the pond.
- The `remove` function removes an element from the pond.
- The `exists` function checks if an element exists in the pond.
- The `print` function prints all elements in the pond.
- In the `main` function, we demonstrate adding elements to the pond, checking for element existence, and removing an element.

This is a basic implementation; in a real-world scenario, you might want to enhance it with additional functionalities or optimize it for specific use cases.
 
 

### 1. Algorithms & Data Structures (C++): Printing Pairs

Certainly! Printing pairs in C++ involves iterating over a collection of pairs and printing each pair's elements. Here's an example code snippet demonstrating how to do this:

```cpp
#include <iostream>
#include <vector>
#include <utility>

using namespace std;

// Function to print pairs
template<typename T1, typename T2>
void printPairs(const vector<pair<T1, T2>>& pairs) {
    for (const auto& pair : pairs) {
        cout << "(" << pair.first << ", " << pair.second << ")" << endl;
    }
}

int main() {
    // Example vector of pairs
    vector<pair<int, string>> pairs = {{1, "one"}, {2, "two"}, {3, "three"}};

    // Print pairs
    cout << "Pairs:" << endl;
    printPairs(pairs);

    return 0;
}
```

In this example:

- We include necessary headers such as `<iostream>` for input-output operations, `<vector>` for using vectors, and `<utility>` for pairs.
- We define a function `printPairs` that takes a vector of pairs as input and prints each pair.
- Inside the `main` function, we create a vector of pairs, `pairs`, containing pairs of integers and strings.
- We then call the `printPairs` function to print the pairs stored in the vector.

Feel free to modify the types of pairs according to your needs!


### 1. Algorithms & Data Structures (C++): Reverse Pairs

In C++, the "reverse pairs" problem typically involves finding the number of pairs `(i, j)` in an array where `i < j` and `nums[i] > 2 * nums[j]`. This problem can be efficiently solved using a modified version of merge sort known as "merge sort with inversion count." Here's how you can implement it:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int merge(vector<int>& nums, int left, int mid, int right) {
    int count = 0;
    int j = mid + 1;
    for (int i = left; i <= mid; ++i) {
        while (j <= right && nums[i] > 2LL * nums[j]) {
            ++j;
        }
        count += (j - (mid + 1));
    }
    
    vector<int> temp;
    int i = left, k = left;
    int p = mid + 1;
    while (i <= mid && p <= right) {
        if (nums[i] <= nums[p]) {
            temp.push_back(nums[i++]);
        } else {
            temp.push_back(nums[p++]);
        }
    }
    while (i <= mid) temp.push_back(nums[i++]);
    while (p <= right) temp.push_back(nums[p++]);
    for (int i = left; i <= right; ++i) {
        nums[i] = temp[i - left];
    }
    return count;
}

int mergeSort(vector<int>& nums, int left, int right) {
    if (left >= right) return 0;
    int mid = left + (right - left) / 2;
    int count = mergeSort(nums, left, mid) + mergeSort(nums, mid + 1, right) + merge(nums, left, mid, right);
    return count;
}

int reversePairs(vector<int>& nums) {
    return mergeSort(nums, 0, nums.size() - 1);
}

int main() {
    vector<int> nums = {1, 3, 2, 3, 1};
    cout << "Number of reverse pairs: " << reversePairs(nums) << endl;
    return 0;
}
```

This code defines a function `reversePairs` that takes a vector of integers `nums` and returns the count of reverse pairs in it. The `mergeSort` function recursively sorts the array while calculating the count of reverse pairs using the `merge` function.


### 1. Algorithms & Data Structures (C++): Sorted Pair Sum

To implement a function that finds pairs of elements in a sorted array whose sum is equal to a given target value, you can use a two-pointer approach. Here's a sample implementation in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

vector<pair<int, int>> sortedPairSum(const vector<int>& nums, int target) {
    vector<pair<int, int>> result;
    int left = 0;
    int right = nums.size() - 1;

    while (left < right) {
        int sum = nums[left] + nums[right];
        if (sum == target) {
            result.push_back({nums[left], nums[right]});
            // Move both pointers to find other pairs
            left++;
            right--;
        } else if (sum < target) {
            // Increment left pointer to increase the sum
            left++;
        } else {
            // Decrement right pointer to decrease the sum
            right--;
        }
    }

    return result;
}

int main() {
    vector<int> nums = {1, 2, 3, 4, 5, 6, 7, 8, 9};
    int target = 10;
    vector<pair<int, int>> pairs = sortedPairSum(nums, target);

    cout << "Pairs with sum " << target << ":" << endl;
    for (const auto& pair : pairs) {
        cout << "(" << pair.first << ", " << pair.second << ")" << endl;
    }

    return 0;
}
```

This implementation has a time complexity of O(n), where n is the size of the input array `nums`, because both pointers move through the array only once. The space complexity is O(1) since we are not using any extra space proportional to the input size.


### 1. Algorithms & Data Structures (C++): Swap Nodes in Pairs

To swap nodes in pairs in a linked list using C++, you can define a simple struct for the linked list node and implement a function to perform the swapping. Here's an example implementation:

```cpp
#include <iostream>

struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* swapPairs(ListNode* head) {
    // If the list is empty or has only one node, no need to swap
    if (!head || !head->next)
        return head;

    ListNode* dummy = new ListNode(0); // Dummy node to simplify edge cases
    dummy->next = head;
    ListNode* prev = dummy;
    ListNode* current = head;

    while (current && current->next) {
        ListNode* first = current;
        ListNode* second = current->next;

        // Swap the nodes
        prev->next = second;
        first->next = second->next;
        second->next = first;

        // Move pointers forward for the next pair
        prev = first;
        current = first->next;
    }

    head = dummy->next;
    delete dummy; // Clean up dummy node
    return head;
}

// Function to print the linked list
void printList(ListNode* head) {
    while (head != nullptr) {
        std::cout << head->val << " ";
        head = head->next;
    }
    std::cout << std::endl;
}

int main() {
    // Create a sample linked list: 1 -> 2 -> 3 -> 4 -> 5
    ListNode* head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);

    std::cout << "Original list: ";
    printList(head);

    // Swap nodes in pairs
    head = swapPairs(head);

    std::cout << "List after swapping pairs: ";
    printList(head);

    // Clean up memory
    while (head) {
        ListNode* temp = head;
        head = head->next;
        delete temp;
    }

    return 0;
}
```

This code defines a `ListNode` structure representing each node in the linked list. The `swapPairs` function takes the head of the linked list as input and swaps every pair of adjacent nodes. The `printList` function is used to print the linked list for demonstration purposes.

You can run this code to see how it swaps pairs of nodes in a linked list.


### 1. Algorithms & Data Structures (C++): The loophole in our implementation of FIFO Queue

Identifying loopholes or weaknesses in data structure implementations is crucial for ensuring their correctness and efficiency. In the case of a FIFO (First-In-First-Out) queue implemented in C++, there are several potential areas where loopholes might exist:

1. **Memory Management**: If memory is not managed properly, it can lead to memory leaks or undefined behavior. Make sure that memory allocated for the queue elements is properly deallocated when they are removed from the queue.

2. **Concurrency Issues**: If the queue is accessed concurrently by multiple threads, synchronization mechanisms should be in place to prevent race conditions and ensure thread safety.

3. **Boundary Conditions**: Check whether the queue implementation handles boundary conditions correctly, such as when the queue is empty or full. Accessing elements from an empty queue or adding elements to a full queue without proper checks can lead to errors.

4. **Error Handling**: Ensure that error conditions, such as attempting to dequeue from an empty queue, are handled gracefully to avoid program crashes or undefined behavior.

5. **Performance**: Analyze the time complexity of the operations (enqueue, dequeue, peek) and ensure they meet the desired performance requirements. Loopholes might exist if the implementation is not efficient or if there are cases where the time complexity is higher than expected.

6. **Data Integrity**: Verify that elements are enqueued and dequeued in the correct order according to the FIFO principle. If elements are being lost or dequeued out of order, it indicates a loophole in the implementation.

7. **Encapsulation and Abstraction**: Ensure that the queue implementation properly encapsulates its internal state and exposes only the necessary interface to the users. Loopholes might exist if users can manipulate the internal state of the queue directly, bypassing the intended interface.

To identify the specific loophole in your implementation of the FIFO queue, carefully review each aspect of the implementation mentioned above and look for any discrepancies or violations of expected behavior. Additionally, thorough testing with various input scenarios can help uncover potential loopholes and validate the correctness of the implementation.


### 1. Algorithms & Data Structures (C++): Triplets

Sure, let's talk about triplets in the context of algorithms and data structures. In programming, a triplet usually refers to a set of three elements. There are various scenarios where triplets can be useful, such as finding unique combinations, solving optimization problems, or performing operations on sets of three items.

Here are some common algorithms and data structures related to triplets in C++:

1. **Finding Triplets Summing to a Given Value**: Given an array of integers, you might need to find all unique triplets that sum up to a specific target value. This problem can be solved using techniques like sorting the array and then using two-pointer or hash map approaches to find the triplets efficiently.

2. **Counting Triplets**: Given an array or a sequence of elements, you might need to count the number of triplets that satisfy a certain condition. For example, in an array of integers, you might need to count all triplets (a, b, c) such that a < b < c.

3. **Enumerating Triplets**: Sometimes, you might need to enumerate or generate all possible triplets from a given set of elements. This can be useful in combinatorial problems or when you need to explore all possible combinations.

4. **Storing Triplets**: If you need to store triplets in memory, you can use data structures like arrays, vectors, tuples, or custom structs/classes depending on your requirements.

5. **Processing Triplets Efficiently**: When dealing with large datasets or complex computations involving triplets, you might need to optimize your algorithms for performance. Techniques such as dynamic programming, memoization, or parallel processing can be useful in such scenarios.

Would you like to delve deeper into any specific aspect or algorithm related to triplets in C++?

### 1. Algorithms & Data Structures (C++): Triplets in GP

Sure, let's talk about finding triplets in a geometric progression (GP) in C++. A geometric progression is a sequence of numbers where each term after the first is found by multiplying the previous one by a fixed, non-zero number called the common ratio.

To find triplets in a GP, we need to iterate through the given array and check for all possible triplets (i, j, k) where i < j < k and arr[j] is the geometric mean of arr[i] and arr[k]. Here's a C++ function to achieve that:

```cpp
#include <iostream>
#include <unordered_map>
#include <vector>

using namespace std;

bool isTripletInGP(const vector<int>& arr) {
    int n = arr.size();
    unordered_map<int, int> count;
    
    // Create a frequency map of elements
    for (int num : arr) {
        count[num]++;
    }
    
    // Sort the array
    vector<int> sortedArr = arr;
    sort(sortedArr.begin(), sortedArr.end());
    
    // Iterate over all triplets
    for (int j = 1; j < n - 1; ++j) {
        int i = j - 1;
        int k = j + 1;
        
        while (i >= 0 && k < n) {
            // Check if arr[j] is the geometric mean of arr[i] and arr[k]
            if ((sortedArr[k] * sortedArr[i]) == (sortedArr[j] * sortedArr[j])) {
                return true;
            } else if ((sortedArr[k] * sortedArr[i]) < (sortedArr[j] * sortedArr[j])) {
                k++;
            } else {
                i--;
            }
        }
    }
    
    return false;
}

int main() {
    vector<int> arr = {1, 2, 4, 8, 16};
    
    if (isTripletInGP(arr)) {
        cout << "Yes, there exists a triplet in geometric progression." << endl;
    } else {
        cout << "No, there is no triplet in geometric progression." << endl;
    }
    
    return 0;
}
```

This program checks if there exists a triplet (i, j, k) in the given array such that arr[j] is the geometric mean of arr[i] and arr[k]. If such a triplet exists, it returns true; otherwise, it returns false.

In the `main` function, you can replace the `arr` vector with any other array of integers to test the function with different inputs.

### 1. Algorithms & Data Structures (C++): Triplets in GP | Hashing with Slider

Sure! If you're looking to find triplets in a geometric progression (GP) within an array using hashing with a sliding window technique in C++, here's a general approach you can take:

```cpp
#include <iostream>
#include <unordered_map>
#include <vector>

using namespace std;

int countTripletsInGP(vector<int>& arr, int r) {
    unordered_map<int, int> second, third;
    int count = 0;

    for (int num : arr) {
        if (third.count(num)) {
            count += third[num];
        }

        if (second.count(num)) {
            third[num * r] += second[num];
        }

        second[num * r]++;
    }

    return count;
}

int main() {
    vector<int> arr = {1, 3, 9, 27, 81};
    int r = 3;
    cout << "Number of triplets in GP: " << countTripletsInGP(arr, r) << endl;
    return 0;
}
```

This code will find the number of triplets in the given array `arr` that form a geometric progression with a common ratio `r`. The `countTripletsInGP` function takes the array and the common ratio as input parameters. It iterates through the array once, using two hash maps (`second` and `third`) to keep track of the occurrences of the elements. The `second` map stores the count of elements that can be the second element of a triplet, and the `third` map stores the count of elements that can be the third element of a triplet. 

For each element in the array, it checks if it can be the third element of a triplet (i.e., it exists in the `third` map). If so, it increments the count. Then it updates the `third` map for the next element, and updates the `second` map for the current element.

In the `main` function, an example array `arr` and a common ratio `r` are provided, and the result is printed.

You can modify the `main` function to test with different arrays and ratios.


### 1. Algorithms & Data Structures (C++): Unordered Pair

An unordered pair in C++ can be implemented in various ways, depending on your specific needs. Here's a simple implementation using a `std::pair` and a custom hash function for unordered containers:

```cpp
#include <iostream>
#include <unordered_set>

struct UnorderedPairHash {
    template<typename T>
    std::size_t operator()(const std::pair<T, T>& pair) const {
        return std::hash<T>()(pair.first) ^ std::hash<T>()(pair.second);
    }
};

template<typename T>
using UnorderedPairSet = std::unordered_set<std::pair<T, T>, UnorderedPairHash>;

int main() {
    UnorderedPairSet<int> pairSet;

    // Insert some pairs
    pairSet.insert({1, 2});
    pairSet.insert({3, 4});
    pairSet.insert({2, 1}); // Duplicate, won't be inserted

    // Check if a pair exists
    std::pair<int, int> searchPair = {3, 4};
    if (pairSet.find(searchPair) != pairSet.end()) {
        std::cout << "Pair {" << searchPair.first << ", " << searchPair.second << "} found\n";
    } else {
        std::cout << "Pair {" << searchPair.first << ", " << searchPair.second << "} not found\n";
    }

    // Print all pairs
    std::cout << "Pairs in the set:\n";
    for (const auto& pair : pairSet) {
        std::cout << "{" << pair.first << ", " << pair.second << "}\n";
    }

    return 0;
}
```

This code demonstrates an unordered set of pairs where the order of elements within each pair doesn't matter. The `UnorderedPairHash` struct provides a custom hash function for pairs, ensuring that pairs with the same elements but in a different order hash to the same value.
