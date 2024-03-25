

### 1. Algorithms & Data Structures (C++): Polynomial

A polynomial in mathematics is an expression consisting of variables (or indeterminates) and coefficients, that involves only the operations of addition, subtraction, multiplication, and non-negative integer exponentiation of variables. In the context of computer science and algorithms, representing and manipulating polynomials efficiently is a common task, often encountered in areas like computational geometry, numerical analysis, and computer graphics.

In C++, you can represent a polynomial using various data structures. One common approach is to use an array or a vector to store the coefficients of each term, with the index of the array/vector representing the exponent of the corresponding term.

Here's a simple implementation of a polynomial class in C++:

```cpp
#include <iostream>
#include <vector>

class Polynomial {
private:
    std::vector<double> coefficients;

public:
    // Constructor to initialize the polynomial with given coefficients
    Polynomial(const std::vector<double>& coeffs) : coefficients(coeffs) {}

    // Evaluate the polynomial at a given value of x
    double evaluate(double x) const {
        double result = 0.0;
        double x_power = 1.0;

        for (double coeff : coefficients) {
            result += coeff * x_power;
            x_power *= x;
        }

        return result;
    }

    // Print the polynomial
    void print() const {
        int degree = coefficients.size() - 1;
        for (int i = degree; i >= 0; --i) {
            if (coefficients[i] != 0.0) {
                if (i < degree)
                    std::cout << (coefficients[i] > 0 ? " + " : " - ");
                if (i > 0)
                    std::cout << abs(coefficients[i]) << "x^" << i;
                else
                    std::cout << abs(coefficients[i]);
            }
        }
        std::cout << std::endl;
    }
};

int main() {
    std::vector<double> coeffs = {2.0, -3.0, 1.0}; // represents 2x^2 - 3x + 1
    Polynomial poly(coeffs);

    poly.print(); // Output: 2x^2 - 3x + 1
    std::cout << "Value at x = 2: " << poly.evaluate(2.0) << std::endl; // Output: 3

    return 0;
}
```

This implementation allows you to create polynomials with arbitrary coefficients and evaluate them at specific values of x. You can extend this implementation further to support operations like addition, subtraction, multiplication, and division of polynomials, as well as other functionalities as per your requirements.

### 1. Algorithms & Data Structures (C++): Polynomial Addition

Polynomial addition involves adding two polynomials together to obtain a single polynomial. Each polynomial is typically represented as a list of terms, where each term consists of a coefficient and an exponent. Here's a C++ implementation to add two polynomials:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Structure to represent a term in the polynomial
struct Term {
    int coefficient;
    int exponent;
};

// Function to add two polynomials
vector<Term> addPolynomials(const vector<Term>& poly1, const vector<Term>& poly2) {
    vector<Term> result;
    int i = 0, j = 0;

    // Traverse both polynomials
    while (i < poly1.size() && j < poly2.size()) {
        // If exponents are same, add their coefficients
        if (poly1[i].exponent == poly2[j].exponent) {
            int coeff = poly1[i].coefficient + poly2[j].coefficient;
            if (coeff != 0) {
                result.push_back({coeff, poly1[i].exponent});
            }
            i++;
            j++;
        } 
        // If exponent of first polynomial is greater, add its term
        else if (poly1[i].exponent > poly2[j].exponent) {
            result.push_back(poly1[i]);
            i++;
        } 
        // If exponent of second polynomial is greater, add its term
        else {
            result.push_back(poly2[j]);
            j++;
        }
    }

    // Add remaining terms of the first polynomial
    while (i < poly1.size()) {
        result.push_back(poly1[i]);
        i++;
    }

    // Add remaining terms of the second polynomial
    while (j < poly2.size()) {
        result.push_back(poly2[j]);
        j++;
    }

    return result;
}

// Function to display a polynomial
void displayPolynomial(const vector<Term>& poly) {
    for (int i = 0; i < poly.size(); i++) {
        if (i > 0 && poly[i].coefficient > 0) {
            cout << " + ";
        }
        cout << poly[i].coefficient << "x^" << poly[i].exponent;
    }
    cout << endl;
}

int main() {
    // Example polynomials
    vector<Term> poly1 = {{3, 2}, {2, 1}, {4, 0}};
    vector<Term> poly2 = {{-1, 2}, {3, 1}, {1, 0}};

    cout << "First polynomial: ";
    displayPolynomial(poly1);

    cout << "Second polynomial: ";
    displayPolynomial(poly2);

    // Add polynomials
    vector<Term> result = addPolynomials(poly1, poly2);

    cout << "Sum of polynomials: ";
    displayPolynomial(result);

    return 0;
}
```

This code defines a `Term` struct to represent each term in a polynomial. The `addPolynomials` function takes two vectors representing polynomials as input and returns their sum as another vector. Finally, `displayPolynomial` function is provided to display the polynomial nicely.

### 1. Algorithms & Data Structures (C++): Polynomial Evaluation

Polynomial evaluation is a common problem in computer science and involves calculating the value of a polynomial for a given input. In C++, you can implement polynomial evaluation using various methods. One common approach is to use the Horner's method, which efficiently evaluates a polynomial using a series of multiplications and additions.

Here's a basic implementation of polynomial evaluation using Horner's method in C++:

```cpp
#include <iostream>
#include <vector>

// Function to evaluate a polynomial using Horner's method
double evaluatePolynomial(const std::vector<double>& coefficients, double x) {
    int degree = coefficients.size() - 1; // Degree of the polynomial
    double result = coefficients[degree]; // Initialize result with coefficient of highest degree

    // Iterate from the second highest degree to 0
    for (int i = degree - 1; i >= 0; i--) {
        result = result * x + coefficients[i]; // Update result using Horner's method
    }

    return result;
}

int main() {
    // Example usage
    std::vector<double> coefficients = {2.0, -3.0, 1.0}; // Coefficients of the polynomial: 2x^2 - 3x + 1
    double x = 3.0; // Value of x for evaluation
    double result = evaluatePolynomial(coefficients, x);
    
    std::cout << "Result of polynomial evaluation: " << result << std::endl;

    return 0;
}
```

In this code:

- The `evaluatePolynomial` function takes a vector of coefficients of the polynomial and the value of `x` for evaluation.
- It initializes the `result` with the coefficient of the highest degree term.
- It iterates through the coefficients in reverse order (from the second highest degree to 0), updating the result using Horner's method.
- Finally, it returns the evaluated result.

You can modify the coefficients vector and the value of `x` in the `main` function to evaluate different polynomials.

### 1. Algorithms & Data Structures (C++): Polynomial Hash

Polynomial hashing is a technique used in computer science, particularly in string processing and cryptography, to quickly compute hash values for strings or sequences of data. In the context of algorithms and data structures, polynomial hashing is often used for string matching algorithms like Rabin-Karp or in hashing-based data structures like hash tables.

The basic idea behind polynomial hashing is to treat a string or a sequence of data as a polynomial with coefficients corresponding to the characters or elements in the string. Each character or element is assigned a numerical value, typically based on its Unicode value or its position in the alphabet, and these values are then used as coefficients in the polynomial. The polynomial is then evaluated at a specific base to produce a hash value.

Here's a simplified example in C++ to demonstrate polynomial hashing for strings:

```cpp
#include <iostream>
#include <string>
#include <cmath>

using namespace std;

const int BASE = 31; // Base for polynomial hashing

// Function to compute the hash value of a string
unsigned long long computeHash(const string& str) {
    unsigned long long hashValue = 0;
    int power = 0;
    for (char c : str) {
        hashValue += (c - 'a' + 1) * pow(BASE, power); // Assuming lowercase English letters
        power++;
    }
    return hashValue;
}

int main() {
    string str = "hello";
    unsigned long long hashValue = computeHash(str);
    cout << "Hash value of '" << str << "': " << hashValue << endl;
    return 0;
}
```

In this example:
- We use a base value of 31, though in practice, prime numbers are often chosen as the base for better distribution of hash values.
- The `computeHash` function takes a string as input and iterates over each character, treating it as a coefficient in the polynomial. It computes the hash value by multiplying each character's numerical value by the base raised to the power corresponding to its position in the string.
- Finally, the hash value is returned.

Keep in mind that this is a basic example, and in practical implementations, additional considerations are needed, such as handling collisions, choosing appropriate base values, and implementing optimizations for performance. Additionally, modulus operation is usually applied to the result to fit the hash value into a certain range (e.g., the size of a hash table).

### 1. Algorithms & Data Structures (C++): Polynomial Representation

In C++, polynomials can be represented in several ways, but one common method is to use an array or a linked list to store the coefficients of each term. Here's a basic implementation using an array:

```cpp
#include <iostream>
#include <cmath>

class Polynomial {
private:
    int degree; // Degree of the polynomial
    double* coefficients; // Array to store coefficients

public:
    // Constructor
    Polynomial(int deg) {
        degree = deg;
        coefficients = new double[degree + 1]; // +1 for the constant term
        for (int i = 0; i <= degree; ++i) {
            coefficients[i] = 0.0; // Initialize all coefficients to 0
        }
    }

    // Destructor
    ~Polynomial() {
        delete[] coefficients;
    }

    // Function to set coefficient of a term
    void setCoefficient(int power, double coefficient) {
        if (power >= 0 && power <= degree) {
            coefficients[power] = coefficient;
        } else {
            std::cout << "Invalid power!" << std::endl;
        }
    }

    // Function to evaluate the polynomial at a given value of x
    double evaluate(double x) {
        double result = 0.0;
        for (int i = 0; i <= degree; ++i) {
            result += coefficients[i] * std::pow(x, i);
        }
        return result;
    }
};

int main() {
    // Create a polynomial of degree 3
    Polynomial poly(3);

    // Set coefficients
    poly.setCoefficient(0, 2.0);
    poly.setCoefficient(1, 3.0);
    poly.setCoefficient(2, -1.0);
    poly.setCoefficient(3, 0.5);

    // Evaluate polynomial at x = 2
    double result = poly.evaluate(2);
    std::cout << "Result: " << result << std::endl;

    return 0;
}
```

This implementation allows you to create a polynomial object, set its coefficients, and evaluate the polynomial at a given value of x.

Another approach is to use a linked list to represent the polynomial terms, with each node containing the coefficient and the power of x. This allows for efficient addition, subtraction, and multiplication of polynomials. Let me know if you'd like to see an implementation using a linked list!

### 1. Algorithms & Data Structures (C++): Polynomial Representation using Linked List

Representing polynomials using linked lists is a classic example in data structures. In C++, you can create a linked list to store the terms of a polynomial where each node represents a term containing the coefficient and exponent. Here's a basic implementation:

```cpp
#include <iostream>

struct Term {
    int coefficient;
    int exponent;
    Term* next;

    Term(int coef, int exp) : coefficient(coef), exponent(exp), next(nullptr) {}
};

class Polynomial {
private:
    Term* head;

public:
    Polynomial() : head(nullptr) {}

    void insert(int coef, int exp) {
        Term* newTerm = new Term(coef, exp);
        if (!head || exp > head->exponent) {
            newTerm->next = head;
            head = newTerm;
        } else {
            Term* current = head;
            while (current->next && exp < current->next->exponent) {
                current = current->next;
            }
            newTerm->next = current->next;
            current->next = newTerm;
        }
    }

    void display() {
        Term* current = head;
        while (current) {
            std::cout << current->coefficient << "x^" << current->exponent;
            if (current->next)
                std::cout << " + ";
            current = current->next;
        }
        std::cout << std::endl;
    }

    ~Polynomial() {
        Term* current = head;
        while (current) {
            Term* temp = current;
            current = current->next;
            delete temp;
        }
    }
};

int main() {
    Polynomial poly;
    poly.insert(5, 2);
    poly.insert(-3, 1);
    poly.insert(2, 0);
    poly.display();

    return 0;
}
```

In this code:

- `Term` represents each term of the polynomial, containing the coefficient, exponent, and a pointer to the next term.
- `Polynomial` class provides methods to insert terms into the polynomial and display the polynomial.
- `insert` method inserts a term into the polynomial in descending order of exponent.
- `display` method prints the polynomial in a human-readable format.
- `main` function demonstrates how to use the `Polynomial` class by creating a polynomial with terms 5x^2 - 3x + 2 and displaying it.

You can extend this implementation by adding operations like addition, subtraction, multiplication, etc., on polynomials.
