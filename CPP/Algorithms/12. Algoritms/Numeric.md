
### 1. Algorithms & Data Structures (C++): Number Theory

Sure! Number theory deals with the properties and relationships of numbers, and it has numerous applications in computer science, particularly in cryptography, algorithm design, and optimization. Here are some common algorithms and data structures related to number theory in C++:

1. **Prime Number Generation**: Generating prime numbers is a fundamental task in number theory. The Sieve of Eratosthenes is a simple and efficient algorithm to generate all prime numbers up to a given limit.

```cpp
#include <iostream>
#include <vector>
using namespace std;

vector<int> sieve(int n) {
    vector<bool> isPrime(n+1, true);
    vector<int> primes;
    for (int p = 2; p * p <= n; p++) {
        if (isPrime[p]) {
            for (int i = p * p; i <= n; i += p)
                isPrime[i] = false;
        }
    }
    for (int p = 2; p <= n; p++) {
        if (isPrime[p])
            primes.push_back(p);
    }
    return primes;
}

int main() {
    int n = 100;
    vector<int> primes = sieve(n);
    for (int prime : primes) {
        cout << prime << " ";
    }
    return 0;
}
```

1. **Greatest Common Divisor (GCD)**: The Euclidean algorithm is commonly used to find the greatest common divisor of two integers efficiently.

```cpp
#include <iostream>
using namespace std;

int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

int main() {
    int a = 48, b = 18;
    cout << "GCD of " << a << " and " << b << " is: " << gcd(a, b) << endl;
    return 0;
}
```

1. **Modular Exponentiation**: Efficiently computing large powers modulo a number is crucial in cryptography and other number theoretic applications. This is often done using the modular exponentiation algorithm, which reduces the time complexity from O(n) to O(log n).

```cpp
#include <iostream>
using namespace std;

long long modPow(long long base, long long exp, long long mod) {
    long long result = 1;
    while (exp > 0) {
        if (exp % 2 == 1)
            result = (result * base) % mod;
        base = (base * base) % mod;
        exp /= 2;
    }
    return result;
}

int main() {
    long long base = 5, exp = 10, mod = 1000000007;
    cout << base << "^" << exp << " mod " << mod << " = " << modPow(base, exp, mod) << endl;
    return 0;
}
```

1. **Prime Factorization**: Decomposing a number into its prime factors is another important operation in number theory. One common approach is trial division.

```cpp
#include <iostream>
#include <vector>
using namespace std;

vector<int> primeFactors(int n) {
    vector<int> factors;
    for (int i = 2; i * i <= n; i++) {
        while (n % i == 0) {
            factors.push_back(i);
            n /= i;
        }
    }
    if (n > 1)
        factors.push_back(n);
    return factors;
}

int main() {
    int n = 315;
    vector<int> factors = primeFactors(n);
    cout << "Prime factors of " << n << " are: ";
    for (int factor : factors) {
        cout << factor << " ";
    }
    return 0;
}
```

These are just a few examples of algorithms and data structures related to number theory in C++. There are many more, including those related to modular arithmetic, Chinese Remainder Theorem, Fermat's Little Theorem, and more.

### 1. Algorithms & Data Structures (C++): Numbers With Repeated Digits

To find numbers with repeated digits efficiently, we can utilize a technique called "inclusion-exclusion principle." Here's a C++ implementation:

```cpp
#include <iostream>
#include <vector>
#include <cmath>
using namespace std;

// Function to count numbers with repeated digits up to n
int countRepeatedDigits(int n) {
    // Convert n to a string to count the number of digits
    string s = to_string(n);
    int digits = s.length();

    // Calculate the count of numbers with distinct digits
    int distinct = 0;
    vector<int> count(10, 0); // count[i] will store the count of occurrences of digit i
    for (int i = 0; i < digits; ++i) {
        for (int j = (i == 0 ? 1 : 0); j < s[i] - '0'; ++j) {
            if (count[j] == 0) {
                distinct += pow(10, digits - i - 1); // Number of ways to fill remaining digits
            }
        }
        if (++count[s[i] - '0'] > 1) break; // If a digit is repeated, stop counting
    }

    // Total numbers up to n with distinct digits
    int totalDistinct = pow(10, digits) - 1 - distinct;

    return n - totalDistinct;
}

int main() {
    int n = 100; // Example: Find numbers with repeated digits up to 100
    cout << "Numbers with repeated digits up to " << n << ": " << countRepeatedDigits(n) << endl;
    return 0;
}
```

This code calculates the count of numbers with repeated digits up to a given number `n`. It iterates through the digits of `n`, counting the number of distinct digits encountered. It then uses the inclusion-exclusion principle to calculate the count of numbers with repeated digits. Finally, it subtracts this count from `n` to get the result.

### 1. Algorithms & Data Structures (C++): Numerical Algorithms

Numerical algorithms are fundamental in computer science and engineering for solving mathematical problems efficiently. In C++, you can implement various numerical algorithms to tackle tasks like numerical integration, solving equations, optimization, and more. Here are some common numerical algorithms along with brief explanations:

1. **Root Finding**:
   - *Newton's Method*: An iterative method for finding the roots of a real-valued function.
   - *Bisection Method*: A simple method that repeatedly bisects an interval and then selects a subinterval in which a root must lie for further processing.

2. **Linear Algebra**:
   - *Matrix Multiplication*: Algorithms for multiplying matrices efficiently, like Strassen's algorithm or Coppersmith-Winograd algorithm.
   - *Matrix Inversion*: Techniques for finding the inverse of a matrix, like Gaussian elimination or LU decomposition.
   - *Eigenvalue and Eigenvector Computation*: Methods like Power iteration, QR iteration, or Jacobi method.

3. **Interpolation and Approximation**:
   - *Polynomial Interpolation*: Techniques for constructing a polynomial that passes through a set of given points.
   - *Least Squares Fitting*: Algorithms for finding the best-fitting curve to a given set of data points.

4. **Numerical Integration**:
   - *Trapezoidal Rule*: An approximation method for numerical integration using trapezoids.
   - *Simpson's Rule*: A more accurate method for numerical integration using quadratic polynomials.

5. **Differential Equations**:
   - *Euler's Method*: A simple numerical method for solving ordinary differential equations.
   - *Runge-Kutta Methods*: Higher-order numerical methods for solving ordinary differential equations with improved accuracy.

6. **Optimization**:
   - *Gradient Descent*: An iterative optimization algorithm for finding the minimum of a function.
   - *Newton's Method for Optimization*: An optimization algorithm based on Newton's method for root finding.

7. **Random Number Generation**:
   - *Linear Congruential Generator (LCG)*: A simple method for generating pseudorandom numbers.
   - *Mersenne Twister*: A more sophisticated pseudorandom number generator known for its long period and high-quality randomness.

When implementing these algorithms in C++, pay attention to efficiency, numerical stability, and precision. Libraries like the Standard Template Library (STL) and external libraries like Eigen or Boost can be helpful for implementing and utilizing numerical algorithms effectively.

### 1. Algorithms & Data Structures (C++): Numerical Integration

Numerical integration is a fundamental concept in computational mathematics and physics. It's used to approximate the definite integral of a function over a specified interval. One common method for numerical integration is the **trapezoidal rule**. Here's how it works:

#### Trapezoidal Rule

Suppose we want to approximate the integral of a function \( f(x) \) over the interval \([a, b]\). We divide the interval into \( n \) subintervals of equal width \( h = \frac{b - a}{n} \). Then, the integral can be approximated as:

\[ \int_a^b f(x) \,dx \approx h \left( \frac{f(a)}{2} + \sum_{i=1}^{n-1} f(a + ih) + \frac{f(b)}{2} \right) \]

In C++, you can implement this as follows:

```cpp
#include <iostream>
#include <cmath>

double func(double x) {
    return /* Define your function here */;
}

double trapezoidal(double a, double b, int n) {
    double h = (b - a) / n;
    double sum = 0.5 * (func(a) + func(b)); // Initialize sum with 0.5 * (f(a) + f(b))
    for (int i = 1; i < n; i++) {
        sum += func(a + i * h);
    }
    return h * sum;
}

int main() {
    double a = /* Lower limit */;
    double b = /* Upper limit */;
    int n = /* Number of subintervals */;
    
    double result = trapezoidal(a, b, n);
    std::cout << "Approximation of the integral: " << result << std::endl;
    
    return 0;
}
```

Replace `func(x)` with your function to integrate, and set `a`, `b`, and `n` according to your requirements. This code will give you an approximation of the integral using the trapezoidal rule.

#### Simpson's Rule

Another commonly used method is Simpson's rule, which provides a more accurate approximation. It approximates the integrand by a quadratic function between each pair of points. The formula is a bit more complex but can yield better results, especially for functions with higher-order curvature.

Would you like an explanation and implementation of Simpson's rule as well?

### 1. Algorithms & Data Structures (C++): Orientation of Points

In computational geometry, determining the orientation of three points (or more generally, a set of points) is a fundamental operation. It helps in various geometric algorithms like convex hull construction, finding the orientation of a polygon, etc. The orientation of three points can be:

1. **Collinear**: All three points lie on the same line.
2. **Clockwise**: The points make a clockwise turn (right turn) when traversed in order.
3. **Counter-clockwise**: The points make a counter-clockwise turn (left turn) when traversed in order.

In C++, you can determine the orientation of three points using the cross product of vectors formed by the points. Here's a basic implementation using vectors:

```cpp
#include <iostream>
using namespace std;

struct Point {
    int x, y;
};

// Function to find orientation of triplet (p, q, r)
// Returns 0 if p, q, r are collinear
// Returns 1 if clockwise
// Returns 2 if counterclockwise
int orientation(Point p, Point q, Point r) {
    int val = (q.y - p.y) * (r.x - q.x) - (q.x - p.x) * (r.y - q.y);

    if (val == 0) return 0; // Collinear
    return (val > 0) ? 1 : 2; // Clockwise or counterclockwise
}

int main() {
    Point p1 = {0, 0}, p2 = {4, 4}, p3 = {1, 2};
    int orient = orientation(p1, p2, p3);
    
    if (orient == 0)
        cout << "Collinear\n";
    else if (orient == 1)
        cout << "Clockwise\n";
    else
        cout << "Counter-clockwise\n";

    return 0;
}
```

This program takes three points `p1`, `p2`, and `p3` as input and prints their orientation. You can modify it according to your specific requirements, such as taking input from the user or processing multiple sets of points.

### 1. Algorithms & Data Structures (C++): POW

In C++, you can implement the power function (pow) using recursion or iteration. Here's an example of both:

```cpp
#include <iostream>

// Recursive power function
double powerRecursive(double base, int exponent) {
    if (exponent == 0) // Base case: anything to the power of 0 is 1
        return 1;
    else if (exponent > 0)
        return base * powerRecursive(base, exponent - 1); // Recursive call for positive exponents
    else
        return 1 / powerRecursive(base, -exponent); // Recursive call for negative exponents
}

// Iterative power function
double powerIterative(double base, int exponent) {
    double result = 1;
    int absExponent = abs(exponent);
    for (int i = 0; i < absExponent; ++i) {
        result *= base;
    }
    return (exponent >= 0) ? result : 1 / result;
}

int main() {
    double base = 2.0;
    int exponent = 5;
    
    // Using recursive power function
    std::cout << "Recursive Power: " << base << " raised to the power of " << exponent << " is " << powerRecursive(base, exponent) << std::endl;
    
    // Using iterative power function
    std::cout << "Iterative Power: " << base << " raised to the power of " << exponent << " is " << powerIterative(base, exponent) << std::endl;
    
    return 0;
}
```

Both functions `powerRecursive` and `powerIterative` calculate the result of `base` raised to the power of `exponent`. The recursive function breaks down the problem by dividing the exponent by smaller values, while the iterative function simply multiplies the base `exponent` times.

### 1. Algorithms & Data Structures (C++): Power Function

Sure! The power function is a common mathematical operation that raises a number to a certain exponent. In C++, you can implement a power function using recursion or iteration. Here's an example implementation of a power function using recursion:

```cpp
#include <iostream>

double power(double base, int exponent) {
    // Base case: if exponent is 0, return 1
    if (exponent == 0)
        return 1;
    
    // Recursive case: multiply base by power(base, exponent - 1)
    // If exponent is negative, take reciprocal
    if (exponent < 0)
        return 1 / (base * power(base, -exponent - 1));
    else
        return base * power(base, exponent - 1);
}

int main() {
    double base;
    int exponent;
    std::cout << "Enter base: ";
    std::cin >> base;
    std::cout << "Enter exponent: ";
    std::cin >> exponent;
    std::cout << "Result: " << power(base, exponent) << std::endl;
    return 0;
}
```

This implementation recursively calculates the power of a number by reducing the exponent by 1 in each recursive call until the base case is reached (exponent is 0). It also handles negative exponents by taking the reciprocal of the result.

Alternatively, you can implement a power function iteratively using a loop:

```cpp
#include <iostream>

double power(double base, int exponent) {
    double result = 1;
    
    // If exponent is negative, take reciprocal of base
    if (exponent < 0) {
        base = 1 / base;
        exponent = -exponent;
    }
    
    // Multiply base by itself exponent times
    for (int i = 0; i < exponent; ++i) {
        result *= base;
    }
    
    return result;
}

int main() {
    double base;
    int exponent;
    std::cout << "Enter base: ";
    std::cin >> base;
    std::cout << "Enter exponent: ";
    std::cin >> exponent;
    std::cout << "Result: " << power(base, exponent) << std::endl;
    return 0;
}
```

This implementation iteratively calculates the power of a number by multiplying the base by itself exponent times. It also handles negative exponents by taking the reciprocal of the base before entering the loop.

### 1. Algorithms & Data Structures (C++): Power of Four

To determine if a given number is a power of four, you can utilize both algorithms and data structures in C++. One efficient approach is to use bitwise operations along with some mathematical properties of powers of four.

Here's a C++ function that checks whether a given number is a power of four:

```cpp
#include <iostream>

bool isPowerOfFour(int num) {
    // A number that is a power of four is always greater than zero
    // and has only one bit set in its binary representation.
    // Also, that bit must be at an odd position.
    
    // Check if the number is positive and if it has only one bit set
    if (num > 0 && (num & (num - 1)) == 0) {
        // Check if the bit set is at an odd position
        // (i.e., the bit at position 0, 2, 4, 6, ...)
        return (num & 0x55555555) != 0;
    }
    return false;
}

int main() {
    int num;
    std::cout << "Enter a number: ";
    std::cin >> num;

    if (isPowerOfFour(num)) {
        std::cout << num << " is a power of four." << std::endl;
    } else {
        std::cout << num << " is not a power of four." << std::endl;
    }

    return 0;
}
```

Explanation:

- The function `isPowerOfFour` takes an integer `num` as input and returns true if `num` is a power of four, otherwise it returns false.
- It first checks if `num` is positive and has only one bit set, which is a common property of powers of two.
- Then it checks if the set bit is at an odd position. In the binary representation of powers of four, the only set bit always appears at an odd position (1, 3, 5, 7, ...).
- In the `main` function, the user is prompted to input a number, and then the result of `isPowerOfFour` is printed.

This algorithm has a time complexity of O(1) because it involves only a few bitwise operations, regardless of the size of the input number.

### 1. Algorithms & Data Structures (C++): Power Sum

The Power Sum problem is a classic algorithmic problem that can be solved using recursion. The problem statement typically goes like this:

Given two integers `X` and `N`, find the number of ways that `X` can be expressed as the sum of `N`th powers of unique natural numbers.

For example, if `X = 10` and `N = 2`, the answer would be `1`, because `10` can only be expressed as `1^2 + 3^2`.

Here's a C++ implementation of the solution using recursion:

```cpp
#include <iostream>
#include <cmath>
using namespace std;

int powerSum(int X, int N, int num = 1) {
    int power = pow(num, N);
    
    if (power > X)
        return 0;
    else if (power == X)
        return 1;
    else
        return powerSum(X, N, num + 1) + powerSum(X - power, N, num + 1);
}

int main() {
    int X, N;
    cout << "Enter X and N: ";
    cin >> X >> N;

    int ways = powerSum(X, N);
    cout << "Number of ways: " << ways << endl;

    return 0;
}
```

In this implementation, the `powerSum` function recursively calculates the number of ways `X` can be expressed as the sum of `N`th powers of unique natural numbers. The base cases are when the power exceeds `X` or when the power equals `X`. Otherwise, it calculates the number of ways by either including the current number `num` in the sum or excluding it.

### 1. Algorithms & Data Structures (C++): Power using Recursion

Sure, here's a C++ implementation of a function to calculate the power of a number using recursion:

```cpp
#include <iostream>

// Function to calculate power using recursion
double power(double base, int exponent) {
    // Base case: if exponent is 0, return 1
    if (exponent == 0) {
        return 1;
    }
    // If exponent is negative, calculate reciprocal
    if (exponent < 0) {
        return 1 / power(base, -exponent);
    }
    // Recursive case: calculate power recursively
    return base * power(base, exponent - 1);
}

int main() {
    double base;
    int exponent;

    std::cout << "Enter base: ";
    std::cin >> base;

    std::cout << "Enter exponent: ";
    std::cin >> exponent;

    // Call the power function and display the result
    std::cout << "Result: " << power(base, exponent) << std::endl;

    return 0;
}
```

This program defines a `power` function that takes a base and an exponent as parameters and calculates the power of the base raised to the exponent using recursion. The main function prompts the user to enter the base and the exponent, calls the `power` function, and prints the result.

### 1. Algorithms & Data Structures (C++): Problem - Decimal to Binary

Sure, I can help you with that. Converting a decimal number to binary involves repeatedly dividing the decimal number by 2 and keeping track of the remainders. Here's a simple algorithm to do that in C++:

```cpp
#include <iostream>
#include <stack>

std::string decimalToBinary(int decimal) {
    if (decimal == 0)
        return "0";

    std::stack<int> binaryDigits;
    
    while (decimal > 0) {
        binaryDigits.push(decimal % 2);
        decimal /= 2;
    }

    std::string binaryString = "";
    while (!binaryDigits.empty()) {
        binaryString += std::to_string(binaryDigits.top());
        binaryDigits.pop();
    }

    return binaryString;
}

int main() {
    int decimal;
    std::cout << "Enter a decimal number: ";
    std::cin >> decimal;

    std::string binary = decimalToBinary(decimal);
    std::cout << "Binary representation: " << binary << std::endl;

    return 0;
}
```

In this code:

- We take the input decimal number.
- We repeatedly divide the decimal number by 2 and push the remainder (which will be either 0 or 1) onto a stack.
- After the division, we pop the digits from the stack one by one and concatenate them to form the binary representation.

This algorithm works for positive decimal numbers. If you want to handle negative decimal numbers as well, you would need to add additional logic to deal with them.

### 1. Algorithms & Data Structures (C++): Ramanujan Number (Taxicab Number)

Ramanujan numbers, also known as Taxicab numbers, are fascinating mathematical entities. They are numbers that can be expressed as the sum of two cubes in different ways. The Indian mathematician Srinivasa Ramanujan was famously associated with these numbers, as he once remarked on the interesting properties of 1729, which is the smallest number that can be expressed as the sum of two cubes in two different ways: \(1^3 + 12^3 = 9^3 + 10^3 = 1729\).

Here's a simple C++ implementation to find Ramanujan numbers within a given range:

```cpp
#include <iostream>
#include <unordered_map>
#include <vector>

using namespace std;

// Function to find Ramanujan numbers within a given range
vector<int> findRamanujanNumbers(int start, int end) {
    vector<int> ramanujanNumbers;
    unordered_map<int, vector<pair<int, int>>> sumsMap;

    // Generate all possible sums of cubes and store them in a map
    for (int i = 1; i * i * i <= end; ++i) {
        for (int j = i + 1; i * i * i + j * j * j <= end; ++j) {
            int sum = i * i * i + j * j * j;
            sumsMap[sum].push_back({i, j});
        }
    }

    // Traverse the map to find numbers with more than one representation
    for (auto& entry : sumsMap) {
        if (entry.second.size() > 1) {
            for (auto& pair : entry.second) {
                int num1 = pair.first;
                int num2 = pair.second;
                if (num1 >= start && num1 <= end && num2 >= start && num2 <= end) {
                    ramanujanNumbers.push_back(entry.first);
                    break; // Only add the number once
                }
            }
        }
    }

    return ramanujanNumbers;
}

int main() {
    int start = 1; // Starting point of the range
    int end = 10000; // Ending point of the range
    vector<int> ramanujanNumbers = findRamanujanNumbers(start, end);

    cout << "Ramanujan numbers between " << start << " and " << end << ":" << endl;
    for (int num : ramanujanNumbers) {
        cout << num << endl;
    }

    return 0;
}
```

This code generates Ramanujan numbers within a specified range by iterating through all possible pairs of cube roots and checking if the sum falls within the range. If a sum appears more than once, it's considered a Ramanujan number and added to the result vector.

### 1. Algorithms & Data Structures (C++): Random Numbers

Random number generation is a fundamental aspect of programming, especially when it comes to simulations, gaming, cryptography, and many other fields. In C++, you have several options for generating random numbers. Here's a brief overview:

1. **rand() Function (C Standard Library):** This is a simple random number generator provided by the C standard library. It generates pseudo-random numbers. You need to include `<cstdlib>` to use it. Example:

```cpp
#include <cstdlib>
#include <iostream>

int main() {
    // Seed the random number generator
    srand(time(0));

    // Generate a random number between 0 and RAND_MAX
    int randomNumber = rand();

    std::cout << "Random number: " << randomNumber << std::endl;

    return 0;
}
```

1. **Random Number Generation in C++11 and later (Standard Library):** Starting from C++11, the `<random>` header provides a more modern and flexible way to generate random numbers. This library includes various random number generators and distributions. Here's a basic example using the Mersenne Twister engine and a uniform distribution:

```cpp
#include <iostream>
#include <random>

int main() {
    // Create a random number engine
    std::random_device rd;
    std::mt19937 gen(rd()); // Mersenne Twister engine

    // Create a uniform distribution
    std::uniform_int_distribution<int> dist(1, 100); // Range: [1, 100]

    // Generate a random number
    int randomNumber = dist(gen);

    std::cout << "Random number: " << randomNumber << std::endl;

    return 0;
}
```

1. **Custom Distributions:** You can also create custom distributions using the `<random>` library. For example, if you need a Gaussian (normal) distribution:

```cpp
#include <iostream>
#include <random>

int main() {
    // Create a random number engine
    std::random_device rd;
    std::mt19937 gen(rd()); // Mersenne Twister engine

    // Create a normal distribution with mean 0 and standard deviation 1
    std::normal_distribution<double> dist(0.0, 1.0);

    // Generate a random number
    double randomNumber = dist(gen);

    std::cout << "Random number (Gaussian): " << randomNumber << std::endl;

    return 0;
}
```

1. **Seed Control:** You can control the seed of the random number generator. This is particularly useful if you want to generate reproducible results or if you're testing your code. For example:

```cpp
std::mt19937 gen(42); // Seed with a specific value (42 in this case)
```

These are just a few examples of random number generation in C++. The `<random>` library offers a wide range of functionalities for different types of distributions and engines.

### 1. Algorithms & Data Structures (C++): Random Randomisation

Randomization is a crucial aspect of many algorithms and data structures, particularly in scenarios where nondeterminism or unpredictability is beneficial. In C++, you can leverage the `<random>` header to implement randomization effectively. Here's a brief overview of how you can use it:

1. **Seeding the random number generator**: Before generating random numbers, you should seed the random number generator. The seed initializes the generator's internal state, ensuring that subsequent calls to generate random numbers produce different sequences. You can use functions like `std::random_device` or `std::seed_seq` for seeding.

```cpp
#include <random>

std::random_device rd; // Obtain a random seed from the OS entropy device
std::mt19937 gen(rd()); // Standard mersenne_twister_engine seeded with rd()
```

1. **Generating random numbers**: Once you've seeded the random number generator, you can use it to generate random numbers of different distributions (uniform, normal, etc.).

```cpp
#include <iostream>
#include <random>

int main() {
    std::random_device rd;
    std::mt19937 gen(rd());
    std::uniform_int_distribution<> dis(1, 6); // Define the range [1, 6] for a six-sided die
    for (int i = 0; i < 10; ++i) {
        std::cout << dis(gen) << ' '; // Generate and print a random number in the specified range
    }
    std::cout << '\n';
    return 0;
}
```

1. **Shuffling elements**: Random shuffling is essential in algorithms like shuffling a deck of cards or randomizing the order of elements in an array. You can use `std::shuffle` for this purpose.

```cpp
#include <iostream>
#include <random>
#include <algorithm>
#include <vector>

int main() {
    std::random_device rd;
    std::mt19937 gen(rd());
    std::vector<int> vec = {1, 2, 3, 4, 5};
    std::shuffle(vec.begin(), vec.end(), gen); // Shuffle the elements of vec
    for (int i : vec) {
        std::cout << i << ' '; // Print the shuffled elements
    }
    std::cout << '\n';
    return 0;
}
```

By incorporating randomization techniques like these, you can develop algorithms and data structures that exhibit desirable randomized behavior, such as improved performance or enhanced security.

### 1. Algorithms & Data Structures (C++): Randomised Random Function

A randomized random function, sometimes called a random number generator, is a crucial component in many algorithms and data structures. In C++, you can implement such a function using the standard library's `<random>` header, which provides utilities for generating random numbers.

Here's a simple example of how you can create a randomized random function in C++:

```cpp
#include <iostream>
#include <random>

// Function to generate a random number between min and max (inclusive)
int randomizedRandom(int min, int max) {
    // Seed the random number generator with the current time
    std::random_device rd;
    std::mt19937 gen(rd());
    
    // Define a uniform distribution
    std::uniform_int_distribution<int> dis(min, max);
    
    // Generate and return a random number
    return dis(gen);
}

int main() {
    // Example usage
    std::cout << "Random number between 1 and 100: " << randomizedRandom(1, 100) << std::endl;
    return 0;
}
```

In this example:

- We include the necessary headers `<iostream>` and `<random>`.
- The `randomizedRandom` function takes two parameters: `min` and `max`, representing the range within which the random number should fall (inclusive).
- Inside `randomizedRandom`, we first seed the random number generator using `std::random_device` to obtain a random seed. Then, we initialize a Mersenne Twister engine (`std::mt19937`) with this seed.
- We define a uniform distribution (`std::uniform_int_distribution`) over the range `[min, max]`.
- Finally, we generate and return a random number using this distribution and the random number generator.

You can use this `randomizedRandom` function wherever you need a random number within a specified range in your C++ programs. Remember to include error checking and handle exceptions appropriately for production code.

### 1. Algorithms & Data Structures (C++): Randomizing Arrays: Randomization Algorithm

Randomizing arrays is a common task in programming, especially when you want to shuffle elements for various purposes like creating randomized tests, implementing card games, or optimizing search algorithms. In C++, you can achieve array randomization using various techniques. One simple and efficient algorithm for randomizing arrays is the Fisher-Yates shuffle algorithm. Here's how you can implement it:

```cpp
#include <iostream>
#include <cstdlib> // for std::rand and std::srand
#include <ctime>   // for std::time

void shuffleArray(int arr[], int size) {
    // Seed the random number generator with current time
    std::srand(std::time(nullptr));

    // Start from the last element and swap one by one
    for (int i = size - 1; i > 0; --i) {
        // Generate a random index between 0 and i (inclusive)
        int j = std::rand() % (i + 1);

        // Swap arr[i] with the element at random index j
        std::swap(arr[i], arr[j]);
    }
}

int main() {
    const int size = 10;
    int arr[size] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

    std::cout << "Original array: ";
    for (int i = 0; i < size; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    shuffleArray(arr, size);

    std::cout << "Shuffled array: ";
    for (int i = 0; i < size; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

This code uses the Fisher-Yates shuffle algorithm to randomly shuffle the elements of the array. Here's a brief overview of how it works:

1. **Seed the random number generator**: Initialize the random number generator with the current time using `std::srand(std::time(nullptr))`. This ensures that the random numbers generated are different each time the program runs.

2. **Shuffle the array**: Iterate through the array from the last element to the second element. For each element at index `i`, generate a random index `j` between 0 and `i` (inclusive). Then, swap the elements at indices `i` and `j`.

3. **Randomness**: By generating a random index within the range of elements yet to be shuffled, every element has an equal chance of being placed at any position in the shuffled array.

This algorithm ensures that every permutation of the array has an equal probability of occurring, making it a fair way to shuffle elements.

### 1. Algorithms & Data Structures (C++): Randomizing Arrays: Randomize Two-Dimensional Array

To randomize a two-dimensional array in C++, you can use the Fisher-Yates shuffle algorithm. This algorithm shuffles elements of an array uniformly at random. Here's how you can implement it for a two-dimensional array:

```cpp
#include <iostream>
#include <cstdlib> // for srand() and rand()
#include <ctime>   // for time()

using namespace std;

const int ROWS = 3;
const int COLS = 3;

void printArray(int arr[][COLS]) {
    for (int i = 0; i < ROWS; ++i) {
        for (int j = 0; j < COLS; ++j) {
            cout << arr[i][j] << " ";
        }
        cout << endl;
    }
}

void shuffleArray(int arr[][COLS]) {
    srand(time(nullptr)); // Seed the random number generator

    for (int i = ROWS - 1; i > 0; --i) {
        for (int j = COLS - 1; j > 0; --j) {
            int randRow = rand() % (i + 1);
            int randCol = rand() % (j + 1);

            // Swap elements at [i][j] and [randRow][randCol]
            int temp = arr[i][j];
            arr[i][j] = arr[randRow][randCol];
            arr[randRow][randCol] = temp;
        }
    }
}

int main() {
    int arr[ROWS][COLS] = {{1, 2, 3},
                            {4, 5, 6},
                            {7, 8, 9}};

    cout << "Original array:" << endl;
    printArray(arr);

    shuffleArray(arr);

    cout << "\nShuffled array:" << endl;
    printArray(arr);

    return 0;
}
```

This code defines a 3x3 two-dimensional array, prints it, shuffles it using the Fisher-Yates shuffle algorithm, and then prints the shuffled array. Make sure to adjust the `ROWS` and `COLS` constants according to the dimensions of your array.

### 1. Algorithms & Data Structures (C++): Reverse Integer

Sure! Here's a simple implementation in C++ to reverse an integer:

```cpp
#include <iostream>

int reverseInteger(int x) {
    int reversed = 0;
    
    while (x != 0) {
        int digit = x % 10;
        x /= 10;
        
        // Check for integer overflow
        if (reversed > INT_MAX / 10 || (reversed == INT_MAX / 10 && digit > 7))
            return 0;
        if (reversed < INT_MIN / 10 || (reversed == INT_MIN / 10 && digit < -8))
            return 0;
        
        reversed = reversed * 10 + digit;
    }
    
    return reversed;
}

int main() {
    int num = 12345;
    std::cout << "Original number: " << num << std::endl;
    std::cout << "Reversed number: " << reverseInteger(num) << std::endl;
    
    return 0;
}
```

This code defines a function `reverseInteger` that takes an integer `x` as input and returns its reverse. The function iteratively extracts the last digit of `x` using modulo operation and builds the reverse number. It also checks for integer overflow conditions to ensure correctness. Finally, in the `main()` function, it demonstrates the usage of `reverseInteger` by reversing the number `12345` and printing the result.

### 1. Algorithms & Data Structures (C++): Segmented Sieve Algorithm

The Segmented Sieve Algorithm is an optimized version of the Sieve of Eratosthenes, used to find all prime numbers less than or equal to a given number `n`. While the original Sieve of Eratosthenes works efficiently for small `n`, it requires a lot of memory for larger `n`. The Segmented Sieve Algorithm addresses this issue by dividing the range `[1, n]` into smaller segments and processing each segment individually.

Here's a basic implementation of the Segmented Sieve Algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <cmath>

using namespace std;

// Function to find all primes smaller than or equal to n
vector<int> segmentedSieve(int n) {
    const int segmentSize = sqrt(n) + 1;
    vector<int> primes;
    vector<bool> isPrime(segmentSize, true);
    
    // Generate all primes up to sqrt(n)
    for (int i = 2; i * i < segmentSize; ++i) {
        if (isPrime[i]) {
            for (int j = i * i; j < segmentSize; j += i) {
                isPrime[j] = false;
            }
        }
    }
    
    // Store primes found in the first segment
    for (int i = 2; i < segmentSize; ++i) {
        if (isPrime[i]) {
            primes.push_back(i);
        }
    }
    
    // Process remaining segments
    for (int low = segmentSize; low <= n; low += segmentSize) {
        int high = min(low + segmentSize - 1, n);
        vector<bool> segment(segmentSize, true);
        
        // Mark multiples of primes in this segment
        for (int prime : primes) {
            int start = (low / prime) * prime;
            if (start < low)
                start += prime;
            for (int j = start; j <= high; j += prime) {
                segment[j - low] = false;
            }
        }
        
        // Add primes from this segment to the list
        for (int i = low; i <= high; ++i) {
            if (segment[i - low] && i > 1) {
                primes.push_back(i);
            }
        }
    }
    
    return primes;
}

int main() {
    int n;
    cout << "Enter a number (n): ";
    cin >> n;
    
    vector<int> primes = segmentedSieve(n);
    
    cout << "Prime numbers up to " << n << " are: ";
    for (int prime : primes) {
        cout << prime << " ";
    }
    cout << endl;
    
    return 0;
}
```

This implementation first generates all primes up to the square root of `n`, storing them in the `primes` vector. Then it processes segments of size `sqrt(n)` starting from `sqrt(n) + 1` up to `n`. Within each segment, it marks multiples of primes found in the first segment. Finally, it collects all primes from each segment and returns them.

### 1. Algorithms & Data Structures (C++): Self Dividing Numbers

Sure! Self-dividing numbers are numbers that are divisible by every digit they contain. In C++, you can write a program to find self-dividing numbers within a given range. Here's a sample implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to check if a number is self-dividing
bool isSelfDividing(int num) {
    int originalNum = num;
    while (num > 0) {
        int digit = num % 10;
        if (digit == 0 || originalNum % digit != 0) {
            return false;
        }
        num /= 10;
    }
    return true;
}

// Function to find self-dividing numbers within a given range
vector<int> selfDividingNumbers(int left, int right) {
    vector<int> result;
    for (int i = left; i <= right; ++i) {
        if (isSelfDividing(i)) {
            result.push_back(i);
        }
    }
    return result;
}

int main() {
    int left = 1, right = 100; // Example range
    vector<int> result = selfDividingNumbers(left, right);
    cout << "Self-dividing numbers between " << left << " and " << right << " are: ";
    for (int num : result) {
        cout << num << " ";
    }
    cout << endl;
    return 0;
}
```

In this program:

- `isSelfDividing` is a function that checks if a given number is self-dividing by iterating through its digits and checking if it's divisible by each digit.
- `selfDividingNumbers` function takes a range (left and right) and returns a vector containing all self-dividing numbers within that range.
- In the `main` function, you can specify the range you want to find self-dividing numbers for and then print out the results.

You can modify the `main` function to specify any range of numbers you want to check for self-dividing numbers.

### 1. Algorithms & Data Structures (C++): Sieve of Eratosthenes

The Sieve of Eratosthenes is an ancient algorithm used to find all prime numbers up to a specified integer value. It's quite efficient for small to medium-sized ranges. Here's a basic implementation of the Sieve of Eratosthenes in C++:

```cpp
#include <iostream>
#include <vector>

void sieveOfEratosthenes(int n) {
    // Create a boolean array "prime[0..n]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be false if i is not a prime, else true.
    std::vector<bool> prime(n + 1, true);

    for (int p = 2; p * p <= n; p++) {
        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {
            // Update all multiples of p
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Print all prime numbers
    for (int p = 2; p <= n; p++)
        if (prime[p])
            std::cout << p << " ";
}

int main() {
    int n;
    std::cout << "Enter the value of n: ";
    std::cin >> n;
    std::cout << "Prime numbers smaller than or equal to " << n << " are:\n";
    sieveOfEratosthenes(n);
    return 0;
}
```

This code snippet takes an input `n` and prints all prime numbers less than or equal to `n`. It works by iteratively marking the multiples of each prime number as composite, effectively sieving out the non-prime numbers.

### 1. Algorithms & Data Structures (C++): Sqrt Decomposition

Sure, let's dive into the concept of Square Root Decomposition (also known as Mo's Algorithm). It's a powerful technique used to solve various range query problems efficiently.

Square Root Decomposition is a method to preprocess an array or sequence in such a way that it can quickly answer queries about subranges or subarrays of that sequence. It's particularly useful for problems where you need to perform multiple queries over different ranges of the array.

Here's a brief outline of how it works:

1. **Preprocessing**: Divide the array into blocks of size approximately √n (where n is the size of the array). Calculate and store the result for each block, such as the sum of elements, minimum/maximum element, or any other required information.

2. **Query Processing**: When a query is received, process it efficiently. If the query range falls completely within one block, you can directly compute the answer for that block. Otherwise, process each block partially covered by the query and combine the results.

Here's a simple example in C++ to illustrate the concept. Let's say we want to find the sum of elements in a given range [l, r] of an array:

```cpp
#include <iostream>
#include <vector>
#include <cmath>

using namespace std;

const int MAXN = 100000; // Maximum size of the array
const int BLOCK_SIZE = 320; // Size of each block (approx. sqrt(MAXN))

vector<int> arr(MAXN);
vector<int> blockSum(BLOCK_SIZE); // Stores sum of each block

// Preprocessing function
void preprocess() {
    for (int i = 0; i < arr.size(); ++i) {
        blockSum[i / BLOCK_SIZE] += arr[i];
    }
}

// Query function
int query(int l, int r) {
    int sum = 0;
    while (l < r && l % BLOCK_SIZE != 0 && l != 0) {
        // Traverse the left over elements not covered by any block
        sum += arr[l];
        ++l;
    }
    while (l + BLOCK_SIZE <= r) {
        // Traverse completely covered blocks
        sum += blockSum[l / BLOCK_SIZE];
        l += BLOCK_SIZE;
    }
    while (l <= r) {
        // Traverse the right over elements not covered by any block
        sum += arr[l];
        ++l;
    }
    return sum;
}

int main() {
    // Sample usage
    arr = {1, 3, 5, 7, 9, 11, 13, 15, 17, 19};
    preprocess();
    cout << query(2, 7) << endl; // Output: 48 (sum of elements from index 2 to 7)
    return 0;
}
```

This is a basic implementation of Square Root Decomposition for range sum queries. You can extend this approach to handle other types of queries like range minimum/maximum, range updates, etc. The time complexity for each query is O(sqrt(n)), which makes it efficient for large arrays.

### 1. Algorithms & Data Structures (C++): Sqrt Decomposition: Range queries

Sure, I can help you with that! Square root decomposition is a technique used to perform efficient range queries on an array. The basic idea is to split the array into blocks of size approximately √n, where n is the size of the array. Each block stores some preprocessed information (like sum, maximum, minimum, etc.), which allows us to answer queries quickly.

Here's a basic implementation in C++ for range sum queries:

```cpp
#include <iostream>
#include <vector>
#include <cmath>

using namespace std;

class SQRTDecomposition {
private:
    vector<int> arr;
    vector<int> blocks;
    int blockSize;

public:
    SQRTDecomposition(const vector<int>& nums) {
        arr = nums;
        int n = arr.size();
        blockSize = sqrt(n);
        blocks.resize((n + blockSize - 1) / blockSize, 0);

        for (int i = 0; i < n; ++i)
            blocks[i / blockSize] += arr[i];
    }

    void update(int index, int val) {
        int blockIndex = index / blockSize;
        blocks[blockIndex] += val - arr[index];
        arr[index] = val;
    }

    int query(int left, int right) {
        int sum = 0;
        int startBlock = left / blockSize;
        int endBlock = right / blockSize;

        if (startBlock == endBlock) {
            for (int i = left; i <= right; ++i)
                sum += arr[i];
        } else {
            for (int i = left; i < (startBlock + 1) * blockSize; ++i)
                sum += arr[i];
            for (int i = startBlock + 1; i < endBlock; ++i)
                sum += blocks[i];
            for (int i = endBlock * blockSize; i <= right; ++i)
                sum += arr[i];
        }

        return sum;
    }
};

int main() {
    vector<int> nums = {1, 3, 5, 7, 9, 11};
    SQRTDecomposition sd(nums);
    cout << "Sum from index 1 to 4: " << sd.query(1, 4) << endl;
    sd.update(2, 6);
    cout << "Sum from index 1 to 4 after update: " << sd.query(1, 4) << endl;
    return 0;
}
```

In this implementation, `SQRTDecomposition` class takes a vector of integers in its constructor and preprocesses the array into blocks. The `update` function allows updating individual elements, and the `query` function returns the sum of elements in a given range.

### 1. Algorithms & Data Structures (C++): Square Roots

In C++, there are several ways to calculate square roots, each with its own trade-offs in terms of speed and accuracy. Here's a simple example of how to calculate square roots using the built-in `sqrt()` function from the `<cmath>` library:

```cpp
#include <iostream>
#include <cmath>

int main() {
    double num = 16.0;
    double squareRoot = sqrt(num);
    
    std::cout << "Square root of " << num << " is " << squareRoot << std::endl;
    
    return 0;
}
```

This will output:

```bash
Square root of 16 is 4
```

If you're interested in understanding the algorithm behind calculating square roots, one of the most common ones is the Newton-Raphson method. Here's an example of how you could implement it:

```cpp
#include <iostream>

double squareRoot(double n, double epsilon = 0.0001) {
    double x = n;
    double y = 1;
    while (x - y > epsilon) {
        x = (x + y) / 2;
        y = n / x;
    }
    return x;
}

int main() {
    double num = 16.0;
    double squareRootValue = squareRoot(num);
    
    std::cout << "Square root of " << num << " is " << squareRootValue << std::endl;
    
    return 0;
}
```

This implementation uses an iterative approach to approximate the square root. The algorithm continues iterating until the difference between consecutive approximations is less than a specified epsilon value. Adjusting the epsilon value allows you to control the accuracy of the result.

These are just a couple of examples, and there are many other algorithms and variations for calculating square roots, each with its own advantages and disadvantages.

### 1. Algorithms & Data Structures (C++): Sum of N Natural Numbers

To calculate the sum of the first \( N \) natural numbers using C++, you can use a simple loop or a mathematical formula. Here's how you can implement both approaches:

#### Using a loop

```cpp
#include <iostream>

int sumOfNNaturalNumbers(int n) {
    int sum = 0;
    for (int i = 1; i <= n; ++i) {
        sum += i;
    }
    return sum;
}

int main() {
    int n;
    std::cout << "Enter the value of N: ";
    std::cin >> n;
    std::cout << "Sum of the first " << n << " natural numbers is: " << sumOfNNaturalNumbers(n) << std::endl;
    return 0;
}
```

#### Using a mathematical formula

The sum of the first \( N \) natural numbers can be calculated using the formula:

\[ \text{Sum} = \frac{N \times (N + 1)}{2} \]

```cpp
#include <iostream>

int sumOfNNaturalNumbers(int n) {
    return (n * (n + 1)) / 2;
}

int main() {
    int n;
    std::cout << "Enter the value of N: ";
    std::cin >> n;
    std::cout << "Sum of the first " << n << " natural numbers is: " << sumOfNNaturalNumbers(n) << std::endl;
    return 0;
}
```

Both of these implementations will give you the sum of the first \( N \) natural numbers. The second approach is more efficient because it calculates the sum in constant time, whereas the first approach has a time complexity of \( O(N) \).

### 1. Algorithms & Data Structures (C++): Sum of N Numbers

Certainly! Here's a simple C++ program to calculate the sum of N numbers using an array:

```cpp
#include <iostream>

using namespace std;

int main() {
    int N;
    cout << "Enter the number of elements: ";
    cin >> N;

    // Dynamically allocate memory for N numbers
    int* numbers = new int[N];

    cout << "Enter " << N << " numbers:\n";
    for (int i = 0; i < N; ++i) {
        cin >> numbers[i];
    }

    int sum = 0;
    for (int i = 0; i < N; ++i) {
        sum += numbers[i];
    }

    cout << "Sum of the numbers is: " << sum << endl;

    // Free dynamically allocated memory
    delete[] numbers;

    return 0;
}
```

This program prompts the user to enter the number of elements (`N`), then allocates memory for `N` integers. It then asks the user to input `N` numbers, calculates their sum using a loop, and finally displays the sum. Don't forget to free the allocated memory using `delete[]` to avoid memory leaks.

### 1. Algorithms & Data Structures (C++): Sum of N using Recursion

Sure! Here's a simple C++ program to find the sum of the first N natural numbers using recursion:

```cpp
#include <iostream>
using namespace std;

// Function to calculate sum of first N natural numbers recursively
int sum(int n) {
    if (n == 0) {
        return 0;
    } else {
        return n + sum(n - 1);
    }
}

int main() {
    int N;
    cout << "Enter the value of N: ";
    cin >> N;

    cout << "Sum of first " << N << " natural numbers: " << sum(N) << endl;

    return 0;
}
```

In this code:

- The `sum` function takes an integer `n` as input and returns the sum of the first `n` natural numbers.
- If `n` is 0, it returns 0 (base case).
- Otherwise, it returns `n` plus the sum of the first `n-1` natural numbers.
- In the `main` function, the user is prompted to enter the value of `N`, and then the `sum` function is called with `N` as the argument, and the result is printed.

### 1. Algorithms & Data Structures (C++): Sum of Natural Number using Recursion

Sure! You can implement a function in C++ to find the sum of natural numbers using recursion. Here's a simple example:

```cpp
#include <iostream>

// Function to calculate the sum of natural numbers up to n using recursion
int sumOfNaturalNumbers(int n) {
    if (n == 1)
        return 1;
    else
        return n + sumOfNaturalNumbers(n - 1);
}

int main() {
    int n;
    std::cout << "Enter a positive integer: ";
    std::cin >> n;

    if (n < 1) {
        std::cout << "Please enter a positive integer.";
        return 1;
    }

    int sum = sumOfNaturalNumbers(n);
    std::cout << "Sum of natural numbers up to " << n << " is: " << sum << std::endl;

    return 0;
}
```

In this code:

- The `sumOfNaturalNumbers` function calculates the sum of natural numbers recursively. It takes an integer `n` as input and returns the sum of natural numbers up to `n`.
- In the `main` function, the user is prompted to enter a positive integer.
- If the user enters a negative number or zero, the program prompts the user to enter a positive integer.
- Finally, it calculates and displays the sum of natural numbers up to the entered number using the `sumOfNaturalNumbers` function.

### 1. Algorithms & Data Structures (C++): Taylor Series Horner's Rule - Recursion

Certainly! Horner's rule is a method used to efficiently evaluate polynomials. When implemented recursively, it can be particularly useful for calculating Taylor series expansions. Here's a basic implementation of Taylor series using Horner's rule in C++:

```cpp
#include <iostream>
using namespace std;

double taylorSeriesHorner(double x, int n) {
    static double result = 1.0; // Initialize result
    if (n == 0)
        return result;
    result = 1 + (x / n) * result;
    return taylorSeriesHorner(x, n - 1);
}

int main() {
    double x = 2.0; // Value for which to evaluate Taylor series
    int n = 10; // Number of terms in the Taylor series
    double taylorSum = taylorSeriesHorner(x, n);
    cout << "e^" << x << " using Taylor series with " << n << " terms: " << taylorSum << endl;
    return 0;
}
```

In this code:

- `taylorSeriesHorner` function is a recursive function that calculates the Taylor series using Horner's rule.
- `x` is the value for which we want to calculate the Taylor series.
- `n` is the number of terms we want in the series.
- `result` is a static variable used to accumulate the result of the Taylor series.
- In each recursive call, we update the result by multiplying it with `x / n` and adding 1, following Horner's rule.
- The recursion continues until we reach the base case (`n == 0`), at which point we return the final result.

You can adjust the value of `x` and `n` in the `main` function to compute the Taylor series for different functions and with different numbers of terms.

### 1. Algorithms & Data Structures (C++): Taylor Series Iterative

Sure, the Taylor series is a mathematical series that can be used to approximate functions. The Taylor series expansion of a function f(x) about a point a is given by:

f(x) = f(a) + f'(a)(x-a) + f''(a)(x-a)^2/2! + f'''(a)(x-a)^3/3! + ...

In C++, you can implement an iterative version of the Taylor series approximation for a given function. Let's say you want to approximate the exponential function (e^x) using its Taylor series expansion around 0. Here's how you could do it:

```cpp
#include <iostream>
#include <cmath>

double exponential(double x, int n) {
    double sum = 1.0; // Initialize sum to the first term of the series which is f(a)

    double term = 1.0; // Initialize term to the first term of the series which is f(a)

    for (int i = 1; i <= n; ++i) {
        term *= x / i; // Calculate the next term using the previous term
        sum += term;   // Add the next term to the sum
    }

    return sum;
}

int main() {
    double x;
    std::cout << "Enter the value of x: ";
    std::cin >> x;

    int n;
    std::cout << "Enter the number of terms in the Taylor series: ";
    std::cin >> n;

    double result = exponential(x, n);
    std::cout << "e^" << x << " (approximated using " << n << " terms) = " << result << std::endl;

    // Compare with the actual value
    double actual = exp(x);
    std::cout << "Actual value of e^" << x << " = " << actual << std::endl;

    return 0;
}
```

In this code:

- `exponential` function calculates the approximation of the exponential function using its Taylor series expansion up to `n` terms.
- `main` function takes input for the value of `x` and the number of terms `n`, then computes and prints the approximation of `e^x` using the specified number of terms.
- It compares the approximation with the actual value of `e^x` calculated using the `exp()` function from the `<cmath>` library.

You can modify this code to approximate other functions by changing the `exponential` function and adjusting the Taylor series expansion accordingly.

### 1. Algorithms & Data Structures (C++): Taylor Series using Horner's Rule

Using Horner's Rule to compute a Taylor series in C++ is a neat way to efficiently approximate a function. Here's a simple implementation:

```cpp
#include <iostream>
#include <cmath>

double taylorSeriesHorner(double x, int n) {
    double result = 1.0; // Initialize result with the first term of the series
    for (int i = n - 1; i > 0; --i) {
        result = 1 + (x / i) * result; // Update result using Horner's rule
    }
    return result;
}

int main() {
    double x = 1.5; // Point at which to evaluate the Taylor series
    int n = 5;      // Number of terms in the series
    double approximation = taylorSeriesHorner(x, n);
    double actualValue = exp(x); // Let's approximate the exponential function
    std::cout << "Approximation using Taylor series: " << approximation << std::endl;
    std::cout << "Actual value of e^x: " << actualValue << std::endl;
    return 0;
}
```

This code calculates the approximation of the exponential function e^x using the Taylor series expansion with Horner's rule. The `taylorSeriesHorner` function takes two arguments: the value of x at which to evaluate the series and the number of terms in the series. It iteratively computes the terms of the series using Horner's rule and returns the result. In the `main` function, you can change the value of `x` and `n` to compute the approximation for different values and different numbers of terms.

### 1. Algorithms & Data Structures (C++): Taylor Series using Recursion

Sure, I can provide you with a C++ implementation of the Taylor series using recursion. The Taylor series expansion represents a function as an infinite sum of terms that are calculated from the values of its derivatives at a single point. Here's a basic implementation of the Taylor series for the exponential function \( e^x \):

```cpp
#include <iostream>
#include <cmath>

double taylorSeries(double x, int n) {
    static double p = 1, f = 1;
    double result;
    
    if (n == 0)
        return 1;
    
    result = taylorSeries(x, n - 1);
    p *= x;
    f *= n;
    
    return result + p / f;
}

int main() {
    double x;
    int n;

    std::cout << "Enter the value of x: ";
    std::cin >> x;
    std::cout << "Enter the number of terms in the series: ";
    std::cin >> n;

    double result = taylorSeries(x, n);
    std::cout << "e^" << x << " = " << result << std::endl;

    return 0;
}
```

In this implementation:

- `taylorSeries` is a recursive function that calculates the value of \( e^x \) using the Taylor series expansion up to \( n \) terms.
- `x` is the value at which we want to evaluate the Taylor series.
- `n` is the number of terms in the series.
- The base case for the recursion is when `n` reaches 0, in which case the function returns 1 (the first term of the Taylor series).
- The function calculates subsequent terms recursively by multiplying the previous term by \( x \) and dividing by \( n \), then adding it to the sum.
- The `main` function takes user input for `x` and `n`, calls `taylorSeries`, and prints the result.

You can modify this code to calculate the Taylor series for other functions by changing the calculation inside the `taylorSeries` function.

### 1. Algorithms & Data Structures (C++): Testing Primality

Testing primality, or determining whether a number is prime or not, is a common problem in computer science and number theory. One of the most famous algorithms for this task is the **Miller-Rabin primality test**. Here's an implementation of the Miller-Rabin primality test in C++:

```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>

using namespace std;

// Modular exponentiation
long long modulo(long long base, long long exponent, long long mod) {
    long long result = 1;
    base = base % mod;
    while (exponent > 0) {
        if (exponent % 2 == 1)
            result = (result * base) % mod;
        exponent = exponent >> 1; // equivalent to exponent /= 2
        base = (base * base) % mod;
    }
    return result;
}

// Miller-Rabin primality test
bool millerRabin(long long n, int k) {
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;
    if (n % 2 == 0)
        return false;

    long long d = n - 1;
    while (d % 2 == 0)
        d /= 2;

    for (int i = 0; i < k; i++) {
        long long a = 2 + rand() % (n - 3);
        long long x = modulo(a, d, n);
        if (x == 1 || x == n - 1)
            continue;

        bool isPrime = false;
        while (d != n - 1) {
            x = (x * x) % n;
            d *= 2;

            if (x == 1)
                return false;
            if (x == n - 1) {
                isPrime = true;
                break;
            }
        }

        if (!isPrime)
            return false;
    }
    return true;
}

int main() {
    srand(time(0)); // Seed for random number generator

    long long num;
    cout << "Enter a number to test for primality: ";
    cin >> num;

    int k = 5; // Number of iterations for the test
    if (millerRabin(num, k))
        cout << num << " is prime.\n";
    else
        cout << num << " is composite.\n";

    return 0;
}
```

In this code:

- `modulo` function calculates `(base^exponent) % mod` efficiently using modular exponentiation.
- `millerRabin` function performs the Miller-Rabin primality test. It takes a number `n` to be tested and the number of iterations `k` to increase the confidence of the test.
- In the `main` function, the user inputs a number to be tested for primality, and the result is printed.

This implementation uses the Miller-Rabin primality test with a fixed number of iterations `k` for simplicity. Increasing `k` increases the confidence in the primality result but also increases the computation time. Typically, a value of `k` around 5 to 10 is sufficient for most practical purposes.

### 1. Algorithms & Data Structures (C++): Theorems in Number Theory

Number theory, the study of integers and their properties, holds relevance in algorithm design and data structures. Here are some theorems and concepts from number theory that find applications in algorithms and data structures, especially in cryptography and optimization:

1. **Euclid's Algorithm**: This classic algorithm computes the greatest common divisor (GCD) of two integers efficiently. It's used in various applications, including simplifying fractions and RSA encryption.

2. **Fermat's Little Theorem**: A fundamental theorem in number theory stating that if \( p \) is a prime number and \( a \) is an integer not divisible by \( p \), then \( a^{p-1} \equiv 1 \mod p \). It's used in primality testing algorithms like the Miller-Rabin test.

3. **Chinese Remainder Theorem (CRT)**: It states that if one knows the remainders of the Euclidean division of an integer \( n \) by several integers, then one can determine uniquely the remainder of the division of \( n \) by the least common multiple of those integers. The CRT has applications in optimizing certain computations and solving systems of linear congruences.

4. **Euler's Totient Function**: Denoted by \( \phi(n) \), it counts the positive integers up to \( n \) that are coprime with \( n \). Euler's totient function finds applications in RSA encryption and primality testing.

5. **Modular Exponentiation**: Computing \( a^b \mod m \) efficiently, where \( a \) and \( b \) are large integers, is crucial in cryptography and is utilized in algorithms like RSA encryption.

6. **Sieve of Eratosthenes**: An ancient algorithm for finding all prime numbers up to any given limit. It's used in various applications where prime numbers are needed, such as in generating prime numbers for cryptographic purposes.

7. **Prime Number Theorem**: It gives an asymptotic estimate for the distribution of prime numbers. Though primarily of theoretical importance, it informs the design and analysis of algorithms related to prime numbers.

8. **Wilson's Theorem**: It provides a necessary and sufficient condition for a prime number. It states that \( p \) is prime if and only if \( (p-1)! \equiv -1 \mod p \). Though not directly used in many algorithms, it's sometimes employed in primality tests.

These theorems and concepts provide a foundation for many algorithms and data structures used in computer science, especially in areas like cryptography, number theory, and optimization. Understanding them can greatly enhance one's ability to design efficient algorithms and data structures.

### 1. Algorithms & Data Structures (C++): Total Hamming Distance

The total Hamming distance between a set of integers is a measure of how different the integers are in terms of their binary representations. It's calculated by counting the total number of positions at which the corresponding bits are different for all pairs of integers in the set.

In C++, you can implement a function to calculate the total Hamming distance as follows:

```cpp
#include <vector>

int totalHammingDistance(const std::vector<int>& nums) {
    int totalDist = 0;
    int n = nums.size();

    // Iterate over each bit position (32 bits for integers)
    for (int i = 0; i < 32; ++i) {
        int countOnes = 0;
        // Count the number of set bits at position i
        for (int num : nums) {
            countOnes += (num >> i) & 1;
        }
        // The number of zeros at position i is n - countOnes
        // Hamming distance at position i is countOnes * (n - countOnes)
        totalDist += countOnes * (n - countOnes);
    }

    return totalDist;
}
```

This function iterates over each bit position from 0 to 31 (assuming integers are 32-bit). For each position, it counts the number of set bits (1s) among all integers in the input vector `nums`. Then, it calculates the number of zeros at that position and adds the product of ones and zeros to the total Hamming distance. Finally, it returns the total distance.

You can call this function with a vector of integers to get the total Hamming distance. For example:

```cpp
#include <iostream>

int main() {
    std::vector<int> nums = {4, 14, 2};
    std::cout << "Total Hamming Distance: " << totalHammingDistance(nums) << std::endl;
    return 0;
}
```

This would output the total Hamming distance for the given vector of integers.

### 1. Algorithms & Data Structures (C++): Total Number of Divisors Till N

To find the total number of divisors for all numbers up to \( N \), you can use the concept of prime factorization. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <vector>
using namespace std;

const int MAX_N = 1000001; // Define a maximum value of N

// Function to calculate the total number of divisors till N
void totalDivisorsTillN(int N) {
    vector<int> divisorsCount(MAX_N, 0); // Initialize an array to store count of divisors

    for (int i = 1; i <= N; i++) {
        for (int j = i; j <= N; j += i) {
            divisorsCount[j]++; // Increment the count of divisors for multiples of i
        }
    }

    long long totalDivisors = 0; // Variable to store the total number of divisors
    for (int i = 1; i <= N; i++) {
        totalDivisors += divisorsCount[i]; // Sum up the counts of divisors
    }

    cout << "Total number of divisors for numbers up to " << N << " is: " << totalDivisors << endl;
}

int main() {
    int N;
    cout << "Enter the value of N: ";
    cin >> N;

    totalDivisorsTillN(N);

    return 0;
}
```

This code computes the total number of divisors for all numbers from 1 to \( N \) efficiently using the concept of sieve and prefix sums. It calculates the count of divisors for each number up to \( N \) and stores them in an array. Finally, it sums up these counts to get the total number of divisors.

### 1. Algorithms & Data Structures (C++): Totient Function

The totient function, also known as Euler's totient function, φ(n), counts the number of positive integers less than or equal to n that are relatively prime to n (i.e., they share no common factors with n other than 1). It's a fundamental concept in number theory and has applications in cryptography, particularly in RSA encryption.

Here's a simple implementation of the totient function in C++:

```cpp
#include <iostream>
using namespace std;

int phi(int n) {
    int result = n; // Initialize result as n
    for (int p = 2; p * p <= n; ++p) {
        // Check if p is a prime factor of n
        if (n % p == 0) {
            // Update result to remove all occurrences of p in n
            while (n % p == 0)
                n /= p;
            result -= result / p;
        }
    }
    // If n has a prime factor greater than sqrt(n),
    // then there can be at most one such prime factor
    if (n > 1)
        result -= result / n;
    return result;
}

int main() {
    int n;
    cout << "Enter a positive integer: ";
    cin >> n;
    cout << "Phi(" << n << ") = " << phi(n) << endl;
    return 0;
}
```

In this implementation:

- We start with initializing the result as n.
- We loop through all prime factors p of n, starting from 2. For each prime factor, we divide n by it and update the result accordingly.
- If n still has a prime factor greater than its square root after the loop, it must be a prime number itself, so we adjust the result accordingly.
- Finally, we return the computed result, which is φ(n).

You can input any positive integer to find its totient value using this program.

### 1. Algorithms & Data Structures (C++): Totient Function code using Seive

Sure, here's a C++ code for calculating the totient function (Euler's totient function) using the Sieve of Eratosthenes algorithm:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void totientFunction(int n) {
    vector<int> phi(n + 1);
    
    // Initialize phi[] with its indices
    for (int i = 0; i <= n; ++i)
        phi[i] = i;
    
    // Compute phi[] using Sieve of Eratosthenes
    for (int p = 2; p <= n; ++p) {
        // If phi[p] is not changed, then it is a prime number
        if (phi[p] == p) {
            // Update phi[] values for all multiples of p
            for (int i = p; i <= n; i += p)
                phi[i] -= phi[i] / p;
        }
    }
    
    // Print the totient function values
    cout << "Totient Function Values from 1 to " << n << ":\n";
    for (int i = 1; i <= n; ++i)
        cout << "phi(" << i << ") = " << phi[i] << endl;
}

int main() {
    int n;
    cout << "Enter the value of n: ";
    cin >> n;
    totientFunction(n);
    return 0;
}
```

This code first initializes an array `phi[]` with indices from 0 to n, where each element initially holds its index value. Then, it iterates through each prime number (starting from 2) using the Sieve of Eratosthenes algorithm and updates the `phi[]` values accordingly. Finally, it prints out the values of the totient function for each number from 1 to n.

### 1. Algorithms & Data Structures (C++): Triangle Pattern

Creating a triangle pattern using C++ involves nested loops to control the number of rows and columns to print. Here's a simple example to print a triangle pattern using asterisks:

```cpp
#include <iostream>

int main() {
    int rows;

    std::cout << "Enter the number of rows for the triangle pattern: ";
    std::cin >> rows;

    for (int i = 1; i <= rows; ++i) {
        // Print spaces
        for (int j = 1; j <= rows - i; ++j) {
            std::cout << " ";
        }
        
        // Print asterisks
        for (int k = 1; k <= 2 * i - 1; ++k) {
            std::cout << "*";
        }
        
        // Move to the next line
        std::cout << std::endl;
    }

    return 0;
}
```

This code prompts the user to enter the number of rows for the triangle pattern. It then iterates over each row, printing spaces followed by asterisks to form the triangle shape. The number of asterisks in each row is equal to `2 * i - 1`, where `i` represents the current row number. The number of spaces decreases with each row to form the triangle shape.

You can adjust the code according to your desired pattern, whether it's a right-angle triangle, equilateral triangle, or any other variant.

### 1. Algorithms & Data Structures (C++): Two Power

Certainly! If you want to implement a function in C++ that calculates the power of 2 efficiently using bitwise operations, you can use the left shift operator `<<`. Each left shift operation by 1 bit is equivalent to multiplying by 2.

Here's a simple implementation:

```cpp
#include <iostream>

unsigned long long powerOfTwo(int exponent) {
    // If exponent is negative, return 0 as 2 raised to a negative power is 0
    if (exponent < 0)
        return 0;

    // Left shift 1 by exponent bits to get the result
    return 1ULL << exponent;
}

int main() {
    int exponent;
    std::cout << "Enter the exponent: ";
    std::cin >> exponent;

    unsigned long long result = powerOfTwo(exponent);
    std::cout << "2^" << exponent << " = " << result << std::endl;

    return 0;
}
```

This program takes an integer input from the user, calculates 2 raised to the power of that input using bitwise left shift, and then prints the result.

### 1. Algorithms & Data Structures (C++): Two Sum

Certainly! The Two Sum problem is a classic algorithmic problem. Given an array of integers `nums` and an integer target, return indices of the two numbers such that they add up to the target.

Here's a C++ implementation of the Two Sum problem using a hash map for efficient lookup:

```cpp
#include <iostream>
#include <unordered_map>
#include <vector>

std::vector<int> twoSum(std::vector<int>& nums, int target) {
    std::unordered_map<int, int> hash_map;
    std::vector<int> result;

    for (int i = 0; i < nums.size(); ++i) {
        int complement = target - nums[i];
        if (hash_map.find(complement) != hash_map.end()) {
            // Found complement, return indices
            result.push_back(hash_map[complement]);
            result.push_back(i);
            return result;
        }
        // Store current number and its index
        hash_map[nums[i]] = i;
    }

    // If no solution found
    return result;
}

int main() {
    std::vector<int> nums = {2, 7, 11, 15};
    int target = 9;
    std::vector<int> indices = twoSum(nums, target);
    
    if (indices.size() == 2) {
        std::cout << "Indices: " << indices[0] << " " << indices[1] << std::endl;
    } else {
        std::cout << "No solution found!" << std::endl;
    }

    return 0;
}
```

In this implementation:

1. We iterate through the array `nums`.
2. For each element, we calculate its complement (the number needed to reach the target) as `target - nums[i]`.
3. We check if this complement exists in the hash map. If it does, we return the indices of the current element and the complement.
4. If the complement doesn't exist in the hash map, we add the current element and its index to the hash map.
5. If no solution is found, an empty vector is returned.

This solution has a time complexity of O(n) since we traverse the list containing n elements only once, and each lookup and insertion in the hash map takes O(1) time on average.

### 1. Algorithms & Data Structures (C++): Two Sum - Hash Table

Certainly! The "Two Sum" problem is a classic algorithmic problem where you're given an array of integers and a target number. The task is to find two numbers in the array that sum up to the target and return their indices.

One efficient way to solve this problem is by using a hash table (unordered_map in C++). Here's how you can implement it:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>

std::vector<int> twoSum(std::vector<int>& nums, int target) {
    std::unordered_map<int, int> hashTable; // Key: number, Value: index

    for (int i = 0; i < nums.size(); ++i) {
        int complement = target - nums[i];
        
        // Check if the complement is present in the hash table
        if (hashTable.find(complement) != hashTable.end()) {
            // If found, return the indices of the two numbers
            return {hashTable[complement], i};
        }
        
        // Otherwise, add the current number and its index to the hash table
        hashTable[nums[i]] = i;
    }

    // If no such pair is found, return an empty vector
    return {};
}

int main() {
    std::vector<int> nums = {2, 7, 11, 15};
    int target = 9;
    std::vector<int> result = twoSum(nums, target);

    if (result.size() == 2) {
        std::cout << "Indices of the two numbers: " << result[0] << " and " << result[1] << std::endl;
    } else {
        std::cout << "No such pair found." << std::endl;
    }

    return 0;
}
```

In this code:

- We iterate through the array once.
- For each element, we calculate its complement by subtracting it from the target.
- We then check if this complement exists in the hash table.
- If it does, we return the indices of the current element and the complement.
- Otherwise, we add the current element and its index to the hash table.
- If no such pair is found, we return an empty vector.

This solution has a time complexity of O(n) since we iterate through the array once, and each lookup and insertion in the hash table takes O(1) time on average.

### 1. Algorithms & Data Structures (C++): Two Sum - Input Array Is Sorted - Binary Search

Certainly! The "Two Sum" problem is a classic coding interview question where you're given an array of integers and a target sum, and you're asked to find two numbers in the array that add up to the target sum. If there are multiple pairs that sum up to the target, you can return any valid pair.

Here's how you can solve the "Two Sum" problem efficiently in C++ when the input array is sorted using the binary search algorithm:

```cpp
#include <vector>
#include <iostream>

using namespace std;

vector<int> twoSum(vector<int>& nums, int target) {
    int left = 0;
    int right = nums.size() - 1;

    while (left < right) {
        int sum = nums[left] + nums[right];
        if (sum == target) {
            return {left + 1, right + 1}; // Indices are 1-based
        } else if (sum < target) {
            left++;
        } else {
            right--;
        }
    }

    // If no solution found
    return {};
}

int main() {
    vector<int> nums = {2, 7, 11, 15};
    int target = 9;

    vector<int> result = twoSum(nums, target);

    if (result.size() == 2) {
        cout << "Indices of the two numbers: " << result[0] << ", " << result[1] << endl;
    } else {
        cout << "No two elements sum up to the target." << endl;
    }

    return 0;
}
```

Explanation:

- We initialize two pointers, `left` pointing to the start of the array and `right` pointing to the end of the array.
- We iterate over the array while `left` is less than `right`.
- At each iteration, we calculate the sum of the elements pointed by `left` and `right`.
- If the sum equals the target, we return the indices `left + 1` and `right + 1` (since the indices are 1-based).
- If the sum is less than the target, we move the `left` pointer to the right to increase the sum.
- If the sum is greater than the target, we move the `right` pointer to the left to decrease the sum.
- If no solution is found, we return an empty vector.

This algorithm has a time complexity of O(n) because we only traverse the array once.

### 1. Algorithms & Data Structures (C++): Two Sum (Brute Force)

Sure, here's a C++ implementation of the brute force solution for the Two Sum problem:

```cpp
#include <iostream>
#include <vector>

std::vector<int> twoSum(std::vector<int>& nums, int target) {
    std::vector<int> result;

    for (int i = 0; i < nums.size(); ++i) {
        for (int j = i + 1; j < nums.size(); ++j) {
            if (nums[i] + nums[j] == target) {
                result.push_back(i);
                result.push_back(j);
                return result;
            }
        }
    }

    // If no solution found
    return result;
}

int main() {
    std::vector<int> nums = {2, 7, 11, 15};
    int target = 9;
    std::vector<int> result = twoSum(nums, target);

    if (result.size() == 2) {
        std::cout << "Indices: " << result[0] << " and " << result[1] << std::endl;
    } else {
        std::cout << "No solution found." << std::endl;
    }

    return 0;
}
```

This code defines a function `twoSum` that takes a vector of integers `nums` and an integer `target` as input. It iterates through all pairs of indices in the array and checks if the sum of the elements at those indices equals the target. If a solution is found, it returns the indices of the two numbers as a vector. If no solution is found, an empty vector is returned.

In the `main` function, we demonstrate the usage of the `twoSum` function by providing a sample input vector `nums` and a target sum `target`. The indices of the two numbers whose sum equals the target are printed if a solution is found, otherwise, a message indicating no solution is printed.

### 1. Algorithms & Data Structures (C++): Two Sum (Hashmap version)

Certainly! The "Two Sum" problem is a classic algorithmic problem where you're given an array of integers and a target sum. The task is to find two numbers in the array that add up to the target sum and return their indices. Here's a C++ implementation using a hashmap (unordered_map) for efficient lookup:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>

std::vector<int> twoSum(std::vector<int>& nums, int target) {
    std::unordered_map<int, int> numIndexMap;

    for (int i = 0; i < nums.size(); ++i) {
        int complement = target - nums[i];
        if (numIndexMap.find(complement) != numIndexMap.end()) {
            // Found the complement, return indices
            return {numIndexMap[complement], i};
        }
        // Store the current number and its index
        numIndexMap[nums[i]] = i;
    }
    
    // If no solution found, return an empty vector
    return {};
}

int main() {
    std::vector<int> nums = {2, 7, 11, 15};
    int target = 9;
    std::vector<int> result = twoSum(nums, target);
    
    if (result.size() == 2) {
        std::cout << "Indices: " << result[0] << ", " << result[1] << std::endl;
    } else {
        std::cout << "No solution found." << std::endl;
    }
    
    return 0;
}
```

In this implementation:

- We use an unordered_map to store the numbers encountered so far and their corresponding indices.
- As we iterate through the array, for each element, we calculate its complement (the number that needs to be paired with it to reach the target sum).
- We then check if this complement exists in the map. If it does, we've found the two numbers that sum up to the target, and we return their indices.
- If not found, we add the current number and its index to the map.
- If no solution is found after iterating through the array, we return an empty vector.

This solution has a time complexity of O(n) since we traverse the array only once, and each lookup in the unordered_map takes O(1) time on average.

### 1. Algorithms & Data Structures (C++): Two Sum Problem

The Two Sum problem is a classic algorithmic problem where you're given an array of integers and a target sum. The task is to find two numbers in the array that add up to the target sum and return their indices.

Here's a C++ implementation of the Two Sum problem using a hash map (unordered_map) for efficient lookup:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>

std::vector<int> twoSum(std::vector<int>& nums, int target) {
    std::unordered_map<int, int> numMap; // Map to store value-index pairs
    
    for (int i = 0; i < nums.size(); ++i) {
        int complement = target - nums[i]; // Calculate the complement needed
        
        // Check if the complement exists in the map
        if (numMap.find(complement) != numMap.end()) {
            // If found, return the indices
            return { numMap[complement], i };
        }
        
        // Otherwise, add the current number to the map
        numMap[nums[i]] = i;
    }
    
    // If no solution is found, return an empty vector
    return {};
}

int main() {
    std::vector<int> nums = {2, 7, 11, 15};
    int target = 9;
    
    std::vector<int> result = twoSum(nums, target);
    
    if (result.size() == 2) {
        std::cout << "Indices: " << result[0] << " and " << result[1] << std::endl;
    } else {
        std::cout << "No solution found." << std::endl;
    }
    
    return 0;
}
```

This implementation has a time complexity of O(n) since it iterates through the array once, and the lookup in the unordered_map is O(1) on average. So, the overall time complexity is O(n).

### 1. Algorithms & Data Structures (C++): Linked List: Binary to Decimal

Converting a binary number to a decimal number involves a straightforward algorithm where you iterate through the binary digits from right to left (least significant bit to most significant bit), multiplying each digit by 2 raised to the power of its position and summing the results. In the context of a linked list, you can represent a binary number as a singly linked list where each node contains a bit (0 or 1) and traverse through it to perform the conversion.

Here's a C++ implementation of converting a binary number represented as a linked list to its decimal equivalent:

```cpp
#include <iostream>

// Define the structure of a linked list node
struct Node {
    int data;
    Node* next;
    
    Node(int value) : data(value), next(nullptr) {}
};

// Function to insert a new node with the given data at the end of the linked list
void insert(Node*& head, int data) {
    Node* newNode = new Node(data);
    if (head == nullptr) {
        head = newNode;
    } else {
        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = newNode;
    }
}

// Function to convert a binary linked list to decimal
int binaryToDecimal(Node* head) {
    int decimal = 0;
    int position = 0;
    while (head != nullptr) {
        decimal += head->data * (1 << position); // Equivalent to pow(2, position)
        position++;
        head = head->next;
    }
    return decimal;
}

// Function to display the linked list
void displayList(Node* head) {
    while (head != nullptr) {
        std::cout << head->data << " ";
        head = head->next;
    }
    std::cout << std::endl;
}

int main() {
    // Example: 1101 (binary) = 13 (decimal)
    Node* head = nullptr;
    insert(head, 1);
    insert(head, 1);
    insert(head, 0);
    insert(head, 1);
    
    std::cout << "Binary representation: ";
    displayList(head);
    
    int decimal = binaryToDecimal(head);
    std::cout << "Decimal representation: " << decimal << std::endl;
    
    // Free memory (optional)
    Node* temp;
    while (head != nullptr) {
        temp = head;
        head = head->next;
        delete temp;
    }
    
    return 0;
}
```

This code demonstrates how to convert a binary number represented as a linked list to its decimal equivalent. It includes functions for inserting nodes into the linked list, converting the binary linked list to decimal, and displaying the linked list. The `binaryToDecimal` function performs the conversion using the binary-to-decimal algorithm mentioned earlier.

### 1. Algorithms & Data Structures (C++): Array & Integer Multiplication

Multiplying large integers stored in arrays is a common problem, especially in cryptography and mathematical computations. Here's a basic implementation in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

vector<int> multiply(vector<int>& num1, vector<int>& num2) {
    int m = num1.size();
    int n = num2.size();
    
    vector<int> result(m + n, 0);
    
    for (int i = m - 1; i >= 0; i--) {
        for (int j = n - 1; j >= 0; j--) {
            int mul = (num1[i] - '0') * (num2[j] - '0');
            int sum = mul + result[i + j + 1];
            
            result[i + j] += sum / 10;
            result[i + j + 1] = sum % 10;
        }
    }
    
    // Remove leading zeros
    int i = 0;
    while (i < m + n && result[i] == 0) {
        i++;
    }
    
    if (i == m + n) {
        return {0};
    }
    
    return vector<int>(result.begin() + i, result.end());
}

int main() {
    vector<int> num1 = {1, 2, 3};
    vector<int> num2 = {4, 5, 6};
    
    vector<int> result = multiply(num1, num2);
    
    for (int num : result) {
        cout << num;
    }
    
    cout << endl;
    
    return 0;
}
```

This code defines a function `multiply` that takes two vectors representing large integers as input and returns their product as another vector. The main algorithm used here is similar to how we multiply numbers by hand. We iterate through each digit of both numbers, calculate their products, and add them to the appropriate positions in the result vector. Finally, we remove any leading zeros from the result.

You can customize this code as per your requirements, like input validation or handling negative numbers. Also, this implementation assumes that both input vectors are representing positive integers.
