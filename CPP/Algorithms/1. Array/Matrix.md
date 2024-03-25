
### 1. Algorithms & Data Structures (C++): Matrices

Matrices are fundamental mathematical structures used in various fields, including computer science and engineering. In the context of algorithms and data structures, matrices can be represented and manipulated efficiently using C++. Here's a brief overview of how matrices can be implemented and some common operations performed on them:

#### Matrix Representation

In C++, matrices are typically represented using multi-dimensional arrays or nested vectors. Here's how you can declare a matrix using these two approaches:

```cpp
// Using multi-dimensional arrays
const int ROWS = 3;
const int COLS = 3;
int matrix[ROWS][COLS];

// Using nested vectors
#include <vector>
using namespace std;
vector<vector<int>> matrix(ROWS, vector<int>(COLS));
```

#### Matrix Operations

1. **Matrix Addition:**

   ```cpp
   vector<vector<int>> addMatrices(const vector<vector<int>>& A, const vector<vector<int>>& B) {
       int rows = A.size();
       int cols = A[0].size();
       vector<vector<int>> result(rows, vector<int>(cols));
       for (int i = 0; i < rows; ++i) {
           for (int j = 0; j < cols; ++j) {
               result[i][j] = A[i][j] + B[i][j];
           }
       }
       return result;
   }
   ```

2. **Matrix Multiplication:**

   ```cpp
   vector<vector<int>> multiplyMatrices(const vector<vector<int>>& A, const vector<vector<int>>& B) {
       int rowsA = A.size();
       int colsA = A[0].size();
       int colsB = B[0].size();
       vector<vector<int>> result(rowsA, vector<int>(colsB, 0));
       for (int i = 0; i < rowsA; ++i) {
           for (int j = 0; j < colsB; ++j) {
               for (int k = 0; k < colsA; ++k) {
                   result[i][j] += A[i][k] * B[k][j];
               }
           }
       }
       return result;
   }
   ```

3. **Matrix Transposition:**

   ```cpp
   vector<vector<int>> transposeMatrix(const vector<vector<int>>& A) {
       int rows = A.size();
       int cols = A[0].size();
       vector<vector<int>> result(cols, vector<int>(rows));
       for (int i = 0; i < rows; ++i) {
           for (int j = 0; j < cols; ++j) {
               result[j][i] = A[i][j];
           }
       }
       return result;
   }
   ```

These are just basic operations, but matrices can be used in many more complex algorithms and data structures such as graph algorithms, linear algebra, and image processing. Understanding how to efficiently manipulate matrices is crucial for various computational tasks.

### 1. Algorithms & Data Structures (C++): Matrix Chain Multiplication

Matrix Chain Multiplication is a classic problem in computer science and algorithm design. It involves finding the most efficient way to multiply a series of matrices together. The goal is to minimize the total number of scalar multiplications required to compute the product.

Here's a brief overview of the problem and a dynamic programming approach to solve it in C++:

```cpp
#include <iostream>
#include <climits>

using namespace std;

// Function to find the minimum number of scalar multiplications needed
// to multiply matrices from i to j (both inclusive).
int matrixChainOrder(int p[], int n) {
    // Create a table to store the minimum number of multiplications
    // needed for each sub-problem. table[i][j] will store the minimum
    // number of scalar multiplications needed to compute the product
    // of matrices from i to j.
    int table[n][n];
    
    // Initialize the table with 0 as cost for multiplying one matrix.
    for (int i = 0; i < n; i++)
        table[i][i] = 0;

    // 'l' is the chain length.
    for (int l = 2; l < n; l++) {
        for (int i = 1; i <= n - l + 1; i++) {
            int j = i + l - 1;
            table[i][j] = INT_MAX;
            for (int k = i; k < j; k++) {
                // Calculate the cost of multiplying matrices from i to j,
                // where the matrices are split at position k.
                int cost = table[i][k] + table[k + 1][j] + p[i - 1] * p[k] * p[j];
                if (cost < table[i][j])
                    table[i][j] = cost;
            }
        }
    }
    // Return the minimum number of scalar multiplications needed to
    // compute the product of matrices from 1 to n.
    return table[1][n - 1];
}

int main() {
    int arr[] = {10, 20, 30, 40, 30};
    int size = sizeof(arr) / sizeof(arr[0]);
    cout << "Minimum number of scalar multiplications needed: "
         << matrixChainOrder(arr, size) << endl;
    return 0;
}
```

In this code:

- `matrixChainOrder` function calculates the minimum number of scalar multiplications needed to multiply a series of matrices using dynamic programming.
- `p[]` is an array of integers representing the dimensions of the matrices. For example, if `p[] = {10, 20, 30}`, it means there are two matrices, one with dimensions 10x20 and the other with dimensions 20x30.
- The `table` array stores the minimum number of scalar multiplications needed to compute the product of matrices from `i` to `j`.
- The code iterates through different chain lengths and calculates the cost of multiplying matrices at different positions to find the minimum cost.
- The result is then returned, representing the minimum number of scalar multiplications needed to compute the product of matrices from 1 to `n`.

This algorithm has a time complexity of O(n^3), where n is the number of matrices.

### 1. Algorithms & Data Structures (C++): Matrix chain problem (problem)

The Matrix Chain Multiplication problem is a classic problem in dynamic programming. The problem is as follows:

Given a sequence of matrices, you need to find the most efficient way to multiply these matrices together. Matrix multiplication is associative but not commutative, so the order in which you multiply matrices affects the number of scalar multiplications needed and thus the total cost.

For example, let's say you have three matrices A, B, and C with dimensions:

- A: 10x30
- B: 30x5
- C: 5x60

If you multiply them as (A * B) * C, then the total cost would be \(10*30*5 + 10*5*60 = 1500 + 3000 = 4500\) scalar multiplications.

However, if you multiply them as A * (B * C), then the total cost would be \(30*5*60 + 10*30*60 = 9000 + 18000 = 27000\) scalar multiplications.

The goal is to find the order of multiplication that minimizes the total cost.

This problem can be solved using dynamic programming. The dynamic programming approach involves breaking down the problem into smaller subproblems and storing the solutions to these subproblems in a table to avoid redundant computations.

The steps for solving the Matrix Chain Multiplication problem using dynamic programming are:

1. Define a table to store the minimum cost of multiplying matrices of various sizes.
2. Initialize the table with appropriate values for the base cases (e.g., single matrix).
3. Use a nested loop to iterate over all possible subchains of matrices, computing the cost of multiplying each subchain and storing the minimum cost in the table.
4. Finally, use the table to reconstruct the optimal order of multiplication.

The time complexity of this dynamic programming approach is O(n^3), where n is the number of matrices in the sequence.

Do you need help with implementing this algorithm in C++?

### 1. Algorithms & Data Structures (C++): Matrix chain problem (solution)

The Matrix Chain Multiplication problem is a classic problem in dynamic programming where the goal is to find the most efficient way to multiply a chain of matrices together. The objective is to minimize the number of scalar multiplications needed to compute the product.

Here's a solution in C++ using dynamic programming to solve the Matrix Chain Multiplication problem:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to find the minimum number of scalar multiplications needed to multiply a chain of matrices
int matrixChainOrder(const vector<int>& dims) {
    int n = dims.size(); // Number of matrices

    // Create a table to store the minimum number of scalar multiplications needed for each subchain
    vector<vector<int>> dp(n, vector<int>(n, 0));

    // Fill the dp table in bottom-up manner
    for (int len = 2; len < n; ++len) {
        for (int i = 1; i < n - len + 1; ++i) {
            int j = i + len - 1;
            dp[i][j] = INT_MAX;
            for (int k = i; k <= j - 1; ++k) {
                int cost = dp[i][k] + dp[k + 1][j] + dims[i - 1] * dims[k] * dims[j];
                if (cost < dp[i][j])
                    dp[i][j] = cost;
            }
        }
    }

    // The result is stored in dp[1][n-1], where 1 and n-1 represent the starting and ending index of the chain
    return dp[1][n - 1];
}

int main() {
    // Dimensions of matrices in the chain
    vector<int> dims = {10, 30, 5, 60};
    
    // Calculate the minimum number of scalar multiplications
    int minMultiplications = matrixChainOrder(dims);
    
    // Output the result
    cout << "Minimum number of scalar multiplications: " << minMultiplications << endl;

    return 0;
}
```

This solution uses dynamic programming to build a table `dp[][]`, where `dp[i][j]` represents the minimum number of scalar multiplications needed to compute the matrix chain starting from `i` to `j`. The solution fills this table bottom-up by considering all possible splits of the matrix chain and choosing the split that minimizes the number of scalar multiplications. Finally, the minimum number of scalar multiplications needed to multiply the entire chain is stored in `dp[1][n-1]`, where `n` is the number of matrices in the chain.

### 1. Algorithms & Data Structures (C++): Matrix Exponentiation

Matrix exponentiation is a powerful technique used in various algorithms, particularly in dynamic programming and number theory, to efficiently compute the power of a matrix. It's commonly used in problems involving recurrence relations, such as Fibonacci numbers, and in solving linear homogeneous recurrence relations with constant coefficients.

Here's a basic outline of how matrix exponentiation works in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

typedef vector<vector<long long>> Matrix;

// Function to multiply two matrices
Matrix multiply(const Matrix &a, const Matrix &b) {
    int n = a.size();
    int m = b[0].size();
    int p = a[0].size();
    Matrix result(n, vector<long long>(m, 0));
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < m; ++j) {
            for (int k = 0; k < p; ++k) {
                result[i][j] += a[i][k] * b[k][j];
            }
        }
    }
    return result;
}

// Function to raise a matrix to power n
Matrix power(const Matrix &base, int n) {
    int m = base.size();
    Matrix result(m, vector<long long>(m, 0));
    for (int i = 0; i < m; ++i) {
        result[i][i] = 1; // Initialize result to identity matrix
    }
    Matrix temp = base;
    while (n > 0) {
        if (n & 1) {
            result = multiply(result, temp); // If n is odd, multiply result with base
        }
        temp = multiply(temp, temp); // Square the base
        n >>= 1;
    }
    return result;
}

int main() {
    // Example usage
    Matrix base = {{1, 1}, {1, 0}}; // Fibonacci matrix
    int n = 10; // Compute Fibonacci(10)
    Matrix result = power(base, n);
    cout << "Fibonacci(" << n << ") is: " << result[0][1] << endl;
    return 0;
}
```

This code defines two functions: `multiply()` to multiply two matrices, and `power()` to compute the power of a matrix. The `power()` function uses binary exponentiation to efficiently compute the result.

You can customize the matrix type and operations according to your specific problem requirements. Matrix exponentiation is incredibly versatile and can be applied to a wide range of problems in algorithm design.

### 1. Algorithms & Data Structures (C++): Matrix Exponentiation and Dynamic Programming

Matrix exponentiation and dynamic programming are powerful techniques used in algorithm design and optimization, particularly in solving problems related to combinatorics, graph theory, and optimization. Let's delve into each of these techniques in the context of C++.

#### Matrix Exponentiation

Matrix exponentiation is a technique used to efficiently compute the power of a square matrix. It's particularly useful in problems where you need to compute the nth term of a linear recurrence relation or solve certain types of dynamic programming problems efficiently.

Here's a high-level overview of how matrix exponentiation works:

1. **Define the matrix**: Identify the matrix representation of the problem. For example, if you're dealing with a linear recurrence relation, the matrix might represent the coefficients of the recurrence relation.

2. **Express the problem as a matrix power**: Convert the problem into a matrix power problem. For instance, if you're trying to find the nth term of a sequence, represent it as the nth power of the transition matrix.

3. **Compute the matrix power efficiently**: Use techniques like exponentiation by squaring to compute the nth power of the matrix efficiently in O(log n) time.

4. **Extract the result**: Once you have the nth power of the matrix, extract the desired result from it. This might involve extracting specific elements from the resulting matrix depending on the problem.

Here's a basic implementation of matrix exponentiation in C++:

```cpp
#include <iostream>
#include <vector>
using namespace std;

typedef vector<vector<int>> Matrix;

Matrix multiply(const Matrix &a, const Matrix &b) {
    int n = a.size();
    int m = b[0].size();
    int p = a[0].size();
    Matrix c(n, vector<int>(m, 0));
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < m; ++j) {
            for (int k = 0; k < p; ++k) {
                c[i][j] += a[i][k] * b[k][j];
            }
        }
    }
    return c;
}

Matrix power(const Matrix &base, int exponent) {
    int n = base.size();
    Matrix result(n, vector<int>(n, 0));
    for (int i = 0; i < n; ++i) {
        result[i][i] = 1; // Initialize result to identity matrix
    }
    Matrix A = base;
    while (exponent > 0) {
        if (exponent % 2 == 1) {
            result = multiply(result, A);
        }
        A = multiply(A, A);
        exponent /= 2;
    }
    return result;
}

int main() {
    // Example usage
    Matrix base = {{1, 1}, {1, 0}}; // Fibonacci sequence matrix
    int exponent = 5;
    Matrix result = power(base, exponent);
    cout << "Fibonacci(5) = " << result[0][1] << endl; // Output: 5
    return 0;
}
```

This code demonstrates how to use matrix exponentiation to efficiently compute Fibonacci numbers.

#### Dynamic Programming

Dynamic programming is a method for solving complex problems by breaking them down into simpler subproblems and solving each subproblem only once, storing their solutions to avoid redundant computations. It's especially useful for optimization problems and combinatorial problems.

Here's a general approach to dynamic programming:

1. **Identify the problem structure**: Understand the problem and identify the recursive structure of its solution. Determine the parameters that define the subproblems.

2. **Define the recurrence relation**: Formulate a recurrence relation that expresses the solution to the problem in terms of solutions to its subproblems.

3. **Memoization or bottom-up approach**: Implement the solution using either memoization (top-down approach) or a bottom-up approach. In memoization, you store the solutions to subproblems in a table to avoid redundant computations. In the bottom-up approach, you iteratively compute the solutions to subproblems in a bottom-up manner.

4. **Return the solution**: Once you've computed the solution to the original problem, return it.

Here's a simple example of dynamic programming in C++ to compute the nth Fibonacci number:

```cpp
#include <iostream>
#include <vector>
using namespace std;

int fibonacci(int n) {
    vector<int> dp(n + 1, 0);
    dp[0] = 0;
    dp[1] = 1;
    for (int i = 2; i <= n; ++i) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    return dp[n];
}

int main() {
    int n = 5; // Example: compute Fibonacci(5)
    cout << "Fibonacci(5) = " << fibonacci(n) << endl; // Output: 5
    return 0;
}
```

This code demonstrates how to use dynamic programming to efficiently compute Fibonacci numbers. The time complexity of this approach is O(n).

### 1. Algorithms & Data Structures (C++): Matrix Exponentiation and Dynamic Programming: Binary Exponentiation

Binary exponentiation, also known as exponentiation by squaring, is a technique to efficiently compute large powers of a number using logarithmic time complexity. It's commonly used in various algorithms, including matrix exponentiation. Here's how it works:

Given a base `a` and an exponent `n`, the goal is to compute \( a^n \).

The algorithm proceeds as follows:

1. Start with the result `result` initialized to 1.
2. Loop until the exponent `n` becomes zero:
   - If the least significant bit of `n` is 1 (i.e., `n % 2 == 1`), multiply `result` by `a`.
   - Square `a`.
   - Right-shift `n` by 1 (i.e., `n = n / 2`).
3. Return the final result.

Here's the implementation of binary exponentiation in C++:

```cpp
long long binaryExponentiation(long long base, long long exponent) {
    long long result = 1;
    while (exponent > 0) {
        if (exponent & 1) // If exponent is odd
            result *= base;
        base *= base; // Square the base
        exponent >>= 1; // Right shift the exponent by 1
    }
    return result;
}
```

You can use this function to efficiently compute large powers of a number. For example:

```cpp
#include <iostream>

int main() {
    long long base = 2;
    long long exponent = 10;
    long long result = binaryExponentiation(base, exponent);
    std::cout << base << "^" << exponent << " = " << result << std::endl;
    return 0;
}
```

This will output: `2^10 = 1024`.

### 1. Algorithms & Data Structures (C++): Matrix Exponentiation and Dynamic Programming: Fast Multiplication

Matrix exponentiation and dynamic programming are powerful techniques used in algorithm design and optimization. When combined, they can lead to efficient solutions for various computational problems. One common application is fast multiplication of matrices using exponentiation.

Here's how it works:

1. **Matrix Representation**: In C++, matrices can be represented using 2D arrays or vectors of vectors.

2. **Matrix Multiplication**: The standard matrix multiplication algorithm has a time complexity of O(n^3) for two n × n matrices. However, by using matrix exponentiation, we can reduce the time complexity significantly for multiplying a matrix with itself multiple times.

3. **Exponentiation by Squaring**: This is a technique to efficiently compute the power of a matrix. Instead of multiplying the matrix with itself repeatedly, we use a divide-and-conquer approach to reduce the number of multiplications needed.

Here's a basic implementation in C++:

```cpp
#include <vector>

using namespace std;

// Define a matrix type
typedef vector<vector<long long>> Matrix;

// Function to multiply two matrices
Matrix multiply(const Matrix& a, const Matrix& b) {
    int n = a.size();
    Matrix c(n, vector<long long>(n, 0));
    for (int i = 0; i < n; ++i)
        for (int j = 0; j < n; ++j)
            for (int k = 0; k < n; ++k)
                c[i][j] += a[i][k] * b[k][j];
    return c;
}

// Function for fast matrix exponentiation
Matrix matrix_power(const Matrix& base, long long exp) {
    int n = base.size();
    Matrix result(n, vector<long long>(n, 0));
    // Initialize result matrix as identity matrix
    for (int i = 0; i < n; ++i)
        result[i][i] = 1;

    Matrix temp = base;
    while (exp > 0) {
        if (exp % 2 == 1)
            result = multiply(result, temp);
        temp = multiply(temp, temp);
        exp /= 2;
    }
    return result;
}

int main() {
    // Example usage
    Matrix base = {{1, 1}, {1, 0}}; // Fibonacci matrix
    long long exponent = 5;
    Matrix result = matrix_power(base, exponent);
    // Output the result
    for (const auto& row : result) {
        for (long long element : row) {
            cout << element << " ";
        }
        cout << endl;
    }
    return 0;
}
```

In this implementation:

- `multiply` function computes the product of two matrices.
- `matrix_power` function calculates the power of a matrix using exponentiation by squaring.
- `main` function demonstrates how to use `matrix_power` to compute the nth power of a matrix.

This approach significantly reduces the time complexity for computing powers of matrices, making it particularly useful in problems that require repeated matrix multiplication.

### 1. Algorithms & Data Structures (C++): Matrix Exponentiation and Dynamic Programming: Fibosum (spoj)

Certainly! The problem "Fibosum" on SPOJ involves a combination of matrix exponentiation and dynamic programming to efficiently compute the sum of Fibonacci numbers in a given range. Let's break down the problem and outline the approach to solve it:

#### Problem Statement

Given two integers \( A \) and \( B \), you need to find the sum of Fibonacci numbers between the \( A \)th and \( B \)th Fibonacci numbers (inclusive).

#### Approach

1. **Calculate Fibonacci Numbers**: We need a way to efficiently calculate Fibonacci numbers. One common method is to use matrix exponentiation to compute Fibonacci numbers in logarithmic time.

2. **Compute Prefix Sum of Fibonacci Numbers**: Once we have a fast way to calculate Fibonacci numbers, we can use dynamic programming to compute the prefix sum of Fibonacci numbers up to a certain index. This will enable us to find the sum of Fibonacci numbers in a given range efficiently.

3. **Prefix Sum**: Let's denote the prefix sum array as \( F \), where \( F[i] \) represents the sum of Fibonacci numbers from 1st to \( i \)th Fibonacci number.

4. **Compute Answer**: With the prefix sum array, we can easily compute the sum of Fibonacci numbers between \( A \) and \( B \) as \( F[B+2] - F[A+1] \).

#### Implementation Steps

1. Calculate Fibonacci numbers using matrix exponentiation.
2. Compute prefix sum of Fibonacci numbers.
3. Calculate the sum of Fibonacci numbers between \( A \) and \( B \) using the prefix sum array.

#### Code (C++)

```cpp
#include <iostream>
#include <vector>
using namespace std;

typedef vector<vector<long long>> Matrix;

Matrix multiply(const Matrix &a, const Matrix &b) {
    int n = a.size();
    Matrix c(n, vector<long long>(n));
    for (int i = 0; i < n; ++i)
        for (int j = 0; j < n; ++j)
            for (int k = 0; k < n; ++k)
                c[i][j] = (c[i][j] + a[i][k] * b[k][j]) % 1000000007;
    return c;
}

Matrix power(const Matrix &a, long long n) {
    if (n == 1) return a;
    if (n % 2 == 1) return multiply(a, power(a, n - 1));
    Matrix half = power(a, n / 2);
    return multiply(half, half);
}

long long fib(int n) {
    if (n <= 1) return n;
    Matrix T = {{1, 1}, {1, 0}};
    T = power(T, n - 1);
    return T[0][0];
}

int main() {
    int t;
    cin >> t;
    while (t--) {
        int a, b;
        cin >> a >> b;
        long long prefixSumB = fib(b + 2);
        long long prefixSumA = fib(a + 1);
        long long result = (prefixSumB - prefixSumA + 1000000007) % 1000000007;
        cout << result << endl;
    }
    return 0;
}
```

This code calculates the sum of Fibonacci numbers between \( A \) and \( B \) for each test case and prints the result. It uses matrix exponentiation to compute Fibonacci numbers efficiently and then calculates the prefix sum to get the final answer. Make sure to handle modulo operations properly to avoid overflow issues.

### 1. Algorithms & Data Structures (C++): Matrix Exponentiation and Dynamic Programming: Matrix Exponentiation

Matrix exponentiation is a powerful technique used in algorithms to efficiently compute the power of a matrix. It's particularly useful in solving various problems in dynamic programming, combinatorics, graph theory, and more.

Here's a basic overview of matrix exponentiation:

#### Matrix Exponentiation Technique

1. **Basic Idea**: Given a square matrix A and a non-negative integer k, compute \( A^k \) efficiently.

2. **Naive Approach**: The naïve approach involves multiplying the matrix A with itself k times, which is not efficient and takes O(n^3 * k) time, where n is the dimension of the matrix.

3. **Optimized Approach (Matrix Exponentiation)**:
   - Utilizes the concept of divide and conquer.
   - Exploits the property of exponentiation: \( A^{2k} = (A^k)^2 \) and \( A^{2k+1} = A * (A^k)^2 \).
   - Uses binary exponentiation to compute \( A^k \) in O(n^3 * log(k)) time.

4. **Algorithm**:
   - Start with an identity matrix I (dimension same as A).
   - Iterate through the binary representation of k:
     - If the current bit is set (1), multiply I by A.
     - Square A in each iteration.
   - At the end of the iteration, I will hold the result \( A^k \).

#### Applications

- **Fibonacci Sequence**: Matrix exponentiation can be used to compute the nth Fibonacci number efficiently.
- **Linear Recurrence Relations**: Solving linear recurrence relations efficiently using matrix exponentiation.
- **Graph Theory**: Finding the number of walks of length k between two nodes in a graph.
- **Optimization Problems**: Solving optimization problems where dynamic programming or recursion is involved.

#### Example (Fibonacci Sequence)

```cpp
#include <iostream>
#include <vector>

using namespace std;

typedef vector<vector<long long>> Matrix;

Matrix matrixMultiply(const Matrix &a, const Matrix &b) {
    int n = a.size();
    int m = b[0].size();
    int p = b.size();
    Matrix result(n, vector<long long>(m));
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < m; ++j) {
            for (int k = 0; k < p; ++k) {
                result[i][j] += a[i][k] * b[k][j];
            }
        }
    }
    return result;
}

Matrix matrixExponentiation(const Matrix &a, long long k) {
    int n = a.size();
    Matrix result(n, vector<long long>(n));
    for (int i = 0; i < n; ++i) {
        result[i][i] = 1; // Identity matrix
    }
    Matrix base = a;
    while (k > 0) {
        if (k & 1) {
            result = matrixMultiply(result, base);
        }
        base = matrixMultiply(base, base);
        k >>= 1;
    }
    return result;
}

int main() {
    Matrix fibonacciMatrix = {{1, 1}, {1, 0}};
    int n = 10;
    Matrix result = matrixExponentiation(fibonacciMatrix, n - 1);
    cout << "The " << n << "th Fibonacci number is: " << result[0][0] << endl;
    return 0;
}
```

Matrix exponentiation is a versatile tool that can significantly speed up computations in various algorithms, especially those dealing with large powers and optimization problems.

### 1. Algorithms & Data Structures (C++): Matrix Exponentiation and Dynamic Programming: Modular Exponentiation

Certainly! Matrix exponentiation and modular exponentiation are two important concepts in algorithms and data structures, especially in the context of competitive programming and algorithm optimization. Let's discuss them both briefly:

#### Matrix Exponentiation

Matrix exponentiation is a technique used to efficiently compute the power of a matrix. It's particularly useful in algorithms involving dynamic programming, especially when dealing with problems related to sequences or graphs. The basic idea is to represent a problem state or transition as a matrix, and then use exponentiation to efficiently compute the result after a certain number of steps.

Here's a brief outline of how matrix exponentiation works:

1. **Represent the problem**: Define a matrix that represents the state or transition of the problem you're trying to solve. For example, if you're dealing with a sequence, each element of the matrix might represent the number of ways to transition from one state to another.

2. **Compute the power**: Use matrix exponentiation to efficiently compute the power of the matrix. This can be done using techniques like binary exponentiation, which reduces the number of multiplications required.

3. **Extract the result**: After computing the desired power of the matrix, extract the relevant information from the resulting matrix to obtain the final answer to the problem.

Matrix exponentiation is often used in problems involving Fibonacci numbers, recurrence relations, and graph algorithms like finding the shortest paths in a graph.

#### Dynamic Programming: Modular Exponentiation

Dynamic programming is a method for solving complex problems by breaking them down into simpler subproblems and solving each subproblem only once, storing the solutions to subproblems in a table (memoization) to avoid redundant computations. It's widely used in algorithm design and optimization.

Modular exponentiation is a technique used to efficiently compute large powers of a number modulo another number. It's commonly used in cryptography and number theory, particularly in applications involving large integers.

Here's a basic overview of how modular exponentiation works:

1. **Start with a base and exponent**: Given a base (often denoted as `base`) and an exponent (often denoted as `exp`), the goal is to compute `base^exp % modulus`.

2. **Repeated squaring**: Break down the exponent into its binary representation. For each bit in the binary representation of the exponent, square the base and take the result modulo the modulus. This process effectively reduces the number of multiplications required.

3. **Modular arithmetic**: After each multiplication, take the result modulo the modulus to keep the numbers small and prevent overflow.

4. **Combine the results**: Multiply the intermediate results together (modularly) to obtain the final result.

Modular exponentiation is particularly useful in situations where dealing with large numbers or preventing overflow is necessary, such as cryptographic algorithms like RSA.

In C++, you can implement both techniques using classes and functions. Libraries like `boost::multiprecision` provide support for arbitrary precision arithmetic, which is often necessary when dealing with large numbers in modular exponentiation.

If you'd like to dive deeper into any of these topics or have specific questions, feel free to ask!

### 1. Algorithms & Data Structures (C++): Matrix or 2D Array: How 2D Arrays are stored in Memory ?

In C++, a 2D array is essentially an array of arrays. When you declare a 2D array like `int arr[3][4];`, it creates a contiguous block of memory to hold elements, arranged in rows and columns.

The memory is organized in a row-major order, meaning that elements of each row are stored together. For example, in a 3x4 array:

```bash
arr[0][0] arr[0][1] arr[0][2] arr[0][3]    <-- Row 0
arr[1][0] arr[1][1] arr[1][2] arr[1][3]    <-- Row 1
arr[2][0] arr[2][1] arr[2][2] arr[2][3]    <-- Row 2
```

In memory, it would be stored as a linear sequence:

```bash
arr[0][0] arr[0][1] arr[0][2] arr[0][3] arr[1][0] arr[1][1] arr[1][2] arr[1][3] arr[2][0] arr[2][1] arr[2][2] arr[2][3]
```

So, accessing `arr[i][j]` involves finding the starting address of the array, then calculating the offset for the desired element based on its row and column indices.

This arrangement allows for efficient traversal of rows and columns, as well as easy memory management due to the contiguous allocation.

### 1. Algorithms & Data Structures (C++): Matrix or 2D Array: Initialise and pass 2D Arrays to function

Sure! In C++, you can use a 2D array or a matrix to represent a grid-like structure. Initializing and passing a 2D array to a function involves some syntax nuances. Let me guide you through initializing and passing a 2D array to a function:

#### Initializing a 2D Array

```cpp
#include <iostream>
using namespace std;

const int ROWS = 3;
const int COLS = 3;

void initializeArray(int arr[][COLS]) {
    int count = 1;
    for (int i = 0; i < ROWS; ++i) {
        for (int j = 0; j < COLS; ++j) {
            arr[i][j] = count++;
        }
    }
}

void printArray(int arr[][COLS]) {
    for (int i = 0; i < ROWS; ++i) {
        for (int j = 0; j < COLS; ++j) {
            cout << arr[i][j] << " ";
        }
        cout << endl;
    }
}

int main() {
    int myArray[ROWS][COLS];
    
    initializeArray(myArray);
    cout << "Initialized Array:" << endl;
    printArray(myArray);
    
    return 0;
}
```

In this example, we've defined a constant `ROWS` and `COLS` to represent the dimensions of the 2D array. We have two functions: `initializeArray` to fill the array with some values and `printArray` to print the array.

#### Passing a 2D Array to a Function

When you pass a 2D array to a function, you need to specify the dimensions of the array except for the first dimension. This is because the first dimension can decay into a pointer. For example:

```cpp
void processArray(int arr[][COLS]) {
    // Function body
}
```

In this function declaration, `COLS` must be specified, but `ROWS` can be left out since it can decay into a pointer.

#### Note

1. If you want to dynamically allocate a 2D array, you'll need to use pointers and manage memory manually using `new` and `delete`. This can be more complex.
2. Using `std::vector<std::vector<int>>` might be more flexible and safer for dynamic 2D arrays, as it handles memory management automatically.

### 1. Algorithms & Data Structures (C++): Sum Of columns

To calculate the sum of columns in a matrix using C++, you can follow these steps:

1. Declare a 2D array to store the matrix.
2. Iterate through each column of the matrix and calculate the sum of elements in that column.
3. Store the sums in an array or print them directly.

Here's a sample code to illustrate this:

```cpp
#include <iostream>

const int ROWS = 3;
const int COLS = 3;

void sumOfColumns(int matrix[ROWS][COLS]) {
    int columnSums[COLS] = {0}; // Array to store sums of each column, initialized to 0

    // Iterate through each column
    for (int col = 0; col < COLS; ++col) {
        // Iterate through each row of the current column
        for (int row = 0; row < ROWS; ++row) {
            columnSums[col] += matrix[row][col]; // Add element to the sum of the current column
        }
    }

    // Print the sums of each column
    std::cout << "Sum of columns:\n";
    for (int col = 0; col < COLS; ++col) {
        std::cout << "Column " << col + 1 << ": " << columnSums[col] << std::endl;
    }
}

int main() {
    int matrix[ROWS][COLS] = {{1, 2, 3},
                               {4, 5, 6},
                               {7, 8, 9}};

    sumOfColumns(matrix);

    return 0;
}
```

This code defines a function `sumOfColumns` that takes a 2D array `matrix` as input and calculates the sum of each column, storing them in an array `columnSums`. Finally, it prints the sums of each column. In the `main` function, a sample 3x3 matrix is declared and passed to the `sumOfColumns` function.

### 1. Algorithms & Data Structures (C++): Sum of Maximum Weights

To solve the problem of finding the sum of maximum weights from an array of integers, you can use dynamic programming. Here's how you can do it in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int maxWeightSum(vector<int>& nums) {
    int n = nums.size();
    if (n == 0) return 0;

    // dp[i][0] represents the maximum sum when the i-th element is not included
    // dp[i][1] represents the maximum sum when the i-th element is included
    vector<vector<int>> dp(n, vector<int>(2));

    dp[0][0] = 0;
    dp[0][1] = nums[0];

    for (int i = 1; i < n; ++i) {
        // If we don't include the i-th element, we take the maximum sum so far
        dp[i][0] = max(dp[i-1][0], dp[i-1][1]);

        // If we include the i-th element, we add it to the maximum sum without the previous element
        dp[i][1] = dp[i-1][0] + nums[i];
    }

    // Return the maximum of including or excluding the last element
    return max(dp[n-1][0], dp[n-1][1]);
}

int main() {
    vector<int> nums = {2, 1, 5, 8, 4}; // Example array
    cout << "Maximum weight sum: " << maxWeightSum(nums) << endl;
    return 0;
}
```

This code defines a function `maxWeightSum` that takes a vector of integers and returns the maximum sum of weights. The function uses dynamic programming to calculate the maximum sum considering each element's inclusion and exclusion. Finally, it returns the maximum sum considering the last element included or excluded.

### 1. Algorithms & Data Structures (C++): Symmetric Matrix

A symmetric matrix is a square matrix that is equal to its transpose. In other words, if you reflect the matrix over its main diagonal (from the top-left to the bottom-right), it remains unchanged. In C++, you can implement a symmetric matrix using a 2D array or a vector of vectors.

Here's a simple implementation of a symmetric matrix in C++:

```cpp
#include <iostream>
#include <vector>

class SymmetricMatrix {
private:
    std::vector<std::vector<int>> data;
    int size;

public:
    // Constructor
    SymmetricMatrix(int n) : size(n) {
        data.resize(n, std::vector<int>(n, 0));
    }

    // Setter
    void setElement(int row, int col, int value) {
        if (row < size && col < size) {
            data[row][col] = value;
            data[col][row] = value; // Set symmetric element
        }
    }

    // Getter
    int getElement(int row, int col) const {
        if (row < size && col < size) {
            return data[row][col];
        }
        return -1; // Invalid index
    }
};

int main() {
    int n = 3; // Size of the symmetric matrix

    SymmetricMatrix matrix(n);

    // Set some elements
    matrix.setElement(0, 0, 1);
    matrix.setElement(0, 1, 2);
    matrix.setElement(0, 2, 3);
    matrix.setElement(1, 1, 4);
    matrix.setElement(1, 2, 5);
    matrix.setElement(2, 2, 6);

    // Get and print elements
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < n; ++j) {
            std::cout << matrix.getElement(i, j) << " ";
        }
        std::cout << std::endl;
    }

    return 0;
}
```

This code defines a class `SymmetricMatrix` with methods to set and get elements of the matrix. The elements are stored in a 2D vector, and when setting an element, its symmetric counterpart is also updated to maintain symmetry. Finally, in the `main` function, an example of setting and getting elements is demonstrated.

### 1. Algorithms & Data Structures (C++): Toeplitz Matrix

A Toeplitz matrix is a special kind of matrix where each descending diagonal from left to right is constant. In other words, all the elements on any diagonal of the matrix have the same value.

Here's a simple C++ implementation to check if a given matrix is a Toeplitz matrix:

```cpp
#include <iostream>
#include <vector>

using namespace std;

bool isToeplitzMatrix(vector<vector<int>>& matrix) {
    int rows = matrix.size();
    int cols = matrix[0].size();
    
    // Check each element except the last row and last column
    for (int i = 0; i < rows - 1; ++i) {
        for (int j = 0; j < cols - 1; ++j) {
            if (matrix[i][j] != matrix[i+1][j+1]) {
                return false;
            }
        }
    }
    
    return true;
}

int main() {
    // Example usage
    vector<vector<int>> matrix = {
        {1, 2, 3, 4},
        {5, 1, 2, 3},
        {9, 5, 1, 2}
    };

    if (isToeplitzMatrix(matrix)) {
        cout << "The matrix is a Toeplitz matrix." << endl;
    } else {
        cout << "The matrix is not a Toeplitz matrix." << endl;
    }

    return 0;
}
```

This code iterates over each element of the matrix except for the last row and last column. For each element, it checks whether the element is equal to the one diagonally below and to the right. If any pair of such elements are found to be different, the function returns `false`, indicating that the matrix is not Toeplitz. Otherwise, it returns `true`.

### 1. Algorithms & Data Structures (C++): Transpose Matrix

Certainly! Transposing a matrix means converting its rows into columns and vice versa. In C++, you can achieve this easily with a nested loop. Here's a simple implementation to transpose a matrix:

```cpp
#include <iostream>
#include <vector>

// Function to transpose a matrix
std::vector<std::vector<int>> transposeMatrix(const std::vector<std::vector<int>>& matrix) {
    int rows = matrix.size();
    int cols = matrix[0].size();

    std::vector<std::vector<int>> result(cols, std::vector<int>(rows, 0));

    for (int i = 0; i < rows; ++i) {
        for (int j = 0; j < cols; ++j) {
            result[j][i] = matrix[i][j];
        }
    }

    return result;
}

// Function to print a matrix
void printMatrix(const std::vector<std::vector<int>>& matrix) {
    for (const auto& row : matrix) {
        for (int elem : row) {
            std::cout << elem << " ";
        }
        std::cout << std::endl;
    }
}

int main() {
    std::vector<std::vector<int>> matrix = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};

    std::cout << "Original matrix:" << std::endl;
    printMatrix(matrix);

    std::vector<std::vector<int>> transposed = transposeMatrix(matrix);

    std::cout << "\nTransposed matrix:" << std::endl;
    printMatrix(transposed);

    return 0;
}
```

In this code:

- `transposeMatrix` function takes a 2D vector representing a matrix as input and returns a new 2D vector representing the transposed matrix.
- `printMatrix` function is used to print the matrix.
- In `main`, we define a sample matrix, print it, transpose it using `transposeMatrix`, and then print the transposed matrix.

### 1. Algorithms & Data Structures (C++): Tri-Diagonal and Tri-Band Matrix

Tri-diagonal and tri-band matrices are specific forms of sparse matrices commonly encountered in numerical computing and scientific computing. They arise in various applications, including solving partial differential equations, finite element methods, and numerical simulations. Let's discuss each briefly:

1. **Tri-Diagonal Matrix**:
   - A tri-diagonal matrix is a special kind of sparse matrix where all the non-zero elements lie on the main diagonal and the diagonals immediately above and below it.
   - Tri-diagonal matrices arise naturally in problems such as solving tridiagonal systems of linear equations or discretizing second-order differential equations using finite difference methods.
   - In the context of data structures and algorithms, efficient storage and manipulation of tri-diagonal matrices are crucial to optimize computational resources.
   - In C++, you can represent a tri-diagonal matrix using a compact storage format like arrays. Each row of the matrix can be represented by three arrays for the sub-diagonal, main diagonal, and super-diagonal elements respectively.

2. **Tri-Band Matrix**:
   - A tri-band matrix is a more generalized form of sparse matrix where the non-zero elements are restricted to three diagonals, but those diagonals may not be adjacent to the main diagonal.
   - Tri-band matrices are commonly encountered in solving systems of linear equations arising from discretization of partial differential equations, especially in finite element methods and finite difference methods.
   - In C++, representing a tri-band matrix efficiently involves using arrays where each row is represented by three arrays: one for the main diagonal and two for the off-diagonals. The width of the bandwidth determines the storage requirements and computational complexity.

When implementing algorithms for solving problems involving tri-diagonal or tri-band matrices, efficiency is crucial. Specialized algorithms such as the Thomas algorithm (for tri-diagonal matrices) or banded matrix algorithms are often used to take advantage of the sparsity of these matrices, leading to more efficient computations compared to general-purpose matrix algorithms.

Would you like a more detailed explanation of how to represent and manipulate these matrices in C++?

### 1. Algorithms & Data Structures (C++): Upper Triangular Matrix Column-Major Mapping

Mapping an upper triangular matrix into a one-dimensional array (column-major order) involves transforming the matrix's structure into a linear array while preserving its column-wise ordering. An upper triangular matrix contains non-zero elements only on or above the main diagonal. Here's how you can map it in C++:

```cpp
#include <iostream>

class UpperTriangularMatrix {
private:
    int size;
    int* array;

    // Get the index in the array for given row and column
    int getIndex(int row, int col) const {
        // Since it's column-major, we need to calculate the index accordingly
        // See https://en.wikipedia.org/wiki/Row-_and_column-major_order#Column-major_order
        return col * (col + 1) / 2 + row;
    }

public:
    // Constructor
    UpperTriangularMatrix(int n) : size(n) {
        // Calculate the size of the array needed to store the upper triangular matrix
        int arraySize = size * (size + 1) / 2;
        array = new int[arraySize];
    }

    // Destructor
    ~UpperTriangularMatrix() {
        delete[] array;
    }

    // Set value at given row and column
    void setValue(int row, int col, int value) {
        if (row <= col) {
            array[getIndex(row, col)] = value;
        } else {
            std::cerr << "Error: Trying to set value outside upper triangular matrix!" << std::endl;
        }
    }

    // Get value at given row and column
    int getValue(int row, int col) const {
        if (row <= col) {
            return array[getIndex(row, col)];
        } else {
            // Return 0 for values outside upper triangular matrix
            return 0;
        }
    }
};

int main() {
    int size = 3; // Change the size as needed
    UpperTriangularMatrix matrix(size);

    // Populate the upper triangular matrix
    matrix.setValue(0, 0, 1);
    matrix.setValue(0, 1, 2);
    matrix.setValue(0, 2, 3);
    matrix.setValue(1, 1, 4);
    matrix.setValue(1, 2, 5);
    matrix.setValue(2, 2, 6);

    // Print the upper triangular matrix
    for (int i = 0; i < size; ++i) {
        for (int j = 0; j < size; ++j) {
            std::cout << matrix.getValue(i, j) << " ";
        }
        std::cout << std::endl;
    }

    return 0;
}
```

In this code:

- We define a class `UpperTriangularMatrix` to represent an upper triangular matrix.
- The `array` member variable holds the elements of the upper triangular matrix.
- The `getIndex` method calculates the index in the array for a given row and column in column-major order.
- The `setValue` method sets the value at a given row and column, ensuring it's within the upper triangular part.
- The `getValue` method retrieves the value at a given row and column.
- In the `main` function, we create an instance of `UpperTriangularMatrix`, populate it, and print its elements.

### 1. Algorithms & Data Structures (C++): Upper Triangular Matrix Row-Major Mapping

Mapping a two-dimensional upper triangular matrix into a one-dimensional array (in row-major order) in C++ requires a systematic approach. Here's how you can achieve this:

```cpp
#include <iostream>

class UpperTriangularMatrix {
private:
    int size;
    int* data;

    // Mapping function to convert 2D index to 1D index
    int map(int row, int col) const {
        // Formula for row-major mapping of upper triangular matrix
        return (row * (row + 1) / 2) + col;
    }

public:
    // Constructor
    UpperTriangularMatrix(int n) {
        size = n;
        data = new int[n * (n + 1) / 2];
    }

    // Destructor
    ~UpperTriangularMatrix() {
        delete[] data;
    }

    // Setter
    void set(int row, int col, int value) {
        if (row >= col) {
            int index = map(row, col);
            data[index] = value;
        } else {
            std::cerr << "Error: Attempting to set value in lower triangle" << std::endl;
        }
    }

    // Getter
    int get(int row, int col) const {
        if (row >= col) {
            int index = map(row, col);
            return data[index];
        } else {
            return 0; // Lower triangular element
        }
    }
};

int main() {
    int size = 4; // Size of the matrix
    UpperTriangularMatrix mat(size);

    // Setting values
    for (int i = 0; i < size; ++i) {
        for (int j = i; j < size; ++j) {
            mat.set(i, j, i * size + j + 1);
        }
    }

    // Displaying matrix
    std::cout << "Upper Triangular Matrix (Row-Major Mapping):\n";
    for (int i = 0; i < size; ++i) {
        for (int j = 0; j < size; ++j) {
            std::cout << mat.get(i, j) << "\t";
        }
        std::cout << std::endl;
    }

    return 0;
}
```

This code defines a class `UpperTriangularMatrix` to represent the upper triangular matrix. The `map` function maps the 2D index `(row, col)` to the corresponding 1D index using the row-major order formula for upper triangular matrices. The `set` and `get` methods allow you to set and retrieve values from the matrix. Finally, the `main` function demonstrates how to use this class by setting values and displaying the matrix.

### 1. Algorithms & Data Structures (C++): Wave Print

The wave print of a matrix is a traversal pattern where you print the elements of the matrix in a wave-like pattern, alternating between moving from left to right and right to left across each row. Here's a C++ implementation of the wave print algorithm for a 2D matrix:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void wavePrint(const vector<vector<int>>& matrix) {
    int rows = matrix.size();
    if (rows == 0) return;
    int cols = matrix[0].size();
    bool goingDown = true; // Flag to determine the direction of traversal

    for (int j = 0; j < cols; j++) {
        if (goingDown) {
            // Print elements of current column in downward direction
            for (int i = 0; i < rows; i++)
                cout << matrix[i][j] << " ";
        } else {
            // Print elements of current column in upward direction
            for (int i = rows - 1; i >= 0; i--)
                cout << matrix[i][j] << " ";
        }
        // Flip the direction for the next column
        goingDown = !goingDown;
    }
    cout << endl;
}

int main() {
    vector<vector<int>> matrix = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    wavePrint(matrix);

    return 0;
}
```

This implementation takes a 2D vector (`matrix`) as input and prints its elements in the wave pattern. It traverses each column of the matrix, alternating between printing elements in downward and upward directions.
