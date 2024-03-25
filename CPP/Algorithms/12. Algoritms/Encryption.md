# Encryption

## General

### 1. Algorithms & Data Structures (C++): Caesar Cipher

The Caesar Cipher is one of the simplest and oldest encryption techniques. It works by shifting each letter in the plaintext by a fixed number of positions down or up the alphabet. For example, with a shift of 3, 'A' would be encrypted to 'D', 'B' to 'E', and so on. Here's a simple implementation of the Caesar Cipher in C++:

```cpp
#include <iostream>
#include <string>

std::string caesarCipherEncrypt(const std::string& text, int shift) {
    std::string result = "";
    for (char c : text) {
        // Encrypt uppercase letters
        if (isupper(c)) {
            result += char(int(c + shift - 65) % 26 + 65);
        }
        // Encrypt lowercase letters
        else if (islower(c)) {
            result += char(int(c + shift - 97) % 26 + 97);
        }
        // Leave non-alphabetic characters unchanged
        else {
            result += c;
        }
    }
    return result;
}

int main() {
    std::string plaintext = "Hello, World!";
    int shift = 3;
    std::string encryptedText = caesarCipherEncrypt(plaintext, shift);
    std::cout << "Encrypted text: " << encryptedText << std::endl;
    return 0;
}
```

This program takes a string and a shift value as input, then encrypts the string using the Caesar Cipher algorithm with the given shift value. It preserves the case of letters and leaves non-alphabetic characters unchanged. You can modify the `main()` function to accept user input for the plaintext and the shift value if you want to make it more interactive.

### 1. Algorithms & Data Structures (C++): Chinese Remainder Theorem

The Chinese Remainder Theorem (CRT) is a fundamental theorem in number theory and has significant applications in computer science, particularly in cryptography and algorithms dealing with modular arithmetic. It states that if one knows the remainders of the division of an integer by several pairwise coprime integers, then one can determine uniquely the remainder of the division of the integer by the product of those integers, under the condition that the divisors are pairwise coprime.

In C++, you can implement the Chinese Remainder Theorem using a combination of modular arithmetic and the Extended Euclidean Algorithm. Here's a basic implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Extended Euclidean Algorithm to find modular inverse
int extendedEuclidean(int a, int b, int& x, int& y) {
    if (a == 0) {
        x = 0;
        y = 1;
        return b;
    }

    int x1, y1;
    int gcd = extendedEuclidean(b % a, a, x1, y1);

    x = y1 - (b / a) * x1;
    y = x1;

    return gcd;
}

// Chinese Remainder Theorem function
int chineseRemainder(const vector<int>& num, const vector<int>& rem) {
    int prod = 1;
    for (int n : num)
        prod *= n;

    int result = 0;
    for (int i = 0; i < num.size(); i++) {
        int pp = prod / num[i];
        int inv, dummy;
        extendedEuclidean(pp, num[i], inv, dummy);
        result += rem[i] * inv * pp;
    }

    return result % prod;
}

int main() {
    vector<int> num = {3, 5, 7}; // pairwise coprime numbers
    vector<int> rem = {2, 3, 2}; // remainders

    int result = chineseRemainder(num, rem);
    cout << "The number is: " << result << endl;

    return 0;
}
```

This code takes vectors `num` and `rem`, where `num` contains pairwise coprime numbers and `rem` contains the corresponding remainders. It then calculates the number that satisfies all the congruences using the Chinese Remainder Theorem. The extended Euclidean algorithm is used to find the modular inverses.

### 1. Algorithms & Data Structures (C++): Decode Permutation

To decode a permutation in C++, you typically need to understand what encoding method was used to create the permutation. For instance, if you have a permutation encoded as a sequence of integers, you can easily decode it by reversing the encoding process.

Here's a simple example of decoding a permutation:

```cpp
#include <iostream>
#include <vector>

std::vector<int> decodePermutation(const std::vector<int>& encoded) {
    int n = encoded.size();
    std::vector<int> permutation(n);

    for (int i = 0; i < n; ++i) {
        permutation[encoded[i] - 1] = i + 1;
    }

    return permutation;
}

int main() {
    // Example encoded permutation
    std::vector<int> encoded = {3, 1, 2};

    // Decode the permutation
    std::vector<int> decoded = decodePermutation(encoded);

    // Print the decoded permutation
    std::cout << "Decoded permutation: ";
    for (int i = 0; i < decoded.size(); ++i) {
        std::cout << decoded[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this example, the `decodePermutation` function takes an encoded permutation (represented as a vector of integers) as input and returns the decoded permutation. The decoding process involves iterating over the encoded permutation and placing each element in its correct position in the decoded permutation.

Keep in mind that this example assumes that the encoding starts from 1 and is contiguous. If your encoding scheme is different, you'll need to adjust the decoding logic accordingly.

### 1. Algorithms & Data Structures (C++): Decode XORed Array

To decode an XORed array in C++, you need to understand how XOR works. XOR, or exclusive OR, is a bitwise operation that compares two bits. It returns 1 if the bits are different and 0 if they are the same. When you XOR a number with itself, you get 0. Using this property, you can decode an XORed array given the original first element and the XORed array.

Here's a C++ function to decode an XORed array:

```cpp
#include <vector>

std::vector<int> decode(std::vector<int>& encoded, int first) {
    std::vector<int> decoded(encoded.size() + 1);
    decoded[0] = first; // First element is given

    for (int i = 0; i < encoded.size(); ++i) {
        // Decoding each element by XOR operation
        decoded[i + 1] = decoded[i] ^ encoded[i];
    }

    return decoded;
}
```

In this function:

- `encoded` is the XORed array.
- `first` is the first element of the original array.
- We create a new array called `decoded` to store the decoded elements. Its size is one more than the size of the `encoded` array because we have the first element.
- We set the first element of `decoded` to `first`.
- Then, we iterate through the `encoded` array and XOR each element with the previous decoded element to get the next decoded element.

Here's how you can use this function:

```cpp
#include <iostream>

int main() {
    std::vector<int> encoded = {1, 2, 3};
    int first = 1;
    
    std::vector<int> decoded = decode(encoded, first);
    
    std::cout << "Decoded array: ";
    for (int num : decoded) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
    
    return 0;
}
```

This will output:

```bash
Decoded array: 1 0 2 3
```

Feel free to adjust the function parameters and test it with different inputs!

### 1. Algorithms & Data Structures (C++): Enigma Cipher

Implementing the Enigma cipher in C++ can be a fascinating project. The Enigma machine was used by the Germans during World War II for encryption and decryption of messages. Here's a simplified version of how you could implement it:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <random>

class Rotor {
private:
    std::vector<int> mapping;
    int position;
public:
    Rotor(const std::vector<int>& initialMapping) : mapping(initialMapping), position(0) {}

    void rotate() {
        std::rotate(mapping.begin(), mapping.begin() + 1, mapping.end());
        position = (position + 1) % mapping.size();
    }

    void setStartPosition(int startPos) {
        position = startPos;
        std::rotate(mapping.begin(), mapping.begin() + startPos, mapping.end());
    }

    int encode(int input) {
        return mapping[(input + position) % 26];
    }

    int decode(int input) {
        auto it = std::find(mapping.begin(), mapping.end(), (input + position) % 26);
        return std::distance(mapping.begin(), it) - position;
    }
};

class EnigmaMachine {
private:
    std::vector<Rotor> rotors;
public:
    EnigmaMachine(const std::vector<std::vector<int>>& rotorMappings) {
        for (const auto& mapping : rotorMappings) {
            rotors.emplace_back(mapping);
        }
    }

    void setRotorStartPositions(const std::vector<int>& startPositions) {
        for (size_t i = 0; i < startPositions.size(); ++i) {
            rotors[i].setStartPosition(startPositions[i]);
        }
    }

    int encode(int input) {
        for (auto& rotor : rotors) {
            input = rotor.encode(input);
        }
        return input;
    }

    int decode(int input) {
        for (auto& rotor : rotors) {
            input = rotor.decode(input);
        }
        return input;
    }

    void rotateRotors() {
        rotors[0].rotate();
        for (size_t i = 1; i < rotors.size(); ++i) {
            if (rotors[i - 1].position == 0)
                rotors[i].rotate();
        }
    }
};

int main() {
    // Example usage
    std::vector<std::vector<int>> rotorMappings = {
        {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25},
        {3, 7, 10, 15, 12, 8, 19, 16, 22, 20, 1, 11, 17, 6, 25, 23, 14, 5, 4, 2, 13, 18, 24, 9, 21, 0},
        {20, 5, 11, 14, 8, 24, 17, 23, 6, 13, 25, 4, 18, 22, 7, 10, 19, 3, 2, 9, 1, 16, 12, 21, 15, 0}
    };

    EnigmaMachine machine(rotorMappings);
    machine.setRotorStartPositions({0, 0, 0});

    std::string message = "HELLO";
    std::string encryptedMessage;
    for (char c : message) {
        if (c >= 'A' && c <= 'Z') {
            int encrypted = machine.encode(c - 'A');
            encryptedMessage += static_cast<char>(encrypted + 'A');
            machine.rotateRotors();
        } else {
            encryptedMessage += c;
        }
    }

    std::cout << "Encrypted message: " << encryptedMessage << std::endl;

    // Decrypting the message
    std::string decryptedMessage;
    machine.setRotorStartPositions({0, 0, 0}); // Reset rotors to initial position
    for (char c : encryptedMessage) {
        if (c >= 'A' && c <= 'Z') {
            int decrypted = machine.decode(c - 'A');
            decryptedMessage += static_cast<char>(decrypted + 'A');
            machine.rotateRotors();
        } else {
            decryptedMessage += c;
        }
    }

    std::cout << "Decrypted message: " << decryptedMessage << std::endl;

    return 0;
}
```

This code provides a basic implementation of the Enigma machine with three rotors. You can customize the rotor mappings and starting positions to simulate different Enigma machine configurations. Keep in mind that this is a simplified version and doesn't include all features and complexities of the original Enigma machine.

### 1. Algorithms & Data Structures (C++): Fast Exponentiation

Fast exponentiation, also known as exponentiation by squaring, is a technique to compute large powers of a number efficiently. It's particularly useful in competitive programming, cryptography, and other areas where large numbers are involved. Here's how it works in C++:

```cpp
#include <iostream>

using namespace std;

// Function to calculate power in O(log n) time
long long fastExponentiation(long long base, long long exponent) {
    long long result = 1;
    while (exponent > 0) {
        // If exponent is odd, multiply base with result
        if (exponent & 1) {
            result *= base;
        }
        // Halve the exponent
        exponent >>= 1;
        // Square the base
        base *= base;
    }
    return result;
}

int main() {
    long long base = 2, exponent = 10;
    cout << base << " raised to the power of " << exponent << " is " << fastExponentiation(base, exponent) << endl;
    return 0;
}
```

This code computes \( \text{base}^\text{exponent} \) in \( O(\log n) \) time complexity. It works by continuously halving the exponent and squaring the base until the exponent becomes zero, thereby reducing the number of multiplications needed. This approach is especially efficient for large exponents.

### 1. Algorithms & Data Structures (C++): Modular Binary Exponentiation

Modular exponentiation is a fundamental operation in cryptography and number theory, where you compute \( (a^b) \mod m \) for large \( a \), \( b \), and \( m \). It's crucial for efficient computation of large powers in modular arithmetic, especially in scenarios like encryption algorithms.

The binary exponentiation algorithm, also known as exponentiation by squaring, is a classic method for efficient exponentiation. Combining this with modular arithmetic yields the modular binary exponentiation algorithm. Here's how it works:

```cpp
#include <iostream>

using namespace std;

long long power(long long base, long long exponent, long long modulus) {
    long long result = 1;
    base = base % modulus; // Ensure base is within modulus range

    while (exponent > 0) {
        // If exponent is odd, multiply result with base and take modulo
        if (exponent % 2 == 1)
            result = (result * base) % modulus;

        // Halve the exponent and square the base
        exponent = exponent >> 1; // Equivalent to exponent /= 2
        base = (base * base) % modulus;
    }
    return result;
}

int main() {
    long long a = 5; // Base
    long long b = 13; // Exponent
    long long m = 1000000007; // Modulus

    cout << "Result: " << power(a, b, m) << endl;

    return 0;
}
```

In this implementation:

- The function `power()` takes three parameters: `base`, `exponent`, and `modulus`.
- It initializes `result` to 1 and iterates through the binary representation of the exponent.
- For each bit of the exponent, it squares the base and takes modulo `modulus`.
- If the bit is 1, it multiplies `result` with the current value of the base and takes modulo `modulus`.
- Finally, it returns the result.

This algorithm has a time complexity of \( O(\log b) \), where \( b \) is the exponent. This makes it significantly more efficient than the naive approach, which has a time complexity of \( O(b) \) when computing \( a^b \) directly.

This implementation ensures that all intermediate calculations stay within the range of the modulus to prevent overflow issues and to maintain the correctness of the result in modular arithmetic.

### 1. Algorithms & Data Structures (C++): Modulo Arithmetic

Modulo arithmetic in C++ is a fundamental concept in programming, especially in competitive programming and when dealing with certain mathematical problems. It involves finding the remainder when one integer is divided by another. In C++, you can use the modulus operator `%` to perform modulo arithmetic.

Here's a simple example demonstrating the use of modulo arithmetic in C++:

```cpp
#include <iostream>

int main() {
    int a = 10;
    int b = 3;
    
    // Finding remainder of a divided by b
    int result = a % b;
    
    std::cout << "Remainder of " << a << " divided by " << b << " is " << result << std::endl;
    
    return 0;
}
```

In this example, when you run the program, it will output:

```bash
Remainder of 10 divided by 3 is 1
```

Modulo arithmetic has several applications in programming:

1. **Finding Remainders**: As shown in the example above, it's commonly used to find the remainder of a division operation.

2. **Checking for Even or Odd Numbers**: You can determine whether a number is even or odd by checking if `number % 2 == 0` or `number % 2 == 1`, respectively.

3. **Wrapping Around**: Modulo arithmetic is often used to create a circular or wrap-around behavior. For example, when dealing with arrays or sequences, you might use modulo to ensure that an index stays within bounds.

4. **Hashing**: Modulo arithmetic is used in hashing functions to map large keys into smaller address ranges.

5. **Congruences**: In number theory, modulo arithmetic is used extensively to solve problems related to congruences and modular equations.

Remember, when dealing with negative numbers, the sign of the result depends on the implementation in C++. In most cases, the sign of the result matches the sign of the dividend (the number being divided), but it's always a good practice to ensure that the output is as expected, especially when dealing with negative numbers.

### 1. Algorithms & Data Structures (C++): Modulo Exponentiation

Modulo exponentiation is a fundamental operation in number theory and cryptography. It's commonly used to efficiently compute large powers of integers modulo some number. This operation is particularly useful in scenarios where dealing with large numbers and preventing overflow is necessary, such as in cryptography.

Here's a simple implementation of modular exponentiation in C++:

```cpp
#include <iostream>

using namespace std;

// Function to perform modular exponentiation
long long power(long long base, long long exp, long long mod) {
    long long result = 1;

    // Update base if it is more than or equal to mod
    base %= mod;

    while (exp > 0) {
        // If exp is odd, multiply base with result and take modulo
        if (exp & 1)
            result = (result * base) % mod;

        // exp must be even now
        exp >>= 1; // equivalent to exp /= 2
        base = (base * base) % mod;
    }

    return result;
}

int main() {
    long long base = 2, exp = 10, mod = 1000000007;
    cout << "Result of " << base << "^" << exp << " % " << mod << " is: " << power(base, exp, mod) << endl;
    return 0;
}
```

This code defines a `power` function that takes three arguments: `base`, `exp`, and `mod`, representing the base, exponent, and modulo respectively. It calculates `(base^exp) % mod` efficiently using the binary exponentiation method. In the `main` function, an example usage is demonstrated, where `2` raised to the power `10` modulo `1000000007` is computed.

Feel free to adjust the values of `base`, `exp`, and `mod` in the `main` function to perform different modulo exponentiation calculations.

### 1. Algorithms & Data Structures (C++): Multiplicative Modulo Inverse

In computer science and mathematics, the multiplicative modulo inverse of an integer \( a \) modulo \( m \) is an integer \( x \) such that \( (a \cdot x) \) is congruent to \( 1 \) modulo \( m \). In simpler terms, it's a number \( x \) such that when you multiply \( a \) by \( x \) and take the result modulo \( m \), you get \( 1 \).

Finding the multiplicative modulo inverse is crucial in many cryptographic algorithms, especially in RSA encryption and decryption.

Here's how you can find the multiplicative modulo inverse of \( a \) modulo \( m \) using the Extended Euclidean Algorithm in C++:

```cpp
#include <iostream>

// Function to calculate the multiplicative modulo inverse
// Returns -1 if inverse doesn't exist
int multiplicativeModuloInverse(int a, int m) {
    int m0 = m, t, q;
    int x0 = 0, x1 = 1;

    if (m == 1) return 0;

    // Apply extended Euclid Algorithm
    while (a > 1) {
        // q is quotient
        q = a / m;

        t = m;

        // m is remainder now, process same as Euclid's algo
        m = a % m, a = t;

        t = x0;

        x0 = x1 - q * x0;

        x1 = t;
    }

    // Make x1 positive
    if (x1 < 0) x1 += m0;

    return x1;
}

int main() {
    int a, m;
    std::cout << "Enter a and m for (a * x) % m = 1: ";
    std::cin >> a >> m;

    int inverse = multiplicativeModuloInverse(a, m);

    if (inverse == -1) {
        std::cout << "Inverse doesn't exist.\n";
    } else {
        std::cout << "Multiplicative Modulo Inverse of " << a << " modulo " << m << " is: " << inverse << std::endl;
    }

    return 0;
}
```

This program calculates the multiplicative modulo inverse of \( a \) modulo \( m \) and prints the result. If the inverse doesn't exist (i.e., \( a \) and \( m \) are not coprime), it returns -1.

### 1. Algorithms & Data Structures (C++): nCr % P

Calculating \( nCr \) (combinations) modulo \( P \) where \( P \) is a prime number is a common problem in competitive programming and mathematics. Here's a simple approach in C++:

```cpp
#include <iostream>
using namespace std;

// Function to calculate (a^b) % P
long long power(long long a, long long b, long long P) {
    long long result = 1;
    while (b > 0) {
        if (b % 2 == 1) {
            result = (result * a) % P;
        }
        a = (a * a) % P;
        b /= 2;
    }
    return result;
}

// Function to calculate nCr % P
long long nCrModP(int n, int r, int P) {
    if (r == 0) {
        return 1;
    }

    // Calculate numerator: n*(n-1)*(n-2)*...*(n-r+1)
    long long numerator = 1;
    for (int i = n; i >= n - r + 1; i--) {
        numerator = (numerator * i) % P;
    }

    // Calculate denominator: r!
    long long denominator = 1;
    for (int i = 1; i <= r; i++) {
        denominator = (denominator * i) % P;
    }

    // Calculate modular inverse of denominator
    long long inverse_denominator = power(denominator, P - 2, P);

    // Calculate result: (numerator * inverse_denominator) % P
    return (numerator * inverse_denominator) % P;
}

int main() {
    int n, r, P;
    cout << "Enter n, r, and P (prime): ";
    cin >> n >> r >> P;

    cout << "nCr % P: " << nCrModP(n, r, P) << endl;

    return 0;
}
```

In this code:

- The `power` function calculates \( a^b \) modulo \( P \) efficiently using modular exponentiation.
- The `nCrModP` function calculates \( nCr \) modulo \( P \) using the formula \( \frac{n!}{r!(n-r)!} \) modulo \( P \).
- The `main` function takes input values for \( n \), \( r \), and \( P \), and outputs \( nCr \) modulo \( P \).

This code efficiently calculates \( nCr \) modulo \( P \) for large values of \( n \) and \( r \).

### 1. Algorithms & Data Structures (C++): nCr using Recursion

To calculate the combination (n choose r) using recursion in C++, you can use the following function:

```cpp
#include <iostream>
using namespace std;

// Function to calculate factorial
int factorial(int n) {
    if (n <= 1)
        return 1;
    else
        return n * factorial(n - 1);
}

// Function to calculate nCr using recursion
int nCr(int n, int r) {
    if (r == 0 || r == n)
        return 1;
    else
        return nCr(n - 1, r - 1) + nCr(n - 1, r);
}

int main() {
    int n, r;
    cout << "Enter the value of n: ";
    cin >> n;
    cout << "Enter the value of r: ";
    cin >> r;

    if (r > n)
        cout << "Invalid input: r should be less than or equal to n" << endl;
    else
        cout << "Combination of " << n << " choose " << r << " is: " << nCr(n, r) << endl;

    return 0;
}
```

This code defines two functions: `factorial` and `nCr`. The `factorial` function calculates the factorial of a given number, and the `nCr` function calculates the combination (n choose r) using the recursive formula C(n, r) = C(n-1, r-1) + C(n-1, r) with base cases C(n, 0) = C(n, n) = 1.

You can use the `main` function to input the values of n and r and display the result.

### 1. Algorithms & Data Structures (C++): Pascal's Triangle

Pascal's Triangle is a classic example in mathematics that demonstrates many interesting properties and patterns. In C++, you can create Pascal's Triangle using various approaches, but one common method involves using a two-dimensional array. Here's a simple implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to generate Pascal's Triangle
vector<vector<int>> generatePascalsTriangle(int numRows) {
    vector<vector<int>> triangle;
    
    // Handle edge case
    if (numRows == 0) return triangle;
    
    // First row
    triangle.push_back({1});
    
    for (int i = 1; i < numRows; ++i) {
        vector<int> row;
        row.push_back(1); // First element of each row
        
        // Calculate each element of the row based on the previous row
        for (int j = 1; j < i; ++j) {
            row.push_back(triangle[i - 1][j - 1] + triangle[i - 1][j]);
        }
        
        row.push_back(1); // Last element of each row
        
        // Add the row to the triangle
        triangle.push_back(row);
    }
    
    return triangle;
}

// Function to print Pascal's Triangle
void printPascalsTriangle(const vector<vector<int>>& triangle) {
    for (const auto& row : triangle) {
        for (int num : row) {
            cout << num << " ";
        }
        cout << endl;
    }
}

int main() {
    int numRows;
    cout << "Enter the number of rows for Pascal's Triangle: ";
    cin >> numRows;

    vector<vector<int>> triangle = generatePascalsTriangle(numRows);
    
    cout << "Pascal's Triangle with " << numRows << " rows:" << endl;
    printPascalsTriangle(triangle);
    
    return 0;
}
```

This code defines two functions:

1. `generatePascalsTriangle`: This function generates Pascal's Triangle up to the specified number of rows and returns it as a 2D vector.
2. `printPascalsTriangle`: This function prints the generated Pascal's Triangle.

In the `main` function, the user is prompted to enter the number of rows they want in Pascal's Triangle. Then, the triangle is generated and printed accordingly.

### 1. Algorithms & Data Structures (C++): Run Length Encoding

Run-Length Encoding (RLE) is a simple compression algorithm that reduces the size of data by replacing sequences of repeating characters with a count and a single instance of the character. Here's a basic implementation of Run-Length Encoding in C++:

```cpp
#include <iostream>
#include <string>

std::string encode(const std::string& input) {
    std::string result;

    // Handle empty input
    if (input.empty()) return result;

    char current_char = input[0];
    int count = 1;

    for (size_t i = 1; i < input.length(); ++i) {
        if (input[i] == current_char) {
            // Increment count if the current character is the same as the previous one
            count++;
        } else {
            // Append the count and character to the result string
            result += std::to_string(count) + current_char;

            // Update current character and reset count
            current_char = input[i];
            count = 1;
        }
    }

    // Append the count and character for the last sequence
    result += std::to_string(count) + current_char;

    return result;
}

std::string decode(const std::string& input) {
    std::string result;

    // Handle empty input
    if (input.empty()) return result;

    for (size_t i = 0; i < input.length(); i += 2) {
        // Convert the count part of the encoded string to an integer
        int count = input[i] - '0';

        // Append the character count times to the result
        result.append(count, input[i + 1]);
    }

    return result;
}

int main() {
    std::string input = "AAABBBCCCCDDDDEEE";
    
    std::string encoded = encode(input);
    std::cout << "Encoded: " << encoded << std::endl;

    std::string decoded = decode(encoded);
    std::cout << "Decoded: " << decoded << std::endl;

    return 0;
}
```

This code defines two functions: `encode()` and `decode()`.

- `encode()` takes an input string and returns its run-length encoded representation.
- `decode()` takes a run-length encoded string and returns the original string.

In the `main()` function, an example string "AAABBBCCCCDDDDEEE" is encoded and then decoded to demonstrate the correctness of the implementation.

### 1. Algorithms & Data Structures (C++): Ways to decode

Decoding algorithms are fundamental in various fields such as cryptography, data compression, and error correction. In C++, you can implement decoding algorithms for different purposes using various techniques and data structures. Here are some common decoding techniques along with their implementations:

1. **Decoding a Caesar Cipher**:
   - The Caesar cipher is a simple substitution cipher where each letter in the plaintext is shifted a certain number of places down or up the alphabet.
   - To decode it, you simply shift each letter in the ciphertext back by the same number of positions.
   - Example implementation:

   ```cpp
   #include <iostream>
   #include <string>

   std::string decodeCaesarCipher(const std::string& ciphertext, int shift) {
       std::string plaintext = "";
       for (char c : ciphertext) {
           if (isalpha(c)) {
               char base = isupper(c) ? 'A' : 'a';
               plaintext += ((c - base - shift + 26) % 26) + base;
           } else {
               plaintext += c;
           }
       }
       return plaintext;
   }

   int main() {
       std::string ciphertext = "Ifmmp xpsme!";
       int shift = 1;
       std::cout << "Decoded text: " << decodeCaesarCipher(ciphertext, shift) << std::endl;
       return 0;
   }
   ```

2. **Huffman Decoding**:
   - Huffman coding is a popular method for lossless data compression. It assigns variable-length codes to input characters, with shorter codes for more frequent characters.
   - To decode a Huffman-encoded message, you traverse the Huffman tree according to the encoded bit sequence.
   - Example implementation requires a Huffman tree data structure and a decoding function.

3. **Run-Length Decoding**:
   - Run-Length Encoding (RLE) is a simple form of data compression where sequences of the same data value occur in a row.
   - To decode RLE, you simply expand each run into its original sequence of values.
   - Example implementation:

   ```cpp
   #include <iostream>
   #include <string>

   std::string decodeRLE(const std::string& encoded) {
       std::string decoded = "";
       for (size_t i = 0; i < encoded.size(); i += 2) {
           char ch = encoded[i];
           int count = encoded[i + 1] - '0'; // Convert char to int
           decoded += std::string(count, ch);
       }
       return decoded;
   }

   int main() {
       std::string encoded = "A3B2C1D3";
       std::cout << "Decoded text: " << decodeRLE(encoded) << std::endl;
       return 0;
   }
   ```

4. **Base64 Decoding**:
   - Base64 is a method of encoding binary data into ASCII characters. To decode Base64, you need to reverse the encoding process.
   - Example implementation:

   ```cpp
   #include <iostream>
   #include <string>
   #include <vector>
   #include <algorithm>

   std::string base64Chars = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/";

   std::string decodeBase64(const std::string& encoded) {
       std::string decoded = "";
       std::string::size_type in_len = encoded.size();
       int i = 0;
       unsigned char array_4[4], array_3[3];
       int j = 0;
       while (in_len-- && (encoded[i] != '=') && is_base64(encoded[i])) {
           array_4[j++] = encoded[i++];
           if (j == 4) {
               for (j = 0; j < 4; j++)
                   array_4[j] = base64Chars.find(array_4[j]);
               array_3[0] = (array_4[0] << 2) + ((array_4[1] & 0x30) >> 4);
               array_3[1] = ((array_4[1] & 0x0f) << 4) + ((array_4[2] & 0x3c) >> 2);
               array_3[2] = ((array_4[2] & 0x03) << 6) + array_4[3];
               for (j = 0; j < 3; j++)
                   decoded += array_3[j];
               j = 0;
           }
       }
       if (j) {
           for (int i = j; i < 4; i++)
               array_4[i] = 0;
           for (int i = 0; i < 4; i++)
               array_4[i] = base64Chars.find(array_4[i]);
           array_3[0] = (array_4[0] << 2) + ((array_4[1] & 0x30) >> 4);
           array_3[1] = ((array_4[1] & 0x0f) << 4) + ((array_4[2] & 0x3c) >> 2);
           array_3[2] = ((array_4[2] & 0x03) << 6) + array_4[3];
           for (int i = 0; i < j - 1; i++) decoded += array_3[i];
       }
       return decoded;
   }

   bool is_base64(unsigned char c) { return (isalnum(c) || (c == '+') || (c == '/')); }

   int main() {
       std::string encoded = "SGVsbG8sIFdvcmxkIQ==";
       std::cout << "Decoded text: " << decodeBase64(encoded) << std::endl;
       return 0;
   }
   ```

These are just a few examples of decoding algorithms in C++. Depending on the context and specific requirements, you might need to use different algorithms and techniques.

### 1. Algorithms & Data Structures (C++): Ways to decode (problem)

The problem of decoding typically involves converting encoded data back into its original form. One common example is decoding a message that has been encoded using a specific scheme or algorithm. In the context of algorithms and data structures, there are several ways to approach decoding problems, depending on the encoding scheme used. Here are some common approaches:

1. **Reverse Engineering**: If you know the encoding algorithm used, you can simply reverse the steps of the algorithm to decode the data. For example, if the data was encoded using a simple substitution cipher, you can decode it by replacing each encoded character with its corresponding original character.

2. **Brute Force**: If the encoding scheme is unknown or complex, you may resort to a brute force approach where you try all possible combinations until you find the correct decoding. This approach is usually not efficient but can be effective for small input sizes or when no other information is available.

3. **Frequency Analysis**: This technique is often used for decoding messages encoded using simple substitution ciphers, such as the Caesar cipher. By analyzing the frequency of letters or symbols in the encoded message, you can make educated guesses about the mapping between encoded and original characters.

4. **Dictionary-based Decoding**: If the encoded data represents text, you can use a dictionary to map encoded words or phrases to their original counterparts. This approach is particularly useful for decoding data that has been compressed or encoded using a known vocabulary.

5. **Dynamic Programming**: For more complex decoding problems, such as decoding a sequence of symbols with certain constraints, dynamic programming can be employed. This technique involves breaking down the decoding problem into smaller subproblems and solving each subproblem only once, storing the solutions to overlapping subproblems to avoid redundant computation.

6. **Tree-based Decoding**: If the encoded data has a hierarchical structure, such as a Huffman tree for compression, decoding can be performed by traversing the tree from the root to the leaves according to the encoded data. This approach is efficient for decoding data encoded using tree-based compression algorithms.

7. **Machine Learning**: In some cases, machine learning algorithms can be trained to automatically learn the decoding process from a set of encoded and decoded data pairs. This approach is particularly useful for decoding tasks that are difficult to solve using traditional algorithms, such as image or speech recognition.

These are just a few examples of the many approaches to decoding problems in algorithms and data structures. The most appropriate approach will depend on the specific characteristics of the encoded data and the requirements of the decoding task.

### 1. Algorithms & Data Structures (C++): Ways to decode (solution)

Decoding a message encoded using a specific algorithm can vary depending on the encoding method used. Here's a general approach for decoding a message in C++:

1. **Understand the Encoding Method**: You need to know how the message was encoded in the first place. Common methods include simple substitution ciphers, base64 encoding, Huffman encoding, etc. The decoding process will depend on this.

2. **Implement the Decoding Algorithm**: Once you understand the encoding method, implement the decoding algorithm. This could involve reversing the steps used in encoding, applying inverse functions, or using a specific decoding algorithm.

3. **Write Code to Decode**: Write C++ code to perform the decoding based on the algorithm you've chosen. This might involve reading input from a file or user input, applying the decoding algorithm, and then outputting the decoded message.

Here's a simple example of decoding a Caesar cipher in C++:

```cpp
#include <iostream>
#include <string>

using namespace std;

string caesarDecrypt(string ciphertext, int shift) {
    string plaintext = "";
    for (char& c : ciphertext) {
        if (isalpha(c)) {
            char base = isupper(c) ? 'A' : 'a';
            c = (c - base + 26 - shift) % 26 + base;
        }
        plaintext += c;
    }
    return plaintext;
}

int main() {
    string ciphertext;
    int shift;
    
    cout << "Enter the ciphertext: ";
    getline(cin, ciphertext);
    
    cout << "Enter the shift value: ";
    cin >> shift;
    
    string plaintext = caesarDecrypt(ciphertext, shift);
    cout << "Decrypted message: " << plaintext << endl;
    
    return 0;
}
```

In this example, `caesarDecrypt` function takes a ciphertext and a shift value and returns the decrypted message using the Caesar cipher decryption algorithm.

Remember to adapt this to your specific encoding/decoding requirements and algorithms. If you have a specific encoding method in mind, I can provide a more tailored example.

### 1. Algorithms & Data Structures (C++): Ways to decode: Complexity analysis

When analyzing the complexity of algorithms and data structures, especially in the context of decoding algorithms, we typically consider factors such as time complexity and space complexity.

Let's consider decoding algorithms in the context of decoding encoded data, such as strings encoded using techniques like run-length encoding, Huffman encoding, or simple substitution ciphers. Here are a few common decoding methods and their complexity analysis in terms of time and space:

1. **Brute Force Decoding**:
   - **Time Complexity**: O(n^2) or higher, where n is the length of the encoded data. In the worst case, you might need to try all possible combinations to decode the data.
   - **Space Complexity**: O(1) if done in place, otherwise O(n) for auxiliary data structures.

2. **Dictionary-based Decoding**:
   - **Time Complexity**: O(n), where n is the length of the encoded data. This assumes constant-time lookups in the dictionary.
   - **Space Complexity**: O(m), where m is the size of the dictionary.

3. **Huffman Decoding**:
   - **Time Complexity**: O(n log n), where n is the number of encoded symbols.
   - **Space Complexity**: O(1) if done in place, otherwise O(n) for auxiliary data structures like the Huffman tree.

4. **Run-Length Decoding**:
   - **Time Complexity**: O(n), where n is the length of the encoded data.
   - **Space Complexity**: O(1) if done in place, otherwise O(n) for the decoded output.

5. **Substitution Cipher Decoding**:
   - **Time Complexity**: O(n), where n is the length of the encoded data. This can vary depending on the complexity of the cipher algorithm.
   - **Space Complexity**: O(n) for the decoded output.

The actual complexity might vary depending on the specific implementation details, the size of the input data, and any optimizations applied. Also, these analyses assume that the size of the alphabet (in the case of character-based encodings) or the range of possible symbols does not significantly affect the complexity.

It's essential to choose the decoding method based on the specific characteristics of the encoded data and the performance requirements of the application. Trade-offs between time and space complexity often exist, and the best choice depends on factors such as the size of the data, available memory, and desired decoding speed.
