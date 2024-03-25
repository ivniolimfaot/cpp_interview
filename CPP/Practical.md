# Practical

## Exersices

### Write a program to check number is palindrome or not

### 44. Write a program to find the factorial of a number

### 45. Program to find the frequency of a number

### 1. Write a C++ Program to Check Whether a Number is a Positive or Negative Number

### 2. Write a Program to Find the Greatest of the Three Numbers

### 3. C++ Program To Check Whether Number is Even Or Odd

### 4. Write a Program to Find the ASCII Value of a Character

### 5. Write a Program to Check Whether a Character is a Vowel or Consonant

### 6. Write a Program to Print Check Whether a Character is an Alphabet or Not

### 7. Write a Program to Find the Length of the String Without using strlen() Function

### 8. Write a Program to Toggle Each Character in a String

### 9. Write a Program to Count the Number of Vowels

### 10. Write a Program to Remove the Vowels from a String

### 11. Write a Program to Remove All Characters From a String Except Alphabets

### 12. Write a Program to Remove Spaces From a String

### 13. Write a Program to Find the Sum of the First N Natural Numbers

### 14. Write a Program to Find the Factorial of a Number Using Loops

### 15. Write a Program to Find a Leap Year or Not

### 16. Write a Program to Check the Prime Number

### 17. Write a Program to Check Palindrome

### 18. Write a Program to Check Whether a Number is an Armstrong Number or Not

### 19. Write a Program to Find the Nth Term of the Fibonacci Series

### 20. Write a Program to Calculate the Greatest Common Divisor of Two Numbers

### 21. Write a Program to Calculate the Lowest Common Multiple (LCM) of Two Numbers

### 22. Write a Program for Finding the Roots of a Quadratic Equation

### 23. Write a Program to Find the Smallest and Largest Element in an Array

### 24. Write a Program to Find the Second Smallest Element in an Array

### 25. Write a Program to Calculate the Sum of Elements in an Array

### 26. Write a Program to Check if the Given String is Palindrome or Not

### 27. Write a Program to Check if Two Strings are Anagram or Not

### 28. Write a Program to Print a Diamond Pattern

### 29. Write a Program to Print a Pyramid Pattern

### 30. Write a Program to Print the Hourglass Pattern

### 31. Write a Program to Print the Rotated Hourglass Pattern

### 32. Write a Program to Print a Simple Pyramid Pattern

### 33. Write a Program to print an Inverted Pyramid

### 34. Write a Program to Print a Triangle Star Pattern

### 35. Write a Program to Print Floyd’s Triangle

### 36. Write a Program to Print the Pascal Triangle

### 37. Write a Program to Print the Given String in Reverse Order

### 38. Write a C++ Program to Print the Given String in Reverse Order Using Recursion

### 39. Write a Program to Check if the Given String is Palindrome or not Using Recursion

### 40. Write a Program to Calculate the Length of the String Using Recursion

### 41. Write a Program to Calculate the Factorial of a Number Using Recursion

### 42. Write a Program to Count the Sum of Numbers in a String

### 43. Write a Program to Print All Natural Numbers up to N Without Using a Semi-Colon

### 44. Write a Program to  Swap the Values of Two Variables Without Using any Extra Variable

### 45. Write a Program to Print the Maximum Value of an Unsigned int Using One’s Complement (~) Operator

### 46. Write a Program to Check for the Equality of Two Numbers Without Using Arithmetic or Comparison Operator

### 47. Write a Program to Find the Maximum and Minimum of the Two Numbers Without Using the Comparison Operator

### 48. Write a Program for Octal to Decimal Conversion

### 49. Write a Program for Hexadecimal to Decimal Conversion

### 50. Write a Program for Decimal to Binary Conversion

### 51. Write a Program for Decimal Octal Conversion

### 52. Write a Program for Decimal to Hexadecimal Conversion

### 53. Write a Program for Binary to Octal Conversion

### 54. Write a Program for Octal to Binary Conversion  

### 55. Write a Program to Implement the Use of Encapsulation

### 56. Write a Program to Implement the Concept of Abstraction

### 60. Write a Program to Implement Single-Level Inheritance

### 61. Write a Program to Create a Class for Complex Numbers

### 62. Write a Program to Implement the Inch Feet System

### 63. Write a Program to Implement Bubble Sort

### 64. Write a Program to Implement Insertion Sort

### 65. Write a Program to Implement Selection Sort

### 66. Write a Program to Implement Merge Sort

### 67. Write a Program to Implement Quick Sort

### 68. Write a Program to Implement Linear Search

### 69. Write a Program to Implement Binary Search

### 70. Write a Program to Find the Index of a Given Element in a Vector

### 71. Write a Program to Remove Duplicate Elements in an Array Using STL

### 72. Write a Program to Sort an Array in Descending Order Using STL

### 73. Write a Program to Calculate the Frequency of Each Word in the Given String

### 74. Write a Program to Find k Maximum Elements of an Array in the Original Order

### 75. Write a Program to Find All Unique Subsets of a Given Set Using STL

### 76. Write a Program to Iterate Over a Queue Without Removing the Element

### 77. Write a Program for the Implementation of Stacks Using an  Array

### 78. Write a Program for the Implementation of a Queue Using an Array

### 79. Write a Program Implementation of Stacks Using a Queue

### 80. Write a Program to Implement a Stack Using the List in STL

### 81. Write a Program to Determine Array is a Subset of Another Array or Not

### 82. Write a Program for Finding the Circular Rotation of an Array by K Positions

### 83. Write a Program to Sort the First Half in Ascending Order and the Second Half in Descending

### 84. Write a Program to Print the Given String in Reverse Order

### 85. Write a Program to Print All Permutations of a String Using Recursion

### 86. Write a Program to Print All Permutations of a Given String in Lexicographically Sorted Order

### 87. Write a Program to Remove Brackets From an Algebraic Expression

### 88. Program to Perform Insert, Delete, and Print Operations Singly Linked List

### 89. Program to Perform Insert, Delete, and Print Operations Doubly Linked List

### 90. Program to Perform Insert, Delete, and Print Operations Circular Linked List

### 91. Program for Inorder Traversal in a Binary Tree

### 92. Program to Find All its Subsets From a Set of Positive Integers

### 93. Program for Preorder Traversal in a Binary Tree

### 94. Program for Postorder Traversal in a Binary Tree

### 95. Program for Level-Order Traversal in a Binary Tree

### 96. Write a Program for the Top View of a Binary Tree

### 97. Write a Program to Print the Bottom View of a Binary Tree

### 98. Write a Program to Print the Left View of a Binary Tree

### 99. Write a Program to Print the Right View of the Binary Tree

### 100. Write a Program for the Conversion of Infix Expression to Postfix Expression

### How do you handle multilingual text and Unicode in C++?

Handling multilingual text and Unicode in C++ involves several considerations, especially since C++ traditionally relies on ASCII characters for string manipulation. However, with modern libraries and standards like C++11 and beyond, handling Unicode and multilingual text becomes more manageable. Here's how you can handle them:

#### 1. Use `std::wstring` or UTF-8 encoded strings

`std::wstring` can hold wide characters, allowing you to work with Unicode characters directly. However, it's important to note that this is not the most common approach in modern C++, especially for cross-platform compatibility. Instead, you might prefer to work with UTF-8 encoded strings, as UTF-8 is a variable-width encoding and can represent all Unicode characters efficiently.

#### 2. Use UTF-8 aware libraries

There are libraries available that provide Unicode support and simplify text manipulation. Libraries like ICU (International Components for Unicode) are widely used for Unicode handling. ICU provides functions for text handling, Unicode normalization, collation, and much more.

#### 3. Utilize C++ Standard Library

Since C++11, the C++ Standard Library has been improved to better support Unicode. For example:

- `std::wstring_convert` and `std::codecvt` for converting between wide and multibyte character encodings.
- `std::u16string` and `std::u32string` for UTF-16 and UTF-32 encoded strings respectively.
- `std::locale` and `std::locale::global()` for setting the locale, which can influence string handling operations like case conversion and collation.

#### 4. Be mindful of encoding conversions

When working with external APIs or libraries, you may need to convert between different character encodings. Use appropriate conversion functions provided by libraries like ICU or facilities in the C++ Standard Library.

##### Example (using C++ Standard Library)

```cpp
#include <iostream>
#include <string>
#include <codecvt>

int main() {
    // UTF-8 string
    std::string utf8Str = u8"你好，世界！"; // Chinese for "Hello, World!"

    // Convert UTF-8 to wstring
    std::wstring_convert<std::codecvt_utf8<wchar_t>> converter;
    std::wstring wideStr = converter.from_bytes(utf8Str);

    // Output wide string
    std::wcout << wideStr << std::endl;

    return 0;
}
```

#### 5. Input and Output operations

When reading or writing multilingual text to files or the console, ensure that input/output operations are properly configured to handle Unicode characters. For console applications, you may need to set the console's code page to UTF-8.

#### 6. Understand Unicode Normalization

Unicode includes characters that can be represented in multiple ways. Normalization ensures that different representations of the same character are treated equivalently. Libraries like ICU provide functions for Unicode normalization.

By following these guidelines and utilizing appropriate libraries, you can effectively handle multilingual text and Unicode in C++.

### How to clear the screen in C++?

In C++, clearing the screen typically involves using system-specific commands since C++ itself does not provide a standard way to clear the screen. One common approach is to use the `system()` function to execute a system command that clears the screen.

Here's how you can achieve this using system-specific commands:

```cpp
#include <cstdlib> // for system()

int main() {
    // Clearing the screen using system-specific commands
    system("clear"); // for Unix/Linux
    // system("cls"); // for Windows

    // Your program continues here...

    return 0;
}
```

In the above code:

- `system("clear")` will clear the screen on Unix/Linux systems.
- `system("cls")` will clear the screen on Windows systems.

Note: Using `system()` can be platform-dependent and may not always be the preferred solution due to security risks and performance overhead. Alternative methods involving libraries like ncurses or specific system calls can be more robust and efficient, especially for larger projects or cross-platform applications.

### How to compile and run a C program in notepad++?

To compile and run a C program in Notepad++, you typically need to use a compiler like GCC (GNU Compiler Collection) and set up a custom build command. Here's a step-by-step guide:

1. **Install GCC**: If you haven't already, download and install GCC, which is a compiler for C, C++, and other programming languages. You can usually install it by installing a package like MinGW (Minimalist GNU for Windows) on Windows or using package managers like apt on Linux.

2. **Set up Environment Variables (Windows)**: Add the directory containing GCC to your system's PATH environment variable. This allows you to run GCC from any directory in the command prompt. The directory typically looks like `C:\MinGW\bin` on Windows if you installed MinGW.

3. **Write Your C Program**: Open Notepad++ and write your C program.

4. **Save Your File**: Save your C program with a .c extension, for example, `program.c`.

5. **Create a Build Script**: Go to the "Run" menu in Notepad++ and select "Run..." (or press F5). In the dialog box that appears, click on the "Create" button to create a new script.

6. **Enter the Build Command**: In the "Program to Run" field, enter the command to compile your C program using GCC. For example, if you're on Windows, the command might look like this:

   ```bash
   cmd /K gcc "$(FULL_CURRENT_PATH)" -o "$(NAME_PART)" && "$(NAME_PART)"
   ```

   - `$(FULL_CURRENT_PATH)` represents the full path of the current file.
   - `$(NAME_PART)` represents the file name without the extension.

   This command compiles the current file (`$(FULL_CURRENT_PATH)`) using GCC and outputs an executable file with the same name as the source file but without the extension (`$(NAME_PART)`). Then it runs the compiled program.

7. **Save the Script**: Give your script a name, for example, "C Compile & Run", and click "Save".

8. **Run Your Program**: Now, whenever you want to compile and run your C program, go to the "Run" menu and select the script you created (e.g., "C Compile & Run" if you followed the example above), or press F5.

Following these steps, you should be able to compile and run your C program directly from Notepad++ using GCC. Make sure to check the output console in Notepad++ for any compilation errors or program output.

### How to give space in C++?

To give space in C++, utilize the `setw` function provided by the `iomanip` library. Start by including the library with `#include <iomanip>` at the beginning. Next, employ setw along with the preferred width to generate an empty space.

For instance, `cout << setw(10);` will produce a space spanning 10 characters.

### How to save a file in C++?

In C++, you can save a file using the `<fstream>` library, which provides classes for file input/output operations. Here's a basic example of how you can save data to a file:

```cpp
#include <iostream>
#include <fstream>

int main() {
    // Create an output file stream object
    std::ofstream outputFile;

    // Open a file for writing. If the file doesn't exist, it will be created.
    outputFile.open("example.txt");

    // Check if the file opened successfully
    if (!outputFile.is_open()) {
        std::cerr << "Error opening the file!" << std::endl;
        return 1; // Return an error code
    }

    // Write data to the file
    outputFile << "Hello, World!" << std::endl;
    outputFile << "This is a sample text." << std::endl;

    // Close the file
    outputFile.close();

    std::cout << "File saved successfully." << std::endl;

    return 0;
}
```

In this example:

1. We include the necessary headers: `<iostream>` for input/output operations and `<fstream>` for file input/output operations.
2. We declare an `ofstream` object called `outputFile` which is used to write data to a file.
3. We open a file named "example.txt" for writing using the `open()` function of `ofstream`.
4. We check if the file opened successfully. If it failed to open, we print an error message and exit the program.
5. We write data to the file using the `<<` operator, just like writing to `std::cout`.
6. Finally, we close the file using the `close()` function.

Remember to handle errors appropriately, especially when dealing with file operations.

### How to find absolute value in C++?

In C++, you can find the absolute value of a number using the `abs()` function. This function is part of the `<cmath>` header for integer types and `<cstdlib>` header for floating-point types. Here's how you can use it:

```cpp
#include <iostream>
#include <cmath> // for integer types
#include <cstdlib> // for floating-point types

int main() {
    int integerNumber = -5;
    float floatingPointNumber = -3.14;

    // Absolute value of an integer
    int absInteger = std::abs(integerNumber);
    std::cout << "Absolute value of " << integerNumber << " is " << absInteger << std::endl;

    // Absolute value of a floating-point number
    float absFloat = std::abs(floatingPointNumber);
    std::cout << "Absolute value of " << floatingPointNumber << " is " << absFloat << std::endl;

    return 0;
}
```

Output:

```bash
Absolute value of -5 is 5
Absolute value of -3.14 is 3.14
```

Make sure to include the appropriate header (`<cmath>` for integer types and `<cstdlib>` for floating-point types) depending on the type of number you're working with.

### How to use the strcmp function in C++?

In C++, the `strcmp` function is used to compare two strings. It compares two null-terminated character arrays (strings) lexicographically. Below is the basic syntax of `strcmp`:

```cpp
#include <cstring>

int strcmp(const char *str1, const char *str2);
```

Here's how you can use `strcmp`:

```cpp
#include <iostream>
#include <cstring>

int main() {
    const char *str1 = "Hello";
    const char *str2 = "World";

    int result = std::strcmp(str1, str2);

    if (result == 0)
        std::cout << "Strings are equal\n";
    else if (result < 0)
        std::cout << "String 1 is less than String 2\n";
    else
        std::cout << "String 1 is greater than String 2\n";

    return 0;
}
```

In this example:

- If `strcmp` returns 0, it means the strings are equal.
- If `strcmp` returns a negative value, it means the first character that doesn't match has a lower value in `str1` than in `str2`.
- If `strcmp` returns a positive value, it means the first character that doesn't match has a greater value in `str1` than in `str2`.

Remember, `strcmp` compares strings based on their ASCII values character by character until a difference is found or one of the strings ends. Also, ensure that the strings passed to `strcmp` are null-terminated.

### How to write to a file in C++?

In C++, you can write to a file using the `<fstream>` library, which provides classes for file input and output operations. Here's a basic example of how to write to a file in C++:

```cpp
#include <iostream>
#include <fstream>

int main() {
    // Open a file for writing
    std::ofstream outputFile("example.txt");

    // Check if the file was opened successfully
    if (!outputFile.is_open()) {
        std::cerr << "Error opening the file!" << std::endl;
        return 1; // Return an error code
    }

    // Write to the file
    outputFile << "Hello, world!\n";
    outputFile << "This is a line written to the file.";

    // Close the file
    outputFile.close();

    std::cout << "Data has been written to the file." << std::endl;

    return 0; // Return success
}
```

In this example:

- We include `<iostream>` for input/output stream functionality and `<fstream>` for file input/output stream functionality.
- We open a file named "example.txt" for writing using `std::ofstream`.
- We use `is_open()` to check if the file was opened successfully.
- We write data to the file using the stream insertion operator `<<`.
- Finally, we close the file using the `close()` method.

Remember to handle file opening errors and always close the file after writing to it.

### How to input a string in C++ with spaces?

In C++, you can input a string with spaces using the `std::getline()` function from the `<string>` header. Here's a simple example:

```cpp
#include <iostream>
#include <string>

int main() {
    std::string input;

    std::cout << "Enter a string with spaces: ";
    std::getline(std::cin, input);

    std::cout << "You entered: " << input << std::endl;

    return 0;
}
```

In this code:

- We include the necessary headers.
- We declare a string variable called `input`.
- We prompt the user to enter a string with spaces using `std::cout`.
- We use `std::getline()` to read the entire line of input, including spaces, and store it in the `input` variable.
- Finally, we print out the input string.

This way, you can input strings with spaces in C++ without any issues.

### How to generate random numbers in C++ with a range?

In C++, you can generate random numbers within a specific range using the `<random>` library introduced in C++11. Here's a basic example of how to generate random numbers within a specified range:

```cpp
#include <iostream>
#include <random>

int main() {
    // Seed the random number generator
    std::random_device rd;
    std::mt19937 gen(rd());

    // Define the range
    int lower_bound = 1;
    int upper_bound = 100;

    // Create a uniform distribution
    std::uniform_int_distribution<int> distribution(lower_bound, upper_bound);

    // Generate a random number within the defined range
    int random_number = distribution(gen);

    // Output the random number
    std::cout << "Random number: " << random_number << std::endl;

    return 0;
}
```

In this example:

- `std::random_device` is used to seed the random number generator.
- `std::mt19937` is the Mersenne Twister pseudo-random generator engine.
- `std::uniform_int_distribution<int>` creates a distribution of uniformly distributed integers within the specified range.
- `distribution(gen)` generates a random number within the specified range using the generator `gen`.
- You can adjust `lower_bound` and `upper_bound` to define the range of random numbers you want to generate.

Remember to include `<random>` header at the beginning of your C++ file.

### You are tasked with sorting a large array of integers in C++. Which sorting algorithm would you choose and why?

The sorting algorithm selected hinges on the particular needs of the task at hand. When dealing with a sizable array and prioritizing time complexity, Quicksort emerges as an optimal solution. With an average time complexity of O(n log n), it exhibits strong practical performance. Additionally, Quicksort operates in-place, eliminating the need for extra memory beyond the array undergoing sorting.

Here's an example of using `std::sort` from the C++ Standard Library to sort a vector of integers:

```cpp
#include <iostream>
#include <vector>
#include <algorithm> // Include the algorithm library for std::sort
using namespace std;

int main() {
    // Define a vector of integers
    vector<int> vec = {10, 7, 8, 9, 1, 5};

    // Print the original vector
    cout << "Original vector: ";
    for (int num : vec) {
        cout << num << " ";
    }
    cout << endl;

    // Sort the vector using std::sort
    sort(vec.begin(), vec.end());

    // Print the sorted vector
    cout << "Sorted vector: ";
    for (int num : vec) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}
```

This code will sort the vector `{10, 7, 8, 9, 1, 5}` using the `std::sort` algorithm from the C++ Standard Library.

### How to concatenate a string in C++?

In C++, you can concatenate strings in several ways:

1. Using the `+` operator:

   ```cpp
   std::string str1 = "Hello, ";
   std::string str2 = "world!";
   std::string result = str1 + str2;
   ```

2. Using the `append()` member function:

   ```cpp
   std::string str1 = "Hello, ";
   std::string str2 = "world!";
   str1.append(str2);
   ```

3. Using the `+=` operator:

   ```cpp
   std::string str1 = "Hello, ";
   std::string str2 = "world!";
   str1 += str2;
   ```

All of these methods will result in `result` containing "Hello, world!". Remember to include the `<string>` header if you're working with `std::string`.

### How to get absolute value in C++?

In C++, you can get the absolute value of a number using the `abs()` function, which is defined in the `<cmath>` or `<cstdlib>` header. This function works for integer types like `int`, `long`, `long long`, etc. For floating-point types like `float`, `double`, or `long double`, you can use the `fabs()` function from `<cmath>`.

Here's how you can use both of these functions:

```cpp
#include <iostream>
#include <cmath>

int main() {
    int integerNumber = -5;
    double floatingNumber = -7.5;

    // Absolute value of an integer
    int absInteger = abs(integerNumber);
    std::cout << "Absolute value of " << integerNumber << " is: " << absInteger << std::endl;

    // Absolute value of a floating-point number
    double absFloating = fabs(floatingNumber);
    std::cout << "Absolute value of " << floatingNumber << " is: " << absFloating << std::endl;

    return 0;
}
```

Output:

```bash
Absolute value of -5 is: 5
Absolute value of -7.5 is: 7.5
```

Make sure to include the appropriate header (`<cmath>` for `fabs()` and `<cstdlib>` for `abs()`) at the beginning of your code.

### How to set decimal places in C++ ?

In C++, you can control the number of decimal places displayed when outputting floating-point numbers using the `std::setprecision` manipulator from the `<iomanip>` header. Here's how you can use it:

```cpp
#include <iostream>
#include <iomanip>

int main() {
    double number = 3.14159265358979323846;

    // Set precision to 2 decimal places
    std::cout << std::fixed << std::setprecision(2) << number << std::endl;

    // Set precision to 5 decimal places
    std::cout << std::fixed << std::setprecision(5) << number << std::endl;

    return 0;
}
```

In this example, `std::fixed` manipulator is used to display the floating-point numbers in fixed-point notation (i.e., with a fixed number of digits after the decimal point). Then, `std::setprecision` is used to set the number of decimal places to be displayed. Remember to include the `<iomanip>` header to use these manipulators.

### You are working on a C++ program that takes user input and performs certain calculations. You notice that the program crashes when the user enters non-numeric input. How would you handle this situation?

To handle situations where the user enters non-numeric input in a C++ program, you can use input validation techniques to ensure that the input is of the expected type. Here's how you can handle it:

```cpp
#include <iostream>
#include <sstream>

int main() {
    std::string userInput;
    double numericInput;

    std::cout << "Please enter a number: ";
    std::getline(std::cin, userInput);

    // Use stringstream to convert input to a double
    std::stringstream ss(userInput);
    if (ss >> numericInput) {
        // Input was successfully converted to a double
        std::cout << "You entered: " << numericInput << std::endl;
        // Perform calculations or other operations with numericInput
    } else {
        // Input was not a valid number
        std::cerr << "Error: Invalid input. Please enter a valid number." << std::endl;
        // Handle the error, for example, ask the user to re-enter the input or terminate the program
    }

    return 0;
}
```

In this code:

1. We prompt the user to enter a number.
2. We read the user input as a string using `std::getline`.
3. We use a `std::stringstream` to convert the string input to a `double`.
4. We check if the conversion was successful by checking the state of the stringstream using the `>>` operator.
5. If the conversion succeeds, we proceed with the program logic using the converted numeric value. If not, we handle the error, such as printing an error message and possibly asking the user to re-enter the input or terminating the program.

By using this approach, you can gracefully handle situations where the user enters non-numeric input without crashing the program.

### You are working on a C++ project that requires handling dates and time. How would you handle date and time operations in C++?

In C++, you can handle date and time operations using the `<chrono>` library, which provides facilities for performing time-related operations. Here's a basic overview of how you can handle dates and times in C++:

1. **Representing Time**:
   - Use `std::chrono::system_clock` for representing the current system time.
   - Use `std::chrono::steady_clock` for measuring time intervals without being affected by system clock adjustments.
   - Use `std::chrono::high_resolution_clock` for measuring time intervals with the highest possible resolution.

2. **Time Point**:
   - A time point represents a specific point in time.
   - Use `std::chrono::time_point` template class to represent time points.

3. **Duration**:
   - A duration represents a time interval.
   - Use `std::chrono::duration` template class to represent durations.

4. **Manipulating Time**:
   - You can perform arithmetic operations on time points and durations.
   - You can add/subtract durations from time points to get new time points.
   - You can calculate the duration between two time points.

5. **Converting Time Points**:
   - You can convert time points between different clock types.
   - Be cautious when converting between system time and steady time due to potential clock drift.

Here's a simple example demonstrating how to work with time points and durations:

```cpp
#include <iostream>
#include <chrono>

int main() {
    // Get the current system time
    auto now = std::chrono::system_clock::now();

    // Represent a duration of 1 hour
    std::chrono::hours an_hour(1);

    // Add one hour to the current time
    auto one_hour_later = now + an_hour;

    // Calculate the duration between now and one hour later
    auto duration = one_hour_later - now;

    // Convert duration to hours
    auto duration_hours = std::chrono::duration_cast<std::chrono::hours>(duration);

    // Output the result
    std::cout << "Now: " << std::chrono::system_clock::to_time_t(now) << std::endl;
    std::cout << "One hour later: " << std::chrono::system_clock::to_time_t(one_hour_later) << std::endl;
    std::cout << "Duration in hours: " << duration_hours.count() << std::endl;

    return 0;
}
```

This is just a basic example. Depending on your requirements, you may need to use additional features provided by `<chrono>` or third-party libraries for more advanced date and time operations, such as parsing date/time strings, handling time zones, etc.

### You are working on a C++ project and need to read and write binary data to files. How would you accomplish this?

In C++, you can read and write binary data to files using file streams (`std::ifstream` for reading and `std::ofstream` for writing). Here's a basic example of how you can accomplish this:

```cpp
#include <iostream>
#include <fstream>

int main() {
    // Writing binary data to a file
    std::ofstream outfile("data.bin", std::ios::binary | std::ios::out);
    if (!outfile.is_open()) {
        std::cerr << "Failed to open file for writing!\n";
        return 1;
    }

    int data_to_write[] = {10, 20, 30, 40, 50}; // Example data
    outfile.write(reinterpret_cast<const char*>(data_to_write), sizeof(data_to_write));
    outfile.close();

    // Reading binary data from a file
    std::ifstream infile("data.bin", std::ios::binary | std::ios::in);
    if (!infile.is_open()) {
        std::cerr << "Failed to open file for reading!\n";
        return 1;
    }

    int data_read[sizeof(data_to_write) / sizeof(data_to_write[0])];
    infile.read(reinterpret_cast<char*>(data_read), sizeof(data_read));
    infile.close();

    // Displaying the read data
    std::cout << "Data read from file:\n";
    for (int i = 0; i < sizeof(data_read) / sizeof(data_read[0]); ++i) {
        std::cout << data_read[i] << std::endl;
    }

    return 0;
}
```

In this example:

- We first open a file for writing in binary mode (`std::ios::binary | std::ios::out`).
- We then write some sample data to the file using `outfile.write()`.
- After writing, we close the output file stream.
- Next, we open the same file for reading in binary mode (`std::ios::binary | std::ios::in`).
- We read the data from the file using `infile.read()`.
- Finally, we close the input file stream and display the read data.

Make sure to handle errors appropriately, especially when dealing with file I/O operations.

### Write a program to dynamic allocate a 2D Array, assign values to the same, print the values and deallocate the 2D Array

### Write a program in C++ to found out whether a word is palindrome or not?

### Write a Message class in C++ containing apis to get and put messages? Ensure that objects of the Message class are destroyed properly in reverse order of creation

### How do I write my own zero-argument manipulator that should work same as hex?

In C++, you can create your own zero-argument manipulator similar to `hex` by overloading the `<<` operator for `ostream` and defining your manipulator function. Here's how you can do it:

```cpp
#include <iostream>
#include <iomanip>

// Define your manipulator function
std::ostream& hex_custom(std::ostream& os) {
    // Set the stream format to hexadecimal
    os << std::hex << std::uppercase;
    return os;
}

// Define your own manipulator type
std::ostream& hex_custom(std::ostream& os);

// Overload the << operator for your manipulator
std::ostream& operator<<(std::ostream& os, std::ostream& (*manip)(std::ostream&)) {
    return manip(os);
}

int main() {
    int num = 255;
    
    // Use your custom manipulator
    std::cout << hex_custom << "Hexadecimal representation of " << num << " is: " << num << std::endl;
    
    return 0;
}
```

In this example, `hex_custom` is the function that acts as your zero-argument manipulator. It sets the stream format to hexadecimal using `std::hex`. `std::uppercase` ensures that the output uses uppercase letters for hexadecimal digits.

The `operator<<` overload allows you to use your manipulator like any other manipulator with the `<<` operator.

You can use it in your `main()` function or anywhere else in your code by inserting `hex_custom` into the stream as shown in the example.

### Write a program that will convert an integer pointer to an integer and  vice-versa

You can achieve this in C++ by using pointer manipulation. Here's a simple program that demonstrates how to convert an integer to an integer pointer and vice versa:

```cpp
#include <iostream>

int main() {
    int num = 42;
    int* ptr = &num;

    // Convert integer to integer pointer
    int convertedPtr = reinterpret_cast<int>(ptr);
    std::cout << "Integer value: " << num << std::endl;
    std::cout << "Integer pointer value: " << convertedPtr << std::endl;

    // Convert integer pointer to integer
    int* convertedInt = reinterpret_cast<int*>(convertedPtr);
    std::cout << "Converted back to integer pointer: " << *convertedInt << std::endl;

    return 0;
}
```

In this program:

- We have an integer variable `num`.
- We take the address of `num` and store it in an integer pointer `ptr`.
- Using `reinterpret_cast`, we convert `ptr` to an integer `convertedPtr`, effectively converting the pointer address to an integer value.
- Then, we convert `convertedPtr` back to an integer pointer `convertedInt` using another `reinterpret_cast`.
- Finally, we dereference `convertedInt` to retrieve the original value.

Please note that this type of pointer manipulation should be used with caution as it can lead to undefined behavior if not handled properly.

### Write a program that allows to create only one instance of a class?

Certainly! You can achieve this by implementing the Singleton design pattern in C++. Here's an example implementation:

```cpp
#include <iostream>

class Singleton {
private:
    // Private constructor to prevent instantiation from outside
    Singleton() {}

    // Static instance of the class
    static Singleton* instance;

public:
    // Static method to get the instance
    static Singleton* getInstance() {
        // Create the instance if it doesn't exist
        if (!instance) {
            instance = new Singleton();
        }
        return instance;
    }

    // Method to perform some operation
    void someOperation() {
        std::cout << "Singleton instance performing some operation." << std::endl;
    }
};

// Initialize the static instance to null
Singleton* Singleton::instance = nullptr;

int main() {
    // Get the instance of the Singleton
    Singleton* singleton1 = Singleton::getInstance();
    // Call some operation
    singleton1->someOperation();

    // Try to get another instance
    Singleton* singleton2 = Singleton::getInstance();
    // Both instances should be the same
    if (singleton1 == singleton2) {
        std::cout << "Both instances are the same." << std::endl;
    } else {
        std::cout << "Error: Instances are not the same!" << std::endl;
    }

    return 0;
}
```

In this implementation, the `getInstance()` method ensures that only one instance of the `Singleton` class is created and returns the reference to that instance whenever it's called. The constructor is made private so that it cannot be instantiated from outside the class.

### Write a program that implements a date class containing day, month and year as data members. Implement assignment operator and copy constructor in this class

Here's a simple implementation of a Date class in C++ with an assignment operator and a copy constructor:

```cpp
#include <iostream>

class Date {
private:
    int day;
    int month;
    int year;

public:
    // Default constructor
    Date() : day(1), month(1), year(2000) {}

    // Parameterized constructor
    Date(int d, int m, int y) : day(d), month(m), year(y) {}

    // Copy constructor
    Date(const Date& other) {
        day = other.day;
        month = other.month;
        year = other.year;
    }

    // Assignment operator
    Date& operator=(const Date& other) {
        // Check for self-assignment
        if (this != &other) {
            day = other.day;
            month = other.month;
            year = other.year;
        }
        return *this;
    }

    // Getter methods
    int getDay() const { return day; }
    int getMonth() const { return month; }
    int getYear() const { return year; }
};

int main() {
    // Creating objects using different constructors
    Date date1; // Default constructor
    Date date2(31, 12, 2023); // Parameterized constructor

    // Copying using copy constructor
    Date date3 = date1;

    // Copying using assignment operator
    Date date4;
    date4 = date2;

    // Outputting dates
    std::cout << "Date 1: " << date1.getDay() << "/" << date1.getMonth() << "/" << date1.getYear() << std::endl;
    std::cout << "Date 2: " << date2.getDay() << "/" << date2.getMonth() << "/" << date2.getYear() << std::endl;
    std::cout << "Date 3 (copy of Date 1): " << date3.getDay() << "/" << date3.getMonth() << "/" << date3.getYear() << std::endl;
    std::cout << "Date 4 (copy of Date 2): " << date4.getDay() << "/" << date4.getMonth() << "/" << date4.getYear() << std::endl;

    return 0;
}
```

In this program, the `Date` class contains data members `day`, `month`, and `year`. It has a default constructor, a parameterized constructor, a copy constructor, and an assignment operator. The copy constructor and the assignment operator ensure deep copying to avoid issues with shallow copying. Finally, in the `main()` function, various instances of the `Date` class are created and copied using both the copy constructor and the assignment operator.
